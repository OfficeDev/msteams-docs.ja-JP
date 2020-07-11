---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
author: laujan
description: ''
keywords: Teams、タブ、送信 Webhook*
ms.topic: conceptual
ms.author: laujan
ms.openlocfilehash: 4881dc8768c7c51947f6a80a55affe78c28874d3
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2020
ms.locfileid: "45102999"
---
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a>送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する

## <a name="what-are-outgoing-webhooks-in-teams"></a>Teams での送信 Webhook とは

Webhook は、Teams と外部アプリを統合させるための便利な手段です。 基本的に Webhook は、コールバック URL に送信される POST 要求です。 Teams で送信 Webhook を使用すれば、ユーザーは Web サービスにメッセージを簡単に送信することができます。[Microsoft Bot Framework](https://dev.botframework.com/) でのボット作成のプロセス全体を踏む必要もありません。 送信 Webhook は Teams からのデータを、JSON ペイロードを受け入れることができる、選択された任意のサービスに投稿します。 送信 Webhook がチームに追加されると、ボットのように動作します。**\@メンション**を使用してメッセージのチャネルをリッスンしたり、外部の Web サービスに通知を送信したりします。カードや画像を含む豊富なメッセージでの応答も行います。

## <a name="outgoing-webhook-key-features"></a>送信 Webhook の主な機能

| 機能 | 説明 |
| ------- | ----------- |
| スコープ構成| Webhook はチームのレベルでスコープが設定されます。 送信 Webhook を追加するチームそれぞれのセットアップ処理を進める必要があります。 |
| 反応性のあるメッセージング| ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。 現在ユーザーが送信 Webhook でメッセージを送信できるのは公開チャネルのみです。個人またはプライベートのスコープ内では行えません |
|標準の HTTP メッセージ交換|応答は元の要求メッセージと同じチェーンに表示され、Bot Framework のメッセージのコンテンツ (リッチ テキスト、画像、カード、絵文字) を含めることができます。 **注**: 送信 Webhook はカードを使用することができますが、`openURL` のカード アクションしか使用することができません。|
| Teams API メソッドのサポート|Teams では、送信 Webhook は HTTP POST を Web サービスに送信し、応答を処理します。 チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a>アプリに送信 Webhook の処理を追加する

**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。  
**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する

サービスは、標準の Azure Bot Service のメッセージング スキーマでメッセージを受信します。 Bot Framework Connector は、[Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) で文書化されているように、サービスが HTTPS プロトコルを使用して JSON 形式のメッセージ交換を処理できるようにする RESTful サービスです。 [Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。 詳細については、「[Azure Bot Service について](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)」も*参照してください*。

送信 Webhook は、`team` レベルにスコープが設定され、チームのすべてのメンバーに表示されます。 Bot と同様に、ユーザーはチャネルで呼び出しを行うために、送信 webhook の名前を** \@ 言及**する必要があります。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 送信 Webhook HMAC トークンを確認するメソッドを作成する

サービスが実際の Teams クライアントからの呼び出しのみを受信できるようにするために、Teams では、認証プロトコルに常に含まれている必要がある HTTP `hmac` ヘッダーに HMAC コードが用意されています。

コードで、要求に含まれる HMAC 署名を常に検証する必要があり、以下のような動作が求められます。

* メッセージの要求本文から HMAC トークンを*生成*します。 ほとんどのプラットフォームでこれを行うための標準ライブラリがあります (Node.js の場合は [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) を*参照してください*。また、C\# の場合は「[Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs)」を*参照してください*)。 Microsoft Teams では、標準の SHA256 HMAC 暗号化を使用します。 本文を UTF8 でバイト配列に変換する必要があります。
* Teams クライアントで送信 Webhook を登録したときに **Teams によって提供された**セキュリティ トークンのバイト配列からハッシュを*計算*します。 以降の説明の「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を*参照してください*。
* UTF-8 エンコーディングを使用してハッシュを文字列に*変換*します。
* 生成されたハッシュの文字列の値と、HTTP 要求で指定された値を*比較*します。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 成功または失敗の応答を送信するメソッドを作成する

送信 Webhook からの応答は、元のメッセージと同じ返信チェーンに表示されます。 ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行し、コードには、メッセージに応答するための 5 秒間が与えられます。この時間を過ぎると、接続がタイムアウトして終了します。

### <a name="example-response"></a>応答の例

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>送信 Webhook を作成する

1. 適切なチームを選び、[(&#8226;&#8226;&#8226;)] ドロップダウン メニューから **[チームの管理]** を選択します。
1. ナビゲーション バーから **[アプリ]** タブを選択します。
1. ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。
1. 表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。

>* **名前** - Webhook のタイトルと @メンションのタップです。
>* **コールバック URL** - JSON ペイロードを受け入れ、Teams からの POST 要求を受信する HTTPS エンドポイントです。
>* **説明** - プロフィール カード、チームのレベルのアプリ ダッシュボードに表示される詳細な文字列です。
>* **プロフィール画像** (省略可能) Webhook のアプリ アイコンです。
>* ポップアップ ウィンドウの右下隅にある **[作成]** ボタンを選択すると、送信 Webhook が現在のチームのチャネルに追加されます。
>* 次のダイアログ ウィンドウには、[ハッシュベースのメッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) のセキュリティ トークンが表示されます。このトークンは、Teams と指定された外部サービスとの通話の認証に使用されます。
>* URL が有効で、サーバーとクライアントの認証トークンが等しい (HMAC のハンドシェイクである) 場合、チームのユーザーは送信 Webhook を使用できるようになります。

## <a name="code-samples"></a>コード サンプル

GitHub で送信 Webhook のコード サンプルを確認することができます。

### <a name="nodejs"></a>Node.js

[OfficeDev/msteams-samples-outgoing-webhook-nodejs](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a>C\#

[OfficeDev/microsoft-teams-sample-outgoing-webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
