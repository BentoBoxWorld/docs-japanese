## カスタマイズ可能な GUI

BentoBox 1.17 では GUI カスタマイズの API が導入されました。ただし、必要な変更の数が多いため、すべてがカスタマイズ可能なわけではなく、この機能を実装しているアドオンはまだ少数です。

カスタマイズ可能な GUI の例:
```yaml
# The name of the panel. It must be the same as file name.
panel_name:
  # Title of the panel
  title: "The Panel Title"
  # Panel Type:
  # INVENTORY - chest GUI type
  # HOPPER - hopper GUI type
  # DROPPER - dropper/dispenser GUI type.
  type: INVENTORY
  # Background item for empty slots
  background:
    # Icon for the element.
    # Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
    icon: BLACK_STAINED_GLASS_PANE
    # Title of the element
    title: "&b&r" # Empty text
    # Description of the element
    description: "I am background"
  # Border item for non-empty border slots
  border:
    # Icon for the element.
    # Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
    icon: BLACK_STAINED_GLASS_PANE
    # Title of the element
    title: "&b&r" # Empty text
    # Description of the element
    description: "I am border"
  # Rows that must be always visible
  force-shown: [2,4]
  # Content of the GUI.
  content:
    # Row number from 1 to 6
    2:
      # Column number
      2: reusable_button_one
      3: reusable_button_one
      4: reusable_button_one
      5: reusable_button_one
      6: reusable_button_one
      7: reusable_button_one
      8: reusable_button_one
    3:
      1:
        # Icon for the element.
        # Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        # Title of the element.
        title: "Button One"
        # Description of the element
        description: "Button description"
        # Data is used for defining some functions that are used for addons.
        # The content of it depends on addon/gui implementation.
        data:
          type: ADDON_THING
        # Actions allow specifying what button should do. Addons can specify extra parameters.
        action:
          # available options can be found here: [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
          left:
            # Addons can define a type of click. 
            type: ADDON_THING
            # Tooltips are a text that will be added to the button description at the end.
            tooltip: "Tooltip for a button"
      9:
        # Icon for the element.
        # Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
        icon: STONE
        # Title of the element.
        title: "Button Twi"
        # Description of the element
        description: "Button description"
        # Data is used for defining some functions that are used for addons.
        # The content of it depends on addon/gui implementation.
        data:
          type: ADDON_THING
        # Actions allow specifying what button should do. Addons can specify extra parameters.
        action:
          # available options can be found here: [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
          left:
            # Addons can define a type of click. 
            type: ADDON_THING
            # Tooltips are a text that will be added to the button description at the end.
            tooltip: "Tooltip for a button"
    5:
      2: reusable_button_two
      3: reusable_button_two
      4: reusable_button_two
      5: reusable_button_two
      6: reusable_button_one
      7: reusable_button_two
      8: reusable_button_two
  # The reusable buttons that are used inside content part multiple times.
  reusable:
    # The id of reusable
    reusable_button_one:
      # Icon for the element.
      # Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
      icon: GLASS
      # Title of the element.
      title: "Reusable Button One"
      # Description of the element
      description: "Button description"
      # Data is used for defining some functions that are used for addons.
      # The content of it depends on addon/gui implementation.
      data:
        type: ADDON_THING
      # Actions allow specifying what button should do. Addons can specify extra parameters.
      action:
        # available options can be found here: [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
        left:
          # Addons can define a type of click. 
          type: ADDON_THING
          # Tooltips are a text that will be added to the button description at the end.
          tooltip: "Tooltip for a button"
    reusable_button_two:
      # Icon for the element.
      # Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
      icon: DIRT
      # Title of the element.
      title: "Reusable Button Two"
      # Description of the element
      description: "Button description"
      # Data is used for defining some functions that are used for addons.
      # The content of it depends on addon/gui implementation.
      data:
        type: ADDON_THING
      # Actions allow specifying what button should do. Addons can specify extra parameters.
      action:
        # available options can be found here: [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
        left:
          # Addons can define a type of click. 
          type: ADDON_THING
          # Tooltips are a text that will be added to the button description at the end.
          tooltip: "Tooltip for a button"
```

### よくある質問

