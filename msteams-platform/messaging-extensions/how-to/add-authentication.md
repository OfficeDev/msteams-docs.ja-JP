---
title: メッセージ拡張機能に認証を追加する
author: surbhigupta
description: このモジュールでは、コード例とサンプルを使用してメッセージング拡張機能に認証を追加する方法について説明します
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: cca9aef8e08b9d997497e1531db928d8e29d7eac
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143544"
---
# <a name="add-authentication-to-your-message-extension"></a>メッセージ拡張機能に認証を追加する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>ユーザーを識別する

サービスに対するすべての要求には、ユーザー ID、ユーザーの表示名、および Azure Active Directory オブジェクト ID が含まれます。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

`id` および `aadObjectId` の値は、認証された Teams ユーザーに対して保証されます。 これらは、サービス内の資格情報またはキャッシュされた状態を検索するためのキーとして使用されます。 さらに、各要求には、ユーザーの組織を識別するために使用される Azure Active Directory テナント ID が含まれています。 該当する場合、要求には、要求の送信元となるチーム ID とチャネル ID も含まれます。

## <a name="authentication"></a>認証

サービスでユーザー認証が必要な場合、ユーザーはメッセージ拡張機能を使用する前にサインインする必要があります。 認証手順は、ボットまたはタブの手順と似ています。シーケンスは次のとおりです。

1. ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。
1. サービスは、Teams ユーザー ID を調べることで、ユーザーが認証されているかどうかを確認します。
1. ユーザーが認証されていない場合は、`auth` 応答を`openUrl` 認証 URL を含む推奨アクションを返します。
1. Microsoft Teams クライアントは、指定された認証 URL を使用して Web ページをホストするダイアログ ボックスを起動します。
1. ユーザーがサインインしたら、ウィンドウを閉じて **認証コード** を Teams クライアントに送信する必要があります。
1. Teams クライアントは、手順 5 で渡された認証コードを含むクエリをサービスに再発行します。

サービスは、手順 6 で受け取った認証コードが手順 5 の認証コードと一致することを確認する必要があります。 これにより、悪意のあるユーザーがサインイン フローのなりすましや侵害を試みないようにします。 これにより、安全な認証シーケンスを終了させるための 「ループを閉じる」 効果があります。

### <a name="respond-with-a-sign-in-action"></a>サインイン アクションで応答する

認証されていないユーザーにサインインを求めるには、認証 URL を含む `openUrl` 型の推奨アクションで応答します。

#### <a name="response-example-for-a-sign-in-action"></a>サインイン アクションの応答の例

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
>
> * サインイン エクスペリエンスを Teams ポップアップ ウィンドウでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧に含まれている必要があります。詳細については、「マニフェスト スキーマの [validDomains](~/resources/schema/manifest-schema.md#validdomains)」 を参照してください。
> * 認証ポップアップのサイズは、幅と高さのクエリ文字列パラメーター `Value = $"{_siteUrl}/searchSettings.html?height=600&width=600"` を含めることによって定義できます。

### <a name="start-the-sign-in-flow"></a>サインイン フローを開始する

サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。 メッセージ パッシングを使用する [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) と統合する必要があります。

Microsoft Teams 内で実行される他の埋め込みエクスペリエンスと同様に、ウィンドウ内のコードは、最初に `microsoftTeams.initialize()` を呼び出す必要があります。 コードで OAuth フローを実行する場合は、Teams ユーザー ID をウィンドウに渡し、OAuth サインイン URL に渡すことができます。

### <a name="complete-the-sign-in-flow"></a>サインイン フローを完了する

サインイン要求が完了し、ページにリダイレクトされたら、次の手順を実行する必要があります。

1. セキュリティ コード (乱数) を生成します。 このコードは、OAuth 2.0 トークンなどのサインイン フローで取得した資格情報を使用して、サービスにキャッシュする必要があります。
1. `microsoftTeams.authentication.notifySuccess` を呼び出して、セキュリティ コードを渡します。

この時点でウィンドウが閉じ、コントロールが Teams クライアントに渡されます。 クライアントは、`state` プロパティのセキュリティ コードと共に、元のユーザー クエリを再発行します。 コードでは、セキュリティ コードを使用して、前に保存した資格情報を検索して認証シーケンスを完了し、ユーザー要求を完了できます。

#### <a name="reissued-request-example"></a>再発行された要求の例

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="code-sample"></a>コード サンプル

|**サンプルの名前** | **説明** |**.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|メッセージ拡張機能 - 認証と構成 | 構成ページを含み、検索要求を受け入れ、ユーザーがサインインした後に結果を返すメッセージ拡張機能。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[表示](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="see-also"></a>関連項目

[メッセージ拡張機能のシングル サインオン (SSO) のサポート](~/messaging-extensions/how-to/enable-sso-auth-me.md)
