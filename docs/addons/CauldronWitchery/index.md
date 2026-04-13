# CauldronWitchery

**CauldronWitchery** はプレイヤーが水、溶岩、雪で満たされた大釜と魔法の杖を使って**あらゆる種類のモブやアイテムを召喚**できるようにします。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("CauldronWitchery", beta=True) }}

## インストール

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを起動します。
3. 管理者コマンド（例: `/[admin_cmd] witchery`）を実行してアドオンを設定します。

## 設定

チャレンジ、バイオーム、ジェネレーターと同様に、CauldronWitchery は全データをデータベース内に保存します。設定ファイルにはアドオンの動作に関する汎用オプションが含まれ、魔法の杖やプレイヤーデータなどの他のデータはデータベースに保存されます。

### config.yml

最新の config.yml は[こちら](https://github.com/BentoBoxWorld/CauldronWitchery/blob/develop/src/main/resources/config.yml)で確認できます。

### テンプレート

CauldronWitchery アドオンには、魔法の杖をデータベースにインポートするために使用できるテンプレートファイルが含まれています。このファイルはゲーム内 GUI を使用したくない方のための一括データ追加に便利です。ただし、テンプレートファイルでは全機能が利用できるわけではなく、一部のアイテム/オプションは GUI からのみ追加できます。
テンプレートファイルはいくつでも用意できます。管理者 GUI でどれをインポートするか選択できます。
テンプレートファイルの例: [template.yml](https://github.com/BentoBoxWorld/CauldronWitchery/blob/develop/src/main/resources/template.yml)

!!! tip "ヒント"
    テンプレートファイルには `magic-sticks` が含まれている必要があります。

??? question "魔法の杖にエンチャントを指定できますか？"
    残念ながら Spigot には汎用的なアイテム解析の仕組みがありません。そのためプラグイン作者は独自のものを作成する必要があります。CauldronWitchery アドオンは BentoBox の [アイテムパーサー](/en/latest/BentoBox/ItemParser/)を使用します。それでサポートされていない機能は使用できません。 

    ただし、ゲーム内の管理者 GUI を使用すれば、制限なくあらゆるアイテムを設定できます。

??? question "追加したレシピが認識されません。理由は何でしょうか？"
    いくつかの理由が考えられます。明らかなエラーがある場合は、ログファイルにエラーメッセージが含まれているはずです。
    
    まず、全てのレシピが `- ` で始まり、全てのアイテム（材料、大釜、レベルなど）が左側に整列しているか確認してください。
    
    もう一つの理由は、エンティティ、アイテム、またはブックが存在しないことです。入力内容が正しいか確認してください。

### ブック

ブックはプレイヤーがレシピを見つける手段です。ブックは非常にカスタマイズ可能ですが、タイトル、著者、ページには文字数制限があることに注意してください。ゲーム内で書き込まれた本を使って試してみてから、翻訳ファイルに入れることをお勧めします。

??? question "ブックに独自の翻訳を追加できますか？"
    はい、できます。[book_id]-[locale_code].yml を作成するか、既存のファイルを変更することで追加できます。 

??? question "自動レシピ生成を無効にできますか？"
    はい、ブックから `recipe` セクションを削除するだけです。

??? question "ブックを追加できますか？"
    はい、`books` ディレクトリに新しいファイルを作成するだけです。ファイル名は `[book_id]-[locale_code].yml` とし、`[book_id]:` で始まる必要があります。

## カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装する機能が導入されました。このアドオンはその機能を使用する最初のアドオンの一つです。カスタマイズをできる限りシンプルにしようとしましたが、一部の機能については説明が必要です。
BentoBox カスタム GUI の詳細はこちらを参照してください: [カスタム GUI](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    アドオンの GUI をカスタマイズするにはバージョン 2.0 が必要です。これが実装された最初のバージョンです。アドオンは `/plugins/BentoBox/addons/CauldronWitchery` の下に `panels` というディレクトリを作成します。

    現在カスタマイズできる GUI は 2 つです:

    - 杖パネル: `stick_panel` - 全ての魔法の杖が含まれ、ユーザーが購入または入手できるパネル。
    - レシピパネル: `recipe_panel` - 魔法の杖で利用可能な全レシピが含まれるパネル。

    各 GUI にはそれぞれに固有の機能があります。

??? question "`PREVIOUS`|`NEXT` ボタンタイプとは何ですか？"
    PREVIOUS と NEXT ボタンタイプは、GUI のスペースより多くの杖やレシピがある場合に自動ページングを作成できます。
    これらのタイプには data の下に追加パラメーターがあります:
 
    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

    例: 
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: cauldron-witchery.gui.buttons.previous.name
        description: cauldron-witchery.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            tooltip: cauldron-witchery.gui.tips.click-to-previous
    ```

??? question "`RETURN` ボタンタイプとは何ですか？"
    RETURN ボタンタイプは recipe_panel で利用できます。杖パネルに戻ることができます。

    例: 
    ```yaml
        icon: OAK_DOOR
        title: cauldron-witchery.gui.buttons.return.name
        description: cauldron-witchery.gui.buttons.return.description
        data:
          type: RETURN
        action:
          left:
            tooltip: cauldron-witchery.gui.tips.click-to-return
    ```

??? question "`STICK` ボタンタイプとは何ですか？"
    このボタンは stick_panel で利用できます。
    STICK ボタンは魔法の杖の動的エントリを作成します。魔法の杖が存在する場合のみボタンが表示されます。例えば 3 本の魔法の杖しかないのに GUI に 7 つのスペースを定義した場合、3 つのスペースのみ埋まります。残りのスペースは空になります。

    デフォルトでは杖は順序番号でソートされますが、data の下の `id` パラメーターで特定の杖を特定のスロットに指定することもできます。
    
    ```yaml
      data:
        type: STICK
        id: example_stick
    ```

    タイトル、説明、アイコンを指定するとデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    このボタンは 2 つの異なるアクションタイプをサポートします:

    - RECIPES - レシピ表示パネルを開きます。
    - PURCHASE - プレイヤーに魔法の杖を購入または配布します。

    例: 
    ```yaml
      data:
        type: STICK
      actions:
        left:
          type: RECIPES
          tooltip: cauldron-witchery.gui.tips.left-click-to-view
        right:
          type: PURCHASE
          tooltip: cauldron-witchery.gui.tips.right-click-to-buy
    ```


??? question "`RECIPE` ボタンタイプとは何ですか？"
    このボタンは recipe_panel で利用できます。
    RECIPE ボタンはレシピの動的エントリを作成します。レシピが存在する場合のみボタンが表示されます。例えば 3 つのレシピしかないのに GUI にレベル用の 7 つのスペースを定義した場合、3 つのスペースのみ埋まります。残りのスペースは空になります。

    デフォルトではレシピは順序番号でソートされ、その後報酬アイテム名でソートされます。
    タイトル、説明、アイコンを指定するとデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    
    例: 
    ```yaml
      data:
        type: RECIPE
    ```

## よくある質問

??? question "レシピはどのように機能しますか？"
    全てのレシピには 3 つのものが必要です:
    
    - プレイヤーのメインハンドにある魔法の杖
    - プレイヤーのオフハンドにあるメイン材料
    - 追加材料

    追加材料は大釜に投入するか、インベントリに保持する必要があります。これはアドオンの設定オプション `mix-in-cauldron` に依存します。このオプションが無効の場合、アイテムはプレイヤーのインベントリにある必要があります。
    
    何も不足していなければレシピが機能します。

??? question "カスタムの魔法の杖アイテムを追加できますか？"
    はい、Spigot がサポートする限り可能です。ただし、テンプレートファイルでは追加できません。管理者 GUI のみがカスタムアイテムの追加をサポートしています。

??? question "プレイヤーはどのようにして魔法の杖を入手できますか？"
    プレイヤーは `/[player_cmd] witchery` コマンドで魔法の杖を購入できます。 

    管理者は杖を配布する独自の方法を作成することもできます。杖を生成する管理者コマンドがあります:
   
    `/[admin_cmd] witchery get stick <stick_id>`

??? question "メイン材料と追加材料の違いは何ですか？"
    メイン材料は常にプレイヤーがレシピのために最後に用意する必要があるアイテムです。常にプレイヤーのオフハンドのアイテムです。

    追加材料はプレイヤーのインベントリにあるか、大釜に投入する必要があるアイテムです（設定によります）。

??? question "溶岩大釜でアイテムが燃えず、消滅もしません。"
    アドオン設定で `mix-in-cauldron` オプションが有効の場合、溶岩大釜でアイテムは燃えず、消滅もしません。
    これはアドオンの動作に必要です。溶岩大釜を必要とするレシピがある可能性があり、アイテムが燃えてしまうとそのようなレシピを実行することができません。大釜内でのアイテム消滅は保護措置として無効化されています。 

??? question "アイランドの誰でも魔法の杖を使えます。制限できますか？"
    はい、アイランド保護フラグを使用してどのユーザーグループが杖を使用できるかを制限できます。
    CauldronWitchery は `CAULDRON_WITCHERY_ISLAND_PROTECTION` を追加し、アイランドビジターからオーナーまでトグルできます。

    メンバーグループ外のユーザーはアイランドで魔法の杖を使用できません。

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/CauldronWitchery/issues)のリストに追加してください。


## 翻訳

{{ translations("CauldronWitchery") }}
