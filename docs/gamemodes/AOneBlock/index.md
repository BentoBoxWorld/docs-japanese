# AOneBlock

**AOneBlock**は、**IJAminecraft**の人気サバイバルマップ「OneBlock」をBentoBox向けにアレンジしたものです。
プレイヤーは魔法の1ブロックの上でサバイバルを繰り広げます。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("AOneBlock") }}

宇宙に浮かぶ1つのブロック。それだけです。さあ、どうする？

## インストール

0. BentoBoxをインストールし、データフォルダを生成するためサーバーを少なくとも1回起動します。
1. このjarファイルをBentoBoxプラグインのaddonsフォルダに配置します。
2. サーバーを再起動します。
3. アドオンがワールドとデータフォルダを作成し、フォルダ内にconfig.ymlとphasesフォルダ内の設定ファイルが生成されます。
4. サーバーを停止します。
5. config.ymlと.ymlの設定ファイルを希望通りに編集します。
6. ワールドの生成に関わる設定を変更した場合は、初回起動で作成されたワールドフォルダを削除します。
7. サーバーを再起動します。

## 設定

メインの`config.yml`ファイルには、ゲームモードアドオンのセットアップに関する基本情報が含まれています。

`phases`にはAOneBlockワールドに存在するフェーズに関するすべての情報が含まれています。

`panels`ではプレイヤーがアクセスできる一部のパネルをカスタマイズできます。

### config.yml

アドオンが正常にインストールされると、config.ymlファイルが作成されます。このファイルのすべての設定にはコメントが付いています。詳細はファイルをご確認ください。
最新の設定ファイルはこちら: [config.yml](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/resources/config.yml)

!!! new "AOneBlock 1.27.0 以降 — `island.save-every`"
    アイランドの進捗がデータベースに書き込まれる頻度（採掘されたブロック数）。サーバーの直接的なシャットダウンがない場合（クラッシュ、`kill -9`、ホスティングパネルの強制再起動）の喪失が可能なため、進捗は各フェーズ変更時、プレイヤーのログアウト時、シャットダウン時にも保存されます。下が安全ですがより頻繁に書き込みます。最小は `1` です。

    デフォルト: `10`（古いハードコードされた 50 を置き換え）。既存の設定は自動的にデフォルトを取得します。

### フェーズインデックス — `phases_index.yml`

!!! new "AOneBlock 1.26.0 で追加"
    `phases_index.yml`は`phases`フォルダと同じ場所に置かれ、どのフェーズをどの順序で読み込むか、各フェーズの長さ、そして各フェーズが必要とするMinecraftバージョンについての信頼できる情報源となります。このファイルはフェーズファイルが解析される**前**に読み込まれるため、より新しいMinecraftバージョンを必要とするフェーズは、そのYAML — およびその中のアイテム — に一切触れることなくスキップされます。

`phases:`リストの各エントリは次のフィールドを取ります:

| フィールド | 意味 |
|---|---|
| `file` | `phases`フォルダ内のフェーズファイルのベース名（`.yml`は付けません）。チェストファイルは`<file>_chests.yml`です。 |
| `section` | フェーズファイル内のトップレベルキー（歴史的には開始ブロック数）。 |
| `name` | 表示名。ログや`/[admin_command] phases`パネルで使用されます。 |
| `length` | そのフェーズのブロック数。 |
| `enabled` | 任意。デフォルトは`true`。`false`にするとそのフェーズを除外します。 |
| `requiredMinecraftVersion` | 任意。このバージョンより古いサーバーでは、そのフェーズはスキップされ、ブロック数も一切消費しません。 |

開始ブロック数は**計算されます**。有効になっている上位のフェーズの長さを 0 から順に足し合わせた値です。つまりフェーズは自由に並べ替えることができ、スキップされたフェーズは進行から消え去ります。最後のフェーズの後、ブロックカウントは`gotoAtEnd`へジャンプします。

トップレベルの`adminLengths: true`は、`/[admin_command] phases`で長さを初めて編集したときに自動的に書き込まれます。それ以降、整合処理が長さを再計算することはなくなるので、あなたの設定値は後のファイル追加、リネーム、アップグレードを経ても維持されます。

#### 整合処理

!!! note "1.26.1 以降、phasesフォルダが信頼できる情報源です"
    インデックスは読み込みのたび、および管理パネルからの保存のたびに、実際にディスク上にあるファイルと突き合わせて整合が取られます。そのため`/[admin_command] phases`が表示する内容は、サーバーが実際に動かしている内容そのものです。起動ログの`Phase index:`で始まる行に注目してください — 何が変更されたかが正確に記載されています。

- **アドオンのバージョン間でファイル名が変わった**エントリは、フェーズ名を手掛かりにあなたのファイルへ再度紐付けられ、そのフェーズが再び読み込まれるようになります。
- **ファイルが見つからないが jar に同梱されている**エントリは自動的に復元されます。`phases/`内のファイルは決して上書きされないため、これがアップグレードしたサーバーで新しいフェーズが現れる仕組みです。
- フォルダに置かれた**カスタムフェーズファイル**は自動的に追加されます。数値キーであればレガシーな開始ブロック位置に収まり、それ以外は末尾に追加されるので、パネルで並べ替えてください。
- ファイルが完全に失われたエントリは警告付きで削除されるので、パネルに存在しないフェーズが並ぶことはありません。
- 修復が必要だった場合、長さはあなたのファイルのレガシーな開始ブロックキーから再計算され、インデックス導入前にサーバーが実際に動かしていたレイアウトが保たれます — ただし`adminLengths`が設定されている場合を除きます。

!!! warning "フェーズを削除するには"
    フェーズを恒久的に削除するには、そのファイルを削除するか、`/[admin_command] phases`でオフに切り替えてください。インデックスのエントリだけを削除しても機能しません — 整合処理がフォルダ内に見つけたフェーズファイルを再追加してしまいます。

    インデックスが壊れている場合は従来の直接ファイル読み込みにフォールバックするため、編集をミスしてもアドオンが動かなくなることはありません。

### フェーズ設定ファイル

!!! abstract "完全ガイド: [フェーズのカスタマイズ](Phases.md)"
    フェーズファイルの完全なウォークスルー — すべての数値が何を意味するのか、加重ブロック/モブプールがどのように機能するのか（実例付き）、チェスト、カスタムブロック、バージョンゲーティング、ゼロからのフェーズ構築方法。

フェーズを設定するための設定ファイルは`phases`フォルダにあります。

各フェーズには2つのファイルがあります — ブロックとモブを含むファイルと、チェストを含むファイルです。

ファイルの最初の数字は、そのフェーズに到達するために採掘が必要なブロック数です。これがフェーズのキー番号です。

!!! tip "1.26.1 以降、フェーズファイル名の数字は任意です"
    カスタムフェーズファイルは、ファイル名にもYAMLのセクションキーにも数値の開始ブロックを必要としなくなりました — `desert:`セクションを持つ`desert.yml`で動作します。チェストファイルは引き続きファイル名で対応付けられます（`<file>_chests.yml`）。同梱ファイルの数字は歴史的なもので、インデックスが管理する今はパネルの開始位置と長さの値が正となります。数値キーは、整合処理にそのファイルがどこに属し、どれだけの長さだったかを伝えるという点で引き続き有用です。

=== "name"
    !!! summary "説明"
        フェーズの表示名です。プレイヤーがフェーズを確認しようとするすべての場所でこの名前が表示されます。

