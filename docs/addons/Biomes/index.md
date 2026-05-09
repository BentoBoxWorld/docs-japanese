# Biomes

**Biomes** はプレイヤーがアイランドの**バイオームを変更**できるようにします。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("Biomes", beta=True) }}

## インストール

1. アドオンの jar を `plugins/BentoBox/addons` フォルダに配置します。
2. サーバーを起動・停止して Biomes の設定ファイルを生成します。
3. [`config.yml`](#config.yml) と [`biomesTemplate.yml`](#Template) ファイルを編集します（`plugins/BentoBox/addons/Biomes` フォルダにあります）。
4. サーバーを再起動します。
5. ゲームモードにバイオームをインポートします。

## 設定

### config.yml

アドオンが正常にインストールされると、config.yml ファイルが作成されます。このファイルの全オプションにはコメントが付いています。詳細はファイルを確認してください。
最新の設定ファイルはこちらで確認できます: [config.yml](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/resources/config.yml)

### テンプレート

!!! warning "警告"
    通常の設定ファイルとは異なり、`biomesTemplate.yml` ファイルへの変更はサーバー起動時に自動的に反映されません。  
    変更を手動でインポートし、以前の設定をインポート済みの場合は上書きする必要があります。

このファイルにはデフォルトバイオームに関する全ての必要な情報が含まれています。
biomes.yml の値を変更した場合、**/[admin_command] biomes** を実行して適用する必要があります。

デフォルトのテンプレートファイルはこちらです: [biomesTemplate.yml](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/resources/biomesTemplate.yml)

!!! info "バイオームに関する便利なリソース"
    - [Spigot のバイオーム一覧](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/block/Biome.html)
    - [Minecraft 公式 Wiki の「Biome」ページ](https://minecraft.gamepedia.com/Biome)

??? テンプレートファイルの構造
    ```
    biomes:                                      # Internal Data Structure. DO NOT CHANGE!
      <unique_name>:                             # Unique name for the biome. Required!
        biome: <BIOME>                           # Spigot BIOME TYPE. Valid values can be found in link below. Required!
        environment: <ENVIRONMENT>               # Spigot WORLD ENVIRONMENT TYPE. World environment value. Default Normal.
        name: <String>                           # String. Custom name for biome. Default <unique_name>.
        description: <String>                    # String. Some extra description in icon lore. Default empty.
        icon: <Item>                             # BentoBox ItemParser type. Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default Paper.
        order: <Integer>                         # Integer. Order of current biome. Default -1.
        unlock:                                  # Section that configures biomes unlock/buy options. Not required.
          level: <Long>                          # Minimal island level for biome to be unlockable. Requires Level addon. Default 0.
          permissions: [<String>]                # Set of permissions for biome to be unlockable. Default empty.
          cost: <Double>                         # Purchase cost (once) for biome. Requires Vault and Economy plugins. Default 0.
          items: [<Item>]                        # Set of items for purchasing biome (once). Write format for each item can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default empty.
        change:                                  # Section that configures cost for each biome usage. Not required.
          mode: <Mode>                           # Mode how cost is applied. Supported values: STATIC - price never changes, PER_BLOCK - cost is applied for each block in area, PER_USAGE - cost increases by [increment] after each usage. Default STATIC.
          cost: <Double>                         # Biome change cost. Requires Vault and Economy plugins. Default 0.
          items: [<Item>]                        # Set of items for changing biome. Write format for each item can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default empty.
          increment: <Double>                    # Increment for all costs (money and items) if usage is set to PER_USAGE. Default 0. (works as static)
    # Here starts the Bundle List
    bundles:                                     # Internal Data Structure.
      <unique_name>:                             # Unique name for the bundle. Required!
        name: <String>                           # String. Custom name for bundle. Default <unique_name>.
        description: <String>                    # String. Some extra description in icon lore. Default empty.
        icon: <Item>                             # BentoBox ItemParser type. Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default Paper.
        biomes: [<String>]                       # Set of <unique_names> that you used in biomes section. Default empty.
    ```

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装する機能が導入されました。このアドオンはその機能を使用する最初のアドオンの一つです。カスタマイズをできる限りシンプルにしようとしましたが、一部の機能については説明が必要です。
BentoBox カスタム GUI の詳細はこちらを参照してください: [カスタム GUI](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    アドオンの GUI をカスタマイズするにはバージョン 2.0 が必要です。これが実装された最初のバージョンです。アドオンは `/plugins/BentoBox/addons/Biomes` の下に `panels` というディレクトリを作成します。

    現在カスタマイズできる GUI は 3 つです:

    - メインパネル: `main_panel` - ユーザーが購入または使用できる全バイオームが含まれるパネル。
    - 詳細パネル: `advanced_panel` - バイオームをアイランドに適用する異なる方法を選択できるパネル。
    - 購入パネル: `buy_panel` - プレイヤーが購入できるバイオームが含まれるパネル。

    各 GUI にはそれぞれに固有の機能があります。

??? question "`PREVIOUS`|`NEXT` ボタンタイプとは何ですか？"
    PREVIOUS と NEXT ボタンタイプは、GUI のスペースより多くのバイオームがある場合に自動ページングを作成できます。
    これらのタイプには data の下に追加パラメーターがあります:
 
    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

    例: 
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: biomes.gui.buttons.previous.name
        description: biomes.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            tooltip: biomes.gui.tips.click-to-previous
    ```

??? question "`RETURN` ボタンタイプとは何ですか？"
    このボタンは全てのパネルで利用できます。
    前のメニューに戻るか GUI を閉じるボタンを作成します。説明はアドオンが生成しますが、全てのボタンと同様にパネルで独自のテキストを指定することもできます。

    例: 
    ```yaml
        data:
          type: RETURN
    ```

??? question "`BIOME` ボタンタイプとは何ですか？"
    このボタンは main_panel と buy_panel で利用できます。
    BIOME ボタンはバイオームオブジェクトの動的エントリを作成します。バイオームが存在する場合のみボタンが表示されます。例えば 3 つのバイオームしかないのに GUI に 7 つのスペースを定義した場合、3 つのスペースのみ埋まります。残りのスペースは空になります。

    デフォルトではバイオームは順序番号でソートされますが、data の下の `id` パラメーターで特定のバイオームを特定のスロットに指定することもできます。
    
    ```yaml
      data:
        type: BIOME
        id: example_biome
    ```

    タイトル、説明、アイコンを指定するとデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    このボタンは 3 つの異なるアクションタイプをサポートします:

    - CHANGE - デフォルトの更新モードとデフォルトの範囲値に基づいてバイオームを変更します。main_panel で利用可能。
    - ADVANCED_PANEL - 異なるバイオーム更新モードを選択できる詳細パネルを開きます。main_panel で利用可能。
    - BUY - 選択されたバイオームを購入します。buy_panel で利用可能。

    例: 
    ```yaml
      data:
        type: BIOME
      actions:
        left:
          type: CHANGE
          # Supports ISLAND | CHUNK:NUMBER | RANGE:NUMBER
          content: ISLAND
          tooltip: biomes.gui.tips.left-click-to-apply
        right: 
          type: ADVANCED_PANEL
          tooltip: biomes.gui.tips.right-click-to-open
    ```

??? question "`PURCHASE` ボタンタイプとは何ですか？"
    このボタンは main_panel で利用できます。
    プレイヤーが購入できるバイオームが含まれる新しいパネルを開くボタンを作成します。

    例: 
    ```yaml
        data:
          type: PURCHASE
        action:
          left:
            tooltip: biomes.gui.tips.click-to-view
    ```


??? question "`INCREASE|REDUCE` ボタンタイプとは何ですか？"
    このボタンは advanced_panel で利用できます。
    バイオーム変更の「範囲」を増加/減少させるボタンを作成します。増加/減少する数値はボタンタイプと一緒に定義できます。

    例: 
    ```yaml
        data:
          type: INCREASE
          value: 5
        actions:
          left:
            tooltip: biomes.gui.tips.click-to-increase
    ```

??? question "`MODE` ボタンタイプとは何ですか？"
    このボタンは advanced_panel で利用できます。
    ISLAND、CHUNK、RANGE モード間でバイオーム更新モードを変更できるボタンを作成します。モードはボタンタイプと一緒に定義します。

    例: 
    ```yaml
        data:
          type: MODE
          value: CHUNK
        actions:
          left:
            tooltip: biomes.gui.tips.click-to-choose
    ```

??? question "`ACCEPT` ボタンタイプとは何ですか？"
    このボタンは advanced_panel で利用できます。
    選択した設定でバイオーム更新を開始できるボタンを作成します。2 つのアクションがあります: 
      
       - ACCEPT: バイオーム更新を開始します
       - INPUT: チャットで数値を手動入力できます。

    例: 
    ```yaml
        data:
          type: ACCEPT
        actions:
          left:
            type: ACCEPT
            tooltip: biomes.gui.tips.left-click-to-accept
          right:
            type: INPUT
            tooltip: biomes.gui.tips.right-click-to-write
    ```

## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。

!!! info "情報"
    Biomes アドオンのプレイヤーコマンドは完全に設定可能です。Biomes アドオンの設定ファイルで変更できます。以下はこれらのコマンドのデフォルト名です。

=== "プレイヤーコマンド"
    - `/[player_command] biomes`: ユーザーのアイランドのバイオームを変更できる GUI を開きます。
    - `/[player_command] biomes help`: 全コマンドのヘルプを表示します。
    - `/[player_command] biomes set <biome> [<type>] [<size>]`: GUI を開かずにアイランドのバイオームを変更します。`<type>` と `<size>` パラメーターが指定されない場合、アドオン設定のデフォルト値が使用されます。
    - `/[player_command] biomes buy <biome>`: GUI を開かずにバイオームを購入します。

    !!! info "情報"
        - `<biome>` は実際の Minecraft バイオーム名ではない場合があります。管理者が定義します。
        - `<type>` はバイオーム変更タイプの3つのうちの一つです。アイランド全体（`ISLAND`）、現在のチャンク（`CHUNK`）、またはプレイヤー周辺の距離（`RANGE`）でバイオームを変更します。


=== "管理者コマンド"
    - `/[admin_command] biomes`: 管理者バイオーム GUI を開きます。
    - `/[admin_command] biomes help`: 全バイオーム関連管理者コマンドのヘルプを表示します。
    - `/[admin_command] biomes import [<file>]`: `biomesTemplate.yml` 設定ファイルまたは指定されたファイルからバイオームをインポートします。
    - `/[admin_command] biomes set <player> <biome> [<type>] [<size>]`: ユーザーのバイオーム設定コマンドと同様ですが、バイオームを更新するプレイヤーも指定する必要があります。
    - `/[admin_command] biomes migrate`: バイオームアドオンのデータを移行します。通常は古いバージョンから新しいバージョンへのアップグレード時に使用します。
    - `/[admin_command] biomes unlock <player> <biome_id> [true]`: プレイヤーのアイランドで指定されたバイオームのロックを解除します（末尾に `true` を追加すると購入も行います）。

## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    以下のリストに不足しているものがあれば、お知らせください！

=== "プレイヤー権限"
    - `[gamemode].biomes` (デフォルト: `true`): プレイヤーが GUI を開くバイオームコマンドを使用できます。
    - `[gamemode].biomes.info` (デフォルト: `true`): プレイヤーがバイオーム情報コマンドを使用できます。
    - `[gamemode].biomes.set` (デフォルト: `true`): プレイヤーがバイオーム設定コマンドを使用できます。
    - `[gamemode].biomes.buy` (デフォルト: `true`): プレイヤーがバイオーム購入コマンドを使用できます。

=== "管理者権限"
    - `[gamemode].admin.biomes` (デフォルト: `op`): プレイヤーが GUI を開く管理者バイオームコマンドを使用できます。

## 変更履歴

??? warning "v2.3.0 の新機能 — BentoBox 3.14.0+ と Paper が必要"
    **リリース日：** 2026-05-05

    - ⚙️ **海洋バイオームの保護。** 新しい `change-ocean-biomes` 設定オプション（デフォルト：`false`）が追加され、バイオーム変更が海洋ブロック（`OCEAN`、`WARM_OCEAN`、`DEEP_OCEAN` など）を上書きするのを防ぎます。アイランドの海岸線と水中エリアが保たれます。`true` に設定すれば従来の動作に戻ります。
    - **`COMMAND` パネルアクションタイプ。** パネルボタンがクリック時にコマンドを実行できるようになりました。スタンドアロンのボタンタイプとして、また既存のバイオームボタンのアクションとして `CHANGE`/`BUY`/`ADVANCED_PANEL` と並んで使えます。「アイランドパネルへ戻る」ボタンや任意のカスタム連携に便利です。
    - **再構築された `biomesTemplate.yml`。** 44 種類のバイオーム（以前の約 29 種類から増加）、コスト再調整、9 つの新規バイオーム（マングローブの沼地、Pale Garden（The Creaking モブ含む）、竹のジャングルなど）。3 つのスターターバンドル（Starter、Explorer、Nether & End）と `PER_USAGE` コストの実例を提供。
    - **ゲームモードを意識したアンロック通知。** 正しいゲームモードのワールドにいるプレイヤーには使い慣れたクリック可能な「今すぐ使う」プロンプトが表示され、別のワールドにいるプレイヤーにはバイオームがアンロックされたゲームモード名を含むプレーンなメッセージが表示されます。違うワールドでコマンドを実行する混乱を避けます。
    - **初回起動時のデフォルトバイオーム自動インポート。** ゲームモードにバイオームが設定されていない場合、`biomesTemplate.yml` から自動的にインポートされるようになりました。新規インストールでの手動 `import` 手順が不要に。
    - **アイランド削除/リセット時のバイオームキューのキャンセル。** アイランドが削除またはリセットされると、キューに入っているバイオーム更新タスクと進行中のタスクが `IslandDeleteEvent` と `IslandResettedEvent` でキャンセルされ、進行中のタスクは `AtomicBoolean` フラグにより次のチャンク境界で停止します。
    - 🐛 管理者 GUI ツールチップでの浮動小数点表示の不正確さを修正（例：`0.0299999999329447746` → `0.03`）。
    - 🐛 小数フォーマッターを `Locale.ROOT` に固定し、ドイツ語などコンマ区切りロケールでも `0.5` が `0.5` と表示されるように。
    - 🐛 99 ブロックのスタック上限を超えるバイオームテンプレートのアイテムが、ロード失敗ではなく有効なスタックサイズに分割されるように。
    - 🔡 23 個のロケールファイル、パネル YAML、ハードコードされた Java 文字列を、レガシーな `&` カラーコードから MiniMessage タグへ移行。14 言語の翻訳を新規追加（cs、de、hr、hu、id、it、ko、pt、pt-BR、ro、ru、tr、vi、zh-HK）。

    🔺 **破壊的変更：** このリリースには **BentoBox 3.14.0+**、**Paper**（Spigot は非対応）、**Java 21** が必要です。アドオンは古いバージョンではロードされません。

    🔡 **ロケールに関する注意：** カスタマイズされたロケールファイルは更新が必要です — `&c`/`&l` などを MiniMessage タグ（`<red>`、`<bold>`）に変換するか、カスタマイズを削除してデフォルトを取得してください。

    ⚙️ **設定に関する注意：** `config.yml` で新しい `change-ocean-biomes` オプション（デフォルト `false`）を確認してください。

    [Release v2.3.0](https://github.com/BentoBoxWorld/Biomes/releases/tag/2.3.0)

## 翻訳

{{ translations("Biomes") }}

## API

Biomes 2.0 と BentoBox 1.17 以降、他のプラグインが Biomes アドオンのデータに直接アクセスできます。ただし、アドオンリクエストは依然として多くの依存関係を使用したくないプラグインには良い解決策です。

### Maven 依存関係

Biomes は他のプラグイン向け API を提供しています。これはバージョン 2.1.0 以降に対応しています。

!!! note "注意"
    Maven POM.xml に Biomes 依存関係を追加してください:

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
                <artifactId>biomes</artifactId>
                <version>2.1.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

最新の Biomes バージョンを使用してください。

Biomes の JavaDocs は[こちら](https://ci.codemc.io/job/BentoBoxWorld/job/Biomes/ws/target/apidocs/index.html)で確認できます。

### イベント

=== "BiomeUnlockedEvent"
    !!! summary "説明"
        プレイヤーが新しいバイオームのロックを解除したときにトリガーされるイベントです。

        イベントはキャンセル可能です。イベントをキャンセルするとユーザーの biomesObject ロック解除が防止されます。

        クラスへのリンク: [BiomeUnlockedEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomeUnlockedEvent.java)

    !!! summary "追加バージョン"
        このイベントは Biomes 2.0 バージョンで追加されました。

    !!! question "変数"
        - `@NotNull BiomesObject biomesObject` - ロック解除される biomesObject。
        - `@Nullable User user` - biomesObject のロックを解除するユーザー。
        - `@NotNull Island island` - biomesObject のロックが解除されるアイランド。
        
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.LOW)
        public void onBiomesUnlock(BiomeUnlockedEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();
            
            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();

            event.setCancelled(false);
        }
        ```

=== "BiomePurchasedEvent"
    !!! summary "説明"
        プレイヤーが新しいバイオームを購入したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [BiomePurchasedEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomePurchasedEvent.java)

    !!! summary "追加バージョン"
        このイベントは Biomes 2.0 バージョンで追加されました。

    !!! question "変数"
        - `@NotNull BiomesObject biomesObject` - 購入される biomesObject。
        - `@NotNull User user` - biomesObject を購入するユーザー。
        - `@NotNull Island island` - biomesObject が購入されるアイランド。
        
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBiomesPurchase(BiomePurchasedEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();
            
            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();
        }
        ```

=== "BiomePreChangeEvent"
    !!! summary "説明"
        アイテムを取り除いてエリアのバイオームを変更する前にトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [BiomePreChangeEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomePreChangeEvent.java)

    !!! summary "追加バージョン"
        このイベントは Biomes 2.0 バージョンで追加されました。

    !!! question "変数"
        - `@NotNull BiomesObject biomesObject` - 使用される biomesObject。
        - `@Nullable User user` - バイオーム変更をトリガーするユーザー。
        - `@NotNull Island island` - バイオームが変更されるアイランド。
        - `@NotNull BlockVector minCoordinate` - バイオーム変更の最小座標。
        - `@NotNull BlockVector maxCoordinate` - バイオーム変更の最大座標。
        
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBiomesPreChange(BiomePreChangeEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();
            
            BlockVector minCoordinate = event.getMinCoordinate();
            BlockVector maxCoordinate = event.getMaxCoordinate();
            
            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();

            int minX = event.getMinX();
            int minY = event.getMinY();
            int minZ = event.getMinZ();

            int maxX = event.getMaxX();
            int maxY = event.getMaxY();
            int maxZ = event.getMaxZ();
        }
        ```


=== "BiomeChangedEvent"
    !!! summary "説明"
        エリア全体のバイオームが変更された後にトリガーされるイベントです。バイオーム変更が失敗した場合でもトリガーされます。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [BiomeChangedEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomeChangedEvent.java)

    !!! summary "追加バージョン"
        このイベントは Biomes 2.0 バージョンで追加されました。

    !!! question "変数"
        - `@NotNull BiomesObject biomesObject` - 使用された biomesObject。
        - `@Nullable User user` - バイオーム変更をトリガーしたユーザー。
        - `@NotNull Island island` - バイオームが変更されたアイランド。
        - `@NotNull BlockVector minCoordinate` - バイオーム変更の最小座標。
        - `@NotNull BlockVector maxCoordinate` - バイオーム変更の最大座標。
        - `@Nullable Result result` - バイオーム変更後の結果値。結果値は次のとおりです:
                                        - FINISHED: バイオーム変更が成功しました。
                                        - TIMEOUT: バイオーム変更がタイムアウト値より長くかかり失敗しました。
                                        - FAILED: バイオーム変更が他の理由で失敗しました。

    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBiomeChanged(BiomeChangedEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();
            
            BlockVector minCoordinate = event.getMinCoordinate();
            BlockVector maxCoordinate = event.getMaxCoordinate();
            
            Result result = event.getResult();            

            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();

            int minX = event.getMinX();
            int minY = event.getMinY();
            int minZ = event.getMinZ();

            int maxX = event.getMaxX();
            int maxY = event.getMaxY();
            int maxZ = event.getMaxZ();

            String resultName = event.getResultName();
        }
        ```

### アドオンリクエストハンドラー

BentoBox 1.17 以前は、アドオンのロードに使用するクラスローダーの問題で BentoBox 環境外からのデータアクセスに問題がありました。
これはデータが他のアドオンからのみアクセス可能だったことを意味します。しかし BentoBox が PlAddon 機能を実装したため、リクエストハンドラーはもはや必要ありません。


=== "biome-data"
    !!! summary "説明"
        リクエストされたバイオームに関する全情報を含む `Map<String, Object>` を返します。

    !!! question "入力"
        - `biomeId`: String - リクエストされたバイオームの一意の ID。

    !!! success "出力"
        出力は以下のキーを持つ `Map<String, Object>` です:

        - `uniqueId`: String - リクエストされたバイオームの一意の ID。
        - `world`: String - バイオームが利用可能なワールドの名前。
        - `biome`: String - 対応する Minecraft バイオームの名前。
        - `name`: String - バイオームの表示名。
        - `deployed`: Boolean - バイオームがデプロイされている場合は `true`、そうでない場合は `false`。
        - `description`: List&lt;String&gt; - バイオームの説明。
        - `icon`: ItemStack - GUI でバイオームを表すアイテム。
        - `order`: Integer - 指定されたバイオームの順序番号。
        - `cost`: Integer - バイオームの使用コスト。
        - `level`: Long - バイオームを使用するために必要な最小アイランドレベル。
        - `permissions`: Set&lt;String&gt; - バイオームを使用するために必要な権限のリスト。

    !!! failure "失敗"
        `biomeId` が提供されていないか、`biomeId` がデータベースで見つからない場合、このハンドラーは空のマップを返します。

    !!! example "コード例"
        ```java
        public Map<String, Object> getBiomeData(String biomeId) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Biomes")
                .label("biome-data")
                .addMetaData("biomeId", biomeId)
                .request();
        }
        ```

=== "biomes-list"
    !!! summary "説明"
        指定されたワールドで定義されている全バイオームの uniqueId のリストを返します。

    !!! question "入力"
        - `world-name`: String - ワールドの名前。

    !!! success "出力"
        出力は指定されたワールドで定義されたバイオームの uniqueId のリストを含む `List<String>` です。

    !!! failure "失敗"
        `world-name` が提供されていないか、`world-name` が存在しないかゲームモードワールドでない場合、このハンドラーは空のリストを返します。

    !!! example "コード例"
        ```java
        public List<String> getBiomesList(String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Biomes")
                .label("biomes-list")
                .addMetaData("world-name", worldName)
                .request();
        }
        ```

=== "biome-request-change"
    !!! summary "説明"
        指定されたパラメーターでバイオーム変更をリクエストします。

    !!! question "入力"
        - 必須パラメーター:
            - `player`: UUID - ターゲットプレイヤーの UUID。
            - `world-name`: String - バイオームが変更されるワールドの名前。
            - `biomeId`: String - バイオームの uniqueId。
        - オプションパラメーター:
            - `updateMode`: String - バイオーム変更時に使用するモード。
                                     ISLAND、RANGE、CHUNK のいずれかを指定できます。
                                     （デフォルト: 設定値）
            - `range`: Integer - バイオームが変更される範囲。
                                 （デフォルト: 設定値）
            - `checkRequirements`: Boolean - `true` の場合、プレイヤーは指定されたバイオームの全要件を満たす必要があります。
                                   （デフォルト: true）
            - `withdraw`: Boolean - `true` の場合、プレイヤーの銀行口座からお金が引き出されます。
                          （デフォルト: true）

    !!! success "出力"
        出力は以下のキーを持つ `Map<String, Object>` です:

        - `status`: Boolean - バイオームが正常に変更された場合は `true`、そうでない場合は `false`。
        - `reason`: String - 何が起きたかを説明するメッセージ（変更が成功したかどうかにかかわらず）。

    !!! failure "失敗"
        失敗した場合、このハンドラーは適切な理由と共に `false` をステータスとして返します。

    !!! example "コード例"
        ```java
        public Map<String, Object> requestBiomeChange(UUID player, String worldName, String biomeId, String mode, int range, boolean requirements, boolean withdraw) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Biomes")
                .label("biome-request-change")
                .addMetaData("player", player)
                .addMetaData("world-name", worldName)
                .addMetaData("biomeId", biomeId)
                .addMetaData("updateMode", mode)
                .addMetaData("range", range)
                .addMetaData("checkRequirements", requirements)
                .addMetaData("withdraw", withdraw)
                .request();
        }
        ```
