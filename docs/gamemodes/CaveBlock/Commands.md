# CaveBlock コマンド { #caveblock-commands }

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/cave`（/cbも可能） | `caveblock.` |
| 管理者 | `/cbadmin`（/cbaも可能） | `caveblock.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド { #standard-commands }

CaveBlockはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/cave`に、`/[admin_command]`を`/cbadmin`に、`[gamemode]`を`caveblock`に置き換えてください。例えば：

```
/cave              アイランドに移動するか、新しく作成する
/cave team invite <player>
/cave settings
/cbadmin info <player>
/cbadmin why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。

## CaveBlockのみのコマンド { #commands-only-in-caveblock }

| コマンド | 説明 | パーミッション | デフォルト |
|---|---|---|---|
| `/cave about` | 著作権およびライセンス情報を表示 | `caveblock.island` | 全員 |

## アドオンコマンド { #addon-commands }

アドオンは`/cave`および`/cbadmin`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/cave level`または[Challenges](../../addons/Challenges/index.md)の`/cave challenges`があります。各アドオンのページを参照してください。
