# Bank

**Bank** はアイランドメンバーがお金を共有できる**アイランド銀行**を提供します。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("Bank") }}

## はじめに

各アイランドには銀行口座があります。プレイヤーは通常の経済口座からアイランド口座にお金を預け入れたり、引き出したりすることができます。アイランドオーナーはチームメンバーのどのランクが口座にアクセスできるかを設定メニューから決定できます。プレイヤーが最も多い（または少ない）お金を持つアイランドを確認できる `baltop` コマンドがあります。

### 機能

* アイランドチームとしてお金を貯めたり使ったりする
* ゲーム内で最高残高を競う
* 口座の取引履歴を全て確認できる

### 必要要件
**Bank** はサーバーに Vault を使用した経済プラグインが導入されている必要があります。理想的には、ワールド間でお金が共有されないようにマルチワールド対応の経済プラグインを使用してください。

## コマンド
### プレイヤーコマンド

デフォルトのプレイヤーコマンドは `bank` で、config.yml で変更できます。例えば `/island bank` のように使用します。

* `bank deposit <amount>` - アイランド銀行にお金を預ける
* `bank withdraw <amount>` - アイランド銀行からお金を引き出す
* `bank balance` - アイランド銀行の残高を確認する
* `bank statement` - アイランド銀行口座の入出金明細を表示する

### 管理者コマンド

デフォルトの管理者コマンドは `bank` で、config.yml で変更できます。

管理者コマンドは魔法のようにお金を操作します。
* `bank give <player> <amount>` - プレイヤーのアイランド銀行にお金を預ける
* `bank take <player> <amount>` - プレイヤーのアイランド銀行からお金を引き出す
* `bank set <player> <amount>` - プレイヤーのアイランド銀行残高を指定金額に設定する
* `bank balance <player>` - プレイヤーのアイランド銀行残高を確認する
* `bank statement <player>` - プレイヤーのアイランド銀行口座の入出金明細を表示する

## プレースホルダー

プレースホルダーは[こちら](Placeholders)で確認できます。


## 設定

```
bank:
  # BentoBox GameModes that can use Bank
  game-modes:
  - BSkyBlock
  - AOneBlock
  - AcidIsland
  - SkyGrid
  - CaveBlock
  commands:
    # User command
    user: bank
    # Admin command
    admin: bank
  placeholders:
    # This is how many ranks will be registered with the placeholder API.
    # There are two placeholders per rank:
    # %Bank_[gamemode]_top_name_1% with island level: %Bank_[gamemode]_top_value_1%
    # [gamemode] is bskyblock, acidisland, etc.
    number-of-ranks: 10
```

## 権限

```
permissions:
  '[gamemode].bank.user':
    description: Player can use bank command
    default: true
  '[gamemode].bank.user.balance':
    description: Player can use bank balance command
    default: true
  '[gamemode].bank.user.deposit':
    description: Player can use the bank deposit command
    default: true
  '[gamemode].bank.user.withdraw':
    description: Player can use bank withdraw command
    default: true
  '[gamemode].bank.user.statement':
    description: Player can use the bank statement command
    default: true
  '[gamemode].bank.user.baltop':
    description: Player can use bank baltop command
    default: true
  '[gamemode].bank.admin':
    description: Player can use admin command
    default: op
  '[gamemode].bank.admin.balance':
    description: Player can use admin balance command
    default: op
  '[gamemode].bank.admin.give':
    description: Player can use the admin give command
    default: op
  '[gamemode].bank.admin.take':
    description: Player can use admin take command
    default: op
  '[gamemode].bank.admin.statement':
    description: Player can use the admin statement command
    default: op
  '[gamemode].bank.admin.set':
    description: Player can use admin set command
    default: op

```

## このアドオンが気に入りましたか？
[スポンサー](https://github.com/sponsors/tastybento)になることで、このようなアドオンをさらに増やし、改善することができます！

## 変更履歴

??? note "v1.10.1 の新機能"
    **リリース日:** 2026-06-21

    バグ修正リリース — ドロップイン交換、設定またはロケールの変更なし。

    - 🐛 **経済がアドオンによって提供される場合、Bankは自身を無効にしなくなります。** BentoBoxはアドオン有効化前の早期フック段階でVaultをフックします。その時点で経済プラグインがプロバイダを登録していない場合、その早期フックは破棄されます — つまり、経済がアドオンから来た場合（例：[InvSwitcher](../InvSwitcher/index.md)、その`onEnable()`で世界ごとのVault経済を登録）、Bankはプロバイダを見つけられず、*"Vault is required"*で自身をシャットダウンしました。Bankはこれで、Vaultフックを再試行してから諦め、`InvSwitcher`を`softdepend`として宣言するようになり、存在する場合は最初に有効化されるため、読み込み順序が確定的になります。

    [Release v1.10.1](https://github.com/BentoBoxWorld/Bank/releases/tag/1.10.1)

??? warning "v1.10.0 の新機能 — 破壊的変更（Java 21、BentoBox 3.14.0、MiniMessage）"
    **リリース日:** 2026-06-16

    モダナイズリリースです。BankはこれからJava 21、Paper 1.21.11、BentoBox 3.14.0を対象とし、ロケール全体がBentoBoxの**MiniMessage**カラーフォーマットに移行されました。

    - 🔡 **新しいプレースホルダー `%Bank_[gamemode]_latest_transaction%`** — プレイヤーの最新のアイランド銀行取引を `[Username] [TxType] $[Amount]` の形式で表示します（例: `tastybento Deposited $500.0`）。完全にローカライズされています。
    - 🔡 **完全な言語対応** — BankはBentoBoxの全ロケールセット（23言語）に対応しました。
    - 🔡 🔺 **MiniMessageロケール形式。** すべてのロケールファイルが、従来の `&`/`§` カラーコードからMiniMessageに変換されました。カスタマイズ済みのBankロケールファイルがある場合は、MiniMessage構文で書き直す必要があります — バックアップを取り、古いファイルを削除して再生成させてから、編集をやり直してください。
    - 🔺 **プラットフォームの近代化。** ビルドがJava 21 / Paper 1.21.11 / BentoBox 3.14.0にアップグレードされました。`plugin.yml` の `api-version` は1.21に、テストスイートはJUnit 5 + MockBukkitに移行されました。
    - 🐛 不正な形式のエントリに対する銀行取引履歴のパース処理を強化し、最新取引プレースホルダーのフォールバックテキストをローカライズしました。

    🔺 **アップデート方法:** このバージョンをインストールする**前に**、BentoBoxを3.14.0に更新し、サーバーがJava 21で動作していることを確認してください。カスタマイズ済みのロケールファイルは事前にバックアップしてください。

    [Release v1.10.0](https://github.com/BentoBoxWorld/Bank/releases/tag/1.10.0)

??? note "v1.9.1 の新機能"
    **リリース日:** 2026-03-28

    - **トップアイランド名プレースホルダー。** `%Bank_[gamemode]_top_island_<number>%` が各リーダーボード順位のアイランド名（オーナー名だけでなく）を返すようになりました。アイランド名はオーナー名・残高と共にキャッシュされます。
    - ⚙️ 利息複利計算のドキュメントと設定コメントを修正しました。`compound-periods-per-year` の計算に off-by-one エラーがあり、複利計算がわずかに不正確でした。古い jar を新しいものに置き換えて設定コメントを更新してください。

    [Release v1.9.1](https://github.com/BentoBoxWorld/Bank/releases/tag/1.9.1)

## 翻訳

{{ translations("Bank") }}
