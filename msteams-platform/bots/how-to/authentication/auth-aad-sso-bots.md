---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者は、OAuth カードのサポートを受け取ってサインイン カードまたは Azure ボット サービスを使用できます。
keywords: トークン、ユーザー トークン、ボットの SSO サポート
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a43c2a46561149ff97d039a3ba8fe9f4472e2073
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566095"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="957fe-105">ボットのシングル サインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="957fe-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="957fe-106">Azure Active Directory (AAD) のシングル サインオン認証では、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑え、認証トークンをサイレント モードで更新します。</span><span class="sxs-lookup"><span data-stu-id="957fe-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="957fe-107">ユーザーがアプリの使用に同意すると、別のデバイスでもう一度同意する必要はありません。自動的にサインインできます。</span><span class="sxs-lookup"><span data-stu-id="957fe-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="957fe-108">このフローは、Microsoft Teams SSO サポート[のフローと](../../../tabs/how-to/authentication/auth-aad-sso.md)似ていますが、ボットがトークンを要求して応答を受け[](#request-a-bot-token)取る方法のプロトコルに[違いがあります](#receive-the-bot-token)。</span><span class="sxs-lookup"><span data-stu-id="957fe-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="957fe-109">OAuth 2.0 は、AAD および他の多くの ID プロバイダーが使用する認証と承認のオープン標準です。</span><span class="sxs-lookup"><span data-stu-id="957fe-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="957fe-110">OAuth 2.0 の基本的な理解は、認証を使用する場合の前提条件Teams。</span><span class="sxs-lookup"><span data-stu-id="957fe-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="957fe-111">実行時のボット SSO</span><span class="sxs-lookup"><span data-stu-id="957fe-111">Bot SSO at runtime</span></span>

![実行時の図でのボット SSO](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="957fe-113">認証およびボット アプリケーション トークンを取得するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="957fe-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="957fe-114">ボットが、`tokenExchangeResource`プロパティを含む OAuthCard でメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="957fe-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="957fe-115">ボット アプリケーションTeamsトークンを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="957fe-116">ユーザーは、アクティブなすべてのユーザー エンドポイントでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="957fe-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="957fe-117">ユーザーは、一度に複数のアクティブなエンドポイントを持つ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="957fe-118">ボット トークンは、すべてのアクティブなユーザーのエンドポイントから受信されます。</span><span class="sxs-lookup"><span data-stu-id="957fe-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="957fe-119">SSO をサポートするには、アプリを個人用のスコープにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-119">The app must be installed in personal scope for SSO support.</span></span>

1. <span data-ttu-id="957fe-120">現在のユーザーが初めてボット アプリケーションを使用している場合は、ユーザーに次のいずれかの操作を要求する要求プロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="957fe-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="957fe-121">必要に応じて同意を提供します。</span><span class="sxs-lookup"><span data-stu-id="957fe-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="957fe-122">2 要素認証などのステップ アップ認証を処理します。</span><span class="sxs-lookup"><span data-stu-id="957fe-122">Handle step-up authentication, such as two-factor authentication.</span></span>

1. <span data-ttu-id="957fe-123">Teamsユーザーの AAD エンドポイントからボット アプリケーション トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="957fe-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

1. <span data-ttu-id="957fe-124">AAD はボット アプリケーション トークンをアプリケーションにTeamsします。</span><span class="sxs-lookup"><span data-stu-id="957fe-124">AAD sends the bot application token to the Teams application.</span></span>

1. <span data-ttu-id="957fe-125">Teamsサインイン **/tokenExchange** という名前の呼び出しアクティビティによって返される値オブジェクトの一部として、トークンをボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="957fe-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
1. <span data-ttu-id="957fe-126">ボット アプリケーションの解析されたトークンは、ユーザーのメール アドレスなど、必要な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="957fe-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="957fe-127">SSO サーバー ボットTeamsする</span><span class="sxs-lookup"><span data-stu-id="957fe-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="957fe-128">SSO ボットを開発するには、次の手順Teamsします。</span><span class="sxs-lookup"><span data-stu-id="957fe-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="957fe-129">[AAD ポータルを使用してアプリを登録します](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="957fe-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
1. <span data-ttu-id="957fe-130">[ボットのTeamsアプリケーション マニフェストを更新します](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="957fe-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
1. <span data-ttu-id="957fe-131">[ボット トークンを要求および受信するコードを追加します](#add-the-code-to-request-and-receive-a-bot-token)。</span><span class="sxs-lookup"><span data-stu-id="957fe-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="957fe-132">AAD ポータルを介してアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="957fe-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="957fe-133">AAD ポータルを介してアプリを登録する手順は、タブ SSO フロー [に似ています](../../../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="957fe-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="957fe-134">アプリを登録するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="957fe-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="957fe-135">アプリ登録ポータルで新[しいAzure Active Directoryを登録](https://go.microsoft.com/fwlink/?linkid=2083908)します。</span><span class="sxs-lookup"><span data-stu-id="957fe-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="957fe-136">[新規 **登録] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="957fe-136">Select **New Registration**.</span></span> <span data-ttu-id="957fe-137">[ **アプリケーションの登録] ページ** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="957fe-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="957fe-138">[アプリケーションの **登録] ページで** 、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="957fe-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="957fe-139">アプリの **[名前]** を入力します。</span><span class="sxs-lookup"><span data-stu-id="957fe-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="957fe-140">[サポートされている **アカウントの種類] を選択し、[** 単一テナント] または [マルチテナント アカウントの種類] を選択します。</span><span class="sxs-lookup"><span data-stu-id="957fe-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="957fe-141">AAD アプリが Teams で認証要求を行っているのと同じテナントに登録されている場合、ユーザーは同意を求めではなく、アクセス トークンが付与されます。</span><span class="sxs-lookup"><span data-stu-id="957fe-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="957fe-142">ただし、AAD アプリが別のテナントに登録されている場合、ユーザーはアクセス許可に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="957fe-143">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="957fe-143">Choose **Register**.</span></span>
4. <span data-ttu-id="957fe-144">[概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。</span><span class="sxs-lookup"><span data-stu-id="957fe-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="957fe-145">後でアプリケーション マニフェストを更新するときにTeams必要です。</span><span class="sxs-lookup"><span data-stu-id="957fe-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="957fe-146">[**管理**] で [**API の公開**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="957fe-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="957fe-147">スタンドアロン ボットを作成する場合は、アプリケーション ID URI を次のように入力します `api://botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="957fe-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="957fe-148">ここでは **、YourBotId** は AAD アプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="957fe-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="957fe-149">ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次のように入力します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="957fe-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="957fe-150">アプリケーションが AAD エンドポイントに必要なアクセス許可を選択し、必要に応じて Microsoft エンドポイントGraph。</span><span class="sxs-lookup"><span data-stu-id="957fe-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="957fe-151">[デスクトップ、web、Teams](/azure/active-directory/develop/v2-permissions-and-consent)アプリケーションのアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="957fe-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="957fe-152">**[スコープの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="957fe-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="957fe-153">開くパネルで、スコープ名を入力してクライアント `access_as_user` アプリ **を追加します**。</span><span class="sxs-lookup"><span data-stu-id="957fe-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="957fe-154">クライアント アプリのaccess_as_userに使用される "管理者とユーザー" スコープは、"管理者とユーザー" です。</span><span class="sxs-lookup"><span data-stu-id="957fe-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="957fe-155">次の重要な制限に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="957fe-156">電子メール、プロファイル、Graph OpenId などのユーザー レベルの API アクセス許可offline_accessのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="957fe-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="957fe-157">その他の Microsoft Graphスコープ (Graphなど) にアクセスする必要がある場合は、 `User.Read` `Mail.Read` 推奨される回避策を[参照してください](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="957fe-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).</span></span>
    > * <span data-ttu-id="957fe-158">アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="957fe-159">アプリごとに複数のドメインは現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="957fe-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="957fe-160">ドメインを使用するアプリケーションは一般的であり、セキュリティ リスクである可能性があるため `azurewebsites.net` 、サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="957fe-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="957fe-161">OAuth 接続を使用して Azure ポータルを更新する</span><span class="sxs-lookup"><span data-stu-id="957fe-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="957fe-162">OAuth 接続を使用して Azure ポータルを更新するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="957fe-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="957fe-163">Azure Portal で、[アプリの登録] **に移動します**。</span><span class="sxs-lookup"><span data-stu-id="957fe-163">In the Azure Portal, navigate to **App registrations**.</span></span>

2. <span data-ttu-id="957fe-164">[API の **アクセス許可] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="957fe-164">Go to **API Permissions**.</span></span> <span data-ttu-id="957fe-165">[**アクセス許可を追加する]** Graph委任されたアクセス許可] を選択し、次のアクセス許可を Microsoft Graph  >    >  API に追加します。</span><span class="sxs-lookup"><span data-stu-id="957fe-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="957fe-166">User.Read (既定で有効)</span><span class="sxs-lookup"><span data-stu-id="957fe-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="957fe-167">メール</span><span class="sxs-lookup"><span data-stu-id="957fe-167">email</span></span>
    * <span data-ttu-id="957fe-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="957fe-168">offline_access</span></span>
    * <span data-ttu-id="957fe-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="957fe-169">OpenId</span></span>
    * <span data-ttu-id="957fe-170">profile</span><span class="sxs-lookup"><span data-stu-id="957fe-170">profile</span></span>

3. <span data-ttu-id="957fe-171">Azure Portal で、[ボット チャネル登録 **] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="957fe-171">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

4. <span data-ttu-id="957fe-172">左側 **設定** を選択し **、[OAuth** 接続] セクション **の**[設定の設定します。</span><span class="sxs-lookup"><span data-stu-id="957fe-172">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![SSOBotHandle2 ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. <span data-ttu-id="957fe-174">[新しい接続設定] フォームを完了するには **、次の手順を実行** します。</span><span class="sxs-lookup"><span data-stu-id="957fe-174">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="957fe-175">**AAD アプリケーション** では暗黙的な付与が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-175">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="957fe-176">[新しい **接続設定]** ページ **に名前を入力** します。</span><span class="sxs-lookup"><span data-stu-id="957fe-176">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="957fe-177">これは、実行時にボット SSO の手順 *5* でボット サービス コードの設定 [内で参照される名前です](#bot-sso-at-runtime)。</span><span class="sxs-lookup"><span data-stu-id="957fe-177">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="957fe-178">[サービス **プロバイダー] ドロップダウン** から、[v2] **Azure Active Directory選択します**。</span><span class="sxs-lookup"><span data-stu-id="957fe-178">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="957fe-179">AAD アプリケーションのクライアント **ID** や **クライアント** シークレットなどのクライアント資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="957fe-179">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="957fe-180">Token Exchange **URL の** 場合は、「Update your Teams アプリケーション マニフェスト」で定義されているスコープ値 [を使用します](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="957fe-180">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="957fe-181">トークンのExchange URL は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示します。</span><span class="sxs-lookup"><span data-stu-id="957fe-181">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="957fe-182">[テナント **ID] ボックスに** 「共通」と *入力します*。</span><span class="sxs-lookup"><span data-stu-id="957fe-182">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="957fe-183">AAD **アプリケーションのダウンストリーム** API へのアクセス許可を指定するときに構成されたスコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="957fe-183">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="957fe-184">クライアント ID とクライアント シークレットが提供されている場合、トークン ストアは、定義されたアクセス許可を持つグラフ トークンのトークンを交換します。</span><span class="sxs-lookup"><span data-stu-id="957fe-184">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="957fe-185">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="957fe-185">Select **Save**.</span></span>

    ![VuSSOBotConnection 設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="957fe-187">ボットのTeamsアプリケーション マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="957fe-187">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="957fe-188">アプリケーションにスタンドアロン ボットが含まれている場合は、次のコードを使用して新しいプロパティをアプリケーション マニフェストTeamsします。</span><span class="sxs-lookup"><span data-stu-id="957fe-188">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="957fe-189">アプリケーションにボットとタブが含まれている場合は、次のコードを使用して新しいプロパティをアプリケーション マニフェストTeamsします。</span><span class="sxs-lookup"><span data-stu-id="957fe-189">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="957fe-190">**webApplicationInfo** は、次の要素の親です。</span><span class="sxs-lookup"><span data-stu-id="957fe-190">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="957fe-191">**id** - アプリケーションのクライアント ID。</span><span class="sxs-lookup"><span data-stu-id="957fe-191">**id** - The client ID of the application.</span></span> <span data-ttu-id="957fe-192">これは、アプリケーションを AAD に登録する一部として取得したアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="957fe-192">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="957fe-193">**resource** - アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="957fe-193">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="957fe-194">これは、AAD ポータルからアプリを登録するで作成するときに登録したプロトコルを含む、同じ `api://` `scope` URI [です](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="957fe-194">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="957fe-195">リソースにパスを `access_as_user` 含めなけれ。</span><span class="sxs-lookup"><span data-stu-id="957fe-195">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="957fe-196">この URI のドメイン部分は、アプリケーション マニフェストの URL で使用されるドメインとサブドメインTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-196">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="957fe-197">ボット トークンを要求および受信するコードを追加する</span><span class="sxs-lookup"><span data-stu-id="957fe-197">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="957fe-198">ボット トークンの要求</span><span class="sxs-lookup"><span data-stu-id="957fe-198">Request a bot token</span></span>

<span data-ttu-id="957fe-199">トークンを取得する要求は、既存のメッセージ スキーマを使用した通常の POST メッセージ要求です。</span><span class="sxs-lookup"><span data-stu-id="957fe-199">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="957fe-200">これは、OAuthCard の添付ファイルに含まれています。</span><span class="sxs-lookup"><span data-stu-id="957fe-200">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="957fe-201">OAuthCard クラスのスキーマは Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義され、サインイン カードに似ています。</span><span class="sxs-lookup"><span data-stu-id="957fe-201">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="957fe-202">Teamsがカードに設定されている場合、この要求はサイレント トークン取得 `TokenExchangeResource` として扱います。</span><span class="sxs-lookup"><span data-stu-id="957fe-202">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="957fe-203">このチャネルTeamsトークン要求を一意に識別するプロパティだけが `Id` 受け入れされます。</span><span class="sxs-lookup"><span data-stu-id="957fe-203">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="957fe-204">SSO 認証Microsoft Bot Framework `OAuthPrompt` `MultiProviderAuthDialog` サポートされている場合は、SSO 認証がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="957fe-204">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="957fe-205">ユーザーが初めてアプリケーションを使用し、ユーザーの同意が必要な場合は、次のダイアログ ボックスが表示され、同意エクスペリエンスが続行されます。</span><span class="sxs-lookup"><span data-stu-id="957fe-205">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

![[同意] ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="957fe-207">ユーザーが **[続行する]** を選択すると、次のイベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="957fe-207">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="957fe-208">ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリームの OAuth カード ボタンからのサインイン フローと同様にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="957fe-208">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="957fe-209">開発者は、ユーザーの同意が必要なアクセス許可を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-209">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="957fe-210">この方法は、 を超えるアクセス許可を持つトークンが必要な場合にお勧めします `openId` 。</span><span class="sxs-lookup"><span data-stu-id="957fe-210">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="957fe-211">たとえば、グラフ リソース用にトークンを交換する場合です。</span><span class="sxs-lookup"><span data-stu-id="957fe-211">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="957fe-212">ボットが OAuth カードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットに対してユーザーの同意が必要です。</span><span class="sxs-lookup"><span data-stu-id="957fe-212">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="957fe-213">このトークンは、基本認証やユーザーの電子メール アドレスの取得に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="957fe-213">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="957fe-214">C#ボタンを使用せずにトークン要求を実行する</span><span class="sxs-lookup"><span data-stu-id="957fe-214">C# token request without a sign-in button</span></span>

```csharp
    var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

       await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receive-the-bot-token"></a><span data-ttu-id="957fe-215">ボット トークンの受信</span><span class="sxs-lookup"><span data-stu-id="957fe-215">Receive the bot token</span></span>

<span data-ttu-id="957fe-216">トークンによる応答は、ボットが今日受け取る他の呼び出しアクティビティと同じスキーマを持つ呼び出しアクティビティを介して送信されます。</span><span class="sxs-lookup"><span data-stu-id="957fe-216">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="957fe-217">唯一の違いは、呼び出し名、**サインイン/tokenExchange、\*\*\*\*および値** フィールドです。</span><span class="sxs-lookup"><span data-stu-id="957fe-217">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="957fe-218">値 **フィールド** には **、Id**、トークンとトークン フィールドを取得する最初の要求の文字列、トークンを含む文字列値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="957fe-218">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="957fe-219">ユーザーが複数のアクティブなエンドポイントを持つ場合、特定の要求に対して複数の応答を受信する場合があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-219">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="957fe-220">トークンを使用して応答を重複排除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-220">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="957fe-221">C#アクティビティを処理するコードを作成する</span><span class="sxs-lookup"><span data-stu-id="957fe-221">C# code to handle the invoke activity</span></span>

```csharp
    protected override async Task<InvokeResponse> OnInvokeActivityAsync
    (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                try
                {
                    if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                    {
                        await OnTokenResponseEventAsync(turnContext, cancellationToken);
                        return new InvokeResponse() { Status = 200 };
                    }
                    else
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                    }
                }
                catch (InvokeResponseException e)
                {
                    return e.CreateInvokeResponse();
                }
            }
```

<span data-ttu-id="957fe-222">is `turnContext.activity.value` of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) と、ボットでさらに使用できるトークンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="957fe-222">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="957fe-223">パフォーマンス上の理由からトークンを保存し、更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-223">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="token-exchange-failure"></a><span data-ttu-id="957fe-224">トークン交換の失敗</span><span class="sxs-lookup"><span data-stu-id="957fe-224">Token exchange failure</span></span>

<span data-ttu-id="957fe-225">トークン交換に失敗した場合は、次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="957fe-225">In case of token exchange failure, use the following code:</span></span>

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

<span data-ttu-id="957fe-226">トークン交換が同意プロンプトのトリガーに失敗した場合のボットの動作を理解するには、次の手順を参照してください。</span><span class="sxs-lookup"><span data-stu-id="957fe-226">To understand what the bot does when the token exchange fails to trigger a consent prompt, see the following steps:</span></span>

>[!NOTE]
> <span data-ttu-id="957fe-227">トークン交換が失敗した場合にボットがアクションを実行する際に、ユーザー操作を実行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="957fe-227">No user action is required to be taken as the bot takes the actions when the token exchange fails.</span></span>

1. <span data-ttu-id="957fe-228">クライアントは、OAuth シナリオをトリガーするボットとの会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="957fe-228">The client starts a conversation with the bot triggering an OAuth scenario.</span></span>
2. <span data-ttu-id="957fe-229">ボットは OAuth カードをクライアントに返します。</span><span class="sxs-lookup"><span data-stu-id="957fe-229">The bot sends back an OAuth card to the client.</span></span>
3. <span data-ttu-id="957fe-230">クライアントは、OAuth カードをユーザーに表示する前に傍受し、プロパティが含まれているか確認 `TokenExchangeResource` します。</span><span class="sxs-lookup"><span data-stu-id="957fe-230">The client intercepts the OAuth card before displaying it to the user and checks if it contains a `TokenExchangeResource` property.</span></span>
4. <span data-ttu-id="957fe-231">プロパティが存在する場合、クライアントはボットに a `TokenExchangeInvokeRequest` を送信します。</span><span class="sxs-lookup"><span data-stu-id="957fe-231">If the property exists, the client sends a `TokenExchangeInvokeRequest` to the bot.</span></span> <span data-ttu-id="957fe-232">クライアントは、ユーザーの交換可能なトークンを持っている必要があります。これは Azure AD v2 トークンで、対象ユーザーはプロパティと同じである必要 `TokenExchangeResource.Uri` があります。</span><span class="sxs-lookup"><span data-stu-id="957fe-232">The client must have an exchangeable token for the user, which must be an Azure AD v2 token and whose audience must be the same as `TokenExchangeResource.Uri` property.</span></span> <span data-ttu-id="957fe-233">クライアントは、次のコードを使用してボットに呼び出しアクティビティを送信します。</span><span class="sxs-lookup"><span data-stu-id="957fe-233">The client sends an invoke activity to the bot with the following code:</span></span>

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. <span data-ttu-id="957fe-234">ボットは、クライアントを `TokenExchangeInvokeRequest` 処理し、 `TokenExchangeInvokeResponse` クライアントに戻します。</span><span class="sxs-lookup"><span data-stu-id="957fe-234">The bot processes the `TokenExchangeInvokeRequest` and returns a `TokenExchangeInvokeResponse` back to the client.</span></span> <span data-ttu-id="957fe-235">クライアントは、 を受信するまで待機する必要があります `TokenExchangeInvokeResponse` 。</span><span class="sxs-lookup"><span data-stu-id="957fe-235">The client must wait till it receives the `TokenExchangeInvokeResponse`.</span></span>

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. <span data-ttu-id="957fe-236">a を `TokenExchangeInvokeResponse` 持 `status` つ `200` 場合、クライアントは OAuth カードを表示しない。</span><span class="sxs-lookup"><span data-stu-id="957fe-236">If the `TokenExchangeInvokeResponse` has a `status` of `200`, then the client does not show the OAuth card.</span></span> <span data-ttu-id="957fe-237">通常の [フロー イメージを参照してください](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="957fe-237">See the [normal flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="957fe-238">その他の `status` 場合、または受信されていない場合、クライアントはユーザーに `TokenExchangeInvokeResponse` OAuth カードを表示します。</span><span class="sxs-lookup"><span data-stu-id="957fe-238">For any other `status` or if the `TokenExchangeInvokeResponse` is not received, then the client shows the OAuth card to the user.</span></span> <span data-ttu-id="957fe-239">フォールバック フロー [イメージを参照してください](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="957fe-239">See the [fallback flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="957fe-240">これにより、ユーザーの同意のようなエラーやアンメット依存関係が発生した場合に、SSO フローが通常の OAuthCard フローに戻ります。</span><span class="sxs-lookup"><span data-stu-id="957fe-240">This ensures that the SSO flow falls back to normal OAuthCard flow in case of any errors or unmet dependencies like user consent.</span></span>


### <a name="update-the-auth-sample"></a><span data-ttu-id="957fe-241">auth サンプルを更新する</span><span class="sxs-lookup"><span data-stu-id="957fe-241">Update the auth sample</span></span>

<span data-ttu-id="957fe-242">認証[Teams開き](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)、次の手順を実行して更新します。</span><span class="sxs-lookup"><span data-stu-id="957fe-242">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="957fe-243">次のコードを含めて、受信要求の重複排除を処理するために TeamsBot を更新します。</span><span class="sxs-lookup"><span data-stu-id="957fe-243">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

    ```csharp
        protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
        protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
    ```
  
2. <span data-ttu-id="957fe-244">[OAuth 接続を使用して Azure portal を更新する] で定義されている 、パスワード、および接続 `appsettings.json` `botId` [名を含める更新プログラム](#update-the-azure-portal-with-the-oauth-connection)。</span><span class="sxs-lookup"><span data-stu-id="957fe-244">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="957fe-245">マニフェストを更新し、有効 `token.botframework.com` なドメイン一覧に含まれています。</span><span class="sxs-lookup"><span data-stu-id="957fe-245">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="957fe-246">詳細については、「Teams[認証サンプル」を参照してください](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。</span><span class="sxs-lookup"><span data-stu-id="957fe-246">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="957fe-247">プロファイル イメージを使用してマニフェストを圧縮し、そのマニフェストをTeams。</span><span class="sxs-lookup"><span data-stu-id="957fe-247">Zip the manifest with the profile images and install it in Teams.</span></span>

## <a name="code-sample"></a><span data-ttu-id="957fe-248">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="957fe-248">Code sample</span></span>
|<span data-ttu-id="957fe-249">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="957fe-249">**Sample name**</span></span> | <span data-ttu-id="957fe-250">**説明**</span><span class="sxs-lookup"><span data-stu-id="957fe-250">**Description**</span></span> |<span data-ttu-id="957fe-251">**.NET**</span><span class="sxs-lookup"><span data-stu-id="957fe-251">**.NET**</span></span> | 
|----------------|-----------------|--------------|
|<span data-ttu-id="957fe-252">ボット フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="957fe-252">Bot framework SDK</span></span> | <span data-ttu-id="957fe-253">ボット フレームワーク SDK を使用するサンプル。</span><span class="sxs-lookup"><span data-stu-id="957fe-253">Sample for using the bot framework SDK.</span></span> |[<span data-ttu-id="957fe-254">View</span><span class="sxs-lookup"><span data-stu-id="957fe-254">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
