# アイランド

すべてのBentoBoxゲームモードは、**アイランド**を中心に構成されています。1人のプレイヤーまたはチームに属する、ワールドの保護されたエリアです。（CaveBlockやBoxedなどのゲームモードでは、「アイランド」は洞窟またはボックスですが、仕組みは同じです。）このページでは、アイランドの作成、サイズ変更、リセット、削除、ホーム機能の動作、古いアイランドのクリーンアップについて説明します。

!!! info "このページのコマンド"
    コマンドはBSkyBlock（`/island`、`/bsbadmin`）用に表示されています。他のゲームモードは独自のコマンド名を使用します。例えばAOneBlockでは`/ob`です。権限はゲームモードのプレフィックスで始まります。例えば`bskyblock.`または`aoneblock.`です。プレイヤーが見るもの情報については、[プレイヤーガイド](../Player-Guide.md)を送ってください。

## オープン前：ワールドを計画する

ゲームモードの`config.yml`内の2つの設定は、**アイランドが存在した後は変更できません**。後で変更するとワールドとデータベースをワイプする必要があるため、プレイヤーが参加する前に決定してください。

```yaml
world:
  # 各アイランドのスペースの半径（ブロック単位）
  # アイランドの中心は2倍の距離だけ離れているため、400は中心を800ブロック離します
  distance-between-islands: 400
  # その空間のうち、所有者が最初に保護できる量（半径）
  # 後からアイランドごと、distance-between-islandsまで増やせます
  protection-range: 50
```

- `distance-between-islands`は、アイランドが成長できる**最大**の大きさです。VIPに付与したり、アップグレードとして販売する可能性がある最大サイズに設定してください。
- `protection-range`は、アイランドが**開始**する場所です。プレイヤーが建築できて保護できるエリアです。

その他の設定を確認してください：`island-height`（スターターアイランドのYレベル）、`max-islands`（ワールド内のアイランド数を上限設定、`0` = 上限なし）、`start-x`/`start-z`（同様に後で変更できません）。

## アイランド作成 { #creating-islands }

新しいプレイヤーが`/island`を実行します。BentoBoxは：

1. 複数のスターターアイランドがある場合は、**アイランド作成**メニューを表示します（ない場合はこれをスキップします）。
2. 次の空いているスポットを見つけ、スターターアイランドをペーストして、プレイヤーをそこにテレポートします。

何が起こるかを変更できます。

| 設定（ゲームモード`config.yml`） | デフォルト | 効果 |
|---|---|---|
| `new-player-action` | `create` | アイランドのないプレイヤーに対して`/island`が実行すること |
| `default-action` | `go` | アイランドのあるプレイヤーに対して`/island`が実行すること |
| `create-island-on-first-login.enable` | `false` | 新しいプレイヤーが参加するとき、自動的にアイランドを作成する |
| `teleport-player-to-island-when-created` | `true` | プレイヤーのアイランドが準備完了したときにテレポート |

**スターターアイランドの選択。** アイランド作成メニューの各選択肢はブループリントバンドルです。VIPアイランドなどの一部のプレイヤーのみが利用できるようにするには、`/bsbadmin blueprint`で権限が必要になるよう設定してから、`bskyblock.island.create.<bundle-name>`を付与します。[スターターアイランド（ブループリント）](../Blueprints.md)を参照してください。

## アイランドサイズ（保護範囲） { #island-size-protection-range }

保護範囲は、アイランドの中心の周りの半径で、所有者が制御します。プレイヤーは`/island info`で確認できます。管理者は`/bsbadmin range display`でゲーム内に表示できます。

一部のプレイヤーにより大きなアイランドを付与するには：

| 方法 | コマンドまたは権限 |
|---|---|
| ランクまたはVIPによって自動的に | 所有者に`bskyblock.island.range.<number>`を付与します。アイランドが作成されたときと所有者がログインしたときにチェックされます |
| 1つのアイランド、手動で | `/bsbadmin range set <player> <range>`、または`range add`/`range remove`で変更できます |
| デフォルトに戻す | `/bsbadmin range reset <player>` |

範囲は`distance-between-islands`を超えることはできません。[Upgrades](../../addons/Upgrades/index.md)などのアドオンも範囲をボーナスとして追加できます。アドオンボーナスを削除するには`/bsbadmin range removebonus <player>`を使用してください。

## ホーム { #homes }

プレイヤーは`/island`または`/island go`でアイランドにテレポートし、`/island sethome`でホームを移動します。

