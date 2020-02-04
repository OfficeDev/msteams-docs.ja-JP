---
title: メッセージング拡張機能に認証を追加する
author: clearab
description: メッセージング拡張機能に認証を追加する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f7ebbcd99b1ec35900de7ec2f54f93263918e945
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674688"
---
# <a name="add-authentication-to-your-messaging-extension"></a>メッセージング拡張機能に認証を追加する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>ユーザーを識別する

サービスへのすべての要求には、要求を実行したユーザーの難読化された ID、およびユーザーの表示名と Azure Active Directory オブジェクト ID が含まれます。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

と`id` `aadObjectId`の値は、認証された Teams のユーザーのものであることが保証されています。 これらは、サービスの資格情報またはキャッシュされた状態を検索するためのキーとして使用できます。 さらに、各要求には、ユーザーの Azure Active Directory テナント ID が含まれています。これは、ユーザーの組織を識別するために使用できます。 該当する場合、要求には、要求の発行元であるチームおよびチャネル Id も含まれます。

## <a name="authentication"></a>認証

サービスでユーザー認証が必要な場合は、メッセージング拡張機能を使用できるようにするには、ユーザーにサインインする必要があります。 ユーザーにサインインする bot またはタブを書いてある場合は、このセクションを理解しておく必要があります。

順序は次のとおりです。

1. ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。
2. サービスは、ユーザーが Teams ユーザー ID を調べて最初に認証されているかどうかを確認します。
3. ユーザーが認証されていない場合は`auth` 、認証 URL `openUrl`を含む推奨されるアクションを使用して応答を返信に送り返します。
4. Microsoft Teams クライアントは、指定された認証 URL を使用して、web ページをホストするポップアップウィンドウを起動します。
5. ユーザーがサインインした後、ウィンドウを閉じて、Teams クライアントに "認証コード" を送信する必要があります。
6. Teams クライアントは、手順5で渡された認証コードを含む、サービスに対してクエリを再度発行します。

サービスは、手順6で受信した認証コードが手順5と一致することを確認する必要があります。 これにより、悪意のあるユーザーがサインインフローをスプーフィングしたり、侵害したりすることを防ぐことができます。 これにより、"ループを閉じる" というセキュリティで保護された認証シーケンスが完了します。

### <a name="respond-with-a-sign-in-action"></a>サインインアクションで応答する

認証されていないユーザーにサインインを求めるメッセージを表示するに`openUrl`は、認証 URL を含む種類の推奨されるアクションで応答します。

#### <a name="response-example-for-a-sign-in-action"></a>サインインアクションの応答の例

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
> チームのポップアップでサインインするために、URL のドメイン部分は、アプリの有効なドメインの一覧に含まれている必要があります。 (マニフェストスキーマの[Validdomains](~/resources/schema/manifest-schema.md#validdomains)を参照してください)。

### <a name="start-the-sign-in-flow"></a>サインインフローを開始する

サインイン手順は、ポップアップウィンドウ内に表示されるようにする必要があります。 これは、メッセージパッシングを使用する[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。

Microsoft Teams 内部で実行されている他の組み込みエクスペリエンスと同様に、ウィンドウ内`microsoftTeams.initialize()`のコードは最初に呼び出す必要があります。 コードで OAuth フローを実行すると、Teams ユーザー ID をウィンドウに渡すことができます。これにより、OAuth サインイン URL に渡されます。

### <a name="complete-the-sign-in-flow"></a>サインインフローを完了する

サインイン要求が完了し、ページにリダイレクトされたら、次の手順を実行します。

1. セキュリティコードを生成します。 (これはランダムな数値になることがあります。)このコードを、サインインフロー (OAuth 2.0 トークンなど) で取得した資格情報と共にサービスにキャッシュする必要があります。
2. を`microsoftTeams.authentication.notifySuccess`呼び出して、セキュリティコードを渡します。

この時点で、ウィンドウが閉じられ、Teams クライアントに制御が渡されます。 クライアントは、元のユーザークエリと、 `state`プロパティのセキュリティコードを再発行することができるようになります。 コードでは、セキュリティコードを使用して、前に保存した資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。

#### <a name="reissued-request-example"></a>再発行した要求の例

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

