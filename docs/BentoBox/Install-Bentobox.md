# ビデオチュートリアル

[![ビデオサムネイル](https://i.ytimg.com/vi/01MagYDuOCk/hqdefault.jpg?sqp=-oaymwEjCPYBEIoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLCzVNO0ObSEMOOpYtUEtv4LjsMhBA)](https://www.youtube.com/watch?v=01MagYDuOCk)

# はじめに

BentoBoxは強力で多機能なプラグインです。BentoBoxWorldでは、BentoBoxの特性に合わせた最もわかりやすいインストール方法を厳選してご紹介しています。

ほとんどのSpigotプラグインと比べると、BentoBoxのインストールにはサーバーのpluginsフォルダへのドラッグ&ドロップよりも少し時間がかかりますが、それがもたらす無数の可能性はその価値があります。

始めましょう！

***

# BentoBoxのダウンロード

BentoBoxは様々なウェブサイトで**無料**でダウンロードできます。公式リリースはプラグインのSpigotページまたは[GitHub `Releases`タブ](https://github.com/BentoBoxWorld/bentobox/releases)で見つけられ、**テストされていない**開発ビルドは[Jenkins](https://ci.codemc.io/job/BentoBoxWorld/job/BentoBox/)からダウンロードできます。

# BentoBoxのセットアップ

BentoBoxをダウンロードしたら、サーバーの`plugins`フォルダに入れる必要があります。ASkyBlockとは異なり、必須の依存関係はありません。BentoBoxは見つけたプラグイン（Vault、PlaceholderAPI、Multiverse-Coreなど）に自動的にフックして機能を拡張します。

サーバーを起動し、すべてのプラグインが完全に有効になるまで待ちます。サーバーに接続しても、BentoBoxは単体では何も行いません。実際、**BentoBox本体だけでは何も起こりません**。SkyBlockゲームモードの追加など、実際に機能させるためには[アドオン](https://github.com/BentoBoxWorld/bentobox/wiki/Addons)が必要です。

サーバーを停止します。BentoBoxの`config.yml`ファイルを確認できます。

# アドオンのインストール

[アドオン](/BentoBox/Addons)がBentoBoxを特別なものにしています。ただし、これらは**プラグインではない**ことに注意してください。`plugins`フォルダに入れても**起動しません**。

まず、追加したいアドオンをダウンロードします。公式アドオンは[https://download.bentobox.world](https://download.bentobox.world)から簡単に入手できます。個別にダウンロードする場合は[BentoBoxWorldのリポジトリ一覧](https://github.com/BentoBoxWorld)の各`Releases`タブを参照してください（**未テスト**の開発ビルドは[Jenkins](https://ci.codemc.io/job/BentoBoxWorld/)から）。

必要なものをすべてダウンロードしたら、`plugins/BentoBox/addons`フォルダに入れてサーバーを起動し、設定ファイルとフォルダが生成されるのを待ちます。その後、サーバーを停止してから設定を編集してください。

アドオンがご利用のBentoBoxバージョンと互換性がない場合があります。公式アドオンには**必ず**対応バージョンの記載がありますが、更新なしで新しいバージョンに対応していることも多いです。

# まとめ

以上でセットアップ完了です！ご利用いただきありがとうございます。ぜひBentoBoxをお楽しみください。
