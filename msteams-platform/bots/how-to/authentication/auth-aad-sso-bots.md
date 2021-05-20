---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者は、OAuth カードのサポートを使用して、サインイン カードまたは Azure ボット サービスを使用できます。
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
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="9764f-105">ボットのシングル サインオン (SSO) サポート</span><span class="sxs-lookup"><span data-stu-id="9764f-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="9764f-106">Azure Active Directory (AAD) のシングル サインオン認証では、認証トークンをサイレントに更新することで、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑えることができます。</span><span class="sxs-lookup"><span data-stu-id="9764f-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="9764f-107">ユーザーがアプリの使用に同意すると、別のデバイスでもう一度同意する必要はありません。自動的にサインインできます。</span><span class="sxs-lookup"><span data-stu-id="9764f-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="9764f-108">フローは[[Microsoft Teamsタブ SSO サポート](../../../tabs/how-to/authentication/auth-aad-sso.md)と似ていますが、違いは、ボットが[トークンを要求](#request-a-bot-token)して応答を[受け取る](#receive-the-bot-token)方法のプロトコルにあります。</span><span class="sxs-lookup"><span data-stu-id="9764f-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="9764f-109">OAuth 2.0 は、AAD および他の多くの ID プロバイダーによって使用される認証と承認のためのオープンスタンダードです。</span><span class="sxs-lookup"><span data-stu-id="9764f-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="9764f-110">OAuth 2.0 の基本知識は、Teamsで認証を操作するための前提条件です。</span><span class="sxs-lookup"><span data-stu-id="9764f-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="9764f-111">実行時のボット SSO</span><span class="sxs-lookup"><span data-stu-id="9764f-111">Bot SSO at runtime</span></span>

