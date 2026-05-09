# BSkyBlock

虚空に浮かぶ孤島から始まるクラシックなスカイブロック体験。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("BSkyBlock") }}

## 歴史
**BSkyBlock**は、新しいMinecraftサーバーバージョン向けの**ASkyBlock**の進化版です。

## インストール

0. BentoBoxをインストールし、データフォルダを生成するためサーバーを少なくとも1回起動します。
1. このjarファイルをBentoBoxプラグインのaddonsフォルダに配置します。
2. サーバーを再起動します。
3. アドオンがワールドとデータフォルダを作成し、フォルダ内にconfig.ymlが生成されます。
4. サーバーを停止します。
5. config.ymlを希望通りに編集します。
6. ワールドの生成に関わる設定を変更した場合は、初回起動で作成されたワールドフォルダを削除します。
7. サーバーを再起動します。

## Config.yml

config.ymlはASkyBlockに似ていますが、*同一ではありません*。島間の距離と保護範囲は**半径の値**であることに注意してください。つまり島のサイズはこれらの値の2倍のブロック数になります！また、島間の距離はチャンク境界（16ブロックの倍数）に自動的に設定されます。

## パーミッション

パーミッションの一覧は[こちら](Permissions)をご覧ください。

## コマンド

コマンドの一覧は[こちら](Commands)をご覧ください。

## プレースホルダー

プレースホルダーの一覧は[こちら](Placeholders)をご覧ください。

## 変更履歴

??? warning "v1.20.0 の新機能 — BentoBox 3.13.0 と Paper 1.21.11 が必要"
    **リリース日：** 2026-04-27

    - 🐛 **モブの湧き不具合を修正。** チャンクジェネレーターが `shouldGenerateMobs()` をオーバーライドしていなかったため、Bukkit API のデフォルトである `false` が使われ、すべての BSkyBlock 生成ワールドでバニラのモブの湧きが密かに抑制されていました。モブが正しく湧くようになりました。
    - 🐛 **水生生物（魚、イカ）の自然湧きを修正。** 1.21 プラットフォーム移行以降、BSkyBlock のワールドで魚やイカが自然に湧かなくなっていました。修正で再び自然に湧きます。[BentoBox #2593](https://github.com/BentoBoxWorld/BentoBox/issues/2593) を解消。
    - ⚡ **チャンク生成のモダン化。** ワールドジェネレーターを古い `generateChunkData()` + `BiomeGrid`（廃止予定）アプローチから、Paper の現行 `generateNoise()` + `BiomeProvider` API に移行しました。
    - 🔡 17 言語すべてのロケールファイルにある看板テキストを、レガシーな `&c` カラーコードから MiniMessage 形式に移行しました。
    - ビルドのモダン化：JDK 21、JUnit 5 + MockBukkit テストスタック。

    🔺 **BentoBox 3.13.0 以降と Paper 1.21.11 が必要。** これより古い BentoBox ではこのアドオンはロードされません。

    🔡 **ロケールに関する注意：** 看板テキストは MiniMessage タグを使うようになりました（例：`&c` ではなく `<red>…</red>`）。カスタマイズしたロケールファイルは更新が必要です。

    [Release v1.20.0](https://github.com/BentoBoxWorld/BSkyBlock/releases/tag/1.20.0)

## 翻訳

{{ translations("BSkyBlock") }}
