# addon.ymlファイルの記入方法

## このファイルとは何ですか？

**addon.yml**ファイルは、BSkyBlockがアドオンをロードしようとする際に、アドオンに関する貴重な情報を提供します。このファイルは属性のセットで構成されており、各属性は新しい行に定義され、インデントはありません。

このファイルがないか、正しく記入されていない場合、BSkyBlockはアドオンをロードせず、`INVALID_DESCRIPTION`としてマークします。

## 必須属性

### name

**説明：** このアドオンの名前。

**コード：**
```yaml
name: "MySuperAddon"
```

**注意事項：**
1. すべて英数字とアンダースコア（a-z,A-Z,0-9, \_）で構成される必要があります。
2. スペースはサポートされておらず、自動的にアンダースコアに変換されます。
3. BSkyBlock全体のAPI内でアドオンを識別するために使用されます。
4. ユーザーが`/bsadmin version YourSuperAddon`と入力したときに表示されます。

### main

**説明：** `BSAddon`を拡張するクラスへのアドレス。

**コード：**
```yaml
main: fr.poslovitch.myaddon.MySuperAddon
```

**注意事項：**
1. これはBukkitと同様に、クラスファイル自体を含む完全な名前空間を含む必要があります。したがって、名前空間が`fr.poslovitch.myaddon`で、クラスファイルが`MySuperAddon`という名前の場合、これは`fr.poslovitch.myaddon.MySuperAddon`でなければなりません。

### version

**説明：** アドオンのバージョン。

**コード：**
```yaml
version: 1.0.0
```

**注意事項：**
1. バージョンは任意の文字列ですが、最も一般的なフォーマットはMajorRelease.MinorRelease.FixRelease（例：3.6.1）です。
2. ユーザーが`/bsadmin version YourSuperAddon`と入力したときに表示されます。

## オプション属性

必須属性の他に、BSkyBlockにアドオンに関する詳細情報を提供するのに役立つ属性があります。

これらの属性はオプションです。

### authors

**説明：** このアドオンを作成した開発者全員、または自分だけをリストアップできます。

**コード：**
```yaml
authors: ["Poslovitch", "Tastybento", "you, maybe? :P"]
# アドオンのauthorsリストに私たちのニックネームを追加することを遠慮なくしてください。ありがたく思います！
```

**注意事項：**
1. 開発者にクレジットを与えます
2. ユーザーが`/bsadmin version YourSuperAddon`と入力したときに表示されます。

### description

**説明：** アドオンが提供する機能のわかりやすい説明。

**コード：**
```yaml
description: "It makes you die when you jump. So 2017."
```

**注意事項：**
1. 説明は複数行にわたることができます（_スーパーアドオンが何をするかを説明するために多くのスペースが必要ですから！_）。
2. ユーザーが`/bsadmin version YourSuperAddon`と入力したときに表示されます。

### website

**説明：** プラグインまたは作者のウェブサイト。

**コード：**
```yaml
website: "https://github.com/tastybento/bskyblock"
```

**注意事項：**
1. 専用のウェブサイトがない場合は、アドオンのGitHubリポジトリへのリンクで十分です。
2. ユーザーが`/bsadmin version YourSuperAddon`と入力したときに表示されます。
