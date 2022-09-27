---
title: 外部 OAuth プロバイダーを使用する
description: 外部 OAuth プロバイダーを使用してアプリ ユーザーを認証し、外部ブラウザーに追加する方法について説明します。
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 4892dc23174e34015a02a9afff64269e01871fb5
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027320"
---
# <a name="use-external-oauth-providers"></a>外部 OAuth プロバイダーを使用する

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

更新された `authenticate()` APIを使用して、Google、GitHub、LinkedIn、Facebook などの外部またはサードパーティ (3P) の OAuth プロバイダーをサポートできます。

```JavaScript
function authenticate(authenticateParameters: AuthenticatePopUpParameters): Promise<string>
```

外部 OAuth プロバイダーをサポートするために、以下が `authenticate()` API に追加されています。

* `isExternal` パラメーター
* 既存の `url` パラメーターの 2 つのプレースホルダー値

次の表に、API パラメーター (`AuthenticatePopUpParameters`) とその説明と関数の`authenticate()`一覧を示します。

| パラメーター| 説明|
| --- | --- |
|`isExternal` | パラメーターの種類はブール値です。これは、認証ウィンドウが外部ブラウザーで開くことを示します。|
|`height` |ポップアップの優先高さ。 許容範囲外の場合、値は無視できます。|
|`url`  <br>|認証ポップアップ用の 3P アプリ サーバーの URL。次の 2 つのパラメーター プレースホルダーがあります。</br> <br> - `oauthRedirectMethod`: Pass placeholder in `{}`. This placeholder is replaced by deeplink or web page by Teams platform, which informs app server if the call is coming from mobile platform.</br> <br> - `authId`: このプレースホルダーは UUID に置き換えられます。 アプリ サーバーはそれを使用してセッションを維持します。|
|`width`|ポップアップの優先幅。 許容範囲外の場合、値は無視できます。|

パラメーターの詳細については、 [authenticate(AuthenticatePopUpParameters)](/javascript/api/@microsoft/teams-js/authentication#@microsoft-teams-js-authentication-authenticate) 関数を参照してください。

## <a name="add-authentication-to-external-browsers"></a>外部ブラウザーへの認証の追加

> [!NOTE]
>
> * 現在、モバイルのタブの外部ブラウザーにのみ認証を追加できます。
> * JS SDK のベータ版を使用して、機能を活用します。 ベータ版は [NPM](https://www.npmjs.com/package/@microsoft/teams-js/v/1.12.0-beta.2) から入手できます。

次の画像は、外部ブラウザーに認証を追加するためのフローを示しています。

 :::image type="content" source="../../../assets/images/tabs/tabs-authenticate-OAuth.PNG" alt-text="authenticate-OAuth":::

**外部ブラウザーに認証を追加するには**

1. 外部認証ログイン プロセスを開始します。

   3P アプリは、`isExternal` を true に設定して SDK 関数 `authentication.authenticate` を呼び出し、外部の認証ログイン プロセスを開始します。

   渡された `url` には、`{authId}` および `{oauthRedirectMethod}` のプレースホルダーが含まれます。  

    ```JavaScript
    import { authentication } from "@microsoft/teams-js";
    authentication.authenticate({
       url: 'https://3p.app.server/auth?oauthRedirectMethod={oauthRedirectMethod}&authId={authId}',
       isExternal: true,
       successCallback: function (result) {
       //sucess 
       } failureCallback: function (reason) {
       //failure 
        }
    });
    ```

2. Teams リンクが外部ブラウザーで開きます。

   Teams クライアントは、`oauthRedirectMethod` および `authId` のプレースホルダーを適切な値に置き換えた後、外部ブラウザーで URL を開きます。

   #### <a name="example"></a>例

   ```http
    https://3p.app.server/auth?oauthRedirectMethod=deeplink&authId=1234567890 
   ```

3. 3P アプリ サーバーが応答します。

   3P アプリ サーバーは、次の 2 つのクエリ パラメーターを使用して `url` を受信して保存します。

   | パラメーター | 説明|
   | --- | --- |
   | `oauthRedirectMethod` |ディープリンクまたはページの 2 つの値のいずれかを使用して、3P アプリが認証要求の応答を Teams に送り返す方法を示します。|
   |`authId` | ディープリンクを通じて Teams に送り返す必要がある、この特定の認証要求用に Teams が作成した request-id。|

    > [!TIP]
    > 3P アプリは、OAuthProvider のログイン URL を生成しながら、OAuth `state` クエリ パラメーターで `authId`、`oauthRedirectMethod` をマーシャリングできます。 OAuthProvider が 3P サーバーにリダイレクトし、3P アプリが「**6. Teams への 3P アプリ サーバーの応答**」で説明されているように認証応答を Teams に送り返すために値を使用する場合、`state` には渡された `authId` と `oauthRedirectMethod` が含まれます。

4. 3P アプリ サーバーは、指定された `url` にリダイレクトします。

   3P アプリ サーバーは、外部ブラウザーの OAuth プロバイダー認証ページにリダイレクトします。 `redirect_uri` は、3P アプリ サーバーの専用ルートです。 `redirect_uri` を OAuth プロバイダーの開発コンソールに静的として登録できます。パラメーターは状態オブジェクトを通じて送信する必要があります。

   #### <a name="example"></a>例

    ```http
    https://accounts.google.com/o/oauth2/v2/auth?redirect_uri=https://3p.app.server/authredirect&state={"authId":"…","oauthRedirectMethod":"…"}&client_id=…    &response_type=code&access_type=offline&scope= … 
    ```

5. 外部ブラウザーにサインインします。

   User signs in to the external browser. The OAuth providers redirects back to the `redirect_uri` with the auth code and the state object.

6. 3P アプリ サーバーは Teams を確認してからそれに応答します。

   3P アプリ サーバーは応答を処理し、`oauthRedirectMethod` をチェックします。これは状態オブジェクトの外部 OAuth プロバイダーから返され、auth-callback ディープリンクまたは `notifySuccess()` を呼び出す Web ページを通じて応答を返す必要があるかどうかを判断します。

      ```JavaScript
      const state = JSON.parse(req.query.state)
      if (state.oauthRedirectMethod === 'deeplink') {
         return res.redirect('msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&result=${req.query.code}')
      }
      else {
      // continue redirecting to a web-page that will call notifySuccess() – usually this method is used in Teams-Web
      …
      ```

7. 3P アプリがディープリンクを生成します。

   3P アプリは、Teams モバイルのディープリンクを次の形式で生成し、セッション ID を含む認証コードを Teams に送り返します。

   ```JavaScript
   return res.redirect(`msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&result=${req.query.code}`)
   ```

8. Teams は成功コールバックを呼び出し、結果を送信します。

    Teams は成功コールバックを呼び出し、結果 (認証コード) を 3P アプリに送信します。 3P アプリは、成功コールバックでコードを受け取り、そのコードを使用してトークンを取得し、次にユーザー情報を取得してユーザー インターフェイスを更新します。

      ```JavaScript
      successCallback: function (result) { 
      … 
      } 
      ```

## <a name="see-also"></a>関連項目

* [ID プロバイダーを構成する](~/concepts/authentication/authentication.md)
* [タブの Microsoft Teams 認証フロー](auth-flow-tab.md)
