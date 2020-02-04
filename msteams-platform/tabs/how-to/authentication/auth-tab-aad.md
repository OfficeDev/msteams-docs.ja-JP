---
title: Azure Active Directory を使用したタブの認証
description: Teams での認証と、それらをタブで使用する方法について説明します。
keywords: teams の認証タブ AAD
ms.openlocfilehash: 760fce99a51dc722905035bade6db008072ee0b4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674878"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Microsoft Teams タブでユーザーを認証する

> [!Note]
> モバイルクライアントのタブで認証を行うには、Teams JavaScript SDK のバージョン1.4.1 以降を使用していることを確認する必要があります。

Teams アプリ内で使用する必要があるサービスは多数ありますが、これらのサービスのほとんどは、サービスへのアクセスを取得するために認証と承認を必要とします。 サービスには、Facebook、Twitter、およびコースチームが含まれます。 Teams のユーザーは、Microsoft Graph を使用して Azure Active Directory (Azure AD) に保存されたユーザープロファイル情報を持っています。この記事では、Azure AD を使用した認証に重点を置いて、この情報にアクセスします。

OAuth 2.0 は、Azure AD とその他の多くのサービスプロバイダーによって使用される、オープンスタンダードの認証です。 OAuth 2.0 については、Teams および Azure AD で認証を処理するための前提条件となります。 次の例では、最終的に Azure AD と Microsoft Graph からユーザーのプロファイル情報を読み取るという目標を持つ OAuth 2.0 暗黙的な付与フローを使用します。

この記事のコードは、Teams サンプルアプリの[Microsoft teams タブ認証のサンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)から取得されます。 このプロパティには、Microsoft Graph のアクセストークンを要求する静的なタブが含まれており、Azure AD からの現在のユーザーの基本プロファイル情報を示しています。

タブの認証フローの一般的な概要については、「[タブでの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)」を参照してください。

タブ内の認証フローは、ボットの認証フローと若干異なります。

## <a name="configuring-identity-providers"></a>Id プロバイダーを構成する

Azure Active Directory を id プロバイダーとして使用する場合は、「 [id プロバイダー](~/concepts/authentication/configure-identity-provider.md)を構成する」の「OAuth 2.0 コールバック URL を構成する」の詳細な手順については、このトピックを参照してください。

## <a name="initiate-authentication-flow"></a>認証フローの開始

認証フローは、ユーザーの操作によってトリガーされます。 これにより、ブラウザーのポップアップブロックがトリガーされ、ユーザーが混乱する可能性があるので、自動的に認証ポップアップを開かないようにする必要があります。

ユーザーが必要なときにサインインできるように、構成ページまたはコンテンツページにボタンを追加します。 この操作は、[タブの[構成](~/tabs/how-to/create-tab-pages/configuration-page.md)] ページまたは任意の[コンテンツ](~/tabs/how-to/create-tab-pages/content-page.md)ページで行うことができます。

多くの id プロバイダーと同様に Azure AD は、そのコンテンツを iframe に配置することを許可しません。 これは、id プロバイダーをホストするポップアップページを追加する必要があることを意味します。 このページの例を次に`/tab-auth/simple-start`示します。 ボタンが`microsoftTeams.authenticate()`選択されているときに、Microsoft TEAMS クライアント SDK の関数を使用してこのページを起動します。

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

### <a name="notes"></a>メモ