=== "icon"
    !!! summary "説明"
        フェーズのアイコンは`phases`パネルでのみ使用されます。

        アイコンは[BentoBox ItemParser](https://docs.bentobox.world/en/latest/BentoBox/ItemParser/)を使用して作成されます。

=== "fixedBlocks"
    !!! summary "説明"
        `fixedBlocks`セクションでは、フェーズ内の特定の番号のブロックを採掘したときに出現するブロックを固定できます。書式はインデックス番号（0始まり）の後にBukkit Materialを続けます。フェーズのブロック総数を超えるインデックスは機能しません。
        
        使用可能な値はこちら: [Materials](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)

        サポートブロックが不要なブロック（松明、レール、植物など）の使用をお勧めします。

    !!! example "例"
        ```yaml
            0: GRASS_BLOCK
            1: GRASS_BLOCK
            2: GRASS_BLOCK
            50: SPONGE
        ```

    !!! tip "CHEST_WITH_X 記法"
        fixedBlocks のエントリに `CHEST_WITH_X` 記法を使用して、特定のアイテムがあらかじめ入ったチェストを設置できます。例：`CHEST_WITH_WATER_BUCKET`。アイテムは有効な Bukkit マテリアル名である必要があります。

=== "holograms"
    !!! summary "説明"
        AOneBlockはこれらの行を表示するためにネイティブホログラムを使用します。フェーズが開始される前に表示される最初の行はaoneblockロケールファイルにあります。
        
        `fixedBlocks`と同様に、`holograms`も表示タイミングの数字から始まり、表示テキストが続きます。

    !!! example "例"
        ```yaml
            0: "&aFirst block is grass!"
            1: "&aSecond block is grass!"
            2: "&cWhat if there will be no next block?"
            3: "&aGood Luck!"
        ```

=== "biome"
    !!! summary "説明"
        `biome`は実験的なオプションです。ただし、「魔法」のブロックの位置のバイオームのみを変更します。
        島全体のバイオームを変更するオプションを持つBiomesアドオンの使用をお勧めします。
        バイオーム変更をトリガーするフェーズ開始コマンドで実行できます。

=== "requiredMinecraftVersion"
    !!! summary "説明"
        1.26.0以降、フェーズ、個々のブロック、個々のモブが、必要とする最小のMinecraftバージョンを宣言できます。サーバーのバージョンが古くて対応できないものは、`Tried to load invalid item`や`ConfigurationSerialization`のエラーを出す代わりに、情報ログ1行だけを残してスキップされます。

        フェーズレベルの値は`phases_index.yml`にも記述します。そうすることで、フェーズファイルが解析される前の段階でそのフェーズをスキップできます。フェーズレベルで設定した場合、古いサーバーではそのフェーズはブロック数を一切消費せず、後続のフェーズが繰り上がります。

        個々の`blocks`と`mobs`のエントリは、`weight`と独自の`requiredMinecraftVersion`を持つオブジェクト形式を取れます。チェストファイルはアイテム単位で読み込まれるため、サーバーのバージョンが知らないアイテムはそれ単体だけがスキップされ、残りのチェストは通常どおり読み込まれます。

    !!! example "例"
        ```yaml
            blocks:
              NETHERRACK: 300
              DRIED_GHAST:
                weight: 25
                requiredMinecraftVersion: '1.21.6'
        ```

=== "start-commands"
    !!! summary "説明"
        `start-commands`セクションでは、プレイヤーがこのフェーズを開始したときにトリガーされるコマンドを定義できます。
    
        コマンドはコンソールとして実行されます。ただし、コマンドの先頭に`[SUDO]`が付いている場合は、コマンドをトリガーしたプレイヤーとして実行されます。
    
        コマンド文字列内のこれらのプレースホルダーは適切な値に置き換えられます:
    
        - `[island]` - 島の名前
        - `[owner]` - 島のオーナーの名前
        - `[player]` - コマンドをトリガーするブロックを破壊したプレイヤーの名前
        - `[phase]` - このフェーズの名前
        - `[blocks]` - 破壊されたブロック数
        - `[level]` - 島のレベル（Levelsアドオンが必要）
        - `[bank-balance]` - 島の銀行残高（Bankアドオンが必要）
        - `[eco-balance]` - プレイヤーの経済残高（VaultとEconomyプラグインが必要）

    !!! example "例"
        ```yaml
            start-commands:
            - 'give [player] WOODEN_AXE 1'
            - 'broadcast [player] just started OneBlock!'
            - 'obadmin biomes set [player] aoneblock_fields ISLAND!'
        ```

=== "end-commands"
    !!! summary "説明"
        `end-commands`セクションでは、プレイヤーがこのフェーズを完了したときにトリガーされるコマンドを定義できます。
    
        コマンドはコンソールとして実行されます。ただし、コマンドの先頭に`[SUDO]`が付いている場合は、コマンドをトリガーしたプレイヤーとして実行されます。
    
        コマンド文字列内のこれらのプレースホルダーは適切な値に置き換えられます:
    
        - `[island]` - 島の名前
        - `[owner]` - 島のオーナーの名前
        - `[player]` - コマンドをトリガーするブロックを破壊したプレイヤーの名前
        - `[phase]` - このフェーズの名前
        - `[blocks]` - 破壊されたブロック数
        - `[level]` - 島のレベル（Levelsアドオンが必要）
        - `[bank-balance]` - 島の銀行残高（Bankアドオンが必要）
        - `[eco-balance]` - プレイヤーの経済残高（VaultとEconomyプラグインが必要）

    !!! example "例"
        ```yaml
            end-commands:
            - '[SUDO]say Just finished [phase]'
        ```

=== "end-commands-first-time"
    !!! summary "説明"
        `end-commands-first-time`セクションでは、プレイヤーがこのフェーズを**初めて**完了したときのみトリガーされるコマンドを定義できます。2回目以降の完了では実行されません。
    
        コマンドはコンソールとして実行されます。ただし、コマンドの先頭に`[SUDO]`が付いている場合は、コマンドをトリガーしたプレイヤーとして実行されます。
    
        コマンド文字列内のこれらのプレースホルダーは適切な値に置き換えられます:
    
        - `[island]` - 島の名前
        - `[owner]` - 島のオーナーの名前
        - `[player]` - コマンドをトリガーするブロックを破壊したプレイヤーの名前
        - `[phase]` - このフェーズの名前
        - `[blocks]` - 破壊されたブロック数
        - `[level]` - 島のレベル（Levelsアドオンが必要）
        - `[bank-balance]` - 島の銀行残高（Bankアドオンが必要）
        - `[eco-balance]` - プレイヤーの経済残高（VaultとEconomyプラグインが必要）

    !!! example "例"
        ```yaml
            end-commands-first-time:
            - 'broadcast &c&l[!] &b[player] &fhas completed the &d&n[phase]&f phase for the first time.'
        ```

=== "requirements"
    !!! summary "説明"
        `requirements`セクションでは、指定した要件が満たされるまで次のフェーズへのアクセスを制限できます。
        現在、5つの要件フィールドがあります:
    
        - `economy-balance` - プレイヤーの最低経済残高（VaultとEconomyプラグインが必要）
        - `bank-balance` - 島の最低銀行残高（Bankアドオンが必要）
        - `level` - 島のレベル（Levelsアドオンが必要）
        - `permission` - パーミッション文字列
        - `cooldown` - フェーズが最後に開始されてから必要な最低秒数（フェーズの急速な切り替えを防ぐ）

    !!! example "例"
        ```yaml
            requirements:
              bank-balance: 10000
              level: 10
              permission: ready.for.battle
              cooldown: 60
        ```

=== "blocks"
    !!! summary "説明"
        blocksセクションには、Bukkit Materialと相対確率のリストが含まれています。
    
        使用可能な値はこちら: [Materials](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)
    
        すべての確率値はフェーズ全体で合計され、ブロックが配置される確率は相対確率を全確率の合計で割った値です。

    !!! example "例"
        ```yaml
            blocks:
              GRASS_BLOCK: 2
              STONE: 3
        ```
        
        この例では草ブロックがスポーンする確率は40%、石は60%です。(2 / (2+3))と(3 / (2+3))

=== "mobs"
    !!! summary "説明"
        mobセクションには、スポーン可能なモブとブロックと共にその相対確率のリストが含まれています。
        このリストには生存可能でスポーン可能なエンティティのみを記載できます。[EntityTypes](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/EntityType.html)

    !!! example "例"
        ```yaml
            mobs:
              COW: 150
              SPIDER: 75
        ```

=== "カスタムブロック"
    !!! summary "説明"
        バージョン1.11以降、カスタムブロックを指定できるようになりました（[@HSGamer](https://github.com/HSGamer)のご協力に感謝します）。
        blocksとfixed-blocksの両方の場所で設定できます。
        
        `blocks`セクションでカスタムブロックを定義するには、各要素の前に`-`を追加する必要があります。
        また、ブロックはtype、data、probabilityの値で定義する必要があります。
        サポートされているタイプは次のとおりです:
        
          - `block-data`: `/setblock`コマンドを使用してワールドにブロックを配置します。`data`フィールドが必要です
          - `mob`: Spawn Entity APIを使用して要求されたエンティティを作成します。`mob`フィールドが必要で、オプションで`underlying-block`フィールドも使用できます（デフォルト: STONE）
          - `itemsadder`: [ItemsAdder](https://itemsadder.devs.beer/) APIを使用してブロックを作成します。`id`フィールドが必要です。ItemsAdderプラグインがインストールされている必要があります。
          - `nexo`: [Nexo](https://polymart.org/resource/nexo.6901) APIを使用してブロックを作成します。`id`フィールドが必要です。Nexoプラグインがインストールされている必要があります。
          - `craftengine`: [CraftEngine](https://github.com/Xiao-MoMi/craft-core) APIを使用してブロックを作成します。`id`フィールドが必要です。CraftEngineプラグインがインストールされている必要があります。BentoBox 3.15.0+が必要です。

    !!! example "例"
        ```yaml
            fixedBlocks:
              0:
                type: block-data
                data: minecraft:chest[waterlogged=true]
              1: GRASS_BLOCK
              2: GRASS_BLOCK
            blocks:
              - type: block-data
                data: minecraft:chest[waterlogged=true]
                probability: 10
              - type: block-data
                data: minecraft:chest
                probability: 10
              - type: mob
                mob: ZOMBIE
                underlying-block: STONE
                probability: 5
              - type: itemsadder
                id: mypack:ruby_ore
                probability: 10
              - type: nexo
                id: mypack:custom_block
                probability: 10
              - type: craftengine
                id: mypack:custom_block
                probability: 10
              - DIRT: 10     # 旧構文も引き続き機能します
        ```

    !!! tip "ItemsAdder、NexoおよびCraftEngine"
        ItemsAdder、NexoまたはCraftEngineのカスタムブロックを使用するには、サーバーに各プラグインがインストールされている必要があります。
        AOneBlockは起動時にこれらのプラグインを自動検出し、適切なブロックハンドラーを登録します。
        `itemsadder`、`nexo`または`craftengine`ブロックを設定してもプラグインがインストールされていない場合、ブロックはSTONEにフォールバックします。


チェストファイルには、フェーズ番号とchestsセクションのみが含まれています。

=== "chests"
    !!! summary "説明"
        blocksセクションにCHESTがリストされている場合、このセクションに従ってランダムに中身が入れられます。
        好きなだけチェストを定義できます。最初の数字はチェストの固有番号です。
        次にチェストの内容物が続き、スロット番号とアイテムスタックの内容が含まれます。
        最後に、COMMON、UNCOMMON、RARE、EPICのいずれかのレアリティが設定されます。確率はハードコードされており、それぞれ62%、25%、9%、4%です。
        
        チェストを設定する最善の方法はゲーム内で行うことです。
        必要な内容物でチェストを満たし、チェストを見ながら`/[admin_cmd] setchest <phase> <rarity>`コマンドを入力します。`<phase>`はフェーズ名、rarityはレアリティです。TabキーでオートコンプリートされるオプションをTab補完で確認できます。チェストは自動的にoneblocks.ymlファイルに追加されて使用できるようになります。チェストの削除は現時点ではoneblocks.ymlファイルを編集してアドオンをリロードする必要があります。
    
        チェストのアイテムを編集する際は、Materialが正しいBukkit Materialであり、正しくスペルされていることを確認してください。


### カスタマイズ可能なGUI

BentoBox 1.17 APIではカスタマイズ可能なGUIを実装する機能が導入されました。このアドオンはこの機能を最初に使用したアドオンの1つです。カスタマイズをできるだけシンプルにするよう努めましたが、一部の機能には説明が必要です。
BentoBoxのカスタムGUIの仕組みについての詳細はこちら: [カスタムGUI](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUIをカスタマイズするにはどうすればよいですか？"
    アドオンのGUIをカスタマイズするにはバージョン1.10が必要です。これが最初にGUIを実装したバージョンです。アドオンは`/plugins/BentoBox/addons/AOneBlock`の下に`panels`という名前のディレクトリを作成します。

??? question "`PREVIOUS`|`NEXT`ボタンタイプとは何ですか？"
    PREVIOUSとNEXTボタンタイプは、GUIに収まりきれない島が多い場合の自動ページングを作成できます。
    これらのタイプにはdataの下に追加パラメーターがあります:
 
    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

    例:
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: aoneblock.gui.buttons.previous.name
        description: aoneblock.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        actions:
          previous:
            click-type: LEFT
            tooltip: aoneblock.gui.tips.click-to-previous
    ```

??? question "`PHASE`ボタンタイプとは何ですか？"
    このボタンはプレイヤーがフェーズ名と要件を表示できるようにします。ユーザーがフェーズ変更のアクセス権を持ち、既にそのフェーズに到達している場合は、再度選択してリプレイできます。

    icon、title、descriptionはフェーズのプロパティに基づいて動的に生成されます。ただし、手動で変更することもできます。

    例:
    ```yaml
      # icon: PLAYER_HEAD
      # title: aoneblock.gui.buttons.phase.name
      # description: aoneblock.gui.buttons.phase.description
      data:
        type: PHASE
      actions:
        select:
          click-type: LEFT
          tooltip: aoneblock.gui.tips.click-to-change
    ```


## コマンド

!!! tip
    `[player_command]`と`[admin_command]`は実行中のゲームモードによって異なるコマンドです。
    
    ゲームモードの`config.yml`ファイルにはこれらの値を変更するオプションがあります。
    
    例えば、AOneBlockでは、デフォルトの`[player_command]`は`ob`、デフォルトの`[admin_command]`は`oba`です。
    
    このアドオンではアドオンの`config.yml`ファイルでプレイヤーコマンドのエイリアスを変更できることに注意してください。

=== "AOneBlock固有のプレイヤーコマンド"
    - `/[player_command] count`: 現在のフェーズの進捗をチャットに送信します。
    - `/[player_command] phases`: フェーズの表示と選択ができるGUIを開きます。
    - `/[player_command] setcount <number>`: `<number>`をフェーズ開始番号として現在のフェーズを変更できます。
    - `/[player_command] check`: 魔法のブロックの周りにパーティクルをスポーンさせるか、何らかの理由でブロックがない場合は再スポーンさせます。
    - `/[player_command] bossbar`: フェーズの進捗を表示するボスバーの表示/非表示を切り替えます。（1.21.2以降、configで`bossbar: true`が必要）
    - `/[player_command] actionbar`: フェーズの進捗を表示するアクションバーの表示/非表示を切り替えます。（1.21.2以降、configで`actionbar: true`が必要）

=== "管理者コマンド"
    - `/[admin_command] sanity [<phase>]`: フェーズ（または`<phase>`）のチェストが正しいかどうかのメッセージをコンソールに送信します。
    - `/[admin_command] setcount <player> <number>`: `<player>`の現在のフェーズを`<number>`（フェーズ開始番号）に変更できます。
    - `/[admin_command] setchest <phase> <rarity>`: 見ているチェストを`<phase>`のチェストセクションに`<rarity>`で保存します。
    - `/[admin_command] phases`: フェーズ順序エディタを開きます。（1.26.0以降）

    ??? tip "フェーズ順序エディタの使い方"
        `/[admin_command] phases`は、すべてのフェーズを順番に、計算された開始ブロック数・長さ・状態とともに表示します。`phases_index.yml`を編集し、ドロップと切り替えを行うとインデックスが保存されてフェーズが即座にリロードされます。

        - フェーズを**左クリック**すると持ち上げられ、残りが左へ詰まります。置きたい場所をクリックすると他が右へ押し出されてそこに配置されます。末尾に置くためのスロットも使えます。それ以外の場所をクリックするか、パネルを閉じると、保存せずに元へ戻ります。
        - **右クリック**でフェーズの有効／無効を切り替えます。
        - **Shift+左クリック**でフェーズの長さを設定します（1.26.1以降）。パネルが閉じて現在の長さがチャットで表示されるので、整数を入力すると適用され、`cancel`と入力すると現状のままになります。不正な入力は再度プロンプトが出て、60秒でタイムアウトします。最初に長さを編集した時点でインデックスに`adminLengths: true`が書き込まれ、以降あなたの値が再計算されることはありません。

        無効なフェーズは灰色のガラス、バージョン制限で使えないフェーズはバリアとして表示されます — どちらも並べ替えは可能です。アイコンが設定されていないフェーズは、そのフェーズの最初のブロックを使用します。


デフォルトでは、BentoBox GameModeアドオンにはデフォルトのサブコマンドセットが付属していますが、各アドオンにはさらに多くのサブコマンドがある場合があります。

[AOneBlockコマンドの完全一覧](Commands)


## パーミッション

!!! tip
    AOneBlockアドオンのすべての場所で`[gamemode]`プレフィックスは`aoneblock`に置き換える必要があります。

=== "プレイヤーパーミッション"
    - `aoneblock.count` - プレイヤーが'/[player_command] count'コマンドを使用できるようにします。デフォルトで有効。
    - `aoneblock.phases` - プレイヤーが'/[player_command] phases'コマンドを使用できるようにします。デフォルトで無効。
    - `aoneblock.island.setcount` - プレイヤーが'/[player_command] setcount'コマンドを使用できるようにします。デフォルトで無効。
    - `aoneblock.respawn-block` - プレイヤーが'/[player_command] check'コマンドを使用できるようにします。デフォルトで有効。
    - `aoneblock.island.bossbar` - プレイヤーが'/[player_command] bossbar'コマンドを使用できるようにします。デフォルトで有効。（configで`bossbar: true`が必要）
    - `aoneblock.island.actionbar` - プレイヤーが'/[player_command] actionbar'コマンドを使用できるようにします。デフォルトで有効。（configで`actionbar: true`が必要）

=== "管理者パーミッション"
    - `aoneblock.admin.sanity` - プレイヤーが'/[admin_command] sanity'コマンドを使用できるようにします。デフォルトOP。
    - `aoneblock.admin.setchest` - プレイヤーが'/[admin_command] setchest'コマンドを使用できるようにします。デフォルトOP。
    - `aoneblock.admin.setcount` - プレイヤーが'/[admin_command] setcount'コマンドを使用できるようにします。デフォルトOP。
    - `aoneblock.admin.phases` - プレイヤーが'/[admin_command] phases'コマンドでフェーズ順序エディタを開けるようにします。デフォルトOP。（1.26.0以降）

デフォルトでは、BentoBox GameModeアドオンにはデフォルトのサブパーミッションセットが付属していますが、各アドオンにはさらに多くのサブパーミッションがある場合があります。

[AOneBlockパーミッションの完全一覧](Permissions)


## フラグ

AOneBlockはゲームプレイの動作を制御するいくつかのカスタムフラグを導入しています:

| フラグ | タイプ | 説明 | デフォルト |
|------|------|-------------|---------|
| `START_SAFETY` | ワールド設定 | 有効にすると、プレイヤーが新しい島を作成した際に短時間移動できなくなり、すぐに落下するのを防ぎます。持続時間はconfigの`starting-safety-duration`で設定されます。 | false |
| `ONEBLOCK_BOSSBAR` | 島の設定 | プレイヤーにOneBlockフェーズ進捗ボスバーを表示するかどうかを切り替えます。configで`bossbar: true`が設定されている場合のみ利用可能です。 | true |
| `ONEBLOCK_ACTIONBAR` | 島の設定 | プレイヤーにOneBlockフェーズ進捗アクションバーを表示するかどうかを切り替えます。configで`actionbar: true`が設定されている場合のみ利用可能です。 | true |
| `MAGIC_BLOCK` | 保護 | 魔法のブロックを破壊するために必要な最低島ランクを設定します。デフォルトランクはCoopです。 | COOP |


## プレースホルダー

AOneBlockアドオンには独自のプレースホルダーがあります。これらのプレースホルダーはAOneBlockが保存しているデータに関連しています。

|プレースホルダー|説明|AOneBlockバージョン|
|--- |--- |--- |
|%aoneblock_my_island_phase%|自分の島のフェーズ|1.1.2|
|%aoneblock_my_island_count%|自分の島のブロック数|1.1.2|
|%aoneblock_visited_island_phase%|現在立っている島のフェーズ|1.1.2|
|%aoneblock_visited_island_count%|現在立っている島のブロック数|1.1.2|
|%aoneblock_my_island_next_phase%|自分の島の次のフェーズ|1.1.2|
|%aoneblock_visited_island_next_phase%|現在立っている島の次のフェーズ|1.1.2|
|%aoneblock_my_island_blocks_to_next_phase%|次のフェーズまでのブロック数（次のフェーズがない場合は「infinite」）|1.5.2|
|%aoneblock_visited_island_blocks_to_next_phase%|現在立っている島の次のフェーズまでのブロック数|1.5.2|
|%aoneblock_my_island_percent_done%|フェーズの完了率|1.5.2|
|%aoneblock_visited_island_percent_done%|現在立っている島のフェーズの完了率|1.5.2|
|%aoneblock_my_island_done_scale%|自分の島のフェーズ完了スケール|1.5.2|
|%aoneblock_visited_island_done_scale%|現在立っている島のフェーズ完了スケール|1.5.2|
|%aoneblock_my_island_lifetime_count%|自分の島の累計ブロック数|1.10.0|
|%aoneblock_visited_island_lifetime_count%|現在立っている島の累計ブロック数|1.10.0|

デフォルトでは、BentoBox GameModeアドオンには[デフォルトのプレースホルダーセット](../../BentoBox/Placeholders)が付属していますが、各アドオンにはさらに多くのプレースホルダーがある場合があります。

[AOneBlockプレースホルダーの完全一覧](Placeholders)

## よくある質問

??? question "機能Xを追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/AOneBlock/issues)のリストに追加してください。

??? question "バグを見つけました。どこに報告すればよいですか？"
    [こちら](https://github.com/BentoBoxWorld/AOneBlock/issues)のリストに追加してください。

??? question "どんなフェーズがありますか？"
    同梱されているフェーズは20個で、順番は次のとおりです: 平原、地下、冬、海洋、ジャングル、沼地、ダンジョン、砂漠、ネザー、豊穣、荒廃、深層の闇、エンド、繁茂の洞窟、鍾乳洞、マングローブの沼地、草原、桜の林、尖った山頂、硫黄の洞窟。

    各フェーズにはその舞台に適したブロック、アイテム、モブのセットが含まれています。

    硫黄の洞窟にはMinecraft 26.2以降が必要です。それより古いサーバーではスキップされ、代わりに尖った山頂がループ地点まで続きます。`/[admin_command] phases`でフェーズを自分で並べ替え、無効化し、長さを変更できるほか、`phases`フォルダに独自のフェーズファイルを追加することもできます。

??? question "全フェーズに合計何ブロックありますか？"
    Minecraft 26.2以降のサーバーで同梱フェーズを使用した場合は15,500ブロック、硫黄の洞窟フェーズがない場合は15,000ブロックです。

??? question "最後のフェーズの後はどうなりますか？"
    フェーズが繰り返されます — ブロックカウントは`phases_index.yml`の`gotoAtEnd`の値に戻ります。デフォルトは0です。

??? question "なぜ何度も落下して死んでしまうのですか？"
    生き残るためのコツはありますが、難しいかもしれません！防衛を築く必要があります。

??? question "なぜ特定のブロックが他よりも多く出現するのですか？"
    そういう設定になっています！phasesフォルダの設定ファイルで相対確率を設定できます。

??? question "どれが魔法のブロックかわかるにはどうすればよいですか？"
    叩くと緑のパーティクルが出ます。

??? question "魔法のブロックがなくなりました！どうすれば別のを入手できますか？"
    その場所にブロックを置く必要があります。最悪の場合、自分で死ねばブロックが生成されます。

??? question "魔法のブロックが液体です！どうやって採掘しますか？"
    バケツを使ってください。

??? question "どんなモブがスポーンしますか？"
    各フェーズには異なるモブセットがあります。落下しないよう注意してください！注意深く聞くと、敵対モブが近づく音が聞こえることがあります。

??? question "敵対モブがスポーンしても反応する時間がありません！"
    準備してください。ブロックを採掘するときに注意深く聞くと、スポーン前に敵対モブが近づく音が聞こえます。敵対フェーズにいる場合は、モブを予想して防衛を築いて身を守りましょう。かなり遠くからブロックを採掘できます。

??? question "モブがスポーンすると防衛が壊されます！なぜですか？"
    モブはスポーンするための空間を作ります。邪魔なものがあれば壊れて落ちます。それに合わせて建築する必要があります。

??? question "チェストはスポーンしますか？"
    はい。チェストは現在のフェーズのランダムなアイテムで出現します。コモン、アンコモン、レア、エピックのチェストがあります。キラキラしているチェストは良いものです。

??? question "このマップでネザーやエンドに到達することはできますか？"
    バニラのネザーはデフォルトで存在しますが、エンドワールドはありません。

    ただし、BentoBoxはカスタマイズ可能で、AOneBlockの設定ファイルでネザー島とエンドワールドを有効にできます。

    魔法のブロックはオーバーワールドにのみ存在することに注意してください。

??? question "最終的なゴールは何ですか？"
    あなたが望むものがゴールです！

??? question "ホログラムの使い方は？"
    AOneBlockは1.12.3以前のバージョンでホログラムに[Holographic Displays](https://dev.bukkit.org/projects/holographic-displays)を使用します。
    ホログラムセクションを使用するにはこのプラグインをインストールする必要があります！
    
    ただし、バージョン1.13以降とMinecraft 1.19.4以降では、ホログラムに追加のプラグインは不要です。Minecraft Text Entityを使用して表示されます。

    ホログラムテキストはレガシー `&` 色コード、`&#RRGGBB` 16 進色、MiniMessage タグ（グラデーション含む）を受け入れます — 16 進と MiniMessage の形式は 1.27.0 以降。[フェーズのカスタマイズ](Phases.md#holograms) を参照してください。

??? question "訪問者が他のプレイヤーのマジックブロックを採掘するのを止めるには？"
    このオプションは既に存在します — 新しい設定が必要ありません。訪問者が誰かのブロックを採掘している場合、そのアイランドの所有者は `Break Blocks` と `Magic Block` 保護設定で許可するように設定しています。修正は、これらの設定をすべてのワールドでリセットし、アイコンを非表示にして、所有者が再度有効にできないようにすることです。

    これらのステップを**この順序で**実行してください。ステップ 3 がステップ 1 を元に戻す場合があります。

    **1. 新しいアイランドのデフォルトを設定します**

    `/oba settings` を実行し、**Island Defaults** タブ（ひび割れた石のレンガのアイコン）を開きます。`Break Blocks` と `Magic Block` を左クリックして両方が **Member** になるまでクリックしてください。これにより AOneBlock の `config.yml` に自動的に保存されます。

    **2. リロードします**

    `/bbox reload` を実行するか、サーバーを再起動してください。

    **3. 既存のすべてのアイランドに対してこれらのデフォルトを適用します**

    ```
    /oba resetflags BREAK_BLOCKS
    /oba resetflags MAGIC_BLOCK
    ```

    それぞれを確認してください。これにより、ステップ 1 で設定したデフォルトで、各アイランドが現在持っているものを上書きするため、ステップ 1 の後に来る必要があります。

    **4. 所有者が変更できないように設定を非表示にします**

    Op として島に立ち、`/ob settings` を実行して、`Break Blocks` と `Magic Block` を SHIFT-LEFT-CLICK してください。各行は Curse of Vanishing のグローを取得します。これは非表示になったことを意味します。Op は引き続き表示されます。他のユーザーはパネルのアイコンを全く見えなくなります。

    これで、すべてのアイランドが Member 以下の誰かのブロック破壊を拒否し、プレイヤーは変更できなくなります。

    !!! tip
        SHIFT-LEFT-CLICK はこの方法で*任意*の保護設定を非表示にします。ワールドごとで、非表示のリストがゲームモードの設定に保存されます。非表示の設定を再度 SHIFT-LEFT-CLICK して復帰させてください。

??? question "Levelsアドオンを使用すべきですか？"
    あなた次第ですが、使用する場合はプレイヤーが無限のブロックを持っているためレベルが高くなる可能性があることに注意してください。
    私はLevelsアドオンを使わずLikesアドオンを使用することを好みます。


## 翻訳

{{ translations("AOneBlock") }}

## API

BentoBox 1.17 APIではクラスローダーの問題を解決する機能が実装されました。コードに直接アクセスしたいプラグインは、これ以降直接アクセスできるようになりました。

プロジェクトの依存関係としてAOneBlockを追加するだけです。Mavenを使用できます:

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>aoneblock</artifactId>
    <version>1.10.0</version>
    <scope>provided</scope>
</dependency>
```

AOneBlockアドオンは別のデータベーステーブルにデータを保存します。

=== "OneBlockIslands"
    !!! summary "説明"
        OneBlockIslandsはフェーズを通じた島の進捗に関するすべての情報を保存します。

        ソースコードへのリンク: [OneBlockIslands](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/dataobjects/OneBlockIslands.java)

    !!! question "変数"
        - "uniqueId": 島の固有ID。Island uniqueIdと同じです。
        - "blockNumber": 現在の破壊済みブロック番号。
        - "lifetime": 破壊されたブロックの総数。
        - "phaseName": 現在のフェーズ名。
        - "hologram": 表示されているホログラムテキスト。

    !!! example "コード例"
        このデータにアクセスするには、AOneBlockアドオンにアクセスする必要があります。いくつかの方法がありますが、以下の例はどこからでもアクセス可能な汎用的な方法を示しています。
        
        ```java
        public void accessToAOneBlockData(@NonNull Island island) {
           BentoBox.getInstance().getAddonsManager().<AOneBlock>getAddonByName("AOneBlock").ifPresent(aOneBlock -> {
                OneBlockIslands oneBlockData = aOneBlock.getOneBlocksIsland(island);           
                        
                String islandUniqueId = oneBlockData.getUniqueId();
                int brokenBlocks = oneBlockData.getBlockNumber();
                long lifetimeBlocks = oneBlockData.getLifetime();
                String phase = oneBlockData.getPhaseName();
                String hologram = oneBlockData.getHologram();
           });
        }
        ```

### イベント

AOneBlockにはAOneBlock専用のカスタムイベントがあります。ただし、BentoBox GameModeのイベントはAOneBlockでも引き続きトリガーされます。

=== "BlockClearEvent"
    !!! summary "説明"
        このイベントはエンティティがスポーンされる前にトリガーされます。空気または水に置き換えられるブロックのリストが含まれています。

        キャンセル可能です。

        クラスへのリンク: [BlockClearEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/BlockClearEvent.java)

    !!! question "変数"
        - `Entity entity` - スポーンされるエンティティ。
        - `List<Block> airBlocks` - 空気に置き換えられるブロックのリスト。
        - `List<Block> waterBlocks` - 水に置き換えられるブロックのリスト。
        - `boolean cancelled` - イベントがキャンセルされているかどうかを示すboolean。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBlockClear(BlockClearEvent event) {
            Entity entity = event.getEntity();
            List<Block> airBlocks = event.getAirBlocks();
            List<Block> waterBlocks = event.getWaterBlocks();

            boolean cancelled = event.isCancelled();
        }
        ```

=== "MagicBlockEntityEvent"
    !!! summary "説明"
        このイベントはエンティティがスポーンされた後にトリガーされます。スポーンされたエンティティに関する基本情報のみが含まれています。

        クラスへのリンク: [MagicBlockEntityEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/MagicBlockEntityEvent.java)

    !!! question "変数"
        - `EntityType entityType` - スポーンされるentityType。
        - `@NonNull Island island` - エンティティが召喚される島。
        - `@Nullable UUID playerUUID` - エンティティのスポーンをトリガーしたユーザーID。Nullの可能性あり。
        - `@NonNull Block block` - 魔法のブロックの位置。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onMagicBlockEntity(MagicBlockEntityEvent event) {
            EntityType entityType = event.getEntityType();

            Island island = event.getIsland();
            UUID playerUUID = event.getPlayerUUID();
            Block block = event.getBlock();
        }
        ```

=== "MagicBlockEvent"
    !!! summary "説明"
        このイベントは魔法のブロックが破壊された後にトリガーされます。

        クラスへのリンク: [MagicBlockEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/MagicBlockEvent.java)

    !!! question "変数"
        - `@Nullable ItemStack tool` - 魔法のブロックを破壊したツール。
        - `@NotNull Material nextBlockMaterial` - 次の魔法のブロックのマテリアル。
        - `@NonNull Island island` - ブロックが召喚される島。
        - `@Nullable UUID playerUUID` - 魔法のブロックを破壊したユーザーID。Nullの可能性あり。
        - `@NonNull Block block` - 魔法のブロックの位置。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onMagicBlock(MagicBlockEvent event) {
            ItemStack tool = event.getTool();
            Material nextBlockMaterial = event.getNextBlockMaterial();

            Island island = event.getIsland();
            UUID playerUUID = event.getPlayerUUID();
            Block block = event.getBlock();
        }
        ```

=== "MagicBlockPhaseEvent"
    !!! summary "説明"
        このイベントは新しいフェーズが開始された後にトリガーされます。

        クラスへのリンク: [MagicBlockPhaseEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/MagicBlockPhaseEvent.java)

    !!! question "変数"
        - `String phase` - 新しいフェーズの名前。
        - `String oldPhase` - 前のフェーズの名前。
        - `int blockNumber` - 新しいフェーズが開始するブロック番号。
        - `@NonNull Island island` - ブロックが召喚される島。
        - `@Nullable UUID playerUUID` - 魔法のブロックを破壊したユーザーID。Nullの可能性あり。
        - `@NonNull Block block` - 魔法のブロックの位置。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onMagicBlockPhase(MagicBlockPhaseEvent event) {
            String phase = event.getPhase();
            String oldPhase = event.getOldPhase();
            int blockNumber = event.getBlockNumber();

            Island island = event.getIsland();
            UUID playerUUID = event.getPlayerUUID();
            Block block = event.getBlock();
        }
        ```

## 変更履歴

??? warning "v1.23.0の新機能 — ロケールとconfig更新が必要"
    **リリース日:** 2026-04-11

    - **Nexoカスタムブロックサポート。** AOneBlockはフェーズ定義での[Nexo](https://github.com/Nexo-MC/Nexo)カスタムブロックをサポートするようになりました（既存のItemsAdderサポートに追加）。フェーズのconfigで`type: nexo`と`id`フィールドを使用して定義します。
    - **アクションバーでのHEX / MiniMessageカラーサポート。** `/ob actionbar`テキストがHEXカラーと完全なMiniMessageフォーマットを正しくレンダリングするようになりました。
    - 🔡 ロシア語ロケールがMiniMessageフォーマットに更新され、文法が修正されました。
    - アクションバーのロケールと翻訳に関するいくつかのバグ修正。

    🔺 **Nexoサポートは新しい設定オプションです。** Nexoを使用する場合は、フェーズの`.yml`ファイルにNexoタイプのブロックエントリを追加してください。

    🔡 カスタマイズがある場合は**ロケールファイルを再生成**してください。

    [リリース v1.23.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.23.0)

??? warning "v1.24.0 の新機能 — BentoBox 3.15.0 が必要"
    **リリース日：** 2026-04-26

    - **CraftEngine カスタムブロックサポート。** フェーズ定義で `type: craftengine` を使用して [CraftEngine](https://github.com/Xiao-MoMi/craft-core) ブロックを生成できるようになりました。BentoBox 3.15.0+ が必要です。
    - **レアリティ別に設定可能なチェストパーティクル。** UNCOMMON/RARE/EPIC チェストの上に表示されるパーティクルの種類と色が `config.yml` の `world.chest-particles` で設定可能になりました。`NONE` に設定すると無効化できます。
    - **`CHEST_WITH_X` 固定ブロック記法。** フェーズの `fixedBlocks` で `CHEST_WITH_<ITEM>` 形式を使用して、そのアイテムが入ったチェストを設置できます（例：`CHEST_WITH_WATER_BUCKET`）。
    - **`OBSIDIAN_SCOOPING` がデフォルトでオフに。** 新規インストールではこのフラグが `false` に設定されます。明示的に設定している既存サーバーは影響を受けません。
    - 🔡 アイランドのないプレイヤーのプレースホルダーデフォルト値：`%aoneblock_my_island_phase%`、`%aoneblock_my_island_count%`、`%aoneblock_my_island_percent_done%` が空文字列の代わりに `Unknown`、`0`、`0%` を返すようになりました。

    🔺 **BentoBox 3.15.0 以降が必要です** — このリリースは古い BentoBox バージョンではロードされません。

    ⚙️ **新しい config セクション** `world.chest-particles` — 設定可能なパーティクルエフェクトを使用したい場合は、最新の `config.yml` からコピーしてください。

    🔡 新しいキーを取得するために**ロケールファイルを再生成**してください。

    [リリース v1.24.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.24.0)

??? note "v1.25.0 の新機能"
    **リリース日：** 2026-05-03

    - **Plenty フェーズで蜂が住み着いた蜂の巣がドロップ。** Plenty フェーズが、既存のハチミツアイテムと同じ密度で `bee_nest`（中に 3 匹のミツバチ、`honey_level=0`）をドロップするようになり、長らく欠けていたハチミツ養蜂のギャップを埋めました。
    - **モブを引いた後のマジックブロックのクライアント再同期。** マジックブロックがモブを引いたとき、サーバーは破壊イベントをキャンセルしましたが、クライアントには通知していなかったため、次のチャンク再同期（通常は再ログイン時）までブロックが透明に見えていました。キャンセル直後に採掘していたプレイヤーへブロック状態が再送されるようになりました。
    - 🐛 **CraftEngine 起動順序の修正。** `AOneBlock` の `onEnable` が CraftEngine がブロックレジストリを準備する前に走るため、有効な `type: craftengine` エントリーごとに大量の誤った `Bad custom block` エラーが出ていました。ブロックパーサーは config 読み込み時に明示的な `type: craftengine` 宣言を信頼するようになり、ID は配置時に検証されます。
    - 🐛 **Config 読み込み時の CraftEngine ブロック ID 検証強化。** 空の ID および `namespace:key` 形式に従わない ID は、設定読み込み時点で拒否されるようになりました。以前は無視されて配置時に失敗していました。
    - 🐛 **設定可能なチェストパーティクルが非 `DUST` タイプでクラッシュしなくなりました。** データタイプが非 `Void` のパーティクル（`ITEM`、`BLOCK`、`ENTITY_EFFECT` など）は以前 `IllegalArgumentException` をスローしていました。これらは検出され、警告としてログに記録され、スキップされるようになりました。`DUST` および void データのパーティクル（`FLAME` など）は変わらず動作します。

    🔺 新しい蜂の巣エントリーが必要な場合は、新しいエントリーを `phases/8500_plenty.yml` にコピーするか（あるいは phases フォルダーを削除して再生成させる） — カスタマイズされたフェーズファイルはアップグレード時に上書きされません。

    [Release v1.25.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.25.0)

??? note "v1.25.1 の新機能"
    **リリース日:** 2026-07-03

    バグ修正リリース — ドロップイン交換、設定またはロケールの変更なし。

    - 🐛 **マイナーミニオンが再度マジックブロックを採掘できます。** JetsMinionsのマイナーミニオンでマジックブロックを壊すと`NullPointerException`をスローし、`/ob respawnblock`で手動で復元されるまでブロックが消えたままになりました。ミニオンの破壊パスはプレイヤーのみのマジックブロック保護チェック（クラッシュの原因）を実行しなくなり、ブロックは期待通りにサイクルとリスポーンを行います。このリグレッションは1.22.0から存在していました。
    - 🐛 **チーム訪問メンバー向けに`my_island_*`プレースホルダーを修正。** チームに属するプレイヤーが別のアイランドを訪問すると、`my_island_*`プレースホルダーは訪問されたアイランドのチームデータではなくプレイヤー自身のアイランドに解決されるようになりました。これで常にプレイヤー自身のアイランドに解決されます。

    [Release v1.25.1](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.25.1)

??? note "v1.25.2 の新機能"
    **リリース日:** 2026-07-18

    バグ修正リリースです — そのまま置き換えられ、設定やロケールの変更はありません。

    - 🐛 **Jobs Reborn の無限報酬エクスプロイトを塞ぎました。** `MAGIC_BLOCK`フラグがプレイヤーによるマジックブロックの破壊を拒否した場合でも、ブロック破壊をリッスンするプラグイン — Jobs Rebornなど — には破壊が成功したように見え、報酬が支払われていました。ブロックは即座にリスポーンするため、訪問者は同じ貴重なブロックを無限に採掘して無限のジョブ報酬を得られました。拒否された破壊は、他のプラグインが処理する前にキャンセルされるようになりました。
    - 🐛 **`actionbar: false`が実際にアクションバーを無効化するようになりました。** ボスバーが有効になっていると、`actionbar: false`を設定してもアクションバーの進捗表示が出続けており、その逆も同様にボスバーで起きていました。両方の設定が尊重されるようになり、また両方を有効にしている場合にブロック破壊ごとに進捗表示が二重に更新されることもなくなりました。

    [Release v1.25.2](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.25.2)

!!! warning "v1.26.0 の新機能 — フェーズインデックス（アップグレード後に確認してください）"
    **リリース日:** 2026-07-20

    Minecraft 26.2 サーバー向けに硫黄の洞窟フェーズを追加します。そして、1.21.xでも動作するアドオンに26.2専用のフェーズを同梱するには本格的なバージョン処理が必要だったため、どのフェーズをどの順序で、どのサーバーバージョンで読み込むかを制御するフェーズインデックスを導入します。互換性: BentoBox API 3.15.0+ · Minecraft 1.21.5 以降 · Java 21。

    - **硫黄の洞窟フェーズ。** 15000の位置に新しいフェーズが加わりました。典型的な地下ブロックの層に硫黄と辰砂が織り込まれ、Wikiのスポーン重みに沿った硫黄キューブや洞窟グモなどが登場し、*Bounce*のミュージックディスクがドロップし得るテーマチェストも用意されています。終盤のループ地点は15000から15500へ移動します。このフェーズは`requiredMinecraftVersion: '26.2'`を宣言しているため、26.2以降のサーバーでは自動的に現れ、それより古い環境では情報ログ1行だけを残してスキップされます — 尖った山頂がそのままループ地点まで続きます。
    - 🔺 **新しい`phases_index.yml`。** フェーズの順序、長さ、有効状態、必要なMinecraftバージョンについての信頼できる情報源になりました。開始ブロック数は上位フェーズの長さの累計なので、フェーズは自由に移動でき、スキップされたフェーズは進行から消え去ります。インデックスはフェーズファイルが解析される**前**に読み込まれるため、新しいバージョンのアイテムが古いサーバーで引き起こしていた`Tried to load invalid item`や`ConfigurationSerialization`のスタックトレースが解消されます。上記の「設定」セクションを参照してください。
    - **バージョンで制御されるブロック・モブ・チェストアイテム。** チェストファイルはアイテム単位で読み込まれるようになったため、このサーバーバージョンが知らないアイテムはログ1行を残してスキップされ、残りのチェストは読み込まれます。ブロックとモブのエントリは、エントリごとの`requiredMinecraftVersion`を持つオブジェクト形式を取れます。
    - 🔡 **新しい`/[admin_command] phases`パネル**（権限`aoneblock.admin.phases`、デフォルトOP）により、インベントリパネル上でフェーズをクリックして動かし、並べ替え・挿入・切り替えができます。

    🔺 **初回起動時に`phases_index.yml`が生成されます。** データフォルダ内のフェーズファイルから生成され、以降はこれがフェーズの順序と長さを制御します。初回起動後に一度確認しておくとよいでしょう。特にフェーズを手作業で編集している場合は重要です。インデックスが壊れている場合は従来の直接ファイル読み込みにフォールバックするため、動かなくなることはありません。

    🔺 **既存のインストールでは新しいフェーズファイルは自動的には追加されません。** `addons/AOneBlock/phases/`内のファイルは決して上書きされません。1.26.0では`15000_sulfur_caves.yml`と`15000_sulfur_caves_chests.yml`をjarから自分でコピーする必要がありましたが、1.26.1以降は整合処理が代わりに復元します。

    🔡 **フェーズ順序エディタ用の新しいロケールキー**が追加されました — 翻訳済みロケールファイルを再生成または更新してください。

    [Release v1.26.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.0)

!!! warning "v1.26.1 の新機能 — phasesフォルダが信頼できる情報源に"
    **リリース日:** 2026-07-21

    1.26.0のフェーズインデックスに対するバグ修正リリースです。1.26.0では、アップグレードしたサーバーは*標準の*`phases_index.yml`を受け取っていましたが、これは現在のjarのファイル名を参照するものである一方、既存の`phases/`フォルダには古い、あるいはカスタマイズされた構成が入っています。その結果、フェーズが何も告げずに読み込みに失敗し、アップグレードしたサーバーには硫黄の洞窟が現れず、`/[admin_command] phases`はサーバーの実態ではなくプリセットを表示していました。

    - 🔺 **自己修復するフェーズインデックス。** インデックスは読み込みのたび、およびパネルからの保存のたびに`phases/`フォルダと突き合わせて整合が取られます。アドオンのバージョン間でリネームされたエントリはフェーズ名を手掛かりにあなたのファイルへ再度紐付けられ、見つからないが jar に同梱されているエントリは復元され（そのためアップグレードした26.2サーバーに硫黄の洞窟が現れます）、カスタムフェーズファイルは自動的に追加され、ファイルが完全に失われたエントリは警告付きで削除されます。修復が必要だった場合、長さはあなたのファイルのレガシーな開始ブロックキーから再計算され、サーバーが実際に動かしていたレイアウトが保たれます。
    - 🔡 **パネルでフェーズの長さを設定できます。** フェーズをShift+左クリックすると、チャットのプロンプト経由で長さを設定できます。最初に長さを編集した時点で`phases_index.yml`に`adminLengths: true`が書き込まれ、以降は整合処理が長さを再計算することはなくなります。
    - **フェーズファイル名の数字が任意になりました。** `desert:`セクションを持つカスタムの`desert.yml`で動作します。チェストファイルは引き続きファイル名で対応付けられます。
    - 🔡 **パネルの改善。** フェーズのアイコンは石ではなくそのフェーズの最初のブロックにフォールバックし、「使い方」の本は4行に折り返され、フェーズごとの説明文は小さなモニター向けに短くなりました。

    🔺 **初回起動時に`phases_index.yml`がおそらく書き換えられます。** phasesフォルダ内のファイルに合わせて調整されます。`Phase index:`で始まるログ行に注目してください — 何が再紐付け・復元・追加・削除されたかが正確に記載されています。1.26.0へのアップグレード後に消えてしまったフェーズは、自動的に戻ってきます。

    🔺 **フェーズを恒久的に削除するには、そのファイルを削除するか**、パネルでオフに切り替えてください。インデックスのエントリだけを削除する方法はもう機能しません — 整合処理がフォルダ内に見つけたフェーズファイルを再追加します。

    🔡 **新規・変更されたロケールキー**が、長さ入力のプロンプトと刷新されたパネルのテキスト向けに追加されました。

    [Release v1.26.1](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.1)

??? note "v1.26.2 の新機能"
    **リリース日:** 2026-07-25

    1.26.0で発生したルートのリグレッションに対するバグ修正リリースです。**1.26.0または1.26.1をお使いの場合はアップデートしてください。**

    - 🐛 **チェストアイテムがメタ情報を再び保持するようになりました。** 1.26.0以降、チェストファイルは`YamlConfiguration`ではなく素のSnakeYAMLで読み込まれるようになりました。これは、サーバーバージョンが知らないアイテムがチェストファイル全体を巻き添えにせず単体でスキップされるようにするためです。その副作用として、読み込み時に何もデシリアライズされなくなっていました。アイテムの`meta`セクションは単なるマップとして渡され、Bukkitのアイテムデシリアライザは`ItemMeta`になっていないメタを何も告げずに無視します。エンチャント、ポーション効果、名前がログにも残らないまま失われていました — 最も目に見える形では平原チェストのエンチャントの本でしたが、影響はすべてのフェーズのすべてのチェストアイテムに及び、ポーション、効果付きの矢、カスタム名付きアイテム、旗、プレイヤーの頭、書き込まれた本も含まれます。

        チェストアイテムの定義は適切に走査され、アイテムを組み立てる前にメタがデシリアライズされるようになりました。1.26.0の動作は変わりません — お使いのMinecraftバージョンに存在しないアイテムは引き続きログ行を残してスキップされます — そして読み取れないメタセクションは、アイテムごと失われるのではなくメタの分だけの損失で済み、その旨がログに記録されます。

    フェーズファイルの変更は不要です: 同梱のフェーズYAMLにある旧形式のエンチャント名（`PROTECTION_FALL`など）は引き続きサーバーが変換するため、カスタマイズしたチェストファイルもそのままで動作します。プレイヤーが**すでに**入手したアイテムはそのままです — メタはチェストが生成された時点で失われているので、後から修復できるものはありません。今後生成されるチェストはすべて正しくなります。

    [Release v1.26.2](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.2)

??? note "v1.26.3 の新機能"
    **リリース日：** 2026-07-29

    フェーズGUIのバグ修正リリースです。そのまま置き換えられ、設定・ロケール・フェーズファイルの変更はありません。

    - 🐛 **「クリックで変更」は、そのクリックが成功する場合にのみ表示されるようになりました。** `/[player_command] phases` パネルは、アイランドの状態とフェーズの要件だけでフェーズ変更アクションを提示するかどうかを判断しており、クリック時に実際に使われる `aoneblock.island.setcount` 権限をプレイヤーが持っているかを確認していませんでした。そのため、一部またはすべてのランクでこの権限が剥奪されているサーバーでは、条件を満たすすべてのフェーズにツールチップが表示され、クリックすると *「このコマンドを実行する権限がありません」* と表示されていました。パネルはアクションを提示する前に権限を確認するようになりました。何らかの理由でサブコマンドを解決できない場合は従来どおり寛容な動作のままなので、この変更によってクリックできなくなるフェーズはありません。権限を**持っている**プレイヤーにとっては何も変わりません。

    互換性: BentoBox API 3.15.0+、Minecraft 1.21.5 以降（Sulfur Caves フェーズ自体は Minecraft 26.2 以降で有効になります）、Java 21。

    [Release v1.26.3](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.3)

!!! warning "v1.27.0 の新機能 — BentoBox 3.22.0 と Java 25 が必要"
    **リリース日:** 2026-08-08

    アイランド進捗の無言で繰り返される喪失を修正し、フェーズテキストに MiniMessage と 16 進色を追加します。互換性：BentoBox API 3.22.0+ · Minecraft 26.x または 1.21.5+（Sulfur Caves フェーズは 26.2+ で有効になります）· **Java 25 サーバー**。

    - 🔺 🐛 **アイランド進捗がシャットダウン時に失われなくなりました。** サーバーがシャットダウンしたときにプレイヤーがオンライン中だった場合、ブロックカウントは最後のチェックポイントまでロールバックしました — 採掘されたブロックが最大 49 個分失われます。毎回シャットダウンです。AOneBlock は Pladdon なので、サーバーが BentoBox の*前に*それを無効にし、シャットダウンセーブは BentoBox 3.22.0 以前のすべてが静かに破棄するキューに入りました。シャットダウンセーブは、コアに独立した直接書き込みになりました。
    - ⚙️ **新しい `island.save-every` オプション** — 進捗がデータベースに書き込まれる頻度（採掘されたブロック数）。デフォルト **10**（古いハードコードされた 50 を置き換え）、シャットダウン前に 9 つのブロックが最大喪失されます。進捗は、フェーズ変更、ログアウト、シャットダウンでも保存されます。既存の設定に自動的に追加されます。上記の Configuration セクションを参照してください。
    - 🎨 **フェーズテキストの MiniMessage と 16 進色。** ホログラムはレガシー `&` コードのみを理解し、アクションバーは別のシリアライザーを使用していました。両方とも現在、レガシーコード、`&#RRGGBB` hex、MiniMessage タグとグラデーション、自由混在を受け入れます — 同じことがロケール文字列にも適用されます。また、開始ホログラムとアクションバーにリテラルテキストとして表示される `§` コードも修正されました。既存の `&` コードは動作し続けます。何も変わる必要はありません。
    - 📄 `0_plains.yml` は数値の意味を説明するようになりました — `blocks:`/`mobs:`/`custom-blocks:` の重み、`fixedBlocks:`/`holograms:` の位置 — そして許可される色構文を文書化します。

    🔺 **BentoBox を 3.22.0 以上に最初に更新してください。** `api-version` が上がっているため、古いコアでは *「Cannot load AOneBlock because it requires BentoBox version 3.22.0 or greater」* を拒否します。BentoBox 3.22.0 は **Java 25** サーバーが必要です — どちらかの jar の前に JVM をアップグレードしてください。引き続き Java 21 を使用しています。

    [Release v1.27.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.27.0)

??? note "v1.27.1 の新機能"
    **リリース日:** 2026-08-29

    バグ修正リリース — 設定またはフェーズファイルの変更なし、既存のロケールカスタマイズは動作し続けます。互換性：BentoBox API 3.22.0+ · Minecraft 26.x または 1.21.5+ · Java 25。

    - 🐛 **`my_island_*` プレースホルダーがチームメンバーのために再び機能するようになりました。** 1.26.0 以降、`%aoneblock_my_island_count%`、`%aoneblock_my_island_percent_done%`、`%aoneblock_my_island_phase%` などは、島の**所有者**のみで機能していました。チームメンバーは空のデフォルト（`0`、`0%`、`Unknown`）を得ていました。検索は優先順位です：プレイヤーが所有する島が優先され、誰も所有していないプレイヤーは属するチーム島にフォールバックします。
    - 🐛 **ボスバーが minion/NPC プラグインの下で壊れなくなりました。** JetsMinions（またはアーマースタンドエンティティ経由でブロックを破壊するその他のプラグイン）がマジックブロックを採掘した場合、`MagicBlockEvent` にはプレイヤー UUID が含まれず、ボスバーリスナーが毎回破壊で `IllegalArgumentException` を投げました。バーを表示するユーザーがいない場合は早期に返されるようになりました。
    - 🐛 **光地衣と蔓が配置されたまま生き残るようになりました。** 多面プラント（`GLOW_LICHEN`、`VINE`、`SCULK_VEIN`、`RESIN_CLUMP`）がどの面にも付着していない状態で生成されたため、最初の隣接ブロック更新がそれらを削除し、骨粉が伝播できませんでした。それらは存在する固体隣人に付着するようになり、何もない場合はマジックブロックがサポートブロック（苔、またはスカルク静脈の場合はスカルク）となりプラントが成長します。
    - 🔡 **すべての 18 のバンドルロケールファイルが MiniMessage に変換されました。** レガシー `&` コード もまだ解析されるため、`locales/` のカスタマイズされたファイルは変更なしで機能し続けます。
    - 🔡 **繁体字中国語（`zh-TW`）が完成しました** @qwe664 によって — 1.27.0 以降の 26 個のキーが不足してしており、用語が改訂されました。

    [Release v1.27.1](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.27.1)
