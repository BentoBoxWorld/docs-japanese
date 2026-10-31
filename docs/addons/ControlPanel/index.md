# ControlPanel

**ControlPanel** はプレイヤーに最もよく使うアイランドコマンドを実行できるクリッカブル GUI メニューを提供します。入力不要です。サーバー管理者はシンプルな YAML ファイルを使用して、複数のクリックアクション、カスタムアイコン、ライブプレースホルダーをサポートした完全カスタマイズ可能なパネルを構築できます。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("ControlPanel") }}

## インストール

1. ControlPanel アドオンの jar を BentoBox プラグインの `addons` フォルダに配置します。
2. サーバーを再起動します。ControlPanel は `plugins/BentoBox/addons/ControlPanel/` 内にデフォルトの `controlPanelTemplate.yml` を作成します。
3. `controlPanelTemplate.yml` を編集してパネルを構築します（下の[設定](#configuration)を参照）。
4. 管理者コマンドでパネルをインポートします:
```
/{admin} cp import
```

!!! tip "ヒント"
    `{admin}` はゲームモードの管理者コマンドラベルに置き換えてください。例: BSkyBlock は `bsb`、AOneBlock は `oa`、AcidIsland は `acid`。

## コマンド

### プレイヤーコマンド

| コマンド | 説明 | 権限 |
|---|---|---|
| `/[label] controlpanel` | プレイヤーに割り当てられたコントロールパネルを開きます | `[gamemode].controlpanel` |
| `/[label] cp` | 上記コマンドの短縮エイリアス | `[gamemode].controlpanel` |

`[label]` はゲームモードのプレイヤーコマンドに置き換えてください。例: BSkyBlock は `island`、AOneBlock は `ob`。

表示されるパネルはプレイヤーの権限によって異なります。特定のパネル権限を持たないプレイヤーには `defaultPanel: true` のマークが付いたパネルが表示されます。プレイヤーが `[gamemode].controlpanel.panel.<suffix>` の特定のパネル権限を持っている場合、そのパネルが表示されます。

### 管理者コマンド

| コマンド | 説明 | 権限 |
|---|---|---|
| `/{admin} cp import` | `controlPanelTemplate.yml` からパネルをインポートします | `[gamemode].controlpanel.admin` |
| `/{admin} cp import <filename>` | カスタム YAML ファイルからパネルをインポートします | `[gamemode].controlpanel.admin` |

ファイル名に `.yml` 拡張子は不要です。自動的に追加されます。ファイルは `plugins/BentoBox/addons/ControlPanel/` に配置する必要があります。

!!! warning "警告"
    ゲームモードのパネルが既に存在する場合、インポート時に置き換え前の確認が求められます。

## 権限

| 権限 | デフォルト | 説明 |
|---|---|---|
| `[gamemode].controlpanel` | `true` | プレイヤーがコントロールパネルを開けます |
| `[gamemode].controlpanel.admin` | `op` | 管理者インポートコマンドの使用を許可します |
| `[gamemode].controlpanel.panel.default` | `true` | デフォルトパネルへのアクセスを付与します |
| `[gamemode].controlpanel.panel.<suffix>` | — | 指定されたサフィックスを持つカスタムパネルへのアクセスを付与します |

`[gamemode]` はゲームモード名の小文字に置き換えてください。例: `bskyblock`、`acidisland`、`aoneblock`、`caveblock`、`skygrid`。

!!! note "注意"
    プレイヤーが複数のパネル権限を持っている場合、アクセス可能なもののうち `defaultPanel: true` のマークが付いた最初のパネルが表示されます。プレイヤーがワイルドカード `*` 権限を持っている場合、最初に定義されたデフォルトパネルが使用されます。

## 設定

ControlPanel は 2 つのファイルを使用します:

- `config.yml` — 一般的なアドオン設定
- `controlPanelTemplate.yml` — パネルとボタンを定義します

両方とも `plugins/BentoBox/addons/ControlPanel/` に配置されています。

### config.yml

メイン設定ファイルには 1 つの設定があります:

??? note "disabled-gamemodes"
    ControlPanel が動作しない GameMode アドオン名のリスト。ControlPanel はこれらのゲームモードにフックしません。

    デフォルト: `[]`

    例:
    ```yaml
    disabled-gamemodes:
      - BSkyBlock
      - AcidIsland
    ```

??? note "template-file"
    （**1.16.1+**）コントロールパネルのインポート元となるテンプレートファイルです。パネルが最初に作成されるときに読み込まれ、`/{admin} bentobox reload` のたびに再読み込みされるため、編集してリロードすれば変更が反映されます。アドオンフォルダ（`plugins/BentoBox/addons/ControlPanel/`）内に存在する必要があります。リロード、管理者の `import` コマンド、初回作成のいずれもこの設定に従うため、アドオンに独自のファイルを指定できます。

    デフォルト: `controlPanelTemplate.yml`

### controlPanelTemplate.yml

このファイルは全てのコントロールパネルとそのボタンを定義します。編集後、`/{admin} bentobox reload`（**1.16.1+**）または `/{admin} cp import` を実行して変更を読み込みます。

!!! warning "リロードで保存済みパネルが置き換えられます（1.16.1+）"
    パネルは BentoBox のデータベースに保存されており、1.16.1 より前のテンプレートは一度だけの初期データでした。テンプレートを編集して `bbox reload` を実行しても、`cp import` も実行しない限り何も起こりませんでした。**1.16.1** 以降、リロードのたびに有効な各ゲームモードの保存済みパネルが消去され、テンプレートファイルから再インポートされます。テンプレートから*削除した*パネルも消え、データベースにのみ存在していたものは失われます — 変更はすべてテンプレートファイルに残してください。

#### パネル構造

```yaml
panel-list:
  <panel-key>:
    defaultPanel: true|false
    panelName: '<title>'
    permission: '<suffix>'
    buttons:
      <slot>:
        name: '<display name>'
        material: MATERIAL_NAME
        icon: 'namespace:item_id'
        itemsadder: 'namespace:item_id'
        description: |-
          line one
          line two
        command: '<left-click command>'
        right_click_command: '<right-click command>'
        shift_click_command: '<shift+left-click command>'
```

#### パネルフィールド

| フィールド | 型 | 説明 |
|---|---|---|
| `defaultPanel` | boolean | 特定のパネル権限を持たないプレイヤーにこのパネルを表示する場合は `true` に設定します。 |
| `panelName` | string | インベントリ GUI のタイトル。`&` カラーコードをサポートします。 |
| `permission` | string | `[gamemode].controlpanel.panel.<suffix>` に追加されるサフィックス。その権限を持つプレイヤーにこのパネルが表示されます。 |

#### ボタンフィールド

| フィールド | 必須 | 説明 |
|---|---|---|
| `slot` | はい | インベントリスロット番号（0〜53）。`"0-8"` のような引用符付き範囲を使うと複数のスロットに同じボタンを配置できます。 |
| `name` | はい | ボタンの表示名。`&` カラーコードをサポートします。 |
| `material` | いいえ | バニラの Minecraft マテリアル（例: `GRASS_BLOCK`）。フォールバックアイコンとして使用されます。 |
| `icon` | いいえ | BentoBox `ItemParser` 形式（例: `minecraft:diamond_block`）。`material` より優先されます。 |
| `itemsadder` | いいえ | [ItemsAdder](https://github.com/LoneDev6/ItemsAdder) カスタムアイテム ID（例: `iasurvival:ruby`）。ItemsAdder のインストールが必要です。未インストールの場合は paper にフォールバックします。 |
| `description` | いいえ | ボタン名の下に表示される lore 行。`&` カラーコード、`|-` による複数行、PlaceholderAPI `%placeholders%`、`[gamemode]` 置換をサポートします。 |
| `command` | いいえ | 左クリック時に実行されるコマンド（他の全クリックタイプのフォールバックとしても機能します）。 |
| `right_click_command` | いいえ | 右クリックまたは Shift+右クリック時に実行されるコマンド。省略した場合は `command` にフォールバックします。 |
| `shift_click_command` | いいえ | Shift+左クリック時に実行されるコマンド。省略した場合は `command` にフォールバックします。 |

!!! info "アイコンの優先順位"
    複数のアイコンフィールドが指定されている場合、優先順位は `itemsadder` > `icon` > `material` です。何も設定されていない場合、ボタンのデフォルトは `PAPER` です。

#### クリックタイプ

各ボタンはプレイヤーのクリック方法によって異なる反応をすることができます:

| クリックアクション | 使用するコマンド |
|---|---|
| 左クリック | `command` |
| 右クリック | `right_click_command`（`command` にフォールバック） |
| Shift + 左クリック | `shift_click_command`（`command` にフォールバック） |
| Shift + 右クリック | `right_click_command`（`command` にフォールバック） |
| その他のクリック | `command` |

#### コマンドプレースホルダー

`command`、`right_click_command`、`shift_click_command` フィールド内で使用できるプレースホルダーです:

| プレースホルダー | 置換される値 |
|---|---|
| `[label]` | ゲームモードのプレイヤーコマンドラベル（例: `island`、`ob`） |
| `[player]` | クリックしたプレイヤーのユーザー名 |
| `[server]` | プレイヤーの代わりにサーバーコンソールとしてコマンドを実行させます |

#### 説明プレースホルダー

`description` フィールド内で使用できるプレースホルダーです:

| プレースホルダー | 置換される値 |
|---|---|
| `[gamemode]` | ゲームモード名の小文字（例: `bskyblock`、`aoneblock`） |
| `%placeholder%` | PlaceholderAPI の登録済みプレースホルダー |

#### スロットレイアウト

GUI はチェストインベントリです。各行には 9 つのスロット（0〜8）があり、最大は 6 行のチェストで 54 スロット（0〜53）です:

```
行 1:  0  1  2  3  4  5  6  7  8
行 2:  9 10 11 12 13 14 15 16 17
行 3: 18 19 20 21 22 23 24 25 26
行 4: 27 28 29 30 31 32 33 34 35
行 5: 36 37 38 39 40 41 42 43 44
行 6: 45 46 47 48 49 50 51 52 53
```

`"0-8"` のような引用符付き範囲を使うと、一行全体に同じボタンを配置できます。装飾的なボーダーに便利です。

## 例: デフォルトパネルと VIP パネル

以下は 2 つのパネルを示す実用的な例です。全プレイヤー用のデフォルトパネルとドナー用の VIP パネルです。スロット範囲、複数クリックアクション、コンソールコマンド、PlaceholderAPI プレースホルダー、ItemsAdder アイコンを使用しています。

```yaml
panel-list:

  # Default panel — shown to all players
  default:
    defaultPanel: true
    panelName: '&0&l Control Panel'
    permission: 'default'
    buttons:

      # Decorative top border using a slot range
      "0-8":
        name: ' '
        material: BLACK_STAINED_GLASS_PANE
        description: ''
        command: ''

      # Go to island with multiple click actions
      9:
        name: '&a&l Go to Island'
        icon: minecraft:grass_block
        description: |-
          &7 Left-click: teleport to your island
          &7 Right-click: go to nether
          &7 Shift-click: set home
          &7 Island level: &e%Level_[gamemode]_island_level%
        command: '[label] go'
        right_click_command: '[label] go nether'
        shift_click_command: '[label] sethome'

      10:
        name: '&e&l Set Home'
        icon: minecraft:white_bed
        description: |-
          &7 Set your island home
          &7 to your current location.
        command: '[label] sethome'

      11:
        name: '&b&l Team'
        icon: minecraft:player_head
        description: |-
          &7 View and manage
          &7 your island team.
        command: '[label] team'

      13:
        name: '&6&l Settings'
        icon: minecraft:anvil
        description: |-
          &7 Configure your island
          &7 protection settings.
        command: '[label] settings'

      # Console command — runs as server, not player
      17:
        name: '&c&l Report Bug'
        icon: minecraft:writable_book
        description: |-
          &7 Opens a support ticket.
        command: '[server] ticket create [player] bug-report'

  # VIP panel — players need bskyblock.controlpanel.panel.vip
  vip:
    defaultPanel: false
    panelName: '&d&l VIP Control Panel'
    permission: 'vip'
    buttons:

      "0-8":
        name: ' '
        material: PURPLE_STAINED_GLASS_PANE
        description: ''
        command: ''

      9:
        name: '&a&l Go to Island'
        icon: minecraft:grass_block
        description: |-
          &7 Teleport to your island.
        command: '[label] go'

      # VIP exclusive — grants a kit via console
      13:
        name: '&d&l VIP Kit'
        icon: minecraft:chest
        description: |-
          &d VIP exclusive!
          &7 Claim your weekly VIP kit.
        command: '[server] kit vipweekly [player]'

      # ItemsAdder custom icon example
      14:
        name: '&6&l VIP Perks'
        itemsadder: 'iasurvival:vip_star'
        description: |-
          &7 Browse all your VIP perks.
        command: 'vipperks'
```

## ヒント

??? tip "装飾的なボーダーの作成"
    スロット範囲とガラスパネルを使ってパネルのきれいなボーダーを作成できます。`command: ''` と `name: ' '` を設定してボタンを非インタラクティブにします:
    ```yaml
    "0-8":
      name: ' '
      material: BLACK_STAINED_GLASS_PANE
      description: ''
      command: ''
    ```

??? tip "コンソールとしてコマンドを実行する"
    コマンドの前に `[server]` を付けるとサーバーコンソールとして実行されます。プレイヤーが直接実行する権限を持たないキット付与、経済コマンド、管理者アクションなどが実行できます:
    ```yaml
    command: '[server] give [player] diamond 64'
    ```

??? tip "ランク別の複数パネルを使用する"
    デフォルト、VIP、スタッフなど異なるプレイヤーグループ用に別々のパネルを作成できます。`bskyblock.controlpanel.panel.vip` や `bskyblock.controlpanel.panel.staff` のような権限を使って割り当てます。各グループには適切なボタンを持つカスタマイズされたパネルが表示されます。

??? tip "説明に PlaceholderAPI を使用する"
    ボタンの説明はパネルが開かれた時点で PlaceholderAPI によって処理されるため、常にライブデータが表示されます。プレースホルダー名の中に `[gamemode]` を使うと、同じテンプレートが複数のゲームモードで機能します:
    ```yaml
    description: |-
      &7 Level: &e%Level_[gamemode]_island_level%
      &7 Rank: &6%Level_[gamemode]_island_rank%
      &7 Balance: &a%vault_balance%
    ```

??? tip "変更後のリロード"
    `controlPanelTemplate.yml` を編集した後、`/{admin} bentobox reload` を実行します（**1.16.1** からはテンプレートが再インポートされます）。または `/{admin} cp import` でインポートします。`config.yml` に変更を加えた場合も `/{admin} bentobox reload` を使用してください。

## よくある質問

??? question "ControlPanel を変更するにはどうすればいいですか？"
    ControlPanel はパネルをデータベースに保存しますが、テンプレートファイルを通じて編集します。`controlPanelTemplate.yml` に変更を加えた後、`/{admin} bentobox reload`（**1.16.1+**）を実行するか、`/{admin} controlpanel import` でインポートします。追加のテンプレートファイルを作成して名前でインポートすることもできます: `/{admin} controlpanel import myPanels`。または、`template-file` 設定オプションで独自のファイルを指定できます。

??? question "ユーザーごとに異なるパネルを設定できますか？"
    はい。テンプレートファイルで複数のパネルを定義し、それぞれに異なる `permission` サフィックスを付けます。その後、プレイヤーに対応する権限（例: `bskyblock.controlpanel.panel.vip`）を割り当てます。特定のパネル権限を持たないプレイヤーには `defaultPanel: true` のマークが付いたパネルが表示されます。

??? question "どのアイコンタイプがサポートされていますか？"
    ControlPanel は 3 つのアイコンタイプをサポートしており、この優先順位で確認されます: ItemsAdder カスタムアイテム（`itemsadder` フィールド）、BentoBox ItemParser 形式（`icon` フィールド）、バニラの Minecraft マテリアル（`material` フィールド）。何も指定されていない場合、ボタンのデフォルトは paper です。

??? question "コンソールとしてコマンドを実行できますか？"
    はい。コマンドの前に `[server]` を付けると、プレイヤーの代わりにコンソールとして実行されます。コマンド文字列に `[player]` を使ってクリックしたプレイヤーの名前を挿入することもできます。例: `[server] give [player] diamond 64`。

??? question "クリック方法によって異なる動作をするボタンを作れますか？"
    はい。各ボタンは最大 3 つの異なるコマンドをサポートします: 左クリック用の `command`、右クリック用の `right_click_command`、Shift+左クリック用の `shift_click_command`。特定のクリックコマンドが設定されていない場合、通常の `command` にフォールバックします。

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/ControlPanel/issues)のリストに追加してください。

## 変更履歴

!!! warning "v1.16.1 の新機能 — リロードで保存済みパネルが上書きされるようになりました"
    **リリース日:** 2026 年 9 月 2 日

    互換性: BentoBox 2.7.1 以降（3.7.4 で Minecraft 1.21.4 での動作確認）· Minecraft 1.21.4 – 26.2 · Java 21。

    - 🔺 ⚙️ **`bbox reload` がテンプレートを再インポートするようになりました。** `controlPanelTemplate.yml` を編集してリロードしても何も起こりませんでした。パネルはデータベースに存在し、テンプレートは一度だけ初期化に使用されたためです。リロードは各アクティブなゲームモードの保存済みパネルをすべて削除し、テンプレートから再インポートするようになったので、`cp import` なしにテンプレート編集が有効になり、テンプレートから削除されたパネルは残る代わりに消えるようになります。
    - ⚙️ **新しい `template-file` 設定オプション**（デフォルト `controlPanelTemplate.yml`）。リロード、初期シード化、管理コマンド `import` すべてがこれに従うので、アドオンを独自のファイルに指定できます。
    - 🔺 **BentoBox の最小バージョンを 2.7.1 に引き下げました。** 1.16.0 は 3.10.0 の `api-version` を宣言していましたがコードには必要なく、BentoBox 3.10+ が実行できないサーバー（特に Minecraft 1.21.4 で上限が BentoBox 3.7.4）では BentoBox がそれを拒否（`INCOMPATIBLE`）していました。これらのサーバーは現在の ControlPanel を再度使用できます。
    - 🔡 繁体字中国語（`zh-TW`）翻訳を更新しました。

    🔺 **リロードで保存済みパネルが上書きされるようになりました。** データベース専用のパネル変更（`controlPanelTemplate.yml` に含まれていないもの）に依存している場合は、アップデート前にそれらをテンプレートに入れてください。さもないと次のリロード時に失われます。新しい `template-file` キーは自動的に `config.yml` に追加されます。既存のインストールは何の変更もなく動き続けます。

    [Release v1.16.1](https://github.com/BentoBoxWorld/ControlPanel/releases/tag/1.16.1)

## 翻訳

{{ translations("ControlPanel") }}
