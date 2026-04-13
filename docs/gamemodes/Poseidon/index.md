# 🌊 Poseidon

作成・メンテナンス: [tastybento](https://github.com/tastybento)

**Poseidon**はMinecraft向けの没入型水中サバイバル体験です。謎の難破船事故の後、水中で呼吸できるという不思議な能力に目覚めたあなた——しかし落とし穴があります。サメのように、生き残るためには動き続けなければなりません。

深海の廃墟から輝くサンゴの都市まで、Poseidonは海があなたの唯一の拠り所となる世界で、生き残り、建築し、探索することに挑戦させます——あなたが灼熱の陸地に足を踏み入れる勇気を持つまで。

## 🐚 特徴

- 🧭 **全く新しいサバイバル**: 動き続けることが生存の鍵。止まれば危険が忍び寄ります。
- 🏰 **水中王国建築**: 深海にサンゴで覆われた城や水中都市を建設しましょう。
- ⚔️ **挑戦的な遭遇**: 執拗なドラウンド、海のモンスター、そして海底に眠る秘密に立ち向かいます。
- 🌋 **水没したネザー**: 水に沈んだ冥界を探索しましょう。
- 📖 **ロア主導のチャレンジ**: 複数レベルのクエストをクリアして、Poseidonの世界の謎を解き明かしましょう。
- 🏝️ **カスタムスターター島**: 始まり方を選べます——シンプルな難破船、小さなモニュメント、またはサンゴに彩られた壮大な領域。

## 🔧 セットアップ手順

> 推奨: Poseidonの全機能を活用するには[BentoBox Challengesアドオン](https://github.com/BentoBoxWorld/Challenges)と共にインストールしてください。

1. **Poseidonアドオンをダウンロードしてインストールします。**
2. **`/plugins/BentoBox/addons/`フォルダに配置します。**
3. **サーバーを起動します** — Poseidon用の新しいワールドが自動的に生成されます。
4. **事前生成を実行させます。** プレイヤーがオンラインでない時のみ機能します。事前生成されるチャンクが多いほど、パフォーマンスが向上します。
5. **ログインしてチャレンジを設定します**:
    - `/padmin challenges`を使用する
    - 🕸️ウェブアイコンをクリックして**Poseidon Challenges**をダウンロードする
6. **スターター島を選択します**:
    - サンゴ付き難破船
    - 小型モニュメント付き難破船
    - 小型と大型モニュメント付き難破船
    - `/padmin bp`を使って島をカスタマイズする
7. **（オプション）** `config.yml`を調整するか、管理者設定GUIを使用する。
    - 大きな変更はデータベースの削除とワールドのリセットが必要な場合があります。

## ⚠️ 注意事項

- エンドワールドは現在**未整備**です。
- 島が事前生成されていない場合、ラグが発生することがあります。プレイヤーを招待する前に事前生成を完了させてください。

## ✅ 互換性

| 機能             | サポート状況                         |
|---------------------|------------------------------------|
| Minecraftバージョン   | ✅ 1.21.4以降（旧バージョンとの互換性なし） |
| BentoBoxバージョン    | ✅ 3.3.0以降                  |
| Javaバージョン        | ✅ Java 21                         |

## プレイヤーコマンド

デフォルトのプレイヤーコマンドは`/poseidon`または略して`/po`です。

## Config.yml

config.ymlファイルはPoseidon専用の設定セクションと、より汎用的なワールドおよび島の設定で構成されている点で他のゲームモードと似ています。Poseidonでは、島は「レルム」と呼ばれます。Poseidon固有の設定は以下の通りです:

```
poseidon:
  air-effect:
    # The time a player can be out of the water without suffering in seconds.
    grace-period: 3
    # Damage per second from being in the air.
    damage: 2
    # The time drinking water will prevent damage from air in seconds. Drinking water is the same as drinking a water breathing potion.
    water-effect-time: 30
  # Chance that water mobs will ignore posiedon's children. In percent.
  # Makes game easier..
  water-mob-ignore: 50
```

## パーミッション

パーミッションの一覧は[こちら](Permissions)をご覧ください。

## コマンド

コマンドの一覧は[こちら](Commands)をご覧ください。

## プレースホルダー

プレースホルダーの一覧は[こちら](Placeholders)をご覧ください。

## 翻訳

{{ translations("Poseidon") }}
