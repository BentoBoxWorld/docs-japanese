# TradeWinds コマンド

プレイヤーコマンドは**`/tw`**（エイリアス`/tradewinds`）です。管理者コマンドは**`/twadmin`**です。ベアの`/tw`を実行すると、デフォルトアクション`go`を実行します。

## プレイヤーコマンド

| コマンド | 説明 | 権限 |
|---------|-------------|------------|
| `/tw go` (エイリアス: `spawn`, `sail`) | 帆を張る—あなたがそれを去った海に入ります。あなたのアイランドで：ホームポイントにステップしてください。海で：ホームへのコースをトグル（昼間は軸受、夜は星の下の正確な距離）。決して海を越えた乗客ではありません。 | `tradewinds.island.spawn` |
| `/tw chart` | チャートコンパスを上げる—チャート島、ドック、あなたのボート、ホームのホログラムマーカー。`/tw chart list`テキストバージョンを印刷します。 | `tradewinds.island.chart` |
| `/tw starchart` | チャート島のスターチャートマップを受け取ります。 | `tradewinds.island.starchart` |
| `/tw rank` (エイリアス: `ranks`) | あなたのシーファーランクと、チャート島のトップテン船乗り。 | `tradewinds.island.rank` |
| `/tw claim` | あなたが立っている野生の小島をあなたのアイランドとしてクレーム（ランクと価格ゲートが適用されます）。 | `tradewinds.island.claim` |
| `/tw sethome` | ホームポイントを設定—あなたのアイランドに立っているときのみ。 | `tradewinds.island.sethome` |
| `/tw home` | あなたのホームポイントにステップ—あなたのアイランドに立っているときのみ。 | `tradewinds.island.home` |
| `/tw unclaim` | クレーム済みの小島を野生に戻してください。所有者のみ、チームを最初に空にします、払い戻しなし。すべてのブロックは左の通りのままです。 | `tradewinds.island.unclaim` |
| `/tw fine` | ポートで犯罪歴を解決（クリーンに戻る）。 | `tradewinds.island.fine` |
| `/tw restart` | 取引キャリアを再開始（使用数制限、設定上限）。 | `tradewinds.island.restart` |
| `/tw info` | あなたがいるアイランドについての情報。 | `tradewinds.island.info` |
| `/tw settings` | アイランド設定を表示。 | `tradewinds.island.settings` |
| `/tw language` | 言語を選択。 | `tradewinds.island.language` |
| `/tw warp` | アイランド水のどこからでもワープダイアログを開きます。**デフォルトではOp**—意図されたパスは、ボーダーカーテンに帆を張っています。これは自動的にダイアログを提供します。 | `tradewinds.island.warp` |
| `/tw trade` | アイランド保護範囲内の任意の場所からアイランドマーケットを開きます。**デフォルトではOp**—意図されたパスはドッキングとプラザのトレーダーを右クリックしています。 | `tradewinds.island.trade` |
| `/tw prices` | あなたの価格記録—あなたが呼んだポートはどのような価格で、どのくらい前。`economy.price-logbook-enabled`フィーチャーフラグがオンの場合のみ登録（デフォルトではオフ）。 | `tradewinds.island.prices` |

## 管理者コマンド

`/twadmin`は、すべての標準的なBentoBox管理コマンド（`version`、`tp`、`getrank`、`setrank`、ブループリントなど）、プラス TradeWinds特有のセット：

| コマンド | 説明 | 権限 |
|---------|-------------|------------|
| `/twadmin islands` | 最も近い取引島をタイプ、技術レベル、バンド、距離で一覧表示します。 | `tradewinds.admin.islands` |
| `/twadmin tpisland <#>` | アイランドリストから取引島にテレポート。 | `tradewinds.admin.tpisland` |
| `/twadmin boat <player>` | プレイヤーのボート記録を検査—材料、カーゴ、燃料、最後に見られた位置、ハルが実際に読み込まれているか、誰かのバックパックにあるかどうか。 | `tradewinds.admin.boat` |
| `/twadmin boat <player> restore` | 失われたアクティブボートを、プレイヤーのバックパックにスタンプされたアイテムとして再生成、カーゴレコード無傷。本物のハルが読み込まれているか持ち運ばれている場合は拒否。 | `tradewinds.admin.boat` |
| `/twadmin rank <player>` | プレイヤーのシーファーランク表示：有効な島、実チャート数、調整。 | `tradewinds.admin.rank` |
| `/twadmin rank <player> <rank\|islands\|reset>` | プレイヤーのランクをランクスラッグまたはアイランド数で設定、または調整をリセット。実際のチャートはトップにカウント。 | `tradewinds.admin.rank` |
| `/twadmin customs` | あなたが立っている場所でカスタムズが何を作るか表示—密輸品、スキャン確率、パトロール強度。 | `tradewinds.admin.customs` |
| `/twadmin priceaudit` | 価格カバレッジを監査—何が販売でき、何が戦利品であり、何が販売不可能か—そして完全なレポートを`price-audit.txt`に書きます。 | `tradewinds.admin.priceaudit` |
| `/twadmin warpfail <player>` | プレイヤーの次のワープをインタースティスへのフェイルに仕組む（もう一度実行してクリア）。オンデマンドのミスジャンプパスのテスト。 | `tradewinds.admin.warpfail` |
| `/twadmin reflag` | すべての取引島にセキュリティバンドフラグを再適用。 | `tradewinds.admin.reflag` |
