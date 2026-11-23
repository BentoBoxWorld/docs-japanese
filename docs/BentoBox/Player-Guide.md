# プレイヤーガイド { #player-guide }

BentoBoxサーバーに初めてですか？このページではアイランドを取得するから、友達を招待する、アイランドを安全に保つ、移動するまでの基本をカバーしています。

!!! info "あなたのサーバーのコマンド"
    このページでは`/island`を使用しています。これはSkyBlock（BSkyBlock）のコマンドです。他のゲームモードには独自のコマンドがあります。例えば、OneBlockは`/ob`、AcidIslandは`/ai`、CaveBlockは`/cave`です。お使いのサーバーに合わせて読み替えてください。サーバーによっては一部の機能をオフにしたり、デフォルトを変更したりしている場合もあります。

## 始めましょう { #get-started }

**`/island`** と入力してください。

- まだアイランドがなければ、1つを選ぶよう求められ（選択肢がある場合）、その後テレポートされます。
- すでにアイランドがあれば、`/island`でホームに戻ります。

以上です。他のすべては任意です。

## 移動する { #getting-around }

| コマンド | 機能 |
|---|---|
| `/island` または `/island go` | アイランドにテレポート |
| `/island sethome` | 立っている場所をホームポイントに設定 |
| `/island sethome <name>` | 別の名前付きホームを設定（複数ホームがサーバーで許可されている場合） |
| `/island go <name>` | 名前付きホームにテレポート |
| `/island homes` | ホーム一覧を表示 |
| `/island spawn` | ゲームモードのスポーン地点にテレポート |
| `/island info` | 立っているアイランドの詳細情報を表示 |
| `/island near` | 近くのアイランドの名前を表示 |

## 友達と遊ぶ { #playing-with-friends }

友達がアイランドを手伝う方法は2つあります。

**チームとして参加。** チームメンバーはアイランドを永続的に共有します。

1. 招待します：`/island team invite <name>`。相手はオンラインである必要があります。
2. 相手が`/island team accept`で承認します（ポップアップが表示された場合は**承認**をクリック）。

気が変わりましたか？`/island team uninvite <name>`で招待を取り下げられます。応答のない招待は自動的に期限切れになります。ほとんどのサーバーでは1日後です。

!!! warning "他人のアイランドに参加する"
    チーム招待を受け入れると、通常**自分のアイランドが失われます**。最初に確認が求められます。サーバー設定によっては、インベントリがクリアされることもあります。

**参加させずに手伝ってもらう。** 相手は自分のアイランドを保ちます。

- `/island team trust <name>`：相手は`/island team untrust <name>`で削除されるまで手伝えます。
- `/island team coop <name>`：相手はチームのみんなが一度ログオフするまで手伝えます。

**`/island team`** を開いてメニューからチームを見たり、プレイヤーを招待したり、ランクを管理したりできます。

| コマンド | 機能 |
|---|---|
| `/island team leave` | チームを脱退。所有者は最初に誰かに島を譲り渡さないと脱退できません |
| `/island team kick <name>` | メンバーを削除 |
| `/island team promote <name>` | メンバーの権限を増やす |
| `/island team demote <name>` | メンバーの権限を減らす |
| `/island team setowner <name>` | チームの別のメンバーにアイランドを譲る |

## アイランドを安全に保つ { #keeping-your-island-safe }

アイランドは保護されています。訪問者は周りを見回すことはできますが、許可しない限りブロックを壊したり、チェストを開いたり、動物を傷つけたりはできません。

**`/island settings`** を開いて、訪問者、coop プレイヤー、信頼できるプレイヤー、チームメンバーが何をできるかを選択します。設定をクリックして許可するランクをサイクルさせます。

| コマンド | 機能 |
|---|---|
| `/island settings` | 各ランクが何をできるかを選択 |
| `/island lock` | アイランドをロックして訪問者を閉め出す（もう一度実行してロック解除） |
| `/island expel <name>` | 訪問者をアイランドから追い出す |
| `/island ban <name>` | プレイヤーをアイランドからバン |
| `/island unban <name>` | バンを解く |
| `/island banlist` | バンされたプレイヤーを表示 |

何かがブロックされていて理由が不明な場合、メッセージは通常何が許可されていないかを伝えます。アイランドの所有者に聞くか、`/island settings`を確認してください。

## アイランド { #your-island }

| コマンド | 機能 |
|---|---|
| `/island setname <name>` | アイランドに名前を付ける |
| `/island resetname` | 名前を削除 |
| `/island language` | BentoBoxメッセージの言語を変更 |
| `/island reset` | 新しいアイランドで新たに開始。**古いアイランドは削除されます。** サーバーがリセット回数を制限している場合があります |

## サーバーが持つかもしれないエクストラ機能 { #extras-your-server-may-have }

サーバーはアドオンで機能を追加します。一般的なものをいくつか紹介します：

| コマンド | アドオン | 機能 |
|---|---|---|
| `/island level` | [Level](../addons/Level/index.md) | アイランドレベルを計算 |
| `/island top` | [Level](../addons/Level/index.md) | トップアイランドを表示 |
| `/island challenges` | [Challenges](../addons/Challenges/index.md) | チャレンジメニューを開く |
| `/island warps` | [Warps](../addons/Warps/index.md) | プレイヤーワープを一覧表示；サインの最初の行に`[Welcome]`と書いて自分のワープを追加 |
| `/island bank` | [Bank](../addons/Bank/index.md) | アイランドの共有銀行 |
| `/island fly` | [IslandFly](../addons/IslandFly/index.md) | アイランドで飛ぶ |

すべてのコマンドを確認するには`/island help`と入力してください。
