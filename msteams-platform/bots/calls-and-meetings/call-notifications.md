---
title: 着信呼び出し通知の処理に関する技術的な詳細
description: 着信呼び出しからの通知の処理に関する詳細な技術情報
keywords: 通話呼び出しの通知のコールバック領域の類似性
ms.date: 04/02/2019
ms.openlocfilehash: be8860ff70cd7dff4fd9599079ea7aab4f454174
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675044"
---
# <a name="incoming-call-notifications-technical-details"></a>着信通話通知: 技術的な詳細

「 [Microsoft Teams での通話と会議のボットの登録](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot)」では、 **(呼び出し元の) URL の webhook (呼び出し元)** の URL (bot へのすべての着信呼び出しの webhook エンドポイント) について説明しました。 このトピックでは、これらの通知に応答するために必要な技術情報について説明します。

## <a name="protocol-determination"></a>プロトコルの決定

受信通知は、以前の[Skype プロトコル](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)との互換性のために従来の形式で提供されます。 呼び出しを Microsoft Graph プロトコルに変換するために、ボットは通知が従来の形式であるかどうかを判断し、次のように応答する必要があります。

```http
HTTP/1.1 204 No Content
```

Bot は通知を再度受け取りますが、今回は Microsoft Graph プロトコルを使用します。

リアルタイムメディアプラットフォームの今後のリリースでは、アプリケーションがサポートするプロトコルを構成して、初期コールバックを従来の形式で受信しないようにすることができます。

## <a name="redirects-for-region-affinity"></a>地域の類似性のリダイレクト

呼び出しをホストしているデータセンターから webhook を呼び出します。 この呼び出しは、任意のデータセンターで開始され、地域の類似性が考慮されることはありません。 GeoDNS の解決に応じて、展開に通知が送信されます。 アプリケーションが初期通知ペイロードを調べることによって、またはそれ以外の場合は、別の展開で実行する必要があると判断すると、アプリケーションは次のように応答します。

```http
HTTP/1.1 302 Found
Location: your-new-location
```

Bot が[応答](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer)API を使用して着信呼び出しに応答できるようにします。 この特定の`callbackUri`呼び出しを処理するを指定できます。 これは、呼び出しが特定のパーティションによって処理される_ステートフル_なインスタンスで、 `callbackUri`右のインスタンスへのルーティングのためにこの情報をに埋め込む場合に便利です。

## <a name="authenticating-the-callback"></a>コールバックの認証

Bot は、要求を検証するために、webhook に投稿されたトークンを検査する必要があります。 API が webhook に投稿されるたびに、HTTP POST メッセージには、ユーザーがアプリケーションのアプリ ID として使用する、ベアラートークンとしての OAuth トークンが含まれます。

アプリケーションは、コールバック要求を受け入れる前に、このトークンを検証する必要があります。

```http
POST https://bot.contoso.com/api/calls
Content-Type: application/json
Authentication: Bearer <TOKEN>

"value": [
    "subscriptionId": "2887CEE8344B47C291F1AF628599A93C",
    "subscriptionExpirationDateTime": "2016-11-20T18:23:45.9356913Z",
    "changeType": "updated",
    "resource": "/app/calls/8A934F51F25B4EE19613D4049491857B",
    "resourceData": {
        "@odata.type": "#microsoft.graph.call",
        "state": "Established"
    }
]
```

OAuth トークンの値は次のようになり、Skype で署名されます。 で<https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration>公開されている OpenID configuration を使用して、トークンを確認できます。

```json
{
    "aud": "0efc74f7-41c3-47a4-8775-7259bfef4241",
    "iss": "https://api.botframework.com",
    "iat": 1466741440,
    "nbf": 1466741440,
    "exp": 1466745340,
    "tid": "1fdd12d0-4620-44ed-baec-459b611f84b2"
}
```

* **aud**対象ユーザーは、アプリケーションに対して指定されたアプリ ID URI です。
* **tid**は Contoso.com のテナント id です。
* **iss**はトークン発行者です`https://api.botframework.com`。

Webhook を処理するコードでは、トークンを検証し、有効期限が切れていないことを確認して、公開された OpenID configuration によって署名されているかどうかを確認する必要があります。 また、コールバック要求を受け入れる前に、 **aud**がアプリ ID と一致するかどうかも確認する必要があります。

[サンプル](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)は、受信要求を検証する方法を示しています。
