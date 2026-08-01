# Level

**Level** はプレイヤーがトップアイランドを目指して競えるようにします！ブロックを設置してアイランドレベルを上げましょう！

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("Level") }}

## インストール

1. Level アドオンの jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます。
4. config.yml を希望通りに編集します。設定にはブロックの価値が指定されています（下記参照）。
5. 変更を加えた場合はサーバーを再起動します。

## 設定

Level アドオンには 3 つの一般的な設定があります:

- config.yml ファイルにはデフォルトのアドオン設定が含まれています。
- blockconfig.yml ファイルには各ブロックの価値が含まれています。
- /panels/ にはプレイヤーの GUI を管理するファイルが含まれています。

### config.yml

設定ファイルにはアドオンのメイン機能が含まれています。

最新の config.yml は[こちら](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/resources/config.yml)で確認できます。

このセクションではアドオンの全体的な設定を定義します。

??? note "disabled-game-modes"
    Level アドオンが動作しない GameModeAddon を指定できます。
    
    Level はこれらのゲームモードアドオンにフックしません。

    デフォルト: `[]`

??? note "log-report-to-console"
    コンソールからコマンドを実行した場合にレベルレポートを表示できます。

    デフォルト: `true`

??? note "concurrent-island-calcs"
    同時に実行できるアイランドレベル計算の数を指定できます。

    CPU が対応できる場合、キューに複数ある場合は並列アイランド計算を実行できます。

    デフォルト: `1`

??? note "calculation-timeout"
    レベル計算を停止するまでの分数を指定できます。

    通常、計算は数秒しかかからないため、これがトリガーされる場合は何かがおかしいです。

    デフォルト: `5`

??? note "zero-new-island-levels"
    スターターブロックをアイランドレベルに含めるかどうかを指定できます。

    true の場合、Level はスターターアイランドのレベルを計算し、将来のレベル計算からそれを差し引きます。
    全スターターブロックが削除されるとプレイヤーのレベルはマイナスになる可能性があります。
    
    false の場合、プレイヤーのスターターアイランドブロックはレベルにカウントされます。

    デフォルト: `true`

??? note "login"
    プレイヤーのログイン時にアイランドレベルを計算するよう設定できます。

    プレイヤーがログインした時に静かにアイランドレベルを計算します。

    デフォルト: `false`

??? note "nether"
    ネザーアイランドをレベル計算に含められます。

    警告: ゲーム途中でこれを有効にすると、アイランドを持つプレイヤーのアイランドレベルが急上昇します。新しいアイランドは正しくゼロになります。

    デフォルト: `false`

??? note "end"
    エンドアイランドをレベル計算に含められます。

    警告: ゲーム途中でこれを有効にすると、アイランドを持つプレイヤーのアイランドレベルが急上昇します。新しいアイランドは正しくゼロになります。

    デフォルト: `false`

??? note "include-chests"
    チェストの内容物をレベル計算に含められます。

    警告: レベル計算が長くなり、サーバーのパフォーマンスに影響する可能性があります。

    デフォルト: `false`

??? note "underwater"
    水中ブロックの倍率を指定できます。

    ブロックが海面より低い場合、より高い価値を持てます（例: 2倍）。
    海がある場合に水中開発を促進します。値は小数でも可能です。

    デフォルト: `1.0`

??? note "levelcost"
    アイランドレベル1の価値を指定できます。

    デフォルト: `100`

    最小値: `1`

??? note "level-calc"
    レベル計算の計算式を指定できます。

    * blocks - デスペナルティを差し引いた全ブロック価値の合計
    * level_cost - 線形方程式における1レベルの価値

    この計算式には +、=、*、/、sqrt、^、sin、cos、tan、log（自然対数）が使えます。
    結果は常にlong整数に丸められます。

    例えば、非線形の代替オプション: `3 * sqrt(blocks / level_cost)`

    デフォルト: `blocks / level_cost`

??? note "levelwait"
    レベルリクエスト間のクールダウンを秒数で指定できます。

    デフォルト: `60`

??? note "deathpenalty"
    デスペナルティを指定できます。

    プレイヤーが死ぬたびに失うブロック価値。
    デフォルト値の 100 は、死ぬたびにプレイヤーが 1 レベル失うことを意味します（levelcost が 100 の場合）。
    
    この機能を使用しない場合はゼロに設定してください。

    デフォルト: `100`

??? note "sumteamdeaths"
    デスペナルティに全チームメンバーの死亡を合計できます。

    false の場合、リーダーの死亡のみがカウントされます。

    デフォルト: `false`

