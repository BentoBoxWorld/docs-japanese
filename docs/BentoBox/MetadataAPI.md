# BentoBox永続メタデータAPI

BentoBoxには、ユーザー、プレイヤー、またはアイランドにメタデータを永続的に保存できる永続メタデータAPIがあります。
これにより、独自のデータベースストレージを処理する必要のないアドオンが、代わりにこのAPIを使用してデータを保存できます。
例えば、Borderアドオンはユーザーの境界がオンかオフかを記録するシンプルなbooleanを保存するだけでよいです。これをデータベーステーブルに保存するのはオーバーキルなので、代わりにアドオンはこのbooleanをUserクラスを通じてPlayerオブジェクトに配置できます。

## クイック例

### メタデータの設定
文字列キーと保存したいオブジェクトを持つ新しい`MetaDataValue`を提供することでメタデータを設定します。
```
// Place a boolean tag on the user with the value of true and name it Border_state
user.putMetaData("Border_state", new MetaDataValue(true));
```

### メタデータの確認
メタデータは文字列キーを提供することで読み取られます。戻り値は存在するかどうかを確認できる`Optional`です。
```
// Check if the user has the metadata called Border_state
boolean on = user.getMetaData("Border_state").map(md -> md.asBoolean()).orElse(false);
```

`getMetaData`は`Optional`を返すことを覚えておいてください。メタデータキーをチェックして存在しない場合は`Optional.empty()`が返されます。
タグが存在するかどうかを明示的に確認したい場合は`isPresent()`を使用してください：

```
if (user.getMetaData("My_key").isPresent()) {
    // Do something
} else {
    // Do something else
}
```

もちろん、`ifPresent()`メソッドを使用してこのようなアクションを実行することもできます：

```
user.getMetaData("My_key").ifPresent(key -> System.out.println("Your key value is " + key.asInt()));
```

ただし、通常は値を取得して何かをしたいので、`map()`と`orElse()`の構文が最も便利です。

### メタデータの削除
メタデータはキーによってアイランドまたはユーザーから削除できます。

例：
```
island.removeMetaData("Bank_balance");
```
データが実際に削除されたか確認したい場合、`removeMetaData`は削除されたデータの`MetaDataValue`を返すか、存在しなかった場合は`Optional.empty()`/`null`を返します。

## サポートされる値
以下のタイプのメタデータを保存できます：

* String
* Integer
* Float
* Double
* Long
* Short
* Byte
* Boolean

## ゲッター
タイプを指定せずにデータを保存できますが、データを取得する際は正しいゲッターを使用する必要があります。
使用しない場合、データは`null`になります。ゲッターは以下の通りです：

* `asInt()`
* `asFloat()`
* `asDouble()`
* `asLong()`
* `asShort()`
* `asByte()`
* `asBoolean()`
* `asString()`

例：
```
String nameTag = user.getMetaData("Level_nametag").map(MetaData::asString).orElse("No nametag");
```

## キーの命名規則
キーには何でも名前を付けられますが、他のアドオンとの衝突を避けるため、慣例としてキーのプレフィックスにアドオン名を使用します。例：

* Level_name
* Challenges_latestChallenge
* Border_state
* など

## アイランドとプレイヤーオブジェクトのメタデータ
アイランドとプレイヤーオブジェクトはUserクラスと同じメタデータAPIを持ちます。プレイヤーオブジェクトのメタデータを操作することは可能ですが、Userクラスのガイドを通じて行うのが最善です。

アイランドのメタデータはサーバーのシャットダウン時またはデータベースが定期的に保存される際に保存されます。
