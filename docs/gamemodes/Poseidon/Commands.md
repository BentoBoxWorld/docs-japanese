<h1><b>Poseidon 管理者コマンド</b>（エイリアス: /padmin）</h2>
<table width="100%" align="center">
<tr>
<td align='left'><b>コマンド</b></td>
<td align='left'><b>説明</b></td>
<td align='left'><b>パーミッション</b></td>
</tr>
<tr>
<td align='left'><b>/padmin add <owner> <player></b></td>
<td align='left'>オーナーのチームにプレイヤーを追加する</td>
<td align='left'>poseidon.mod.team</td>
</tr>
<tr>
<td align='left'><b>/padmin challenges</b></td>
<td align='left'>/padmin challengesの管理者コマンドにアクセスする。Challengesアドオンが必要。</td>
<td align='left'>poseidon.admin.challenges</td>
</tr>
<tr>
<td align='left'><b>/padmin deaths</b></td>
<td align='left'>プレイヤーの死亡回数を編集する</td>
<td align='left'>poseidon.admin.deaths</td>
</tr>
<tr>
<td align='left'><b>/padmin delete</b></td>
<td align='left'>プレイヤーのレルムを削除する</td>
<td align='left'>poseidon.admin.delete</td>
</tr>
<tr>
<td align='left'><b>/padmin disband <owner></b></td>
<td align='left'>オーナーのチームを解散する</td>
<td align='left'>poseidon.mod.team</td>
</tr>
<tr>
<td align='left'><b>/padmin getrank <player></b></td>
<td align='left'>プレイヤーのレルムでのランクを取得する</td>
<td align='left'>poseidon.admin.getrank</td>
</tr>
<tr>
<td align='left'><b>/padmin info <player></b></td>
<td align='left'>現在地またはプレイヤーのレルムの情報を取得する</td>
<td align='left'>poseidon.mod.info</td>
</tr>
<tr>
<td align='left'><b>/padmin kick <team player></b></td>
<td align='left'>チームからプレイヤーを追放する</td>
<td align='left'>poseidon.mod.team</td>
</tr>
<tr>
<td align='left'><b>/padmin level <player></b></td>
<td align='left'>プレイヤーのレルムレベルを計算する — Levelアドオンが必要</td>
<td align='left'>poseidon.admin.level</td>
</tr>
<tr>
<td align='left'><b>/padmin range</b></td>
<td align='left'>管理者のレルム範囲コマンド</td>
<td align='left'>poseidon.admin.range</td>
</tr>
<tr>
<td align='left'><b>/padmin register <player></b></td>
<td align='left'>現在地のオーナーなしレルムにプレイヤーを登録する</td>
<td align='left'>poseidon.admin.register</td>
</tr>
<tr>
<td align='left'><b>/padmin reload</b></td>
<td align='left'>プラグインをリロードする</td>
<td align='left'>poseidon.admin.relaod</td>
</tr>
<tr>
<td align='left'><b>/padmin reset</b></td>
<td align='left'>commands.admin.resets.reset.description</td>
<td align='left'>poseidon.admin.settingsreset</td>
</tr>
<tr>
<td align='left'><b>/padmin bp</b></td>
<td align='left'>ブループリントを操作する</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin bp copy [air]</b></td>
<td align='left'>pos1とpos2で設定したクリップボードをコピーする（空気ブロックも含めることができる）</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin bp load <schem name></b></td>
<td align='left'>ブループリントをクリップボードに読み込む</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin bp origin</b></td>
<td align='left'>ブループリントの原点を現在地に設定する</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin bp paste</b></td>
<td align='left'>クリップボードを現在地にペーストする</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin bp pos1</b></td>
<td align='left'>直方体クリップボードの第1コーナーを設定する</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin bp pos2</b></td>
<td align='left'>直方体クリップボードの第2コーナーを設定する</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin bp save <blueprint name></b></td>
<td align='left'>コピーしたクリップボードを保存する</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<td align='left'><b>/padmin bp rename <blueprint name></b></td>
<td align='left'>ブループリントの名前を変更する</td>
<td align='left'>poseidon.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/padmin setowner <player> [realm owner]</b></td>
<td align='left'>レルムのオーナーをプレイヤーに移譲する。現在のオーナーを指定すればコンソールから実行できる</td>
<td align='left'>poseidon.mod.team</td>
</tr>
<tr>
<td align='left'><b>/padmin setrank <player> <rank></b></td>
<td align='left'>プレイヤーのレルムでのランクを設定する</td>
<td align='left'>poseidon.admin.setrank</td>
</tr>
<tr>
<td align='left'><b>/padmin setspawn</b></td>
<td align='left'>この場所にワールドのスポーン位置を設定する</td>
<td align='left'>poseidon.admin.setspawn</td>
</tr>
<tr>
<td align='left'><b>/padmin top</b></td>
<td align='left'>トップテンリストを表示する — Levelアドオンが必要</td>
<td align='left'>poseidon.admin.top</td>
</tr>
<tr>
<td align='left'><b>/padmin tp <player></b></td>
<td align='left'>プレイヤーのレルムにテレポートする</td>
<td align='left'>poseidon.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/padmin tpend <player></b></td>
<td align='left'>プレイヤーのエンドレルムにテレポートする</td>
<td align='left'>poseidon.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/padmin tpnether <player></b></td>
<td align='left'>プレイヤーのネザーレルムにテレポートする</td>
<td align='left'>poseidon.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/padmin unregister <owner></b></td>
<td align='left'>レルムからオーナーの登録を解除するが、レルムのブロックは保持する</td>
<td align='left'>poseidon.admin.unregister</td>
</tr>
<tr>
<td align='left'><b>/padmin version</b></td>
<td align='left'>BentoBoxとアドオンのバージョンを表示する</td>
<td align='left'>poseidon.admin.version</td>
</tr>
<tr>
<td align='left'><b>/padmin why <player></b></td>
<td align='left'>コンソールの保護デバッグレポートを切り替える</td>
<td align='left'>poseidon.admin.why</td>
</tr>
</table>

