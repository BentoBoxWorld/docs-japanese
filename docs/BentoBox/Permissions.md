# 権限 { #permissions }

すべてのBentoBox権限はBentoBoxソースから生成されています。使用方法（VIPランク、スタッフロール、一般的な誤り）については、[権限とVIPパーク](Permissions-Guide.md)を参照してください。

ゲームモード権限はゲームモードのプレフィックスで始まり、ここでは`[gamemode].`として記述します：`bskyblock.`、`aoneblock.`、`acidisland.`、`caveblock.`など。アドオン権限は各[アドオンのページ](../addons/Bank/index.md)にリストされています。

!!! tip "サーバーのデフォルトを確認してください"
    デフォルト（全員、オペレーターのみ、または誰も不可）は各ゲームモードによって設定され、ゲームモード間で異なります。コンソールで`/bentobox perms`を実行して、サーバー上のすべてのコマンド権限とそのデフォルトを出力します。

## BentoBox { #bentobox }

| 権限 | デフォルト | 許可すること |
|---|---|---|
| `bentobox.about` | 全員 | `/bentobox about` |
| `bentobox.version` | オペレーター | `/bentobox version` |
| `bentobox.admin` | オペレーター | `/bentobox`とそのサブコマンド |
| `bentobox.admin.reload` | オペレーター | `/bentobox reload`と`reload locales` |
| `bentobox.admin.manage` | オペレーター | `/bentobox manage` |
| `bentobox.admin.catalog` | オペレーター | `/bentobox catalog` |
| `bentobox.admin.locale` | オペレーター | `/bentobox locale` |
| `bentobox.admin.migrate` | オペレーター | `/bentobox migrate` |
| `bentobox.admin.perms` | オペレーター | `/bentobox perms` |
| `bentobox.admin.rank` | オペレーター | `/bentobox rank` |
| `bentobox.admin.placeholders` | オペレーター | `/bentobox placeholders` |
| `bentobox.admin.dump-placeholders` | オペレーター | `/bentobox dump-placeholders` |

## ゲームモード：プレイヤーコマンド { #game-mode-player-commands }

これらのほとんどはゲームモードによってすべてのユーザーに与えられます。`/bentobox perms`でチェックしてください。一部のゲームモードでは`island.homes`、`island.deletehome`、`island.renamehome`はデフォルトではオペレーターのみです。

| 権限 | 許可すること |
|---|---|
| `[gamemode].island` | プレイヤーコマンド自体と`help` |
| `[gamemode].island.ban` | `ban`、`banlist`、`unban` |
| `[gamemode].island.create` | `create` |
| `[gamemode].island.deletehome` | `deletehome` |
| `[gamemode].island.expel` | `expel` |
| `[gamemode].island.home` | `go` |
| `[gamemode].island.homes` | `homes` |
| `[gamemode].island.info` | `info` |
| `[gamemode].island.language` | `language` |
| `[gamemode].island.lock` | `lock` |
| `[gamemode].island.name` | `resetname`、`setname` |
| `[gamemode].island.near` | `near` |
| `[gamemode].island.renamehome` | `renamehome` |
| `[gamemode].island.reset` | `reset` |
| `[gamemode].island.sethome` | `sethome` |
| `[gamemode].island.settings` | `settings` |
| `[gamemode].island.spawn` | `spawn` |
| `[gamemode].island.team` | `team` |
| `[gamemode].island.team.accept` | `team accept` |
| `[gamemode].island.team.coop` | `team coop`、`team uncoop` |
| `[gamemode].island.team.invite` | `team invite` |
| `[gamemode].island.team.kick` | `team kick` |
| `[gamemode].island.team.leave` | `team leave` |
| `[gamemode].island.team.promote` | `team demote`、`team promote` |
| `[gamemode].island.team.reject` | `team reject` |
| `[gamemode].island.team.setowner` | `team setowner` |
| `[gamemode].island.team.trust` | `team trust`、`team untrust` |

