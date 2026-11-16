# Poseidon コマンド { #poseidon-commands }

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/po` | `poseidon.` |
| 管理者 | `/padmin` | `poseidon.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド { #standard-commands }

PoseidonはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/po`に、`/[admin_command]`を`/padmin`に、`[gamemode]`を`poseidon`に置き換えてください。例えば：

```
/po              アイランドに移動するか、新しく作成する
/po team invite <player>
/po settings
/padmin info <player>
/padmin why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。

## Poseidonのみのコマンド { #commands-only-in-poseidon }

| コマンド | 説明 | パーミッション | デフォルト |
|---|---|---|---|
| `/po about` | 著作権およびライセンス情報を表示 | `poseidon.island` | 全員 |

## アドオンコマンド { #addon-commands }

アドオンは`/po`および`/padmin`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/po level`または[Challenges](../../addons/Challenges/index.md)の`/po challenges`があります。各アドオンのページを参照してください。
