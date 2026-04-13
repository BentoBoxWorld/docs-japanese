# AOneBlock コマンド

AOneBlockはBSkyBlockと同じコマンドが多くあります。以下はAOneBlock固有のコマンドです:

**注意:** このリストはまだ完成していません。

## 管理者コマンド

* `/obadmin setchest <phase> <rarity>` - 見ているチェストを指定したフェーズとレアリティで設定する
* `/obadmin setcount <name> <count>`: プレイヤーの島のブロック数を設定する
* `/obadmin sanity <phase>`: コンソールにフェーズの確率のサニティチェックを表示する

チェストのレアリティにはCOMMON、UNCOMMON、RARE、EPICが使用できます。

## プレイヤーコマンド

* `/ob count` - 島が現在いるフェーズとカウントを表示する
* `/ob setcount <number>` - 採掘されたブロック数を変更する
* `/ob phases` - フェーズのGUIを表示する
* `/ob bossbar` - フェーズの進捗を表示するボスバーの表示/非表示を切り替える（1.21.2以降、configで`bossbar: true`が必要）
* `/ob actionbar` - フェーズの進捗を表示するアクションバーの表示/非表示を切り替える（1.21.2以降、configで`actionbar: true`が必要）
