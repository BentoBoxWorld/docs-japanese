# Poseidon パーミッション

Poseidonパーミッションは`poseidon.`で始まります。すべてのパーミッションは[パーミッションリファレンス](../../BentoBox/Permissions.md)に`poseidon`の代わりにリストされています。より大きなチーム、アイランド、より多くのホームなどのVIP特典については、[パーミッション&VIP特典](../../BentoBox/Permissions-Guide.md)を参照してください。

## プレイヤーコマンド：デフォルトで誰が持っているか

これらのデフォルトはPoseidonの`addon.yml`から来ています。**全員**とは、除外しない限りすべてのプレイヤーが権限を持つことを意味します。**オペレーター**とは、パーミッションプラグインでプレイヤーに与える必要があることを意味します。コンソールで`/bentobox perms`を実行して、サーバーのデフォルトを確認してください。

| パーミッション | コマンド | デフォルト |
|---|---|---|
| `poseidon.island` | プレイヤーコマンド自体 | 全員 |
| `poseidon.island.create` | `create` | 全員 |
| `poseidon.island.home` | `go` | 全員 |
| `poseidon.island.homes` | `homes` | 全員 |
| `poseidon.island.sethome` | `sethome` | 全員 |
| `poseidon.island.deletehome` | `deletehome` | 全員 |
| `poseidon.island.renamehome` | `renamehome` | 全員 |
| `poseidon.island.spawn` | `spawn` | 全員 |
| `poseidon.island.info` | `info` | 全員 |
| `poseidon.island.near` | `near` | 全員 |
| `poseidon.island.reset` | `reset` | 全員 |
| `poseidon.island.name` | `setname`, `resetname` | 全員 |
| `poseidon.island.language` | `language` | 全員 |
| `poseidon.island.settings` | `settings` | 全員 |
| `poseidon.island.lock` | `lock` | 全員 |
| `poseidon.island.ban` | `ban`, `unban`, `banlist` | 全員 |
| `poseidon.island.expel` | `expel` | 全員 |
| `poseidon.island.team` | `team` | 全員 |
| `poseidon.island.team.invite` | `team invite` | 全員 |
| `poseidon.island.team.accept` | `team accept` | 全員 |
| `poseidon.island.team.reject` | `team reject` | 全員 |
| `poseidon.island.team.leave` | `team leave` | 全員 |
| `poseidon.island.team.kick` | `team kick` | 全員 |
| `poseidon.island.team.promote` | `team promote`, `team demote` | 全員 |
| `poseidon.island.team.setowner` | `team setowner` | 全員 |
| `poseidon.island.team.trust` | `team trust`, `team untrust` | 全員 |
| `poseidon.island.team.coop` | `team coop`, `team uncoop` | 全員 |

管理者およびモデレーターパーミッション（`poseidon.admin.*`、`poseidon.mod.*`）はデフォルトでオペレーター用です。[スタッフパーミッション](../../BentoBox/Permissions-Guide.md#staff-permissions)を参照してください。
