---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
description: 送信 Webhook を追加する方法について説明します。
ms.topic: conceptual
ms.author: lajanuar
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: 20d30be7a35b33b94dc4a856439c51d5d0cc441c
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093254"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a><span data-ttu-id="e61db-104">送信 Webhook を使用して Teams にカスタム ボットを追加する</span><span class="sxs-lookup"><span data-stu-id="e61db-104">Add custom bots to Teams with outgoing webhooks</span></span>

## <a name="what-are-outgoing-webhooks-in-teams"></a><span data-ttu-id="e61db-105">Teams での送信 Webhook とは</span><span class="sxs-lookup"><span data-stu-id="e61db-105">What are outgoing webhooks in Teams?</span></span>

<span data-ttu-id="e61db-106">Webhook は、Teams を外部アプリと統合するための最も優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="e61db-106">Webhooks are an eminent way for Teams to integrate with external apps.</span></span> <span data-ttu-id="e61db-107">基本的に Webhook は、コールバック URL に送信される POST 要求です。</span><span class="sxs-lookup"><span data-stu-id="e61db-107">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="e61db-108">送信 Webhook を使用すると、ユーザーは Microsoft Bot Framework を介してボットを作成する完全なプロセスを実行することなく、Web サービスにメッセージ [を送信できます](https://dev.botframework.com/)。</span><span class="sxs-lookup"><span data-stu-id="e61db-108">Outgoing webhooks allow users to send messages to your web service without going through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

<span data-ttu-id="e61db-109">送信 Webhook は、Teams から JSON ペイロードを受け入れ可能な選択されたサービスにデータを送信します。</span><span class="sxs-lookup"><span data-stu-id="e61db-109">Outgoing webhook sends data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="e61db-110">送信 Webhook をチームに追加した後、ボットとして機能し、メンションを使用してチャネル内のメッセージを検索 **\@ します**。</span><span class="sxs-lookup"><span data-stu-id="e61db-110">After adding the outgoing webhooks to a team, it acts as a bot and looks for messages in channels using **\@mention**.</span></span> <span data-ttu-id="e61db-111">外部 Web サービスに通知を送信し、カードや画像を含むリッチ メッセージで応答します。</span><span class="sxs-lookup"><span data-stu-id="e61db-111">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="e61db-112">送信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="e61db-112">Outgoing webhook key features</span></span>

| <span data-ttu-id="e61db-113">機能</span><span class="sxs-lookup"><span data-stu-id="e61db-113">Feature</span></span> | <span data-ttu-id="e61db-114">説明</span><span class="sxs-lookup"><span data-stu-id="e61db-114">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="e61db-115">スコープ指定された構成</span><span class="sxs-lookup"><span data-stu-id="e61db-115">Scoped configuration</span></span>| <span data-ttu-id="e61db-116">Webhook はチームのレベルでスコープが設定されます。</span><span class="sxs-lookup"><span data-stu-id="e61db-116">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="e61db-117">送信 Webhook を追加するチームごとにセットアップ プロセスを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e61db-117">You must go through the setup process for each team where you want to add your outgoing webhook.</span></span> |
| <span data-ttu-id="e61db-118">反応性メッセージング</span><span class="sxs-lookup"><span data-stu-id="e61db-118">Reactive messaging</span></span>| <span data-ttu-id="e61db-119">ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e61db-119">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="e61db-120">現在、ユーザーはパブリック チャネル内の送信 Webhook にのみメッセージを送信できます。個人用スコープまたはプライベート スコープ内ではメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="e61db-120">Currently, users can only message an outgoing webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="e61db-121">標準の HTTP メッセージ交換</span><span class="sxs-lookup"><span data-stu-id="e61db-121">Standard HTTP message exchange</span></span>|<span data-ttu-id="e61db-122">応答は元の要求メッセージと同じチェーンに表示され、リッチ テキスト、画像、カード、絵文字など、任意のボット フレームワーク メッセージ コンテンツを含めできます。</span><span class="sxs-lookup"><span data-stu-id="e61db-122">Responses appear in the same chain as the original request message and can include any bot framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="e61db-123">送信 Webhook はカードを使用することができますが、次の場合を除き、カードアクションを使用することはできません `openURL` 。</span><span class="sxs-lookup"><span data-stu-id="e61db-123">Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="e61db-124">Teams API メソッドのサポート</span><span class="sxs-lookup"><span data-stu-id="e61db-124">Teams API method support</span></span>|<span data-ttu-id="e61db-125">送信 Webhook は、HTTP POST を Web サービスに送信し、応答を処理します。</span><span class="sxs-lookup"><span data-stu-id="e61db-125">Outgoing webhook sends an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="e61db-126">チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="e61db-126">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="creating-actionable-messages"></a><span data-ttu-id="e61db-127">操作可能なメッセージの作成</span><span class="sxs-lookup"><span data-stu-id="e61db-127">Creating actionable messages</span></span>

<span data-ttu-id="e61db-128">コネクタ カードには、カードに表示される 3 つのボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e61db-128">The connector cards include three visible buttons on the card.</span></span> <span data-ttu-id="e61db-129">各ボタンは、アクションを `potentialAction` 使用してメッセージのプロパティで定義 `ActionCard` されます。</span><span class="sxs-lookup"><span data-stu-id="e61db-129">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions.</span></span> <span data-ttu-id="e61db-130">それぞれに `ActionCard` 入力の種類、テキスト フィールド、日付の選択、または複数選択肢リストが含まれる。</span><span class="sxs-lookup"><span data-stu-id="e61db-130">Each `ActionCard` contains an input type; a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="e61db-131">各 `ActionCard` アクションには、たとえば、関連付けられたアクションがあります `HttpPOST` 。</span><span class="sxs-lookup"><span data-stu-id="e61db-131">Each `ActionCard` action has an associated action, for example, `HttpPOST`.</span></span>

<span data-ttu-id="e61db-132">コネクタ カードでは、3 種類のアクションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e61db-132">Connector cards support three types of actions:</span></span>

| <span data-ttu-id="e61db-133">アクション</span><span class="sxs-lookup"><span data-stu-id="e61db-133">Action</span></span> | <span data-ttu-id="e61db-134">説明</span><span class="sxs-lookup"><span data-stu-id="e61db-134">Description</span></span> |
| ------- | ----------- |
| `ActionCard` |<span data-ttu-id="e61db-135">1 つ以上の入力の種類と関連するアクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="e61db-135">Presents one or more input types and associated actions.</span></span>|
| `HttpPOST` | <span data-ttu-id="e61db-136">POST 要求を URL に送信します。</span><span class="sxs-lookup"><span data-stu-id="e61db-136">Sends a POST request to a URL.</span></span> |
| `OpenUri` |  <span data-ttu-id="e61db-137">URI を別のブラウザーまたはアプリで開きます。必要に応じて、オペレーティング システムに基づいて異なる URI を対象とします。</span><span class="sxs-lookup"><span data-stu-id="e61db-137">Opens a URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>|

<span data-ttu-id="e61db-138">`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e61db-138">The `ActionCard` action supports three input types:</span></span>

| <span data-ttu-id="e61db-139">入力の種類</span><span class="sxs-lookup"><span data-stu-id="e61db-139">Input type</span></span> | <span data-ttu-id="e61db-140">説明</span><span class="sxs-lookup"><span data-stu-id="e61db-140">Description</span></span> |
| ------- | ----------- |
| `TextInput` | <span data-ttu-id="e61db-141">1 行または複数行のテキスト フィールドで、オプションの長さ制限があります。</span><span class="sxs-lookup"><span data-stu-id="e61db-141">A single-line or multiline text field with an optional length limit.</span></span> |
| `DateInput` | <span data-ttu-id="e61db-142">オプションの時刻セレクターを含む日付セレクター。</span><span class="sxs-lookup"><span data-stu-id="e61db-142">A date selector with an optional time selector.</span></span> |
| `MultichoiceInput` | <span data-ttu-id="e61db-143">1 つの選択または複数の選択肢を提供する、指定された選択肢のリスト。</span><span class="sxs-lookup"><span data-stu-id="e61db-143">A specified list of choices, offering either a single selection or multiple selections.</span></span>|

<span data-ttu-id="e61db-144">`MultichoiceInput` は `style` 、完全に展開されたリストの表示を制御するプロパティをサポートします。</span><span class="sxs-lookup"><span data-stu-id="e61db-144">`MultichoiceInput` supports a `style` property that controls the display of a fully expanded list.</span></span> <span data-ttu-id="e61db-145">既定値は値 `style` によって異 `isMultiSelect` なります。</span><span class="sxs-lookup"><span data-stu-id="e61db-145">The default value of `style` depends on the `isMultiSelect` value.</span></span>

| <span data-ttu-id="e61db-146">`isMultiSelect` value</span><span class="sxs-lookup"><span data-stu-id="e61db-146">`isMultiSelect` value</span></span>  | <span data-ttu-id="e61db-147">`style` 既定値</span><span class="sxs-lookup"><span data-stu-id="e61db-147">`style` default value</span></span>  |
| --- | --- |
| <span data-ttu-id="e61db-148">`false` または指定なし</span><span class="sxs-lookup"><span data-stu-id="e61db-148">`false` or not specified</span></span> | <span data-ttu-id="e61db-149">既定のスタイルは次の値です。 `compact`</span><span class="sxs-lookup"><span data-stu-id="e61db-149">The default style is `compact`</span></span>|
| `true` | <span data-ttu-id="e61db-150">既定のスタイルは次の値です。 `expanded`</span><span class="sxs-lookup"><span data-stu-id="e61db-150">The default style is `expanded`</span></span> |

> [!NOTE]
> * <span data-ttu-id="e61db-151">複数選択リストをコンパクト なスタイルで表示する場合は、両方 `"isMultiSelect": true` `"style": true` を入力します。</span><span class="sxs-lookup"><span data-stu-id="e61db-151">Enter both `"isMultiSelect": true` and `"style": true`, if you want the multi-select list to be displayed in a compact style.</span></span>
> * <span data-ttu-id="e61db-152">Teams で `compact` プロパティを `style` 選択する方法は、Microsoft Outlook でプロパティを選択する場合 `normal` `style` と同じです。</span><span class="sxs-lookup"><span data-stu-id="e61db-152">Selecting `compact` for the `style` property in Teams is the same as selecting `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="e61db-153">Webhook は、365 Officeカードとアダプティブ カードのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="e61db-153">Webhooks support only Office 365 message back cards and adaptive cards.</span></span>

<span data-ttu-id="e61db-154">コネクタ カードのアクションに関するその他の詳細については、操作 **[可能](/outlook/actionable-messages/card-reference#actions)** なメッセージ カード リファレンスの「アクション」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e61db-154">For all other details about connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="adding-outgoing-webhooks-to-your-app"></a><span data-ttu-id="e61db-155">送信 Webhook をアプリに追加する</span><span class="sxs-lookup"><span data-stu-id="e61db-155">Adding outgoing webhooks to your app</span></span>

<span data-ttu-id="e61db-156">**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="e61db-156">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="e61db-157">**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="e61db-157">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="e61db-158">1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する</span><span class="sxs-lookup"><span data-stu-id="e61db-158">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="e61db-159">サービスは、標準の Azure Bot Service メッセージング スキーマでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="e61db-159">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="e61db-160">ボット フレームワーク コネクタは [、AZURE Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理するサービスを支援する RESTful サービスです。</span><span class="sxs-lookup"><span data-stu-id="e61db-160">The bot framework connector is a RESTful service that empowers your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="e61db-161">[Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="e61db-161">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="e61db-162">[「Azure Bot Service について」も参照してください](/azure/bot-service/bot-service-overview-introduction)。</span><span class="sxs-lookup"><span data-stu-id="e61db-162">See also [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>


<span data-ttu-id="e61db-163">送信 Webhook はレベルにスコープが設定され、すべてのチーム `team` メンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e61db-163">Outgoing webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="e61db-164">ボットと同様に、ユーザーは送信 **\@** Webhook の名前をメンションしてチャネルで呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="e61db-164">Just like a bot, users need to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="e61db-165">2. 送信 Webhook HMAC トークンを確認するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="e61db-165">2. Create a method to verify the outgoing webhook HMAC token</span></span>

#### <a name="hmac-signature-for-testing-with-code-example"></a><span data-ttu-id="e61db-166">コード例を使ったテスト用の HMAC 署名</span><span class="sxs-lookup"><span data-stu-id="e61db-166">HMAC signature for testing with code example</span></span>

<span data-ttu-id="e61db-167">受信メッセージと ID の例を使用: {"contoso" の SigningKeyDictionary の "contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。</span><span class="sxs-lookup"><span data-stu-id="e61db-167">Using example of inbound message and id: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="e61db-168">要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。</span><span class="sxs-lookup"><span data-stu-id="e61db-168">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="e61db-169">サービスが実際の Teams クライアントからの呼び出しのみを受信するために、Teams は HTTP ヘッダーに HMAC コードを提供 `hmac` します。</span><span class="sxs-lookup"><span data-stu-id="e61db-169">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` header.</span></span> <span data-ttu-id="e61db-170">常に認証プロトコルにコードを含める。</span><span class="sxs-lookup"><span data-stu-id="e61db-170">Always included the code in your authentication protocol.</span></span>

<span data-ttu-id="e61db-171">コードでは、要求に含まれる HMAC 署名を常に検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e61db-171">Your code must always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="e61db-172">メッセージの要求本文から HMAC トークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="e61db-172">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="e61db-173">ほとんどのプラットフォームでこれを行う標準的なライブラリがあります (Node.jsの[](https://nodejs.org/api/crypto.html#crypto_crypto)Crypto を参照するか[、C 用の Teams Webhook サンプル](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs)を参照してください \# )。</span><span class="sxs-lookup"><span data-stu-id="e61db-173">There are standard libraries to do this on most platforms (see [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="e61db-174">Microsoft Teams では、標準的な SHA256 HMAC 暗号化を使用します。</span><span class="sxs-lookup"><span data-stu-id="e61db-174">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="e61db-175">UTF8 で本文をバイト配列に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e61db-175">You need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="e61db-176">Teams クライアントで送信 Webhook を登録したときに Teams によって提供されたセキュリティ トークンのバイト配列からハッシュを **計算** します。</span><span class="sxs-lookup"><span data-stu-id="e61db-176">Compute the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="e61db-177">「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e61db-177">See [Create an outgoing webhook](#create-an-outgoing-webhook).</span></span>
* <span data-ttu-id="e61db-178">UTF-8 エンコーディングを使用してハッシュを文字列に変換します。</span><span class="sxs-lookup"><span data-stu-id="e61db-178">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="e61db-179">生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。</span><span class="sxs-lookup"><span data-stu-id="e61db-179">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="e61db-180">3. 成功または失敗の応答を送信するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="e61db-180">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="e61db-181">送信 Webhook からの応答は、元のメッセージと同じ返信チェーンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e61db-181">Responses from your outgoing webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="e61db-182">ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行し、コードは接続がタイム アウトして終了する前にメッセージに応答するために 5 秒を取得します。</span><span class="sxs-lookup"><span data-stu-id="e61db-182">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="e61db-183">応答の例</span><span class="sxs-lookup"><span data-stu-id="e61db-183">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="e61db-184">送信 Webhook を作成する</span><span class="sxs-lookup"><span data-stu-id="e61db-184">Create an outgoing webhook</span></span>

1. <span data-ttu-id="e61db-185">適切なチームを選択し、(&#8226;&#8226;&#8226;) ドロップダウン メニューから [チームの管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e61db-185">Select the appropriate team and choose **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="e61db-186">ナビゲーション バーから **[アプリ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="e61db-186">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="e61db-187">ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e61db-187">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="e61db-188">表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。</span><span class="sxs-lookup"><span data-stu-id="e61db-188">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="e61db-189">**名前** - Webhook のタイトルと @メンションのタップです。</span><span class="sxs-lookup"><span data-stu-id="e61db-189">**Name** - The webhook title and @mention tap.</span></span>
>* <span data-ttu-id="e61db-190">**コールバック URL** - JSON ペイロードを受け入れ、Teams から POST 要求を受信する HTTPS エンドポイント。</span><span class="sxs-lookup"><span data-stu-id="e61db-190">**Callback URL** - The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
>* <span data-ttu-id="e61db-191">**説明** - プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列。</span><span class="sxs-lookup"><span data-stu-id="e61db-191">**Description** - A detailed string that appear in the profile card and the team-level App dashboard.</span></span>
>* <span data-ttu-id="e61db-192">**Webhook** のオプションのアプリ アイコンのプロファイル画像。</span><span class="sxs-lookup"><span data-stu-id="e61db-192">**Profile Picture** an optional app icon for your webhook.</span></span>
>* <span data-ttu-id="e61db-193">ポップアップ ウィンドウ **の** 右下隅から [作成] ボタンを選択すると、送信 Webhook が現在のチームのチャネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="e61db-193">Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.</span></span>
>* <span data-ttu-id="e61db-194">次のダイアログ ウィンドウには、Teams と指定された外部サービスとの間の呼び出しを認証するために使用されるハッシュベースのメッセージ認証コード [(HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) セキュリティ トークンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e61db-194">The next dialog window displays an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that is used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="e61db-195">送信 Webhook は、URL が有効で、サーバー認証トークンとクライアント認証トークンが等しい場合 (HMAC ハンドシェイクなど) の場合にのみ、チームのユーザーが使用できます。</span><span class="sxs-lookup"><span data-stu-id="e61db-195">The outgoing webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal for example, an HMAC handshake.</span></span>

## <a name="code-samples"></a><span data-ttu-id="e61db-196">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="e61db-196">Code samples</span></span>

<span data-ttu-id="e61db-197">GitHub で送信 Webhook のコード サンプルを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="e61db-197">You can view outgoing webhook code samples on GitHub:</span></span>

### <a name="nodejs"></a><span data-ttu-id="e61db-198">Node.js</span><span class="sxs-lookup"><span data-stu-id="e61db-198">Node.js</span></span>

[<span data-ttu-id="e61db-199">OfficeDev/msteams-samples-outgoing-webhook-nodejs</span><span class="sxs-lookup"><span data-stu-id="e61db-199">OfficeDev/msteams-samples-outgoing-webhook-nodejs</span></span>](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a><span data-ttu-id="e61db-200">C\#</span><span class="sxs-lookup"><span data-stu-id="e61db-200">C\#</span></span>

[<span data-ttu-id="e61db-201">OfficeDev/microsoft-teams-sample-outgoing-webhook</span><span class="sxs-lookup"><span data-stu-id="e61db-201">OfficeDev/microsoft-teams-sample-outgoing-webhook</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