* 渡される URL `microsoftTeams.authentication.authenticate()`は、認証フローの開始ページです。 この例では`/tab-auth/simple-start`、です。 これは、 [AZURE AD アプリケーション登録ポータル](https://apps.dev.microsoft.com)に登録した内容と一致する必要があります。

* 認証フローは、ドメイン上のページで開始する必要があります。 このドメインは、マニフェストの[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)セクションにも記載されている必要があります。 失敗すると、空のポップアップが発生します。

* 使用`microsoftTeams.authentication.authenticate()`できない場合は、サインインプロセスの終了時にポップアップが閉じられない問題が発生します。

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>ポップアップページから [認証] ページに移動します。

ポップアップページ (`/tab-auth/simple-start`) が表示されると、次のコードが実行されます。 このページの主な目的は、ユーザーがサインインできるように、id プロバイダーにリダイレクトすることです。 このリダイレクトは、HTTP 302 を使用してサーバー側で実行でき`window.location.assign()`ますが、この場合は、の呼び出しを使用してクライアント側で行われます。 これは、 `microsoftTeams.getContext()` Azure AD に渡すことができるヒント情報を取得するためにも使用できます。

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
        resource: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

ユーザーが認証を完了すると、ユーザーは、アプリで指定されたコールバックページ`/tab-auth/simple-end`にリダイレクトされます。

### <a name="notes"></a>メモ

* 認証要求および Url の作成方法については、「 [get user context information](~/tabs/how-to/access-teams-context.md) 」を参照してください。 たとえば、ユーザーのログイン名を Azure AD サインインの`login_hint`値として使用できます。これは、ユーザーがより少ない値を入力する必要があることを意味します。 攻撃者が悪意のあるブラウザーにページを読み込み、必要な情報を提供する可能性があるため、このコンテキストを id の証明として直接使用することはできないことに注意してください。
* Tab コンテキストはユーザーに関して有用な情報を提供しますが、この情報を使用してユーザーがタブのコンテンツ URL への URL パラメーターとして`microsoftTeams.getContext()`取得するか、Microsoft TEAMS クライアント SDK の関数を呼び出すかを認証しません。 悪意のあるアクターは、独自のパラメーターを使用してタブコンテンツ URL を呼び出すことができ、Microsoft Teams を偽装している web ページは、タブコンテンツ URL `getContext()`を iframe に読み込み、そのデータを関数に返すことができました。 Tab コンテキストの id 関連情報は単にヒントとして扱い、使用する前に検証する必要があります。
* この`state`パラメーターは、コールバック URI を呼び出すサービスが、呼び出したサービスであることを確認するために使用されます。 コールバック`state`内のパラメーターが、呼び出し中に送信したパラメーターと一致しない場合は、戻り呼び出しは検証されず、終了する必要があります。
* アプリの manifest.xml ファイルの`validDomains`リストに id プロバイダーのドメインを含める必要はありません。

## <a name="the-callback-page"></a>コールバックページ

最後のセクションでは、azure AD authorization service を呼び出して、ユーザーとアプリの情報を渡して、Azure AD がユーザーに独自のモノリシックな認証環境を提供できるようにしました。 アプリには、この操作での動作を制御する機能はありません。 提供されたコールバックページが Azure AD によって呼び出されたときに`/tab-auth/simple-end`返されることがわかっています ()。

このページでは、Azure AD によって返された情報と、または`microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()`の呼び出しに基づいて、成功または失敗を特定する必要があります。 ログインに成功すると、サービスリソースにアクセスできるようになります。

````javascript
// Split the key-value pairs passed from Azure AD
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Azure AD after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    microsoftTeams.authentication.notifyFailure(hashParams["error"]);
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    // This validates that the data is coming from Azure AD
    let expectedState = localStorage.getItem("simple.state");
    if (expectedState !== hashParams["state"]) {
        // State does not match, report error
        microsoftTeams.authentication.notifyFailure("StateDoesNotMatch");
    } else {
        // Success: return token information to the tab
        microsoftTeams.authentication.notifySuccess({
            idToken: hashParams["id_token"],
            accessToken: hashParams["access_token"],
            tokenType: hashParams["token_type"],
            expiresIn: hashParams["expires_in"]
        })
    }
} else {
    // Unexpected condition: hash does not contain error or access_token parameter
    microsoftTeams.authentication.notifyFailure("UnexpectedFailure");
}
````

このコードで`window.location.hash`は、 `getHashParameters()`ヘルパー関数を使用して Azure AD から受信したキーと値のペアを解析します。 が`access_token`で、その`state`値が認証フローの開始時に指定されたものと同じである場合は、呼び出し`notifySuccess()`によってタブへのアクセストークンが返されます。それ以外の場合は、 `notifyFailure()`でエラーが報告されます。

### <a name="notes"></a>メモ

`NotifyFailure()`には、次のような定義済みエラーの理由があります。

* `CancelledByUser`ユーザーが認証フローを完了する前にポップアップウィンドウを閉じました。
* `FailedToOpenWindow`ポップアップウィンドウを開くことができませんでした。 ブラウザーで Microsoft Teams を実行している場合、これは通常、ポップアップブロックによってウィンドウがブロックされたことを意味します。

成功した場合は、ページを更新または再読み込みして、現在認証されているユーザーに関連するコンテンツを表示することができます。 認証が失敗した場合は、エラーメッセージを表示します。

アプリは、自分のセッション cookie を設定して、ユーザーが現在のデバイスのタブに戻ったときにもう一度サインインしないようにすることができます。

> [!NOTE]
> Chrome 80 (初期2020でリリースが予定されています)。新しい cookie 値を紹介し、既定で cookie ポリシーを設定します。 既定のブラウザーの動作に依存するのではなく、cookie に対して使用する目的を設定することをお勧めします。 [SameSite cookie 属性 (2020 update)](../../../resources/samesite-cookie-update.md)を*参照してください*。

シングルサインオン (SSO) の詳細については、「[サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)」を参照してください。

## <a name="samples"></a>サンプル

Azure AD を使用したタブ認証プロセスを示すサンプルコードについては、以下を参照してください。

* [Microsoft Teams タブ認証のサンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
