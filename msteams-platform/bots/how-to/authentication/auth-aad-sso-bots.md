---
title: ボットのシングル サインオンのサポート
description: ユーザートークンを取得する方法について説明します。 現在、ボット開発者は、OAuth カードサポート付きのサインインカードまたは azure bot サービスを使用できます。
keywords: ボットのトークン、ユーザートークン、SSO のサポート
ms.openlocfilehash: a056ce1a8bf0e59c9f4f30392df3bce7e8c63e00
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346855"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="ad9d8-105">ボットに対するシングルサインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="ad9d8-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="ad9d8-106">Azure Active Directory のシングルサインオン認証 (Azure AD) は、ユーザーが認証トークンを自動的に更新することによってログイン資格情報の入力が必要になる回数を最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-106">Single sign-on authentication in Azure Active Directory (Azure AD) minimizes the number of times users need to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="ad9d8-107">ユーザーがアプリを使用することに同意しない場合は、別のデバイスで再度同意する必要がなく、自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-107">If users agrees to use your app, they will not have to consent again on another device and will be signed in automatically.</span></span> <span data-ttu-id="ad9d8-108">このフローは、 [Teams タブ SSO のサポート]( ../../../tabs/how-to/authentication/auth-aad-sso.md)によく似ています。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-108">The flow is very similar to the [Teams tab SSO support]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="ad9d8-109">違いは、bot がトークンを要求し、応答を受信する方法のプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-109">The difference is the protocol for how a bot requests tokens and receives responses.</span></span>

<span data-ttu-id="ad9d8-110">OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-110">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="ad9d8-111">OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-111">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="ad9d8-112">実行時のボット SSO</span><span class="sxs-lookup"><span data-stu-id="ad9d8-112">Bot SSO at runtime</span></span>

![実行時の図のボット SSO](../../../assets/images/bots/bots-sso-diagram.png)

1. <span data-ttu-id="ad9d8-114">Bot は、プロパティを含む OAuthCard を持つメッセージを送信し `tokenExchangeResource` ます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="ad9d8-115">これにより、チームは bot アプリケーションの認証トークンを取得するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="ad9d8-116">ユーザーは、ユーザーのすべてのアクティブなエンドポイントでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-116">The user receives messages at all the active endpoints of the user.</span></span>

> [!NOTE]
>* <span data-ttu-id="ad9d8-117">ユーザーは、一度に複数のアクティブなエンドポイントを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-117">A user can have more than one active endpoint at a time.</span></span>  
>* <span data-ttu-id="ad9d8-118">Bot トークンは、ユーザーのすべてのアクティブエンドポイントから受信されます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-118">The bot token is received from every active endpoint of the user.</span></span>
>* <span data-ttu-id="ad9d8-119">現在、シングルサインオンがサポートされているためには、アプリを個人スコープにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-119">Single sign-on support currently requires the app to be installed in personal scope.</span></span>

2. <span data-ttu-id="ad9d8-120">現在のユーザーが初めて bot アプリケーションを使用していた場合は、同意を求めるメッセージが表示されます (同意が必要な場合)。または、ステップアップ認証 (2 要素認証など) を処理するための要求があります。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-120">If it is the first time the current user has used your bot application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>

3. <span data-ttu-id="ad9d8-121">Microsoft Teams は、現在のユーザーの Azure AD エンドポイントから bot アプリケーショントークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-121">Microsoft Teams requests the bot application token from the Azure AD endpoint for the current user.</span></span>

4. <span data-ttu-id="ad9d8-122">Azure AD は bot アプリケーショントークンを Teams アプリケーションに送信します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-122">Azure AD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="ad9d8-123">Microsoft Teams は、呼び出しアクティビティによって返される値オブジェクトの一部として、そのトークンを、サインイン/tokenExchange という名前で送信します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-123">Microsoft Teams sends the token to the bot as part of the value object returned by the invoke activity with the name sign-in/tokenExchange.</span></span>
  
6. <span data-ttu-id="ad9d8-124">このトークンは bot アプリケーションで解析され、ユーザーの電子メールアドレスなど、必要な情報を抽出します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-124">The token will be parsed in the bot application to extract the needed information, such as the user's email address.</span></span>
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a><span data-ttu-id="ad9d8-125">シングルサインオン Microsoft Teams bot を開発する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-125">Develop a Single sign-on Microsoft Teams bot</span></span>
  
