---
title: サード パーティの OAuth 認証を構成する
description: この記事では、Teams 認証タブMicrosoft Azure AD、Teams での認証、およびタブで使用する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 1afc7e7512c75c9002849801cfc14fb8eb1aa726
ms.sourcegitcommit: 36c6a5ba1dcd27a15ba31f479e534eab69aa17e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2022
ms.locfileid: "67465373"
---
# <a name="configure-third-party-oauth-idp-authentication"></a>サード パーティの OAuth IdP 認証を構成する

> [!Note]
> モバイル クライアントのタブで認証を機能させるには、バージョン 1.4.1 以降の Teams JavaScript SDK を使用していることを確認します。

Teams アプリ内で使用するサービスは多数あります。これらのサービスのほとんどは、サービスにアクセスするために認証と承認が必要です。 サービスには、Facebook、Twitter、Teams が含まれます。
Teams ユーザー プロファイル情報は Microsoft Graph を使用して Azure AD に格納され、この記事では、この情報にアクセスするために Azure AD を使用した認証に焦点を当てます。

OAuth 2.0 は、Azure AD や他の多くのサービス プロバイダーで使用される認証のオープン 標準です。 OAuth 2.0 について理解することは、Teams と Azure AD で認証を操作するための前提条件です。 次の例では、OAuth 2.0 暗黙的許可フローを使用します。 Azure AD と Microsoft Graph からユーザーのプロファイル情報を読み取ります。

この記事のコードは、Teams サンプル アプリ [Microsoft Teams 認証サンプル (ノード)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) から提供されています。 これには、Microsoft Graph のアクセス トークンを要求する静的タブが含まれており、Azure AD から現在のユーザーの基本的なプロファイル情報が表示されます。

