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
# <a name="single-sign-on-sso-support-for-tabs"></a><span data-ttu-id="a8256-104">タブのシングル サインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="a8256-104">Single sign-on (SSO) support for tabs</span></span>

<span data-ttu-id="a8256-105">ユーザーは、Microsoft Teams、学校、または Microsoft アカウントを通じて、Office 365、Outlookサインインします。</span><span class="sxs-lookup"><span data-stu-id="a8256-105">Users sign in to Microsoft Teams through their work, school, or Microsoft accounts that is Office 365, Outlook, and so on.</span></span> <span data-ttu-id="a8256-106">この利点を利用するには、シングル サインオンでデスクトップまたはモバイル クライアントの [Teams] タブまたはタスク モジュールを承認できます。</span><span class="sxs-lookup"><span data-stu-id="a8256-106">You can take advantage of this by allowing a single sign-on to authorize your Teams tab or task module on desktop or mobile clients.</span></span> <span data-ttu-id="a8256-107">ユーザーがアプリの使用に同意した場合、自動的にサインインする別のデバイスで再度同意する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a8256-107">If a user consents to use your app, they do not have to consent again on another device as they are signed in automatically.</span></span> <span data-ttu-id="a8256-108">さらに、アクセス トークンは、パフォーマンスと読み込み時間を向上させるためにプリフェッチされます。</span><span class="sxs-lookup"><span data-stu-id="a8256-108">In addition, your access token is prefetched to improve performance and load times.</span></span>

> [!NOTE]
> <span data-ttu-id="a8256-109">**Teams SSO をサポートするモバイル クライアント バージョン**</span><span class="sxs-lookup"><span data-stu-id="a8256-109">**Teams mobile client versions supporting SSO**</span></span>  
>
> <span data-ttu-id="a8256-110">✔Teams (1416/1.0.0.2020073101 以降)</span><span class="sxs-lookup"><span data-stu-id="a8256-110">✔Teams for Android (1416/1.0.0.2020073101 and later)</span></span>
>
> <span data-ttu-id="a8256-111">✔Teams iOS のバージョン (_バージョン_: 2.0.18 以降)</span><span class="sxs-lookup"><span data-stu-id="a8256-111">✔Teams for iOS (_Version_: 2.0.18 and later)</span></span>  
>
> <span data-ttu-id="a8256-112">最新のバージョンの iOS Teams Android を使用して、アプリのエクスペリエンスを向上します。</span><span class="sxs-lookup"><span data-stu-id="a8256-112">For the best experience with Teams, use the latest version of iOS and Android.</span></span>

> [!NOTE]
> <span data-ttu-id="a8256-113">**クイックスタート**</span><span class="sxs-lookup"><span data-stu-id="a8256-113">**Quickstart**</span></span>  
>
> <span data-ttu-id="a8256-114">タブ SSO を使い始める最も簡単なパスは、TeamsツールキットVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="a8256-114">The simplest path to getting started with tab SSO is with the Teams toolkit for Visual Studio Code.</span></span> <span data-ttu-id="a8256-115">詳細については、「SSO with [Teamsツールキット」および「Visual Studio Code」を参照してください。](../../../toolkit/visual-studio-code-tab-sso.md)</span><span class="sxs-lookup"><span data-stu-id="a8256-115">For more information, see [SSO with Teams toolkit and Visual Studio Code for tabs](../../../toolkit/visual-studio-code-tab-sso.md)</span></span>

## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="a8256-116">実行時の SSO の動作のしくみ</span><span class="sxs-lookup"><span data-stu-id="a8256-116">How SSO works at runtime</span></span>

