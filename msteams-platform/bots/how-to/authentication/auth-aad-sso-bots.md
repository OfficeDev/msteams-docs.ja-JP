---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者はサインイン カードまたは Azure Bot サービスを OAuth カードのサポートと一緒に使用できます。
keywords: トークン、ユーザー トークン、ボットの SSO サポート
ms.openlocfilehash: ee9dbee063acf90f5596fc95d002caf53f88a08a
ms.sourcegitcommit: 0a9e91c65d88512eda895c21371b3cd4051dca0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/23/2020
ms.locfileid: "49729083"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="86806-105">ボットのシングル サインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="86806-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="86806-106">Azure Active Directory (Azure AD) のシングル サインオン認証は、ユーザーがログイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンをサイレント 更新します。</span><span class="sxs-lookup"><span data-stu-id="86806-106">Single sign-on authentication in Azure Active Directory (Azure AD) minimizes the number of times users need to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="86806-107">ユーザーがアプリの使用に同意した場合、別のデバイスでもう一度同意する必要はありません。また、自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="86806-107">If users agree to use your app, they will not have to consent again on another device and will be signed in automatically.</span></span> <span data-ttu-id="86806-108">このフローは、Teams タブ SSO の [サポートと非常に似ています]( ../../../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="86806-108">The flow is very similar to the [Teams tab SSO support]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="86806-109">違いは、ボットがトークンを要求して応答を受信する方法のプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="86806-109">The difference is the protocol for how a bot requests tokens and receives responses.</span></span>

<span data-ttu-id="86806-110">OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。</span><span class="sxs-lookup"><span data-stu-id="86806-110">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="86806-111">OAuth 2.0 の基本的な理解は、Teams で認証を操作する場合の前提条件です。</span><span class="sxs-lookup"><span data-stu-id="86806-111">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="86806-112">実行時の Bot SSO</span><span class="sxs-lookup"><span data-stu-id="86806-112">Bot SSO at runtime</span></span>

![実行時のボット SSO の図](../../../assets/images/bots/bots-sso-diagram.png)

1. <span data-ttu-id="86806-114">ボットは、プロパティを含む OAuthCard でメッセージを送信 `tokenExchangeResource` します。</span><span class="sxs-lookup"><span data-stu-id="86806-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="86806-115">ボット アプリケーションの認証トークンを取得するために Teams に指示します。</span><span class="sxs-lookup"><span data-stu-id="86806-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="86806-116">ユーザーは、ユーザーのすべてのアクティブなエンドポイントでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="86806-116">The user receives messages at all the active endpoints of the user.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="86806-117">ユーザーは一度に複数のアクティブなエンドポイントを持つ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="86806-117">A user can have more than one active endpoint at a time.</span></span>  
    >* <span data-ttu-id="86806-118">ボット トークンは、ユーザーのアクティブなエンドポイントごとに受信されます。</span><span class="sxs-lookup"><span data-stu-id="86806-118">The bot token is received from every active endpoint of the user.</span></span>
    >* <span data-ttu-id="86806-119">現在、シングル サインオンのサポートでは、アプリを個人用スコープでインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="86806-119">Single sign-on support currently requires the app to be installed in personal scope.</span></span>

2. <span data-ttu-id="86806-120">現在のユーザーが初めてボット アプリケーションを使用する場合は、同意を求める要求プロンプト (同意が必要な場合) またはステップ アップ認証 (2 要素認証など) の処理を求めるプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="86806-120">If it is the first time the current user has used your bot application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>

3. <span data-ttu-id="86806-121">Microsoft Teams は、現在のユーザーの Azure AD エンドポイントにボット アプリケーション トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="86806-121">Microsoft Teams requests the bot application token from the Azure AD endpoint for the current user.</span></span>

4. <span data-ttu-id="86806-122">Azure AD、ボット アプリケーション トークンを Teams アプリケーションに送信します。</span><span class="sxs-lookup"><span data-stu-id="86806-122">Azure AD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="86806-123">Microsoft Teams は、呼び出しアクティビティによって返される値オブジェクトの一部として、サインイン/トークンExchange という名前でトークンをボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="86806-123">Microsoft Teams sends the token to the bot as part of the value object returned by the invoke activity with the name sign-in/tokenExchange.</span></span>
  
