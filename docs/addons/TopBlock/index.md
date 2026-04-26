# TopBlock

AOneBlock 専用のアイランドレベルを計算する BentoBox 用アドオンです。ランクは採掘されたマジックブロックの数（カウント）によって決まります。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("TopBlock") }}

## インストール

1. TopBlock アドオンの jar を BentoBox プラグインの addons フォルダに配置します
2. サーバーを再起動します
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます
4. config.yml を希望通りに編集します
5. 変更した場合はサーバーを再起動します

## 設定

TopBlock アドオンには 2 つの全般的な設定があります:

- config.yml ファイルにはアドオンのデフォルト設定が含まれます。
- /panels/ にはプレイヤー GUI を管理するファイルが含まれます。

### config.yml

設定ファイルにはアドオンの主要な機能が含まれます。

最新の config.yml は[こちら](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/config.yml)で確認できます。

このセクションではアドオンの全般的な設定を定義します。

??? note "refresh-time"
    トップ 10 が更新される頻度（分単位）。最小は 1 分、デフォルトは 5 分です。
    更新のたびにデータベースからすべてのアイランドを読み込む必要があるため、頻繁に実行しないでください。

    デフォルト: `5`

??? note "shorthand"
    アイランドレベル数値を短縮表示できます。

    大きなレベル値を切り捨て表示します。例: 10,345 → 10k

    デフォルト: `false`

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装できる機能が導入されました。できるだけシンプルなカスタマイズを目指しましたが、一部の機能には説明が必要です。
BentoBox カスタム GUI の詳細はこちらをご覧ください: [Custom GUI's](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
     アドオンは `/plugins/bentobox/addons/topblock` の下に `panels` という名前のディレクトリを作成します。

    現在カスタマイズ可能な GUI:

    - トップパネル: `top_panel` - トップ 10 のアイランドを表示します。

??? question "`TOP` ボタンタイプとは何ですか？"
    このボタンは top_panel で利用可能です。アイランドトップの X 位のアイランドを表示します。
    
    `icon` はデフォルトで適切なプレイヤースキンの `PLAYER_HEAD` になります。有効にすると指定したマテリアルに置き換えられます。

    データフィールドの `index` では、現在のスポットに表示するトップ 10 の順位を指定できます。

    トップパネルには追加アドオンが必要な 2 つのアクションがあります:
    
    - `warp` - Warps アドオンが必要です。プレイヤーのアイランドにワープサインが存在する場合のみ表示されます。
    - `visit` - Visit アドオンが必要です。プレイヤーのアイランドへの訪問が許可されている場合のみ表示されます。

    Fallback では、トップスポットにプレイヤーがいない場合のバックグラウンドアイコンを変更できます。

    例:
    ```yaml
        #icon: PLAYER_HEAD
        title: topblock.gui.buttons.island.name
        description: topblock.gui.buttons.island.description
        data:
          type: TOP
          index: 1
        actions:
          warp:
            click-type: LEFT
            tooltip: topblock.gui.tips.click-to-warp
          visit:
            click-type: RIGHT
            tooltip: topblock.gui.tips.right-click-to-visit
        fallback:
          icon: LIME_STAINED_GLASS_PANE
          title: topblock.gui.buttons.island.empty
    ```

??? question "`VIEW` ボタンタイプとは何ですか？"
    このボタンは top_panel で利用可能です。閲覧者のアイランドの TopBlock 値を表示します。

    `icon` はデフォルトで適切なプレイヤースキンの `PLAYER_HEAD` になります。有効にすると指定したマテリアルに置き換えられます。
    
    `view` アクションはプレイヤーのアイランドの詳細メニューを表示します。

    例:
    ```yaml
        #icon: PLAYER_HEAD
        title: topblock.gui.buttons.island.name
        description: topblock.gui.buttons.island.description
        data:
          type: VIEW
        actions:
          view:
            click-type: unknown
            tooltip: topblock.gui.tips.click-to-view
    ```

## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。

=== "プレイヤーコマンド"
    - `/[player_command] topblock`: トップパネルにアクセスします。`aoneblock.island.topblock` 権限が必要です。

## 権限

=== "プレイヤー権限"
    - `aoneblock.island.topblock` - (デフォルト: `true`) - プレイヤーが `/[player_command] top` コマンドを使用できます。
    - `aoneblock.intopten` - (デフォルト: `true`) - プレイヤーのアイランドがトップテンに表示されるかどうかを制御します。管理者やテスターからこの権限を削除するとランキングから除外されます。

??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    もし本当に不足しているものがあれば、お知らせください！


## プレースホルダー

{{ placeholders_source(source="TopBlock") }}

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/TopBlock/issues)のリストに追加してください。

## 変更履歴

??? warning "v2.0.0 の新機能 — プラットフォームアップグレードが必要"
    **リリース日：** 2026-04-26

    - 🐛 **トップテンパネルが修正されました。** 長年のバグにより、トップテンパネルに空の緑色のプレースホルダーしか表示されていませんでした。イベントハンドラーが `private` だったため Bukkit に無視されていましたが、修正済み — プレイヤーのスキンと統計が正しく表示されます。
    - ✨ **`aoneblock.intopten` 権限。** この権限（デフォルトで全プレイヤーに付与）を削除することで、管理者やテスターをトップテンから除外できます。
    - 🔡 **22 の新しいロケール** — cs, de, es, fr, hr, hu, id, it, ja, ko, lv, nl, pl, pt, pt-BR, ro, ru, tr, uk, vi, zh-CN, zh-HK。
    - 🔺 **Paper 1.21.x**、**Java 21**、**BentoBox 3.14.0+**、**AOneBlock 1.18.0+** が必要になりました。Spigot はサポートされなくなりました。

    🔺 再起動前に **`addons/TopBlock/panels/top_panel.yml` を削除**して、更新されたパネルテンプレートが展開されるようにしてください。その後、カスタムレイアウトを再適用してください。

    🔡 更新後に `/bentobox reload` を実行して、BentoBox が新しいロケールキーを既存のファイルにマージできるようにしてください。

    [Release v2.0.0](https://github.com/BentoBoxWorld/TopBlock/releases/tag/2.0.0)

## 翻訳

{{ translations("TopBlock") }}

## API

### Maven 依存関係
TopBlock は他のプラグイン向けの API を提供しています。

!!! note "注意"
    Maven POM.xml に TopBlock の依存関係を追加します:

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
                <artifactId>topblock</artifactId>
                <version>1.0.1</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

TopBlock の JavaDocs は[こちら](https://ci.codemc.io/job/BentoBoxWorld/job/TopBlock/ws/target/apidocs/index.html)で確認できます。
