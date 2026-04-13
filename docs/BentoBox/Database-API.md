# はじめに

BentoBoxは開発者向けのデータベースAPIを提供しているため、自分で作成する必要はありません。BentoBoxデータベースは、フラットファイル、MySQL、Mongo、SQLite、PostGreSQL、MariaDBなどにデータを保存するよう選択できます。どれが使用されているか心配する必要はありません。YAMLはデータベースとしてはサポートされなくなりましたが、Config APIを介して設定ファイルには引き続き使用されることに注意してください。

## 哲学

BentoBoxデータベースには「NoSQL」アプローチを採用しています。つまり、シリアライズされたJavaオブジェクトをJSON「ブロブ」としてデータベースに保存します。データベース内の各テーブルは特定のJavaオブジェクト（アイランド、プレイヤー、チャレンジなど）を保存するために割り当てられ、テーブルの各エントリは1つのオブジェクトです。テーブルには一意のIDとJSONオブジェクトの2つの列があります。PostgreSQLなどのデータベースはこれらのJSONオブジェクトをバイナリ形式で保存でき、このアプローチを効率的に処理できます。

### BentoBox外からデータにアクセスするには？
サポートされているほとんどのデータベース（MySQL、PostgreSQLなど）はJSONデータへのクエリを直接サポートしています。フラットファイルベースのもの（JSONとSQLite）はサポートしていません。したがって、データベースのJSONクエリの作成方法についてはドキュメントを確認してください。

## 方法

クラスをBentoBoxデータベースに保存するには：

1. DataObjectを拡張するクラスを作成する
2. クラスのフィールドを定義する
3. 1つのフィールドは**uniqueId**という名前のStringでなければなりません。これはデータベースがオブジェクトを識別するために使用する一意のID（キー）です
5. データベースに保存したいすべてのフィールドを@Exposeアノテーションで公開する
6. クラスに[ゼロ引数コンストラクター](https://en.wikipedia.org/wiki/Nullary_constructor)があることを確認する
7. すべてのフィールドにゲッターとセッターを作成する — ほとんどのIDEが自動的に行えるはずです

**警告：** クラスの完全なカノニカル名はデータベースのテーブル作成に使用されますが、その名前の最大長は**64文字**のみです。データオブジェクトクラスを定義する際は、パッケージとクラス名が十分に短いことを確認してください。**また**BentoBoxはデータベーステーブルにプレフィックスを持てるため、カノニカル名の合計がプレフィックス用に約60文字以下になるようにしてください。

カスタムフィールドなど一部のフィールドタイプでは、フィールドのデータのシリアライゼーションとデシリアライゼーションを処理する独自のAdapterクラスを定義する必要があるかもしれません。

## 例
```
public class Names implements DataObject {

    @Expose
    private String uniqueId = ""; // name
    @Expose
    private UUID uuid;
    
    public Names() {}
    
    public Names(String name, UUID uuid) {
        this.uniqueId = name;
        this.uuid = uuid;
    }
    
    @Override
    public String getUniqueId() {
        return uniqueId;
    }

    @Override
    public void setUniqueId(String uniqueId) {
        this.uniqueId = uniqueId;        
    }

    /**
     * @return the uuid
     */
    public UUID getUuid() {
        return uuid;
    }

    /**
     * @param uuid the uuid to set
     */
    public void setUuid(UUID uuid) {
        this.uuid = uuid;
    }


}
```

## uniqueID

DataObjectインターフェースの契約では、getUniqueId()とsetUniqueID()メソッドをオーバーライドする必要があります。uniqueIdはデータベース内のデータオブジェクトを識別するために使用される文字列です。典型的なuniqueIdはプレイヤーのUUID（Stringに変換）です。データベースオブジェクトが1つしかない場合は、このuniqueIdを定数にすることができます（例：「TopTen」）。uniqueIdは作成したタイプのデータオブジェクトのスコープ内でのみ一意である必要があります。すべてのデータオブジェクトにわたって一意である必要はありません。

# データベースオブジェクトのインスタンス化

データオブジェクトを作成したら、使用するためにインスタンス化する必要があります。BSkyBlockを最初の引数に、クラスを2番目の引数にして新しいBSBDatabaseオブジェクトを作成することでそれを行います。例えば：

`BSBDatabase<Names> names = new BSBDatabase<>(plugin, Names.class);`

# データベースへのデータ保存

データベースにデータを書き込むには：

1. データベースオブジェクトのインスタンスを作成する（この例ではNamesクラス）
2. コンストラクターまたはセッターを使用してデータを入れる
3. saveObject()メソッドを使用してデータベースに保存する

例えば：

`names.saveObject(new Names(user.getName(), user.getUniqueId()));`

saveObjectメソッドの呼び出しを繰り返すことで複数のオブジェクトをデータベースに保存できます。オブジェクトが以前に保存されたオブジェクトと同じuniqueIdを持つ場合、自動的に上書きされます。

# データベースからのデータロード

データをロードするには2つの方法があります。uniqueIdで特定のレコード（オブジェクト）をロードするか、このタイプのすべてのオブジェクトを一度にロードします。

## 単一オブジェクトのロード

これを行うには、必要なレコードのuniqueIdを知る必要があります。次にuniqueIdを引数にしてloadObjectメソッドを使用します。例えば：

`Names loadedName = names.loadObject("tastybento");`

ロードしたオブジェクトから必要なデータがわかっていて、それが存在することが確実な場合は、直接取得できます：

`UUID uuid = names.loadObject(string).getUuid();`

## すべてのオブジェクトのロード

データベース全体をメモリにロードして常時アクセスできるようにする必要がある場合があります。必要な場合以外は行わないようにしてください。すべてのオブジェクトをロードするには、loadObjects()メソッドを使用します。これらはすべてListとしてロードされます。例えば：

`List<UUID> uuids = names.loadObjects();`

データベースからのロードには時間がかかる場合があるため、ゲーム中はメインスレッドで行わないようにしてください。オブジェクトを非同期スレッドでロードできるはずです。

# データベース内のオブジェクト存在確認

オブジェクトが存在するかどうかを確認するには、uniqueIdが必要です。このように確認します：

`return names.objectExists("tastybento") ? "he exists in the db" : "who?";'`

オブジェクトの存在確認も時間がかかる場合があるため、可能であればメインスレッドでは行わないようにしてください。

# データベース内のオブジェクト削除

オブジェクトを削除するにはuniqueIdが必要です。このようにオブジェクトを削除します：

`names.deleteObject("tastybento");`

削除できない場合はコンソールにエラーをログしますが、それ以外は静かです。

現在、データベース内のすべてのオブジェクトを削除する方法はありません。

# データベースのクローズ

データベース接続はプラグインが無効化された際に自動クローズするよう設定されていますが、リソースを節約するために接続を明示的にクローズしたい場合は、このメソッドを使用します：

`names.close()`

これにより、接続オブジェクトのデータベースとすべてのJDBCリソースが自動リリースを待たずにすぐに解放されます。

# オブジェクトタイプのサポート

*YAMLデータベースはサポートされなくなりました！*
データベースはGSONを使用してオブジェクトをシリアライズします。これはほとんどの汎用オブジェクトタイプと[ConfigurationSerializable](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/configuration/serialization/ConfigurationSerializable.html)インターフェースを実装するすべてのBukkitクラスを処理します。例えば：

* World
* Location
* Vector（BukkitのVector）
* PotionEffectType
* など

データベースにシリアライズして保存する必要があるオブジェクトを実装する場合は、Bukkitの[ConfigurationSerializable](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/configuration/serialization/ConfigurationSerializable.html)インターフェースを実装してください。