<h1><b>Poseidon プレイヤーコマンド</b>（エイリアス: /po）</h2>
<table width="100%" align="center">
<tr>
<td align='left'><b>コマンド</b></td>
<td align='left'><b>説明</b></td>
<td align='left'><b>パーミッション</b></td>
</tr>
<tr>
<td align='left'><b>/poseidon</b></td>
<td align='left'>メインのレルムコマンド</td>
<td align='left'>poseidon.island</td>
</tr>
<tr>
<td align='left'><b>/poseidon about</b></td>
<td align='left'>このアドオンについて</td>
<td align='left'>poseidon.island</td>
</tr>
<tr>
<td align='left'><b>/poseidon ban <player></b></td>
<td align='left'>プレイヤーを自分のレルムからBANする</td>
<td align='left'>poseidon.island.ban</td>
</tr>
<tr>
<td align='left'><b>/poseidon banlist</b></td>
<td align='left'>BANされたプレイヤーの一覧を表示する</td>
<td align='left'>poseidon.island.ban</td>
</tr>
<tr>
<td align='left'><b>/poseidon biomes</b></td>
<td align='left'>バイオーム変更GUIを開くメインのバイオームアドオンコマンド。Biomesアドオンが必要。</td>
<td align='left'>poseidon.admin.biomes</td>
</tr>
<tr>
<td align='left'><b>/poseidon challenges [Level]</b></td>
<td align='left'>/poseidon challengesコマンドの使用を許可する。Challengesアドオンが必要</td>
<td align='left'>poseidon.challenges</td>
</tr>
<tr>
<td align='left'><b>/poseidon create <blueprint></b></td>
<td align='left'>オプションのブループリントを使用してレルムを作成する（通常プレイヤーが直接使用するものではない）</td>
<td align='left'>poseidon.island.create</td>
</tr>
<tr>
<td align='left'><b>/poseidon go [home name]</b></td>
<td align='left'>自分のレルムまたは指定したホーム名にテレポートする（有効な場合）</td>
<td align='left'>poseidon.island.home</td>
</tr>
<tr>
<td align='left'><b>/poseidon info <player></b></td>
<td align='left'>自分のレルムまたはプレイヤーのレルムの情報を表示する</td>
<td align='left'>poseidon.island.info</td>
</tr>
<tr>
<td align='left'><b>/poseidon language</b></td>
<td align='left'>言語を選択する</td>
<td align='left'>poseidon.island.language</td>
</tr>
<tr>
<td align='left'><b>/poseidon level [player]</b></td>
<td align='left'>自分のレルムレベルを計算するか[player]のレベルを表示する — Levelアドオンが必要</td>
<td align='left'>poseidon.island.level</td>
</tr>
<tr>
<td align='left'><b>/poseidon near</b></td>
<td align='left'>周囲の隣接レルムの名前を表示する（ある場合）</td>
<td align='left'>poseidon.island.near</td>
</tr>
<tr>
<td align='left'><b>/poseidon reset</b></td>
<td align='left'>レルムをリスタートして古いレルムを削除する</td>
<td align='left'>poseidon.island.reset</td>
</tr>
<tr>
<td align='left'><b>/poseidon homes</b></td>
<td align='left'>設定したホームの一覧を表示する</td>
<td align='left'>poseidon.island.homes</td>
</tr>
<tr>
<td align='left'><b>/poseidon sethome [home name]</b></td>
<td align='left'>ホームのテレポートポイントを設定し、オプションで名前を付ける</td>
<td align='left'>poseidon.island.sethome</td>
</tr>
<tr>
<td align='left'><b>/poseidon deletehome [home name]</b></td>
<td align='left'>ホームのテレポートポイントを削除する</td>
<td align='left'>poseidon.island.deletehome</td>
</tr>
<tr>
<td align='left'><b>/poseidon rename [home name]</b></td>
<td align='left'>ホームのテレポートポイントの名前を変更する</td>
<td align='left'>poseidon.island.renamehome</td>
</tr>
<tr>
<td align='left'><b>/poseidon settings</b></td>
<td align='left'>レルムの設定を表示する</td>
<td align='left'>poseidon.island.settings</td>
</tr>
<tr>
<td align='left'><b>/poseidon spawn</b></td>
<td align='left'>スポーンにテレポートする</td>
<td align='left'>poseidon.island.home</td>
</tr>
<tr>
<td align='left'><b>/poseidon setname</b></td>
<td align='left'>レルムの名前を設定する</td>
<td align='left'>poseidon.mod.setname</td>
</tr>
<tr>
<td align='left'><b>/poseidon resetname</b></td>
<td align='left'>レルムの名前をリセットする</td>
<td align='left'>poseidon.mod.resetname</td>
</tr>
<tr>
<td align='left'><b>/poseidon unban <player></b></td>
<td align='left'>プレイヤーのレルムへのBANを解除する</td>
<td align='left'>poseidon.island.ban</td>
</tr>
<tr>
<td align='left'><b>/poseidon team</b></td>
<td align='left'>チームを管理する</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team accept</b></td>
<td align='left'>招待を承諾する</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team coop <player></b></td>
<td align='left'>プレイヤーにレルムのコープランクを付与する</td>
<td align='left'>poseidon.island.team.coop</td>
</tr>
<tr>
<td align='left'><b>/poseidon team demote <player></b></td>
<td align='left'>レルムのプレイヤーのランクを1段階下げる</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team leave</b></td>
<td align='left'>レルムを離れる</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team invite</b></td>
<td align='left'>プレイヤーをレルムに招待する</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team kick <player></b></td>
<td align='left'>レルムからメンバーを削除する</td>
<td align='left'>poseidon.island.expel</td>
</tr>
<tr>
<td align='left'><b>/poseidon team promote <player></b></td>
<td align='left'>レルムのプレイヤーのランクを1段階上げる</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team reject</b></td>
<td align='left'>招待を拒否する</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team setowner <player></b></td>
<td align='left'>レルムのオーナーをメンバーに移譲する</td>
<td align='left'>poseidon.island.team</td>
</tr>
<tr>
<td align='left'><b>/poseidon team trust <player></b></td>
<td align='left'>プレイヤーにレルムのトラストランクを付与する</td>
<td align='left'>poseidon.island.team.trust</td>
</tr>
<tr>
<td align='left'><b>/poseidon top</b></td>
<td align='left'>トップテンを表示する — Levelアドオンが必要</td>
<td align='left'>poseidon.island.level</td>
</tr>
<tr>
<td align='left'><b>/poseidon team uncoop <player></b></td>
<td align='left'>プレイヤーからコープランクを削除する</td>
<td align='left'>poseidon.island.team.coop</td>
</tr>
<tr>
<td align='left'><b>/poseidon team untrust <player></b></td>
<td align='left'>プレイヤーからトラストランクを削除する</td>
<td align='left'>poseidon.island.team.trust</td>
</tr>
<tr>
<td align='left'><b>/poseidon warp <name></b></td>
<td align='left'>プレイヤーのワープサインにワープする — Warpアドオンが必要</td>
<td align='left'>poseidon.island.warp</td>
</tr>
<tr>
<td align='left'><b>/poseidon warps</b></td>
<td align='left'>ワープパネルを開く — Warpアドオンが必要</td>
<td align='left'>poseidon.island.warp</td>
</tr>
</table>
<BR>
<h3>レルムの設定 (/po settings)</h3>
レルムには保護設定、一般設定、Poseidon設定を適用できます。これらの設定はそれぞれ、訪問者、コープ、トラスト、メンバー、サブオーナー、オーナーなどのプレイヤータイプへのアクセスを有効または無効にします。以下の表では各タイプに関連するアイコンを示しており、1回または複数回クリックすることで希望の設定を行えます。

