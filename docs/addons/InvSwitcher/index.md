# InvSwitcher

**InvSwitcher** は様々なワールド間でプレイヤーのインベントリとその他の要素を分離します。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("InvSwitcher") }}

以下の要素がワールドごとに切り替えられます:

* インベントリとアーマー
* 進捗
* 食料レベル
* 経験値
* 体力
* ゲームモード（クリエイティブ、サバイバルなど）
* 所持金（ワールドごとの経済、1.18.0 で追加）

## 使い方

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します。
2. サーバーを再起動します。
3. 完了！

## Config.yml

InvSwitcher には 2 つのメインセクションを持つ `config.yml` があります。

### ワールド

InvSwitcher が動作するゲームモードワールドの一覧です。ネザーとエンドのワールドは自動的に含まれます。

```yml
worlds:
- bskyblock_world
- acidisland_world
- oneblock_world
# ... etc.
```

### オプション

ワールドごと、また必要に応じてアイランドごとに切り替えるプレイヤーの要素を制御します。

```yml
options:
  inventory: true
  health: true
  food: true
  advancements: true
  gamemode: true       # game mode (Survival/Creative/etc.)
  experience: true
  ender-chest: true
  statistics: true
  money: true          # ワールドごとの所持金（1.18.0 で追加）。Vault が必要です。
  # Per-island inventory switching (added in 1.17.0)
  # The world-level option must also be true for the island option to take effect.
  islands:
    active: true       # Enable per-island switching overall
    inventory: true    # Give players a different inventory on each island they own
    health: false
    food: false
    advancements: false
    gamemode: false
    experience: false
    ender-chest: true
    statistics: false
    money: false       # アイランドごとの財布（1.18.0 で追加）。false の場合はワールドごとの所持金のみ。
```

`islands.active: true` に設定すると、複数のアイランドを所有するプレイヤーがゲームモードワールドごとだけでなく、アイランドごとに別々のインベントリ（およびその他の要素）を維持できます。

### 経済

1.18.0 で追加。`options.money` を有効にすると、InvSwitcher は自身を Vault の経済プロバイダーとして登録し、**切り替えられる各ワールドごとに別々の残高**を保持します。取引（ショップでの売買、`/pay`、ジョブなど）は、対象のプレイヤーがオフラインでも別のワールドにいても、その取引が属するワールドの残高に振り分けられます。InvSwitcher が管理しないワールドは既存の経済プラグイン（例：EssentialsX）に引き渡され、他に経済プラグインがなければ InvSwitcher がすべてのワールドを自分で処理します。