## ゲームモード：管理者とモデレーターコマンド { #game-mode-admin-and-moderator-commands }

デフォルトではオペレーターのみです。

| 権限 | `/[admin_command]`を許可する |
|---|---|
| `[gamemode].admin` | 管理者コマンド自体と`help` |
| `[gamemode].admin.blueprint` | `blueprint` |
| `[gamemode].admin.blueprint.copy` | `blueprint copy` |
| `[gamemode].admin.blueprint.delete` | `blueprint delete` |
| `[gamemode].admin.blueprint.list` | `blueprint list` |
| `[gamemode].admin.blueprint.load` | `blueprint load` |
| `[gamemode].admin.blueprint.origin` | `blueprint origin` |
| `[gamemode].admin.blueprint.paste` | `blueprint paste` |
| `[gamemode].admin.blueprint.pos1` | `blueprint pos1` |
| `[gamemode].admin.blueprint.pos2` | `blueprint pos2` |
| `[gamemode].admin.blueprint.rename` | `blueprint rename` |
| `[gamemode].admin.blueprint.save` | `blueprint save` |
| `[gamemode].admin.blueprint.sink` | `blueprint sink` |
| `[gamemode].admin.deaths` | `deaths` |
| `[gamemode].admin.deaths.add` | `deaths add` |
| `[gamemode].admin.deaths.remove` | `deaths remove` |
| `[gamemode].admin.deaths.reset` | `deaths reset` |
| `[gamemode].admin.deaths.set` | `deaths set` |
| `[gamemode].admin.delete` | `delete` |
| `[gamemode].admin.getrank` | `getrank` |
| `[gamemode].admin.purge` | `purge` |
| `[gamemode].admin.purge.age-regions` | `purge age-regions` |
| `[gamemode].admin.purge.deleted` | `purge deleted` |
| `[gamemode].admin.purge.protect` | `purge protect` |
| `[gamemode].admin.purge.unowned` | `purge unowned` |
| `[gamemode].admin.range` | `range` |
| `[gamemode].admin.range.add` | `range add` |
| `[gamemode].admin.range.display` | `range display` |
| `[gamemode].admin.range.purgebonus` | `range purgebonus` |
| `[gamemode].admin.range.remove` | `range remove` |
| `[gamemode].admin.range.removebonus` | `range removebonus` |
| `[gamemode].admin.range.reset` | `range reset` |
| `[gamemode].admin.range.set` | `range set` |
| `[gamemode].admin.register` | `register` |
| `[gamemode].admin.reload` | `reload` |
| `[gamemode].admin.resetflags` | `resetflags` |
| `[gamemode].admin.resets` | `resets` |
| `[gamemode].admin.resets.add` | `resets add` |
| `[gamemode].admin.resets.remove` | `resets remove`、`resets reset` |
| `[gamemode].admin.resets.set` | `resets set` |
| `[gamemode].admin.setprotectionlocation` | `setprotectionlocation` |
| `[gamemode].admin.setrank` | `setrank` |
| `[gamemode].admin.setspawn` | `setspawn` |
| `[gamemode].admin.setspawnpoint` | `setspawnpoint` |
| `[gamemode].admin.settings` | `settings` |
| `[gamemode].admin.tp` | `tp`、`tpend`、`tpnether` |
| `[gamemode].admin.tpuser` | `tpuser`、`tpuserend`、`tpusernether` |
| `[gamemode].admin.undelete` | `undelete` |
| `[gamemode].admin.unregister` | `unregister` |
| `[gamemode].admin.version` | `version` |
| `[gamemode].admin.why` | `why` |
| `[gamemode].mod.deletehomes` | `deletehomes` |
| `[gamemode].mod.info` | `info` |
| `[gamemode].mod.maxhomes` | `maxhomes` |
| `[gamemode].mod.resethome` | `resethome` |
| `[gamemode].mod.resetname` | `resetname` |
| `[gamemode].mod.switch` | `switch` |
| `[gamemode].mod.team` | `team` |
| `[gamemode].mod.team.add` | `team add` |
| `[gamemode].mod.team.disband` | `team disband` |
| `[gamemode].mod.team.disbandall` | `team disbandall` |
| `[gamemode].mod.team.kick` | `team kick` |
| `[gamemode].mod.team.maxsize` | `team maxsize` |
| `[gamemode].mod.team.setowner` | `team setowner` |

