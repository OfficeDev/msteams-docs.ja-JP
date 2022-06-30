---
title: Microsoft Graph を使用して外部プラットフォーム メッセージを Teams にインポートする
description: Microsoft Graph を使用して外部プラットフォームから Teams にメッセージをインポートする方法について説明します。
ms.localizationpriority: high
author: akjo
ms.author: lajanuar
ms.topic: Overview
ms.openlocfilehash: 853a3d28254a1d6a6f74da553c0047ae0803e6be
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484853"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする

Microsoft Graph を使用すると、ユーザーの既存のメッセージ履歴とデータを外部システムから Teams チャネルに移行できます。 Teams 内でサード パーティのプラットフォーム メッセージング階層を再現できるようにすることで、ユーザーはシームレスな方法で通信を継続し、中断することなく続行できます。

> [!NOTE]
> 今後、Microsoft は、インポートされるデータの量に基づいて、お客様またはお客様の顧客に追加料金の支払いを要求する場合があります。

## <a name="import-overview"></a>インポートの概要

大まかに言うと、インポート プロセスは次の要素で構成されます。

1. [バックインタイム タイムスタンプを持つチームを作成する](#step-1-create-a-team)。
1. [バックインタイム タイムスタンプを持つチャネルを作成する](#step-2-create-a-channel)。
1. [外部のバックインタイム 日付メッセージをインポートする](#step-3-import-messages)。
1. [チームとチャネルの移行プロセスを完了す](#step-4-complete-migration-mode)。
1. [チーム メンバーを追加する](#step-five-add-team-members)。

## <a name="prerequisites"></a>前提条件

### <a name="analyze-and-prepare-message-data"></a>メッセージ データを分析して準備する

* サード パーティのデータを確認して、移行する内容を決定します。  
* 選択したデータをサード パーティのチャット システムから抽出します。  
* サード パーティのチャット構造を Teams 構造にマッピングします。  
* インポート データを移行に必要な形式に変換します。  

### <a name="set-up-your-office-365-tenant"></a>Office 365 テナントのセットアップ

* インポート データの Office 365 テナントが存在することを確認します。 Teams の Office 365 テナントを設定する方法の詳細については、「[Office 365 テナントを準備する](../../concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。
* チーム メンバーが Azure Active Directory にいることを確認します。 詳細については、「Azure AD に[新しいユーザーを追加](/azure/active-directory/fundamentals/add-users-azure-active-directory)する」を参照してください。

## <a name="step-1-create-a-team"></a>手順 1: リストを作成する

既存のデータを移行するため、元のメッセージ タイムスタンプを維持し、移行プロセス中にメッセージング アクティビティを防止することは、Teams でユーザーの既存のメッセージ フローを再作成する際に重要です。 これは次のように実現されます。

> チーム リソース `createdDateTime` プロパティを使用して、バックインタイム タイムスタンプを持つ[新しいチームを作成します](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true)。 移行プロセスが完了するまで `migration mode` のチーム内のほとんどのアクティビティからユーザーを制限する特別な状態の新しいチームを配置します。 `teamCreationMode` インスタンス属性と `migration` 値を POST リクエストに含めて、移行用に作成された新しいチームを明示的に識別します。  

> [!NOTE]
> `createdDateTime` フィールドは、移行されたチームまたはチャネルのインスタンスにのみ設定されます。

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意はありましたか?|対象となるエンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行の管理|Teams に移行するためのリソースを作成して管理する。|**アプリケーション専用**|**はい**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>POST リクエストの例については、「要求 (移行状態でチームを作成する)」をご覧ください。

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

次のシナリオでは、エラー メッセージを受け取ることができます。

* `createdDateTime` が将来に向けて設定されている場合。
* `createdDateTime` は正しく指定されていますが、`teamCreationMode` インスタンス属性が欠落しているか、無効な値に設定されています。

## <a name="step-2-create-a-channel"></a>ステップ 2: 移行タスクを作成する

インポートされたメッセージのチャネルの作成は、チームの作成シナリオと似ています。

> チャネル リソース `createdDateTime` プロパティを使用して、バックインタイム タイムスタンプを持つ[新しいチャネルを作成](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true)します。 新しいチャネルを `migration mode` に配置します。これは、移行プロセスが完了するまで、チャネル内のほとんどのチャット アクティビティからユーザーを制限する特別な状態です。 `channelCreationMode` インスタンス属性と `migration` 値を POST リクエストに含めて、移行用に作成された新しいチームを明示的に識別します。  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意はありましたか?|対象となるエンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行の管理|Teams に移行するためのリソースを作成して管理する。|**アプリケーション専用**|**はい**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>リクエスト (移行状態でチャネルを作成する)

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

次のシナリオでは、エラー メッセージを受け取ることができます。

* `createdDateTime` が将来に向けて設定されている場合。
* `createdDateTime` が正しく指定されているが、`channelCreationMode` インスタンス属性が欠落しているか、無効な値に設定されている場合。

## <a name="step-3-import-messages"></a>手順 3: メッセージをインポートする

チームとチャネルが作成されたら、リクエスト本文の `createdDateTime` キーと `from` キーを使用してバックインタイム メッセージの送信を開始できます。

> [!NOTE]
>
> * メッセージ スレッド `createdDateTime` より前の `createdDateTime` でインポートされたメッセージはサポートされていません。
> * `createdDateTime` は、同じスレッド内のメッセージ間で一意である必要があります。
> * `createdDateTime` は、ミリ秒単位の精度のタイム スタンプをサポートします。 たとえば、受信要求メッセージの `createdDateTime` 値が *2020-09-16T05:50:31.0025302Z* の場合、メッセージの取り込み時に *2020-09-16T05:50:31.002Z* に変換されます。

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

#### <a name="request-post-a-message-with-inline-image"></a>リクエスト (インライン画像でメッセージを投稿)

> [!NOTE]
>
> * リクエストは `chatMessage` の一部であるため、このシナリオには特別な権限スコープはありません。
> * `chatMessage` のスコープはここに適用されます。

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

## <a name="step-4-complete-migration-mode"></a>手順 4: 移行モードを完了する

メッセージの移行プロセスが完了すると、チームとチャネルの両方が `completeMigration` メソッドを使用して移行モードから解除されます。 この手順では、チーム メンバーが一般的に使用するためにチーム リソースとチャネル リソースを開きます。 アクションは `team` インスタンスにバインドされます。 チームが完了する前に、すべてのチャネルを移行モードから完了する必要があります。

#### <a name="request-end-channel-migration-mode"></a>要求 (エンド チャネル移行モード)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration
```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>要求 (エンド チーム移行モード)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 NoContent
```

`migrationMode` にない `team` または `channel` で呼び出されたアクション。

## <a name="step-five-add-team-members"></a>手順 5: チーム メンバーを追加する

[Teams UI を使用](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)して、または Microsoft Graph [[メンバーを追加]](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API を使用して、チームにメンバーを追加できます。

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

## <a name="tips-and-additional-information"></a>ヒントとその他の情報

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* `completeMigration` 要求が行われた後、それ以降のメッセージをチームにインポートすることはできません。

* 新しいチームにチーム メンバーを追加できるのは、`completeMigration` 要求が成功した応答を返した後だけです。

* 調整: チャネルあたり 5 つの RPS でメッセージがインポートされます。

* 移行結果を修正する必要がある場合は、チームを削除し、手順を繰り返してチームとチャネルを作成し、メッセージを再移行する必要があります。

> [!NOTE]
> 現在、インライン イメージは、インポート メッセージ API スキーマでサポートされている唯一の種類のメディアです。

##### <a name="import-content-scope"></a>コンテンツ スコープをインポートする

次の表に、コンテンツ スコープを示します。

|スコープ内 | 現在はスコープ外です|
|----------|--------------------------|
|チーム メッセージとチャネル メッセージ|1:1 とグループ チャット メッセージ|
|元のメッセージの作成時刻|プライベート チャネル|
|メッセージの一部としてのインライン イメージ|＠メンション|
|SPO または OneDrive 内の既存のファイルへのリンク|リアクション|
|リッチ テキストを含むメッセージ|ビデオ|
|メッセージ応答チェーン|お知らせ|
|高スループット処理|コード スニペット|
||ステッカー|
||絵文字|
||見積もり|
||チャネル間のクロス 投稿|
||共有チャネル|

## <a name="see-also"></a>関連項目

* [Microsoft Graph と Teams の統合](/graph/teams-concept-overview)
* [Microsoft Teams エクスポート API を使ってコンテンツをエクスポートする](/microsoftteams/export-teams-content)
