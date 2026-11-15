# メニューのカスタマイズ

BentoBoxプレイヤーが見るほとんどのメニュー（チームメニュー、アイランド設定、アイランド作成メニュー、ホーム、言語など）は、**パネルテンプレート**から構築されています。編集可能なYAMLファイルです。メニューのタイトル、サイズ、背景、各ボタンに使用するアイコン、テキスト、配置を変更できます。

新しい種類のボタンを作成することはできません。各メニューは、そのコードが提供するボタンタイプのみを理解しています。コマンドを実行するボタンを持つ独自のメニューの場合は、[ControlPanel](../../addons/ControlPanel/index.md)アドオンを使用してください。

## メニューファイルの場所

| メニュー元 | フォルダ |
|---|---|
| BentoBox | `plugins/BentoBox/panels/` |
| ゲームモード（そのゲームモードのみ） | `plugins/BentoBox/addons/<GameMode>/panels/` |
| アドオン（Level、Challenges、Warpsなど） | `plugins/BentoBox/addons/<Addon>/panels/` |

BentoBoxは各メニューが初めて使用されたときに、テンプレートを`plugins/BentoBox/panels/`に書き込みます。アドオンは自分のフォルダに書き込みます。

### BentoBoxのメニュー

| ファイル | メニュー | ゲームモードが独自のコピーを持つことができるか |
|---|---|---|
| `island_creation_panel.yml` | アイランド作成またはリセット時にアイランドを選択 | はい |
| `island_homes_panel.yml` | `/island homes` | はい |
| `language_panel.yml` | `/island language` | はい |
| `settings_panel.yml` | `/island settings` | はい |
| `admin_settings_panel.yml` | `/bsbadmin settings` | はい |
| `command_ranks_panel.yml` | 設定メニューのコマンドランクページ | はい |
| `team_panel.yml` | `/island team` | いいえ |
| `team_invite_panel.yml` | チームメニューの招待画面 | いいえ |
| `placeholder_panel.yml`、`placeholder_list_panel.yml` | プレースホルダーブラウザ | いいえ |

**ゲームモードごとに異なるメニュー：** `plugins/BentoBox/panels/`からファイルをゲームモードの`panels`フォルダにコピーし（必要に応じてフォルダを作成）、コピーを編集します。例えば、`plugins/BentoBox/addons/AOneBlock/panels/island_creation_panel.yml`はAOneBlockのみのアイランド作成メニューを変更します。他のゲームモードはBentoBoxバージョンを使用し続けます。

### アドオンメニュー

テンプレートを使用するアドオンには、Level（`top_panel`、`value_panel`、`detail_panel`、`donation_panel`）、Challenges、Biomes、Warps、Upgrades、Likes、Visit、TopBlock、CheckMeOut、MagicCobblestoneGenerator、AOneBlock（`phases_panel`）、CauldronWitcheryが含まれます。各アドオンの`panels`フォルダを確認してください。以下と同じフォーマットを使用します。

## 変更を加える

1. プレイヤーがメニューを開かないようにするか、テストサーバーで行ってください。
2. `.yml`ファイルを編集します。元のコピーを保存しておきます。
3. `/bentobox reload`を実行します。これにより開いているメニューが閉じられ、テンプレートが再度読み込まれます。
4. ゲーム内でメニューを開いて確認します。

メニューが開かなくなったり、何も表示されない場合は、YAMLが無効である可能性があります。サーバーコンソールでエラーを確認し、ファイルをYAMLチェッカーに貼り付けてください。**デフォルトに戻すには**、ファイルを削除します。メニューが次に開かれるときに、BentoBoxはデフォルトをコピーします。アドオンのファイルの場合は、サーバーを再起動します。

## よくある変更

### タイトルまたはボタンのテキストを変更する { #change-the-title-or-button-text }

テキストはプレーンテキストまたは**ロケールキー**のいずれかです。デフォルトテンプレートはロケールキーを使用しているため、メニューが翻訳されます：

```yaml
team_panel:
  title: commands.island.team.gui.titles.team-panel
```

- **すべての言語でテキストを変更する：** ロケールファイル（`plugins/BentoBox/locales/`またはアドオンの`locales`フォルダ）でそのキーを編集します。[言語とメッセージ](../../BentoBox/About/Multilingual.md)を参照してください。
- **すべてのユーザーに同じテキストを使用する：** キーを独自のテキストに置き換えます。例えば`title: "&6My Team"`。

