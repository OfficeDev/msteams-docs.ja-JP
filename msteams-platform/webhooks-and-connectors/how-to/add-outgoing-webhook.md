---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
description: 送信 Webhook を追加する方法について説明します。
ms.topic: conceptual
ms.author: lajanuar
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: 20d30be7a35b33b94dc4a856439c51d5d0cc441c
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093254"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>送信 Webhook を使用して Teams にカスタム ボットを追加する

## <a name="what-are-outgoing-webhooks-in-teams"></a>Teams での送信 Webhook とは

Webhook は、Teams を外部アプリと統合するための最も優れた方法です。 基本的に Webhook は、コールバック URL に送信される POST 要求です。 送信 Webhook を使用すると、ユーザーは Microsoft Bot Framework を介してボットを作成する完全なプロセスを実行することなく、Web サービスにメッセージ [を送信できます](https://dev.botframework.com/)。

送信 Webhook は、Teams から JSON ペイロードを受け入れ可能な選択されたサービスにデータを送信します。 送信 Webhook をチームに追加した後、ボットとして機能し、メンションを使用してチャネル内のメッセージを検索 **\@ します**。 外部 Web サービスに通知を送信し、カードや画像を含むリッチ メッセージで応答します。

## <a name="outgoing-webhook-key-features"></a>送信 Webhook の主な機能

| 機能 | 説明 |
| ------- | ----------- |
| スコープ指定された構成| Webhook はチームのレベルでスコープが設定されます。 送信 Webhook を追加するチームごとにセットアップ プロセスを実行する必要があります。 |
| 反応性メッセージング| ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。 現在、ユーザーはパブリック チャネル内の送信 Webhook にのみメッセージを送信できます。個人用スコープまたはプライベート スコープ内ではメッセージを送信できます。 |
|標準の HTTP メッセージ交換|応答は元の要求メッセージと同じチェーンに表示され、リッチ テキスト、画像、カード、絵文字など、任意のボット フレームワーク メッセージ コンテンツを含めできます。 送信 Webhook はカードを使用することができますが、次の場合を除き、カードアクションを使用することはできません `openURL` 。|
| Teams API メソッドのサポート|送信 Webhook は、HTTP POST を Web サービスに送信し、応答を処理します。 チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。|

## <a name="creating-actionable-messages"></a>操作可能なメッセージの作成

コネクタ カードには、カードに表示される 3 つのボタンが含まれます。 各ボタンは、アクションを `potentialAction` 使用してメッセージのプロパティで定義 `ActionCard` されます。 それぞれに `ActionCard` 入力の種類、テキスト フィールド、日付の選択、または複数選択肢リストが含まれる。 各 `ActionCard` アクションには、たとえば、関連付けられたアクションがあります `HttpPOST` 。

コネクタ カードでは、3 種類のアクションがサポートされています。

| アクション | 説明 |
| ------- | ----------- |
| `ActionCard` |1 つ以上の入力の種類と関連するアクションを表示します。|
| `HttpPOST` | POST 要求を URL に送信します。 |
| `OpenUri` |  URI を別のブラウザーまたはアプリで開きます。必要に応じて、オペレーティング システムに基づいて異なる URI を対象とします。|

`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。

| 入力の種類 | 説明 |
| ------- | ----------- |
| `TextInput` | 1 行または複数行のテキスト フィールドで、オプションの長さ制限があります。 |
| `DateInput` | オプションの時刻セレクターを含む日付セレクター。 |
| `MultichoiceInput` | 1 つの選択または複数の選択肢を提供する、指定された選択肢のリスト。|

`MultichoiceInput` は `style` 、完全に展開されたリストの表示を制御するプロパティをサポートします。 既定値は値 `style` によって異 `isMultiSelect` なります。

| `isMultiSelect` value  | `style` 既定値  |
| --- | --- |
| `false` または指定なし | 既定のスタイルは次の値です。 `compact`|
| `true` | 既定のスタイルは次の値です。 `expanded` |

> [!NOTE]
> * 複数選択リストをコンパクト なスタイルで表示する場合は、両方 `"isMultiSelect": true` `"style": true` を入力します。
> * Teams で `compact` プロパティを `style` 選択する方法は、Microsoft Outlook でプロパティを選択する場合 `normal` `style` と同じです。
> * Webhook は、365 Officeカードとアダプティブ カードのみをサポートします。

コネクタ カードのアクションに関するその他の詳細については、操作 **[可能](/outlook/actionable-messages/card-reference#actions)** なメッセージ カード リファレンスの「アクション」を参照してください。

## <a name="adding-outgoing-webhooks-to-your-app"></a>送信 Webhook をアプリに追加する

**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。  
**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する

サービスは、標準の Azure Bot Service メッセージング スキーマでメッセージを受信します。 ボット フレームワーク コネクタは [、AZURE Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理するサービスを支援する RESTful サービスです。 [Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。 [「Azure Bot Service について」も参照してください](/azure/bot-service/bot-service-overview-introduction)。


送信 Webhook はレベルにスコープが設定され、すべてのチーム `team` メンバーに表示されます。 ボットと同様に、ユーザーは送信 **\@** Webhook の名前をメンションしてチャネルで呼び出す必要があります。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 送信 Webhook HMAC トークンを確認するメソッドを作成する

#### <a name="hmac-signature-for-testing-with-code-example"></a>コード例を使ったテスト用の HMAC 署名

受信メッセージと ID の例を使用: {"contoso" の SigningKeyDictionary の "contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。

要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。

サービスが実際の Teams クライアントからの呼び出しのみを受信するために、Teams は HTTP ヘッダーに HMAC コードを提供 `hmac` します。 常に認証プロトコルにコードを含める。

コードでは、要求に含まれる HMAC 署名を常に検証する必要があります。

* メッセージの要求本文から HMAC トークンを生成します。 ほとんどのプラットフォームでこれを行う標準的なライブラリがあります (Node.jsの[](https://nodejs.org/api/crypto.html#crypto_crypto)Crypto を参照するか[、C 用の Teams Webhook サンプル](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs)を参照してください \# )。 Microsoft Teams では、標準的な SHA256 HMAC 暗号化を使用します。 UTF8 で本文をバイト配列に変換する必要があります。
* Teams クライアントで送信 Webhook を登録したときに Teams によって提供されたセキュリティ トークンのバイト配列からハッシュを **計算** します。 「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を参照してください。
* UTF-8 エンコーディングを使用してハッシュを文字列に変換します。
* 生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 成功または失敗の応答を送信するメソッドを作成する

送信 Webhook からの応答は、元のメッセージと同じ返信チェーンに表示されます。 ユーザーがクエリを実行すると、Microsoft Teams はサービスに同期 HTTP 要求を発行し、コードは接続がタイム アウトして終了する前にメッセージに応答するために 5 秒を取得します。

### <a name="example-response"></a>応答の例

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>送信 Webhook を作成する

1. 適切なチームを選択し、(&#8226;&#8226;&#8226;) ドロップダウン メニューから [チームの管理] を選択します。
1. ナビゲーション バーから **[アプリ]** タブを選択します。
1. ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。
1. 表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。

>* **名前** - Webhook のタイトルと @メンションのタップです。
>* **コールバック URL** - JSON ペイロードを受け入れ、Teams から POST 要求を受信する HTTPS エンドポイント。
>* **説明** - プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列。
>* **Webhook** のオプションのアプリ アイコンのプロファイル画像。
>* ポップアップ ウィンドウ **の** 右下隅から [作成] ボタンを選択すると、送信 Webhook が現在のチームのチャネルに追加されます。
>* 次のダイアログ ウィンドウには、Teams と指定された外部サービスとの間の呼び出しを認証するために使用されるハッシュベースのメッセージ認証コード [(HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) セキュリティ トークンが表示されます。
>* 送信 Webhook は、URL が有効で、サーバー認証トークンとクライアント認証トークンが等しい場合 (HMAC ハンドシェイクなど) の場合にのみ、チームのユーザーが使用できます。

## <a name="code-samples"></a>コード サンプル

GitHub で送信 Webhook のコード サンプルを確認することができます。

### <a name="nodejs"></a>Node.js

[OfficeDev/msteams-samples-outgoing-webhook-nodejs](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a>C\#

[OfficeDev/microsoft-teams-sample-outgoing-webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
