# BentoBox Config API

これはYAMLファイル向けのBukkit Config APIを強化するオプションのAPIです。BentoBox Config APIには以下の機能が追加されています：

1. 設定ファイルは保存後もコメントを保持できます
2. アドオンを更新した際に新しい設定で設定ファイルを更新できます
3. configクラスは設定の取得と設定も行う場所です

このAPIを使用したくない場合は、saveDefaultConfig()、getConfig()などの標準Bukkit APIメソッドを使用できます。

## はじめに — 例

新しいプラグイン用のconfigファイルを作りたいとします。おそらく以下のようになります：

```yaml
# This is my config.yml file
# It is for my addon

world:
  # This is the name of the world.
  name: My_world_name
  # Size - minimum is 10, max is 100
  size: 100
```

### ConfigObject
Config APIを使用するには、`ConfigObject`を実装する新しいクラスを作成します：

```java
public class Settings implements ConfigObject {

}
```

このconfigオブジェクトが保存される場所を指定する必要があります。場所はアドオンのデータフォルダに対する相対パスです。

```java
@StoreAt(filename="config.yml") // Explicitly call out what name this should have.
public class Settings implements ConfigObject {

}
```

### @ConfigEntry
次に、configに入れたいデータフィールドを追加する必要があります。そのために`@ConfigEntry`アノテーションを使用します：

```java
@StoreAt(filename="config.yml") // Explicitly call out what name this should have.
public class Settings implements ConfigObject {
    @ConfigEntry(path = "world.name")
    private String worldName = "My_world_name";

    @ConfigEntry(path = "world.size")
    private int worldSize = 100;
}
```

フィールドにはデフォルト値が割り当てられていることに注意してください。

### ゲッターとセッター
次に、これらのフィールドにアクセスするためのゲッターとセッターを追加する必要があります。ゲッターとセッターの名前とパラメーター名は[JavaBeans命名規則](https://www.oreilly.com/library/view/javaserver-pages-3rd/0596005636/ch20s01s01.html)を満たす必要があります：

```java
@StoreAt(filename="config.yml") // Explicitly call out what name this should have.
public class Settings implements ConfigObject {
    @ConfigEntry(path = "world.name")
    private String worldName = "My_world_name";

    @ConfigEntry(path = "world.size")
    private int worldSize = 100;

    public String getWorldName() {
        return worldName;
    }
    public void setWorldName(String worldName) {
        this.worldName = worldName;
    }
    public int getWorldSize() {
        return worldSize;
    }
    public void setWorldSize(int worldSize) {
        this.worldSize = worldSize;
    }
}
```

### `@ConfigComment`
次に、`ConfigComment`アノテーションを使用してコメントを追加できます：

```java
@StoreAt(filename="config.yml") // Explicitly call out what name this should have.
@ConfigComment("This is my config.yml file") // Note that the comment will automatically
@ConfigComment("It is for my addon") // be proceeded with a # and space
public class Settings implements ConfigObject {
    @ConfigEntry(path = "world.name")
    @ConfigComment("This is the name of the world.")
    private String worldName = "My_world_name";

    @ConfigEntry(path = "world.size")
    @ConfigComment("Size - minimum is 10, max is 100")
    private int worldSize = 100;

    public String getWorldName() {
        return worldName;
    }
    public void setWorldName(String worldName) {
        this.worldName = worldName;
    }
    public int getWorldSize() {
        return worldSize;
    }
    public void setWorldSize(int worldSize) {
        this.worldSize = worldSize;
    }
}
```

### ロードと保存

Addonクラスでconfigをロードするには：

```java
Settings settings = new Config<>(this, Settings.class).loadConfigObject();
```

Addonクラスでconfigを保存するには：

```java
Settings settings = new Settings();
new Config<>(this, Settings.class).saveConfigObject(settings);
```

アドオンが設定をロードしてからすぐに保存するのは良い習慣です。これにより設定ファイルが最新のオプションとコメントで更新されます。初期configを作成するには、アドオンのjarに保存されているデフォルトconfig.ymlを保存するAddonの`saveDefaultConfig()`メソッドを使用してください。config.yml以外のファイルを使用している場合は、`saveResource(resourcePath, replace)`メソッドを使用できます。

### デフォルト設定ファイル
アドオンjarにデフォルトのconfig.ymlファイルを設定します。次にアドオンで標準の`saveDefaultConfig()`メソッドを使用してファイルシステムに保存します。全体的なアプローチは以下の通りです：

1. saveDefaultConfig() - 存在しない場合、jarからデフォルトのconfig.ymlを保存します。
2. Config APIを使用してconfigをロードし、管理者の設定を取得します
3. Config APIを使用してconfigを保存し、config.ymlを最新の設定オプションとコメントで更新します

以上です！このAPIの詳細については、JavaDocsをお読みください。
