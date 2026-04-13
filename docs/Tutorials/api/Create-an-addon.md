# はじめに

BentoBox は**新しい機能や新しい_ゲームモード_を提供するために_アドオン_に依存しています**。
このチュートリアルでは**最初のアドオンの作成**プロセスをガイドします。

アドオンの作成は最初からプラグインを作成するよりも簡単で速いことが多いです。BentoBox が[ラッパー](https://en.wikipedia.org/wiki/Wrapper_function)と主要な API 機能を提供しているためです。
アドオンはまた、[Java クラスローダーの可視性原則](https://www.javatpoint.com/classloader-in-java)により、プラグインとは異なり、他のアドオンの API に直接アクセスできます。
さらに、BentoBox の [Config API](../../BentoBox/Config-API.md) と [Database API](../../BentoBox/Database-API.md) にもアクセスできます。

このチュートリアルを快適に進めるには、アドオン開発の経験が必要です。
アドオン開発プロセスは実際には非常に似ており、簡潔さのため、このチュートリアル全体を通じて主要な Java の概念を理解していることを前提とします。

# プロジェクトの準備

## 事前作成されたアドオンテンプレートを使用する

現時点ではテンプレートは存在しません。

## 手動でプロジェクトを作成する

### BentoBox を依存関係としてインポートする

BentoBox にはアドオンの作成と登録に必要なすべての API が含まれています。
そのため、プロジェクトの依存関係として追加する必要があります。

BentoBox は Maven を使用しており、Maven リポジトリは [CodeMC](https://codemc.org/) によって提供されています。
ただし、Gradle を使用して BentoBox を取得することもできます。

#### Maven

`pom.xml` ファイルに以下を追加します。

```xml
<repositories>
  <repository>
    <id>codemc-repo</id>
    <url>https://repo.codemc.org/repository/maven-public/</url>
  </repository>
</repositories>

<dependencies>
  <dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>bentobox</artifactId>
    <version>PUT-VERSION-HERE</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
```

#### Gradle

`build.gradle` ファイルに以下を追加します。

```groovy
repositories {
  maven { url "https://repo.codemc.org/repository/maven-public/" }
}

dependencies {
  compileOnly 'world.bentobox:bentobox:PUT-VERSION-HERE'
}
```

問題がある場合は [Gradle の依存関係宣言に関するドキュメント](https://docs.gradle.org/current/userguide/declaring_dependencies.html)を参照してください。

### プロジェクトアーキテクチャのセットアップ

# メインアドオンクラスの作成

**アドオンのメインクラス**はプラグインのメインクラスと同様に機能します。
主にアドオンの読み込み、有効化、リロード、無効化時に実行されるコードを処理します。

メインクラスは **`Addon` を継承します**。

*例:*
```java
import world.bentobox.bentobox.api.addons.Addon;

public class MyAddon extends Addon {

}
```

!!! tip "ヒント"
    メインクラスの命名を検討する際:
    クラス名をアドオン名にできるだけ近いものにすることをお勧めします。
    また、クラス名に "Addon" を追加して目的をさらに明確にすることもできます。

*実際の例*: [Greenhouses](https://github.com/BentoBoxWorld/Greenhouses/blob/develop/src/main/java/world/bentobox/greenhouses/Greenhouses.java),
[Chat](https://github.com/BentoBoxWorld/Chat/blob/develop/src/main/java/world/bentobox/chat/Chat.java),
[Biomes](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/BiomesAddon.java)。

## 必須メソッド

Bukkit プラグインと同様に、アドオンは適切に有効化されるためにいくつかのメソッドをオーバーライドする必要があります。

メインアドオンクラスは以下のようになります:

```java
import world.bentobox.bentobox.api.addons.Addon;

public class MyAddon extends Addon {
    @Override
    public void onEnable() {}
    
    @Override
    public void onDisable() {}
}
```

### onEnable()

このメソッドは `#onLoad()` の後に呼び出されます。

### onDisable()

このメソッドはアドオンが無効化されるとき（通常はサーバーシャットダウン時）に呼び出されます。

## オプションメソッド

必要に応じて追加のメソッドをオーバーライドできます。

```java
import world.bentobox.bentobox.api.addons.Addon;

public class MyAddon extends Addon {
    @Override
    public void onLoad() {}

    @Override
    public void onEnable() {}

    @Override
    public void onReload() {}
    
    @Override
    public void onDisable() {}
}
```

### onLoad()
onLoad() メソッドのコードはアドオンが読み込まれたとき、onEnable() の前に実行されます。設定の読み込みや、このアドオンがゲームモードの場合のコマンドセットアップに適した場所です:
```
    @Override
    public void onLoad() {
        // Save the default config from config.yml
        saveDefaultConfig();
        // Load settings from config.yml. This will check if there are any issues with it too.
        loadSettings();
        // Register game mode commands
        playerCommand = new DefaultPlayerCommand(this)

        {
            @Override
            public void setup()
            {
                super.setup();
                new IslandAboutCommand(this);
            }
        };
        adminCommand = new DefaultAdminCommand(this) {};
    }
```

### onReload()
このメソッドのコードは管理者が `bbox reload` コマンドを使用してアドオンをリロードするときに実行されます。

# addon.yml の作成
addon.yml はアドオンを BentoBox に説明するために必要です。Bukkit で使用される plugin.yml とほぼ同一です。以下は最小限の例です:

```
name: Bank
main: world.bentobox.bank.Bank
version: 1.0.0
api-version: 1.15.4
authors: tastybento
```
上記のタグは必須であり、すべての addon.yml に含める必要があります。<br>

<table cellspacing="0" cellpadding="4" border="1">
   <caption>addon.yml 属性
   </caption>
   <tbody>
       <tr>
           <th>属性
           </th>
           <th>必須
           </th>
           <th>説明
           </th>
           <th>例
           </th>
           <th>備考
           </th>
       </tr>
       <tr style="font-weight: bold;">
           <td>name
           </td>
           <td>yes
           </td>
           <td>アドオンの名前。
           </td>
           <td>
               <code>name: MyAddon</code>
           </td>
           <td>
               <ul>
                   <li>英数字とアンダースコア (a-z, A-Z, 0-9, _)</li>
                   <li>アドオンのデータフォルダ名の決定に使用されます。データフォルダはデフォルトで ./addons/ ディレクトリ内に作成されます。</li>
                   <li>例: 'Bank.jar' のように jar ファイルと同じ名前にすることが推奨されます。</li>
               </ul>
           </td>
       </tr>
       <tr style="font-weight: bold;">
           <td>version
           </td>
           <td>yes
           </td>
           <td>このアドオンのバージョン。
           </td>
           <td>
               <code>version: 1.3.1</code>
           </td>
           <td>
               <ul>
                   <li>バージョンは任意の文字列ですが、最も一般的な形式は MajorRelease.MinorRelease.Build（例: 1.4.1）です。</li>
                   <li>通常、新しい機能やバグ修正をリリースするたびにインクリメントします。</li>
                   <li>
                       ユーザーが 
                       <code>/bbox version</code>
                       と入力したときに表示されます。
                   </li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>description
           </td>
           <td>no
           </td>
           <td>アドオンが提供する機能の人が読めるような説明。
           </td>
           <td>
               <code>description: This addon is so boxy.</code>
           </td>
           <td>
               <ul>
                   <li>説明は複数行にわたることができます。</li>
                   <li>
                       ユーザーが 
                       <code>/version addonName</code>
                       と入力したときに表示されます。
                   </li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>authors
           </td>
           <td>yes
           </td>
           <td>共同プロジェクトの場合、1 人または複数の作者をリストできます。複数の場合は YAML 文字列リスト形式を使用します。
           これは実際には必須項目です。
           </td>
           <td>
<code>authors:
- BONNe
- tastybento</code><br>
または<br>
<code>authors: tastybento</code>
           </td>
           <td>
               <ul>
                   <li>1 人または複数の作者をリストできます。</li>
               </ul>
           </td>
       </tr>
       <tr style="font-weight: bold;">
           <td>main
           </td>
           <td>yes
           </td>
           <td>Addon または Pladdon を継承するクラスを指定します。
           </td>
           <td>
               <code>main: world.bentobox.acidisland.AcidIsland</code>
           </td>
           <td>
               <ul>
                   <li>クラスファイル自体を含む完全な名前空間を含める必要があります。</li>
                   <li>
                       名前空間が 
                       <code>world.bentobox.addon</code>
                       でクラスファイルが 
                       <code>Myaddon</code>
                       の場合、これは 
                       <code>world.bentobox.addon.Myaddon</code>
                       でなければなりません。
                   </li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>depend
           </td>
           <td>no
           </td>
           <td>アドオンの読み込みに必要なアドオンのリスト。
           </td>
           <td>
               <code>depend: Oneaddon, Anotheraddon</code>
           </td>
           <td>
               <ul>
                   <li>
                       値はカンマ区切りです。
                   </li>
                   <li>依存関係を指定するには必要なアドオンの "name" 属性を使用します。</li>
                   <li>ここにリストされているアドオンが見つからない場合、アドオンの読み込みに失敗します。</li>
                   <li>複数のアドオンが互いを depend としてリストし、読み込めない依存関係のないアドオンがない場合、すべての読み込みに失敗します。</li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>softdepend
           </td>
           <td>no
           </td>
           <td>アドオンが必要とする可能性があるが必須ではないアドオンのリスト。
           </td>
           <td>
               <code>softdepend: AcidIsland, BSkyBlock, SkyGrid, CaveBock, AOneBlock</code>
           </td>
           <td>
               <ul>
                   <li>
                       値はカンマ区切りです。
                   </li>
                   <li>依存関係を指定するには目的のアドオンの "name" 属性を使用します。</li>
                   <li>アドオンはここにリストされているプラグインの後に読み込まれます。</li>
                   <li>循環するソフト依存関係は任意の順序で読み込まれます。</li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>permissions
           </td>
           <td>no
           </td>
           <td>アドオンが登録したい権限。各ノードは登録する権限を表します。各権限には追加の属性を持てます。
           </td>
           <td>
               <pre>permissions:    
  '[gamemode].intopten':
    description: Player is in the top ten.
    default: true
  '[gamemode].island.level':
    description: Player can use level command
    default: true
  '[gamemode].island.top':
    description: Player can use top ten command
    default: true</pre>
           </td>
           <td>
               <ul>
                   <li>権限の登録はオプションで、コードからも行えます。</li>
                   <li>権限登録では説明、デフォルト値、子親関係を設定できます。</li>
                   <li>権限名には <code>[gamemode]</code> タグを含めて、サーバーに読み込まれたすべてのゲームモードに適用できます。</li>
               </ul>
           </td>
       </tr>
   </tbody>
</table>

# Pladdon
Pladdon は Bukkit Plugin とアドオンの組み合わせです。Pladdon の主な利点は Bukkit Server クラスローダーで読み込まれるため、その中のデータをプラグインから直接アクセスできることです。例えばレベルアドオンのようなユーティリティアドオンを作成する場合、他のプラグイン開発者がコードを通じて生成されたデータに API 経由でアクセスしたいと思うかもしれません。最もシンプルな方法は Pladdon を作成することで、コード内のメソッドを直接呼び出すことができます。プラグインがアドオンのデータにアクセスしないようにしたい場合は、アドオンのままにしてください。

## アドオンを Pladdon にする
これを行うには、推奨名 `MyAddonPladdon.java`（MyAddon はアドオンと同じ名前）のクラスを作成し `Pladdon` を継承します。`plugin.yml` を作成する代わりに、コンポーネントはアノテーションを使用して宣言されます。アノテーションは以下のようになります。ApiVersion は必要に応じて最新のサーバーバージョンに更新できます。

```
@Plugin(name="Pladdon", version="1.0")
@ApiVersion(ApiVersion.Target.v1_16)
@Dependency(value = "BentoBox")
public class LevelPladdon extends Pladdon {
    private Addon addon;
    
    @Override
    public Addon getAddon() {
        if (addon == null) {
            addon = new Level();
        }
        return addon;
    }
}
```

定義すべき唯一のメソッドは `getAddon()` メソッドで、アドオンのインスタンスを返す必要があります。このメソッドが複数回呼び出された場合に重複が作成されないよう、1 つのインスタンスのみを返すようにしてください。

これが完了すると、アドオンはプラグインと同様に読み込まれ、他のプラグインからアクセスできるようになります。




