# VoidPortals

**VoidPortals** はプレイヤーがボイドに落ちることでディメンション間を移動できます。フラグが有効なワールドでプレイヤーがボイドに落ちると、死亡する代わりに次のディメンションの対応する位置に安全にテレポートします——**オーバーワールド → ネザー → ジ・エンド → オーバーワールド**。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("VoidPortals", beta=True) }}

!!! info "互換性"
    **BentoBox 3.14.0** 以降、**Minecraft 1.21+**、**Java 21** が必要です。

## インストール

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. 「Void world teleports」フラグは**デフォルトで無効**です——ゲームモードの管理設定パネルでワールドごとに有効にしてください。

## フラグ

VoidPortals は単一のワールド設定フラグを追加します。ゲームモードの管理設定パネルでワールドごとに切り替えてください。

{{ flags_source("VoidPortals", "WORLD_SETTING") }}

## 翻訳

{{ translations("VoidPortals") }}

??? note "v1.6.1 の新機能"
    **リリース日:** 2026-06-01

    バグ修正リリースです。詳細は [Release v1.6.1](https://github.com/BentoBoxWorld/VoidPortals/releases/tag/1.6.1) をご覧ください。

    - ボイド落下で到着時に死亡しなくなりました。ボイドに落ちると下向きの速度が蓄積され、それがテレポート後も引き継がれて、次のディメンションに到着した瞬間に地面に叩きつけられていました。到着時に速度と落下距離がリセットされるようになり、安全に着地できます。

??? warning "v1.6.0 の新機能 — 破壊的変更"
    **リリース日:** 2026-06-01

    2019 年以来の初リリース——VoidPortals は現在の BentoBox エコシステム向けに完全に近代化されました。詳細は [Release v1.6.0](https://github.com/BentoBoxWorld/VoidPortals/releases/tag/1.6.0) をご覧ください。

    - 🔺 **Java 21、Paper 1.21.11、BentoBox 3.14.0 が必要です**（以前は Spigot 1.13.2 / BentoBox 1.5.0）。このリリースは古いサーバーでは読み込まれません。
    - 最新の Paper サーバーで jar が正しく読み込まれるよう、`Pladdon` と `plugin.yml` を同梱しました。
    - 🔡 14 の新しい言語を追加し、すべての言語ファイルを **MiniMessage** 形式に変換しました。言語ファイルをカスタマイズしている場合は、再生成するか変更を移植してください——従来の `&` カラーコードは使用されなくなりました。
    - JUnit 5 / MockBukkit テストスイートを追加しました。対角のボイド落下でも依然としてテレポートすることを保証する回帰テストを含みます。
