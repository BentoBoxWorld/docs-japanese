# SkyGrid コマンド

<h1><b>SkyGrid 管理者コマンド</b>（エイリアス: /sga）</h2>
<table width="100%" align="center">
<tr>
<td align='left'><b>コマンド</b></td>
<td align='left'><b>説明</b></td>
<td align='left'><b>パーミッション</b></td>
</tr>
<tr>
<td align='left'><b>/sgadmin</b></td>
<td align='left'>SkyGridの管理者コマンドを一覧表示する</td>
<td align='left'>skygrid.admin</td>
</tr>
<tr>
<td align='left'><b>/sgadmin deaths</b></td>
<td align='left'>プレイヤーの死亡数を編集する</td>
<td align='left'>skygrid.admin.deaths</td>
</tr>
<tr>
<td align='left'><b>/sgadmin delete</b></td>
<td align='left'>プレイヤーを削除してエリアを再生成する</td>
<td align='left'>skygrid.admin.delete</td>
</tr>
<tr>
<td align='left'><b>/sgadmin getrank <player></b></td>
<td align='left'>プレイヤーのエリアでのランクを取得する</td>
<td align='left'>skygrid.admin.getrank</td>
</tr>
<tr>
<td align='left'><b>/sgadmin info <player></b></td>
<td align='left'>現在地またはプレイヤーのエリアの情報を取得する</td>
<td align='left'>skygrid.mod.info</td>
</tr>
<tr>
<td align='left'><b>/sgadmin kick <player></b></td>
<td align='left'>チームからプレイヤーを追放する</td>
<td align='left'>skygrid.mod.team</td>
</tr>
<tr>
<td align='left'><b>/sgadmin range</b></td>
<td align='left'>管理者エリア範囲コマンド</td>
<td align='left'>skygrid.admin.setrange</td>
</tr>
<tr>
<td align='left'><b>/sgadmin register <player></b></td>
<td align='left'>現在地の未所有エリアにプレイヤーを登録する</td>
<td align='left'>skygrid.admin.register</td>
</tr>
<tr>
<td align='left'><b>/sgadmin reload</b></td>
<td align='left'>プラグインをリロードする</td>
<td align='left'>skygrid.admin.reload</td>
</tr>
<tr>
<td align='left'><b>/sgadmin resetflags</b></td>
<td align='left'>すべてのエリアをconfig.ymlのデフォルトフラグ設定にリセットする</td>
<td align='left'>skygrid.admin.settingsreset</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp</b></td>
<td align='left'>ブループリントを操作する</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp copy [air]</b></td>
<td align='left'>pos1とpos2で設定したクリップボードをコピーする（オプションで空気ブロックも含む）</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp load <bp name></b></td>
<td align='left'>ブループリントをクリップボードに読み込む</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp origin</b></td>
<td align='left'>ブループリントの原点を現在地に設定する</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp paste</b></td>
<td align='left'>クリップボードを現在地に貼り付ける</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp pos1</b></td>
<td align='left'>直方体クリップボードの第1コーナーを設定する</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp pos2</b></td>
<td align='left'>直方体クリップボードの第2コーナーを設定する</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp save <bp name></b></td>
<td align='left'>コピーしたクリップボードを保存する</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin setowner <player> [area owner]</b></td>
<td align='left'>エリアのオーナーシップをプレイヤーに移譲する。現在のオーナーを指定すればコンソールから実行できる</td>
<td align='left'>skygrid.mod.team</td>
</tr>
<tr>
<td align='left'><b>/sgadmin setrank <player> <rank></b></td>
<td align='left'>プレイヤーのエリアでのランクを設定する</td>
<td align='left'>skygrid.admin.setrank</td>
</tr>
<tr>
<td align='left'><b>/sgadmin setspawn</b></td>
<td align='left'>このゲームモードのスポーンとしてエリアを設定する</td>
<td align='left'>skygrid.admin.setspawn</td>
</tr>
<tr>
<td align='left'><b>/sgadmin tp <player></b></td>
<td align='left'>プレイヤーのエリアにテレポートする</td>
<td align='left'>skygrid.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/sgadmin tpend <player></b></td>
<td align='left'>プレイヤーのエンドエリアにテレポートする</td>
<td align='left'>skygrid.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/sgadmin tpnether <player></b></td>
<td align='left'>プレイヤーのネザーエリアにテレポートする</td>
<td align='left'>skygrid.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/sgadmin unregister <owner></b></td>
<td align='left'>エリアのブロックを保持したままオーナーの登録を解除する</td>
<td align='left'>skygrid.admin.unregister</td>
</tr>
<tr>
<td align='left'><b>/sgadmin version</b></td>
<td align='left'>BentoBoxとアドオンのバージョンを表示する</td>
<td align='left'>skygrid.admin.version</td>
</tr>
<tr>
<td align='left'><b>/sgadmin why <player></b></td>
<td align='left'>コンソールの保護デバッグレポートのオン/オフを切り替える</td>
<td align='left'>skygrid.admin.why</td>
</tr>
</table>

