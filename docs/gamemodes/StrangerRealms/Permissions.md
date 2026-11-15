# StrangerRealms パーミッション

StrangerRealmsパーミッションは`strangerrealms.`で始まります。すべてのパーミッションは[パーミッションリファレンス](../../BentoBox/Permissions.md)に`strangerrealms`の代わりにリストされています。より大きなチーム、アイランド、より多くのホームなどのVIP特典については、[パーミッション&VIP特典](../../BentoBox/Permissions-Guide.md)を参照してください。

## プレイヤーコマンド：デフォルトで誰が持っているか

これらのデフォルトはStrangerRealmsの`addon.yml`から来ています。**全員**とは、除外しない限りすべてのプレイヤーが権限を持つことを意味します。**オペレーター**とは、パーミッションプラグインでプレイヤーに与える必要があることを意味します。コンソールで`/bentobox perms`を実行して、サーバーのデフォルトを確認してください。

| パーミッション | コマンド | デフォルト |
|---|---|---|
| `strangerrealms.island` | プレイヤーコマンド自体 | 全員 |
| `strangerrealms.island.create` | `create` | オペレーター (not declared) |
| `strangerrealms.island.home` | `go` | 全員 |
| `strangerrealms.island.homes` | `homes` | 全員 |
| `strangerrealms.island.sethome` | `sethome` | 全員 |
| `strangerrealms.island.deletehome` | `deletehome` | 全員 |
| `strangerrealms.island.renamehome` | `renamehome` | 全員 |
| `strangerrealms.island.info` | `info` | 全員 |
| `strangerrealms.island.near` | `near` | 全員 |
| `strangerrealms.island.reset` | `reset` | Nobody |
| `strangerrealms.island.name` | `setname`, `resetname` | 全員 |
| `strangerrealms.island.language` | `language` | 全員 |
| `strangerrealms.island.settings` | `settings` | 全員 |
| `strangerrealms.island.lock` | `lock` | 全員 |
| `strangerrealms.island.ban` | `ban`, `unban`, `banlist` | 全員 |
| `strangerrealms.island.expel` | `expel` | 全員 |
| `strangerrealms.island.team` | `team` | 全員 |
| `strangerrealms.island.team.invite` | `team invite` | 全員 |
| `strangerrealms.island.team.accept` | `team accept` | 全員 |
| `strangerrealms.island.team.reject` | `team reject` | 全員 |
| `strangerrealms.island.team.leave` | `team leave` | 全員 |
| `strangerrealms.island.team.kick` | `team kick` | 全員 |
| `strangerrealms.island.team.promote` | `team promote`, `team demote` | 全員 |
| `strangerrealms.island.team.setowner` | `team setowner` | 全員 |
| `strangerrealms.island.team.trust` | `team trust`, `team untrust` | 全員 |
| `strangerrealms.island.team.coop` | `team coop`, `team uncoop` | 全員 |

## StrangerRealmsのみのパーミッション

| パーミッション | 許可 | デフォルト |
|---|---|---|
| `strangerrealms.claim` | `/st claim` | 全員 |
| `strangerrealms.unclaim` | `/st unclaim` | 全員 |
| `strangerrealms.spawn` | `/st spawn` | 全員 |
| `strangerrealms.admin.worldborder` | `/stranger worldborder` | オペレーター (not declared) |

管理者およびモデレーターパーミッション（`strangerrealms.admin.*`、`strangerrealms.mod.*`）はデフォルトでオペレーター用です。[スタッフパーミッション](../../BentoBox/Permissions-Guide.md#staff-permissions)を参照してください。
