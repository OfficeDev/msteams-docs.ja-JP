---
title: 匿名ユーザー用のアプリをビルドする
author: v-sdhakshina
description: 匿名ユーザー向けのアプリを構築し、すべての管理者設定を持つ会議アプリで匿名ユーザーに提供されるエクスペリエンスをテストする方法について説明します。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: ff897c5135740557e12898e7e5d231557b2e2823
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615477"
---
# <a name="build-apps-for-anonymous-users"></a>匿名ユーザー用のアプリを作成する

アプリでボット、メッセージング拡張機能、カード、タスク モジュールを構築して、匿名の会議参加者と対話できます。

匿名ユーザーに対するアプリのエクスペリエンスをテストするには、会議の招待で URL を選択し、プライベート ブラウザー ウィンドウから会議に参加します。

## <a name="admin-setting-for-anonymous-user-app-interaction"></a>匿名ユーザー アプリの操作の管理設定

Teams 管理者は、管理者ポータルを使用して、テナント全体の匿名ユーザー アプリの操作を有効または無効にすることができます。 既定では、この設定は有効になっています。 詳細については、「 [匿名ユーザーが会議でアプリを操作できるようにする](/microsoftteams/meeting-settings-in-teams)」を参照してください。

## <a name="in-meeting-getcontext-from-teams-client-sdk"></a>Teams クライアント SDK から getContext をIn-Meetingする

アプリは、共有アプリ ステージから API を呼び出すときに、匿名ユーザーに対して次の `getContext` 情報を受け取ります。 **[不明**] の値を確認することで、匿名ユーザーを`userLicenseType`認識できます。

```csharp
"userObjectId": "8:anon:<GUID1>",
"userLicenseType": "Unknown",
"loginHint": "8:teamsvisitor:<ID>",
"userPrincipalName": "8:teamsvisitor:<ID>",
"tid": "<meeting organizer tenant ID>"
```

| **プロパティ名** | **説明** |
| --- | --- |
| `userObjectId` | 匿名ユーザーの一意の生成値。 この値は、Graph API の呼び出しでは使用できません。 |
| `userLicenseType` | `Unknown`は匿名ユーザーを表します。 |
| `loginHint` | 一意の生成された値。 この値は、ログイン フローのヒントとして使用できません。 |
| `userPrincipalName` | 一意の生成された値。 この値は、Graph API の呼び出しでは使用できません。 |
| `tid` | 会議開催者のテナント ID。 |

> [!NOTE]
> 匿名ユーザーが会議に参加すると、新しいユーザー ID が生成されます。 匿名ユーザーが会議に再参加するたびに、別のユーザー ID が生成されます。

## <a name="bot-activities-and-apis"></a>ボットのアクティビティと API

いくつかの違いにより、ボットに送信されるアクティビティとボット API から受け取る応答は、匿名の会議参加者と匿名でない会議参加者の間で一貫しています。 一般に、以下のことが行われます。

* ユーザー ID は生成された値であり、匿名ユーザーが会議に参加するたびに異なります。
* プロパティは `aadObjectId` 省略されます。
* プロパティは `userRole` 匿名に設定 **されます**。
* 指定されたテナント ID は、会議開催者のテナント ID に設定されます。

### <a name="get-members-and-get-single-member-apis"></a>メンバーを取得し、単一メンバー API を取得する

