---
title: 着信通知
description: 着信からの通知の処理に関する詳細な技術情報
ms.topic: conceptual
localization_priority: Normal
keywords: 呼び出し通知コールバック地域アフィニティ
ms.date: 04/02/2019
ms.openlocfilehash: 06068c13d27598b9a7b5e70181c69f9efb2c0afb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020177"
---
# <a name="incoming-call-notifications"></a><span data-ttu-id="91a0a-104">着信通知</span><span class="sxs-lookup"><span data-stu-id="91a0a-104">Incoming call notifications</span></span>

<span data-ttu-id="91a0a-105">[Microsoft Teams の通話と会議ボットを](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)登録する場合、URL を呼び出す Webhook について説明します。</span><span class="sxs-lookup"><span data-stu-id="91a0a-105">In [registering a calls and meetings bot for Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), the Webhook for calling URL is mentioned.</span></span> <span data-ttu-id="91a0a-106">この URL は、ボットへのすべての着信呼び出しの Webhook エンドポイントです。</span><span class="sxs-lookup"><span data-stu-id="91a0a-106">This URL is the webhook endpoint for all incoming calls to your bot.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="91a0a-107">プロトコルの決定</span><span class="sxs-lookup"><span data-stu-id="91a0a-107">Protocol determination</span></span>