??? question "多言語のタイトルと説明を設定できますか？"
    はい、できます。GUI のすべてのテキストは常に BentoBox のローカライゼーションを使用しようとします。つまり、翻訳にリンクするテキストを指定すると、それが使用されます。
    例:
    ```yaml
    tooltip: panels.tooltips.left
    ```
    は、BentoBox のいずれかのロケールから翻訳文字列を取得しようとします:
    ```yaml
    panels:
      tooltips:
        left: "Left Click Tooltip"
    ```

??? question "タイプとは何ですか？"
    Spigot プラグインではプレイヤーが操作できる 3 種類のインベントリを指定できます:
    - `INVENTORY` - 27 から 54 スロットのチェストのようなシンプルなインベントリ。
    - `HOPPER` - 5 スロットのホッパーインベントリ。
    - `DROPPER` - 9 スロットのドロッパーインベントリ。
    
    エンチャント台やアンビルなどの他のインベントリは Spigot でサポートされておらず、追加のプラグインが必要です。そのため、BentoBox は現在これらをサポートしていません。

??? question "バックグラウンドとは何ですか？"
    バックグラウンドアイテムは GUI 内のすべての空のスペースに統一されたアイテムを設定できます。
    アイコンとタイトルが必要です。設定したくない場合は `background` の行を削除してください。
    `background` の下で唯一必須なのはアイコンです。`title` と `description` は削除できます。
    ```yaml
        icon: BLACK_STAINED_GLASS_PANE
        title: "The title of background item"
        description: "The description of background item"
    ```

??? question "ボーダーとは何ですか？"
    ボーダーアイテムは GUI の周囲すべてに統一されたアイテムを設定できます。空のスペースのみを置き換えます。
    アイコンとタイトルが必要です。設定したくない場合は `border` の行を削除してください。
    `background` の下で唯一必須なのはアイコンです。`title` と `description` は削除できます。
    ```yaml
        icon: BLACK_STAINED_GLASS_PANE
        title: "The title of border item"
        description: "The description of border item"
    ```

??? question "空のテキストを設定してツールチップを非表示にできますか？"
    残念ながら、Minecraft サーバーはクライアントのテキストとツールチップのレンダリングを無効にできません。改造されたクライアント（fabric や forge など）のみ可能です。
    最も近い方法は空のテキストを設定することです: `&b&r`


??? question "`force-shown` とは何ですか？"
    インベントリ GUI では完全に空の行を削除しようとします。これにより、利用可能な要素の数に応じて GUI の動的なサイズが可能になります。ただし、特定の行を常に表示したい場合があります。force-show オプションはそれを可能にし、行（0-6）を整数でリストできます。

??? question "`reusable` とは何ですか？"
    一部の GUI では、チャレンジやバイオームのように多くの繰り返しアイテムを指定する必要があります。Reusable を使用すると、コンテンツ部分でオブジェクトが必要なすべての場所に置き換えられる単一の要素を作成できます。

??? question "`content` を適切に設定するにはどうすればいいですか？"
    コンテンツは最初に行番号（1 から 6）、次に各ボタンの列番号（1 から 9）を指定する必要があります。すべてのスロットを指定する必要はなく、埋めたいものだけでかまいません。その他はすべて空、バックグラウンド、またはボーダーになります。
    
    一部の GUI タイプには複数の行がなかったり、列が少ない場合があることに注意してください。

??? question "ボタンの `data` とは何ですか？"
    Data はアドオンがカスタム機能を使用するために実装した方法です。例えば、Challenges アドオンには CHALLENGE と LEVEL の 2 つのデータタイプがあります。各アドオンには独自のデータがあり、タイプ以外のものも含まれる場合があります。

??? question "ボタンの `actions` とは何ですか？"
    `Actions` はプレイヤーがボタンで異なるクリックオプションを使用した場合に発生するさまざまなことを実装できます。
    すべてのクリックオプションはこちらで確認できます: [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
    すべてのオプションがプレイヤーによって使用できるわけではないことに注意してください。

    `action` はツールチップ生成をサポートしています。ツールチップは常にボタンの説明の末尾にアクションの順序で追加されます。
