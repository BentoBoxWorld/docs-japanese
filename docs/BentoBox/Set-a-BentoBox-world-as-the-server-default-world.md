## はじめに

**BentoBoxワールドをサーバーのデフォルトワールドに設定する**ことで、**デフォルトのバニラワールドの生成**を回避できます。

!!! warning 
    このステップバイステップの例/チュートリアルでは、`BSkyBlock`を対象として説明しています。
    他のゲームモードでも同じプロセスですが、**ワールドの名前に注意してください**！

## 準備

1. 手順全体はサーバーが**停止している**間に実行する必要があります。
2. バニラワールド（`world`、`world_nether`、`world_the_end`）をフォルダごと削除してください。

![削除するワールド](https://user-images.githubusercontent.com/20014332/62977233-bebf1180-be1e-11e9-9ec8-ddcfd3352b13.png)

*ハイライトされたフォルダがデフォルトワールドのものです。削除する必要があります。*

## server.properties

`server.properties`ファイルを開きます。

以下の行を見つけます：
```properties
level-name=world
```

`world`をBentoBoxワールドの名前に置き換えます。通常は`[gamemode]_world`で、`[gamemode]`はゲームモード名の小文字です（例：`bskyblock`または`caveblock`）。ただし、ゲームモードの`config.yml`ファイルで変更できるため、正しいものを確認してください。

シンプルにするため、ワールド名が変更されていないジェネリックなままであると仮定し、`bskyblock_world`とします。

行は以下のようになるはずです：
```properties
level-name=bskyblock_world
```

## bukkit.yml

`bukkit.yml`ファイルを開きます：デフォルトワールドがカスタムジェネレーターを使用することをBukkitに伝える必要があります。**そうしないとワールド生成が壊れます**。バニラのネザーまたはエンドを使用したい場合は、このファイルにそれらを記載しないでください。

追加する設定セクションはおそらく既に`bukkit.yml`ファイルに存在しないため、作成する必要があります。セクションの詳細については、公式[Bukkit Wiki](https://bukkit.fandom.com/wiki/Bukkit.yml)を参照してください。

以下のセクションをファイルに追加します。リストされている名前はワールドの名前**でなければなりません**：
```yaml
worlds:
  bskyblock_world:
    generator: BentoBox
  bskyblock_world_nether:
    generator: BentoBox
  bskyblock_world_the_end:
    generator: BentoBox
```

バニラのネザーまたはエンドを使用する場合は、それらを記載しないでください。オーバーワールドだけを記載してください。例えば：
```yaml
worlds:
  bskyblock_world:
    generator: BentoBox
```
