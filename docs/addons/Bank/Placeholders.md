# はじめに

[プレースホルダーページ](../../../BentoBox/Placeholders)をお読みください。

# プレースホルダー

## 共通プレースホルダー

これらのプレースホルダーは現在利用可能な全ゲームモード（[BSkyBlock](../../../gamemodes/BSkyBlock/Placeholders)、[AcidIsland](../../../gamemodes/AcidIsland/Placeholders)、[CaveBlock](../../../gamemodes/CaveBlock/Placeholders)、[SkyGrid](../../../gamemodes/SkyGrid/Placeholders)、[AOneBlock](../../../gamemodes/AOneBlock/Placeholders)）で使用できます。

**利用可能なプレースホルダー一覧**

| プレースホルダー | 説明 | Bank バージョン |
|-------------------------------------------------------|--------------------------------------------------------------------------------|-----------|
| `%Bank_[gamemode]_island_balance%` | Vault でフォーマットされたプレイヤーのアイランド残高 | 1.1.0 |
| `%Bank_[gamemode]_visited_island_balance%` | Vault でフォーマットされたプレイヤーが現在いるアイランドの残高 | 1.1.0 |
| `%Bank_[gamemode]_island_balance_number%` | プレイヤーのアイランド残高（フォーマットなし・生の値） | 1.4.0 |
| `%Bank_[gamemode]_visited_island_balance_number%` | プレイヤーが現在いるアイランドの残高（フォーマットなし・生の値） | 1.4.0 |
| `%Bank_[gamemode]_island_balance_formatted%` | フォーマットされたプレイヤーのアイランド残高（例: 1.5M） | 1.1.1 |
| `%Bank_[gamemode]_visited_island_balance_formatted%` | フォーマットされたプレイヤーが現在いるアイランドの残高（例: 1.2k） | 1.1.0 |
| `%Bank_[gamemode]_top_value_#RANK#%` | リーダーボードの `#RANK#` 位アイランドの残高 | 1.1.0 |
| `%Bank_[gamemode]_top_name_#RANK#%` | リーダーボードの `#RANK#` 位アイランドのオーナー名 | 1.1.0 |
| `%Bank_[gamemode]_top_island_#RANK#%` | リーダーボードの `#RANK#` 位アイランドの名前 | 1.10.0 |
| `%Bank_[gamemode]_latest_transaction%` | プレイヤーの最新のアイランド銀行取引。`[Username] [TxType] $[Amount]` の形式で表示されます（例: `tastybento Deposited $500.0`） | 1.10.0 |

*注意*: `#RANK#` は 1 から Bank の config.yml の `number-of-ranks` 設定値までの数値です。

## 使用例
### BSkyBlock で上位 10 件を表示する
1. `%Bank_bskyblock_top_name_1% with island balance: %Bank_bskyblock_top_value_1%`
2. `%Bank_bskyblock_top_name_2% with island balance: %Bank_bskyblock_top_value_2%`
3. `%Bank_bskyblock_top_name_3% with island balance: %Bank_bskyblock_top_value_3%`
4. `%Bank_bskyblock_top_name_4% with island balance: %Bank_bskyblock_top_value_4%`
5. `%Bank_bskyblock_top_name_5% with island balance: %Bank_bskyblock_top_value_5%`
6. `%Bank_bskyblock_top_name_6% with island balance: %Bank_bskyblock_top_value_6%`
7. `%Bank_bskyblock_top_name_7% with island balance: %Bank_bskyblock_top_value_7%`
8. `%Bank_bskyblock_top_name_8% with island balance: %Bank_bskyblock_top_value_8%`
9. `%Bank_bskyblock_top_name_9% with island balance: %Bank_bskyblock_top_value_9%`
10. `%Bank_bskyblock_top_name_10% with island balance: %Bank_bskyblock_top_value_10%`