<table width='100%' align='center'>
<tr>
<td align='left' valign='top'><b>設定</b></td>
<td align='left'><b>有効/無効にできるフラグ</b></td>
</tr>
<tr>
<td align='left' valign='top'>保護設定</td>
<td align='left'>動物に乗る、金床、鎧立て、ビーコン、ベッド、ブロック破壊、動物の繁殖、醸造台、バケツ、ボタン、コーラスフルーツ、溶岩収集、水収集、卵を投げる、エンチャントテーブル、エンドポータル、エンダーパール、経験値取得、火、火の消火、魚のすくい上げ、フロストウォーカー、かまど、門、動物を傷つける、モンスターを傷つける、村人を傷つける、アイテムドロップ、アイテム取得、ジュークボックスの使用、リード使用、レバー使用、レルムのロック、搾乳、マウントのインベントリ、名前タグ、ネザーポータル、音符ブロック、ブロック設置、感圧板、レッドストーンアイテム、刈り取り、スポーンエッグ、次のページ（看板）、TNTダメージ、作物の踏み荒らし、扉、カメの卵、ドアの使用、村人との取引、作業台、コンテナの使用、ディスペンサーの使用、ドロッパーの使用、ホッパーの使用、額縁の使用、ポーションを投げる、前のページ（看板）</td>
</tr>
<tr>
<td align='left' valign='top'>一般設定</td>
<td align='left'>動物のスポーン、エンドPVP、火の拡散、モンスターのスポーン、ネザーPVP、オーバーワールドPVP</td>
</tr>
<tr>
<td align='left' valign='top'>BSkyBlock設定</td>
<td align='left'>チェストダメージ、スーパーフラットをクリア、粗い土の耕作、クリーパーダメージ、クリーパーのグリーフィング、エンダーチェスト、エンダーマンのグリーフィング、入退場メッセージ、レルムのリスポーン、オフラインレッドストーン、ピストンプッシュ、モンスターの削除、黒曜石のすくい取り、落下羽テレポート、コマンドランク、無敵訪問者、モブをレルムに制限</td>
</tr>
</table>
