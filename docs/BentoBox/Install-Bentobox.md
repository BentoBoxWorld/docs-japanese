# ビデオチュートリアル

[![ビデオサムネイル](https://i.ytimg.com/vi/01MagYDuOCk/hqdefault.jpg?sqp=-oaymwEjCPYBEIoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLCzVNO0ObSEMOOpYtUEtv4LjsMhBA)](https://www.youtube.com/watch?v=01MagYDuOCk)

# はじめに

BentoBoxはサーバーにインストールして実行する強力ですが特殊なプラグインです。BentoBoxWorldでは、BentoBoxの主要な特徴に最も適した最もユーザーフレンドリーなインストール方法を長々と議論してきました。

ほとんどのSpigotプラグインと比べると、BentoBoxのインストールにはサーバーのpluginsフォルダへのドラッグ&ドロップよりも少し時間がかかりますが、それがもたらす無数の可能性はその価値があります。

始めましょう！

***

# BentoBoxのダウンロード

BentoBoxは様々なウェブサイトで**無料**でダウンロードできます。公式リリースはプラグインのSpigotページまたは[GitHub `Releases`タブ](https://github.com/BentoBoxWorld/bentobox/releases)で見つけられ、**テストされていない**開発ビルドは[Jenkins](https://ci.codemc.io/job/BentoBoxWorld/job/BentoBox/)からダウンロードできます。

# BentoBoxのセットアップ

BentoBoxをダウンロードしたら、サーバーの`plugins`フォルダに入れる必要があります。ASkyBlockとは異なり、必須の依存関係はありません。BentoBoxは見つけたプラグイン（Vault、PlaceholderAPI、Multiverse-Coreなど）に自動的にフックして機能を拡張します。

サーバーを起動し、すべてのプラグインが完全に有効になるまで待ちます。サーバーに接続しても、BentoBoxは何も特別なことをしません。実際、**BentoBox単体では何もしません**。Skyblockゲームモードを管理するなど、「学ぶ」ために[アドオン](https://github.com/BentoBoxWorld/bentobox/wiki/Addons)を追加する必要があります。

サーバーを停止します。BentoBoxの`config.yml`ファイルを確認できます。

# アドオンのインストール

[アドオン](/BentoBox/Addons)がBentoBoxを特別なものにしています。ただし、これらは**プラグインではない**ことに注意してください。`plugins`フォルダに入れても**起動しません**。

まず、サーバーに追加したいアドオンをダウンロードする必要があります。公式のものは[BentoBoxWorldのリポジトリリスト](https://github.com/BentoBoxWorld)にあり、`Releases`タブからダウンロードできます（**テストされていない**開発ビルドは[Jenkins](https://ci.codemc.io/job/BentoBoxWorld/)から）。後でダウンロードしやすくするウェブサイトをいつか設置する予定です。

必要なものをすべてダウンロードしたら、それらを`plugins\BentoBox\addons`フォルダに入れ、サーバーを起動して設定ファイルとフォルダが作成されるのを待ち、最後にサーバーに支障をきたすことなく編集できるようにシャットダウンします。

アドオンが使用しているBentoBoxのバージョンと互換性がない場合があることに注意してください。公式アドオンは**常に**サポートするバージョンの明確な説明とともに提供されます。ただし、更新なしに新しいバージョンをサポートすることが多いことに注意してください。

# まとめ

準備ができたはずです！
私たちのプラグインを使用していただき嬉しいです。私たちが改善を楽しんでいるのと同じくらい楽しんでいただければ幸いです。
