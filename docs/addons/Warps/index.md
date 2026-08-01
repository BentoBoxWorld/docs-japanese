# Warps

**Warps** はプレイヤーがアイランドに個人ワープサインを追加できるようにします。

作成・メンテナンス: [tastybento](https://github.com/tastybento)

{{ addon_description("Warps") }}

## インストール

1. Warps アドオンの jar を BentoBox プラグインの addons フォルダに配置します
2. サーバーを再起動します
3. アドオンはデータフォルダを作成し、その中に config.yml が作成されます
4. config.yml を希望通りに編集します
5. 変更した場合はサーバーを再起動します

## 設定

### config.yml

アドオンが正常にインストールされると、config.yml ファイルが作成されます。このファイルのすべてのオプションにはコメントが付いています。詳細はファイルを確認してください。
最新の設定ファイルはこちらで確認できます: [config.yml](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/resources/config.yml)

??? question "ワープ制限とは何ですか？"
    これはワープサインの作成を、少なくとも特定のアイランドレベルを持つプレイヤーに制限します。Level アドオンが必要で、デフォルトレベルは 10 です。

??? question "ウェルカムテキストとは何ですか？"
    これはプレイヤーがワープサインを作成するために看板に書く必要があるテキストです（例: [Welcome]）。大文字小文字を区別しません！
    
    このテキストは一番上の行に記述する必要があります。

??? question "無効化されたゲームモードとは何ですか？"
    このリストには Warps アドオンが動作しないゲームモードが保存されます。

    アドオンを無効にするには、- で始まる新しい行にその名前を記述します。例:
    ```
      disabled-gamemodes:
       - BSkyBlock
    ```

??? question "ロアフォーマットとは何ですか？"
    ロアフォーマットは看板の説明行のデフォルトカラーを変更できます。説明行は GUI で使用されます。

    説明行は [welcome] テキストより下の看板の行です。

??? question "他のワールドでの許可とは何をするのですか？"
    これにより、非 BentoBox のワールドを含む*任意*のワールドにワープサインを設置できます。

    プレイヤーは使用するために `welcomewarpsigns.warp` 権限が必要です。

??? question "show-warps-on-map とは何ですか？"
    `true` に設定すると、ワープサインの場所がウェブマッププラグイン（Dynmap、BlueMap）にマーカーとして表示されます。

    互換性のあるマッププラグインと BentoBox マップフックが必要です。各ワープサインは `[Welcome]` の下の看板行のテキストを持つポイントマーカーとして表示されます。

    デフォルト: `true`

??? question "warp と warps とは何ですか？"
    コマンド `warp` はテレポートするプレイヤーの `<player>` が必要ですが、`warps` はプレイヤーを選択できるメニューを開きます。

    `allow in other worlds` を有効にした場合はメインコマンド `/warp` になります。
    
    BentoBox の各ゲームモードでは `/[player_cmd] warp` のままです。
    

### カスタマイズ可能な GUI

BentoBox 1.17 API ではカスタマイズ可能な GUI を実装できる機能が導入されました。このアドオンはこの機能を使用する最初のアドオンの 1 つです。できるだけシンプルなカスタマイズを目指しましたが、一部の機能には説明が必要です。
BentoBox カスタム GUI の詳細はこちらをご覧ください: [Custom GUI's](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "GUI をカスタマイズするにはどうすればいいですか？"
    アドオン GUI をカスタマイズするにはバージョン 1.12 が必要です。これが最初に実装されたバージョンです。アドオンは `/plugins/BentoBox/addons/Warps` の下に `panels` という名前のディレクトリを作成します。

??? question "`PREVIOUS`|`NEXT` ボタンタイプとは何ですか？"
    PREVIOUS および NEXT ボタンタイプは、GUI にスペースよりも多くのアイランドがある場合に自動ページングを作成します。
    これらのタイプにはデータの下に追加パラメーターがあります:
 
    - `indexing` - ボタンにページ番号を表示するかどうかを示します。

    例: 
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: warps.gui.buttons.previous.name
        description: warps.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            action: PREVIOUS
            tooltip: warps.gui.tips.click-to-previous
    ```

??? question "`RANDOM` ボタンタイプとは何ですか？"
    このボタンはプレイヤーがランダムなワープにテレポートできます。
    2 つ以上のワープがある場合にのみ利用可能です。

    例: 
    ```yaml
        icon: DROPPER
        title: warps.gui.buttons.random.name
        description: warps.gui.buttons.random.description
        data:
          type: RANDOM
        actions:
          warp:
            click-type: left
            tooltip: warps.gui.tips.click-to-warp
    ```

??? question "`WARP` ボタンタイプとは何ですか？"
    WARP ボタンはワープオブジェクトの動的エントリを作成します。

    タイトル、説明、アイコンを指定すると看板とデータベースデータに基づく動的生成が上書きされます。デフォルトではこれらの値はデータベースエントリから生成されます。
    
    PLAYER_HEAD アイコンはオーナーのプレイヤーヘッドに置き換えられます。ただし、現時点では異なるプレイヤーヘッドを指定するオプションはありません。

    例: 
    ```yaml
        warp_button:
          icon: PLAYER_HEAD
          title: warps.gui.buttons.warp.name
          description: warps.gui.buttons.warp.description
          data:
            type: WARP
          actions:
            warp:
              click-type: left
              tooltip: warps.gui.tips.click-to-warp
    ```


## コマンド

!!! tip "ヒント"
    `[player_command]` は実行中のゲームモードによって異なるコマンドです。
    ゲームモードの `config.yml` ファイルにはこれらの値を変更するオプションがあります。
    例えば BSkyBlock では、デフォルトの `[player_command]` は `island` です。
    このアドオンではアドオンの `config.yml` でプレイヤーコマンドのエイリアスを変更できることに注意してください。

=== "プレイヤーコマンド"
    - `/[player_command] warp <player>`: 対象の看板にプレイヤーをワープします。
    - `/[player_command] warps`: 利用可能なすべてのワープサインを表示する GUI を開きます。

## 権限

!!! tip "ヒント"
    `[gamemode]` は実行中のゲームモードによって異なるプレフィックスです。
    プレフィックスはゲームモード名の小文字です。例えば BSkyBlock を使用している場合、プレフィックスは `bskyblock` です。
    同様に AcidIsland を使用している場合、プレフィックスは `acidisland` です。

=== "プレイヤー権限"
    - `[gamemode].island.warp` - プレイヤーが `/[player_command] warp` と `/[player_command] warps` コマンドを使用できます。デフォルトで有効。
    - `[gamemode].island.addwarp` - プレイヤーがワープサインを作成できます。デフォルトで有効。
    - `welcomewarpsigns.warp` - プレイヤーが `/warp` と `/warps` コマンドを使用できます。デフォルトで無効。`allow-in-other-worlds` が必要。
    - `welcomewarpsigns.addwarp` - プレイヤーがワープサインを作成できます。デフォルトで無効。`allow-in-other-worlds` が必要。
 
??? question "何か不足していますか？"
    このアドオンの [addon.yml](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/resources/addon.yml) ファイルで権限の完全なリストを確認できます。  
    もし本当に不足しているものがあれば、お知らせください！

## よくある質問

??? question "機能 X を追加してもらえますか？"
    [こちら](https://github.com/BentoBoxWorld/Warps/issues)のリストに追加してください。

??? question "バグを発見しました。どこに報告すればいいですか？"
    [こちら](https://github.com/BentoBoxWorld/Warps/issues)のリストに追加してください。

## 変更履歴

??? note "v1.18.0 の新機能"
    **リリース日:** 2026-04-05

    - **ウェブマップのサポート（Dynmap / BlueMap）。** `show-warps-on-map` オプションが有効（デフォルト: true）な場合、ワープサインがウェブマップにポイントマーカーとして表示されるようになりました。BentoBox 互換のマッププラグインが必要です。
    - 新しい `show-warps-on-map` 設定オプション（上記の設定を参照）。
    - ロシア語ロケールが MiniMessage 形式に更新され、完全なキーカバレッジが追加されました。
    - 追加のロケールファイルが追加・更新され、BentoBox フォーマットと一致するようになりました。
    - BentoBox API 3.12.0 以降が必要です。

    新しいフォーマットでロケールファイルを再生成するには `BentoBox/addons/Warps/locales/` を削除してください。

    [Release v1.18.0](https://github.com/BentoBoxWorld/Warps/releases/tag/1.18.0)

??? warning "v1.19.0 の新機能 — ロケール移行が必要"
    **リリース日:** 2026-04-11

    - **すべてのロケールファイルが MiniMessage に移行されました。** BentoBox 3.14 との一貫性のため、すべてのロケールファイルがレガシーの `&` カラーコードから MiniMessage タグに変換されました。
    - BentoBox API 3.14.0 以降が必要です。
    - Warps は Paper 1.21.11 専用にビルドされるようになりました（Spigot API は廃止）。

    **BentoBox 3.14.0 が必要です。** Warps をアップグレードする前に BentoBox を更新してください。

    **ロケールファイルを再生成してください** — `BentoBox/locales/Warps/` を削除してサーバーを再起動してください。カスタムロケールファイルの `&` カラーコードはレンダリングされなくなります。

    [Release v1.19.0](https://github.com/BentoBoxWorld/Warps/releases/tag/1.19.0)

??? note "v1.19.1 の新機能"
    **リリース日：** 2026-07-30

    パッチリリースです。設定やロケールの変更は不要です。

    - 🐛 **ワープが看板のブロックにフォールバックした際、看板の所有者に通知されるようになりました。** ワープ看板の正面に安全な場所がない場合 — 看板がプラットフォームの端にあり、正面がボイドになっているケースでよく起こります — 訪問者は静かに看板自身のブロックへテレポートされていました。`WarpInitiateEvent` も発火せず、vanish のチェックも行われず、所有者への「X さんがあなたのワープ看板にワープしました！」というメッセージもありませんでした。フォールバックも通常のワープと同じ完了処理を通るようになったため、訪問者がどこに着地しても、イベント・vanish の処理・音・所有者への通知が同じように動作します。到着時の向きも看板の向きに合うようになりました。
    - 既存の Modrinth ワークフローに加えて、CurseForge と Hangar への公開が自動化されました。また Modrinth のゲームバージョン一覧に MC 26.1.2 が追加されました。
    - `addon.yml` の API バージョンを 3.12.0 に引き上げ、読み込み順序を改善するための softdepend エントリを追加しました。

    互換性: BentoBox API 3.12.0+、Minecraft 1.21.x、Java 21。

    [Release v1.19.1](https://github.com/BentoBoxWorld/Warps/releases/tag/1.19.1)

## 翻訳

{{ translations("Warps") }}

## API

### イベント

BentoBox 1.17 API ではクラスローダーの問題を解決した機能が実装されました。イベントを直接使用したいプラグインは、これを利用できます。

プロジェクトに Warps を依存関係として追加するだけです。Maven を使用できます:

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>warps</artifactId>
    <version>1.11.2</version>
    <scope>provided</scope>
</dependency>
```

=== "WarpInitiateEvent"
    !!! summary "説明"
        プレイヤーが新しいワープサインを作成した後に発火するイベントです。

        クラスへのリンク: [WarpInitiateEvent](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/java/world/bentobox/warps/event/WarpInitiateEvent.java)

    !!! question "変数"
        - `UUID player` - ワープサインを作成したプレイヤーの ID。
        - `Location warpLoc` - ワープサインの場所。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onWarpInitiate(WarpInitiateEvent event) {
            UUID player = event.getPlayer();
            Location warpLoc = event.getWarpLoc();
        }
        ```

=== "WarpRemoveEvent"
    !!! summary "説明"
        ワープサインが削除された後に発火するイベントです。

        クラスへのリンク: [WarpRemoveEvent](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/java/world/bentobox/warps/event/WarpRemoveEvent.java)

    !!! question "変数"
        - `UUID owner` - ワープサインを所有しているプレイヤーの ID。
        - `UUID remover` - ワープサインを削除したプレイヤーの ID。
        - `Location warpLoc` - ワープサインの場所。
 
    !!! example "コード例"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onWarpRemove(WarpRemoveEvent event) {
            UUID owner = event.getOwner();
            UUID remover = event.getRemover();
            Location warpLoc = event.getWarpLocation();
        }
        ```
