## **Greenhouses の権限**

| **権限**                            | **説明**                                                                                                                                              | **デフォルト** |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| [gamemode].greenhouses.player       | プレイヤーコマンドへのアクセスを付与します。[gamemode] はゲームモード名に置き換えてください（例: bskyblock、acidisland、aoneblock など）。             | true           |
| [gamemode].greenhouses.admin        | 管理者コマンドへのアクセスを付与します                                                                                                                | op             |
| [gamemode].greenhouses.admin.list   | グリーンハウスの一覧表示を許可します（1.10.0 以降）                                                                                                   | op             |
| [gamemode].greenhouses.admin.info   | グリーンハウスの詳細表示を許可します（1.10.0 以降）                                                                                                   | op             |
| [gamemode].greenhouses.admin.delete | グリーンハウスのレコード削除を許可します（1.10.0 以降）                                                                                               | op             |
| [gamemode].greenhouses.admin.tp     | グリーンハウスへのテレポートを許可します（1.10.0 以降）                                                                                               | op             |
| [gamemode].greenhouses.admin.verify | グリーンハウスをレシピと照合して再チェックすることを許可します（1.10.0 以降）                                                                         | op             |
| [gamemode].greenhouses.admin.reload | biomes.yml とグリーンハウスデータベースのリロードを許可します（1.10.0 以降）                                                                          | op             |
| greenhouses.biome.nether            | ネザーバイオームへのアクセスを付与します。バイオームごとの権限は `biomes.yml` で設定します — [Greenhouses ページ](index.md#permissions)を参照してください。 | true           |
