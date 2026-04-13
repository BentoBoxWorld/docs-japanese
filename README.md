# BentoBox ドキュメント（日本語）

BentoBox日本語ドキュメントサイトの公式ソースリポジトリへようこそ。このリポジトリには、公式日本語ドキュメントサイトの構築に使用されるすべてのMarkdownファイルが含まれています。

-----

## ドキュメントを読む

公開・最新版のドキュメントはこちらでご覧いただけます：

**[https://docs.bentobox.world](https://docs.bentobox.world)**

> BentoBoxのドキュメントを読んだりサポートを受けたりするだけであれば、上記リンクをご参照ください。このリポジトリはドキュメントへの**貢献**を目的としています。

英語の参照ドキュメントはメインリポジトリにあります：[BentoBoxWorld/docs](https://github.com/BentoBoxWorld/docs)

-----

## このリポジトリについて

このリポジトリにはBentoBoxドキュメントの日本語翻訳が含まれています。内容：

- BentoBoxコアドキュメント
- ゲームモード（AcidIsland、AOneBlock、BSkyBlock、CaveBlock など）
- アドオン（Bank、Border、Challenges、Level、Limits、Warps など）
- 開発者向けチュートリアル

翻訳は定期的にメインの英語ドキュメントと同期されます。不足または古いコンテンツを見つけた場合、貢献を歓迎します！

-----

## 貢献する

誤字の修正からガイド全体の翻訳まで、あらゆる貢献を歓迎します。あなたのご協力が日本語ユーザーのBentoBox体験を向上させます。

### 貢献方法

1. このリポジトリを自分のGitHubアカウントに**フォーク**します。
2. 変更内容に合わせた**新しいブランチを作成**します（例：`fix/config-correction` や `feat/translate-addon-xyz`）。
3. Markdownファイルに**変更を加えます**。
4. 変更を**コミットしてフォークにプッシュ**します。
5. 自分のブランチからこのリポジトリの `master` ブランチへ**Pull Request（PR）を作成**します。

### 翻訳のガイドライン

- 技術的な名称は英語のまま残してください：コマンド名（例：`/island`）、YAMLキー（例：`disabled-gamemodes`）、Javaクラス名、MkDocsマクロ（例：`{{ addon_description("Level") }}`）。
- セクションタイトル、説明文、説明テキストは翻訳してください。
- 既存のMarkdown書式（コードブロック、admonition、テーブル）を維持してください。

-----

## 自動公開プロセス

このリポジトリは**[ReadTheDocs](https://readthedocs.org/)**サービスに接続されており、ビルドとデプロイを管理しています。

- **コミット/マージ時：** `master` ブランチにコミットがプッシュされると、ReadTheDocsにWebhookが送信されます。
- **ビルド：** ReadTheDocsが最新の変更を取得し、MarkdownファイルをHTMLスタティックサイトにビルドします。
- **公開：** ビルドが成功すると、新バージョンのドキュメントが自動的に公開されます。

あなたのPull Requestがマージされてから数分以内にドキュメントサイトに反映されます。

## ライセンス

BentoBoxドキュメントのテキストとコンテンツ（このリポジトリ）は**[Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/)**ライセンスの下で提供されています。

ドキュメントに含まれるコードスニペットは、特に断りのない限り**[MIT](https://opensource.org/licenses/MIT)**ライセンスの下で提供されています。
