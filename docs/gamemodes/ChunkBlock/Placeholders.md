# ChunkBlock プレースホルダー

ChunkBlockはAOneBlockエンジンから継承されたマジックブロックプレースホルダーを登録、すべて`chunkblock_`とプレフィックス、プラス5つの領土プレースホルダーの独自。

!!! tip "5つ、あなたはおそらくあなたのスコアボード上に欲しい"
    - `%chunkblock_island_chunks%` ——チャンク所有
    - `%chunkblock_island_max_chunks%` ——天井
    - `%chunkblock_island_chunk_credit%` ——支出可能なレベル、今
    - `%chunkblock_island_next_chunk_level%` ——次のチャンク買うためのアイランドレベル
    - `%chunkblock_island_ring%` ——中央からどのくらい領土が到達

    `credit`と`chunks`一緒に進行全体が一目で：*「9チャンク、3支出。」*

プレースホルダーが読むプレイヤーの**独自**アイランドは、彼らが立つアイランドを解決、誰かの他。`visited_island_*`バリエーションプレイヤーは現在いるアイランドを読む。

{{ placeholders_bundle(gamemode_name="chunkblock") }}
