# Boxed コマンド

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/boxed`（/bx, /boxも可能） | `boxed.` |
| 管理者 | `/boxadmin` | `boxed.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド

BoxedはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/boxed`に、`/[admin_command]`を`/boxadmin`に、`[gamemode]`を`boxed`に置き換えてください。例えば：

```
/boxed              アイランドに移動するか、新しく作成する
/boxed team invite <player>
/boxed settings
/boxadmin info <player>
/boxadmin why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。

## Boxedのみのコマンド

| コマンド | 説明 | パーミッション | デフォルト |
|---|---|---|---|
| `/boxadmin place <x> <y> <z> <rotation> <mirror> <no mobs>` | Place a structure at a location | `boxed.admin.place` | オペレーター |

## アドオンコマンド

アドオンは`/boxed`および`/boxadmin`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/boxed level`または[Challenges](../../addons/Challenges/index.md)の`/boxed challenges`があります。各アドオンのページを参照してください。
