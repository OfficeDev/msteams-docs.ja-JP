---
title: 着信呼び出し通知の処理に関する技術的な詳細
description: 着信呼び出しからの通知の処理に関する詳細な技術情報
keywords: 通話呼び出しの通知のコールバック領域の類似性
ms.date: 04/02/2019
ms.openlocfilehash: be8860ff70cd7dff4fd9599079ea7aab4f454174
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675044"
---
# <a name="incoming-call-notifications-technical-details"></a><span data-ttu-id="3a480-104">着信通話通知: 技術的な詳細</span><span class="sxs-lookup"><span data-stu-id="3a480-104">Incoming call notifications: technical details</span></span>

<span data-ttu-id="3a480-105">「 [Microsoft Teams での通話と会議のボットの登録](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot)」では、 **(呼び出し元の) URL の webhook (呼び出し元)** の URL (bot へのすべての着信呼び出しの webhook エンドポイント) について説明しました。</span><span class="sxs-lookup"><span data-stu-id="3a480-105">In [Registering a calling and meeting bot for Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), we mentioned the **Webhook (for calling)** URL — the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="3a480-106">このトピックでは、これらの通知に応答するために必要な技術情報について説明します。</span><span class="sxs-lookup"><span data-stu-id="3a480-106">This topic discusses the technical details you'll need to respond to these notifications.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="3a480-107">プロトコルの決定</span><span class="sxs-lookup"><span data-stu-id="3a480-107">Protocol determination</span></span>

<span data-ttu-id="3a480-108">受信通知は、以前の[Skype プロトコル](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)との互換性のために従来の形式で提供されます。</span><span class="sxs-lookup"><span data-stu-id="3a480-108">The incoming notification is provided in legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="3a480-109">呼び出しを Microsoft Graph プロトコルに変換するために、ボットは通知が従来の形式であるかどうかを判断し、次のように応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a480-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in legacy format and reply with:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="3a480-110">Bot は通知を再度受け取りますが、今回は Microsoft Graph プロトコルを使用します。</span><span class="sxs-lookup"><span data-stu-id="3a480-110">Your bot will receive the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="3a480-111">リアルタイムメディアプラットフォームの今後のリリースでは、アプリケーションがサポートするプロトコルを構成して、初期コールバックを従来の形式で受信しないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="3a480-111">In a future release of the Real-time Media Platform, we'll allow you to configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="3a480-112">地域の類似性のリダイレクト</span><span class="sxs-lookup"><span data-stu-id="3a480-112">Redirects for region affinity</span></span>

<span data-ttu-id="3a480-113">呼び出しをホストしているデータセンターから webhook を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3a480-113">You'll call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="3a480-114">この呼び出しは、任意のデータセンターで開始され、地域の類似性が考慮されることはありません。</span><span class="sxs-lookup"><span data-stu-id="3a480-114">The call may start in any data center and doesn't take into account region affinities.</span></span> <span data-ttu-id="3a480-115">GeoDNS の解決に応じて、展開に通知が送信されます。</span><span class="sxs-lookup"><span data-stu-id="3a480-115">The notification will be sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="3a480-116">アプリケーションが初期通知ペイロードを調べることによって、またはそれ以外の場合は、別の展開で実行する必要があると判断すると、アプリケーションは次のように応答します。</span><span class="sxs-lookup"><span data-stu-id="3a480-116">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application may reply with:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="3a480-117">Bot が[応答](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer)API を使用して着信呼び出しに応答できるようにします。</span><span class="sxs-lookup"><span data-stu-id="3a480-117">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="3a480-118">この特定の`callbackUri`呼び出しを処理するを指定できます。</span><span class="sxs-lookup"><span data-stu-id="3a480-118">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="3a480-119">これは、呼び出しが特定のパーティションによって処理される_ステートフル_なインスタンスで、 `callbackUri`右のインスタンスへのルーティングのためにこの情報をに埋め込む場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="3a480-119">This is useful for _stateful_ instances where your call is handled by a particular partition and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

## <a name="authenticating-the-callback"></a><span data-ttu-id="3a480-120">コールバックの認証</span><span class="sxs-lookup"><span data-stu-id="3a480-120">Authenticating the callback</span></span>

<span data-ttu-id="3a480-121">Bot は、要求を検証するために、webhook に投稿されたトークンを検査する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a480-121">Your bot should inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="3a480-122">API が webhook に投稿されるたびに、HTTP POST メッセージには、ユーザーがアプリケーションのアプリ ID として使用する、ベアラートークンとしての OAuth トークンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3a480-122">Whenever the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a Bearer token, with audience as your application's App ID.</span></span>

<span data-ttu-id="3a480-123">アプリケーションは、コールバック要求を受け入れる前に、このトークンを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a480-123">Your application should validate this token before accepting the callback request.</span></span>

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

<span data-ttu-id="3a480-124">OAuth トークンの値は次のようになり、Skype で署名されます。</span><span class="sxs-lookup"><span data-stu-id="3a480-124">The OAuth token will have values like the following, and will be signed by Skype.</span></span> <span data-ttu-id="3a480-125">で<https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration>公開されている OpenID configuration を使用して、トークンを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3a480-125">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span>

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

* <span data-ttu-id="3a480-126">**aud**対象ユーザーは、アプリケーションに対して指定されたアプリ ID URI です。</span><span class="sxs-lookup"><span data-stu-id="3a480-126">**aud** audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="3a480-127">**tid**は Contoso.com のテナント id です。</span><span class="sxs-lookup"><span data-stu-id="3a480-127">**tid** is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="3a480-128">**iss**はトークン発行者です`https://api.botframework.com`。</span><span class="sxs-lookup"><span data-stu-id="3a480-128">**iss** is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="3a480-129">Webhook を処理するコードでは、トークンを検証し、有効期限が切れていないことを確認して、公開された OpenID configuration によって署名されているかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a480-129">Your code handling the webhook should validate the token, ensure it hasn't expired, and check whether it has been signed by our published OpenID configuration.</span></span> <span data-ttu-id="3a480-130">また、コールバック要求を受け入れる前に、 **aud**がアプリ ID と一致するかどうかも確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a480-130">You should also check whether **aud** matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="3a480-131">[サンプル](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)は、受信要求を検証する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3a480-131">[Sample](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) shows how to validate inbound requests.</span></span>
