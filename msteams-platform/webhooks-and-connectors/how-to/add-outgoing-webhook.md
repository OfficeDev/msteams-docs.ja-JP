---
title: 送信 Webhook を作成する
author: laujan
description: では、送信 Webhook を作成する方法について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
keywords: Teams タブの送信 Webhook アクション可能メッセージの確認 Webhook
ms.openlocfilehash: 2b77118e76bfde8c0fac7c74fce4dab1d78c7dd5
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356295"
---
# <a name="create-outgoing-webhook"></a>送信 Webhook を作成する

送信 Webhook はボットとして機能し、**@mention** を使用してチャネル内のメッセージを検索します。 外部 Web サービスに通知を送信し、カードや画像などの豊富なメッセージで応答します。 [Microsoft Bot Framework](https://dev.botframework.com/) を使用してボットを作成するプロセスをスキップすることができます。

<!--- TBD: Edit this article.
* Admonitions/alerts may be overused in this article. Check once.
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* Some screenshots like teamschannel.png may be redundant. Check once.
* Some headings use title case. We use sentence case for titles.
* Check for markdownlint errors. 
* Try using &nbsp; to add spaces in codeblocks for indentation and remove the hard tabs.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

## <a name="key-features-of-outgoing-webhook"></a>送信 Webhook の主な機能

次の表には、送信 Webhook の機能と説明があります。

| 機能 | 説明 |
| ------- | ----------- |
| スコープ構成| Webhook はチームのレベルでスコープが設定されます。 それぞれの必須セットアップ プロセスで、送信 Webhook が追加されます。 |
| 反応性のあるメッセージング| ユーザーは、メッセージを受信するために Webhook に @Mention を使用する必要があります。 現在ユーザーが送信 Webhook でメッセージを送信できるのは公開チャネルのみです。個人またはプライベートのスコープ内では行えません。 |
|標準の HTTP メッセージ交換|応答は元の要求メッセージと同じチェーンに表示され、Bot Framework メッセージの内容を含めることができます。 たとえば、リッチ テキスト、画像、カード、絵文字などです。 送信 Webhook はカードを使用することができますが、`openURL` のカード アクションしか使用することができません。|
| Teams API メソッドのサポート|送信 Webhook は HTTP POST を Web サービスに送信し、応答を取得します。 チーム内の参加者一覧やチャネルのリストの取得など、他の API にはアクセスすることはできません。|

## <a name="create-outgoing-webhooks"></a>送信 Webhook を作成する

送信 Webhook を作成し、カスタム ボットを Teams に追加します。

送信 Webhook を作成するには、次の手順を実行します。

1. 左側のウィンドウから **Teams** を選択します。 **Teams** ページが表示されます。

    ![Teams チャネル](~/assets/images/teamschannel.png)

1. **Teams** ページで、送信 Webhook を作成するために必要なチームを選択し、&#8226;&#8226;&#8226; を選択します。ドロップダウン メニューで **[チームの管理]** を選択します。

    ![送信 Webhook を作成する](~/assets/images/outgoingwebhook1.png)

1. チャネル ページの **アプリ** タブを選択します。

    ![送信 Webhook を作成する](~/assets/images/outgoingwebhook2.png)

1. **送信 Webhook を作成する** を選択します。

    ![送信 Webhook を作成する](~/assets/images/outgoingwebhook3.png)

1. **送信 Webhook を作成する** ページに次の詳細を入力します。

    * **名前**: Webhook のタイトルと @メンションのタブです。
    * **コールバック URL**: JSON ペイロードを受け入れ、Teams からの POST 要求を受信する HTTPS エンドポイントです。
    * **説明**: プロフィール カード、チームのレベルのアプリ ダッシュボードに表示される詳細な文字列です。
    * **プロフィール画像**: Webhook のアプリ アイコンで、省力可能です。

1. **[作成]** を選択します。送信 Webhook が、現在のチームのチャネルに追加されます。

    ![送信 Webhook を作成する](~/assets/images/outgoingwebhook.png)

[ハッシュ ベースのメッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) ダイアログ ボックスが表示されます。 これはセキュリティ トークンで、Teams と指定された外部サービス間の呼び出しを認証するために使用されます。 HMAC セキュリティ トークンは有効期限がなく、構成ごとに一意です。

>[!NOTE]
> URL が有効で、サーバーとクライアントの認証トークンが等しい場合、チームのユーザーは送信 Webhook を使用できるようになります。 たとえば、HMAC ハンドシェイクなどです。

次のシナリオは、送信 Webhook を追加するための詳細です。

* シナリオ: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。
* 例: 作成、読み取り、更新、削除など、すべての CRUD 操作を追跡する基幹業務アプリがあります。 これらの操作は Office 365 テナント全体で HR ユーザーによって従業員記録に対して行われました。

# <a name="url-json-payload"></a>[URL JSON ペイロード](#tab/urljsonpayload)

**アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する**

サービスは、標準の Azure Bot Service のメッセージング スキーマでメッセージを受信します。 Bot Framework Connector は、[Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) で文書化されているように、サービスが HTTPS プロトコルを使用して JSON 形式のメッセージ交換を処理できるようにする RESTful サービスです。 Microsoft Bot Framework SDK を使用して、メッセージの処理と解析を行うこともできます。 詳細については、[Azure Bot Service の概要](/azure/bot-service/bot-service-overview-introduction) を参照してください。

送信 Webhook は、`team` レベルにスコープが設定され、チームのすべてのメンバーに表示されます。 ユーザーは送信 Webhook の名前を **\@メンション** して、チャネルで呼び出す必要があります。

# <a name="verify-hmac-token"></a>[HMAC トークンを確認する](#tab/verifyhmactoken)

**送信 Webhook HMAC トークンを確認するメソッドを作成する**

受信メッセージと ID の例: {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" } という SigningKeyDictionary の "contoso"。 

要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。

サービスが受け取る呼び出しが本物の Teams クライアントからの呼び出しのみになるよう、Teams により HTTP `hmac` ヘッダーに HMAC コードが提供されます。このコードは常に認証プロトコルに含める必要があります。

次のように、コードで要求に含まれる HMAC 署名を常に検証する必要があります。

* メッセージの要求本文から HMAC トークンを生成します。 ほとんどのプラットフォームでこれを行うための標準ライブラリがあり、Node.js の場合は [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto)、C\# の場合は [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) などがあります。 Microsoft Teams では、標準の SHA256 HMAC 暗号化を使用します。 本文を UTF8 でバイト配列に変換する必要があります。
* Teams クライアントで送信 Webhook を登録したときに Teams によって提供されたセキュリティ トークンのバイト配列からハッシュを計算します。「[送信 Webhook を作成する](#create-outgoing-webhook)」を参照してください。
* UTF-8 エンコーディングを使用してハッシュを文字列に変換します。
* 生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。

# <a name="method-to-respond"></a>[応答するメソッド](#tab/methodtorespond)

**成功または失敗の応答を送信するメソッドを作成する**

送信 Webhook からの応答は、元のメッセージと同じ返信チェーンに表示されます。ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行し、コードには、メッセージに応答するための 5 秒間が与えられます。この時間を過ぎると、接続がタイムアウトして終了します。

### <a name="example-response"></a>応答の例

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

---

> [!NOTE]
> * アダプティブ カード、ヒーロー カード、テキスト メッセージは、送信 Webhook で添付ファイルとして送信できます。
> * カードでは、書式設定がサポートされています。詳細については、「[マークダウンを使用したカードの書式設定](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)」を参照してください。

以下のコードは、アダプティブ カードの応答例です。

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

---

## <a name="code-sample"></a>コード サンプル

|**サンプルの名前** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhookの送信 | Microsoft Teams で使用するカスタム ボットを作成するサンプルです。| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|


## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

「[ステップ バイ ステップ ガイド](../../sbs-outgoing-webhooks.yml)」に従って、Teams で送信 Webhook を作成します。

## <a name="see-also"></a>関連項目

* [受信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