<span data-ttu-id="91a0a-108">受信通知は、以前の Skype プロトコルとの互換性を保つレガシ形式で [提供されます](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="91a0a-108">The incoming notification is provided in a legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="91a0a-109">呼び出しを Microsoft Graph プロトコルに変換するには、ボットが通知が従来の形式であるかどうかを判断し、次の応答を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91a0a-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in a legacy format and provide the following response:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="91a0a-110">ボットは通知を再度受信しますが、今回は Microsoft Graph プロトコルで受信します。</span><span class="sxs-lookup"><span data-stu-id="91a0a-110">Your bot receives the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="91a0a-111">リアルタイム メディア プラットフォームの将来のリリースでは、アプリケーションがサポートするプロトコルを構成して、従来の形式で最初のコールバックを受信しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="91a0a-111">In a future release of the Real-time Media Platform, you can configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

<span data-ttu-id="91a0a-112">次のセクションでは、展開に地域アフィニティ用にリダイレクトされる着信呼び出し通知の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="91a0a-112">The next section provides details on incoming call notifications redirected for region affinity to your deployment.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="91a0a-113">地域アフィニティのリダイレクト</span><span class="sxs-lookup"><span data-stu-id="91a0a-113">Redirects for region affinity</span></span>

<span data-ttu-id="91a0a-114">Webhook は、呼び出しをホストするデータ センターから呼び出します。</span><span class="sxs-lookup"><span data-stu-id="91a0a-114">You call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="91a0a-115">呼び出しは任意のデータ センターで開始され、地域アフィニティは考慮されません。</span><span class="sxs-lookup"><span data-stu-id="91a0a-115">The call starts in any data center and does not take into account region affinities.</span></span> <span data-ttu-id="91a0a-116">通知は、GeoDNS 解決に応じて展開に送信されます。</span><span class="sxs-lookup"><span data-stu-id="91a0a-116">The notification is sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="91a0a-117">アプリケーションが最初の通知ペイロードを調べ、それ以外の場合は別の展開で実行する必要があると判断した場合、アプリケーションは次の応答を提供します。</span><span class="sxs-lookup"><span data-stu-id="91a0a-117">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application provides the following response:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="91a0a-118">ボットが応答 API を使用して着信呼び出しに応答 [できます](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) 。</span><span class="sxs-lookup"><span data-stu-id="91a0a-118">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="91a0a-119">この特定の呼び `callbackUri` 出しを処理するを指定できます。</span><span class="sxs-lookup"><span data-stu-id="91a0a-119">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="91a0a-120">これは、呼び出しが特定のパーティションによって処理され、この情報を適切なインスタンスにルーティングするために埋め込むステートフル インスタンスに `callbackUri` 役立ちます。</span><span class="sxs-lookup"><span data-stu-id="91a0a-120">This is useful for stateful instances where your call is handled by a particular partition, and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

<span data-ttu-id="91a0a-121">次のセクションでは、Webhook に投稿されたトークンを調によるコールバックの認証の詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="91a0a-121">The next section provides details on authenticating the callback by inspecting the token posted to your webhook.</span></span>

## <a name="authenticate-the-callback"></a><span data-ttu-id="91a0a-122">コールバックの認証</span><span class="sxs-lookup"><span data-stu-id="91a0a-122">Authenticate the callback</span></span>

<span data-ttu-id="91a0a-123">ボットは、Webhook に投稿されたトークンを検査して要求を検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91a0a-123">Your bot must inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="91a0a-124">API が Webhook に投稿する度に、HTTP POST メッセージには、承認ヘッダーに OAuth トークンがベアラー トークンとして含まれます。対象ユーザーはアプリケーションのアプリ ID です。</span><span class="sxs-lookup"><span data-stu-id="91a0a-124">Every time the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a bearer token, with the audience as your application's App ID.</span></span>

<span data-ttu-id="91a0a-125">アプリケーションは、コールバック要求を受け入れる前に、このトークンを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91a0a-125">Your application must validate this token before accepting the callback request.</span></span>

<span data-ttu-id="91a0a-126">コールバックを認証するには、次のサンプル コードを使用します。</span><span class="sxs-lookup"><span data-stu-id="91a0a-126">The following sample code is used to authenticate the callback:</span></span>

```http
POST https://bot.contoso.com/api/calls
Content-Type: application/json
Authentication: Bearer <TOKEN>

"value": [
    "subscriptionId": "2887CEE8344B47C291F1AF628599A93C",
    "subscriptionExpirationDateTime": "2016-11-20T18:23:45.9356913Z",
    "changeType": "updated",
    "resource": "/app/calls/8A934F51F25B4EE19613D4049491857B",
    "resourceData": {
        "@odata.type": "#microsoft.graph.call",
        "state": "Established"
    }
]
```

<span data-ttu-id="91a0a-127">OAuth トークンは次の値を持ち、Skype によって署名されます。</span><span class="sxs-lookup"><span data-stu-id="91a0a-127">The OAuth token has the following values, and is signed by Skype:</span></span>

```json
{
    "aud": "0efc74f7-41c3-47a4-8775-7259bfef4241",
    "iss": "https://api.botframework.com",
    "iat": 1466741440,
    "nbf": 1466741440,
    "exp": 1466745340,
    "tid": "1fdd12d0-4620-44ed-baec-459b611f84b2"
}
```

<span data-ttu-id="91a0a-128">公開されている OpenID 構成 <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> を使用して、トークンを確認できます。</span><span class="sxs-lookup"><span data-stu-id="91a0a-128">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span> <span data-ttu-id="91a0a-129">各 OAuth トークンの値は、次のように使用されます。</span><span class="sxs-lookup"><span data-stu-id="91a0a-129">Each OAuth token value is used as follows:</span></span>

* <span data-ttu-id="91a0a-130">`aud` 対象ユーザーは、アプリケーションに指定されたアプリ ID URI です。</span><span class="sxs-lookup"><span data-stu-id="91a0a-130">`aud` where audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="91a0a-131">`tid` は、ユーザーのテナント id Contoso.com。</span><span class="sxs-lookup"><span data-stu-id="91a0a-131">`tid` is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="91a0a-132">`iss` はトークン発行者です `https://api.botframework.com` 。</span><span class="sxs-lookup"><span data-stu-id="91a0a-132">`iss` is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="91a0a-133">コード処理では、Webhook はトークンを検証し、有効期限が切れていないか確認し、発行された OpenID 構成によって署名されているかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91a0a-133">For your code handling, the webhook must validate the token, ensure it has not expired, and check whether it has been signed by the published OpenID configuration.</span></span> <span data-ttu-id="91a0a-134">コールバック要求を受け入れる前に、aud がアプリ ID と一致するかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91a0a-134">You must also check whether aud matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="91a0a-135">詳細については、「受信要求 [の検証」を参照してください](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)。</span><span class="sxs-lookup"><span data-stu-id="91a0a-135">For more information, see [validate inbound requests](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).</span></span>

## <a name="next-step"></a><span data-ttu-id="91a0a-136">次の手順</span><span class="sxs-lookup"><span data-stu-id="91a0a-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="91a0a-137">アプリケーションホスト型メディア ボットの要件と考慮事項</span><span class="sxs-lookup"><span data-stu-id="91a0a-137">Requirements and considerations for application-hosted media bots</span></span>](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
