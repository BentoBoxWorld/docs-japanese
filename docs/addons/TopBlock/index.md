# TopBlock

マジックブロックゲームモード用のトップテンランキングを生成する BentoBox 用アドオンです。ランクは採掘されたマジックブロックの数（カウント）によって決まります。

TopBlock は [**AOneBlock**](../../gamemodes/AOneBlock/index.md) と [**ChunkBlock**](../../gamemodes/ChunkBlock/index.md) をサポートしています。どちらか一方、または両方をインストールできます — 両方が存在する場合、各ゲームモードは独自の完全に分離されたトップテン、独自の `topblock` コマンド、および独自のプレースホルダーセットを取得します。AOneBlock でのプレイヤーの立場は ChunkBlock での立場に影響しません。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("TopBlock") }}

## インストール

1. TopBlock アドオンの jar を BentoBox プラグインの addons フォルダに配置します
2. サーバーを再起動します
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます
4. config.yml を希望通りに編集します
5. 変更した場合はサーバーを再起動します

!!! note "TopBlock はスタンドアロンではありません"
    TopBlock には [AOneBlock](../../gamemodes/AOneBlock/index.md) または [ChunkBlock](../../gamemodes/ChunkBlock/index.md) **の少なくとも 1 つ**が一緒にインストールされている必要があります。どちらも見つからない場合、TopBlock はエラーを記録して自身を無効にします。起動時に見つかったゲームモードをフックするため、後でゲームモードをインストールまたは削除すると、再起動後にのみ有効になります。

## 設定

TopBlock アドオンには 2 つの全般的な設定があります:

- config.yml ファイルにはアドオンのデフォルト設定が含まれます。
- /panels/ にはプレイヤー GUI を管理するファイルが含まれます。

### config.yml

設定ファイルにはアドオンの主要な機能が含まれます。

最新の config.yml は[こちら](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/config.yml)で確認できます。

このセクションではアドオンの全般的な設定を定義します。これらの設定はグローバルです — TopBlock がフックしたすべてのゲームモードに適用されます。ゲームモードごとの設定はありません。

??? note "refresh-time"
    トップ 10 が更新される頻度（分単位）。最小は 1 分、デフォルトは 5 分です。
    更新のたびにデータベースからすべてのフックされたゲームモードのアイランドを読み込む必要があります（2.1.1 以降はその読み込みはメインスレッドの外で実行されるため、ラグスパイクが起きなくなりました）。AOneBlock と ChunkBlock の両方を実行している場合、各更新は両方のアイランドセットを読み込むため、デフォルトのままにするか、または上げることを検討してください。

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
    - `/[player_command] topblock`: トップパネルにアクセスします。そのゲームモードの `island.topblock` 権限が必要です（`aoneblock.island.topblock` または `chunkblock.island.topblock`）。

TopBlock はフックされた**各**ゲームモードで `topblock` サブコマンドを登録するため、両方がインストールされている場合、AOneBlock 向けに `/ob topblock`、ChunkBlock 向けに同等のコマンドが得られます。各パネルは実行したワールドのゲームモードを開きます — 2 つのランキングは完全に分離されています。

## 権限

=== "プレイヤー権限"
    - `aoneblock.island.topblock` - (デフォルト: `true`) - プレイヤーが AOneBlock で `/[player_command] topblock` コマンドを使用できます。
    - `aoneblock.intopten` - (デフォルト: `true`) - プレイヤーのアイランドが AOneBlock トップテンに表示されるかどうかを制御します。ランキングから除外するには管理者やテスターからこの権限を削除してください。
    - `chunkblock.island.topblock` - (デフォルト: `true`) - プレイヤーが ChunkBlock で `/[player_command] topblock` コマンドを使用できます。
    - `chunkblock.intopten` - (デフォルト: `true`) - プレイヤーのアイランドが ChunkBlock トップテンに表示されるかどうかを制御します。

