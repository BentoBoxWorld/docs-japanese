プレースホルダーを使用すると、BentoBoxのアドオンやゲームモードのデータを他のプラグインで表示できます。逆も同様です！

## プレースホルダーの使い方

### 必要なプレースホルダーAPIをダウンロードする

BentoBoxはプレースホルダーに[**PlaceholderAPI**](https://www.spigotmc.org/resources/placeholderapi.6245/)を使用します。

### サーバーを起動するだけで準備完了！

どのプレースホルダーAPIを使用しているかにかかわらず、サーバーを起動するだけです。**ダウンロードする拡張機能はありません**：BentoBoxがすべてを処理します！

## チャットにプレースホルダーを表示するには？

**EssentialsChat**と**PlaceholderAPI**を使用している場合、チャットにプレースホルダーを表示するには**[ChatInjector](https://www.spigotmc.org/resources/chatinjector-1-13.81201/)**をインストールする**必要があります**。ただし、ChatInjectorは問題を引き起こす可能性があるという報告があることに注意してください。

代わりに、[**ChatControl**](https://www.spigotmc.org/resources/chatcontrol%E2%84%A2-the-ultimate-chat-plugin-500-000-downloads-1-2-5-1-14-4.271/)などのPlaceholderAPIをサポートする代替チャットプラグインの使用を推奨します。

## スコアボードにプレースホルダーを表示するには？

**PlaceholderAPI**をネイティブにサポートしていないが**MVdWPlaceholderAPI**（**Featherboard**など）をサポートするスコアボードプラグインを使用している場合でも、BentoBoxのプレースホルダーを使用できます。ただし、`{placeholderapi_[text]}`を追加し、*[text]*を*%*なしのプレースホルダーに置き換える必要があります。例：`{placeholderapi_bskyblock_island_name}`。

## 新しいプレースホルダーを提案するには？

BentoBoxや他のデフォルトゲームモードのプレースホルダーを追加すべきと思う場合は、[プレースホルダーリクエスト](https://github.com/BentoBoxWorld/BentoBox/issues/new?assignees=&labels=Status%3A+Pending%2C+Type%3A+Enhancement&template=placeholder_request.md&title=Placeholder%3A+)を提出してください。

## ゲームモードアドオンのデフォルトプレースホルダー

すべてのゲームモードアドオンには、自動的に登録されるデフォルトプレースホルダーがいくつかあります。

**利用可能なデフォルトプレースホルダー**

| プレースホルダー | 説明 | バージョン |
|-------------------------------------------------------|--------------------------------------------------------------------------------|-----------|
| %[gamemode]_world_friendly_name% | ゲームモードのワールド名 | 1.4.0 |
| %[gamemode]_world_islands% | このゲームモードのワールド内のアイランド数 | 1.5.0 |
| %[gamemode]_island_distance% | ゲームモードのワールドのアイランド中心間距離の半分 | 1.4.0 |
| %[gamemode]_island_distance_diameter% | ゲームモードのワールドのアイランド間距離 | 1.5.0 |
| %[gamemode]_island_protection_range% | アイランドの保護範囲の半径 | 1.4.0 |
| %[gamemode]_island_protection_range_diameter% | アイランドの保護範囲の直径 | 1.5.0 |
| %[gamemode]_island_owner% | アイランドオーナーの名前 | 1.4.0 |
| %[gamemode]_island_creation_date% | アイランドの作成日 | 1.4.0 |
| %[gamemode]_island_name% | アイランドの名前 | 1.4.0 |
| %[gamemode]_island_center% | アイランド中心の座標 | 1.5.0 |
| %[gamemode]_island_center_x% | アイランド中心のX座標 | 1.5.0 |
| %[gamemode]_island_center_y% | アイランド中心のY座標 | 1.5.0 |
| %[gamemode]_island_center_z% | アイランド中心のZ座標 | 1.5.0 |
| %[gamemode]_island_members_max% | アイランドのメンバーの最大数 | 1.5.0 |
| %[gamemode]_island_members_count% | アイランドのメンバー、サブオーナー、オーナーの数 | 1.5.0 |
| %[gamemode]_island_members_list% | アイランドでMEMBER以上のプレイヤー名のカンマ区切りリスト | 1.13.0 |
| %[gamemode]_island_coop_list% | アイランドでCOOPのプレイヤー名のカンマ区切りリスト | 2.4.2 |
| %[gamemode]_island_trusted_list% | アイランドでTRUSTEDのプレイヤー名のカンマ区切りリスト | 2.4.2 |
| %[gamemode]_island_trustees_count% | アイランドにトラストされているプレイヤー数 | 1.5.0 |
| %[gamemode]_island_coops_count% | アイランドにコープされているプレイヤー数 | 1.5.0 |
| %[gamemode]_island_visitors_count% | 現在アイランドを訪問しているプレイヤー数 | 1.5.0 |
| %[gamemode]_island_bans_count% | アイランドからバンされているプレイヤー数 | 1.5.0 |
| %[gamemode]_island_uuid% | データベースで使用されるアイランドの一意のID | 1.15.4 |
| %[gamemode]_visited_island_protection_range% | プレイヤーが立っているアイランドの保護範囲の半径 | 1.5.2 |
| %[gamemode]_visited_island_protection_range_diameter% | プレイヤーが立っているアイランドの保護範囲の直径 | 1.5.2 |
| %[gamemode]_visited_island_owner% | プレイヤーが立っているアイランドのオーナー名 | 1.5.2 |
| %[gamemode]_visited_island_creation_date% | プレイヤーが立っているアイランドの作成日 | 1.5.2 |
| %[gamemode]_visited_island_name% | プレイヤーが立っているアイランドの名前 | 1.5.2 |
| %[gamemode]_visited_island_center% | プレイヤーが立っているアイランドの中心座標 | 1.5.2 |
| %[gamemode]_visited_island_center_x% | プレイヤーが立っているアイランドの中心X座標 | 1.5.2 |
| %[gamemode]_visited_island_center_y% | プレイヤーが立っているアイランドの中心Y座標 | 1.5.2 |
| %[gamemode]_visited_island_center_z% | プレイヤーが立っているアイランドの中心Z座標 | 1.5.2 |
| %[gamemode]_visited_island_members_max% | プレイヤーが立っているアイランドの最大メンバー数 | 1.5.2 |
| %[gamemode]_visited_island_members_count% | プレイヤーが立っているアイランドのメンバー、サブオーナー、オーナーの数 | 1.5.2 |
| %[gamemode]_visited_island_coop_list% | プレイヤーが立っているアイランドでCOOPのプレイヤー名のカンマ区切りリスト | 2.4.2 |
| %[gamemode]_visited_island_trusted_list% | プレイヤーが立っているアイランドでTRUSTEDのプレイヤー名のカンマ区切りリスト | 2.4.2 |
| %[gamemode]_visited_island_members_list% | プレイヤーが立っているアイランドでMEMBER以上のプレイヤー名のカンマ区切りリスト | 1.13.0 |
| %[gamemode]_visited_island_trustees_count% | プレイヤーが立っているアイランドにトラストされているプレイヤー数 | 1.5.2 |
| %[gamemode]_visited_island_coops_count% | プレイヤーが立っているアイランドにコープされているプレイヤー数 | 1.5.2 |
| %[gamemode]_visited_island_visitors_count% | プレイヤーが立っているアイランドを現在訪問しているプレイヤー数 | 1.5.2 |
| %[gamemode]_visited_island_bans_count% | プレイヤーが立っているアイランドからバンされているプレイヤー数 | 1.5.2 |
| %[gamemode]_visited_island_uuid% | プレイヤーが立っているアイランドの一意のID | 1.15.4 |
| %[gamemode]_has_island% | プレイヤーがアイランドを持っているかどうか | 1.5.0 |
| %[gamemode]_rank% | プレイヤーが自分のアイランドで持つランク | 1.5.0 |
| %[gamemode]_resets% | プレイヤーがアイランドをリセットした回数 | 1.5.0 |
| %[gamemode]_resets_left% | プレイヤーがアイランドをリセットできる残り回数 | 1.5.0 |
| %[gamemode]_deaths% | プレイヤーが死んだ回数 | 1.12.0 |
| %[gamemode]_on_island% | プレイヤーが自分が属するアイランドにいるかどうか | 1.13.0 |

### フラグプレースホルダー

ゲームモードに登録されたすべての保護フラグと設定フラグはプレースホルダーも公開します。プレースホルダー名は`flag_`の後に小文字のフラグIDが続きます：

| プレースホルダー | 説明 |
|-------------|-------------|
| %[gamemode]_flag_[flag_id]% | 値はフラグタイプによって異なります：**PROTECTION** → 許可される最低ランクの翻訳名（例：`Member`）；**SETTING** → `true`または`false`；**WORLD_SETTING** → `true`または`false` |

**例：**

```
%bskyblock_flag_pvp_overworld%   → "false"
%bskyblock_flag_break_blocks%    → "Member"
%bskyblock_flag_ender_chest%     → "true"
```

アドオン定義のフラグは実行時にフラグが追加されると自動的に登録されます。

## 関連情報
ゲームモードとアドオンも独自のプレースホルダーを持てます。ニーズにより適したであろう以下のページも確認することを強くお勧めします。

- ゲームモード
    - [AcidIsland](../../gamemodes/AcidIsland/Placeholders)
    - [AOneBlock](../../gamemodes/AOneBlock/Placeholders)
    - [Boxed](../../gamemodes/Boxed/Placeholders)
    - [BSkyBlock](../../gamemodes/BSkyBlock/Placeholders)
    - [CaveBlock](../../gamemodes/CaveBlock/Placeholders)
    - [SkyGrid](../../gamemodes/SkyGrid/Placeholders)
- アドオン
    - [Bank](../../addons/Bank/#placeholders)
    - [Challenges](../../addons/Challenges/#placeholders)
    - [Level](../../addons/Level/#placeholders)
    - [Likes](../../addons/Likes/#placeholders)
    - [Limits](../../addons/Limits/#placeholders)
    - [MagicCobblestoneGenerator](../../addons/MagicCobblestoneGenerator/#placeholders)
