# CheckMeOut

これはアイランド審査申請アドオンです。このアドオンにより、プレイヤーが自分のアイランドを管理者の審査のために提出できます。管理者はサーバー全体のチャレンジやコンペティションを設定し、プレイヤーが参加してアイランドを提出できます。管理者は提出されたアイランドの一覧を表示する GUI があり、そこからアイランドにテレポートできます。アイランドが管理者に確認されると削除でき、またはアクティビティ全体が終わったら全ての提出をクリアできます。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("CheckMeOut") }}


## インストール

0. BentoBox をインストールし、データフォルダを作成するためにサーバーで少なくとも一度起動します。
1. この jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます。
4. サーバーを停止します。
5. config.yml を希望通りに編集します。
7. サーバーを再起動します。

## 設定

メインの `config.yml` ファイルにはゲームモードアドオンの設定に関する基本情報が含まれています。

`panels` は一部のユーザーがアクセスできるパネルのカスタマイズを許可します。


### config.yml

アドオンが正常にインストールされると、config.yml ファイルが作成されます。このファイルの全オプションにはコメントが付いています。詳細はファイルを確認してください。
最新の設定ファイルはこちらで確認できます: [config.yml](https://github.com/BentoBoxWorld/CheckMeOut/blob/develop/src/main/resources/config.yml)

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装する機能が導入されました。このアドオンはその機能を使用する最初のアドオンの一つです。カスタマイズをできる限りシンプルにしようとしましたが、一部の機能については説明が必要です。
BentoBox カスタム GUI の詳細はこちらを参照してください: [カスタム GUI](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    アドオンの GUI をカスタマイズするにはバージョン 1.1 が必要です。これが実装された最初のバージョンです。アドオンは `/plugins/BentoBox/addons/CheckMeOut` の下に `panels` というディレクトリを作成します。

    現在カスタマイズできる GUI は 1 つです:

    - メインパネル: `view_panel` - 提出されたアイランドが含まれるパネル。

??? question "`PREVIOUS`|`NEXT` ボタンタイプとは何ですか？"
    PREVIOUS と NEXT ボタンタイプは、GUI のスペースより多くのアイランドがある場合に自動ページングを作成できます。
    これらのタイプには data の下に追加パラメーターがあります:

    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

    例: 
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: checkmeout.gui.buttons.previous.name
        description: checkmeout.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            action: PREVIOUS
            tooltip: checkmeout.gui.tips.click-to-previous
    ```

??? question "`RANDOM` ボタンタイプとは何ですか？"
    このボタンはプレイヤーがランダムな提出にテレポートできます。
    
    - warp アクションは Warps アドオンをインストールしておりプレイヤーがワープサインを持っている場合のみ利用できます。
    - visit アクションは Visit アドオンをインストールしている場合のみ利用できます。
    - check アクションはアドオンのデフォルトのテレポートメカニズムです。

    例: 
    ```yaml
        icon: DROPPER
        title: checkmeout.gui.buttons.random.name
        description: checkmeout.gui.buttons.random.description
        data:
          type: RANDOM
        actions:
          # Warp action requires WARP addon. If warp addon is not present, warp action will not work.
          warp:
            click-type: UNKNOWN
            tooltip: checkmeout.gui.tips.click-to-warp
          # Visit action requires Visit addon. If Visit addon is not present, visit action will not work.
          visit:
            click-type: UNKNOWN
            tooltip: checkmeout.gui.tips.click-to-visit
          # Check action requires player to have "[gamemode].checkmeout.admin.check" permission.
          check:
            click-type: UNKNOWN
            tooltip: checkmeout.gui.tips.click-to-check
    ```

??? question "`ISLAND` ボタンタイプとは何ですか？"
    このボタンはメインパネルで利用できます。
    ISLAND ボタンはアイランドオブジェクトの動的エントリを作成します。

    タイトル、説明、アイコンを指定するとデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    このボタンは 3 つの異なるアクションタイプをサポートします:

    - warp アクションは Warps アドオンをインストールしておりプレイヤーがワープサインを持っている場合のみ利用できます。
    - visit アクションは Visit アドオンをインストールしている場合のみ利用できます。
    - check アクションはアドオンのデフォルトのテレポートメカニズムです。

    例: 
    ```yaml
      # icon: PLAYER_HEAD
      title: checkmeout.gui.buttons.island.name
      description: checkmeout.gui.buttons.island.description
      data:
        type: ISLAND
      actions:
        # Warp action requires WARP addon. If warp addon is not present, warp action will not work.
        warp:
          # Click type UNKNOWN means that it accept any click type.
          click-type: UNKNOWN
          tooltip: checkmeout.gui.tips.click-to-warp
        # Visit action requires Visit addon. If Visit addon is not present, visit action will not work.
        visit:
          # Click type UNKNOWN means that it accept any click type.
          click-type: UNKNOWN
          tooltip: checkmeout.gui.tips.click-to-visit
        # Check action requires player to have "[gamemode].checkmeout.admin.check" permission.
        check:
          # Click type UNKNOWN means that it accept any click type.
          click-type: UNKNOWN
          tooltip: checkmeout.gui.tips.click-to-check
    ```

## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。
    このアドオンではアドオンの `config.yml` ファイルでプレイヤーコマンドのエイリアスを変更できることに注意してください。

=== "プレイヤーコマンド"
    - `/[player_command] checkmeout`: アイランドを審査のために提出します。
    - `/[player_command] checkmeout view`: 他の提出されたアイランドを表示する GUI を開きます。

=== "管理者コマンド"
    - `/[admin_command] checkmeout`: メイン管理者コマンド。
    - `/[admin_command] checkmeout check <player>`: 提出されたアイランドにプレイヤーをテレポートします。
    - `/[admin_command] checkmeout clearall`: 提出された全てのアイランドを削除します。
    - `/[admin_command] checkmeout delete <player>`: <player> が提出したアイランドを削除します。
    - `/[admin_command] checkmeout seesubs`: 提出された全てのアイランドを表示するメニューを開きます。


## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "プレイヤー権限"
    - `[gamemode].checkmeout` - プレイヤーがアイランドを提出するための '/[player_command] checkmeout' コマンドを使用できます。デフォルト: true。
    - `[gamemode].checkmeout.view` - プレイヤーが全提出アイランドを表示するための '/[admin_command] checkmeout view' コマンドを使用できます。デフォルト: true。
    - `checkmeout.icon.[material]` - プレイヤー所有のアイランドの View GUI でのアイコン変更を許可します。デフォルト: false。

=== "管理者権限"
    - `[gamemode].checkmeout.admin.check` - '/[admin_command] checkmeout check' コマンドを使用できます。デフォルト: OP。
    - `[gamemode].checkmeout.admin.delete` - '/[admin_command] checkmeout delete' コマンドを使用できます。デフォルト: OP。
    - `[gamemode].checkmeout.admin.clearsubmissions` - '/[admin_command] checkmeout clearall' コマンドを使用できます。デフォルト: OP。
    - `[gamemode].checkmeout.admin.seesubs` - '/[admin_command] checkmeout seesubs' コマンドを使用できます。デフォルト: OP。
    
??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    以下のリストに不足しているものがあれば、お知らせください！

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/CheckMeOut/issues)のリストに追加してください。

## API

### イベント

BentoBox 1.17 API はクラスローダーの問題を解決する機能を実装しました。イベントを直接使用したいプラグインは今すぐできます。

CheckMeOut をプロジェクトの依存関係として追加する必要があります。Maven を使用できます:

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>checkmeout</artifactId>
    <version>1.1.0</version>
    <scope>provided</scope>
</dependency>
```

=== "IslandSubmittedEvent"
    !!! summary "説明"
        プレイヤーが審査のためにアイランドを提出した後にトリガーされるイベントです。

        クラスへのリンク: [IslandSubmittedEvent](https://github.com/BentoBoxWorld/CheckMeOut/blob/develop/src/main/java/world/bentobox/checkmeout/events/IslandSubmittedEvent.java)

    !!! question "変数"
        - `UUID uuid` - アイランドを提出したプレイヤーの ID。
        - `Location location` - 提出の場所。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onSubmittion(IslandSubmittedEvent event) {
            UUID player = event.getUUID();
            Location location = event.getLocation();
        }
        ```

## 翻訳

{{ translations("CheckMeOut") }}
