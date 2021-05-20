---
title: Microsoft Graphを使用して外部プラットフォーム メッセージをTeamsにインポートする
description: Microsoft Graphを使用して外部プラットフォームからTeamsにメッセージをインポートする方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: チームインポートメッセージ API グラフ マイクロソフト移行の投稿
ms.openlocfilehash: 5ea06e8b490bae0595abb31086848d0b050bded0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566160"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする

Microsoft Graphでは、ユーザーの既存のメッセージ履歴とデータを外部システムからTeamsチャネルに移行できます。 Teams内のサードパーティのプラットフォームメッセージング階層の再作成を可能にすることで、ユーザーはシームレスな方法で通信を継続し、中断することなく続行できます。

> [!NOTE] 
> 今後、Microsoft は、インポートされるデータの量に基づいて、お客様またはお客様の顧客に追加料金の支払いを要求する場合があります。

## <a name="import-overview"></a>インポートの概要

大まかに言えば、インポートプロセスは次の要素で構成されます。

1. [バックインタイムタイムスタンプを持つチームを作成する](#step-one-create-a-team)
1. [バックインタイムタイムスタンプを使用してチャネルを作成する](#step-two-create-a-channel) 
1. [外部バックインタイムの日付付きメッセージをインポートする](#step-three-import-messages)
1. [チームとチャネルの移行プロセスを完了する](#step-four-complete-migration-mode)
1. [チーム メンバーの追加](#step-five-add-team-members)

## <a name="necessary-requirements"></a>必要な要件

### <a name="analyze-and-prepare-message-data"></a>メッセージ データの分析と準備

✔ サード パーティのデータを確認して、移行する内容を決定します。  
✔ 選択したデータをサードパーティのチャット システムから抽出します。  
✔ サードパーティのチャット構造をTeams構造にマップします。  
✔ インポート データを移行に必要な形式に変換します。  

### <a name="set-up-your-office-365-tenant"></a>Office 365 テナントのセットアップ

✔ インポート データのOffice 365テナントが存在することを確認します。 Teams用のOffice 365テナントの設定の詳細については[、「Office 365 テナントの準備](../../concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。  
✔ チーム メンバーが Azure Active Directory (AAD) に所属していることを確認します。  詳細については[、「Azure Active Directoryに新しいユーザーを追加](/azure/active-directory/fundamentals/add-users-azure-active-directory)する」を参照してください。

## <a name="step-one-create-a-team"></a>ステップ 1: チームを作成する

既存のデータが移行されるため、移行プロセス中に元のメッセージ・タイム・スタンプを維持し、メッセージング・アクティビティーを防止することが、Teamsでユーザーの既存のメッセージ・フローを再作成する鍵となります。 これは、次のように行われます。

> チーム リソース プロパティを使用して、バックイン タイム タイムスタンプを使用して[新しい](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true)チームを作成 `createdDateTime` します。 新しいチームを `migration mode` に配置し、移行プロセスが完了するまで、チーム内のほとんどのアクティビティからユーザーを禁止する特別な状態にします。 POST `teamCreationMode` 要求に値を持つインスタンス属性を含めて `migration` 、新しいチームを移行用に作成するチームとして明示的に識別します。  

> [!Note]
> この `createdDateTime` フィールドは、移行されたチームまたはチャネルのインスタンスに対してのみ設定されます。

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意?|対象となるエンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行の管理|Microsoft Teamsへの移行用リソースの作成、管理。|**アプリケーションのみ**|**はい**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>リクエスト (移行状態でチームを作成する)

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

#### <a name="error-messages"></a>エラー メッセージ

```http
400 Bad Request
```

* `createdDateTime`  将来に向けて設定します。
* `createdDateTime`  正しく指定されていますが、 `teamCreationMode`  インスタンス属性が見つからないか、無効な値に設定されています。

## <a name="step-two-create-a-channel"></a>ステップ 2: チャネルを作成する

インポートされたメッセージのチャネルの作成は、チーム作成シナリオと似ています。

> チャネル リソース プロパティを使用して、バックイン タイム タイムスタンプを使用して[新しい](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true)チャネルを作成 `createdDateTime` します。 新しいチャネルを `migration mode` に配置する特別な状態では、移行プロセスが完了するまで、チャネル内のほとんどのチャット アクティビティからユーザーを表示します。  POST `channelCreationMode` 要求に値を持つインスタンス属性を含めて `migration` 、新しいチームを移行用に作成するチームとして明示的に識別します。  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意?|対象となるエンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行の管理|Microsoft Teamsへの移行用リソースの作成、管理。|**アプリケーションのみ**|**はい**|`POST /teams`|

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

* `createdDateTime`  将来に向けて設定します。
* `createdDateTime`  正しく指定されていますが `channelCreationMode`  、インスタンス属性が欠落しているか、無効な値に設定されています。

## <a name="step-three-import-messages"></a>手順 3: メッセージをインポートする

チームとチャネルを作成した後、要求本文の キーと キーを使用して、バックインタイム メッセージの送信を開始できます `createdDateTime` `from`  。 **メモ**: メッセージ `createdDateTime` スレッドより前のバージョンでインポートされたメッセージ `createdDateTime` はサポートされていません。

> [!NOTE]
> * `createdDateTime` 同じスレッド内のメッセージ間で一意である必要があります。
> * `createdDateTime` はミリ秒精度のタイムスタンプをサポートします。 たとえば、着信要求メッセージの値が `createdDateTime` *2020-09-16T05:50:31.0025302Z* に設定されている場合、メッセージの取り込み時に *2020-09-16T05:50:31.002Z* に変換されます。

#### <a name="request-post-message-that-is-text-only"></a>要求 (テキストのみである POST メッセージ)

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

#### <a name="error-messages"></a>エラー メッセージ

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>要求 (インライン 画像を含むメッセージを POST)

> [!Note]
> 要求は chatMessage の一部であるため、このシナリオには特別なアクセス許可スコープはありません。チャットメッセージのスコープもここに適用されます。

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

## <a name="step-four-complete-migration-mode"></a>ステップ 4: 移行モードを完了する

メッセージの移行プロセスが完了すると、チームとチャネルの両方が、このメソッドを使用して移行モードから除外されます  `completeMigration`  。 この手順では、チーム メンバーが一般的に使用するチームリソースとチャネル リソースを開きます。 アクションはインスタンスにバインドされます `team` 。 チームを完了するには、すべてのチャネルを移行モードから終了する必要があります。

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

* にはない 、 に対して呼び出 `team` `channel` されるアクション `migrationMode` 。

## <a name="step-five-add-team-members"></a>ステップ 5: チーム メンバーを追加する

Teams UI または Microsoft の [メンバーの追加] API[を使用して](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)、[チームにメンバー](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Graph追加できます。

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

* 要求が `completeMigration` 完了すると、チームにメッセージをインポートすることはできません。

* チーム メンバーは、要求が正常な応答を返した後にのみ新しいチームに追加できます `completeMigration` 。

* スロットル: チャネルあたり 5 RPS でメッセージをインポートします。

* 移行結果を修正する必要がある場合は、チームを削除し、チームとチャネルを作成し、メッセージを再移行する手順を繰り返す必要があります。

> [!NOTE]
> 現在、インライン イメージは、インポート メッセージ API スキーマでサポートされるメディアの唯一の種類です。

##### <a name="import-content-scope"></a>コンテンツの範囲をインポートする

|スコープ内 | 現在範囲外|
|----------|--------------------------|
|チームおよびチャネルメッセージ|1:1 とグループ チャット メッセージ|
|元のメッセージの作成時刻|プライベート チャネル|
|メッセージの一部としてのインライン 画像|言及時|
|SPO/OneDrive内の既存のファイルへのリンク|反応|
|リッチ テキストを含むメッセージ|ビデオ|
|メッセージ応答チェーン|お知らせ|
|高スループット処理|コード スニペット|
||ステッカー|
||絵文字|
||引用符|
||チャネル間のクロスポスト|


## <a name="see-also"></a>関連項目

[マイクロソフトのGraphとTeams統合の詳細](/graph/teams-concept-overview)
