= 目次
:toc:

= はじめに
ゲームモードはBSkyBlockやAcidIslandのようなアドオンです。ゲームモードアドオンたらしめるのは、BentoBoxに*ワールド*を作成して登録し、BentoBoxにWorldSettingsクラスオブジェクトを提供することです。

現在、BentoBoxに登録されるワールドはオーバーワールドである必要がありますが、ワールドが登録されると、関連するネザーとエンドのワールドもこのゲームモードアドオンに属します。

これがどのように機能するかを示すために、BSkyBlockのコード（わかりやすくするためにいくつかの行を削除）を見てみましょう：

[source,java]
----
    @Override
    public void onLoad() {
        // Save the default config from config.yml
        saveDefaultConfig();
        // Load settings from config.yml. This will check if there are any issues with it too.
        settings = new Config<>(this, Settings.class).loadConfigObject();
        // Load or create worlds
        bsbWorlds = new BSkyBlockWorld(this);
    }
----

コメントはかなり明確ですが、最初の2つの呼び出しはconfig.ymlファイルと設定のセットアップです。この場合、コメント付きのYAMLファイルの動的保存を可能にするBentoBox Configuration APIのConfigクラスを使用しています。これは強力なConfig APIです。使用したくない場合は使用する*必要はありません*。代わりに通常のBukkitスタイルのconfigシステムを使用できます。config.ymlファイルを自動的に最新の状態に保てるため使用しました。

= Settingsクラス

Settingsクラスを見てみましょう（わかりやすくするためにいくつかの行を削除）：

[source,java]
----
@StoreAt(filename="config.yml", path="addons/BSkyBlock") // Explicitly call out what name this should have.
@ConfigComment("BSkyBlock Configuration [version]")
@ConfigComment("This config file is dynamic and saved when the server is shutdown.")
@ConfigComment("You cannot edit it while the server is running because changes will")
@ConfigComment("be lost! Use in-game settings GUI or edit when server is offline.")
@ConfigComment("")
public class Settings implements DataObject, WorldSettings {

