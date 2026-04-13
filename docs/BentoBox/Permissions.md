# BentoBoxパーミッション

ここに記載されているパーミッションはBentoBox用です。アドオンは独自のパーミッションを登録します。

**BentoBoxパーミッション（1.6.0以降）**

| パーミッション | 親パーミッション | デフォルト値 | 説明 |
|------------------------|-------------------|---------------|----------------------------------------|
| bentobox.admin         |                   | op            | ほとんどのBentoBoxコマンドの使用を許可します |
| bentobox.admin.catalog | bentobox.admin    | op            | /bentobox catalogの使用を許可します |
| bentobox.admin.locale  | bentobox.admin    | op            | /bentobox localeの使用を許可します |
| bentobox.admin.manage  | bentobox.admin    | op            | /bentobox manageの使用を許可します |
| bentobox.admin.migrate | bentobox.admin    | op            | /bentobox migrateの使用を許可します |
| bentobox.admin.reload  | bentobox.admin    | op            | /bentobox reloadの使用を許可します |
| bentobox.about         |                   | true          | /bentobox aboutの使用を許可します |
| bentobox.version       |                   | true          | /bentobox versionの使用を許可します |
