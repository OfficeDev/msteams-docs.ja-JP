---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者はサインイン カードまたは Azure Bot サービスを OAuth カードのサポートと一緒に使用できます。
keywords: トークン, ユーザー トークン, ボットの SSO サポート
ms.topic: conceptual
ms.openlocfilehash: 8537cf41cdd7218b9bf7618fccf0e1704ac6b815
ms.sourcegitcommit: 92fa912a51f295bb8a2dc1593a46ce103752dcdd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/21/2021
ms.locfileid: "49917586"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="996f7-105">ボットのシングル サインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="996f7-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="996f7-106">Azure Active Directory (AAD) のシングル サインオン認証では、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンをサイレント 更新します。</span><span class="sxs-lookup"><span data-stu-id="996f7-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="996f7-107">ユーザーがアプリの使用に同意した場合、別のデバイスでもう一度同意する必要はありません。また、自動的にサインインできます。</span><span class="sxs-lookup"><span data-stu-id="996f7-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="996f7-108">フローは[Microsoft Teams](../../../tabs/how-to/authentication/auth-aad-sso.md)タブ SSO サポートのフローと似ていますが、ボットがトークンを要求して[](#request-a-bot-token)応答を受信する方法のプロトコルが[異なっています](#receive-the-bot-token)。</span><span class="sxs-lookup"><span data-stu-id="996f7-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="996f7-109">OAuth 2.0 は、AAD や他の多くの ID プロバイダーで使用される認証と承認のオープン標準です。</span><span class="sxs-lookup"><span data-stu-id="996f7-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="996f7-110">OAuth 2.0 の基本的な理解は、Teams で認証を操作する場合の前提条件です。</span><span class="sxs-lookup"><span data-stu-id="996f7-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="996f7-111">実行時の Bot SSO</span><span class="sxs-lookup"><span data-stu-id="996f7-111">Bot SSO at runtime</span></span>

