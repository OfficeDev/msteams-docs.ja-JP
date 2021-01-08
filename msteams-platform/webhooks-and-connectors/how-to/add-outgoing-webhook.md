---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
author: laujan
description: 送信 Webhook を追加する方法
keywords: Teams、タブ、送信 Webhook*
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 61dc8441795925b53e5c8459f9c6eed5a28856e1
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552466"
---
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a><span data-ttu-id="cca18-104">送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する</span><span class="sxs-lookup"><span data-stu-id="cca18-104">Add custom bots to Microsoft Teams with outgoing webhooks</span></span>

## <a name="what-are-outgoing-webhooks-in-teams"></a><span data-ttu-id="cca18-105">Teams での送信 Webhook とは</span><span class="sxs-lookup"><span data-stu-id="cca18-105">What are outgoing webhooks in Teams?</span></span>

<span data-ttu-id="cca18-106">Webhook は、Teams と外部アプリを統合させるための便利な手段です。</span><span class="sxs-lookup"><span data-stu-id="cca18-106">Webhooks are a great way for Teams to integrate with external apps.</span></span> <span data-ttu-id="cca18-107">基本的に Webhook は、コールバック URL に送信される POST 要求です。</span><span class="sxs-lookup"><span data-stu-id="cca18-107">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="cca18-108">Teams で送信 Webhook を使用すれば、ユーザーは Web サービスにメッセージを簡単に送信することができます。[Microsoft Bot Framework](https://dev.botframework.com/) でのボット作成のプロセス全体を踏む必要もありません。</span><span class="sxs-lookup"><span data-stu-id="cca18-108">In Teams, outgoing webhooks provide a simple way to allow users to send messages to your web service without having to go through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="cca18-109">送信 Webhook は Teams からのデータを、JSON ペイロードを受け入れることができる、選択された任意のサービスに投稿します。</span><span class="sxs-lookup"><span data-stu-id="cca18-109">Outgoing webhooks post data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="cca18-110">送信 Webhook がチームに追加されると、ボットのように動作します。**\@メンション** を使用してメッセージのチャネルをリッスンしたり、外部の Web サービスに通知を送信したりします。カードや画像を含む豊富なメッセージでの応答も行います。</span><span class="sxs-lookup"><span data-stu-id="cca18-110">Once an outgoing webhook is added to a team, it acts like bot, listening in channels for messages using **\@mention**, sending notifications to external web services, and responding with rich messages that can include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="cca18-111">送信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="cca18-111">Outgoing webhook key features</span></span>

| <span data-ttu-id="cca18-112">機能</span><span class="sxs-lookup"><span data-stu-id="cca18-112">Feature</span></span> | <span data-ttu-id="cca18-113">説明</span><span class="sxs-lookup"><span data-stu-id="cca18-113">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="cca18-114">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="cca18-114">Scoped Configuration</span></span>| <span data-ttu-id="cca18-115">Webhook はチームのレベルでスコープが設定されます。</span><span class="sxs-lookup"><span data-stu-id="cca18-115">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="cca18-116">送信 Webhook を追加するチームそれぞれのセットアップ処理を進める必要があります。</span><span class="sxs-lookup"><span data-stu-id="cca18-116">You’ll need to go through the setup process for each team you want to add your outgoing webhook to.</span></span> |
| <span data-ttu-id="cca18-117">反応性のあるメッセージング</span><span class="sxs-lookup"><span data-stu-id="cca18-117">Reactive Messaging</span></span>| <span data-ttu-id="cca18-118">ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cca18-118">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="cca18-119">現在ユーザーが送信 Webhook でメッセージを送信できるのは公開チャネルのみです。個人またはプライベートのスコープ内では行えません</span><span class="sxs-lookup"><span data-stu-id="cca18-119">Currently users can only message an outgoing webhook in public channels and not within the personal or private scope</span></span> |
|<span data-ttu-id="cca18-120">標準の HTTP メッセージ交換</span><span class="sxs-lookup"><span data-stu-id="cca18-120">Standard HTTP message exchange</span></span>|<span data-ttu-id="cca18-121">応答は元の要求メッセージと同じチェーンに表示され、Bot Framework のメッセージのコンテンツ (リッチ テキスト、画像、カード、絵文字) を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="cca18-121">Responses will appear in the same chain as the original request message and can include any Bot Framework message content (rich text, images, cards, and emojis).</span></span> <span data-ttu-id="cca18-122">**注**: 送信 Webhook はカードを使用することができますが、`openURL` のカード アクションしか使用することができません。</span><span class="sxs-lookup"><span data-stu-id="cca18-122">**Note**: Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="cca18-123">Teams API メソッドのサポート</span><span class="sxs-lookup"><span data-stu-id="cca18-123">Teams API method support</span></span>|<span data-ttu-id="cca18-124">Teams では、送信 Webhook は HTTP POST を Web サービスに送信し、応答を処理します。</span><span class="sxs-lookup"><span data-stu-id="cca18-124">In Teams, outgoing webhooks send an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="cca18-125">チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="cca18-125">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a><span data-ttu-id="cca18-126">アプリに送信 Webhook の処理を追加する</span><span class="sxs-lookup"><span data-stu-id="cca18-126">Adding outgoing webhook processing to your app</span></span>

<span data-ttu-id="cca18-127">**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="cca18-127">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="cca18-128">**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="cca18-128">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="cca18-129">1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する</span><span class="sxs-lookup"><span data-stu-id="cca18-129">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="cca18-130">サービスは、標準の Azure Bot Service のメッセージング スキーマでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="cca18-130">Your service will receive messages in the standard Azure bot service messaging schema.</span></span> <span data-ttu-id="cca18-131">Bot Framework Connector は、[Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) で文書化されているように、サービスが HTTPS プロトコルを使用して JSON 形式のメッセージ交換を処理できるようにする RESTful サービスです。</span><span class="sxs-lookup"><span data-stu-id="cca18-131">The Bot Framework connector is a RESTful service that enables your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="cca18-132">[Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="cca18-132">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="cca18-133">詳細については、「[Azure Bot Service について](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)」も *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="cca18-133">*See also*  [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).</span></span>

<span data-ttu-id="cca18-134">送信 Webhook は、`team` レベルにスコープが設定され、チームのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="cca18-134">Outgoing webhooks are scoped to the `team` level and are visible to all members of the team.</span></span> <span data-ttu-id="cca18-135">ボットと同様、チャネルで送信 Webhook を呼び出すには、ユーザーはその名前を **\@メンション** する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cca18-135">Just like a bot, users are required to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="cca18-136">2. 送信 Webhook HMAC トークンを確認するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="cca18-136">2. Create a method to verify the outgoing webhook HMAC token</span></span>

#### <a name="hmac-signature-for-testing-with-code-example"></a><span data-ttu-id="cca18-137">コード例を使ったテスト用の HMAC 署名</span><span class="sxs-lookup"><span data-stu-id="cca18-137">HMAC signature for testing with code example</span></span>

<span data-ttu-id="cca18-138">受信メッセージと ID の例: {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" } という SigningKeyDictionary の "contoso"。 </span><span class="sxs-lookup"><span data-stu-id="cca18-138">Using example of inbound message and id : "contoso" of  SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="cca18-139">要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。</span><span class="sxs-lookup"><span data-stu-id="cca18-139">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="cca18-140">サービスが受け取る呼び出しが本物の Teams クライアントからの呼び出しのみになるよう、認証プロトコルに常に含まれている必要がある HTTP `hmac` ヘッダーの HMAC コードが Teams によって提供されます。</span><span class="sxs-lookup"><span data-stu-id="cca18-140">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC Code in the HTTP `hmac` header that should always be  included in your authentication protocol.</span></span>

<span data-ttu-id="cca18-141">コードで、要求に含まれる HMAC 署名を常に検証する必要があり、以下のような動作が求められます。</span><span class="sxs-lookup"><span data-stu-id="cca18-141">Your code should always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="cca18-142">メッセージの要求本文から HMAC トークンを *生成* します。</span><span class="sxs-lookup"><span data-stu-id="cca18-142">*Generate* the HMAC token from the request body of the message.</span></span> <span data-ttu-id="cca18-143">ほとんどのプラットフォームでこれを行うための標準ライブラリがあります (Node.js の場合は [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) を *参照してください*。また、C\# の場合は「[Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs)」を *参照してください*)。</span><span class="sxs-lookup"><span data-stu-id="cca18-143">There are standard libraries to do this on most platforms (*see* [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or  *see* [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="cca18-144">Microsoft Teams では、標準の SHA256 HMAC 暗号化を使用します。</span><span class="sxs-lookup"><span data-stu-id="cca18-144">Microsoft Teams uses standard SHA256 HMAC cryptography .</span></span> <span data-ttu-id="cca18-145">本文を UTF8 でバイト配列に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cca18-145">You will need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="cca18-146">Teams クライアントで送信 Webhook を登録したときに **Teams によって提供された** セキュリティ トークンのバイト配列からハッシュを *計算* します。</span><span class="sxs-lookup"><span data-stu-id="cca18-146">*Compute* the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="cca18-147">以降の説明の「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="cca18-147">*See* [Create an outgoing webhook](#create-an-outgoing-webhook), below.</span></span>
* <span data-ttu-id="cca18-148">UTF-8 エンコーディングを使用してハッシュを文字列に *変換* します。</span><span class="sxs-lookup"><span data-stu-id="cca18-148">*Convert* the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="cca18-149">生成されたハッシュの文字列の値と、HTTP 要求で指定された値を *比較* します。</span><span class="sxs-lookup"><span data-stu-id="cca18-149">*Compare* the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="cca18-150">3. 成功または失敗の応答を送信するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="cca18-150">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="cca18-151">送信 Webhook からの応答は、元のメッセージと同じ返信チェーンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="cca18-151">Responses from your outgoing webhook will appear in the same reply chain as the original message.</span></span> <span data-ttu-id="cca18-152">ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行し、コードには、メッセージに応答するための 5 秒間が与えられます。この時間を過ぎると、接続がタイムアウトして終了します。</span><span class="sxs-lookup"><span data-stu-id="cca18-152">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code will have 5 seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="cca18-153">応答の例</span><span class="sxs-lookup"><span data-stu-id="cca18-153">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="cca18-154">送信 Webhook を作成する</span><span class="sxs-lookup"><span data-stu-id="cca18-154">Create an outgoing webhook</span></span>

1. <span data-ttu-id="cca18-155">適切なチームを選び、[(&#8226;&#8226;&#8226;)] ドロップダウン メニューから **[チームの管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="cca18-155">Select the appropriate team and select **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="cca18-156">ナビゲーション バーから **[アプリ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="cca18-156">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="cca18-157">ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="cca18-157">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="cca18-158">表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。</span><span class="sxs-lookup"><span data-stu-id="cca18-158">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="cca18-159">**名前** - Webhook のタイトルと @メンションのタップです。</span><span class="sxs-lookup"><span data-stu-id="cca18-159">**Name** - The webhook title and @mention tap.</span></span>
>* <span data-ttu-id="cca18-160">**コールバック URL** - JSON ペイロードを受け入れ、Teams からの POST 要求を受信する HTTPS エンドポイントです。</span><span class="sxs-lookup"><span data-stu-id="cca18-160">**Callback URL** - The HTTPS endpoint that accepts JSON payloads and will receive POST requests from Teams.</span></span>
>* <span data-ttu-id="cca18-161">**説明** - プロフィール カード、チームのレベルのアプリ ダッシュボードに表示される詳細な文字列です。</span><span class="sxs-lookup"><span data-stu-id="cca18-161">**Description** - A detailed string that will appear in the profile card and the team-level App dashboard.</span></span>
>* <span data-ttu-id="cca18-162">**プロフィール画像** (省略可能) Webhook のアプリ アイコンです。</span><span class="sxs-lookup"><span data-stu-id="cca18-162">**Profile Picture** (optional) an app icon for your webhook.</span></span>
>* <span data-ttu-id="cca18-163">ポップアップ ウィンドウの右下隅にある **[作成]** ボタンを選択すると、送信 Webhook が現在のチームのチャネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="cca18-163">Select the **Create** button from lower right corner of the pop-up window and the outgoing webhook will be added to the current team's channels.</span></span>
>* <span data-ttu-id="cca18-164">次のダイアログ ウィンドウには、[ハッシュベースのメッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) のセキュリティ トークンが表示されます。このトークンは、Teams と指定された外部サービスとの通話の認証に使用されます。</span><span class="sxs-lookup"><span data-stu-id="cca18-164">The next dialog window will display an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that will be used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="cca18-165">URL が有効で、サーバーとクライアントの認証トークンが等しい (HMAC のハンドシェイクである) 場合、チームのユーザーは送信 Webhook を使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="cca18-165">If the URL is valid and the server and client authentication tokens are equal (i.e., an HMAC handshake), the outgoing webhook will be available to the team's users.</span></span>

## <a name="code-samples"></a><span data-ttu-id="cca18-166">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="cca18-166">Code samples</span></span>

<span data-ttu-id="cca18-167">GitHub で送信 Webhook のコード サンプルを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="cca18-167">You can view outgoing webhook code samples on GitHub:</span></span>

### <a name="nodejs"></a><span data-ttu-id="cca18-168">Node.js</span><span class="sxs-lookup"><span data-stu-id="cca18-168">Node.js</span></span>

[<span data-ttu-id="cca18-169">OfficeDev/msteams-samples-outgoing-webhook-nodejs</span><span class="sxs-lookup"><span data-stu-id="cca18-169">OfficeDev/msteams-samples-outgoing-webhook-nodejs</span></span>](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a><span data-ttu-id="cca18-170">C\#</span><span class="sxs-lookup"><span data-stu-id="cca18-170">C\#</span></span>

[<span data-ttu-id="cca18-171">OfficeDev/microsoft-teams-sample-outgoing-webhook</span><span class="sxs-lookup"><span data-stu-id="cca18-171">OfficeDev/microsoft-teams-sample-outgoing-webhook</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
