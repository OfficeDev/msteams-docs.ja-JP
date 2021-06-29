---
title: メッセージを作成して送信する
author: laujan
description: Microsoft Teams で Office 365 コネクタを使用する方法について説明します。
ms.topic: how-to
localization_priority: Normal
keywords: Teams o365 コネクタ
ms.openlocfilehash: 8835e43ed74a8da5ad3b3b4358b259d63068b469
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179896"
---
# <a name="create-and-send-messages"></a><span data-ttu-id="ec14d-104">メッセージを作成して送信する</span><span class="sxs-lookup"><span data-stu-id="ec14d-104">Create and send messages</span></span>

<span data-ttu-id="ec14d-105">アクション可能なメッセージを作成し、受信 Webhook または受信コネクタを介してOffice 365できます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-105">You can create actionable messages and send it through Incoming Webhook or Office 365 Connector.</span></span>

## <a name="create-actionable-messages"></a><span data-ttu-id="ec14d-106">アクション可能なメッセージを作成する</span><span class="sxs-lookup"><span data-stu-id="ec14d-106">Create actionable messages</span></span>

<span data-ttu-id="ec14d-107">アクション可能なメッセージには、カードに表示される 3 つのボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-107">The actionable messages include three visible buttons on the card.</span></span> <span data-ttu-id="ec14d-108">各ボタンは、入力型、テキスト フィールド、日付選択リスト、または複数選択肢リストを持つアクションを使用して、メッセージのプロパティ `potentialAction` `ActionCard` で定義されます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-108">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each with an input type, a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="ec14d-109">各 `ActionCard` アクションには、たとえば、関連付けられたアクションがあります `HttpPOST` 。</span><span class="sxs-lookup"><span data-stu-id="ec14d-109">Each `ActionCard` has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="ec14d-110">コネクタ カードは、次の操作をサポートします。</span><span class="sxs-lookup"><span data-stu-id="ec14d-110">The connector cards support the following actions:</span></span>

- <span data-ttu-id="ec14d-111">`ActionCard`: 1 つ以上の入力型と関連付けられたアクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-111">`ActionCard`: Presents one or more input types and associated actions.</span></span>
- <span data-ttu-id="ec14d-112">`HttpPOST`: POST 要求を URL に送信します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-112">`HttpPOST`: Sends POST request to a URL.</span></span>
- <span data-ttu-id="ec14d-113">`OpenUri`: 別のブラウザーまたはアプリで URI を開き、必要に応じてオペレーティング システムに基づいて異なる URI を対象とします。</span><span class="sxs-lookup"><span data-stu-id="ec14d-113">`OpenUri`: Opens URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>

