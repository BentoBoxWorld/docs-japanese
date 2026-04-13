# Boxed

プレイヤーは実績を達成することでのみ広げられるボックスの中でサバイバルします！

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("Boxed") }}

## BentoBoxの要件

* 常に最新のBentoBoxバージョンを使用してください（スナップショットはこちらからダウンロードできます: [https://ci.bentobox.world](https://ci.bentobox.world)）
* InvSwitcher — サーバー上のワールド間で実績、インベントリなどを別々に保持する
* Border — ボックスを表示する

## インストール方法

### クイックスタート

1. BoxedアドオンをInvSwitcherとBorderと共にBentoBoxのaddonsフォルダに配置します（最新バージョンを使用してください！）。
2. サーバーを再起動します — 新しいワールドが作成されます。*初回は時間がかかります*
3. ログインします
4. `/boxed`と入力して開始します。
5. （オプション）実績の告知をオフにします `/gamerule announceAdvancements false` — これを設定しないと、プレイヤーが実績を取得するたびにサーバーから大量のスパムが送られます。

* 木の近くからスタートします。便利なアイテムが入ったチェストがあります。（これが島のブループリントです）
* 操作できるエリアはボーダーとして表示されるボックスのみです。
* ボックスを大きくするには実績を達成してください。
* 進捗状況は実績画面（Lキー）で確認できます。
* モンスターはデフォルトではボックスの外にスポーンしませんが、ボックスが大きくなると、モブをスポーンさせるのに1ブロックあれば十分です！
* ボックスのオーナーはボックス内からエンダーパールを投げてボックスを移動させることができます。注意！一方通行です。（config.ymlのオプション設定）
* ボックスの設定には他のランクによるボックス移動を許可するオプションがあります（コンポスターボックスアイコンを探してください）

## カスタム実績

カスタム実績用の[公式BoxedデータパックをダウンロードAする](https://github.com/BentoBoxWorld/BoxedDataPack)。
または自分で作成することもできます。[チュートリアル動画はこちら](https://youtu.be/zNzQvIbweQs)

## Regioneratorの使用

*注意: このプラグインはワールドの未使用リージョンを削除するように設計されています！使用する場合は必ずバックアップを取ってください！自己責任でご使用ください！*

[Regionerator](https://github.com/Jikoo/Regionerator)はワールドサイズを小さく保つために未使用のチャンクを徐々に削除するプラグインです。BentoBoxチームが作成したものではありませんが、BentoBoxをサポートしてボックスの境界を尊重します。ボックスチャンクを削除して再生成するためにも使用できます。Boxedはシードワールドをコピーするためのシードワールドを使用するため、Regioneratorによって未使用と判断され削除される可能性があり、起動が非常に遅くなることがあります。これを防ぐには、Regioneratorの設定ファイルのworldセクションにシードワールドを除外設定として追加してください:

```
# Worlds the plugin is able to delete regions in
worlds:
  # "default" applies to all worlds not specified.
  boxed_world/seed_base:
    days-till-flag-expires: -1
  boxed_world/seed:
    days-till-flag-expires: -1
  default:
    # Flags older than x days can be ignored and the region deleted.
    # Set to -1 to disable Regionerator in a world.
    # To disable flagging, set this to 0.
    # days-till-flag-expires must be greater than 0 to be used with delete-new-unvisited-chunks
    days-till-flag-expires: 0
```

Regioneratorを最大限に活用するには、BentoBoxのconfig.ymlファイルを変更して、島が削除されるときにチャンクを*削除しない*ようにします。これにより削除がRegioneratorに任され、未使用エリアが十分に大きければチャンクがクリーンアップされるはずです。設定は`keep-previous-island-on-reset: true`です:

```
deletion:
    # Toggles whether islands, when players are resetting them, should be kept in the world or deleted.
    # * If set to 'true', whenever a player resets his island, his previous island will become unowned and won't be deleted from the world.
    #   You can, however, still delete those unowned islands through purging.
    #   On bigger servers, this can lead to an increasing world size.
    #   Yet, this allows admins to retrieve a player's old island in case of an improper use of the reset command.
    #   Admins can indeed re-add the player to his old island by registering him to it.
    # * If set to 'false', whenever a player resets his island, his previous island will be deleted from the world.
    #   This is the default behaviour.
    # Added since 1.13.0.
    keep-previous-island-on-reset: true
```


## 高度な設定

### config.yml
設定はBSkyBlock、AcidIslandなどと非常に似ています。

各プレイヤーは島の距離値の制限まで自分だけの土地を探索できます。デフォルトは400なので、土地は800×800ブロックになります。土地は半ランダムですが、各プレイヤーはほぼ同じレイアウトになります（バイオーム設定を参照）。村、壊れたネザーゲート、難破船などの構造物はランダムで、一部のプレイヤーは手に入れ、他のプレイヤーは手に入れないことがあります。将来のバージョンでは、構造物のオフ切り替えがconfigオプションになります。要塞はオフになっており存在しません。各プレイヤーの土地は異なる温度の海に囲まれています。ボーダーが固体でない場合、プレイヤーは理論的に他の土地を探索できます。

*ワールドシード*
ワールドシードは土地を生成するために使用されます。この値を維持することをお勧めします。変更すると土地が大きく異なる可能性があります。

### ブループリント

「island」という1つのブループリントがあり、木、チェスト、y=5まで下のブロックを生成するために使用されます。地表のデフォルトの高さは約y=65なので、ブループリントは約60ブロックの高さが必要です。良いブループリントを作成したら、ぜひ共有してください！

### advancements.yml
このファイルにはすべての実績と、それを取得するとボックスがどれだけ大きくなるかが含まれています。カスタム実績がある場合はそれも含めることができます。

上部に2つの設定があります — 最初の`default-root-increase`はおそらく変更する必要はありません。これは、ルートの実績のスコアを0に設定します。つまり、プレイヤーは新しい実績タブを見ただけではボックスの拡張を得られません。

2番目の設定`unknown-advancement-increase`は、このファイルにリストされていない未知の実績（つまりデータパックを通じてカスタム実績を追加した場合のもの）にデフォルト値を与えます。これにより、このファイルに新しい実績をすべて記載する必要がなくなります。

例:

```
# Lists how many blocks the box will increase when advancement occurs
settings:
  default-root-increase: 0
  unknown-advancement-increase: 1
advancements:
  'minecraft:adventure/adventuring_time': 1
  'minecraft:adventure/arbalistic': 1
  'minecraft:adventure/bullseye': 1
...
```
  
### biomes.yml
プレイヤーの土地にはバイオームがあり、ここで定義されています。今のところバイオームの場所を定義することはできず、地形への影響のみを定義できます。

* height: デフォルトの高さは8です。数値が小さいと土地が低くなり、大きいと高くなります。
* scale: 土地の滑らかさを設定します。数値が小さいとでこぼこになり、大きいと平らになります。

海のバイオームに高い数値を設定すると、海底が海面より上になり、陸地になります。

これらの数値の多くは現在おおよその推測であり、より良い値を見つけた場合はぜひ共有してください！


## パーミッション

パーミッションの一覧は[こちら](Permissions)をご覧ください。

## コマンド

コマンドの一覧は[こちら](Commands)をご覧ください。

## プレースホルダー

プレースホルダーの一覧は[こちら](Placeholders)をご覧ください。

## 翻訳

{{ translations("Boxed") }}
