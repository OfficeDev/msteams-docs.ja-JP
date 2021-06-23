---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
description: 送信 Webhook を追加する方法について説明します。
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams タブ送信 webhook アクション可能メッセージ verify webhook
ms.openlocfilehash: 2fac6f42e27a4c8cb3d079ea281d458a4dfe41ed
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069177"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>送信 webhooks を使用してTeamsボットを追加する

## <a name="outgoing-webhooks-in-teams"></a>送信 webhooks in Teams

Webhooks は、外部アプリと統合するTeams優れた方法です。 基本的に Webhook は、コールバック URL に送信される POST 要求です。 送信 Webhooks を使用すると、ユーザーは web サービスを介してボットを作成する完全なプロセスを実行せずに、web サービスに[メッセージを送信Microsoft Bot Framework。](https://dev.botframework.com/)

送信 Webhook は、JSON ペイロードを受けTeamsできる選択したサービスにデータを送信します。 送信 Webhook をチームに追加した後、ボットとして機能し、メンションを使用してチャネル内のメッセージを検索 **\@ します**。 外部 Web サービスに通知を送信し、カードや画像を含むリッチ メッセージで応答します。

## <a name="outgoing-webhook-key-features"></a>送信 Webhook の主な機能

| 機能 | 説明 |
| ------- | ----------- |
| スコープ構成| Webhook はチームのレベルでスコープが設定されます。 送信 Webhook を追加するチームごとにセットアップ プロセスを実行する必要があります。 |
| 反応性メッセージング| ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。 現在、ユーザーはパブリック チャネルでのみ送信 Webhook にメッセージを送信できます。個人またはプライベート スコープ内ではメッセージを送信できます。 |
|標準の HTTP メッセージ交換|応答は元の要求メッセージと同じチェーンに表示され、リッチ テキスト、画像、カード、絵文字など、任意のボット フレームワーク メッセージ コンテンツを含めできます。 送信 Webhooks はカードを使用することができますが、 を除き、カードアクションを使用することはできません `openURL` 。|
| Teams API メソッドのサポート|送信 Webhook は HTTP POST を Web サービスに送信し、応答を処理します。 チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。|

## <a name="creating-actionable-messages"></a>操作可能なメッセージの作成

コネクタ カードには、カードに 3 つの表示ボタンが含まれます。 各ボタンは、アクション `potentialAction` を使用してメッセージのプロパティで定義 `ActionCard` されます。 それぞれに、入力タイプ、テキスト フィールド、日付ピッカー、または複数選択肢 `ActionCard` リストが含まれる。 各 `ActionCard` アクションには、たとえば、関連付けられたアクションがあります `HttpPOST` 。

コネクタ カードでは、3 種類のアクションがサポートされています。

| アクション | 説明 |
| ------- | ----------- |
| `ActionCard` |1 つ以上の入力型と関連付けられたアクションを表示します。|
| `HttpPOST` | POST 要求を URL に送信します。 |
| `OpenUri` |  別のブラウザーまたはアプリで URI を開き、必要に応じてオペレーティング システムに基づいてさまざまな URI を対象とします。|

`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。

| 入力の種類 | 説明 |
| ------- | ----------- |
| `TextInput` | オプションの長さ制限を持つ単一行または複数行のテキスト フィールド。 |
| `DateInput` | オプションのタイム セレクターを含む日付セレクター。 |
| `MultichoiceInput` | 1 つの選択範囲または複数の選択項目を提供する、指定された選択肢の一覧。|

`MultichoiceInput` 完全に `style` 展開されたリストの表示を制御するプロパティをサポートします。 既定値は、 `style` 値によって異 `isMultiSelect` なります。

| `isMultiSelect` value  | `style` 既定値  |
| --- | --- |
| `false` または指定なし | 既定のスタイルは次の値です。 `compact`|
| `true` | 既定のスタイルは次の値です。 `expanded` |

> [!NOTE]
> * 複数選択リストをコンパクト なスタイルで表示する場合は、両方 `"isMultiSelect": true` `"style": true` を入力します。
> * [プロパティ `compact` の選択] `style` Teamsは、Microsoft のプロパティを選択する場合と同 `normal` `style` Outlook。
> * Webhooks は、Office 365カードとアダプティブ カードのみをサポートします。

コネクタ カードのアクションに関するその他の詳細については、「 **[アクション可能](/outlook/actionable-messages/card-reference#actions)** なメッセージ カードリファレンスのアクション」を参照してください。

## <a name="adding-outgoing-webhooks-to-your-app"></a>送信 Webhook をアプリに追加する

**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。  
**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する

サービスは、標準の Azure ボット サービス メッセージング スキーマでメッセージを受信します。 ボット フレームワーク コネクタは RESTful サービスで [、Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理できます。 [Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。 「Azure [Bot Service について」も参照してください](/azure/bot-service/bot-service-overview-introduction)。


送信 Webhook はレベルにスコープが設定され `team` 、すべてのチーム メンバーに表示されます。 ボットと同様に、ユーザーは送信 **\@** Webhook の名前を指定してチャネルで呼び出す必要があります。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 送信 Webhook HMAC トークンを確認するメソッドを作成する

#### <a name="hmac-signature-for-testing-with-code-example"></a>コード例を使ったテスト用の HMAC 署名

受信メッセージと id の使用例: {"contoso"の SigningKeyDictionary の "contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。

要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。

サービスが実際のクライアントからのみ呼び出しを受信Teams、http ヘッダー Teams HMAC コードを提供 `hmac` します。 常に認証プロトコルにコードを含める。

コードでは、要求に含まれる HMAC 署名を常に検証する必要があります。

* メッセージの要求本文から HMAC トークンを生成します。 ほとんどのプラットフォームでこれを行う標準的なライブラリがあります (「Crypto [for](https://nodejs.org/api/crypto.html#crypto_crypto) Node.js [Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) sample for C」を参照Teams参照 \# )。 Microsoft Teams SHA256 HMAC 暗号化を使用します。 UTF8 で本文をバイト配列に変換する必要があります。
* Teams クライアントで送信 Webhook を登録したときに Teams によって提供されたセキュリティ トークンのバイト配列からハッシュを **計算** します。 「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を参照してください。
* UTF-8 エンコーディングを使用してハッシュを文字列に変換します。
* 生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 成功または失敗の応答を送信するメソッドを作成する

送信 Webhook からの応答は、元のメッセージと同じ返信チェーンに表示されます。 ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行し、接続が切れ、終了する前にコードがメッセージに応答するために 5 秒を取得します。

### <a name="example-response"></a>応答の例

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

> [!NOTE]
> * 送信 Webhook を使用して、アダプティブ カード、ヒーロー カード、およびテキスト メッセージを添付ファイルとして送信できます。
> * カードは書式設定をサポートします。 詳細については [、「markdown を使用した書式カード」を参照してください](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#formatting-cards-with-markdown)。

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

## <a name="create-an-outgoing-webhook"></a>送信 Webhook を作成する

1. 適切なチームを選択し **、[チーム** の管理] ([&#8226;&#8226;&#8226;] ドロップダウン メニューから [チームの管理] を選択します。
1. ナビゲーション バーから **[アプリ]** タブを選択します。
1. ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。
1. 表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。

>* **名前**: Webhook のタイトルと@mentionタップ
>* **コールバック URL**: JSON ペイロードを受け入れ、JSON ペイロードから POST 要求を受信する HTTPS エンドポイントTeams
>* **説明**: プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列
>* **プロファイル画像**: Webhook 用のオプションのアプリ アイコン
>* ポップアップ ウィンドウ **の右下** 隅から [作成] ボタンを選択すると、送信 Webhook が現在のチームのチャネルに追加されます。
>* 次のダイアログ ウィンドウには、ハッシュ ベースのメッセージ認証コード[(HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)セキュリティ トークンが表示され、Teams と指定された外部サービス間の呼び出しを認証するために使用されます。
>* 送信 Webhook は、URL が有効で、サーバー認証トークンとクライアント認証トークン (HMAC ハンドシェイクなど) が等しい場合にのみ、チームのユーザーが使用できます。

## <a name="code-sample"></a>コード サンプル
|**サンプル名** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 送信 Webhook | カスタム ボット **を作成するサンプルを** 使用して、Microsoft Teams。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

