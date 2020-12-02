---
title: タブのシングルサインオンのサポート
description: シングルサインオン (SSO) について説明します。
keywords: teams 認証 SSO AAD シングルサインオン api
ms.openlocfilehash: 08ad1ab55a06ccb887755322fbd572f745952d8e
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552452"
---
# <a name="single-sign-on-sso-support-for-tabs"></a><span data-ttu-id="d4327-104">タブのシングルサインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="d4327-104">Single sign-on (SSO) support for tabs</span></span>

<span data-ttu-id="d4327-105">ユーザーは、職場、学校、または Microsoft アカウント (Office 365、Outlook など) 経由で Microsoft Teams にサインインします。</span><span class="sxs-lookup"><span data-stu-id="d4327-105">Users sign in to Microsoft Teams via their work, school, or Microsoft accounts (Office 365, Outlook, etc).</span></span> <span data-ttu-id="d4327-106">この機能を利用すると、シングルサインオンで、デスクトップまたはモバイルクライアントの Microsoft Teams タブ (またはタスクモジュール) を承認できるようになります。</span><span class="sxs-lookup"><span data-stu-id="d4327-106">You can take advantage of this by allowing a single sign-on to authorize your Microsoft Teams tab (or task module) on desktop or mobile clients.</span></span> <span data-ttu-id="d4327-107">そのため、ユーザーがアプリを使用することに同意場合、別のデバイスで再び同意する必要はありません。自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="d4327-107">Thus, if a user consents to use your app, they won’t have to consent again on another device — they will be signed in automatically.</span></span> <span data-ttu-id="d4327-108">また、アクセストークンをプリフェッチして、パフォーマンスと負荷の時間を短縮します。</span><span class="sxs-lookup"><span data-stu-id="d4327-108">In addition, we prefetch your access token to improve performance and load times.</span></span>

>[!NOTE]
> <span data-ttu-id="d4327-109">**SSO をサポートする Teams モバイルクライアントバージョン**</span><span class="sxs-lookup"><span data-stu-id="d4327-109">**Teams mobile client versions supporting SSO**</span></span>  
>
> <span data-ttu-id="d4327-110">Android 用の✔ Teams (1416/1.0.0.2020073101 以降)</span><span class="sxs-lookup"><span data-stu-id="d4327-110">✔Teams for Android (1416/1.0.0.2020073101 and later)</span></span>
>
> <span data-ttu-id="d4327-111">✔ Teams for iOS (_バージョン_: 2.0.18 以降)</span><span class="sxs-lookup"><span data-stu-id="d4327-111">✔Teams for iOS (_Version_: 2.0.18 and later)</span></span>  
>
> <span data-ttu-id="d4327-112">Teams でのベストな利便性を実現するため、iOS と Android の最新バージョンをご利用ください。</span><span class="sxs-lookup"><span data-stu-id="d4327-112">For the best experience with Teams, please use the latest version of iOS and Android.</span></span>

>[!NOTE]
> <span data-ttu-id="d4327-113">**クイックスタート**</span><span class="sxs-lookup"><span data-stu-id="d4327-113">**Quickstart**</span></span>  
>
> <span data-ttu-id="d4327-114">Tab SSO を使用して作業を開始するための最も簡単なパスは、Microsoft Teams Toolkit for Visual Studio Code です。</span><span class="sxs-lookup"><span data-stu-id="d4327-114">The simplest path to getting started with tab SSO is with the Microsoft Teams Toolkit for Visual Studio Code.</span></span> [<span data-ttu-id="d4327-115">詳細情報</span><span class="sxs-lookup"><span data-stu-id="d4327-115">Learn more</span></span>](../../../toolkit/visual-studio-code-tab-sso.md)


## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="d4327-116">実行時の SSO の動作のしくみ</span><span class="sxs-lookup"><span data-stu-id="d4327-116">How SSO works at runtime</span></span>

