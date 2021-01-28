---
title: Azure Active Directory を使用したタブの認証
description: Teams での認証とタブでの認証の使い方について説明します。
ms.topic: how-to
keywords: Teams 認証タブ AAD
ms.openlocfilehash: 1502d2634b39230e0428863383bf97ada0be0359
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014566"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>Microsoft Teams タブでユーザーを認証する

> [!Note]
> モバイル クライアントのタブで認証を機能するには、Teams JavaScript SDK のバージョン 1.4.1 以降を使用している必要があります。

Teams アプリ内で使用するサービスは多数あるので、それらのサービスのほとんどで、サービスにアクセスするには認証と承認が必要です。 サービスには、Facebook、Twitter、そしてもちろん Teams が含まれます。 Teams のユーザーは、Microsoft Graph を使用して Azure Active Directory (Azure AD) に保存されているユーザー プロファイル情報を持っています。この記事では、Azure AD を使用してこの情報にアクセスする認証に重点を置きます。

OAuth 2.0 は、Azure AD他の多くのサービス プロバイダーで使用される認証のオープン標準です。 OAuth 2.0 について理解するには、Teams および Azure AD で認証を操作する必要があります。 次の例では、OAuth 2.0 の暗黙的な付与フローを使用して、最終的に Azure AD および Microsoft Graph からユーザーのプロファイル情報を読み取るという目標を達成しています。

