# AcidIsland コマンド

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/ai` | `acidisland.` |
| 管理者 | `/acid` | `acidisland.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド

AcidIslandはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/ai`に、`/[admin_command]`を`/acid`に、`[gamemode]`を`acidisland`に置き換えてください。例えば：

```
/ai              アイランドに移動するか、新しく作成する
/ai team invite <player>
/ai settings
/acid info <player>
/acid why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。

## AcidIslandのみのコマンド

| コマンド | 説明 | パーミッション | デフォルト |
|---|---|---|---|
| `/ai about` | 著作権およびライセンス情報を表示 | `acidisland.island` | 全員 |

## アドオンコマンド

アドオンは`/ai`および`/acid`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/ai level`または[Challenges](../../addons/Challenges/index.md)の`/ai challenges`があります。各アドオンのページを参照してください。
