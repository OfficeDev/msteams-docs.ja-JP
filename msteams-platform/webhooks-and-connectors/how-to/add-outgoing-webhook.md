---
title: 送信 Webhook を使用して Microsoft Teams にカスタム ボットを追加する
description: 発信 Webhook を追加する方法を説明します
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: チームタブ送信ウェブフックアクション可能なメッセージは、ウェブフックを確認します
ms.openlocfilehash: a5a0cdfc9080ac4567f438b6fb6fd0671df8c19f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566531"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>送信ウェブフックを使用してTeamsにカスタムボットを追加する

## <a name="outgoing-webhooks-in-teams"></a>Teamsでの送信ウェブフック

Webhook は、Teamsが外部アプリと統合するための優れた方法です。 基本的に Webhook は、コールバック URL に送信される POST 要求です。 送信 webhook を使用すると、ユーザーは[Microsoft Bot Framework](https://dev.botframework.com/)を介してボットを作成する完全なプロセスを経ることなく、Web サービスにメッセージを送信できます。

送信 webhook は、json ペイロードを受け入れることができる任意の選択されたサービスにTeamsからデータを送信します。 発信ウェブフックをチームに追加した後、ボットとして機能し、**\@ メンション** を使用してチャネル内のメッセージを探します。 外部 Web サービスに通知を送信し、カードや画像を含むリッチメッセージで応答します。

## <a name="outgoing-webhook-key-features"></a>送信 Webhook の主な機能

| 機能 | 説明 |
| ------- | ----------- |
| スコープ構成| Webhook はチームのレベルでスコープが設定されます。 送信 webhook を追加する各チームのセットアップ プロセスを実行する必要があります。 |
| 反応型メッセージング| ユーザーは、メッセージを受信するために Webhook に @メンションを使用する必要があります。 現在、ユーザーはパブリック チャネル内の送信 Webhook のみをメッセージで送信でき、個人スコープまたはプライベート スコープ内ではメッセージを送信できません。 |
|標準の HTTP メッセージ交換|応答は元の要求メッセージと同じチェーンに表示され、リッチテキスト、画像、カード、絵文字などのボットフレームワークメッセージコンテンツを含めることができます。 発信 Webhook ではカードを使用できますが、 以外のカード アクションは使用できません `openURL` 。|
| Teams API メソッドのサポート|送信 Webhook は HTTP POST を Web サービスに送信し、応答を処理します。 チーム内の名簿やチャネルの一覧の取得など、他の API にはアクセスすることはできません。|

## <a name="creating-actionable-messages"></a>操作可能なメッセージの作成

コネクタ カードには、カードに 3 つのボタンが表示されます。 各ボタンは、アクションを `potentialAction` 使用してメッセージのプロパティで定義 `ActionCard` されます。 それぞれに `ActionCard` は、入力タイプ、テキストフィールド、日付ピッカー、または複数選択リストが含まれます。 各 `ActionCard` アクションには、関連付けられたアクションがあります `HttpPOST` 。

コネクタ カードでは、3 種類のアクションがサポートされています。

| アクション | 説明 |
| ------- | ----------- |
| `ActionCard` |1 つ以上の入力タイプと関連するアクションを示します。|
| `HttpPOST` | URL に POST 要求を送信します。 |
| `OpenUri` |  別のブラウザーまたはアプリで URI を開き、オプションで、オペレーティング システムに基づいて異なる URI を対象にします。|

`ActionCard` アクションでは、次の 3 つの入力の種類がサポートされています。

| 入力タイプ | 説明 |
| ------- | ----------- |
| `TextInput` | 長さの制限を省略できる単一行または複数行のテキスト フィールド。 |
| `DateInput` | オプションの時間セレクタを持つ日付セレクタ。 |
| `MultichoiceInput` | 単一の選択または複数の選択を提供する、指定された選択肢のリスト。|

`MultichoiceInput` は、 `style` 完全に展開されたリストの表示を制御するプロパティをサポートします。 デフォルト値は `style` 、値によって異なります `isMultiSelect` 。

| `isMultiSelect` 価値  | `style` 既定値  |
| --- | --- |
| `false` または指定なし | デフォルトのスタイルは `compact`|
| `true` | デフォルトのスタイルは `expanded` |

> [!NOTE]
> * `"isMultiSelect": true` `"style": true` 複数選択リストをコンパクトなスタイルで表示する場合は、 と と の両方を入力します。
> * `compact` `style` Teamsでプロパティを選択することは `normal` 、Microsoft Outlookでプロパティを選択するのと同 `style` じです。
> * Webhook は、Office 365メッセージ バック カードとアダプティブ カードのみをサポートします。

コネクタ カードアクションに関するその他の詳細については、アクション可能なメッセージ カード リファレンスの **[アクション](/outlook/actionable-messages/card-reference#actions)** を参照してください。

## <a name="adding-outgoing-webhooks-to-your-app"></a>アプリへの送信ウェブフックの追加

**シナリオ**: Teams のチャネル データベース サーバーの変更状況通知をアプリにプッシュします。  
**例**: Teams のチャネルの HR ユーザーが Office 365 テナント全体で従業員のレコードに対して行った、すべての CRUD 操作を追跡する基幹業務アプリがあります。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. アプリのサーバー上で URL を作成し、JSON ペイロードを使用して POST 要求を受け入れて処理する

サービスは、標準の Azure ボット サービス メッセージング スキーマでメッセージを受信します。 ボット フレームワーク コネクタは、 [サービスが、Azure Bot](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)サービス API に記載されている HTTPS プロトコルを介して JSON 形式のメッセージの交換を処理する権限を与える RESTful サービスです。 [Microsoft Bot Framework SDK] を使用して、メッセージの処理と解析を行うこともできます。 [「Azure ボット サービスについて](/azure/bot-service/bot-service-overview-introduction)」も参照してください。


発信 webhook は、レベルにスコープされ `team` 、すべてのチーム メンバーに表示されます。 ボットと同様に、ユーザーはチャネルで呼び出すために発信 webhook の名前を **\@ 指定** する必要があります。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 送信 Webhook HMAC トークンを確認するメソッドを作成する

#### <a name="hmac-signature-for-testing-with-code-example"></a>コード例を使ったテスト用の HMAC 署名

受信メッセージと ID の例を使用して: {"contoso"、"vqF0En+Z0ucuRTM/01o2GuhMH3hKk/N2bOmlM31zaA=" の署名キーディクショナリの "contoso" }

要求ヘッダーの認証には、"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" という値を使用します。

サービスが実際のTeams クライアントからのみ呼び出しを受信するように、Teamsは HTTP ヘッダーに HMAC コードを提供 `hmac` します。 常に認証プロトコルにコードを含める。

コードは、要求に含まれる HMAC 署名を常に検証する必要があります。

* メッセージの要求本文から HMAC トークンを生成します。 ほとんどのプラットフォームでこれを行うための標準ライブラリがあります (Node.js用[の暗号を](https://nodejs.org/api/crypto.html#crypto_crypto)参照するか、または C の[Webhook サンプルTeams](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs)参照 \# してください)。 Microsoft Teamsは、標準の SHA256 HMAC 暗号化を使用します。 本体を UTF8 でバイト配列に変換する必要があります。
* Teams クライアントで送信 Webhook を登録したときに Teams によって提供されたセキュリティ トークンのバイト配列からハッシュを **計算** します。 「[送信 Webhook を作成する](#create-an-outgoing-webhook)」を参照してください。
* UTF-8 エンコーディングを使用してハッシュを文字列に変換します。
* 生成されたハッシュの文字列の値と、HTTP 要求で指定された値を比較します。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 成功または失敗の応答を送信するメソッドを作成する

送信 Webhook からの応答は、元のメッセージと同じ応答チェーンに表示されます。 ユーザーがクエリを実行すると、Microsoft Teamsサービスに同期 HTTP 要求が発行され、コードは、接続がタイムアウトして終了する前にメッセージに応答するために 5 秒を取得します。

### <a name="example-response"></a>応答の例

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>送信 Webhook を作成する

1. 適切なチームを選択し、(&#8226;&#8226;&#8226;)ドロップダウンメニューから **[チームの管理** ]を選択します。
1. ナビゲーション バーから **[アプリ]** タブを選択します。
1. ウィンドウの右下隅で、**[送信 Webhook を作成する]** を選択します。
1. 表示されたポップアップ ウィンドウの必要なフィールドへの入力を行います。

>* **名前**: ウェブフックのタイトルと@mentionタップ
>* **コールバック URL**: JSON ペイロードを受け取り、Teamsからの POST 要求を受信する HTTPS エンドポイント
>* **説明**: プロファイル カードとチーム レベルのアプリ ダッシュボードに表示される詳細な文字列
>* **プロフィール写真**: ウェブフック用のオプションのアプリアイコン
>* ポップアップ ウィンドウの右下隅にある [ **作成]** ボタンを選択すると、送信 webhook が現在のチームのチャンネルに追加されます。
>* 次のダイアログ ウィンドウには、Teamsと指定された外部サービス間の呼び出しを認証するために使用される[ハッシュ ベース メッセージ認証コード (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)セキュリティ トークンが表示されます。
>* 発信 webhook は、URL が有効で、サーバーとクライアントの認証トークンが等しい場合のみ、チームのユーザーが使用できます(HMAC ハンドシェイクなど)。

## <a name="code-sample"></a>コード サンプル
|**サンプル名** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 送信 Webhook | Microsoft Teamsで使用する **カスタム ボットを** 作成するサンプル。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

