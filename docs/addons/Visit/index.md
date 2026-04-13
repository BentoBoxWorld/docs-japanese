# Visit アドオン

**Visit** は他のプレイヤーのアイランドへの訪問を可能にするシンプルな BentoBox アドオンです。
これは Warps アドオンの代替です。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("Visit") }}

## インストール

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します
2. サーバーを再起動します
3. `/[admin_cmd] visit` コマンドを実行してアドオンを設定します

## 設定

多くのアドオン設定は管理者 GUI で変更できますが、一部はできません。
コマンドラベルの変更にはサーバーの再起動が必要です。

### config.yml

アドオンが正常にインストールされると、config.yml ファイルが作成されます。このファイルのすべてのオプションにはコメントが付いています。詳細はファイルを確認してください。
最新の設定ファイルはこちらで確認できます: [config.yml](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/resources/config.yml)

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装できる機能が導入されました。このアドオンはこの機能を使用する最初のアドオンの 1 つです。できるだけシンプルなカスタマイズを目指しましたが、一部の機能には説明が必要です。
BentoBox カスタム GUI の詳細はこちらをご覧ください: [Custom GUI's](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    アドオン GUI をカスタマイズするにはバージョン 1.5 が必要です。これが最初に実装されたバージョンです。アドオンは `/plugins/BentoBox/addons/Visit` の下に `panels` という名前のディレクトリを作成します。

    現在 2 つの GUI をカスタマイズできます:

    - メインパネル: `main_panel` - すべてのアイランドを含むパネル。
    - 管理パネル: `manage_panel` - いくつかの設定オプションを含むパネル。

    各 GUI にはそれぞれがサポートする機能が含まれています。

??? question "`PREVIOUS`|`NEXT` ボタンタイプとは何ですか？"
    PREVIOUS および NEXT ボタンタイプは、GUI にスペースよりも多くのアイランドがある場合に自動ページングを作成します。
    これらのタイプにはデータの下に追加パラメーターがあります:
 
    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

    例: 
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: visit.gui.buttons.previous.name
        description: visit.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            action: PREVIOUS
            tooltip: visit.gui.tips.click-to-previous
    ```

??? question "`SEARCH` ボタンタイプとは何ですか？"
    このボタンはメインパネルで利用可能です。
    特定のアイランドを検索するためのボタンを作成します。

    例: 
    ```yaml
        icon: PAPER
        title: visit.gui.buttons.search.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.search.description
        data:
          type: SEARCH
        actions:
          left:
            type: INPUT
            tooltip: visit.gui.tips.left-click-to-edit
          right:
            type: CLEAR
            tooltip: visit.gui.tips.right-click-to-clear
    ```

??? question "`FILTER` ボタンタイプとは何ですか？"
    このボタンはメインパネルで利用可能です。
    何らかのプロパティでアイランドをフィルタリングするためのボタンを作成します。

    例: 
    ```yaml
        # Icon is generated dynamically. However, you can set it manualy.
        # icon: SANDSTONE
        title: visit.gui.buttons.filter.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.filter.description
        data:
          type: FILTER
        actions:
          left:
            type: UP
            tooltip: visit.gui.tips.left-click-to-cycle
          right:
            type: DOWN
            tooltip: visit.gui.tips.right-click-to-cycle
    ```

??? question "`ISLAND` ボタンタイプとは何ですか？"
    このボタンはメインパネルで利用可能です。
    ISLAND ボタンはアイランドオブジェクトの動的エントリを作成します。

    タイトル、説明、アイコンを指定するとデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    このボタンは 3 種類のアクションタイプをサポートしています:

    - `VISIT` タイプはプレイヤーがアイランドを訪問できます
    - `CONFIRM` タイプは config で ask-payment-confirmation が有効な場合に訪問を確認できます。
    - `CANCEL` タイプは config で ask-payment-confirmation が有効な場合に訪問をキャンセルできます。

    例: 
    ```yaml
      # Data is generated dynamicaly. However, setting them will overwrite it.
      # icon: PLAYER_HEAD
      # title: visit.gui.buttons.island.name
      # description: visit.gui.buttons.island.description
      data:
        type: ISLAND
      actions:
        - click-type: left
          type: VISIT
          tooltip: visit.gui.tips.click-to-visit
        - click-type: left
          type: CONFIRM
          tooltip: visit.gui.tips.left-click-to-confirm
        - click-type: right
          type: CANCEL
          tooltip: visit.gui.tips.right-click-to-cancel
    ```

??? question "`PAYMENT` ボタンタイプとは何ですか？"
    このボタンは管理パネルで利用可能です。
    訪問者がアイランドを訪問する際の支払い額を設定するためのボタンを作成します。

    例: 
    ```yaml
        icon: ANVIL
        title: visit.gui.buttons.payment.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.payment.description
        data:
          type: PAYMENT
        actions:
          left:
            type: CHANGE
            tooltip: visit.gui.tips.click-to-change
    ```

??? question "`OFFLINE` ボタンタイプとは何ですか？"
    このボタンは管理パネルで利用可能です。
    アイランドメンバーが誰もオンラインでない場合にプレイヤーがアイランドを訪問できるかどうかを設定するためのボタンを作成します。

    例: 
    ```yaml
        icon: REDSTONE_LAMP
        title: visit.gui.buttons.offline.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.offline.description
        data:
          type: OFFLINE
        actions:
          left:
            type: TOGGLE
            tooltip: visit.gui.tips.click-to-toggle
    ```

??? question "`ALLOWED` ボタンタイプとは何ですか？"
    このボタンは管理パネルで利用可能です。
    ワンクリックで訪問を無効にするためのボタンを作成します。これは設定でフラグ `ALLOW_VISITS_FLAG` の値を変更するショートカットです。

    例: 
    ```yaml
        icon: PUMPKIN_PIE
        title: visit.gui.buttons.enabled.name
        # description: visit.gui.buttons.enabled.description
        data:
          type: ALLOWED
        actions:
          left:
            type: TOGGLE
            tooltip: visit.gui.tips.click-to-toggle
    ```

## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。
    このアドオンではアドオンの `config.yml` でプレイヤーコマンドのエイリアスを変更できることに注意してください。

=== "プレイヤーコマンド"
    - `/[player_command] visit <player>`: GUI を開くか、対象プレイヤーのアイランドを訪問します。
    - `/[player_command] visit configure`: 訪問設定を管理する GUI を開きます。
    - `/[player_command] visit setlocation`: 訪問者のスポーン場所を変更します。

=== "管理者コマンド"
    - `/[admin_command] visit <player>`: アドオン設定の編集とアイランドデータの設定ができる GUI を開きます。

## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "プレイヤー権限"
    - `[gamemode].visit` - プレイヤーが '/[player_command] visit' コマンドを使用できます。
    - `[gamemode].visit.configure` - プレイヤーが '/[admin_command] visit configure' コマンドを使用できます。
    - `[gamemode].visit.setlocation` - プレイヤーが '/[admin_command] visit setlocation' コマンドを使用できます。
    - `visit.icon.[material]` - Visit GUI でプレイヤー所有アイランドのアイコンを変更できます。

=== "管理者権限"
    - `[gamemode].admin.visit` - プレイヤーが '/[admin_command] visit' コマンドとそのサブコマンドを使用できます。
    
??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    もし本当に不足しているものがあれば、お知らせください！
   
## フラグ

アドオンは 2 つの BentoBox 保護フラグを導入します:

- ![pumpkin_pie](https://static.wikia.nocookie.net/minecraft_gamepedia/images/a/ac/Pumpkin_Pie_JE2_BE2.png){: loading=lazy width=16px } ALLOW_VISITS_FLAG: アイランド設定でアイランドへの訪問を有効/無効にするフラグ。
- ![paper](https://static.wikia.nocookie.net/minecraft_gamepedia/images/f/f2/Paper_JE2_BE2.png){: loading=lazy width=16px } RECEIVE_VISIT_MESSAGE_FLAG: アイランド設定でアイランドメンバーが訪問/退去メッセージを受け取るかどうかを有効/無効にするフラグ。


## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/Visit/issues)のリストに追加してください。

??? question "プレイヤーは訪問者がテレポートされる場所を変更できますか？"
    はい、プレイヤーはコマンド `/[player_cmd] visit setlocation` で設定できます。ただし、訪問者は「危険な」スポットにテレポートされず、場所が安全でない場合はより安全な場所にテレポートされることに注意してください。

??? question "管理者は訪問者がテレポートされる場所を変更できますか？"
    はい、管理者はコマンド `/[admin_cmd] setspawnpoint` で設定できます。ただし、訪問者は「危険な」スポットにテレポートされず、場所が安全でない場合はより安全な場所にテレポートされることに注意してください。

??? question "プレイヤーはカスタムアイコンを設定できますか？"
    はい、Visit パネルのアイランドアイコンはアイランドオーナーに `visit.icon.[material]` 権限を付与することで変更できます。

??? question "エコノミーを使いたくありません。完全に無効にできますか？"
    はい、設定オプション `disable-economy` ですべてのエコノミー部分を完全に無効にできます。

??? question "アイランドメンバーが訪問値を変更できるようにする/しないにはどうすればいいですか？"
    アイランドオーナー（および `CHANGE_SETTINGS` 権限を持つメンバー）は設定パネルで `RANKED_COMMANDS` アクセスを編集できます。一覧に `/[player_cmd] visit configure` コマンドが表示されます。

??? question "アイランドメンバーが訪問場所を変更できるようにする/しないにはどうすればいいですか？"
    アイランドオーナー（および `CHANGE_SETTINGS` 権限を持つメンバー）は設定パネルで `RANKED_COMMANDS` アクセスを編集できます。一覧に `/[player_cmd] visit setlocation` コマンドが表示されます。

## 翻訳

{{ translations("Visit") }}

## API

Visit 1.4.0 および BentoBox 1.17 以降、他のプラグインは Visit アドオンのデータに直接アクセスできます。

### Maven 依存関係

Visit は他のプラグイン向けの API を提供しています。これはバージョン 1.5.0 以降に対応しています。

!!! note "注意"
    Maven POM.xml に Visit の依存関係を追加します:

    ```xml
        <repositories>
            <repository>
                <id>codemc-repo</id>
                <url>https://repo.codemc.io/repository/bentoboxworld/</url>
            </repository>
        </repositories>
        
        <dependencies>
            <dependency>
                <groupId>world.bentobox</groupId>
                <artifactId>visit</artifactId>
                <version>1.5.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

最新の Visit バージョンを使用してください。

Visit の JavaDocs は[こちら](https://ci.codemc.io/job/BentoBoxWorld/job/Visit/ws/target/apidocs/index.html)で確認できます。

### イベント

=== "VisitEvent"
    !!! summary "説明"
        プレイヤーがアイランドにテレポートされる前、ただし支払い後に発火するイベントです。

        キャンセル可能です。（キャンセル時に支払いは返却されません）

        クラスへのリンク: [VisitEvent](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/java/world/bentobox/visit/events/VisitEvent.java)

    !!! question "変数"
        - `User player` - アイランドを訪問しようとしているプレイヤーの ID。
        - `Island island` - プレイヤーが訪問しようとしているアイランド。
        - `boolean cancelled` - イベントがキャンセルされたかどうかを示すブール値。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onVisit(VisitEvent event) {
            UUID player = event.getPlayer();
            User user = event.getUser();
            Island island = event.getIsland();

            boolean cancelled = event.isCancelled();
        }
        ```
