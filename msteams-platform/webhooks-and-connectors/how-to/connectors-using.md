---
title: メッセージを作成して送信する
author: laujan
description: Microsoft Teams で Office 365 コネクタを使用する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
keywords: Teams o365 コネクタ
ms.openlocfilehash: 6d10a173079fb31db303e98bfaf0800ff048a187
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156996"
---
# <a name="create-and-send-messages"></a>メッセージを作成して送信する

アクション可能なメッセージを作成し、受信 Webhook または受信コネクタを介してOffice 365できます。

## <a name="create-actionable-messages"></a>アクション可能なメッセージを作成する

アクション可能なメッセージには、カードに表示される 3 つのボタンが含まれます。 各ボタンは、入力型、テキスト フィールド、日付選択リスト、または複数選択肢リストを持つアクションを使用して、メッセージのプロパティ `potentialAction` `ActionCard` で定義されます。 各 `ActionCard` アクションには、たとえば、関連付けられたアクションがあります `HttpPOST` 。

コネクタ カードは、次の操作をサポートします。

- `ActionCard`: 1 つ以上の入力型と関連付けられたアクションを表示します。
- `HttpPOST`: POST 要求を URL に送信します。
- `OpenUri`: 別のブラウザーまたはアプリで URI を開き、必要に応じてオペレーティング システムに基づいて異なる URI を対象とします。

