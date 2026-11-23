# AOneBlockフェーズのカスタマイズ

プレイヤーがマジックブロックから採掘するすべてのものは、**フェーズファイル**から取得されます。このページでは、これらのファイルの仕組み、その中のすべての数字が何を意味するのか、そして独自のフェーズを構築する方法について説明します。

!!! tip "簡潔な説明"
    マテリアルまたはエンティティの後の数字（`COBBLESTONE: 900`）は、**重み**です。カウント数ではなく、パーセンテージでもありません。フェーズはすべての重みを加算し、その重みに比例して1つのエントリをランダムに選択します。`blocks:`、`mobs:`、`custom-blocks:`はすべて同じ1つのプールから抽出されます。

## ファイルの保存場所

アドオンが1度実行されると、ファイルは以下の場所に保存されます：

```
plugins/BentoBox/addons/AOneBlock/
├── config.yml
├── phases_index.yml          ← どのフェーズをどの順序で読み込むか、各フェーズの長さ
└── phases/
    ├── 0_plains.yml          ← フェーズのブロック、モブ、ホログラム、設定
    ├── 0_plains_chests.yml   ← そのフェーズのルートテーブル
    ├── 700_underground.yml
    ├── 700_underground_chests.yml
    └── ...
```

すべてのフェーズは2つのファイルで構成されます：`<name>.yml`と`<name>_chests.yml`。チェストファイルはファイル名で対応付けられるため、1つの名前を変更する場合は、もう1つの名前も変更する必要があります。

!!! info "`0_plains.yml`は参照ファイルです"
    同梱されている`0_plains.yml`には、すべてのオプションについた詳細なコメントが付いています。1つのファイルだけ読むなら、それを読んでください。このページでは、同じ内容を実践例付きで説明しています。

任意のファイルを編集した後、アドオンをリロードするか（`/bbox reload`）、またはサーバーを再起動してください。

---

## 3つの種類の数字

ここが混乱しやすいポイントです。フェーズファイルには3つのまったく異なる種類の数字が含まれており、どれかは**そのセクション**に完全に依存します。

| 場所 | 数字が示すもの |
|---|---|
| `blocks:`、`mobs:`、`custom-blocks:` | **重み** — このエントリのランダムプール内のシェア。 |
| `fixedBlocks`と`holograms`内のキー | **位置** — このフェーズ内で0から数えたブロック数。 |
| ファイルのトップレベルキー（`'0':`、`'2500':`） | フェーズの**セクション名**。歴史的には開始ブロック数。フェーズの順序と長さは現在`phases_index.yml`から取得されます。 |

---

## 重み — `blocks:`セクションと`mobs:`セクション

### ロール方法

プレイヤーがマジックブロックを破壊するたびに、AOneBlockは：

1. 現在のフェーズの**すべて**の重みを加算します — `blocks:`、`mobs:`、`custom-blocks:`のすべてです。
2. その範囲内のランダムな数字を選んで、その数字が属するエントリを返します。

したがって：

```
エントリの確率 = エントリの重み ÷ フェーズ内のすべての重みの合計
```

重みは数量ではありません。`STONE: 1000`は、そのフェーズ中に1000個の石が生成されるという意味ではなく、石がラッフルで1000枚のチケットを得て、すべてのブロック破壊で新たにロールされるということです。

### 実践例

```yaml
'2500':
  name: Winter
  firstBlock: SNOW_BLOCK
  biome: SNOWY_TAIGA
  blocks:
    COBBLESTONE: 900
    SAND: 100
    DIRT: 200
    STONE: 1000
    SPRUCE_LEAVES: 500
```

重みの合計は`900 + 100 + 200 + 1000 + 500 = 2700`なので、以下のようになります：

| ブロック | 重み | 1回の破壊あたりの確率 |
|---|---:|---:|
| `STONE` | 1000 | 1000 / 2700 = **37.0%** |
| `COBBLESTONE` | 900 | 900 / 2700 = **33.3%** |
| `SPRUCE_LEAVES` | 500 | 500 / 2700 = **18.5%** |
| `DIRT` | 200 | 200 / 2700 = **7.4%** |
| `SAND` | 100 | 100 / 2700 = **3.7%** |

1000ブロックのフェーズ中、石は約370個出現することが予想されますが、すべての破壊は独立したロールなので、実数値はその数字周辺で変動します。

### 比率だけが重要

