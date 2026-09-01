# ChunkBlock 権限

すべてのChunkBlock権限は`chunkblock.`とプレフィックス。デフォルトはバニラインストールが意図したゲームを権限プラグインなしでも再生するように選ばれています：すべてプレイヤーがニーズは`true`、管理ツールは OP、2つのノードはゲームそのものを変更——フェーズGUIとチャンクロックバイパス——オフまで、あなたは、それを付与。

!!! warning "`chunkblock.mod.bypasschunks` 意図的に OP デフォルトではない"
    ホルダーをチャンクロックから完全に免除し、有効`/chadmin bypass`。そのデフォルトは`false`、**not** `op`、だからスタッフはまったく同じルール再生まであなたは権限プラグインで明示的に付与。

    それは分離ノード`chunkblock.mod.bypasslock`、BentoBoxのアイランド*ロック*バイパスと異なる機能。

!!! note "2つのノードはデフォルトでオフ"
    - `chunkblock.phases` ——`/ch phases` GUI。プレイヤーがフェーズをブラウズしてリプレイしたい場合、付与。
    - `chunkblock.island.setcount` ——フェーズリプレイ。OP デフォルトのみ、フェーズGUIはチェック前に提供それを*「クリック変更」*。

## ChunkBlock固有の権限

| Permission | Description | Default |
|------------|-------------|---------|
| `chunkblock.admin.chunks` | '/chadmin chunks' コマンド使用を許可 - 検査、セット、またはプレイヤーのアンロック済みチャンクを再計算 | OP |
| `chunkblock.admin.phases` | '/chadmin phases' コマンド使用を許可 - フェーズ順序エディターを開く | OP |
| `chunkblock.admin.sanity` | '/chadmin sanity' コマンド使用を許可 - コンソール内のフェーズ確率のサニティチェックを表示 | OP |
| `chunkblock.admin.setchest` | '/chadmin setchest' コマンド使用を許可 - 見ているチェストをフェーズに指定された希少性と置く | OP |
| `chunkblock.admin.setcount` | '/chadmin setcount' コマンド使用を許可 - プレイヤーのブロックカウント設定 | OP |
| `chunkblock.count` | '/ch count' コマンド使用を許可 - ブロックカウントとフェーズを表示 | `true` |
| `chunkblock.island.actionbar` | '/ch actionbar' コマンド使用を許可 - actionbar をトグル | `true` |
| `chunkblock.island.bossbar` | '/ch bossbar' コマンド使用を許可 - bossbar をトグル | `true` |
| `chunkblock.island.chunks` | '/ch chunks' コマンド使用を許可 - アンロック済みチャンクと領土マップを表示 | `true` |
| `chunkblock.island.setcount` | '/ch setCount' コマンド使用を許可 - ブロックカウントを以前完了した値に設定 | OP |
| `chunkblock.mod.bypasschunks` | ホルダーをチャンクロックから完全に免除。'/chadmin bypass' をトグルも許可。ops に与えないデフォルト - それは明示的に付与されなければならず、スタッフはオプトインまでおよび同じルール再生。 | `false` |
| `chunkblock.phases` | '/ch phases' コマンド使用を許可 - すべてのフェーズの一覧を表示 | `false` |
| `chunkblock.respawn-block` | '/ch respawnBlock' コマンド使用を許可 - 消えてしまう状況でマジックブロックをリスポーン | `true` |

## 完全なリスト

