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
```

`islands.active: true` に設定すると、複数のアイランドを所有するプレイヤーがゲームモードワールドごとだけでなく、アイランドごとに別々のインベントリ（およびその他の要素）を維持できます。

## コマンド

コマンドはありません。

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

## 翻訳

{{ translations("InvSwitcher") }}
