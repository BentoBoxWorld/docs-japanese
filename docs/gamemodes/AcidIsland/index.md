# AcidIsland

**AcidIsland** は、酸の海に囲まれた島でプレイヤーが生き残りを賭けるゲームモードです。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("AcidIsland") }}

## ストーリー
酸の海に浮かぶ小さな島から始まりましょう！スカイブロックが好きなら、新たな挑戦としてAcidIslandがぴったりです。

スカイブロックの変種ですが、虚空の代わりに危険な酸の海があなたを待っています。落ちれば只では済みません。また、ボートで他のプレイヤーの島に渡ることもできます。

## インストール

0. BentoBoxをインストールし、データフォルダを生成するためサーバーを少なくとも1回起動します。
1. このjarファイルをBentoBoxプラグインのaddonsフォルダに配置します。
2. サーバーを再起動します。
3. アドオンがワールドとデータフォルダを作成し、フォルダ内にconfig.ymlが生成されます。
4. サーバーを停止します。
5. config.ymlを希望通りに編集します。
6. ワールドの生成に関わる設定を変更した場合は、初回起動で作成されたワールドフォルダを削除します。
7. サーバーを再起動します。

## 設定

最新の `config.yml` は[こちら](https://github.com/BentoBoxWorld/AcidIsland/blob/develop/src/main/resources/config.yml)で確認できます。

### 浄化された水

!!! new "AcidIsland 1.22.0で追加"
    酸の海は相変わらず危険ですが、ついに水を**浄化**できるようになりました。酸の水入り瓶を飲むとバニラの毒エフェクトがかかり、浄化された水入り瓶を飲むと体力が回復します。どのアイテムが安全かひと目で分かるよう、水アイテムには色付きの説明文が付きます。水を浄化する方法は4通り ― かまどで水入り瓶や水バケツを精錬する、醸造台で水入り瓶を石炭と組み合わせる、鍾乳石の滴を大釜に集める ― のどれでもお好みで。

??? note "acid.purified-water.enabled"
    浄化された水の機能全体のマスタースイッチです。`false` にすると、タグ付け、かまど/醸造の介入、大釜の追跡がすべて停止します。

    デフォルト: `true`

??? note "acid.purified-water.heal-amount"
    浄化された水入り瓶を飲んだときに回復するハートの半分単位の量です。`4.0` はハート2個分になります。

    デフォルト: `4.0`

??? note "acid.purified-water.bucket-furnace-enabled"
    かまどで水バケツを精錬して浄化された水バケツを作ることを許可します。精錬時間は100秒（瓶の5倍）です。サーバーのバランス上「簡単すぎる」と感じる場合は `false` に設定してください。

    デフォルト: `true`

??? note "acid.purified-water.nether-enabled"
    このアドオンのネザーワールド（島型・バニラ型どちらも）で浄化された水の仕組みを有効にします。

    デフォルト: `true`

??? note "acid.purified-water.end-enabled"
    このアドオンのエンドワールド（島型・バニラ型どちらも）で浄化された水の仕組みを有効にします。

    デフォルト: `true`

## パーミッション

パーミッションの一覧は[こちら](Permissions)をご覧ください。

## コマンド

コマンドの一覧は[こちら](Commands)をご覧ください。

## プレースホルダー

プレースホルダーの一覧は[こちら](Placeholders)をご覧ください。

## 変更履歴

??? note "v1.22.0の新機能 — 浄化された水の仕組み"
    **リリース日:** 2026-04-15

    酸の水を浄化して、安全に飲んだり、農業に使ったり、瓶詰めにして持ち歩けるようになりました。すべての水アイテムには <span style="color:red">Acid Water</span> または <span style="color:green">Purified Water</span> の色付きの説明文が付き、大釜はサーバー再起動をまたいで中の水の状態を覚えています。

    - ⚙️ **浄化された水を追加** — 浄化方法は4通り。かまどで水入り瓶を精錬する（10秒）、醸造台で水入り瓶と石炭を組み合わせる、かまどで水バケツを精錬する（100秒、オン/オフ切替可能）、または鍾乳石の滴を大釜に集める。
    - ⚙️ **飲用時の効果** — 酸の水入り瓶はバニラの毒エフェクトを付与し、浄化された水入り瓶は体力を回復します（回復量は `acid.purified-water.heal-amount` で調整可能）。
    - ⚙️ 新しい設定ブロック `acid.purified-water.*` を追加（詳細は上の「設定」セクションを参照）。マスタースイッチ、回復量、水バケツのかまど精錬の切替、ネザー/エンドごとの切替を含みます。
    - 🔡 `acidisland.purified-water.*` 以下の新しいロケールキーを2つ追加。18言語すべてに同期済みです。
    - **新しいイベント** — 他のプラグインからフックできるよう、`ItemFillWithAcidEvent` と `PlayerDrinkPurifiedWaterEvent` を追加しました。
    - コード整備: パターンマッチングの `instanceof` 採用、`Math.clamp` の利用、`onPlayerMove`/`getWorld`/`findEntities`/`makeNetherRoof` の複雑度削減、テストの最新化など。

    [リリース v1.22.0](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/1.22.0)

??? warning "v1.21.0の新機能 — BentoBox 3.14.0が必要、ロケール移行あり"
    **リリース日:** 2026-04-12

    - **チェリーグローブ聖域スターター島。** Minecraft 1.21+サーバー向けに、チェリーグローブバイオームをテーマにした新しいスターター島のブループリントが含まれています。有効化するには、`BentoBox/addons/AcidIsland/blueprints/`を削除して次回起動時にブループリントを再生成してください。
    - 🔺 **BentoBox API 3.14.0以上が必要になりました。** このリリースをインストールする前にBentoBoxを更新してください。
    - 🔡 **全24のロケールファイルが`&`コードからMiniMessageに移行されました。** `BentoBox/locales/AcidIsland/`を削除して再起動すると再生成されます。カスタムファイルに残っている`&`コードはプレーンテキストとして表示されます。
    - バグ修正: EssentialsXの起動時読み込みに失敗した場合のゴッドモードチェックでのNullPointerException。
    - 移行中に発見されたいくつかの既存のロケールバグを修正。

    [リリース v1.21.0](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/1.21.0)

## 翻訳

{{ translations("AcidIsland") }}