`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。

- `TextInput`: 1 行または複数行のテキスト フィールドで、オプションの長さ制限があります。
- `DateInput`: オプションのタイム セレクターを含む日付セレクター。
- `MultichoiceInput`: 1 つの選択または複数の選択を提供する選択肢の列挙リストです。

`MultichoiceInput` では、最初にすべて展開した状態でリストを表示するかどうかを制御する `style` プロパティがサポートされています。 既定値は、 `style` 次の値によって `isMultiSelect` 異なります。

| `isMultiSelect` | `style` 既定 |
| --- | --- |
| `false` または指定なし | `compact` |
| `true` | `expanded` |

コンパクト なスタイルで複数選択リストを表示するには、 と の両方を指定する `"isMultiSelect": true` 必要があります `"style": true` 。

コネクタ カードのアクションの詳細については、「Actions」を [参照してください](/outlook/actionable-messages/card-reference#actions)。

> [!NOTE]
> * Microsoft Teams で `style` プロパティに `compact` を指定することは、Microsoft Outlook で `style` プロパティに `normal` を指定することと同じです。
> * HttpPOST アクションでは、ベアラー トークンは要求に含まれています。 このトークンには、アクションを実行した Office 365 ユーザーの Azure AD ID が含まれています。

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>受信 Webhook または受信コネクタを介してOffice 365する

受信 Webhook または受信コネクタを介してメッセージをOffice 365するには、JSON ペイロードを Webhook URL に投稿します。 このペイロードは、コネクタ カードの形式Office 365[必要があります](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。

また、この JSON を使用して、テキスト入力、複数選択、日付と時刻の選択などのリッチ入力を含むカードを作成できます。 カードを生成し、Webhook URL に投稿するコードは、ホストされている任意のサービスで実行できます。 これらのカードは、アクション可能なメッセージの一部として定義され、カード[](~/task-modules-and-cards/what-are-cards.md)でサポートされ、Teams拡張機能で使用されます。

### <a name="example-of-connector-message"></a>コネクタ メッセージの例

コネクタ メッセージの例は次のとおりです。

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

このメッセージは、チャネルに次のカードを提供します。

![コネクタ カードのスクリーンショット](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a>cURL と PowerShell を使用してメッセージを送信する

# <a name="curl"></a>[cURL](#tab/cURL)

**cURL を使用して Webhook にメッセージを投稿するには**

1. を使用して cURL をインストールします https://curl.haxx.se/ 。

1. コマンド ラインから、次の cURL コマンドを入力します。

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > POST が成功した場合は、単純な **1** 出力を表示する必要があります `curl` 。

1. 新しいMicrosoft Teamsのクライアントを確認します。

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 前提条件: PowerShell のインストールとその基本的な使用方法に関する知識。

**PowerShell を使用して Webhook にメッセージを投稿するには**

1. PowerShell プロンプトで次のコマンドを入力します。

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > POST が成功した場合は、単純な **1** 出力を表示する必要があります `Invoke-RestMethod` 。

1. Webhook URL に関連付けられている Microsoft Teams チャネルを確認します。 チャネルに投稿された新しいカードを確認できます。 コネクタを使用してアプリをテストまたは発行する前に、次の操作を行う必要があります。

    - [アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。
    - マニフェストの `icons` 部分を URL ではなくアイコンのファイル名に変更します。

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>受信 Webhook を使用してアダプティブ カードを送信する

> [!NOTE]
> * ネイティブのアダプティブ カード スキーマ要素 (ただし `Action.Submit` 、 を除く) はすべて完全にサポートされています。
> * サポートされているアクションは [**、Action.OpenURL、Action.ShowCard、**](https://adaptivecards.io/explorer/Action.OpenUrl.html)[**および Action.ToggleVisibility です**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。 [](https://adaptivecards.io/explorer/Action.ShowCard.html)

**受信 Webhook を介してアダプティブ カードを送信するには**

1. [カスタム Webhook をカスタム webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) Teams。
1. 次のコードを使用してアダプティブ カード JSON ファイルを作成します。

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

    アダプティブ カード JSON ファイルのプロパティは次のとおりです。

    * `"type"` フィールドは `"message"` であることが必要です。
    * `"attachments"` 配列には、カード オブジェクトのセットが含まれています。
    * フィールド `"contentType"` はアダプティブ カードの種類に設定する必要があります。
    * `"content"` オブジェクトは、JSON で書式設定されたカードです。

1. Postman でアダプティブ カードをテストする:

    * Postman を使用して [アダプティブ カードをテスト](https://www.postman.com) し、受信 Webhook をセットアップするために作成された POST 要求を URL に送信します。
    * 要求の本文に JSON ファイルを貼り付け、アダプティブ カード メッセージを [アダプティブ カード] Teams。

> [!TIP]
> アダプティブ カード のコード [サンプルとテンプレートを使用して](https://adaptivecards.io/samples) POST 要求の本文をテストします。

## <a name="rate-limiting-for-connectors"></a>コネクタのレート制限

アプリケーション レートの制限は、コネクタまたは受信 Webhook がチャネルで生成できるトラフィックを制御します。 Teamsレート ウィンドウと増分カウンターを使用して、数秒で測定された要求を追跡します。 1 秒間に 4 つ以上の要求が行われた場合、固定レートの期間ウィンドウが更新されるまで、クライアント接続が調整されます。

### <a name="transactions-per-second-thresholds"></a>1 秒あたりのトランザクションのしきい値

次の表に、時間ベースのトランザクションの詳細を示します。

| 時間 (秒)  | 許可される最大要求数  |
|---|---|
| 1   | 4   |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

指数 [バックオフによる再試行ロジック](/azure/architecture/patterns/retry) は、要求が 1 秒以内に制限を超える場合のレート制限を軽減できます。 ベスト [プラクティスに従](../../bots/how-to/rate-limit.md) って、レート制限に達しないようにします。

> [!NOTE]
> 指数 [バックオフによる再試行ロジック](/azure/architecture/patterns/retry) は、要求が 1 秒以内に制限を超える場合のレート制限を軽減できます。 レート制限を避けるために、[HTTP 429 応答](../../bots/how-to/rate-limit.md#handle-http-429-responses)を参照してください。

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

これらの制限は、コネクタによるチャネルの spamming を減らすために設定され、ユーザーに最適なエクスペリエンスを保証します。

## <a name="see-also"></a>関連項目

* [Office 365コネクタのMicrosoft Teams](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [受信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
