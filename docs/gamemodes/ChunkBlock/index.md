# ChunkBlock

マジックブロック1つ。チャンク1つ。歩いて渡ることができない壁。

**ChunkBlock**は、誰もが知るOneBlockループ——マジックブロックを採掘するとそれが何か別のものに変わる、フェーズが進む——に、16ブロック先の堅い境界を加えたものです。スタートチャンク外のすべてが禁止エリア：歩く、飛ぶ、グライダー、パール、乗る、掘る、どれもできません。抜け出す唯一の方法は*より豊か*になることです。

アイランドレベルが通貨です。レベルを上げて壁に向かい、**進みたい方向に壁を殴ってください**。反対側のチャンクが開き、ボーダーが1ステップ外側に移動します。レベルが下がると壁が戻ってきます——最も新しいチャンクから——農場はレベルを取り戻すまで壁の向こう側です。

作成・メンテナンス：[tastybento](https://github.com/tastybento)。マジックブロックエンジンは[AOneBlock](../AOneBlock/index.md)から来たもので、フェーズファイルは互換性があります。チャンク制御はChunkBlock固有です。

{{ addon_description("ChunkBlock") }}

## プレイヤーがはまる理由

- 🔒 **本当に渡れない境界がある。** 歩き、ダッシュジャンプ、エリトラ、ripツイハリ、エンダーパール（払い戻し）、コーラスフルーツ、馬、ボート、マインカート、クリエイティブフライはすべてゲート設定されています——*すべての*高さ、void から build limit 上まで。飛び越すルートもない、掘り下げるルートもありません。
- 💰 **レベルは領土。** ショップではなく、ランクでもなく、タイマーでもありません。プレイヤーが既に最適化している——アイランドレベル——これが領土を買うものです。置かれたすべてのブロックは次のチャンクへの頭金です。
- 👊 **拡張は物理的なジェスチャー。** GUI なし、`/buy chunk` なし。オーナーが壁に立ち、殴ると、世界は音と緑のパーティクルスイープで開きます。方向を選べるので、2つのアイランドが同じ形で成長することはありません。
- ⚠️ **損失は歯を持っています——残酷ではなく。** レベルドロップは最近クレームされたチャンクを正確な逆順で再度ロックします。内側には何も触れられません：ビルド、チェスト、モブはすべてレベルが戻ってくるときにまだそこにあります。優しいゲームを好みますか？1行の設定で領土がラチェットになり、決して縮みません。
- 🗺️ **フロンティアが見える。** プレイヤー当たりのパーティクルカーテンがあなた近くのすべてのロック面をマーク（オプションでクライアント側バリアブロック）し、`/ch chunks`は色分けされたマップで何を所有、次に何を要求、何がコストであるかを表示します。
- 🧱 **何も漏れない。** ピストン、流動、ディスペンサー、樹木成長、火と草の蔓延、爆発、自然なモブスポーンはすべてラインで止まり、ドロップアイテムは禁止ゾーンに失われるのではなく反発します。
- ⛏️ **フルOneBlockゲーム。** 20のテーマ付きフェーズ、15,500ブロックのコンテンツ、重み付きブロックとモブプール、希少チェスト、ホログラム、ボスバーとアクションバープログレス——すべてが、成長するボックスの中です。

## セッションはどのような感じか

草ブロックの上でどこにも生まれ、すべての方向に赤い壁が見えます。採掘。もう一度採掘。丸石、土、その場で端を歩いていく鶏。50番目のブロック目の周りでチャットが「クレジットがあります」と言うので、日の出側に向きを変え、壁を殴ると、*崩れ落ちます*——1秒前より2倍の世界、そして実際に麦農場を建てることができます。

50レベル後、あなたのアイランドは3×3ブロックのチャンクで、方向を意図的に選んでいます：オーシャンフェーズが来ていて、東側のドロップの方に余地が必要です。その後、ダンジョンフェーズで悪く死に、チャンク分のレベルを失い、最新のチャンクが炉銀行を中で閉ざします。それは消えていません。壁の後ろに*있*です、レベルを取り戻すまで。

## セットアップ

!!! warning "Level アドオンは必須です"
    アイランドレベルが唯一のチャンク通貨なので、ChunkBlockはLevel なしでは実行されません。Levelが見つからない場合、ChunkBlockは明確なメッセージと共にコンソールで自分自身を無効にし、半分実行開始しません。

0. BentoBoxをインストールし、サーバーを1回実行してフォルダを存在させます。
1. **Level** アドオンを`plugins/BentoBox/addons/`にインストールします。
2. **ChunkBlock** jar を`plugins/BentoBox/addons/`にドロップしてリスタートします。
3. ChunkBlockは`chunkblock_world`、データフォルダ、`config.yml`、`phases`フォルダ、`phases_index.yml`を作成します。
4. サーバーを停止し、`config.yml`を編集し、変更が生成に影響する場合は作成したワールドを削除します。
5. リスタートします。

ChunkBlockはAOneBlock、CaveBlockなどの他の場所で幸せに実行される——独自のワールド、コマンド（`/ch`、`/chadmin`）、権限（`chunkblock.*`）、フラグ、データベーステーブル。

!!! tip "推奨されるコンパニオン"
    - **Level** ——必須、チューニング価値あり：その死亡ペナルティとブロック値は、ChunkBlockで*領土*設定です。
    - **Border** ——互換性あり。アイランドの全体保護限界を描画します。チャンクフロンティア内はChunkBlock独自のカーテンです。
    - **InvSwitcher** ——他のゲームモードからインベントリを分離します。
    - Challenges、Warps、Likes、Biomes、Greenhouses など通常のようにアンロックされたチャンク内で動作します。

## 互換性

| 機能 | サポート |
|---|---|
| サーバー | ✅ Paper / Spigot、Minecraft 1.21+ |
| BentoBox バージョン | ✅ 3.13.0 以上 |
| Java バージョン | ✅ Java 21 |
| Level アドオン | ⚠️ 必須——アイランドレベルはチャンク通貨 |
| Nether / End | ⪀ デフォルト生成オフ、下記参照 |

## 設定

`config.yml`は標準BentoBoxゲームモードファイルにChunkBlock専用ブロック1つを加えたものです。すべてのオプションはファイル自体にコメント付きです。最新のコピーは[config.yml](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/resources/config.yml)にあります。

### チャンク設定

```yaml
chunkblock:
  # 1つのチャンク要求にいくつのアイランドレベルが必要か。最小1。
  levels-per-chunk: 1
  # アイランドが要求できるチャンク最大数（中央チャンク含む）。
  # 441は完全な21×21チャンク正方形。-1は「保護範囲が保持するもの」という意味。
  max-chunks: 441
  # 支出より下のレベルを失うと、最新のチャンクが再ロックされます。
  # false = 'ラチェットモード': 要求されたチャンクは再ロックされません。
  relock-on-level-loss: true
  # 再ロックされるチャンク内のプレイヤーを移出。
  eject-players-on-relock: true
  # ロックされたチャンク内の自然モブスポーンをキャンセル。
  deny-mob-spawns-in-locked: true
  # ドロップアイテムをボーダーで反発させる代わりに失われないようにする。
  bounce-back-items: true
  border:
    # ロックされたチャンク面でプレイヤー当たりのパーティクルカーテン。
    show-particles: true
    particle-color:
      ==: Color
      ALPHA: 255
      RED: 255
      GREEN: 0
      BLUE: 0
    # クライアント側バリアブロックも送信。純粋にビジュアル。ワールドは決して修正されません。
    client-side-barrier-blocks: false
```

!!! abstract "完全ガイド：[チャンク要求](Chunks.md)"
    各設定がゲームの感覚をどのように影響するか、実践的なクレジット例、再ロックルール、カジュアルまたはハードコアサーバーのペースをチューニングする方法。

### 通常より重要なワールド設定

=== "distance-between-islands"
    !!! summary "8の倍数である必要があります"
        アイランド中心が、チャンク内のど真ん中（x ≡ 8、z ≡ 8）に着地しなければならないか、マジックブロックはチャンク継目に座ります。ChunkBlockは読み込み時にこの値を最も近い8の倍数にスナップするため、手編集の`250`は黙って`248`になります。デフォルトは`256`です。

=== "protection-range"
    !!! summary "2番目の堅いサイズキャップ"
        クレームされたチャンクはアイランドの保護範囲内に完全に収まらなければならないため、範囲は`max-chunks`が何と言おうと領土をキャップします。フィットする最大リングradius は`(protection-range − 8) ÷ 16`、端数切り捨て、`(2r + 1)²`チャンク与えます。

        デフォルト——`protection-range: 240`——では、これは radius 14、841チャンク、`max-chunks: 441`が実際に噛みつく設定です。`max-chunks`を上げれば、範囲がそれを保持し、範囲は決して`distance-between-islands`を超えられないことを思い出してください。

=== "offset-x / offset-z"
    !!! summary "意図的に欠席"
        他のゲームモードワールドオフセットを公開します。ChunkBlockは`start-x`/`start-z`から内部で計算するため、マジックブロックは常にチャンク中央に、設定は一切提供されません。

=== "nether and end"
    !!! summary "デフォルトでオフ"
        両方の`nether.generate`と`end.generate`はデフォルト`false`。いずれかをオンにして、その次元は独自の中央チャンクと同じ要求ルール、同じアイランドレベルで駆動されます。マジックブロックはOverworldでのみ存在します。

### フェーズ

マジックブロック、フェーズファイル、`phases_index.yml`は、AOneBlockで行うのとまったく同じように動作します——形式はバイト単位で互換性があり、コミュニティフェーズパックは直接ドロップされます。

!!! abstract "完全ガイド：[マジックブロックとフェーズ](Phases.md)"
    出荷された20フェーズ進行、フェーズインデックス、管理フェーズエディター、完全なフィールド参照の場所。

### カスタマイズ可能なGUI

ChunkBlockはBentoBoxテンプレートパネルAPIをフェーズGUIに使用します。初回実行時、`plugins/BentoBox/addons/ChunkBlock`下の`panels`フォルダに`phases_panel.yml`を作成します。[カスタマイズ可能なGUI](../../Tutorials/generic/Customizable-GUI.md)メカニクスを参照。`PREVIOUS`、`NEXT`、`PHASE`ボタンタイプは[AOneBlockドキュメント](../AOneBlock/index.md#customizable-guis)で説明されている通り動作します。

## コマンド

!!! tip
    デフォルトプレイヤーコマンドは`/ch`（別称`/chunkblock`）、デフォルト管理者コマンドは`/chadmin`（別称`/chunkblockadmin`、`/cha`）です。両方とも`config.yml`の`chunkblock.command`下で設定可能です。

=== "ChunkBlock ユニークプレイヤーコマンド"
    - `/ch chunks` ——チャンク数、支出可能なクレジット、領土のチャットマップ。
    - `/ch count` ——現在のマジックブロック数とフェーズ。
    - `/ch phases` ——フェーズGUI。
    - `/ch setcount <number>` ——既に到達したフェーズをリプレイ。
    - `/ch check` ——マジックブロックをリスポーンさせるか、パーティクルを表示。
    - `/ch bossbar` / `/ch actionbar` ——プログレスディスプレイをトグル。

=== "ChunkBlock ユニーク管理者コマンド"
    - `/chadmin chunks <player> [reset]` ——プレイヤーのチャンク、支出、クレジットを検査、または中央チャンクに再ロック。
    - `/chadmin bypass` ——自分用のチャンクロック強制をトグル。
    - `/chadmin setcount <player> <number> [lifetime]` ——プレイヤーのブロックカウントを設定。
    - `/chadmin setchest <phase> <rarity>` ——見ているチェストをフェーズに保存。
    - `/chadmin sanity [<phase>]` ——フェーズの確率をコンソールでチェック。
    - `/chadmin phases` ——フェーズ順序エディター。

[完全なChunkBlockコマンドリスト](Commands.md)

## 権限

!!! tip
    すべてのChunkBlock権限は`chunkblock.`とプレフィックスされています。

!!! warning "`chunkblock.mod.bypasschunks`はopsに与えられていません"
    チャンクロックバイパスのデフォルトは`false`——**not** `op`——だから、スタッフは権限プラグインで明示的に付与するまでみんなと同じルールでプレイします。BentoBoxの`chunkblock.mod.bypasslock`から意図的に分離されており、これはアイランド*ロック*をバイパスし、異なる機能です。

=== "プレイヤー権限"
    - `chunkblock.island.chunks` ——`/ch chunks`を使用。デフォルト`true`。
    - `chunkblock.count` ——`/ch count`を使用。デフォルト`true`。
    - `chunkblock.phases` ——`/ch phases`を使用。デフォルト`false`。
    - `chunkblock.island.setcount` ——`/ch setcount`を使用。デフォルトOP。
    - `chunkblock.respawn-block` ——`/ch check`を使用。デフォルト`true`。
    - `chunkblock.island.bossbar` / `chunkblock.island.actionbar` ——プログレスディスプレイをトグル。デフォルト`true`。

=== "管理者権限"
    - `chunkblock.admin.chunks` ——`/chadmin chunks`を使用。デフォルトOP。
    - `chunkblock.mod.bypasschunks` ——チャンクロックから除外、`/chadmin bypass`を使用。**デフォルト`false`。**
    - `chunkblock.admin.setcount`、`chunkblock.admin.setchest`、`chunkblock.admin.sanity`、`chunkblock.admin.phases` ——デフォルトOP。

[完全なChunkBlock権限リスト](Permissions.md)

## フラグ

ChunkBlockは独自のフラグIDを登録するため、AOneBlockの隣で実行できます。

| フラグ | タイプ | 説明 | デフォルト |
|---|---|---|---|
| `CHUNKBLOCK_START_SAFETY` | ワールド設定 | プレイヤーはアイランド作成後短時間移動できないため、すぐに落ちません。期間は設定の`starting-safety-duration`です。 | false |
| `CHUNKBLOCK_BOSSBAR` | アイランド設定 | フェーズプログレスボスバーを表示。設定で`bossbar: true`の場合のみ利用可能。 | true |
| `CHUNKBLOCK_ACTIONBAR` | アイランド設定 | フェーズプログレスアクションバーを表示。設定で`actionbar: true`の場合のみ利用可能。 | true |
| `MAGIC_BLOCK` | 保護 | マジックブロックを破壊するために必要な最小アイランドランク。 | COOP |

!!! warning "バージョン1.0.0からアップグレード"
    これらのフラグは1.0.0では`START_SAFETY`、`ONEBLOCK_BOSSBAR`、`ONEBLOCK_ACTIONBAR`と呼ばれていました。アップグレード後にいずれかをデフォルトから変更した場合、1回設定を再適用してください——古い値はもう読まれません。

## プレースホルダー

マジックブロックエンジンから継承されたフェーズプレースホルダーとともに、ChunkBlockは5つの領土プレースホルダーを追加します：

| プレースホルダー | 説明 |
|---|---|
| `%chunkblock_island_chunks%` | アンロックされたチャンク数（中央チャンク含む） |
| `%chunkblock_island_max_chunks%` | このアイランドが要求できる最大チャンク |
| `%chunkblock_island_chunk_credit%` | 今支出可能なレベルクレジット |
| `%chunkblock_island_next_chunk_level%` | 次のチャンクを購入するために必要な総アイランドレベル |
| `%chunkblock_island_ring%` | 最外部のクレームされたチャンクのリング番号 |

[完全なChunkBlockプレースホルダーリスト](Placeholders.md)

## よくあるご質問

??? question "光る赤い壁を過ぎて歩けないのはなぜ？"
    そのチャンクはまだロックされています。あなたがアイランドオーナーでレベルクレジットがあれば、壁を殴ると開きます。`/ch chunks`はあなたのクレジットと要求可能なものを表示します。

??? question "チームメンバーがチャンクを要求できますか？"
    いいえ——要求はアイランドオーナーの決断です。みんなテムが領土を活用し、クレジット通知を見え、`/ch chunks`を実行できますが、境界で支出するのはオーナーだけです。

??? question "レベルを失い、農場が壁の向こう側にあります。消えていますか？"
    いいえ。再ロックされたチャンク内に何も触れられません——ブロック、チェスト、モブはまさにあなたが置いたまま。レベルを取り戻してクレームを取り戻し、再ロックはいつも最新のチャンクからなので、失った順に取り戻します。管理者は`relock-on-level-loss: false`で再ロックを完全に無効にできます。

??? question "立っているときにチャンクが再ロックされました。私に何が起こりますか？"
    あなたは独自のアイランド内の最も近いアンロック箇所に移動します——飛行状態保存、落下ダメージキャンセル、着地ブロックが安全でない場合は下に作成されます。誰も取り残されたり、voidに落ちたりしません。そのアイランドに属さないプレイヤーは代わりに独自のアイランドホームに送られます。

??? question "より早くチャンク要求を取得するにはどうすればよいですか？"
    アイランドレベルを上げる：より多く、より価値のあるブロックを置く。より太っ腹な拡張を望む場合は`levels-per-chunk`を下げるか、マップをゆっくり開くようにしたい場合は上げます。

??? question "対角線上で要求できますか？"
    直接ではありません。新しいチャンクは既に所有している領土と**面**を共有する必要があるため、コーナーチャンクは2つの直交隣人のいずれかを最初に要求する必要があります。

??? question "アイランドはどのくらい大きくなりますか？"
    より小さい方：`max-chunks`（デフォルト441、21×21正方形）またはアイランドの保護範囲内に収まるチャンクの最大正方形。`/ch chunks`は有効な最大値を表示します。

??? question "ずっと落ちて死んでいますか？"
    スタート時はチャンクは多くの部屋ではありません。上になる前に外に出す——死亡がレベルをコストすることを思い出し、レベルは領土です。

??? question "どのフェーズがありますか？"
    AOneBlockと同じ進行：平原、地下、冬、海、ジャングル、沼地、ダンジョン、砂漠、ネザー、plenty、荒廃、深黒、エンド、豊かな洞窟、鍾乳洞、マングローブ沼地、草地、サクラグローブ、ギザギザ頂上、硫黄洞窟。[フェーズ](Phases.md)を参照。

??? question "ネザーまたはエンドがありますか？"
    両方ともデフォルトでオフ。`config.yml`でオンにして、それぞれは独自の中央チャンクと同じ要求ルールを取得します。マジックブロックはOverworldでのみ存在します。

??? question "Border アドオンが必要ですか？"
    いいえ、削除する必要もありません。Borderはアイランドの外側保護限界を描画します。ChunkBlockはその中のチャンクフロンティアを描画します。異なるものを示し、うまく共存します。

??? question "バグがあるか、機能のアイデアがあります。どこに入れますか？"
    [issue tracker](https://github.com/BentoBoxWorld/ChunkBlock/issues)で。

## 翻訳

{{ translations("ChunkBlock") }}

## API

ChunkBlockはデータを独自のデータベーステーブル`ChunkBlockIslands`に保存し、イベント、リクエストハンドラー、アドオンクラスを通じて領土状態を公開します。

プロジェクトにprovided依存関係として追加します：

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>chunkblock</artifactId>
    <version>1.0.1</version>
    <scope>provided</scope>
</dependency>
```

### データオブジェクト

=== "OneBlockIslands"
    !!! summary "説明"
        アイランド単位の状態：AOneBlockエンジンから継承されたマジックブロック進行プラス、チャンク領土。

        ソースへのリンク：[OneBlockIslands](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/java/world/bentobox/chunkblock/dataobjects/OneBlockIslands.java)

    !!! question "変数"
        - `uniqueId` ——アイランド一意ID、アイランドの`uniqueId`に等しい。
        - `blockNumber` ——現在の破壊ブロック番号。
        - `lifetime` ——これまでに破壊されたすべてのブロック数。
        - `phaseName` ——現在のフェーズ名。
        - `hologram` ——表示されているホログラムテキスト。
        - `unlockedChunks` ——順序付けられた`"dx,dz"`要求リスト、中央チャンクに相対。`"0,0"`は常に最初で削除できません。
        - `lastKnownLevel` ——前回の計算時のアイランドレベル、利益と損失を検出するために使用。

    !!! example "コード例"
        ```java
        public void accessChunkBlockData(@NonNull Island island) {
            BentoBox.getInstance().getAddonsManager().<ChunkBlock>getAddonByName("ChunkBlock")
                .ifPresent(chunkBlock -> {
                    OneBlockIslands data = chunkBlock.getOneBlocksIsland(island);
                    int chunks = data.getUnlockedChunkCount();
                    List<String> claimOrder = data.getUnlockedChunks();

                    ChunkManager cm = chunkBlock.getChunkManager();
                    long credit = cm.getCredit(island);
                    long spent = cm.getSpentLevels(island);
                    int max = cm.getMaxChunks(island);
                    boolean here = cm.isUnlocked(island, someLocation);
                });
        }
        ```

### イベント

ChunkBlockはAOneBlockマジックブロックイベント（`BlockClearEvent`、`MagicBlockEntityEvent`、`MagicBlockEvent`、`MagicBlockPhaseEvent`——[AOneBlock APIセクション](../AOneBlock/index.md#events)を参照、同じフィールド、`world.bentobox.chunkblock.events`パッケージ内）に加えて独自の2つを発火させます。

=== "ChunkUnlockEvent"
    !!! summary "説明"
        アイランドがクレームするたびに1回発火。**キャンセル不可**——クレームは既に決定され支払われています。これは通知です。

        クラスへのリンク：[ChunkUnlockEvent](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/java/world/bentobox/chunkblock/events/ChunkUnlockEvent.java)

    !!! question "変数"
        - `@NonNull Island island` ——チャンクをクレームしたアイランド。
        - `@NonNull Vector chunkOffset` ——中央チャンクに相対的なチャンクオフセット（xとz。yは常に0）。
        - `int unlockIndex` ——アイランドのクレーム順序内のチャンクの位置。中央チャンクは0。

    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onChunkUnlock(ChunkUnlockEvent event) {
            Island island = event.getIsland();
            Vector offset = event.getChunkOffset();
            int index = event.getUnlockIndex();
        }
        ```

=== "ChunkRelockEvent"
    !!! summary "説明"
        アイランドがレベルドロップの時にチャンクを失うたびに1回発火。**キャンセル不可。** イベントは最近クレームされたものからパネアが、チャンクが実際に取られている順序と一致します。

        クラスへのリンク：[ChunkRelockEvent](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/java/world/bentobox/chunkblock/events/ChunkRelockEvent.java)

    !!! question "変数"
        - `@NonNull Island island` ——チャンクを失ったアイランド。
        - `@NonNull Vector chunkOffset` ——中央チャンクに相対的なチャンクオフセット。
        - `int unlockIndex` ——クレーム順序でチャンクが保有していた位置。

    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onChunkRelock(ChunkRelockEvent event) {
            Island island = event.getIsland();
            Vector offset = event.getChunkOffset();
            int index = event.getUnlockIndex();
        }
        ```

### リクエストハンドラー

コンパイル時の依存関係を望まないプラグインは[Addon Request API](../../BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons.md)を使用できます。ChunkBlockはマジックブロックエンジンから`island-stats`と`location-stats`を登録プラス：

=== "unlocked-chunks"
    !!! summary "説明"
        プレイヤーのアイランドの領土情報。`"player"` → `UUID`を送信。プレイヤーがChunkBlockワールドでアイランドを持たない場合は空のマップを返します。

    !!! question "返却マップ"
        - `count` ——`Integer`、中央を含むアンロックされたチャンク。
        - `max` ——`Integer`、このアイランドがアンロックできる最大。
        - `ring` ——`Integer`、最外部のアンロックされたチャンクのリング番号。
        - `spent` ——`Long`、チャンク上で既に支出されたレベル。
        - `credit` ——`Long`、支出可能なレベルクレジット。
        - `chunks` ——`List<String>`、クレーム順序の`"dx,dz"`オフセット。

    !!! example "コード例"
        ```java
        Map<String, Object> request = Map.of("player", player.getUniqueId());
        @SuppressWarnings("unchecked")
        Map<String, Object> result = (Map<String, Object>) new AddonRequestBuilder()
                .addonName("ChunkBlock")
                .label("unlocked-chunks")
                .addMetaData(request)
                .request();
        int chunks = (int) result.getOrDefault("count", 0);
        ```

## チェンジログ

??? note "バージョン1.0.0の新機能"
    **リリース：** 2026-07-28

    初回リリース。OneBlockループ、あなたが支払うときに成長するチャンク。

    - **ボーダーを殴ってチャンクを要求。** アイランドレベルは支出可能なクレジット（`levels-per-chunk`ごと、デフォルト1）。オーナーは壁を狙ってパンチまたは右クリックして次のチャンク、任意の方向を開きます。
    - **領土には後ろ足がある。** すべてのクレームは順番に記録されます。アイランドレベルが支出したもの以下に低下した場合、最近クレームされたチャンクが再ロック、最新のものからです。ビルド内は触れられません。`relock-on-level-loss: false`はラチェットモード。
    - **本当に渡れないボーダー。** 歩き、ダッシュジャンプ、エリトラ、ripツイハリ、エンダーパール（払い戻し）、コーラスフルーツ、乗り物、ボート、フライはゲート設定です。ピストン、液体、ディスペンサー、樹木成長、蔓延、爆発は過ぎることができず、ドロップアイテムは跳ね返ります。
    - **見えるフロンティア。** プレイヤー単位のパーティクルカーテンがロック面をマークし、オプションクライアント側バリアブロック、クレジット獲得と要求祝いエフェクト。ワールドは決して修正されません。
    - **`/ch chunks`** ——領土の色分けチャットマップ、次に要求可能、クレジット。
    - **デザイン上安全。** 再ロックチャンクに捕まったプレイヤーは最も近いアンロック箇所に移動、飛行保存、落下ダメージなし。
    - **Level アドオンが必須** ——アイランドレベルが唯一チャンク通貨。

    [Release 1.0.0](https://github.com/BentoBoxWorld/ChunkBlock/releases/tag/1.0.0)

!!! warning "バージョン1.0.1の新機能——フラグIDとデフォルトコマンド変更"
    **リリース：** 2026-07-30

    1.0.0に対して報告されたすべてのバグを修正するパッチリリース、他のゲームモードをChunkBlockの隣で実行するときのみ現れる2つの互換性問題。

    - 🐛 **ボーダー近くの採掘はもうクレームメッセージをスパムしません。** クレーム検出は実際にクリックしたブロックを無視し、壁を通過したため、壁から数ブロック離れたジェネレーターを採掘する通知*「このチャンクをクレームするにはN以上のレベルクレジットが必要」*スイングのたびに。クレームは実際のボーダーに対する本物の目標のみでトリガー、失敗フィードバックはレート制限されます。[#14](https://github.com/BentoBoxWorld/ChunkBlock/issues/14)を修正。
    - 🐛 **リスポーンはもはや見知らぬアイランドでプレイヤーを置き去りできません。** ロックされたチャンク内の古い、または放棄されたアイランドでのリスポーン着地は、プレイヤーを*そのアイランド内*で再配置、着地ブロック生成。そのアイランドに属さないプレイヤーは代わりに独自のアイランドホームに送られます。[#13](https://github.com/BentoBoxWorld/ChunkBlock/issues/13)を修正。
    - 🔡 **フェーズGUIはsetcount権限を尊重。** *「クリックして変更」*はもう`chunkblock.island.setcount`なしのプレイヤーに提供されず、GUIタイトルはChunkBlockフェーズと言う。[#11](https://github.com/BentoBoxWorld/ChunkBlock/issues/11)を修正。
    - 🔺 ⚙️ **独自フラグID、AOneBlockとの衝突なし。** ボスバー、アクションバー、スタート安全フラグは`CHUNKBLOCK_BOSSBAR`、`CHUNKBLOCK_ACTIONBAR`、`CHUNKBLOCK_START_SAFETY`。AOneBlockのIDを以前共有し、BentoBoxは重複フラグ登録を拒否——両者を実行するサーバーでは、どのアドオンが2番目にロードされたとしても、黙ってフラグが失われます。
    - 🔺 ⚙️ **デフォルトコマンドは`/cb`から`/ch`に変更。** CaveBlockは既に`/cb`と`/cbadmin`を使用するため、デフォルトは`ch chunkblock`（プレイヤー）と`chadmin chunkblockadmin cha`（管理者）。既存のサーバーは`config.yml`内のいかなるエイリアスでも保持；新規インストールだけが新しいデフォルトを取得します。
    - **Levelが見つからないとき、きれいなシャットダウン。** ChunkBlockは今、明確なメッセージで自分自身を無効にする代わりに、左半登録リスナーがすべての結合と移動でスパムエラーを残します。

    🔺 **アップグレード後：** ボスバー、アクションバー、またはスタート安全ワールド設定をデフォルトから変更した場合、1回設定を再適用してください——古い`ONEBLOCK_*` / `START_SAFETY`値はもう読まれません。

    🔡 **ロケールノート：** キーがリネーム（`protection.flags.CHUNKBLOCK_*`、フェーズGUIタイトル）。カスタマイズされたロケールファイルを再生成または更新。

    **互換性：** BentoBox API 3.13.0+、Minecraft 1.21+、Java 21。

    [Release 1.0.1](https://github.com/BentoBoxWorld/ChunkBlock/releases/tag/1.0.1)
