# プレースホルダー { #placeholders }

プレースホルダーは他のプラグインがBentoBox情報を表示することができます：スコアボードのプレイヤーのアイランド名またはレベル、チャットのランク、ホログラムのアイランド数など。

## セットアップ { #setting-up }

1. [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/)をインストールします。
2. サーバーを再起動します。

以上です。BentoBoxはプレースホルダーをPlaceholderAPIに登録します。`/papi ecloud`でダウンロードする拡張はありません。

その後、PlaceholderAPIをサポートする任意のプラグイン（スコアボード、タブリスト、チャット、ホログラムなど）でプレースホルダーを使用します。

## プレースホルダーの名前付け方法 { #how-placeholders-are-named }

各ゲームモードはすべてのプレースホルダーの独自のコピーを登録し、ゲームモードの名前の小文字で始まります：

```
%bskyblock_island_name%
%aoneblock_island_members_count%
%acidisland_rank%
```

以下の表はこのプレフィックスを`[gamemode]`として記述します。アドオンのプレースホルダーはアドオン名とゲームモードで始まります。例えば`%Level_bskyblock_island_level%`です。各[アドオンのページ](../addons/Level/index.md#placeholders)にリストされています。

2種類があります：

- `[gamemode]_island_...`は**プレイヤー自身のアイランド**についてです。
- `[gamemode]_visited_island_...`は**プレイヤーが立っているアイランド**についてです。別の誰かのものかもしれません。

## ゲーム内でプレースホルダーを見つける { #finding-a-placeholder-in-game }

| コマンド | 機能 |
|---|---|
| `/bentobox placeholders` | BentoBoxとアドオンから各プレースホルダーを検索できるメニューを開きます。個別のプレースホルダーのオン/オフもできます |
| `/bentobox dump-placeholders` | すべての登録されたプレースホルダーを`plugins/BentoBox/placeholder-dump.md`に書き込む |
| `/papi parse me %bskyblock_island_name%` | プレースホルダーがあなたに対して返すもの（PlaceholderAPIコマンド） |

## BentoBoxプレースホルダー { #bentobox-placeholders }

これらはすべてのゲームモードに登録されます。

{{ placeholders_source("BentoBox") }}

### 番号付きプレースホルダー { #numbered-placeholders }

`_<n>`で終わるプレースホルダーは各番号に対して登録されます：

- `island_member_name_<n>`、`island_member_rank_<n>`、`island_banned_name_<n>`（およびそれらの`visited_island_`バージョン）は1～50です。チームまたはバンリストを1行ずつリストするため。例えば`%bskyblock_island_member_name_1%`。
- `island_name_<n>`と`island_memberlist_<n>`はプレイヤーが所有できるアイランド数（`concurrent-islands`）までです。[複数アイランド](ConcurrentIslands.md)を参照してください。

### フラグプレースホルダー { #flag-placeholders }

保護フラグ、アイランド設定、ワールド設定のすべてがプレースホルダーを持ちます：`flag_`の後にフラグのIDが小文字で続きます。

| フラグタイプ | 返すもの |
|---|---|
| 保護フラグ | プレイヤーのアイランドで許可されている最低ランク。例えば`Member` |
| アイランド設定 | プレイヤーのアイランド用の`true`または`false` |
| ワールド設定 | ゲームモードのワールド用の`true`または`false` |

```
%bskyblock_flag_break_blocks%    → Member
%bskyblock_flag_pvp_overworld%   → false
```

フラグIDは[フラグ](Flags.md)にリストされています。アドオンで追加されたフラグは自動的にプレースホルダーを取得します。

## ゲームモードページ { #game-mode-pages }

各ゲームモードのページは、これらのプレースホルダーとゲームモード独自のプレースホルダーを独自のプレフィックスが埋め込まれてリストします：

[AcidIsland](../gamemodes/AcidIsland/Placeholders.md) · [AOneBlock](../gamemodes/AOneBlock/Placeholders.md) · [Boxed](../gamemodes/Boxed/Placeholders.md) · [BSkyBlock](../gamemodes/BSkyBlock/Placeholders.md) · [CaveBlock](../gamemodes/CaveBlock/Placeholders.md) · [ChunkBlock](../gamemodes/ChunkBlock/Placeholders.md) · [Poseidon](../gamemodes/Poseidon/Placeholders.md) · [SkyGrid](../gamemodes/SkyGrid/Placeholders.md) · [TradeWinds](../gamemodes/TradeWinds/Placeholders.md)

## トラブルシューティング { #troubleshooting }

**プレースホルダーがテキストとして表示されます（`%bskyblock_island_name%`）。**
PlaceholderAPIがインストールされており、プラグインがそれを表示しているのがPlaceholderAPIをサポートしており、プレースホルダーが`/bentobox placeholders`でオフになっていないか確認します。一部のチャットプラグインはプレースホルダーを解析するための追加の設定またはプラグインが必要です。`/papi parse me <placeholder>`でテストしてください。

**プレースホルダーが空です。**
プレイヤーはそのゲームモードにアイランドを持っていません。または`visited_island_`プレースホルダーの場合、アイランドに立っていません。

**アドオンのプレースホルダーが存在しません。**
アドオンがインストールされており、そのゲームモードに対して有効になっているか確認します。アドオンプレースホルダーはアドオン名、その後ゲームモード名で始まります：`%Level_bskyblock_island_level%`。また、`/bentobox placeholders`でオフになっていないか確認してください。

**存在しないプレースホルダーが必要です。**
GitHubで[リクエスト](https://github.com/BentoBoxWorld/BentoBox/issues/new?labels=Status%3A+Pending%2C+Type%3A+Enhancement&template=placeholder_request.md&title=Placeholder%3A+)してください。
