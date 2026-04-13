# BentoBox ItemParser

configファイルからアイテムスタックを定義するための良い方法はありません。
各アイテムには異なるメタデータが割り当てられる可能性があります。
そのためBentoBoxはASkyBlock時代から受け継いだ非常に変わったフォーマットを使用します。

## クイック例

### 汎用Minecraftアイテム変換

BentoBox 2.0.0以降、giveコマンドのようなMinecraftアイテム変換を使用できます：

    - minecraft:diamond_sword{display:{Lore:["\"A legendary weapon\""]}}
    - minecraft:stone
    - diamond_chestplate{Enchantments:[{id:mending,lvl:1},{id:protection,lvl:4},{id:unbreaking,lvl:3}]}

### 一般的な変換

デフォルトでは、すべてのアイテムは次のフォーマットで変換されます：
    
    - [TYPE]<:QUANTITY>

数量は必須ではありませんが、提供する場合は前に`:`を追加する必要があります。

すべてのタイプはこちらで確認できます：[Material](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)

ただし、さらなるカスタマイズが利用可能ないくつかの例外があります。以下で確認できます。

### ダメージ可能なアイテム

ダメージ可能なアイテムは次のフォーマットで定義できます：

    - [TYPE]:<DAMAGE_AMOUNT>:<QUANTITY>

ダメージ量と数量はオプションです。

### ポーションと先端付き矢

ポーション、スプラッシュポーション、残留ポーション、先端付き矢は同じパターンに従います：

    - [TYPE]:<POTION_TYPE>:QUANTITY

[TYPE]はPOTION、SPLASH_POTION、LINGERING_POTION、またはTIPPED_ARROWに置き換えられます。
すべてのポーションタイプはこちらで確認できます：[PotionTypes](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/potion/PotionType.html)

例：

    - POTION:STRENGTH:1 - 強化I効果の拡張ポーションを作成します。
    - SPLASH_POTION:INSTANT_DAMAGE:2 - ダメージII効果のスプラッシュポーション2個を作成します
    - LINGERING_POTION:STRONG_LEAPING:1 - ジャンプブーストII残留ポーションを作成します。
    - TIPPED_ARROW:WEAKNESS:1 - 弱体化I先端付き矢を作成します。

### バナー

バナーには次のスキームに従うカスタム解析オプションがあります：

    - [color]_BANNER:QUANTITY<:PatternType:DyeColor>

パターンはいくつでも指定できますが、パターンと染料の色の順序に従う必要があります。

すべてのパターンタイプはこちらで確認できます：[PatternType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/block/banner/PatternType.html)

すべての染料の色はこちらで確認できます：[DyeColor](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/DyeColor.html)


### プレイヤーヘッド

プレイヤーヘッドにはカスタム解析オプションがあります。次のスキームに従います：

 - PLAYER_HEAD:<Name|Trimmed UUID|UUID|Texture>:<QUANTITY>

PLAYER_HEAD - アイテムがプレイヤーヘッドであることを示します。
次の部分で以下を指定できます：

    - プレイヤー名
    - プレイヤートリムUUID（-なし）
    - プレイヤーUUID（-あり）
    - テクスチャリンク

最後にスタック内のプレイヤーヘッドの数を指定できます。
例：`PLAYER_HEAD:BONNe1704` - BONNe1704スキンのプレイヤーヘッドを1つ提供します。

### カスタムモデルデータ

カスタムモデルデータは解析可能な任意のアイテムスタックに追加できます。カスタムモデルデータテキストは解析可能な文字列の任意の部分に追加できます。カスタムモデルデータのスキームは：

- `CMD-[number]`

例：

- IRON_INGOT:2:CMD-12345678 => カスタムモデルデータ`12345678`を持つ鉄のインゴット2個のアイテムスタックを作成します
- GOLD_INGOT:CMD-12345678 => カスタムモデルデータ`12345678`を持つ金のインゴットのアイテムスタックを作成します
- PLAYER_HEAD:BONNe1704:CMD-12345678 => カスタムモデルデータ`12345678`を持つBONNe1704プレイヤーヘッドのアイテムスタックを作成します
