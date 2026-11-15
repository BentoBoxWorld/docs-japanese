# コマンド { #commands }

すべてのBentoBoxおよびそのゲームモードのコマンドは、BentoBoxソースから生成されています。使用方法については、[管理者ガイド](About/Teams.md)と[プレイヤーガイド](Player-Guide.md)を参照してください。

## ゲームモードコマンドの名付け方 { #how-game-mode-commands-are-named }

各ゲームモードは独自のプレイヤーコマンドと管理者コマンドを持ちます。以下の表は、`/[player_command]`と`/[admin_command]`として記述します。権限はゲームモードのプレフィックスで始まり、`[gamemode].`として記述します：

| ゲームモード | `[player_command]` | `[admin_command]` | `[gamemode]` |
|---|---|---|---|
| BSkyBlock | `/island`、`/is` | `/bsbadmin`、`/bsb` | `bskyblock` |
| AOneBlock | `/ob`、`/oneblock` | `/oba`、`/obadmin` | `aoneblock` |
| AcidIsland | `/ai` | `/acid` | `acidisland` |
| CaveBlock | `/cave`、`/cb` | `/cbadmin`、`/cba` | `caveblock` |

他のゲームモードはそれぞれのページにリストされています。すべてのラベルはゲームモードの`config.yml`で変更できます。