![実行時のボット SSO の図](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="996f7-113">認証トークンとボット アプリケーション トークンを取得するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="996f7-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="996f7-114">ボットは、プロパティを含む OAuthCard でメッセージを送信 `tokenExchangeResource` します。</span><span class="sxs-lookup"><span data-stu-id="996f7-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="996f7-115">ボット アプリケーションの認証トークンを取得するために Teams に指示します。</span><span class="sxs-lookup"><span data-stu-id="996f7-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="996f7-116">ユーザーは、すべてのアクティブなユーザー エンドポイントでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="996f7-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="996f7-117">ユーザーは一度に複数のアクティブなエンドポイントを持つ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="996f7-118">ボット トークンは、すべてのアクティブユーザー エンドポイントから受信されます。</span><span class="sxs-lookup"><span data-stu-id="996f7-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="996f7-119">SSO をサポートするには、アプリを個人用スコープでインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-119">The app must be installed in personal scope for SSO support.</span></span>

2. <span data-ttu-id="996f7-120">現在のユーザーがボット アプリケーションを初めて使用する場合は、次のいずれかの操作をユーザーに要求する要求プロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="996f7-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="996f7-121">必要に応じて同意を提供します。</span><span class="sxs-lookup"><span data-stu-id="996f7-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="996f7-122">2 要素認証などのステップ アップ認証を処理します。</span><span class="sxs-lookup"><span data-stu-id="996f7-122">Handle step-up authentication, such as two-factor authentication.</span></span>

3. <span data-ttu-id="996f7-123">Teams は、現在のユーザーの AAD エンドポイントからボット アプリケーション トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="996f7-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

4. <span data-ttu-id="996f7-124">AAD はボット アプリケーション トークンを Teams アプリケーションに送信します。</span><span class="sxs-lookup"><span data-stu-id="996f7-124">AAD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="996f7-125">Teams は、サインイン **/トークンExchange** という名前で、呼び出しアクティビティによって返される値オブジェクトの一部としてボットにトークンを送信します。</span><span class="sxs-lookup"><span data-stu-id="996f7-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
6. <span data-ttu-id="996f7-126">ボット アプリケーションで解析されたトークンは、ユーザーの電子メール アドレスなどの必要な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="996f7-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="996f7-127">SSO Teams ボットを開発する</span><span class="sxs-lookup"><span data-stu-id="996f7-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="996f7-128">SSO Teams ボットを開発するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="996f7-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="996f7-129">[AAD ポータルからアプリを登録します](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="996f7-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
2. <span data-ttu-id="996f7-130">[ボットの Teams アプリケーション マニフェストを更新します](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="996f7-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
3. <span data-ttu-id="996f7-131">[ボット トークンを要求および受信するコードを追加します](#add-the-code-to-request-and-receive-a-bot-token)。</span><span class="sxs-lookup"><span data-stu-id="996f7-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="996f7-132">AAD ポータルを通じてアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="996f7-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="996f7-133">AAD ポータルを通じてアプリを登録する手順は、タブ SSO フロー [に似ています](../../../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="996f7-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="996f7-134">アプリを登録するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="996f7-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="996f7-135">Azure Active Directory アプリ登録ポータルに [新しいアプリケーションを登録](https://go.microsoft.com/fwlink/?linkid=2083908) します。</span><span class="sxs-lookup"><span data-stu-id="996f7-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="996f7-136">[新規 **登録] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="996f7-136">Select **New Registration**.</span></span> <span data-ttu-id="996f7-137">[ **アプリケーションの登録] ページ** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="996f7-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="996f7-138">[アプリケーション **の登録] ページで** 、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="996f7-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="996f7-139">アプリの **名前** を入力します。</span><span class="sxs-lookup"><span data-stu-id="996f7-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="996f7-140">サポートされている **アカウントの種類を選択し、** 単一テナントアカウントの種類またはマルチテナント アカウントの種類を選択します。</span><span class="sxs-lookup"><span data-stu-id="996f7-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="996f7-141">AAD アプリが Teams で認証要求を行っているのと同じテナントに登録されている場合、ユーザーは同意を求めではなく、アクセス トークンを直接付与されます。</span><span class="sxs-lookup"><span data-stu-id="996f7-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="996f7-142">ただし、AAD アプリが別のテナントに登録されている場合、ユーザーはアクセス許可に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="996f7-143">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="996f7-143">Choose **Register**.</span></span>
4. <span data-ttu-id="996f7-144">[概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。</span><span class="sxs-lookup"><span data-stu-id="996f7-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="996f7-145">後で Teams アプリケーション マニフェストを更新するときに必要になります。</span><span class="sxs-lookup"><span data-stu-id="996f7-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="996f7-146">[**管理**] で [**API の公開**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="996f7-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="996f7-147">スタンドアロン ボットを作成する場合は、アプリケーション ID URI を次のように入力します `api://botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="996f7-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="996f7-148">ここで **、YourBotId** は AAD アプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="996f7-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="996f7-149">ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次のように入力します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="996f7-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="996f7-150">アプリケーションが AAD エンドポイントに必要とするアクセス許可と、必要に応じて Microsoft Graph に必要なアクセス許可を選択します。</span><span class="sxs-lookup"><span data-stu-id="996f7-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="996f7-151">Teams[のデスクトップ、Web、](/azure/active-directory/develop/v2-permissions-and-consent)モバイル アプリケーションのアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="996f7-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="996f7-152">**[スコープの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="996f7-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="996f7-153">開くパネルで、スコープ名として入力してクライアント `access_as_user` アプリを **追加します**。</span><span class="sxs-lookup"><span data-stu-id="996f7-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="996f7-154">クライアント アプリのaccess_as_user "管理者とユーザー" のスコープです。</span><span class="sxs-lookup"><span data-stu-id="996f7-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="996f7-155">次の重要な制限に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="996f7-156">ユーザー レベルの Microsoft Graph API のアクセス許可 (メール、プロファイル、offline_access、OpenId など) だけがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="996f7-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="996f7-157">その他の Microsoft Graph スコープにアクセスする必要がある場合 (または、推奨される回避策 `User.Read` `Mail.Read` [を参照してください](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes))。</span><span class="sxs-lookup"><span data-stu-id="996f7-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes).</span></span>
    > * <span data-ttu-id="996f7-158">アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="996f7-159">現在、アプリごとに複数のドメインはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="996f7-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="996f7-160">ドメインを使用するアプリケーションは、一般的であり、セキュリティ上のリスクが `azurewebsites.net` 高い可能性からサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="996f7-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="996f7-161">OAuth 接続を使用して Azure Portal を更新する</span><span class="sxs-lookup"><span data-stu-id="996f7-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="996f7-162">OAuth 接続を使用して Azure Portal を更新するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="996f7-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="996f7-163">Azure Portal で、ボット チャネル登録 **に移動します**。</span><span class="sxs-lookup"><span data-stu-id="996f7-163">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="996f7-164">API の **アクセス許可に移動します**。</span><span class="sxs-lookup"><span data-stu-id="996f7-164">Go to **API Permissions**.</span></span> <span data-ttu-id="996f7-165">[Microsoft Graph **委任されたアクセス** 許可のアクセス許可の追加] を選択し、Microsoft Graph API から次のアクセス  >    >  許可を追加します。</span><span class="sxs-lookup"><span data-stu-id="996f7-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="996f7-166">User.Read (既定で有効)</span><span class="sxs-lookup"><span data-stu-id="996f7-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="996f7-167">メール</span><span class="sxs-lookup"><span data-stu-id="996f7-167">email</span></span>
    * <span data-ttu-id="996f7-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="996f7-168">offline_access</span></span>
    * <span data-ttu-id="996f7-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="996f7-169">OpenId</span></span>
    * <span data-ttu-id="996f7-170">プロフィール</span><span class="sxs-lookup"><span data-stu-id="996f7-170">profile</span></span>

3. <span data-ttu-id="996f7-171">左側 **のウィンドウで [** 設定] を選択し、[OAuth 接続 **の設定]** セクションで [ **設定の追加] を選択** します。</span><span class="sxs-lookup"><span data-stu-id="996f7-171">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![SSOBotHandle2 ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

4. <span data-ttu-id="996f7-173">[新しい接続設定] フォームを完了するには **、次の手順を実行** します。</span><span class="sxs-lookup"><span data-stu-id="996f7-173">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="996f7-174">**AAD アプリケーション** では暗黙的な許可が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-174">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="996f7-175">[新しい **接続設定** ] **ページに名前を入力** します。</span><span class="sxs-lookup"><span data-stu-id="996f7-175">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="996f7-176">これは、実行時に Bot SSO の手順 *5* でボット サービス コードの設定内で参照される [名前です](#bot-sso-at-runtime)。</span><span class="sxs-lookup"><span data-stu-id="996f7-176">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="996f7-177">[サービス **プロバイダー] ドロップダウンから\*\*\*\*、Azure Active Directory v2 を選択します**。</span><span class="sxs-lookup"><span data-stu-id="996f7-177">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="996f7-178">AAD アプリケーションのクライアント **ID** や **クライアント** シークレットなどのクライアント資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="996f7-178">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="996f7-179">トークン交換 **URL の場合は**、「ボットの Teams アプリケーション マニフェストを更新 [する」で定義されているスコープ値を使用します](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="996f7-179">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="996f7-180">Token Exchange URL は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示します。</span><span class="sxs-lookup"><span data-stu-id="996f7-180">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="996f7-181">[テナント **ID] ボックスに** 「共通」と *入力します*。</span><span class="sxs-lookup"><span data-stu-id="996f7-181">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="996f7-182">AAD **アプリケーションのダウンストリーム** API へのアクセス許可を指定するときに構成されたスコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="996f7-182">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="996f7-183">クライアント ID とクライアント シークレットが提供された場合、トークン ストアは、定義されたアクセス許可を持つグラフ トークンのトークンを交換します。</span><span class="sxs-lookup"><span data-stu-id="996f7-183">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="996f7-184">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="996f7-184">Select **Save**.</span></span>

    ![VuSSOBotConnection 設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="996f7-186">ボットの Teams アプリケーション マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="996f7-186">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="996f7-187">アプリケーションにスタンドアロン ボットが含まれている場合は、次のコードを使用して新しいプロパティを Teams アプリケーション マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="996f7-187">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="996f7-188">アプリケーションにボットとタブが含まれている場合は、次のコードを使用して新しいプロパティを Teams アプリケーション マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="996f7-188">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="996f7-189">**webApplicationInfo** は、次の要素の親です。</span><span class="sxs-lookup"><span data-stu-id="996f7-189">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="996f7-190">**id** - アプリケーションのクライアント ID。</span><span class="sxs-lookup"><span data-stu-id="996f7-190">**id** - The client ID of the application.</span></span> <span data-ttu-id="996f7-191">これは、アプリケーションを AAD に登録する一部として取得したアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="996f7-191">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="996f7-192">**resource** - アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="996f7-192">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="996f7-193">これは `api://` `scope` [、AAD](#register-your-app-through-the-aad-portal)ポータルからアプリを登録するときに登録したプロトコルを含め、同じ URI です。</span><span class="sxs-lookup"><span data-stu-id="996f7-193">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="996f7-194">リソースにパスを `access_as_user` 含めずにしてください。</span><span class="sxs-lookup"><span data-stu-id="996f7-194">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="996f7-195">この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用されるドメインとサブドメインと一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-195">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="996f7-196">ボット トークンを要求して受信するコードを追加する</span><span class="sxs-lookup"><span data-stu-id="996f7-196">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="996f7-197">ボット トークンを要求する</span><span class="sxs-lookup"><span data-stu-id="996f7-197">Request a bot token</span></span>

<span data-ttu-id="996f7-198">トークンを取得する要求は、既存のメッセージ スキーマを使用した通常の POST メッセージ要求です。</span><span class="sxs-lookup"><span data-stu-id="996f7-198">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="996f7-199">OAuthCard の添付ファイルに含まれています。</span><span class="sxs-lookup"><span data-stu-id="996f7-199">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="996f7-200">OAuthCard クラスのスキーマは Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義され、サインイン カードに似ています。</span><span class="sxs-lookup"><span data-stu-id="996f7-200">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="996f7-201">カードにプロパティが設定されている場合、Teams は、この要求をサイレント トークン取得 `TokenExchangeResource` として処理します。</span><span class="sxs-lookup"><span data-stu-id="996f7-201">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="996f7-202">Teams チャネルでは、トークン要求を一意に識別するプロパティ `Id` だけが使用されます。</span><span class="sxs-lookup"><span data-stu-id="996f7-202">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="996f7-203">Microsoft Bot Framework または SSO `OAuthPrompt` `MultiProviderAuthDialog` 認証がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="996f7-203">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="996f7-204">ユーザーがアプリケーションを初めて使用し、ユーザーの同意が必要な場合は、次のダイアログ ボックスが表示され、同意エクスペリエンスが続行されます。</span><span class="sxs-lookup"><span data-stu-id="996f7-204">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

![[同意] ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="996f7-206">ユーザーが [続行] を選択 **すると**、次のイベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="996f7-206">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="996f7-207">ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリーム内の OAuth カード ボタンからのサインイン フローと同様にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="996f7-207">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="996f7-208">開発者は、ユーザーの同意を必要とするアクセス許可を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-208">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="996f7-209">この方法は、それ以上のアクセス許可を持つトークンが必要な場合に推奨されます `openId` 。</span><span class="sxs-lookup"><span data-stu-id="996f7-209">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="996f7-210">たとえば、グラフ リソースのトークンを交換する場合です。</span><span class="sxs-lookup"><span data-stu-id="996f7-210">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="996f7-211">ボットが OAuth カードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットに対してユーザーの同意が必要です。</span><span class="sxs-lookup"><span data-stu-id="996f7-211">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="996f7-212">このトークンは、基本認証やユーザーの電子メール アドレスの取得に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="996f7-212">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="996f7-213">サインイン ボタンのない C# トークン要求</span><span class="sxs-lookup"><span data-stu-id="996f7-213">C# token request without a sign-in button</span></span>

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

#### <a name="receive-the-bot-token"></a><span data-ttu-id="996f7-214">ボット トークンを受信する</span><span class="sxs-lookup"><span data-stu-id="996f7-214">Receive the bot token</span></span>

<span data-ttu-id="996f7-215">トークンを含む応答は、ボットが現在受け取る他の呼び出しアクティビティと同じスキーマを持つ呼び出しアクティビティを通じて送信されます。</span><span class="sxs-lookup"><span data-stu-id="996f7-215">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="996f7-216">唯一の違いは、呼び出し名、**サインイン/トークンExchange、\*\*\*\*および値** フィールドです。</span><span class="sxs-lookup"><span data-stu-id="996f7-216">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="996f7-217">値 **フィールド** には **、Id、** トークンとトークン フィールドを取得する最初の要求の文字列、トークンを含む文字列値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="996f7-217">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="996f7-218">ユーザーが複数のアクティブなエンドポイントを持つ場合、特定の要求に対して複数の応答を受け取る場合があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-218">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="996f7-219">トークンを使用して応答を重複排除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-219">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="996f7-220">呼び出しアクティビティを処理する C# コード</span><span class="sxs-lookup"><span data-stu-id="996f7-220">C# code to handle the invoke activity</span></span>

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

<span data-ttu-id="996f7-221">`turnContext.activity.value` [TokenExchangeInvokeRequest 型](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)であり、ボットでさらに使用できるトークンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="996f7-221">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="996f7-222">パフォーマンス上の理由からトークンを保存し、更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="996f7-222">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="update-the-auth-sample"></a><span data-ttu-id="996f7-223">認証サンプルを更新する</span><span class="sxs-lookup"><span data-stu-id="996f7-223">Update the auth sample</span></span>

<span data-ttu-id="996f7-224">[Teams 認証サンプルを開](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)き、次の手順を実行して更新します。</span><span class="sxs-lookup"><span data-stu-id="996f7-224">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="996f7-225">次のコードを含めて、受信要求の重複を処理するために TeamsBot を更新します。</span><span class="sxs-lookup"><span data-stu-id="996f7-225">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

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
  
2. <span data-ttu-id="996f7-226">`appsettings.json`「OAuth 接続を使用して Azure portal を更新する」で定義されている接続名 、パスワード `botId` [を含める更新](#update-the-azure-portal-with-the-oauth-connection)。</span><span class="sxs-lookup"><span data-stu-id="996f7-226">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="996f7-227">マニフェストを更新し、有効 `token.botframework.com` なドメインの一覧に含まれています。</span><span class="sxs-lookup"><span data-stu-id="996f7-227">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="996f7-228">詳細については [、Teams 認証サンプルを参照してください](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。</span><span class="sxs-lookup"><span data-stu-id="996f7-228">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="996f7-229">マニフェストをプロファイル イメージと一緒に Zip し、Teams にインストールします。</span><span class="sxs-lookup"><span data-stu-id="996f7-229">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="996f7-230">その他のコード サンプル</span><span class="sxs-lookup"><span data-stu-id="996f7-230">Additional code samples</span></span>

* <span data-ttu-id="996f7-231">[Bot Framework SDK を使用した C# サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。</span><span class="sxs-lookup"><span data-stu-id="996f7-231">[C# sample using the Bot Framework SDK](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).</span></span>

* <span data-ttu-id="996f7-232">[Bot Framework SDK を使用してトークン要求](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)を重複排除する C# サンプル。</span><span class="sxs-lookup"><span data-stu-id="996f7-232">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* <span data-ttu-id="996f7-233">[Bot Framework SDK トークン ストアを使用しない C# サンプル](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)。</span><span class="sxs-lookup"><span data-stu-id="996f7-233">[C# sample without using the Bot Framework SDK token store](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw).</span></span>
