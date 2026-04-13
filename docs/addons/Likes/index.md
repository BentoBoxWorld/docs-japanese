# Likes

**Likes** はプレイヤーが他のアイランドをいいね、悪いね、またはスターで評価できるようにします。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("Likes") }}

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
最新の設定ファイルはこちらで確認できます: [config.yml](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/resources/config.yml)

一部の設定オプションはゲーム内の管理 GUI から変更できます。ただし、一部はできません。

最も重要な設定オプションはモードです:

!!! summary "Likes モード"
    mode: アドオンが動作するモードを変更できます

    - LIKES - アイランドにいいねのみを追加できます。
    - LIKES_DISLIKES - アイランドにいいねと悪いねのみを追加できます。
    - STARS - アイランドをスターで評価できます。

一度に使用できるモードは 1 つだけです。

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装する機能が導入されました。このアドオンはその機能を使用する最初のアドオンの一つです。カスタマイズをできる限りシンプルにしようとしましたが、一部の機能については説明が必要です。
BentoBox カスタム GUI の詳細はこちらを参照してください: [カスタム GUI](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    アドオンの GUI をカスタマイズするにはバージョン 2.2 が必要です。これが実装された最初のバージョンです。アドオンは `/plugins/BentoBox/addons/Likes` の下に `panels` というディレクトリを作成します。

    現在カスタマイズできる GUI は 3 つです:

    - 表示パネル: `view_panels` - プレイヤーのアイランドをいいねした人を表示するパネル。
    - トップパネル: `top_panel` - 特定の値でトップアイランドが含まれるパネル。
    - 管理パネル: `manage_panels` - いいね/悪いねまたはスターを追加できるパネル。

    表示パネルと管理パネルには各モード用の 3 つの異なるパネルがあります。


## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。

=== "プレイヤーコマンド"
    - `/[player_command] likes`: いいね、悪いね、スターを追加/削除する GUI を開きます。
    - `/[player_command] likes top`: いいね、悪いね、スターでトップアイランドを表示する GUI を開きます。
    - `/[player_command] likes view <player>`: アイランドにいいねやスターを付けた人を表示する GUI を開きます。

=== "管理者コマンド"
    - `/[admin_command] likes`: 管理者 GUI を開きます。
    - `/[admin_command] likes settings`: 管理者設定 GUI を開きます。

## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "プレイヤー権限"
    - `[gamemode].likes` - (デフォルト: `true`) - プレイヤーが '/[player_command] likes' コマンドを使用できます。
    - `[gamemode].likes.top` - (デフォルト: `true`) - プレイヤーが '/[player_command] likes top' コマンドを使用できます。
    - `[gamemode].likes.view` - (デフォルト: `true`) - プレイヤーが '/[player_command] likes top' コマンドを使用できます。
    - `[gamemode].likes.icon.[MATERIAL]` - (デフォルト: `false`) - トップ GUI でアイランドオーナーのアイコン変更を許可します。

=== "管理者権限"
    - `[gamemode].likes.view.others` - (デフォルト: `op`) - プレイヤーが '/[player_command] likes view <player>' コマンドを使用できます。
    - `[gamemode].likes.bypass-cost` - (デフォルト: `op`) - アドオン内の操作のコストをバイパスできます。
    - `[gamemode].likes.admin` - (デフォルト: `op`) - '/[admin_command] likes' コマンドの使用を許可します。
    - `[gamemode].likes.admin.settings` - (デフォルト: `op`) - '/[admin_command] likes settings' コマンドの使用を許可します。

??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    以下のリストに不足しているものがあれば、お知らせください！

## プレースホルダー

{{ placeholders_source(source="Likes") }}

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/Likes/issues)のリストに追加してください。

??? question "悪いねを無効にできますか？"
    はい、Likes アドオンは 3 つの動作モードをサポートしています:

    - Likes: アイランドにいいねのみを追加できます
    - LikesDislikes: いいねと悪いねを追加できます
    - Stars: プレイヤーのアイランドを 1〜5 つのスターで評価できます
       
??? question "他のプレイヤーのいいねを見ることはできますか？"
    はい、ただし権限 `[gamemode].likes.view.others` が必要です。
    
    その権限があればプレイヤーは `/[playercmd] likes view <player>` を使って他のプレイヤーのいいねを確認できます。
    
??? question "特定のアイランドだけ表示アイコンを変更できますか？"
    はい、可能です。
    
    2 つの方法があります:
    
    1. 管理者 GUI でアイランドを選択して表示するブロックを選択できます。
    2. アイランドオーナーに権限を追加する: `[gamemode].likes.icon.[MATERIAL]`
        
    注意: PLAYER_HEAD はアイランドオーナーの頭に変換されます。

## 翻訳

{{ translations("Likes") }}

## API

Likes 2.2.0 と BentoBox 1.17 以降、他のプラグインが Likes アドオンのデータに直接アクセスできます。

### Maven 依存関係

Likes は他のプラグイン向け API を提供しています。これはバージョン 2.2.0 以降に対応しています。

!!! note "注意"
    Maven POM.xml に Likes 依存関係を追加してください:

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
                <artifactId>likes</artifactId>
                <version>2.2.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

最新の Likes バージョンを使用してください。

