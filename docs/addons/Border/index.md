# Border

**Border** はプレイヤーが通過できないアイランド周囲のボーダーを作成・表示できます。  
ボーダーは以下のいずれかです:

- バニラのワールドボーダー
- プレイヤーが近づいたときに表示されるカスタムボーダー（ビジュアルは設定可能）。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("Border") }}

## インストール

1. サーバーを再起動します（アドオンを有効化し `config.yml` ファイルを生成するため）。
2. アドオン jar を `plugins/BentoBox/addons` フォルダに配置します。
3. `config.yml` の設定をカスタマイズします（任意）。
4. 新しい設定を適用するためにサーバーを再起動します。

## コマンド

!!! tip "ヒント"
    `[player_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこの値を変更する設定があります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island` です。

### border
**コマンド**: `/[player command] border`  
**説明**: ボーダーのオン/オフを切り替えます。  
**権限**: `[gamemode].border.toggle`。デフォルト: `op`。  
**注意**: バージョン 3.0.0 以降は権限が必要です。  

### border type {...}
**コマンド**: `/[player command] border type {barrier | vanilla}`  
**説明**: ボーダーの種類を設定します。引数なしで実行すると、利用可能な種類を切り替えます。  
**権限**: `[gamemode].border.type`。デフォルト: `true`。  
**例**: `/[player command] border type barrier`  

### bordertype {...}
**コマンド**: `/[player command] bordertype {barrier | vanilla}`  
**説明**: `border type` と同じコマンドで、ゲームモードのコマンド直下に登録されています。  
**権限**: `[gamemode].border.bordertype`。デフォルト: `false`。  
**例**: `/[player command] bordertype vanilla`  

### border color {red|green|blue}
**コマンド**: `/[player command] border color {red | green | blue}`（`/[player command] bordercolor {red | green | blue}` としても利用できます）  
**説明**: プレイヤーのバニラワールドボーダーの色を設定します。バニラボーダータイプ使用時のみ適用されます。  
**権限**: コマンドを実行するには `[gamemode].border.color` が必要です。デフォルト: `true`。  
さらに、それぞれの色に個別の権限が必要です: `[gamemode].border.color.red`、`[gamemode].border.color.green`、`[gamemode].border.color.blue`（または全色に `[gamemode].border.color.*`）。デフォルト: `op`。  
**例**: `/[player command] border color green`  

!!! warning "4.8.5 での権限変更"
    `[gamemode].border.color` は 4.8.5 より前は宣言されていなかったため、暗黙のうちに op 限定にフォールバックしており、通常のプレイヤーは色コマンドをまったく実行できませんでした。現在はデフォルト `true` で宣言されています。

    宣言されていたノード `[gamemode].bordertype` も、コマンドが実際に確認しているノードである `[gamemode].border.bordertype` に改名されました。LuckPerms（などの権限プラグイン）で `[gamemode].bordertype` を許可または拒否していた場合は、ルールを更新してください — 古いノードは実際には何の効果もありませんでした。

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

## 設定

`config.yml` ファイルには設定が含まれています。  
明示的に記載がない限り、デフォルト値は通常サンプル値と同じです。

### ゲームモードの無効化
この設定でアドオンを無効にできます。  
デフォルトでは、Border は BentoBox サーバーの全ゲームモードワールドで動作します。

`-` で始まる新しい行にゲームモード名を書くことでゲームモードを無効にできます。  
BSkyBlock を無効にする例:

```yml
disabled-gamemodes:
  - BSkyBlock
```

デフォルト値:

```yml
disabled-gamemodes: []
```

### ボーダーの種類
新しいプレイヤーが取得するボーダーのデフォルトな種類。2つの選択肢があります:

- `VANILLA` — Minecraft 独自のワールドボーダー効果を使用します（バニラゲームで見られるゆらゆらした壁）。色を付けることができます。
- `BARRIER` — 目に見えないバリアブロックと色付きパーティクルを使用します。エッジに近づいたときだけ表示されます。

権限のあるプレイヤーは `/[player command] border type` でボーダーを切り替えられます。権限がない場合は、ここで設定したボーダーが提供されます。

```yml
type: VANILLA
```

