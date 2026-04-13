# IslandFly

**IslandFly** はプレイヤーがアイランドで飛行できるようにします。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("IslandFly") }}

## インストール

0. BentoBox をインストールし、データフォルダを作成するためにサーバーで少なくとも一度起動します。
1. この jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます。
4. サーバーを停止します。
5. config.yml を希望通りに編集します。
7. サーバーを再起動します。

## 設定

アドオンが正常にインストールされると、config.yml ファイルが作成されます。このファイルの全オプションにはコメントが付いています。詳細はファイルを確認してください。
最新の設定ファイルはこちらで確認できます: [config.yml](https://github.com/BentoBoxWorld/IslandFly/blob/develop/src/main/resources/config.yml)

=== "fly-timeout"
    !!! summary "説明"
        プレイヤーがアイランドを離れた後、アドオンが飛行モードを無効にするまで待機する秒数。

=== "logout-disable-fly"
    !!! summary "説明"
        プレイヤーが切断したときに飛行モードを無効にするかどうか。

=== "disabled-gamemode"
    !!! summary "説明"
        このリストには islandFly アドオンが動作しない GameMode が含まれます。アドオンを無効にするには、- で始まる新しい行にそのゲームモード名を書く必要があります。
        
    !!! example "例"
        ```yaml
            disabled-gamemodes:
            - BSkyBlock
        ```   

=== "allow-command-outside-protection-range"
    !!! summary "説明"
        アイランド保護範囲外でのコマンド使用を許可します。

## コマンド

!!! tip "ヒント"
    `[player_command]` と `[admin_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island`、デフォルトの `[admin_command]` は `bsbadmin` です。

=== "プレイヤーコマンド"
    - `/[player_command] fly`: 飛行のオン/オフを切り替えます。

## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "権限"
    - `[gamemode].island.fly` - (デフォルト: `true`) - プレイヤーが '/[player_command] fly' コマンドを使用できます。
    - `[gamemode].island.flyspawn` - (デフォルト: `op`) - プレイヤーがスポーンアイランドで飛行できます。
    - `[gamemode].island.flybypass` - (デフォルト: `op`) - プレイヤーが他のプレイヤーのアイランドで飛行できます。

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/IslandFly/issues)のリストに追加してください。

??? question "バグを発見しました。どこに報告すればいいですか？"
    [こちら](https://github.com/BentoBoxWorld/IslandFly/issues)のリストに追加してください。

## 翻訳

{{ translations("IslandFly") }}
