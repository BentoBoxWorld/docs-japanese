# StrangerRealms コマンド { #strangerrealms-commands }

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/st`（/strangeも可能） | `strangerrealms.` |
| 管理者 | `/stranger` | `strangerrealms.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド { #standard-commands }

StrangerRealmsはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/st`に、`/[admin_command]`を`/stranger`に、`[gamemode]`を`strangerrealms`に置き換えてください。例えば：

```
/st              アイランドに移動するか、新しく作成する
/st team invite <player>
/st settings
/stranger info <player>
/stranger why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。

## StrangerRealmsのみのコマンド { #commands-only-in-strangerrealms }

| コマンド | 説明 | パーミッション | デフォルト |
|---|---|---|---|
| `/st claim` | Claim the land you are standing on | `strangerrealms.claim` | 全員 |
| `/st unclaim` | Remove your claim | `strangerrealms.unclaim` | 全員 |
| `/st spawn` | Teleport to the spawn (replaces the standard spawn command) | `strangerrealms.spawn` | 全員 |
| `/stranger worldborder [on\|off\|set\|auto\|info]` | Change the world border settings | `strangerrealms.admin.worldborder` | オペレーター (not declared) |

## アドオンコマンド { #addon-commands }

アドオンは`/st`および`/stranger`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/st level`または[Challenges](../../addons/Challenges/index.md)の`/st challenges`があります。各アドオンのページを参照してください。
