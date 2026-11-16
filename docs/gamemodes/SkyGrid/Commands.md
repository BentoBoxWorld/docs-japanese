# SkyGrid コマンド { #skygrid-commands }

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/skygrid`（/sgも可能） | `skygrid.` |
| 管理者 | `/sgadmin`（/sgaも可能） | `skygrid.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド { #standard-commands }

SkyGridはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/skygrid`に、`/[admin_command]`を`/sgadmin`に、`[gamemode]`を`skygrid`に置き換えてください。例えば：

```
/skygrid              アイランドに移動するか、新しく作成する
/skygrid team invite <player>
/skygrid settings
/sgadmin info <player>
/sgadmin why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。


## アドオンコマンド { #addon-commands }

アドオンは`/skygrid`および`/sgadmin`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/skygrid level`または[Challenges](../../addons/Challenges/index.md)の`/skygrid challenges`があります。各アドオンのページを参照してください。
