# BSkyBlock パーミッション

BSkyBlockパーミッションは`bskyblock.`で始まります。すべてのパーミッションは[パーミッションリファレンス](../../BentoBox/Permissions.md)に`bskyblock`の代わりにリストされています。より大きなチーム、アイランド、より多くのホームなどのVIP特典については、[パーミッション&VIP特典](../../BentoBox/Permissions-Guide.md)を参照してください。

## プレイヤーコマンド：デフォルトで誰が持っているか

これらのデフォルトはBSkyBlockの`addon.yml`から来ています。**全員**とは、除外しない限りすべてのプレイヤーが権限を持つことを意味します。**オペレーター**とは、パーミッションプラグインでプレイヤーに与える必要があることを意味します。コンソールで`/bentobox perms`を実行して、サーバーのデフォルトを確認してください。

| パーミッション | コマンド | デフォルト |
|---|---|---|
| `bskyblock.island` | プレイヤーコマンド自体 | 全員 |
| `bskyblock.island.create` | `create` | 全員 |
| `bskyblock.island.home` | `go` | 全員 |
| `bskyblock.island.homes` | `homes` | 全員 |
| `bskyblock.island.sethome` | `sethome` | 全員 |
| `bskyblock.island.deletehome` | `deletehome` | 全員 |
| `bskyblock.island.renamehome` | `renamehome` | 全員 |
| `bskyblock.island.spawn` | `spawn` | 全員 |
| `bskyblock.island.info` | `info` | 全員 |
| `bskyblock.island.near` | `near` | 全員 |
| `bskyblock.island.reset` | `reset` | 全員 |
| `bskyblock.island.name` | `setname`, `resetname` | 全員 |
| `bskyblock.island.language` | `language` | 全員 |
| `bskyblock.island.settings` | `settings` | 全員 |
| `bskyblock.island.lock` | `lock` | 全員 |
| `bskyblock.island.ban` | `ban`, `unban`, `banlist` | 全員 |
| `bskyblock.island.expel` | `expel` | 全員 |
| `bskyblock.island.team` | `team` | 全員 |
| `bskyblock.island.team.invite` | `team invite` | 全員 |
| `bskyblock.island.team.accept` | `team accept` | 全員 |
| `bskyblock.island.team.reject` | `team reject` | 全員 |
| `bskyblock.island.team.leave` | `team leave` | 全員 |
| `bskyblock.island.team.kick` | `team kick` | 全員 |
| `bskyblock.island.team.promote` | `team promote`, `team demote` | 全員 |
| `bskyblock.island.team.setowner` | `team setowner` | 全員 |
| `bskyblock.island.team.trust` | `team trust`, `team untrust` | 全員 |
| `bskyblock.island.team.coop` | `team coop`, `team uncoop` | 全員 |

管理者およびモデレーターパーミッション（`bskyblock.admin.*`、`bskyblock.mod.*`）はデフォルトでオペレーター用です。[スタッフパーミッション](../../BentoBox/Permissions-Guide.md#staff-permissions)を参照してください。
