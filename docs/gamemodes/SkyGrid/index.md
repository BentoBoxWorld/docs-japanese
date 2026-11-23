# SkyGrid

**SkyGrid**は、すべての方向に4ブロック間隔でブロックが点在する浮遊マップです。ブロックとブロックの間はすべて空気——足を踏み外せばアウトです。オリジナルSkyBlockの作者SethBlingが2012年に公開し、Minecraftで最も人気のあるマップのひとつです。

攻略目標や生き残りのテクニックはオンラインで豊富に見つかりますので、ぜひ参考にしてください！

作成・メンテナンス: [tastybento](https://github.com/tastybento)。

{{ addon_description("SkyGrid") }}

## インストール

0. BentoBoxをインストールし、データフォルダを生成するためサーバーを少なくとも1回起動します。
1. このjarをBentoBoxプラグインのaddonsフォルダに配置します。
2. サーバーを再起動します。
3. アドオンがワールドとデータフォルダを作成し、フォルダ内にconfig.ymlが生成されます。
4. サーバーを停止します。
5. config.ymlを好みに合わせて編集します。
6. ワールドの生成に関わる設定を変更した場合は、初回起動で作成されたワールドフォルダを削除します。
7. サーバーを再起動します。

## 設定

SkyGrid の `config.yml` には、各ワールドのグリッドを構成するブロックが、それぞれの重みとともに記載されています。最新のファイルは[こちら](https://github.com/BentoBoxWorld/SkyGrid/blob/master/src/main/resources/config.yml)です。

### スポナーのモブ { #spawner-mobs }

SkyGrid 2.3.0 以降では、グリッドのスポナーから出てくるモブを選べます。ワールドごとに個別のリストがあり、形式は `EntityType: weight` です：

| ワールド | リスト |
|---|---|
| オーバーワールド | `world.spawners` |
| ネザー | `world.nether.spawners` |
| エンド | `world.end.spawners` |

```yaml
world:
  end:
    spawners:
      ENDERMAN: 45
      ENDERMITE: 54
      SHULKER: 1
```

- モブは重みに比例して選ばれます。この例では、エンドのスポナー 100 個のうち 1 個がシュルカーのスポナーになります。
- 特定の種類のスポナーが作られないようにするには、そのモブを削除するか、重みを `0` に設定します。例えば、`world.spawners` から `VILLAGER` と `IRON_GOLEM` を削除します。
- スポナーを一切置かないようにするには、そのワールドのブロックリストから `SPAWNER` を削除します。
- リストが空の場合、SkyGrid は組み込みのリストを使用し、それをファイルに書き込みます。
- `ARROW` など、スポナーに入れられないモブはスキップされ、コンソールに警告が表示されます。

変更は、その後に生成されるチャンクにのみ反映されます。

### グリッドの高さと位置合わせ { #grid-height-and-alignment }

グリッドのブロックは 4 ブロックごとに配置されます。2.3.0 以降、`world.skygrid-height` は最も近い 4 の倍数に丸められる（最大 252）ため、各プレイヤーのエリアの中心がグリッドの層に重なります。

`world.start-x`、`world.start-z`、`world.space-around-players` も 4 の倍数にしてください。4 の倍数でない場合、SkyGrid は警告をログに出力しますが、値は変更しません。変更すると、既存のワールドのすべてのエリアが移動してしまうためです。

## パーミッション

パーミッションの一覧は[こちら](Permissions)をご覧ください。

## コマンド

コマンドの一覧は[こちら](Commands)をご覧ください。

## プレースホルダー

プレースホルダーの一覧は[こちら](Placeholders)をご覧ください。

## 変更履歴

??? warning "v2.2.4 の新機能 — ワールド生成の修正"
    **リリース:** 2026-11-05

    互換性：BentoBox API 3.3.1 · Minecraft 1.21.x（Paper 26.3 でテスト済み）· Java 21。

    - 🔺 **グリッドが石と草だらけにならなくなりました。** グリッドの下にバニラの地形が生成され、バニラの地表生成によってブロックが草に置き換えられていました。グリッドの各地点には、設定にあるブロックだけが置かれるようになりました。[PR #88](https://github.com/BentoBoxWorld/SkyGrid/pull/88)
    - 🔺 **チャンクが繰り返されなくなりました。** すべてのチャンクが同じ乱数列から始まっていたため、16 ブロックごとに同じパターンが繰り返されていました。現在は各チャンクが独自の乱数列を使います。[PR #88](https://github.com/BentoBoxWorld/SkyGrid/pull/88)
    - **サトウキビに水が付くようになりました。** 小さな砂岩の水たまりの中に置かれるため、水がその場にとどまります。寒冷バイオームでは水たまりの水が凍ることがあります。[PR #89](https://github.com/BentoBoxWorld/SkyGrid/pull/89)
    - **サボテンと枯れ木が浮かなくなりました。** 砂岩の上の砂の上に立つようになりました。[PR #89](https://github.com/BentoBoxWorld/SkyGrid/pull/89)

    🔺 **既存のワールド：** すでに生成済みのチャンクは変わらないため、古いチャンクと新しいチャンクの境目に目に見える食い違いが生じます。一貫したグリッドにするには、SkyGrid のワールドを削除して再生成させてください — **これによりそれらのワールドのすべてのアイランドが削除されます**。プレイヤーと計画を立て、事前にバックアップを取ってください。

    [Release v2.2.4](https://github.com/BentoBoxWorld/SkyGrid/releases/tag/2.2.4)

!!! warning "v2.3.0 の新機能 — スポナーのモブ、プレイヤーがチームとホームのコマンドを使用可能に"
    **リリース:** 2026-11-22

    互換性：BentoBox API 3.3.1 · Minecraft 1.21.x および 26.x · Java 21。

    - ⚙️ **スポナーのモブを設定可能に。** 新しいリスト `world.spawners`、`world.nether.spawners`、`world.end.spawners` で、スポナーに入るモブとそれぞれの出現しやすさを設定します。既存の設定には、これまでと同じ確率で追加されます。[スポナーのモブ](#spawner-mobs)を参照してください。[PR #94](https://github.com/BentoBoxWorld/SkyGrid/pull/94)
    - ⚙️ **グリッドの高さがグリッドに揃うように。** `skygrid-height` は最も近い 4 の倍数に丸められます（最大 252）。グリッド自体は変わりませんが、プレイヤーのスポーン地点が最大 2 ブロック移動することがあります。`start-x`、`start-z`、`space-around-players` が 4 の倍数でない場合、SkyGrid は警告を出します。[グリッドの高さと位置合わせ](#grid-height-and-alignment)を参照してください。[PR #94](https://github.com/BentoBoxWorld/SkyGrid/pull/94)
    - 🔺 **プレイヤーがチームとホームのコマンドを使えるように。** 12 個のプレイヤー用パーミッションが宣言されていなかったため、オペレーターしか持っていませんでした。対象は、チームの `invite`、`accept`、`reject`、`kick`、`leave`、`promote`、`setowner`、`info`、`near`、そして `homes`、`renamehome`、`deletehome` です。現在はデフォルトで全員に与えられます。[パーミッション](Permissions.md)を参照してください。[PR #92](https://github.com/BentoBoxWorld/SkyGrid/pull/92)
    - ⚙️ **新規インストール向けの新しいデフォルト設定。** 危険に関わる 8 つの設定がプレイヤーから非表示になり（`TNT_DAMAGE`、`BLOCK_EXPLODE_DAMAGE`、`FIRE_BURNING`、`FIRE_IGNITE`、`FIRE_SPREAD`、`LEAF_DECAY`、`ENDERMAN_TELEPORT`、`SHULKER_TELEPORT`）、`PISTON_PUSH` が記載されてオフになりました。既存のサーバーでは `config.yml` はそのまま保持されます。これらを使いたい場合は、`world.hidden-flags` と `world.flags` にエントリをコピーしてください。[PR #93](https://github.com/BentoBoxWorld/SkyGrid/pull/93)

    🔺 **チームやホームのコマンドを意図的にオペレーターや特定のランクに限定していた場合は、** 制限を残したいパーミッションを、パーミッションプラグインで否定（false に設定）してください。例：`skygrid.island.team.invite`。

    [Release v2.3.0](https://github.com/BentoBoxWorld/SkyGrid/releases/tag/2.3.0)

## 翻訳

{{ translations("SkyGrid") }}