デフォルトでは、各アイランドは1つのホームを持ちます。複数の名前付きホームを許可するには：

```yaml
island:
  max-homes: 1    # ゲームモード config.yml
```

またはプレイヤー所有者に`bskyblock.island.maxhomes.<number>`を付与します。プレイヤーは`/island sethome <name>`、`/island go <name>`、`/island homes`を使用します。管理者は1つのアイランドに対して`/bsbadmin maxhomes <player> <number>`で変更できます。

`/island go <name>`は、大文字小文字が違っていても、または名前の最初の部分のみを入力しても、ホームを見つけます。Minecraft 26以降では、複数のホームを持つプレイヤーが`/island go`を入力すると、1つを選ぶポップアップが表示されます（BentoBoxの`config.yml`の`island.dialogs.go-picker`）。

**ネザーとエンドのホーム**（ゲームモードにネザーおよびエンドのアイランドワールドがある場合）は`island.sethome.nether.allow`と`island.sethome.the-end.allow`で制御されます。

| 管理者タスク | コマンド |
|---|---|
| プレイヤーのホームをデフォルトの場所に戻す | `/bsbadmin resethome <player>` |
| プレイヤーの名前付きホームをすべて削除 | `/bsbadmin deletehomes <player>` |
| プレイヤーのアイランドにアクセス | `/bsbadmin tp <player>` |

## アイランド名 { #island-names }

プレイヤーは`/island setname <name>`でアイランドに名前を付け、`/island resetname`で削除できます。名前はリーダーボード、ワープ、プレースホルダーに表示されます。

**BentoBox**の`config.yml`でルールを設定します。

```yaml
island:
  name:
    min-length: 4
    max-length: 20
    uniqueness: false   # true = ゲームモード内で2つのアイランドが同じ名前を共有できない
```

プレイヤーが名前に色を使用するには、`bskyblock.island.name.format`が必要です。管理者はアイランドに立って`/bsbadmin resetname`を実行すれば、不快な名前をクリアできます。

## アイランドのリセット { #resetting-islands }

`/island reset`はプレイヤーに新しいアイランドを与えます。**古いアイランドは削除されます。** リセットできるのは所有者のみです。チームメンバーはすべてアイランドから削除されます。

ゲームモードの`config.yml`で制御します。

```yaml
island:
  reset:
    reset-limit: -1   # -1 = 無制限、0 = リセットなし、2 = 2回のリセット（合計3つのアイランド）
```

BentoBoxの`config.yml`内：

```yaml
island:
  cooldown:
    time:
      reset: 300        # プレイヤーがリセット間で待つ必要がある秒数
  confirmation:
    commands:
      reset: true       # プレイヤーはリセット前に確認する必要があります
```

新しいアイランドから消される（インベントリ、エンダーチェスト、お金、XP）ものは、[チームとランク](Teams.md)で説明されている`on-join`オプションによって設定されます。

プレイヤーに追加のリセットを与えるには、彼らのリセットカウンターを変更します。

| コマンド | 効果 |
|---|---|
| `/bsbadmin resets reset <player>` | 0リセット使用済みに戻す |
| `/bsbadmin resets set <player> <number>` | 使用済みリセット数を設定 |
| `/bsbadmin resets add <player> <number>` | さらにリセットを使用済みとしてカウント |
| `/bsbadmin resets remove <player> <number>` | リセットを返す |

リセットを追加するための権限はありません。例えばランクアップまたはストアプラグインからこれらのコマンドを使用してください。

## アイランド削除 { #deleting-islands }

| 実行したいこと | コマンド |
|---|---|
| プレイヤーのアイランドを削除 | `/bsbadmin delete <player>` |
| 立っているアイランドを削除 | `/bsbadmin delete`（チームがまだある間は拒否されます） |
| クリーンアップ実行前に削除を取り消す | そのアイランドに立って`/bsbadmin undelete`を実行 |
| 削除されたまたは所有されていないアイランドをプレイヤーに譲渡 | そのアイランドに立って`/bsbadmin register <player>`を実行 |
| 所有者を削除するがブロックは保持 | `/bsbadmin unregister <owner>` |

アイランドを削除すると、所有者はすぐに削除されるため、プレイヤーは新しいアイランドを作成できます。**ブロック**は後で、リージョンファイルがクリーンアップされるときに削除されます（以下を参照）。それまでの間、`undelete`または`register`でアイランドを戻すことができます。

## 古いアイランドのクリーンアップ

