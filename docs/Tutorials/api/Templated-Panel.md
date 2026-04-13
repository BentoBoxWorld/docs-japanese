# BentoBox TemplatedPanel ドキュメント

BentoBox の TemplatedPanel は Minecraft 開発者向けの強力なツールで、インベントリベースのカスタマイズ可能なユーザーインターフェース（UI）を簡単に作成できます。YAML でパネルレイアウトを定義することで、コードを大幅に変更することなく UI 要素を素早く調整できます。TemplatedPanel を YAML で設定する方法の詳細な説明です。

## パネルの定義

### パネルの識別
- `detail_panel`: コード内での参照のためにパネルの一意の名前を定義します。

### パネルのタイトル
- `title`: パネルの表示タイトルを設定します。このタイトルはロケールファイルの参照を通じてローカライズできます。

### パネルタイプ
- `type`: 表示するインベントリのタイプを選択します。オプションは `INVENTORY`、`HOPPER`、`DROPPER` です。

### バックグラウンドとボーダー
- `background`: Minecraft のアイテムを使用してパネルのバックグラウンドをカスタマイズします。例えば、`BLACK_STAINED_GLASS_PANE` を装飾効果として使用できます。
- `border`: Minecraft のアイテムを使用してパネルのボーダーの外観を定義します。これにより、パネルのアイテムとのコントラストが生まれます。

### 表示設定
- `force-shown`: パネルで表示する行を指定し、パネルの縦サイズに影響します。

## コンテンツの設定

### ボタンのレイアウトと機能
- `content`: このセクション内でパネルの各アイテムまたはボタンを詳細に設定します。行番号と列番号を使用して各要素を配置します。
  - `icon`: ボタンアイコンとして使用する Minecraft アイテムを設定します。
  - `title`: ボタンのタイトルを指定します。ローカライズ可能です。
  - `description`: ボタンの説明を追加します。ローカライズ可能です。
  - `data`: ボタンの機能に関連するデータ（トリガーするアクションのタイプなど）を含めます。
  - `actions`: ボタンが操作されたときに発生するアクションを定義し、クリックのタイプとツールチップを指定します。

### 再利用可能なボタン
- `reusable`: パネル内で複数回使用されるボタンのテンプレートを定義します。
  - このセクション内で、ボタンのアイコン、タイトル、説明、関連データなどの詳細を指定します。

## ボタン設定の例
- 行 1、列 2 のボタン:
  ```yaml
  1:
    2:
      icon: STONE
      title: level.gui.buttons.all_blocks.name
      description: level.gui.buttons.all_blocks.description
      data:
        type: TAB
        tab: ALL_BLOCKS
      actions:
        view:
          click-type: unknown
          tooltip: level.gui.tips.click-to-view
  ```

- `material_button` という名前の再利用可能なボタン:
  ```yaml
  reusable:
    material_button:
      title: level.gui.buttons.material.name
      description: level.gui.buttons.material.description
      data:
        type: BLOCK
  ```

この TemplatedPanel システムにより、BentoBox 開発者はゲーム内でインタラクティブな UI 要素を設計・実装するための合理的で柔軟な方法を得られ、ユーザーエンゲージメントと機能性が向上します。

# TemplatedPanelBuilder ドキュメント

`TemplatedPanelBuilder` クラスは BentoBox API の一部であり、`TemplatedPanel` オブジェクトの作成を容易にするために設計されています。テンプレート、ユーザーコンテキスト、ワールドコンテキスト、リスナーなど、さまざまなカスタマイズオプションを持つパネルを構築するための流れるようなインターフェースを提供します。機能と使用法の概要です。

## クラスの概要

`TemplatedPanelBuilder` は `TemplatedPanel` のインスタンスを構築するために使用されます。Minecraft ワールド、特に BentoBox フレームワーク内でのパネルの動作に必要なさまざまなパラメーターと設定を設定できます。

## メソッド

### テンプレートメソッド

- `template(String guiName, File dataFolder)`: GUI 名とデータフォルダに基づいてパネルのテンプレートを設定します。チェーン用に `TemplatedPanelBuilder` インスタンスを返します。
- `template(String panelName, String templateName, File dataFolder)`: パネル名、テンプレート名、データフォルダに基づいてパネルのテンプレートを設定します。バージョン 1.20.0 で導入されました。チェーン用に `TemplatedPanelBuilder` インスタンスを返します。

