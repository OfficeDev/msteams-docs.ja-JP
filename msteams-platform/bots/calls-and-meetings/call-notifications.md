---
title: 着信通知
description: コード サンプルを使用した着信呼び出しからの通知の処理、呼び出しのリダイレクトと認証に関する詳細な技術情報について説明します
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 呼び出しの通知コールバックリージョンのアフィニティ
ms.date: 04/02/2019
ms.openlocfilehash: e2844649764284f74e242967106adbfdc8edf8cf
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757144"
---
# <a name="incoming-call-notifications"></a>着信通知

[Microsoft Teamsの通話と会議ボットを登録する](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)際に、呼び出し URL の Webhook について説明します。 この URL は、ボットへのすべての着信呼び出しの Webhook エンドポイントです。

## <a name="protocol-determination"></a>プロトコルの決定

受信通知は、以前の[Skype プロトコル](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)との互換性を確保するために従来の形式で提供されます。 呼び出しを Microsoft Graph プロトコルに変換するには、ボットは通知がレガシ形式であるかどうかを判断し、次の応答を提供する必要があります。

```http
HTTP/1.1 204 No Content
```

ボットは再び通知を受け取りますが、今度は Microsoft Graph プロトコルで通知を受け取ります。

リアルタイム メディア プラットフォームの今後のリリースでは、アプリケーションがサポートするプロトコルを構成して、レガシ形式の初期コールバックを受信しないようにすることができます。

次のセクションでは、リージョンアフィニティにリダイレクトされた着信呼び出し通知について、デプロイにリダイレクトする方法について詳しく説明します。

## <a name="redirects-for-region-affinity"></a>リージョン アフィニティのリダイレクト

呼び出しをホストしているデータ センターから Webhook を呼び出します。 呼び出しはどのデータ センターでも開始され、リージョンのアフィニティは考慮されません。 GeoDNS の解決に応じて、通知がデプロイに送信されます。 アプリケーションが最初の通知ペイロードまたはその他の方法を調べることで、別のデプロイで実行する必要があると判断した場合、アプリケーションは次の応答を提供します。

```http
HTTP/1.1 302 Found
Location: your-new-location
```

ボットが応答 API を使用して着信呼び出しに [応答](/graph/api/call-answer?view=graph-rest-1.0&tabs=http&preserve-view=true) できるようにします。 この特定の `callbackUri` 呼び出しを処理するように指定できます。 これは、呼び出しが特定のパーティションによって処理され、適切なインスタンスへのルーティングのためにこの情報 `callbackUri` を埋め込むステートフル インスタンスに便利です。

次のセクションでは、Webhook に投稿されたトークンを調べることでコールバックを認証する方法について詳しく説明します。

## <a name="authenticate-the-callback"></a>コールバックを認証する

ボットは、Webhook に投稿されたトークンを調べて、要求を検証する必要があります。 API が Webhook に投稿するたびに、HTTP POST メッセージには承認ヘッダーに OAuth トークンがベアラー トークンとして含まれ、対象ユーザーはアプリケーションのアプリ ID になります。

コールバック要求を受け入れる前に、アプリケーションでこのトークンを検証する必要があります。

次のサンプル コードは、コールバックを認証するために使用されます。

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

OAuth トークンには次の値があり、Skypeによって署名されます。

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

公開されている <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> OpenID 構成を使用して、トークンを確認できます。 各 OAuth トークン値は、次のように使用されます。

* `aud` 対象ユーザーは、アプリケーションに指定されたアプリ ID URI です。
* `tid` は、Contoso.com のテナント ID です。
* `iss` はトークン発行者です。 `https://api.botframework.com`.

コード処理では、Webhook でトークンを検証し、有効期限が切れていないことを確認し、発行された OpenID 構成によって署名されているかどうかを確認する必要があります。 コールバック要求を受け入れる前に、aud がアプリ ID と一致するかどうかを確認する必要もあります。

詳細については、「 [受信要求の検証](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)」を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリケーションでホストされるメディア ボットの要件と考察](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)

## <a name="see-also"></a>関連項目

* [自動応答を設定する](/microsoftteams/create-a-phone-system-auto-attendant)
* [Android および Teams ビデオ電話デバイスの Microsoft Teams Rooms 自動応答を設定する](/microsoftteams/set-up-auto-answer-on-teams-android)