<span data-ttu-id="a8256-117">次の図は、SSO プロセスの動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="a8256-117">The following image shows how the SSO process works:</span></span>

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="a8256-118">タブでは、JavaScript 呼び出しが `getAuthToken()`に対してなされます。</span><span class="sxs-lookup"><span data-stu-id="a8256-118">In the tab, a JavaScript call is made to `getAuthToken()`.</span></span> <span data-ttu-id="a8256-119">これにより、Teamsアプリケーションの認証トークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-119">This tells Teams to obtain an authentication token for the tab application.</span></span>
2. <span data-ttu-id="a8256-120">現在のユーザーが初めてタブ アプリケーションを使用する場合は、同意が必要な場合は同意を求める要求プロンプトや、2 要素認証などのステップアップ認証を処理する要求プロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a8256-120">If this is the first time the current user has used your tab application, there is a request prompt to consent if consent is required or to handle step-up authentication such as two-factor authentication.</span></span>
3. <span data-ttu-id="a8256-121">Teamsユーザーに対して、Azure Active Directory (AAD) エンドポイントからタブ アプリケーション トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="a8256-121">Teams requests the tab application token from the Azure Active Directory (AAD) endpoint for the current user.</span></span>
4. <span data-ttu-id="a8256-122">AAD は、タブ アプリケーション トークンをアプリケーションのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="a8256-122">AAD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="a8256-123">Teamsによって返される結果オブジェクトの一部としてタブ アプリケーション トークンをタブに送信 `getAuthToken()` します。</span><span class="sxs-lookup"><span data-stu-id="a8256-123">Teams sends the tab application token to the tab as part of the result object returned by the `getAuthToken()` call.</span></span>
6. <span data-ttu-id="a8256-124">トークンは JavaScript を使用してタブ アプリケーションで解析され、ユーザーのメール アドレスなどの必要な情報を抽出します。</span><span class="sxs-lookup"><span data-stu-id="a8256-124">The token is parsed in the tab application using JavaScript, to extract required information, such as the user's email address.</span></span>

> [!NOTE]
> <span data-ttu-id="a8256-125">この API は、電子メール、プロファイル、および OpenId であるユーザー レベル API の制限されたセット `getAuthToken()` offline_access有効です。</span><span class="sxs-lookup"><span data-stu-id="a8256-125">The `getAuthToken()` is only valid for consenting to a limited set of user-level APIs that is email, profile, offline_access and OpenId.</span></span> <span data-ttu-id="a8256-126">または など、他のスコープGraphには使用 `User.Read` されません `Mail.Read` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-126">It is not used for further Graph scopes such as `User.Read` or `Mail.Read`.</span></span> <span data-ttu-id="a8256-127">推奨される回避策については、その他の[スコープGraph参照してください](#apps-that-require-additional-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="a8256-127">For suggested workarounds, see [additional Graph scopes](#apps-that-require-additional-graph-scopes).</span></span>

<span data-ttu-id="a8256-128">SSO API は、Web コンテンツを [埋め込むタスク](../../../task-modules-and-cards/what-are-task-modules.md) モジュールでも機能します。</span><span class="sxs-lookup"><span data-stu-id="a8256-128">The SSO API also works in [task modules](../../../task-modules-and-cards/what-are-task-modules.md) that embed web content.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="a8256-129">[SSO] タブMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="a8256-129">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="a8256-130">このセクションでは、SSO を使用する [Teams] タブの作成に関連するタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a8256-130">This section describes the tasks involved in creating a Teams tab that uses SSO.</span></span> <span data-ttu-id="a8256-131">これらのタスクは言語とフレームワークに依存しないタスクです。</span><span class="sxs-lookup"><span data-stu-id="a8256-131">These tasks are language- and framework-agnostic.</span></span>

### <a name="1-create-your-aad-application"></a><span data-ttu-id="a8256-132">1. AAD アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="a8256-132">1. Create your AAD application</span></span>