```yaml
blocks:
  STONE: 1000
  DIRT: 200
```

は、以下と**まったく同じ**に動作します

```yaml
blocks:
  STONE: 10
  DIRT: 2
```

同梱ファイルは意図的に大きな数字を使用しています：合計が数千であれば、レアエントリを重み`5`で追加できるので、その他すべてを再スケールしてパーセンテージを合理的に保つ必要はありません。

### ブロックとモブは1つのプール

!!! warning "モブの重みはブロックの重みと同じ合計にカウント"
    `mobs:`は独立したロールではありません。モブエントリは同じラッフル内のもう1枚のチケットに過ぎないため、`CHICKEN: 200`は重み200のブロックとまったく同じ可能性があります — そしてモブを追加するとすべてのブロックがわずかにレアになります。

同梱されているPlains（平原）フェーズがこれを具体的に示しています。その`blocks:`の重みの合計は11450で、`mobs:`の重みの合計は665で、フェーズ全体は**12115**です：

| エントリ | 重み | 1回の破壊あたりの確率 |
|---|---:|---:|
| `GRASS_BLOCK` | 2000 | 16.5% |
| `OAK_LOG` | 2000 | 16.5% |
| `CHEST` | 200 | 1.7% |
| `CHICKEN` *(モブ)* | 200 | 1.7% |
| `COW` *(モブ)* | 150 | 1.2% |
| `DIAMOND_ORE` | 30 | 0.25% |
| `VILLAGER` *(モブ)* | 15 | 0.12% |
| `EMERALD_ORE` | 10 | 0.08% |

### チューニングレシピ

| 実現したいこと | これを行う |
|---|---|
| 何かを2倍一般的にする | その重みを2倍にする |
| 何かを削除する | その行を削除します（またはコメント化） |
| 約*X*%の確率でブロックを追加する | 重み ≈ `X/100 × 現在の合計 ÷ (1 − X/100)` — または現在の合計を取り、~1%なら重み ≈ 合計/100のエントリを追加 |
| フェーズ全体を再バランスする | 1度に1つの重みを変更します — すべての変更が他のパーセンテージをシフトさせます。合計が移動するためです。 |
| モブをレアにしてブロックに触れない | `mobs:`の重みを下げます。ブロックのパーセンテージは自動的に上昇します。 |

### ルールと落とし穴

- 重みは**1以上の整数**である必要があります。`0`、負の値、または小数は拒否され、`Bad item weight for <phase>: <material>`としてログに記録されます。
- マテリアルは、**ブロック**である実際のBukkit [Material](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)である必要があります。`DIAMOND`のようなアイテムは`Bad block material`としてログに記録されます。
- モブは、ライブでスポーン可能な[EntityType](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/EntityType.html)である必要があります。無効な名前は、起動時に有効な名前の完全なリストをログに記録します。
- フェーズに有効な重みがまったくない場合、`has zero probability of generating blocks`としてログに記録され、単一のブロックタイプにフォールバックします — セクション名のスペルをご確認ください。

### `CHEST`は特殊なケース

`CHEST`がプールからロールされると、AOneBlockはそのフェーズの`_chests.yml`ファイルから埋めます。つまり`CHEST`の重みは**1つ**のチェストを得る確率です。どのチェストを得るかは、レアリティ上の**2番目の独立したロール**です：

| レアリティ | 確率 |
|---|---:|
| `COMMON` | 62% |
| `UNCOMMON` | 25% |
| `RARE` | 9% |
| `EPIC` | 4% |

これらのレアリティ確率はコード内で固定され、設定変更できません。フェーズに定義されたレアリティがない場合、`COMMON`リストが代わりに使用されます。チェストがまったくない場合、空のチェストが配置されます。

### モブ

モブがロールされると、マジックブロックが空だった場合は`STONE`になり、モブがその上にスポーンします。`config.yml`で`clear-blocks: true`の場合、大きなモブが適合するようにブロックがクリアされます。

```yaml
mobs:
  COW: 150
  SPIDER: 75
  SHEEP: 75
  PIG: 150
  VILLAGER: 15
  CHICKEN: 200
```

---

## 位置 — `fixedBlocks`と`holograms`

これらの2つのセクションのキーは、**フェーズ内の位置**です。0から数えます。位置`0`はフェーズの最初のブロック、`1`は2番目、というように続きます。これらはプレイヤーの全体的なブロックカウントではなく、フェーズの長さより大きい位置は到達しません。

