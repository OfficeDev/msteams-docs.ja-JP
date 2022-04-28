---
title: Azure Active Directoryを使用したタブの認証
description: Teamsでの認証と、それをタブで使用する方法について説明します
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 認証タブ Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 41d2a3f0cb9d05acfe879654c255e1d012c1f874
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104057"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>[Microsoft Teams] タブでユーザーを認証する

> [!Note]
> モバイル クライアントのタブで認証を機能させるには、バージョン 1.4.1 以降の Teams JavaScript SDK を使用していることを確認する必要があります。

Teams アプリ内で使用するサービスは多数あります。これらのサービスのほとんどは、サービスにアクセスするために認証と承認が必要です。 サービスには、Facebook、Twitter、Teamsが含まれます。 Teamsユーザー プロファイル情報は Microsoft Graphを使用してAzure ADに格納されます。この記事では、この情報にアクセスするためにAzure ADを使用した認証に焦点を当てます。

OAuth 2.0 は、Azure ADおよびその他の多くのサービス プロバイダーで使用される認証のオープン 標準です。 OAuth 2.0 を理解することは、TeamsおよびAzure ADで認証を操作するための前提条件です。 次の例では、OAuth 2.0 暗黙的許可フローを使用して、最終的にAzure ADと Microsoft Graphからユーザーのプロファイル情報を読み取ります。

この記事のコードは、Teams サンプル アプリ[Microsoft Teamsタブ認証サンプル (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) から提供されています。 これには、Microsoft Graphのアクセス トークンを要求し、Azure ADから現在のユーザーの基本的なプロファイル情報を表示する静的タブが含まれています。

タブの認証フローの一般的な概要については、タブ [の認証フローに関するページを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。

タブの認証フローは、ボットの認証フローとは若干異なります。

## <a name="configuring-identity-providers"></a>ID プロバイダーの構成

[ID プロバイダー](~/concepts/authentication/configure-identity-provider.md)としてAzure ADを使用する場合の OAuth 2.0 コールバック リダイレクト URL の構成に関する詳細な手順については、ID プロバイダーの構成に関するトピックを参照してください。

## <a name="initiate-authentication-flow"></a>認証フローを開始する

認証フローは、ユーザー アクションによってトリガーする必要があります。 ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性があるため、認証ポップアップを自動的に開く必要はありません。

必要に応じてユーザーがサインインできるように、構成ページまたはコンテンツ ページにボタンを追加します。 これは、タブ [構成](~/tabs/how-to/create-tab-pages/configuration-page.md) ページまたは [任意のコンテンツ](~/tabs/how-to/create-tab-pages/content-page.md) ページで行うことができます。

Azure ADは、ほとんどの ID プロバイダーと同様に、そのコンテンツを iframe に配置することはできません。 つまり、ID プロバイダーをホストするためにポップアップ ページを追加する必要があります。 次の例では、このページは `/tab-auth/simple-start`. `microsoftTeams.authenticate()` Microsoft Teams クライアント SDK の機能を使用して、ボタンが選択されたときにこのページを起動します。

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

* 渡す `microsoftTeams.authentication.authenticate()` URL は、認証フローの開始ページです。 この例では、次のようになります `/tab-auth/simple-start`。 これは、[Azure AD アプリケーション登録ポータルで登録](https://apps.dev.microsoft.com)したものと一致する必要があります。

* 認証フローは、ドメイン上のページで開始する必要があります。 このドメインは、マニフェストの [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) セクションにも一覧表示する必要があります。 そうしないと、空のポップアップが表示されます。

* 使用 `microsoftTeams.authentication.authenticate()` しないと、サインイン プロセスの最後にポップアップが閉じない場合に問題が発生します。

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>ポップアップ ページから承認ページに移動する

ポップアップ ページ (`/tab-auth/simple-start`) が表示されると、次のコードが実行されます。 このページの主な目的は、ユーザーがサインインできるように ID プロバイダーにリダイレクトすることです。 このリダイレクトは、HTTP 302 を使用してサーバー側で実行できますが、この場合はクライアント側で呼び出し `window.location.assign()`を使用して実行されます。 また、`microsoftTeams.getContext()`これを使用してヒント情報を取得し、Azure ADに渡すこともできます。

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

ユーザーが承認を完了すると、ユーザーはアプリ `/tab-auth/simple-end`で指定したコールバック ページにリダイレクトされます。

### <a name="notes"></a>メモ

* 認証要求と URL の構築に関するヘルプについては、 [ユーザー コンテキスト情報の取得](~/tabs/how-to/access-teams-context.md) に関するページを参照してください。 たとえば、サインインAzure ADの値として`login_hint`ユーザーのログイン名を使用できます。つまり、ユーザーの入力が少なくなる可能性があります。 攻撃者は悪意のあるブラウザーにページを読み込み、必要な情報を提供する可能性があるため、このコンテキストを ID の証明として直接使用しないでください。
* タブ コンテキストはユーザーに関する有用な情報を提供しますが、タブ コンテンツ URL の URL パラメーターとして取得するか、Microsoft Teams クライアント SDK で関数を呼び出`microsoftTeams.getContext()`すかに関係なく、この情報を使用してユーザーを認証しないでください。 悪意のあるアクターが独自のパラメーターを使用してタブ コンテンツ URL を呼び出す可能性があり、偽装Microsoft Teams Web ページが iframe にタブ コンテンツ URL を読み込み、独自のデータを関数に`getContext()`返す可能性があります。 タブ コンテキスト内の ID 関連情報は、単にヒントとして扱い、使用する前に検証する必要があります。
* このパラメーターは `state` 、コールバック URI を呼び出すサービスが呼び出したサービスであることを確認するために使用されます。 コールバック内のパラメーターが `state` 呼び出し中に送信したパラメーターと一致しない場合、戻り値の呼び出しは検証されず、終了する必要があります。
* アプリの manifest.json ファイルの一覧に ID プロバイダーのドメイン `validDomains` を含める必要はありません。

## <a name="the-callback-page"></a>コールバック ページ

最後のセクションでは、Azure AD承認サービスを呼び出し、ユーザーとアプリの情報を渡して、Azure AD独自のモノリシック承認エクスペリエンスをユーザーに提示できるようにしました。 アプリは、このエクスペリエンスで何が起こるかを制御しません。 Azure ADが指定したコールバック ページを呼び出すときに返される内容は、すべて認識されています (`/tab-auth/simple-end`)。

このページでは、Azure ADと呼び出しまたは呼び出`microsoftTeams.authentication.notifySuccess()`しによって返される情報に基づいて、成功または失敗を判断する必要があります`microsoftTeams.authentication.notifyFailure()`。 ログインに成功した場合は、サービス リソースにアクセスできます。

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

このコードは、ヘルパー関数を使用してAzure ADから受信したキーと値の`window.location.hash`ペアを解析します`getHashParameters()`。 認証フローの開始時に`state`指定されたものと同じ値が見つかる`access_token`と、アクセス トークンが呼び出`notifySuccess()`されてタブに返されます。それ以外の場合はエラー`notifyFailure()`が報告されます。

### <a name="notes"></a>メモ

`NotifyFailure()` には、次の定義済みのエラーの理由があります。

* `CancelledByUser` ユーザーは、認証フローを完了する前にポップアップ ウィンドウを閉じました。
* `FailedToOpenWindow` ポップアップ ウィンドウを開くことができませんでした。 ブラウザーでMicrosoft Teamsを実行している場合、これは通常、ポップアップ ブロックによってウィンドウがブロックされたことを意味します。

成功した場合は、ページを更新または再読み込みし、現在認証されたユーザーに関連するコンテンツを表示できます。 認証に失敗すると、エラー メッセージが表示されます。

アプリは、ユーザーが現在のデバイスのタブに戻ったときにもう一度サインインする必要がないように、独自のセッション Cookie を設定できます。

> [!NOTE]
>
> * Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。 既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。 「[SameSite Cookie 属性 (2020 更新プログラム)](../../../resources/samesite-cookie-update.md)」を *参照してください*。
> * Microsoft Teams Free ユーザーとゲスト ユーザーに対して正しいトークンを取得するには、アプリでテナント固有のエンドポイント`https://login.microsoftonline.com/**{tenantId}**`を使用することが重要です。 bot メッセージまたはタブ コンテキストから tenantId を取得できます。 アプリが使用 `https://login.microsoftonline.com/common`されている場合、ユーザーは正しくないトークンを取得し、現在サインインしているテナントではなく "ホーム" テナントにログオンします。

シングル Sign-On (SSO) の詳細については、 [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)に関する記事を参照してください。

## <a name="code-sample"></a>コード サンプル

Azure ADを使用したタブ認証プロセスを示すサンプル コード:

| **サンプルの名前** | **説明** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teams タブ認証 | Azure ADを使用したタブ認証プロセス。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>関連項目

* [ユーザー認証を計画する](../../../concepts/design/understand-use-cases.md)
* [Microsoft Teams 用のタブを設計する](~/tabs/design/tabs.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-aad.md)
* [メッセージ拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)
* [ボットに対するシングル サインオン (SSO) のサポート](~/bots/how-to/authentication/auth-aad-sso-bots.md)