![実行時のボット SSO 図](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="9764f-113">認証およびボット アプリケーション トークンを取得するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="9764f-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="9764f-114">ボットが、`tokenExchangeResource`プロパティを含む OAuthCard でメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="9764f-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="9764f-115">Teamsに対して、ボット アプリケーションの認証トークンを取得するように指示します。</span><span class="sxs-lookup"><span data-stu-id="9764f-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="9764f-116">ユーザーは、アクティブなすべてのユーザー エンドポイントでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="9764f-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="9764f-117">ユーザーは、一度に複数のアクティブなエンドポイントを持つ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="9764f-118">ボット トークンは、すべてのアクティブなユーザーのエンドポイントから受信されます。</span><span class="sxs-lookup"><span data-stu-id="9764f-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="9764f-119">SSO をサポートするには、アプリを個人用のスコープにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-119">The app must be installed in personal scope for SSO support.</span></span>

1. <span data-ttu-id="9764f-120">現在のユーザーが初めてボット アプリケーションを使用している場合は、次のいずれかの操作を要求する要求プロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9764f-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="9764f-121">必要に応じて、同意を提供します。</span><span class="sxs-lookup"><span data-stu-id="9764f-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="9764f-122">2 要素認証などのステップ アップ認証を処理します。</span><span class="sxs-lookup"><span data-stu-id="9764f-122">Handle step-up authentication, such as two-factor authentication.</span></span>

1. <span data-ttu-id="9764f-123">Teamsは、現在のユーザーの AAD エンドポイントからボット アプリケーション トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="9764f-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

1. <span data-ttu-id="9764f-124">AAD は、ボット アプリケーション トークンをTeams アプリケーションに送信します。</span><span class="sxs-lookup"><span data-stu-id="9764f-124">AAD sends the bot application token to the Teams application.</span></span>

1. <span data-ttu-id="9764f-125">Teamsは、名前 **サインイン/tokenExchange** を使用して、invoke アクティビティによって返される値オブジェクトの一部としてトークンをボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="9764f-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
1. <span data-ttu-id="9764f-126">ボット アプリケーションの解析されたトークンは、ユーザーのメール アドレスなど、必要な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="9764f-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="9764f-127">SSO Teamsボットの開発</span><span class="sxs-lookup"><span data-stu-id="9764f-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="9764f-128">SSO Teams ボットを開発するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="9764f-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="9764f-129">[AAD ポータル を使用してアプリを登録する](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="9764f-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
1. <span data-ttu-id="9764f-130">[Teamsアプリケーション マニフェストをボット用に更新します](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="9764f-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
1. <span data-ttu-id="9764f-131">[ボット トークンを要求して受け取るコードを追加](#add-the-code-to-request-and-receive-a-bot-token)します。</span><span class="sxs-lookup"><span data-stu-id="9764f-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="9764f-132">AAD ポータルを使用してアプリを登録する</span><span class="sxs-lookup"><span data-stu-id="9764f-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="9764f-133">AAD ポータルを通じてアプリを登録する手順は、 [SSO フロー タブ](../../../tabs/how-to/authentication/auth-aad-sso.md)に似ています。</span><span class="sxs-lookup"><span data-stu-id="9764f-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="9764f-134">アプリを登録するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="9764f-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="9764f-135">Azure Active Directory – アプリ登録ポータルで新しい[アプリケーションを登録します](https://go.microsoft.com/fwlink/?linkid=2083908)。</span><span class="sxs-lookup"><span data-stu-id="9764f-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="9764f-136">[ **新規登録 ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-136">Select **New Registration**.</span></span> <span data-ttu-id="9764f-137">[ **アプリケーションの登録]** ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9764f-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="9764f-138">[ **アプリケーションの登録]** ページで、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="9764f-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="9764f-139">アプリの **[名前] を** 入力します。</span><span class="sxs-lookup"><span data-stu-id="9764f-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="9764f-140">[ **サポートされているアカウントの種類**] を選択し、[シングル テナント] または [マルチテナント アカウントの種類] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="9764f-141">AAD アプリがTeamsで認証要求を行っているテナントと同じテナントに登録されている場合、ユーザーは同意を求めらなくて、すぐにアクセス トークンが付与されます。</span><span class="sxs-lookup"><span data-stu-id="9764f-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="9764f-142">ただし、AAD アプリが別のテナントに登録されている場合は、ユーザーがアクセス許可に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="9764f-143">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-143">Choose **Register**.</span></span>
4. <span data-ttu-id="9764f-144">概要ページで、 **アプリケーション (クライアント) ID** をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="9764f-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="9764f-145">後でTeamsアプリケーション マニフェストを更新するときに必要になります。</span><span class="sxs-lookup"><span data-stu-id="9764f-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="9764f-146">[**管理**] で [**API の公開**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="9764f-147">スタンドアロン ボットを構築する場合は、アプリケーション ID URI を `api://botid-{YourBotId}` として入力します。</span><span class="sxs-lookup"><span data-stu-id="9764f-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="9764f-148">ここで **YourBotId** は AAD アプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="9764f-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="9764f-149">ボットとタブを使用してアプリをビルドする場合は、アプリケーション ID URI を `api://fully-qualified-domain-name.com/botid-{YourBotId}` として入力します。</span><span class="sxs-lookup"><span data-stu-id="9764f-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="9764f-150">アプリケーションが AAD エンドポイントに必要なアクセス許可を選択し、必要に応じて Microsoft Graph用に選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="9764f-151">デスクトップ、Web、モバイルアプリケーションTeamsの[アクセス許可を付与](/azure/active-directory/develop/v2-permissions-and-consent)します。</span><span class="sxs-lookup"><span data-stu-id="9764f-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="9764f-152">**[スコープの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="9764f-153">開いたパネルで、スコープ名 と入力してクライアント アプリケーション `access_as_user` を追加します。</span><span class="sxs-lookup"><span data-stu-id="9764f-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="9764f-154">クライアント アプリを追加するために使用される "access_as_user" スコープは、"管理者とユーザー" 用です。</span><span class="sxs-lookup"><span data-stu-id="9764f-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="9764f-155">次の重要な制限事項に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="9764f-156">電子メール、プロファイル、offline_access、OpenId などのユーザー レベルの Microsoft Graph API のアクセス許可のみがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="9764f-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="9764f-157">または などの他の Microsoft Graph スコープにアクセスする必要がある場合 `User.Read` `Mail.Read` は、「[回避策](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9764f-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).</span></span>
    > * <span data-ttu-id="9764f-158">アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="9764f-159">現在、アプリごとに複数のドメインがサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="9764f-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="9764f-160">ドメインを使用するアプリケーション `azurewebsites.net` は、一般的であり、セキュリティ上のリスクがあるため、サポートされません。</span><span class="sxs-lookup"><span data-stu-id="9764f-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="9764f-161">OAuth 接続を使用して Azure ポータルを更新する</span><span class="sxs-lookup"><span data-stu-id="9764f-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="9764f-162">OAuth 接続で Azure ポータルを更新するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="9764f-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="9764f-163">Azure ポータルで、[ **アプリの登録**] に移動します。</span><span class="sxs-lookup"><span data-stu-id="9764f-163">In the Azure Portal, navigate to **App registrations**.</span></span>

2. <span data-ttu-id="9764f-164">API **の権限** に移動します。</span><span class="sxs-lookup"><span data-stu-id="9764f-164">Go to **API Permissions**.</span></span> <span data-ttu-id="9764f-165">[Microsoft   >  **Graph**  >  **委任されたアクセス許可** を追加する] を選択し、Microsoft Graph API から次のアクセス許可を追加します。</span><span class="sxs-lookup"><span data-stu-id="9764f-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="9764f-166">ユーザー.読み取り(デフォルトで有効)</span><span class="sxs-lookup"><span data-stu-id="9764f-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="9764f-167">メール</span><span class="sxs-lookup"><span data-stu-id="9764f-167">email</span></span>
    * <span data-ttu-id="9764f-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="9764f-168">offline_access</span></span>
    * <span data-ttu-id="9764f-169">オープンID</span><span class="sxs-lookup"><span data-stu-id="9764f-169">OpenId</span></span>
    * <span data-ttu-id="9764f-170">profile</span><span class="sxs-lookup"><span data-stu-id="9764f-170">profile</span></span>

3. <span data-ttu-id="9764f-171">Azure ポータルで、[ボット **チャネルの登録**] に移動します。</span><span class="sxs-lookup"><span data-stu-id="9764f-171">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

4. <span data-ttu-id="9764f-172">左側のペインで **設定** を選択し **、[OAuth 接続設定** セクションの下にある **[設定の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-172">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. <span data-ttu-id="9764f-174">次の手順を実行して、 **新しい接続設定** フォームを完成させます。</span><span class="sxs-lookup"><span data-stu-id="9764f-174">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="9764f-175">**AAD アプリケーションでは、暗黙的な許可** が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-175">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="9764f-176">**[新しい接続設定]** ページに **[名前**] を入力します。</span><span class="sxs-lookup"><span data-stu-id="9764f-176">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="9764f-177">これは、実行時に Bot [SSO](#bot-sso-at-runtime)の *ステップ 5* でボット サービス コードの設定の内部で参照される名前です。</span><span class="sxs-lookup"><span data-stu-id="9764f-177">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="9764f-178">[**サービス プロバイダ**] ドロップダウンから **、[v2 Azure Active Directory]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-178">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="9764f-179">AAD アプリケーションのクライアント ID や **クライアント シークレット** などの **クライアント** 資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="9764f-179">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="9764f-180">[**トークン Exchangeの URL]** には [、「Teams アプリケーション マニフェストをボットに更新する](#update-your-teams-application-manifest-for-your-bot)」で定義されているスコープ値を使用します。</span><span class="sxs-lookup"><span data-stu-id="9764f-180">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="9764f-181">トークン Exchange URL は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示します。</span><span class="sxs-lookup"><span data-stu-id="9764f-181">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="9764f-182">[ **テナント ID]** ボックスに「 *共通*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="9764f-182">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="9764f-183">AAD アプリケーションのダウンストリーム API へのアクセス許可を指定するときに構成されたすべての **スコープ** を追加します。</span><span class="sxs-lookup"><span data-stu-id="9764f-183">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="9764f-184">クライアント ID とクライアント シークレットが提供されている場合、トークン ストアは、定義されたアクセス許可を持つグラフ トークンのトークンを交換します。</span><span class="sxs-lookup"><span data-stu-id="9764f-184">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="9764f-185">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="9764f-185">Select **Save**.</span></span>

    ![設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="9764f-187">ボットのTeams アプリケーション マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="9764f-187">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="9764f-188">アプリケーションにスタンドアロン ボットが含まれている場合は、次のコードを使用して、Teams アプリケーション マニフェストに新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="9764f-188">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="9764f-189">アプリケーションにボットとタブが含まれている場合は、次のコードを使用して、Teamsアプリケーション マニフェストに新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="9764f-189">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="9764f-190">**は** 、次の要素の親です。</span><span class="sxs-lookup"><span data-stu-id="9764f-190">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="9764f-191">**id** - アプリケーションのクライアント ID。</span><span class="sxs-lookup"><span data-stu-id="9764f-191">**id** - The client ID of the application.</span></span> <span data-ttu-id="9764f-192">これは、AAD にアプリケーションを登録する際に取得したアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="9764f-192">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="9764f-193">**resource** - アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="9764f-193">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="9764f-194">これは `api://` `scope` [、AAD ポータルを使用してアプリを登録](#register-your-app-through-the-aad-portal)する で作成したときに登録したプロトコルを含む、同じ URI です。</span><span class="sxs-lookup"><span data-stu-id="9764f-194">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="9764f-195">リソースにパスを含める必要はありません `access_as_user` 。</span><span class="sxs-lookup"><span data-stu-id="9764f-195">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="9764f-196">この URI のドメイン部分は、Teamsアプリケーション マニフェストの URL で使用されるドメインとサブドメインと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-196">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="9764f-197">ボット トークンを要求して受け取るコードを追加する</span><span class="sxs-lookup"><span data-stu-id="9764f-197">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="9764f-198">ボット トークンのリクエスト</span><span class="sxs-lookup"><span data-stu-id="9764f-198">Request a bot token</span></span>

<span data-ttu-id="9764f-199">トークンを取得する要求は、既存のメッセージ スキーマを使用する通常の POST メッセージ要求です。</span><span class="sxs-lookup"><span data-stu-id="9764f-199">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="9764f-200">OAuthCard の添付ファイルに含まれています。</span><span class="sxs-lookup"><span data-stu-id="9764f-200">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="9764f-201">OAuthCard クラスのスキーマは [、Microsoft Bot スキーマ 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義されており、サインイン カードに似ています。</span><span class="sxs-lookup"><span data-stu-id="9764f-201">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="9764f-202">Teamsは `TokenExchangeResource` 、プロパティがカードに設定されている場合、この要求をサイレント トークン取得として扱います。</span><span class="sxs-lookup"><span data-stu-id="9764f-202">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="9764f-203">Teams チャネルでは、 `Id` トークン要求を一意に識別するプロパティのみが受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="9764f-203">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="9764f-204">Microsoft Bot Framework `OAuthPrompt` または は `MultiProviderAuthDialog` 、SSO 認証でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9764f-204">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="9764f-205">ユーザーが初めてアプリケーションを使用していて、ユーザーの同意が必要な場合は、次のダイアログ ボックスが同意の操作を続行するように表示されます。</span><span class="sxs-lookup"><span data-stu-id="9764f-205">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

![同意ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="9764f-207">ユーザーが **[続行する]** を選択すると、次のイベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="9764f-207">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="9764f-208">ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリームの OAuth カード ボタンからのサインイン フローと同様にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="9764f-208">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="9764f-209">開発者は、ユーザーの同意が必要なアクセス許可を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-209">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="9764f-210">この方法は、 以外のアクセス許可を持つトークンが必要な場合にお勧めします `openId` 。</span><span class="sxs-lookup"><span data-stu-id="9764f-210">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="9764f-211">たとえば、グラフ リソースにトークンを交換する場合です。</span><span class="sxs-lookup"><span data-stu-id="9764f-211">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="9764f-212">ボットが OAuth カードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットにユーザーの同意が必要です。</span><span class="sxs-lookup"><span data-stu-id="9764f-212">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="9764f-213">このトークンは、基本認証やユーザーの電子メール アドレスの取得に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9764f-213">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="9764f-214">サインイン ボタンなしの C# トークン要求</span><span class="sxs-lookup"><span data-stu-id="9764f-214">C# token request without a sign-in button</span></span>

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

#### <a name="receive-the-bot-token"></a><span data-ttu-id="9764f-215">ボット トークンを受け取る</span><span class="sxs-lookup"><span data-stu-id="9764f-215">Receive the bot token</span></span>

<span data-ttu-id="9764f-216">トークンを含む応答は、今日ボットが受信する他の呼び出しアクティビティと同じスキーマを持つ invoke アクティビティを通じて送信されます。</span><span class="sxs-lookup"><span data-stu-id="9764f-216">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="9764f-217">唯一の違いは、呼び出し名、 **サインイン/トークン交換** 、および **値** フィールドです。</span><span class="sxs-lookup"><span data-stu-id="9764f-217">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="9764f-218">**値** フィールドには、 **Id** トークンを取得するための最初の要求の文字列と **トークン** フィールドが含まれます。</span><span class="sxs-lookup"><span data-stu-id="9764f-218">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="9764f-219">ユーザーが複数のアクティブなエンドポイントを持っている場合、特定の要求に対して複数の応答を受け取る場合があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-219">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="9764f-220">トークンを使用して応答を重複除去する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-220">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="9764f-221">呼び出しアクティビティを処理する C# コード</span><span class="sxs-lookup"><span data-stu-id="9764f-221">C# code to handle the invoke activity</span></span>

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

<span data-ttu-id="9764f-222">`turnContext.activity.value`型は[TokenExchangeInvokeRequest であり](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)、ボットでさらに使用できるトークンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9764f-222">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="9764f-223">パフォーマンス上の理由からトークンを保存し、更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9764f-223">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="token-exchange-failure"></a><span data-ttu-id="9764f-224">トークン交換の失敗</span><span class="sxs-lookup"><span data-stu-id="9764f-224">Token exchange failure</span></span>

<span data-ttu-id="9764f-225">トークン交換に失敗した場合は、次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="9764f-225">In case of token exchange failure, use the following code:</span></span>

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

<span data-ttu-id="9764f-226">トークン交換が同意プロンプトをトリガーできなかった場合にボットが何をするのかを理解するには、次の手順を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9764f-226">To understand what the bot does when the token exchange fails to trigger a consent prompt, see the following steps:</span></span>

>[!NOTE]
> <span data-ttu-id="9764f-227">トークン交換が失敗したときにボットがアクションを実行するので、ユーザーの操作は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="9764f-227">No user action is required to be taken as the bot takes the actions when the token exchange fails.</span></span>

1. <span data-ttu-id="9764f-228">クライアントは、OAuth シナリオをトリガーするボットとの会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="9764f-228">The client starts a conversation with the bot triggering an OAuth scenario.</span></span>
2. <span data-ttu-id="9764f-229">ボットは OAuth カードをクライアントに返送します。</span><span class="sxs-lookup"><span data-stu-id="9764f-229">The bot sends back an OAuth card to the client.</span></span>
3. <span data-ttu-id="9764f-230">クライアントは、OAuth カードをユーザーに表示する前にインターセプトし、プロパティが含まれているかどうかを確認 `TokenExchangeResource` します。</span><span class="sxs-lookup"><span data-stu-id="9764f-230">The client intercepts the OAuth card before displaying it to the user and checks if it contains a `TokenExchangeResource` property.</span></span>
4. <span data-ttu-id="9764f-231">プロパティが存在する場合、クライアントは `TokenExchangeInvokeRequest` ボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="9764f-231">If the property exists, the client sends a `TokenExchangeInvokeRequest` to the bot.</span></span> <span data-ttu-id="9764f-232">クライアントは、Azure AD v2 トークンで、対象ユーザーがプロパティと同じである必要がある、ユーザーに交換可能なトークンを持っている必要があります `TokenExchangeResource.Uri` 。</span><span class="sxs-lookup"><span data-stu-id="9764f-232">The client must have an exchangeable token for the user, which must be an Azure AD v2 token and whose audience must be the same as `TokenExchangeResource.Uri` property.</span></span> <span data-ttu-id="9764f-233">クライアントは、次のコードを使用して、呼び出しアクティビティをボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="9764f-233">The client sends an invoke activity to the bot with the following code:</span></span>

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

5. <span data-ttu-id="9764f-234">ボットは を処理 `TokenExchangeInvokeRequest` し、 `TokenExchangeInvokeResponse` クライアントに戻ります。</span><span class="sxs-lookup"><span data-stu-id="9764f-234">The bot processes the `TokenExchangeInvokeRequest` and returns a `TokenExchangeInvokeResponse` back to the client.</span></span> <span data-ttu-id="9764f-235">クライアントは、 を受け取るまで待つ必要があります `TokenExchangeInvokeResponse` 。</span><span class="sxs-lookup"><span data-stu-id="9764f-235">The client must wait till it receives the `TokenExchangeInvokeResponse`.</span></span>

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

6. <span data-ttu-id="9764f-236">が `TokenExchangeInvokeResponse` が を持つ `status` `200` 場合、クライアントは OAuth カードを表示しません。</span><span class="sxs-lookup"><span data-stu-id="9764f-236">If the `TokenExchangeInvokeResponse` has a `status` of `200`, then the client does not show the OAuth card.</span></span> <span data-ttu-id="9764f-237">通常の [フロー画像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9764f-237">See the [normal flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="9764f-238">その他の場合 `status` 、または `TokenExchangeInvokeResponse` が受信されていない場合、クライアントは OAuth カードをユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="9764f-238">For any other `status` or if the `TokenExchangeInvokeResponse` is not received, then the client shows the OAuth card to the user.</span></span> <span data-ttu-id="9764f-239">フォールバック [フロー イメージ](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9764f-239">See the [fallback flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="9764f-240">これにより、エラーやユーザーの同意などの未適合の依存関係が発生した場合に、SSO フローが通常の OAuthCard フローにフォールバックされます。</span><span class="sxs-lookup"><span data-stu-id="9764f-240">This ensures that the SSO flow falls back to normal OAuthCard flow in case of any errors or unmet dependencies like user consent.</span></span>


### <a name="update-the-auth-sample"></a><span data-ttu-id="9764f-241">認証サンプルの更新</span><span class="sxs-lookup"><span data-stu-id="9764f-241">Update the auth sample</span></span>

<span data-ttu-id="9764f-242">[認証サンプルTeams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)開き、次の手順を実行して更新します。</span><span class="sxs-lookup"><span data-stu-id="9764f-242">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="9764f-243">次のコードを含めることによって、受信要求の複製を処理するように TeamsBot を更新します。</span><span class="sxs-lookup"><span data-stu-id="9764f-243">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

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
  
2. <span data-ttu-id="9764f-244">更新 `appsettings.json` プログラムを使用して `botId` [、「OAuth 接続で Azure ポータルを更新](#update-the-azure-portal-with-the-oauth-connection)する 」で定義されている、パスワード、および接続名を含めます。</span><span class="sxs-lookup"><span data-stu-id="9764f-244">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="9764f-245">マニフェストを更新し、 `token.botframework.com` 有効なドメインリストに含まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="9764f-245">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="9764f-246">詳細については、「[認証のサンプルTeams」](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9764f-246">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="9764f-247">プロファイル イメージをマニフェストに zip して、Teamsにインストールします。</span><span class="sxs-lookup"><span data-stu-id="9764f-247">Zip the manifest with the profile images and install it in Teams.</span></span>

## <a name="code-sample"></a><span data-ttu-id="9764f-248">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="9764f-248">Code sample</span></span>
|<span data-ttu-id="9764f-249">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="9764f-249">**Sample name**</span></span> | <span data-ttu-id="9764f-250">**説明**</span><span class="sxs-lookup"><span data-stu-id="9764f-250">**Description**</span></span> |<span data-ttu-id="9764f-251">**.NET**</span><span class="sxs-lookup"><span data-stu-id="9764f-251">**.NET**</span></span> | 
|----------------|-----------------|--------------|
|<span data-ttu-id="9764f-252">ボット フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="9764f-252">Bot framework SDK</span></span> | <span data-ttu-id="9764f-253">ボット フレームワーク SDK の使用例。</span><span class="sxs-lookup"><span data-stu-id="9764f-253">Sample for using the bot framework SDK.</span></span> |[<span data-ttu-id="9764f-254">View</span><span class="sxs-lookup"><span data-stu-id="9764f-254">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