    @ConfigComment("Allow obsidian to be scooped up with an empty bucket back into lava")
    @ConfigEntry(path = "general.allow-obsidian-scooping")
    private boolean allowObsidianScooping = true;

...
----

ここでは、クラス宣言の前に多くのアノテーションが見え、その後にフィールド宣言の周りにさらにアノテーションがあります。1つずつ見ていきましょう：

. クラスの前の@StoreAtアノテーションは、このconfigファイルが保存される場所を定義します。BentoBoxプラグインのデータフォルダからの相対パスです。ファイルはBentoBoxフォルダ内にのみ保存される必要があります。この場所を明示的に宣言することが非常に重要です！
. @Commentアノテーションは、YAMLファイルにコメント行を追加するために使用されます。「[version]」プレースホルダーはアドオンのバージョン番号に自動的に置き換えられます。
. クラスはDataObjectとWorldSettingsの両方を実装する必要があります。DataObjectはクラスをデータベースに保存できるようにするためのもの（BBConfigを介して）で、WorldSettingsはこれがゲームモードアドオンであるためです
. フィールド「allowObsidianScooping」はデフォルト値とともに宣言され、コメントアノテーションと@ConfigEntryアノテーションがあります。後者はこの値がYAMLファイルのどこに配置されるかを定義するために使用されます。YAMLエントリは@ConfigEntryが別の場所に配置することを強制しない限り、一般的にコードで書かれているのと同じ順序で配置されることに注意してください。
. フィールドが宣言された後、これらのフィールドのゲッターとセッターも作成する必要があります。（コードでは省略）

WorldSettingインターフェースを実装することで、必須のワールド設定に対していくつかのゲッターを@Overrideする必要があることに注意してください。BSkyBlockのSettingsクラスでは、ほぼすべてがconfigファイルからロードされます。1つの例外は*Optional<Addon> getAddon()*です。これはアドオンインスタンスを返す必要があります。現在、アドオンがこれを設定する必要があります。将来的にはBentoBoxが設定するかもしれません。

= BentoBoxへのワールドの登録

次に、上記で述べたBSkyBlockWorldクラスをより詳しく見てみましょう。このクラスは主に3つのことを行います：

. BSkyBlockのワールドを作る（ワールドを作成してジェネレーターを定義する）
. メインオーバーワールドとSettingsクラスをBentoBoxに登録する
. IslandCreateクラスで新しいアイランドを作成する際に使用されるschemsを登録する

これを行う方法：

[source,java]
----
// Create the world if it does not exist
islandWorld = WorldCreator.name(worldName).type(WorldType.FLAT).environment(World.Environment.NORMAL)
    .generator(new ChunkGeneratorWorld(addon)).createWorld();

// Register the world and settings with BentoBox
addon.getPlugin().registerWorld(islandWorld, addon.getSettings());

// Make the nether and end worlds if required (not shown)

// Load schematics
addon.getPlugin().getSchemsManager().loadIslands(islandWorld);
----

このコードで、*addon*はアドオンインスタンスです。getPlugin()はBentoBoxを取得するために使用され、registerWorld()はワールドを登録するために使用されます。ネザーとエンドのワールドはBentoBoxに登録*しない*ことに注意してください。オーバーワールドのみを登録します。BentoBoxは関連するネザーまたはエンドがあれば、それらもアドオンが所有していると仮定します。

schemsについては（BentoBoxの独自スキーマティックファイルフォーマット）、アドオンのschemsフォルダに各ワールドのデフォルトアイランド用のschemsが必要です。以下のように命名する必要があります：

* island.schem（必須）
* nether-island.schem（オプション）
* end-island.schem（オプション）

schemを作るには、BentoBoxのschemコマンド（またはBSkyBlockやAcidIslandのschemコマンド）を使用してください。

= コマンドの登録

ワールド、関連するワールド/ゲームモード設定、schemを登録した後、次のステップはアドオンに何かをさせることです。コマンドが必要な場合は、CompositeCommandを拡張して作ることができます。BSkyBlockがトップレベルコマンド*/island*とその下のサブコマンドをどのように登録するかを見てみましょう：

[source,java]
----
public class IslandCommand extends CompositeCommand {

    public IslandCommand(BSkyBlock addon) {
        super(addon, "island", "is");
    }

    @Override
    public void setup() {
        setOnlyPlayer(true);
        // Permission
        setPermissionPrefix("bskyblock");
        setPermission("island");
        setWorld(((BSkyBlock)getAddon()).getIslandWorld());
        // Set up subcommands
        new IslandAboutCommand(this);
        new IslandCreateCommand(this);
        new IslandGoCommand(this);
        new IslandResetCommand(this);
        new IslandSetnameCommand(this);
        new IslandResetnameCommand(this);
        new IslandSethomeCommand(this);
        new IslandSettingsCommand(this);
        new IslandLanguageCommand(this);
        new IslandBanCommand(this);
        new IslandUnbanCommand(this);
        new IslandBanlistCommand(this);
        // Team commands
        new IslandTeamCommand(this);
    }
----

コマンドを登録するためのキーとなる行は：

```
super(addon, "island", "is");
```

これはBentoBoxに「/island」がBSkyBlockアドオンのトップレベルコマンドで、「/is」というエイリアスを持つことを伝えます。次にsetup()メソッドで、いくつかの非常に重要な（トップレベルコマンドには必須の）宣言があります：

```
setWorld(((BSkyBlock)getAddon()).getIslandWorld());
```

これは非常に重要です。このコマンドが動作するワールドを定義します。すべてのサブコマンドはgetWorld()メソッドを使用してこれを参照します。

その後、コマンドはいくつかのサブコマンドをインスタンス化し、自身をパラメーターとして渡します。これらのクラスはそのパラメーターをそれぞれのsuper()呼び出しの親として使用します。

= まとめ

以上が新しいゲームモードタイプのアドオンを作成する場合に行うべきことです。引き続きAPIの作業を行っているため、将来的にはいくつかのことがより簡単に達成できるようになるかもしれません。
