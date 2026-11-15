# 管理ツール { #admin-tools }

BentoBoxはアイランドを調査し、何かがブロックされた理由を見つけ、サーバーを管理するためのゲーム内ツールを持っており、データファイルを手動で編集する必要はほぼありません。このページでは最も使用するツールをカバーしています。すべてのコマンドは[コマンドリファレンス](../Commands.md)にあります。

!!! info "このページのコマンド"
    ゲームモード管理者コマンドは`/bsbadmin`（BSkyBlock）で表示されます。代わりに、あなたのゲームモードの管理者コマンドを使用してください。例えば`/oba`（AOneBlock）、`/acid`（AcidIsland）、`/cbadmin`（CaveBlock）。デフォルトではオペレーターのみです。スタッフに与える場合は[パーミッションと VIP パーク](../Permissions-Guide.md#staff-permissions)を参照してください。

## アイランドを調べる { #look-up-an-island }

| 目的 | コマンド |
|---|---|
| プレイヤーのアイランドについてすべてを見る：所有者、チーム、範囲、ホーム、リセット、デス、バン | `/bsbadmin info <player>` |
| 立っているアイランドを見る | `/bsbadmin info` |
| プレイヤーが持つ複数のアイランドのうち1つを見る | `/bsbadmin info <player> <island name>` |
| プレイヤーのアイランドに移動（またはそのネザー/エンドアイランド） | `/bsbadmin tp <player>`、`tpnether`、`tpend` |
| プレイヤーを別のプレイヤーのアイランドに送る | `/bsbadmin tpuser <player> <island owner>` |
| プレイヤーのアイランド内での役職を見る | `/bsbadmin getrank <player>` |
| ゲーム内でアイランドの保護エリアを表示 | `/bsbadmin range display` |

## 何かがブロックされた理由を見つける { #find-out-why-something-is-blocked }

プレイヤーが何かができないと言ったとき（またはできるはずがないことができるとき）は、**why**ツールをオンにします：

```
/bsbadmin why <player>
```

その後、プレイヤーに再度試すよう指示してください。コンソールはそのプレイヤーのすべての保護チェックをログに記録します：何を試したか、どこで、許可されたか、そしてどのフラグまたはランクが決定したか。同じコマンドを再度実行してオフにします。プレイヤーはオンラインである必要があります。

ほとんどの問題は、予想と異なるランクに対して設定されたフラグ、またはプレイヤーが他のプレイヤーのアイランドにいることであると判明します。[保護、フラグとランク](../Island-Protection,-Flags-&-Ranks.md)を参照してください。

## 通常のプレイヤーとして行動する { #act-as-a-normal-player }

バイパスパーミッションを持つオペレーターとモデレーターはアイランド保護を無視するため、テストが混乱します。**`/bsbadmin switch`** はバイパスをオフにしてあなたを通常プレイヤーのように保護します。もう一度実行してオンに戻してください。オペレーターステータス自体は影響を受けません。[保護をバイパスする](../Island-Protection,-Flags-&-Ranks.md#bypass-the-protection)を参照してください。

## アイランドを修正する { #fix-an-island }

| 目的 | コマンド | 詳細 |
|---|---|---|
| プレイヤーのアイランド上での役職を変更 | `/bsbadmin setrank <player> <rank>` | [チームとランク](Teams.md) |
| チームメンバーの追加または削除、所有者の変更 | `/bsbadmin team add`、`team kick`、`team setowner` | [チームとランク](Teams.md#common-admin-tasks) |
| アイランドの設定を変更 | `/bsbadmin settings <player>` | [保護、フラグとランク](../Island-Protection,-Flags-&-Ranks.md) |
| アイランドを大きくまたは小さくする | `/bsbadmin range set <player> <range>` | [アイランド](IslandManagement.md#island-size-protection-range) |
| プレイヤーのホームをリセットするか、ホームを削除 | `/bsbadmin resethome <player>`、`deletehomes <player>` | [アイランド](IslandManagement.md#homes) |
| アイランドの名前をクリア | その上に立ち、`/bsbadmin resetname` | [アイランド](IslandManagement.md#island-names) |
| プレイヤーにリセットを戻す | `/bsbadmin resets reset <player>` | [アイランド](IslandManagement.md#resetting-islands) |
| アイランドの削除、削除解除、または再割り当て | `/bsbadmin delete`、`undelete`、`register` | [アイランド](IslandManagement.md#deleting-islands) |
| アイランドの保護エリアの中心を移動 | その場所に立ち、`/bsbadmin setprotectionlocation` | |
| すべてのアイランドの設定を設定ファイルのデフォルトにリセット | `/bsbadmin resetflags` | |
| アイランドをゲームモードのスポーンにする | その上に立ち、`/bsbadmin setspawn` | |

## ワールド設定 { #world-settings }

**`/bsbadmin settings`** はゲームモードのワールドの管理者設定メニューを開きます：ワールド設定（クリーパーダメージやビジター持ち込み可能など）、アイランド外の保護ルール、新しいアイランドのデフォルト、そしてプレイヤーが見ることができるアイランド設定。[管理者設定パネル](../Island-Protection,-Flags-&-Ranks.md#admin-settings-panel)を参照してください。

## BentoBox の管理 { #managing-bentobox }

| コマンド | 機能 |
|---|---|
| `/bentobox version` | BentoBox、ゲームモード、アドオンのバージョン、サーバーバージョン、データベース。**ヘルプを求める際またはバグを報告する際にこれを含めてください。** |
| `/bentobox manage` | 管理パネル：ゲームモード、アドオン、フック（BentoBoxが連携する他のプラグイン）のタブ、プラスアドオンカタログ |
| `/bentobox catalog` | ダウンロード可能なゲームモードとアドオンを閲覧 |
| `/bentobox reload` | BentoBoxとアドオンの設定、言語ファイル、メニューテンプレートをリロード |
| `/bsbadmin reload` | 1つのゲームモードの設定をリロード |
| `/bentobox perms` | すべてのコマンドパーミッションとそのデフォルトを出力（コンソール） |
| `/bentobox locale` | 言語ファイルで翻訳が不足していないか確認 |
| `/bentobox placeholders` | プレースホルダーを閲覧したり、オンやオフに設定したり。[プレースホルダー](../Placeholders.md)を参照 |

ワールド生成や`distance-between-islands`のような一部の設定は完全な再起動後にのみ効果があります。

## データベース { #database }

BentoBoxはアイランドとプレイヤーをBentoBoxの`config.yml`で設定されたデータベースに保存します。デフォルトはBentoBoxフォルダ内の**JSON**ファイルで、セットアップが不要です。より大きなサーバーの場合、または複数のサーバーがデータを共有する場合は、**MySQL**（5.7以上）、**MariaDB**（10.2.3以上）、**PostgreSQL**（9.4以上）、**SQLite**（3.28以上）、または**MongoDB**（3.6以上）を使用できます。

データを失わずにデータベースタイプを変更するには、[データベースの変更](../Database-transition.md)を参照してください。常にバックアップを取ってください。

## 関連項目も参照 { #see-also }

- [コマンドリファレンス](../Commands.md)
- [パーミッションと VIP パーク](../Permissions-Guide.md)
- [BentoBox リリースノート](../Release-Notes.md)
