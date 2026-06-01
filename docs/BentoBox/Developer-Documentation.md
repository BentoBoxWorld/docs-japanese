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
