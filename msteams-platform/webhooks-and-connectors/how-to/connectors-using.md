---
title: メッセージを作成して送信する
author: laujan
description: Microsoft Teams で Office 365 コネクタを使用する方法について説明します。
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams o365 コネクタ
ms.openlocfilehash: 01ce665d9fa165827ab4f03a9f08ff5ac12ee806
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059743"
---
# <a name="create-and-send-messages"></a>メッセージを作成して送信する

アクション可能なメッセージを作成し、受信 Webhook または Office 365 コネクタを介して送信できます。

## <a name="create-actionable-messages"></a>操作可能なメッセージを作成する

アクション可能なメッセージには、カードに表示される 6 つのボタンが含まれています。 各ボタンは、入力の種類、テキスト フィールド、日付ピッカー、または複数選択リストを持つ`ActionCard`アクションを使用して、`potentialAction`メッセージの プロパティで定義されます。 各 `ActionCard` には、 `HttpPOST`などのアクションが関連付けられます。

コネクタ カードは、次のアクションがサポートされています。

- `ActionCard`: 1 つ以上の入力の種類と関連するアクションを表示します。
- `HttpPOST`: POST 要求を URL に送信します。
- `OpenUri`: 別のブラウザーまたはアプリで URI を開き、必要に応じてオペレーティング システムに基づいて異なる URI をターゲットにします。

`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。

- `TextInput`: 1 行または複数行のテキスト フィールド (オプションの長さの制限あり)。
- `DateInput`: オプションの時刻セレクターを持つ日付セレクター。
- `MultichoiceInput`: 1 つまたは複数の選択を提供する選択肢の列挙リスト。

`MultichoiceInput` では、最初にすべて展開した状態でリストを表示するかどうかを制御する `style` プロパティがサポートされています。 `style`の既定値は、次のように`isMultiSelect`の値によって異なります。

| `isMultiSelect` | `style` 既定 |
| --- | --- |
| `false` または指定なし | `compact` |
| `true` | `expanded` |

コンパクト スタイルで複数選択リストを表示するには、 `"isMultiSelect": true` と `"style": true`の両方を指定する必要があります。

コネクタ カードのアクションの詳細については、「 [Actions](/outlook/actionable-messages/card-reference#actions)」を参照してください。

> [!NOTE]
> * Microsoft Teams で `style` プロパティに `compact` を指定することは、Microsoft Outlook で `style` プロパティに `normal` を指定することと同じです。
> * HttpPOST アクションでは、ベアラー トークンは要求に含まれています。 このトークンには、アクションを実行した Office 365 ユーザーの Azure AD ID が含まれています。

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>受信 Webhook または Office 365 コネクタ経由でメッセージを送信する

受信 Webhook または Office 365 コネクタを介してメッセージを送信するには、WEBhook URL に JSON ペイロードを投稿します。 このペイロードは、 [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)の形式である必要があります。

この JSON を使用して、テキスト入力、複数選択、日付と時刻の選択など、豊富な入力を含むカードを作成することもできます。 カードを生成して Webhook URL に投稿するコードは、ホストされている任意のサービスで実行できます。 これらのカードは、アクション可能なメッセージの一部として定義され、Teams ボットとメッセージング拡張機能で使用される [カード](~/task-modules-and-cards/what-are-cards.md)でもサポートされます。

### <a name="example-of-connector-message"></a>コネクタ メッセージの例

コネクタ メッセージの例を次に示します。

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

1. https://curl.haxx.se/を使用して cURL をインストールします。

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
    > POST が成功した場合は、`curl`によって単純な **1** 出力が表示される必要があります。

1. Microsoft Teams クライアントで、投稿された新しいカードを確認します。

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 前提条件: PowerShell のインストールとその基本的な使用方法の理解。

**PowerShell を使用して Webhook にメッセージを投稿するには**

1. PowerShell プロンプトで次のコマンドを入力します。

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > POST が成功した場合は、`Invoke-RestMethod`によって単純な **1** 出力が表示される必要があります。

1. Webhook URL に関連付けられている Microsoft Teams チャネルを確認します。 チャネルに投稿された新しいカードを確認できます。 コネクタを使用してアプリをテストまたは発行する前に、次の操作を行う必要があります。

    - [アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。
    - マニフェストの `icons` 部分を、URL ではなくアイコンのファイル名に変更します。

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>受信 Webhook を使用してアダプティブ カードを送信する

> [!NOTE]
> * `Action.Submit`を除くすべてのネイティブ アダプティブ カード スキーマ要素は、完全にサポートされています。
> * ✔ サポートされているアクションは [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、および [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) です。

**受信 Webhookを介してアダプティブ カードを送信するには**

1. [Teams でカスタム Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) をセットアップします。
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
    * `"contentType"` フィールドは、アダプティブ カードの種類に設定する必要があります。
    * `"content"` オブジェクトは、JSON で書式設定されたカードです。

1. Postman でアダプティブ カードをテストする:

    * [Postman](https://www.postman.com)を使用してアダプティブ カードをテストし、受信 Webhook を設定するために作成された URL に POST 要求を送信します。
    * 要求の本文に JSON ファイルを貼り付け、アダプティブ カード メッセージを [アダプティブ カード] Teams。

> [!TIP]
> アダプティブ カード [コード サンプルとテンプレート](https://adaptivecards.io/samples) を使用して、POST 要求の本文をテストします。

## <a name="rate-limiting-for-connectors"></a>コネクタのレート制限

アプリケーションレート制限は、コネクタまたは受信 Webhook がチャネルで生成することを許可されるトラフィックを制御します。 Teams は、秒単位で測定された固定レート ウィンドウと増分カウンターを使用して要求を追跡します。 1 秒間に 4 つ以上の要求が行われた場合、クライアント接続は、ウィンドウが固定レートの間更新されるまで調整されます。

### <a name="transactions-per-second-thresholds"></a>1 秒あたりのトランザクションのしきい値

次の表に、時間ベースのトランザクションの詳細を示します。

| 時間 (秒)  | 許可される最大要求数  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

[指数バックオフを備えた再試行ロジック](/azure/architecture/patterns/retry)では、要求が 1 秒以内に制限を超えている場合のレート制限を軽減できます。 レート制限に達しないよう、[ベスト プラクティス](../../bots/how-to/rate-limit.md)に従ってください。

> [!NOTE]
> [指数バックオフを備えた再試行ロジック](/azure/architecture/patterns/retry)では、要求が 1 秒以内に制限を超えている場合のレート制限を軽減できます。 レート制限を避けるために、[HTTP 429 応答](../../bots/how-to/rate-limit.md#handle-http-429-responses)を参照してください。

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

これらの制限は、コネクタによるチャネルのスパムを減らし、ユーザーに最適なエクスペリエンスを確保するために実施されます。

## <a name="see-also"></a>関連項目

* [Microsoft Teams 用の Office 365 コネクタ](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [受信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Teams ボットメッセージのレート制限](~/bots/how-to/rate-limit.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Microsoft Teams のカードの書式設定](~/task-modules-and-cards/cards/cards-format.md)