<span data-ttu-id="d4327-117">次の図は、SSO プロセスのしくみを示しています。</span><span class="sxs-lookup"><span data-stu-id="d4327-117">The following diagram shows how the SSO process works:</span></span>

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="d4327-118">タブで、に対して JavaScript 呼び出しが行われ `getAuthToken()` ます。</span><span class="sxs-lookup"><span data-stu-id="d4327-118">In the tab, a JavaScript call is made to `getAuthToken()`.</span></span> <span data-ttu-id="d4327-119">これにより、チームはタブアプリケーションの認証トークンを取得するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="d4327-119">This tells Teams to obtain an authentication token for the tab application.</span></span>
2. <span data-ttu-id="d4327-120">現在のユーザーが初めてタブアプリケーションを使用していた場合は、同意を求めるメッセージが表示されます (同意が必要な場合)。または、ステップアップ認証 (2 要素認証など) を処理するための要求があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-120">If this is the first time the current user has used your tab application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>
3. <span data-ttu-id="d4327-121">Teams は、現在のユーザーの Azure AD エンドポイントからタブアプリケーショントークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="d4327-121">Teams requests the tab application token from the Azure AD endpoint for the current user.</span></span>
4. <span data-ttu-id="d4327-122">Azure AD は、タブアプリケーショントークンを Teams アプリケーションに送信します。</span><span class="sxs-lookup"><span data-stu-id="d4327-122">Azure AD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="d4327-123">チームは、呼び出しによって返される result オブジェクトの一部として、タブにタブアプリケーショントークンを送信し `getAuthToken()` ます。</span><span class="sxs-lookup"><span data-stu-id="d4327-123">Teams sends the tab application token to the tab as part of the result object returned by the `getAuthToken()` call.</span></span>
6. <span data-ttu-id="d4327-124">このトークンは、JavaScript を使用してタブアプリケーションで解析され、ユーザーの電子メールアドレスなど、必要な情報を抽出します。</span><span class="sxs-lookup"><span data-stu-id="d4327-124">The token will be parsed in the tab application, via JavaScript, to extract the needed information, such as the user's email address.</span></span>

