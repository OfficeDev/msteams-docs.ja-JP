---
title: タブを使用したタブAzure Active Directory
description: 認証の詳細Teamsタブで使用する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 認証タブAAD
ms.openlocfilehash: 96ceb632f4cd619ecc17864b5cd2fb5a665022cd
ms.sourcegitcommit: 37b1724bb0d2f1b087c356e0fd0ff80145671e22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2021
ms.locfileid: "60291703"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>[ユーザーの認証] タブでMicrosoft Teamsする

> [!Note]
> モバイル クライアントでタブで認証を機能するには、JavaScript SDK のバージョン 1.4.1 以降を使用Teams必要があります。

Teams アプリ内で使用するサービスは多数あるので、サービスにアクセスするには認証と承認が必要です。 サービスには、Facebook、Twitter、およびTeams。 Teamsプロファイル情報は Microsoft Graph を使用して Azure Active Directory (Azure AD) に格納され、この記事では、Azure AD を使用してこの情報にアクセスする認証に重点を置いて説明します。

OAuth 2.0 は、ユーザーや他の多くのサービス プロバイダーが使用する認証Azure AD標準です。 OAuth 2.0 について理解は、認証と認証の操作を行うTeams前提条件Azure AD。 次の例では、OAuth 2.0 の暗黙的な許可フローを使用して、最終的に Azure AD および Microsoft Graph からユーザーのプロファイル情報を読み取る目的で使用します。

