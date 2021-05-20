---
title: メッセージング拡張機能の SSO サポート
author: KirtiPereira
description: メッセージング拡張機能の SSO サポートを有効にする方法
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 02d08506a07e955693531908f4f3cf16573a02c0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566202"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="7263b-103">メッセージング拡張機能のシングル サインオン (SSO) サポート</span><span class="sxs-lookup"><span data-stu-id="7263b-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="7263b-104">シングル サインオンのサポートは、メッセージング拡張機能とリンクの展開で使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="7263b-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="7263b-105">メッセージング拡張機能のシングル サインオン (SSO) を有効にすると、認証トークンがサイレントモードで更新されるため、Microsoft Teamsにサインイン資格情報を入力する必要がある回数が最小限に抑えられます。</span><span class="sxs-lookup"><span data-stu-id="7263b-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="7263b-106">このドキュメントでは、SSO を有効にし、必要に応じて認証トークンを保存する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7263b-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7263b-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="7263b-107">Prerequisites</span></span>

<span data-ttu-id="7263b-108">メッセージング拡張機能およびリンクの展開に対して SSO を有効にする前提条件は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7263b-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="7263b-109">[Azure](https://azure.microsoft.com/en-us/free/)アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="7263b-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="7263b-110">AAD ポータルを使用してアプリを構成し[、AAD ポータルを通じてアプリを登録](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)するに定義されているとおりに、ボットのTeams アプリケーション マニフェストを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7263b-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="7263b-111">Azure アカウントの作成とアプリ マニフェストの更新の詳細については、「 [ボットのシングル サインオン (SSO) サポート](../../bots/how-to/authentication/auth-aad-sso-bots.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7263b-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="7263b-112">メッセージング拡張機能およびリンクの展開に対して SSO を有効にする</span><span class="sxs-lookup"><span data-stu-id="7263b-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="7263b-113">前提条件が完了したら、メッセージング拡張機能およびリンクの展開に対して SSO を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="7263b-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="7263b-114">**SSO を有効にするには**</span><span class="sxs-lookup"><span data-stu-id="7263b-114">**To enable SSO**</span></span>
1. <span data-ttu-id="7263b-115">Azure ポータルでボット [OAuth 接続](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) の詳細を更新します。</span><span class="sxs-lookup"><span data-stu-id="7263b-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="7263b-116">[メッセージング拡張機能のサンプルを](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)ダウンロードし、ウィザードのセットアップ手順に従います。</span><span class="sxs-lookup"><span data-stu-id="7263b-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="7263b-117">メッセージング拡張機能を設定する際に、ボット OAuth 接続を使用します。</span><span class="sxs-lookup"><span data-stu-id="7263b-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="7263b-118">ファイルで[.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs)ファイルで、および/または .  `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync`</span><span class="sxs-lookup"><span data-stu-id="7263b-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="7263b-119">他のハンドラー SSO はサポートされていませんが、 `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` チーム メッセージングエクステンションサーチオーポフィ.csファイルを除きます。</span><span class="sxs-lookup"><span data-stu-id="7263b-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="7263b-120">`OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` SSO を有効にするシナリオに応じて、ペイロードまたは のハンドラーでトークンを受け取 `OnTeamsAppBasedLinkQueryAsync` ります。</span><span class="sxs-lookup"><span data-stu-id="7263b-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="7263b-121">OAuth 接続を使用している場合は、ストア内のトークンを更新または追加する.csファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="7263b-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
   ```C#
   protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
            if (valueObject["authentication"] != null)
            {
                JObject authenticationObject = JObject.FromObject(valueObject["authentication"]);
                if (authenticationObject["token"] != null)
                {
                    //If the token is NOT exchangeable, then return 412 to require user consent
                    if (await TokenIsExchangeable(turnContext, cancellationToken))
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
                    }
                    else
                    {
                        var response = new InvokeResponse();
                        response.Status = 412;
                        return response;
                    }
                }
            }
            return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
        }
        private async Task<bool> TokenIsExchangeable(ITurnContext turnContext, CancellationToken cancellationToken)
        {
            TokenResponse tokenExchangeResponse = null;
            try
            {
                JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
                var tokenExchangeRequest =
                ((JObject)valueObject["authentication"])?.ToObject<TokenExchangeInvokeRequest>();
                tokenExchangeResponse = await (turnContext.Adapter as IExtendedUserTokenProvider).ExchangeTokenAsync(
                 turnContext,
                 _connectionName,
                 turnContext.Activity.From.Id,
                 new TokenExchangeRequest
                 {
                     Token = tokenExchangeRequest.Token,
                 },
                 cancellationToken).ConfigureAwait(false);
            }
    #pragma warning disable CA1031 //Do not catch general exception types (ignoring, see comment below)
            catch
    #pragma warning restore CA1031 //Do not catch general exception types
            {
                //ignore exceptions
                //if token exchange failed for any reason, tokenExchangeResponse above remains null, and a failure invoke response is sent to the caller.
                //This ensures the caller knows that the invoke has failed.
            }
            if (tokenExchangeResponse == null || string.IsNullOrEmpty(tokenExchangeResponse.Token))
            {
                return false;
            }
            return true;
        }
    
    ```    

## <a name="see-also"></a><span data-ttu-id="7263b-122">関連項目</span><span class="sxs-lookup"><span data-stu-id="7263b-122">See also</span></span>

* [<span data-ttu-id="7263b-123">メッセージング拡張機能に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="7263b-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)
* [<span data-ttu-id="7263b-124">ボットに SSO を使用する</span><span class="sxs-lookup"><span data-stu-id="7263b-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [<span data-ttu-id="7263b-125">リンク展開</span><span class="sxs-lookup"><span data-stu-id="7263b-125">Link unfurling</span></span>](link-unfurling.md)

