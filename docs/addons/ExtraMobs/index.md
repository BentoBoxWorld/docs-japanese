# ExtraMobs

**ExtraMobs** はブレイズ、ウィザースケルトン、シュルカーを出現させるためにモブのスポーンルールを調整します。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("ExtraMobs", beta=True) }}

## インストール

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. ゲーム内でこのアドオンの使用を許可するフラグを変更できます。

## 情報

このアドオンは Minecraft のスポーンルールを変更しません。代わりに自然にスポーンする他のモブを利用して、全ての条件が満たされた場合に新しいエンティティタイプに変換します。

##### ウィザースケルトンとブレイズの場合:

アドオンは設定の確率で次の条件が全て満たされた場合にゾンビピグリンをブレイズまたはウィザースケルトンに置き換えます:
 - 指定されたワールドが GameMode アドオンによって生成されている。
 - 指定されたワールドがネザーである。
 - ゾンビピグリンがネザーレンガ、ネザーレンガのハーフブロック、またはネザーレンガの階段の上に立っている。

##### シュルカーの場合:

アドオンは設定の確率で次の条件が全て満たされた場合にエンダーマンをシュルカーに置き換えます:
 - 指定されたワールドが GameMode アドオンによって生成されている。
 - 指定されたワールドがエンドである。
 - エンダーマンがパーパーブロック、パーパーの階段、またはパーパーのハーフブロックの上に立っている。

##### ガーディアンの場合:

アドオンは設定の確率で次の条件が全て満たされた場合にタラ、サーモン、またはトロピカルフィッシュをガーディアンに置き換えます:
 - 指定されたワールドが GameMode アドオンによって生成されている。
 - 指定されたワールドがオーバーワールドである。
 - 指定された場所のバイオームが深海またはそのバリアントである。
 - 魚がスポーンする水面の最初のブロック上がプリズマリン、プリズマリンレンガ、またはダークプリズマリン（ブロック、ハーフブロック、階段）である。

## 設定

最新の `config.yml` は[こちら](https://github.com/BentoBoxWorld/ExtraMobs/blob/develop/src/main/resources/config.yml)にあります。

??? note "disabled-gamemodes"
    このアドオンを動作させない GameMode の一覧です。各エントリは `-` で始まる独立した行に記述します。

    デフォルト: `[]`（空 — アドオンはすべての GameMode で動作します）

??? note "nether-chances"
    ネザーでゾンビピグリンを置き換える確率です。`wither-skeleton` と `blaze` はそれぞれ 0.0～1.0 の範囲の確率です。

    デフォルト: `wither-skeleton: 0.01`、`blaze: 0.1`

??? note "end-chances"
    `shulker` — エンドでエンダーマンをシュルカーに置き換える確率です。

    デフォルト: `0.1`

??? note "overworld-chance"
    `guardian` — オーバーワールドでタラ、サーモン、トロピカルフィッシュをガーディアンに置き換える確率です。

    デフォルト: `0.1`

??? note "gamemode-settings"
    上記のグローバルな確率を上書きする、GameMode ごとの置き換えルールです。1.15.0 で追加されました。

    各キーは GameMode アドオンの正確な名前（大文字小文字を区別）で、GameMode ごとに最大 3 つの環境セクション — オーバーワールド用の `world:`、`nether:`、`end:` — を定義できます。各セクションは `old`（置き換え対象の `EntityType`）、`new`（置き換え後の `EntityType`）、`chance`（0.0～1.0）を持つルールのリストです。

    GameMode ごとのルールは、その環境のグローバルなデフォルトよりも先に順番に評価されます。あるルールがスポーンするエンティティにマッチし、**かつ**確率の判定に成功した場合、置き換えが適用され、そのイベントの処理はそこで終了します。どのルールもマッチしない場合、またはマッチしたルールすべてが確率の判定に失敗した場合は、グローバルな `nether-chances` / `end-chances` / `overworld-chance` の値がフォールバックとして使用されます。

    デフォルト: `{}` — オプトイン方式なので、ここに記載されていない GameMode には引き続きグローバルな確率が適用されます。

    ```yaml
    gamemode-settings:
      BSkyBlock:
        nether:
          - old: ZOMBIFIED_PIGLIN
            new: WITHER_SKELETON
            chance: 0.05
          - old: ZOMBIFIED_PIGLIN
            new: BLAZE
            chance: 0.1
        end:
          - old: ENDERMAN
            new: SHULKER
            chance: 0.3
        world:
          - old: COD
            new: GUARDIAN
            chance: 0.15
      AcidIsland:
        end:
          - old: ENDERMAN
            new: SHULKER
            chance: 0.5
    ```

## 互換性

- [x] BentoBox 3.14.0 以降
- [x] Paper Minecraft 1.21.x
- [x] Java 21 以降

このアドオンは全ての Game mode アドオンをサポートしています。

## 翻訳

{{ translations("ExtraMobs") }}

## 変更履歴

!!! note "v1.15.0 の新機能 — Java 21 と BentoBox 3.14.0 が必須に"
    **リリース日:** 2026-05-31

    互換性: BentoBox API 3.14.0+ · Paper Minecraft 1.21.x · Java 21+。

    - ⚙️ **GameMode ごとのスポーン置き換えルール。** 新しい `gamemode-settings` 設定ブロックにより、サーバー全体で 1 つのグローバル設定を共有するのではなく、BentoBox の GameMode ごとに個別の置き換えルールを定義できます。デフォルトは `{}` のオプトイン方式なので、記載されていない GameMode では既存のグローバルな確率の値がこれまでどおり機能します。上記の「設定」セクションを参照してください。
    - 🔺 **Java 21 と BentoBox 3.14.0 が必須になりました。** アップグレード前に、サーバーが両方の条件を満たしていることを確認してください。
    - **Pladdon のエントリーポイントと `plugin.yml` が追加され**、最新の BentoBox アドオンとして読み込まれるようになりました。
    - テストスイートを JUnit 5 と MockBukkit で再構築し、SonarCloud 解析付きの GitHub Actions ビルドを追加、各種の保守性の問題を解消しました。

    [Release v1.15.0](https://github.com/BentoBoxWorld/ExtraMobs/releases/tag/1.15.0)