### 背景またはボーダーを変更する

```yaml
  background:
    icon: GRAY_STAINED_GLASS_PANE
    title: "&b&r"     # 名前を表示しない
  border:
    icon: LIGHT_BLUE_STAINED_GLASS_PANE
    title: "&b&r"
```

`background`または`border`セクションを削除して、これらのスロットを空にします。`"&b&r"`は名前を持たないアイテムを表示する通常の方法です。Minecraftは常にツールチップを表示するため、完全に非表示にすることはできません。

### ボタンのアイコンを変更する

ボタンに`icon`を設定します。データを持つアイテム、ポーション色、プレイヤーの頭を含む任意のアイテムが機能します。[アイテムフォーマット](../../BentoBox/ItemParser.md)を参照してください。

```yaml
      icon: DIAMOND
      icon: tipped_arrow[potion_contents={custom_color:11546150}]
```

`icon`を省略した場合、いくつかのボタンは独自のアイコンを選択します。例えば、チームメニューはプレイヤーの頭を表示し、アイランド作成メニューはアイランドのアイコンを表示します。

### ボタンを移動する

ボタンは`content`の下の**行**（1～6）と**列**（1～9）で配置されます。ボタンを移動するには、その行番号または列番号を変更します：

```yaml
  content:
    1:        # 行1
      1:      # 列1
        data:
          type: STATUS
```

### メニューを高くする

メニューはボタンを持つ行に合わせて縮小します。空の行でも保持するには、`force-shown`を使用します：

```yaml
  force-shown: 6        # 常に行1～6を表示
  force-shown: [2, 4]   # 常に行2と4を表示
```

これは空の行のみを追加します。**ページあたりより多くのアイテムを表示**する（より多くのアイランド、より多くのホーム）には、繰り返しボタンをより多く新しいスロットに追加してください。[アイランド作成メニューを大きくする](Bigger-Create-Island-Menu.md)ページがこれについて詳しく説明しています。

### ボタンを削除する

`content`からボタンを削除します。スロットは背景を表示します。メニューが機能するために必要なボタンもあります。複数ページを持つことができるメニューで`NEXT`/`PREVIOUS`ボタンを保持してください。

## テンプレートがどのように配置されているか

すべてのテンプレートは同じ部分を持っています。この短縮された例はアイランド作成メニューに基づいています：

```yaml
island_creation_panel:          # ファイル名と一致する必要があります
  title: panels.island_creation.title
  type: INVENTORY               # INVENTORY（チェスト）、HOPPER（5スロット）、またはDROPPER（9スロット）
  background:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  border:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  force-shown: []
  content:
    2:
      2: blueprint_bundle_button    # 名前は`reusable`のボタンを参照します
      3: blueprint_bundle_button
    3:
      9:                            # またはボタンをここに直接定義します
        icon: ARROW
        title: panels.buttons.next.name
        description: panels.buttons.next.description
        data:
          type: NEXT
        actions:
          next:
            click-type: UNKNOWN
            tooltip: panels.tips.click-to-next
  reusable:
    blueprint_bundle_button:
      title: panels.island_creation.buttons.bundle.name
      description: panels.island_creation.buttons.bundle.description
      data:
        type: BUNDLE
      actions:
        select:
          click-type: UNKNOWN
          tooltip: panels.tips.click-to-choose
```

### ボタン設定

| 設定 | 機能 |
|---|---|
| `icon` | 表示されるアイテム。[アイテムフォーマット](../../BentoBox/ItemParser.md)を参照 |
| `title` | アイテムの名前：テキストまたはロケールキー |
| `description` | 名前の下の行：テキストまたはロケールキー |
| `data` | **ボタンが何であるか。** `type`はボタンのタイプを選択します（以下を参照）。いくつかのタイプは追加の設定を取ります。例えば、設定タブボタンの`tab` |
| `actions` | 各クリックが実行することとそれに追加されるツールチップ行 |
| `fallback` | このボタンを表示できない場合に代わりに表示する別のボタン。例えば、最後のページのスロットを埋めるものが何も残っていない場合。完全なボタンまたは`reusable`ボタンの名前にすることができます。BentoBox 3.23.0以降が必要です |

