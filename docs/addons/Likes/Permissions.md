#### LikesAddon の権限（バージョン 1.7.0 時点）

| 権限 | 親権限 | デフォルト値 | 説明 |
|---------------------------------|-----------------------|---------------|------------------------------------------------------|
| [gamemode].likes                |                       | true          | `/[gamemode_user] likes` の使用を許可します |
| [gamemode].likes.top            | [gamemode].likes      | true          | `/[gamemode_user] likes top` の使用を許可します |
| [gamemode].likes.view           | [gamemode].likes      | true          | `/[gamemode_user] likes view` の使用を許可します |
| [gamemode].likes.view.others    | [gamemode].likes.view | op            | `/[gamemode_user] likes view <player>` の使用を許可します |
| [gamemode].likes.bypass-cost    | [gamemode].likes      | op            | いいね/いやいねの支払いをバイパスできます |
| [gamemode].likes.admin          |                       | op            | `/[gamemode_admin] likes` の使用を許可します |
| [gamemode].likes.admin.settings | [gamemode].likes.admin| op            | `/[gamemode_admin] likes settings` の使用を許可します |
| [gamemode].likes.icon.X         |                       |               | プレイヤーのカスタムアイコン（X はマテリアル名）の設定を許可します |
