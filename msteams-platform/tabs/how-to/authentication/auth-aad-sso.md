---
title: タブのシングル サインオンのサポート
description: シングル サインオン (SSO) について説明します。
ms.topic: how-to
keywords: Teams 認証 SSO AAD シングル サインオン API
ms.openlocfilehash: 9392c3c01a7fa6dffc673cd01f57d0eab1720efe
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014125"
---
# <a name="single-sign-on-sso-support-for-tabs"></a><span data-ttu-id="dcd8a-104">タブのシングル サインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="dcd8a-104">Single sign-on (SSO) support for tabs</span></span>

<span data-ttu-id="dcd8a-105">ユーザーは、自分の仕事、学校、または Microsoft アカウント (Office 365、Outlook など) を介して Microsoft Teams にサインインします。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-105">Users sign in to Microsoft Teams via their work, school, or Microsoft accounts (Office 365, Outlook, etc).</span></span> <span data-ttu-id="dcd8a-106">これを利用するには、シングル サインオンを使用して、デスクトップまたはモバイル クライアントで Microsoft Teams タブ (またはタスク モジュール) を承認できます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-106">You can take advantage of this by allowing a single sign-on to authorize your Microsoft Teams tab (or task module) on desktop or mobile clients.</span></span> <span data-ttu-id="dcd8a-107">したがって、ユーザーがアプリの使用に同意した場合、別のデバイスでもう一度同意する必要はありません。ユーザーは自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-107">Thus, if a user consents to use your app, they won’t have to consent again on another device — they will be signed in automatically.</span></span> <span data-ttu-id="dcd8a-108">さらに、アクセス トークンをプリフェッチして、パフォーマンスと読み込み時間を向上させます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-108">In addition, we prefetch your access token to improve performance and load times.</span></span>

>[!NOTE]
> <span data-ttu-id="dcd8a-109">**SSO をサポートする Teams モバイル クライアントのバージョン**</span><span class="sxs-lookup"><span data-stu-id="dcd8a-109">**Teams mobile client versions supporting SSO**</span></span>  
>
> <span data-ttu-id="dcd8a-110">✔Teams for Android (1416/1.0.0.2020073101 以降)</span><span class="sxs-lookup"><span data-stu-id="dcd8a-110">✔Teams for Android (1416/1.0.0.2020073101 and later)</span></span>
>
> <span data-ttu-id="dcd8a-111">✔ iOS 用のチーム (_バージョン_: 2.0.18 以降)</span><span class="sxs-lookup"><span data-stu-id="dcd8a-111">✔Teams for iOS (_Version_: 2.0.18 and later)</span></span>  
>
> <span data-ttu-id="dcd8a-112">Teams で最高のエクスペリエンスを得る場合は、最新バージョンの iOS と Android を使用してください。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-112">For the best experience with Teams, please use the latest version of iOS and Android.</span></span>

>[!NOTE]
> <span data-ttu-id="dcd8a-113">**クイックスタート**</span><span class="sxs-lookup"><span data-stu-id="dcd8a-113">**Quickstart**</span></span>  
>
> <span data-ttu-id="dcd8a-114">タブ SSO の使用を開始する最も簡単な方法は、Microsoft Teams Toolkit for Visual Studio です。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-114">The simplest path to getting started with tab SSO is with the Microsoft Teams Toolkit for Visual Studio Code.</span></span> [<span data-ttu-id="dcd8a-115">詳細情報</span><span class="sxs-lookup"><span data-stu-id="dcd8a-115">Learn more</span></span>](../../../toolkit/visual-studio-code-tab-sso.md)


## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="dcd8a-116">実行時の SSO の動作のしくみ</span><span class="sxs-lookup"><span data-stu-id="dcd8a-116">How SSO works at runtime</span></span>

