# SkyGrid パーミッション { #skygrid-permissions }

SkyGridパーミッションは`skygrid.`で始まります。すべてのパーミッションは[パーミッションリファレンス](../../BentoBox/Permissions.md)に`skygrid`の代わりにリストされています。より大きなチーム、アイランド、より多くのホームなどのVIP特典については、[パーミッション&VIP特典](../../BentoBox/Permissions-Guide.md)を参照してください。

## プレイヤーコマンド：デフォルトで誰が持っているか { #player-commands-who-has-them-by-default }

これらのデフォルトはSkyGridの`addon.yml`から来ています。**全員**とは、除外しない限りすべてのプレイヤーが権限を持つことを意味します。**オペレーター**とは、パーミッションプラグインでプレイヤーに与える必要があることを意味します。コンソールで`/bentobox perms`を実行して、サーバーのデフォルトを確認してください。

| パーミッション | コマンド | デフォルト |
|---|---|---|
| `skygrid.island` | プレイヤーコマンド自体 | 全員 |
| `skygrid.island.create` | `create` | 全員 |
| `skygrid.island.home` | `go` | 全員 |
| `skygrid.island.homes` | `homes` | 全員 |
| `skygrid.island.sethome` | `sethome` | 全員 |
| `skygrid.island.deletehome` | `deletehome` | 全員 |
| `skygrid.island.renamehome` | `renamehome` | 全員 |
| `skygrid.island.spawn` | `spawn` | 全員 |
| `skygrid.island.info` | `info` | 全員 |
| `skygrid.island.near` | `near` | 全員 |
| `skygrid.island.reset` | `reset` | 全員 |
| `skygrid.island.name` | `setname`, `resetname` | 全員 |
| `skygrid.island.language` | `language` | 全員 |
| `skygrid.island.settings` | `settings` | 全員 |
| `skygrid.island.lock` | `lock` | なし |
| `skygrid.island.ban` | `ban`, `unban`, `banlist` | 全員 |
| `skygrid.island.expel` | `expel` | 全員 |
| `skygrid.island.team` | `team` | 全員 |
| `skygrid.island.team.invite` | `team invite` | 全員 |
| `skygrid.island.team.accept` | `team accept` | 全員 |
| `skygrid.island.team.reject` | `team reject` | 全員 |
| `skygrid.island.team.leave` | `team leave` | 全員 |
| `skygrid.island.team.kick` | `team kick` | 全員 |
| `skygrid.island.team.promote` | `team promote`, `team demote` | 全員 |
| `skygrid.island.team.setowner` | `team setowner` | 全員 |
| `skygrid.island.team.trust` | `team trust`, `team untrust` | 全員 |
| `skygrid.island.team.coop` | `team coop`, `team uncoop` | 全員 |

管理者およびモデレーターパーミッション（`skygrid.admin.*`、`skygrid.mod.*`）はデフォルトでオペレーター用です。[スタッフパーミッション](../../BentoBox/Permissions-Guide.md#staff-permissions)を参照してください。
