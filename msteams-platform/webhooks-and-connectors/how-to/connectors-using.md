---
title: コネクタと Webhook にメッセージを送信する
description: Microsoft Teams で Office 365 コネクタを使用する方法について説明します。
ms.topic: how-to
localization_priority: Normal
keywords: Teams o365 コネクタ
ms.openlocfilehash: 96092e4589f218a96f31ce05339b89acb82f1fd7
ms.sourcegitcommit: 20764037458026e5870ee3975b966404103af650
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2021
ms.locfileid: "52583737"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="81b09-104">コネクタと Webhook にメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="81b09-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="81b09-105">Office 365 コネクタまたは着信 Webhook 経由でメッセージを送信するには、Webhook URL に JSON ペイロードを投稿します。</span><span class="sxs-lookup"><span data-stu-id="81b09-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="81b09-106">通常、このペイロードは [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)の形式になります。</span><span class="sxs-lookup"><span data-stu-id="81b09-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="81b09-107">この JSON を使用して、テキスト入力、複数選択、または日付と時刻の選択など、リッチな入力を含むカードを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="81b09-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="81b09-108">カードを生成して Webhook URL への投稿を行うコードは、いずれのホステッド サービスでも実行できます。</span><span class="sxs-lookup"><span data-stu-id="81b09-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="81b09-109">これらのカードは、操作可能なメッセージの一部として定義されています。また、Teams ボットやメッセージング拡張機能で使用される[カード](~/task-modules-and-cards/what-are-cards.md)でもサポートされます。</span><span class="sxs-lookup"><span data-stu-id="81b09-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="81b09-110">コネクタ メッセージの例</span><span class="sxs-lookup"><span data-stu-id="81b09-110">Example connector message</span></span>

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

<span data-ttu-id="81b09-111">このメッセージは、チャネルに次のカードを生成します。</span><span class="sxs-lookup"><span data-stu-id="81b09-111">This message produces the following card in the channel:</span></span>