### 繰り返しボタン（`reusable`）

リストを表示するメニュー（アイランド、ホーム、チームメンバー、言語、フラグ）は、すべてのエントリに対して1つのボタンデザインを使用します。`reusable`の下に1回定義し、エントリが表示される可能性がある各スロットにその名前を配置します。メニューはこれらのスロットを順番に埋め、残りをページングします。

### クリックアクション

各アクションは名前、クリックタイプ、ツールチップを持っています：

```yaml
        actions:              # チームメニューのメンバーボタン
          kick:
            click-type: SHIFT_RIGHT
            tooltip: commands.island.team.gui.tips.SHIFT_RIGHT.kick
          setowner:
            click-type: SHIFT_LEFT
            tooltip: commands.island.team.gui.tips.SHIFT_LEFT.setowner
```

- `click-type`はMinecraftクリックです：`LEFT`、`RIGHT`、`SHIFT_LEFT`、`SHIFT_RIGHT`、`MIDDLE`、`DROP`など。`UNKNOWN`は任意のクリックを意味します。
- アクション名（`kick`、`setowner`）はメニューが行うことです。デフォルトファイルに既にある名前を使用してください。どのクリックがアクションをトリガーするかを変更したり、プレイヤーがメニューから使用したくないアクションを削除したりできます。
- ツールチップは説明の下に、アクションが列挙された順序で追加されます。

### BentoBoxのメニューのボタンタイプ

| メニュー | ボタンタイプ（`data: type:`） |
|---|---|
| アイランド作成 | `BUNDLE`、`NEXT`、`PREVIOUS` |
| ホーム | `ISLAND`、`NEXT`、`PREVIOUS` |
| 言語 | `LOCALE`、`NEXT`、`PREVIOUS` |
| チーム | `STATUS`、`MEMBER`、`RANK`、`INVITE`、`INVITED` |
| チーム招待 | `PROSPECT`、`SEARCH`、`BACK`、`NEXT`、`PREVIOUS` |
| 設定／管理者設定 | `FLAG`、`TAB`、`MODE`、`RESET`、`NEXT`、`PREVIOUS` |
| コマンドランク | `COMMAND`、`NEXT`、`PREVIOUS` |
| プレースホルダー | `BENTOBOX`、`ADDON`、`PLACEHOLDER`、`BACK`、`NEXT`、`PREVIOUS` |

デフォルトファイルには各タイプの説明がコメントされています。設定メニューは[保護、フラグとランク](../../BentoBox/Island-Protection,-Flags-&-Ranks.md#customizing-the-settings-panel)で詳しく説明されています。

## トラブルシューティング

**私の変更が表示されません。**
`/bentobox reload`を実行してからメニューを再度開いてください。ゲームモードが`addons/<GameMode>/panels/`に独自のコピーを持っている場合、そのコピーが`plugins/BentoBox/panels/`のコピーの代わりに使用されます。

**メニューが空であるか、編集後に開かない。**
YAMLが無効であるか、トップレベルの名前がファイル名と一致しなくなっています。コンソールをチェックしてファイルを修正するか、ファイルを削除してデフォルトに戻します。

**行を追加しましたが、何も表示されません。**
`force-shown`は空きスペースのみを追加します。新しいスロットに繰り返しボタン（例えば`blueprint_bundle_button`）を追加してください。

**テキストが単語ではなく`commands.island.…`として表示される。**
そのキーがプレイヤーの言語のロケールファイルにありません。追加するか、プレーンテキストを代わりに使用してください。

**コマンドを実行するボタンが必要です。**
テンプレートはこれを実行できません。[ControlPanel](../../addons/ControlPanel/index.md)アドオンを使用してください。

## 関連項目

- [アイランド作成メニューを大きくする](Bigger-Create-Island-Menu.md)：完全な実例
- [アイテムフォーマット](../../BentoBox/ItemParser.md)：アイコンの書き方
- [言語とメッセージ](../../BentoBox/About/Multilingual.md)：メニューテキストの変更
- [テンプレートパネルAPI](../api/Templated-Panel.md)：独自のアドオンにテンプレートを追加する開発者向け