削除されたおよびリセットされたアイランド、および戻ってこなかったプレイヤーのアイランドは、ディスク容量を使用します。BentoBoxは、アクティブなアイランドがなくなったら、ワールドの**リージョンファイル**（それぞれ512×512ブロック領域をカバー）を削除することで、アイランドを削除します。

**自動クリーンアップ**はBentoBoxの`config.yml`で設定されます。

```yaml
island:
  deletion:
    housekeeping:
      deleted-sweep:
        enabled: true         # 削除およびリセットされたアイランドをクリーンアップ
        interval-hours: 24
      age-sweep:
        enabled: false        # 誰も訪問していないアイランドもクリーンアップ
        interval-days: 30
        min-age-days: 60
  purge-level: 10             # このレベル以上のアイランドはパージしない（Levelが必要）
```

削除されたアイランドスイープは安全でデフォルトでオンです。年齢スイープはデフォルトではオフです。削除されなかった放棄されたアイランドを削除するためです。

**手動クリーンアップ：**

| コマンド | 内容 |
|---|---|
| `/bsbadmin purge <days>` | その日数間だれも触れていないリージョンファイル内のアイランドを削除 |
| `/bsbadmin purge deleted` | 削除されたアイランドをスイープを待つ代わりに今クリーンアップ |
| `/bsbadmin purge unowned` | 所有者のいないアイランドを削除可能としてマーク |
| `/bsbadmin purge protect` | アイランドに立ってこれを実行してすべてのパージから保護 |

パージはオンラインプレイヤーのいるアイランド、スポーンアイランド、保護されたアイランド、`purge-level`上のアイランドをスキップします。

!!! warning "最初にバックアップ"
    パージはディスクからリージョンファイルを削除し、取り消せません。最初のパージ前にワールドフォルダーをバックアップしてください。アクティブなアイランドと同じリージョンファイルを共有するアイランドは、そのリージョンが空になるまで残ります。

## プレイヤーごとの複数アイランド

プレイヤーがゲームモード内で複数のアイランドを所有できるようにすることができます。

```yaml
island:
  concurrent-islands: 1          # BentoBox config.yml：すべてのゲームモードのデフォルト

world:
  concurrent-islands: 1          # ゲームモード config.yml：0 = BentoBoxの値を使用
  disallow-team-member-islands: true
```

またはプレイヤーに`bskyblock.island.number.<number>`を付与してください。プレイヤーがアイランドを作成し、アイランド間を切り替える方法については、[複数のアイランド](../ConcurrentIslands.md)を参照してください。

## アイランドについて調べる

| コマンド | 表示内容 |
|---|---|
| `/island info` | 立っているアイランドの所有者、チーム、サイズ、位置 |
| `/bsbadmin info [player]` | 完全な詳細：所有者、メンバー、範囲、ホーム、リセット、死亡など。名前なしは立っているアイランド |
| `/bsbadmin why <player>` | プレイヤーが何かできるまたはできない理由のログ。[管理者ツール](AdminTools.md)を参照 |

## トラブルシューティング

**`distance-between-islands`を変更した後、サーバーが起動しません。**
アイランドが存在した後は変更できません。古い値に戻してください。

**より大きなアイランドまたはより多くのホームのVIP権限が適用されませんでした。**
権限はアイランド**所有者**に対してチェックされます。ログイン時に（範囲については作成時）。所有者にログアウトしてログインさせてください。

**プレイヤーにリセットが残っていません。**
`/bsbadmin resets reset <player>`。

**削除されたアイランドがまだここにあります。**
ブロックはリージョンファイルがクリーンアップされるとき、次の削除されたアイランドスイープ（デフォルト24時間）で、または`/bsbadmin purge deleted`を実行するとき削除されます。別のアクティブなアイランドがリージョンファイルを共有する場合、ブロックは残ります。

**ディスク使用量が増え続けています。**
`deleted-sweep`が有効になっていることを確認し、`/bsbadmin purge <days>`を検討するか、放棄されたアイランド用の年齢スイープを検討してください。

## 関連ページ

- [プレイヤーガイド](../Player-Guide.md)：プレイヤーが使用するコマンド
- [チームとランク](Teams.md)
- [保護、フラグ、ランク](../Island-Protection,-Flags-&-Ranks.md)
- [スターターアイランド（ブループリント）](../Blueprints.md)
- [複数のアイランド](../ConcurrentIslands.md)
- [管理者ツール](AdminTools.md)