タブの認証フローの概要については、タブ [の認証フローに関するページを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。

タブの認証フローは、ボットの認証フローとは異なります。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="configure-your-app-to-use-azure-ad-as-an-identity-provider"></a>ID プロバイダーとして Azure AD を使用するようにアプリを構成する

OAuth 2.0 をサポートする ID プロバイダーは、不明なアプリケーションからの要求を認証しません。 事前にアプリケーションを登録する必要があります。 Azure AD でこれを行うには、次の手順に従います。

1. [アプリケーション登録ポータル](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)を開きます。

2. アプリを選択してプロパティを表示するか、[新しい登録] ボタンを選択します。 アプリの **リダイレクト URI** セクションを見つけます。

3. ドロップダウン メニューから **[Web** ] を選択します。 URL を認証エンドポイントに更新します。 GitHub 上の TypeScript/Node.js および C# サンプル アプリの場合、リダイレクト URL は次のようになります。

    リダイレクト URL: `https://<hostname>/bot-auth/simple-start`

実際のホストに置き換えます `<hostname>` 。 このホストは、Azure、Glitch などの専用ホスティング サイト、開発マシン上の localhost への ngrok トンネル (例: `abcd1234.ngrok.io`. この情報がない場合は、アプリ (またはサンプル アプリ) を完了またはホストしていることを確認します。 この情報がある場合は、このプロセスを再開します。

> [!NOTE]
> LinkedIn、Google、その他のサードパーティ OAuth プロバイダーを選択できます。 これらのプロバイダーの認証を有効にするプロセスは、サード パーティの OAuth プロバイダーとして Azure AD を使用する場合と似ています。 サードパーティ OAuth プロバイダーの使用の詳細については、特定のプロバイダーの Web サイトを参照してください。

## <a name="initiate-authentication-flow"></a>認証フローを開始する

認証フローは、ユーザー アクションによってトリガーする必要があります。 ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性があるため、認証ポップアップを自動的に開く必要はありません。

必要に応じてユーザーがサインインできるように、構成ページまたはコンテンツ ページにボタンを追加します。 これは、タブ [構成](~/tabs/how-to/create-tab-pages/configuration-page.md) ページまたは [任意のコンテンツ](~/tabs/how-to/create-tab-pages/content-page.md) ページで行うことができます。

Azure AD は、ほとんどの ID プロバイダーと同様に、そのコンテンツを `iframe`. つまり、ID プロバイダーをホストするためにポップアップ ページを追加する必要があります。 次の例では、このページは `/tab-auth/simple-start`. ボタンが `authentication.authenticate()` 選択されているときにこのページを起動するには、Microsoft Teams クライアント SDK の機能を使用します。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
import { authentication } from "@microsoft/teams-js";
authentication.authenticate({
    url: window.location.origin + "/tab/simple-start-v2",
    width: 600,
    height: 535})
.then((result) => {
    console.log("Login succeeded: " + result);
    let data = localStorage.getItem(result);
    localStorage.removeItem(result);
    let tokenResult = JSON.parse(data);
    showIdTokenAndClaims(tokenResult.idToken);
    getUserProfile(tokenResult.accessToken);
})
.catch((reason) => {
    console.log("Login failed: " + reason);
    handleAuthError(reason);
});
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
microsoftTeams.authentication.authenticate({
    url: window.location.origin + "/tab-auth/simple-start",
    width: 600,
    height: 535,
    successCallback: function (result) {
        getUserProfile(result.accessToken);
    },
    failureCallback: function (reason) {
        handleAuthError(reason);
    }
});
```
---

### <a name="notes"></a>備考

* 渡す `authenticate()` URL は、認証フローの開始ページです。 この例では、次のようになります `/tab-auth/simple-start`。 これは、 [Azure AD アプリケーション登録ポータル](https://apps.dev.microsoft.com)で登録したものと一致する必要があります。

* 認証フローは、ドメイン上のページで開始する必要があります。 このドメインは、マニフェストの [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) セクションにも一覧表示する必要があります。 そうしないと、空のポップアップが表示されます。

* 使用 `authenticate()` しないと、サインイン プロセスの最後にポップアップが閉じない場合に問題が発生します。

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>ポップアップ ページから承認ページに移動する

ポップアップ ページ (`/tab-auth/simple-start`) が表示されると、次のコードが実行されます。 ページの主な目的は、ユーザーがサインインできるように ID プロバイダーにリダイレクトすることです。 このリダイレクトは、HTTP 302 を使用してサーバー側で実行できますが、この場合はクライアント側で呼び出し `window.location.assign()`を使用して実行されます。 また、 `app.getContext()` これを使用してヒント情報を取得し、Azure AD に渡すこともできます。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
app.getContext().then((context) => {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");

    // Go to the Azure AD authorization endpoint
    let queryParams = {
        client_id: "{{appId}}",
        response_type: "id_token token",
        response_mode: "fragment",
        scope: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
        // is used as hinting information
        login_hint: context.user.loginHint,
    };

    let authorizeEndpoint = `https://login.microsoftonline.com/${context.user.tenant.id}/oauth2/v2.0/authorize?${toQueryString(queryParams)}`;
    window.location.assign(authorizeEndpoint);
});
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
microsoftTeams.getContext(function (context) {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");
    // Go to the Azure AD authorization endpoint
    let queryParams = {
        client_id: "YOUR_APP_ID_HERE",
        response_type: "id_token token",
        response_mode: "fragment",
        scope: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/v2.0/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

---

ユーザーが承認を完了すると、ユーザーはアプリ `/tab-auth/simple-end`で指定したコールバック ページにリダイレクトされます。

### <a name="notes"></a>備考

* 認証要求と URL の構築に関するヘルプについては、 [ユーザー コンテキスト情報の取得](~/tabs/how-to/access-teams-context.md) に関するページを参照してください。 たとえば、Azure AD サインインの値としてユーザーのログイン名を `login_hint` 使用できます。つまり、ユーザーの入力が少なくなる可能性があります。 攻撃者が悪意のあるブラウザーにページを読み込み、必要な情報を提供する可能性があるため、このコンテキストを ID の証明として直接使用しないでください。
* タブ コンテキストはユーザーに関する有用な情報を提供しますが、タブ コンテンツ URL の URL パラメーターとして取得するか、Microsoft Teams クライアント SDK で関数を呼び出 `app.getContext()` すかに関係なく、この情報を使用してユーザーを認証しないでください。 悪意のあるアクターが独自のパラメーターを使用してタブ コンテンツ URL を呼び出す可能性があり、Microsoft Teams を偽装する Web ページが iframe にタブ コンテンツ URL を読み込み、独自のデータを関数に `getContext()` 返す可能性があります。 タブ コンテキスト内の ID 関連情報は、単にヒントとして扱い、使用する前に検証する必要があります。
* このパラメーターは `state` 、コールバック URI を呼び出すサービスが呼び出したサービスであることを確認するために使用されます。 コールバック内の `state` パラメーターが呼び出し中に送信したパラメーターと一致しない場合、戻り値の呼び出しは検証されないため、終了する必要があります。
* アプリの manifest.json ファイルの一覧に ID プロバイダーのドメイン `validDomains` を含める必要はありません。

## <a name="the-callback-page"></a>コールバック ページ

最後のセクションでは、Azure AD 承認サービスを呼び出し、Azure AD が独自のモノリシック承認エクスペリエンスをユーザーに提供できるように、ユーザーとアプリの情報を渡しました。 アプリは、このエクスペリエンスで何が起こるかを制御しません。 Azure AD が指定したコールバック ページを呼び出したときに返される内容は、すべて認識されています (`/tab-auth/simple-end`)。

このページでは、Azure AD と呼び出しまたは呼び出 `authentication.notifySuccess()` しによって返される情報に基づいて成功または失敗を判断する必要があります `authentication.notifyFailure()`。 ログインに成功した場合は、サービス リソースにアクセスできます。

```javascript
// Split the key-value pairs passed from Azure AD
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Azure AD after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    localStorage.setItem("simple.error", JSON.stringify(hashParams));
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    let expectedState = localStorage.getItem("simple.state");
    if (expectedState !== hashParams["state"]) {
        // State does not match, report error
        localStorage.setItem("simple.error", JSON.stringify(hashParams));
        authentication.notifyFailure("StateDoesNotMatch");
    } else {
        // Success -- return token information to the parent page.
        // Use localStorage to avoid passing the token via notifySuccess; instead we send the item key.
        let key = "simple.result";
        localStorage.setItem(key, JSON.stringify({
            idToken: hashParams["id_token"],
            accessToken: hashParams["access_token"],
            tokenType: hashParams["token_type"],
            expiresIn: hashParams["expires_in"]
        }));
        authentication.notifySuccess(key);
    }
} else {
    // Unexpected condition: hash does not contain error or access_token parameter
    localStorage.setItem("simple.error", JSON.stringify(hashParams));
    authentication.notifyFailure("UnexpectedFailure");
}
```

このコードは、ヘルパー関数を使用して、Azure AD から受信したキーと値の `window.location.hash` ペアを解析します `getHashParameters()` 。 認証フローの開始時に`state`指定されたものと同じ値が見つかる`access_token`と、アクセス トークンが呼び出`notifySuccess()`されてタブに返されます。それ以外の場合はエラー`notifyFailure()`が報告されます。

### <a name="notes"></a>備考

`NotifyFailure()` には、次の定義済みのエラーの理由があります。

* `CancelledByUser` ユーザーは、認証フローを完了する前にポップアップ ウィンドウを閉じました。
* `FailedToOpenWindow` ポップアップ ウィンドウを開くことができませんでした。 ブラウザーで Microsoft Teams を実行している場合、これは通常、ポップアップ ブロックによってウィンドウがブロックされたことを意味します。

成功した場合は、ページを更新または再読み込みし、現在認証されたユーザーに関連するコンテンツを表示できます。 認証に失敗すると、エラー メッセージが表示されます。

アプリは、ユーザーが現在のデバイスのタブに戻ったときにもう一度サインインする必要がないように、独自のセッション Cookie を設定できます。

> [!NOTE]
>
> * Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../../../resources/samesite-cookie-update.md)」を *参照してください*。
> * Microsoft Teams Free とゲスト ユーザーの正しいトークンを取得するには、アプリでテナント固有のエンドポイント `https://login.microsoftonline.com/**{tenantId}**`を使用することが重要です。 bot メッセージまたはタブ コンテキストから tenantId を取得できます。 アプリが使用 `https://login.microsoftonline.com/common`されている場合、ユーザーは正しくないトークンを取得し、現在サインインしているテナントではなく "ホーム" テナントにログオンします。

シングル Sign-On (SSO) の詳細については、 [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)に関する記事を参照してください。

## <a name="code-sample"></a>コード サンプル

Azure AD を使用したタブ認証プロセスを示すサンプル コード:

| **サンプルの名前** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teams タブ認証 | Azure AD を使用したタブ認証プロセス。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>関連項目

* [ユーザー認証を計画する](../../../concepts/design/understand-use-cases.md)
* [Microsoft Teams 用のタブを設計する](~/tabs/design/tabs.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-aad.md)
* [メッセージ拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)
* [ボット向けのシングル サインオン (SSO) サポート](~/bots/how-to/authentication/auth-aad-sso-bots.md)
