---
title: シングル サインオン
description: シングルサインオン (SSO) について説明します。
keywords: teams 認証 SSO AAD
ms.openlocfilehash: 1857651aecd902f04bd57f5b4e2fb0fda88eb348
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674635"
---
# <a name="single-sign-on"></a><span data-ttu-id="2d9ab-104">シングル サインオン</span><span class="sxs-lookup"><span data-stu-id="2d9ab-104">Single Sign-On</span></span>

> [!NOTE]
> <span data-ttu-id="2d9ab-105">現在、"シングルサインオン" API は_開発者向けプレビュー_でのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-105">The "single sign-on" API is currently supported in _Developer Preview_ only.</span></span>

<span data-ttu-id="2d9ab-106">ユーザーが職場または学校 (Office 365) アカウントを使用して Microsoft Teams にサインインし、シングルサインオン (SSO) を使用して Microsoft Teams タブにユーザーを承認することで、この機能を利用できるようになります。これは、ユーザーがデスクトップでアプリを使用することを同意する場合、モバイルで再び同意する必要がなく、自動的にログインされることを意味します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-106">Users sign-in to Microsoft Teams using their work or school (Office 365) account and you can take advantage of this by using single sign-on (SSO) to authorize the user to your Microsoft Teams tab. That means if a user consents to use your app on desktop, they won’t have to consent again on mobile and will be automatically logged in.</span></span> 

## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="2d9ab-107">実行時の SSO の動作のしくみ</span><span class="sxs-lookup"><span data-stu-id="2d9ab-107">How SSO works at runtime</span></span>

<span data-ttu-id="2d9ab-108">次の図は、SSO プロセスのしくみを示しています。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-108">The following diagram shows how the SSO process works:</span></span>

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="2d9ab-109">タブで、JavaScript は getAuthToken () を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-109">In the tab, JavaScript calls getAuthToken().</span></span> <span data-ttu-id="2d9ab-110">これにより、Teams アプリケーションに対して、タブアプリケーションへの認証トークンを取得するように指示します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-110">This tells the Teams application to obtain an authentication token to the tab application.</span></span>
2. <span data-ttu-id="2d9ab-111">現在のユーザーが初めてタブアプリケーションを使用していた場合は、同意を求めるメッセージが表示されます (同意が必要な場合)。または、手順アップ認証 (2 要素認証など) の処理を求められます。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-111">If this is the first time the current user has used your tab application, they will be prompted to consent (if consent is required) or asked to handle step-up authentication (such as two-factor authentication).</span></span>
3. <span data-ttu-id="2d9ab-112">Microsoft Teams アプリケーションは、現在のユーザーの Azure AD v2.0 エンドポイントからタブアプリケーショントークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-112">The Microsoft Teams application requests the tab application token from the Azure AD v1.0 endpoint for the current user.</span></span>
4. <span data-ttu-id="2d9ab-113">Azure AD は、タブアプリケーショントークンを Teams アプリケーションに送信します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-113">Azure AD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="2d9ab-114">Microsoft Teams アプリケーションは、getAuthToken () 呼び出しによって返される result オブジェクトの一部として、タブにタブアプリケーショントークンを送信します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-114">The Microsoft Teams application sends the tab application token to the tab as part of the result object returned by the getAuthToken() call.</span></span>
6. <span data-ttu-id="2d9ab-115">タブアプリケーションの JavaScript は、トークンを解析し、ユーザーの電子メールアドレスなど、必要な情報を抽出できます。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-115">JavaScript in the tab application can parse the token and extract the information it needs, such as the user's email address.</span></span>
    * <span data-ttu-id="2d9ab-116">注: このトークンは、限られたレベルのユーザーレベルの Api (例: 電子メール、プロファイルなど) に対してのみ有効であり、その他のグラフスコープ (同意など) では使用できません。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-116">Note: this token is only valid for consenting to a limited set of user-level APIs (ex: email, profile, etc)  and not for further Graph scopes (such as Mail.Read).</span></span> <span data-ttu-id="2d9ab-117">追加のグラフスコープが必要な場合の回避策については、このドキュメントの最後にあるセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-117">See our section at the end of this document for suggested workarounds if you require additional Graph scopes.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="2d9ab-118">SSO Microsoft Teams タブを開発する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-118">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="2d9ab-119">このセクションでは、SSO を使用する Microsoft Teams タブの作成に関連するタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-119">This section describes the tasks involved in creating an Microsoft Teams tab that use SSO.</span></span> <span data-ttu-id="2d9ab-120">ここでは、これらのタスクについて、言語とフレームワークに依存しない方法で説明しています。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-120">These tasks are described here in a language- and framework-agnostic way.</span></span>