| Permission | Description | Default |
|------------|-------------|---------|
| `chunkblock.admin` | '/chadmin' コマンド使用を許可 - 管理者コマンド | OP |
| `chunkblock.admin.blueprint` | '/chadmin blueprint' コマンド使用を許可 - ブループリントを操作 | OP |
| `chunkblock.admin.blueprint.copy` | '/chadmin blueprint copy' コマンド使用を許可 - pos1 と pos2 によって設定されたクリップボードをコピー、オプションで air ブロック | OP |
| `chunkblock.admin.blueprint.delete` | '/chadmin blueprint delete' コマンド使用を許可 - ブループリントを削除 | OP |
| `chunkblock.admin.blueprint.list` | '/chadmin blueprint list' コマンド使用を許可 - 利用可能なブループリントを一覧表示 | OP |
| `chunkblock.admin.blueprint.load` | '/chadmin blueprint load' コマンド使用を許可 - ブループリントをクリップボードにロード | OP |
| `chunkblock.admin.blueprint.origin` | '/chadmin blueprint origin' コマンド使用を許可 - ブループリントの原点をあなたの位置に設定 | OP |
| `chunkblock.admin.blueprint.paste` | '/chadmin blueprint paste' コマンド使用を許可 - クリップボードをあなたの位置に貼り付け | OP |
| `chunkblock.admin.blueprint.pos1` | '/chadmin blueprint pos1' コマンド使用を許可 - 立方体クリップボードの 1 番目のコーナーを設定 | OP |
| `chunkblock.admin.blueprint.pos2` | '/chadmin blueprint pos2' コマンド使用を許可 - 立方体クリップボードの 2 番目のコーナーを設定 | OP |
| `chunkblock.admin.blueprint.rename` | '/chadmin blueprint rename' コマンド使用を許可 - ブループリントを名前変更 | OP |
| `chunkblock.admin.blueprint.save` | '/chadmin blueprint save' コマンド使用を許可 - コピーされたクリップボードを保存 | OP |
| `chunkblock.admin.chunks` | '/chadmin chunks' コマンド使用を許可 - 検査、セット、またはプレイヤーのアンロック済みチャンクを再計算 | OP |
| `chunkblock.admin.deaths` | '/chadmin deaths' コマンド使用を許可 - プレイヤーの死亡を編集 | OP |
| `chunkblock.admin.deaths.add` | '/chadmin deaths add' コマンド使用を許可 - プレイヤーに死亡を追加 | OP |
| `chunkblock.admin.deaths.remove` | '/chadmin deaths remove' コマンド使用を許可 - プレイヤーから死亡を削除 | OP |
| `chunkblock.admin.deaths.reset` | '/chadmin deaths reset' コマンド使用を許可 - プレイヤーの死亡をリセット | OP |
| `chunkblock.admin.deaths.set` | '/chadmin deaths set' コマンド使用を許可 - プレイヤーの死亡を設定 | OP |
| `chunkblock.admin.delete` | '/chadmin delete' コマンド使用を許可 - プレイヤーのアイランドを削除 | OP |
| `chunkblock.admin.getrank` | '/chadmin getrank' コマンド使用を許可 - プレイヤーまたはオーナーのアイランドでプレイヤーのランクを取得 | OP |
| `chunkblock.admin.noban` | プレイヤーはアイランドから禁止されることはできない | OP |
| `chunkblock.admin.noexpel` | プレイヤーはアイランドから追放されることはできない | OP |
| `chunkblock.admin.phases` | '/chadmin phases' コマンド使用を許可 - フェーズ順序エディターを開く | OP |
| `chunkblock.admin.purge` | '/chadmin purge' コマンド使用を許可 - [日数]より長く放棄されたアイランドをパージ | OP |
| `chunkblock.admin.purge.protect` | '/chadmin purge protect' コマンド使用を許可 - アイランドパージ保護をトグル | OP |
| `chunkblock.admin.purge.status` | '/chadmin purge status' コマンド使用を許可 - パージのステータスを表示 | OP |
| `chunkblock.admin.purge.stop` | '/chadmin purge stop' コマンド使用を許可 - 進行中のパージを停止 | OP |
| `chunkblock.admin.purge.unowned` | '/chadmin purge unowned' コマンド使用を許可 - 未所有のアイランドをパージ | OP |
| `chunkblock.admin.range` | '/chadmin range' コマンド使用を許可 - 管理者アイランド範囲コマンド | OP |
| `chunkblock.admin.range.add` | '/chadmin range add' コマンド使用を許可 - アイランド保護範囲を増加 | OP |
| `chunkblock.admin.range.display` | '/chadmin range display' コマンド使用を許可 - アイランド範囲指標を表示/非表示 | OP |
| `chunkblock.admin.range.remove` | '/chadmin range remove' コマンド使用を許可 - アイランド保護範囲を減少 | OP |
| `chunkblock.admin.range.reset` | '/chadmin range reset' コマンド使用を許可 - アイランド保護範囲をワールドデフォルトにリセット | OP |
| `chunkblock.admin.range.set` | '/chadmin range set' コマンド使用を許可 - アイランド保護範囲を設定 | OP |
| `chunkblock.admin.register` | '/chadmin register' コマンド使用を許可 - プレイヤーを所有されていないアイランドに登録 | OP |
| `chunkblock.admin.reload` | '/chadmin reload' コマンド使用を許可 - リロード | OP |
| `chunkblock.admin.resetflags` | '/chadmin resetflags' コマンド使用を許可 - すべてのアイランドをデフォルトフラグ設定にリセット | OP |
| `chunkblock.admin.resets` | '/chadmin resets' コマンド使用を許可 - プレイヤーのリセット値を編集 | OP |
| `chunkblock.admin.resets.add` | '/chadmin resets add' コマンド使用を許可 - このプレイヤーのアイランドリセットカウントを追加 | OP |
| `chunkblock.admin.resets.remove` | '/chadmin resets remove' コマンド使用を許可 - プレイヤーのアイランドリセットカウントを削減 | OP |
| `chunkblock.admin.resets.set` | '/chadmin resets set' コマンド使用を許可 - このプレイヤーがアイランドをリセット回数を設定 | OP |
| `chunkblock.admin.sanity` | '/chadmin sanity' コマンド使用を許可 - コンソール内のフェーズ確率のサニティチェックを表示 | OP |
| `chunkblock.admin.setchest` | '/chadmin setchest' コマンド使用を許可 - 見ているチェストをフェーズに指定された希少性と置く | OP |
| `chunkblock.admin.setcount` | '/chadmin setcount' コマンド使用を許可 - プレイヤーのブロックカウント設定 | OP |
| `chunkblock.admin.setprotectionlocation` | '/chadmin setprotectionlocation' コマンド使用を許可 - 現在の位置または [x y z] をアイランドの保護エリアの中心として設定 | OP |
| `chunkblock.admin.setrank` | '/chadmin setrank' コマンド使用を許可 - プレイヤーまたはオーナーのアイランドでプレイヤーのランクを設定 | OP |
| `chunkblock.admin.setspawn` | '/chadmin setspawn' コマンド使用を許可 - アイランドをこのゲームモードのスポーンに設定 | OP |
| `chunkblock.admin.setspawnpoint` | '/chadmin setspawnpoint' コマンド使用を許可 - 現在の位置をこのアイランドのスポーンポイントとして設定 | OP |
| `chunkblock.admin.settings` | '/chadmin settings' コマンド使用を許可 - 設定 GUI を開く、または設定を設定 | OP |
| `chunkblock.admin.tp` | '/chadmin tp/tpnether/tpend' コマンド使用を許可 - プレイヤーのアイランドにテレポート | OP |
| `chunkblock.admin.unregister` | '/chadmin unregister' コマンド使用を許可 - オーナーをアイランドから登録解除、ただしアイランドブロックを保持 | OP |
| `chunkblock.admin.version` | '/chadmin version' コマンド使用を許可 - BentoBox とアドオンのバージョンを表示 | OP |
| `chunkblock.admin.why` | '/chadmin why' コマンド使用を許可 - コンソール保護デバッグレポーティングをトグル | OP |
| `chunkblock.count` | '/ch count' コマンド使用を許可 - ブロックカウントとフェーズを表示 | `true` |
| `chunkblock.island` | '/ch' コマンド使用を許可 - メインアイランドコマンド | `true` |
| `chunkblock.island.actionbar` | '/ch actionbar' コマンド使用を許可 - actionbar をトグル | `true` |
| `chunkblock.island.ban` | '/ch ban' または '/ch unban' または '/ch banlist' コマンド使用を許可 - 禁止されたプレイヤー | `true` |
| `chunkblock.island.bossbar` | '/ch bossbar' コマンド使用を許可 - bossbar をトグル | `true` |
| `chunkblock.island.chunks` | '/ch chunks' コマンド使用を許可 - アンロック済みチャンクと領土マップを表示 | `true` |
| `chunkblock.island.create` | '/ch create' コマンド使用を許可 - アイランドを作成、オプションのブループリント使用（権限が必要） | `true` |
| `chunkblock.island.deletehome` | '/ch deletehome' コマンド使用を許可 - ホーム位置を削除 | OP |
| `chunkblock.island.expel` | '/ch expel' コマンド使用を許可 - プレイヤーをアイランドから追放 | `true` |
| `chunkblock.island.home` | '/ch go' コマンド使用を許可 - あなたのアイランドにテレポート | `true` |
| `chunkblock.island.homes` | '/ch homes' コマンド使用を許可 - あなたのホームを一覧表示 | OP |
| `chunkblock.island.info` | '/ch info' コマンド使用を許可 - あなたのアイランドまたはプレイヤーのアイランドについての情報を表示 | `true` |
| `chunkblock.island.language` | '/ch language' コマンド使用を許可 - 言語を選択 | `true` |
| `chunkblock.island.lock` | アイランド設定でロックを許可 | `true` |
| `chunkblock.island.name` | '/ch setname' または '/ch resetname' コマンド使用を許可 - あなたのアイランド名 | `true` |
| `chunkblock.island.near` | '/ch near' コマンド使用を許可 - あなたの周りの隣接するアイランドの名前を表示 | `true` |
| `chunkblock.island.renamehome` | '/ch renamehome' コマンド使用を許可 - ホーム位置の名前を変更 | OP |
| `chunkblock.island.reset` | '/ch reset' コマンド使用を許可 - あなたのアイランドを再開し、古いのを削除 | `true` |
| `chunkblock.island.setcount` | '/ch setCount' コマンド使用を許可 - ブロックカウントを以前完了した値に設定 | OP |
| `chunkblock.island.sethome` | '/ch sethome' コマンド使用を許可 - あなたのホームテレポートポイントを設定 | `true` |
| `chunkblock.island.settings` | '/ch settings' コマンド使用を許可 - アイランド設定を表示 | `true` |
| `chunkblock.island.spawn` | '/ch spawn' コマンド使用を許可 - スポーンにテレポート | `true` |
| `chunkblock.island.team` | '/ch team' コマンド使用を許可 - チームを管理 | `true` |
| `chunkblock.island.team.accept` | '/ch team accept' コマンド使用を許可 - 招待を受け入れ | `true` |
| `chunkblock.island.team.coop` | '/ch team coop, uncoop' コマンド使用を許可 | `true` |
| `chunkblock.island.team.invite` | '/ch team invite' コマンド使用を許可 - プレイヤーをアイランドに招待 | `true` |
| `chunkblock.island.team.kick` | '/ch team kick' コマンド使用を許可 - メンバーをアイランドから削除 | `true` |
| `chunkblock.island.team.leave` | '/ch team leave' コマンド使用を許可 - あなたのアイランドを離れる | `true` |
| `chunkblock.island.team.promote` | '/ch team promote, demote' コマンド使用を許可 | `true` |
| `chunkblock.island.team.reject` | '/ch team reject' コマンド使用を許可 - 招待を拒否 | `true` |
| `chunkblock.island.team.setowner` | '/ch team setowner' コマンド使用を許可 - メンバーにアイランドの所有権を譲渡 | `true` |
| `chunkblock.island.team.trust` | '/ch team trust, untrust' コマンド使用を許可 | `true` |
| `chunkblock.mod.bypassban` | アイランド禁止をバイパス | OP |
| `chunkblock.mod.bypasschunks` | ホルダーをチャンクロックから完全に免除。'/chadmin bypass' をトグルも許可。ops に与えないデフォルト - それは明示的に付与されなければならず、スタッフはオプトインまでおよび同じルール再生。 | `false` |
| `chunkblock.mod.bypasscooldowns` | 管理者がクールダウンをバイパスすることを許可 | OP |
| `chunkblock.mod.bypassdelays` | 管理者が遅延をバイパスすることを許可 | OP |
| `chunkblock.mod.bypassexpel` | 管理者がアイランド追放をバイパスすることを許可 | OP |
| `chunkblock.mod.bypasslock` | アイランドロックをバイパス | OP |
| `chunkblock.mod.bypassprotect` | 管理者がアイランド保護をバイパスすることを許可 | OP |
| `chunkblock.mod.clearreset` | アイランドリセット制限をクリアすることを許可 | `false` |
| `chunkblock.mod.deletehomes` | '/chadmin deletehomes' コマンド使用を許可 - アイランドからすべての名前付きホームを削除 | OP |
| `chunkblock.mod.info` | '/chadmin info' コマンド使用を許可 - あなたがいる場所またはプレイヤーのアイランドについての情報を取得 | OP |
| `chunkblock.mod.lock` | アイランドのロック・ロック解除を許可 | OP |
| `chunkblock.mod.resetname` | '/chadmin resetname' コマンド使用を許可 - プレイヤーのアイランド名をリセット | OP |
| `chunkblock.mod.switch` | '/chadmin switch' コマンド使用を許可 - 保護バイパスをオン・オフ | OP |
| `chunkblock.mod.team` | '/chadmin team' コマンド使用を許可 - チームを管理 | `false` |
| `chunkblock.mod.team.add` | '/chadmin team add' または '/chadmin add' コマンド使用を許可 - プレイヤーをオーナーのチームに追加 | OP |
| `chunkblock.mod.team.disband` | '/chadmin team disband' または '/chadmin disband' コマンド使用を許可 - オーナーのチームを解散 | OP |
| `chunkblock.mod.team.fix` | '/chadmin team fix' または '/chadmin fix' コマンド使用を許可 - スキャンとクロスアイランドメンバーシップをデータベースで修正 | OP |
| `chunkblock.mod.team.kick` | '/chadmin team kick' または '/chadmin kick' コマンド使用を許可 - プレイヤーをチームからキック | OP |
| `chunkblock.mod.team.setowner` | '/chadmin team setowner' コマンド使用を許可 - プレイヤーにアイランドの所有権を譲渡 | OP |
| `chunkblock.phases` | '/ch phases' コマンド使用を許可 - すべてのフェーズの一覧を表示 | `false` |
| `chunkblock.respawn-block` | '/ch respawnBlock' コマンド使用を許可 - 消えてしまう状況でマジックブロックをリスポーン | `true` |
| `chunkblock.settings.*` | アイランドで設定の使用を許可 | `true` |
