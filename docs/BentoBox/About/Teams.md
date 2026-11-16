# チーム & ランク { #teams-ranks }

チームにより複数のプレイヤーが1つのアイランドを共有できます。すべてのアイランドには1人の**所有者**がいます。所有者は他のプレイヤーを**メンバー**として招待できます。一時的に手伝うだけのプレイヤーは、参加せずに**信頼**または**coop**にすることができます。

このページでは、チームがどのように機能するか、管理者として何をコンフィグできるか、プレイヤーから受ける一般的なリクエストにどう対処するかを説明しています。

!!! info "このページのコマンド"
    コマンドはBSkyBlock（`/island`、`/bsbadmin`）向けに表示されています。他のゲームモードは独自のコマンド名を使用します。例えばAOneBlockの`/ob`またはAcidIslandの`/acid`。パーミッションはゲームモードのプレフィックスで始まります。例えば`bskyblock.`または`aoneblock.`。

## チームがどのように機能するか { #how-teams-work }

- プレイヤーは`/island team invite <player>`で誰かを招待してチームを開始します。招待されたプレイヤーが承認すると、自分のアイランドを失い（デフォルト）、チームアイランドにテレポートされます。
- アイランド上のすべてのプレイヤーが**ランク**を持っています。ランクは彼らができることを決定します：ブロックを壊す、チェストを開く、プレイヤーを招待する、キックするなど。
- 所有者はアイランド設定メニュー（`/island settings`）でそれぞれのランクができることを決定します。[保護、フラグとランク](../Island-Protection,-Flags-&-Ranks.md)を参照。
- 所有者は1人です。所有者はアイランドを別のメンバーに譲ることができますが、その前に出発する必要があります。

### ランク { #the-ranks }

| ランク | 値 | 誰が持つか | チームサイズにカウント？ |
|---|---|---|---|
| 所有者 | 1000 | アイランドを所有するプレイヤー | はい |
| サブオーナー | 900 | 所有者が昇進させたメンバー | はい |
| メンバー | 500 | チーム招待を受け入れたプレイヤー | はい |
| 信頼 | 400 | `/island team trust`で信頼されたプレイヤー | いいえ（別の制限） |
| Coop | 200 | `/island team coop`でcoopされたプレイヤー | いいえ（別の制限） |
| ビジター | 0 | アイランド上の他のすべての人 | いいえ |
| バン済み | -1 | `/island ban`でバンされたプレイヤー | いいえ |