### <a name="1-create-your-aad-application-in-azure"></a><span data-ttu-id="2d9ab-121">1. Azure で AAD アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-121">1. Create your AAD application in Azure</span></span>

<span data-ttu-id="2d9ab-122">Azure AD v2.0 エンドポイントの登録ポータルでアプリケーションを登録します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-122">Register you application at the registration portal for the Azure AD v1.0 endpoint.</span></span> <span data-ttu-id="2d9ab-123">このプロセスには、次に示すタスクを含めて 5 分から 10 分の時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-123">This is a 5–10 minute process that includes the following tasks:</span></span>

* <span data-ttu-id="2d9ab-124">AAD アプリケーション ID を取得する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-124">Getting your AAD application ID</span></span>
* <span data-ttu-id="2d9ab-125">AAD エンドポイント (およびオプションで Microsoft Graph) に対してアプリケーションに必要なアクセス許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-125">Specify the permissions that your application needs for the AAD endpoint (and optionally to Microsoft Graph).</span></span> 
* <span data-ttu-id="2d9ab-126">アプリケーションに信頼するように Microsoft Teams デスクトップ、web、モバイルアプリケーションに付与する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-126">Grant the Microsoft Teams desktop, web and mobile application to trust to your application</span></span>
* <span data-ttu-id="2d9ab-127">既定の`access_as_user`スコープ名を使用して、アプリに対して Microsoft Teams アプリケーションを事前認証します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-127">Preauthorize the Microsoft Teams application to your app with the default scope name of `access_as_user`.</span></span>

> [!NOTE]
> <span data-ttu-id="2d9ab-128">注意すべき重要な制限がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-128">There are some important restrictions you should be aware of:</span></span>
>
> * <span data-ttu-id="2d9ab-129">ユーザーレベルの Graph API のアクセス許可 (ie: email、profile、offline_access、openid) のみサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-129">We only support user-level Graph API permissions (ie: email, profile, offline_access, openid.</span></span> <span data-ttu-id="2d9ab-130">他のグラフスコープにアクセスする必要がある場合は、このドキュメントの最後にある「推奨される回避策」をお読みください。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-130">If you need access to other Graph scopes, read our recommended workaround at the end of this documentation.</span></span>
> * <span data-ttu-id="2d9ab-131">アプリケーションのドメイン名が Azure AD アプリケーションに登録されていることが重要です。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-131">It's important that your application's domain name be registered with your Azure AD application.</span></span> <span data-ttu-id="2d9ab-132">これは、Teams で認証トークンを要求するときにアプリケーションが実行するドメイン名と同じである必要があります。また、Teams のマニフェストでリソースのプロパティを指定するときにも、次のセクションの詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-132">This must be the same domain name that your application runs on when requesting an authentication token in Teams and also when specifying the resource property in your Teams manifest (more details in the next section).</span></span>
> * <span data-ttu-id="2d9ab-133">現在、アプリごとに複数のドメインをサポートしていません</span><span class="sxs-lookup"><span data-stu-id="2d9ab-133">We do not currently support multiple domains per app</span></span>
> * <span data-ttu-id="2d9ab-134">また、このドメインが一般的すぎるために`azurewebsites.net`ドメインを使用するアプリケーションをサポートしておらず、セキュリティリスクになる可能性もあります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-134">We also do not support applications that use the `azurewebsites.net` domain since this domain is too common and may be a security risk</span></span>

#### <a name="steps"></a><span data-ttu-id="2d9ab-135">手順</span><span class="sxs-lookup"><span data-stu-id="2d9ab-135">Steps</span></span>

