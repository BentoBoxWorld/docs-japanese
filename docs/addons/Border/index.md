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
**説明**: ボーダーの種類を設定します。  
**権限**: `[gamemode].border.set-type`。デフォルト: `true`。  
**例**: `/[player command] border type barrier`  

### color {red|green|blue}
**コマンド**: `/[player command] color {red | green | blue}`  
**説明**: プレイヤーのバニラワールドボーダーの色を設定します。バニラボーダータイプ使用時のみ適用されます。  
**権限**: `[gamemode].color.red`、`[gamemode].color.green`、`[gamemode].color.blue`（または全色に `[gamemode].color.*`）。デフォルト: `op`。  
**例**: `/[player command] color green`  

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

### マップにワープを表示
バニラワールドボーダーの色機能が利用可能かどうかを制御します。個々のプレイヤーの色は `/[player_command] color` コマンドで設定します。ウェブマッププラグイン（Dynmap または BlueMap）と BentoBox マップフックが必要です。

```yml
show-warps-on-map: true
```

## プレースホルダー

| プレースホルダー | 説明 | バージョン |
|---|---|---|
| `%Border_color%` | プレイヤーの現在のボーダー色（`red`、`green`、または `blue`） | 4.8.0 |

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

## 翻訳

{{ translations("Border") }}

## ソース
貢献したいですか？このドキュメントのソースコードは [GitHub](https://github.com/BentoBoxWorld/docs/blob/master/docs/addons/Border/) で確認できます。