この記事のコードは、Teams サンプル アプリ [の Microsoft Teams タブ認証サンプル (ノード) から提供されています](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。 Microsoft Graph のアクセス トークンを要求し、Azure Graph から現在のユーザーの基本的なプロファイル情報を表示する静的タブAD。

タブの認証フローの概要については、タブの「認証フロー」 [を参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。

タブの認証フローは、ボットの認証フローとは若干異なります。

## <a name="configuring-identity-providers"></a>ID プロバイダーの構成

Azure Active Directory を [ID](~/concepts/authentication/configure-identity-provider.md) プロバイダーとして使用する場合の OAuth 2.0 コールバック リダイレクト URL の構成に関する詳細な手順については、「ID プロバイダーを構成する」を参照してください。

## <a name="initiate-authentication-flow"></a>認証フローを開始する

認証フローは、ユーザーの操作によってトリガーされる必要があります。 認証ポップアップは、ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性が高いので、自動的に開かれません。

必要に応じてユーザーがサインインできるボタンを構成ページまたはコンテンツ ページに追加します。 これは、タブ構成ページまたは [任意のコンテンツ](~/tabs/how-to/create-tab-pages/configuration-page.md) ページで [行](~/tabs/how-to/create-tab-pages/content-page.md) えます。

Azure AD、ほとんどの ID プロバイダーと同様に、そのコンテンツを iframe に配置する機能は許可されています。 つまり、ID プロバイダーをホストするためにポップアップ ページを追加する必要があります。 次の例では、このページは `/tab-auth/simple-start` 次のとおりです。 Microsoft `microsoftTeams.authenticate()` Teams クライアント SDK の機能を使用して、ボタンが選択されているときにこのページを起動します。

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

### <a name="notes"></a>Notes

* 渡す URL `microsoftTeams.authentication.authenticate()` は、認証フローの開始ページです。 この例では、 `/tab-auth/simple-start` . これは、Azure AD [アプリケーション登録ポータルに登録したデータと一致する必要があります](https://apps.dev.microsoft.com)。

* 認証フローは、ドメイン上のページから開始する必要があります。 このドメインは、マニフェストのセクション [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) にも一覧表示する必要があります。 そうしない場合は、空のポップアップが表示されます。

* 使用に失敗すると、サインイン プロセスの最後にポップアップが閉じない問題 `microsoftTeams.authentication.authenticate()` が発生します。

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>ポップアップ ページから承認ページに移動する

ポップアップ ページ ( ) が表示 `/tab-auth/simple-start` される場合は、次のコードが実行されます。 このページの主な目的は、ユーザーがサインインできるよう ID プロバイダーにリダイレクトする方法です。 このリダイレクトは、HTTP 302 を使用してサーバー側で実行できますが、この場合は、クライアント側で呼び出しを使用して行われます `window.location.assign()` 。 これにより、Azure AD に渡されるヒント情報 `microsoftTeams.getContext()` を取得するためにも使用AD。

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

ユーザーが承認を完了すると、ユーザーはアプリに対して指定したコールバック ページにリダイレクトされます `/tab-auth/simple-end` 。

### <a name="notes"></a>Notes

* 認証 [要求と URL の構築に](~/tabs/how-to/access-teams-context.md) 関するヘルプについては、ユーザー コンテキスト情報の取得に関するページを参照してください。 たとえば、Azure AD サインインの値としてユーザーのログイン名を使用できます。これは、ユーザーが入力する必要が少ない可能性があることを `login_hint` 意味します。 攻撃者が悪意のあるブラウザーにページを読み込み、必要な情報をページに提供する可能性があります。そのため、このコンテキストを ID の証明として直接使用することはできません。
* タブ コンテキストはユーザーに関する有用な情報を提供しますが、タブ コンテンツの URL への URL パラメーターとして取得するか、Microsoft Teams クライアント SDK の関数を呼び出す場合でも、この情報を使用してユーザーを認証しません。 `microsoftTeams.getContext()` 悪意のあるアクターが独自のパラメーターを使用してタブ コンテンツの URL を呼び出す可能性があります。また、Microsoft Teams を偽装する Web ページが iframe にタブ コンテンツ URL を読み込み、独自のデータを関数に返す可能性があります。 `getContext()` タブ コンテキストでは、ID 関連の情報をヒントとして扱い、使用する前に検証する必要があります。
* この `state` パラメーターは、コールバック URI を呼び出すサービスが呼び出したサービスを確認するために使用されます。 コールバックのパラメーターが呼び出し中に送信したパラメーターと一致しない場合、戻り値の呼び出しは検証されないの `state` で、終了する必要があります。
* ID プロバイダーのドメインをアプリの on ファイルの一覧に含 `validDomains` manifest.js必要はありません。

## <a name="the-callback-page"></a>コールバック ページ

最後のセクションでは、Azure AD 認証サービスを呼び出し、Azure AD が独自のモノリシックな承認エクスペリエンスをユーザーに提供できるよう、ユーザーとアプリの情報を渡しました。 アプリは、このエクスペリエンスで何が起こるかを制御する必要はありません。 Azure ADが指定したコールバック ページ () を呼び出す場合に返されるのは、そのことを知っているだけです `/tab-auth/simple-end` 。

このページでは、Azure が返す情報に基づいて、成功または失敗を判断する必要があります。AD呼び出し `microsoftTeams.authentication.notifySuccess()` または `microsoftTeams.authentication.notifyFailure()` . ログインが成功した場合は、サービス リソースにアクセスできます。

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

このコードは、ヘルパー関数を使用して Azure ADキーと値のペア `window.location.hash` を `getHashParameters()` 解析します。 認証フローの開始時点で指定した値と同じ値が見つからなければ、アクセス トークンを呼び出してタブに返します。それ以外の場合は、エラーを報告 `access_token` `state` `notifySuccess()` します `notifyFailure()` 。

### <a name="notes"></a>Notes

`NotifyFailure()` には、次の定義済みのエラーの理由があります。

* `CancelledByUser` ユーザーが認証フローを完了する前にポップアップ ウィンドウを閉じた。
* `FailedToOpenWindow` ポップアップ ウィンドウを開く必要がありました。 ブラウザーで Microsoft Teams を実行する場合、これは通常、ウィンドウがポップアップ ブロックによってブロックされた状態を意味します。

成功した場合は、ページを更新または再読み込みし、現在認証されたユーザーに関連するコンテンツを表示できます。 認証に失敗した場合は、エラー メッセージを表示します。

アプリでは、ユーザーが現在のデバイスのタブに戻る際にもう一度サインインする必要が生じないので、独自のセッション Cookie を設定できます。

> [!NOTE]
> Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../../../resources/samesite-cookie-update.md)」を *参照してください*。

>[!NOTE]
>Microsoft Teams 無料ユーザーとゲスト ユーザーの適切なトークンを取得するには、アプリでテナント固有のエンドポイント https://login.microsoftonline.com/ **{tenantId} を使用することが重要です**。 bot メッセージまたはタブ コンテキストから tenantId を取得できます。 アプリが使用されている場合、ユーザーは正しくないトークンを取得し、現在サインインしているテナントではなく https://login.microsoftonline.com/common 、"ホーム" テナントにログオンします。

シングル 認証 (SSO) の詳細Sign-Onサイレント認証の記事 [を参照してください](~/tabs/how-to/authentication/auth-silent-AAD.md)。

## <a name="samples"></a>サンプル

Azure 認証を使用したタブ認証プロセスを示すサンプル コードAD参照してください。

* [Microsoft Teams タブ認証のサンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