6. <span data-ttu-id="86806-124">トークンはボット アプリケーションで解析され、ユーザーの電子メール アドレスなどの必要な情報を抽出します。</span><span class="sxs-lookup"><span data-stu-id="86806-124">The token will be parsed in the bot application to extract the needed information, such as the user's email address.</span></span>
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a><span data-ttu-id="86806-125">シングル サインオン Microsoft Teams ボットを開発する</span><span class="sxs-lookup"><span data-stu-id="86806-125">Develop a Single sign-on Microsoft Teams bot</span></span>
  
<span data-ttu-id="86806-126">SSO Microsoft Teams ボットを開発するには、次の手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="86806-126">The following steps are required to develop an SSO Microsoft Teams bot:</span></span>

1. [<span data-ttu-id="86806-127">Azure 無料アカウントを作成する</span><span class="sxs-lookup"><span data-stu-id="86806-127">Create an Azure free account</span></span>](#create-an-azure-account)
2. [<span data-ttu-id="86806-128">Teams アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="86806-128">Update your Teams app manifest</span></span>](#update-your-app-manifest)
3. [<span data-ttu-id="86806-129">ボット トークンを要求して受信するコードを追加する</span><span class="sxs-lookup"><span data-stu-id="86806-129">Add the code to request and receive the bot token</span></span>](#request-a-bot-token)

### <a name="create-an-azure-account"></a><span data-ttu-id="86806-130">Azure アカウントを作成する</span><span class="sxs-lookup"><span data-stu-id="86806-130">Create an Azure account</span></span>

<span data-ttu-id="86806-131">この手順は、タブ [SSO フローに似ています](../../../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="86806-131">This step is similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md):</span></span>

1. <span data-ttu-id="86806-132">Teams の [デスクトップAD Web、](/graph/concepts/auth-register-app-v2) またはモバイル クライアントの Azure アプリケーション ID を取得します。</span><span class="sxs-lookup"><span data-stu-id="86806-132">Get your [Azure AD Application ID](/graph/concepts/auth-register-app-v2) for Teams desktop, web, or mobile client.</span></span>
2. <span data-ttu-id="86806-133">アプリケーションが Azure AD エンドポイントと、必要に応じて Microsoft Graph に必要なアクセス許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="86806-133">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="86806-134">Teams[のデスクトップ、Web、](/azure/active-directory/develop/v2-permissions-and-consent)およびモバイル アプリケーションのアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="86806-134">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="86806-135">**[スコープの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="86806-135">Select **Add a scope**.</span></span>
5. <span data-ttu-id="86806-136">開くパネルで、スコープ名として入力してクライアント `access_as_user` アプリを **追加します**。</span><span class="sxs-lookup"><span data-stu-id="86806-136">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="86806-137">クライアント アプリのaccess_as_user "管理者とユーザー" のスコープです。</span><span class="sxs-lookup"><span data-stu-id="86806-137">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>

    > [!IMPORTANT]
    > * <span data-ttu-id="86806-138">スタンドアロン ボットを作成する場合は、アプリケーション ID URI を Here に設定します `api://botid-{YourBotId}` **。YourBotId** は Azure ADアプリケーション ID を参照します。</span><span class="sxs-lookup"><span data-stu-id="86806-138">If you are building a standalone bot, set the Application ID URI to `api://botid-{YourBotId}` Here, **YourBotId** refers to your Azure AD application ID.</span></span>
    > * <span data-ttu-id="86806-139">ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次に設定します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="86806-139">If you are building an app with a bot and a tab, set the Application ID URI to `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="86806-140">アプリ マニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="86806-140">Update your app manifest</span></span>

<span data-ttu-id="86806-141">Microsoft Teams マニフェストに新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="86806-141">Add new properties to your Microsoft Teams manifest:</span></span>

<span data-ttu-id="86806-142">**WebApplicationInfo** - 次の要素の親。</span><span class="sxs-lookup"><span data-stu-id="86806-142">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="86806-143">**id** - アプリケーションのクライアント ID。</span><span class="sxs-lookup"><span data-stu-id="86806-143">**id** - The client ID of the application.</span></span> <span data-ttu-id="86806-144">これは、Azure AD にアプリケーションを登録する一環として取得したアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="86806-144">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="86806-145">**resource** - アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="86806-145">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="86806-146">これは、上記の手順 6 で作成するときに登録した URI (プロトコルを含む `api://` ) `scope` と同じです。</span><span class="sxs-lookup"><span data-stu-id="86806-146">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="86806-147">リソースにパスを `access_as_user` 含めてはならない。</span><span class="sxs-lookup"><span data-stu-id="86806-147">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="86806-148">この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用される任意のサブドメインを含むドメインと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="86806-148">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a><span data-ttu-id="86806-149">ボット トークンを要求する</span><span class="sxs-lookup"><span data-stu-id="86806-149">Request a bot token</span></span>

<span data-ttu-id="86806-150">トークンを取得する要求は、通常の POST メッセージ要求です (既存のメッセージ スキーマを使用)。</span><span class="sxs-lookup"><span data-stu-id="86806-150">The request to get the token is a normal POST message request (using the existing message schema).</span></span> <span data-ttu-id="86806-151">OAuthCard の添付ファイルに含まれています。</span><span class="sxs-lookup"><span data-stu-id="86806-151">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="86806-152">OAuthCard クラスのスキーマは Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義され、サインイン カードに非常に似ています。</span><span class="sxs-lookup"><span data-stu-id="86806-152">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is very similar to a sign-in card.</span></span> <span data-ttu-id="86806-153">プロパティがカードに入力されている場合、Teams は、この要求をサイレント トークン取得 `TokenExchangeResource` として処理します。</span><span class="sxs-lookup"><span data-stu-id="86806-153">Teams will treat this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="86806-154">Teams チャネルでは、トークン要求を一意に識別するプロパティ `Id` のみを尊重します。</span><span class="sxs-lookup"><span data-stu-id="86806-154">For the Teams channel, we honor only the `Id` property, which uniquely identifies a token request.</span></span>

>[!NOTE]
> <span data-ttu-id="86806-155">Bot Framework `OAuthPrompt` またはシングル `MultiProviderAuthDialog` サインオン (SSO) 認証がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="86806-155">The Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for single sign-on (SSO) authentication.</span></span>

<span data-ttu-id="86806-156">ユーザーが初めてアプリケーションを使用し、ユーザーの同意が必要な場合は、次のような同意エクスペリエンスを続行するダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="86806-156">If this is the first time the user is using your application and the user consent is required, the user will be shown a dialog to continue with the consent experience similar to the one below.</span></span> <span data-ttu-id="86806-157">ユーザーが [ **続行**] を選択すると、ボットが定義されているかどうかと OAuthCard のサインイン ボタンに応じて、2 つの異なる処理が行われます。</span><span class="sxs-lookup"><span data-stu-id="86806-157">When the user selects **Continue**, two different things occur depending on whether the bot is defined or not and a sign-in button on the OAuthCard.</span></span>

![[同意] ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="86806-159">ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリーム内のカード ボタンからのサインイン フローと同様にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="86806-159">If the bot defines a sign-in button, the sign-in flow for bots will be triggered similarly to the sign-in flow from a card button in a message stream.</span></span> <span data-ttu-id="86806-160">開発者は、ユーザーに同意を求めるアクセス許可を決定します。</span><span class="sxs-lookup"><span data-stu-id="86806-160">It is up to the developer to decide which permissions to ask for the user to consent.</span></span> <span data-ttu-id="86806-161">この方法は、たとえば、グラフ リソースのトークンを交換する場合など、アクセス許可を持つトークンが必要な `openId` 場合に推奨されます。</span><span class="sxs-lookup"><span data-stu-id="86806-161">This approach is recommended if you need a token with permissions beyond `openId`, for example, if you want to exchange the token for graph resources.</span></span>

<span data-ttu-id="86806-162">ボットがカードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットに対するユーザーの同意がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="86806-162">If the bot is not providing a sign-in button on the card, it triggers user consent for a minimal set of permissions.</span></span> <span data-ttu-id="86806-163">このトークンは、基本認証とユーザーの電子メール アドレスの取得に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="86806-163">This token is useful for basic authentication and getting the user's email address.</span></span>

<span data-ttu-id="86806-164">**サインイン ボタンのない C# トークン要求**:</span><span class="sxs-lookup"><span data-stu-id="86806-164">**C# token request without a sign-in button**:</span></span>

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

#### <a name="receiving-the-token"></a><span data-ttu-id="86806-165">トークンの受信</span><span class="sxs-lookup"><span data-stu-id="86806-165">Receiving the token</span></span>

<span data-ttu-id="86806-166">トークンを持つ応答は、ボットが今日受け取るアクティビティを呼び出す他のユーザーと同じスキーマを持つ呼び出しアクティビティを通じて送信されます。</span><span class="sxs-lookup"><span data-stu-id="86806-166">The response with the token is sent through an invoke activity with the same schema as others invoke activities the bots receive today.</span></span> <span data-ttu-id="86806-167">唯一の違いは、呼び出し名、**サインイン/トークンExchange、** およびトークンとトークン フィールドを取得する最初の要求の **ID** (文字列)を含む値フィールド (トークンを含む文字列値) です。 </span><span class="sxs-lookup"><span data-stu-id="86806-167">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field which will contain the **Id** (a string) of the initial request to get the token and the **token** field (a string value including the token).</span></span> <span data-ttu-id="86806-168">ユーザーが複数のアクティブなエンドポイントを持っている場合、特定の要求に対して複数の応答を受信する場合があります。</span><span class="sxs-lookup"><span data-stu-id="86806-168">Please note that you might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="86806-169">トークンを使用して応答を重複排除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="86806-169">It is up to you to deduplicate the responses with the token.</span></span>

<span data-ttu-id="86806-170">**呼び出しアクティビティを処理するために応答する C# コード**:</span><span class="sxs-lookup"><span data-stu-id="86806-170">**C# code to respond to handle the invoke activity**:</span></span>

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

<span data-ttu-id="86806-171">`turnContext.activity.value` [TokenExchangeInvokeRequest 型](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)であり、ボットでさらに使用できるトークンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="86806-171">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="86806-172">パフォーマンス上の理由からトークンを安全に保存し、更新します。</span><span class="sxs-lookup"><span data-stu-id="86806-172">Store the tokens securely for performance reasons and refresh them.</span></span>

### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="86806-173">OAuth 接続を使用して Azure Portal を更新する</span><span class="sxs-lookup"><span data-stu-id="86806-173">Update the Azure portal with the OAuth connection</span></span>

1. <span data-ttu-id="86806-174">Azure Portal で、ボット チャネル登録に **戻る**。</span><span class="sxs-lookup"><span data-stu-id="86806-174">In the Azure Portal, navigate back to the **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="86806-175">[設定] ブレード **に切** り替え、[OAuth 接続の設定] セクションで [設定の追加] を選択します。 </span><span class="sxs-lookup"><span data-stu-id="86806-175">Switch to the **Settings** blade and choose **Add Setting** under the OAuth Connection Settings section.</span></span>

    ![SSOBotHandle2 ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. <span data-ttu-id="86806-177">[接続設定 **] フォームに入力** します。</span><span class="sxs-lookup"><span data-stu-id="86806-177">Complete the **Connection Setting** form:</span></span>

    > [!div class="checklist"]
    >
    > * <span data-ttu-id="86806-178">新しい接続設定の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="86806-178">Enter a name for your new Connection Setting.</span></span> <span data-ttu-id="86806-179">これは、手順 5 でボット サービス コードの設定内で参照される **名前になります**。</span><span class="sxs-lookup"><span data-stu-id="86806-179">This will be the name that gets referenced inside the settings of your bot service code in **step 5**.</span></span>
    > * <span data-ttu-id="86806-180">[サービス プロバイダー] ドロップダウンで **、Azure Active Directory V2 を選択します**。</span><span class="sxs-lookup"><span data-stu-id="86806-180">In the Service Provider dropdown, select **Azure Active Directory V2**.</span></span>
    >* <span data-ttu-id="86806-181">AAD アプリケーションのクライアント資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="86806-181">Enter the client credentials for the AAD application.</span></span>

    >[!NOTE]
    > <span data-ttu-id="86806-182">**AAD アプリケーション** では暗黙的な許可が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="86806-182">**Implicit grant** may be required in the AAD application.</span></span>

    >* <span data-ttu-id="86806-183">トークン交換 URL の場合は、AAD アプリケーションの前の手順で定義したスコープ値を使用します。</span><span class="sxs-lookup"><span data-stu-id="86806-183">For the Token Exchange URL, use the scope value defined in the previous step of your AAD application.</span></span> <span data-ttu-id="86806-184">Token Exchange URL の存在は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示しています。</span><span class="sxs-lookup"><span data-stu-id="86806-184">The presence of the Token Exchange URL is indicating to the SDK that this AAD application is configured for SSO.</span></span>
    >* <span data-ttu-id="86806-185">テナント ID として "common" **を指定します**。</span><span class="sxs-lookup"><span data-stu-id="86806-185">Specify "common" as the **Tenant ID**.</span></span>
    >* <span data-ttu-id="86806-186">AAD アプリケーションのダウンストリーム API に対するアクセス許可を指定するときに構成されたスコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="86806-186">Add all the scopes configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="86806-187">クライアント ID とクライアント シークレットが提供された場合、トークン ストアは、定義済みのアクセス許可を持つグラフ トークンのトークンを交換します。</span><span class="sxs-lookup"><span data-stu-id="86806-187">With the client id and client secret provided, the token store will exchange the token for a graph token with defined permissions for you.</span></span>
    >* <span data-ttu-id="86806-188">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="86806-188">Select **Save**.</span></span>

    ![VuSSOBotConnection 設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a><span data-ttu-id="86806-190">認証サンプルを更新する</span><span class="sxs-lookup"><span data-stu-id="86806-190">Update the auth sample</span></span>

<span data-ttu-id="86806-191">まず、 [チームの認証サンプルを参照してください](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。</span><span class="sxs-lookup"><span data-stu-id="86806-191">Start with the [teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>

1. <span data-ttu-id="86806-192">TeamsBot を更新して、次を含める。</span><span class="sxs-lookup"><span data-stu-id="86806-192">Update the TeamsBot to include the following.</span></span> <span data-ttu-id="86806-193">受信要求の重複を処理するには、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="86806-193">To handle the deduping of the incoming request, see below:</span></span>

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
  
2. <span data-ttu-id="86806-194">上記で `appsettings.json` 定義した接続名 `botId` 、パスワード、および接続名を含めるには、更新します。</span><span class="sxs-lookup"><span data-stu-id="86806-194">Update the `appsettings.json` to include the `botId`, password, and the connection name defined above.</span></span>
3. <span data-ttu-id="86806-195">マニフェストを更新し、有効 `token.botframework.com` なドメイン セクションに含まれています。</span><span class="sxs-lookup"><span data-stu-id="86806-195">Update the manifest and ensure that `token.botframework.com` is in the valid domains section.</span></span>
4. <span data-ttu-id="86806-196">マニフェストをプロファイル イメージと一緒に Zip し、Teams にインストールします。</span><span class="sxs-lookup"><span data-stu-id="86806-196">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="86806-197">その他のコード サンプル</span><span class="sxs-lookup"><span data-stu-id="86806-197">Additional code samples</span></span>

* <span data-ttu-id="86806-198">[Bot Framework SDK を使用した C# サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。</span><span class="sxs-lookup"><span data-stu-id="86806-198">[C# sample using the Bot Framework SDK](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).</span></span>

* <span data-ttu-id="86806-199">[Bot Framework SDK を使用してトークン要求](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)を重複排除する C# サンプル。</span><span class="sxs-lookup"><span data-stu-id="86806-199">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* <span data-ttu-id="86806-200">[Bot Framework SDK トークン ストアを使用しない C# サンプル](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)。</span><span class="sxs-lookup"><span data-stu-id="86806-200">[C# sample without using the Bot Framework SDK token store](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw).</span></span>