1. <span data-ttu-id="2d9ab-136">新しいアプリケーションを[Azure Active Directory に登録する–アプリ登録](https://go.microsoft.com/fwlink/?linkid=2083908)ポータル</span><span class="sxs-lookup"><span data-stu-id="2d9ab-136">Register a new application in the [Azure Active Directory – App Registration](https://go.microsoft.com/fwlink/?linkid=2083908) portal</span></span>
2. <span data-ttu-id="2d9ab-137">[新しい登録] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-137">Select “New Registration”.</span></span> <span data-ttu-id="2d9ab-138">[アプリケーションの登録] ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-138">On the register an application page, set the values as follows:</span></span>
    * <span data-ttu-id="2d9ab-139">**名前**をアプリ名に設定します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-139">Set **name** to your app name</span></span>
    * <span data-ttu-id="2d9ab-140">**任意の組織ディレクトリおよび個人の Microsoft アカウントのアカウント**に**サポートされているアカウントの種類**を設定する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-140">Set **supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**</span></span>
    * <span data-ttu-id="2d9ab-141">**リダイレクト URI**を空のままにする</span><span class="sxs-lookup"><span data-stu-id="2d9ab-141">Leave **Redirect URI** empty</span></span>
    * <span data-ttu-id="2d9ab-142">[**登録**] を選択する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-142">Choose **Register**</span></span>
3. <span data-ttu-id="2d9ab-143">[概要] ページで、**アプリケーション (クライアント) ID**をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-143">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="2d9ab-144">Teams アプリケーションマニフェストを更新するときには、後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-144">You’ll need it later when updating your Teams application manifest.</span></span>
4. <span data-ttu-id="2d9ab-145">**[管理]** の下の **[API の公開]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-145">Select **Expose an API** under **Manage**.</span></span> <span data-ttu-id="2d9ab-146">[**設定**] リンクを選択して、アプリケーション ID URI をの`api://{AppID}`形式で生成します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-146">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="2d9ab-147">二重スラッシュと GUID の間に、完全修飾ドメイン名 (末尾にスラッシュ "/" を付加したもの) を挿入します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-147">Insert your fully qualified domain name (with a forward slash "/" appended to the end) between the double forward slashes and the GUID.</span></span> <span data-ttu-id="2d9ab-148">ID 全体の形式は次のようになります。`api://fully-qualified-domain-name.com/{AppID}`</span><span class="sxs-lookup"><span data-stu-id="2d9ab-148">The entire ID should have the form of: `api://fully-qualified-domain-name.com/{AppID}`</span></span>
    * <span data-ttu-id="2d9ab-149">ex: `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-149">ex: `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`.</span></span>

> [!NOTE]
> <span data-ttu-id="2d9ab-150">ドメインを所有しているにもかかわらず、そのドメインが既に所有されているというエラーが表示される場合は、「[クイック スタート: カスタム ドメイン名を Azure Active Directory に追加する](/azure/active-directory/fundamentals/add-custom-domain)」の手順に従って登録し、この手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-150">If you get an error saying that the domain is already owned but you own it, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) to register it, and then repeat this step.</span></span> <span data-ttu-id="2d9ab-151">このエラーは、Office 365 テナントの管理者の資格情報を使用してサインインしていない場合にも発生します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-151">(This error can also occur if you are not signed in with credentials of an admin in the Office 365 tenancy).</span></span>

5. <span data-ttu-id="2d9ab-152">**[Scope の追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-152">Select the **Add a scope** button.</span></span> <span data-ttu-id="2d9ab-153">開いたパネルで、**[スコープ名]** として `access_as_user` を入力します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-153">In the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>
6. <span data-ttu-id="2d9ab-154">同意できるユーザーを設定する管理者とユーザーに対して</span><span class="sxs-lookup"><span data-stu-id="2d9ab-154">Set Who can consent? to Admins and users</span></span>
7. <span data-ttu-id="2d9ab-155">[管理者] と [ユーザーの同意] の入力を構成するためのフィールドに`access_as_user` 、範囲に適した値を入力します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-155">Fill in the fields for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope.</span></span> <span data-ttu-id="2d9ab-156">提案:</span><span class="sxs-lookup"><span data-stu-id="2d9ab-156">Suggestions:</span></span>
    * <span data-ttu-id="2d9ab-157">**管理者の同意のタイトル:** Teams はユーザーのプロファイルにアクセスできます</span><span class="sxs-lookup"><span data-stu-id="2d9ab-157">**Admin consent title:** Teams can access the user’s profile</span></span>
    * <span data-ttu-id="2d9ab-158">**管理者の同意の説明**: Teams は、現在のユーザーとしてアプリの web api を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-158">**Admin consent description**: Allows Teams to call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="2d9ab-159">**ユーザーの同意のタイトル**: Teams はユーザープロファイルにアクセスして、自分の代わりに要求を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-159">**User consent title**: Teams can access your user profile and make requests on your behalf</span></span>
    * <span data-ttu-id="2d9ab-160">**ユーザーの同意の説明:** Teams が同じ権限でこのアプリの Api を呼び出せるようにします。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-160">**User consent description:** Enable Teams to call this app’s APIs with the same rights that you have</span></span>
8. <span data-ttu-id="2d9ab-161">**状態**が**有効**に設定されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-161">Ensure that **State** is set to **Enabled**</span></span>
9. <span data-ttu-id="2d9ab-162">[**範囲の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-162">Select **Add scope**</span></span>
    * <span data-ttu-id="2d9ab-163">注: テキストフィールドのすぐ下に表示される**スコープ名**のドメイン部分は、前の手順で設定した**アプリケーション ID** URI と`/access_as_user`一致するように、末尾に追加する必要があります。例えば：</span><span class="sxs-lookup"><span data-stu-id="2d9ab-163">Note: The domain part of the **Scope name** displayed just below the text field should automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end; for example:</span></span> 
        * `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7/access_as_user`
10. <span data-ttu-id="2d9ab-164">[承認された**クライアントアプリケーション**] セクションで、アプリの web アプリケーションに承認するアプリケーションを特定します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-164">In the **Authorized client applications** section, you identify the applications that you want to authorize to your app’s web application.</span></span> <span data-ttu-id="2d9ab-165">次の各 Id を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-165">Each of the following IDs needs to be entered:</span></span>
    * <span data-ttu-id="2d9ab-166">`1fec8e78-bce4-4aaf-ab1b-5451cc387264`(Teams モバイル/デスクトップアプリケーション)</span><span class="sxs-lookup"><span data-stu-id="2d9ab-166">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams mobile/desktop application)</span></span>
    * <span data-ttu-id="2d9ab-167">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346`(Teams web アプリケーション)</span><span class="sxs-lookup"><span data-stu-id="2d9ab-167">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web application)</span></span>
