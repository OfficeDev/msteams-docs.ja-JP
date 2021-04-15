---
title: メッセージング拡張機能に認証を追加する
author: clearab
description: メッセージング拡張機能に認証を追加する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 04ece6fe6f5e824873ed6e69385bce017df6927d
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696774"
---
# <a name="add-authentication-to-your-messaging-extension"></a>メッセージング拡張機能に認証を追加する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>ユーザーを識別する

サービスに対する要求には、ユーザー ID、ユーザーの表示名、Azure Active Directory オブジェクト ID が含まれます。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

認証 `id` された `aadObjectId` Teams ユーザーの値と値が保証されます。 これらは、サービス内の資格情報またはキャッシュされた状態を参照するためのキーとして使用されます。 さらに、各要求には、ユーザーの組織を識別するために使用される、ユーザーの Azure Active Directory テナント ID が含まれます。 該当する場合、要求には、要求の発信元であるチーム ID とチャネル ID も含まれる。

## <a name="authentication"></a>認証

サービスでユーザー認証が必要な場合、ユーザーはメッセージング拡張機能を使用する前にサインインする必要があります。 認証手順は、ボットまたはタブの認証手順と似ています。シーケンスは次のとおりです。

1. ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。
1. サービスは、Teams ユーザー ID を検査して、ユーザーが認証されているかどうかを確認します。
1. ユーザーが認証されていない場合は、認証 URL を含む推奨されるアクションを含む応答 `auth` `openUrl` を返します。
1. Microsoft Teams クライアントは、指定された認証 URL を使用して Web ページをホストするダイアログ ボックスを起動します。
1. ユーザーがサインインした後、ウィンドウを閉じて、Teams クライアントに **認証コード** を送信する必要があります。
1. Teams クライアントは、手順 5 で渡された認証コードを含むクエリをサービスに再発行します。

サービスは、手順 6 で受信した認証コードが手順 5 の認証コードと一致することを確認する必要があります。 これにより、悪意のあるユーザーがサインイン フローのスプーフィングや侵害を試みない。 これにより、効果的に "ループを閉じる" と、セキュリティで保護された認証シーケンスが完了します。

### <a name="respond-with-a-sign-in-action"></a>サインイン アクションで応答する

認証されていないユーザーにサインインを求めるメッセージを表示するには、認証 URL を含む種類の推奨 `openUrl` されるアクションで応答します。

#### <a name="response-example-for-a-sign-in-action"></a>サインイン アクションの応答例

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
> サインイン エクスペリエンスを Teams ポップアップ ウィンドウでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧にある必要があります。 詳細については、マニフェスト [スキーマの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。

### <a name="start-the-sign-in-flow"></a>サインイン フローを開始する

サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。 メッセージの受け渡しを [使用する Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。

Microsoft Teams 内で実行されている他の埋め込みエクスペリエンスと同様に、ウィンドウ内のコードは最初に呼び出す必要があります `microsoftTeams.initialize()` 。 コードで OAuth フローを実行する場合は、Teams ユーザー ID をウィンドウに渡し、OAuth サインイン URL に渡します。

### <a name="complete-the-sign-in-flow"></a>サインイン フローを完了する

サインイン要求が完了し、ページにリダイレクトしたら、次の手順を実行する必要があります。

1. セキュリティ コードを生成します。 これは乱数です。 このコードは、OAuth 2.0 トークンなどのサインイン フローで取得した資格情報と共に、サービスにキャッシュする必要があります。
1. セキュリティ `microsoftTeams.authentication.notifySuccess` コードを呼び出して渡します。

この時点で、ウィンドウが閉じ、コントロールが Teams クライアントに渡されます。 クライアントは、プロパティのセキュリティ コードと共に、元のユーザー クエリを再発行 `state` します。 コードでは、セキュリティ コードを使用して、以前に格納された資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。

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
|**サンプル名** | **説明** |**.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|メッセージング拡張機能 - auth と config | 構成ページを持ち、検索要求を受け入れ、ユーザーがサインインした後に結果を返すメッセージング拡張機能。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
