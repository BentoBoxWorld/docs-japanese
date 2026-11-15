# 言語とメッセージ { #languages-messages }

BentoBoxとそのアドオンのすべてのメッセージ、メニュー、アイテム名は、**ロケールファイル**から来ます。言語ごとに1つのYAMLファイルです。プレイヤーは自分の言語を選択でき、テキスト、色、またはメッセージの表示方法（チャット、アクションバー、タイトル、サウンド）を変更できます。

## 言語 { #languages }

BentoBoxは25の言語で出荷されます。

| 言語 | ファイル | 言語 | ファイル |
|---|---|---|---|
| 英語（デフォルト） | `en-US` | イタリア語 | `it` |
| 中国語（簡体字） | `zh-CN` | 日本語 | `ja` |
| 中国語（繁体字、香港） | `zh-HK` | 韓国語 | `ko` |
| 中国語（繁体字、台湾） | `zh-TW` | ラトビア語 | `lv` |
| クロアチア語 | `hr` | ポーランド語 | `pl` |
| チェコ語 | `cs` | ポルトガル語 | `pt` |
| オランダ語 | `nl` | ポルトガル語（ブラジル） | `pt-BR` |
| フランス語 | `fr` | ルーマニア語 | `ro` |
| ドイツ語 | `de` | ロシア語 | `ru` |
| ハンガリー語 | `hu` | スペイン語 | `es` |
| インドネシア語 | `id` | トルコ語 | `tr` |
| | | ウクライナ語 | `uk` |
| | | ベトナム語 | `vi` |

アドオンはより少ない言語をサポート可能です。各[ゲームモード](../../gamemodes/Comparison.md)および[アドオン](Addons.md)ページは、各言語がどの程度完成しているかを示すテーブルを持っています。

### サーバーのデフォルト言語 { #the-servers-default-language }

新しいプレイヤーはデフォルト言語を見ます。それを選ぶまで。BentoBoxの`config.yml`で設定します、テーブルからファイル名を使用。

```yaml
general:
  default-language: en-US
```

その後、再起動するか`/bentobox reload`を実行します。BentoBoxはプレイヤーのMinecraft言語を自動的に検出しません。

### プレイヤーが言語を選択 { #players-choosing-a-language }

プレイヤーは**`/island language`**（またはゲームモード独自のコマンド）で言語を変更します。インストール済みの言語のメニューが開きます。彼らの選択はBentoBoxおよびすべてのアドオンに適用されます。すべてのゲームモードで。

プレイヤーの言語にメッセージが不足している場合、BentoBoxはサーバーのデフォルト言語を使用し、その後英語を使用します。

## メッセージを変更 { #changing-messages }

ロケールファイルは以下の場所にあります。

| テキスト提供元 | フォルダー |
|---|---|
| BentoBox | `plugins/BentoBox/locales/BentoBox/` |
| ゲームモードまたはアドオン | `plugins/BentoBox/locales/<AddonName>/`。例えば`locales/BSkyBlock/` |

メッセージを変更するには。

1. **見つけます**。言語ファイル（例えば`en-US.yml`）でプレイヤーが見るテキストを検索。
2. **キーを変更せず、テキストを変更します**。キーと字下げを保持します。`[name]`、`[number]`、`[prefix_island]`のような角括弧内のもの、それらのまま。BentoBoxで入力するもの。（`[prefix_island]`はゲームモードの「アイランド」という言葉になります、「洞窟」または「ボックス」など。）
3. `/bentobox reload locales`を実行。

```yaml
commands:
  island:
    create:
      creating-island: "<green>Building your [prefix_island], hang tight...</green>"
```

すべての言語を変更してください。プレイヤーが使用するもの。他のものはまだ古いテキストを表示します。

**更新時、あなたの変更が保持されます。** BentoBoxまたはアドオンが更新されるとき、新しいメッセージはサーバー上のファイルに追加されます。しかしすでに存在するメッセージは上書きされません。つまり、更新がメッセージのワーディングを改善する場合、その行（またはファイル全体）を削除してリロードするまで、それは表示されません。

