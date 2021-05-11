---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
description: 送信 Webhook を追加する方法について説明します。
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams タブ送信 webhook アクション可能メッセージ verify webhook
ms.openlocfilehash: cfa8bd550eaf1f198b83cdcc1ee699c75ac1d34d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020212"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a><span data-ttu-id="aa83b-104">送信 webhooks を使用してTeamsボットを追加する</span><span class="sxs-lookup"><span data-stu-id="aa83b-104">Add custom bots to Teams with outgoing webhooks</span></span>

## <a name="what-are-outgoing-webhooks-in-teams"></a><span data-ttu-id="aa83b-105">Teams での送信 Webhook とは</span><span class="sxs-lookup"><span data-stu-id="aa83b-105">What are outgoing webhooks in Teams?</span></span>

<span data-ttu-id="aa83b-106">Webhooks は、外部アプリと統合するTeams優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="aa83b-106">Webhooks are an eminent way for Teams to integrate with external apps.</span></span> <span data-ttu-id="aa83b-107">基本的に Webhook は、コールバック URL に送信される POST 要求です。</span><span class="sxs-lookup"><span data-stu-id="aa83b-107">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="aa83b-108">送信 Webhooks を使用すると、ユーザーは web サービスを介してボットを作成する完全なプロセスを実行せずに、web サービスに[メッセージを送信Microsoft Bot Framework。](https://dev.botframework.com/)</span><span class="sxs-lookup"><span data-stu-id="aa83b-108">Outgoing webhooks allow users to send messages to your web service without going through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

<span data-ttu-id="aa83b-109">送信 Webhook は、JSON ペイロードを受けTeamsできる選択したサービスにデータを送信します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-109">Outgoing webhook sends data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="aa83b-110">送信 Webhook をチームに追加した後、ボットとして機能し、メンションを使用してチャネル内のメッセージを検索 **\@ します**。</span><span class="sxs-lookup"><span data-stu-id="aa83b-110">After adding the outgoing webhooks to a team, it acts as a bot and looks for messages in channels using **\@mention**.</span></span> <span data-ttu-id="aa83b-111">外部 Web サービスに通知を送信し、カードや画像を含むリッチ メッセージで応答します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-111">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="aa83b-112">送信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="aa83b-112">Outgoing webhook key features</span></span>

| <span data-ttu-id="aa83b-113">機能</span><span class="sxs-lookup"><span data-stu-id="aa83b-113">Feature</span></span> | <span data-ttu-id="aa83b-114">説明</span><span class="sxs-lookup"><span data-stu-id="aa83b-114">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="aa83b-115">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="aa83b-115">Scoped configuration</span></span>| <span data-ttu-id="aa83b-116">Webhook はチームのレベルでスコープが設定されます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-116">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="aa83b-117">送信 Webhook を追加するチームごとにセットアップ プロセスを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa83b-117">You must go through the setup process for each team where you want to add your outgoing webhook.</span></span> |
| <span data-ttu-id="aa83b-118">反応性メッセージング</span><span class="sxs-lookup"><span data-stu-id="aa83b-118">Reactive messaging</span></span>| <span data-ttu-id="aa83b-119">ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa83b-119">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="aa83b-120">現在、ユーザーはパブリック チャネルでのみ送信 Webhook にメッセージを送信できます。個人またはプライベート スコープ内ではメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-120">Currently, users can only message an outgoing webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="aa83b-121">標準の HTTP メッセージ交換</span><span class="sxs-lookup"><span data-stu-id="aa83b-121">Standard HTTP message exchange</span></span>|<span data-ttu-id="aa83b-122">応答は元の要求メッセージと同じチェーンに表示され、リッチ テキスト、画像、カード、絵文字など、任意のボット フレームワーク メッセージ コンテンツを含めできます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-122">Responses appear in the same chain as the original request message and can include any bot framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="aa83b-123">送信 Webhooks はカードを使用することができますが、 を除き、カードアクションを使用することはできません `openURL` 。</span><span class="sxs-lookup"><span data-stu-id="aa83b-123">Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="aa83b-124">Teams API メソッドのサポート</span><span class="sxs-lookup"><span data-stu-id="aa83b-124">Teams API method support</span></span>|<span data-ttu-id="aa83b-125">送信 Webhook は HTTP POST を Web サービスに送信し、応答を処理します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-125">Outgoing webhook sends an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="aa83b-126">チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="aa83b-126">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="creating-actionable-messages"></a><span data-ttu-id="aa83b-127">操作可能なメッセージの作成</span><span class="sxs-lookup"><span data-stu-id="aa83b-127">Creating actionable messages</span></span>

<span data-ttu-id="aa83b-128">コネクタ カードには、カードに 3 つの表示ボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-128">The connector cards include three visible buttons on the card.</span></span> <span data-ttu-id="aa83b-129">各ボタンは、アクション `potentialAction` を使用してメッセージのプロパティで定義 `ActionCard` されます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-129">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions.</span></span> <span data-ttu-id="aa83b-130">それぞれに、入力タイプ、テキスト フィールド、日付ピッカー、または複数選択肢 `ActionCard` リストが含まれる。</span><span class="sxs-lookup"><span data-stu-id="aa83b-130">Each `ActionCard` contains an input type; a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="aa83b-131">各 `ActionCard` アクションには、たとえば、関連付けられたアクションがあります `HttpPOST` 。</span><span class="sxs-lookup"><span data-stu-id="aa83b-131">Each `ActionCard` action has an associated action, for example, `HttpPOST`.</span></span>

<span data-ttu-id="aa83b-132">コネクタ カードでは、3 種類のアクションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="aa83b-132">Connector cards support three types of actions:</span></span>

| <span data-ttu-id="aa83b-133">アクション</span><span class="sxs-lookup"><span data-stu-id="aa83b-133">Action</span></span> | <span data-ttu-id="aa83b-134">説明</span><span class="sxs-lookup"><span data-stu-id="aa83b-134">Description</span></span> |
| ------- | ----------- |
| `ActionCard` |<span data-ttu-id="aa83b-135">1 つ以上の入力型と関連付けられたアクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-135">Presents one or more input types and associated actions.</span></span>|
| `HttpPOST` | <span data-ttu-id="aa83b-136">POST 要求を URL に送信します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-136">Sends a POST request to a URL.</span></span> |
| `OpenUri` |  <span data-ttu-id="aa83b-137">別のブラウザーまたはアプリで URI を開き、必要に応じてオペレーティング システムに基づいてさまざまな URI を対象とします。</span><span class="sxs-lookup"><span data-stu-id="aa83b-137">Opens a URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>|

<span data-ttu-id="aa83b-138">`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="aa83b-138">The `ActionCard` action supports three input types:</span></span>

| <span data-ttu-id="aa83b-139">入力の種類</span><span class="sxs-lookup"><span data-stu-id="aa83b-139">Input type</span></span> | <span data-ttu-id="aa83b-140">説明</span><span class="sxs-lookup"><span data-stu-id="aa83b-140">Description</span></span> |
| ------- | ----------- |
| `TextInput` | <span data-ttu-id="aa83b-141">オプションの長さ制限を持つ単一行または複数行のテキスト フィールド。</span><span class="sxs-lookup"><span data-stu-id="aa83b-141">A single-line or multiline text field with an optional length limit.</span></span> |
| `DateInput` | <span data-ttu-id="aa83b-142">オプションのタイム セレクターを含む日付セレクター。</span><span class="sxs-lookup"><span data-stu-id="aa83b-142">A date selector with an optional time selector.</span></span> |
| `MultichoiceInput` | <span data-ttu-id="aa83b-143">1 つの選択範囲または複数の選択項目を提供する、指定された選択肢の一覧。</span><span class="sxs-lookup"><span data-stu-id="aa83b-143">A specified list of choices, offering either a single selection or multiple selections.</span></span>|

<span data-ttu-id="aa83b-144">`MultichoiceInput` 完全に `style` 展開されたリストの表示を制御するプロパティをサポートします。</span><span class="sxs-lookup"><span data-stu-id="aa83b-144">`MultichoiceInput` supports a `style` property that controls the display of a fully expanded list.</span></span> <span data-ttu-id="aa83b-145">既定値は、 `style` 値によって異 `isMultiSelect` なります。</span><span class="sxs-lookup"><span data-stu-id="aa83b-145">The default value of `style` depends on the `isMultiSelect` value.</span></span>

| <span data-ttu-id="aa83b-146">`isMultiSelect` value</span><span class="sxs-lookup"><span data-stu-id="aa83b-146">`isMultiSelect` value</span></span>  | <span data-ttu-id="aa83b-147">`style` 既定値</span><span class="sxs-lookup"><span data-stu-id="aa83b-147">`style` default value</span></span>  |
| --- | --- |
| <span data-ttu-id="aa83b-148">`false` または指定なし</span><span class="sxs-lookup"><span data-stu-id="aa83b-148">`false` or not specified</span></span> | <span data-ttu-id="aa83b-149">既定のスタイルは次の値です。 `compact`</span><span class="sxs-lookup"><span data-stu-id="aa83b-149">The default style is `compact`</span></span>|
| `true` | <span data-ttu-id="aa83b-150">既定のスタイルは次の値です。 `expanded`</span><span class="sxs-lookup"><span data-stu-id="aa83b-150">The default style is `expanded`</span></span> |

> [!NOTE]
> * <span data-ttu-id="aa83b-151">複数選択リストをコンパクト なスタイルで表示する場合は、両方 `"isMultiSelect": true` `"style": true` を入力します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-151">Enter both `"isMultiSelect": true` and `"style": true`, if you want the multi-select list to be displayed in a compact style.</span></span>
> * <span data-ttu-id="aa83b-152">[プロパティ `compact` の選択] `style` Teamsは、Microsoft のプロパティを選択する場合と同 `normal` `style` Outlook。</span><span class="sxs-lookup"><span data-stu-id="aa83b-152">Selecting `compact` for the `style` property in Teams is the same as selecting `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="aa83b-153">Webhooks は、Office 365カードとアダプティブ カードのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="aa83b-153">Webhooks support only Office 365 message back cards and adaptive cards.</span></span>

<span data-ttu-id="aa83b-154">コネクタ カードのアクションに関するその他の詳細については、「 **[アクション可能](/outlook/actionable-messages/card-reference#actions)** なメッセージ カードリファレンスのアクション」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="aa83b-154">For all other details about connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="adding-outgoing-webhooks-to-your-app"></a><span data-ttu-id="aa83b-155">送信 Webhook をアプリに追加する</span><span class="sxs-lookup"><span data-stu-id="aa83b-155">Adding outgoing webhooks to your app</span></span>

<span data-ttu-id="aa83b-156">**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="aa83b-156">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="aa83b-157">**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="aa83b-157">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="aa83b-158">1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する</span><span class="sxs-lookup"><span data-stu-id="aa83b-158">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="aa83b-159">サービスは、標準の Azure ボット サービス メッセージング スキーマでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-159">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="aa83b-160">ボット フレームワーク コネクタは RESTful サービスで [、Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理できます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-160">The bot framework connector is a RESTful service that empowers your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="aa83b-161">[Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-161">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="aa83b-162">「Azure [Bot Service について」も参照してください](/azure/bot-service/bot-service-overview-introduction)。</span><span class="sxs-lookup"><span data-stu-id="aa83b-162">See also [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>


<span data-ttu-id="aa83b-163">送信 Webhook はレベルにスコープが設定され `team` 、すべてのチーム メンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-163">Outgoing webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="aa83b-164">ボットと同様に、ユーザーは送信 **\@** Webhook の名前を指定してチャネルで呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa83b-164">Just like a bot, users need to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="aa83b-165">2. 送信 Webhook HMAC トークンを確認するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="aa83b-165">2. Create a method to verify the outgoing webhook HMAC token</span></span>

#### <a name="hmac-signature-for-testing-with-code-example"></a><span data-ttu-id="aa83b-166">コード例を使ったテスト用の HMAC 署名</span><span class="sxs-lookup"><span data-stu-id="aa83b-166">HMAC signature for testing with code example</span></span>

<span data-ttu-id="aa83b-167">受信メッセージと id の使用例: {"contoso"の SigningKeyDictionary の "contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。</span><span class="sxs-lookup"><span data-stu-id="aa83b-167">Using example of inbound message and id: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="aa83b-168">要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-168">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="aa83b-169">サービスが実際のクライアントからのみ呼び出しを受信Teams、http ヘッダー Teams HMAC コードを提供 `hmac` します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-169">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` header.</span></span> <span data-ttu-id="aa83b-170">常に認証プロトコルにコードを含める。</span><span class="sxs-lookup"><span data-stu-id="aa83b-170">Always included the code in your authentication protocol.</span></span>

<span data-ttu-id="aa83b-171">コードでは、要求に含まれる HMAC 署名を常に検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa83b-171">Your code must always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="aa83b-172">メッセージの要求本文から HMAC トークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-172">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="aa83b-173">ほとんどのプラットフォームでこれを行う標準的なライブラリがあります (「Crypto [for](https://nodejs.org/api/crypto.html#crypto_crypto) Node.js [Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) sample for C」を参照Teams参照 \# )。</span><span class="sxs-lookup"><span data-stu-id="aa83b-173">There are standard libraries to do this on most platforms (see [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="aa83b-174">Microsoft Teams SHA256 HMAC 暗号化を使用します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-174">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="aa83b-175">UTF8 で本文をバイト配列に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa83b-175">You need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="aa83b-176">Teams クライアントで送信 Webhook を登録したときに Teams によって提供されたセキュリティ トークンのバイト配列からハッシュを **計算** します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-176">Compute the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="aa83b-177">「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="aa83b-177">See [Create an outgoing webhook](#create-an-outgoing-webhook).</span></span>
* <span data-ttu-id="aa83b-178">UTF-8 エンコーディングを使用してハッシュを文字列に変換します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-178">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="aa83b-179">生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-179">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="aa83b-180">3. 成功または失敗の応答を送信するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="aa83b-180">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="aa83b-181">送信 Webhook からの応答は、元のメッセージと同じ返信チェーンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-181">Responses from your outgoing webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="aa83b-182">ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行し、接続が切れ、終了する前にコードがメッセージに応答するために 5 秒を取得します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-182">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="aa83b-183">応答の例</span><span class="sxs-lookup"><span data-stu-id="aa83b-183">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="aa83b-184">送信 Webhook を作成する</span><span class="sxs-lookup"><span data-stu-id="aa83b-184">Create an outgoing webhook</span></span>

1. <span data-ttu-id="aa83b-185">適切なチームを選択し **、[チーム** の管理] ([&#8226;&#8226;&#8226;] ドロップダウン メニューから [チームの管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-185">Select the appropriate team and choose **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="aa83b-186">ナビゲーション バーから **[アプリ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-186">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="aa83b-187">ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa83b-187">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="aa83b-188">表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。</span><span class="sxs-lookup"><span data-stu-id="aa83b-188">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="aa83b-189">**名前** - Webhook のタイトルと @メンションのタップです。</span><span class="sxs-lookup"><span data-stu-id="aa83b-189">**Name** - The webhook title and @mention tap.</span></span>
>* <span data-ttu-id="aa83b-190">**コールバック URL** - JSON ペイロードを受け入れ、JSON ペイロードから POST 要求を受信する HTTPS エンドポイントTeams。</span><span class="sxs-lookup"><span data-stu-id="aa83b-190">**Callback URL** - The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
>* <span data-ttu-id="aa83b-191">**説明** - プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列。</span><span class="sxs-lookup"><span data-stu-id="aa83b-191">**Description** - A detailed string that appear in the profile card and the team-level App dashboard.</span></span>
>* <span data-ttu-id="aa83b-192">**Profile Picture** Webhook のオプションのアプリ アイコン。</span><span class="sxs-lookup"><span data-stu-id="aa83b-192">**Profile Picture** an optional app icon for your webhook.</span></span>
>* <span data-ttu-id="aa83b-193">ポップアップ ウィンドウ **の右下** 隅から [作成] ボタンを選択すると、送信 Webhook が現在のチームのチャネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-193">Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.</span></span>
>* <span data-ttu-id="aa83b-194">次のダイアログ ウィンドウには、ハッシュ ベースのメッセージ認証コード[(HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)セキュリティ トークンが表示され、Teams と指定された外部サービス間の呼び出しを認証するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-194">The next dialog window displays an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that is used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="aa83b-195">送信 Webhook は、URL が有効で、サーバー認証トークンとクライアント認証トークン (HMAC ハンドシェイクなど) が等しい場合にのみ、チームのユーザーが使用できます。</span><span class="sxs-lookup"><span data-stu-id="aa83b-195">The outgoing webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal for example, an HMAC handshake.</span></span>

## <a name="code-sample"></a><span data-ttu-id="aa83b-196">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="aa83b-196">Code sample</span></span>
|<span data-ttu-id="aa83b-197">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="aa83b-197">**Sample name**</span></span> | <span data-ttu-id="aa83b-198">**説明**</span><span class="sxs-lookup"><span data-stu-id="aa83b-198">**Description**</span></span> | <span data-ttu-id="aa83b-199">**.NET**</span><span class="sxs-lookup"><span data-stu-id="aa83b-199">**.NET**</span></span> | <span data-ttu-id="aa83b-200">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="aa83b-200">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="aa83b-201">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="aa83b-201">Outgoing webhooks</span></span> | <span data-ttu-id="aa83b-202">カスタム ボット **を作成するサンプルを** 使用して、Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="aa83b-202">Samples to create **Custom Bots** to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="aa83b-203">View</span><span class="sxs-lookup"><span data-stu-id="aa83b-203">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="aa83b-204">View</span><span class="sxs-lookup"><span data-stu-id="aa83b-204">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