??? question "プレイヤーをランキングから非表示にするには？"
    非表示にしたいゲームモードから `intopten` 権限を削除（またはネゲート）してください — `aoneblock.intopten` または `chunkblock.intopten`。プレフィックスがゲームモードごとなので、1 つのランキングから非表示にしながら、別のランキングには表示させたままにできます。

    注意すべき 2 つのこと：

    - 権限は島の**所有者がオンラインの場合**にのみチェックされます。オフライン所有者は常に含まれます。Bukkit はログインしていないプレイヤーの権限を確実に評価することができないためです。別のアカウント（alt）ではなく、実際にログインするアカウントから権限を削除してください。
    - チェックされるのは**島所有者の**権限のみです。チームメンバーの権限は違いを作りません。

    変更は次の更新時に有効になるため、島がリストから削除されるまで最大 `refresh-time` 分待つことができます。

??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    もし本当に不足しているものがあれば、お知らせください！


## プレースホルダー

プレースホルダーはフックされたゲームモードごとに別々に登録され、そのゲームモード独自のプレフィックスを使用します。ChunkBlock がインストールされている場合にのみ `chunkblock_` セットが存在し、ChunkBlock 独自のランキングを報告します — 2 つが混在することはありません。

{{ placeholders_source(source="TopBlock") }}

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/TopBlock/issues)のリストに追加してください。

## 変更履歴

??? note "v2.1.1 の新機能"
    **リリース日:** 2026-08-27

    パッチリリース — 設定、ロケール、データ形式の変更なし。2.1.0 の直接置き換え。

    - 🐛 **トップテン更新がメインスレッドをもう止めなくなりました。** 更新タスク（`refresh-time` 分ごと、デフォルト 5）はゲームモードの島データベース全体を同期的にメインスレッドで読み込みました — 多くの島があるサーバーで最大～1 秒、AOneBlock と ChunkBlock の両方がフックされている場合は 2 倍 — 定期的なラグスパイクを引き起こしました。データベース読み込みは非同期に実行されるようになりました。安価な島とパーミッションの検索のみメインスレッドのままです。

    [Release v2.1.1](https://github.com/BentoBoxWorld/TopBlock/releases/tag/2.1.1)

??? note "v2.1.0 の新機能 — ChunkBlock サポート"
    **リリース日:** 2026-08-21

    TopBlock はもう AOneBlock のみではありません。**ChunkBlock** もサポートするようになり、どちらのゲームモード — または両方一緒に — もインストールできます。互換性：BentoBox API 3.14.0+ · AOneBlock 1.18.0+ と ChunkBlock 1.0.1+ · Paper Minecraft 1.21.x · Java 21。

    - ✨ **ChunkBlock サポート。** TopBlock は起動時に見つかった AOneBlock と ChunkBlock をフックします。両方がインストールされている場合、各ゲームモードは完全に分離されたトップテン、`topblock` コマンド、プレースホルダーセットを保持します。
    - ✨ **新しいプレースホルダー** — 既存の `aoneblock_` 境界をミラーリングし、ChunkBlock 独自のランキングを報告する完全な `%chunkblock_island_*_top_<number>%` セット。
    - ✨ **新しい権限** — `chunkblock.island.topblock` と `chunkblock.intopten`、両方デフォルト `true`、AOneBlock 相当をミラーリング。プレフィックスはゲームモードごとなので、1 つのランキングからプレイヤーを非表示にしながら別に見えるようにできます。
    - 🔺 **AOneBlock はソフト依存になりました。** TopBlock は以前 AOneBlock なしで読み込みを拒否していました。サポートされたゲームモードが*どちらも*存在しない場合のみ自身を無効にします。既存の AOneBlock のみのセットアップは影響を受けず、変更は不要です。
    - 🐛 **各トップテンは自身のゲームモードのアイランドのみを表示するようになりました。** AOneBlock と ChunkBlock の両方が `database/OneBlockIslands/` の下にアイランドを保存するため、ChunkBlock 更新は AOneBlock のレコードもロードして間違ったプレイヤーが表示されました。アイランドはゲームモードのワールドでフィルタリングされるようになりました。
    - 🐛 **トップテンパネルの Steve ヘッド修正。** `top_panel.yml` で `icon: PLAYER_HEAD` がコメント解除されていたら、スキン解決が発動されず、すべてのヘッドが Steve としてレンダリングされました。パネルは名前ベースのヘッド経路にフォールスルーするようになりました。

    ℹ️ これは AOneBlock サーバーのドロップイン更新です — 設定、パネル、ロケール変更は不要です。

    [Release v2.1.0](https://github.com/BentoBoxWorld/TopBlock/releases/tag/2.1.0)

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