??? note "shorthand"
    アイランドレベルの表示を短縮できます。

    大きなレベル値を四捨五入して表示します（例: 10,345 → 10k）。

    デフォルト: `false`

### blockconfig.yml

ブロック設定ファイルにはブロックの価値が含まれています。

最新の blockconfig.yml は[こちら](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/resources/blockconfig.yml)で確認できます。

このセクションではブロックの価値とその制限を定義します。

!!! tip "ヒント"
    このファイルの値は整数（全数）のみをサポートします。

!!! tip "ヒント"
    正しいマテリアル名は Spigot のマテリアルページで確認できます。

    注意: これが最新の Spigot マテリアルリストです: [MATERIALS](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)

??? note "limits"
    このセクションには特定のブロックの制限が記載されています。
    この量を超えるブロックはカウントされません。
    この制限は全ゲームモードに適用され、ワールド固有ではありません。

    形式: `MATERIAL: NUMBER`

    Level 2.28.0 以降、これらの制限は**寄付された**ブロックにも適用されます。設置する代わりに寄付することで、ブロックの上限を超えてポイントを得ることはできません。

    - レベル計算は、寄付されたブロックの種類ごとに現在の制限で上限を設けます。プレイヤーが寄付した後に制限を引き下げた場合、新しい制限までしかカウントされません。
    - `/[player_command] donate hand`、`/[player_command] donate inv`、寄付パネルはいずれも事前に制限を確認し、実際にカウントされる数量まで確認プロンプトを切り詰め（切り詰めた場合は警告行を表示します）、提供されたものがすべて制限に達している場合はきっぱり拒否します。
    - 制限の照会は大文字小文字を区別しないため、大文字小文字が混在したカスタムブロック ID（Oraxen のアイテムなど）でも、どこでも同じ制限に解決されます。

??? note "blocks"
    このセクションには全ゲームモード（ワールド）におけるブロックの価値が記載されています。
    ワールド固有の値を指定するには次のセクションを使用してください。
    記載されていないブロックは価値 0 となります。AIR は常にゼロです。

    形式: `MATERIAL: NUMBER`

    CraftEngine のカスタムブロックもサポートされています（BentoBox 3.15.0+ が必要）。ネームスペース ID をキーとして使用してください：

    ```yaml
    blocks:
      mynamespace:my_block: 50
      mynamespace:custom_ore: 3
    ```

