# IslandStats

**IslandStats** はプレイヤー単位ではなく、アイランド単位で統計情報を保持します。モブの死亡から始まります：アイランド上で死亡したモブの種類ごとの数と、プレイヤーが倒したモブの数。すべてのゲームモードで動作します。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("IslandStats") }}

## インストール

1. IslandStats アドオンの jar を BentoBox プラグインの addons フォルダに配置します
2. サーバーを再起動します
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます
4. config.yml を希望通りに編集します
5. 変更を加えた場合はサーバーを再起動します

IslandStats には BentoBox 3.23.0 以降、Minecraft 26.2 以降、Java 25 が必要です。

!!! warning "カウントはアドオンがインストールされたときから始まります"
    IslandStats は古いプレイヤー統計を読み込まないため、すべてのアイランドはゼロから始まります。

## 統計情報

アドオンはモブの種類ごとに 2 つのカウントを保持します：

| 統計 | カウント |
|---|---|
| `KILL_ENTITY` | アイランド上のプレイヤーに倒されたモブ。バニラの `KILL_ENTITY` プレイヤー統計と同じ意味。 |
| `ENTITY_DEATH` | プレイヤー、モブ農場、落下ダメージ、溶岩など、あらゆる原因でアイランド上で死亡したモブ。 |

死亡は、それが発生した保護エリアを持つアイランドに対してカウントされます。プレイヤーとアーマースタンドはカウントされません。訪問者が倒したモブは、`count-visitor-kills` をオフにしない限り `KILL_ENTITY` にカウントされます。アイランド上のすべての死亡は常に `ENTITY_DEATH` にカウントされます。

アドオンがバニラのプレイヤー統計を使用しないのは、バニラ統計がプレイヤーの手柄になったキルしか記録せず、モブがどこにいたかも記録しないためです。それではモブ農場が漏れてしまい、モブが死亡したアイランドではなく、倒したプレイヤーのアイランドにカウントされてしまいます。

### 統計ダイアログ

`/[player_command] stats` はダイアログを開きます：

- サマリーページは各統計のトータルを表示し、ボタンを使用して開きます。
- 各統計ページはモブを最も多いものから最も少ないものにリストし、前へ、次へ、戻る、閉じるボタンがあります。
- モブ名は翻訳可能なテキストとして送信されるため、各プレイヤーは自分のクライアント言語で見ることができます。

### ストレージ

統計情報は BentoBox データベース API を通じて保存されるため、BentoBox が使用するように設定されたデータベースに保存されます。アイランドごとに 1 つのレコードがあります。JSON データベースでは `plugins/BentoBox/database/IslandStatsData/` に格納されます。カウントはメモリで行われ、変更されたアイランドはタイマー（`save-interval`）と サーバー停止時に保存されます。アイランドが削除またはリセットされるとその統計も削除されます。

## 設定

最新の `config.yml` は[こちら](https://github.com/BentoBoxWorld/IslandStats/blob/develop/src/main/resources/config.yml)にあります。

??? note "disabled-gamemodes"
    ここにリストされているゲームモードは IslandStats によって無視されます。

    デフォルト: `[]`

    ```yaml
    disabled-gamemodes:
      - BSkyBlock
    ```

??? note "count-visitor-kills"
    アイランドのメンバーではなく、訪問者や coop など、アイランド上で倒されたモブをカウントします。これは「プレイヤーによって倒されたモブ」の統計にのみ影響します。アイランド上のすべてのモブ死亡は常に「すべてのモブ死亡」の統計にカウントされます。

    デフォルト: `true`

??? note "ignored-entities"
    カウントされないエンティティタイプ。Bukkit エンティティタイプ名を使用してください。アーマースタンドはサーバーにとって生きているエンティティであるため、デフォルトで無視されます。

    デフォルト: `ARMOR_STAND`

??? note "save-interval"
    変更された統計がデータベースに書き込まれる頻度（分単位）。統計はメモリで数えられ、サーバー停止時に常に保存されます。最小 1。

    デフォルト: `5`

??? note "dialog.page-size"
    統計ダイアログの各ページに表示するモブ行の数。範囲 1～50。

    デフォルト: `15`

## コマンド

!!! tip
    `[player_command]` と `[admin_command]` はゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルには、これらの値を変更できるオプションが含まれています。
    例えば、BSkyBlock では、デフォルトの `[player_command]` は `island` で、デフォルトの `[admin_command]` は `bsbadmin` です。

=== "プレイヤーコマンド"
    - `/[player_command] stats` ：アイランドの統計ダイアログを開きます。

=== "管理者コマンド"
    - `/[admin_command] stats <player>` ：そのプレイヤーのアイランド統計を表示します。プレイヤーはダイアログを見て、コンソールはチャット行として統計を受け取ります。
    - `/[admin_command] stats <player> reset` ：確認を求めた後、アイランドの統計を削除します。

!!! warning "あなたがいるワールドのコマンドを使用してください"
    `/[player_command] stats` はそのゲームモードのワールド内でのみ機能します。例えば、OneBlock ワールドでは OneBlock コマンドを使用してください。そうしないと、複数のゲームモードでアイランドを持つプレイヤーが正しいものを見ることができません。

## 権限

!!! tip
    `[gamemode]` はゲームモードによって異なるプレフィックスです。

| 権限 | デフォルト | 許可する内容 |
|---|---|---|
| `[gamemode].island.stats` | true | `/[player_command] stats` で、アイランドの統計を開きます |
| `[gamemode].admin.stats` | op | `/[admin_command] stats <player> [reset]` |

## プレースホルダー

{{ placeholders_source("IslandStats") }}

`<entity>` は小文字のモブタイプです（`zombie` や `iron_golem` など）。PlaceholderAPI では、プレースホルダーは `%IslandStats_bskyblock_island_kill_entity_zombie%` のようになります。

## アドオン開発者向け

他のアドオンはマネージャーを通じてカウントを読み込むことができます：

```java
IslandStats stats = (IslandStats) BentoBox.getInstance().getAddonsManager().getAddonByName("IslandStats").orElseThrow();
long zombies = stats.getManager().getCount(island, IslandStat.KILL_ENTITY, EntityType.ZOMBIE);
long allDeaths = stats.getManager().getTotal(island, IslandStat.ENTITY_DEATH);
```

??? note "v1.0.0 の新機能 — 最初のリリース"
    **リリース日：** 2026 年 10 月 4 日

    最初のリリース。互換性：BentoBox API 3.23.0 · Minecraft 26.2 以降 · Java 25。[Release 1.0.0](https://github.com/BentoBoxWorld/IslandStats/releases/tag/1.0.0)

    - アイランドごとのモブ殺害と死亡カウント（`KILL_ENTITY` と `ENTITY_DEATH`）。
    - `/[player_command] stats` の統計ダイアログと、`/[admin_command] stats <player> [reset]` による管理者ビューとリセット。
    - アイランド合計、モブごとのカウント、プレイヤーが立っているアイランドのプレースホルダー。
    - 🔡 このリリースでは `en-US` ロケールのみが付属しています。翻訳を歓迎します。

## 翻訳

{{ translations("IslandStats") }}