[メンバーを取得](/microsoftteams/platform/bots/how-to/get-teams-context#fetch-the-roster-or-user-profile)し、[1 つのメンバー API を取得すると](/microsoftteams/platform/bots/how-to/get-teams-context#get-single-member-details)、匿名ユーザーに限定された情報が返されます。

```json
{ 
  "id": "<GUID1>", 
  "name": "<AnonTest (Guest)>",  
  "tenantId": "<GUID2>", 
  "userRole": "anonymous" 
} 
```

| **プロパティ名** | **説明** |
| --- | --- |
| `id` | 匿名ユーザーの一意の生成値。 |
| `name` | 会議に参加するときに匿名ユーザーによって提供される名前。 |
| `tenantId` | 会議開催者のテナント ID。 |
| `userRole` | `anonymous`は匿名ユーザーを表します。 |

> [!NOTE]
> ボット API と Teams クライアント SDK API から受信した ID は同じではありません。

### <a name="conversationupdate-activity-membersadded-and-membersremoved"></a>ConversationUpdate アクティビティ MembersAdded と MembersRemoved

```csharp
{ 
  "membersAdded": [ 
    { 
      "id": "<GUID1>" 
    } 
  ], 
  "type": "conversationUpdate", 
  "timestamp": "<timestamp>", 
  "id": "<event unique identifier>", 
  "channelId": "msteams", 
  "serviceUrl": "<serviceURL>", 
  "from": { 
    "id": "<GUID2>" 
  }, 
  "conversation": { 
    "isGroup": true, 
    "tenantId": "<tenant id>", 
    "id": "<conversation id>" 
  }, 
  "recipient": { 
    "id": "<bot id>", 
    "name": "<bot name>" 
  }, 
  "channelData": { 
    "tenant": { 
      "id": "<tenant id>" 
    }, 
    "source": null, 
    "meeting": { 
      "id": "<meeting id>" 
    } 
  } 
} 
```

| **プロパティ名** | **説明** |
| --- | --- |
| `membersAdded.id` | 匿名ユーザー ID。 |
| `from.id` | 会議の開催者 ID。 |
| `conversation.tenantId` | 会議開催者のテナント ID。 |
| `conversation.id` | 会議チャットの会話 ID。 |
| `tenant.id` | 会議開催者のテナント ID。 |

同様の変更がアクティビティ ペイロードに `membersRemoved` 適用されます。

> [!NOTE]
>
> 匿名ユーザーが会議に参加または退席すると、ペイロード内の `from` オブジェクトには、他のユーザーによってアクションが実行された場合でも、常に会議の開催者の ID が保持されます。

### <a name="create-conversation-api"></a>Conversation API を作成する

ボットは、匿名ユーザーとの 1 対 1 の会話を開始することはできません。 ボットが匿名ユーザーのユーザー ID を使用して会話 API の作成を呼び出すと、不適切な `400` 要求状態コードと次のエラー応答が表示されます。

```csharp
{ 
  "error": {
    "code": "BadArgument",
    "message": "Bot cannot create a conversation with an anonymous user"
  }
} 
```

### <a name="adaptive-cards"></a>アダプティブ カード

匿名ユーザーは、会議チャットでアダプティブ カードを表示および操作できます。 アダプティブ カードアクションは、匿名ユーザーと非匿名ユーザーの場合と同じように動作します。 詳細については、「 [カードアクション](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)」を参照してください。

## <a name="known-issues-and-limitations"></a>既知の問題と制限事項

* サイド パネル のタブとコンテンツ バブルは、匿名ユーザーには使用できません。 匿名ユーザーは、会議ステージで共有されているアプリ コンテンツを引き続き表示できます。

* 匿名ユーザーの場合、ボットから `getContext` 受信したユーザー ID とユーザー ID は異なります。 この 2 つを直接関連付けすることはできません。 タブとボットの間でユーザーの ID を追跡する必要がある場合は、外部 ID プロバイダーで認証するようにユーザーに求めるメッセージを表示する必要があります。

* 匿名ユーザーには、アプリの実際のアイコンではなく、ボット メッセージとカードに汎用アプリ アイコンが表示されます。 以下に例を示します。

    :::image type="content" source="../assets/images/apps-in-meetings/app-icon.png" alt-text="このスクリーンショットは、匿名ユーザーのアプリ アイコンの表示方法を示しています。":::

## <a name="see-also"></a>関連項目

* [Teams 会議ステージ用のアプリをビルドする](build-apps-for-teams-meeting-stage.md)
* [会議アプリ API](meeting-apps-apis.md)
* [Microsoft Teams ボットの仕組み](/azure/bot-service/bot-builder-basics-teams)
