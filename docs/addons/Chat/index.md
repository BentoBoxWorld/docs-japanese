# Chat

**Chat** はプレイヤーがビジターやアイランドメンバーと非公開でトークできる**チームチャット**と**アイランドチャット**を提供します。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("Chat") }}

## アイランドチャット

有効にすると、チャットはビジターを含むアイランド上のプレイヤーのみに制限されます。管理者やモデレーターはスパイコマンドを使ってアイランドチャットを傍聴できます。

## チームチャット

有効にすると、チャットはチームメンバーのみに送信されます。チームプレイヤーは自分のチャットがチームチャットチャンネルに送られるかどうかを切り替えられます。管理者はスパイコマンドを使って全てのチームチャットを傍聴できます。

## コマンド
### プレイヤーコマンド

* `chat` - アイランドチャットのオン/オフを切り替えます。
* `teamchat` - プレイヤーのチャットをチームチャンネルに送るかどうかを切り替えます。

### 管理者コマンド

* `chatspy` - アイランドチャットスパイのオン/オフを切り替えます。
* `teamchatspy` - チームチャットスパイのオン/オフを切り替えます。

設定ファイルには必要に応じて全チャットをログに記録する設定もあります。

## 設定

```
# Configuration file for Chat
team-chat:
  gamemodes:
  - BSkyBlock
  - AcidIsland
  - CaveBlock
  - SkyGrid
  # Log team chats to console.
  log: false
island-chat:
  # Lists the gamemodes in which you want the Chat addon to be effective.
  gamemodes:
  - BSkyBlock
  - AcidIsland
  - CaveBlock
  - SkyGrid
  # Log island chats to console.
  log: false
chat-listener:
  # Sets priority of AsyncPlayerChatEvent. Change this if Chat addon
  # is conflicting with other plugins which listen to the same event
  # Acceptable values: lowest, low, normal, high, highest, monitor
  priority: normal
```

## 権限

```
permissions:
  '[gamemode].chat.team-chat':
    description: Player can use team chat
    default: true
  '[gamemode].chat.island-chat':
    description: Player can use island chat
    default: true
  '[gamemode].chat.spy':
    description: Player can use team or island chat spy
    default: op

```

## このアドオンが気に入りましたか？
[スポンサー](https://github.com/sponsors/tastybento)になることで、このようなアドオンをさらに増やし、改善することができます！

## 翻訳

{{ translations("Chat") }}
