---
title: 送信 web フックを使用して Microsoft Teams にカスタムボットを追加する
author: laujan
description: ''
keywords: teams タブ送信 webhook *
ms.topic: conceptual
ms.author: laujan
ms.openlocfilehash: 4570e597484494f05f4e18b4d29746da96c73661
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674814"
---
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a><span data-ttu-id="ae377-103">送信 web フックを使用して Microsoft Teams にカスタムボットを追加する</span><span class="sxs-lookup"><span data-stu-id="ae377-103">Add custom bots to Microsoft Teams with outgoing webhooks</span></span>

## <a name="what-are-outgoing-webhooks-in-teams"></a><span data-ttu-id="ae377-104">Teams での送信 web フックとは</span><span class="sxs-lookup"><span data-stu-id="ae377-104">What are outgoing webhooks in Teams?</span></span>

<span data-ttu-id="ae377-105">Webhooks は、Teams が外部アプリと統合するための便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="ae377-105">Webhooks are a great way for Teams to integrate with external apps.</span></span> <span data-ttu-id="ae377-106">Webhook は基本的に、コールバック URL に送信される POST 要求です。</span><span class="sxs-lookup"><span data-stu-id="ae377-106">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="ae377-107">Teams では、送信用の webhook により、ユーザーが web サービスにメッセージを送信できるようにするための簡単な方法が提供されます。これにより、 [Microsoft bot フレームワーク](https://dev.botframework.com/)を使用してボットを作成する完全なプロセスを実行する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="ae377-107">In Teams, outgoing webhooks provide a simple way to allow users to send messages to your web service without having to go through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="ae377-108">送信 web フックは、JSON ペイロードを受け入れることができる、選択された任意のサービスに Teams からのデータを投稿します。</span><span class="sxs-lookup"><span data-stu-id="ae377-108">Outgoing webhooks post data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="ae377-109">送信 webhook がチームに追加されると、ボットのように機能し、 \*\* \@メンション\*\*を使用したメッセージのチャネルをリッスンし、外部 web サービスに通知を送信し、カードや画像を含むことができるリッチメッセージに応答します。</span><span class="sxs-lookup"><span data-stu-id="ae377-109">Once an outgoing webhook is added to a team, it acts like bot, listening in channels for messages using **\@mention**, sending notifications to external web services, and responding with rich messages that can include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="ae377-110">送信 webhook キー機能</span><span class="sxs-lookup"><span data-stu-id="ae377-110">Outgoing webhook key features</span></span>

| <span data-ttu-id="ae377-111">機能</span><span class="sxs-lookup"><span data-stu-id="ae377-111">Feature</span></span> | <span data-ttu-id="ae377-112">説明</span><span class="sxs-lookup"><span data-stu-id="ae377-112">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="ae377-113">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="ae377-113">Scoped Configuration</span></span>| <span data-ttu-id="ae377-114">Webhooks はチームレベルでスコープ設定されます。</span><span class="sxs-lookup"><span data-stu-id="ae377-114">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="ae377-115">送信 webhook を追加する各チームのセットアッププロセスを進める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae377-115">You’ll need to go through the setup process for each team you want to add your outgoing webhook to.</span></span> |
| <span data-ttu-id="ae377-116">リアクティブメッセージング</span><span class="sxs-lookup"><span data-stu-id="ae377-116">Reactive Messaging</span></span>| <span data-ttu-id="ae377-117">ユーザーは、メッセージを受信するために webhook に @mention を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae377-117">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="ae377-118">現在ユーザーは、個人またはプライベートのスコープ内ではなく、パブリックチャネルでの送信 webhook のみをメッセージできます。</span><span class="sxs-lookup"><span data-stu-id="ae377-118">Currently users can only message an outgoing webhook in public channels and not within the personal or private scope</span></span> |
|<span data-ttu-id="ae377-119">標準の HTTP メッセージ交換</span><span class="sxs-lookup"><span data-stu-id="ae377-119">Standard HTTP message exchange</span></span>|<span data-ttu-id="ae377-120">応答は元の要求メッセージと同じチェーンに表示され、任意の Bot フレームワークメッセージコンテンツ (リッチテキスト、画像、カード、および絵文字) を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="ae377-120">Responses will appear in the same chain as the original request message and can include any Bot Framework message content (rich text, images, cards, and emojis).</span></span> <span data-ttu-id="ae377-121">**注**: 送信 web フックはカードを使用することができますが、を`openURL`除くカードアクションを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="ae377-121">**Note**: Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="ae377-122">Teams API メソッドのサポート</span><span class="sxs-lookup"><span data-stu-id="ae377-122">Teams API method support</span></span>|<span data-ttu-id="ae377-123">Teams では、送信 web フックは HTTP POST を web サービスに送信し、応答を処理します。</span><span class="sxs-lookup"><span data-stu-id="ae377-123">In Teams, outgoing webhooks send an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="ae377-124">チーム内の名簿やチャネルのリストを取得するなど、他の Api にはアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="ae377-124">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a><span data-ttu-id="ae377-125">アプリに送信 webhook 処理を追加する</span><span class="sxs-lookup"><span data-stu-id="ae377-125">Adding outgoing webhook processing to your app</span></span>

<span data-ttu-id="ae377-126">**シナリオ**: Teams チャネルデータベースサーバーで、アプリに変更状態通知をプッシュします。</span><span class="sxs-lookup"><span data-stu-id="ae377-126">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="ae377-127">**例**: Office 365 テナント全体で TEAMS の HR ユーザーによって従業員のレコードに対して行われたすべての CRUD 操作を追跡する基幹業務アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="ae377-127">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="ae377-128">1. JSON ペイロードを使用して POST 要求を受け入れて処理するためのアプリのサーバー上で URL を作成する</span><span class="sxs-lookup"><span data-stu-id="ae377-128">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="ae377-129">サービスは、標準の Azure bot サービスメッセージングスキーマでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="ae377-129">Your service will receive messages in the standard Azure bot service messaging schema.</span></span> <span data-ttu-id="ae377-130">Bot フレームワークコネクタは、 [Azure Bot サービス API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)で文書化されているように、サービスが HTTPS プロトコルを使用して JSON 形式のメッセージのインターチェンジを処理できるようにする RESTful サービスです。</span><span class="sxs-lookup"><span data-stu-id="ae377-130">The Bot Framework connector is a RESTful service that enables your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="ae377-131">または、[Microsoft Bot Framework SDK] をフォローしてメッセージの処理と解析を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="ae377-131">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="ae377-132">[Azure Bot サービスについ](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)て*も参照してください*。  </span><span class="sxs-lookup"><span data-stu-id="ae377-132">*See also*  [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).</span></span>

<span data-ttu-id="ae377-133">送信 web フックは、 `team`レベルに設定され、チームのすべてのメンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ae377-133">Outgoing webhooks are scoped to the `team` level and are visible to all members of the team.</span></span> <span data-ttu-id="ae377-134">Bot と同様に、ユーザー ae は、チャネルで呼び出しを行うために、送信 webhook の名前を\*\* \@言及\*\*する必要がありました。</span><span class="sxs-lookup"><span data-stu-id="ae377-134">Just like a bot, users ae required to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="ae377-135">2. 送信 webhook HMAC トークンを確認するメソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="ae377-135">2. Create a method to verify the outgoing webhook HMAC token</span></span>

<span data-ttu-id="ae377-136">サービスが実際の Teams クライアントからの呼び出しのみを受信できるようにするために、Teams では`hmac` 、認証プロトコルに常に含める必要がある HMAC コードが HTTP ヘッダーに用意されています。</span><span class="sxs-lookup"><span data-stu-id="ae377-136">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC Code in the HTTP `hmac` header that should always be  included in your authentication protocol.</span></span>

<span data-ttu-id="ae377-137">コードでは、要求に含まれている HMAC 署名を常に検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae377-137">Your code should always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="ae377-138">メッセージの要求本文から HMAC トークンを*生成*します。</span><span class="sxs-lookup"><span data-stu-id="ae377-138">*Generate* the HMAC token from the request body of the message.</span></span> <span data-ttu-id="ae377-139">ほとんどのプラットフォームでこれを行うための標準ライブラリがあります (node.js の[Crypto](https://nodejs.org/api/crypto.html#crypto_crypto)を*参照*してください)。または *「* [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ae377-139">There are standard libraries to do this on most platforms (*see* [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or  *see* [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="ae377-140">Microsoft Teams では、標準の SHA256 HMAC 暗号化を使用します。</span><span class="sxs-lookup"><span data-stu-id="ae377-140">Microsoft Teams uses standard SHA256 HMAC cryptography .</span></span> <span data-ttu-id="ae377-141">本文を UTF8 でバイト配列に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ae377-141">You will need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="ae377-142">Teams クライアントで送信 webhook を登録したときに**teams によって提供され**たセキュリティトークンのバイト配列からのハッシュを*計算*します。</span><span class="sxs-lookup"><span data-stu-id="ae377-142">*Compute* the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="ae377-143">下記の「[送信 webhook を作成する](#create-an-outgoing-webhook) *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="ae377-143">*See* [Create an outgoing webhook](#create-an-outgoing-webhook), below.</span></span>
* <span data-ttu-id="ae377-144">UTF-8 エンコードを使用して、ハッシュを文字列に*変換*します。</span><span class="sxs-lookup"><span data-stu-id="ae377-144">*Convert* the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="ae377-145">生成されたハッシュの文字列値と、HTTP 要求で指定された値を*比較*します。</span><span class="sxs-lookup"><span data-stu-id="ae377-145">*Compare* the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="ae377-146">3. 成功または失敗応答を送信するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="ae377-146">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="ae377-147">送信した webhook からの応答は、元のメッセージと同じ応答チェーンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ae377-147">Responses from your outgoing webhook will appear in the same reply chain as the original message.</span></span> <span data-ttu-id="ae377-148">ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行し、コードには、接続がタイムアウトして終了する前にメッセージに応答するための5秒の時間が与えられます。</span><span class="sxs-lookup"><span data-stu-id="ae377-148">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code will have 5 seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="ae377-149">応答の例</span><span class="sxs-lookup"><span data-stu-id="ae377-149">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="ae377-150">送信 webhook を作成する</span><span class="sxs-lookup"><span data-stu-id="ae377-150">Create an outgoing webhook</span></span>

1. <span data-ttu-id="ae377-151">適切なチームを選択し、[(&#8226;&#8226;&#8226;)] ドロップダウンメニューから [**チームの管理**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ae377-151">Select the appropriate team and select **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="ae377-152">ナビゲーションバーから [**アプリ**] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="ae377-152">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="ae377-153">ウィンドウの右下隅から、[**送信 webhook を作成する**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ae377-153">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="ae377-154">表示されるポップアップウィンドウで、必要なフィールドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ae377-154">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="ae377-155">**Name** -webhook のタイトルと @mention タップを指定します。</span><span class="sxs-lookup"><span data-stu-id="ae377-155">**Name** - The webhook title and @mention tap.</span></span>
>* <span data-ttu-id="ae377-156">**コールバック URL** -JSON ペイロードを受け入れ、Teams からの POST 要求を受け取る HTTPS エンドポイント。</span><span class="sxs-lookup"><span data-stu-id="ae377-156">**Callback URL** - The HTTPS endpoint that accepts JSON payloads and will receive POST requests from Teams.</span></span>
>* <span data-ttu-id="ae377-157">**Description** -プロファイルカードおよびチームレベルのアプリダッシュボードに表示される詳細な文字列。</span><span class="sxs-lookup"><span data-stu-id="ae377-157">**Description** - A detailed string that will appear in the profile card and the team-level App dashboard.</span></span>
>* <span data-ttu-id="ae377-158">**プロファイル画像**(省略可能) webhook のアプリアイコン。</span><span class="sxs-lookup"><span data-stu-id="ae377-158">**Profile Picture** (optional) an app icon for your webhook.</span></span>
>* <span data-ttu-id="ae377-159">ポップアップウィンドウの右下隅から [**作成**] ボタンを選択すると、送信 webhook が現在のチームのチャネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="ae377-159">Select the **Create** button from lower right corner of the pop-up window and the outgoing webhook will be added to the current team's channels.</span></span>
>* <span data-ttu-id="ae377-160">次のダイアログウィンドウには、Teams と指定された外部サービスとの間の通話の認証に使用される[ハッシュベースのメッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)セキュリティトークンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ae377-160">The next dialog window will display an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that will be used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="ae377-161">URL が有効であり、サーバーとクライアントの認証トークンが等しい (つまり HMAC ハンドシェイクである) 場合、送信された webhook はチームのユーザーが使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ae377-161">If the URL is valid and the server and client authentication tokens are equal (i.e., an HMAC handshake), the outgoing webhook will be available to the team's users.</span></span>

## <a name="code-samples"></a><span data-ttu-id="ae377-162">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="ae377-162">Code samples</span></span>

<span data-ttu-id="ae377-163">GitHub で送信 webhook のコードサンプルを表示できます。</span><span class="sxs-lookup"><span data-stu-id="ae377-163">You can view outgoing webhook code samples on GitHub:</span></span>

### <a name="nodejs"></a><span data-ttu-id="ae377-164">Node.js</span><span class="sxs-lookup"><span data-stu-id="ae377-164">Node.js</span></span>

[<span data-ttu-id="ae377-165">OfficeDev/msteams-サンプル--webhook-nodejs</span><span class="sxs-lookup"><span data-stu-id="ae377-165">OfficeDev/msteams-samples-outgoing-webhook-nodejs</span></span>](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a><span data-ttu-id="ae377-166">40u-c\#</span><span class="sxs-lookup"><span data-stu-id="ae377-166">C\#</span></span>

[<span data-ttu-id="ae377-167">OfficeDev/microsoft-teams-サンプル-webhook</span><span class="sxs-lookup"><span data-stu-id="ae377-167">OfficeDev/microsoft-teams-sample-outgoing-webhook</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