11. <span data-ttu-id="2d9ab-168">[ **API アクセス許可**] に移動し、次のアクセス許可を追加していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-168">Navigate to **API Permissions**, and make sure to add the follow permissions:</span></span>
    * <span data-ttu-id="2d9ab-169">User. 読み取り (既定では有効)</span><span class="sxs-lookup"><span data-stu-id="2d9ab-169">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="2d9ab-170">メール</span><span class="sxs-lookup"><span data-stu-id="2d9ab-170">email</span></span>
    * <span data-ttu-id="2d9ab-171">offline_access</span><span class="sxs-lookup"><span data-stu-id="2d9ab-171">offline_access</span></span>
    * <span data-ttu-id="2d9ab-172">openid</span><span class="sxs-lookup"><span data-stu-id="2d9ab-172">openid</span></span>
    * <span data-ttu-id="2d9ab-173">profile</span><span class="sxs-lookup"><span data-stu-id="2d9ab-173">profile</span></span>

### <a name="2-update-your-microsoft-teams-application-manifest"></a><span data-ttu-id="2d9ab-174">2. Microsoft Teams アプリケーションマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-174">2. Update your Microsoft Teams application manifest</span></span>

<span data-ttu-id="2d9ab-175">Microsoft Teams のマニフェストに新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-175">Add new properties to your Microsoft Teams manifest:</span></span>

