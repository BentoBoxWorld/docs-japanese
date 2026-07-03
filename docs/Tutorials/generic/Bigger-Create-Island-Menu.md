# アイランド作成メニューを大きくする（行数を増やす）

**質問：** 「アイランド作成メニューをもっと大きくすることはできますか？デフォルトの3行ではなく、5行または6行にしたいのですが」

**回答：** はい。アイランド作成メニューは完全に[カスタマイズ可能な GUI](Customizable-GUI.md)です。行数とそれぞれのページに表示されるブループリント バンドル の数は、`island_creation_panel.yml`テンプレートを編集することで制御できます。このページでは、その方法を説明します。

最初に、以下のどれが必要かを決めてください。それぞれ異なる変更が必要です：

- **メニューを*見た目上*高くしたいだけ**（スペースがある、大きく見える、など）→ 以下の[`force-shown`ショートカット](#メニューを高くしたいだけ-force-shown)を使用します。追加の行は空の背景で埋められます。
- **もっと多くのアイランドを一度に見たい / ページ数を減らしたい** → [6行メニューの例](#例-6行メニュー)を参照して、さらにバンドルボタンを追加する必要があります。`force-shown`だけではこれを実現できません。

## メニューを高くしたいだけ？（`force-shown`）

メニューを高くしたいだけで、必ずしももっと多くのアイランドを画面に表示する必要がない場合は、1行の変更で済みます。`island_creation_panel.yml`に`force-shown`行を追加（または編集）します：

```yaml
force-shown: 6
```

`force-shown: 6`は行1〜6を常に表示するようにを強制し、完全な**6行（54スロット）**パネルを提供します。5行の場合は`5`を使用するなど、同様に機能します。

**重要：** `force-shown`はパネルの**高さのみ**を制御します。開くことになった追加の行は、`background`/`border`アイテムで満たされます。追加のアイランド バンドル を含むわけではありません。バンドルは、`content`セクションに`blueprint_bundle_button`エントリが存在する場所にのみ表示されます。したがって、目標が*もっと多くのアイランドを一度に表示する*ことである場合（単にボックスを大きくすることではない場合）は、[6行メニュー例](#例-6行メニュー)をスキップして、追加のバンドルボタンも追加します。

## 背景：メニューの構築方法

アイランド作成メニュー（およびプレイヤーがアイランドをリセットする時に表示される同一のメニュー）は、`island_creation_panel.yml`というパネルテンプレートから生成されます。BentoBoxには、**3行**とページあたり最大**7個のバンドルボタン**を備えたデフォルトバージョンが付属しています（より多くのバンドルがある場合は、ページングのための「前へ」/「次へ」矢印ペアがあります）。

プレイヤーが実際に見る行数は、2つのルールによって決まります：

1. **パネルはそのコンテンツに適応して成長します。** ボタンを含む場合は行が表示されます。内部的にはグリッドは常に6行ですが、空の行は削除されるため、デフォルトのテンプレートは行1、5、6が空なので、見た目上は3行のように見えます。
2. **`force-shown`は空の行も開いたままにできます**（バンドル リストが成長しても、固定レイアウトを保つのに便利です）。

つまり、メニューを大きくするには、単に`blueprint_bundle_button`エントリをより多くの行に追加します。**6行**（54スロット）がハードマックスです。これは Minecraft チェストインベントリが最大サイズだからです。

## ファイルの配置場所

メニューは2つのレベルでオーバーライドできます。BentoBoxは次の順序でファイルを探します：

1. **ゲームモード単位**（推奨） — `plugins/<GameMode>/panels/island_creation_panel.yml`
   例：`plugins/AcidIsland/panels/island_creation_panel.yml`、`plugins/BSkyBlock/panels/island_creation_panel.yml`。
   これは、そのゲームモードにのみ影響します。
2. **グローバルフォールバック** — `plugins/BentoBox/panels/island_creation_panel.yml`
   独自のコピーを持たないゲームモードで使用されます。

どちらのファイルも存在しない場合は、組み込みのデフォルト（BentoBox jar内）が使用されます。

> **ヒント：** ゼロから書くのではなく、デフォルトファイルをコピーしてください。サーバーを一度起動するので、BentoBoxがデフォルトを書き出し、その後`plugins/BentoBox/panels/island_creation_panel.yml`をゲームモードの`panels/`フォルダにコピーして編集します。保存後に`/bentobox reload`を実行するか、サーバーを再起動してください。

## 例：6行メニュー

このテンプレートは、枠のレイアウトを備えた完全な6行メニューを示しています。行2〜5はブループリント バンドル ボタンを保持し（ページあたり最大**28**のバンドル）、行6はページング矢印を保持します。

```yaml
island_creation_panel:
  title: panels.island_creation.title
  type: INVENTORY
  background:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  border:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  # すべての6行が常に表示されるようにピンします。代わりに[]を使用して、
  # パネルをコンテンツに自動サイズさせます。
  force-shown: 6
  content:
    2:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    3:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    4:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    5:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    6:
      1:
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: panels.buttons.previous.name
        description: panels.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        actions:
          previous:
            click-type: UNKNOWN
            tooltip: panels.tips.click-to-previous
      9:
        icon: tipped_arrow[potion_contents={custom_color:8439583}]
        title: panels.buttons.next.name
        description: panels.buttons.next.description
        data:
          type: NEXT
          indexing: true
        actions:
          next:
            click-type: UNKNOWN
            tooltip: panels.tips.click-to-next
  reusable:
    blueprint_bundle_button:
      # icon: GRASS_BLOCK   # すべてのバンドルに対して1つのアイコンを強制するには、
                            # コメント外してください。そうしない場合、各バンドルは独自に
                            # 設定されたアイコンを使用します。
      title: panels.island_creation.buttons.bundle.name
      description: panels.island_creation.buttons.bundle.description
      data:
        type: BUNDLE
      actions:
        select:
          click-type: UNKNOWN
          tooltip: panels.tips.click-to-choose
```

### 代わりに5行メニューにしたい場合

`content`から行`5`を削除し、`force-shown: 6`を`force-shown: 5`に変更します。必要に応じて、ページング矢印を行`5`に移動します。1〜6の行数は同じように機能します — `blueprint_bundle_button`エントリの行を追加または削除するだけです。

## パーツの仕組み

| 設定 | 機能 |
|---|---|
| `content`行`1`〜`6` | 各キー`1`〜`6`は行です。各ネストされたキー`1`〜`9`は列です。行にコンテンツがある場合（または強制されている場合）のみ表示されます。 |
| `blueprint_bundle_button` | `type: BUNDLE`の再利用可能なボタン。**このテンプレート内のこれらのボタンの数=ページあたりに表示されるバンドルの数。** より多くのバンドルをそれぞれ表示するには、さらに追加します。 |
| `force-shown` | `force-shown: 6`は行1〜6を常に強制的にレンダリングします（固定高さ）。`force-shown: [2,4]`は行2と4のみを強制します。`force-shown: []`（またはそれを省略）では、パネルをそのコンテンツに自動サイズさせます。 |
| `type: PREVIOUS` / `type: NEXT` | ページング矢印。1ページに収まる以上のバンドルがある場合のみ表示されるため、常に含めても安全です。 |
| `unique_id`（オプション） | ボタンの`data:`の下に`unique_id: <bundleId>`を追加すると、1つの特定のバンドルをその正確なスロットにピンし、順序に従って埋めるのではなく。 |

## よくある質問

**「行を追加しましたが、メニューはまだ小さいままです。」**
行は、ボタンを含む*または*`force-shown`にリストされている場合にのみ表示されます。各新しい行に実際に`blueprint_bundle_button`エントリが含まれていることを確認し、YAML インデント（行と列は`content`の下にネストされた数値キー）を確認してください。

**「6行より大きくすることはできますか？」**
いいえ。6行/54スロットは Minecraft チェスト GUI の最大サイズであるため、`INVENTORY`タイプのパネルの上限です。

**「変更しても何も起こりませんでした。」**
ファイルがテストしているゲームモードの正しいフォルダにあることを確認してください（モード単位のフォルダはグローバル BentoBox フォルダより優先されます）、ファイルの名前は正確に`island_creation_panel.yml`です。編集後に`/bentobox reload`を実行するか、サーバーを再起動しました。YAML 構文エラーはBentoBoxが組み込みのデフォルトにフォールバックします — 起動時のサーバーコンソールで警告を確認してください。

**「これによってプレイヤーが*アイランドをリセット*する際のメニューも変わりますか？」**
はい。リセット アイランド メニューは同じ`island_creation_panel.yml`テンプレートを使用します。

## 参照

- [カスタマイズ可能な GUI](Customizable-GUI.md) — これらのメニューが構築される基盤となるシステム、アイテム/アイコン オプションの完全なリスト。
- [ItemParser](https://docs.bentobox.world/en/latest/BentoBox/ItemParser/) — `icon:`フィールドの構文。
