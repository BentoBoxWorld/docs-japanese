# Challenges

**Challenges** はプレイヤーが**様々なカスタマイズ可能なチャレンジを完了して報酬を受け取れる**ようにします！

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("Challenges") }}

## インストール

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. 管理者チャレンジコマンド（例: `/bsbadmin challenges`）を実行してアドオンを設定します。

## 設定

デフォルトでは、チャレンジアドオンにはチャレンジやレベルが含まれていません。初回起動時は管理者 GUI のみアクセスできます。
管理者は独自のチャレンジを作成するか、デフォルトのチャレンジセットをロードできます。デフォルトのチャレンジには 5 つのレベルと 57 のチャレンジが含まれています。
また、管理者が公開チャレンジをダウンロードできるウェブライブラリもあります。管理者 GUI のウェブアイコンをクリックしてアクセスできます。

### config.yml

設定ファイルにはアドオンのメイン機能が含まれています。

最新の config.yml は[こちら](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/config.yml)で確認できます。

### テンプレート

チャレンジアドオンにはチャレンジをデータベースにインポートするために使用できるテンプレートファイルが含まれています。このファイルはゲーム内 GUI を使用したくない方のための一括チャレンジ追加に便利です。ただし、テンプレートファイルでは全機能が利用できるわけではなく、一部のアイテム/オプションは GUI からのみ追加できます。
テンプレートファイルはいくつでも用意できます。管理者 GUI でどれをインポートするか選択できます。
テンプレートファイルの例: [template.yml](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/template.yml)

!!! tip "ヒント"
    テンプレートファイルにはチャレンジとレベルの両方が含まれている必要があります。どちらかがないと機能しません。

??? question "チャレンジタイプとは何ですか？"
    チャレンジアドオンには 4 つの異なるチャレンジタイプがあります。各タイプはチャレンジを完了とマークするために異なる条件をテストします。これらのタイプは次のとおりです:
    
    - インベントリチャレンジ（`INVENTORY_TYPE`）- プレイヤーインベントリのアイテムが必要なチャレンジ。
    - アイランドチャレンジ（`ISLAND_TYPE`）- プレイヤーのアイランド上のブロックまたはエンティティが必要なチャレンジ。
    - その他チャレンジ（`OTHER_TYPE`）- プレイヤーの XP、お金、またはアイランドレベルが必要なチャレンジ。
    - 統計チャレンジ（`STATISTIC_TYPE`）- プレイヤーの統計から特定の値が必要なチャレンジ。

??? question "必要/報酬アイテムにエンチャントを指定できますか？"
    残念ながら Spigot には汎用的なアイテム解析の仕組みがありません。そのためプラグイン作者は独自のものを作成する必要があります。チャレンジアドオンは BentoBox の [アイテムパーサー](/en/latest/BentoBox/ItemParser/)を使用します。それでサポートされていない機能は使用できません。ただし、ゲーム内の管理者 GUI を使用すれば、制限なくあらゆるアイテムを設定できます。

