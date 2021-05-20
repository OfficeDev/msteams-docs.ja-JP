---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
description: 発信 Webhook を追加する方法を説明します
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: チームタブ送信ウェブフックアクション可能なメッセージは、ウェブフックを確認します
ms.openlocfilehash: a5a0cdfc9080ac4567f438b6fb6fd0671df8c19f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566531"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a><span data-ttu-id="a2ffb-104">送信ウェブフックを使用してTeamsにカスタムボットを追加する</span><span class="sxs-lookup"><span data-stu-id="a2ffb-104">Add custom bots to Teams with outgoing webhooks</span></span>

## <a name="outgoing-webhooks-in-teams"></a><span data-ttu-id="a2ffb-105">Teamsでの送信ウェブフック</span><span class="sxs-lookup"><span data-stu-id="a2ffb-105">Outgoing webhooks in Teams</span></span>

<span data-ttu-id="a2ffb-106">Webhook は、Teamsが外部アプリと統合するための優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-106">Webhooks are an eminent way for Teams to integrate with external apps.</span></span> <span data-ttu-id="a2ffb-107">基本的に Webhook は、コールバック URL に送信される POST 要求です。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-107">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="a2ffb-108">送信 webhook を使用すると、ユーザーは[Microsoft Bot Framework](https://dev.botframework.com/)を介してボットを作成する完全なプロセスを経ることなく、Web サービスにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-108">Outgoing webhooks allow users to send messages to your web service without going through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

<span data-ttu-id="a2ffb-109">送信 webhook は、json ペイロードを受け入れることができる任意の選択されたサービスにTeamsからデータを送信します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-109">Outgoing webhook sends data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="a2ffb-110">発信ウェブフックをチームに追加した後、ボットとして機能し、**\@ メンション** を使用してチャネル内のメッセージを探します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-110">After adding the outgoing webhooks to a team, it acts as a bot and looks for messages in channels using **\@mention**.</span></span> <span data-ttu-id="a2ffb-111">外部 Web サービスに通知を送信し、カードや画像を含むリッチメッセージで応答します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-111">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="a2ffb-112">送信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="a2ffb-112">Outgoing webhook key features</span></span>

| <span data-ttu-id="a2ffb-113">機能</span><span class="sxs-lookup"><span data-stu-id="a2ffb-113">Feature</span></span> | <span data-ttu-id="a2ffb-114">説明</span><span class="sxs-lookup"><span data-stu-id="a2ffb-114">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="a2ffb-115">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="a2ffb-115">Scoped configuration</span></span>| <span data-ttu-id="a2ffb-116">Webhook はチームのレベルでスコープが設定されます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-116">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="a2ffb-117">送信 webhook を追加する各チームのセットアップ プロセスを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-117">You must go through the setup process for each team where you want to add your outgoing webhook.</span></span> |
| <span data-ttu-id="a2ffb-118">反応型メッセージング</span><span class="sxs-lookup"><span data-stu-id="a2ffb-118">Reactive messaging</span></span>| <span data-ttu-id="a2ffb-119">ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-119">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="a2ffb-120">現在、ユーザーはパブリック チャネル内の送信 Webhook のみをメッセージで送信でき、個人スコープまたはプライベート スコープ内ではメッセージを送信できません。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-120">Currently, users can only message an outgoing webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="a2ffb-121">標準の HTTP メッセージ交換</span><span class="sxs-lookup"><span data-stu-id="a2ffb-121">Standard HTTP message exchange</span></span>|<span data-ttu-id="a2ffb-122">応答は元の要求メッセージと同じチェーンに表示され、リッチテキスト、画像、カード、絵文字などのボットフレームワークメッセージコンテンツを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-122">Responses appear in the same chain as the original request message and can include any bot framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="a2ffb-123">発信 Webhook ではカードを使用できますが、 以外のカード アクションは使用できません `openURL` 。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-123">Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="a2ffb-124">Teams API メソッドのサポート</span><span class="sxs-lookup"><span data-stu-id="a2ffb-124">Teams API method support</span></span>|<span data-ttu-id="a2ffb-125">送信 Webhook は HTTP POST を Web サービスに送信し、応答を処理します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-125">Outgoing webhook sends an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="a2ffb-126">チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-126">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="creating-actionable-messages"></a><span data-ttu-id="a2ffb-127">操作可能なメッセージの作成</span><span class="sxs-lookup"><span data-stu-id="a2ffb-127">Creating actionable messages</span></span>

<span data-ttu-id="a2ffb-128">コネクタ カードには、カードに 3 つのボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-128">The connector cards include three visible buttons on the card.</span></span> <span data-ttu-id="a2ffb-129">各ボタンは、アクションを `potentialAction` 使用してメッセージのプロパティで定義 `ActionCard` されます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-129">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions.</span></span> <span data-ttu-id="a2ffb-130">それぞれに `ActionCard` は、入力タイプ、テキストフィールド、日付ピッカー、または複数選択リストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-130">Each `ActionCard` contains an input type; a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="a2ffb-131">各 `ActionCard` アクションには、関連付けられたアクションがあります `HttpPOST` 。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-131">Each `ActionCard` action has an associated action, for example, `HttpPOST`.</span></span>

<span data-ttu-id="a2ffb-132">コネクタ カードでは、3 種類のアクションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-132">Connector cards support three types of actions:</span></span>

| <span data-ttu-id="a2ffb-133">アクション</span><span class="sxs-lookup"><span data-stu-id="a2ffb-133">Action</span></span> | <span data-ttu-id="a2ffb-134">説明</span><span class="sxs-lookup"><span data-stu-id="a2ffb-134">Description</span></span> |
| ------- | ----------- |
| `ActionCard` |<span data-ttu-id="a2ffb-135">1 つ以上の入力タイプと関連するアクションを示します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-135">Presents one or more input types and associated actions.</span></span>|
| `HttpPOST` | <span data-ttu-id="a2ffb-136">URL に POST 要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-136">Sends a POST request to a URL.</span></span> |
| `OpenUri` |  <span data-ttu-id="a2ffb-137">別のブラウザーまたはアプリで URI を開き、オプションで、オペレーティング システムに基づいて異なる URI を対象にします。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-137">Opens a URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>|

<span data-ttu-id="a2ffb-138">`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-138">The `ActionCard` action supports three input types:</span></span>

| <span data-ttu-id="a2ffb-139">入力タイプ</span><span class="sxs-lookup"><span data-stu-id="a2ffb-139">Input type</span></span> | <span data-ttu-id="a2ffb-140">説明</span><span class="sxs-lookup"><span data-stu-id="a2ffb-140">Description</span></span> |
| ------- | ----------- |
| `TextInput` | <span data-ttu-id="a2ffb-141">長さの制限を省略できる単一行または複数行のテキスト フィールド。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-141">A single-line or multiline text field with an optional length limit.</span></span> |
| `DateInput` | <span data-ttu-id="a2ffb-142">オプションの時間セレクタを持つ日付セレクタ。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-142">A date selector with an optional time selector.</span></span> |
| `MultichoiceInput` | <span data-ttu-id="a2ffb-143">単一の選択または複数の選択を提供する、指定された選択肢のリスト。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-143">A specified list of choices, offering either a single selection or multiple selections.</span></span>|

<span data-ttu-id="a2ffb-144">`MultichoiceInput` は、 `style` 完全に展開されたリストの表示を制御するプロパティをサポートします。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-144">`MultichoiceInput` supports a `style` property that controls the display of a fully expanded list.</span></span> <span data-ttu-id="a2ffb-145">デフォルト値は `style` 、値によって異なります `isMultiSelect` 。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-145">The default value of `style` depends on the `isMultiSelect` value.</span></span>

| <span data-ttu-id="a2ffb-146">`isMultiSelect` 価値</span><span class="sxs-lookup"><span data-stu-id="a2ffb-146">`isMultiSelect` value</span></span>  | <span data-ttu-id="a2ffb-147">`style` 既定値</span><span class="sxs-lookup"><span data-stu-id="a2ffb-147">`style` default value</span></span>  |
| --- | --- |
| <span data-ttu-id="a2ffb-148">`false` または指定なし</span><span class="sxs-lookup"><span data-stu-id="a2ffb-148">`false` or not specified</span></span> | <span data-ttu-id="a2ffb-149">デフォルトのスタイルは `compact`</span><span class="sxs-lookup"><span data-stu-id="a2ffb-149">The default style is `compact`</span></span>|
| `true` | <span data-ttu-id="a2ffb-150">デフォルトのスタイルは `expanded`</span><span class="sxs-lookup"><span data-stu-id="a2ffb-150">The default style is `expanded`</span></span> |

> [!NOTE]
> * <span data-ttu-id="a2ffb-151">`"isMultiSelect": true` `"style": true` 複数選択リストをコンパクトなスタイルで表示する場合は、 と と の両方を入力します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-151">Enter both `"isMultiSelect": true` and `"style": true`, if you want the multi-select list to be displayed in a compact style.</span></span>
> * <span data-ttu-id="a2ffb-152">`compact` `style` Teamsでプロパティを選択することは `normal` 、Microsoft Outlookでプロパティを選択するのと同 `style` じです。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-152">Selecting `compact` for the `style` property in Teams is the same as selecting `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="a2ffb-153">Webhook は、Office 365メッセージ バック カードとアダプティブ カードのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-153">Webhooks support only Office 365 message back cards and adaptive cards.</span></span>

<span data-ttu-id="a2ffb-154">コネクタ カードアクションに関するその他の詳細については、アクション可能なメッセージ カード リファレンスの **[アクション](/outlook/actionable-messages/card-reference#actions)** を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-154">For all other details about connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="adding-outgoing-webhooks-to-your-app"></a><span data-ttu-id="a2ffb-155">アプリへの送信ウェブフックの追加</span><span class="sxs-lookup"><span data-stu-id="a2ffb-155">Adding outgoing webhooks to your app</span></span>

<span data-ttu-id="a2ffb-156">**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-156">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="a2ffb-157">**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-157">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="a2ffb-158">1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する</span><span class="sxs-lookup"><span data-stu-id="a2ffb-158">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="a2ffb-159">サービスは、標準の Azure ボット サービス メッセージング スキーマでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-159">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="a2ffb-160">ボット フレームワーク コネクタは、 [サービスが、Azure Bot](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)サービス API に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理する権限を与える RESTful サービスです。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-160">The bot framework connector is a RESTful service that empowers your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="a2ffb-161">[Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-161">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="a2ffb-162">[「Azure ボット サービスについて](/azure/bot-service/bot-service-overview-introduction)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-162">See also [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>


<span data-ttu-id="a2ffb-163">発信 webhook は、レベルにスコープされ `team` 、すべてのチーム メンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-163">Outgoing webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="a2ffb-164">ボットと同様に、ユーザーはチャネルで呼び出すために発信 webhook の名前を **\@ 指定** する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-164">Just like a bot, users need to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="a2ffb-165">2. 送信 Webhook HMAC トークンを確認するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="a2ffb-165">2. Create a method to verify the outgoing webhook HMAC token</span></span>

#### <a name="hmac-signature-for-testing-with-code-example"></a><span data-ttu-id="a2ffb-166">コード例を使ったテスト用の HMAC 署名</span><span class="sxs-lookup"><span data-stu-id="a2ffb-166">HMAC signature for testing with code example</span></span>

<span data-ttu-id="a2ffb-167">受信メッセージと ID の例を使用して: {"contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKk/N2bOmlM31zaA=" の署名キーディクショナリの "contoso" }</span><span class="sxs-lookup"><span data-stu-id="a2ffb-167">Using example of inbound message and id: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="a2ffb-168">要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-168">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="a2ffb-169">サービスが実際のTeams クライアントからのみ呼び出しを受信するように、Teamsは HTTP ヘッダーに HMAC コードを提供 `hmac` します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-169">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` header.</span></span> <span data-ttu-id="a2ffb-170">常に認証プロトコルにコードを含める。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-170">Always included the code in your authentication protocol.</span></span>

<span data-ttu-id="a2ffb-171">コードは、要求に含まれる HMAC 署名を常に検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-171">Your code must always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="a2ffb-172">メッセージの要求本文から HMAC トークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-172">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="a2ffb-173">ほとんどのプラットフォームでこれを行うための標準ライブラリがあります (Node.js用[の暗号を](https://nodejs.org/api/crypto.html#crypto_crypto)参照するか、または C の[Webhook サンプルTeams](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs)参照 \# してください)。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-173">There are standard libraries to do this on most platforms (see [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="a2ffb-174">Microsoft Teamsは、標準の SHA256 HMAC 暗号化を使用します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-174">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="a2ffb-175">本体を UTF8 でバイト配列に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-175">You need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="a2ffb-176">Teams クライアントで送信 Webhook を登録したときに Teams によって提供されたセキュリティ トークンのバイト配列からハッシュを **計算** します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-176">Compute the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="a2ffb-177">「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-177">See [Create an outgoing webhook](#create-an-outgoing-webhook).</span></span>
* <span data-ttu-id="a2ffb-178">UTF-8 エンコーディングを使用してハッシュを文字列に変換します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-178">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="a2ffb-179">生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-179">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="a2ffb-180">3. 成功または失敗の応答を送信するメソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="a2ffb-180">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="a2ffb-181">送信 Webhook からの応答は、元のメッセージと同じ応答チェーンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-181">Responses from your outgoing webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="a2ffb-182">ユーザーがクエリを実行すると、Microsoft Teamsサービスに同期 HTTP 要求が発行され、コードは、接続がタイムアウトして終了する前にメッセージに応答するために 5 秒を取得します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-182">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="a2ffb-183">応答の例</span><span class="sxs-lookup"><span data-stu-id="a2ffb-183">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="a2ffb-184">送信 Webhook を作成する</span><span class="sxs-lookup"><span data-stu-id="a2ffb-184">Create an outgoing webhook</span></span>

1. <span data-ttu-id="a2ffb-185">適切なチームを選択し、(&#8226;&#8226;&#8226;)ドロップダウンメニューから **[チームの管理** ]を選択します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-185">Select the appropriate team and choose **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="a2ffb-186">ナビゲーション バーから **[アプリ]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-186">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="a2ffb-187">ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-187">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="a2ffb-188">表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-188">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="a2ffb-189">**名前**: ウェブフックのタイトルと@mentionタップ</span><span class="sxs-lookup"><span data-stu-id="a2ffb-189">**Name**: The webhook title and @mention tap</span></span>
>* <span data-ttu-id="a2ffb-190">**コールバック URL**: JSON ペイロードを受け取り、Teamsからの POST 要求を受信する HTTPS エンドポイント</span><span class="sxs-lookup"><span data-stu-id="a2ffb-190">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams</span></span>
>* <span data-ttu-id="a2ffb-191">**説明**: プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列</span><span class="sxs-lookup"><span data-stu-id="a2ffb-191">**Description**: A detailed string that appear in the profile card and the team-level App dashboard</span></span>
>* <span data-ttu-id="a2ffb-192">**プロフィール写真**: ウェブフック用のオプションのアプリアイコン</span><span class="sxs-lookup"><span data-stu-id="a2ffb-192">**Profile Picture**: An optional app icon for your webhook</span></span>
>* <span data-ttu-id="a2ffb-193">ポップアップ ウィンドウの右下隅にある [ **作成]** ボタンを選択すると、送信 webhook が現在のチームのチャンネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-193">Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.</span></span>
>* <span data-ttu-id="a2ffb-194">次のダイアログ ウィンドウには、Teamsと指定された外部サービス間の呼び出しを認証するために使用される[ハッシュ ベース メッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)セキュリティ トークンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-194">The next dialog window displays an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that is used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="a2ffb-195">発信 webhook は、URL が有効で、サーバーとクライアントの認証トークンが等しい場合のみ、チームのユーザーが使用できます(HMAC ハンドシェイクなど)。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-195">The outgoing webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal for example, an HMAC handshake.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a2ffb-196">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="a2ffb-196">Code sample</span></span>
|<span data-ttu-id="a2ffb-197">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="a2ffb-197">**Sample name**</span></span> | <span data-ttu-id="a2ffb-198">**説明**</span><span class="sxs-lookup"><span data-stu-id="a2ffb-198">**Description**</span></span> | <span data-ttu-id="a2ffb-199">**.NET**</span><span class="sxs-lookup"><span data-stu-id="a2ffb-199">**.NET**</span></span> | <span data-ttu-id="a2ffb-200">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="a2ffb-200">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="a2ffb-201">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="a2ffb-201">Outgoing webhooks</span></span> | <span data-ttu-id="a2ffb-202">Microsoft Teamsで使用する **カスタム ボットを** 作成するサンプル。</span><span class="sxs-lookup"><span data-stu-id="a2ffb-202">Samples to create **Custom Bots** to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="a2ffb-203">View</span><span class="sxs-lookup"><span data-stu-id="a2ffb-203">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="a2ffb-204">View</span><span class="sxs-lookup"><span data-stu-id="a2ffb-204">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