### `fixedBlocks`

固定ブロックは保証されており、加重プールをまったくバイパスします。スクリプト化された瞬間に使用します。

```yaml
fixedBlocks:
  0: GRASS_BLOCK
  1: GRASS_BLOCK
  2: GRASS_BLOCK
  3: OAK_LOG
  4: OAK_LOG
  5: OAK_LOG
  700: CHEST_WITH_WATER_BUCKET
```

- ここで位置`0`を定義すると、`firstBlock`が置き換わり、その後は不要になります。
- `CHEST_WITH_<ITEM>`は、その素材の1つのアイテムを保持するチェストを配置するショートハンドです — Ocean（海）フェーズ前にプレイヤーに水バケツを提供するのに便利です。
- サポートが不要なブロックを選択してください。火種、レール、苗木などをマジックブロックとして配置するとポップオフします。
- 固定ブロックエントリは、[カスタムブロック](#カスタムブロック)の定義にすることもできます。

### `holograms`

同じ番号付けですが、値はマジックブロック上に浮かぶテキストです。`&`カラーコードが機能します。

```yaml
holograms:
  0: "&aFirst block is grass!"
  1: "&aSecond block is grass!"
  3: "&aGood Luck!"
```

最初のホログラム — フェーズ1開始前に表示されるもの — は、ここではなくアドオンのロケールファイルに保存されます。

---

## フェーズの順序と長さ — `phases_index.yml`

!!! new "AOneBlock 1.26.0 以降"
    フェーズの順序と長さは、ファイル名またはトップレベルキーから取得され**ません**。`phases_index.yml`が情報源です。

```yaml
phases:
  - file: 0_plains
    section: '0'
    name: Plains
    length: 700
  - file: 700_underground
    section: '700'
    name: Underground
    length: 1300
gotoAtEnd: 0
```

| フィールド | 意味 |
|---|---|
| `file` | `.yml`なしのフェーズファイルのベース名。チェストファイルは`<file>_chests.yml`です。 |
| `section` | そのフェーズファイル内のトップレベルキー。 |
| `name` | 表示名。ログと`/[admin_command] phases`で使用されます。 |
| `length` | このフェーズが続くブロック数。 |
| `enabled` | オプション。デフォルトは`true`。`false`に設定するとそのフェーズを完全に除外します。 |
| `requiredMinecraftVersion` | オプション。フェーズはより古いサーバーではスキップされ、ブロック数をまったく消費しません。 |

開始ブロックは**計算されます**：各フェーズは、0から始まる上記の有効なフェーズの長さの実行合計で開始します。フェーズを自由に並べ替えます。無効またはスキップされたフェーズは進行から消えます。最後のフェーズの後、ブロックカウントは`gotoAtEnd`にジャンプします。

このすべてを変更する最も簡単な方法は、ゲーム内で`/[admin_command] phases`を使用することです。これはインデックスを編集します。ここで長さを編集すると、`adminLengths: true`がインデックスに書き込まれ、そのファイル内のアップグレードをまたいでも長さは再計算されません。

!!! tip "ファイル名の数字はヒントに過ぎません"
    `0_plains`、`2500_winter`などは歴史的なものです。カスタムフェーズは`my_phase.yml`で`my_phase:`トップレベルキーを持ち、どこにも数字がないことができます。数字はまだ新しいファイルに便利です — インデックス整合処理にそのフェーズが実行順序のどこに属するかを伝えます。

---

## フェーズファイルの構造

```yaml
'0':                          # セクション名 (phases_index.ymlを参照)
  name: Plains                # 表示名
  icon: GRASS_BLOCK           # phases GUIのアイコン (BentoBox ItemParser)
  firstBlock: GRASS_BLOCK     # 位置0のブロック (オプション)
  biome: PLAINS               # マジックブロック場所のバイオーム
  requiredMinecraftVersion: '1.21.6'   # オプションのバージョンゲート

  fixedBlocks: { ... }        # 位置での保証ブロック
  holograms: { ... }          # 位置でのテキスト

  blocks: { ... }             # ブロックの加重プール
  mobs: { ... }               # モブの加重プール — 同じプール
  custom-blocks: [ ... ]      # カスタムエントリの加重プール — 同じプール

  start-commands: [ ... ]
  end-commands: [ ... ]
  end-commands-first-time: [ ... ]
  requirements: { ... }
  finale: { ... }             # フェーズを終わらせるボス（オプション、1.29.0+）
```

=== "name"
    表示名。phases GUI、ボスバー、ログ行、`[phase]`コマンドプレースホルダーで表示されます。

=== "icon"
    phases GUIでのみ使用されるアイコン。[BentoBox ItemParser](../../BentoBox/ItemParser.md)で解析されるため、カスタムプレイヤーヘッドと任意の表示可能なアイテムが機能します。アイコンのないフェーズは最初のブロックにフォールバックします。

=== "firstBlock"
    フェーズの位置0に配置されるブロック。オプション — `fixedBlocks`の下で`0:`を定義すると同じ仕事をし、優先されます。

=== "biome"
    **マジックブロック位置のみ**のバイオームを変更します。島全体のバイオーム変更ではありません。フェーズ変更時に島全体をバイオーム化するには、`start-commands`エントリからBiomesアドオンを呼び出します。無効なバイオーム名は起動時に有効なバイオーム名の完全なリストをログに記録します。

=== "requirements"
    フェーズへの進入をゲートします。すべての要件が満たされるまで、プレイヤーは前のフェーズの終了時に保たれます。

    - `economy-balance` — 最小プレイヤー残高 (VaultとエコノミープラグインのインストールをBentoBox：필요)
    - `bank-balance` — 最小島銀行残高 (Bankアドオンが必要)
    - `level` — 最小島レベル (Levelアドオンが必要)
    - `permission` — プレイヤーが持つ必要があるパーミッション文字列
    - `cooldown` — フェーズが最後に開始してから経過する秒数

    ```yaml
    requirements:
      bank-balance: 10000
      level: 10
      permission: ready.for.battle
      cooldown: 60
    ```

---

## フェーズ変更時のコマンド { #commands-on-phase-change }

コマンドは**コンソール**として実行されます。ただし、`[SUDO]`というプレフィックスが付いている場合は、トリガーされたプレイヤーとして実行されます。

| セクション | 実行時期 |
|---|---|
| `start-commands` | フェーズが開始するとき |
| `end-commands` | フェーズが完了するたびに |
| `end-commands-first-time` | このアイランドが**最初に**このフェーズを完了したときのみ |

コマンド文字列に置き換えられるプレースホルダー：

| プレースホルダー | 値 |
|---|---|
| `[island]` | アイランド名 |
| `[owner]` | アイランドオーナーの名前 |
| `[player]` | ブロックを破壊したプレイヤーの名前 |
| `[phase]` | このフェーズの名前 |
| `[blocks]` | 破壊されたブロックの数 |
| `[level]` | アイランドレベル (Levelアドオンが必要) |
| `[bank-balance]` | アイランド銀行残高 (Bankアドオンが必要) |
| `[eco-balance]` | プレイヤーのエコノミー残高 (VaultとエコノミープラグインのインストールをBentoBox:必要) |

```yaml
start-commands:
- 'give [player] WOODEN_AXE 1'
- 'broadcast [player] just started OneBlock!'
end-commands-first-time:
- 'broadcast &c&l[!] &b[player] &fhas completed the &d&n[phase]&f phase for the first time.'
```

---

## フェーズフィナーレ — フェーズを終わらせるボス { #phase-finales-the-boss-that-ends-a-phase }

*AOneBlock 1.29.0 で追加されました。*

`finale:` セクションのあるフェーズは、ボス戦で終わります。フェーズの最後のブロックを掘ると、魔法ブロックが封印され、その上にボスが出現します。ボスを倒すまでフェーズは変わりません。`finale:` セクションのないフェーズは、これまでどおりに終わります。

```yaml
  finale:
    boss: GIANT
    name: '<dark_green>The Colossus'
    health: 100
    scale: 0.5
    damage: 4
    speed: 0.25
    minions:
      ZOMBIE: 2
    drops:
      IRON_INGOT: 8
      BREAD: 8
```

### 戦いの流れ

- **予兆。** フェーズの最後の20ブロックの間、心臓の鼓動音が鳴り、音程が上がっていきます。残り5ブロックで鐘が鳴ります。ボスが待ち構えると、フェーズバーにボスの名前が表示されます。
- **戦闘。** ボスは襲撃の角笛と稲妻とともに魔法ブロックの上に出現します。ボスを倒すまで魔法ブロックは掘れず、フェーズバーはボスの体力バーに置き換わります。
- **アイランドを守る仕組み。** ボスにダメージを与えられるのはプレイヤーだけです（近接攻撃、飛び道具、ペット）。ボスとその手下はブロックを壊したり、燃やしたり、爆破したりできません。ボスがアイランドの外に出ると引き戻されます。
- **落下。** プレイヤーは突き落とされることがあります。奈落に落とされたボスは、`void-respawn` が `false` でない限り魔法ブロックに戻ってきます。
- **敗北。** 全員が死ぬか立ち去ると、ボスは約10秒後に退却します。魔法ブロックを叩くと再び呼び出せます。戦いに負けるたびに次の挑戦が10%やさしくなり、体力は最小で半分まで下がります。
- **チーム。** アイランドにいるプレイヤーが1人増えるごとにボスの体力が50%増えます（4人まで）。
- **報酬。** ボスは `drops` を落とします。その後、勝つたびに `commands` が実行され、そのアイランドが初めて倒したときだけ `first-time-commands` が実行されます。

難易度がピースフルの場合、ボスが出現できないためフィナーレはスキップされます。

### オプション

| オプション | 内容 | デフォルト |
|---|---|---|
| `boss` | ボスの `EntityType`。`GIANT` はバニラでは AI を持ちませんが、AOneBlock が AI を与えます（Paper が必要）。`mythic-boss` を使う場合は、オプションの代替になります | 必須（`mythic-boss` を設定した場合を除く） |
| `mythic-boss` | 代わりにボスとして使う [MythicMobs](#mythicmobs-bosses-and-minions) のモブタイプ（1.30.0+） | なし |
| `mythic-level` | MythicMobs のボスと `mythic-minions` のレベル（1.30.0+） | `1` |
| `name` | 表示名。MiniMessage またはレガシーの `&` コード。`mythic-boss` にも設定してください。設定しないとボスバーにタイプ ID が表示されます | モブの名前 |
| `health` | 基本の最大体力。`0` にするとモブ本来の体力のままになります（1.30.0+）。`spigot.yml` の `settings.attribute.maxHealth` を上げない限り、サーバーの上限は 1024 です | `100`（`mythic-boss` の場合は `0`） |
| `scale` | 大きさの倍率。`1` が通常サイズ | `1`（`mythic-boss` の場合はモブ本来の大きさ） |
| `damage` | 攻撃ダメージ。省略するか `0` にするとモブ本来の値 | モブ本来の値 |
| `speed` | 移動速度。省略するか `0` にするとモブ本来の値 | モブ本来の値 |
| `void-respawn` | `true`：奈落に落とされたボスが魔法ブロックに戻ります。`false`：奈落でボスが死に、勝利として扱われます | `true` |
| `warning` | フェーズ終了の何ブロック前から予兆を始めるか。`0` で予兆なし | `20` |
| `minions` | ボスと一緒に出現するモブ。`TYPE: count` の形式 | なし |
| `mythic-minions` | ボスと一緒に出現する MythicMobs のモブ。`type: count` の形式。`mythic-level` が使われます（1.30.0+） | なし |
| `drops` | ボスが死んだときに落とすアイテム。`MATERIAL: amount` の形式 | なし |
| `commands` | ボスを倒すたびに実行されるコマンド。プレフィックスとプレースホルダーは [`end-commands`](#commands-on-phase-change) と同じです | なし |
| `first-time-commands` | そのアイランドが初めてボスを倒したときだけ実行されるコマンド | なし |

同梱の [`0_plains.yml`](https://github.com/BentoBoxWorld/AOneBlock/blob/master/src/main/resources/phases/0_plains.yml) には、すべてのオプションの説明がコメントとして書かれています。サーバー上のコピーは作成時のコメントのままなので、後のバージョンで追加されたオプションは同梱のファイルで確認してください。

### MythicMobs のボスと手下 { #mythicmobs-bosses-and-minions }

*AOneBlock 1.30.0 で追加されました。*

MythicMobs プラグインがインストールされていれば、フィナーレのボスに自分の MythicMobs のモブを使い、手下にも MythicMobs のモブを使えます。BentoBox が自動的に MythicMobs と連携するので、有効にする設定はありません。

```yaml
  finale:
    mythic-boss: SkeletonKing      # MythicMobs のモブタイプ
    mythic-level: 3                # オプション、デフォルトは 1
    boss: WITHER_SKELETON          # MythicMob が出現できない場合の代替（オプション）
    name: '<gold>The Skeleton King'
    mythic-minions:                # MythicMobs のタイプ: 数
      SkeletalMinion: 3
    minions:                       # バニラの手下も引き続き使えます
      ZOMBIE: 2
    drops:
      DIAMOND: 4
```

- **戦いのルールは同じです。** MythicMobs のボスもアイランドの外に出られず、ボスバーが表示され、プレイヤーからのダメージだけを受けます。プレイヤーが増えると体力が増え、戦いに負けると体力が減ります。MythicMobs のスキル、AI、ドロップはそのまま動作します。フィナーレの `drops` とコマンドも追加で与えられます。
- **体力と大きさ。** フェーズファイルで `health` や `scale` を設定しない限り、ボスは MythicMobs の設定どおりの体力と大きさになります。
- **手下。** `mythic-minions` は、バニラのボスでも MythicMobs のボスでも使えます。バニラの手下と同じく、ブロックを変更できず、戦いが終わると削除されます。現在のところ、名前にはタイプ ID が表示されます。
- **代替。** MythicMobs がインストールされていない場合や、そのモブが見つからない場合は、`boss` のタイプが使われます。`boss` がなければ、戦いなしでフェーズが進みます。不明な手下のタイプはログに記録され、スキップされます。

### フィナーレのオン・オフ { #turning-finales-on-and-off }

- **すべてのフィナーレ：** AOneBlock の `config.yml` で `island.phase-finales: false` を設定します。
- **1つのフェーズだけ：** そのフェーズのファイルから `finale:` セクションを削除します。

!!! warning "1.29.0 より前からアップグレードしたサーバーにはボスがいません"
    アップグレードで `plugins/BentoBox/addons/AOneBlock/phases/` のフェーズファイルが上書きされることはないため、それらのファイルには `finale:` セクションがありません。[同梱の各フェーズファイル](https://github.com/BentoBoxWorld/AOneBlock/tree/master/src/main/resources/phases)から `finale:` セクションを自分のファイルにコピーして、再起動してください。新規インストールでは最初から入っています。

### 同梱のボス

| フェーズ | ボス | モブ |
|---|---|---|
| Plains | The Colossus | ジャイアント |
| Underground | The Broodmother | クモ |
| Winter | The Frostbitten | ストレイ |
| Ocean | The Drowned King | ドラウンド |
| Jungle | The Temple Guardian | アイアンゴーレム |
| Swamp | The Bog Witch | ウィッチ |
| Dungeon | The Jailer | ウィザースケルトン |
| Desert | The Pharaoh | ハスク |
| The Nether | The Warlord | ピグリンブルート |
| Plenty | The Harvest Beast | ラヴェジャー |
| Desolation | The Last Titan | ジャイアント |
| Deep Dark | The Warden | ウォーデン |
| The End | The Void Walker | エンダーマン |
| Lush Caves | The Mossback | ボグド |
| Dripstone Caves | The Burrower | シルバーフィッシュ |
| Mangrove Swamp | The Mire Lurker | 洞窟グモ |
| Meadow | The Summoner | エヴォーカー |
| Cherry Grove | The Petal Phantom | イリュージョナー |
| Jagged Peaks | The Gale | ブリーズ |
| Sulfur Caves | Brimstone | ブレイズ |
| Dappled Forest | The Woodcutter | ヴィンディケーター |

---

## チェスト

チェストはフェーズの`_chests.yml`ファイルに、同じトップレベルセクション名の下に保存されます：

```yaml
'0':
  chests:
    '1':
      rarity: COMMON
      contents:
        0: ==: org.bukkit.inventory.ItemStack ...
    '2':
      rarity: EPIC
      contents:
        ...
```

- 各チェストをキーする数字（`'1'`、`'2'`）は単なる**ユニークID** — 重みでもなく位置でもありません。与えられたレアリティのチェストが期限切れになると、その同一の確率でそのレアリティのチェストの1つがランダムに選択されます。
- `contents`キーは**インベントリスロット番号**です。
- `rarity`は`COMMON`、`UNCOMMON`、`RARE`、`EPIC`です。

!!! tip "ゲーム内でチェストを作成し、手動では作成しないでください"
    あなたが望むもので実際のチェストを埋め、それを見て、`/[admin_command] setchest <phase> <rarity>`を実行してください。チェストは直接フェーズのチェストファイルにシリアル化され、正しく、最初に行われます。シリアル化されたアイテムYAMLを手動で編集することはエラーが発生しやすいです。その後、`/[admin_command] sanity [<phase>]`を使用してルートテーブルをチェックしてください。チェストを削除する場合でも、ファイルを編集してリロードすることを意味します。

---

## カスタムブロック

`custom-blocks:`は、平易なマテリアルではないエントリのリストです。各エントリは`probability:`フィールドを持ち、これは——その名前にもかかわらず——**重み**です。`blocks:`と`mobs:`と同じプール内で、`probability: 10`は重み`10`のブロックと同じ可能性があります。

```yaml
custom-blocks:
  - type: block-data
    data: minecraft:chest[waterlogged=true]
    probability: 10
  - type: mob
    mob: ZOMBIE
    underlying-block: STONE
    probability: 5
  - type: mob-data
    data: breeze{Glowing:1b,attributes:[{id:scale,base:2f}]}
    underlying-block: STONE
    probability: 15
  - type: itemsadder
    id: mypack:ruby_ore
    probability: 10
  - type: mythic-mob
    mob: SkeletalKnight      # MythicMob のタイプ ID（必須）
    level: 3                 # オプション、デフォルトは 1
    power: 1.0               # オプション、デフォルトは 0
    display-name: "Boss"     # オプション
    stance: ""               # オプション
    underlying-block: STONE  # オプション
    probability: 5
  - type: nexo
    id: custom_block
    probability: 10
  - type: craftengine
    id: craftengine:custom_block
    probability: 25
```

| `type` | 実行すること | 要件 |
|---|---|---|
| `block` / `block-data` | `/setblock`を実行します。ブロックデータ、ブロック状態、NBT、オプションの`destroy`\|`keep`\|`replace`モード。NBTを使用する場合は`block`を選択してください。 | — |
| `mob` | Spawn Entity APIを使用してバニラエンティティをスポーンさせます。 | `mob`; オプションの`underlying-block` (デフォルト `STONE`) |
| `mob-data` | バニラNBT/コンポーネントで`/summon`を実行します。モブの(スケール済み)バウンディングボックス内のブロックは、スポーン後1ティック後にクリアされて適合します。 | `data` |
| `mythic-mob` | BentoBoxのフックを通してMythicMobをスポーンさせます。 | MythicMobsプラグイン |
| `itemsadder` | [ItemsAdder](https://itemsadder.devs.beer/)からのブロック。 | ItemsAdderプラグイン |
| `nexo` | [Nexo](https://polymart.org/resource/nexo.6901)からのブロック。 | Nexoプラグイン |
| `craftengine` | [CraftEngine](https://github.com/Xiao-MoMi/craft-core)からのブロック。 | CraftEngineプラグイン、BentoBox 3.15.0+ |

カスタムブロックは`fixedBlocks`でも使用でき、マテリアル名の代わりにオブジェクトとして：

```yaml
fixedBlocks:
  0:
    type: block-data
    data: minecraft:chest[waterlogged=true]
  1: GRASS_BLOCK
```

!!! warning "データ文字列を引用符で囲んでください"
    カスタムブロック`data`文字列には`{`、`}`、`[`、`]`、二重引用符が含まれます。内部の二重引用符がYAMLの文字列デリミタと競合しないように、値全体を**シングル**引用符で囲んでください。

    ```yaml
    - type: mob-data
      data: 'breeze{CustomName:[{text:"Breezy",color:"#f90606"}],Glowing:1b}'
      underlying-block: STONE
      probability: 10
    ```

!!! tip "スポナーの落とし穴"
    タイミングフィールドなしで配置されたスポナーは、バニラ1.21では非アクティブです（`Delay:-1`は「決してティックしない」を意味します）。明示的に`Delay`、`MinSpawnDelay`、`MaxSpawnDelay`などを設定してください。そうしないと、スポナーは表示されますが何もしません。`Delay:0`は最初のスポーンを次のティックで発生させます。

カスタムブロックのプラグインがインストールされていない場合、ブロックは`STONE`にフォールバックし、ログに行が書き込まれます。

---

## バージョンゲーティング

フェーズ、個別のブロック、個別のモブは、それが必要とする最小Minecraftバージョンを宣言できます。サーバーが古すぎるものはすべて、`Tried to load invalid item`エラーの代わりに1つの情報行でログに記録されてスキップされます。

**全フェーズ** — `phases_index.yml`に`requiredMinecraftVersion`を配置して、ファイルが古いサーバーで解析されないようにします。その後、フェーズはブロック数をまったく消費せず、その後のフェーズは崩壊します。

**単一のブロックまたはモブ** — オブジェクトフォームを使用します。バリウェイトを`weight:`フィールドに置き換えます：

```yaml
blocks:
  NETHERRACK: 300
  DRIED_GHAST:
    weight: 25
    requiredMinecraftVersion: '1.21.6'

mobs:
  ZOMBIFIED_PIGLIN: 100
  HAPPY_GHAST:
    weight: 5
    requiredMinecraftVersion: '1.21.6'
```

チェストファイルはアイテムごとに読まれるため、サーバーバージョンが認識しないアイテムはそれ自体でスキップされ、チェストの残りはまだロードされます。

---

## 新しいフェーズの構築

1. **`phases`フォルダ内の既存ペアのファイルをコピーします** — たとえば`4000_jungle.yml`と`4000_jungle_chests.yml` — `volcano.yml`と`volcano_chests.yml`にコピーしてください。
2. **両方のファイルのトップレベルキーを変更してください**。`volcano:`のような何か一意に。両方で一致する必要があります。
3. **`name:`と`icon:`を設定してから、`blocks:`と`mobs:`を希望する重みで編集します。** パーセンテージは*フェーズ*合計に対して相対的であることを忘れずに。
4. **再起動またはリロードします。** アドオンは新しいファイルを認識し、デフォルトの長さ500の`phases_index.yml`の最後に追加し、ログに記録します：
   `Phase index: added Volcano from volcano.yml at the end of the phase order. Move it with the admin phases GUI.`
5. **`/[admin_command] phases`を使用して位置付けします** — 左クリックして選択、配置場所をクリック、Shift+左クリックして長さを設定します。
6. **テストします** — `/[admin_command] setcount <player> <number>`を使用してフェーズの開始ブロックにジャンプすることができます。

!!! tip "スクラッチアイランドでテストします"
    数百ブロックを破壊して、実際に何が出現するかを見てください。重みは紙上で読むのとは異なり、ゲーム内で動作します。`/[player_command] count`はフェーズ内の位置を表示します。

---

## トラブルシューティング

| 症状 | 考えられる原因 |
|---|---|
| `Bad block material in <phase>: X` | `X`はBukkitマテリアルではありません。またはアイテムです。ブロックではなく |
| `Bad item weight for <phase>: X. Must be positive number above 1` | 重みは0、負の値、または整数ではありません |
| `Bad entity type in <phase>: X` | 有効な`EntityType`ではありません。ログに有効なものがリストされます |
| `<phase> has zero probability of generating blocks` | `blocks:`セクションが存在しない、空である、または間違ったセクションキーの下にあります |
| `Phase name trying to be set to X but already set to Y. Duplicate phase file?` | 2つのファイルが同じトップレベルセクションキーを使用しています |
| フェーズが表示されない | `phases_index.yml`で`enabled: false`です、またはその`requiredMinecraftVersion`がサーバーより新しい |
| チェストが空で出現する | チェストファイルのトップレベルキーはフェーズファイルのキーと一致しません。またはそのアイテムはロードに失敗しました — `/[admin_command] sanity`を実行してください |
| フェーズがボスなしで終わる | フェーズファイルに `finale:` セクションがない（1.29.0 より前からアップグレードしたサーバーは[追加する](#turning-finales-on-and-off)必要があります）、`island.phase-finales` が `false`、またはワールドの難易度がピースフルです。`mythic-boss` を使っていて代替の `boss` がない場合は、MythicMobs がインストールされていないか、そのモブタイプが見つかりません |
| 編集が機能しない | アドオンがリロードされていません。またはjarの`src/main/resources`内のファイルを編集しました。`plugins/BentoBox/addons/AOneBlock/phases/`内ではなく |

サーバーログを起動時に注意してください。読み込まれたすべてのフェーズファイルはログに記録されます。また、拒否されたすべてのブロック、モブ、アイテム、および索引整合器が行った変更もログに記録されます（`Phase index:`で始まる行）。
