---
title: コネクタと Webhook にメッセージを送信する
description: Microsoft Teams で Office 365 コネクタを使用する方法について説明します。
localization_priority: Priority
keywords: Teams o365 コネクタ
ms.openlocfilehash: 55cfbc870ed8b04a8fbac58fdfa9b40110410ad7
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875015"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a>コネクタと Webhook にメッセージを送信する

Office 365 コネクタまたは着信 Webhook 経由でメッセージを送信するには、Webhook URL に JSON ペイロードを投稿します。 通常、このペイロードは [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)の形式になります。

この JSON を使用して、テキスト入力、複数選択、または日付と時刻の選択など、リッチな入力を含むカードを作成することもできます。 カードを生成して Webhook URL への投稿を行うコードは、いずれのホステッド サービスでも実行できます。 これらのカードは、操作可能なメッセージの一部として定義されています。また、Teams ボットやメッセージング拡張機能で使用される[カード](~/task-modules-and-cards/what-are-cards.md)でもサポートされます。

### <a name="example-connector-message"></a>コネクタ メッセージの例

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

このメッセージにより、チャネルに次のカードが生成されます。

![コネクタ カードのスクリーンショット](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a>操作可能なメッセージの作成

前のセクションの例では、3 つのボタンがカードに表示されています。 各ボタンは、`ActionCard` アクションを使用して `potentialAction` プロパティに定義されています。それぞれには、入力の種類 (テキスト フィールド、日付の選択、または複数選択リスト) が含まれています。 それぞれの `ActionCard` アクションには、`HttpPOST` など、関連付けられたアクションがあります。

コネクタ カードでは、3 種類のアクションがサポートされています。

- `ActionCard` 1 つまたは複数の入力の種類と、関連付けられたアクションを示します
- `HttpPOST` POST 要求を URL に送信します
- `OpenUri` URI を別のブラウザーまたはアプリで開きます。必要に応じて、オペレーティング システムに基づいて異なる URI をターゲットにします。

`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。

- `TextInput` 単一行または複数行の、オプションとして長さ制限が付いたテキスト フィールド
- `DateInput` オプションとして時間選択が付いた、日付選択
- `MultichoiceInput` 1つまたは複数の選択を行える、選択肢を列挙したリスト

`MultichoiceInput` では、最初にすべて展開した状態でリストを表示するかどうかを制御する `style` プロパティがサポートされています。 `style` の既定値は、`isMultiSelect`の値によって決まります。

| `isMultiSelect` | `style` 既定 |
| --- | --- |
| `false` または指定なし | `compact` |
| `true` | `expanded` |

複数選択リストを最初はコンパクトなスタイルで表示させる場合は、`"isMultiSelect": true` と `"style": true` の両方を指定する必要があります。

> [!NOTE]
> Microsoft Teams で `style` プロパティに `compact` を指定することは、Microsoft Outlook で `style` プロパティに `normal` を指定することと同じです。

コネクタ カードのアクションのその他の詳細については、操作可能なメッセージ カードのレファレンスの、「**[アクション](/outlook/actionable-messages/card-reference#actions)**」を参照してください。

## <a name="setting-up-a-custom-incoming-webhook"></a>カスタム着信 Webhook の設定

単純なカードをコネクタに送信する方法を見るには、次の手順に従って操作を行ってください。

1. Microsoft Teams で、チャネル名の横にある [**その他のオプション**] (**&#8943;**) を選択し、[**コネクタ**] を選択します。
2. コネクタのリストをスクロールして [**着信 Webhook**] を選択し、次に [**追加**] を選択します。
3. Webhook の名前を入力し、Webhook からのデータと関連づける画像を更新し、[**作成**] を選択します。
4. Webhook をクリップボードにコピーして保存します。 Microsoft Teams に情報を送信するには、Webhook URL が必要です。
5. [**完了**] を選択します。

### <a name="post-a-message-to-the-webhook-using-curl"></a>cURL を使用してメッセージを Webhook に投稿する

次の手順では、[cURL](https://curl.haxx.se/) を使用します。 これが既にインストールされており、基本的な使用方法に精通しているものみなします。

1. コマンド ラインから、次の cURL コマンドを入力します。

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

2. POST が成功すると、単に "**1**" という `curl` の出力が表示されます。
3. Microsoft Team クライアントを確認します。 チームに新しいカードが投稿されるはずです。

### <a name="post-a-message-to-the-webhook-using-powershell"></a>PowerShell を使用して Webhook にメッセージを投稿します。

次の手順では、PowerShell を使用します。 これが既にインストールされており、基本的な使用方法に精通しているものみなします。

1. PowerShell プロンプトで次のコマンドを入力します。

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. POST が成功すると、単に "**1**" という `Invoke-RestMethod` の出力が表示されます。
3. Webhook URL に関連付けられている Microsoft Teams チャネルを確認します。 チャネルに新しいカードが投稿されているはずです。

- [アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。
- マニフェストの `icons` の部分を変更し、アイコンの URL ではなくアイコンのファイル名を参照するようにします。

次の manifest.json ファイルには、アプリをテストして送信するために必要な基本的な要素が含まれています。

> [!NOTE]
> 次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。

#### <a name="example-manifestjson-with-connector"></a>コネクタを使用した manifest.json の例

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

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>受信 Webhook を使用してアダプティブ カードを送信する

> [!NOTE]
>
> ✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。
>
> ✔ サポートされているアクションは [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、および [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) です。

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a>受信 Webhook を通して [アダプティブ カード](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) を送信するためのフローは次のとおりです。

**1.** [カスタム webhook](#setting-up-a-custom-incoming-webhook) を Teams に設定します。</br></br>
**2.** アダプティブ カード JSON ファイルを作成します。

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
> - `"type"` フィールドは `"message"` であることが必要です。
> - `"attachments"` 配列には、カード オブジェクトのセットが含まれています。
> - `"contentType"` フィールドにはアダプティブカードの種類が設定されていることが必要です。
> - `"content"` オブジェクトは、JSON で書式設定されたカードです。

**3.** Postman でアダプティブ カードをテストする

[Postman](https://www.postman.com) を使用して、受信 Webhook の設定時に作成した URL に POST 要求を送信することで、アダプティブカードをテストできます。 JSON ファイルを要求の本文に貼り付け、Teams でアダプティブ カード メッセージを表示します。

>[!TIP]
> テストの Post 要求の本文には、アダプティブ カード コードの [サンプルとテンプレート](https://adaptivecards.io/samples) を使用できます。

## <a name="testing-your-connector"></a>コネクタをテストする

コネクタをテストするには、他のアプリと同じ方法でコネクタをチームにアップロードします。 (前のセクションの指示に従って変更された) コネクタ開発者ダッシュボードからのマニフェスト ファイルと 2 つのアイコン ファイルを使用して .zip パッケージを作成できます。

アプリをアップロードしたら、任意のチャネルからコネクタ リストを開きます。 一番下までスクロールして、アプリが [**アップロード済み**] セクションに表示されていることを確認します。

![コネクタ ダイアログ ボックスの [アップロード済み] セクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

構成機能を起動できるようになりました。 このフローは、ポップアップ ウィンドウを通してすべて Microsoft Teams 内で行われる点に注意してください。 現在、この動作は、ここで作成したコネクタの構成機能とは異なります。Microsoft では、構成機能の共通化に取り組んでいます。

`HttpPOST` アクションが正常に動作していることを確認するには、[カスタム着信 Webhook](#setting-up-a-custom-incoming-webhook) を使用します。

## <a name="rate-limiting-for-connectors"></a>コネクタのレート制限

アプリケーション レートの制限は、コネクタまたは着信 Webhook がチャネルで発生させることが許可されているトラフィックを制御します。 Teams は、固定レート ウィンドウと増分カウンター (秒単位で測定) を使用して、要求を追跡します。  要求が多すぎる場合は、ウィンドウが更新されるまで (つまり固定レートの期間中)、クライアント接続が制限されます。

### <a name="transactions-per-second-thresholds"></a>**1 秒あたりのトランザクションのしきい値**

| 時間 (秒)  | 許可される最大要求数  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

「[Office 365 コネクタ — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)」*も参照*

次のような[指数バックオフを使用した再試行ロジック](/azure/architecture/patterns/retry)は、要求が 1 秒以内に制限を超えてしまうケースで、レート制限を緩和します。 レート制限に達しないよう、「[ベスト プラクティス](../../bots/how-to/rate-limit.md#best-practices)」に従ってください。

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
 
これらの制限は、大量のメッセージがコネクタからチャネルに送信されることを減らすために設定されており、エンドユーザーのために最適な操作性を確保するためのものです。
