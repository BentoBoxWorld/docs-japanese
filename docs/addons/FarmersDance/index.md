# Farmers Dance

**Farmers Dance** はプレイヤーがどんな植物の近くでもダンスすることでその植物を成長させられるシンプルなアドオンです。

作成・メンテナンス: [BONNe](https://github.com/BONNe)

{{ addon_description("FarmersDance", beta=True) }}

## インストール

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. アドオンが変更可能な設定ファイルを生成します。

## 情報

このアドオンの主なアイデアはアイランド上の植物を速く成長させることです。
TwerkingForTrees との主な違いは、このアドオンがサボテン、カボチャ、キノコを含む全ての成長可能な植物で機能することです。

### config.yml

アドオンが正常にインストールされると、config.yml ファイルが作成されます。このファイルの全オプションにはコメントが付いています。詳細はファイルを確認してください。
最新の設定ファイルはこちらで確認できます: [config.yml](https://github.com/BentoBoxWorld/FarmersDance/blob/develop/src/main/resources/config.yml)

## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "プレイヤー権限"
    - `[gamemode].farmersdance` - プレイヤーが植物を成長させるためにダンスを使用できます。

    
??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/FarmersDance/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    以下のリストに不足しているものがあれば、お知らせください！

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/FarmersDance/issues)のリストに追加してください。

## 互換性

- [x] BentoBox - バージョン 1.20.0

このアドオンは Minecraft 1.19.2 と BentoBox 1.20.0 で構築されています。

このアドオンは全ての Game mode アドオンをサポートしています。

## 翻訳

{{ translations("FarmersDance") }}
