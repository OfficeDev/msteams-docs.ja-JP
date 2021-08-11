---
title: Microsoft Graphを使用して外部プラットフォーム メッセージをインポートTeams
description: Microsoft Graph を使用して外部プラットフォームからメッセージをインポートする方法についてTeams
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 17e68db9803e00d3dfb8743ba3b371753508fb5a3471317c25d7a42c8027c248
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704404"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする

Microsoft Graphを使用すると、ユーザーの既存のメッセージ履歴とデータを外部システムから別のチャネルにTeamsできます。 Teams 内のサード パーティプラットフォーム メッセージング階層のレクリエーションを有効にすると、ユーザーはシームレスな方法で通信を続行し、中断することなく続行できます。

> [!NOTE]
> 今後、Microsoft は、インポートされるデータの量に基づいて、お客様またはお客様の顧客に追加料金の支払いを要求する場合があります。

## <a name="import-overview"></a>インポートの概要

高レベルでは、インポート プロセスは次で構成されます。

1. [タイム スタンプを使用してチームを作成します](#step-1-create-a-team)。
1. [タイム スタンプを使用してチャネルを作成します](#step-2-create-a-channel)。
1. [外部のバックインタイム日付メッセージをインポートします](#step-3-import-messages)。
1. [チームとチャネルの移行プロセスを完了します](#step-4-complete-migration-mode)。
1. [チーム メンバーを追加します](#step-five-add-team-members)。

## <a name="prerequisites"></a>前提条件

### <a name="analyze-and-prepare-message-data"></a>メッセージ データの分析と準備

* サード パーティのデータを確認して、移行するデータを決定します。  
* 選択したデータをサードパーティのチャット システムから抽出します。  
* サード パーティ製のチャット構造を、その他のTeamsします。  
* インポート データを移行に必要な形式に変換します。  

### <a name="set-up-your-office-365-tenant"></a>Office 365 テナントのセットアップ

* インポート データにOffice 365テナントが存在することを確認します。 ユーザーのテナントを設定する方法のOffice 365については、「Teamsテナントの準備[」をOffice 365してください](../../concepts/build-and-test/prepare-your-o365-tenant.md)。
* チーム メンバーが (AAD) Azure Active Directory確認します。 詳細については、「AAD に [新しいユーザーを追加する](/azure/active-directory/fundamentals/add-users-azure-active-directory) 」を参照してください。

## <a name="step-1-create-a-team"></a>手順 1: チームを作成する

既存のデータを移行する場合は、元のメッセージ タイムスタンプを維持し、移行プロセス中にメッセージング アクティビティを防止する方法が、Teams でユーザーの既存のメッセージ フローを再作成する際に重要です。 これは、次のように実現されます。

> [チーム リソース プロパティを使用して](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 、タイム スタンプを使用して新しいチームを作成 `createdDateTime` します。 移行プロセスが完了するまで、チーム内のほとんどのアクティビティからユーザーを制限する特別な状態で、新しいチーム `migration mode` を配置します。 新しいチームが移行用に作成されているとして明示的に識別するには、POST 要求に値を持つ `teamCreationMode` `migration` instance 属性を含める。  

> [!NOTE]
> この `createdDateTime` フィールドは、移行されたチームまたはチャネルのインスタンスにのみ設定されます。

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意|対象のエンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行の管理|ユーザーへの移行用のリソースの作成とMicrosoft Teams。|**アプリケーション専用**|**はい**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>要求 (移行状態でチームを作成する)

```http
POST https://graph.microsoft.com/v1.0/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a>エラー メッセージ

```http
400 Bad Request
```

次のシナリオでエラー メッセージを受け取ります。

* If `createdDateTime` は将来に設定されます。
* 正 `createdDateTime` しく指定されているが `teamCreationMode` 、instance 属性が見つからないか、無効な値に設定されている場合。

## <a name="step-2-create-a-channel"></a>手順 2: チャネルを作成する

インポートされたメッセージのチャネルの作成は、チームの作成シナリオに似ています。

> [チャネル リソース プロパティを使用](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) して、タイム スタンプをバックインする新しいチャネルを作成 `createdDateTime` します。 移行プロセスが完了するまで、チャネル内のほとんどのチャット アクティビティからユーザーを制限する特別な状態で、新しいチャネル `migration mode` を配置します。 新しいチームが移行用に作成されているとして明示的に識別するには、POST 要求に値を持つ `channelCreationMode` `migration` instance 属性を含める。  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意|対象のエンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行の管理|ユーザーへの移行用のリソースの作成とMicrosoft Teams。|**アプリケーション専用**|**はい**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>要求 (移行状態でチャネルを作成する)

```http
POST https://graph.microsoft.com/v1.0/teams/{team-id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels/$entity",
   "id":"id-value",
   "createdDateTime":null,
   "displayName":"Architecture Discussion",
   "description":"This channel is where we debate all future architecture plans",
   "isFavoriteByDefault":null,
   "email":null,
   "webUrl":null,
   "membershipType":null,
   "moderationSettings":null
}
```

#### <a name="error-message"></a>エラー メッセージ

```http
400 Bad Request
```
次のシナリオでエラー メッセージを受け取ります。

* If `createdDateTime` は将来に設定されます。
* 正 `createdDateTime` しく指定されているが、 `channelCreationMode` インスタンス属性が見つからないか、無効な値に設定されている場合。

## <a name="step-3-import-messages"></a>手順 3: メッセージのインポート

チームとチャネルを作成したら、要求本文のキーとキーを使用して、バックインタイム メッセージ `createdDateTime` `from` の送信を開始できます。

> [!NOTE]
> * メッセージ スレッドより `createdDateTime` 前にインポートされたメッセージ `createdDateTime` はサポートされていません。
> * `createdDateTime` 同じスレッド内のメッセージ間で一意である必要があります。
> * `createdDateTime` ミリ秒単位の精度のタイムスタンプをサポートします。 たとえば、受信要求メッセージの値が `createdDateTime` *2020-09-16T05:50:31.0025302Z* の場合、メッセージが取り込まれたときに *2020-09-16T05:50:31.002Z* に変換されます。

#### <a name="request-post-message-that-is-text-only"></a>要求 (テキスト専用の POST メッセージ)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

{
   "createdDateTime":"2019-02-04T19:58:15.511Z",
   "from":{
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   }
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
   "id":"id-value",
   "replyToId":null,
   "etag":"id-value",
   "messageType":"message",
   "createdDateTime":"2019-02-04T19:58:15.58Z",
   "lastModifiedDateTime":null,
   "deleted":false,
   "subject":null,
   "summary":null,
   "importance":"normal",
   "locale":"en-us",
   "policyViolation":null,
   "from":{
      "application":null,
      "device":null,
      "conversation":null,
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   },
   "attachments":[
   ],
   "mentions":[
   ],
   "reactions":[
   ]
}
```

#### <a name="error-message"></a>エラー メッセージ

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>要求 (インライン イメージを含むメッセージを POST する)

> [!NOTE]
> * このシナリオでは、要求がに含まれるので、特別なアクセス許可スコープはありません `chatMessage` 。
> * 対象範囲は、 `chatMessage` ここで適用されます。

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

{
  "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"../hostedContents/1/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "hostedContents":[
        {
            "@microsoft.graph.temporaryId": "1",
            "contentBytes": "iVBORw0KGgoAAAANSUhEUgAAANcAAAExCAYAAADvFzeeAAAXjklEQVR4Ae2d/XNU1RnH+9e0FFrA0RCIyaS8hRA0HV5KbS1gHRgVpjMClY4GHJ3yYm1HCmXaWttaaZUZtIIFKYi8lFAkvOQ9u5vN225IARVBbX9/Os9NbrLZbMjmhCfJPX5+2Lmb3T25y3O+n/M599x7w9f+++UXwoMakIF7n4GvUdR7X1RqSk01A8CFuZm5GGUAuIwKi72wF3ABF+YyygBwGRUWc2Eu4AIuzGWUAeAyKizmwlzABVyYyygDwGVUWMyFuYALuDCXUQaAy6iwmAtzARdwfWXMdeuzT+TGxz3Sfb1LunrapL07IW3pePDQ5/qavqef0c+OdYAELuAac4jGGkLL9rdvfyo9N9ODQAqBGmmrwGlb/R0u3xG4gMspOC5hG882CoRaaCSA8n1ff9doIQMu4PIOrus3u+8ZVNnw6e/Od5AALuDKOyz5hmqiPnfnzi1J9bSbgRWCpvvQfY307wQu4BoxJCOFaDK8rwsQmQsUIQhWW93XSIsewAVckYdLQ24F0Ui/926AARdwRRounZ6Np7GyYdN9DzdFBC7gijRc43GMlQ1U9s/6HXJNjYELuHI<<-----Removed----->>>>",
            "contentType": "image/png"
        }
    ]
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
    "id": "id-value",
    "replyToId": null,
    "etag": "id-value",
    "messageType": "message",
    "createdDateTime": "2019-02-04T19:58:15.511Z",
    "lastModifiedDateTime": null,
    "deleted": false,
    "subject": null,
    "summary": null,
    "importance": "normal",
    "locale": "en-us",
    "policyViolation": null,
    "from": {
        "application": null,
        "device": null,
        "conversation": null,
        "user": {
            "id": "id-value",
            "displayName": "Joh Doe",
            "userIdentityType": "aadUser"
        }
    },
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-4-complete-migration-mode"></a>手順 4: 移行モードの完了

メッセージの移行プロセスが完了すると、チームとチャネルの両方がメソッドを使用して移行モードから取り出  `completeMigration` されます。 この手順では、チーム メンバーが一般的に使用するチームリソースとチャネル リソースを開きます。 アクションはインスタンスにバインド `team` されます。 チームが完了する前に、すべてのチャネルを移行モードから完了する必要があります。

#### <a name="request-end-channel-migration-mode"></a>要求 (エンド チャネル移行モード)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>要求 (チーム移行モードの終了)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 NoContent
```

a に対して呼び `team` 出されたアクション、 `channel` またはに含めされていないアクション `migrationMode` 。

## <a name="step-five-add-team-members"></a>手順 5: チーム メンバーを追加する

メンバーをチームに追加するには、次の UI または Microsoft Teams [API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)をGraph[使用](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)します。

#### <a name="request-add-member"></a>要求 (メンバーの追加)

```http
POST https://graph.microsoft.com/beta/teams/{team-id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>ヒントと追加情報

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* 要求が `completeMigration` 行われた後、チームにそれ以上のメッセージをインポートすることはできません。

* 新しいチームにチーム メンバーを追加できるのは、要求が正常に応答 `completeMigration` を返した後のみです。

* 調整: チャネルごとに 5 つの RPS でメッセージがインポートされます。

* 移行結果を修正する必要がある場合は、チームを削除し、手順を繰り返してチームとチャネルを作成し、メッセージを再移行する必要があります。

> [!NOTE]
> 現在、インライン イメージは、インポート メッセージ API スキーマでサポートされているメディアの唯一の種類です。

##### <a name="import-content-scope"></a>コンテンツ スコープのインポート

次の表に、コンテンツ スコープを示します。

|スコープ内 | 現在のスコープ外|
|----------|--------------------------|
|チームメッセージとチャネル メッセージ|1:1 およびグループ チャット メッセージ|
|元のメッセージの作成時刻|プライベート チャネル|
|メッセージの一部としてのインライン イメージ|メンション|
|SPO または SPO の既存のファイルへのOneDrive|リアクション|
|リッチ テキストを含むメッセージ|ビデオ|
|メッセージ返信チェーン|お知らせ|
|高スループット処理|コード スニペット|
||ステッカー|
||絵文字|
||見積もり|
||チャネル間のクロス投稿|


## <a name="see-also"></a>関連項目

[Microsoft GraphとTeams統合](/graph/teams-concept-overview)