!!! warning "Vault が必要"
    ワールドごとの所持金には [Vault](https://www.spigotmc.org/resources/vault.34315/) プラグインが必要です。別途の経済プラグインは任意です — InvSwitcher が唯一の経済になることもできます。**Bank** アドオンを使用している場合、アイランドの財布もワールドごとになります。

`economy:` ブロックは `options.money` が `true` の場合にのみ使用されます:

```yml
economy:
  starting-balance: 0.0              # 管理対象ワールドに初めて入ったときに付与される残高（インポートされない場合）
  currency-name-singular: Dollar
  currency-name-plural: Dollars
  fractional-digits: 2               # 小数点以下の桁数
  import-existing-balances: true     # 各プレイヤーの既存残高を初回入場時に一度だけインポート
  delegate-unmanaged-worlds: true    # 管理外のワールドを以前の経済プラグインに引き渡す
  debug: false                       # すべての取引をコンソールに記録（冗長）
```

## コマンド

1.18.0 で追加。管理対象の各ゲームモードは、そのゲームモードのワールドに限定された独自の経済コマンドを取得します。そのため、どこにいても `/bsb balance` は BSkyBlock の残高を、`/ai balance` は AcidIsland の残高を表示します。

!!! tip
    `[player_command]` と `[admin_command]` は、使用しているゲームモードによって異なるコマンドです。

=== "プレイヤーコマンド"

    | コマンド | 説明 |
    |---|---|
    | `/[player_command] balance` | このワールドでの所持金残高を表示 |
    | `/[player_command] pay <プレイヤー> <金額>` | 他のプレイヤーに支払う |

=== "管理者コマンド"

    | コマンド | 説明 |
    |---|---|
    | `/[admin_command] eco give <プレイヤー> <金額>` | プレイヤーに所持金を与える |
    | `/[admin_command] eco take <プレイヤー> <金額>` | プレイヤーから所持金を取り上げる |
    | `/[admin_command] eco set <プレイヤー> <金額>` | プレイヤーの残高を設定 |
    | `/[admin_command] eco balance <プレイヤー>` | プレイヤーの残高を表示 |

## 機能
このアドオンはインストールされた各ゲームモードとそれに対応するワールドごとに、プレイヤーに別々のインベントリ、体力、食料レベル、進捗、経験値を与えます。プレイヤーが各ゲームモードを独立してプレイできるようにします。

## 例
**BSkyBlock** のインベントリ、体力、食料レベル、進捗、経験値は対応するワールド間でのみ共有されます:
- BSkyBlock_world
- BSkyBlock_world_nether
- BSkyBlock_world_the_end

**ご注意:**
- BentoBox のワールドだけに限定されません。現時点ではサーバー上の全てのワールドに適用されます。

## 変更履歴

??? note "v1.17.0 の新機能"
    **リリース日:** 2026-03-31

    - **アイランドごとのインベントリ切り替え。** 複数のアイランドを所有するプレイヤーが、同じゲームモード内でアイランドごとに別々のインベントリ（および必要に応じて体力、食料、経験値、エンダーチェスト、統計）を維持できるようになりました。`options.islands.active: true` で有効にし、各サブオプションを設定してください。ワールドレベルのオプションも `true` でなければ、対応するアイランドオプションは有効になりません。
    - ⚙️ `config.yml` に新しい `options.islands` セクションを追加。
    - バグ修正: 元のアイランドに戻る際にインベントリが失われていた問題。

    [Release v1.17.0](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.17.0)

??? note "v1.17.1 の新機能"
    **リリース日：** 2026-05-09

    - 🐛 **BentoBox ワールドから非 BentoBox ワールドへテレポートしたときにインベントリがクリアされる問題を修正。** 以前は、プレイヤーが BentoBox ゲームワールド（例：BSkyBlock）から非 BentoBox ワールド（例：デフォルトのオーバーワールドや第三者プラグインのワールド）へ離れるとき、それぞれの非 BentoBox ワールドが独自のキーでデータを保存していたため、「外側」のインベントリが失われることがありました。すべての非 BentoBox ワールドが単一のストレージキーを共有するようになり、プレイヤーのインベントリは常に正しく復元されます。古いワールドごとのキーで保存されたデータの自動マイグレーションを含みます。

    [Release v1.17.1](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.17.1)

??? warning "v1.18.0 の新機能 — BentoBox 3.17.0 が必要"
    **リリース日：** 2026-05-31

    - 🔺⚙️🔡 **ワールドごとの所持金。** InvSwitcher は、すでに切り替えているインベントリ・体力・経験値・統計に加えて、すべてのゲームワールドに独立した経済を与えられるようになりました。`options.money` を有効にすると、自身を Vault の経済プロバイダーとして登録し、プレイヤーがオフラインでも別のワールドにいても、各取引を正しいワールドの残高に振り分けます。
    - ⚙️ **新しい設定：** `options.money`、`options.islands.money`、および `economy:` ブロック（開始残高、通貨名、小数桁数、インポートの切り替え、委譲の切り替え、デバッグ）。既存の設定はそのまま動作し、新しいキーは安全なデフォルト値で追加されます。
    - 🔡 **新しいコマンドとプレースホルダー：** プレイヤー向けのゲームモードごとの `balance` と `pay`、管理者向けの `eco give/take/set/balance`、さらに `<gamemode>_invswitcher_balance` と `<gamemode>_invswitcher_balance_formatted` のプレースホルダー。BentoBox が同梱するすべての言語に翻訳されています。
    - 🐛 ワールド切り替え時に進捗が経験値を不正に増やさないようになりました。
    - 🐛 BentoBox のアイランドリセットが誤ったワールドのインベントリを消去しないようになりました — InvSwitcher は代わりに正しいワールドの*保存された*データを消去します。

    🔺 **BentoBox 3.17.0 が必要：** InvSwitcher は 3.17.0 で導入された BentoBox のプレイヤーリセットイベント（新しい所持金リセットイベントを含む）をリッスンするようになりました。それより古い BentoBox では読み込まれません。

    🔺 **経済の動作変更：** `options.money` を有効にすると、InvSwitcher がサーバーの Vault 経済プロバイダーになります。管理しないワールドは既存の経済（例：EssentialsX）に引き渡され、管理対象のワールドはワールドごとの独自残高を持ちます。所持金には Vault プラグインが必要です。

    [Release v1.18.0](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.18.0)

## プレースホルダー

{{ placeholders_source("InvSwitcher") }}

## 翻訳

{{ translations("InvSwitcher") }}
