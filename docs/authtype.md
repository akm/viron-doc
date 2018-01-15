---
id: authtype
title: 認証方式を追加する
---

Vironサーバでは標準でメールアドレスおよびGoogleOAuthによる認証をサポートしています。  
認証方式を追加する場合は、 `/viron_authtype` に定義を追加する必要があります。

### authtype controller

Vironサーバがサポートしている認証方式をクライアントに返すためのAPIです。   
`api/controller/viron_authtype.js` に `auth_type#list` という名前でcontrollerを実装します。  
下記インタフェースでAPIを実装してください。

```javascript
[
  // メールアドレスとパスワードによる認証。利用しない場合は削除しても良い
  {
    type: 'email', // メールアドレスとパスワードによる独自認証を利用する場合のtype
    provider: 'example-node',
    url: '/signin', // サインインフォームでsubmitする際のリクエストURL
    method: 'POST', // submitする際のリクエストメソッド
  },
  // GoogleOAuthによる認証。利用しない場合は削除しても良い
  {
    type: 'oauth', // OAuth認証を利用する場合のtype
    provider: 'google', // OAuthを提供するプロバイダ。
    url: '/googlesignin',
    method: 'POST',
  },
  // 認証方式ではありませんが、サインアウト時にコールするAPIを定義するために必須です。
  {
    type: 'signout',
    provider: '',
    url: '/signout',
    method: 'POST',
  },
];
```