<span data-ttu-id="dcd8a-117">次の図は、SSO プロセスのしくみを示しています。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-117">The following diagram shows how the SSO process works:</span></span>

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="dcd8a-118">タブでは、JavaScript 呼び出しが実行されます `getAuthToken()` 。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-118">In the tab, a JavaScript call is made to `getAuthToken()`.</span></span> <span data-ttu-id="dcd8a-119">これにより、タブ アプリケーションの認証トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-119">This tells Teams to obtain an authentication token for the tab application.</span></span>
2. <span data-ttu-id="dcd8a-120">現在のユーザーが初めてタブ アプリケーションを使用する場合は、同意を求める要求プロンプト (同意が必要な場合) またはステップ アップ認証 (2 要素認証など) の処理を求めるプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-120">If this is the first time the current user has used your tab application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>
3. <span data-ttu-id="dcd8a-121">Teams は、現在のユーザーの Azure AD エンドポイントにタブ アプリケーション トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-121">Teams requests the tab application token from the Azure AD endpoint for the current user.</span></span>
4. <span data-ttu-id="dcd8a-122">Azure AD Teams アプリケーションにタブ アプリケーション トークンを送信します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-122">Azure AD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="dcd8a-123">Teams は、呼び出しによって返される結果オブジェクトの一部としてタブにタブ アプリケーション トークンを送信 `getAuthToken()` します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-123">Teams sends the tab application token to the tab as part of the result object returned by the `getAuthToken()` call.</span></span>
6. <span data-ttu-id="dcd8a-124">トークンは、JavaScript を使用してタブ アプリケーションで解析され、ユーザーの電子メール アドレスなどの必要な情報を抽出します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-124">The token will be parsed in the tab application, via JavaScript, to extract the needed information, such as the user's email address.</span></span>

