# TwerkingForTrees

**TwerkingForTrees** はプレイヤーがトワークすることで木を速く育てることができます。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("TwerkingForTrees") }}

!!! info "互換性"
    **BentoBox 3.14.0** 以降、**Minecraft 1.21.3 – 1.21.4**、**Java 21** が必要です。

## インストール

1. アドオンの jar を BentoBox プラグインの addons フォルダに配置します
2. サーバーを再起動します
3. アイランドに木を植えます
4. トワーク、トワーク、トワーク...
5. 木が育ちます！

## 木

ほとんどの木は単一のトワークした苗木から育ちます。**ダークオーク**と**ペールオーク**は例外で、バニラの Minecraft と同様に 2x2 限定の巨木です。4 本の苗木を 2x2 のグリッドに並べてその隣でトワークする必要があります——単一の苗木では育ちません。

## 設定ファイル

```
# TwerkingForTrees configuration file.
#
# How many times the player must twerk before the tree start growing faster.
# If the player has not twerked enough, then the tree will not grow faster.
minimum-twerks: 4
# Hold to twerk. Accessibility feature. Instead of hitting the crouch button continuously, hold it down.
hold-for-twerk: false
# Use sprinting to grow trees instead of twerking.
sprint-to-grow: false
# Range to look for saplings when twerking. A range of 5 will look +/- 5 blocks in all directions around the player
# Making this too big will lag your server.
range: 5
sounds:
  # Toggle on/off the sounds.
  enabled: true
  twerk:
    # Sound that plays when the player twerked enough for the sapling to start growing faster.
    # Available sounds are the following:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: block.note_block.bass
    volume: 1.0
    pitch: 2.0
  growing-small-tree:
    # Sound that plays when a small tree (1x1) grows.
    # Available sounds are the following:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: block.bubble_column.upwards_ambient
    volume: 1.0
    pitch: 1.0
  growing-big-tree:
    # Sound that plays when a big tree (2x2) grows.
    # Available sounds are the following:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: block.bubble_column.upwards_ambient
    volume: 1.0
    pitch: 1.0
effects:
  # Toggle on/off the particle effects.
  enabled: true
  # Effect that plays each time the player twerks.
  # Available effects are the following:
  #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Effect.html
  twerk: MOBSPAWNER_FLAMES

```

## 翻訳

{{ translations("TwerkingForTrees") }}

??? warning "v1.6.0 の新機能 — 破壊的変更"
    **リリース日:** 2026-06-01

    大規模な近代化リリースです。詳細は [Release v1.6.0](https://github.com/BentoBoxWorld/TwerkingForTrees/releases/tag/1.6.0) をご覧ください。

    - 🔺 **BentoBox 3.14.0 が必要です**（Java 21、Paper 1.21.11、Minecraft 1.21.3 – 1.21.4）。それより古いサーバーでは読み込まれません。
    - 🌳 **ペールオーク**のサポートを追加しました（2x2 の巨木バリアントを含む）。ダークオークと同様、ペールオークは 2x2 限定の木で、単一の苗木では育ちません。
    - ⚙️ **サウンド設定フォーマットが変更されました。** config.yml のサウンド識別子は小文字のドット区切り形式（例: `block.note_block.bass`）を使用するようになりました。1.5.2 から config.yml を引き継いでいる場合は、トワークと木の成長のサウンドが機能し続けるように更新してください。
    - 新しい設定オプションを追加しました: `hold-for-twerk`（アクセシビリティ——連続して押す代わりにスニークを長押し）、`sprint-to-grow`（スプリントで木を育てる）、`range`（苗木の検索半径）。
    - 最新の Paper サーバーで依存関係を考慮した読み込みができるよう、`Pladdon` と `plugin.yml` を同梱しました。
    - ダークオークの苗木が単一の苗木から育つ問題を修正し、ブロック単位のアイランド境界の適用を復元し（原木と葉がアイランドの境界を越えて配置されなくなりました）、木の成長時のリソースリークを修正しました。
    - JUnit 5 / MockBukkit テストスイートを追加しました。
