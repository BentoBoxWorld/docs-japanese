# AOneBlock コマンド { #aoneblock-commands }

| | コマンド | パーミッションプレフィックス |
|---|---|---|
| プレイヤー | `/ob`（/oneblockも可能） | `aoneblock.` |
| 管理者 | `/obadmin`（/oneblockadmin, /obaも可能） | `aoneblock.` |

ゲームモードの`config.yml`内で両方のコマンドの名前を変更できます。

## 標準コマンド { #standard-commands }

AOneBlockはBentoBoxの標準プレイヤーおよび管理者コマンドを使用します。それらはすべてリストされており、パーミッション付きで[コマンドリファレンス](../../BentoBox/Commands.md)にあります。`/[player_command]`を`/ob`に、`/[admin_command]`を`/obadmin`に、`[gamemode]`を`aoneblock`に置き換えてください。例えば：

```
/ob              アイランドに移動するか、新しく作成する
/ob team invite <player>
/ob settings
/obadmin info <player>
/obadmin why <player>
```

詳細については、[プレイヤーガイド](../../BentoBox/Player-Guide.md)および管理者ガイド（[チーム&ランク](../../BentoBox/About/Teams.md)および[アイランド](../../BentoBox/About/IslandManagement.md)など）を参照してください。

## AOneBlockのみのコマンド { #commands-only-in-aoneblock }

| コマンド | 説明 | パーミッション | デフォルト |
|---|---|---|---|
| `/ob count` | ブロック数とフェーズを表示 | `aoneblock.count` | 全員 |
| `/ob phases` | すべてのフェーズのリストを表示 | `aoneblock.phases` | オペレーター |
| `/ob setCount <count>` | すでに到達した値にブロック数を設定する | `aoneblock.island.setcount` | オペレーター |
| `/ob respawnBlock` | 魔法のブロックが消えた場合は復活させる（別名: check） | `aoneblock.respawn-block` | 全員 |
| `/ob bossbar` | フェーズボスバーをオン/オフにする | `aoneblock.island.bossbar` | 全員 |
| `/ob actionbar` | フェーズアクションバーをオン/オフにする | `aoneblock.island.actionbar` | 全員 |
| `/obadmin setcount <name> <count> [lifetime]` | プレイヤーのブロック数を設定する | `aoneblock.admin.setcount` | オペレーター |
| `/obadmin setchest <phase> <rarity>` | 見ているチェストをそのレアリティでフェーズに追加する | `aoneblock.admin.setchest` | オペレーター |
| `/obadmin sanity <phase>` | フェーズのブロック確率チェックをコンソールに出力 | `aoneblock.admin.sanity` | オペレーター |
| `/obadmin phases` | フェーズ順序エディターを開く | `aoneblock.admin.phases` | オペレーター |

## アドオンコマンド { #addon-commands }

アドオンは`/ob`および`/obadmin`にサブコマンドを追加します。例えば[Level](../../addons/Level/index.md)の`/ob level`または[Challenges](../../addons/Challenges/index.md)の`/ob challenges`があります。各アドオンのページを参照してください。