<span data-ttu-id="ec14d-114">`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ec14d-114">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="ec14d-115">`TextInput`: 1 行または複数行のテキスト フィールドで、オプションの長さ制限があります。</span><span class="sxs-lookup"><span data-stu-id="ec14d-115">`TextInput`: A single line or multiline text field with an optional length limit.</span></span>
- <span data-ttu-id="ec14d-116">`DateInput`: オプションのタイム セレクターを含む日付セレクター。</span><span class="sxs-lookup"><span data-stu-id="ec14d-116">`DateInput`: A date selector with an optional time selector.</span></span>
- <span data-ttu-id="ec14d-117">`MultichoiceInput`: 1 つの選択または複数の選択を提供する選択肢の列挙リストです。</span><span class="sxs-lookup"><span data-stu-id="ec14d-117">`MultichoiceInput`: An enumerated list of choices offering either a single selection or multiple selections.</span></span>

<span data-ttu-id="ec14d-118">`MultichoiceInput` では、最初にすべて展開した状態でリストを表示するかどうかを制御する `style` プロパティがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ec14d-118">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="ec14d-119">既定値は、 `style` 次の値によって `isMultiSelect` 異なります。</span><span class="sxs-lookup"><span data-stu-id="ec14d-119">The default value of `style` depends on the value of `isMultiSelect` as follows:</span></span>

| `isMultiSelect` | <span data-ttu-id="ec14d-120">`style` 既定</span><span class="sxs-lookup"><span data-stu-id="ec14d-120">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="ec14d-121">`false` または指定なし</span><span class="sxs-lookup"><span data-stu-id="ec14d-121">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="ec14d-122">コンパクト なスタイルで複数選択リストを表示するには、 と の両方を指定する `"isMultiSelect": true` 必要があります `"style": true` 。</span><span class="sxs-lookup"><span data-stu-id="ec14d-122">To display the multiselect list in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="ec14d-123">コネクタ カードのアクションの詳細については、「Actions」を [参照してください](/outlook/actionable-messages/card-reference#actions)。</span><span class="sxs-lookup"><span data-stu-id="ec14d-123">For more information on connector card actions, see [Actions](/outlook/actionable-messages/card-reference#actions).</span></span>

> [!NOTE]
> * <span data-ttu-id="ec14d-124">Microsoft Teams で `style` プロパティに `compact` を指定することは、Microsoft Outlook で `style` プロパティに `normal` を指定することと同じです。</span><span class="sxs-lookup"><span data-stu-id="ec14d-124">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="ec14d-125">HttpPOST アクションでは、ベアラー トークンは要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="ec14d-125">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="ec14d-126">このトークンには、アクションを実行した Office 365 ユーザーの Azure AD ID が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ec14d-126">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a><span data-ttu-id="ec14d-127">受信 Webhook または受信コネクタを介してOffice 365する</span><span class="sxs-lookup"><span data-stu-id="ec14d-127">Send a message through Incoming Webhook or Office 365 Connector</span></span>

<span data-ttu-id="ec14d-128">受信 Webhook または受信コネクタを介してメッセージをOffice 365するには、JSON ペイロードを Webhook URL に投稿します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-128">To send a message through your Incoming Webhook or Office 365 Connector, post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="ec14d-129">このペイロードは、コネクタ カードの形式Office 365[必要があります](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="ec14d-129">This payload must be in the form of an [Office 365 connector card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="ec14d-130">また、この JSON を使用して、テキスト入力、複数選択、日付と時刻の選択などのリッチ入力を含むカードを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-130">You can also use this JSON to create cards containing rich inputs, such as text entry, multiselect, or selecting date and time.</span></span> <span data-ttu-id="ec14d-131">カードを生成し、Webhook URL に投稿するコードは、ホストされている任意のサービスで実行できます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-131">The code that generates the card and posts it to the webhook URL can run on any hosted service.</span></span> <span data-ttu-id="ec14d-132">これらのカードは、アクション可能なメッセージの一部として定義され、カード[](~/task-modules-and-cards/what-are-cards.md)でサポートされ、Teams拡張機能で使用されます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-132">These cards are defined as part of actionable messages and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md), used in Teams bots and messaging extensions.</span></span>

### <a name="example-of-connector-message"></a><span data-ttu-id="ec14d-133">コネクタ メッセージの例</span><span class="sxs-lookup"><span data-stu-id="ec14d-133">Example of connector message</span></span>

<span data-ttu-id="ec14d-134">コネクタ メッセージの例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ec14d-134">An example of connector message is as follows:</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
        "activitySubtitle": "On Project Tango",
        "activityImage": "https://teamsnodesample.azurewebsites.net/static/img/image5.png",
        "facts": [{
            "name": "Assigned to",
            "value": "Unassigned"
        }, {
            "name": "Due date",
            "value": "Mon May 01 2017 17:07:18 GMT-0700 (Pacific Daylight Time)"
        }, {
            "name": "Status",
            "value": "Not started"
        }],
        "markdown": true
    }],
    "potentialAction": [{
        "@type": "ActionCard",
        "name": "Add a comment",
        "inputs": [{
            "@type": "TextInput",
            "id": "comment",
            "isMultiline": false,
            "title": "Add a comment here for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Add comment",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Set due date",
        "inputs": [{
            "@type": "DateInput",
            "id": "dueDate",
            "title": "Enter a due date for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Change status",
        "inputs": [{
            "@type": "MultichoiceInput",
            "id": "list",
            "title": "Select a status",
            "isMultiSelect": "false",
            "choices": [{
                "display": "In Progress",
                "value": "1"
            }, {
                "display": "Active",
                "value": "2"
            }, {
                "display": "Closed",
                "value": "3"
            }]
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

<span data-ttu-id="ec14d-135">このメッセージは、チャネルに次のカードを提供します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-135">This message provides the following card in the channel:</span></span>

![コネクタ カードのスクリーンショット](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a><span data-ttu-id="ec14d-137">cURL と PowerShell を使用してメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="ec14d-137">Send messages using cURL and PowerShell</span></span>

# <a name="curl"></a>[<span data-ttu-id="ec14d-138">cURL</span><span class="sxs-lookup"><span data-stu-id="ec14d-138">cURL</span></span>](#tab/cURL)

<span data-ttu-id="ec14d-139">**cURL を使用して Webhook にメッセージを投稿するには**</span><span class="sxs-lookup"><span data-stu-id="ec14d-139">**To post a message in the webhook with cURL**</span></span>

1. <span data-ttu-id="ec14d-140">を使用して cURL をインストールします https://curl.haxx.se/ 。</span><span class="sxs-lookup"><span data-stu-id="ec14d-140">Install cURL using: https://curl.haxx.se/.</span></span>

1. <span data-ttu-id="ec14d-141">コマンド ラインから、次の cURL コマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-141">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="ec14d-142">POST が成功した場合は、単純な **1** 出力を表示する必要があります `curl` 。</span><span class="sxs-lookup"><span data-stu-id="ec14d-142">If the POST succeeds, you must see a simple **1** output by `curl`.</span></span>

1. <span data-ttu-id="ec14d-143">新しいMicrosoft Teamsのクライアントを確認します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-143">Check the Microsoft Teams client for the new card posted.</span></span>

# <a name="powershell"></a>[<span data-ttu-id="ec14d-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec14d-144">PowerShell</span></span>](#tab/PowerShell)

 <span data-ttu-id="ec14d-145">前提条件: PowerShell のインストールとその基本的な使用方法に関する知識。</span><span class="sxs-lookup"><span data-stu-id="ec14d-145">Prerequisite: Installation of PowerShell and familiarization with its basic usage.</span></span>

<span data-ttu-id="ec14d-146">**PowerShell を使用して Webhook にメッセージを投稿するには**</span><span class="sxs-lookup"><span data-stu-id="ec14d-146">**To post a message to the webhook with PowerShell**</span></span>

1. <span data-ttu-id="ec14d-147">PowerShell プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-147">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="ec14d-148">POST が成功した場合は、単純な **1** 出力を表示する必要があります `Invoke-RestMethod` 。</span><span class="sxs-lookup"><span data-stu-id="ec14d-148">If the POST succeeds, you must see a simple **1** output by `Invoke-RestMethod`.</span></span>

1. <span data-ttu-id="ec14d-149">Webhook URL に関連付けられている Microsoft Teams チャネルを確認します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-149">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="ec14d-150">チャネルに投稿された新しいカードを確認できます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-150">You can see the new card posted to the channel.</span></span> <span data-ttu-id="ec14d-151">コネクタを使用してアプリをテストまたは発行する前に、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ec14d-151">Before you use the connector to test or publish your app, you must do the following:</span></span>

    - <span data-ttu-id="ec14d-152">[アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="ec14d-152">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
    - <span data-ttu-id="ec14d-153">マニフェストの `icons` 部分を URL ではなくアイコンのファイル名に変更します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-153">Modify the `icons` portion of the manifest to the file names of the icons instead of URLs.</span></span>

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="ec14d-154">受信 Webhook を使用してアダプティブ カードを送信する</span><span class="sxs-lookup"><span data-stu-id="ec14d-154">Send Adaptive Cards using an Incoming Webhook</span></span>

> [!NOTE]
> * <span data-ttu-id="ec14d-155">ネイティブのアダプティブ カード スキーマ要素 (ただし `Action.Submit` 、 を除く) はすべて完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ec14d-155">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="ec14d-156">サポートされているアクションは [**、Action.OpenURL、Action.ShowCard、**](https://adaptivecards.io/explorer/Action.OpenUrl.html)[**および Action.ToggleVisibility です**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。 [](https://adaptivecards.io/explorer/Action.ShowCard.html)</span><span class="sxs-lookup"><span data-stu-id="ec14d-156">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

<span data-ttu-id="ec14d-157">**受信 Webhook を介してアダプティブ カードを送信するには**</span><span class="sxs-lookup"><span data-stu-id="ec14d-157">**To send Adaptive Cards through an Incoming Webhook**</span></span>

1. <span data-ttu-id="ec14d-158">[カスタム Webhook をカスタム webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) Teams。</span><span class="sxs-lookup"><span data-stu-id="ec14d-158">[Setup a custom webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) in Teams.</span></span>
1. <span data-ttu-id="ec14d-159">次のコードを使用してアダプティブ カード JSON ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-159">Create Adaptive Card JSON file using the following code:</span></span>

    ```json
    {
       "type":"message",
       "attachments":[
          {
             "contentType":"application/vnd.microsoft.card.adaptive",
             "contentUrl":null,
             "content":{
                "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
                "type":"AdaptiveCard",
                "version":"1.2",
                "body":[
                    {
                    "type": "TextBlock",
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    <span data-ttu-id="ec14d-160">アダプティブ カード JSON ファイルのプロパティは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ec14d-160">The properties for Adaptive Card JSON file are as follows:</span></span>

    * <span data-ttu-id="ec14d-161">`"type"` フィールドは `"message"` であることが必要です。</span><span class="sxs-lookup"><span data-stu-id="ec14d-161">The `"type"` field must be `"message"`.</span></span>
    * <span data-ttu-id="ec14d-162">`"attachments"` 配列には、カード オブジェクトのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ec14d-162">The `"attachments"` array contains a set of card objects.</span></span>
    * <span data-ttu-id="ec14d-163">フィールド `"contentType"` はアダプティブ カードの種類に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ec14d-163">The `"contentType"` field must be set to Adaptive Card type.</span></span>
    * <span data-ttu-id="ec14d-164">`"content"` オブジェクトは、JSON で書式設定されたカードです。</span><span class="sxs-lookup"><span data-stu-id="ec14d-164">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="ec14d-165">Postman でアダプティブ カードをテストする:</span><span class="sxs-lookup"><span data-stu-id="ec14d-165">Test your Adaptive Card with Postman:</span></span>

    * <span data-ttu-id="ec14d-166">Postman を使用して [アダプティブ カードをテスト](https://www.postman.com) し、受信 Webhook をセットアップするために作成された POST 要求を URL に送信します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-166">Test the Adaptive Card using [Postman](https://www.postman.com) to send a POST request to the URL, created to set up Incoming Webhook.</span></span>
    * <span data-ttu-id="ec14d-167">要求の本文に JSON ファイルを貼り付け、アダプティブ カード メッセージを [アダプティブ カード] Teams。</span><span class="sxs-lookup"><span data-stu-id="ec14d-167">Paste the JSON file in the body of the request and view the Adaptive Card message in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="ec14d-168">アダプティブ カード のコード [サンプルとテンプレートを使用して](https://adaptivecards.io/samples) POST 要求の本文をテストします。</span><span class="sxs-lookup"><span data-stu-id="ec14d-168">Use Adaptive Card [code samples and templates](https://adaptivecards.io/samples) to test the body of POST request.</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="ec14d-169">コネクタのレート制限</span><span class="sxs-lookup"><span data-stu-id="ec14d-169">Rate limiting for connectors</span></span>

<span data-ttu-id="ec14d-170">アプリケーション レートの制限は、コネクタまたは受信 Webhook がチャネルで生成できるトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-170">Application rate limits control the traffic that a connector or an Incoming Webhook is permitted to generate on a channel.</span></span> <span data-ttu-id="ec14d-171">Teamsレート ウィンドウと増分カウンターを使用して、数秒で測定された要求を追跡します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-171">Teams track requests using a fixed rate window and incremental counter measured in seconds.</span></span> <span data-ttu-id="ec14d-172">1 秒間に 4 つ以上の要求が行われた場合、固定レートの期間ウィンドウが更新されるまで、クライアント接続が調整されます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-172">If more than four requests are made in a second, the client connection is throttled until the window refreshes for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="ec14d-173">1 秒あたりのトランザクションのしきい値</span><span class="sxs-lookup"><span data-stu-id="ec14d-173">Transactions per second thresholds</span></span>

<span data-ttu-id="ec14d-174">次の表に、時間ベースのトランザクションの詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-174">The following table provides the time based transaction details:</span></span>

| <span data-ttu-id="ec14d-175">時間 (秒)</span><span class="sxs-lookup"><span data-stu-id="ec14d-175">Time in seconds</span></span>  | <span data-ttu-id="ec14d-176">許可される最大要求数</span><span class="sxs-lookup"><span data-stu-id="ec14d-176">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="ec14d-177">1 </span><span class="sxs-lookup"><span data-stu-id="ec14d-177">1</span></span>   | <span data-ttu-id="ec14d-178">4 </span><span class="sxs-lookup"><span data-stu-id="ec14d-178">4</span></span>  |  
| <span data-ttu-id="ec14d-179">30</span><span class="sxs-lookup"><span data-stu-id="ec14d-179">30</span></span>   | <span data-ttu-id="ec14d-180">60</span><span class="sxs-lookup"><span data-stu-id="ec14d-180">60</span></span>  |  
| <span data-ttu-id="ec14d-181">3600</span><span class="sxs-lookup"><span data-stu-id="ec14d-181">3600</span></span>   | <span data-ttu-id="ec14d-182">100</span><span class="sxs-lookup"><span data-stu-id="ec14d-182">100</span></span>  |
| <span data-ttu-id="ec14d-183">7200</span><span class="sxs-lookup"><span data-stu-id="ec14d-183">7200</span></span> | <span data-ttu-id="ec14d-184">150</span><span class="sxs-lookup"><span data-stu-id="ec14d-184">150</span></span>  |
| <span data-ttu-id="ec14d-185">86400</span><span class="sxs-lookup"><span data-stu-id="ec14d-185">86400</span></span>  | <span data-ttu-id="ec14d-186">1800</span><span class="sxs-lookup"><span data-stu-id="ec14d-186">1800</span></span>  |

<span data-ttu-id="ec14d-187">指数 [バックオフによる再試行ロジック](/azure/architecture/patterns/retry) は、要求が 1 秒以内に制限を超える場合のレート制限を軽減できます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-187">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="ec14d-188">ベスト [プラクティスに従](../../bots/how-to/rate-limit.md) って、レート制限に達しないようにします。</span><span class="sxs-lookup"><span data-stu-id="ec14d-188">Follow [best practices](../../bots/how-to/rate-limit.md) to avoid hitting the rate limits.</span></span>

> [!NOTE]
> <span data-ttu-id="ec14d-189">指数 [バックオフによる再試行ロジック](/azure/architecture/patterns/retry) は、要求が 1 秒以内に制限を超える場合のレート制限を軽減できます。</span><span class="sxs-lookup"><span data-stu-id="ec14d-189">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="ec14d-190">レート制限を避けるために、[HTTP 429 応答](../../bots/how-to/rate-limit.md#handle-http-429-responses)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ec14d-190">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

```csharp
// Please note that response body needs to be extracted and read 
// as Connectors do not throw 429s
try
{
    // Perform Connector POST operation     
    var httpResponseMessage = await _client.PostAsync(IncomingWebhookUrl, new StringContent(content));
    // Read response content
    var responseContent = await httpResponseMessage.Content.ReadAsStringAsync();
    if (responseContent.Contains("Microsoft Teams endpoint returned HTTP error 429")) 
    {
        // initiate retry logic
    }
}
```

<span data-ttu-id="ec14d-191">これらの制限は、コネクタによるチャネルの spamming を減らすために設定され、ユーザーに最適なエクスペリエンスを保証します。</span><span class="sxs-lookup"><span data-stu-id="ec14d-191">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to users.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec14d-192">関連項目</span><span class="sxs-lookup"><span data-stu-id="ec14d-192">See also</span></span>

* [<span data-ttu-id="ec14d-193">Office 365コネクタのMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="ec14d-193">Office 365 Connectors for Microsoft Teams</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="ec14d-194">受信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="ec14d-194">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="ec14d-195">送信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="ec14d-195">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