<span data-ttu-id="a8256-133">**AAD ポータルの概要に [アプリケーションを登録](https://azure.microsoft.com/features/azure-portal/) するには**</span><span class="sxs-lookup"><span data-stu-id="a8256-133">**To register your application in the [AAD portal](https://azure.microsoft.com/features/azure-portal/) overview**</span></span>

1. <span data-ttu-id="a8256-134">[AAD アプリケーション ID を取得します](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。</span><span class="sxs-lookup"><span data-stu-id="a8256-134">Get your [AAD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span> 
1. <span data-ttu-id="a8256-135">アプリケーションが AAD エンドポイントに必要なアクセス許可を指定し、必要に応じてGraph。</span><span class="sxs-lookup"><span data-stu-id="a8256-135">Specify the permissions that your application needs for the AAD endpoint and, optionally, Graph.</span></span>
1. <span data-ttu-id="a8256-136">[デスクトップ、web、Teams](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)アプリケーションのアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="a8256-136">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
1. <span data-ttu-id="a8256-137">[スコープのTeams] ボタンを選択し、開くパネルで [スコープ名] とaccess_as_user **を\*\*\*\*入力** します。</span><span class="sxs-lookup"><span data-stu-id="a8256-137">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter **access_as_user** as the **Scope name**.</span></span>

> [!NOTE]
> <span data-ttu-id="a8256-138">以下の重要な制限を知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-138">There are some important restrictions that you must know:</span></span>
>
> * <span data-ttu-id="a8256-139">API のアクセス許可Graphユーザー レベルのアクセス許可 (電子メール、プロファイル、offline_access OpenId) だけがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="a8256-139">Only user-level Graph API permissions are supported that is, email, profile, offline_access, OpenId.</span></span> <span data-ttu-id="a8256-140">その他のスコープ (Graphアクセスできる必要がある場合は、推奨 `User.Read` `Mail.Read` される回避策を[参照してください](#apps-that-require-additional-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="a8256-140">If you must have access to other Graph scopes such as `User.Read` or `Mail.Read`, see [recommended workaround](#apps-that-require-additional-graph-scopes).</span></span>
> * <span data-ttu-id="a8256-141">アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じ名前にすることが重要です。</span><span class="sxs-lookup"><span data-stu-id="a8256-141">It is important that your application's domain name is the same as the domain name you have registered for your AAD application.</span></span>
> * <span data-ttu-id="a8256-142">現在、アプリごとに複数のドメインはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a8256-142">Currently multiple domains per app are not supported.</span></span>

<span data-ttu-id="a8256-143">**AAD ポータルを使用してアプリを登録するには**</span><span class="sxs-lookup"><span data-stu-id="a8256-143">**To register your app through the AAD portal**</span></span>

1. <span data-ttu-id="a8256-144">AAD アプリ登録ポータルに [新しいアプリケーションを登録](https://go.microsoft.com/fwlink/?linkid=2083908) します。</span><span class="sxs-lookup"><span data-stu-id="a8256-144">Register a new application in the [AAD App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
1. <span data-ttu-id="a8256-145">[新規 **登録] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-145">Select **New Registration**.</span></span> <span data-ttu-id="a8256-146">[ **アプリケーションの登録] ページ** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a8256-146">The **Register an application** page appears.</span></span>
1. <span data-ttu-id="a8256-147">[アプリケーションの **登録] ページで** 、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="a8256-147">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="a8256-148">アプリの **[名前]** を入力します。</span><span class="sxs-lookup"><span data-stu-id="a8256-148">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="a8256-149">[サポートされている **アカウントの種類] を選択し、[** 単一テナント] または [マルチテナント アカウントの種類] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a8256-149">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span> <span data-ttu-id="a8256-150">¹</span><span class="sxs-lookup"><span data-stu-id="a8256-150">¹</span></span>
    * <span data-ttu-id="a8256-151">**[リダイレクト URI]** を空のままにします。</span><span class="sxs-lookup"><span data-stu-id="a8256-151">Leave **Redirect URI** empty.</span></span>
    3. <span data-ttu-id="a8256-152">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a8256-152">Choose **Register**.</span></span>
1. <span data-ttu-id="a8256-153">[概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-153">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="a8256-154">アプリケーション マニフェストを更新する際には、後でTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-154">You must have it later when updating your Teams application manifest.</span></span>
1. <span data-ttu-id="a8256-155">[**管理**] で [**API の公開**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a8256-155">Under **Manage**, select **Expose an API**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8256-156">ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次のように入力します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-156">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

1. <span data-ttu-id="a8256-157">[設定 **] リンクを** 選択して、 の形式でアプリケーション ID URI を生成します `api://{AppID}` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-157">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="a8256-158">2 つのスラッシュと GUID の間に、末尾にスラッシュ "/" が付加された完全修飾ドメイン名を挿入します。</span><span class="sxs-lookup"><span data-stu-id="a8256-158">Insert your fully qualified domain name with a forward slash "/" appended to the end, between the double forward slashes and the GUID.</span></span> <span data-ttu-id="a8256-159">ID 全体に . の形式が必要です `api://fully-qualified-domain-name.com/{AppID}` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-159">The entire ID must have the form of `api://fully-qualified-domain-name.com/{AppID}`.</span></span> <span data-ttu-id="a8256-160">² たとえば `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 、 .</span><span class="sxs-lookup"><span data-stu-id="a8256-160">² For example, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`.</span></span> <span data-ttu-id="a8256-161">完全修飾ドメイン名は、アプリが提供される人間が読み取り可能なドメイン名です。</span><span class="sxs-lookup"><span data-stu-id="a8256-161">The fully qualified domain name is the human readable domain name from which your app is served.</span></span> <span data-ttu-id="a8256-162">ngrok などのトンネリング サービスを使用している場合は、ngrok サブドメインが変更されるたびにこの値を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-162">If you are using a tunneling service such as ngrok, you must update this value whenever your ngrok subdomain changes.</span></span>
1. <span data-ttu-id="a8256-163">**[スコープの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a8256-163">Select **Add a scope**.</span></span> <span data-ttu-id="a8256-164">開くパネルで、[スコープ名] **access_as_user** を **入力します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-164">In the panel that opens, enter **access_as_user** as the **Scope name**.</span></span>
1. <span data-ttu-id="a8256-165">[同意 **できるWho] ボックスに、「\*\*\*\*管理者とユーザー」と入力します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-165">In the **Who can consent?** box, enter **Admins and users**.</span></span>
1. <span data-ttu-id="a8256-166">スコープに適した値を使用して管理者とユーザーの同意のプロンプトを構成するための詳細をボックスに入力 `access_as_user` します。</span><span class="sxs-lookup"><span data-stu-id="a8256-166">Enter the details in the boxes for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope:</span></span>
    * <span data-ttu-id="a8256-167">**管理者の同意タイトル:** チームはユーザーのプロフィールにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a8256-167">**Admin consent title:** Teams can access the user’s profile.</span></span>
    * <span data-ttu-id="a8256-168">**管理者の同意の** 説明: Teamsアプリの Web API を現在のユーザーとして呼び出す場合があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-168">**Admin consent description**: Teams can call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="a8256-169">**ユーザーの同意タイトル**: Teamsにアクセスして、ユーザーに代わって要求を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a8256-169">**User consent title**: Teams can access your profile and make requests on your behalf.</span></span>
    * <span data-ttu-id="a8256-170">**ユーザーの同意の説明: Teams** と同じ権限でこのアプリの API を呼び出す場合があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-170">**User consent description:** Teams can call this app’s APIs with the same rights as you have.</span></span>
1. <span data-ttu-id="a8256-171">**[状態]** が **[有効]** に設定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="a8256-171">Ensure that **State** is set to **Enabled**.</span></span>
1. <span data-ttu-id="a8256-172">[スコープ **の追加] を** 選択して詳細を保存します。</span><span class="sxs-lookup"><span data-stu-id="a8256-172">Select **Add scope** to save the details.</span></span> <span data-ttu-id="a8256-173">テキスト フィールドの下に表示 **されるスコープ** 名のドメイン 部分は、前の手順で設定した **アプリケーション ID** URI と自動的に一致し、末尾に追加 `/access_as_user` する必要があります `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-173">The domain part of the **Scope name** displayed below the text field must automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.</span></span>
1. <span data-ttu-id="a8256-174">[承認済 **みクライアント アプリケーション** ] セクションで、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。</span><span class="sxs-lookup"><span data-stu-id="a8256-174">In the **Authorized client applications** section, identify the applications that you want to authorize for your app’s web application.</span></span> <span data-ttu-id="a8256-175">[クライアント **アプリケーションの追加] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-175">Select **Add a client application**.</span></span> <span data-ttu-id="a8256-176">次の各クライアント ID を入力し、前の手順で作成した承認済みスコープを選択します。</span><span class="sxs-lookup"><span data-stu-id="a8256-176">Enter each of the following client IDs and select the authorized scope you created in the previous step:</span></span>
    * <span data-ttu-id="a8256-177">`1fec8e78-bce4-4aaf-ab1b-5451cc387264`モバイルTeamsデスクトップ アプリケーションの場合。</span><span class="sxs-lookup"><span data-stu-id="a8256-177">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` for Teams mobile or desktop application.</span></span>
    * <span data-ttu-id="a8256-178">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346`web アプリケーションTeamsの場合。</span><span class="sxs-lookup"><span data-stu-id="a8256-178">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` for Teams web application.</span></span>
1. <span data-ttu-id="a8256-179">**[API のアクセス許可] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-179">Navigate to **API Permissions**.</span></span> <span data-ttu-id="a8256-180">[**アクセス許可を**  >  **追加する] Graph** 委任されたアクセス許可を選択し、次のアクセス許可を API から  >  Graphします。</span><span class="sxs-lookup"><span data-stu-id="a8256-180">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Graph API:</span></span>
    * <span data-ttu-id="a8256-181">User.Read は既定で有効になっています</span><span class="sxs-lookup"><span data-stu-id="a8256-181">User.Read enabled by default</span></span>
    * <span data-ttu-id="a8256-182">メール</span><span class="sxs-lookup"><span data-stu-id="a8256-182">email</span></span>
    * <span data-ttu-id="a8256-183">offline_access</span><span class="sxs-lookup"><span data-stu-id="a8256-183">offline_access</span></span>
    * <span data-ttu-id="a8256-184">OpenId</span><span class="sxs-lookup"><span data-stu-id="a8256-184">OpenId</span></span>
    * <span data-ttu-id="a8256-185">profile</span><span class="sxs-lookup"><span data-stu-id="a8256-185">profile</span></span>

1. <span data-ttu-id="a8256-186">[認証] **に移動します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-186">Navigate to **Authentication**.</span></span>

    <span data-ttu-id="a8256-187">アプリに IT 管理者の同意が与えされていない場合、ユーザーはアプリを初めて使用する場合に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-187">If an app has not been granted IT admin consent, users have to provide consent the first time they use an app.</span></span>

    <span data-ttu-id="a8256-188">リダイレクト URI を入力するには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="a8256-188">To enter a redirect URI:</span></span>
    * <span data-ttu-id="a8256-189">[プラットフォーム **の追加] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-189">Select **Add a platform**.</span></span>
    * <span data-ttu-id="a8256-190">**[Web] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a8256-190">Select **web**.</span></span>
    * <span data-ttu-id="a8256-191">アプリの **リダイレクト URI** を入力します。</span><span class="sxs-lookup"><span data-stu-id="a8256-191">Enter the **redirect URI** for your app.</span></span> <span data-ttu-id="a8256-192">これは、成功した暗黙的な付与フローがユーザーをリダイレクトするページです。</span><span class="sxs-lookup"><span data-stu-id="a8256-192">This is the page where a successful implicit grant flow redirects the user.</span></span> <span data-ttu-id="a8256-193">これは、手順 5 で入力した完全修飾ドメイン名の後に、認証応答が送信される API ルートと同じです。</span><span class="sxs-lookup"><span data-stu-id="a8256-193">This is the same fully qualified domain name that you entered in step 5 followed by the API route where an authentication response is sent.</span></span> <span data-ttu-id="a8256-194">次のサンプルに従う場合は、Teamsです `https://subdomain.example.com/auth-end` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-194">If you are following any of the Teams samples, this is `https://subdomain.example.com/auth-end`.</span></span>

    <span data-ttu-id="a8256-195">次のボックスをチェックして暗黙的な付与を有効にする: ✔ ID トークン✔アクセス トークン</span><span class="sxs-lookup"><span data-stu-id="a8256-195">Enable implicit grant by checking the following boxes:  ✔ ID Token  ✔ Access Token</span></span>

<span data-ttu-id="a8256-196">お疲れさまでした。</span><span class="sxs-lookup"><span data-stu-id="a8256-196">Congratulations!</span></span> <span data-ttu-id="a8256-197">タブ SSO アプリを続行するためのアプリ登録の前提条件が完了しました。</span><span class="sxs-lookup"><span data-stu-id="a8256-197">You have completed the app registration prerequisites to proceed with your tab SSO app.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="a8256-198">¹ AAD アプリが Teams で認証要求を行うのと同じテナントに登録されている場合、ユーザーは同意を求めれなく、アクセス トークンがすぐ付与されます。</span><span class="sxs-lookup"><span data-stu-id="a8256-198">¹ If your AAD app is registered in the same tenant where you are making an authentication request in Teams, the user cannot be asked to consent and is granted an access token right away.</span></span> <span data-ttu-id="a8256-199">ユーザーは、AAD アプリが別のテナントに登録されている場合にのみ、これらのアクセス許可に同意します。</span><span class="sxs-lookup"><span data-stu-id="a8256-199">Users only consent to these permissions if the AAD app is registered in a different tenant.</span></span>
> * <span data-ttu-id="a8256-200">² カスタム ドメインが AAD に追加されていない場合は、ホスト名が既に所有されているドメインに基づいていなければならないというエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a8256-200">² If the custom domain is not added to AAD, you get an error stating that the host name must not be based on an already owned domain.</span></span> <span data-ttu-id="a8256-201">カスタム ドメインを AAD に追加して登録するには [、AAD](/azure/active-directory/fundamentals/add-custom-domain) にカスタム ドメイン名を追加する手順に従い、手順 5 を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="a8256-201">To add custom domain to AAD and register it, follow the [add a custom domain name to AAD](/azure/active-directory/fundamentals/add-custom-domain) procedure, and then repeat step 5.</span></span> <span data-ttu-id="a8256-202">このエラーは、テナントの管理者資格情報でサインインしていない場合Office 365できます。</span><span class="sxs-lookup"><span data-stu-id="a8256-202">You can also get this error if you are not signed in with Admin credentials in the Office 365 tenancy.</span></span>
> * <span data-ttu-id="a8256-203">返されるアクセス トークンでユーザー プリンシパル名 (UPN) を受信していない場合は、AAD でオプションの [クレームとして追加](/azure/active-directory/develop/active-directory-optional-claims) できます。</span><span class="sxs-lookup"><span data-stu-id="a8256-203">If you are not receiving the user principal name (UPN) in the returned access token, you can add it as an [optional claim](/azure/active-directory/develop/active-directory-optional-claims) in AAD.</span></span>

### <a name="2-update-your-teams-application-manifest"></a><span data-ttu-id="a8256-204">2. アプリケーション マニフェストTeams更新する</span><span class="sxs-lookup"><span data-stu-id="a8256-204">2. Update your Teams application manifest</span></span>

<span data-ttu-id="a8256-205">次のコードを使用して、新しいプロパティをマニフェストにTeamsします。</span><span class="sxs-lookup"><span data-stu-id="a8256-205">Use the following code to add new properties to your Teams manifest:</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* <span data-ttu-id="a8256-206">**WebApplicationInfo** は、次の要素の親です。</span><span class="sxs-lookup"><span data-stu-id="a8256-206">**WebApplicationInfo** is the parent of the following elements:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8256-207">**id** - アプリケーションのクライアント ID。</span><span class="sxs-lookup"><span data-stu-id="a8256-207">**id** - The client ID of the application.</span></span> <span data-ttu-id="a8256-208">これは、Azure アプリケーションへのアプリケーションの登録の一環として取得したアプリケーション ID AD。</span><span class="sxs-lookup"><span data-stu-id="a8256-208">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="a8256-209">**resource** - アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="a8256-209">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="a8256-210">これは、手順 6 で作成するときに登録したのと同じ URI (プロトコルを含む `api://` ) `scope` です。</span><span class="sxs-lookup"><span data-stu-id="a8256-210">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6.</span></span> <span data-ttu-id="a8256-211">リソースにパスを `access_as_user` 含めなけれ。</span><span class="sxs-lookup"><span data-stu-id="a8256-211">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="a8256-212">この URI のドメイン部分は、アプリケーション マニフェストの URL で使用されるサブドメインを含むドメインTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-212">The domain part of this URI must match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="a8256-213">AAD アプリのリソースは、通常、サイト URL のルートと appID (たとえば) です `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-213">The resource for an AAD app is usually the root of its site URL and the appID (e.g. `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`).</span></span> <span data-ttu-id="a8256-214">この値は、要求が同じドメインから送信されるのを確認するためにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="a8256-214">This value is also used to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="a8256-215">タブの `contentURL` リソース プロパティと同じドメインが使用されます。</span><span class="sxs-lookup"><span data-stu-id="a8256-215">Ensure that the `contentURL` for your tab uses the same domains as your resource property.</span></span>
>* <span data-ttu-id="a8256-216">フィールドを実装するには、マニフェスト バージョン 1.5 以上を使用する必要 `webApplicationInfo` があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-216">You must use manifest version 1.5 or higher to implement the `webApplicationInfo` field.</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="a8256-217">3. クライアント側コードから認証トークンを取得する</span><span class="sxs-lookup"><span data-stu-id="a8256-217">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="a8256-218">次の認証 API を使用します。</span><span class="sxs-lookup"><span data-stu-id="a8256-218">Use the following authentication API:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="a8256-219">ユーザー レベルのアクセス許可を呼び出し、追加のユーザーの同意が必要な場合は、追加の同意を付与するためのダイアログ `getAuthToken` がユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a8256-219">When you call `getAuthToken` - and additional user consent is required for user-level permissions, a dialog is shown to the user to grant additional consent.</span></span>

<span data-ttu-id="a8256-220">成功コールバックでアクセス トークンを受信した後、アクセス トークンをデコードして、そのトークンに関連付けられているクレームを表示できます。</span><span class="sxs-lookup"><span data-stu-id="a8256-220">After you receive the access token in the success callback, you can decode the access token to view the claims associated with that token.</span></span> <span data-ttu-id="a8256-221">必要に応じて、アクセス トークンを手動でコピーしてツールに貼り付[](https://jwt.ms/)けます (コンテンツを jwt.ms など)。</span><span class="sxs-lookup"><span data-stu-id="a8256-221">Optionally, you can manually copy and paste the access token into a tool, such as [jwt.ms](https://jwt.ms/) to inspect its contents.</span></span> <span data-ttu-id="a8256-222">返されるアクセス トークンで UPN を受信していない場合は、AAD でオプションのクレーム [として](/azure/active-directory/develop/active-directory-optional-claims) 追加できます。</span><span class="sxs-lookup"><span data-stu-id="a8256-222">If you are not receiving the UPN in the returned access token, you can add it as an [optional claim](/azure/active-directory/develop/active-directory-optional-claims) in AAD.</span></span>

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a><span data-ttu-id="a8256-223">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="a8256-223">Code sample</span></span>

|<span data-ttu-id="a8256-224">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="a8256-224">**Sample name**</span></span>|<span data-ttu-id="a8256-225">**説明**</span><span class="sxs-lookup"><span data-stu-id="a8256-225">**Description**</span></span>|<span data-ttu-id="a8256-226">**C#**</span><span class="sxs-lookup"><span data-stu-id="a8256-226">**C#**</span></span>|<span data-ttu-id="a8256-227">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="a8256-227">**Node.js**</span></span>|
|---------------|---------------|------|--------------|
| <span data-ttu-id="a8256-228">タブ SSO</span><span class="sxs-lookup"><span data-stu-id="a8256-228">Tab SSO</span></span> |<span data-ttu-id="a8256-229">Microsoft Teamsのサンプル アプリ Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a8256-229">Microsoft Teams sample app for tabs Azure AD SSO</span></span>| [<span data-ttu-id="a8256-230">View</span><span class="sxs-lookup"><span data-stu-id="a8256-230">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|<span data-ttu-id="a8256-231">[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、</span><span class="sxs-lookup"><span data-stu-id="a8256-231">[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs),</span></span> </br>[<span data-ttu-id="a8256-232">Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="a8256-232">Teams Toolkit</span></span>](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a><span data-ttu-id="a8256-233">既知の制限</span><span class="sxs-lookup"><span data-stu-id="a8256-233">Known limitations</span></span>

### <a name="apps-that-require-additional-graph-scopes"></a><span data-ttu-id="a8256-234">追加のスコープを必要とするGraphアプリ</span><span class="sxs-lookup"><span data-stu-id="a8256-234">Apps that require additional Graph scopes</span></span>

<span data-ttu-id="a8256-235">SSO の現在の実装では、メール、プロファイル、offline_access、OpenId などのユーザー レベルのアクセス許可に対する同意のみを付与し、User.Read や Mail.Read などの他の API には同意しません。</span><span class="sxs-lookup"><span data-stu-id="a8256-235">Our current implementation for SSO only grants consent for user-level permissions that is email, profile, offline_access, OpenId and not for other APIs such as User.Read or Mail.Read.</span></span> <span data-ttu-id="a8256-236">アプリがスコープをさらにGraph場合は、次のセクションで有効にする回避策を示します。</span><span class="sxs-lookup"><span data-stu-id="a8256-236">If your app needs further Graph scopes, the next section provides some enabling workarounds.</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="a8256-237">テナント管理者の同意</span><span class="sxs-lookup"><span data-stu-id="a8256-237">Tenant Admin Consent</span></span>

<span data-ttu-id="a8256-238">最も簡単な方法は、組織の代わりにテナント管理者に事前同意を得る方法です。</span><span class="sxs-lookup"><span data-stu-id="a8256-238">The simplest approach is to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="a8256-239">つまり、ユーザーはこれらのスコープに同意する必要が無く、AAD の代理フローを使用してトークン サーバー側を自由に交換 [できます](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。</span><span class="sxs-lookup"><span data-stu-id="a8256-239">This means users do not have to consent to these scopes and you can then be free to exchange the token server side using AAD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="a8256-240">この回避策は、社内の業務用アプリケーションでは受け入れ可能ですが、テナント管理者の承認に依存できないサードパーティの開発者には十分ではありません。</span><span class="sxs-lookup"><span data-stu-id="a8256-240">This workaround is acceptable for internal line-of-business applications but is not enough for third-party developers who are not able to rely on tenant admin approval.</span></span>

<span data-ttu-id="a8256-241">テナント管理者として組織に代わって同意する簡単な方法は、 を参照する方法です `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` 。</span><span class="sxs-lookup"><span data-stu-id="a8256-241">A simple way of consenting on behalf of an organization as a tenant admin is to refer to `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`.</span></span>

#### <a name="ask-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="a8256-242">Auth API を使用して追加の同意を求める</span><span class="sxs-lookup"><span data-stu-id="a8256-242">Ask for additional consent using the Auth API</span></span>

<span data-ttu-id="a8256-243">Graph スコープを追加するもう 1 つの方法は、Azure AD 同意ダイアログ ボックスをポップアップする既存の Web ベース[の Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)認証アプローチを使用して同意ダイアログを表示する方法です。</span><span class="sxs-lookup"><span data-stu-id="a8256-243">Another approach for getting additional Graph scopes is to present a consent dialog using our existing [web-based Azure AD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an Azure AD consent dialog box.</span></span> 

<span data-ttu-id="a8256-244">**Auth API を使用して追加の同意を求めるには**</span><span class="sxs-lookup"><span data-stu-id="a8256-244">**To ask for additional consent using the Auth API**</span></span>

1. <span data-ttu-id="a8256-245">これらの追加の API へのアクセスを取得するには `getAuthToken()` 、AAD [on-half-Graph of](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow を使用してサーバー側で交換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-245">The token retrieved using `getAuthToken()` needs to be exchanged server-side using AAD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) to get access to those additional Graph APIs.</span></span> <span data-ttu-id="a8256-246">この交換に v2 Graphエンドポイントを使用してください。</span><span class="sxs-lookup"><span data-stu-id="a8256-246">Ensure you use the v2 Graph endpoint for this exchange.</span></span>
2. <span data-ttu-id="a8256-247">Exchange が失敗した場合、AAD は無効な付与例外を返します。</span><span class="sxs-lookup"><span data-stu-id="a8256-247">If the exchange fails, AAD returns an invalid grant exception.</span></span> <span data-ttu-id="a8256-248">通常、2 つのエラー メッセージの 1 つ、 `invalid_grant` または `interaction_required` .</span><span class="sxs-lookup"><span data-stu-id="a8256-248">There are usually one of two error messages, `invalid_grant` or `interaction_required`.</span></span>
3. <span data-ttu-id="a8256-249">交換が失敗した場合は、追加の同意を求める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8256-249">When the exchange fails, you must ask for additional consent.</span></span> <span data-ttu-id="a8256-250">ユーザーに追加の同意を許可するユーザー インターフェイス (UI) を表示します。</span><span class="sxs-lookup"><span data-stu-id="a8256-250">Show some user interface (UI) asking the user to grant additional consent.</span></span> <span data-ttu-id="a8256-251">この UI には、AAD 認証 API を使用して AAD 同意ダイアログ ボックスをトリガーする [ボタンが含まれる必要があります](~/concepts/authentication/auth-silent-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="a8256-251">This UI must include a button that triggers an AAD consent dialog box using our [AAD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="a8256-252">AAD から追加の同意を求める場合は、クエリ文字列パラメーターを AAD に含める必要があります。それ以外の場合、AAD は追加のスコープを `prompt=consent` 求めずに[](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)行います。</span><span class="sxs-lookup"><span data-stu-id="a8256-252">When asking for additional consent from AAD, you must include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to AAD, otherwise AAD does not ask for the additional scopes.</span></span>
    * <span data-ttu-id="a8256-253">代わりに `?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="a8256-253">Instead of `?scope={scopes}`</span></span>
    * <span data-ttu-id="a8256-254">これを使用する `?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="a8256-254">Use this `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="a8256-255">Mail.Read や User.Read など、ユーザーに求めるすべてのスコープ `{scopes}` が含まれるか確認します。</span><span class="sxs-lookup"><span data-stu-id="a8256-255">Ensure that `{scopes}` includes all the scopes you are prompting the user for, for example, Mail.Read or User.Read.</span></span>
5. <span data-ttu-id="a8256-256">ユーザーが追加のアクセス許可を付与したら、これらの追加 API へのアクセスを取得するために、フローの代理を再試行します。</span><span class="sxs-lookup"><span data-stu-id="a8256-256">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-aad-authentication"></a><span data-ttu-id="a8256-257">AAD 以外の認証</span><span class="sxs-lookup"><span data-stu-id="a8256-257">Non-AAD authentication</span></span>

<span data-ttu-id="a8256-258">上記の認証ソリューションは、ID プロバイダーとして AAD をサポートするアプリとサービスでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="a8256-258">The above-described authentication solution only works for apps and services that support AAD as an identity provider.</span></span> <span data-ttu-id="a8256-259">AAD ベース以外のサービスを使用して認証するアプリは、ポップアップ ベースの Web 認証フローを引き続き [使用する必要があります](~/concepts/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="a8256-259">Apps that want to authenticate using non-AAD based services must continue using the pop-up-based [web authentication flow](~/concepts/authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a8256-260">SSO は、AAD B2C テナント内の顧客所有アプリでサポートされます。</span><span class="sxs-lookup"><span data-stu-id="a8256-260">SSO is supported for customer owned apps within the AAD B2C tenants.</span></span>
