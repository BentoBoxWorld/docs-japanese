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
