---
title: 着信通知
description: 着信からの通知の処理に関する詳細な技術情報
ms.topic: conceptual
localization_priority: Normal
keywords: 呼び出し通知コールバック地域アフィニティ
ms.date: 04/02/2019
ms.openlocfilehash: 5c24aa83b26999070f65978fce9b19139f2445955acb8f5aa7b5c0a46255c927
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705046"
---
# <a name="incoming-call-notifications"></a>着信通知

会議[の呼び出しと](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)会議ボットを登録するMicrosoft Teams URL を呼び出す Webhook について説明します。 この URL は、ボットへのすべての着信呼び出しの Webhook エンドポイントです。

## <a name="protocol-determination"></a>プロトコルの決定

受信通知は、以前のプロトコルと互換性を保つレガシ形式[でSkypeされます](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)。 呼び出しを Microsoft Graph プロトコルに変換するには、ボットが通知が従来の形式であるかどうかを判断し、次の応答を提供する必要があります。

```http
HTTP/1.1 204 No Content
```

ボットは通知を再び受信しますが、今回は Microsoft Graphされます。

リアルタイム メディア プラットフォームの将来のリリースでは、アプリケーションがサポートするプロトコルを構成して、従来の形式で最初のコールバックを受信しないようにすることができます。

次のセクションでは、展開に地域アフィニティ用にリダイレクトされる着信呼び出し通知の詳細について説明します。

## <a name="redirects-for-region-affinity"></a>地域アフィニティのリダイレクト

Webhook は、呼び出しをホストするデータ センターから呼び出します。 呼び出しは任意のデータ センターで開始され、地域アフィニティは考慮されません。 通知は、GeoDNS 解決に応じて展開に送信されます。 アプリケーションが最初の通知ペイロードを調べ、それ以外の場合は別の展開で実行する必要があると判断した場合、アプリケーションは次の応答を提供します。

```http
HTTP/1.1 302 Found
Location: your-new-location
```

ボットが応答 API を使用して着信呼び出しに応答 [できます](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) 。 この特定の呼び `callbackUri` 出しを処理するを指定できます。 これは、呼び出しが特定のパーティションによって処理され、この情報を適切なインスタンスにルーティングするために埋め込むステートフル インスタンスに `callbackUri` 役立ちます。

次のセクションでは、Webhook に投稿されたトークンを調によるコールバックの認証の詳細を示します。

## <a name="authenticate-the-callback"></a>コールバックの認証

ボットは、Webhook に投稿されたトークンを検査して要求を検証する必要があります。 API が Webhook に投稿する度に、HTTP POST メッセージには、承認ヘッダーに OAuth トークンがベアラー トークンとして含まれます。対象ユーザーはアプリケーションのアプリ ID です。

アプリケーションは、コールバック要求を受け入れる前に、このトークンを検証する必要があります。

コールバックを認証するには、次のサンプル コードを使用します。

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

OAuth トークンは次の値を持ち、次の値で署名Skype。

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

公開されている OpenID 構成 <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> を使用して、トークンを確認できます。 各 OAuth トークンの値は、次のように使用されます。

* `aud` 対象ユーザーは、アプリケーションに指定されたアプリ ID URI です。
* `tid` は、ユーザーのテナント id Contoso.com。
* `iss` はトークン発行者です `https://api.botframework.com` 。

コード処理では、Webhook はトークンを検証し、有効期限が切れていないか確認し、発行された OpenID 構成によって署名されているかどうかを確認する必要があります。 コールバック要求を受け入れる前に、aud がアプリ ID と一致するかどうかを確認する必要があります。

詳細については、「受信要求 [の検証」を参照してください](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリケーションホスト型メディア ボットの要件と考慮事項](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
