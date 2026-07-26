# BentoBox開発者ドキュメントへようこそ！

BentoBoxはその上で動作するアドオン向けのAPIスイートをサポートするプラットフォームプラグインです。アーキテクチャはBukkitプラグインシステムと事実上同じです。BSkyBlockのように独自のゲームモード体験をプレイヤーに提供するGameModeAddonsを作成することも、ゲームモードでワープサインを使用できるようにするWarpsのようなユーティリティAddonsを開発することもできます。

## Pladdon（プラドン）

サーバーの動作方式の変更（ロード時のコードのリマッピング）により、すべてのAddonsがBukkit Pluginラッパー内で動作することが推奨されるようになりました。このラッパーはBentoBoxによって提供され、Pladdon（Plugin + Addon）と呼ばれます。Pluginであることで、Paperなどのサーバーにロードされる際に正しくリマッピングされます。

Pladdons ラッパーの役割は、Addonインスタンスを生成し、`getAddon`メソッドを通じていつでも要求に応じて提供することです。

AddonsがPluginsになった結果、サーバーによってそのようにリストされますが、`Bentobox/Addons`フォルダに配置する必要があることに変わりはありません。

# JavaDocs
JavaDocsはこちら：[https://javadocs.bentobox.world](https://ci.codemc.io/job/BentoBoxWorld/job/BentoBox/javadoc/)

コアAPIパッケージは`world.bentobox.bentobox.api.*`です。これらのパッケージのメソッドは長期的にできるだけ安定していることを目指しています。APIパッケージ外のメソッドとクラスは頻繁に変更される場合があります。

# サンプルアドオン

@BONNeがサンプルアドオンをこちらでメンテナンスしています：[https://github.com/BONNePlayground/ExampleAddon](https://github.com/BONNePlayground/ExampleAddon)

# キャンセル可能なプレイヤーリセットイベント

*BentoBox 3.17.0 で追加。*

プレイヤーがチームを離れたり、アイランドがリセットされたりすると、BentoBox は各ゲームモードの `island.reset.on-leave` 設定に応じて、インベントリ・エンダーチェスト・所持金・体力・空腹度・経験値をクリアし、テイムした動物を野生に戻すことがあります。これらの各リセット動作は、実行**前**に**キャンセル可能な**イベントを発火するようになり、アドオンは「全部か無か」ではなく個々のリセットに拒否権を行使できます。リスナーがイベントをキャンセルすると、BentoBox はその動作をスキップします。

これらのイベントは `world.bentobox.bentobox.api.events.player` にあります:

| イベント | 発火するタイミング（直前） |
| --- | --- |
| `PlayerTamedRemovalEvent` | プレイヤーのテイムした動物を野生に戻す |
| `PlayerResetEnderChestEvent` | エンダーチェストのクリア |
| `PlayerResetInventoryEvent` | インベントリのクリア |
| `PlayerResetMoneyEvent` | プレイヤーの残高の引き出し |
| `PlayerResetHealthEvent` | 体力のリセット |
| `PlayerResetHungerEvent` | 空腹度のリセット |
| `PlayerResetExpEvent` | 経験値のリセット |

すべてのイベントは `PlayerBaseEvent`（`Cancellable` を実装）を継承し、プレイヤーの UUID、アイランド、ワールドを保持します。リッスンは標準的な Bukkit の方法です:

```java
@EventHandler
public void onInventoryReset(PlayerResetInventoryEvent e) {
    if (shouldKeepInventory(e.getPlayerUUID())) {
        e.setCancelled(true); // インベントリはクリアされません
    }
}
```

イベントは小さなビルダー API を通じて構築・発火されます:

```java
PlayerEvent.builder()
    .reason(PlayerEvent.Reason.INVENTORY_RESET)
    .involvedPlayer(uuid)
    .island(island)
    .world(world)
    .build();
```

これは完全に追加的なもので、すべてのクラスが新規であり既存の API は変更されていないため、3.17.0 は既存のアドオンとバイナリ互換です。[Inventory Switcher アドオン](../addons/InvSwitcher/index.md)はこれらのイベントを利用して、リセット時にワールドごとのインベントリと残高を保護します。[Release 3.17.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.17.0) を参照してください。

# モーダルダイアログ { #modal-dialogs }

*BentoBox 3.21.0 で追加されました。*

`world.bentobox.bentobox.api.dialogs` は Paper のモーダルダイアログシステムをラップしたもので、**Minecraft 26 以降**が必要です。ダイアログは Panels API と並び立つ存在です。パネルはプレイヤーがクリックして閉じられるインベントリですが、ダイアログはプレイヤーが必ず答えなければならないモーダルです。コアはこれをコマンドの確認、`/island go` の行き先ピッカー、チーム招待、初回参加時のゲームモード選択に使用しています。

| クラス | 用途 |
| --- | --- |
| `Dialogs` | `Dialogs.isSupported()` — このサーバーがダイアログを表示できるかどうか |
| `DialogBuilder` | 流暢なビルダー: `title`、`body`、`escapable`、`pause`、`confirmation`、`button`、`build` |
| `DialogButton` | ラベル、任意のツールチップ、および `Consumer<User>` のクリックハンドラー |
| `BBDialog` | ビルドされたダイアログ — `show(User)` で表示します |

`title(...)`、`body(...)`、`DialogButton.of(...)` はいずれも Adventure の `Component`、または `User` とロケール参照（任意で変数付き）のどちらかを受け取ります。そのため、ダイアログのテキストはアドオンの他の部分と同じ方法で翻訳されます。すべてが端から端まで `Component` ベースなので、クリックアクションも失われません。

```java
if (!Dialogs.isSupported()) {
    // 26 より前のサーバー: 従来のチャットまたはパネルのフローにフォールバック
    askInChat(user);
    return;
}
new DialogBuilder()
    .title(user, "myaddon.confirm.title")
    .body(user, "myaddon.confirm.body", "[name]", island.getName())
    .confirmation(
        DialogButton.of(user, "myaddon.confirm.yes", u -> doTheThing(u)),
        DialogButton.of(user, "myaddon.confirm.no", u -> u.sendMessage("myaddon.confirm.cancelled")))
    .build()
    .show(user);
```

!!! warning "必ずフォールバックを用意してください"
    コアと同じように、`Dialogs.isSupported()` をチェックし、古いサーバー向けに従来のチャットまたはパネルの動作を残しておいてください。ボタンのクリックハンドラーはメインスレッドで実行されるため、Bukkit API を直接呼び出せます。

[Release 3.21.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.21.0) を参照してください。