より高いランクは、より低いランクができることはすべてできます。`/bentobox rank add`でこれらの間に独自のランクを追加できます（[カスタムランク](#custom-ranks)を参照）。

### 信頼とCoopプレイヤー：参加せずに支援 { #trusted-and-coop-helping-without-joining }

信頼とCoopプレイヤーはチームメンバーにならずアイランドで作業できます。彼らは自分のアイランドを保ちます。

- **信頼**プレイヤーは`/island team untrust <player>`で削除されるまでランクを保ちます。
- **Coop**プレイヤーはアイランドにチームメンバーがオンラインの間だけランクを保ちます。最後のチームメンバーがログオフすると、そのアイランド上のすべてのCoopプレイヤーはランクを失います。ログオフするCoopプレイヤーもCoopランクを失います。

信頼とCoopはチーム招待と同じように機能します：相手プレイヤーは招待を受け取り、承認する必要があります。

## プレイヤーができること { #what-players-can-do }

プレイヤーは`/island team`でチームメニューを開きます。メニューからチームを見たり、プレイヤーを招待したり、コマンドを入力せずにランクを変更したりできます。同じアクションはコマンドとしても利用できます：

| コマンド | 機能 |
|---|---|
| `/island team` | チームメニューを開く |
| `/island team invite <player>` | オンラインプレイヤーをチームに招待 |
| `/island team accept` | 保留中の招待を承認（チーム、信頼、coop） |
| `/island team reject` | 保留中の招待を拒否 |
| `/island team leave` | チームを脱退。所有者は脱退できません。最初にアイランドを譲る必要があります |
| `/island team kick <player>` | チームからメンバーを削除。プレイヤーがオフラインのときに機能 |
| `/island team promote <player>` | メンバーを1ランク上げる（所有者にはなりません） |
| `/island team demote <player>` | メンバーを1ランク下げる（メンバー以下にはなりません） |
| `/island team setowner <player>` | 別のメンバーにアイランドを譲る。古い所有者はサブオーナーになる |
| `/island team trust <player>` | プレイヤーに信頼ランクを与える |
| `/island team untrust <player>` | 信頼ランクを削除 |
| `/island team coop <player>` | オンラインプレイヤーにCoopランクを与える |
| `/island team uncoop <player>` | Coopランクを削除 |

プレイヤーは**一度に1つだけ**保留中の招待を持つことができます。新しい招待は古いものを置き換えます。

Minecraft 26以降では、チーム招待を受け取ったプレイヤーは**承認/拒否**ダイアログを見るため、コマンドを入力する必要がありません。`kick`と`leave`などの機密コマンドもダイアログで確認を求めます。どちらもBentoBoxの`config.yml`（`island.dialogs.team-invites`と`island.dialogs.confirmations`）でオフにできます。

### メンバーがチームを管理させる { #letting-members-manage-the-team }

デフォルトでは所有者のみが招待、キック、昇進、降格、信頼、coopできます。所有者は設定メニューの**コマンドランク**ページから下位ランクにこれらのコマンドを使用させることができます。例えば、所有者はサブオーナーに招待とキックをさせることができます。

同じページはまた、`ban`、`unban`、`expel`、`lock`、`setname`、`sethome`などのアイランドコマンドもコントロールします。ホームコマンド（`sethome`、`renamehome`、`deletehome`）はメンバーにデフォルト設定されます。他は所有者にデフォルト。

プレイヤーは同じまたはそれより高いランクの誰かをキック、昇進、降格することはできません。

## チームの設定（管理者） { #setting-up-teams-admins }

### チームサイズ { #team-size }

チームサイズはゲームモードの`config.yml`で設定されます。**制限は所有者を含みます**。ですから`max-team-size: 4`は所有者プラス3メンバーを意味します。

```yaml
island:
  # 所有者 + メンバー
  max-team-size: 4
  # Coop と信頼プレイヤーの別制限
  max-coop-size: 4
  max-trusted-size: 4
```

### VIPまたはランクのより大きなチーム { #bigger-teams-for-vips-or-ranks }

**アイランド所有者**にサイズの終わりを持つパーミッションを与えてください：

| パーミッション | 効果 |
|---|---|
| `bskyblock.team.maxsize.<number>` | このプレイヤーが所有するアイランドのチームサイズ |
| `bskyblock.coop.maxsize.<number>` | Coop制限 |
| `bskyblock.trust.maxsize.<number>` | 信頼制限 |

例えばLuckPermsで：

```
/lp group vip permission set bskyblock.team.maxsize.8 true
```

パーミッションは所有者がオンラインのときチェックされ、アイランドは結果を記憶します。所有者のパーミッションのみが重要です。メンバーのパーミッションは無視されます。

パーミッション不要で1つのアイランドの制限を変更するには、`/bsbadmin team maxsize <player> <size>`を使用してください。

### プレイヤーが参加または離脱するときのアイテムとお金に何が起こるか { #what-happens-to-items-and-money-when-players-join-or-leave }

プレイヤーがチーム招待を受け入れると、通常**自分のアイランドが失われます**。承認する前に、警告され確認を求められます。

BentoBoxはプレイヤーがチームに参加または離脱するときに、プレイヤーのインベントリ、エンダーチェスト、お金、ヘルス、ハンガー、XPをクリアすることもできます。これはプレイヤーが1つのアイランドから別のアイランドにアイテムを運ぶのを止めます。ゲームモードの`config.yml`で設定してください：

```yaml
island:
  reset:
    # 離脱またはキックされるとプレイヤーのアイランドリセットの1つを使用
    leavers-lose-reset: false
    # キックされたプレイヤーはon-leave inventoryがtrueでもインベントリを保つ
    kicked-keep-inventory: false
    on-join:      # プレイヤーがチームに参加またはアイランドを作成したとき
      inventory: false
      ender-chest: false
      money: false
      exp: false
      health: true
      hunger: true
    on-leave:     # プレイヤーが離脱またはキックされたとき
      inventory: false
      ender-chest: false
      money: false
      # ... on-joinと同じオプション
```

!!! warning "ほとんどのサーバーに推奨"
    デフォルトはインベントリを保つので、テスト中にアイテムを失いません。ライブサーバーでは、`on-join`と`on-leave` `inventory`と`ender-chest`を`true`に、`leavers-lose-reset: true`に設定することを検討してください。そうでなければプレイヤーはインベントリを満たし、友達のアイランドに参加し、離脱、繰り返すことができます。

プレイヤーが参加または離脱したときにコマンドを実行することもできます。例えばチャレンジをリセットするかキットを与える：

```yaml
island:
  commands:
    on-join:
      - 'bsbadmin deaths set [name] 0'
    on-leave: []
```

これらはコマンドが`[SUDO]`で始まらない限りコンソールから実行されます。これはプレイヤーとして実行されます。

### 招待クールダウンと確認 { #invite-cooldowns-and-confirmations }

これらは**BentoBoxの** `config.yml`（`plugins/BentoBox/`）にあり、すべてのゲームモードに適用されます：

```yaml
island:
  cooldown:
    time:
      invite: 60   # キックされたまたは離脱したプレイヤーがそのアイランドに再び招待される前の分
      coop: 5      # Uncoopされたプレイヤーが再びcoopされる前の分
      trust: 5     # Untrustedされたプレイヤーが再び信頼される前の分
  confirmation:
    time: 10       # プレイヤーが確認するのに持つ秒
    commands:
      kick: true
      leave: true
    invites: false
```

招待クールダウンはプレイヤーが繰り返し参加、チャレンジを完了、離脱、再参加するのを止めます。

### チームをオフにする { #turning-teams-off }

一部のゲームモードはソロプレイ用に設計されています。ゲームモードはワールドのチームを無効にできます。その後、招待、キック、離脱、昇進、降格、setownerコマンドは実行を拒否しますが、信頼とcoopは引き続き機能するため、プレイヤーはまだ互いに手伝うことができます。既にチームを持つワールドのこれをオンにすると、`/bsbadmin team disbandall`を一度実行して既存のチームを破壊してください。

### 複数のアイランドを持つプレイヤー { #players-with-more-than-one-island }

複数のアイランド/プレイヤーを許可する場合（`concurrent-islands`が1より上）、`disallow-team-member-islands: true`はチームメンバーが自分のアイランドも作成するのを止めます。[複数のアイランド](../ConcurrentIslands.md)を参照。

## 一般的な管理者タスク { #common-admin-tasks }

| 目的 | 実行 |
|---|---|
| プレイヤーのチーム上にいるプレイヤーを見る | `/bsbadmin info <player>` |
| プレイヤーをチームに追加 | `/bsbadmin team add <owner> <player>` |
| プレイヤーをチームから削除 | `/bsbadmin team kick <player>` |
| 別のメンバーにアイランドを譲る（所有者がサーバーを離脱） | `/bsbadmin team setowner <player>` |
| チームを破壊 | `/bsbadmin team disband <owner>` |
| このワールドのすべてのチームを破壊 | `/bsbadmin team disbandall` |
| 1つのアイランドにより大きなチームを持たせる | `/bsbadmin team maxsize <player> <size>` |
| プレイヤーのランクにより大きなチームを持たせる | `bskyblock.team.maxsize.<number>`を与える |
| メンバーが他のプレイヤーを招待させる | 所有者が`/island settings` → コマンドランクを開く |
| メンバーがアイランド上でできることを変更 | 所有者が`/island settings`を開く。管理者がゲームモード設定でデフォルトを設定。[保護、フラグとランク](../Island-Protection,-Flags-&-Ranks.md)を参照 |

## カスタムランク { #custom-ranks }

`/bentobox rank`コマンドで組み込みの間にランクを追加できます：

```
/bentobox rank list
/bentobox rank add ranks.veteran 700
/bentobox rank remove ranks.veteran
```

## トラブルシューティング { #troubleshooting }

**「アイランドが満杯です」ですが、チームが小さく見えます。**
制限は所有者を含みます。`max-team-size`と、所有者が`team.maxsize`パーミッションを持っているかどうかを確認してください。新しいパーミッションが適用されるようにするには、所有者は一度ログインする必要があります。

**プレイヤーを招待できません。**
プレイヤーは既にチームに参加している可能性があります（最初に脱退する必要があります）、既に保留中の招待がある可能性があります。またはそのアイランドから脱退またはキックされた後の招待クールダウン中である可能性があります。

**Coopプレイヤーはランクを失い続けます。**
これはCoopの仕組みです。チームメンバーがオンラインでなくなると終了します。アクセスを保持する必要があるプレイヤーの場合は、信頼を代わりに使用してください。

**所有者は脱退したいです。**
所有者は脱退できません。`/island team setowner <player>`で別のメンバーに譲るか、管理者が`/bsbadmin team setowner`で実行する必要があります。

**プレイヤーはチームの参加/脱退を利用してアイテムまたは報酬を複製しています。**
`on-join`と`on-leave`リセットをオンにして、`leavers-lose-reset: true`を設定し、招待クールダウンを保つこと。

## 関連項目も参照 { #see-also }

- [保護、フラグとランク](../Island-Protection,-Flags-&-Ranks.md)：各ランクがアイランド上でできることを説明
- [アイランド](IslandManagement.md)：アイランドの作成、リセット、削除
- [複数のアイランド](../ConcurrentIslands.md)
- [メニューのカスタマイズ](../../Tutorials/generic/Customizable-GUI.md)：チームメニューは`plugins/BentoBox/panels/team_panel.yml`