* <span data-ttu-id="2d9ab-176">**WebApplicationInfo** - 次の要素の親。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-176">**WebApplicationInfo** - The parent of the following elements.</span></span>
* <span data-ttu-id="2d9ab-177">**Id** -アプリケーションのクライアント id。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-177">**Id** - The client ID of the application.</span></span> <span data-ttu-id="2d9ab-178">これは、アプリケーションを Azure AD 1.0 エンドポイントに登録する際に取得するアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-178">This is an application ID that you obtain as part of registering the application with Azure AD 1.0 endpoint.</span></span>
* <span data-ttu-id="2d9ab-179">**Resource** -アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-179">**Resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="2d9ab-180">これは、AAD にアプリを登録`api://`するときに使用したものと同じ URI (プロトコルを含む) です。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-180">This is the same URI (including the `api://` protocol) that you used when registering the app in AAD.</span></span> <span data-ttu-id="2d9ab-181">この URI のドメイン部分は、Teams アプリケーションマニフェストのセクションの Url で使用されているすべてのサブドメインを含むドメインと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-181">The domain part of this URI should match the domain, including any subdomains, used in the URLs in the section of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "<application_GUID here>",
  "resource": "<web_API resource here>"
}
```

<span data-ttu-id="2d9ab-182">注:</span><span class="sxs-lookup"><span data-stu-id="2d9ab-182">Notes:</span></span>

* <span data-ttu-id="2d9ab-183">AAD アプリのリソースは、通常、そのサイトの URL と appID (例`api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`) のルートにすぎません。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-183">The resource for an AAD app will usually just be the root of its site URL and the appID (e.g. `api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`).</span></span> <span data-ttu-id="2d9ab-184">また、この値を使用して、要求が同じドメインから送信されるようにします。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-184">We also use this value to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="2d9ab-185">Therefor タブ`contentURL`のがリソースプロパティと同じドメインを使用していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-185">Therefor make sure that your `contentURL` for your tab uses the same domains as your resource property.</span></span>
* <span data-ttu-id="2d9ab-186">これらのフィールドを使用するには、マニフェストバージョン1.5 またはそれ以降を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-186">You need to be using manifest version 1.5 or higher for these fields to be used.</span></span>
* <span data-ttu-id="2d9ab-187">範囲はマニフェストではサポートされていません。代わりに、Azure portal の API 権限セクションで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-187">Scopes aren’t supported in the manifest and instead should be specified in the API Permissions section in the Azure portal</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="2d9ab-188">3. クライアント側のコードから認証トークンを取得する</span><span class="sxs-lookup"><span data-stu-id="2d9ab-188">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="2d9ab-189">認証 API は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-189">Here's what the authentication API looks like:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); },
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="2d9ab-190">を呼び出し`getAuthToken`て、ユーザーレベルの権限に対してユーザーの同意を追加する必要がある場合は、追加の同意を付与するためのダイアログがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-190">When you call `getAuthToken` - and additional user consent is required (for user-level permissions) - we will show a dialog to the user encouraging them to grant additional consent.</span></span> 

<img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>

## <a name="demo-code"></a><span data-ttu-id="2d9ab-191">デモコード</span><span class="sxs-lookup"><span data-stu-id="2d9ab-191">Demo code</span></span>

<span data-ttu-id="2d9ab-192">ここでは、「test application [Task Meow](https://github.com/ydogandjiev/taskmeow) 」を参照し、SSO マニフェストを使用`teams.auth.service.js`し`sso.auth.service.js`て、およびファイルをチェックアウトし、認証ワークフローの処理方法を確認できます。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-192">For now you can visit our test application [Task Meow](https://github.com/ydogandjiev/taskmeow) and use the SSO manifest and checkout the `teams.auth.service.js` and `sso.auth.service.js` file to see how we handle the authentication workflow.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="2d9ab-193">既知の制限</span><span class="sxs-lookup"><span data-stu-id="2d9ab-193">Known Limitations</span></span>

### <a name="apps-that-require-additional-graph-scopes"></a><span data-ttu-id="2d9ab-194">追加のグラフスコープが必要なアプリ</span><span class="sxs-lookup"><span data-stu-id="2d9ab-194">Apps that require additional Graph Scopes</span></span>

<span data-ttu-id="2d9ab-195">現在の SSO の実装では、ユーザーレベルのアクセス許可 (電子メール、プロファイル、offline_access、openid) に対する同意のみが付与されますが、その他の Api (メールなど) については同意しません。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-195">Our current implementation for SSO only grants consent for user-level permissions (email, profile, offline_access, openid) but not for other APIs (such as Mail.Read).</span></span> <span data-ttu-id="2d9ab-196">アプリにさらにグラフスコープが必要な場合は、これを有効にするための回避策がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-196">If your app needs further Graph scopes, there are some workarounds to enable this.</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="2d9ab-197">テナント管理者の同意</span><span class="sxs-lookup"><span data-stu-id="2d9ab-197">Tenant Admin Consent</span></span>

<span data-ttu-id="2d9ab-198">最も簡単な方法は、テナント管理者が組織の代わりに事前同意を得ることです。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-198">The simplest approach would be to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="2d9ab-199">これは、ユーザーがこれらのスコープに同意する必要がないことを意味します。これにより、AAD の送信[フロー](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)を使用してトークンサーバー側を自由に交換できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-199">This means users won’t have to consent to these scopes and you can then be free to exchange the token server side using AAD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="2d9ab-200">内部の基幹業務アプリケーションではこの回避策は許容されますが、テナント管理者の承認を利用できない可能性がある Isv にとっては十分ではない場合があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-200">This workaround is acceptable for internal line-of-business applications but may not be enough for ISVs who may not be able to rely on tenant admin approval.</span></span>

<span data-ttu-id="2d9ab-201">組織の代わりに (テナント管理者として) 同意を簡単に参照するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-201">A simple way of consenting on behalf of an organization (as a tenant admin) is to visit:</span></span>

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="2d9ab-202">Auth API を使用して追加の同意を求める</span><span class="sxs-lookup"><span data-stu-id="2d9ab-202">Asking for additional consent using the Auth API</span></span>

<span data-ttu-id="2d9ab-203">追加のグラフスコープを取得するためのもう1つの方法は、既存[の web ベースの aad 認証方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)を使用して、aad 同意ダイアログをポップアップするという同意ダイアログを表示することです。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-203">Another approach for getting additional Graph scopes would be to present a consent dialog using our existing [web-based AAD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an AAD consent dialog.</span></span> <span data-ttu-id="2d9ab-204">注目すべき追加事項がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-204">There are some notable additions:</span></span>

1. <span data-ttu-id="2d9ab-205">GetAuthToken を使用して取得したトークンは、その追加の Graph Api へのアクセスを取得するために、[代理送信フロー](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)を使用してサーバー側を交換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-205">The token retrieved using getAuthToken would need to be exchanged server side using AADs [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow) to get access to those additional Graph APIs.</span></span>
    * <span data-ttu-id="2d9ab-206">必ず、この exchange の v2 Graph エンドポイントを使用してください。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-206">Be sure to use the v2 Graph endpoint for this exchange</span></span>
2. <span data-ttu-id="2d9ab-207">Exchange に障害が発生した場合、AAD は無効な付与の例外を返します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-207">If the exchange fails, AAD will return an invalid grant exception.</span></span> <span data-ttu-id="2d9ab-208">通常、次の2つのエラーメッセージ`ConsentRequired`のいずれかがあります。`InteractionRequired`</span><span class="sxs-lookup"><span data-stu-id="2d9ab-208">There are usually one of two error messages: `ConsentRequired` or `InteractionRequired`</span></span>
3. <span data-ttu-id="2d9ab-209">Exchange に障害が発生した場合は、追加の同意を求める必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-209">When the exchange fails, then you need to ask for additional consent.</span></span> <span data-ttu-id="2d9ab-210">ユーザーに追加の同意を付与するように求める UI を表示することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-210">We recommend showing some UI asking the user to grant additional consent.</span></span> <span data-ttu-id="2d9ab-211">この UI には、 [aad 認証 API](~/concepts/authentication/auth-silent-aad.md)を使用して aad 同意ダイアログをトリガーするボタンが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-211">This UI should include a button that triggers an AAD consent dialog using our [AAD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="2d9ab-212">AAD から追加の同意を求めている場合は、 `prompt=consent` aad に[クエリ文字列-パラメーター](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)を含める必要があります。それ以外の場合、aad は追加のスコープを要求しません。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-212">When asking for additional consent from AAD, you need to include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to AAD otherwise AAD will not ask for the additional scopes.</span></span>
    * <span data-ttu-id="2d9ab-213">代わりに：`?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="2d9ab-213">Instead of: `?scope={scopes}`</span></span>
    * <span data-ttu-id="2d9ab-214">使用するもの:`?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="2d9ab-214">Use this: `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="2d9ab-215">ユーザーに対し`{scopes}`て要求しているすべてのスコープが含まれていることを確認してください (例: Mail. read または User. read)。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-215">Be sure that `{scopes}` includes all the scopes you are prompting the user for (ex: Mail.Read or User.Read).</span></span>
5. <span data-ttu-id="2d9ab-216">ユーザーが追加のアクセス許可を付与した後、代理送信を再試行して、追加の Api へのアクセス権を取得します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-216">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-aad-authentication"></a><span data-ttu-id="2d9ab-217">非 AAD 認証</span><span class="sxs-lookup"><span data-stu-id="2d9ab-217">Non-AAD Authentication</span></span>

<span data-ttu-id="2d9ab-218">前述の認証ソリューションは、id プロバイダーとして Azure AD をサポートするアプリとサービスに対してのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-218">The above-described authentication solution only works for apps and services that support Azure AD as an identity provider.</span></span> <span data-ttu-id="2d9ab-219">AAD 以外のサービスを使用して認証するアプリは、ポップアップベースの[web 認証フロー](~/concepts/authentication.md)を引き続き使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9ab-219">Apps that want to authenticate using non-AAD based services need to continue using the popup-based [web authentication flow](~/concepts/authentication.md).</span></span>