### ユーザーメソッド

- `user(User user)`: パネルを作成するユーザーを設定します。チェーン用に `TemplatedPanelBuilder` インスタンスを返します。

### ワールドメソッド

- `world(World world)`: パネルのワールドコンテキストを設定します。チェーン用に `TemplatedPanelBuilder` インスタンスを返します。

### パラメーターメソッド

- `parameters(@NonNull String... parameters)`: パネルタイトルのパラメーターを設定します。チェーン用に `TemplatedPanelBuilder` インスタンスを返します。バージョン 1.20.0 から利用可能です。
- 例: `panelBuilder.parameters("[name]", this.user.getName());` はユーザーの名前をパネルのタイトルに配置します。

### リスナーメソッド

- `listener(PanelListener listener)`: ユーザーインタラクションを処理するための `PanelListener` をパネルに追加します。チェーン用に `TemplatedPanelBuilder` インスタンスを返します。
- リスナーは、別のタブへの移動やクリックへの反応などの機能は API 内で処理されるため、必須ではありません。
- カスタム機能が必要な場合にのみリスナーが必要になる場合があります。

### タイプビルダーの登録

- `registerTypeBuilder(String type, BiFunction<ItemTemplateRecord, TemplatedPanel.ItemSlot, PanelItem> buttonCreator)`: パネルの新しいボタンタイプビルダーを登録します。チェーン用に `TemplatedPanelBuilder` インスタンスを返します。
- 例:
```
        panelBuilder.registerTypeBuilder("NEXT", this::createNextButton);
        panelBuilder.registerTypeBuilder("PREVIOUS", this::createPreviousButton);
        panelBuilder.registerTypeBuilder("BLOCK", this::createMaterialButton);
```
- 関連付けられた名前のボタンがクリックされると、適切なメソッドが呼び出されます。ItemTemplateRecord、ItemSlot、PanelItem が渡されます。

### ビルドメソッド

- `build()`: 提供された設定に基づいて `TemplatedPanel` インスタンスを構築して返します。

## ゲッター

- `getPanelTemplate()`: 現在の `PanelTemplateRecord` を取得します。
- `getUser()`: パネルに関連付けられた `User` オブジェクトを取得します。
- `getWorld()`: パネルの `World` コンテキストを返します。
- `getParameters()`: パネルタイトルに設定されたパラメーターのリストを取得します。
- `getListener()`: パネルに接続された `PanelListener` を返します。
- `getObjectCreatorMap()`: オブジェクトとそのパネルアイテムクリエーターをリンクするマップへのアクセスを提供します。

## 変数

- `panelTemplate`: GUI テンプレートレコードを保存します。
- `user`: GUI を開くユーザーへの参照を保持します。
- `world`: GUI が動作するワールドを表します。
- `listener`: GUI インタラクションを処理するための `PanelListener` を保存します。
- `parameters`: タイトルオブジェクトのパラメーターを保存するリスト。
- `objectCreatorMap`: オブジェクトタイプとそれぞれのパネルアイテムクリエーターをリンクするマップ。

## 使用法

`TemplatedPanelBuilder` を使用するには、インスタンス化してメソッドをチェーンしてパネルを必要に応じて設定します。すべての設定が完了したら、`build()` メソッドを呼び出して `TemplatedPanel` インスタンスを作成します。

例:

```
        // Start building panel.
        TemplatedPanelBuilder panelBuilder = new TemplatedPanelBuilder();
        panelBuilder.user(this.user);
        panelBuilder.world(this.user.getWorld());

        panelBuilder.template("detail_panel", new File(this.addon.getDataFolder(), "panels"));

        panelBuilder.parameters("[name]", this.user.getName());

        panelBuilder.registerTypeBuilder("NEXT", this::createNextButton);
        panelBuilder.registerTypeBuilder("PREVIOUS", this::createPreviousButton);
        panelBuilder.registerTypeBuilder("BLOCK", this::createMaterialButton);

        panelBuilder.registerTypeBuilder("FILTER", this::createFilterButton);

        // Register tabs
        panelBuilder.registerTypeBuilder("TAB", this::createTabButton);

        // Register unknown type builder.
        panelBuilder.build();
```
