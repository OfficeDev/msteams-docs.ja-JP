---
title: コネクタと Webhook にメッセージを送信する
description: Microsoft Teams で Office 365 コネクタを使用する方法について説明します。
localization_priority: Priority
keywords: Teams o365 コネクタ
ms.openlocfilehash: 871253e6c902b1e07e002a7c94dbf3ab11dea29c
ms.sourcegitcommit: 4275a502f9f7742da2900c79e19551e481c9e48a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797046"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="ff206-104">コネクタと Webhook にメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="ff206-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="ff206-105">Office 365 コネクタまたは着信 Webhook 経由でメッセージを送信するには、Webhook URL に JSON ペイロードを投稿します。</span><span class="sxs-lookup"><span data-stu-id="ff206-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="ff206-106">通常、このペイロードは [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)の形式になります。</span><span class="sxs-lookup"><span data-stu-id="ff206-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="ff206-107">この JSON を使用して、テキスト入力、複数選択、または日付と時刻の選択など、リッチな入力を含むカードを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="ff206-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="ff206-108">カードを生成して Webhook URL への投稿を行うコードは、いずれのホステッド サービスでも実行できます。</span><span class="sxs-lookup"><span data-stu-id="ff206-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="ff206-109">これらのカードは、操作可能なメッセージの一部として定義されています。また、Teams ボットやメッセージング拡張機能で使用される[カード](~/task-modules-and-cards/what-are-cards.md)でもサポートされます。</span><span class="sxs-lookup"><span data-stu-id="ff206-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="ff206-110">コネクタ メッセージの例</span><span class="sxs-lookup"><span data-stu-id="ff206-110">Example connector message</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
        }]
        {
            "@type": "OpenUri",
            "name": "Learn More",
            "targets": [{ "os": "default", "uri": "https://docs.microsoft.com/outlook/actionable-messages" }]
        }
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
            "target": "http://..."
        }]
    }]
}
```

<span data-ttu-id="ff206-111">このメッセージにより、チャネルに次のカードが生成されます。</span><span class="sxs-lookup"><span data-stu-id="ff206-111">This message produces the following card in the channel.</span></span>

![コネクタ カードのスクリーンショット](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="ff206-113">操作可能なメッセージの作成</span><span class="sxs-lookup"><span data-stu-id="ff206-113">Creating actionable messages</span></span>

<span data-ttu-id="ff206-114">前のセクションの例では、3 つのボタンがカードに表示されています。</span><span class="sxs-lookup"><span data-stu-id="ff206-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="ff206-115">各ボタンは、`ActionCard` アクションを使用して `potentialAction` プロパティに定義されています。それぞれには、入力の種類 (テキスト フィールド、日付の選択、または複数選択リスト) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ff206-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="ff206-116">それぞれの `ActionCard` アクションには、`HttpPOST` など、関連付けられたアクションがあります。</span><span class="sxs-lookup"><span data-stu-id="ff206-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="ff206-117">コネクタ カードでは、3 種類のアクションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ff206-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="ff206-118">`ActionCard` 1 つまたは複数の入力の種類と、関連付けられたアクションを示します</span><span class="sxs-lookup"><span data-stu-id="ff206-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="ff206-119">`HttpPOST` POST 要求を URL に送信します</span><span class="sxs-lookup"><span data-stu-id="ff206-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="ff206-120">`OpenUri` URI を別のブラウザーまたはアプリで開きます。必要に応じて、オペレーティング システムに基づいて異なる URI をターゲットにします。</span><span class="sxs-lookup"><span data-stu-id="ff206-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="ff206-121">`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ff206-121">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="ff206-122">`TextInput` 単一行または複数行の、オプションとして長さ制限が付いたテキスト フィールド</span><span class="sxs-lookup"><span data-stu-id="ff206-122">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="ff206-123">`DateInput` オプションとして時間選択が付いた、日付選択</span><span class="sxs-lookup"><span data-stu-id="ff206-123">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="ff206-124">`MultichoiceInput` 1つまたは複数の選択を行える、選択肢を列挙したリスト</span><span class="sxs-lookup"><span data-stu-id="ff206-124">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="ff206-125">`MultichoiceInput` では、最初にすべて展開した状態でリストを表示するかどうかを制御する `style` プロパティがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ff206-125">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="ff206-126">`style` の既定値は、`isMultiSelect`の値によって決まります。</span><span class="sxs-lookup"><span data-stu-id="ff206-126">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="ff206-127">`style` 既定</span><span class="sxs-lookup"><span data-stu-id="ff206-127">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="ff206-128">`false` または指定なし</span><span class="sxs-lookup"><span data-stu-id="ff206-128">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="ff206-129">複数選択リストを最初はコンパクトなスタイルで表示させる場合は、`"isMultiSelect": true` と `"style": true` の両方を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff206-129">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

