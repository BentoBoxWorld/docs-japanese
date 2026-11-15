# BSkyBlock コマンド

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/island`（/is, /skyblock, /sbも可能） | `bskyblock.` |
| 管理者 | `/bsbadmin`（/bsb, /skyblockadmin, /sbadmin, /sbaも可能） | `bskyblock.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド

BSkyBlockはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/island`に、`/[admin_command]`を`/bsbadmin`に、`[gamemode]`を`bskyblock`に置き換えてください。例えば：

```
/island              アイランドに移動するか、新しく作成する
/island team invite <player>
/island settings
/bsbadmin info <player>
/bsbadmin why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。

## BSkyBlockのみのコマンド

| コマンド | 説明 | パーミッション | デフォルト |
|---|---|---|---|
| `/island about` | 著作権およびライセンス情報を表示 | `bskyblock.island` | 全員 |

## アドオンコマンド

アドオンは`/island`および`/bsbadmin`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/island level`または[Challenges](../../addons/Challenges/index.md)の`/island challenges`があります。各アドオンのページを参照してください。
