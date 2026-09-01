## 利用可能なロケール

{{ translations("BentoBox") }}

## MiniMessageフォーマット

BentoBoxはすべてのロケール文字列に[MiniMessage](https://docs.advntr.dev/minimessage/format.html)を使用します。つまり、MiniMessageタグを翻訳に使用してリッチテキストフォーマットを適用できます。例えば：

```yaml
my-message: "<green>Welcome to the island!</green>"
my-message: "<bold><red>Warning!</red></bold> Something happened."
my-message: "<gradient:gold:yellow>Island Name</gradient>"
```

レガシーの`§`または`&`カラーコードは後方互換性のためまだサポートされており、ロード時にMiniMessageフォーマットに自動変換されます。

## メッセージ配信タグ

ロケール文字列では特別なインラインタグを使用してプレイヤーへのメッセージの配信方法を制御できます。配信タグがない場合、メッセージはチャットで送信されます（デフォルトの動作）。

### `[actionbar]`

メッセージを**アクションバー**メッセージとして送信します（ホットバーの上に表示されるテキスト）。

```yaml
island-go: "[actionbar]Teleporting..."
```

### `[title]`と`[subtitle]`

メッセージを画面上の**タイトル**オーバーレイとして送信します。`[title]`は大きな見出しテキストを表示し、`[subtitle]`はその下に小さなテキストを表示します。`[subtitle]`はスタンドアロンの配信タイプではありません。`[title]`メッセージ内の区切り文字としてのみ機能します。`[title]`なしの場合は、チャットパスにフォールバックします。

```yaml
# タイトルとサブタイトル
island-go: "[title]Teleporting...[subtitle]Wait a second."
# タイトルのみ（空のタイトル、テキストはサブタイトルとして）
scooping: "[title][subtitle]You scooped the lava!"
```

### `[sound:name:volume:pitch]`

プレイヤーに**サウンド**を再生します。ボリュームとピッチはオプションです（デフォルト`1.0`）。Bukkit/Minecraftのサウンドリストのアンダースコア区切りのサウンド名を使用します（例：`entity_experience_orb_pickup`）。サウンドタグは任意の配信タイプタグと組み合わせられます。

```yaml
island-go: "[sound:entity_experience_orb_pickup:1:1][title]Teleporting...[subtitle]Wait a second."
```

!!! note
    非プレイヤー送信者（コンソールなど）は、アクションバーまたはタイトルタグが使用されている場合、チャット出力にフォールバックします。

## ガイドライン

* [https://download.bentobox.world/translate.html](https://download.bentobox.world/translate.html)でファイルの翻訳を可能にするツールが利用できます。これはブラウザでローカルに実行され、翻訳に役立てられます。新しいファイルはGitHubでPRとして提出してください。
* 翻訳者には特別なバッジが与えられます！
* 角括弧内のテキストはプレースホルダーなので翻訳しないでください。例：[name]は英語のまま残してください
* 翻訳をテストしてください — 提出前にできる限り確認してください
* 翻訳に広告、悪言、侮辱的なコメントを含めないでください。PRを承認前に確認します。
* 翻訳についての質問はDiscordで自由にどうぞ。

## ゲームモード

- [AcidIsland](../gamemodes/AcidIsland/index.md#translations)
- [AOneBlock](../gamemodes/AOneBlock/index.md#translations)
- [Boxed](../gamemodes/Boxed/index.md#translations)
- [BSkyBlock](../gamemodes/BSkyBlock/index.md#translations)
- [CaveBlock](../gamemodes/CaveBlock/index.md#translations)
- [ChunkBlock](../gamemodes/ChunkBlock/index.md#translations)
- [Poseidon](../gamemodes/Poseidon/index.md#translations)
- [SkyGrid](../gamemodes/SkyGrid/index.md#translations)
- [Stranger Realms](../gamemodes/StrangerRealms/index.md#translations)
- [TradeWinds](../gamemodes/TradeWinds/index.md#translations)

## アドオン

- [Bank](../addons/Bank/index.md#translations)
- [Biomes](../addons/Biomes/index.md#translations)
- [Border](../addons/Border/index.md#translations)
- [CauldronWitchery](../addons/CauldronWitchery/index.md#translations)
- [Challenges](../addons/Challenges/index.md#translations)
- [Chat](../addons/Chat/index.md#translations)
- [CheckMeOut](../addons/CheckMeOut/index.md#translations)
- [ControlPanel](../addons/ControlPanel/index.md#translations)
- [DimensionalTrees](../addons/DimensionalTrees/index.md#translations)
- [ExtraMobs](../addons/ExtraMobs/index.md#translations)
- [FarmersDance](../addons/FarmersDance/index.md#translations)
- [Greenhouses](../addons/Greenhouses/index.md#translations)
- [InvSwitcher](../addons/InvSwitcher/index.md#translations)
- [IslandFly](../addons/IslandFly/index.md#translations)
- [Level](../addons/Level/index.md#translations)
- [Likes](../addons/Likes/index.md#translations)
- [Limits](../addons/Limits/index.md#translations)
- [MagicCobblestoneGenerator](../addons/MagicCobblestoneGenerator/index.md#translations)
- [TopBlock](../addons/TopBlock/index.md#translations)
- [TwerkingForTrees](../addons/TwerkingForTrees/index.md#translations)
- [Upgrades](../addons/Upgrades/index.md#translations)
- [Visit](../addons/Visit/index.md#translations)
- [VoidPortals](../addons/VoidPortals/index.md#translations)
- [Warps](../addons/Warps/index.md#translations)
