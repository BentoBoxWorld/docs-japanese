# AOneBlock パーミッション { #aoneblock-permissions }

AOneBlockパーミッションは`aoneblock.`で始まります。すべてのパーミッションは[パーミッションリファレンス](../../BentoBox/Permissions.md)に`aoneblock`の代わりにリストされています。より大きなチーム、アイランド、より多くのホームなどのVIP特典については、[パーミッション&VIP特典](../../BentoBox/Permissions-Guide.md)を参照してください。

## プレイヤーコマンド：デフォルトで誰が持っているか { #player-commands-who-has-them-by-default }

これらのデフォルトはAOneBlockの`addon.yml`から来ています。**全員**とは、除外しない限りすべてのプレイヤーが権限を持つことを意味します。**オペレーター**とは、パーミッションプラグインでプレイヤーに与える必要があることを意味します。コンソールで`/bentobox perms`を実行して、サーバーのデフォルトを確認してください。

| パーミッション | コマンド | デフォルト |
|---|---|---|
| `aoneblock.island` | プレイヤーコマンド自体 | 全員 |
| `aoneblock.island.create` | `create` | 全員 |
| `aoneblock.island.home` | `go` | 全員 |
| `aoneblock.island.homes` | `homes` | 全員 |
| `aoneblock.island.sethome` | `sethome` | 全員 |
| `aoneblock.island.deletehome` | `deletehome` | 全員 |
| `aoneblock.island.renamehome` | `renamehome` | 全員 |
| `aoneblock.island.spawn` | `spawn` | 全員 |
| `aoneblock.island.info` | `info` | 全員 |
| `aoneblock.island.near` | `near` | 全員 |
| `aoneblock.island.reset` | `reset` | 全員 |
| `aoneblock.island.name` | `setname`, `resetname` | 全員 |
| `aoneblock.island.language` | `language` | 全員 |
| `aoneblock.island.settings` | `settings` | 全員 |
| `aoneblock.island.lock` | `lock` | 全員 |
| `aoneblock.island.ban` | `ban`, `unban`, `banlist` | 全員 |
| `aoneblock.island.expel` | `expel` | 全員 |
| `aoneblock.island.team` | `team` | 全員 |
| `aoneblock.island.team.invite` | `team invite` | 全員 |
| `aoneblock.island.team.accept` | `team accept` | 全員 |
| `aoneblock.island.team.reject` | `team reject` | 全員 |
| `aoneblock.island.team.leave` | `team leave` | 全員 |
| `aoneblock.island.team.kick` | `team kick` | 全員 |
| `aoneblock.island.team.promote` | `team promote`, `team demote` | 全員 |
| `aoneblock.island.team.setowner` | `team setowner` | 全員 |
| `aoneblock.island.team.trust` | `team trust`, `team untrust` | 全員 |
| `aoneblock.island.team.coop` | `team coop`, `team uncoop` | 全員 |
| `aoneblock.island.setcount` | `/ob setCount` | オペレーター |
| `aoneblock.island.bossbar` | `/ob bossbar` | 全員 |
| `aoneblock.island.actionbar` | `/ob actionbar` | 全員 |

## AOneBlockのみのパーミッション { #permissions-only-in-aoneblock }

| パーミッション | 許可 | デフォルト |
|---|---|---|
| `aoneblock.count` | `/ob count` | 全員 |
| `aoneblock.phases` | `/ob phases` | オペレーター |
| `aoneblock.island.setcount` | `/ob setCount` | オペレーター |
| `aoneblock.respawn-block` | `/ob respawnBlock` | 全員 |
| `aoneblock.island.bossbar` | `/ob bossbar` | 全員 |
| `aoneblock.island.actionbar` | `/ob actionbar` | 全員 |
| `aoneblock.admin.setcount` | `/obadmin setcount` | オペレーター |
| `aoneblock.admin.setchest` | `/obadmin setchest` | オペレーター |
| `aoneblock.admin.sanity` | `/obadmin sanity` | オペレーター |
| `aoneblock.admin.phases` | `/obadmin phases` | オペレーター |

管理者およびモデレーターパーミッション（`aoneblock.admin.*`、`aoneblock.mod.*`）はデフォルトでオペレーター用です。[スタッフパーミッション](../../BentoBox/Permissions-Guide.md#staff-permissions)を参照してください。
