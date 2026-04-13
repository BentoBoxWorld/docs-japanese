BentoBoxはBentoBoxのインストール全体を管理するためのいくつかのコマンドを実装しています。

**利用可能なコマンド（2.2.0以降）**

| コマンド | パーミッション | 説明 |
|-----------------------------------------|------------------------------|-------------------------------------------------------------|
| /bentobox [help/h]                      | bentobox.admin               | 利用可能なすべてのBentoBoxコマンドを表示します |
| /bentobox about                         | bentobox.about               | 著作権とライセンス情報を表示します |
| /bentobox catalog                       | bentobox.admin.catalog       | カタログを表示します |
| /bentobox locale                        | bentobox.admin.locale        | ローカライゼーションファイルの分析を行います |
| /bentobox manage/overview               | bentobox.admin.manage        | 管理パネルを表示します |
| /bentobox migrate                       | bentobox.admin.migrate       | あるデータベースから別のデータベースへデータを移行します |
| /bentobox perms                         | bentobox.admin.perms         | BentoBoxとアドオンの有効なパーミッションをYAML形式で表示します |
| /bentobox rank [list \| add \| remove] [rank reference] [rank value] | bentobox.admin.rank | ランクのリスト表示、追加、削除 |
| /bentobox reload/rl                     | bentobox.admin.reload        | BentoBoxとすべてのアドオン、設定、ロケールをリロードします |
| /bentobox version/v/versions/addons     | bentobox.version             | BentoBoxとアドオンのバージョンを表示します |

`/bentobox`のエイリアスは`/bbox`です。

バグレポートを提出したりサポートを求めたりする際は、使用しているソフトウェア、データベース、アドオンのバージョンを知らせるために`/bentobox version`コマンドの出力を**必ず**提供してください。
