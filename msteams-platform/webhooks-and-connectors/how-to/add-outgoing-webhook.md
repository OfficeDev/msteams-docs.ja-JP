---
title: 送信 Webhook の作成
author: laujan
description: 送信 Webhook を作成する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
keywords: teams タブ送信 webhook アクション可能メッセージ verify webhook
ms.openlocfilehash: c02ff5388e47ba40056afcc1fcf5e8d7ad4437e8
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140338"
---
# <a name="create-outgoing-webhook"></a><span data-ttu-id="6787f-104">送信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="6787f-104">Create Outgoing Webhook</span></span>

<span data-ttu-id="6787f-105">送信 Webhook はボットとして機能し、ボットを使用してチャネル内の **メッセージ@mention。**</span><span class="sxs-lookup"><span data-stu-id="6787f-105">The Outgoing Webhook acts as a bot and search for messages in channels using **@mention**.</span></span> <span data-ttu-id="6787f-106">外部 Web サービスに通知を送信し、カードや画像を含むリッチ メッセージで応答します。</span><span class="sxs-lookup"><span data-stu-id="6787f-106">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span> <span data-ttu-id="6787f-107">これは、ボットを作成するプロセスをスキップするのに役立[Microsoft Bot Framework。](https://dev.botframework.com/)</span><span class="sxs-lookup"><span data-stu-id="6787f-107">It helps to skip the process of creating bots through the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

## <a name="key-features-of-outgoing-webhook"></a><span data-ttu-id="6787f-108">送信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="6787f-108">Key features of Outgoing Webhook</span></span>

<span data-ttu-id="6787f-109">次の表に、送信 Webhook の機能と説明を示します。</span><span class="sxs-lookup"><span data-stu-id="6787f-109">The following table provides the features and description of Outgoing Webhooks:</span></span>

| <span data-ttu-id="6787f-110">機能</span><span class="sxs-lookup"><span data-stu-id="6787f-110">Features</span></span> | <span data-ttu-id="6787f-111">説明</span><span class="sxs-lookup"><span data-stu-id="6787f-111">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="6787f-112">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="6787f-112">Scoped configuration</span></span>| <span data-ttu-id="6787f-113">Webhook はチームのレベルでスコープが設定されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-113">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="6787f-114">それぞれの必須のセットアップ プロセスでは、送信 Webhook が追加されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-114">Mandatory set up process for each adds an Outgoing Webhook.</span></span> |
| <span data-ttu-id="6787f-115">反応性メッセージング</span><span class="sxs-lookup"><span data-stu-id="6787f-115">Reactive messaging</span></span>| <span data-ttu-id="6787f-116">ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6787f-116">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="6787f-117">現在、ユーザーはパブリック チャネルでのみ送信 Webhook にメッセージを送信できます。個人またはプライベート スコープ内ではメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="6787f-117">Currently, users can only message an Outgoing Webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="6787f-118">標準の HTTP メッセージ交換</span><span class="sxs-lookup"><span data-stu-id="6787f-118">Standard HTTP message exchange</span></span>|<span data-ttu-id="6787f-119">応答は元の要求メッセージと同じチェーンに表示され、リッチ テキスト、画像、カード、絵文字など、任意の Bot Framework メッセージ コンテンツを含めできます。</span><span class="sxs-lookup"><span data-stu-id="6787f-119">Responses appear in the same chain as the original request message and can include any Bot Framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="6787f-120">送信 Webhooks はカードを使用することができますが、 を除き、カードアクションを使用することはできません `openURL` 。</span><span class="sxs-lookup"><span data-stu-id="6787f-120">Although Outgoing Webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="6787f-121">Teams API メソッドのサポート</span><span class="sxs-lookup"><span data-stu-id="6787f-121">Teams API method support</span></span>|<span data-ttu-id="6787f-122">送信 Webhooks は HTTP POST を Web サービスに送信し、応答を取得します。</span><span class="sxs-lookup"><span data-stu-id="6787f-122">Outgoing Webhooks sends an HTTP POST to a web service and gets a response.</span></span> <span data-ttu-id="6787f-123">チーム内のチャネルの名簿やリストの取得など、他の API にはアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="6787f-123">They cannot access any other APIs, such as retrieve the roster or list of channels in a team.</span></span>|

## <a name="create-outgoing-webhooks"></a><span data-ttu-id="6787f-124">送信 Webhooks の作成</span><span class="sxs-lookup"><span data-stu-id="6787f-124">Create Outgoing Webhooks</span></span>

<span data-ttu-id="6787f-125">送信 Webhook を作成し、カスタム ボットをユーザー設定にTeams。</span><span class="sxs-lookup"><span data-stu-id="6787f-125">Create Outgoing Webhooks and add custom bots to Teams.</span></span>

<span data-ttu-id="6787f-126">**送信 Webhook を作成するには**</span><span class="sxs-lookup"><span data-stu-id="6787f-126">**To create an Outgoing Webhook**</span></span>

1. <span data-ttu-id="6787f-127">左側 **のTeams** ウィンドウから [新しいウィンドウ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6787f-127">Select **Teams** from the left pane.</span></span> <span data-ttu-id="6787f-128">**[Teams]** ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-128">The **Teams** page appears:</span></span>

    ![Teams チャネル](~/assets/images/teamschannel.png)

1. <span data-ttu-id="6787f-130">[送信 **Teams]** ページで、送信 Webhook を作成するために必要なチームを選択し、送信 Webhook を &#8226;&#8226;&#8226;。</span><span class="sxs-lookup"><span data-stu-id="6787f-130">In the **Teams** page, select the required team to create an Outgoing Webhook and select the &#8226;&#8226;&#8226;.</span></span> <span data-ttu-id="6787f-131">ドロップダウン メニューで、[チームの管理] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="6787f-131">In the dropdown menu, select **Manage team**:</span></span>

    ![送信 Webhook の作成](~/assets/images/outgoingwebhook1.png)

1. <span data-ttu-id="6787f-133">チャネル ページ **の [アプリ** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="6787f-133">Select the **Apps** tab on the channel page:</span></span>

    ![送信 Webhook の作成](~/assets/images/outgoingwebhook2.png)

1. <span data-ttu-id="6787f-135">[ **送信 Webhook の作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="6787f-135">Select **Create an Outgoing Webhook**:</span></span>

    ![送信 Webhooks の作成](~/assets/images/outgoingwebhook3.png)

1. <span data-ttu-id="6787f-137">[送信 Webhook の作成] **ページに次の詳細を入力** します。</span><span class="sxs-lookup"><span data-stu-id="6787f-137">Type the following details in the **Create an Outgoing Webhook** page:</span></span>

    * <span data-ttu-id="6787f-138">**名前**: [Webhook] タイトルと [@mention] タブ。</span><span class="sxs-lookup"><span data-stu-id="6787f-138">**Name**: The webhook title and @mention tab.</span></span>
    * <span data-ttu-id="6787f-139">**コールバック URL**: JSON ペイロードを受け入れ、JSON ペイロードから POST 要求を受信する HTTPS エンドポイントTeams。</span><span class="sxs-lookup"><span data-stu-id="6787f-139">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
    * <span data-ttu-id="6787f-140">**説明**: プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列。</span><span class="sxs-lookup"><span data-stu-id="6787f-140">**Description**: A detailed string that appears in the profile card and the team-level App dashboard.</span></span>
    * <span data-ttu-id="6787f-141">**プロファイル画像**: Webhook のアプリ アイコン (省略可能)。</span><span class="sxs-lookup"><span data-stu-id="6787f-141">**Profile Picture**: An app icon for your webhook, which is optional.</span></span>

1. <span data-ttu-id="6787f-142">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6787f-142">Select **Create**.</span></span> <span data-ttu-id="6787f-143">送信 Webhook は、現在のチームのチャネルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-143">The Outgoing Webhook is added to the current team's channel:</span></span>

    ![送信 Webhook の作成](~/assets/images/outgoingwebhook.png)

<span data-ttu-id="6787f-145">ハッシュ [ベースのメッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-145">A [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) dialogue box appears.</span></span> <span data-ttu-id="6787f-146">これは、指定された外部サービスとの間の呼び出しTeams認証するために使用されるセキュリティ トークンです。</span><span class="sxs-lookup"><span data-stu-id="6787f-146">It is a security token used to authenticate calls between Teams and the designated outside service.</span></span>

>[!NOTE]
> <span data-ttu-id="6787f-147">送信 Webhook は、URL が有効で、サーバーとクライアントの認証トークンが等しい場合にのみ、チームのユーザーが使用できます。</span><span class="sxs-lookup"><span data-stu-id="6787f-147">The Outgoing Webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal.</span></span> <span data-ttu-id="6787f-148">たとえば、HMAC ハンドシェイクです。</span><span class="sxs-lookup"><span data-stu-id="6787f-148">For example, an HMAC handshake.</span></span>

<span data-ttu-id="6787f-149">次のシナリオでは、送信 Webhook を追加する詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="6787f-149">The following scenario provides the details to add an Outgoing Webhook:</span></span>

* <span data-ttu-id="6787f-150">シナリオ: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="6787f-150">Scenario: Push change status notifications on a Teams channel database server to your app.</span></span>
* <span data-ttu-id="6787f-151">例: 作成、読み取り、更新、削除など、すべての CRUD 操作を追跡する一行のビジネス アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="6787f-151">Example: You have a line of business app that tracks all CRUD operations, such as create, read, update, and delete.</span></span> <span data-ttu-id="6787f-152">これらの操作は、従業員レコードに対して、Teamsテナント全体の人事ユーザー Office 365されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-152">These operations are made to the employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

# <a name="url-json-payload"></a>[<span data-ttu-id="6787f-153">URL JSON ペイロード</span><span class="sxs-lookup"><span data-stu-id="6787f-153">URL JSON payload</span></span>](#tab/urljsonpayload)
<span data-ttu-id="6787f-154">**JSON ペイロードを使用して POST 要求を受け入れて処理する URL をアプリのサーバーに作成する**</span><span class="sxs-lookup"><span data-stu-id="6787f-154">**Create a URL on your app's server to accept and process a POST request with a JSON payload**</span></span>

<span data-ttu-id="6787f-155">サービスは、標準の Azure ボット サービス メッセージング スキーマでメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="6787f-155">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="6787f-156">ボット フレームワーク コネクタは RESTful サービスで [、Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理できます。</span><span class="sxs-lookup"><span data-stu-id="6787f-156">The Bot Framework connector is a RESTful service that empowers to process the interchange of JSON formatted messages through HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="6787f-157">または、SDK の手順に従ってMicrosoft Bot Frameworkメッセージを処理して解析することもできます。</span><span class="sxs-lookup"><span data-stu-id="6787f-157">Alternatively, you can follow the Microsoft Bot Framework SDK to process and parse messages.</span></span> <span data-ttu-id="6787f-158">詳細については [、「Azure Bot Service の概要」を参照してください](/azure/bot-service/bot-service-overview-introduction)。</span><span class="sxs-lookup"><span data-stu-id="6787f-158">For more information, see [overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>

<span data-ttu-id="6787f-159">送信 Webhook はレベルの範囲に設定 `team` され、すべてのチーム メンバーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-159">Outgoing Webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="6787f-160">ユーザーは、**\@ チャネルで** 呼び出す送信 Webhook の名前を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6787f-160">Users need to **\@mention** the name of the Outgoing Webhook to invoke it in the channel.</span></span>

# <a name="verify-hmac-token"></a>[<span data-ttu-id="6787f-161">HMAC トークンを確認する</span><span class="sxs-lookup"><span data-stu-id="6787f-161">Verify HMAC token</span></span>](#tab/verifyhmactoken)
<span data-ttu-id="6787f-162">**送信 Webhook HMAC トークンを確認するメソッドを作成する**</span><span class="sxs-lookup"><span data-stu-id="6787f-162">**Create a method to verify the Outgoing Webhook HMAC token**</span></span>

<span data-ttu-id="6787f-163">受信メッセージと ID の使用例: {"contoso"の SigningKeyDictionary の "contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。</span><span class="sxs-lookup"><span data-stu-id="6787f-163">Using example of inbound message and ID: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="6787f-164">要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。</span><span class="sxs-lookup"><span data-stu-id="6787f-164">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="6787f-165">サービスが実際のクライアントからのみ呼び出しを受信Teams、Teams HTTP 承認ヘッダーに HMAC コードを `hmac` 提供します。</span><span class="sxs-lookup"><span data-stu-id="6787f-165">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` authorization header.</span></span> <span data-ttu-id="6787f-166">認証プロトコルにコードを常に含める。</span><span class="sxs-lookup"><span data-stu-id="6787f-166">Always include the code in your authentication protocol.</span></span>

<span data-ttu-id="6787f-167">コードでは、要求に含まれる HMAC 署名を次のように常に検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6787f-167">Your code must always validate the HMAC signature included in the request as follows:</span></span>

* <span data-ttu-id="6787f-168">メッセージの要求本文から HMAC トークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="6787f-168">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="6787f-169">ほとんどのプラットフォームでこれを行う標準的なライブラリがあります(たとえば、Node.js[](https://nodejs.org/api/crypto.html#crypto_crypto)の Crypto Teams [Webhook サンプル](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \# )。</span><span class="sxs-lookup"><span data-stu-id="6787f-169">There are standard libraries to do this on most platform, such as [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js and [Teams webhook sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="6787f-170">Microsoft Teams SHA256 HMAC 暗号化を使用します。</span><span class="sxs-lookup"><span data-stu-id="6787f-170">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="6787f-171">UTF8 で本文をバイト配列に変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6787f-171">You must convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="6787f-172">送信 Webhook をクライアントに登録した場合、Teams によって提供されるセキュリティ トークンのバイト配列からハッシュTeamsします。</span><span class="sxs-lookup"><span data-stu-id="6787f-172">Compute the hash from the byte array of the security token provided by Teams when you registered the Outgoing Webhook in the Teams client.</span></span> <span data-ttu-id="6787f-173">「 [送信 Webhook の作成」を参照してください](#create-outgoing-webhook)。</span><span class="sxs-lookup"><span data-stu-id="6787f-173">See [create an Outgoing Webhook](#create-outgoing-webhook).</span></span>
* <span data-ttu-id="6787f-174">UTF-8 エンコーディングを使用してハッシュを文字列に変換します。</span><span class="sxs-lookup"><span data-stu-id="6787f-174">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="6787f-175">生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。</span><span class="sxs-lookup"><span data-stu-id="6787f-175">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

# <a name="method-to-respond"></a>[<span data-ttu-id="6787f-176">応答するメソッド</span><span class="sxs-lookup"><span data-stu-id="6787f-176">Method to respond</span></span>](#tab/methodtorespond)
<span data-ttu-id="6787f-177">**成功または失敗の応答を送信するメソッドを作成する**</span><span class="sxs-lookup"><span data-stu-id="6787f-177">**Create a method to send a success or failure response**</span></span>

<span data-ttu-id="6787f-178">送信 Webhooks からの応答は、元のメッセージと同じ返信チェーンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6787f-178">Responses from your Outgoing Webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="6787f-179">ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行し、接続が切れ、終了する前にコードがメッセージに応答するために 5 秒を取得します。</span><span class="sxs-lookup"><span data-stu-id="6787f-179">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="6787f-180">応答の例</span><span class="sxs-lookup"><span data-stu-id="6787f-180">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * <span data-ttu-id="6787f-181">送信 Webhook を使用して、アダプティブ カード、ヒーロー カード、およびテキスト メッセージを添付ファイルとして送信できます。</span><span class="sxs-lookup"><span data-stu-id="6787f-181">You can send Adaptive Card, Hero card, and text messages as attachment with Outgoing Webhook.</span></span>
> * <span data-ttu-id="6787f-182">カードは書式設定をサポートします。</span><span class="sxs-lookup"><span data-stu-id="6787f-182">Cards support formatting.</span></span> <span data-ttu-id="6787f-183">詳細については [、「markdown を使用した書式カード」を参照してください](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)。</span><span class="sxs-lookup"><span data-stu-id="6787f-183">For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).</span></span>

<span data-ttu-id="6787f-184">アダプティブ カード応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6787f-184">Following codes are examples of an Adaptive Card response:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6787f-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6787f-185">C#/.NET</span></span>](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6787f-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6787f-186">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# <a name="json"></a>[<span data-ttu-id="6787f-187">JSON</span><span class="sxs-lookup"><span data-stu-id="6787f-187">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: Megan"
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card.."
                    }
                ]
            }
        }
    ]
}
```

* * *

## <a name="code-sample"></a><span data-ttu-id="6787f-188">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="6787f-188">Code sample</span></span>

|<span data-ttu-id="6787f-189">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="6787f-189">**Sample name**</span></span> | <span data-ttu-id="6787f-190">**説明**</span><span class="sxs-lookup"><span data-stu-id="6787f-190">**Description**</span></span> | <span data-ttu-id="6787f-191">**.NET**</span><span class="sxs-lookup"><span data-stu-id="6787f-191">**.NET**</span></span> | <span data-ttu-id="6787f-192">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="6787f-192">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="6787f-193">送信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="6787f-193">Outgoing Webhooks</span></span> | <span data-ttu-id="6787f-194">カスタム ボットを作成するサンプルを使用して、Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="6787f-194">Samples to create custom bots to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="6787f-195">View</span><span class="sxs-lookup"><span data-stu-id="6787f-195">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="6787f-196">View</span><span class="sxs-lookup"><span data-stu-id="6787f-196">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a><span data-ttu-id="6787f-197">関連項目</span><span class="sxs-lookup"><span data-stu-id="6787f-197">See also</span></span>
* [<span data-ttu-id="6787f-198">受信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="6787f-198">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="6787f-199">Office 365 コネクタを作成する</span><span class="sxs-lookup"><span data-stu-id="6787f-199">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="6787f-200">メッセージを作成して送信する</span><span class="sxs-lookup"><span data-stu-id="6787f-200">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