> [!NOTE]
> <span data-ttu-id="dcd8a-125">The is only valid for consenting to a `getAuthToken()` limited set of user-level APIs — email, profile, offline_access and OpenId — and not for further Microsoft Graph scopes such as or `User.Read` `Mail.Read` .</span><span class="sxs-lookup"><span data-stu-id="dcd8a-125">The `getAuthToken()` is only valid for consenting to a limited set of user-level APIs — email, profile, offline_access and OpenId — and not for further Microsoft Graph scopes such as `User.Read` or `Mail.Read`.</span></span> <span data-ttu-id="dcd8a-126">追加の Graph スコープが必要な場合に推奨される回避策については、このドキュメントの最後にあるセクション [を参照してください](#apps-that-require-additional-microsoft-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-126">See our section at the end of this document for suggested workarounds if you require [additional Graph scopes](#apps-that-require-additional-microsoft-graph-scopes).</span></span>

<span data-ttu-id="dcd8a-127">SSO API は、Web コンテンツを埋 [め込むタスク モジュール](../../../task-modules-and-cards/what-are-task-modules.md) でも機能します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-127">The SSO API will also work in [Task Modules](../../../task-modules-and-cards/what-are-task-modules.md) that embed web content.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="dcd8a-128">SSO Microsoft Teams タブを開発する</span><span class="sxs-lookup"><span data-stu-id="dcd8a-128">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="dcd8a-129">このセクションでは、SSO を使用する Teams タブの作成に関連するタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-129">This section describes the tasks involved in creating a Teams tab that uses SSO.</span></span> <span data-ttu-id="dcd8a-130">ここでは、これらのタスクについて、言語とフレームワークに依存しないタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-130">These tasks are described here are language- and framework-agnostic.</span></span>

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a><span data-ttu-id="dcd8a-131">1. Azure Active Directory (Azure AD) アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="dcd8a-131">1. Create your Azure Active Directory (Azure AD) application</span></span>

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a><span data-ttu-id="dcd8a-132">Azure AD[ポータルでのアプリケーションの登録の](https://azure.microsoft.com/features/azure-portal/) 概要:</span><span class="sxs-lookup"><span data-stu-id="dcd8a-132">Registering your application in the[Azure AD portal](https://azure.microsoft.com/features/azure-portal/) overview:</span></span>

1. <span data-ttu-id="dcd8a-133">Azure AD [アプリケーション ID を取得します](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-133">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span>
2. <span data-ttu-id="dcd8a-134">アプリケーションが Azure AD エンドポイントと、必要に応じて Microsoft Graph に必要なアクセス許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-134">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="dcd8a-135">Teams[のデスクトップ、Web、](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)モバイル アプリケーションのアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-135">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="dcd8a-136">[範囲の追加] ボタンを選択して Teams を事前承認し、開くパネルで、スコープ `access_as_user` 名として **入力します**。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-136">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

> [!NOTE]
> <span data-ttu-id="dcd8a-137">次の重要な制限に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-137">There are some important restrictions you should be aware of:</span></span>
>
> * <span data-ttu-id="dcd8a-138">ユーザー レベルの Microsoft Graph API のアクセス許可 (メール、プロファイル、offline_access、OpenId など) のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-138">We only support user-level Microsoft Graph API permissions, i.e., email, profile, offline_access, OpenId.</span></span> <span data-ttu-id="dcd8a-139">他の Microsoft Graph スコープ (またはなど) にアクセスする必要がある場合は、このドキュメントの最後にある推奨 `User.Read` `Mail.Read` される回避策を参照してください。 [](#apps-that-require-additional-microsoft-graph-scopes)</span><span class="sxs-lookup"><span data-stu-id="dcd8a-139">If you need access to other Microsoft Graph scopes (such as `User.Read` or `Mail.Read`), see our [recommended workaround](#apps-that-require-additional-microsoft-graph-scopes) at the end of this documentation.</span></span>
> * <span data-ttu-id="dcd8a-140">アプリケーションのドメイン名は、Azure AD アプリケーションに登録したドメイン名と同じ名前にすることが重要です。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-140">It's important that your application's domain name is the same as the domain name you've registering for your Azure AD application.</span></span>
> * <span data-ttu-id="dcd8a-141">現在、アプリごとに複数のドメインはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-141">We don't currently support multiple domains per app.</span></span>
> * <span data-ttu-id="dcd8a-142">ドメインが一般的すぎるため、セキュリティ 上のリスクが考えられますが、ドメインを使用するアプリケーション `azurewebsites.net` はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-142">We don't support applications that use the `azurewebsites.net` domain because it is too common and may be a security risk.</span></span> <span data-ttu-id="dcd8a-143">ただし、この制限を積極的に削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-143">However, we're actively seeking to remove this restriction.</span></span>

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a><span data-ttu-id="dcd8a-144">Azure Active Directory ポータルを使用してアプリを登録する詳細:</span><span class="sxs-lookup"><span data-stu-id="dcd8a-144">Registering your app through the Azure Active Directory portal in-depth:</span></span>

1. <span data-ttu-id="dcd8a-145">Azure Active Directory アプリ登録ポータルに [新しいアプリケーションを登録](https://go.microsoft.com/fwlink/?linkid=2083908) します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-145">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="dcd8a-146">[ **新しい登録] を** 選択し、[アプリケーションの *登録] ページで* 次の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-146">Select **New Registration** and on the *register an application page*, set following values:</span></span>
    * <span data-ttu-id="dcd8a-147">アプリ **名に** 名前を設定します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-147">Set **name** to your app name.</span></span>
    * <span data-ttu-id="dcd8a-148">サポートされている **アカウントの種類を選択** する (任意のアカウントの種類が機能します) ¹</span><span class="sxs-lookup"><span data-stu-id="dcd8a-148">Choose the **supported account types** (any account type will work) ¹</span></span>
    * <span data-ttu-id="dcd8a-149">**[リダイレクト URI]** を空のままにします。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-149">Leave **Redirect URI** empty.</span></span>
    * <span data-ttu-id="dcd8a-150">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-150">Choose **Register**.</span></span>
3. <span data-ttu-id="dcd8a-151">[概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-151">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="dcd8a-152">後で Teams アプリケーション マニフェストを更新するときに必要になります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-152">You’ll need it later when updating your Teams application manifest.</span></span>
4. <span data-ttu-id="dcd8a-153">[**管理**] で [**API の公開**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-153">Under **Manage**, select **Expose an API**.</span></span> 
5. <span data-ttu-id="dcd8a-154">**[Set]** リンクを選択して、アプリケーション ID URI を次の形式で生成します `api://{AppID}` 。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-154">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="dcd8a-155">二重スラッシュと GUID の間に完全修飾ドメイン名 (末尾にスラッシュ "/" が付加された名前) を挿入します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-155">Insert your fully qualified domain name (with a forward slash "/" appended to the end) between the double forward slashes and the GUID.</span></span> <span data-ttu-id="dcd8a-156">ID 全体は次の形式である `api://fully-qualified-domain-name.com/{AppID}` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-156">The entire ID should have the form of: `api://fully-qualified-domain-name.com/{AppID}` ²</span></span>
    * <span data-ttu-id="dcd8a-157">例: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .</span><span class="sxs-lookup"><span data-stu-id="dcd8a-157">ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`.</span></span>
    
    <span data-ttu-id="dcd8a-158">完全修飾ドメイン名は、アプリが提供される人間が読み取り可能なドメイン名です。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-158">The fully qualified domain name is the human readable domain name from which your app is served.</span></span> <span data-ttu-id="dcd8a-159">ngrok などのトンネリング サービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-159">If you are using a tunneling service such as ngrok, you will need to update     this value whenever your ngrok subdomain changes.</span></span> 
6. <span data-ttu-id="dcd8a-160">**[Scope の追加]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-160">Select the **Add a scope** button.</span></span> <span data-ttu-id="dcd8a-161">開いたパネルで、**[スコープ名]** として `access_as_user` を入力します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-161">In the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>
7. <span data-ttu-id="dcd8a-162">同意 **できるユーザーを設定** する `Admins and users`</span><span class="sxs-lookup"><span data-stu-id="dcd8a-162">Set **Who can consent?** to `Admins and users`</span></span>
8. <span data-ttu-id="dcd8a-163">管理者とユーザーの同意のプロンプトを構成するためのフィールドに、範囲に適した値を入力 `access_as_user` します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-163">Fill in the fields for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope:</span></span>
    * <span data-ttu-id="dcd8a-164">**管理者の同意のタイトル:** Teams はユーザーのプロファイルにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-164">**Admin consent title:** Teams can access the user’s profile.</span></span>
    * <span data-ttu-id="dcd8a-165">**管理者の同意の説明**: Teams がアプリの Web API を現在のユーザーとして呼び出すのを許可します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-165">**Admin consent description**: Allows Teams to call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="dcd8a-166">**ユーザーの同意のタイトル**: Teams はユーザー プロファイルにアクセスし、ユーザーに代わって要求を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-166">**User consent title**: Teams can access the user profile and make requests on the user's behalf.</span></span>
    * <span data-ttu-id="dcd8a-167">**ユーザーの同意の説明:** Teams がユーザーと同じ権限でこのアプリの API を呼び出すのを有効にする。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-167">**User consent description:** Enable Teams to call this app’s APIs with the same rights as the user.</span></span>
9. <span data-ttu-id="dcd8a-168">状態が **[有効]** に **設定されている**</span><span class="sxs-lookup"><span data-stu-id="dcd8a-168">Ensure that **State** is set to **Enabled**</span></span>
10. <span data-ttu-id="dcd8a-169">[範囲の **追加] ボタンを** 選択して保存する</span><span class="sxs-lookup"><span data-stu-id="dcd8a-169">Select the **Add scope** button to save</span></span> 
    * <span data-ttu-id="dcd8a-170">テキスト フィールドの下に **表示されるスコープ** 名のドメイン部分は、前の手順で設定したアプリケーション **ID** URI と自動的に一致し、末尾に追加 `/access_as_user` されます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-170">The domain part of the **Scope name** displayed just below the text field should automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end:</span></span>
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. <span data-ttu-id="dcd8a-171">[ **承認済みクライアント アプリケーション** ] セクションで、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-171">In the **Authorized client applications** section, identify the applications that you want to authorize for your app’s web application.</span></span> <span data-ttu-id="dcd8a-172">[クライアント *アプリケーションの追加] を選択します*。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-172">Select *Add a client application*.</span></span> <span data-ttu-id="dcd8a-173">次の各クライアント ID を入力し、前の手順で作成した承認済みスコープを選択します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-173">Enter each of the following client IDs and select the authorized scope you created in the previous step:</span></span>
    * <span data-ttu-id="dcd8a-174">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams モバイル/デスクトップ アプリケーション)</span><span class="sxs-lookup"><span data-stu-id="dcd8a-174">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams mobile/desktop application)</span></span>
    * <span data-ttu-id="dcd8a-175">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams Web アプリケーション)</span><span class="sxs-lookup"><span data-stu-id="dcd8a-175">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web application)</span></span>
12. <span data-ttu-id="dcd8a-176">API の **アクセス許可に移動します**。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-176">Navigate to **API Permissions**.</span></span> <span data-ttu-id="dcd8a-177">[Microsoft Graph *委任されたアクセス* 許可のアクセス許可の追加] を選択し、Microsoft Graph API から次のアクセス  >    >  許可を追加します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-177">Select *Add a permission* > *Microsoft Graph* > *Delegated permissions*, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="dcd8a-178">User.Read (既定で有効)</span><span class="sxs-lookup"><span data-stu-id="dcd8a-178">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="dcd8a-179">メール</span><span class="sxs-lookup"><span data-stu-id="dcd8a-179">email</span></span>
    * <span data-ttu-id="dcd8a-180">offline_access</span><span class="sxs-lookup"><span data-stu-id="dcd8a-180">offline_access</span></span>
    * <span data-ttu-id="dcd8a-181">OpenId</span><span class="sxs-lookup"><span data-stu-id="dcd8a-181">OpenId</span></span>
    * <span data-ttu-id="dcd8a-182">profile</span><span class="sxs-lookup"><span data-stu-id="dcd8a-182">profile</span></span>

13. <span data-ttu-id="dcd8a-183">[認証] に **移動する**</span><span class="sxs-lookup"><span data-stu-id="dcd8a-183">Navigate to **Authentication**</span></span>

    <span data-ttu-id="dcd8a-184">アプリに IT 管理者の同意が与えされていない場合、ユーザーは初めてアプリを使用する場合に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-184">If an app hasn't been granted IT admin consent, users will have to provide consent the first time they use an app.</span></span>

    <span data-ttu-id="dcd8a-185">リダイレクト URI を設定します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-185">Set a redirect URI:</span></span>
    * <span data-ttu-id="dcd8a-186">[プラットフォーム **の追加] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-186">Select **Add a platform**.</span></span>
    * <span data-ttu-id="dcd8a-187">Web を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-187">Select **web**.</span></span>
    * <span data-ttu-id="dcd8a-188">アプリの **リダイレクト URI** を入力します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-188">Enter the **redirect URI** for your app.</span></span> <span data-ttu-id="dcd8a-189">これは、暗黙的な許可フローが成功するとユーザーがリダイレクトされるページです。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-189">This will be the page where a successful implicit grant flow will redirect the user.</span></span> <span data-ttu-id="dcd8a-190">これは、手順 5 で入力した完全修飾ドメイン名と、認証応答を送信する API ルートと同じ名前です。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-190">This will be same fully qualified domain name that you entered in step 5 followed by the API route where a authentication response should be sent.</span></span> <span data-ttu-id="dcd8a-191">Teams のサンプルを実行している場合は、次のようになります。 `https://subdomain.example.com/auth-end`</span><span class="sxs-lookup"><span data-stu-id="dcd8a-191">If you are following any of the Teams samples, this will be: `https://subdomain.example.com/auth-end`</span></span>

    <span data-ttu-id="dcd8a-192">次に、次のボックスをオンにして暗黙的な許可を有効にします。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-192">Next, enable implicit grant by checking the following boxes:</span></span>  
    <span data-ttu-id="dcd8a-193">✔ ID トークン</span><span class="sxs-lookup"><span data-stu-id="dcd8a-193">✔ ID Token</span></span>  
    <span data-ttu-id="dcd8a-194">✔ アクセス トークン</span><span class="sxs-lookup"><span data-stu-id="dcd8a-194">✔ Access Token</span></span>  
    
<span data-ttu-id="dcd8a-195">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="dcd8a-195">Congratulations!</span></span> <span data-ttu-id="dcd8a-196">タブ SSO アプリを続行するには、アプリ登録の前提条件が完了しています。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-196">You have completed the app registration prerequisites to proceed with your tab SSO app.</span></span>     

> [!NOTE]
>
> * <span data-ttu-id="dcd8a-197">¹ Azure AD アプリが Teams で認証要求を行っているのと同じテナントに登録されている場合、ユーザーは同意を求められなく、アクセス トークンがすぐ付与されます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-197">¹ If your Azure AD app is registered in the _same_ tenant where you're making an authentication request in Teams, the user won't be asked to consent and will be granted an access token right away.</span></span> <span data-ttu-id="dcd8a-198">ユーザーがこれらのアクセス許可に同意する必要があるのは、Azure AD アプリが別のテナントに登録されている場合のみです。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-198">Users only need to consent to these permissions if the Azure AD app is registered in a different tenant.</span></span>
> * <span data-ttu-id="dcd8a-199">ドメインが既に所有され、自分が所有者であることを示すエラーが表示された場合は、「クイック スタート [: Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) にカスタム ドメイン名を追加してドメインを登録し、上記の手順 5. を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-199">² If you get an error stating that the domain is already owned and you are the owner, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) to register the domain, and then repeat step 5, above.</span></span> <span data-ttu-id="dcd8a-200">(このエラーは、Office 365 テナントで管理者の資格情報でサインインしていない場合にも発生します)。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-200">(This error can also occur if you aren't signed in with Admin credentials in the Office 365 tenancy).</span></span>
> * <span data-ttu-id="dcd8a-201">返されたアクセス トークンで UPN (ユーザー プリンシパル名) を受信していない場合は、Azure AD[](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)でオプションのクレームとして追加できます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-201">If you are not receiving the UPN (User Principal Name) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

### <a name="2-update-your-microsoft-teams-application-manifest"></a><span data-ttu-id="dcd8a-202">2. Microsoft Teams アプリケーション マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="dcd8a-202">2. Update your Microsoft Teams application manifest</span></span>

<span data-ttu-id="dcd8a-203">Microsoft Teams マニフェストに新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-203">Add new properties to your Microsoft Teams manifest:</span></span>

* <span data-ttu-id="dcd8a-204">**WebApplicationInfo** - 次の要素の親。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-204">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dcd8a-205">**id** - アプリケーションのクライアント ID。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-205">**id** - The client ID of the application.</span></span> <span data-ttu-id="dcd8a-206">これは、Azure AD にアプリケーションを登録する一環として取得したアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-206">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="dcd8a-207">**resource** - アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-207">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="dcd8a-208">これは、上記の手順 6 で作成するときに登録した URI (プロトコルを含む `api://` ) `scope` と同じです。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-208">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="dcd8a-209">リソースにパスを `access_as_user` 含めてはならない。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-209">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="dcd8a-210">この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用される任意のサブドメインを含むドメインと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-210">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* <span data-ttu-id="dcd8a-211">AAD アプリのリソースは、通常、サイト URL のルートと appID (例: ) です `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-211">The resource for an AAD app will usually be the root of its site URL and the appID (e.g. `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`).</span></span> <span data-ttu-id="dcd8a-212">また、この値を使用して、要求が同じドメインから送信されるのを確認します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-212">We also use this value to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="dcd8a-213">したがって、タブのドメインがリソース `contentURL` プロパティと同じドメインを使用している必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-213">Therefore, make sure that the `contentURL` for your tab uses the same domains as your resource property.</span></span>
>* <span data-ttu-id="dcd8a-214">フィールドを実装するには、マニフェスト バージョン 1.5 以上を使用する必要 `webApplicationInfo` があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-214">You need to use manifest version 1.5 or higher to implement the `webApplicationInfo` field.</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="dcd8a-215">3. クライアント側コードから認証トークンを取得する</span><span class="sxs-lookup"><span data-stu-id="dcd8a-215">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="dcd8a-216">認証 API は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-216">Here's what the authentication API looks like:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="dcd8a-217">(ユーザー レベルのアクセス許可に対して) 呼び出しを行い、追加のユーザーの同意が必要な場合は、追加の同意を与えるダイアログがユーザーに `getAuthToken` 表示されます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-217">When you call `getAuthToken` - and additional user consent is required (for user-level permissions) - we will show a dialog to the user encouraging them to grant additional consent.</span></span> 

<span data-ttu-id="dcd8a-218">成功コールバックでアクセス トークンを受信したら、アクセス トークンをデコードして、そのトークンに関連付けられているクレームを表示できます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-218">Once you've received the access token in the success callback you can decode the access token to view the claims associated with that token.</span></span> <span data-ttu-id="dcd8a-219">(必要に応じて、アクセス トークンを手動でコピー/貼り付け[](https://jwt.io/)(コンテンツを調JWT.ioなど) できます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-219">(Optionally, you can manually copy/paste the access token into a tool such as [JWT.io](https://jwt.io/) to inspect its contents).</span></span> <span data-ttu-id="dcd8a-220">返されたアクセス トークンで UPN (ユーザー プリンシパル名) を受信していない場合は、Azure AD[](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)でオプションのクレームとして追加できます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-220">If you are not receiving the UPN (User Principal Name) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a><span data-ttu-id="dcd8a-221">サンプル コード</span><span class="sxs-lookup"><span data-stu-id="dcd8a-221">Sample code</span></span>

<span data-ttu-id="dcd8a-222">サンプル アプリケーションにアクセスする: [MSTeams PnP SSO サンプル](https://github.com/pnp/teams-dev-samples/tree/master/samples/tab-sso)</span><span class="sxs-lookup"><span data-stu-id="dcd8a-222">Visit our sample application: [MSTeams PnP SSO Sample](https://github.com/pnp/teams-dev-samples/tree/master/samples/tab-sso)</span></span>

<span data-ttu-id="dcd8a-223">README では、開発環境をセットアップする方法と、Azure AD でアプリケーションを構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-223">The README explains how to set up your development environment and how to configure your application in Azure AD.</span></span> <span data-ttu-id="dcd8a-224">また、コードベースを理解するのに役立つ、アプリの構造に関[](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure)するセクションで、サンプルがどのように構成されているのかについて詳しい情報も確認できます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-224">You can also find further information on how the sample is structured in the [app structure section](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) to help familiarize yourself with the codebase.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="dcd8a-225">既知の制限</span><span class="sxs-lookup"><span data-stu-id="dcd8a-225">Known Limitations</span></span>

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a><span data-ttu-id="dcd8a-226">追加の Microsoft Graph スコープが必要なアプリ</span><span class="sxs-lookup"><span data-stu-id="dcd8a-226">Apps that require additional Microsoft Graph Scopes</span></span>

<span data-ttu-id="dcd8a-227">SSO の現在の実装では、他の API (User.Read や Mail.Read など) ではなく、ユーザー レベルのアクセス許可 (電子メール、プロファイル、offline_access、OpenId) に対する同意のみを付与しています。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-227">Our current implementation for SSO only grants consent for user-level permissions — email, profile, offline_access, OpenId — not for other APIs (such as User.Read or Mail.Read).</span></span> <span data-ttu-id="dcd8a-228">アプリにさらに Microsoft Graph スコープが必要な場合は、いくつかの有効な回避策を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-228">If your app needs further Microsoft Graph scopes, here are some enabling workarounds:</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="dcd8a-229">テナント管理者の同意</span><span class="sxs-lookup"><span data-stu-id="dcd8a-229">Tenant Admin Consent</span></span>

<span data-ttu-id="dcd8a-230">最も簡単な方法は、テナント管理者に組織の代わりに事前同意を得る方法です。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-230">The simplest approach is to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="dcd8a-231">つまり、ユーザーはこれらのスコープに同意する必要がならないので、Azure AD の代理フローを使用してトークン サーバー側を自由に交換 [できます](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-231">This means users won’t have to consent to these scopes and you can then be free to exchange the token server side using Azure AD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="dcd8a-232">この回避策は、内部の業務アプリケーションでは許容されますが、テナント管理者の承認に依存できないサードパーティの開発者には十分ではない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-232">This workaround is acceptable for internal line-of-business applications but may not be enough for third-party developers who may not be able to rely on tenant admin approval.</span></span>

<span data-ttu-id="dcd8a-233">(テナント管理者として) 組織の代わりに同意する簡単な方法は、次にアクセスする方法です。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-233">A simple way of consenting on behalf of an organization (as a tenant admin) is to visit:</span></span>

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="dcd8a-234">Auth API を使用して追加の同意を求める</span><span class="sxs-lookup"><span data-stu-id="dcd8a-234">Asking for additional consent using the Auth API</span></span>

<span data-ttu-id="dcd8a-235">追加の Microsoft Graph スコープを取得するためのもう 1 つのアプローチは、既存の Web ベースの [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) 認証アプローチを使用して同意ダイアログを表示する方法です。この認証方法では、Azure AD 同意ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-235">Another approach for getting additional Microsoft Graph scopes is to present a consent dialog using our existing [web-based Azure AD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an Azure AD consent dialog.</span></span> <span data-ttu-id="dcd8a-236">いくつかの追加機能があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-236">There are some notable additions:</span></span>

1. <span data-ttu-id="dcd8a-237">取得するトークンは、追加の Microsoft Graph API にアクセスするために `getAuthToken()` 、Azure AD [on-behalf-of](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) フローを使用してサーバー側で交換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-237">The token retrieved using `getAuthToken()` needs to be exchanged server-side using Azure AD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) to get access to those additional Microsoft Graph APIs.</span></span>
    * <span data-ttu-id="dcd8a-238">この交換には必ず v2 Microsoft Graph エンドポイントを使用してください。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-238">Be sure to use the v2 Microsoft Graph endpoint for this exchange</span></span>
2. <span data-ttu-id="dcd8a-239">交換が失敗した場合、Azure AD無効な付与例外が返されます。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-239">If the exchange fails, Azure AD will return an invalid grant exception.</span></span> <span data-ttu-id="dcd8a-240">通常、次の 2 つのエラー メッセージの 1 `invalid_grant` つがあります。 `interaction_required`</span><span class="sxs-lookup"><span data-stu-id="dcd8a-240">There are usually one of two error messages: `invalid_grant` or `interaction_required`</span></span>
3. <span data-ttu-id="dcd8a-241">交換が失敗した場合は、追加の同意を求める必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-241">When the exchange fails, then you need to ask for additional consent.</span></span> <span data-ttu-id="dcd8a-242">ユーザーに追加の同意を求める UI を表示することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-242">We recommend showing some UI asking the user to grant additional consent.</span></span> <span data-ttu-id="dcd8a-243">この UI には、Azure 認証 API を使用して Azure AD同意ダイアログ [をトリガーするAD含める必要があります](~/concepts/authentication/auth-silent-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-243">This UI should include a button that triggers an Azure AD consent dialog using our [Azure AD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="dcd8a-244">Azure AD から追加の同意を求める場合は、Azure AD へのクエリ文字列パラメーターに含める必要があります。それ以外の場合 `prompt=consent` 、Azure AD[](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)は追加のスコープを求めしません。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-244">When asking for additional consent from Azure AD, you need to include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to Azure AD otherwise Azure AD will not ask for the additional scopes.</span></span>
    * <span data-ttu-id="dcd8a-245">代わりに： `?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="dcd8a-245">Instead of: `?scope={scopes}`</span></span>
    * <span data-ttu-id="dcd8a-246">次のコマンドを使用します。 `?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="dcd8a-246">Use this: `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="dcd8a-247">ユーザーに確認を求めるすべてのスコープ `{scopes}` (Mail.Read、User.Read など) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-247">Be sure that `{scopes}` includes all the scopes you are prompting the user for (ex: Mail.Read or User.Read).</span></span>
5. <span data-ttu-id="dcd8a-248">ユーザーが追加のアクセス許可を付与したら、代理フローを再試行して、これらの追加の API にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-248">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-azure-ad-authentication"></a><span data-ttu-id="dcd8a-249">Azure 以外のAD認証</span><span class="sxs-lookup"><span data-stu-id="dcd8a-249">Non-Azure AD Authentication</span></span>

<span data-ttu-id="dcd8a-250">上記の認証ソリューションは、Azure 認証をサポートするアプリとサービスADプロバイダーとしてのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-250">The above-described authentication solution only works for apps and services that support Azure AD as an identity provider.</span></span> <span data-ttu-id="dcd8a-251">Azure ベース以外のサービスを使用してADするアプリは、ポップアップ ベースの Web 認証フローを引き続き [使用する必要があります](~/concepts/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="dcd8a-251">Apps that want to authenticate using non-Azure AD based services need to continue using the pop-up-based [web authentication flow](~/concepts/authentication.md).</span></span>
