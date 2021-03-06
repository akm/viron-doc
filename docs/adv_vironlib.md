---
id: adv_vironlib
title: node-vironlib
---

APIサーバーを迅速に構築するための手助けとして [node-vironlib](https://github.com/cam-inc/node-vironlib) を公開しています。

node-vironlibは、認証や監査ログ取得等Vironの基本機能をライブラリとして提供するものです。

[example-emailのvironlib設定箇所](https://github.com/cam-inc/viron/blob/develop/example-email/shared/context.js#L51)

`new VironLib()` に設定を渡すことで初期化されたvironlibインスタンスが生成されます。

すべての設定を渡すと最も簡単にvironlibの全機能を利用することができますが、
独自で実装を行いたい場合は設定を渡さないことで機能をオフにすることができます。

| property name | type | required | description |
| ------------- | ---- | -------- | ----------- |
| account | Object | no | アカウント設定（管理ユーザー自身によるパスワード変更機能）のコントローラ |
| account.admin_users | Sequelize#Model | yes | `admin_users` モデル |
| acl | Object | no | `Access-Control` レスポンスヘッダを付加するミドルウェア |
| acl.allow_origin | String | no | `Access-Control-Allow-Origin` に設定する値 |
| acl.allow_headers | String | no | `Access-Control-Allow-Headers` に設定する値 |
| acl.expose_headers | String | no | `Access-Control-Expose-Headers` に設定する値 |
| audit_log | Object | no | 監査ログを取得するミドルウェア、および閲覧用のコントローラ |
| audit_log.audit_logs | Sequelize#Model | yes | `audit_logs` モデル |
| audit_log.unless | Object | no | 監査ログ取得を除外する設定 [express-unless](https://github.com/jfromaniello/express-unless) |
| admin_user | Object | no | 管理ユーザー情報のコントローラ | 
| admin_user.admin_users | Sequelize#Model | yes | `admin_users` モデル |
| admin_user.default_role | String | yes | 管理ユーザーが追加された際に付与される初期権限ID |
| admin_role | Object | no | 管理権限をチェックするミドルウェア、および管理権限のコントローラ |
| admin_role.admin_roles | Sequelize#Model | yes | `admin_roles` モデル |
| admin_role.admin_users | Sequelize#Model | yes | `admin_users` モデル |
| admin_role.store | Sequelize | yes | `sequelize` インスタンス |
| admin_role.default_role | String | yes | 管理ユーザーが追加された際に付与される初期権限ID |
| auth | Object | no | メール認証、GoogleOAuth認証に必要なミドルウェア、コントローラ |
| auth.admin_roles | Sequelize#Model | yes | `admin_roles` モデル |
| auth.admin_users | Sequelize#Model | yes | `admin_users` モデル |
| auth.super_role | String | yes | スーパーユーザーの権限ID |
| auth.default_role | String | yes | 管理ユーザーが追加された際に付与される初期権限ID |
| auth.auth_jwt | Object | yes | JWTの設定 |
| auth.auth_jwt.algorithm | String | yes | JWT生成に用いるアルゴリズム ex) "RS512" |
| auth.auth_jwt.claims | Object | yes | JWTに含めるclaimセット |
| auth.auth_jwt.claims.iss | String | yes | JWT発行者の識別子 |
| auth.auth_jwt.claims.aud | String | yes | JWT利用者の識別子 |
| auth.google_oauth | Object | no | GoogleOAuthの設定 |
| auth.google_oauth.client_id | String | yes | GoogleOAuthクライアントID |
| auth.google_oauth.client_secret | String | yes | GoogleOAuthクライアントシークレット |
| auth.google_oauth.redirect_url | String | no | Google認証後に呼び出されるViron側のAPI |
| auth.google_oauth.allow_email_domains | Array<String> | no | 利用を許可するドメインの一覧 |
| autocomplete | Object | no | 汎用オートコンプリートのコントローラ |
| autocomplete.store | Sequelize | yes | `sequelize` インスタンス |
| pager | Object | no | ページャー用ヘルパー関数 |
| pager.limit | Number | yes | 1ページあたりの件数 |
| swagger | Object | no | Swagger取得用コントローラおよびヘルパー関数 |
| swagger.host | String | yes | APIサーバーのホスト名 |
| swagger.store | Sequelize | yes | `sequelize` インスタンス |
| body_completion | Object | no | VironからPOST(PUT)されなかったデータを特定の値で補完するためのミドルウェア |
| body_completion.exclude_paths | Array<String> | no | 補完から除外するパス |
| logger | CustomLogger | no | node-vironlibが利用するロガーインスタンス default) console |