### バニラボーダーの色
バニラワールドボーダーの色。ボーダーの種類が `VANILLA` の場合のみ使用されます。  
選択肢は `RED`、`GREEN`、または `BLUE`。権限のあるプレイヤーは `/[player command] border color` でカスタムカラーを選べます。

```yml
color: BLUE
```

### アイテムのバウンスバック
`true` の場合、プレイヤーがボーダーに投げたアイテムは外に飛び出さず、内側に戻されます。`false` に設定すると、投げたアイテムはボーダーを通過します。

```yml
bounce-back: true
```

### 帰還テレポート
プレイヤーがボーダーを何らかの方法で通過した場合（例: 同じワールド内でのテレポート）、アイランドに戻すかどうかを制御します。

プレイヤーを戻したい場合は `true` に設定してください。

**警告**: この値を `false` に設定し、かつ `use-barrier-blocks` も `false` に設定した場合、プレイヤーはボーダーを自由に通り抜けられるようになります。

```yml
return-teleport: true
```

!!! tip "ヒント"
    このアドオンをプレイヤーへの**ボーダー表示のみ**に使用したい場合は、次の設定を使用してください:
    ```yml
    use-barrier-blocks: false
    return-teleport: false
    ```

### 帰還テレポート時の安全ブロック
`return-teleport` が `true` の場合のみ使用されます。プレイヤーがボーダー内にテレポートで戻され、危険な場所に着地した場合（例: 崖の上やマグマ内）、足元に安全ブロックを配置して怪我を防ぎます。

```yml
return-teleport-safety-block: true
```

### バリアブロックの使用
バニラボーダータイプを**使用していない**プレイヤーにのみ適用されます。

- `true`: ボーダーはバリアブロックで構成されます。  
- `false`: バリアブロックベースのボーダーは設置されません。これはプレイヤーがアイランドを離れた際のテレポートについて `return-teleport` 設定に委ねられます。

```yml
use-barrier-blocks: true
```

### デフォルトのボーダー動作
プレイヤーは適切な権限があればコマンドでボーダーのオン/オフを切り替えられます。  
この設定はデフォルトのオン/オフを決定します。デフォルトでオンにするには `true` に設定してください。

```yml
show-by-default: true
```

### 最大保護範囲ボーダーの表示
バニラボーダータイプを**使用していない**プレイヤーにのみ適用されます。

最大保護範囲でバリア（🚫）パーティクルを表示する場合は `true` に設定してください。  
これは Boxed のようにプレイヤーの保護エリアが移動できるゲームモードで有用です。

これらはバリアブロックではなく**パーティクル**なので、「空気」がそのように**見えるだけ**です。

```yml
show-max-border: true
``` 

### パーティクルの表示
アドオンが表示する全種類のウォールパーティクル（ボーダーと最大保護範囲パーティクル）を有効/無効にします。

**いかなる**ウォールパーティクルも表示しない場合は `false` に設定してください。

```
show-particles: true
```

### バリアオフセット
バニラボーダータイプを**使用していない**プレイヤーにのみ適用されます。

通常、ボーダーはプレイヤーの保護範囲の端に正確に配置されます。この設定はバリアを指定ブロック数分**外向き**にシフトするため、プレイヤーは壁に当たる前に保護範囲を少し超えて歩くことができます。

覚えておくべき重要な点:

- 保護範囲そのものを大きくする**わけではありません** — プレイヤーは追加スペースに建築したり保護したりできません。ただ立つことができるだけです。
- ボーダーはアイランド距離を超えて外に出ることは決してありません。どんな大きな数字を設定しても関係ありません。
- 最小値（およびデフォルト値）は `0` で、これはボーダーが保護範囲の上に配置されることを意味します。

```yml
barrier-offset: 0
```

## プレースホルダー

| プレースホルダー | 説明 | バージョン |
|---|---|---|
| `%Border_color%` | プレイヤーの現在のボーダー色（`red`、`green`、または `blue`） | 4.8.0 |

## FAQ

