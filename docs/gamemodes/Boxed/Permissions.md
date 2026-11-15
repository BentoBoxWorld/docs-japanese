# Boxed パーミッション

Boxedパーミッションは`boxed.`で始まります。すべてのパーミッションは[パーミッションリファレンス](../../BentoBox/Permissions.md)に`boxed`の代わりにリストされています。より大きなチーム、アイランド、より多くのホームなどのVIP特典については、[パーミッション&VIP特典](../../BentoBox/Permissions-Guide.md)を参照してください。

## プレイヤーコマンド：デフォルトで誰が持っているか

これらのデフォルトはBoxedの`addon.yml`から来ています。**全員**とは、除外しない限りすべてのプレイヤーが権限を持つことを意味します。**オペレーター**とは、パーミッションプラグインでプレイヤーに与える必要があることを意味します。コンソールで`/bentobox perms`を実行して、サーバーのデフォルトを確認してください。

| パーミッション | コマンド | デフォルト |
|---|---|---|
| `boxed.island` | プレイヤーコマンド自体 | 全員 |
| `boxed.island.create` | `create` | 全員 |
| `boxed.island.home` | `go` | 全員 |
| `boxed.island.homes` | `homes` | 全員 |
| `boxed.island.sethome` | `sethome` | 全員 |
| `boxed.island.deletehome` | `deletehome` | 全員 |
| `boxed.island.renamehome` | `renamehome` | 全員 |
| `boxed.island.spawn` | `spawn` | 全員 |
| `boxed.island.info` | `info` | 全員 |
| `boxed.island.near` | `near` | 全員 |
| `boxed.island.reset` | `reset` | 全員 |
| `boxed.island.name` | `setname`, `resetname` | 全員 |
| `boxed.island.language` | `language` | 全員 |
| `boxed.island.settings` | `settings` | 全員 |
| `boxed.island.lock` | `lock` | 全員 |
| `boxed.island.ban` | `ban`, `unban`, `banlist` | 全員 |
| `boxed.island.expel` | `expel` | 全員 |
| `boxed.island.team` | `team` | 全員 |
| `boxed.island.team.invite` | `team invite` | 全員 |
| `boxed.island.team.accept` | `team accept` | 全員 |
| `boxed.island.team.reject` | `team reject` | 全員 |
| `boxed.island.team.leave` | `team leave` | 全員 |
| `boxed.island.team.kick` | `team kick` | 全員 |
| `boxed.island.team.promote` | `team promote`, `team demote` | 全員 |
| `boxed.island.team.setowner` | `team setowner` | 全員 |
| `boxed.island.team.trust` | `team trust`, `team untrust` | 全員 |
| `boxed.island.team.coop` | `team coop`, `team uncoop` | 全員 |

## Boxedのみのパーミッション

| パーミッション | 許可 | デフォルト |
|---|---|---|
| `boxed.admin.place` | `/boxadmin place` | オペレーター |

管理者およびモデレーターパーミッション（`boxed.admin.*`、`boxed.mod.*`）はデフォルトでオペレーター用です。[スタッフパーミッション](../../BentoBox/Permissions-Guide.md#staff-permissions)を参照してください。