## ゲームモード：制限とパーク { #game-mode-limits-and-perks }

これらは数字で終わり、そのプレイヤーの設定値を置き換えます。プレイヤーが持つ最高の数字が優先されます。ルールについては[権限とVIPパーク](Permissions-Guide.md#perks-with-a-number)を参照してください。

| 権限 | 設定 | 置き換える設定値 |
|---|---|---|
| `[gamemode].team.maxsize.<n>` | チームサイズ（所有者を含む）（アイランド所有者の権限） | `island.max-team-size` |
| `[gamemode].coop.maxsize.<n>` | Coopプレイヤー（アイランド所有者の権限） | `island.max-coop-size` |
| `[gamemode].trust.maxsize.<n>` | 信頼されたプレイヤー（アイランド所有者の権限） | `island.max-trusted-size` |
| `[gamemode].island.range.<n>` | アイランド保護範囲（アイランド所有者の権限） | `world.protection-range` |
| `[gamemode].island.maxhomes.<n>` | ホーム数（アイランド所有者の権限） | `island.max-homes` |
| `[gamemode].island.number.<n>` | プレイヤーが所有できるアイランド数 | `world.concurrent-islands` |
| `[gamemode].ban.maxlimit.<n>` | 一度にバンできるプレイヤー | `world.ban-limit` |

| 権限 | 許可すること |
|---|---|
| `[gamemode].island.create.<bundle>` | 権限が必要なスターターアイランド（ブループリントバンドル）を選択 |
| `[gamemode].island.name.format` | アイランド名のカラーコード |

## ゲームモード：アイランド設定 { #game-mode-island-settings }

| 権限 | 許可すること |
|---|---|
| `[gamemode].settings.<FLAG_ID>` | `/[player_command] settings`でその設定を変更 |
| `[gamemode].settings.*` | すべての設定を変更 |
| `[gamemode].admin.settings.<FLAG_ID>` | `/[admin_command] settings`でそのフラグを変更 |
| `[gamemode].admin.world.settings.<FLAG_ID>` | そのワールド設定またはワールド保護を変更 |
| `[gamemode].admin.set-world-defaults` | 管理者設定のワールド保護タブ |

フラグIDについては[保護、フラグとランク](Island-Protection,-Flags-&-Ranks.md)を参照してください。

## ゲームモード：モデレーターバイパス { #game-mode-moderator-bypasses }

| 権限 | 効果 |
|---|---|
| `[gamemode].mod.bypassprotect` | すべての保護フラグをどこでも無視 |
| `[gamemode].mod.bypass.<FLAG_ID>.everywhere` | 1つの保護フラグをどこでも無視 |
| `[gamemode].mod.bypass.<FLAG_ID>.island` | 1つの保護フラグをアイランドで無視 |
| `[gamemode].mod.bypasslock` | ロックされたアイランドに入る |
| `[gamemode].mod.bypassban` | バンされているアイランドに入る |
| `[gamemode].mod.bypassexpel` | 追い出されない |
| `[gamemode].mod.bypasscooldowns` | コマンドクールダウンをスキップ |
| `[gamemode].mod.bypassdelays` | テレポート遅延をスキップ |
| `[gamemode].admin.noban` | アイランドからバンされない |
| `[gamemode].admin.noexpel` | アイランドから追い出されない |

`/[admin_command] switch`はモデレーターのバイパス権限のオン/オフを切り替えます。[保護をバイパス](Island-Protection,-Flags-&-Ranks.md#bypass-the-protection)を参照してください。
