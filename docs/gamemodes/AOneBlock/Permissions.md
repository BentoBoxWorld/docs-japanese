# AOneBlock パーミッション

| パーミッション | 有効化対象 | 説明 |
|-----------------------------------|------------|----------------------------------------------------|
| aoneblock.admin                   | op         | '/obadmin'コマンドの使用を許可する — 管理者コマンド    |
| aoneblock.admin.blueprint         | op         | '/obadmin blueprint'コマンドの使用を許可する — ブループリントを管理する |
| aoneblock.admin.clearresetall     | op         | すべてのプレイヤーの島リセット上限のクリアを許可する |
| aoneblock.admin.delete            | op         | プレイヤーを完全に削除できるようにする（島を含む） |
| aoneblock.admin.getrank           | op         | プレイヤーのランクを取得する                                |
| aoneblock.admin.noban             | op         | プレイヤーが島からBANされないようにする             |
| aoneblock.admin.noexpel           | op         | プレイヤーが島から追放されないようにする           |
| aoneblock.admin.purge             | op         | '/obadmin purge'コマンドの使用を許可する — 指定した日数以上放置された島をパージする |
| aoneblock.admin.range             | op         | '/obadmin range'コマンドの使用を許可する — 島の範囲を管理する |
| aoneblock.admin.register          | op         | 最も近い島を別のプレイヤーに登録できるようにする |
| aoneblock.admin.reload            | op         | config.ymlをリロードする                              |
| aoneblock.admin.setchest          | op         | 見ているチェストを指定したレアリティでフェーズに設定する |
| aoneblock.admin.setlanguage       | op         | すべてのプレイヤーの言語をリセットしてデフォルト言語を設定する |
| aoneblock.admin.setrank           | op         | プレイヤーのランクを設定する                                |
| aoneblock.admin.setrange          | op         | 島の保護範囲の設定を許可する          |
| aoneblock.admin.setspawn          | op         | スポーンツールの使用を許可する                          |
| aoneblock.admin.settingsreset     | op         | すべての島をデフォルトの保護設定にリセットする |
| aoneblock.admin.tp                | op         | 島へのテレポートを許可する                       |
| aoneblock.island.actionbar        | true       | '/ob actionbar'コマンドの使用を許可する — アクションバーの進捗表示を切り替える |
| aoneblock.island.bossbar          | true       | '/ob bossbar'コマンドの使用を許可する — ボスバーの進捗表示を切り替える |
| aoneblock.count                   | true       | aoneblockのcountコマンドの使用を許可する           |
| aoneblock.island                  | true       | '/ob'コマンドの使用を許可する — メインの島コマンド |
| aoneblock.phases                  | false      | '/ob phases'コマンドの使用を許可する — すべてのフェーズの一覧を表示する |
| aoneblock.island.ban              | true       | '/ob ban'または'/ob unban'コマンドの使用を許可する — BANされたプレイヤーを管理する |
| aoneblock.island.create           | true       | '/ob create'コマンドの使用を許可する — 島を作成する（オプションのブループリントを使用） |
| aoneblock.island.deletehome       | op         | '/ob deletehome'コマンドの使用を許可する — ホーム位置を削除する |
| aoneblock.island.expel            | true       | '/ob expel'コマンドの使用を許可する — 訪問者を追放する  |
| aoneblock.island.home             | true       | '/ob go'コマンドの使用を許可する — 島にテレポートする |
| aoneblock.island.homes            | op         | '/ob homes'コマンドの使用を許可する — ホームの一覧を表示する |
| aoneblock.island.info             | true       | '/ob info'コマンドの使用を許可する — 島の情報を表示する |
| aoneblock.island.language         | true       | '/ob language'コマンドの使用を許可する — 言語を選択する |
| aoneblock.island.lock             | true       | 設定で島のロックを許可する                  |
| aoneblock.island.name             | true       | '/ob setname'または'/ob resetname'コマンドの使用を許可する — 島の名前を設定する |
| aoneblock.island.near             | true       | '/ob near'コマンドの使用を許可する — 近くの島の名前を表示する |
| aoneblock.island.renamehome       | op         | '/ob renamehome'コマンドの使用を許可する — ホーム位置の名前を変更する |
| aoneblock.island.reset            | true       | '/ob reset'コマンドの使用を許可する — 島をリスタートする |
| aoneblock.island.setcount         | op         | '/ob setCount'コマンドの使用を許可する — ブロック数を完了値に設定する |
| aoneblock.island.sethome          | true       | '/ob sethome'コマンドの使用を許可する — ホームのテレポートポイントを設定する |
| aoneblock.island.settings         | true       | '/ob settings'コマンドの使用を許可する — 島の設定を表示する |
| aoneblock.island.spawn            | true       | '/ob spawn'コマンドの使用を許可する — スポーンが設定されている場合に島のスポーンにテレポートする |
| aoneblock.island.team             | true       | '/ob team'コマンドの使用を許可する — チームを管理する |
| aoneblock.island.team.accept      | true       | '/ob team accept'コマンドの使用を許可する — 招待を承諾する |
| aoneblock.island.team.coop        | true       | '/ob team coop'コマンドの使用を許可する — 他のプレイヤーと協力する |
| aoneblock.island.team.invite      | true       | '/ob team invite'コマンドの使用を許可する — プレイヤーを島に招待する |
| aoneblock.island.team.kick        | true       | '/ob team kick'コマンドの使用を許可する — チームからメンバーを削除する |
| aoneblock.island.team.leave       | true       | '/ob team leave'コマンドの使用を許可する — 島のチームを離れる |
| aoneblock.island.team.promote     | true       | '/ob team promote'コマンドの使用を許可する — チームメンバーを昇格させる |
| aoneblock.island.team.reject      | true       | '/ob team reject'コマンドの使用を許可する — 招待を拒否する |
| aoneblock.island.team.setowner    | true       | '/ob team setowner'コマンドの使用を許可する — 島のオーナーを移譲する |
| aoneblock.island.team.trust       | true       | '/ob team trust'コマンドの使用を許可する — 島のプレイヤーを信頼する |
| aoneblock.mod.bypassban           | op         | 島のBANを無視する                                |
| aoneblock.mod.bypassexpel         | op         | モデレーターが島からの追放を無視することを許可する         |
| aoneblock.mod.bypasslock          | op         | 島のロックを無視する                            |
| aoneblock.mod.bypasscooldowns     | op         | モデレーターがクールダウンを無視することを許可する                |
| aoneblock.mod.bypassdelays        | op         | モデレーターが遅延を無視することを許可する                   |
| aoneblock.mod.bypassprotect       | op         | モデレーターが島の保護を無視することを許可する        |
| aoneblock.mod.clearreset          | false      | 島のリセット上限のクリアを許可する               |
| aoneblock.mod.info                | op         | モデレーターがプレイヤーの情報を確認できるようにする               |
| aoneblock.mod.lock                | op         | 島のロック・アンロックを許可する                 |
| aoneblock.mod.switch              | op         | '/obadmin switch'コマンドの使用を許可する — 保護バイパスを切り替える |
| aoneblock.respawn-block           | true       | '/ob respawnBlock'コマンドの使用を許可する — 魔法のブロックを再スポーンさせる |
| aoneblock.settings.*              | true       | 島での設定の使用を許可する                    |