この記事のコードは、タブ認証TeamsサンプルMicrosoft Teams [(Node) のサンプル アプリから提供されています](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。 このタブには、Microsoft Graph のアクセス トークンを要求し、現在のユーザーの基本的なプロファイル情報をユーザーから表示する静的Azure AD。

タブの認証フローの一般的な概要については、「タブの [認証フロー」を参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。

タブ内の認証フローは、ボットの認証フローとは若干異なります。

## <a name="configuring-identity-providers"></a>ID プロバイダーの構成

ID プロバイダーとして[OAuth](~/concepts/authentication/configure-identity-provider.md) 2.0 コールバック リダイレクト URL を構成する方法の詳細については、「Azure Active Directory ID プロバイダーの構成」を参照してください。

## <a name="initiate-authentication-flow"></a>認証フローの開始

認証フローは、ユーザー アクションによってトリガーされる必要があります。 これは、ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性が高いので、認証ポップアップを自動的に開く必要があります。

構成ページまたはコンテンツ ページにボタンを追加して、必要に応じてユーザーがサインインできます。 これは、タブ構成ページまたは任意 [の](~/tabs/how-to/create-tab-pages/configuration-page.md) コンテンツ ページで [実行](~/tabs/how-to/create-tab-pages/content-page.md) できます。

Azure AD ID プロバイダーと同様に、コンテンツを iframe に配置できない場合があります。 つまり、ID プロバイダーをホストするためにポップアップ ページを追加する必要があります。 次の例では、このページは `/tab-auth/simple-start` . ボタンが `microsoftTeams.authenticate()` 選択されている場合Microsoft Teamsクライアント SDK の機能を使用して、このページを起動します。

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

### <a name="notes"></a>備考

* 渡す URL `microsoftTeams.authentication.authenticate()` は、認証フローの開始ページです。 この例では、 `/tab-auth/simple-start` です。 これは、アプリケーション登録ポータルで登録[したAzure AD一致する必要があります](https://apps.dev.microsoft.com)。

* 認証フローは、ドメイン上のページで開始する必要があります。 このドメインは、マニフェストのセクション [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) にも一覧表示する必要があります。 この操作を実行しない場合は、空のポップアップが表示されます。

* 使用に失敗すると、サインイン プロセスの最後にポップアップが閉じない問題 `microsoftTeams.authentication.authenticate()` が発生します。

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>ポップアップ ページから承認ページに移動する

ポップアップ ページ ( ) が表示 `/tab-auth/simple-start` される場合は、次のコードが実行されます。 このページの主な目的は、ユーザーがサインインできるよう ID プロバイダーにリダイレクトする方法です。 このリダイレクトは、HTTP 302 を使用してサーバー側で実行できますが、この場合、クライアント側で呼び出しを使用して行われます `window.location.assign()` 。 これにより、ヒント情報を取得するためにも使用できます。この情報は、ユーザーに渡 `microsoftTeams.getContext()` Azure AD。

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

ユーザーが承認を完了すると、ユーザーはアプリで指定したコールバック ページにリダイレクトされます `/tab-auth/simple-end` 。

### <a name="notes"></a>備考

* 認証 [要求と URL の作成に](~/tabs/how-to/access-teams-context.md) 関するヘルプについては、「ユーザー コンテキスト情報の取得」を参照してください。 たとえば、ユーザーのログイン名を、Azure ADサインインの値として使用できます。つまり、ユーザーが入力する必要が少ない `login_hint` 場合があります。 攻撃者が悪意のあるブラウザーにページを読み込み、必要な情報を提供する可能性がある場合は、このコンテキストを ID の証明として直接使用する必要があります。
* タブ コンテキストはユーザーに関する有用な情報を提供しますが、この情報を使用して、タブ コンテンツ URL への URL パラメーターとして取得するか、Microsoft Teams クライアント SDK で関数を呼び出す場合でも、ユーザーを認証しません。 `microsoftTeams.getContext()` 悪意のあるアクターが、独自のパラメーターを使用してタブ コンテンツ URL を呼び出し、Microsoft Teams を偽装する Web ページが iframe にタブ コンテンツ URL を読み込み、独自のデータを関数に返す可能性があります。 `getContext()` 使用する前に、タブ コンテキスト内の ID 関連情報をヒントとして扱い、検証する必要があります。
* この `state` パラメーターは、コールバック URI を呼び出すサービスが、呼び出したサービスを確認するために使用されます。 コールバック内のパラメーターが呼び出し中に送信したパラメーターと一致しない場合、戻り値の呼び出しは検証されないので、 `state` 終了する必要があります。
* ID プロバイダーのドメインをアプリの manifest.json ファイルの一覧に含 `validDomains` める必要はありません。

## <a name="the-callback-page"></a>コールバック ページ

最後のセクションでは、Azure AD 認証サービスを呼び出し、ユーザーとアプリの情報を渡して、Azure AD独自のモノリシック認証エクスペリエンスをユーザーに提示します。 アプリは、このエクスペリエンスで何が起こるかを制御できます。 知っているのは、指定したコールバック ページAzure AD呼び出した場合に返される処理だけです `/tab-auth/simple-end` 。

このページでは、ユーザーが返す情報に基づいて成功または失敗をAzure ADする必要 `microsoftTeams.authentication.notifySuccess()` があります `microsoftTeams.authentication.notifyFailure()` 。 ログインが成功した場合は、サービス リソースにアクセスできます。

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

このコードは、ヘルパー関数を使用して、Azure ADキーと値のペア `window.location.hash` を `getHashParameters()` 解析します。 認証フローの開始時点で指定した値と同じ値が見つけられる場合は、呼び出してタブにアクセス トークンを返します。それ以外の場合は、 でエラーを報告します `access_token` `state` `notifySuccess()` `notifyFailure()` 。

### <a name="notes"></a>備考

`NotifyFailure()` 次の定義済みのエラー理由があります。

* `CancelledByUser` ユーザーは、認証フローを完了する前にポップアップ ウィンドウを閉じていました。
* `FailedToOpenWindow` ポップアップ ウィンドウを開くことができません。 ブラウザーでMicrosoft Teamsを実行する場合、これは通常、ポップアップ ブロッカーによってウィンドウがブロックされたという意味です。

成功した場合は、ページを更新または再読み込みし、現在認証されたユーザーに関連するコンテンツを表示できます。 認証に失敗すると、エラー メッセージが表示されます。

アプリは、ユーザーが現在のデバイスのタブに戻ったときに再度サインインする必要が生じないので、独自のセッション Cookie を設定できます。

> [!NOTE]
> Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../../../resources/samesite-cookie-update.md)」を *参照してください*。

>[!NOTE]
>無料ユーザーとゲスト ユーザー Microsoft Teamsトークンを取得するには、アプリでテナント固有のエンドポイントを使用することが重要です `https://login.microsoftonline.com/**{tenantId}**` 。 bot メッセージまたはタブ コンテキストから tenantId を取得できます。 アプリが使用されている場合、ユーザーは正しくないトークンを取得し、現在サインインしているテナントではなく"ホーム" テナント `https://login.microsoftonline.com/common` にログオンします。

シングル 認証 (SSO) のSign-Onについては、「サイレント認証」の記事 [を参照してください](~/tabs/how-to/authentication/auth-silent-AAD.md)。

## <a name="code-sample"></a>コード サンプル

次のコードを使用してタブ認証プロセスを示すAzure AD。

| **サンプルの名前** | **description** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teamsタブ認証 | タブ認証プロセスは、Azure AD。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |
