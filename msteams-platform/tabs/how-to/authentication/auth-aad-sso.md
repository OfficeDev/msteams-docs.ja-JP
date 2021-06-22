---
title: タブのシングル サインオンのサポート
description: シングル サインオン (SSO) について説明します。
ms.topic: how-to
localization_priority: Normal
keywords: teams 認証 SSO AAD シングル サインオン API
ms.openlocfilehash: 1e26189a9a04991c2ad384e58f4fd6d68ca69b6d
ms.sourcegitcommit: 3d02dfc13331b28cffba42b39560cfeb1503abe2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53049037"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>タブのシングル サインオン (SSO) のサポート

ユーザーは、Microsoft Teams、学校、または Microsoft アカウントを通じて、Office 365、Outlookサインインします。 この利点を利用するには、シングル サインオンでデスクトップまたはモバイル クライアントの [Teams] タブまたはタスク モジュールを承認できます。 ユーザーがアプリの使用に同意した場合、自動的にサインインする別のデバイスで再度同意する必要はありません。 さらに、アクセス トークンは、パフォーマンスと読み込み時間を向上させるためにプリフェッチされます。

> [!NOTE]
> **Teams SSO をサポートするモバイル クライアント バージョン**  
>
> ✔Teams (1416/1.0.0.2020073101 以降)
>
> ✔Teams iOS のバージョン (_バージョン_: 2.0.18 以降)  
>
> 最新のバージョンの iOS Teams Android を使用して、アプリのエクスペリエンスを向上します。

> [!NOTE]
> **クイックスタート**  
>
> タブ SSO を使い始める最も簡単なパスは、TeamsツールキットVisual Studio Code。 詳細については、「SSO with [Teamsツールキット」および「Visual Studio Code」を参照してください。](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>実行時の SSO の動作のしくみ

次の図は、SSO プロセスの動作を示しています。

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. タブでは、JavaScript 呼び出しが `getAuthToken()`に対してなされます。 これにより、Teamsアプリケーションの認証トークンを取得する必要があります。
2. 現在のユーザーが初めてタブ アプリケーションを使用する場合は、同意が必要な場合は同意を求める要求プロンプトや、2 要素認証などのステップアップ認証を処理する要求プロンプトが表示されます。
3. Teamsユーザーに対して、Azure Active Directory (AAD) エンドポイントからタブ アプリケーション トークンを要求します。
4. AAD は、タブ アプリケーション トークンをアプリケーションのTeamsします。
5. Teamsによって返される結果オブジェクトの一部としてタブ アプリケーション トークンをタブに送信 `getAuthToken()` します。
6. トークンは JavaScript を使用してタブ アプリケーションで解析され、ユーザーのメール アドレスなどの必要な情報を抽出します。

> [!NOTE]
> この API は、電子メール、プロファイル、および OpenId であるユーザー レベル API の制限されたセット `getAuthToken()` offline_access有効です。 または など、他のスコープGraphには使用 `User.Read` されません `Mail.Read` 。 推奨される回避策については、その他の[スコープGraph参照してください](#apps-that-require-additional-graph-scopes)。

SSO API は、Web コンテンツを [埋め込むタスク](../../../task-modules-and-cards/what-are-task-modules.md) モジュールでも機能します。

## <a name="develop-an-sso-microsoft-teams-tab"></a>[SSO] タブMicrosoft Teamsする

このセクションでは、SSO を使用する [Teams] タブの作成に関連するタスクについて説明します。 これらのタスクは言語とフレームワークに依存しないタスクです。

### <a name="1-create-your-aad-application"></a>1. AAD アプリケーションを作成する

**AAD ポータルの概要に [アプリケーションを登録](https://azure.microsoft.com/features/azure-portal/) するには**

1. [AAD アプリケーション ID を取得します](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。 
1. アプリケーションが AAD エンドポイントに必要なアクセス許可を指定し、必要に応じてGraph。
1. [デスクトップ、web、Teams](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)アプリケーションのアクセス許可を付与します。
1. [スコープのTeams] ボタンを選択し、開くパネルで [スコープ名] とaccess_as_user **を****入力** します。

> [!NOTE]
> 以下の重要な制限を知る必要があります。
>
> * API のアクセス許可Graphユーザー レベルのアクセス許可 (電子メール、プロファイル、offline_access OpenId) だけがサポートされます。 その他のスコープ (Graphアクセスできる必要がある場合は、推奨 `User.Read` `Mail.Read` される回避策を[参照してください](#apps-that-require-additional-graph-scopes)。
> * アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じ名前にすることが重要です。
> * 現在、アプリごとに複数のドメインはサポートされていません。

**AAD ポータルを使用してアプリを登録するには**

1. AAD アプリ登録ポータルに [新しいアプリケーションを登録](https://go.microsoft.com/fwlink/?linkid=2083908) します。
1. [新規 **登録] を選択します**。 [ **アプリケーションの登録] ページ** が表示されます。
1. [アプリケーションの **登録] ページで** 、次の値を入力します。
    1. アプリの **[名前]** を入力します。
    2. [サポートされている **アカウントの種類] を選択し、[** 単一テナント] または [マルチテナント アカウントの種類] を選択します。 ¹
    * **[リダイレクト URI]** を空のままにします。
    3. **[登録]** を選択します。
1. [概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。 アプリケーション マニフェストを更新する際には、後でTeams必要があります。
1. [**管理**] で [**API の公開**] を選択します。

    > [!NOTE]
    > ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次のように入力します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

1. [設定 **] リンクを** 選択して、 の形式でアプリケーション ID URI を生成します `api://{AppID}` 。 2 つのスラッシュと GUID の間に、末尾にスラッシュ "/" が付加された完全修飾ドメイン名を挿入します。 ID 全体に . の形式が必要です `api://fully-qualified-domain-name.com/{AppID}` 。 ² たとえば `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 、 . 完全修飾ドメイン名は、アプリが提供される人間が読み取り可能なドメイン名です。 ngrok などのトンネリング サービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。
1. **[スコープの追加]** を選択します。 開くパネルで、[スコープ名] **access_as_user** を **入力します**。
1. [同意 **できるWho] ボックスに、「****管理者とユーザー」と入力します**。
1. スコープに適した値を使用して管理者とユーザーの同意のプロンプトを構成するための詳細をボックスに入力 `access_as_user` します。
    * **管理者の同意タイトル:** チームはユーザーのプロフィールにアクセスできます。
    * **管理者の同意の** 説明: Teamsアプリの Web API を現在のユーザーとして呼び出す場合があります。
    * **ユーザーの同意タイトル**: Teamsにアクセスして、ユーザーに代わって要求を行うことができます。
    * **ユーザーの同意の説明: Teams** と同じ権限でこのアプリの API を呼び出す場合があります。
1. **[状態]** が **[有効]** に設定されていることを確認してください。
1. [スコープ **の追加] を** 選択して詳細を保存します。 テキスト フィールドの下に表示 **されるスコープ** 名のドメイン 部分は、前の手順で設定した **アプリケーション ID** URI と自動的に一致し、末尾に追加 `/access_as_user` する必要があります `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` 。
1. [承認済 **みクライアント アプリケーション** ] セクションで、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。 [クライアント **アプリケーションの追加] を選択します**。 次の各クライアント ID を入力し、前の手順で作成した承認済みスコープを選択します。
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`モバイルTeamsデスクトップ アプリケーションの場合。
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`web アプリケーションTeamsの場合。
1. **[API のアクセス許可] に移動します**。 [**アクセス許可を**  >  **追加する] Graph** 委任されたアクセス許可を選択し、次のアクセス許可を API から  >  Graphします。
    * User.Read は既定で有効になっています
    * メール
    * offline_access
    * OpenId
    * profile

1. [認証] **に移動します**。

    アプリに IT 管理者の同意が与えされていない場合、ユーザーはアプリを初めて使用する場合に同意する必要があります。

    リダイレクト URI を入力するには、次のコマンドを使用します。
    * [プラットフォーム **の追加] を選択します**。
    * **[Web] を選択します**。
    * アプリの **リダイレクト URI** を入力します。 これは、成功した暗黙的な付与フローがユーザーをリダイレクトするページです。 これは、手順 5 で入力した完全修飾ドメイン名の後に、認証応答が送信される API ルートと同じです。 次のサンプルに従う場合は、Teamsです `https://subdomain.example.com/auth-end` 。

    次のボックスをチェックして暗黙的な付与を有効にする: ✔ ID トークン✔アクセス トークン

お疲れさまでした。 タブ SSO アプリを続行するためのアプリ登録の前提条件が完了しました。

> [!NOTE]
>
> * ¹ AAD アプリが Teams で認証要求を行うのと同じテナントに登録されている場合、ユーザーは同意を求めれなく、アクセス トークンがすぐ付与されます。 ユーザーは、AAD アプリが別のテナントに登録されている場合にのみ、これらのアクセス許可に同意します。
> * ² カスタム ドメインが AAD に追加されていない場合は、ホスト名が既に所有されているドメインに基づいていなければならないというエラーが表示されます。 カスタム ドメインを AAD に追加して登録するには [、AAD](/azure/active-directory/fundamentals/add-custom-domain) にカスタム ドメイン名を追加する手順に従い、手順 5 を繰り返します。 このエラーは、テナントの管理者資格情報でサインインしていない場合Office 365できます。
> * 返されるアクセス トークンでユーザー プリンシパル名 (UPN) を受信していない場合は、AAD でオプションの [クレームとして追加](/azure/active-directory/develop/active-directory-optional-claims) できます。

### <a name="2-update-your-teams-application-manifest"></a>2. アプリケーション マニフェストTeams更新する

次のコードを使用して、新しいプロパティをマニフェストにTeamsします。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** は、次の要素の親です。

> [!div class="checklist"]
> * **id** - アプリケーションのクライアント ID。 これは、Azure アプリケーションへのアプリケーションの登録の一環として取得したアプリケーション ID AD。
>* **resource** - アプリケーションのドメインとサブドメイン。 これは、手順 6 で作成するときに登録したのと同じ URI (プロトコルを含む `api://` ) `scope` です。 リソースにパスを `access_as_user` 含めなけれ。 この URI のドメイン部分は、アプリケーション マニフェストの URL で使用されるサブドメインを含むドメインTeams必要があります。

> [!NOTE]
>
>* AAD アプリのリソースは、通常、サイト URL のルートと appID (たとえば) です `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。 この値は、要求が同じドメインから送信されるのを確認するためにも使用されます。 タブの `contentURL` リソース プロパティと同じドメインが使用されます。
>* フィールドを実装するには、マニフェスト バージョン 1.5 以上を使用する必要 `webApplicationInfo` があります。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. クライアント側コードから認証トークンを取得する

次の認証 API を使用します。

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

ユーザー レベルのアクセス許可を呼び出し、追加のユーザーの同意が必要な場合は、追加の同意を付与するためのダイアログ `getAuthToken` がユーザーに表示されます。

成功コールバックでアクセス トークンを受信した後、アクセス トークンをデコードして、そのトークンに関連付けられているクレームを表示できます。 必要に応じて、アクセス トークンを手動でコピーしてツールに貼り付[](https://jwt.ms/)けます (コンテンツを jwt.ms など)。 返されるアクセス トークンで UPN を受信していない場合は、AAD でオプションのクレーム [として](/azure/active-directory/develop/active-directory-optional-claims) 追加できます。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>コード サンプル

|**サンプル名**|**説明**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| タブ SSO |Microsoft Teamsのサンプル アプリ Azure AD SSO| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、 </br>[Teams Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>既知の制限

### <a name="apps-that-require-additional-graph-scopes"></a>追加のスコープを必要とするGraphアプリ

SSO の現在の実装では、メール、プロファイル、offline_access、OpenId などのユーザー レベルのアクセス許可に対する同意のみを付与し、User.Read や Mail.Read などの他の API には同意しません。 アプリがスコープをさらにGraph場合は、次のセクションで有効にする回避策を示します。

#### <a name="tenant-admin-consent"></a>テナント管理者の同意

最も簡単な方法は、組織の代わりにテナント管理者に事前同意を得る方法です。 つまり、ユーザーはこれらのスコープに同意する必要が無く、AAD の代理フローを使用してトークン サーバー側を自由に交換 [できます](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。 この回避策は、社内の業務用アプリケーションでは受け入れ可能ですが、テナント管理者の承認に依存できないサードパーティの開発者には十分ではありません。

テナント管理者として組織に代わって同意する簡単な方法は、 を参照する方法です `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` 。

#### <a name="ask-for-additional-consent-using-the-auth-api"></a>Auth API を使用して追加の同意を求める

Graph スコープを追加するもう 1 つの方法は、Azure AD 同意ダイアログ ボックスをポップアップする既存の Web ベース[の Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)認証アプローチを使用して同意ダイアログを表示する方法です。 

**Auth API を使用して追加の同意を求めるには**

1. これらの追加の API へのアクセスを取得するには `getAuthToken()` 、AAD [on-half-Graph of](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow を使用してサーバー側で交換する必要があります。 この交換に v2 Graphエンドポイントを使用してください。
2. Exchange が失敗した場合、AAD は無効な付与例外を返します。 通常、2 つのエラー メッセージの 1 つ、 `invalid_grant` または `interaction_required` .
3. 交換が失敗した場合は、追加の同意を求める必要があります。 ユーザーに追加の同意を許可するユーザー インターフェイス (UI) を表示します。 この UI には、AAD 認証 API を使用して AAD 同意ダイアログ ボックスをトリガーする [ボタンが含まれる必要があります](~/concepts/authentication/auth-silent-aad.md)。
4. AAD から追加の同意を求める場合は、クエリ文字列パラメーターを AAD に含める必要があります。それ以外の場合、AAD は追加のスコープを `prompt=consent` 求めずに[](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)行います。
    * 代わりに `?scope={scopes}`
    * これを使用する `?prompt=consent&scope={scopes}`
    * Mail.Read や User.Read など、ユーザーに求めるすべてのスコープ `{scopes}` が含まれるか確認します。
5. ユーザーが追加のアクセス許可を付与したら、これらの追加 API へのアクセスを取得するために、フローの代理を再試行します。

### <a name="non-aad-authentication"></a>AAD 以外の認証

上記の認証ソリューションは、ID プロバイダーとして AAD をサポートするアプリとサービスでのみ機能します。 AAD ベース以外のサービスを使用して認証するアプリは、ポップアップ ベースの Web 認証フローを引き続き [使用する必要があります](~/concepts/authentication.md)。

> [!NOTE]
> SSO は、AAD B2C テナント内の顧客所有アプリでサポートされます。
