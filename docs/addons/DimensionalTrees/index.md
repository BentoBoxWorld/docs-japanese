# DimensionalTrees

**DimensionalTrees** はネザーやエンドで育つ木がそのディメンションに合った木に変わるようにするアドオンです。

作成: [Awakened-Redstone](https://github.com/Awakened-Redstone)、メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("DimensionalTrees") }}

## 設定

最新の `config.yml` は[こちら](https://github.com/BentoBoxWorld/DimensionalTrees/blob/develop/src/main/resources/config.yml)で確認できます。

各マテリアルのスロット（`logs` / `leaves`）には、単一の文字列ではなく **`material: weight` の重み付きマップ** を指定できるようになりました。重みの合計がちょうど 100 なら、その値どおりの確率で適用されます。100 を超えると比例配分され、100 未満なら残りはそのまま AIR として残ります。どちらの場合も、起動時に警告ログが出力されます。

```yaml
nether:
  logs:
    gravel: 80
    netherrack: 20
  leaves:
    glowstone: 70
    soul_sand: 30
```

木が生えるときの解決順序は **per-tree の上書き → per-gamemode の上書き → 全体デフォルト** です。

??? note "nether.logs / end.logs"
    ネザー / エンドの木の原木に使う置き換え素材の全体設定です。単一のマテリアル名（旧形式）でも、重み付きマップでも指定できます。

??? note "nether.leaves / end.leaves"
    ネザー / エンドの木の葉に使う置き換え素材の全体設定です。

??? note "nether.per-tree / end.per-tree"
    樹種ごとの上書き（任意）。`oak`、`acacia`、`birch`、`jungle`、`spruce`、`dark_oak` それぞれに独自の `logs` / `leaves` マップを割り当てられます。値が空だったり無効だった場合は、自動的に全体デフォルトへフォールバックします。

??? note "nether.per-gamemode / end.per-gamemode"
    ゲームモードごとの上書き（任意）。BSkyBlock と CaveBlock など複数のゲームモードを同じサーバーで動かしている場合に便利です。ゲームモードの判定はイベント発生時に `IWM.getAddon(world)` で解決されます。

!!! tip "1.8.0 からの自動マイグレーション"
    既存の単一文字列の値（例: `logs: gravel`）は、1.9.0 の初回起動時に自動で重み付きマップ形式（`logs: {gravel: 100}`）へ変換されます。ログに変換完了のメッセージが出力されるだけで、手動編集は不要です。

## 変更履歴

??? note "v1.9.0の新機能 — 樹種別・ゲームモード別設定と重み付きマテリアル"
    **リリース日:** 2026-04-14

    - ⚙️ **樹種ごとの上書き** — ネザーとエンドで、6種類の樹種それぞれに独自の原木/葉の置き換えを設定できるようになりました（`per-tree.logs`、`per-tree.leaves`）。
    - ⚙️ **ゲームモードごとの上書き** — 複数の BentoBox ゲームモードを動かしているサーバーでは、ゲームモードごとに異なる置き換えを設定できるようになりました（`per-gamemode.logs`、`per-gamemode.leaves`）。
    - ⚙️ 🔺 **重み付きマルチマテリアルミックス** — すべてのマテリアルスロットで `material: weight` のマップを受け付けるようになり、複数のブロックタイプを混ぜられるようになりました。
    - ⚙️ **設定の自動マイグレーション** — 1.8.0 の単一文字列の値は、初回起動時に新しい重み付きマップ形式へ自動で変換されます。
    - Java 21、Paper 1.21.11、BentoBox 3.14.0 に更新。スタンドアロン動作に対応した Pladdon サポートも追加しました。
    - JUnit 5 + MockBukkit のテストスイートを追加。
    - 非推奨の `Material.matchMaterial` を最新の Registry API に置き換えました。
    - 🔡 エラーメッセージのロケールファイルを MiniMessage のカラーコードに対応させました。

    [リリース v1.9.0](https://github.com/BentoBoxWorld/DimensionalTrees/releases/tag/1.9.0)

## 翻訳

{{ translations("DimensionalTrees") }}