Likes の JavaDocs は[こちら](https://ci.codemc.io/job/BentoBoxWorld/job/Likes/ws/target/apidocs/index.html)で確認できます。

### イベント

=== "LikeAddEvent"
    !!! summary "説明"
        プレイヤーがアイランドに新しいいいねを追加したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [LikeAddEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/LikeAddEvent.java)


    !!! question "変数"
        - `UUID user` - いいねを追加したプレイヤーの ID。
        - `String islandId` - いいねを受け取るアイランドの ID。
        
    !!! example "例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLike(LikeAddEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

=== "LikeRemoveEvent"
    !!! summary "説明"
        プレイヤーがアイランドからいいねを削除したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [LikeRemoveEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/LikeRemoveEvent.java)

    !!! question "変数"
        - `UUID user` - いいねを削除したプレイヤーの ID。
        - `String islandId` - いいねを失うアイランドの ID。
        
    !!! example "例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLikeRemove(LikeRemoveEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  
   
=== "DislikeAddEvent"
    !!! summary "説明"
        プレイヤーがアイランドに新しい悪いねを追加したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [DislikeAddEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/DislikeAddEvent.java)

    !!! question "変数"
        - `UUID user` - 悪いねを追加したプレイヤーの ID。
        - `String islandId` - 悪いねを受け取るアイランドの ID。

    !!! example "例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onDislike(DislikeAddEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

=== "DislikeRemoveEvent"
    !!! summary "説明"
        プレイヤーがアイランドから悪いねを削除したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [DislikeRemoveEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/DislikeRemoveEvent.java)

    !!! question "変数"
        - `UUID user` - 悪いねを削除したプレイヤーの ID。
        - `String islandId` - 悪いねを失うアイランドの ID。

    !!! example "例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onDislikeRemove(DislikeRemoveEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

=== "StarsAddEvent"
    !!! summary "説明"
        プレイヤーがアイランドに新しいスターを追加したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [StarsAddEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/StarsAddEvent.java)

    !!! question "変数"
        - `UUID user` - スターを追加したプレイヤーの ID。
        - `String islandId` - スターを受け取るアイランドの ID。
        - `int value` - 追加されたスターの値（1〜5）

    !!! example "例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onStarsAdd(StarsAddEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
            int value = event.getValue();
        }
        ```  

=== "StarsRemoveEvent"
    !!! summary "説明"
        プレイヤーがアイランドからスターを削除したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [StarsRemoveEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/StarsRemoveEvent.java)

    !!! question "変数"
        - `UUID user` - スターを追加したプレイヤーの ID。
        - `String islandId` - スターを失うアイランドの ID。

    !!! example "例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onStarsRemove(StarsRemoveEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

### アドオンリクエストハンドラー

BentoBox 1.17 以前は、アドオンのロードに使用するクラスローダーの問題で BentoBox 環境外からのデータアクセスに問題がありました。
これはデータが他のアドオンからのみアクセス可能だったことを意味します。しかし BentoBox が PlAddon 機能を実装したため、リクエストハンドラーはもはや必要ありません。

アドオンリクエストハンドラーの詳細は[こちら](/en/latest/BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons/)をご覧ください。

=== "island-likes"
    !!! summary "説明"
        指定されたワールドのアイランドに保存されたいいねデータを返します。

    !!! question "入力"
        - `world-name`: String - ワールドの名前。
        - `island`: String - アイランドの UUID。

    !!! success "出力"
        出力は以下のキーを持つ `Map<String, Object>` です:

        - `likes`: long - 指定されたアイランドに設定されたいいねの数。
        - `dislikes`: long - 指定されたアイランドに設定された悪いねの数。
        - `rank`: long - 指定されたアイランドのランク数。
        - `stars`: double - 指定されたアイランドの平均スター値。
        - `placeByLikes`: integer - いいねによるランキングでの順位。
        - `placeByDislikes`: integer - 悪いねによるランキングでの順位。
        - `placeByRank`: integer - ランクによるランキングでの順位。
        - `placeByStars`: integer - スターによるランキングでの順位。
        - `likedBy`: List&lt;UUID&gt; - 指定されたアイランドをいいねしたプレイヤーの UUID のリスト。
        - `dislikedBy`: List&lt;UUID&gt; - 指定されたアイランドを悪いねしたプレイヤーの UUID のリスト。
        - `staredBy`: Map&lt;UUID, Integer&gt; - 指定されたアイランドをスターしたプレイヤーの UUID と追加したスター数のマップ。


    !!! failure "失敗"
        `world-name` が提供されていないか存在しないかゲームモードワールドでない場合、またはアイランドが提供されていないかアイランドのデータが空の場合、このハンドラーは空のマップを返します。

    !!! example "コード例"
        ```java
        public Map<String, Object> getLikesData(String worldName, String islandUUID) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Likes")
                .label("island-likes")
                .addMetaData("world-name", worldName)
                .addMetaData("island", islandUUID)
                .request();
        }
        ```

=== "top-ten-likes"
    !!! summary "説明"
        トップ 10 のアイランド UUID とその値のマップを含む `Map<String, Number>` を返します。

    !!! question "入力"
        - `world-name`: String - ワールドの名前。
        - `type`: String - トップのタイプ。サポート: STARS、LIKES、DISLIKES、RANK。

    !!! success "出力"
        トップ 10 のアイランドの UUID をキーとし、アイランドのトップ値を値とするマップ。

    !!! failure "失敗"
        `world-name` が提供されていないか存在しないかゲームモードワールドでない場合、または指定されたトップタイプにデータがない場合、このハンドラーは空のマップを返します。

    !!! example "コード例"
        ```java
        public Map<String, Number> getTopTenLikes(String worldName, String type) {
            return (Map<String, Number>) new AddonRequestBuilder()
                .addon("Likes")
                .label("top-ten-likes")
                .addMetaData("world-name", worldName)
                .addMetaData("type", type)
                .request();
        }
        ```
