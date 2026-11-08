# addons

アドオンを配置する場所です。

# locales

言語ファイルを配置する場所です。

# database

フラットファイルデータベース（YAMLファイル）が保存される場所です。アドオンからのデータが保存されます。

BentoBox自身のテーブルもここに保存されます（例：`Islands`、`Players`、`Names`、`WorldSettings`）。`WorldSettings`テーブルには、ゲームモードの`config.yml`ではなくBentoBox自身が保存するワールド設定（現在は常に許可するエンティティタイプのリスト）が、ゲームモードごとに1ファイルずつ保存されます。