サブコマンドなしでコマンドを入力すると、デフォルトが実行されます。プレイヤーの場合、`/[player_command]`はアイランドを作成するかホームにテレポートし（[アイランド](About/IslandManagement.md#creating-islands)を参照）、`/[admin_command]`と`help`はプレイヤーが使用できるコマンドをリストします。

アドオンは例えば`/island level`または`/island challenges`のように、これらにサブコマンドを追加します。各[アドオンのページ](../addons/Bank/index.md)を参照してください。

## BentoBoxコマンド { #bentobox-commands }

`/bentobox`コマンド（エイリアス`/bbox`）はBentoBox自体を管理します。

| コマンド | 説明 | 権限 |
|---|---|---|
| `/bentobox about` | 著作権とライセンス情報 | `bentobox.about` |
| `/bentobox version` | BentoBox、アドオン、サーバーのバージョン。サポートを求めるときに含めてください | `bentobox.version` |
| `/bentobox reload` | BentoBoxとすべてのアドオン、設定、ロケール、メニューテンプレートを再度読み込む | `bentobox.admin.reload` |
| `/bentobox reload locales` | ロケールファイルのみを再度読み込む | `bentobox.admin.reload` |
| `/bentobox manage` | 管理パネルを開く | `bentobox.admin.manage` |
| `/bentobox catalog` | ゲームモードとアドオンのカタログを開く | `bentobox.admin.catalog` |
| `/bentobox locale` | ロケールファイルをチェックして不足している翻訳を見つける | `bentobox.admin.locale` |
| `/bentobox migrate` | データベースタイプ間でデータを移動します。[データベースの変更](Database-transition.md)を参照 | `bentobox.admin.migrate` |
| `/bentobox perms` | すべてのコマンド権限とそのデフォルトを出力します（コンソールのみ） | `bentobox.admin.perms` |
| `/bentobox rank [list \| add \| remove] [rank reference] [rank value]` | アイランドランクをリスト、追加、削除します。[チーム＆ランク](About/Teams.md#custom-ranks)を参照 | `bentobox.admin.rank` |
| `/bentobox placeholders` | プレースホルダーブラウザを開く | `bentobox.admin.placeholders` |
| `/bentobox dump-placeholders` | すべてのプレースホルダーをマークダウンファイルに書き込む | `bentobox.admin.dump-placeholders` |

## プレイヤーコマンド { #player-commands }

| コマンド | 説明 | 権限 |
|---|---|---|
| `/[player_command] ban <player>` | プレイヤーをアイランドからバンする | `[gamemode].island.ban` |
| `/[player_command] banlist` | バンされたプレイヤーをリストする | `[gamemode].island.ban` |
| `/[player_command] create <blueprint>` | アイランドを作成し、オプションでブループリントを使用します（権限が必要） | `[gamemode].island.create` |
| `/[player_command] deletehome [home name]` | ホームの位置を削除する | `[gamemode].island.deletehome` |
| `/[player_command] expel <player>` | プレイヤーをアイランドから追い出す | `[gamemode].island.expel` |
| `/[player_command] go [home name]` | アイランドにテレポートする | `[gamemode].island.home` |
| `/[player_command] homes` | ホームをリストする | `[gamemode].island.homes` |
| `/[player_command] info <player>` | アイランドまたはプレイヤーのアイランドについての情報を表示 | `[gamemode].island.info` |
| `/[player_command] language [language]` | 言語を選択 | `[gamemode].island.language` |
| `/[player_command] lock` | アイランドをロック/アンロック | `[gamemode].island.lock` |
| `/[player_command] near` | 周りの近隣アイランドの名前を表示 | `[gamemode].island.near` |
| `/[player_command] renamehome [home name]` | ホームの位置を名前変更 | `[gamemode].island.renamehome` |
| `/[player_command] reset <blueprint>` | アイランドを再起動して古いものを削除 | `[gamemode].island.reset` |
| `/[player_command] resetname` | アイランド名をリセット | `[gamemode].island.name` |
| `/[player_command] sethome` | ホームテレポート地点を設定 | `[gamemode].island.sethome` |
| `/[player_command] setname <name>` | アイランドの名前を設定 | `[gamemode].island.name` |
| `/[player_command] settings` | アイランド設定を表示 | `[gamemode].island.settings` |
| `/[player_command] spawn` | スポーンにテレポート | `[gamemode].island.spawn` |
| `/[player_command] team` | チームを管理 | `[gamemode].island.team` |
| `/[player_command] team accept` | 招待を承認 | `[gamemode].island.team.accept` |
| `/[player_command] team coop <player>` | プレイヤーをアイランドのcoop権限にする | `[gamemode].island.team.coop` |
| `/[player_command] team demote <player>` | プレイヤーを1ランク下げる（メンバー以下にはなりません） | `[gamemode].island.team.promote` |
| `/[player_command] team invite <player>` | プレイヤーをアイランドに招待 | `[gamemode].island.team.invite` |
| `/[player_command] team kick <player>` | メンバーをアイランドから削除 | `[gamemode].island.team.kick` |
| `/[player_command] team leave` | アイランドを脱退 | `[gamemode].island.team.leave` |
| `/[player_command] team promote <player>` | プレイヤーをアイランドでランク上げ | `[gamemode].island.team.promote` |
| `/[player_command] team reject` | 招待を拒否 | `[gamemode].island.team.reject` |
| `/[player_command] team setowner <player>` | アイランドの所有権をメンバーに譲渡 | `[gamemode].island.team.setowner` |
| `/[player_command] team trust <player>` | プレイヤーにアイランドの信頼権限を与える | `[gamemode].island.team.trust` |
| `/[player_command] team uncoop <player>` | プレイヤーからcoop権限を削除 | `[gamemode].island.team.coop` |
| `/[player_command] team untrust <player>` | プレイヤーから信頼権限を削除 | `[gamemode].island.team.trust` |
| `/[player_command] unban <player>` | プレイヤーをアイランドからアンバン | `[gamemode].island.ban` |

## 管理者コマンド { #admin-commands }

管理者コマンドはデフォルトではオペレーター用です。`mod.`権限を持つコマンドはフルアドミンではないモデレーター向けです。[権限とVIPパーク](Permissions-Guide.md#staff-permissions)を参照してください。

| コマンド | 説明 | 権限 |
|---|---|---|
| `/[admin_command] blueprint <load/copy/paste/pos1/pos2/save>` | ブループリントを操作 | `[gamemode].admin.blueprint` |
| `/[admin_command] blueprint copy [air] [biome] [nowater]` | pos1とpos2で設定されたクリップボードをコピーし、オプションで空気、バイオーム、水ブロックをコピー | `[gamemode].admin.blueprint.copy` |
| `/[admin_command] blueprint delete <name>` | ブループリントを削除 | `[gamemode].admin.blueprint.delete` |
| `/[admin_command] blueprint list` | 利用可能なブループリントをリスト | `[gamemode].admin.blueprint.list` |
| `/[admin_command] blueprint load <name>` | ブループリントをクリップボードに読み込む | `[gamemode].admin.blueprint.load` |
| `/[admin_command] blueprint origin` | ブループリントの原点を現在の位置に設定 | `[gamemode].admin.blueprint.origin` |
| `/[admin_command] blueprint paste` | クリップボードを現在の位置に貼り付け | `[gamemode].admin.blueprint.paste` |
| `/[admin_command] blueprint pos1` | 直方体クリップボードの1番目のコーナーを設定 | `[gamemode].admin.blueprint.pos1` |
| `/[admin_command] blueprint pos2` | 直方体クリップボードの2番目のコーナーを設定 | `[gamemode].admin.blueprint.pos2` |
| `/[admin_command] blueprint rename <blueprint name> <new name>` | ブループリントを名前変更 | `[gamemode].admin.blueprint.rename` |
| `/[admin_command] blueprint save <blueprint name>` | コピーされたクリップボードを保存 | `[gamemode].admin.blueprint.save` |
| `/[admin_command] blueprint sink` | ブループリントを貼り付けたときに海底に沈むように設定 | `[gamemode].admin.blueprint.sink` |
| `/[admin_command] deaths` | プレイヤーのデスを編集 | `[gamemode].admin.deaths` |
| `/[admin_command] deaths add <player> <deaths>` | プレイヤーにデスを追加 | `[gamemode].admin.deaths.add` |
| `/[admin_command] deaths remove <player> <deaths>` | プレイヤーからデスを削除 | `[gamemode].admin.deaths.remove` |
| `/[admin_command] deaths reset <player>` | プレイヤーのデスをリセット | `[gamemode].admin.deaths.reset` |
| `/[admin_command] deaths set <player> <deaths>` | プレイヤーのデスを設定 | `[gamemode].admin.deaths.set` |
| `/[admin_command] delete [player]` | プレイヤーのアイランドを削除するか、プレイヤーが指定されていない場合は立っているアイランドを削除 | `[gamemode].admin.delete` |
| `/[admin_command] deletehomes <player>` | アイランドから名前付きホームすべてを削除 | `[gamemode].mod.deletehomes` |
| `/[admin_command] getrank <player> [island owner]` | プレイヤーのアイランドまたはオーナーのアイランドでのプレイヤーのランクを取得 | `[gamemode].admin.getrank` |
| `/[admin_command] info <player> [island name]` | 現在の位置またはプレイヤーのアイランドについての情報を取得 | `[gamemode].mod.info` |
| `/[admin_command] maxhomes <number / player> <number> [island name]` | このアイランドまたはプレイヤーのアイランドで許可されているホーム数を変更 | `[gamemode].mod.maxhomes` |
| `/[admin_command] purge [days]` | [days]日以上触れられていないアイランドのリージョンファイルを削除（ディスク解放） | `[gamemode].admin.purge` |
| `/[admin_command] purge age-regions [days]` | デバッグ/テスト：リージョンファイルのタイムスタンプを書き直してパージ可能にする | `[gamemode].admin.purge.age-regions` |
| `/[admin_command] purge deleted` | 削除にマークされたアイランドのリージョンファイルをパージ | `[gamemode].admin.purge.deleted` |
| `/[admin_command] purge protect` | アイランドパージ保護をトグル | `[gamemode].admin.purge.protect` |
| `/[admin_command] purge unowned` | 所有されていないアイランドを削除可能にマークしてから回収できるようにする | `[gamemode].admin.purge.unowned` |
| `/[admin_command] range` | 管理アイランド範囲コマンド | `[gamemode].admin.range` |
| `/[admin_command] range add <player> <range> [island location]` | アイランド保護範囲を増加 | `[gamemode].admin.range.add` |
| `/[admin_command] range display` | アイランド範囲インジケーターを表示/非表示 | `[gamemode].admin.range.display` |
| `/[admin_command] range purgebonus <id>` | ボーナス範囲IDをすべてのアイランドから削除（例えばそれを追加したアドオンを削除した後） | `[gamemode].admin.range.purgebonus` |
| `/[admin_command] range remove <player> <range> [island location]` | アイランド保護範囲を減少 | `[gamemode].admin.range.remove` |
| `/[admin_command] range removebonus <player> [id]` | ボーナス範囲をアイランドから削除（すべてまたはID一つ） | `[gamemode].admin.range.removebonus` |
| `/[admin_command] range reset <player>` | アイランド保護範囲をワールドのデフォルトにリセット | `[gamemode].admin.range.reset` |
| `/[admin_command] range set <player> <range> [island location]` | アイランド保護範囲を設定 | `[gamemode].admin.range.set` |
| `/[admin_command] register <player>` | プレイヤーを所有されていないアイランドに登録 | `[gamemode].admin.register` |
| `/[admin_command] reload` | 再度読み込む | `[gamemode].admin.reload` |
| `/[admin_command] resetflags [flag]` | すべてのアイランドをconfig.ymlのデフォルトフラグ設定にリセット | `[gamemode].admin.resetflags` |
| `/[admin_command] resethome <player> [island name]` | プレイヤーのホームをデフォルトにリセット | `[gamemode].mod.resethome` |
| `/[admin_command] resetname` | プレイヤーアイランド名をリセット | `[gamemode].mod.resetname` |
| `/[admin_command] resets` | プレイヤーのリセット値を編集 | `[gamemode].admin.resets` |
| `/[admin_command] resets add <player> <resets>` | プレイヤーのアイランドリセット数を追加 | `[gamemode].admin.resets.add` |
| `/[admin_command] resets remove <player> <resets>` | プレイヤーのアイランドリセット数を削減 | `[gamemode].admin.resets.remove` |
| `/[admin_command] resets reset <player>` | プレイヤーのアイランドリセット数を0に設定 | `[gamemode].admin.resets.remove` |
| `/[admin_command] resets set <player> <resets>` | プレイヤーがアイランドをリセットした回数を設定 | `[gamemode].admin.resets.set` |
| `/[admin_command] setprotectionlocation [x y z coords]` | 現在の位置または[x y z]をアイランドの保護エリアの中心として設定 | `[gamemode].admin.setprotectionlocation` |
| `/[admin_command] setrank <player> <rank> [island owner \| x,y,z]` | プレイヤーをチームアイランドのランクに昇進/降格させるか、またはオーナーまたはx,y,z中心で指定されたアイランドに昇進/降格させる | `[gamemode].admin.setrank` |
| `/[admin_command] setspawn` | アイランドをこのゲームモードのスポーンとして設定 | `[gamemode].admin.setspawn` |
| `/[admin_command] setspawnpoint` | 現在の位置をこのアイランドのスポーンポイントとして設定 | `[gamemode].admin.setspawnpoint` |
| `/[admin_command] settings [player]/[world flag]/spawn-island [flag/active/disable] [rank/active/disable]` | 設定GUIを開くか設定を設定 | `[gamemode].admin.settings` |
| `/[admin_command] switch` | 保護バイパスのオン/オフ | `[gamemode].mod.switch` |
| `/[admin_command] team` | チームを管理 | `[gamemode].mod.team` |
| `/[admin_command] team add <owner> <player>` | プレイヤーをオーナーのチームに追加 | `[gamemode].mod.team.add` |
| `/[admin_command] team disband <owner>` | オーナーのチームを解散 | `[gamemode].mod.team.disband` |
| `/[admin_command] team disbandall` | このワールドのすべてのアイランドからすべてのメンバーとサブオーナーを削除 | `[gamemode].mod.team.disbandall` |
| `/[admin_command] team kick <team player> [x,y,z]` | チームからプレイヤーをキック | `[gamemode].mod.team.kick` |
| `/[admin_command] team maxsize <player> <size>` | プレイヤーのアイランドの最大チームサイズを設定（0を使用してワールドのデフォルトにリセット） | `[gamemode].mod.team.maxsize` |
| `/[admin_command] team setowner <player> [island owner]` | アイランドの所有権をプレイヤーに譲渡。コンソールから実行するために現在のアイランドオーナーに名前を付ける | `[gamemode].mod.team.setowner` |
| `/[admin_command] tp <player> [player's island]` | プレイヤーのアイランドにテレポート | `[gamemode].admin.tp` |
| `/[admin_command] tpend <player> [player's island]` | プレイヤーのアイランドのエンドにテレポート | `[gamemode].admin.tp` |
| `/[admin_command] tpnether <player> [player's island]` | プレイヤーのアイランドのネザーにテレポート | `[gamemode].admin.tp` |
| `/[admin_command] tpuser <teleporting player> <island's player> [player's island]` | プレイヤーを別のプレイヤーのアイランドにテレポート | `[gamemode].admin.tpuser` |
| `/[admin_command] tpuserend <teleporting player> <island's player> [player's island]` | プレイヤーを別のプレイヤーのアイランドのエンドにテレポート | `[gamemode].admin.tpuser` |
| `/[admin_command] tpusernether <teleporting player> <island's player> [player's island]` | プレイヤーを別のプレイヤーのアイランドのネザーにテレポート | `[gamemode].admin.tpuser` |
| `/[admin_command] undelete` | 立っている所有されていないアイランドから保留中の削除ステータスを削除 | `[gamemode].admin.undelete` |
| `/[admin_command] unregister <owner> [x,y,z]` | オーナーをアイランドから登録解除しますが、アイランドブロックは保持 | `[gamemode].admin.unregister` |
| `/[admin_command] version` | BentoBoxおよびアドオンのバージョンを表示 | `[gamemode].admin.version` |
| `/[admin_command] why <player>` | コンソール保護デバッグレポートをトグル | `[gamemode].admin.why` |

`/[admin_command] add`、`disband`、`kick`、`setowner`は、古いバージョンとの互換性のため、`team`なしでも機能します（例えば`/bsbadmin kick <player>`）。
