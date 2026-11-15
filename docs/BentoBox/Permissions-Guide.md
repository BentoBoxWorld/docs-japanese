# パーミッションと VIP パーク

BentoBoxはあらゆるパーミッションプラグインで動作します（LuckPermsが最も一般的です）。このページではBentoBoxのパーミッション名の付け方、プレイヤーがデフォルトでどのパーミッションを持っているか、そしてランクやVIPをより大きなチーム、より大きなアイランド、より多くのホーム、その他の特典で与える方法を説明しています。

!!! info "このページの例"
    例はBSkyBlockを使用しており、そのパーミッションは`bskyblock.`で始まります。また、LuckPermsコマンドを使用しています。各ゲームモードには独自のプレフィックスがあります。例えば`aoneblock.`、`acidisland.`、`caveblock.`などですので、特典はゲームモードごとに1回付与する必要があります。

## パーミッション名の付け方

| パーミッション先頭 | 用途 | デフォルトで誰が持っているか |
|---|---|---|
| `bentobox.` | `/bentobox`コマンド | オペレーター（`bentobox.about`はみんな） |
| `<gamemode>.island.` | `bskyblock.island.team.invite`などのプレイヤーコマンド | 主にプレイヤー。[下記](#check-what-players-have-by-default)を参照 |
| `<gamemode>.admin.` | `bskyblock.admin.delete`などの管理者コマンド | オペレーター |
| `<gamemode>.mod.` | `bskyblock.mod.info`などのモデレーターコマンドと保護バイパス | オペレーター |
| `<gamemode>.settings.` | `/island settings`でアイランド設定を変更 | プレイヤー |
| `<gamemode>.<thing>.<number>` | `bskyblock.team.maxsize.8`などの制限 | 誰も持っていません：設定値が使用されます |

アドオンは独自のパーミッションを追加します。それぞれの[アドオンのページ](../addons/Bank/index.md)にリストがあります。

### プレイヤーがデフォルトで持っているものを確認

コンソールで**`/bentobox perms`** を実行してください。すべてのBentoBoxとゲームモードコマンドのパーミッションがそのデフォルト（`TRUE`はみんな、`OP`はオペレーター、`FALSE`は誰も）と共に表示され、パーミッションプラグインに貼り付けられる形式になっています。

!!! warning "一部のプレイヤーコマンドはデフォルトでオペレーターのみ"
    BSkyBlock、AOneBlock、AcidIslandでは、`island.deletehome`と`island.renamehome`はデフォルトでオペレーターのみです。AOneBlockとAcidIslandでは`island.homes`もそうです。プレイヤーに複数のホームを与える場合は、これらも与えてください：

    ```
    /lp group default permission set bskyblock.island.homes true
    /lp group default permission set bskyblock.island.deletehome true
    /lp group default permission set bskyblock.island.renamehome true
    ```

## 数字が付いた特典

これらのパーミッションは数字で終わります。その数字はゲームモードの`config.yml`のそのプレイヤーの値に置き換わります。

| 特典 | パーミッション | 設定デフォルト | 確認対象 |
|---|---|---|---|
| チームサイズ（所有者含む） | `bskyblock.team.maxsize.<n>` | `island.max-team-size` | アイランド所有者 |
| Coop プレイヤー | `bskyblock.coop.maxsize.<n>` | `island.max-coop-size` | アイランド所有者 |
| 信頼できるプレイヤー | `bskyblock.trust.maxsize.<n>` | `island.max-trusted-size` | アイランド所有者 |
| アイランドサイズ（保護範囲） | `bskyblock.island.range.<n>` | `world.protection-range` | アイランド所有者 |
| ホーム数 | `bskyblock.island.maxhomes.<n>` | `island.max-homes` | アイランド所有者 |
| アイランド数 | `bskyblock.island.number.<n>` | `world.concurrent-islands` | プレイヤー |
| バンできるプレイヤー | `bskyblock.ban.maxlimit.<n>` | `world.ban-limit`（`-1` = 制限なし） | プレイヤー |

数字の計算方法：

- **最も高い数字が勝ちます。** `team.maxsize.6`と`team.maxsize.10`の両方を持つプレイヤーは10を得ます。ランクは競合することなくスタックできます。
- **その数字は設定値を置き換えます。たとえ低くてもです。** `team.maxsize.2`は、設定が4であってもチームサイズを2にします。制限を上げるためだけにこれらのパーミッションを与えてください。
- **`.*`は無視されます。** `bskyblock.team.maxsize.*`を持つプレイヤー（例えばワイルドカードまたはオペレーターのプラグイン経由）は、設定値を得ます。無制限ではなく、大きな数字を使用してください。
- **アイランド特典は所有者に従います。** チームサイズ、範囲、ホームはアイランド**所有者の**パーミッションから来ます。各メンバーのではなく。所有者がログインしたときに更新され、アイランド作成時に範囲も設定されます。
- **アイランドサイズは** `distance-between-islands`でキャップされます；それ以上を要求しても効果はありません。[アイランド](About/IslandManagement.md#island-size-protection-range)を参照してください。

## その他の特典

| 特典 | パーミッション |
|---|---|
| アイランド作成メニューのVIPスターターアイランド | `bskyblock.island.create.<bundle-name>`。`/bsbadmin blueprint`でそのバンドルをパーミッション要件に設定した後。[アイランド](About/IslandManagement.md#creating-islands)を参照 |
| アイランド名のカラーコード | `bskyblock.island.name.format` |
| コマンドクールダウンをスキップ（リセット、招待） | `bskyblock.mod.bypasscooldowns` |
| テレポートディレイをスキップ | `bskyblock.mod.bypassdelays` |
| アイランドからバンまたは追放されない | `bskyblock.admin.noban`、`bskyblock.admin.noexpel` |
| 特定のアイランド設定を変更できない | `bskyblock.settings.<FLAG_ID>`を削除。[保護、フラグとランク](Island-Protection,-Flags-&-Ranks.md#settings-tab)を参照 |

**パーミッションではない**こと：追加アイランドリセット（`/bsbadmin resets`を使用。[アイランド](About/IslandManagement.md#resetting-islands)を参照）、および誰かのアイランドに招待、キック、またはバンする権利（アイランド所有者がランクで制御します。[チームとランク](About/Teams.md#letting-members-manage-the-team)を参照）。

## 例：VIP ランク

BSkyBlockのVIPグループ、チームサイズ8、より大きなアイランド、3つのホーム、VIPスターターアイランド：

```
/lp creategroup vip
/lp group vip permission set bskyblock.team.maxsize.8 true
/lp group vip permission set bskyblock.island.range.100 true
/lp group vip permission set bskyblock.island.maxhomes.3 true
/lp group vip permission set bskyblock.island.homes true
/lp group vip permission set bskyblock.island.deletehome true
/lp group vip permission set bskyblock.island.renamehome true
/lp group vip permission set bskyblock.island.create.vip true
/lp user <player> parent add vip
```

プレイヤーは**ログアウトして再度ログイン**して、すでに持っているアイランドに対してチームサイズ、範囲、ホームを適用する必要があります。

ゲーム内のお金でアップグレードをステップバイステップ（より大きなアイランド、チームスロット増加、ホーム増加）を販売する場合は、[Upgrades](../addons/Upgrades/index.md)アドオンを参照してください。

## スタッフパーミッション

| 役割 | 付与 |
|---|---|
| 1つのゲームモードの完全な管理者 | `bskyblock.admin.*`と`bskyblock.mod.*` |
| 見ることはできるが変更できない管理者 | `bskyblock.mod.info`、`bskyblock.admin.tp`、`bskyblock.mod.bypasslock`、`bskyblock.mod.bypassban` |
| 任意の場所で構築できる管理者 | `bskyblock.mod.bypassprotect`と`bskyblock.mod.switch`を追加（`/bsbadmin switch`でバイパスをオフにできます） |
| BentoBox 管理者（リロード、管理、移行） | `bentobox.admin`とそのサブパーミッション |

すべての保護バイパスパーミッションは[保護、フラグとランク](Island-Protection,-Flags-&-Ranks.md#bypass-the-protection)で説明されています。

## トラブルシューティング

**特典が適用されません。**
アイランド特典は所有者から来ており、ログイン時に更新されます。所有者にログアウトして再度ログインするよう指示してください。範囲については、`distance-between-islands`がその数字より低くないか確認してください。

**VIP が通常プレイヤーより小さいチームになった。**
別のグループの低い数字が設定値を置き換えました。それを削除してください；プレイヤーが持つ最高の数字が使用されます。

**プレイヤーがコマンドを使用できない。**
`/bentobox perms`を実行し、そのコマンドのデフォルトを確認してください。それが`OP`または`FALSE`の場合、デフォルトグループにパーミッションを与えてください。

**特典が1つのゲームモードでは機能するが、別のモードでは機能しない。**
各ゲームモードには独自のプレフィックスがあります。`aoneblock.`、`acidisland.`などのパーミッションを再度与えてください。

## 関連項目を参照

- [パーミッション参照](Permissions.md)：すべてのBentoBoxとゲームモードパーミッション
- [コマンド参照](Commands.md)
- [チームとランク](About/Teams.md)、[アイランド](About/IslandManagement.md)、[保護、フラグとランク](Island-Protection,-Flags-&-Ranks.md)
