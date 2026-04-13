# Limits

**Limits** は BSkyBlock や AcidIsland などのゲームモードでアイランドのブロックやエンティティを制限できます。

このアドオンはホッパーなどラグの原因となるエンティティやブロックを制限するために作られました。通常のブロックやエンティティの制限にも使用できますが、すべてを制限できるわけではありません。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("Limits") }}

## インストール

1. Limits アドオンの jar を BentoBox プラグインの addons フォルダに配置します
2. サーバーを再起動します
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます
4. config.yml を希望通りに編集します
5. 変更した場合はサーバーを再起動します

## コマンド

`limits` というユーザーコマンドと管理者コマンドがあります。管理者は特定のアイランドオーナーの制限を確認できます。どちらも制限と現在のカウントを GUI パネルで表示します。

## セットアップ - Config.yml

config.yml には以下のセクションがあります:

* blocklimits
* worlds
* entitylimits

### blocklimits

各ブロックマテリアルで許可される最大ブロック数を設定します。非ブロックマテリアルは機能しないため使用しないでください。制限はすべてのゲームワールドに適用されます。

### worlds

特定のワールドのブロック制限を設定します。AcidIsland_world のようにワールド名を正確に指定し、マテリアルと制限値を記述します。

### entitylimits

プレイヤーのアイランドスペース（保護エリアからアイランド境界まで）内のデフォルトエンティティ制限を設定します。制限値 5 はオーバーワールドで最大 5 体のエンティティを許可します。すべての種類のクリーチャースポーンに影響します。MINECARTS などのエンティティも含まれます。エンティティ制限はネザーとエンドでは対応していません。これはチャンクをロードしてエンティティをカウントする必要があり、過度なラグの原因となるためです。

注意: 制限 GUI には最初の 49 個の制限ブロックとエンティティのみが表示されます。

### entitygrouplimits

!!! note "実験的機能"
    以下の機能は ci.codemc.io の開発版ビルドでのみ利用可能です。

```yaml
entitygrouplimits:
  friendly:
    limit: 2
    entities:
      - COW
      - SHEEP
  monsters:
    limit: 4
    entities:
      - ZOMBIE
      - CREEPER
```

## 権限

アイランドオーナーはデフォルト設定やワールド設定を上書きする専用権限を持てます。形式は以下の通りです:

形式: `GAME-MODE-NAME.island.limit.MATERIAL.LIMIT`

例: `bskyblock.island.limit.hopper.10`

権限はプレイヤーがログインしたときに有効になります。

使用権限は以下の通りです（先頭にゲームモード名、例: acidisland を付けてください）:

```
  GAMEMODE_NAME.limits.player.limits:
    description: Player can use limits command
    default: true
  GAMEMODE_NAME.mod.bypass:
    description: Player can bypass limits
    default: op
  GAMEMODE_NAME.limits.admin.limits:
    description: Player can use admin limits command
    default: op
```

全権限の一覧は[こちら](Permissions)をご覧ください。

## プレースホルダー

{{ placeholders_source(source="Limits") }}


## 翻訳

{{ translations("Limits") }}

## 制限できないアイテム

現時点で制限できないアイテムがあります。主な理由は、追跡されずにアイテムを削除する方法が多すぎるためです。プログラマーでこれらを修正できる場合は PR を送ってください！

* 着火した TNT
* エヴォーカーの牙
* ラマのつば
* ドラゴンのファイアボール
* エリアエフェクトクラウド
* エンダーシグナル
* 小さいファイアボール
* ファイアボール
* 投げた経験値ボトル
* シュルカーの弾丸
* ウィザーの頭蓋骨
* トライデント
* 矢
* スペクトラルアロー
* 雪玉
* 卵
* リード
* エンダークリスタル
* エンダーパール
* エンダードラゴン
* アイテムフレーム
* 絵画


## 変更履歴

??? warning "v1.28.0 の新機能 — Java 21 が必要"
    **リリース日:** 2026-04-01

    - **Paper でシュルカー複製ファームが適切に制限されるようになりました。** Paper の `ShulkerDuplicateEvent` を使用して複製前に制限を適用し、シュルカーが制限チェック前にアイランド外にテレポートしていたバイパスを修正。
    - **銅チェストの制限をバイパスできなくなりました。** すべての銅チェストバリアント（酸化、ワックス付き、削り取り済み、ゴーレム生成）が単一の追跡マテリアルに正規化されました。ブロック状態の遷移も適切にカウントされます。
    - **無効な設定エントリが適切に処理されるようになりました。** `blocklimits` 設定の不正な名前空間キー、非ブロックマテリアル、カウント不可能なマテリアル（溶岩、水、空気）は NPE の代わりに明確な警告メッセージを出力するようになりました。
    - Java 21 が必要になりました（以前は Java 17）。アップグレード前にサーバーが Java 21 で動作していることを確認してください。
    - Spigot ターゲットを 1.21.11 に更新。

    [Release v1.28.0](https://github.com/BentoBoxWorld/Limits/releases/tag/1.28.0)

??? note "v1.28.1 の新機能"
    **リリース日:** 2026-04-07

    1.28.0 の 2 つのリグレッションのホットフィックス:

    - **既存のデータベースが再び読み込めるようになりました。** 1.28.0 では `IslandBlockCount` のマップフィールドが `Map<Material, Integer>` から `Map<NamespacedKey, Integer>` に変更され、1.28.0 以前の JSON ファイルの読み込みが失敗していました。下位互換性のある Gson `TypeAdapter` により、レガシーの列挙名、名前空間付き文字列、複合配列形式が読み込めるようになりました。**手動での移行は不要** — 古いファイルはそのまま読み込まれます。
    - **制限 GUI でブロック名が再び読みやすくなりました。** キーのフォーマットが誤っていたため、アイテムが `Minecraft:hopper` と表示されていました。

    [Release v1.28.1](https://github.com/BentoBoxWorld/Limits/releases/tag/1.28.1)
