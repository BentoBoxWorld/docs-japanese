# ChunkBlock コマンド

デフォルトプレイヤーコマンドは**`/ch`**（別称`/chunkblock`）、デフォルト管理者コマンドは**`/chadmin`**（別称`/chunkblockadmin`、`/cha`）。両方、そして複数のサブコマンドラベルは、設定可能`chunkblock.command`下`config.yml`：

```yaml
chunkblock:
  command:
    island: ch chunkblock
    admin: chadmin chunkblockadmin cha
    # Sub-command run on a player's very first /ch
    new-player-action: create
    # Sub-command run on every later bare /ch
    default-action: go
    count-command: count
    phases-command: phases
    set-count-command: setCount
    bossbar-command: bossbar
    actionbar-command: actionbar
    respawn-block-command: respawnBlock check
```

裸の`/ch`最初の時間アイランドを作成、その後プレイヤーをホームにテレポート。

!!! note "なぜ`/ch`ではなく`/cb`"
    ChunkBlockのデフォルトは1.0.0で`/cb`と`/cbadmin`でした、CaveBlockと衝突。1.0.1以降新規インストールは`/ch`と`/chadmin`取得。既存のサーバーは、その`config.yml`のいかなるエイリアスも保有。

## ChunkBlock プレイヤーコマンド

これらはChunkBlock固有なサブコマンド。他は何でも——`go`、`create`、`reset`、`sethome`、`team`、`ban`、`expel`、`settings`、`language`、`info`、`near`など——標準 BentoBox ゲームモードセット。

| Command | Description | Permission |
|---------|-------------|------------|
| `/ch chunks` | アンロック済みチャンク数、最大値、支出可能レベルクレジット、領土の色分けチャットマップ示し、チャンク次を要求できます。 | `chunkblock.island.chunks` |
| `/ch count` | アイランドの現在のマジックブロックカウントとフェーズ。 | `chunkblock.count` |
| `/ch phases` | フェーズGUI開く——ブラウズフェーズと、権限で、既に到達したフェーズのリプレイ。デフォルトでオフ。 | `chunkblock.phases` |
| `/ch setcount <number>` | 以前のジャンプブロックカウント完了フェーズのスタート値。受ける`set-count-cooldown`（デフォルト5分）。 | `chunkblock.island.setcount` |
| `/ch check` (alias `respawnBlock`) | マジックブロックのパーティクルを表示、またはそれがなくなった場合リスポーン。 | `chunkblock.respawn-block` |
| `/ch bossbar` | フェーズプログレスボスバーをトグル。`bossbar: true`が必須設定。 | `chunkblock.island.bossbar` |
| `/ch actionbar` | フェーズプログレスアクションバーをトグル。`actionbar: true`が必須設定。 | `chunkblock.island.actionbar` |

## ChunkBlock 管理者コマンド

`/chadmin`は完全標準 BentoBox 管理者セット（`version`、`tp`、`info`、`getrank`、`setrank`、`range`、`resets`、`deaths`、`purge`、`blueprint`、`register`、`delete`、`settings`、`reload`、`why`、`switch`、`team`など）にプラスChunkBlock固有コマンド下。

| Command | Description | Permission |
|---------|-------------|------------|
| `/chadmin chunks <player>` | アンロック済みチャンク数、有効な最大値、支出レベル、残余クレジットのプレイヤーを表示。 | `chunkblock.admin.chunks` |
| `/chadmin chunks <player> reset` | すべてを中央チャンクに再ロック、支出レコードをクリア。ビルドは触れられない——領土は単に再得しなければならず。 | `chunkblock.admin.chunks` |
| `/chadmin bypass` | 自分自身のチャンクロック強制をトグル。バイパス中、ロック済みチャンクを移動し、ボーダーカーテンはあなたのため隠れた。 | `chunkblock.mod.bypasschunks` |
| `/chadmin setcount <player> <number> [lifetime]` | プレイヤーのマジックブロックカウント、またはそれらの生涯カウントを設定。 | `chunkblock.admin.setcount` |
| `/chadmin setchest <phase> <rarity>` | チェストを見ているのを保存をフェーズのチェストファイル与えられた希少性（`COMMON`、`UNCOMMON`、`RARE`、`EPIC`）。チェストは埋ったシングルチェストである必要があります。 | `chunkblock.admin.setchest` |
| `/chadmin sanity [<phase>]` | フェーズの確率のサニティチェックをコンソールにプリント。 | `chunkblock.admin.sanity` |
| `/chadmin phases` | フェーズ順序エディター開く——再注文、リサイズ、有効・無効フェーズ。 | `chunkblock.admin.phases` |

!!! tip "`/chadmin bypass` ops 持っていない権限が必要"
    `chunkblock.mod.bypasschunks`デフォルト`false`、だから偶数では op がコマンド動作する前に明示的に付与される必要があります。それは意図的：スタッフはおよび同じルールでオプトインまで再生。Spectator モードは常に免除関係なく。

!!! tip "フェーズ順序エディターの使用"
    `/chadmin phases`すべてのフェーズを一覧表示順序で計算されたスタートブロック、長さ、状態、書き込み`phases_index.yml`。

    - **左クリック** はピックフェーズアップ。どこでクリックそれが行くべき、またはドロップエンドスロット、配置。どこかをクリック他、またはパネルを閉じて、それを戻す未変更。
    - **右クリック** はトグルフェーズオン・オフ。
    - **Shift-左クリック** はセットフェーズ長さはチャットプロンプト経由。最初の長さ編集は書き込み`adminLengths: true`をインデックス、だからあなたの長さは決して再計算。

    無効フェーズはグレイグラス表示、バージョンロック者をバリア。全フィール[フェーズ](Phases.md)を参照。

## `/ch chunks` 読み取り

```
Chunks: 9/441. Credit: 3 level(s) — a chunk costs 1.
Your island territory (9/441 chunks):
□ □ □ □ □
□ ▣ ▣ ▣ □
□ ▣ ■ ■ ▣
□ ▣ ■ ◆ ▣
□ □ ▣ ▣ □
■ yours  ▣ claimable (1 level(s) each)  □ locked
```

| Glyph | Meaning |
|---|---|
| `■` green | チャンクあなたは所有 |
| `▣` yellow | 今要求可能——隣接、範囲、制限以下 |
| `□` grey | ロック、まだ要求不可 |
| `◆` blue | チャンクあなたは立つ |

マップは15×15ビューまでアイランドと共に広がる。