> [!NOTE]
> <span data-ttu-id="ff206-130">Microsoft Teams で `style` プロパティに `compact` を指定することは、Microsoft Outlook で `style` プロパティに `normal` を指定することと同じです。</span><span class="sxs-lookup"><span data-stu-id="ff206-130">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>

<span data-ttu-id="ff206-131">コネクタ カードのアクションのその他の詳細については、操作可能なメッセージ カードのレファレンスの、「**[アクション](/outlook/actionable-messages/card-reference#actions)**」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff206-131">For all other details about Connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="ff206-132">カスタム着信 Webhook の設定</span><span class="sxs-lookup"><span data-stu-id="ff206-132">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="ff206-133">単純なカードをコネクタに送信する方法を見るには、次の手順に従って操作を行ってください。</span><span class="sxs-lookup"><span data-stu-id="ff206-133">Follow these steps to see how to send a simple card to a Connector.</span></span>

1. <span data-ttu-id="ff206-134">Microsoft Teams で、チャネル名の横にある [**その他のオプション**] (**&#8943;**) を選択し、[**コネクタ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff206-134">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
2. <span data-ttu-id="ff206-135">コネクタのリストをスクロールして [**着信 Webhook**] を選択し、次に [**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff206-135">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
3. <span data-ttu-id="ff206-136">Webhook の名前を入力し、Webhook からのデータと関連づける画像を更新し、[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff206-136">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
4. <span data-ttu-id="ff206-137">Webhook をクリップボードにコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="ff206-137">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="ff206-138">Microsoft Teams に情報を送信するには、Webhook URL が必要です。</span><span class="sxs-lookup"><span data-stu-id="ff206-138">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
5. <span data-ttu-id="ff206-139">[**完了**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff206-139">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="ff206-140">cURL を使用してメッセージを Webhook に投稿する</span><span class="sxs-lookup"><span data-stu-id="ff206-140">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="ff206-141">次の手順では、[cURL](https://curl.haxx.se/) を使用します。</span><span class="sxs-lookup"><span data-stu-id="ff206-141">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="ff206-142">これが既にインストールされており、基本的な使用方法に精通しているものみなします。</span><span class="sxs-lookup"><span data-stu-id="ff206-142">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="ff206-143">コマンド ラインから、次の cURL コマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ff206-143">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="ff206-144">POST が成功すると、単に "**1**" という `curl` の出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff206-144">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
3. <span data-ttu-id="ff206-145">Microsoft Team クライアントを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff206-145">Check the Microsoft Team client.</span></span> <span data-ttu-id="ff206-146">チームに新しいカードが投稿されるはずです。</span><span class="sxs-lookup"><span data-stu-id="ff206-146">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="ff206-147">PowerShell を使用して Webhook にメッセージを投稿します。</span><span class="sxs-lookup"><span data-stu-id="ff206-147">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="ff206-148">次の手順では、PowerShell を使用します。</span><span class="sxs-lookup"><span data-stu-id="ff206-148">The following steps use PowerShell.</span></span> <span data-ttu-id="ff206-149">これが既にインストールされており、基本的な使用方法に精通しているものみなします。</span><span class="sxs-lookup"><span data-stu-id="ff206-149">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="ff206-150">PowerShell プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ff206-150">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="ff206-151">POST が成功すると、単に "**1**" という `Invoke-RestMethod` の出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff206-151">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
3. <span data-ttu-id="ff206-152">Webhook URL に関連付けられている Microsoft Teams チャネルを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff206-152">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="ff206-153">チャネルに新しいカードが投稿されているはずです。</span><span class="sxs-lookup"><span data-stu-id="ff206-153">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="ff206-154">[アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="ff206-154">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="ff206-155">マニフェストの `icons` の部分を変更し、アイコンの URL ではなくアイコンのファイル名を参照するようにします。</span><span class="sxs-lookup"><span data-stu-id="ff206-155">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="ff206-156">次の manifest.json ファイルには、アプリをテストして送信するために必要な基本的な要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ff206-156">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="ff206-157">次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ff206-157">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="ff206-158">コネクタを使用した manifest.json の例</span><span class="sxs-lookup"><span data-stu-id="ff206-158">Example manifest.json with connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="ff206-159">受信 Webhook を使用してアダプティブ カードを送信する</span><span class="sxs-lookup"><span data-stu-id="ff206-159">Send adaptive cards using an incoming webhook</span></span>

> [!NOTE]
>
> <span data-ttu-id="ff206-160">✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="ff206-160">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="ff206-161">✔ サポートされているアクションは [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、および [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) です。</span><span class="sxs-lookup"><span data-stu-id="ff206-161">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a><span data-ttu-id="ff206-162">受信 Webhook を通して [アダプティブ カード](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) を送信するためのフローは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ff206-162">The flow for sending [adaptive cards](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via an incoming webhook is as follows:</span></span>

<span data-ttu-id="ff206-163">**1.** [カスタム webhook](#setting-up-a-custom-incoming-webhook) を Teams に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff206-163">**1.** [Setup a custom webhook](#setting-up-a-custom-incoming-webhook) in Teams.</span></span></br></br>
<span data-ttu-id="ff206-164">**2.** アダプティブ カード JSON ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ff206-164">**2.** Create your adaptive card JSON file:</span></span>

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
                "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)",
                }
            ]
         }
      }
   ]
}
```

> [!div class="checklist"]
>
> - <span data-ttu-id="ff206-165">`"type"` フィールドは `"message"` であることが必要です。</span><span class="sxs-lookup"><span data-stu-id="ff206-165">The `"type"` field must be `"message"`.</span></span>
> - <span data-ttu-id="ff206-166">`"attachments"` 配列には、カード オブジェクトのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ff206-166">The `"attachments"` array contains a set of card objects.</span></span>
> - <span data-ttu-id="ff206-167">`"contentType"` フィールドにはアダプティブカードの種類が設定されていることが必要です。</span><span class="sxs-lookup"><span data-stu-id="ff206-167">The `"contentType"` field must be set to adaptive card type.</span></span>
> - <span data-ttu-id="ff206-168">`"content"` オブジェクトは、JSON で書式設定されたカードです。</span><span class="sxs-lookup"><span data-stu-id="ff206-168">The `"content"` object is the card formatted in JSON.</span></span>

<span data-ttu-id="ff206-169">**3.** Postman でアダプティブ カードをテストする</span><span class="sxs-lookup"><span data-stu-id="ff206-169">**3.** Test your adaptive card with Postman</span></span>

<span data-ttu-id="ff206-170">[Postman](https://www.postman.com) を使用して、受信 Webhook の設定時に作成した URL に POST 要求を送信することで、アダプティブカードをテストできます。</span><span class="sxs-lookup"><span data-stu-id="ff206-170">You can test your adaptive card using [Postman](https://www.postman.com) to send a POST request to the URL that you created when you setup your incoming webhook.</span></span> <span data-ttu-id="ff206-171">JSON ファイルを要求の本文に貼り付け、Teams でアダプティブ カード メッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="ff206-171">Paste your JSON file in the body of the request and view your adaptive card message in Teams.</span></span>

>[!TIP]
> <span data-ttu-id="ff206-172">テストの Post 要求の本文には、アダプティブ カード コードの [サンプルとテンプレート](https://adaptivecards.io/samples) を使用できます。</span><span class="sxs-lookup"><span data-stu-id="ff206-172">You can use adaptive card code [Samples and Templates](https://adaptivecards.io/samples) for the body of your test Post request.</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="ff206-173">コネクタをテストする</span><span class="sxs-lookup"><span data-stu-id="ff206-173">Testing your connector</span></span>

<span data-ttu-id="ff206-174">コネクタをテストするには、他のアプリと同じ方法でコネクタをチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="ff206-174">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="ff206-175">(前のセクションの指示に従って変更された) コネクタ開発者ダッシュボードからのマニフェスト ファイルと 2 つのアイコン ファイルを使用して .zip パッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ff206-175">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="ff206-176">アプリをアップロードしたら、任意のチャネルからコネクタ リストを開きます。</span><span class="sxs-lookup"><span data-stu-id="ff206-176">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="ff206-177">一番下までスクロールして、アプリが [**アップロード済み**] セクションに表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff206-177">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![コネクタ ダイアログ ボックスの [アップロード済み] セクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="ff206-179">構成機能を起動できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ff206-179">You can now launch the configuration experience.</span></span> <span data-ttu-id="ff206-180">このフローは、ポップアップ ウィンドウを通してすべて Microsoft Teams 内で行われる点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="ff206-180">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="ff206-181">現在、この動作は、ここで作成したコネクタの構成機能とは異なります。Microsoft では、構成機能の共通化に取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="ff206-181">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="ff206-182">`HttpPOST` アクションが正常に動作していることを確認するには、[カスタム着信 Webhook](#setting-up-a-custom-incoming-webhook) を使用します。</span><span class="sxs-lookup"><span data-stu-id="ff206-182">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="ff206-183">コネクタのレート制限</span><span class="sxs-lookup"><span data-stu-id="ff206-183">Rate limiting for connectors</span></span>

<span data-ttu-id="ff206-184">アプリケーション レートの制限は、コネクタまたは着信 Webhook がチャネルで発生させることが許可されているトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="ff206-184">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="ff206-185">Teams は、固定レート ウィンドウと増分カウンター (秒単位で測定) を使用して、要求を追跡します。</span><span class="sxs-lookup"><span data-stu-id="ff206-185">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="ff206-186">要求が多すぎる場合は、ウィンドウが更新されるまで (つまり固定レートの期間中)、クライアント接続が制限されます。</span><span class="sxs-lookup"><span data-stu-id="ff206-186">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="ff206-187">**1 秒あたりのトランザクションのしきい値**</span><span class="sxs-lookup"><span data-stu-id="ff206-187">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="ff206-188">時間 (秒)</span><span class="sxs-lookup"><span data-stu-id="ff206-188">Time (seconds)</span></span>  | <span data-ttu-id="ff206-189">許可される最大要求数</span><span class="sxs-lookup"><span data-stu-id="ff206-189">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="ff206-190">1</span><span class="sxs-lookup"><span data-stu-id="ff206-190">1</span></span>   | <span data-ttu-id="ff206-191">4</span><span class="sxs-lookup"><span data-stu-id="ff206-191">4</span></span>  |  
| <span data-ttu-id="ff206-192">30</span><span class="sxs-lookup"><span data-stu-id="ff206-192">30</span></span>   | <span data-ttu-id="ff206-193">60</span><span class="sxs-lookup"><span data-stu-id="ff206-193">60</span></span>  |  
| <span data-ttu-id="ff206-194">3600</span><span class="sxs-lookup"><span data-stu-id="ff206-194">3600</span></span>   | <span data-ttu-id="ff206-195">100</span><span class="sxs-lookup"><span data-stu-id="ff206-195">100</span></span>  |
| <span data-ttu-id="ff206-196">7200</span><span class="sxs-lookup"><span data-stu-id="ff206-196">7200</span></span> | <span data-ttu-id="ff206-197">150</span><span class="sxs-lookup"><span data-stu-id="ff206-197">150</span></span>  |
| <span data-ttu-id="ff206-198">86400</span><span class="sxs-lookup"><span data-stu-id="ff206-198">86400</span></span>  | <span data-ttu-id="ff206-199">1800</span><span class="sxs-lookup"><span data-stu-id="ff206-199">1800</span></span>  |

<span data-ttu-id="ff206-200">「[Office 365 コネクタ — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)」*も参照*</span><span class="sxs-lookup"><span data-stu-id="ff206-200">*See also* [Office 365 Connectors — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span></span>

<span data-ttu-id="ff206-201">次のような[指数バックオフを使用した再試行ロジック](/azure/architecture/patterns/retry)は、要求が 1 秒以内に制限を超えてしまうケースで、レート制限を緩和します。</span><span class="sxs-lookup"><span data-stu-id="ff206-201">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="ff206-202">レート制限に達しないよう、「[ベスト プラクティス](../../bots/how-to/rate-limit.md#best-practices)」に従ってください。</span><span class="sxs-lookup"><span data-stu-id="ff206-202">Please follow [best practices](../../bots/how-to/rate-limit.md#best-practices) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="ff206-203">これらの制限は、大量のメッセージがコネクタからチャネルに送信されることを減らすために設定されており、エンドユーザーのために最適な操作性を確保するためのものです。</span><span class="sxs-lookup"><span data-stu-id="ff206-203">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>
