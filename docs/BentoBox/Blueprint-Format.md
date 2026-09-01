# ブループリントファイル形式

**仕様バージョン2**

このページは、BentoBoxがアイランドブループリント（`.blueprint`ファイル）とブループリントバンドル（バンドル`.json`ファイル）に使用するディスク上のJSON形式を文書化しています。これは、BentoBoxリポジトリに含まれている機械可読[JSONスキーマ](https://github.com/BentoBoxWorld/BentoBox/tree/develop/schemas)のための、人間が読める同等物です。これはエディターまたはCIでファイルを検証するために使用できます。

*ゲーム内で*ブループリントを作成したい場合は、[ブループリントページ](Blueprints.md)を参照してください。このページは開発者とパワーユーザーが直接ブループリントファイルを生成、編集、または検証する場合を対象としています。

## リビジョン履歴

| バージョン | 日付 | BentoBoxバージョン | 説明 |
|---|---|---|---|
| 1 | 2019-06-09 | [1.5.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/1.5.0) | 初期バージョン、BentoBox Schem形式の導出 |
| 1.1 | 2026 | 2.x | ストレージがZIP圧縮バイナリからプレーンJSONに変更。`.blueprint`がプライマリ拡張子に |
| 2 | 2026-08-14 | 3.22.x | ソースから生成されたフルフィールドレベル仕様。JSONスキーマが発行 |

## ファイル形式

| 拡張子 | 形式 | 状態 |
|---|---|---|
| `.blueprint` | 単一の[ブループリント](#blueprint)オブジェクトを含むプレーンUTF-8 JSON | 現在 |
| `.blu` | 同じJSONの単一エントリを含むZIPアーカイブ | レガシー—ロード可能だが書き込みなし |
| `<uniqueId>.json` | 単一の[ブループリントバンドル](#blueprintbundle)オブジェクトを含むプレーンUTF-8 JSON | 現在 |

両方のファイルはゲームモードアドオンの`blueprints/`フォルダーに住んでいます。例えば、`plugins/BentoBox/addons/BSkyBlock/blueprints/`。バンドルは`name`でブループリントを参照し、参照される`.blueprint`ファイルは同じフォルダーに座る必要があります。

## シリアライゼーションルール

ブループリントはGsonで書き込まれます。これらのルールはすべてに適用され、下記で見るシェイプを説明します：

- このスペシフィケーションに記載されているフィールドのみが出力されます。プロデューサーは他のキーを追加しないでください。
- **ベクトル**（`org.bukkit.util.Vector`）は3要素のJSON配列です：`[x, y, z]`。ブロック位置は慣例的に整数を保有しますが、基礎タイプは二重です。
- **ベクトルでキーされたマップ**はGsonの複雑なマップキーフォームを使用します：JSON*ペアの配列*—`[[<vector>, <value>], ...]`—JSONオブジェクトではなく。これは`blocks`、`attached`、`entities`に適用されます。
- **列挙型でキーされたマップ**（例えば、バンドルの`blueprints`マップ）は、列挙型名をキーとして持つ通常のJSONオブジェクトです。
- **整数でキーされたマップ**（インベントリスロット→アイテム）は、文字列化された整数キー（`"0"`、`"13"`など）を持つJSONオブジェクトです。
- **ItemStacks**はBukkit YAML（`ConfigurationSerializable`経由）にシリアライズされ、JSON*文字列*として保存されます。値を不透明なYAMLドキュメントとして扱います。`YamlConfiguration#loadFromString`で解析可能です。
- **列挙型**はJava`name()`によってシリアライズされます。
- **色**（`org.bukkit.Color`）は`{"ALPHA": int, "RED": int, "GREEN": int, "BLUE": int}`としてシリアライズされます。
- ファイルはライターによってきれいにプリントされます。コンシューマーは空白を頼りにしてはいけません。
- すべてのフィールド名は**大文字小文字を区別**します。

## ブループリント

`.blueprint`ファイルのトップレベルオブジェクト。ブロックボリューム、アタッチされたブロック、アンカー（`bedrock`）に対するエンティティを説明します。

| フィールド | 型 | 説明 |
|---|---|---|
| `name` | string | 一意の識別子。バンドルから検索するために使用されます。慣例的にファイル名の茎に一致します。 |
| `displayName` | string | UI で表示される人間が読める名前。レガシー`§`色コードまたはMiniMessageタグを含むことができます。 |
| `icon` | string | アイコン素材：Bukkit`Material`名（`DIAMOND`）、バニラキー（`minecraft:diamond`）、またはリソースパックカスタムモデルキー。デフォルト`PAPER`。 |
| `description` | string[] | 選択UIのアイコンの下に表示される伝説行。 |
| `bedrock` | Vector | アンカーポイント。貼り付けるとき、ブループリント`(0,0,0)`は、`bedrock`が貼り付けターゲットに到達するように変換されます。省略された場合、BentoBoxは自動的に`(xSize/2, ySize/2, zSize/2)`でロード時に作成します。 |
| `xSize`, `ySize`, `zSize` | integer | ブロック単位でのバウンディングボックスの寸法。 |
| `sink` | boolean | Trueの場合、ブループリントはアンカーの正確なYで貼り付けるのではなく、貼り付け時に表面を見つけるまで下降します。 |
| `blocks` | Vector-keyed map | プライマリブロック。ブループリント原点に対する位置によってキー（各軸で0..size-1）。[BlueprintBlock](#blueprintblock)を参照。 |
| `attached` | Vector-keyed map | `blocks`の**後に**貼り付けされたブロック。なぜなら彼らはサポートに接着します：たいまつ、はしご、レール、ベッド、ドア、サイン、など。`blocks`と同じ座標慣例。 |
| `entities` | Vector-keyed map of lists | ブロック位置あたりのスポーンするエンティティ。複数のエンティティは1つのキーを共有することができます。微調整されたブロック内オフセットは[BlueprintEntity](#blueprintentity)に住んでいます。 |

最小限の例：

```json
{
  "name": "island",
  "displayName": "&aStarter island",
  "icon": "GRASS_BLOCK",
  "description": ["A tiny island"],
  "bedrock": [2.0, 1.0, 2.0],
  "xSize": 5, "ySize": 3, "zSize": 5,
  "blocks": [
    [[2.0, 1.0, 2.0], {"blockData": "minecraft:bedrock"}],
    [[2.0, 2.0, 2.0], {"blockData": "minecraft:grass_block[snowy=false]"}]
  ],
  "attached": [
    [[2.0, 3.0, 2.0], {"blockData": "minecraft:oak_sign[rotation=0,waterlogged=false]", "signLines": ["[spawn_here]", "", "", ""]}]
  ],
  "entities": [
    [[1.0, 2.0, 1.0], [{"type": "COW", "adult": true}]]
  ]
}
```

## ブループリントブロック

1つのブロックセル。`blockData`のみが必須です。他のすべてのフィールドはブロック型がサポートしている場合のみ適用されます。

| フィールド | 型 | 説明 |
|---|---|---|
| `blockData` | string | **必須。** Bukkit `BlockData`文字列、つまり`BlockData#getAsString()`の出力—例えば、`minecraft:chest[facing=north,type=single,waterlogged=false]`。 |
| `signLines` | string[] (≤4) | 前面サインライン。レガシー`§`色コードサポート。1.24.0以降、サイド固有のフィールド有利に非推奨ですが、まだ書き込みと読み取り。 |
| `signLines2` | string[] (≤4) | 背面サインライン（デュアルサイドサイン、1.24.0で追加）。 |
| `glowingText` | boolean | サインの前面に光るテキストがあります。 |
| `glowingText2` | boolean | サインの背面に光るテキストがあります。 |
| `inventory` | slot map | コンテナコンテンツ（チェスト、バレル、ホッパー、シュルカー、炉、醸造スタンドなど）。キーは文字列化されたスロット指数です。値はYAML符号化されたItemStackです。 |
| `bannerPatterns` | object[] | 順序で適用されたバナーパターンレイヤー。各エントリは`pattern`（レガシー短コード、例えば`bri`）と`color`（`DyeColor`名）を持ちます。 |
| `biome` | string | このブロックセルのバイオムオーバーライド（Bukkit`Biome`名）。 |
| `creatureSpawner` | object | `blockData`がスポーナーの場合のみ存在。[ブループリントクリーチャースポーナー](#blueprintcreaturespawner)を参照。 |
| `trialSpawner` | object | `blockData`がトライアルスポーナーの場合のみ存在（1.21+、BentoBox 3.4.2で追加）。`creatureSpawner`と相互排他的。[ブループリントトライアルスポーナー](#blueprinttrialspawner)を参照。 |
| `itemsAdderBlock` | string | ItemsAdderカスタムブロックID（例えば`myserver:custom_ore`）。ItemsAdderがインストールされている場合のみ意味があります。それ以外、ブロックは`blockData`にフォールバック。 |

### ブループリントクリーチャースポーナー

バニラ（非トライアル）モブスポーナー設定。

| フィールド | 型 | 説明 |
|---|---|---|
| `spawnedType` | string | Bukkit `EntityType`名。 |
| `delay` | integer | 次のスポーン試行までの現在のカウントダウン（ティック）。 |
| `maxNearbyEntities` | integer | スポーニングは、スポーンされた型の少なくともこの多くがトラッキング範囲内にある場合は一時停止します。 |
| `minSpawnDelay`, `maxSpawnDelay` | integer | ランダム化された遅延の境界（ティック）は、各スポーン後に選択されます。 |
| `requiredPlayerRange` | integer | スポーナーをアクティブに保つ最大プレイヤー距離（ブロック）。 |
| `spawnRange` | integer | モブがスポーンできる半径（ブロック）。 |

### ブループリントトライアルスポーナー

トライアルスポーナー設定（Minecraft 1.21+）。`spawnedType`**または**`potentialSpawns`を使用しますが、両方ではありません。

| フィールド | 型 | 説明 |
|---|---|---|
| `ominous` | boolean | スポーナーが不穏な（呪いの）状態にあるかどうか。 |
| `spawnedType` | string | 単一`EntityType`がスポーン。 |
| `potentialSpawns` | object[] | 重み付けされたスポーン候補。各エントリ：`snapshot`（不透明な`EntitySnapshot#getAsString`値）、`spawnrule`（Bukkit`SpawnRule`オブジェクト。キーはサーバーバージョンによって異なります）、および必須`spawnWeight`（integer ≥ 1）。 |
| `delay` | integer | スポーン遅延。 |
| `baseSimEnts` / `addSimulEnts` | number | ベース同時エンティティが生きていた/追加されたプレイヤーあたり。 |
| `baseSpawnsB4Cool` / `addSpawnsB4Cool` | number | ベース総スポーン前クールダウン/追加プレイヤーあたり。 |
| `spawnRange`, `requiredPlayerRange`, `playerRange` | integer | ブロック単位での範囲。 |
| `lootTableMap` | array of pairs | 候補報酬略奪テーブル相対的な重み：`[[{"nameSpace": "minecraft", "key": "chests/trial_chambers/reward"}, 1], ...]`。 |

## ブループリントエンティティ

スポーンするエンティティ。`type`のみが必須です。未設定フィールドは「Bukkit既定のままにする」を意味します。各フィールドはエンティティクラスがサポートしている場合のみ適用されます。

**一般**

| フィールド | 型 | 説明 |
|---|---|---|
| `type` | string | **必須。** Bukkit `EntityType`名（`VILLAGER`、`ARMOR_STAND`、`ITEM_FRAME`など）。 |
| `customName` | string | 表示名。レガシー`§`色コードサポート。 |
| `x`, `y`, `z` | number | 位置セル内での微調整オフセット（通常`0.0 ≤ v < 1.0`）。 |
| `glowing` | boolean | グロー効果。 |
| `gravity` | boolean | 重力が適用されるかどうか。 |
| `visualFire` | boolean | `fireTicks`に関係なく火を描画。 |
| `silent` | boolean | 周囲の音を抑制。 |
| `invulnerable` | boolean | すべての損害に免疫。 |
| `fireTicks` | integer | 残っている火の期間（ティック）。 |

**モブ**

| フィールド | 型 | 説明 |
|---|---|---|
| `adult` | boolean | 年齢を重ねるエンティティ—`false`はベビーをスポーン。 |
| `color` | string | `DyeColor`名。色付け可能なエンティティ用（羊、シュルカー、オオカミの首輪など）。 |
| `tamed` | boolean | 馴家可能なエンティティ。所有者は復元されません。 |
| `chest` | boolean | チェスト運搬馬/ラマ。 |
| `domestication` | integer (0–100) | 馬の家畜化レベル。 |
| `inventory` | slot map | 馬/ラマインベントリ。 |
| `style` | string | 馬のコートスタイル：`WHITE`、`WHITEFIELD`、`WHITE_DOTS`、`BLACK_DOTS`、`NONE`。 |
| `profession` | string |村人の職業（列挙型名またはネームスペースキー）。 |
| `level` | integer (1–5) | 村人レベル。 |
| `experience` | integer | 村人経験。 |
| `villagerType` | string | 村人バイオームバリアント（列挙型名またはネームスペースキー）。 |

**プラグインインテグレーション**（プラグインがインストールされている場合のみ意味がある）

| フィールド | 型 | 説明 |
|---|---|---|
| `npc` | string | Citizens NPC ID。 |
| `MMtype`, `MMLevel`, `MMpower`, `MMStance` | string / number | MythicMobsタイプ、レベル、パワー、スタンス。 |

**ディスプレイエンティティとアイテムフレーム**

| フィールド | 型 | 説明 |
|---|---|---|
| `displayRec` | object | すべてのディスプレイエンティティに共通の特性—[DisplayRec](#displayrec)を参照。 |
| `blockDisp` | object | ブロックディスプレイペイロード：[BlueprintBlock](#blueprintblock)として表示されたブロック。 |
| `itemDisp` | object | アイテムディスプレイペイロード：`item`（YAML符号化ItemStack）と`itemDispTrans`（`ItemDisplayTransform`名：`NONE`、`HEAD`、`GUI`、`GROUND`、`FIXED`、`THIRDPERSON_LEFTHAND`など）。 |
| `textDisp` | object | テキストディスプレイペイロード—下記を参照。 |
| `itemFrame` | object | アイテムフレームペイロード（3.2.6以降）：`item`（YAML符号化ItemStack）、`rotation`（Bukkit`Rotation`名）、`isFixed`、`isVisible`、`dropChance`（0.0–1.0）。 |

TextDisplayペイロードフィールド：`text`（レガシー`§`コード許可）、`alignment`（`CENTER`/`LEFT`/`RIGHT`）、`bgColor`（カラーオブジェクト）、`face`（`BlockFace`名）、`lWidth`（ラップライン幅、ピクセル）、`opacity`（署名バイト、−1 = デフォルト）、`isShadowed`、`isSeeThrough`、`isDefaultBg`。

### DisplayRec

| フィールド | 型 | 説明 |
|---|---|---|
| `billboard` | string | `FIXED`、`VERTICAL`、`HORIZONTAL`、または`CENTER`—ディスプレイがビューアーに面する方法。 |
| `brightness` | object | Bukkit`Display.Brightness`。通常`{"block": int, "sky": int}`。 |
| `width`, `height` | number | ディスプレイサイズ。 |
| `glowColorOverride` | Color | グロー輪郭色。 |
| `interpolationDelay`, `interpolationDuration`, `teleportDuration` | integer | アニメーションのタイミング。 |
| `shadowRadius`, `shadowStrength` | number | 影のレンダリング。 |
| `transformation` | object | Bukkit`Transformation`（変換、回転、スケール）。不透明。 |
| `range` | number | 表示範囲。 |

## ブループリントバンドル

バンドルは最大3つのブループリント—各ワールド環境1つ—をアイランド作成UIの単一オプションにグループ化し、そのオプションの費用、権限、GUIスロット、使用上限、作成後コマンドを制御します。ゲームモードの`blueprints/`フォルダーに`<uniqueId>.json`として永続化。ファイル名の茎は`uniqueId`**と等しい**である必要があります。

| フィールド | 型 | 説明 |
|---|---|---|
| `uniqueId` | string | **必須。** 一意ID。`requirePermission`がtrueの場合、パーミッション接尾辞。 |
| `displayName` | string | 選択GUIで表示される名前。 |
| `icon` | string | アイコン素材。ブループリントアイコンと同じ形式。デフォルト`PAPER`。 |
| `description` | string[] | アイコンの下にある伝説行。 |
| `blueprints` | object | 環境（`NORMAL`、`NETHER`、`THE_END`、`CUSTOM`）から同じフォルダー内のブループリントの`name`へのマップ。エントリのない環境は生成されません。 |
| `requirePermission` | boolean | Trueの場合、プレイヤーは`<gamemode>.island.create.<uniqueId>`が必要です。 |
| `slot` | integer | 推奨0ベースのGUIスロット。実行時に固定。 |
| `times` | integer | 単一プレイヤーがこのバンドルで作成できる最大アイランド。`0` = 無制限。 |
| `cost` | number | Vault経済費用。`0` = 無料。エコノミープラグインが必須。 |
| `commands` | string[] | このバンドルでアイランドが作成されたときに実行されるコマンド（2.6.0で追加）。`[player]`と`[owner]`が置換されます。`[SUDO]`付きプレフィックスエントリはプレイヤーとして実行、その他はコンソールとして。 |

例`default.json`：

```json
{
  "uniqueId": "default",
  "displayName": "Default Island",
  "icon": "GRASS_BLOCK",
  "description": ["A standard island", "with grass and dirt"],
  "blueprints": {
    "NORMAL": "island",
    "NETHER": "nether",
    "THE_END": "end"
  },
  "requirePermission": false,
  "slot": 0,
  "times": 0,
  "cost": 0.0,
  "commands": ["[SUDO] me has arrived!"]
}
```

## ファイルの検証

BentoBoxリポジトリは2つのJSONスキーマ（ドラフト2020-12）を発行：

- [`schemas/blueprint.schema.json`](https://github.com/BentoBoxWorld/BentoBox/blob/develop/schemas/blueprint.schema.json) — `.blueprint`ファイルまたはバンドルを検証
- [`schemas/blueprint-bundle.schema.json`](https://github.com/BentoBoxWorld/BentoBox/blob/develop/schemas/blueprint-bundle.schema.json) — バンドルファイルを単独で検証

例えば、[ajv](https://ajv.js.org/)で、エディターまたはCIバリデーターでポイント：

```bash
ajv validate --spec=draft2020 -s blueprint.schema.json -d island.blueprint
```

YAML符号化ItemStack文字列と少数のBukkit`ConfigurationSerializable`オブジェクト（変換、スポーンルール）は、スキーマに対して不透明です—スキーマ有効ファイルはまだ、これらの埋め込みドキュメントが不正形式の場合、ロードに失敗できます。