<span data-ttu-id="ad9d8-126">SSO Microsoft Teams bot を開発するには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-126">The following steps: are required to develop an SSO Microsoft Teams bot:</span></span>

1. [<span data-ttu-id="ad9d8-127">Azure 無料アカウントを作成する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-127">Create an Azure free account</span></span>](#create-an-azure-account)
2. [<span data-ttu-id="ad9d8-128">Teams アプリマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-128">Update your Teams app manifest</span></span>](#update-your-app-manifest)
3. [<span data-ttu-id="ad9d8-129">Bot トークンを要求および受信するコードを追加する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-129">Add the code to request and receive the bot token</span></span>](#request-a-bot-token)

### <a name="create-an-azure-account"></a><span data-ttu-id="ad9d8-130">Azure アカウントを作成する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-130">Create an Azure account</span></span>

<span data-ttu-id="ad9d8-131">この手順は、 [タブ SSO フロー](../../../tabs/how-to/authentication/auth-aad-sso.md)に似ています。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-131">This step is similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md):</span></span>

1. <span data-ttu-id="ad9d8-132">[AZURE AD アプリケーション ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)を取得します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-132">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span>
2. <span data-ttu-id="ad9d8-133">Azure AD エンドポイントと、必要に応じて Microsoft Graph に対してアプリケーションに必要なアクセス許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-133">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="ad9d8-134">Teams デスクトップ、web、モバイルアプリケーションに[アクセス許可を付与](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-134">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="ad9d8-135">事前承認する [ **スコープの追加** ] ボタンを選択し、表示されるパネルで、 `access_as_user` **範囲名** としてを入力します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-135">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="ad9d8-136">スタンドアロン bot を構築する場合は、アプリケーション ID URI をに設定し `api://botid-{YourBotId}` ます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-136">If you are building a standalone bot, set the Application ID URI to `api://botid-{YourBotId}` .</span></span>
> * <span data-ttu-id="ad9d8-137">Bot とタブを使用してアプリを作成する場合は、アプリケーション ID URI をに設定し `api://fully-qualified-domain-name.com/botid-{YourBotId}` ます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-137">If you are building an app with a bot and a tab, set the Application ID URI to `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="ad9d8-138">アプリのマニフェストを更新する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-138">Update your app manifest</span></span>

<span data-ttu-id="ad9d8-139">Microsoft Teams のマニフェストに新しいプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-139">Add new properties to your Microsoft Teams manifest:</span></span>

<span data-ttu-id="ad9d8-140">**Webapplicationinfo** -次の要素の親。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-140">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ad9d8-141">**id** -アプリケーションのクライアント id。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-141">**id** - The client ID of the application.</span></span> <span data-ttu-id="ad9d8-142">これは、アプリケーションを Azure AD に登録する際に取得したアプリケーション ID です。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-142">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="ad9d8-143">**resource** -アプリケーションのドメインとサブドメイン。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-143">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="ad9d8-144">これは、 `api://` 上記の手順6でを作成するときに登録したものと同じ URI (プロトコルを含む) です `scope` 。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-144">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="ad9d8-145">リソースにパスを含めることはでき `access_as_user` ません。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-145">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="ad9d8-146">この URI のドメイン部分は、Teams アプリケーションマニフェストの Url で使用されるすべてのサブドメインを含むドメインと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-146">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a><span data-ttu-id="ad9d8-147">Bot トークンを要求する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-147">Request a bot token</span></span>

<span data-ttu-id="ad9d8-148">トークンを取得する要求は、(既存のメッセージスキーマを使用して) 通常の POST メッセージ要求です。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-148">The request to get the token is a normal POST message request (using the existing message schema).</span></span> <span data-ttu-id="ad9d8-149">これは、OAuthCard の添付ファイルに含まれています。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-149">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="ad9d8-150">OAuthCard クラスのスキーマは、 [Microsoft Bot スキーマ 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義されており、サインインカードに非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-150">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is very similar to a sign-in card.</span></span> <span data-ttu-id="ad9d8-151">この `TokenExchangeResource` プロパティがカードに設定されている場合、Teams はこの要求をサイレントトークンの取得として扱います。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-151">Teams will treat this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="ad9d8-152">Teams チャネルの場合は、 `Id` トークン要求を一意に識別するプロパティのみを優先します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-152">For the Teams channel we honor only the `Id` property, which uniquely identifies a token request.</span></span>

<span data-ttu-id="ad9d8-153">ユーザーが初めてアプリケーションを使用していて、ユーザーの同意が必要な場合は、次のような同意を得るためのダイアログがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-153">If this is the first time the user is using your application and the user consent is required, the user will be shown a dialog to continue with the consent experience similar to the one below.</span></span> <span data-ttu-id="ad9d8-154">ユーザーが [ **続行**] を選択すると、bot が定義されているかどうか、および OAuthCard のサインインボタンが定義されているかどうかに応じて、次の2つの問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-154">When the user selects **Continue**, two different things occur depending on whether the bot is defined or not and a sign-in button on the OAuthCard.</span></span>

![同意ダイアログボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="ad9d8-156">Bot がサインインボタンを定義している場合、ボットのサインインフローは、メッセージストリームのカードボタンからのサインインフローと同様にトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-156">If the bot defines a sign-in button, the sign-in flow for bots will be triggered similarly to the sign-in flow from a card button in a message stream.</span></span> <span data-ttu-id="ad9d8-157">ユーザーに同意を求めるアクセス許可を決定するのは開発者のことです。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-157">It is up to the developer to decide which permissions to ask for the user to consent.</span></span> <span data-ttu-id="ad9d8-158">このアプローチが推奨されるのは、 `openId` たとえば、グラフリソースのトークンを交換する必要がある場合など、アクセス許可を含むトークンが必要な場合です。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-158">This approach is recommended if you need a token with permissions beyond `openId`, for example, if you want to exchange the token for graph resources.</span></span>

<span data-ttu-id="ad9d8-159">Bot がカードにサインインボタンを提供していない場合、最小限のアクセス許可セットに対してユーザーの同意がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-159">If the bot is not providing a sign-in button on the card, it triggers user consent for a minimal set of permissions.</span></span> <span data-ttu-id="ad9d8-160">このトークンは、基本認証とユーザーの電子メールアドレスの取得に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-160">This token is useful for basic authentication and getting the user email address.</span></span>

<span data-ttu-id="ad9d8-161">**[サインイン] ボタンのない C# トークン要求**:</span><span class="sxs-lookup"><span data-stu-id="ad9d8-161">**C# token request without a sign-in button**:</span></span>

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

#### <a name="receiving-the-token"></a><span data-ttu-id="ad9d8-162">トークンの受信</span><span class="sxs-lookup"><span data-stu-id="ad9d8-162">Receiving the token</span></span>

<span data-ttu-id="ad9d8-163">トークンを使用した応答は、呼び出しアクティビティを通じて同じスキーマで送信されます。その他の場合は、現在のボットが受け取るアクティビティを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-163">The response with the token is sent through an invoke activity with the same schema as others invoke activities the bots receive today.</span></span> <span data-ttu-id="ad9d8-164">唯一の違いは、呼び出し名、**サインイン/** トークンの交換、およびトークンと **トークン** フィールド (トークンを含む文字列値) を取得する最初の要求の **Id** (文字列) が含まれる **値** フィールドです。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-164">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field which will contain the **Id** (a string) of the initial request to get the token and the **token** field (a string value including the token).</span></span> <span data-ttu-id="ad9d8-165">ユーザーが複数のアクティブエンドポイントを持っている場合は、特定の要求に対して複数の応答を受信する可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-165">Please note that you might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="ad9d8-166">このトークンを使用して、応答を deduplicate することができます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-166">It is up to you to deduplicate the responses with the token.</span></span>

<span data-ttu-id="ad9d8-167">**呼び出しアクティビティを処理するために応答する C# コード**:</span><span class="sxs-lookup"><span data-stu-id="ad9d8-167">**C# code to respond to handle the invoke activity**:</span></span>

```csharp
protected override async Task<InvokeResponse> OnInvokeActivity
  (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            try
            {
                if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                {
                    await OnTokenResponse(turnContext, cancellationToken);
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

<span data-ttu-id="ad9d8-168">`turnContext.activity.value`は[TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)型であり、bot がさらに使用できるトークンを含みます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-168">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="ad9d8-169">パフォーマンス上の理由でトークンを安全に保存し、更新します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-169">Store the tokens securely for performance reasons and refresh them.</span></span>

### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="ad9d8-170">Azure portal を OAuth 接続で更新する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-170">Update the Azure portal with the OAuth connection</span></span>

1. <span data-ttu-id="ad9d8-171">Azure Portal で、 **Bot チャネル登録** に戻ります。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-171">In the Azure Portal, navigate back to the **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="ad9d8-172">[ **設定** ] ブレードに切り替え、[OAuth 接続設定] セクションの下にある [ **設定** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-172">Switch to the **Settings** blade and choose **Add Setting** under the OAuth Connection Settings section.</span></span>

![SSOBotHandle2 ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. <span data-ttu-id="ad9d8-174">[ **接続設定** ] フォームを完成させます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-174">Complete the **Connection Setting** form:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ad9d8-175">新しい接続設定の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-175">Enter a name for your new Connection Setting.</span></span> <span data-ttu-id="ad9d8-176">これは、 **手順 5** で bot サービスコードの設定内で参照される名前になります。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-176">This will be the name that gets referenced inside the settings of your bot service code in **step 5**.</span></span>
> * <span data-ttu-id="ad9d8-177">サービスプロバイダーのドロップダウンで、[ **Azure Active Directory V2**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-177">In the Service Provider dropdown, select **Azure Active Directory V2**.</span></span>
>* <span data-ttu-id="ad9d8-178">AAD アプリケーションのクライアント資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-178">Enter the client credentials for the AAD application.</span></span>
>* <span data-ttu-id="ad9d8-179">トークン交換 URL の場合は、AAD アプリケーションの前の手順で定義した範囲の値を使用します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-179">For the Token Exchange URL, use the scope value defined in the previous step of your AAD application.</span></span> <span data-ttu-id="ad9d8-180">トークン交換 URL の存在は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-180">The presence of the Token Exchange URL is indicating to the SDK that this AAD application is configured for SSO.</span></span>
>* <span data-ttu-id="ad9d8-181">**テナント ID** として "common" を指定します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-181">Specify "common" as the **Tenant ID**.</span></span>
>* <span data-ttu-id="ad9d8-182">AAD アプリケーションの下流 Api へのアクセス許可を指定するときに構成されているすべてのスコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-182">Add all the scopes configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="ad9d8-183">クライアント id とクライアントシークレットが指定されている場合、トークンストアは、定義されたアクセス許可を持つグラフトークンのトークンを交換します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-183">With the client id and client secret provided, token store will exchange the token for a graph token with defined permissions for you.</span></span>
>* <span data-ttu-id="ad9d8-184">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-184">Select **Save**.</span></span>

![VuSSOBotConnection 設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a><span data-ttu-id="ad9d8-186">Auth サンプルを更新する</span><span class="sxs-lookup"><span data-stu-id="ad9d8-186">Update the auth sample</span></span>

<span data-ttu-id="ad9d8-187">最初に [teams auth サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)から始めます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-187">Start with the [teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>

1. <span data-ttu-id="ad9d8-188">次のものを含めるように、TeamsBot を更新します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-188">Update the TeamsBot to include the following.</span></span> <span data-ttu-id="ad9d8-189">着信要求の deduping を処理するには、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-189">To handle the deduping of the incoming request, see below:</span></span>

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
  
2. <span data-ttu-id="ad9d8-190">を更新して、に `appsettings.json` `botId` 定義されている、パスワード、および接続名を含めます。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-190">Update the `appsettings.json` to include the `botId`, password, and the connection name defined above.</span></span>
3. <span data-ttu-id="ad9d8-191">マニフェストを更新して、 `token.botframework.com` が [有効なドメイン] セクションにあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-191">Update the manifest and ensure that `token.botframework.com` is in the valid domains section.</span></span>
4. <span data-ttu-id="ad9d8-192">プロファイル画像を使用してマニフェストを圧縮し、Teams にインストールします。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-192">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="ad9d8-193">その他のコードサンプル</span><span class="sxs-lookup"><span data-stu-id="ad9d8-193">Additional code samples</span></span>

* <span data-ttu-id="ad9d8-194">[C# のサンプルは Bot フレームワーク SDK を使用して](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c)います。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-194">[C# sample using the Bot Framework SDK](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c).</span></span>

* <span data-ttu-id="ad9d8-195">[C# のサンプル Bot フレームワーク SDK を使用して、トークン要求を deduplicate](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)します。</span><span class="sxs-lookup"><span data-stu-id="ad9d8-195">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* [<span data-ttu-id="ad9d8-196">Bot フレームワーク SDK トークンストアを使用しない C# サンプル</span><span class="sxs-lookup"><span data-stu-id="ad9d8-196">C# sample without using the Bot Framework SDK token store</span></span>](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)