??? question "ボーダーのサイズを変更するには？"
    ボーダーはそのもの自体のサイズを持っていません — 各アイランドの**保護範囲**の周りに描画されます。ボーダーを大きくまたは小さくするには、保護範囲を変更します。

    - プレイヤーに `[gamemode].island.range.<number>` のような権限を与えてより大きな範囲を提供します（例: `bskyblock.island.range.150`）。
    - 管理者は管理範囲コマンドで特定のアイランドの範囲を設定できます。例: `/bsbadmin range set <player> <number>`。
    - 範囲は**アイランド間の距離の半分**を超えることはできません。この距離はワールド作成時に一度だけ設定され、その後は変更できません。

    詳細は [Island Range and Spacing](../../BentoBox/About/IslandManagement.md#island-range-and-spacing) を参照してください。

??? question "ボーダーをアイランドの範囲より少し大きくすることはできますか？"
    はい！`config.yml` の `barrier-offset` 設定を使用してください。選択したブロック数分ボーダーを外向きにシフトするため、プレイヤーは壁に当たる前に保護範囲を少し超えて立つことができます。

    この設定はボーダーを移動させるだけで、プレイヤーに建築または保護できる追加土地を**与えません**。上記の [バリアオフセット](#バリアオフセット) 設定を参照してください。

??? question "バリアとバニラボーダータイプの違いは何ですか？"
    - **バニラ** は Minecraft 独自のワールドボーダー効果を使用します — 通常のゲームで知られている輝く壁。赤、緑、青に色付けできます。
    - **バリア** は見えないバリアブロックと、エッジに近づいたときだけ表示される色付きパーティクルを使用します。

    権限のあるプレイヤーは `/[player command] border type` で切り替えられます。

??? question "固い壁ではなく、プレイヤーが越えられるラインだけが欲しいのですが？"
    はい。`use-barrier-blocks: false` で固い壁がなくなり、`return-teleport: false` でプレイヤーが引き戻されません。これでビジュアルボーダーだけが残ります。`config.yml` に以下を設定します:

    ```yml
    use-barrier-blocks: false
    return-teleport: false
    ```

??? question "ボーダーの色を変更するには？"
    色は**バニラ**ボーダータイプでのみ機能します。`config.yml` の `color` 設定でサーバー全体のデフォルトを設定します（`RED`、`GREEN` または `BLUE`）。権限のあるプレイヤーはゲーム内で `/[player command] border color {red|green|blue}` で色を選択できます。

??? question "ボーダーをオフにするには？"
    プレイヤーは `/[player command] border` でボーダーのオン/オフを切り替えられます（`[gamemode].border.toggle` 権限が必要です）。全員デフォルトでオフにするには、`config.yml` で `show-by-default: false` に設定します。

??? question "ボーダーが表示されていません —何を確認すればいい？"
    - `config.yml` の `disabled-gamemodes` にゲームモードが記載されていないか確認してください。
    - プレイヤーがボーダーを実際にオンにしているか確認します（`/[player command] border`）。また `show-by-default` が `true` か確認します。
    - ボーダーは自分のアイランドの保護範囲周りにだけ表示されるため、エッジの近くにいないと見えません。
    - **バリア**タイプで `show-particles: false` を使用している場合、触れるまで壁は見えません — これは期待通りです。

??? question "機能 X を追加してくれませんか？"
    [issue tracker](https://github.com/BentoBoxWorld/Border/issues) でリクエストしてください。

## 変更履歴

??? note "v4.7.0 → v4.8.2 の新機能"
    **リリース日:** 2026-02-16 ～ 2026-04-04

    - **バニラワールドボーダーの色選択。** バニラボーダータイプを使用するプレイヤーが `/[player_command] color {red|green|blue}` でボーダーの色（赤、緑、青）を選択できるようになりました。
    - 新しい `%Border_color%` プレースホルダーがプレイヤーの現在のボーダー色を返します。
    - 新しい権限 `[gamemode].color.red`、`[gamemode].color.green`、`[gamemode].color.blue`（または全色に `[gamemode].color.*`）。デフォルト: op。
    - バグ修正: プレイヤーが全アイランドスペース外にいる場合のボーダーテレポートバイパス（4.7.0）。
    - バグ修正: プレイヤーがアイランド間をテレポートしてもバニラワールドボーダーがリセットされない問題（Bedrock/Geyser プレイヤーが制限状態に入ることがありました）（4.8.1）。
    - バグ修正: 一部の設定で `%Border_color%` プレースホルダーが null エラーをスローする問題（4.8.1）。
    - バグ修正: バニラのネザーとエンドワールドでボーダーが誤って有効化される問題（4.8.1）。

    [Release v4.7.0](https://github.com/BentoBoxWorld/Border/releases/tag/4.7.0) · [v4.8.0](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.0) · [v4.8.1](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.1) · [v4.8.2](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.2)

??? note "v4.8.3 の新機能"
    **リリース日：** 2026-04-26

    - 🔡 すべてのロケールファイルをレガシー `&` カラーコードから MiniMessage 形式に変換しました。
    - 🔡 英語以外のすべてのロケールに不足していた `set-color` キーを追加しました。
    - 🔡 ポーランド語、ウクライナ語、中国語ロケールファイルのバグを修正しました。
    - 🔺 最低 BentoBox API バージョンを **3.12.0** に引き上げました。

    🔺 **`plugins/BentoBox/addons/Border/locales/` にカスタムロケールオーバーライドがある場合**、再起動前に `&a` スタイルのカラーコードを MiniMessage タグ（例：`<green>`）に移行してください。

    [Release v4.8.3](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.3)

??? note "v4.8.4 の新機能"
    **リリース日：** 2026-05-26

    - 🐛 **Paper/Purpur 1.21.10 での `NoSuchMethodError: WorldBorder.changeSize` を修正。** 4.8.3 のビルドは Paper 1.21.11 に対してコンパイルされており、ワールドボーダーのメソッドが改名されていたため、`/[player_command] bordertype vanilla` を使用すると 1.21.10 サーバーでバニラのボーダータイプがクラッシュしていました。Border はバージョン互換の `setSize` API を使用するようになり、**1.21.10 と 1.21.11 の両方**で動作します。
    - 🐛 Modrinth 公開ワークフローを修正（成果物のパスが不正でした）。

    設定やロケールの変更は不要です。`bordertype barrier` で回避していた場合は、4.8.4 をインストールすれば `vanilla` に戻せます。

    [Release v4.8.4](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.4)

??? warning "v4.8.5 の新機能 — 権限の変更"
    **リリース日：** 2026-08-01

    互換性と権限に関する修正リリースです。設定やロケールの変更は不要です。

    - 🐛 **他プラグインからドロップ品を横取りしなくなりました。** 4.7.0 で追加された死亡ドロップの保護は、`PlayerDeathEvent` からすべてのアイテムを取り出して自前でスポーンさせ、リストを空にしていました。そのため DeathChest や墓石系プラグイン、インベントリ保持機能は後から実行されて空のイベントを受け取り、アイテムはすでに地面に落ちている状態でした。デフォルトの `bounce-back: true` では、これがそれらすべてを静かに壊していました。Border はイベントのドロップ品に手を触れず、MONITOR 優先度で実行し、直後のティックに死亡地点付近でサーバー自身がスポーンさせたアイテムだけを跳ね返すようになりました。他のプラグインがドロップ品を取得した場合は何も跳ね返らず、ドロップ品が残った場合はこれまでどおり跳ね返り、バニラの初速や消滅タイマーも保たれます。
    - 🔺 **`[gamemode].border.color` がデフォルト `true` で宣言されるようになりました。** これにより、通常のプレイヤーもドキュメントどおりに色コマンドを使用できます。以前は `addon.yml` で宣言されていなかったため、op 限定にフォールバックしていました。個別の色（`.red`、`.green`、`.blue`）は引き続き `op` です。この不具合を回避するために明示的に付与していた権限は、そのままでも動作します。
    - 🔺 **`[gamemode].bordertype` を `[gamemode].border.bordertype` に改名。** これは `BorderTypeCommand` が実際に確認しているノードです。デフォルトの `false` は変更ありません。古いノードを参照している LuckPerms のルールは更新してください — どちらにせよ効果はありませんでした。
    - リリースが Modrinth に加えて CurseForge と Hangar にも自動公開されるようになり、Modrinth の掲載対象が 1.21.5～1.21.11 および 26.1.x になりました。

    互換性: BentoBox API 3.12.0+、Minecraft 1.21.5～1.21.11 および 26.1.x、Java 21。

    [Release v4.8.5](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.5)

## 翻訳

{{ translations("Border") }}

## ソース
貢献したいですか？このドキュメントのソースコードは [GitHub](https://github.com/BentoBoxWorld/docs/blob/master/docs/addons/Border/) で確認できます。
