# BentoBoxブループリント仕様

**バージョン1**

!!! warning "非推奨"
    このページは履歴参考のために保存されています。現在の完全な仕様 — ブループリント、ブロック、エンティティ、バンドルのすべてのフィールド、および検証用の公開JSON Schema — は[ブループリントファイルフォーマット](Blueprint-Format.md)ページです。

このドキュメントの「MUST」「MUST NOT」「REQUIRED」「SHALL」「SHALL NOT」「SHOULD」「SHOULD NOT」「RECOMMENDED」「MAY」「OPTIONAL」というキーワードは[RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)に記載されているように解釈されます。

## はじめに

この仕様は、シリアライゼーションおよびディスクまたはJSONベースデータベースへの保存を目的とした[Minecraft](https://minecraft.net)ワールドのリージョン（ブロックとエンティティで構成される）を記述するフォーマットを定義します。プラットフォーム、バージョン、様々な修正状態での最大限の相互互換性を可能にするように設計されています。

BentoBoxブループリントフォーマットの目標は、Minecraftワールドのリージョンをディスクまたはユーザーが選択したストレージメソッドにシリアライズして後でワールドに戻す機能を、シリアライズおよびデシリアライズ機能を提供するためのサードパーティソフトウェアやプラグインに依存せずに提供することです。

## リビジョン履歴

| バージョン | 日付 | BentoBoxバージョン | 説明 |
|---|---|---|---|
| 1 | 2019-06-09 | [1.5.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/1.5.0) | 初期バージョン、BentoBox Schemフォーマットの派生 |
| 1.1 | 2026 | 2.x | ストレージフォーマットが圧縮（zip）バイナリからプレーンJSONに変更；`.blueprint`が主要な拡張子になりました；レガシーの`.blu`（zip）ファイルは後方互換性のため引き続き読み込み可能 |

## 定義

### <a name="defMaterial"></a>マテリアル（Material）

[マテリアル](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html)は[Bukkit API](https://dev.bukkit.org/)が提供するIDで、ブロックやアイテムのリテラルタイプを定義します。光、透明度、表示などのクライアント側のさまざまなレンダリングオプションに影響します。実際の対応するNamespacedKeyへのプログラム的なショートカットを表します。

## 仕様

### フォーマット

この仕様で規定された構造は、ユーザーが選択したストレージメソッドに[JavaScript Object Notation](https://json.org)（JSON）フォーマットを使用して永続化されます。BentoBox 2.x以降、ブループリントファイルは`.blueprint`ファイル拡張子を持つ**プレーン（非圧縮）JSON**として保存されます。

レガシーブループリントファイルは`.blu`拡張子を持つzip（圧縮）バイナリフォーマットを使用していました。BentoBoxは後方互換性のため引き続き`.blu`ファイルを読み込みますが、新しく保存されるブループリントはすべて`.blueprint`プレーンJSONフォーマットを使用します。

この仕様を使用するファイルは以下のいずれかのファイル拡張子を使用しなければなりません：
* `.blueprint` — プレーンJSON（現在の推奨）
* `.blu` — zip/圧縮JSON（レガシー）

仕様内のすべてのフィールド名は**大文字小文字を区別します**。

### スキーマ

#### フィールド

| フィールド名 | 型 | 説明 |
|---|---|---|
| name | `String` | ブループリントの表示名 |
| icon | `String` | ゲーム内でブループリントをアイコンとして表すアイテムの[マテリアル](#defMaterial) |
| attached | `Array` | |
| entities | `Array` | |
| blocks | `Array` | |
| xSize | `integer` | |
| ySize | `integer` | |
| zSize | `integer` | |
| bedrock | `Array` | |
