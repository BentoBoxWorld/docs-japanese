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

??? note "v1.9.1 の新機能"
    **リリース日:** 2026-03-28

    - **トップアイランド名プレースホルダー。** `%Bank_[gamemode]_top_island_<number>%` が各リーダーボード順位のアイランド名（オーナー名だけでなく）を返すようになりました。アイランド名はオーナー名・残高と共にキャッシュされます。
    - ⚙️ 利息複利計算のドキュメントと設定コメントを修正しました。`compound-periods-per-year` の計算に off-by-one エラーがあり、複利計算がわずかに不正確でした。古い jar を新しいものに置き換えて設定コメントを更新してください。

    [Release v1.9.1](https://github.com/BentoBoxWorld/Bank/releases/tag/1.9.1)

## 翻訳

{{ translations("Bank") }}
