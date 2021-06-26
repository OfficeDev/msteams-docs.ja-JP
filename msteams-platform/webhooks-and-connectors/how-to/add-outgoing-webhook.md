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
# <a name="create-outgoing-webhook"></a>送信 Webhook の作成

送信 Webhook はボットとして機能し、ボットを使用してチャネル内の **メッセージ@mention。** 外部 Web サービスに通知を送信し、カードや画像を含むリッチ メッセージで応答します。 これは、ボットを作成するプロセスをスキップするのに役立[Microsoft Bot Framework。](https://dev.botframework.com/)

## <a name="key-features-of-outgoing-webhook"></a>送信 Webhook の主な機能

次の表に、送信 Webhook の機能と説明を示します。

| 機能 | 説明 |
| ------- | ----------- |
| スコープ構成| Webhook はチームのレベルでスコープが設定されます。 それぞれの必須のセットアップ プロセスでは、送信 Webhook が追加されます。 |
| 反応性メッセージング| ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。 現在、ユーザーはパブリック チャネルでのみ送信 Webhook にメッセージを送信できます。個人またはプライベート スコープ内ではメッセージを送信できます。 |
|標準の HTTP メッセージ交換|応答は元の要求メッセージと同じチェーンに表示され、リッチ テキスト、画像、カード、絵文字など、任意の Bot Framework メッセージ コンテンツを含めできます。 送信 Webhooks はカードを使用することができますが、 を除き、カードアクションを使用することはできません `openURL` 。|
| Teams API メソッドのサポート|送信 Webhooks は HTTP POST を Web サービスに送信し、応答を取得します。 チーム内のチャネルの名簿やリストの取得など、他の API にはアクセスできません。|

## <a name="create-outgoing-webhooks"></a>送信 Webhooks の作成

送信 Webhook を作成し、カスタム ボットをユーザー設定にTeams。

**送信 Webhook を作成するには**

1. 左側 **のTeams** ウィンドウから [新しいウィンドウ] を選択します。 **[Teams]** ページが表示されます。

    ![Teams チャネル](~/assets/images/teamschannel.png)

1. [送信 **Teams]** ページで、送信 Webhook を作成するために必要なチームを選択し、送信 Webhook を &#8226;&#8226;&#8226;。 ドロップダウン メニューで、[チームの管理] **を選択します**。

    ![送信 Webhook の作成](~/assets/images/outgoingwebhook1.png)

1. チャネル ページ **の [アプリ** ] タブを選択します。

    ![送信 Webhook の作成](~/assets/images/outgoingwebhook2.png)

1. [ **送信 Webhook の作成] を選択します**。

    ![送信 Webhooks の作成](~/assets/images/outgoingwebhook3.png)

1. [送信 Webhook の作成] **ページに次の詳細を入力** します。

    * **名前**: [Webhook] タイトルと [@mention] タブ。
    * **コールバック URL**: JSON ペイロードを受け入れ、JSON ペイロードから POST 要求を受信する HTTPS エンドポイントTeams。
    * **説明**: プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列。
    * **プロファイル画像**: Webhook のアプリ アイコン (省略可能)。

1. **[作成]** を選択します。 送信 Webhook は、現在のチームのチャネルに追加されます。

    ![送信 Webhook の作成](~/assets/images/outgoingwebhook.png)

ハッシュ [ベースのメッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) ダイアログ ボックスが表示されます。 これは、指定された外部サービスとの間の呼び出しTeams認証するために使用されるセキュリティ トークンです。

>[!NOTE]
> 送信 Webhook は、URL が有効で、サーバーとクライアントの認証トークンが等しい場合にのみ、チームのユーザーが使用できます。 たとえば、HMAC ハンドシェイクです。

次のシナリオでは、送信 Webhook を追加する詳細を示します。

* シナリオ: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。
* 例: 作成、読み取り、更新、削除など、すべての CRUD 操作を追跡する一行のビジネス アプリがあります。 これらの操作は、従業員レコードに対して、Teamsテナント全体の人事ユーザー Office 365されます。

# <a name="url-json-payload"></a>[URL JSON ペイロード](#tab/urljsonpayload)
**JSON ペイロードを使用して POST 要求を受け入れて処理する URL をアプリのサーバーに作成する**

サービスは、標準の Azure ボット サービス メッセージング スキーマでメッセージを受信します。 ボット フレームワーク コネクタは RESTful サービスで [、Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理できます。 または、SDK の手順に従ってMicrosoft Bot Frameworkメッセージを処理して解析することもできます。 詳細については [、「Azure Bot Service の概要」を参照してください](/azure/bot-service/bot-service-overview-introduction)。

送信 Webhook はレベルの範囲に設定 `team` され、すべてのチーム メンバーに表示されます。 ユーザーは、**\@ チャネルで** 呼び出す送信 Webhook の名前を指定する必要があります。

# <a name="verify-hmac-token"></a>[HMAC トークンを確認する](#tab/verifyhmactoken)
**送信 Webhook HMAC トークンを確認するメソッドを作成する**

受信メッセージと ID の使用例: {"contoso"の SigningKeyDictionary の "contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。

要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。

サービスが実際のクライアントからのみ呼び出しを受信Teams、Teams HTTP 承認ヘッダーに HMAC コードを `hmac` 提供します。 認証プロトコルにコードを常に含める。

コードでは、要求に含まれる HMAC 署名を次のように常に検証する必要があります。

* メッセージの要求本文から HMAC トークンを生成します。 ほとんどのプラットフォームでこれを行う標準的なライブラリがあります(たとえば、Node.js[](https://nodejs.org/api/crypto.html#crypto_crypto)の Crypto Teams [Webhook サンプル](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \# )。 Microsoft Teams SHA256 HMAC 暗号化を使用します。 UTF8 で本文をバイト配列に変換する必要があります。
* 送信 Webhook をクライアントに登録した場合、Teams によって提供されるセキュリティ トークンのバイト配列からハッシュTeamsします。 「 [送信 Webhook の作成」を参照してください](#create-outgoing-webhook)。
* UTF-8 エンコーディングを使用してハッシュを文字列に変換します。
* 生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。

# <a name="method-to-respond"></a>[応答するメソッド](#tab/methodtorespond)
**成功または失敗の応答を送信するメソッドを作成する**

送信 Webhooks からの応答は、元のメッセージと同じ返信チェーンに表示されます。 ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行し、接続が切れ、終了する前にコードがメッセージに応答するために 5 秒を取得します。

### <a name="example-response"></a>応答の例

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * 送信 Webhook を使用して、アダプティブ カード、ヒーロー カード、およびテキスト メッセージを添付ファイルとして送信できます。
> * カードは書式設定をサポートします。 詳細については [、「markdown を使用した書式カード」を参照してください](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)。

アダプティブ カード応答の例を次に示します。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

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

## <a name="code-sample"></a>コード サンプル

|**サンプル名** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 送信 Webhooks | カスタム ボットを作成するサンプルを使用して、Microsoft Teams。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a>関連項目
* [受信 Webhook の作成](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