??? note "worlds"
    特定のワールドで異なる価値を持つブロックを記載します。
    ブロックが記載されていない場合は、ブロックセクションのデフォルト値が使用されます。
    ワールド名をプレフィックスとして付けます。その値は関連するネザーとエンドに適用されます（存在する場合）。

    例:

    ```
        worlds:
          AcidIsland_world:
            SAND: 0
            SANDSTONE: 0
            ICE: 0
    ```

    この例では、AcidIsland は砂、砂岩、氷を除く全てのブロックで BSkyBlock と同じ価値を使用します。

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装する機能が導入されました。カスタマイズをできる限りシンプルにしようとしましたが、一部の機能については説明が必要です。
BentoBox カスタム GUI の詳細はこちらを参照してください: [カスタム GUI](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    Level アドオンの GUI をカスタマイズするにはバージョン 2.10.0 が必要です。これが実装された最初のバージョンです。アドオンは `/plugins/bentobox/addons/level` の下に `panels` というディレクトリを作成します。

    現在カスタマイズできる GUI は 3 つです:

    - トップパネル: `top_panel` - 上位 10 つのアイランドを表示できます。
    - 詳細ブロックパネル: `detail_panel` - ゲーム内でブロック価値の詳細リストを表示できます。
    - ブロック価値パネル: `value_panel` - ゲーム内で各ブロックの価値を表示できます。

    各 GUI にはそれぞれに固有の機能があります。

??? question "`PREVIOUS`|`NEXT` ボタンタイプとは何ですか？"
    このボタンは detail_panel と value_panel で利用できます。
    PREVIOUS と NEXT ボタンタイプは、GUI のスペースより多くのブロックがある場合に自動ページングを作成できます。
    これらのタイプには data の下に追加パラメーターがあります:

    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

      例: 
      ```yaml
          icon: tipped_arrow[potion_contents={custom_color:11546150}]
          title: level.gui.buttons.previous.name
          description: level.gui.buttons.previous.description
          data:
            type: PREVIOUS
            indexing: true
          action:
            left:
              tooltip: level.gui.tips.click-to-previous
      ```

??? question "`TOP` ボタンタイプとは何ですか？"
    このボタンは top_panel で利用できます。アイランドレベルで上位 X 位のアイランドを表示します。
    
    `icon` のデフォルトは適切なプレイヤースキンの `PLAYER_HEAD` です。有効にすると指定されたマテリアルに置き換えられます。

    data フィールドの `index` で、現在のスポットに表示するトップ 10 の順位を指定できます。

    トップパネルには追加アドオンが必要な 2 つのアクションがあります:
    
    - `warp` - Warps アドオンが必要。プレイヤーのアイランドにワープサインが存在する場合のみ表示されます。
    - `visit` - Visit アドオンが必要。プレイヤーのアイランドへの訪問が許可されている場合のみ表示されます。

    フォールバックにより、トップスポットにプレイヤーがいない場合の背景アイコンを変更できます。

    例:
    ```yaml
        #icon: PLAYER_HEAD
        title: level.gui.buttons.island.name
        description: level.gui.buttons.island.description
        data:
          type: TOP
          index: 1
        actions:
          warp:
            click-type: LEFT
            tooltip: level.gui.tips.click-to-warp
          visit:
            click-type: RIGHT
            tooltip: level.gui.tips.right-click-to-visit
        fallback:
          icon: LIME_STAINED_GLASS_PANE
          title: level.gui.buttons.island.empty
    ```

??? question "`VIEW` ボタンタイプとは何ですか？"
    このボタンは top_panel で利用できます。閲覧者のアイランドレベルを表示します。

    `icon` のデフォルトは適切なプレイヤースキンの `PLAYER_HEAD` です。有効にすると指定されたマテリアルに置き換えられます。
    
    `view` アクションでプレイヤーのアイランドの詳細メニューを見ることができます。

    例:
    ```yaml
        #icon: PLAYER_HEAD
        title: level.gui.buttons.island.name
        description: level.gui.buttons.island.description
        data:
          type: VIEW
        actions:
          view:
            click-type: unknown
            tooltip: level.gui.tips.click-to-view
    ```

??? question "`BLOCK` ボタンタイプとは何ですか？"
    このボタンは detail_panel と value_panel で利用できます。指定されたマテリアルをアイコンとして表示します。

    例:
    ```yaml
      #icon: STONE
      title: level.gui.buttons.value.name
      description: level.gui.buttons.value.description
      data:
        type: BLOCK
    ```

## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。

=== "プレイヤーコマンド"
    - `/[player_command] top`: トップパネルにアクセスします。`[gamemode].island.top` 権限が必要です。
    - `/[player_command] level`: プレイヤーのレベル計算をトリガーします。`[gamemode].island.level` 権限が必要です。
    - `/[player_command] value [material]`: ブロックの価値を確認できます。`[gamemode].island.value` 権限が必要です。
    - `/[player_command] donate`: チェストスタイルの GUI を開いてブロックをアイランドのレベルに直接寄付します。寄付されたポイントは将来のレベル再計算後も保持されます。`[gamemode].island.level.donate` 権限が必要です。
    - `/[player_command] donate hand [amount]`: GUI を開かずにプレイヤーが手に持っているアイテム（または指定した数量）をアイランドレベルに直接寄付します。`[gamemode].island.level.donate` 権限が必要です。
    - `/[player_command] donate inv`: プレイヤーのインベントリ内にある寄付可能なブロックをマテリアルごとの価値と合計値付きで一覧表示し、確認するとすべて寄付してレベル再計算を実行します。設定されていない価値のアイテムやブロック以外のアイテムはインベントリに残ります。`[gamemode].island.level.donate` 権限が必要です。

    !!! note "備考"
        2.28.0 以降、3 つの寄付経路はいずれも [`blockconfig.yml`](#blockconfigyml) で設定されたブロックの `limits` に従い、寄付されたポイントは再計算のたびに現在のブロック価値から算出されます。


=== "管理者コマンド"
    - `/[admin_command] level <player>`: プレイヤーのレベル計算をトリガーします。`[gamemode].admin.level` 権限が必要です。
    - `/[admin_command] levelstatus`: キューにあるアイランドの数を表示します。`[gamemode].admin.levelstatus` 権限が必要です。
    - `/[admin_command] sethandicap <player> <number>`: アイランドレベルの初期値を設定できます。`[gamemode].admin.level.sethandicap` 権限が必要です。
    - `/[admin_command] top`: チャットでトップ 10 のアイランドを表示します。`[gamemode].admin.top` 権限が必要です。
    - `/[admin_command] top remove <player>`: プレイヤーをトップから削除できます。`[gamemode].admin.top.remove` 権限が必要です。


## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "プレイヤー権限"
    - `[gamemode].intopten` - (デフォルト: `true`) - プレイヤーがトップ 10 パネルに表示されることを許可します。
    - `[gamemode].island.level` - (デフォルト: `true`) - プレイヤーが `/[player_command] level` コマンドを使用できます。
    - `[gamemode].island.top` - (デフォルト: `true`) - プレイヤーが `/[player_command] top` コマンドを使用できます。
    - `[gamemode].island.value` - (デフォルト: `true`) - プレイヤーが `/[player_command] value` コマンドを使用できます。
    - `[gamemode].island.level.details.blocks` - (デフォルト: `true`) - プレイヤーがアイランドのブロック詳細リストを表示できます。
    - `[gamemode].island.level.details.spawners` - (デフォルト: `false`) - プレイヤーがアイランドのスポナー詳細リストを表示できます。
    - `[gamemode].island.level.details.underwater` - (デフォルト: `false`) - プレイヤーがアイランドの水中ブロック詳細リストを表示できます。
    - `[gamemode].island.level.details.above-sea-level` - (デフォルト: `false`) - プレイヤーがアイランドの海面より上のブロック詳細リストを表示できます。
    - `[gamemode].island.level.donate` - (デフォルト: `true`) - プレイヤーが `/[player_command] donate` コマンドを使用できます。

=== "管理者権限"
    - `[gamemode].admin.level` - (デフォルト: `op`) - プレイヤーが `/[admin_command] level <player>` コマンドを使用できます。
    - `[gamemode].admin.levelstatus` - (デフォルト: `op`) - プレイヤーが `/[admin_command] levelstatus` コマンドを使用できます。
    - `[gamemode].admin.level.sethandicap` - (デフォルト: `op`) - プレイヤーが `/[admin_command] sethandicap <player> <number>` コマンドを使用できます。
    - `[gamemode].admin.top` - (デフォルト: `op`) - `/[admin_command] top` コマンドへのアクセスを許可します。
    - `[gamemode].admin.top.remove` - (デフォルト: `op`) - `/[admin_command] top remove <player>` コマンドへのアクセスを許可します。

??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    以下のリストに不足しているものがあれば、お知らせください！


## プレースホルダー

{{ placeholders_source(source="Level") }}

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/Level/issues)のリストに追加してください。

??? question "`level-cost` をレベルごとに増加させるにはどうすればいいですか？"
    `level-cost` 設定は固定値であり、BentoBox はアイランドレベルをレベルごとに反復するのではなく、総ブロック数に単一の計算式を適用してアイランドレベルを計算するため、レベルごとに反復的に増加させることはできません。

    増加するレベルコストを実現する方法は `level-calc` 計算式を使用することです。例えば、各レベルが前のレベルより 50% 難しくなるようにする場合（つまり、レベル 1 は 100 ブロック、レベル 2 は 150、レベル 3 は 225 など）の計算式は:

    `level-calc: 2.4661 * log(blocks) - (2.4661 * log(level_cost) - 1)`

    ここで `level_cost` はレベル 1 に到達するために必要なブロック数です。

    そのプログレッションのグラフはこちらです:

    ![template](https://user-images.githubusercontent.com/4407265/212771452-edc943fe-c861-4ba1-b581-8ec987e52f94.png){: loading=lazy }

    !!! warning "警告"
        この計算式はレベル 25 あたりで漸近線になり始め、レベル 26 や 27 に到達するには非常に多くのブロックが必要になり、時間の経過とともにほとんどのプレイヤーが同じ最大レベルに収束する可能性があります。プログレッションカーブを選ぶ際にこの点を考慮してください。

    **カスタム計算式の導出**

    特定のプログレッションカーブに合った計算式を作成するには:

    1. スプレッドシート（Excel や Google シートなど）でターゲットレベルとそれに対応するブロックコストの表を作成します。
    2. 表の X/Y グラフを作成します。
    3. グラフを右クリックしてトレンドラインを追加します。カーブに最もよく合う近似タイプ（線形、対数、指数など）を選択し、「グラフに方程式を表示」を有効にします。
    4. 得られた方程式で `x` を `blocks` に置き換えて `level-calc` の値として使用します。

    例えば、上記の 50% プログレッションはこの方法で導出され、次の式になります:

    `level-calc: 2.4661 * log(blocks) - 10.357`

    ![template](https://user-images.githubusercontent.com/4407265/212773894-6f635ed4-f337-4936-b50f-3b616b6bf041.png){: loading=lazy }
    ![template](https://user-images.githubusercontent.com/4407265/212773929-b51ae6b3-5df3-43ae-b35f-bc6fcb42d78f.png){: loading=lazy }



## 変更履歴

??? note "v2.23.0 の新機能"
    **リリース日:** 2026-02-21

    - **Oraxen と Nexo のファーニチャー/カスタムブロックサポート。** Level が Oraxen のファーニチャーメカニクスと Nexo のカスタムブロック・ファーニチャーをアイランドレベルにカウントできるようになりました。これらの統合はベータ版です。どちらかのプラグインをインストールしている場合は有効にしてください。
    - 新しいブロックごとのプレースホルダー: `[gamemode]_island_count_<block>`（アイランド上の特定ブロックの数）、`[gamemode]_island_value_<block>`（ブロックタイプの価値）、`[gamemode]_island_limit_<block>`（設定されたブロック制限）。ブロックキーにはアンダースコアを使用（例: `_island_count_minecraft_stone`）。

    [Release v2.23.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.23.0)

??? warning "v2.24.0 の新機能 — 対応が必要"
    **リリース日:** 2026-04-12

    - **ブロック寄付システム。** プレイヤーが `/[player_command] donate`（GUI）または `/[player_command] donate hand [amount]`（手持ちから素早く寄付）を使ってアイランドのレベルにブロックを永続的に寄付できるようになりました。寄付されたポイントはアイランドごとに保存され、レベル再計算後も再追加されます。
    - 新しい `ISLAND_BLOCK_DONATION` 保護フラグで誰が寄付できるかを制御します。デフォルトはオーナーのみ。メンバーランクまで拡張可能です。
    - `detail_panel.yml` に寄付履歴を表示する新しい **DONATED** タブを追加。
    - `level-cost` 計算式でより大きなチームを不利にするための新しい `island_members` 変数が利用可能。
    - 管理者レベルレポートに寄付ブロックの内訳を含めるようになりました。
    - 全ロケールファイルを MiniMessage フォーマットに移行。
    - 🆕 ロシア語（`ru.yml`）ロケールを追加。
    - 並行書き込み時のトップテン順序のバグを修正。
    - 吊り看板、ツタ、洞窟のツタのブロックアイコンが正しくレンダリングされるように修正。

    🔺 新しい DONATED タブテンプレートが生成されるよう、再起動前に **`plugins/BentoBox/addons/Level/panels/detail_panel.yml` を削除してください**。このファイルはアップグレード時に上書きされません。

    🔡 カスタマイズがある場合は**ロケールファイルを再生成してください** — 古い `&` カラーコードはもはや有効ではありません。

    [Release v2.24.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.24.0)

??? note "v2.25.0 の新機能"
    **リリース日：** 2026-04-26

    - **CraftEngine カスタムブロックサポート。** CraftEngine のブロックがアイランドレベル計算でカウントされるようになりました。ネームスペース ID を使って `blockconfig.yml` に追加してください（例：`mynamespace:my_block: 50`）。BentoBox 3.15.0+ が必要です。`config.yml` の `disabled-plugin-hooks: [CraftEngine]` で無効化できます。
    - **`hand` キーワードのローカライズ対応。** `/island donate` と `/island value` の `hand` 引数が新しいロケールキー `island.donate.hand.keyword` で翻訳可能になりました。英語の `hand` は常にフォールバックとして受け付けられます。
    - 🔡 英語以外の 16 のロケールファイルを更新し、不足しているキーを追加しました。
    - 🔡 ウクライナ語ロケールが完全に翻訳されました。

    🔡 新しい `island.donate.hand.keyword` キーを取得するために**ロケールファイルを再生成**してください。

    [Release v2.25.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.25.0)

??? note "v2.26.0 の新機能"
    **リリース日：** 2026-05-04

    - **設定可能な寄付パネル。** 寄付 GUI が新しい `panels/donation_panel.yml` テンプレートで完全に設定可能になりました。価値、詳細、トップテンの各パネルと同じ仕組みです。サーバー管理者はパネルを 1～6 行にリサイズし、4 つの名前付きボタン（`INFO`、`CANCEL`、`PREVIEW`、`CONFIRM`）の位置とアイコンを変更し、装飾アイテムを追加できます。寄付グリッドは枠でも名前付きボタンでもないすべてのセルを自動で埋めます。
    - `force-shown: [1,2,3,4]` でパネルが使う行数を制御します（1～6 行サポート）。4 つの必須ボタンは `data.type` に従って配置されます。テンプレートが見つからないか必須ボタンのいずれかが存在しない場合、パネルは従来のハードコードされた 4 行レイアウトにフォールバックします。
    - 🐛 装飾用テンプレートアイテムが実際にインベントリに表示されるようになりました。寄付パネルのカスタム `title:` も尊重されるようになりました。`force-shown` は他のパネル YAML と同様にリストとしてパースされます。
    - API の破壊的変更なし、ロケール変更なし、`config.yml` の移行なし。

    ⚙️ **寄付パネルレイアウト。** 初回起動時に新しい `panels/donation_panel.yml` がデータフォルダに展開されます。触らなければ 2.25.0 と同じレイアウトでレンダリングされ、編集すればカスタマイズできます。

    [Release v2.26.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.26.0)

??? warning "v2.27.0 の新機能 — 対応が必要"
    **リリース日：** 2026-05-13

    🔺 **BentoBox 3.16.0 以降が必要です。** このリリースでは `addon.yml` の `api-version` が `3.16.0` に引き上げられ、新しい `CraftEngineHook.getItemId` / `getItemStack` ヘルパーに依存します。古いバージョンの BentoBox ではアドオンのロードが拒否されます。

    - ⚙️ **寄付専用モード。** `config.yml` に新しい `donations-only` オプションが追加されました（デフォルト `false`）。`true` にすると、再計算ごとのチャンクスキャンが完全にスキップされ、アイランドレベルは設定済みの `level-calc` フォーミュラを使って寄付ポイントのみから算出されます。このモードでは `/island detail` は登録されず、トップテンビューアーのボタンも詳細パネルを開かなくなります。保存済みの `initialCount` は `/island level` 実行時に無視されるため、既存アイランドがあるサーバーでこのモードを有効にしても、プレイヤーが大きくマイナスのレベルに落ちることはありません。
    - 💎 **`/island donate inv` — インベントリからすべて寄付。** 確認付きの新しい `inv` サブコマンドを追加。プレイヤーのインベントリ内にある寄付可能なブロックをマテリアルごとの価値と合計値付きで一覧表示し、確認するとすべて寄付してレベル再計算を実行します。設定されていない価値のアイテムやブロック以外のアイテムはインベントリに残ります。タブ補完で第1引数に `hand` / `inv` を、`hand` の後には手持ちアイテムの個数を提案するようになりました。
    - 🧱 **価値・詳細・寄付メニュー全体でカスタムブロックに対応。** Oraxen、Nexo、ItemsAdder、CraftEngine のカスタムブロックが `/level value` で除外されたり、`/level detail` で名前のない PAPER アイコンとして表示されたりしなくなりました。価値パネルと詳細パネルは各プラグインのレジストリから実際のカスタムブロックの `ItemStack` を取得するため、設定済みのテクスチャ/モデルデータと表示名が保持されます。カスタムアイテムを手に持った状態での `/island value hand` は、設定済みの価値と表示名を報告するようになりました。寄付経路（`/island donate hand`、`/island donate inv`、寄付パネル）はカスタムブロックのアイテムを受け付け、カスタム ID のもとで寄付を記録します。
    - 🐛 **マイナス方向への進行を修正。** 非線形の `level-calc` フォーミュラ（例：`3 * sqrt(blocks / level_cost)`）が、レベル間でゼロを下回らなくなりました。@msmith-codes に感謝します！
    - ⚡ **パフォーマンス。** ポイント境界を計算する際、`tidyUp()` がメインスレッド上で最大 1,000 万ポイントを線形に走査しなくなりました — 前方・後方スキャンは二分探索を使用するようになり（数百万回ではなく約 23 回の反復）。

    🔡 **ロケールを更新。** 出荷済みの 18 ロケールすべてに新しい `island.donate.inv.*` キー（`keyword`、`confirm-header`、`confirm-line`、`confirm-total`）が追加されました。`plugins/BentoBox/addons/Level/locales/` にカスタマイズ済みのロケールファイルがある場合は、新しい `donate.inv` ブロックをコピーしてください。そうしないと、新しい `/island donate inv` の流れで生のキーが表示されてしまいます。

    [Release v2.27.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.27.0)

??? warning "v2.28.0 の新機能 — 対応が必要"
    **リリース日：** 2026-07-28

    互換性: BentoBox API 3.16.0、Minecraft 1.21.x および 26.1.x、Java 21。

    - 🔺 **寄付の制限が全経路で適用されるようになりました。** [`blockconfig.yml`](#blockconfigyml) で定義したブロックの制限が、寄付に関わるすべての場所で適用されます。レベル計算は寄付されたブロックの種類ごとに現在の制限で上限を設け、`/island donate hand`、`/island donate inv`、寄付 GUI はいずれも事前に制限を確認して、実際にカウントされる数量まで確認プロンプトを切り詰め、すでに上限に達しているマテリアルはスキップし、誤解を招く 0 ポイントのプロンプトの代わりに「寄付の制限に達しました」という明確なメッセージを表示します。管理者向けのレベルレポートも寄付の行を現在の制限で打ち切り（「capped at N」と表示）、寄付の合計と一致するようになりました。
    - **寄付ポイントが現在のブロック価値に追随するようになりました。** ポイントは保存された寄付ブロックのマップから、再計算のたびに現在の（およびワールド固有の）価値を使って算出されます。そのため `blockconfig.yml` の価値を変更すると、古い保存済みの合計値ではなく過去の寄付にも遡って反映されます。寄付 GUI の「現在の寄付」の数値も、レベルが使用するものと同じ実効ポイントを表示します。
    - 制限の照会は大文字小文字を区別しないため、大文字小文字が混在したカスタムブロック ID（Oraxen のアイテムなど）でも、どこでも同じ制限に解決されます。
    - リリースが Modrinth に加えて CurseForge と Hangar にも自動公開されるようになり、対応バージョンに Minecraft 26.1.2 が追加されました。

    🔺 **アップグレード後にアイランドのレベルが下がる場合があります。** プレイヤーがブロックの制限を超えて寄付していたサーバーでは、それらのブロックがレベル計算から除外されるようになります。これは意図した修正ですが、問い合わせに備えてください。

    🔡 **ロケールを更新。** 出荷済みの 17 ロケールすべてに `island.donate` 配下の新しいキー 3 つ（`limit-reached`、`limit-notice`、`limit-reached-all`）が追加されました。`plugins/BentoBox/addons/Level/locales/` にカスタマイズ済みのロケールファイルがある場合は、これらのキーを追加してください。そうしないと制限の警告が生のキーで表示されます。

    !!! note "開発ビルドをご利用の方へ"
        このサイクル中のスナップショットビルドに登場した実験的なチャンク単位のゼロ化エンジンは、リリース前に削除され、2.28.0 には**含まれていません**。安定版リリースの利用者に影響はありません。

    [Release v2.28.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.28.0)

??? note "v2.28.1 の新機能"
    **リリース日：** 2026-07-29

    バグ修正リリースです。2.28.0 からそのまま置き換えられ、ロケール・設定・パネルの変更はありません。

    - 🐛 **価値パネルの検索ボタンがチャットプロンプトを重複して積み上げなくなりました。** クリックのたびに 90 秒の「検索する値を入力してください」という会話が新たに開始されていました。最初のプロンプトが見えていない場合 — 例えば CMI のようなチャット管理プラグインがそれを飲み込んだ場合 — プレイヤーはボタンを繰り返しクリックし、積み上がった会話が後から `Conversation cancelled!` と `Please enter a search value` の交互のスパムとして再生され、そのたびに GUI が開き直されていました。検索入力は、すでに会話が保留中の場合は 2 つ目を作らずに質問を再表示するようになりました。

    [Release v2.28.1](https://github.com/BentoBoxWorld/Level/releases/tag/2.28.1)

## 翻訳

{{ translations("Level") }}



## API

Level 2.7.2 と BentoBox 1.17 以降、他のプラグインが Level アドオンのデータに直接アクセスできます。ただし、アドオンリクエストは依然として多くの依存関係を使用したくないプラグインには良い解決策です。

### Maven 依存関係
Level は他のプラグイン向け API を提供しています。これは Level 2.8.1 以降に対応しています。

!!! note "注意"
    Maven POM.xml に Level 依存関係を追加してください:

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
                <artifactId>level</artifactId>
                <version>2.8.1</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```
最新の Level バージョンを使用してください。

ワールド内のアイランドのプレイヤーレベルを取得するには、アイランドがあるワールドを取得し、そのワールドでプレイヤーがアイランドのオーナーであることを確認した後、Level に問い合わせます。

Level の JavaDocs は[こちら](https://ci.codemc.io/job/BentoBoxWorld/job/Level/ws/target/apidocs/index.html)で確認できます。

### イベント

=== "IslandLevelCalculatedEvent"
    !!! summary "説明"
        プレイヤーのレベルが計算されたときにトリガーされるイベントです。

        クラスへのリンク: [IslandLevelCalculatedEvent](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/events/IslandLevelCalculatedEvent.java)

    !!! question "変数"
        - `Island island` - アイランドオブジェクト。
        - `UUID targetPlayer` - レベルを計算したプレイヤーの ID。
        - `Results results` - 計算されたアイランドの結果。
        
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCalculated(IslandLevelCalculatedEvent event) {
            UUID user = event.getTargetPlayer();
            Island island = event.getIsland();
            Results results = event.getResults();
            
            // death handicap from results.
            int deathHandicap = event.getDeathHandicap();

            // the island initial level from results.
            long initialLevel = event.getInitialLevel();
            
            // the island level from results.
            long level = event.getLevel();

            // this will overwrite island level to 100.
            event.setLevel(100);
            
            // number of points required to next level
            long pointsToNextLevel = event.getPointsToNextLevel();

            // the report text from results.
            List<String> report = event.getReport();
        }
        ``` 

=== "IslandPreLevelEvent "
    !!! summary "説明"
        プレイヤーのレベルが計算される前にトリガーされるイベントです。

        クラスへのリンク: [IslandPreLevelEvent](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/events/IslandPreLevelEvent.java)

    !!! question "変数"
        - `Island island` - アイランドオブジェクト。
        - `UUID targetPlayer` - レベルを計算したプレイヤーの ID。
        
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.LOW)
        public void beforeLevelCalculated(IslandPreLevelEvent event) {
            UUID user = event.getTargetPlayer();
            Island island = event.getIsland();
        }
        ```

### アドオンリクエストハンドラー

***このAPIはもはや必要ありません***。Level は現在 Bukkit プラグインとしてロードされているため、そのメソッドに直接アクセスできます。Level の JavaDocs は[こちら](https://ci.codemc.io/job/BentoBoxWorld/job/Level/ws/target/apidocs/index.html)で確認できます。例えばプレイヤーのレベルを取得したい場合は、LevelsManager クラスのメソッドから直接取得できます。ただし、レガシーの理由からこのドキュメントは保存されています。

アドオンリクエストハンドラーの詳細は[こちら](/en/latest/BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons/)をご覧ください。

=== "island-level"
    !!! summary "説明"
        指定されたワールドにおけるこのプレイヤーのアイランドレベルを返します。

    !!! question "入力"
        - `world-name`: String - ワールドの名前。
        - `player`: UUID - プレイヤーの UUID。

    !!! success "出力"
        プレイヤーのアイランドレベル、または入力が無効な場合やこのプレイヤーがこのワールドにアイランドを持っていない場合は `0L`。

    !!! failure "失敗"
        `world-name` が提供されていないか、`world-name` が存在しないかゲームモードワールドでない場合、このハンドラーは `0L` を返します。

    !!! example "コード例"
        ```java
            /**
             * Returns the level of this player's island in the given world.
             * @param playerUUID UUID of the player, not null.
             * @param worldName Name of the world (Overworld) the island is in, not null.
             * @return the player's island level or {@code 0L} if the input was invalid or
             *         if this player does not have an island in this world.
             */
            public long getIslandLevel(UUID playerUUID, String worldName) {
                return (Long) new AddonRequestBuilder()
                    .addon("Level")
                    .label("island-level")
                    .addMetaData("world-name", worldName)
                    .addMetaData("player", playerUUID)
                    .request();
            }
        ```

=== "top-ten-level"
    !!! summary "説明"
        アイランドレベルのトップ 10 のアイランドオーナーの UUID をキーとし、アイランドレベルを値とするマップを返します。

    !!! question "入力"
        - `world-name`: String - ワールドの名前。

    !!! success "出力"
        トップ 10 のアイランドオーナーの UUID をキーとし、アイランドレベルを値とする `Map<UUID, Long>`。

    !!! failure "失敗"
        `world-name` が提供されていないか、`world-name` が存在しないかゲームモードワールドでない場合、このハンドラーは空のマップを返します。

    !!! example "コード例"
        ```java
            /**
             * Returns the players whose island they own is in the Top 10 mapped to the level of their island.
             * @param worldName Name of the world (Overworld) the island is in, not null.
             * @return a Map containing the UUIDs of the island owners whose island is in the Top 10, mapped to the level of their island,
             *         or an empty map if the specified world doesn't exist or doesn't contain islands.
             */
            public Map<UUID, Long> getTopTen(String worldName) {
                return (Map<UUID, Long>) new AddonRequestBuilder()
                    .addon("Level")
                    .label("top-ten-level")
                    .addMetaData("world-name", worldName)
                    .request();
            }
        ```
