# Request Handler API

**注意：** このAPIは非推奨です。ほとんどのAddonsがPluginsとしてロードされるようになったためです。このページは参照用としてそのまま残されています。

---

このAPIはプラグイン作者がアドオンからデータをリクエストできるようにします。アドオン作者は公開したいデータを正確に決定できます。Javaのクラスローダーのセキュリティルールにより、プラグインはアドオン内のクラスに直接アクセスすることはできません。

## Levelアドオンの例

Levelアドオンは2つのリクエストハンドラー[LevelRequestHandler](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/requests/LevelRequestHandler.java)と[TopTenRequestHandler](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/requests/TopTenRequestHandler.java)を公開しています。以下はプラグインがLevelRequestHandlerからプレイヤーのレベルを取得する方法です：

### LevelRequestHandler

ラベル：`island-level`

入力マップ：

* キー：`world-name` -> String
* 値：`player` -> UUID

    !!! example "コード例"
        ```java
            /**
             * Returns the level of this player's island in the given world.
             * @param playerUUID UUID of the player, not null.
             * @param worldName Name of the world (Overworld) the island is in, not null.
             * @return the player's island level or {@code 0L} if the input was invalid or
             *         if this player does not have an island in this world.
             */
            public long getIslandLevel(UUID playerUUID, String worldName) {
                return (Long) new AddonRequestBuilder()
                    .addon("Level")
                    .label("island-level")
                    .addMetaData("world-name", worldName)
                    .addMetaData("player", playerUUID)
                    .request();
            }
        ```

アドオンが公開しているデータはアドオンのコードまたはドキュメントを確認することで知ることができます。

# アドオンからデータを公開する
データを公開するには、[AddonRequestHandler](https://bentoboxworld.github.io/BentoBox/world/bentobox/bentobox/api/addons/request/AddonRequestHandler.html)を拡張する各要素のクラスを作成します。次にアドオンにリクエストハンドラーを登録します。例えば：

```
        // Register request handlers
        registerRequestHandler(new LevelRequestHandler(this));
        registerRequestHandler(new TopTenRequestHandler(this));
```

ハンドラーはコンストラクターでラベルを定義する必要があります。例えば：

```
    public LevelRequestHandler(Level addon) {
        super("island-level"); // the label is "island-level"
        this.addon = addon;
    }
```

ラベルはアドオン内で一意である必要があります。

次に、マップをパラメーターとして受け取る`handle`メソッドをオーバーライドします：

```
    @Override
    public Object handle(Map<String, Object> map) {
```

マップの内容は定義できますが、Objectはアドオン内の一意のクラスであってはなりません。すべてのプラグインに存在するクラスのみ使用できます。隠れたクラスを参照しようとすると、プラグインは例外を生成します。したがって、整数、long、BukkitのLocation、ワールドなどは問題ありません。

プラグイン作者が使用するため、マップの内容をドキュメント化することは良い習慣です：

```
        /*
            What we need in the map:
            0. "world-name" -> String
            1. "player" -> UUID
            What we will return:
            - 0L if invalid input/player has no island
            - the island level otherwise (which may be 0)
         */
```

その後マップを処理して結果を提供します：

```

        if (map == null || map.isEmpty()
                || map.get("world-name") == null || !(map.get("world-name") instanceof String)
                || map.get("player") == null || !(map.get("player") instanceof UUID)
                || Bukkit.getWorld((String) map.get("world-name")) == null) {
            return 0L;
        }

        return addon.getIslandLevel(Bukkit.getWorld((String) map.get("world-name")), (UUID) map.get("player"));
    }
```

`Object`を返しているため、プラグイン作者は正しい形式にキャストする必要があります。この場合は`long`です。マップの形式エラーからアドオンを保護するために、適切なレベルのパラメーターチェックを行うことが良い習慣です。