![コネクタ カードのスクリーンショット](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="81b09-113">操作可能なメッセージの作成</span><span class="sxs-lookup"><span data-stu-id="81b09-113">Creating actionable messages</span></span>

<span data-ttu-id="81b09-114">前のセクションの例では、3 つのボタンがカードに表示されています。</span><span class="sxs-lookup"><span data-stu-id="81b09-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="81b09-115">各ボタンは、`ActionCard` アクションを使用して `potentialAction` プロパティに定義されています。それぞれには、入力の種類 (テキスト フィールド、日付の選択、または複数選択リスト) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="81b09-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="81b09-116">それぞれの `ActionCard` アクションには、`HttpPOST` など、関連付けられたアクションがあります。</span><span class="sxs-lookup"><span data-stu-id="81b09-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="81b09-117">コネクタ カードでは、3 種類のアクションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="81b09-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="81b09-118">`ActionCard` 1 つまたは複数の入力の種類と、関連付けられたアクションを示します</span><span class="sxs-lookup"><span data-stu-id="81b09-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="81b09-119">`HttpPOST` POST 要求を URL に送信します</span><span class="sxs-lookup"><span data-stu-id="81b09-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="81b09-120">`OpenUri` URI を別のブラウザーまたはアプリで開きます。必要に応じて、オペレーティング システムに基づいて異なる URI をターゲットにします。</span><span class="sxs-lookup"><span data-stu-id="81b09-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="81b09-121">`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="81b09-121">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="81b09-122">`TextInput` 単一行または複数行の、オプションとして長さ制限が付いたテキスト フィールド</span><span class="sxs-lookup"><span data-stu-id="81b09-122">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="81b09-123">`DateInput` オプションとして時間選択が付いた、日付選択</span><span class="sxs-lookup"><span data-stu-id="81b09-123">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="81b09-124">`MultichoiceInput` 1つまたは複数の選択を行える、選択肢を列挙したリスト</span><span class="sxs-lookup"><span data-stu-id="81b09-124">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="81b09-125">`MultichoiceInput` では、最初にすべて展開した状態でリストを表示するかどうかを制御する `style` プロパティがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="81b09-125">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="81b09-126">`style` の既定値は、`isMultiSelect`の値によって決まります。</span><span class="sxs-lookup"><span data-stu-id="81b09-126">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="81b09-127">`style` 既定</span><span class="sxs-lookup"><span data-stu-id="81b09-127">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="81b09-128">`false` または指定なし</span><span class="sxs-lookup"><span data-stu-id="81b09-128">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="81b09-129">複数選択リストを最初はコンパクトなスタイルで表示させる場合は、`"isMultiSelect": true` と `"style": true` の両方を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="81b09-129">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="81b09-130">コネクタ カード アクションの詳細については、アクション可能メッセージ カードの参考資料の [**アクション**] (/outlook/actionable-messages/card-reference#actions) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="81b09-130">For more information on Connector card actions, see **[Actions]**(/outlook/actionable-messages/card-reference#actions) in the actionable message card reference.</span></span>

> [!NOTE]
> <span data-ttu-id="81b09-131">Microsoft Teams で `style` プロパティに `compact` を指定することは、Microsoft Outlook で `style` プロパティに `normal` を指定することと同じです。</span><span class="sxs-lookup"><span data-stu-id="81b09-131">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> 
> <span data-ttu-id="81b09-132">HttpPOST アクションでは、ベアラー トークンは要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="81b09-132">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="81b09-133">このトークンには、アクションを実行した Office 365 ユーザーの Azure AD ID が含まれています。</span><span class="sxs-lookup"><span data-stu-id="81b09-133">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="81b09-134">カスタム着信 Webhook の設定</span><span class="sxs-lookup"><span data-stu-id="81b09-134">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="81b09-135">コネクタに単純なカードを送信する方法を確認するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="81b09-135">Follow these steps to see how to send a simple card to a Connector:</span></span>

1. <span data-ttu-id="81b09-136">Microsoft Teams で、チャネル名の横にある [**その他のオプション**] (**&#8943;**) を選択し、[**コネクタ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="81b09-136">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
1. <span data-ttu-id="81b09-137">コネクタのリストをスクロールして [**着信 Webhook**] を選択し、次に [**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="81b09-137">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
1. <span data-ttu-id="81b09-138">Webhook の名前を入力し、Webhook からのデータと関連づける画像を更新し、[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="81b09-138">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
1. <span data-ttu-id="81b09-139">Webhook をクリップボードにコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="81b09-139">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="81b09-140">Microsoft Teams に情報を送信するには、Webhook URL が必要です。</span><span class="sxs-lookup"><span data-stu-id="81b09-140">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
1. <span data-ttu-id="81b09-141">[**完了**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="81b09-141">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="81b09-142">cURL を使用してメッセージを Webhook に投稿する</span><span class="sxs-lookup"><span data-stu-id="81b09-142">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="81b09-143">次の手順では、[cURL](https://curl.haxx.se/) を使用します。</span><span class="sxs-lookup"><span data-stu-id="81b09-143">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="81b09-144">これが既にインストールされており、基本的な使用方法に精通しているものみなします。</span><span class="sxs-lookup"><span data-stu-id="81b09-144">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="81b09-145">コマンド ラインから、次の cURL コマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="81b09-145">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

1. <span data-ttu-id="81b09-146">POST が成功すると、単に "**1**" という `curl` の出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="81b09-146">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
1. <span data-ttu-id="81b09-147">Microsoft Team クライアントを確認します。</span><span class="sxs-lookup"><span data-stu-id="81b09-147">Check the Microsoft Team client.</span></span> <span data-ttu-id="81b09-148">チームに新しいカードが投稿されるはずです。</span><span class="sxs-lookup"><span data-stu-id="81b09-148">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="81b09-149">PowerShell を使用して Webhook にメッセージを投稿します。</span><span class="sxs-lookup"><span data-stu-id="81b09-149">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="81b09-150">次の手順では、PowerShell を使用します。</span><span class="sxs-lookup"><span data-stu-id="81b09-150">The following steps use PowerShell.</span></span> <span data-ttu-id="81b09-151">これが既にインストールされており、基本的な使用方法に精通しているものみなします。</span><span class="sxs-lookup"><span data-stu-id="81b09-151">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="81b09-152">PowerShell プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="81b09-152">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

1. <span data-ttu-id="81b09-153">POST が成功すると、単に "**1**" という `Invoke-RestMethod` の出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="81b09-153">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
1. <span data-ttu-id="81b09-154">Webhook URL に関連付けられている Microsoft Teams チャネルを確認します。</span><span class="sxs-lookup"><span data-stu-id="81b09-154">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="81b09-155">チャネルに新しいカードが投稿されているはずです。</span><span class="sxs-lookup"><span data-stu-id="81b09-155">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="81b09-156">[アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="81b09-156">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="81b09-157">マニフェストの `icons` の部分を変更し、アイコンの URL ではなくアイコンのファイル名を参照するようにします。</span><span class="sxs-lookup"><span data-stu-id="81b09-157">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="81b09-158">ファイルのmanifest.jsには、アプリのテストと送信に必要な基本的な要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="81b09-158">The following manifest.json file contains the basic elements needed to test and submit your app:</span></span>

> [!NOTE]
> <span data-ttu-id="81b09-159">次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="81b09-159">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="81b09-160">コネクタを使用した manifest.json の例</span><span class="sxs-lookup"><span data-stu-id="81b09-160">Example manifest.json with connector</span></span>

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

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="81b09-161">受信 Webhook を使用してアダプティブ カードを送信する</span><span class="sxs-lookup"><span data-stu-id="81b09-161">Send adaptive cards using an incoming webhook</span></span>

> [!NOTE]
>
> <span data-ttu-id="81b09-162">✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。</span><span class="sxs-lookup"><span data-stu-id="81b09-162">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="81b09-163">✔ サポートされているアクションは [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、および [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) です。</span><span class="sxs-lookup"><span data-stu-id="81b09-163">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a><span data-ttu-id="81b09-164">受信 Webhook を通して [アダプティブ カード](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) を送信するためのフローは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="81b09-164">The flow for sending [adaptive cards](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via an incoming webhook is as follows:</span></span>

1. <span data-ttu-id="81b09-165">[カスタム Webhook をカスタム webhook](#setting-up-a-custom-incoming-webhook) Teams。</span><span class="sxs-lookup"><span data-stu-id="81b09-165">[Setup a custom webhook](#setting-up-a-custom-incoming-webhook) in Teams.</span></span>
1. <span data-ttu-id="81b09-166">アダプティブ カード JSON ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="81b09-166">Create your adaptive card JSON file:</span></span>

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

    > [!div class="checklist"]
    >
    > - <span data-ttu-id="81b09-167">`"type"` フィールドは `"message"` であることが必要です。</span><span class="sxs-lookup"><span data-stu-id="81b09-167">The `"type"` field must be `"message"`.</span></span>
    > - <span data-ttu-id="81b09-168">`"attachments"` 配列には、カード オブジェクトのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="81b09-168">The `"attachments"` array contains a set of card objects.</span></span>
    > - <span data-ttu-id="81b09-169">`"contentType"` フィールドにはアダプティブカードの種類が設定されていることが必要です。</span><span class="sxs-lookup"><span data-stu-id="81b09-169">The `"contentType"` field must be set to adaptive card type.</span></span>
    > - <span data-ttu-id="81b09-170">`"content"` オブジェクトは、JSON で書式設定されたカードです。</span><span class="sxs-lookup"><span data-stu-id="81b09-170">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="81b09-171">Postman でアダプティブ カードをテストします。</span><span class="sxs-lookup"><span data-stu-id="81b09-171">Test your adaptive card with Postman.</span></span>

<span data-ttu-id="81b09-172">[Postman](https://www.postman.com) を使用して、受信 Webhook の設定時に作成した URL に POST 要求を送信することで、アダプティブカードをテストできます。</span><span class="sxs-lookup"><span data-stu-id="81b09-172">You can test your adaptive card using [Postman](https://www.postman.com) to send a POST request to the URL that you created when you setup your incoming webhook.</span></span> <span data-ttu-id="81b09-173">JSON ファイルを要求の本文に貼り付け、Teams でアダプティブ カード メッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="81b09-173">Paste your JSON file in the body of the request and view your adaptive card message in Teams.</span></span>

>[!TIP]
> <span data-ttu-id="81b09-174">テストの Post 要求の本文には、アダプティブ カード コードの [サンプルとテンプレート](https://adaptivecards.io/samples) を使用できます。</span><span class="sxs-lookup"><span data-stu-id="81b09-174">You can use adaptive card code [Samples and Templates](https://adaptivecards.io/samples) for the body of your test Post request.</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="81b09-175">コネクタをテストする</span><span class="sxs-lookup"><span data-stu-id="81b09-175">Testing your connector</span></span>

<span data-ttu-id="81b09-176">コネクタをテストするには、他のアプリと同じ方法でコネクタをチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="81b09-176">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="81b09-177">前のセクションと 2 .zipの指示に応じて変更されたコネクタ開発者ダッシュボードのマニフェスト ファイルを使用して、新しいパッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="81b09-177">You can create a .zip package using the manifest file from the Connectors Developer Dashboard which was modified as directed in the preceding section and the two icon files.</span></span>

<span data-ttu-id="81b09-178">アプリをアップロードしたら、任意のチャネルからコネクタ リストを開きます。</span><span class="sxs-lookup"><span data-stu-id="81b09-178">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="81b09-179">下にスクロールして、[アップロード] セクションにアプリ **を表示** します。</span><span class="sxs-lookup"><span data-stu-id="81b09-179">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

![コネクタ ダイアログ ボックスの [アップロード済み] セクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="81b09-181">構成機能を起動できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="81b09-181">You can now launch the configuration experience.</span></span> <span data-ttu-id="81b09-182">このフローは、ポップアップ ウィンドウを通してすべて Microsoft Teams 内で行われる点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="81b09-182">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="81b09-183">現在、この動作は、ここで作成したコネクタの構成機能とは異なります。Microsoft では、構成機能の共通化に取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="81b09-183">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="81b09-184">`HttpPOST` アクションが正常に動作していることを確認するには、[カスタム着信 Webhook](#setting-up-a-custom-incoming-webhook) を使用します。</span><span class="sxs-lookup"><span data-stu-id="81b09-184">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="81b09-185">コネクタのレート制限</span><span class="sxs-lookup"><span data-stu-id="81b09-185">Rate limiting for connectors</span></span>

<span data-ttu-id="81b09-186">アプリケーション レートの制限は、コネクタまたは着信 Webhook がチャネルで発生させることが許可されているトラフィックを制御します。</span><span class="sxs-lookup"><span data-stu-id="81b09-186">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="81b09-187">Teams は、固定レート ウィンドウと増分カウンター (秒単位で測定) を使用して、要求を追跡します。</span><span class="sxs-lookup"><span data-stu-id="81b09-187">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="81b09-188">要求が多すぎる場合は、ウィンドウが更新されるまで (つまり固定レートの期間中)、クライアント接続が制限されます。</span><span class="sxs-lookup"><span data-stu-id="81b09-188">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="81b09-189">**1 秒あたりのトランザクションのしきい値**</span><span class="sxs-lookup"><span data-stu-id="81b09-189">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="81b09-190">時間 (秒)</span><span class="sxs-lookup"><span data-stu-id="81b09-190">Time (seconds)</span></span>  | <span data-ttu-id="81b09-191">許可される最大要求数</span><span class="sxs-lookup"><span data-stu-id="81b09-191">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="81b09-192">1</span><span class="sxs-lookup"><span data-stu-id="81b09-192">1</span></span>   | <span data-ttu-id="81b09-193">4</span><span class="sxs-lookup"><span data-stu-id="81b09-193">4</span></span>  |  
| <span data-ttu-id="81b09-194">30</span><span class="sxs-lookup"><span data-stu-id="81b09-194">30</span></span>   | <span data-ttu-id="81b09-195">60</span><span class="sxs-lookup"><span data-stu-id="81b09-195">60</span></span>  |  
| <span data-ttu-id="81b09-196">3600</span><span class="sxs-lookup"><span data-stu-id="81b09-196">3600</span></span>   | <span data-ttu-id="81b09-197">100</span><span class="sxs-lookup"><span data-stu-id="81b09-197">100</span></span>  |
| <span data-ttu-id="81b09-198">7200</span><span class="sxs-lookup"><span data-stu-id="81b09-198">7200</span></span> | <span data-ttu-id="81b09-199">150</span><span class="sxs-lookup"><span data-stu-id="81b09-199">150</span></span>  |
| <span data-ttu-id="81b09-200">86400</span><span class="sxs-lookup"><span data-stu-id="81b09-200">86400</span></span>  | <span data-ttu-id="81b09-201">1800</span><span class="sxs-lookup"><span data-stu-id="81b09-201">1800</span></span>  |

<span data-ttu-id="81b09-202">次のような[指数バックオフを使用した再試行ロジック](/azure/architecture/patterns/retry)は、要求が 1 秒以内に制限を超えてしまうケースで、レート制限を緩和します。</span><span class="sxs-lookup"><span data-stu-id="81b09-202">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="81b09-203">レート制限を避けるために、[HTTP 429 応答](../../bots/how-to/rate-limit.md#handle-http-429-responses)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="81b09-203">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="81b09-204">これらの制限は、大量のメッセージがコネクタからチャネルに送信されることを減らすために設定されており、エンドユーザーのために最適な操作性を確保するためのものです。</span><span class="sxs-lookup"><span data-stu-id="81b09-204">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>

## <a name="see-also"></a><span data-ttu-id="81b09-205">関連項目</span><span class="sxs-lookup"><span data-stu-id="81b09-205">See also</span></span>

[<span data-ttu-id="81b09-206">Office 365コネクタ - Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="81b09-206">Office 365 Connectors — Microsoft Teams</span></span>](/connectors/teams/)