<h1><b>SkyGrid プレイヤーコマンド</b>（エイリアス: /sg）</h2>
<table width="100%" align="center">
<tr>
<td align='left'><b>コマンド</b></td>
<td align='left'><b>説明</b></td>
<td align='left'><b>パーミッション</b></td>
</tr>
<tr>
<td align='left'><b>/skygrid</b></td>
<td align='left'>メインのプレイヤーコマンド</td>
<td align='left'>skygrid.island</td>
</tr>
<tr>
<td align='left'><b>/skygrid ban <player></b></td>
<td align='left'>プレイヤーをエリアからBANする</td>
<td align='left'>skygrid.island.ban</td>
</tr>
<tr>
<td align='left'><b>/skygrid banlist</b></td>
<td align='left'>BANされたプレイヤーの一覧を表示する</td>
<td align='left'>skygrid.island.ban</td>
</tr>
<tr>
<td align='left'><b>/skygrid create</b></td>
<td align='left'>新しいエリアを作成する</td>
<td align='left'>skygrid.island.create</td>
</tr>
<tr>
<td align='left'><b>/skygrid expel <player></b></td>
<td align='left'>プレイヤーをエリアから追放する</td>
<td align='left'>skygrid.island.expel</td>
</tr>
<tr>
<td align='left'><b>/skygrid go</b></td>
<td align='left'>エリアのホームにテレポートする</td>
<td align='left'>skygrid.island.home</td>
</tr>
<tr>
<td align='left'><b>/skygrid info <player></b></td>
<td align='left'>自分またはプレイヤーのエリアの情報を表示する</td>
<td align='left'>skygrid.island.info</td>
</tr>
<tr>
<td align='left'><b>/skygrid language</b></td>
<td align='left'>言語を選択する</td>
<td align='left'>skygrid.island.language</td>
</tr>
<tr>
<td align='left'><b>/skygrid reset</b></td>
<td align='left'>エリアをリスタートして古いエリアを削除する</td>
<td align='left'>skygrid.island.reset</td>
</tr>
<tr>
<td align='left'><b>/skygrid sethome</b></td>
<td align='left'>ホームのテレポートポイントを設定する</td>
<td align='left'>skygrid.island.sethome</td>
</tr>
<tr>
<td align='left'><b>/skygrid setname <name></b></td>
<td align='left'>エリアに名前を設定する</td>
<td align='left'>skygrid.island.name</td>
</tr>
<tr>
<td align='left'><b>/skygrid settings</b></td>
<td align='left'>エリアの設定を表示する</td>
<td align='left'>skygrid.island.settings</td>
</tr>
<tr>
<td align='left'><b>/skygrid spawn</b></td>
<td align='left'>スポーンにテレポートする</td>
<td align='left'>skygrid.island.spawn</td>
</tr>
<tr>
<td align='left'><b>/skygrid resetname</b></td>
<td align='left'>エリア名をリセットする</td>
<td align='left'>skygrid.mod.resetname</td>
</tr>
<tr>
<td align='left'><b>/skygrid unban <player></b></td>
<td align='left'>プレイヤーのエリアへのBANを解除する</td>
<td align='left'>skygrid.island.ban</td>
</tr>
<tr>
<td align='left'><b>/skygrid team</b></td>
<td align='left'>チームを管理する</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team accept</b></td>
<td align='left'>招待を承諾する</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team coop <player></b></td>
<td align='left'>プレイヤーにエリアのコープランクを付与する</td>
<td align='left'>skygrid.island.team.coop</td>
</tr>
<tr>
<td align='left'><b>/skygrid team demote <player></b></td>
<td align='left'>エリアのプレイヤーのランクを1段階下げる</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team invite <player></b></td>
<td align='left'>プレイヤーをエリアに招待する</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team kick <player></b></td>
<td align='left'>エリアからメンバーを削除する</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team leave</b></td>
<td align='left'>エリアを離れる</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team promote <player></b></td>
<td align='left'>エリアのプレイヤーのランクを1段階上げる</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team reject</b></td>
<td align='left'>招待を拒否する</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team setowner <player></b></td>
<td align='left'>エリアのオーナーをメンバーに移譲する</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team trust <player></b></td>
<td align='left'>プレイヤーにエリアのトラストランクを付与する</td>
<td align='left'>skygrid.island.team.trust</td>
</tr>
<tr>
<td align='left'><b>/skygrid team uncoop <player></b></td>
<td align='left'>プレイヤーからコープランクを削除する</td>
<td align='left'>skygrid.island.team.coop</td>
</tr>
<tr>
<td align='left'><b>/skygrid team untrust <player></b></td>
<td align='left'>プレイヤーからトラストランクを削除する</td>
<td align='left'>skygrid.island.team.trust</td>
</tr>
</table>
