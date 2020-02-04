---
title: 送信 web フックを使用して Microsoft Teams にカスタムボットを追加する
author: laujan
description: ''
keywords: teams タブ送信 webhook *
ms.topic: conceptual
ms.author: laujan
ms.openlocfilehash: 4570e597484494f05f4e18b4d29746da96c73661
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674814"
---
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a>送信 web フックを使用して Microsoft Teams にカスタムボットを追加する

## <a name="what-are-outgoing-webhooks-in-teams"></a>Teams での送信 web フックとは

Webhooks は、Teams が外部アプリと統合するための便利な方法です。 Webhook は基本的に、コールバック URL に送信される POST 要求です。 Teams では、送信用の webhook により、ユーザーが web サービスにメッセージを送信できるようにするための簡単な方法が提供されます。これにより、 [Microsoft bot フレームワーク](https://dev.botframework.com/)を使用してボットを作成する完全なプロセスを実行する必要がなくなります。 送信 web フックは、JSON ペイロードを受け入れることができる、選択された任意のサービスに Teams からのデータを投稿します。 送信 webhook がチームに追加されると、ボットのように機能し、 ** \@メンション**を使用したメッセージのチャネルをリッスンし、外部 web サービスに通知を送信し、カードや画像を含むことができるリッチメッセージに応答します。

## <a name="outgoing-webhook-key-features"></a>送信 webhook キー機能

| 機能 | 説明 |
| ------- | ----------- |
| スコープ構成| Webhooks はチームレベルでスコープ設定されます。 送信 webhook を追加する各チームのセットアッププロセスを進める必要があります。 |
| リアクティブメッセージング| ユーザーは、メッセージを受信するために webhook に @mention を使用する必要があります。 現在ユーザーは、個人またはプライベートのスコープ内ではなく、パブリックチャネルでの送信 webhook のみをメッセージできます。 |
|標準の HTTP メッセージ交換|応答は元の要求メッセージと同じチェーンに表示され、任意の Bot フレームワークメッセージコンテンツ (リッチテキスト、画像、カード、および絵文字) を含めることができます。 **注**: 送信 web フックはカードを使用することができますが、を`openURL`除くカードアクションを使用することはできません。|
| Teams API メソッドのサポート|Teams では、送信 web フックは HTTP POST を web サービスに送信し、応答を処理します。 チーム内の名簿やチャネルのリストを取得するなど、他の Api にはアクセスできません。|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a>アプリに送信 webhook 処理を追加する

**シナリオ**: Teams チャネルデータベースサーバーで、アプリに変更状態通知をプッシュします。  
**例**: Office 365 テナント全体で TEAMS の HR ユーザーによって従業員のレコードに対して行われたすべての CRUD 操作を追跡する基幹業務アプリがあります。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. JSON ペイロードを使用して POST 要求を受け入れて処理するためのアプリのサーバー上で URL を作成する

サービスは、標準の Azure bot サービスメッセージングスキーマでメッセージを受信します。 Bot フレームワークコネクタは、 [Azure Bot サービス API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)で文書化されているように、サービスが HTTPS プロトコルを使用して JSON 形式のメッセージのインターチェンジを処理できるようにする RESTful サービスです。 または、[Microsoft Bot Framework SDK] をフォローしてメッセージの処理と解析を行うこともできます。 [Azure Bot サービスについ](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)て*も参照してください*。  

送信 web フックは、 `team`レベルに設定され、チームのすべてのメンバーに表示されます。 Bot と同様に、ユーザー ae は、チャネルで呼び出しを行うために、送信 webhook の名前を** \@言及**する必要がありました。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 送信 webhook HMAC トークンを確認するメソッドを作成します。

サービスが実際の Teams クライアントからの呼び出しのみを受信できるようにするために、Teams では`hmac` 、認証プロトコルに常に含める必要がある HMAC コードが HTTP ヘッダーに用意されています。

コードでは、要求に含まれている HMAC 署名を常に検証する必要があります。

* メッセージの要求本文から HMAC トークンを*生成*します。 ほとんどのプラットフォームでこれを行うための標準ライブラリがあります (node.js の[Crypto](https://nodejs.org/api/crypto.html#crypto_crypto)を*参照*してください)。または *「* [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#」を参照してください。 Microsoft Teams では、標準の SHA256 HMAC 暗号化を使用します。 本文を UTF8 でバイト配列に変換する必要があります。
* Teams クライアントで送信 webhook を登録したときに**teams によって提供され**たセキュリティトークンのバイト配列からのハッシュを*計算*します。 下記の「[送信 webhook を作成する](#create-an-outgoing-webhook) *」を参照してください*。
* UTF-8 エンコードを使用して、ハッシュを文字列に*変換*します。
* 生成されたハッシュの文字列値と、HTTP 要求で指定された値を*比較*します。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 成功または失敗応答を送信するメソッドを作成する

送信した webhook からの応答は、元のメッセージと同じ応答チェーンに表示されます。 ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行し、コードには、接続がタイムアウトして終了する前にメッセージに応答するための5秒の時間が与えられます。

### <a name="example-response"></a>応答の例

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>送信 webhook を作成する

1. 適切なチームを選択し、[(&#8226;&#8226;&#8226;)] ドロップダウンメニューから [**チームの管理**] を選択します。
1. ナビゲーションバーから [**アプリ**] タブを選択します。
1. ウィンドウの右下隅から、[**送信 webhook を作成する**] を選択します。
1. 表示されるポップアップウィンドウで、必要なフィールドを入力します。

>* **Name** -webhook のタイトルと @mention タップを指定します。
>* **コールバック URL** -JSON ペイロードを受け入れ、Teams からの POST 要求を受け取る HTTPS エンドポイント。
>* **Description** -プロファイルカードおよびチームレベルのアプリダッシュボードに表示される詳細な文字列。
>* **プロファイル画像**(省略可能) webhook のアプリアイコン。
>* ポップアップウィンドウの右下隅から [**作成**] ボタンを選択すると、送信 webhook が現在のチームのチャネルに追加されます。
>* 次のダイアログウィンドウには、Teams と指定された外部サービスとの間の通話の認証に使用される[ハッシュベースのメッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)セキュリティトークンが表示されます。
>* URL が有効であり、サーバーとクライアントの認証トークンが等しい (つまり HMAC ハンドシェイクである) 場合、送信された webhook はチームのユーザーが使用できるようになります。

## <a name="code-samples"></a>コード サンプル

GitHub で送信 webhook のコードサンプルを表示できます。

### <a name="nodejs"></a>Node.js

[OfficeDev/msteams-サンプル--webhook-nodejs](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a>40u-c\#

[OfficeDev/microsoft-teams-サンプル-webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