??? question "統計チャレンジタイプに設定できる値はどこで確認できますか？"
    統計タイプはここで確認できます: [Statistic](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Statistic.html)。
    
    一部の情報は fandom サイトで確認できます: [minecraft.fandom](https://minecraft.fandom.com/wiki/Statistics)
    
    ただし、指定できる内容を全て確認できる場所はありません。統計チャレンジの作成にはゲーム内の管理者 GUI を使用することをお勧めします。より多くのオプションがあり、どのフィールドに何を入力できるかを検出できます。

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装する機能が導入されました。チャレンジアドオンはその機能を使用する最初のアドオンの一つです。カスタマイズをできる限りシンプルにしようとしましたが、一部の機能については説明が必要です。
BentoBox カスタム GUI の詳細はこちらを参照してください: [カスタム GUI](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    チャレンジアドオンの GUI をカスタマイズするにはバージョン 1.0 が必要です。これが実装された最初のバージョンです。アドオンは `/plugins/bentobox/addons/challenges` の下に `panels` というディレクトリを作成します。
    
    現在カスタマイズできる GUI は 3 つです:

    - メインチャレンジパネル: `main_panel` - プレイヤーがチャレンジの一覧を見ることができるパネル。
    - 複数完了パネル: `multiple_panel` - プレイヤーがチャレンジを完了する回数を指定できるパネル。
    - ゲームモード選択パネル: `gamemode_panel` - 設定で `commands.global-command` が有効で複数のゲームモードがインストールされている場合に開くパネル。

    各 GUI にはそれぞれに固有の機能があります。

??? question "`PREVIOUS`|`NEXT` ボタンタイプとは何ですか？"
    このボタンは main_panel と gamemode_panel で利用できます。
    PREVIOUS と NEXT ボタンタイプは、GUI のスペースより多くのチャレンジがある場合に自動ページングを作成できます。
    これらのタイプには data の下に追加パラメーターがあります:
    - `target` - main_panel では `LEVEL` または `CHALLENGE`、gamemode_panel では `GAMEMODE` を切り替えるかどうかを示します。
    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

    例: 
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: challenges.gui.buttons.previous.name
        description: challenges.gui.buttons.previous.description
        data:
          type: PREVIOUS
          target: CHALLENGE
          indexing: true
        action:
          left:
            tooltip: challenges.gui.tips.click-to-previous
    ```

??? question "`CHALLENGE` ボタンタイプとは何ですか？"
    このボタンは main_panel で利用できます。
    CHALLENGE ボタンはチャレンジの動的エントリを作成します。チャレンジが存在する場合のみボタンが表示されます。例えば 3 つのチャレンジしかないのに GUI に 7 つのスペースを定義した場合、3 つのスペースのみ埋まります。残りのスペースは空になります。

    デフォルトではチャレンジは順序番号でソートされますが、data の下の `id` パラメーターで特定のレベルを特定のスロットに指定することもできます。
    
    ```yaml
      data:
        type: CHALLENGE
        id: example_challenge
    ```

    タイトル、説明、アイコンを指定するとデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    このボタンは 3 つの異なるアクションタイプをサポートします:

    - COMPLETE - チャレンジを 1 回完了します。
    - COMPLETE_MAX - チャレンジを可能な限り多く完了します。
    - MULTIPLE_PANEL - 何回完了するか選択できる複数完了パネルを開きます。

    例: 
    ```yaml
      data:
        type: CHALLENGE
      actions:
        left:
          type: COMPLETE
          tooltip: challenges.gui.tips.click-to-complete
        right:
          type: MULTIPLE_PANEL
          tooltip: challenges.gui.tips.right-click-multiple-open
        shift_left:
          type: COMPLETE_MAX
          tooltip: challenges.gui.tips.shift-left-click-to-complete-all
    ```


??? question "`LEVEL` ボタンタイプとは何ですか？"
    このボタンは main_panel で利用できます。
    LEVEL ボタンはチャレンジレベルの動的エントリを作成します。レベルが存在する場合のみボタンが表示されます。例えば 3 つのレベルしかないのに GUI に 7 つのスペースを定義した場合、3 つのスペースのみ埋まります。残りのスペースは空になります。

    デフォルトではレベルは進行順にソートされますが、data の下の `id` パラメーターで特定のレベルを特定のスロットに指定することもできます。
    
    ```yaml
      data:
        type: LEVEL
        id: example_level
    ```

    タイトル、説明、アイコンを指定するとデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    
    例: 
    ```yaml
      data:
        type: LEVEL
      actions:
        left:
          tooltip: challenges.gui.tips.click-to-select
    ```
    
??? question "`UNASSIGNED_CHALLENGES` ボタンタイプとは何ですか？"
    このボタンは main_panel で利用できます。
    UNASSIGNED_CHALLENGES ボタンはフリーチャレンジ用のボタンを選択できます。
    追加機能や動的生成はありません。

??? question "`GAMEMODE` ボタンタイプとは何ですか？"
    このボタンは gamemode_panel で利用できます。
    Challenges がインストールされている各ゲームモードアドオンのボタンを生成します。

??? question "`INCREASE`|`REDUCE` ボタンタイプとは何ですか？"
    このボタンは multiple_panel で利用できます。
    これらのタイプはチャレンジ完了回数を増加/減少させます。

    `data` の下に `value: <number>` を指定することで、異なるカスタム増減数を設定できます。

??? question "`ACCEPT` ボタンタイプとは何ですか？"
    このボタンは multiple_panel で利用できます。
    このタイプは入力数を受け入れてチャレンジをその回数完了させます。

    アクションの下に `type: ACCEPT` を指定するとチャレンジを完了します。 
    アクションの下に `type: INPUT` を指定するとプレイヤーにチャットで数値を入力させます。

## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。

=== "プレイヤーコマンド"
    - `/challenges`: プレイヤーチャレンジ GUI にアクセスします。現在のワールドのチャレンジまたはチャレンジが有効なワールドの一覧が表示されます。設定で有効にする必要があります。
    - `/[player_command] challenges [challenge] [number]`: BSkyBlock プレイヤーチャレンジ GUI にアクセスします。チャレンジ名が指定された場合、そのチャレンジを 1 回完了します。数値が指定された場合、チャレンジを 0〜指定回数完了します。

=== "管理者コマンド"
    - `/challengesadmin`: 管理者チャレンジ GUI にアクセスします。チャレンジが有効なワールドの一覧が表示されます。設定で有効にする必要があります。
    - `/[admin_command] challenges`: BSkyBlock 管理者チャレンジ GUI にアクセスします。
    - `/[admin_command] challenges reload [hard]`: チャレンジアドオンの設定をリロードできます。このメソッドはキャッシュデータもクリアします。`hard` パラメーターを指定するとデータベース接続をリセットできます。

## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "プレイヤー権限"
    - `[gamemode].challenges` - (デフォルト: `true`) - プレイヤーが '/[player_command] challenges' コマンドを使用できます。
    - `[gamemode].challenges.multiple` - (デフォルト: `true`) - プレイヤーが一度に複数回チャレンジを完了できます。
    - `[gamemode].challenges.complete` - (デフォルト: `false`) - プレイヤーが '/[player_command] challenges complete <challenge> <number>' コマンドを使用できます。
    - `addon.challenges` - (デフォルト: `true`) - 設定で有効な場合 '/challenges' コマンドへのアクセスを許可します。
    - `[gamemode].command.challengeexempt` - (デフォルト: `false`) - プレイヤーへの報酬コマンド実行をブロックできます。

=== "管理者権限"
    - `[gamemode].admin.challenges` - (デフォルト: `op`) - プレイヤーが '/[admin_command] challenges' コマンドを使用できます。
    - `[gamemode].admin.challenges.complete` - (デフォルト: `op`) - プレイヤーが '/[admin_command] challenges complete' コマンドを使用できます。
    - `[gamemode].admin.challenges.reset` - (デフォルト: `op`) - プレイヤーが '/[admin_command] challenges reset' コマンドを使用できます。
    - `addon.admin.challenges` - (デフォルト: `op`) - 設定で有効な場合 '/challengesadmin' コマンドへのアクセスを許可します。

??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    以下のリストに不足しているものがあれば、お知らせください！


## プレースホルダー

{{ placeholders_source(source="Challenges") }}

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/Challenges/issues)のリストに追加してください。

??? question "新しいチャレンジを追加するにはどうすればいいですか？"
    公式な方法は管理者 GUI またはテンプレートファイルでチャレンジを追加することです。
    テンプレートファイルは管理者 GUI の適切なアイコン（「テンプレートのインポート」）を使用した後にのみインポートされます。GUI でどのテンプレートをゲームモードにインポートするか選択できます。 
    
    ただし、エクスポートされたデータベースファイルを編集するオプションもあります。`/[admin_command] challenges` から「データベースのエクスポート」ボタンをクリックしてファイルにエクスポートできます。

??? question "アイランドごとにチャレンジを有効にできますか？すべてのアイランドメンバーが同じチャレンジを持つように。"
    はい、アドオンの設定ファイルで設定できます: `store-island-data: true`

??? question "プレイヤーごとにチャレンジを有効にできますか？"
    はい、アドオンの設定ファイルで設定できます: `store-island-data: false`

??? question "報酬コマンドが機能しません。なぜですか？"
    最も可能性が高い原因は、定義が正しくないことです。コマンドの前に `/` 記号は不要です。
    
    プレイヤーの視点からコマンドを実行したい場合は、コマンド呼び出しの前に `[SELF]` を追加する必要があります。例: `[SELF] kill` はプレイヤーが `/kill` コマンドを呼び出す結果になります。

    権限が原因である場合もあります。`[gamemode].command.challengeexempt` はプレイヤーがコマンドを実行するのを防ぎます。プレイヤーがこの権限を持っていないか確認してください。

??? question "報酬コマンドにプレースホルダーを追加するにはどうすればいいですか？"
    現在、アドオンは報酬コマンドにプレースホルダーをサポートしていません。必要な場合は GitHub でリクエストできます。
    
    現在報酬コマンドでサポートされている唯一のプレースホルダーは `[player]` で、チャレンジを完了したプレイヤーの名前を返します。

??? question "チャレンジの説明の要素の順序が気に入りません。変更できますか？"
    はい、要素の順序はアドオンのロケールファイルで定義されています。

    [チャレンジの説明](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/locales/en-US.yml#L852-L994)
    [レベルの説明](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/locales/en-US.yml#L995-L1042)

    lore の部分を切り替えたり削除したりすると、表示される要素の順序が変わります。

    ```yaml
        lore: |-
            [description]
            [status]
            [cooldown]
            [requirements]
            [rewards]
    ```

    これらの各部分は以下のタグによって生成されており、それらも変更できます。例えば [status] 部分は次から生成されます:

    ```yaml
    status:
        # Status message for completed unrepeatable challenge
        completed: "&2&l Completed"
        # Status message that contains number of completions for unlimited repeatable challenge
        completed-times: "&2 Completed &7&l [number] &r&2 time(-s)"
        # Status message that contains number of completions from max available for repeatable challenge
        completed-times-of: "&2 Completed &7&l [number] &r&2 out of &7&l [max] &r&2 times"
        # Status message that indicates that max completion count reached for repeatable challenge
        completed-times-reached: "&2&l Completed all &7 [max] &2 times"
    ```

## 変更履歴

??? warning "v1.6.0 の新機能 — ロケールの再生成が必要"
    **リリース日:** 2026-04-13

    - 🔡 **全ロケールファイルを MiniMessage に移行しました。** 全てのロケールファイルがレガシーの `&` カラーコードから MiniMessage タグに変換されました。`BentoBox/locales/Challenges/` を削除してサーバーを再起動し、更新されたファイルを再生成してください。
    - 新しいチャレンジメニュー設定（@stuffyerface 提供）。
    - ウェブライブラリパネルの改善: 言語フィルターの追加、説明の折り返し表示、カタログダウンロード中のローディングインジケーター表示、不正なカタログエントリの適切な処理。
    - チャレンジとレベルの lore の報酬テキストに折り返しを適用してよりきれいに表示。
    - **新しいダウンロード可能なチャレンジライブラリ**がゲーム内のウェブライブラリから利用可能:
        - **Skyblock** — 複数の進行パスを持つモダンなスカイブロックチャレンジ（EN、ZH-CN、DE、ES、RU、FR）
        - **AcidIsland** — Shipwrecked から Admiral までの海洋チャレンジ進行（EN、ZH-CN、DE、ES、RU、FR）
        - **Poseidon** — Poseidon ゲームモードのデフォルトチャレンジ（EN、ZH-CN、DE、ES、RU、FR）
    - BentoBox API 3.12.0+ が必要です。

    [Release v1.6.0](https://github.com/BentoBoxWorld/Challenges/releases/tag/1.6.0)

## 翻訳

!!! info "チャレンジの翻訳について"
    翻訳にはチャレンジ自体は含まれません。
    各チャレンジにはエンドユーザーの設定プロセスをできる限りシンプルにするために、ローカライズされない独自の「表示名」と「説明」があります。  
    ただし、GitHub の[オンラインチャレンジライブラリ](https://github.com/BentoBoxWorld/weblink/tree/master/challenges/library)で様々なチャレンジの翻訳を見つけたり提供したりできます。

    ロケール[ファイル](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/locales/en-US.yml#L1248-L1270)を通じて一部を翻訳するオプションもあります。

{{ translations("Challenges") }}

## API

Challenges 1.0 と BentoBox 1.17 以降、他のプラグインが Challenges アドオンのデータに直接アクセスできます。ただし、アドオンリクエストは依然として多くの依存関係を使用したくないプラグインには良い解決策です。

### Maven 依存関係

Challenges は他のプラグイン向け API を提供しています。これはバージョン 1.1.0 以降に対応しています。

!!! note "注意"
    Maven POM.xml に Challenges 依存関係を追加してください:

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
                <artifactId>challenges</artifactId>
                <version>1.1.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

最新の Challenges バージョンを使用してください。

Challenges の JavaDocs は[こちら](https://ci.codemc.io/job/BentoBoxWorld/job/Challenges/ws/target/apidocs/index.html)で確認できます。

### イベント

BentoBox 1.17 API はクラスローダーの問題を解決する機能を実装しました。イベントを直接使用したいプラグインは今すぐできます。

=== "ChallengeCompletedEvent"
    !!! summary "説明"
        プレイヤーがチャレンジを完了したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [ChallengeCompletedEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/ChallengeCompletedEvent.java)


    !!! question "変数"
        - `String challengeId` - 完了したチャレンジの ID。
        - `UUID user` - チャレンジを完了したプレイヤーの ID。
        - `Boolean admin` - チャレンジが管理者によって完了されたかどうかを示します。
        - `Integer completionCount` - チャレンジ完了回数。
        
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(ChallengeCompletedEvent event) {
            UUID user = event.getPlayerUUID();
            String challenge = event.getChallengeID();
            boolean isAdmin = event.isAdmin();
            int count = event.getCompletionCount();
        }
        ``` 

=== "LevelCompletedEvent"
    !!! summary "説明"
        プレイヤーがレベルを完了したときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [LevelCompletedEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/LevelCompletedEvent.java)


    !!! question "変数"
        - `String levelId` - 完了したレベルの ID。
        - `UUID user` - レベルを完了したプレイヤーの ID。
        - `Boolean admin` - レベルが管理者によって完了されたかどうかを示します。
        
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(LevelCompletedEvent event) {
            UUID user = event.getPlayerUUID();
            String levelId = event.getLevelID();
            boolean isAdmin = event.isAdmin();
        }
        ``` 

=== "ChallengeResetAllEvent"
    !!! summary "説明"
        プレイヤーの全チャレンジがリセットされたときにトリガーされるイベントです。チャレンジレベルデータも含まれます。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [ChallengeResetAllEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/ChallengeResetAllEvent.java)

    !!! question "変数"
        - `String worldName` - チャレンジがリセットされたワールドの名前。
        - `UUID playerUUID` - ターゲットプレイヤーの ID。
        - `Boolean admin` - リセットが管理者によって行われたかどうかを示します。
        - `String reason` - リセットの理由が含まれます。

    !!! warning "定数値"
        - `reason` - プレイヤーによる場合は "ISLAND_RESET"、管理者による場合は "RESET_ALL" に設定されます。

    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(ChallengeResetAllEvent event) {
            UUID user = event.getPlayerUUID();
            String worldName = event.getWorldName();
            boolean isAdmin = event.isAdmin();
            String reason = event.getReason();
        }
        ``` 

=== "ChallengeResetEvent"
    !!! summary "説明"
        チャレンジが管理者によってリセットされたときにトリガーされるイベントです。

        このイベントは情報提供のみです。キャンセルできません。

        クラスへのリンク: [ChallengeResetEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/ChallengeResetEvent.java)

    !!! question "変数"
        - `String challengeID` - リセットされたチャレンジの ID。
        - `UUID playerUUID` - ターゲットプレイヤーの ID。
        - `Boolean admin` - チャレンジが管理者によってリセットされたかどうかを示します。
        - `String reason` - リセットの理由が含まれます。

    !!! warning "定数値"
        - `admin` - true に設定されます。非管理者による単一チャレンジのリセットはまだ実装されていません。
        - `reason` - "RESET" に設定されます。

    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(ChallengeResetEvent event) {
            UUID user = event.getPlayerUUID();
            String challengeId = event.getChallengeID();
            boolean isAdmin = event.isAdmin();
            String reason = event.getReason();
        }
        ```

### アドオンリクエストハンドラー

BentoBox 1.17 以前は、アドオンのロードに使用するクラスローダーの問題で BentoBox 環境外からのデータアクセスに問題がありました。
これはデータが他のアドオンからのみアクセス可能だったことを意味します。しかし BentoBox が PlAddon 機能を実装したため、リクエストハンドラーはもはや必要ありません。

アドオンリクエストハンドラーの詳細は[こちら](/en/latest/BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons/)をご覧ください。

=== "challenge-list"
    !!! summary "説明"
        指定されたワールドで定義されている全チャレンジの uniqueId のリストを返します。

    !!! question "入力"
        - `world-name`: String - ワールドの名前。

    !!! success "出力"
        出力は指定されたワールドで定義されたチャレンジの uniqueId のリストを含む `List<String>` です。

    !!! failure "失敗"
        `world-name` が提供されていないか、`world-name` が存在しないかゲームモードワールドでない場合、このハンドラーは空のリストを返します。

    !!! example "コード例"
        ```java
        public List<String> getChallenges(String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("challenge-list")
                .addMetaData("world-name", worldName)
                .request();
        }
        ```

=== "challenge-data"
    !!! summary "説明"
        リクエストされたチャレンジに関する全情報を含む `Map<String, Object>` を返します。

    !!! question "入力"
        - `challenge-name`: String - リクエストされたチャレンジの一意の ID。

    !!! success "出力"
        出力は以下のキーを持つ `Map<String, Object>` です:

        - `uniqueId`: String - リクエストされたチャレンジの一意の ID。
        - `name`: String - チャレンジの表示名。
        - `icon`: ItemStack - GUI でチャレンジを表すアイテム。
        - `levelId`: String - リクエストされたチャレンジが割り当てられているレベルの uniqueId。
        - `order`: Integer - 指定されたチャレンジの順序番号。
        - `deployed`: Boolean - チャレンジがデプロイされている場合は `true`、そうでない場合は `false`。
        - `description`: List&lt;String&gt; - チャレンジの説明。
        - `type`: String - リクエストされたチャレンジタイプの名前。
        - `repeatable`: Boolean - チャレンジが繰り返し可能な場合は `true`、そうでない場合は `false`。
        - `maxTimes`: Integer - リクエストされたチャレンジの最大完了回数。

    !!! failure "失敗"
        `challengeId` が提供されていないか、`challengeId` がデータベースで見つからない場合、このハンドラーは空のマップを返します。

    !!! example "コード例"
        ```java
        public Map<String, Object> getChallengeDataMap(String challengeId) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("challenge-data")
                .addMetaData("challenge-name", challengeId)
                .request();
        }
        ```

=== "level-list"
    !!! summary "説明"
        指定されたワールドで定義されている全レベルの uniqueId のリストを返します。

    !!! question "入力"
        - `world-name`: String - ワールドの名前。

    !!! success "出力"
        出力は指定されたワールドで定義されたレベルの uniqueId のリストを含む `List<String>` です。

    !!! failure "失敗"
        `world-name` が提供されていないか、`world-name` が存在しないかゲームモードワールドでない場合、このハンドラーは空のリストを返します。

    !!! example "コード例"
        ```java
        public List<String> getChallengeLevels(String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("level-list")
                .addMetaData("world-name", worldName)
                .request();
        }
        ```

=== "level-data"
    !!! summary "説明"
        リクエストされたレベルに関する全情報を含む `Map<String, Object>` を返します。

    !!! question "入力"
        - `level-name`: String - リクエストされたレベルの一意の ID。

    !!! success "出力"
        出力は以下のキーを持つ `Map<String, Object>` です:

        - `uniqueId`: String - リクエストされたレベルの一意の ID。
        - `name`: String - レベルの表示名。
        - `icon`: ItemStack - GUI でレベルを表すアイテム。
        - `world`: String - レベルが機能するワールド名。
        - `order`: Integer - 指定されたレベルの順序番号。
        - `message`: String - 指定されたレベルのアンロックメッセージ。
        - `waiveramount`: Integer - アンロック前に未完了のままにできるチャレンジ数。
        - `challenges`: List&lt;String&gt; - 割り当てられたチャレンジの ID のリスト。

    !!! failure "失敗"
        `levelId` が提供されていないか、`levelId` がデータベースで見つからない場合、このハンドラーは空のマップを返します。

    !!! example "コード例"
        ```java
        public Map<String, Object> getChallengeLevelData(String levelId) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("level-data")
                .addMetaData("level-name", levelId)
                .request();
        }
        ```

=== "completed-challenges"
    !!! summary "説明"
        指定されたワールドで定義され、指定されたプレイヤーによって完了された全チャレンジの uniqueId のリストを返します。

    !!! question "入力"
        - `player`: UUID - プレイヤーの UUID。
        - `world-name`: String - ワールドの名前。

    !!! success "出力"
        出力は指定されたワールドでプレイヤーによって完了されたチャレンジの uniqueId のセットを含む `Set<String>` です。

    !!! failure "失敗"
        `world-name` が提供されていないか、`world-name` が存在しないかゲームモードワールドでない場合、このハンドラーは空のセットを返します。
        `player` が提供されていないか、`player` が存在しない場合、このハンドラーは空のセットを返します。

    !!! example "コード例"
        ```java
        public List<String> getCompletedChallenges(UUID playerUUID, String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("completed-challenges")
                .addMetaData("player", playerUUID)
                .addMetaData("world-name", worldName)
                .request();
        }
        ```