> [!NOTE]
> <span data-ttu-id="d4327-125">は、 `getAuthToken()` 同意に対してのみ、ユーザーレベルの api の制限付きセット (電子メール、プロファイル、offline_access および OpenId) に対してのみ有効です `User.Read` 。また、またはなどの Microsoft Graph スコープでは使用できません `Mail.Read` 。</span><span class="sxs-lookup"><span data-stu-id="d4327-125">The `getAuthToken()` is only valid for consenting to a limited set of user-level APIs — email, profile, offline_access and OpenId — and not for further Microsoft Graph scopes such as `User.Read` or `Mail.Read`.</span></span> <span data-ttu-id="d4327-126">[追加のグラフスコープ](#apps-that-require-additional-microsoft-graph-scopes)が必要な場合の回避策については、このドキュメントの最後にあるセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d4327-126">See our section at the end of this document for suggested workarounds if you require [additional Graph scopes](#apps-that-require-additional-microsoft-graph-scopes).</span></span>

<span data-ttu-id="d4327-127">SSO API は、web コンテンツを埋め込む [タスクモジュール](../../../task-modules-and-cards/what-are-task-modules.md) でも動作します。</span><span class="sxs-lookup"><span data-stu-id="d4327-127">The SSO API will also work in [Task Modules](../../../task-modules-and-cards/what-are-task-modules.md) that embed web content.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="d4327-128">SSO Microsoft Teams タブを開発する</span><span class="sxs-lookup"><span data-stu-id="d4327-128">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="d4327-129">このセクションでは、SSO を使用する Teams タブの作成に関連するタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d4327-129">This section describes the tasks involved in creating a Teams tab that uses SSO.</span></span> <span data-ttu-id="d4327-130">これらのタスクについては、言語とフレームワークに依存しません。</span><span class="sxs-lookup"><span data-stu-id="d4327-130">These tasks are described here are language- and framework-agnostic.</span></span>

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a><span data-ttu-id="d4327-131">1. Azure Active Directory (Azure AD) アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="d4327-131">1. Create your Azure Active Directory (Azure AD) application</span></span>

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a><span data-ttu-id="d4327-132">[AZURE AD ポータル](https://azure.microsoft.com/features/azure-portal/)でのアプリケーションの登録の概要:</span><span class="sxs-lookup"><span data-stu-id="d4327-132">Registering your application in the[Azure AD portal](https://azure.microsoft.com/features/azure-portal/) overview:</span></span>

1. <span data-ttu-id="d4327-133">[AZURE AD アプリケーション ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)を取得します。</span><span class="sxs-lookup"><span data-stu-id="d4327-133">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span>
2. <span data-ttu-id="d4327-134">Azure AD エンドポイントと、必要に応じて Microsoft Graph に対してアプリケーションに必要なアクセス許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="d4327-134">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="d4327-135">Teams デスクトップ、web、モバイルアプリケーションに[アクセス許可を付与](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)します。</span><span class="sxs-lookup"><span data-stu-id="d4327-135">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="d4327-136">事前承認する [ **スコープの追加** ] ボタンを選択し、表示されるパネルで、 `access_as_user` **範囲名** としてを入力します。</span><span class="sxs-lookup"><span data-stu-id="d4327-136">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

> [!NOTE]
> <span data-ttu-id="d4327-137">注意すべき重要な制限がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="d4327-137">There are some important restrictions you should be aware of:</span></span>
>
> * <span data-ttu-id="d4327-138">ユーザーレベルの Microsoft Graph API アクセス許可 (電子メール、プロファイル、offline_access、OpenId) のみがサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d4327-138">We only support user-level Microsoft Graph API permissions, i.e., email, profile, offline_access, OpenId.</span></span> <span data-ttu-id="d4327-139">他の Microsoft Graph スコープ (やなど) へのアクセスが必要な場合は `User.Read` `Mail.Read` 、このドキュメントの最後にある [推奨回避策](#apps-that-require-additional-microsoft-graph-scopes) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d4327-139">If you need access to other Microsoft Graph scopes (such as `User.Read` or `Mail.Read`), see our [recommended workaround](#apps-that-require-additional-microsoft-graph-scopes) at the end of this documentation.</span></span>
> * <span data-ttu-id="d4327-140">アプリケーションのドメイン名が Azure AD アプリケーションに登録したドメイン名と同じであることが重要です。</span><span class="sxs-lookup"><span data-stu-id="d4327-140">It's important that your application's domain name is the same as the domain name you've registering for your Azure AD application.</span></span>
> * <span data-ttu-id="d4327-141">現在、アプリごとに複数のドメインをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="d4327-141">We don't currently support multiple domains per app.</span></span>
> * <span data-ttu-id="d4327-142">`azurewebsites.net`ドメインは一般的すぎるため、セキュリティ上のリスクがある場合があるため、ドメインを使用するアプリケーションはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d4327-142">We don't support applications that use the `azurewebsites.net` domain because it is too common and may be a security risk.</span></span> <span data-ttu-id="d4327-143">しかし、この制限を排除することを積極的に目指しています。</span><span class="sxs-lookup"><span data-stu-id="d4327-143">However, we're actively seeking to remove this restriction.</span></span>

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a><span data-ttu-id="d4327-144">Azure Active Directory ポータルを使用してアプリを詳細に登録する:</span><span class="sxs-lookup"><span data-stu-id="d4327-144">Registering your app through the Azure Active Directory portal in-depth:</span></span>

1. <span data-ttu-id="d4327-145">新しいアプリケーションを [Azure Active Directory –アプリ登録](https://go.microsoft.com/fwlink/?linkid=2083908) ポータルに登録します。</span><span class="sxs-lookup"><span data-stu-id="d4327-145">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="d4327-146">[ **新規登録** ] を選択し、[ *アプリケーションの登録] ページ* で、次の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="d4327-146">Select **New Registration** and on the *register an application page*, set following values:</span></span>
    * <span data-ttu-id="d4327-147">**名前** をアプリ名に設定します。</span><span class="sxs-lookup"><span data-stu-id="d4327-147">Set **name** to your app name.</span></span>
    * <span data-ttu-id="d4327-148">**サポートされているアカウントの種類**(任意のアカウントの種類が機能する) を選択します。</span><span class="sxs-lookup"><span data-stu-id="d4327-148">Choose the **supported account types** (any account type will work) ¹</span></span>
    * <span data-ttu-id="d4327-149">**[リダイレクト URI]** を空のままにします。</span><span class="sxs-lookup"><span data-stu-id="d4327-149">Leave **Redirect URI** empty.</span></span>
    * <span data-ttu-id="d4327-150">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d4327-150">Choose **Register**.</span></span>
3. <span data-ttu-id="d4327-151">[概要] ページで、 **アプリケーション (クライアント) ID** をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="d4327-151">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="d4327-152">Teams アプリケーションマニフェストを更新するときには、後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="d4327-152">You’ll need it later when updating your Teams application manifest.</span></span>
4. <span data-ttu-id="d4327-153">[**管理**] で [**API の公開**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d4327-153">Under **Manage**, select **Expose an API**.</span></span> 
5. <span data-ttu-id="d4327-154">[ **設定** ] リンクを選択して、アプリケーション ID URI をの形式で生成し `api://{AppID}` ます。</span><span class="sxs-lookup"><span data-stu-id="d4327-154">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="d4327-155">二重スラッシュと GUID の間に、完全修飾ドメイン名 (末尾にスラッシュ "/" を付加したもの) を挿入します。</span><span class="sxs-lookup"><span data-stu-id="d4327-155">Insert your fully qualified domain name (with a forward slash "/" appended to the end) between the double forward slashes and the GUID.</span></span> <span data-ttu-id="d4327-156">ID 全体の形式は次のようにする必要があります: `api://fully-qualified-domain-name.com/{AppID}` ²</span><span class="sxs-lookup"><span data-stu-id="d4327-156">The entire ID should have the form of: `api://fully-qualified-domain-name.com/{AppID}` ²</span></span>
    * <span data-ttu-id="d4327-157">ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。</span><span class="sxs-lookup"><span data-stu-id="d4327-157">ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`.</span></span>
    
    <span data-ttu-id="d4327-158">完全修飾ドメイン名は、アプリが提供される人間が読むことができるドメイン名です。</span><span class="sxs-lookup"><span data-stu-id="d4327-158">The fully qualified domain name is the human readable domain name from which your app is served.</span></span> <span data-ttu-id="d4327-159">Ngrok などのトンネリングサービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-159">If you are using a tunneling service such as ngrok, you will need to update     this value whenever your ngrok subdomain changes.</span></span> 
6. <span data-ttu-id="d4327-160">**[Scope の追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="d4327-160">Select the **Add a scope** button.</span></span> <span data-ttu-id="d4327-161">開いたパネルで、**[スコープ名]** として `access_as_user` を入力します。</span><span class="sxs-lookup"><span data-stu-id="d4327-161">In the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>
7. <span data-ttu-id="d4327-162">**同意できるユーザー** を設定するには`Admins and users`</span><span class="sxs-lookup"><span data-stu-id="d4327-162">Set **Who can consent?** to `Admins and users`</span></span>
8. <span data-ttu-id="d4327-163">[管理者] と [ユーザーの同意] プロンプトを構成するためのフィールドに、範囲に適した値を入力し `access_as_user` ます。</span><span class="sxs-lookup"><span data-stu-id="d4327-163">Fill in the fields for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope:</span></span>
    * <span data-ttu-id="d4327-164">**管理者の同意のタイトル:** Teams は、ユーザーのプロファイルにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="d4327-164">**Admin consent title:** Teams can access the user’s profile.</span></span>
    * <span data-ttu-id="d4327-165">**管理者の同意の説明**: Teams は、現在のユーザーとしてアプリの web api を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="d4327-165">**Admin consent description**: Allows Teams to call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="d4327-166">**ユーザーの同意のタイトル**: Teams はユーザープロファイルにアクセスし、ユーザーに代わって要求を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d4327-166">**User consent title**: Teams can access the user profile and make requests on the user's behalf.</span></span>
    * <span data-ttu-id="d4327-167">**ユーザーの同意の説明:** Teams が、ユーザーと同じ権限でこのアプリの Api を呼び出せるようにします。</span><span class="sxs-lookup"><span data-stu-id="d4327-167">**User consent description:** Enable Teams to call this app’s APIs with the same rights as the user.</span></span>
9. <span data-ttu-id="d4327-168">**状態** が **有効** に設定されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="d4327-168">Ensure that **State** is set to **Enabled**</span></span>
10. <span data-ttu-id="d4327-169">[ **スコープの追加** ] ボタンを選択して保存します。</span><span class="sxs-lookup"><span data-stu-id="d4327-169">Select the **Add scope** button to save</span></span> 
    * <span data-ttu-id="d4327-170">テキストフィールドのすぐ下に表示される **スコープ名** のドメイン部分は、前の手順で設定した **アプリケーション ID** URI を `/access_as_user` 次の末尾に追加して自動的に一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-170">The domain part of the **Scope name** displayed just below the text field should automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end:</span></span>
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. <span data-ttu-id="d4327-171">[承認された **クライアントアプリケーション** ] セクションで、アプリの web アプリケーションに対して承認するアプリケーションを特定します。</span><span class="sxs-lookup"><span data-stu-id="d4327-171">In the **Authorized client applications** section, identify the applications that you want to authorize for your app’s web application.</span></span> <span data-ttu-id="d4327-172">[ *クライアントアプリケーションの追加*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d4327-172">Select *Add a client application*.</span></span> <span data-ttu-id="d4327-173">次の各クライアント Id を入力し、前の手順で作成した承認済みスコープを選択します。</span><span class="sxs-lookup"><span data-stu-id="d4327-173">Enter each of the following client IDs and select the authorized scope you created in the previous step:</span></span>
    * <span data-ttu-id="d4327-174">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams モバイル/デスクトップアプリケーション)</span><span class="sxs-lookup"><span data-stu-id="d4327-174">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams mobile/desktop application)</span></span>
    * <span data-ttu-id="d4327-175">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web アプリケーション)</span><span class="sxs-lookup"><span data-stu-id="d4327-175">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web application)</span></span>
12. <span data-ttu-id="d4327-176">[ **API アクセス許可** に移動します。</span><span class="sxs-lookup"><span data-stu-id="d4327-176">Navigate to **API Permissions**.</span></span> <span data-ttu-id="d4327-177">[*アクセス許可を追加する*  >  *microsoft graph* のデリゲートされた  >  *アクセス許可*] を選択し、次のアクセス許可を microsoft graph API から追加します。</span><span class="sxs-lookup"><span data-stu-id="d4327-177">Select *Add a permission* > *Microsoft Graph* > *Delegated permissions*, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="d4327-178">User. 読み取り (既定では有効)</span><span class="sxs-lookup"><span data-stu-id="d4327-178">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="d4327-179">メール</span><span class="sxs-lookup"><span data-stu-id="d4327-179">email</span></span>
    * <span data-ttu-id="d4327-180">offline_access</span><span class="sxs-lookup"><span data-stu-id="d4327-180">offline_access</span></span>
    * <span data-ttu-id="d4327-181">OpenId</span><span class="sxs-lookup"><span data-stu-id="d4327-181">OpenId</span></span>
    * <span data-ttu-id="d4327-182">profile</span><span class="sxs-lookup"><span data-stu-id="d4327-182">profile</span></span>

13. <span data-ttu-id="d4327-183">[**認証** に移動します。</span><span class="sxs-lookup"><span data-stu-id="d4327-183">Navigate to **Authentication**</span></span>

    <span data-ttu-id="d4327-184">アプリに管理者の同意が与えられていない場合、ユーザーはアプリを初めて使用するときに同意を得る必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-184">If an app hasn't been granted IT admin consent, users will have to provide consent the first time they use an app.</span></span>

    <span data-ttu-id="d4327-185">リダイレクト URI を設定します。</span><span class="sxs-lookup"><span data-stu-id="d4327-185">Set a redirect URI:</span></span>
    * <span data-ttu-id="d4327-186">[ **プラットフォームの追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d4327-186">Select **Add a platform**.</span></span>
    * <span data-ttu-id="d4327-187">[ **Web**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d4327-187">Select **web**.</span></span>
    * <span data-ttu-id="d4327-188">アプリの **リダイレクト URI** を入力します。</span><span class="sxs-lookup"><span data-stu-id="d4327-188">Enter the **redirect URI** for your app.</span></span> <span data-ttu-id="d4327-189">これは、暗黙的な付与フローが成功した場合にユーザーをリダイレクトするページになります。</span><span class="sxs-lookup"><span data-stu-id="d4327-189">This will be the page where a successful implicit grant flow will redirect the user.</span></span> <span data-ttu-id="d4327-190">これは、手順5で入力したのと同じ完全修飾ドメイン名となり、認証応答を送信する API ルートが続きます。</span><span class="sxs-lookup"><span data-stu-id="d4327-190">This will be same fully qualified domain name that you entered in step 5 followed by the API route where a authentication response should be sent.</span></span> <span data-ttu-id="d4327-191">Teams のサンプルのいずれかをフォローしている場合は、次のようになります。 `https://subdomain.example.com/auth-end`</span><span class="sxs-lookup"><span data-stu-id="d4327-191">If you are following any of the Teams samples, this will be: `https://subdomain.example.com/auth-end`</span></span>

    <span data-ttu-id="d4327-192">次に、以下のチェックボックスをオンにして暗黙的な付与を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d4327-192">Next, enable implicit grant by checking the following boxes:</span></span>  
    <span data-ttu-id="d4327-193">✔ ID トークン</span><span class="sxs-lookup"><span data-stu-id="d4327-193">✔ ID Token</span></span>  
    <span data-ttu-id="d4327-194">✔アクセストークン</span><span class="sxs-lookup"><span data-stu-id="d4327-194">✔ Access Token</span></span>  
    
<span data-ttu-id="d4327-195">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="d4327-195">Congratulations!</span></span> <span data-ttu-id="d4327-196">タブ SSO アプリを続行するには、アプリの登録の前提条件を完了している必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-196">You have completed the app registration prerequisites to proceed with your tab SSO app.</span></span>     

> [!NOTE]
>
> * <span data-ttu-id="d4327-197">\* Teams で認証要求を行うのと _同じ_ テナントに Azure AD アプリが登録されている場合は、ユーザーに同意を求められず、アクセストークンがすぐに付与されます。</span><span class="sxs-lookup"><span data-stu-id="d4327-197">¹ If your Azure AD app is registered in the _same_ tenant where you're making an authentication request in Teams, the user won't be asked to consent and will be granted an access token right away.</span></span> <span data-ttu-id="d4327-198">ユーザーは、Azure AD アプリが別のテナントに登録されている場合にのみ、これらのアクセス許可に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-198">Users only need to consent to these permissions if the Azure AD app is registered in a different tenant.</span></span>
> * <span data-ttu-id="d4327-199">²ドメインが既に所有されていて所有者であることを示すエラーが表示された場合は、「 [クイックスタート: カスタムドメイン名を Azure Active Directory に追加](/azure/active-directory/fundamentals/add-custom-domain) してドメインを登録する」の手順に従って、上記の手順5を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="d4327-199">² If you get an error stating that the domain is already owned and you are the owner, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) to register the domain, and then repeat step 5, above.</span></span> <span data-ttu-id="d4327-200">(このエラーは、Office 365 テナントの管理者の資格情報を使用してサインインしていない場合にも発生する可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="d4327-200">(This error can also occur if you aren't signed in with Admin credentials in the Office 365 tenancy).</span></span>
> * <span data-ttu-id="d4327-201">返されたアクセストークンで UPN (ユーザープリンシパル名) を受信していない場合は、Azure AD に [オプションの要求](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) として追加できます。</span><span class="sxs-lookup"><span data-stu-id="d4327-201">If you are not receiving the UPN (User Principal Name) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

### <a name="2-update-your-microsoft-teams-application-manifest"></a><span data-ttu-id="d4327-202">2. Microsoft Teams アプリケーションマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="d4327-202">2. Update your Microsoft Teams application manifest</span></span>

<span data-ttu-id="d4327-203">Microsoft Teams のマニフェストに新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="d4327-203">Add new properties to your Microsoft Teams manifest:</span></span>

* <span data-ttu-id="d4327-204">**Webapplicationinfo** -次の要素の親。</span><span class="sxs-lookup"><span data-stu-id="d4327-204">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d4327-205">**id** -アプリケーションのクライアント id。</span><span class="sxs-lookup"><span data-stu-id="d4327-205">**id** - The client ID of the application.</span></span> <span data-ttu-id="d4327-206">これは、アプリケーションを Azure AD に登録する際に取得したアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="d4327-206">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="d4327-207">**resource** -アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="d4327-207">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="d4327-208">これは、 `api://` 上記の手順6でを作成するときに登録したものと同じ URI (プロトコルを含む) です `scope` 。</span><span class="sxs-lookup"><span data-stu-id="d4327-208">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="d4327-209">リソースにパスを含めることはでき `access_as_user` ません。</span><span class="sxs-lookup"><span data-stu-id="d4327-209">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="d4327-210">この URI のドメイン部分は、Teams アプリケーションマニフェストの Url で使用されるすべてのサブドメインを含むドメインと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-210">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* <span data-ttu-id="d4327-211">AAD アプリのリソースは、通常、そのサイト URL と appID のルートになります (例: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` )。</span><span class="sxs-lookup"><span data-stu-id="d4327-211">The resource for an AAD app will usually be the root of its site URL and the appID (e.g. `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`).</span></span> <span data-ttu-id="d4327-212">また、この値を使用して、要求が同じドメインから送信されるようにします。</span><span class="sxs-lookup"><span data-stu-id="d4327-212">We also use this value to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="d4327-213">そのため、の `contentURL` タブのがリソースプロパティと同じドメインを使用していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="d4327-213">Therefore, make sure that the `contentURL` for your tab uses the same domains as your resource property.</span></span>
>* <span data-ttu-id="d4327-214">フィールドを実装するには、マニフェストバージョン1.5 以降を使用する必要があり `webApplicationInfo` ます。</span><span class="sxs-lookup"><span data-stu-id="d4327-214">You need to use manifest version 1.5 or higher to implement the `webApplicationInfo` field.</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="d4327-215">3. クライアント側のコードから認証トークンを取得する</span><span class="sxs-lookup"><span data-stu-id="d4327-215">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="d4327-216">認証 API は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d4327-216">Here's what the authentication API looks like:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="d4327-217">`getAuthToken`を呼び出して、ユーザーレベルの権限に対してユーザーの同意を追加する必要がある場合は、追加の同意を付与するためのダイアログがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d4327-217">When you call `getAuthToken` - and additional user consent is required (for user-level permissions) - we will show a dialog to the user encouraging them to grant additional consent.</span></span> 

<span data-ttu-id="d4327-218">成功のコールバックでアクセストークンを受信したら、アクセストークンをデコードして、そのトークンに関連付けられているクレームを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="d4327-218">Once you've received the access token in the success callback you can decode the access token to view the claims associated with that token.</span></span> <span data-ttu-id="d4327-219">(オプションで、アクセストークンを [JWT.io](https://jwt.io/) などのツールに手動でコピー/貼り付けて、そのコンテンツを検査することもできます)。</span><span class="sxs-lookup"><span data-stu-id="d4327-219">(Optionally, you can manually copy/paste the access token into a tool such as [JWT.io](https://jwt.io/) to inspect its contents).</span></span> <span data-ttu-id="d4327-220">返されたアクセストークンで UPN (ユーザープリンシパル名) を受信していない場合は、Azure AD に [オプションの要求](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) として追加できます。</span><span class="sxs-lookup"><span data-stu-id="d4327-220">If you are not receiving the UPN (User Principal Name) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a><span data-ttu-id="d4327-221">サンプル コード</span><span class="sxs-lookup"><span data-stu-id="d4327-221">Sample code</span></span>

<span data-ttu-id="d4327-222">サンプルアプリケーションを参照してください。 [Msteams TAB SSO サンプル-Nodejs](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)</span><span class="sxs-lookup"><span data-stu-id="d4327-222">Visit our sample application: [MSTeams Tabs SSO Sample - Nodejs](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)</span></span>

<span data-ttu-id="d4327-223">この README では、開発環境をセットアップする方法と、Azure AD でアプリケーションを構成する方法について説明しています。</span><span class="sxs-lookup"><span data-stu-id="d4327-223">The README explains how to set up your development environment and how to configure your application in Azure AD.</span></span> <span data-ttu-id="d4327-224">また、このサンプルが [「アプリ構造」セクション](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) でどのように構造化されているかについては、コードベースの理解に役立つ情報もあります。</span><span class="sxs-lookup"><span data-stu-id="d4327-224">You can also find further information on how the sample is structured in the [app structure section](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) to help familiarize yourself with the codebase.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="d4327-225">既知の制限</span><span class="sxs-lookup"><span data-stu-id="d4327-225">Known Limitations</span></span>

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a><span data-ttu-id="d4327-226">追加の Microsoft Graph スコープが必要なアプリ</span><span class="sxs-lookup"><span data-stu-id="d4327-226">Apps that require additional Microsoft Graph Scopes</span></span>

<span data-ttu-id="d4327-227">現在の SSO の実装では、ユーザーレベルのアクセス許可 (電子メール、プロファイル、offline_access、OpenId) に対してのみ同意が付与されます。他の Api (ユーザーによる読み取りまたはメールなど) に対しては使用できません。</span><span class="sxs-lookup"><span data-stu-id="d4327-227">Our current implementation for SSO only grants consent for user-level permissions — email, profile, offline_access, OpenId — not for other APIs (such as User.Read or Mail.Read).</span></span> <span data-ttu-id="d4327-228">アプリにさらに Microsoft Graph のスコープが必要な場合は、次のいくつかの回避策を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d4327-228">If your app needs further Microsoft Graph scopes, here are some enabling workarounds:</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="d4327-229">テナント管理者の同意</span><span class="sxs-lookup"><span data-stu-id="d4327-229">Tenant Admin Consent</span></span>

<span data-ttu-id="d4327-230">最も簡単な方法は、テナント管理者に組織の代わりに事前の同意を得ることです。</span><span class="sxs-lookup"><span data-stu-id="d4327-230">The simplest approach is to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="d4327-231">これは、ユーザーがこれらのスコープに同意する必要がなく、Azure AD の送信 [フロー](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)を使用してトークンサーバー側を自由に交換できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="d4327-231">This means users won’t have to consent to these scopes and you can then be free to exchange the token server side using Azure AD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="d4327-232">この回避策は内部の基幹業務アプリケーションには適していますが、テナント管理者の承認を利用できない可能性があるサードパーティの開発者には十分ではない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-232">This workaround is acceptable for internal line-of-business applications but may not be enough for third-party developers who may not be able to rely on tenant admin approval.</span></span>

<span data-ttu-id="d4327-233">組織の代わりに (テナント管理者として) 同意を簡単に参照するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="d4327-233">A simple way of consenting on behalf of an organization (as a tenant admin) is to visit:</span></span>

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="d4327-234">Auth API を使用して追加の同意を求める</span><span class="sxs-lookup"><span data-stu-id="d4327-234">Asking for additional consent using the Auth API</span></span>

<span data-ttu-id="d4327-235">追加の Microsoft Graph スコープを取得するためのもう1つの方法は、既存の [web ベースの AZURE ad 認証方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) を使用して、azure ad 同意ダイアログをポップアップするという同意ダイアログを表示することです。</span><span class="sxs-lookup"><span data-stu-id="d4327-235">Another approach for getting additional Microsoft Graph scopes is to present a consent dialog using our existing [web-based Azure AD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an Azure AD consent dialog.</span></span> <span data-ttu-id="d4327-236">注目すべき追加事項がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="d4327-236">There are some notable additions:</span></span>

1. <span data-ttu-id="d4327-237">を使用して取得したトークンは、その `getAuthToken()` 他の Microsoft Graph api にアクセスするために、AZURE AD [の代理送信フロー](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) を使用して、サーバー側を交換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-237">The token retrieved using `getAuthToken()` needs to be exchanged server-side using Azure AD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) to get access to those additional Microsoft Graph APIs.</span></span>
    * <span data-ttu-id="d4327-238">この exchange では、v2 Microsoft Graph エンドポイントを使用してください。</span><span class="sxs-lookup"><span data-stu-id="d4327-238">Be sure to use the v2 Microsoft Graph endpoint for this exchange</span></span>
2. <span data-ttu-id="d4327-239">Exchange に障害が発生した場合、Azure AD は無効な付与の例外を返します。</span><span class="sxs-lookup"><span data-stu-id="d4327-239">If the exchange fails, Azure AD will return an invalid grant exception.</span></span> <span data-ttu-id="d4327-240">通常、次の2つのエラーメッセージのいずれかがあります。 `invalid_grant``interaction_required`</span><span class="sxs-lookup"><span data-stu-id="d4327-240">There are usually one of two error messages: `invalid_grant` or `interaction_required`</span></span>
3. <span data-ttu-id="d4327-241">Exchange に障害が発生した場合は、追加の同意を求める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-241">When the exchange fails, then you need to ask for additional consent.</span></span> <span data-ttu-id="d4327-242">ユーザーに追加の同意を付与するように求める UI を表示することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d4327-242">We recommend showing some UI asking the user to grant additional consent.</span></span> <span data-ttu-id="d4327-243">この UI には、azure [ad 認証 API](~/concepts/authentication/auth-silent-aad.md)を使用して azure ad 同意ダイアログをトリガーするボタンが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-243">This UI should include a button that triggers an Azure AD consent dialog using our [Azure AD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="d4327-244">Azure ad から追加の同意を求める場合は、azure ad `prompt=consent` に [クエリ文字列-パラメーター](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) を含める必要があります。それ以外の場合、azure ad は追加のスコープを要求しません。</span><span class="sxs-lookup"><span data-stu-id="d4327-244">When asking for additional consent from Azure AD, you need to include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to Azure AD otherwise Azure AD will not ask for the additional scopes.</span></span>
    * <span data-ttu-id="d4327-245">代わりに： `?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="d4327-245">Instead of: `?scope={scopes}`</span></span>
    * <span data-ttu-id="d4327-246">使用するもの: `?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="d4327-246">Use this: `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="d4327-247">ユーザーに対して要求しているすべてのスコープが含まれていることを確認してください `{scopes}` (例: Mail. read または user. read)。</span><span class="sxs-lookup"><span data-stu-id="d4327-247">Be sure that `{scopes}` includes all the scopes you are prompting the user for (ex: Mail.Read or User.Read).</span></span>
5. <span data-ttu-id="d4327-248">ユーザーが追加のアクセス許可を付与した後、代理送信を再試行して、追加の Api へのアクセス権を取得します。</span><span class="sxs-lookup"><span data-stu-id="d4327-248">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-azure-ad-authentication"></a><span data-ttu-id="d4327-249">非 Azure AD 認証</span><span class="sxs-lookup"><span data-stu-id="d4327-249">Non-Azure AD Authentication</span></span>

<span data-ttu-id="d4327-250">前述の認証ソリューションは、id プロバイダーとして Azure AD をサポートするアプリとサービスに対してのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="d4327-250">The above-described authentication solution only works for apps and services that support Azure AD as an identity provider.</span></span> <span data-ttu-id="d4327-251">非 Azure AD ベースのサービスを使用して認証するアプリケーションは、ポップアップベースの [web 認証フロー](~/concepts/authentication.md)を引き続き使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d4327-251">Apps that want to authenticate using non-Azure AD based services need to continue using the pop-up-based [web authentication flow](~/concepts/authentication.md).</span></span>