**メッセージを隠すには**。空の文字列に設定：`creating-island: ""`。空のメッセージは送信されません。

**翻訳欠落をチェックするには**。`/bentobox locale`を実行。英語と各言語ファイルを比較します。BentoBoxとすべてのアドオン。翻訳不足を報告。

## 色と書式 { #colours-and-formatting }

メッセージは[MiniMessage](https://docs.advntr.dev/minimessage/format.html)タグを使用。

```yaml
example: "<green>Welcome to the island!</green>"
example: "<bold><red>Warning!</red></bold> Something happened."
example: "<gradient:gold:yellow>Island Name</gradient>"
```

古いスタイルの色コード（`&a`、`&l`、`§c`）はまだ動作。

## メッセージの表示方法 { #how-a-message-is-shown }

デフォルトでメッセージはチャットに移動。別の場所に表示するにはタグで開始。

| タグ | メッセージを表示 |
|---|---|
| `[actionbar]` | ホットバーの上 |
| `[title]` | 画面中央の大きなタイトルとして。`[subtitle]`を追加して、小さな行の下にテキストを配置 |
| `[sound:name:volume:pitch]` | サウンドも再生。ボリュームとピッチはオプション。アンダースコア付きのMinecraftサウンド名を使用。例えば`entity_experience_orb_pickup` |

```yaml
example: "[actionbar]Teleporting..."
example: "[title]Teleporting...[subtitle]Wait a second."
example: "[sound:entity_experience_orb_pickup:1:1][title]Teleporting...[subtitle]Wait a second."
```

コンソールへのメッセージは常にコンソールログに移動。

### クリック可能なメッセージ { #clickable-messages }

メッセージ内のどこかに追加してメッセージ全体をクリック可能にするか、ホバーでテキストを表示。

| タグ | 効果 |
|---|---|
| `[run_command: /command]` | クリックするとコマンドを実行 |
| `[suggest_command: /command]` | クリックするとチャットボックスにコマンドを配置 |
| `[open_url: https://...]` | クリックするとリンクを開く |
| `[copy_to_clipboard: text]` | クリックするとテキストをコピー |
| `[hover: text]` | プレイヤーがメッセージにホバーするとテキストを表示 |

```yaml
example: "You're not on your island. Click to go home![run_command: /island go][hover: Teleport home]"
```

## メニュー テキスト { #menu-text }

メニュータイトルとボタンテキストもロケールファイル内。メニューテンプレートから参照。[メニューのカスタマイズ](../../Tutorials/generic/Customizable-GUI.md#change-the-title-or-button-text)を参照。

## 翻訳の修正または追加 { #fixing-or-adding-translations }

翻訳はAI支援で作成され、コミュニティによって修正。誤りを見つけた場合は、プロジェクトのGitHubリポジトリのロケールファイルで修正してプルリクエストを開くか、[Discord](https://discord.bentobox.world)で教えてください。ガイドラインと各プロジェクトの翻訳状態については、[BentoBoxの翻訳](../Translate-BentoBox-and-addons.md)を参照。

## トラブルシューティング { #troubleshooting }

**自分の変更が表示されません。**
`/bentobox reload locales`を実行。編集したプレイヤーの言語と右のフォルダーを確認（BentoBoxの独自メッセージは`locales/BentoBox/`。ゲームモード メッセージは`locales/<GameMode>/`）。

**サーバーが`commands.island...`ではなくメッセージを表示。**
キーがプレイヤーの言語、サーバーのデフォルト言語、英語で欠落。ファイルを削除してBentoBoxに新しいコピーを書かせるか、キーを追加してください。

**更新後、メッセージにまだ古いワーディングがあります。**
ファイルは古いテキストを保持。その行またはファイル全体を削除して`/bentobox reload locales`を実行。

**編集後、YAMLファイルが読み込まれません。**
通常、引用符がないか、インデント が間違い。`:` または `#` を含むメッセージを引用符で囲み、コンソールで行番号をチェック。
