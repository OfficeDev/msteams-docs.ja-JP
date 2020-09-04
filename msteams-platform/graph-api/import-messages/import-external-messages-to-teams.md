---
title: Microsoft Graph を使用して外部プラットフォームのメッセージを Teams にインポートする
description: Microsoft Graph を使用して外部プラットフォームから Teams にメッセージをインポートする方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 余裕期間インポートメッセージ api グラフ microsoft は移行の投稿を移行する
ms.openlocfilehash: 0e0aa96373d29f07893456adf54986ec23bdec3c
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340950"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする

>[!IMPORTANT]
> Microsoft Graph と Microsoft Teams の公開プレビューは、早期アクセスおよびフィードバックに使用できます。 このリリースは広範なテストを経ていますが、運用環境での使用は想定されていません。

Microsoft Graph を使用すると、ユーザーの既存のメッセージ履歴やデータを外部システムから Teams チャネルに移行できます。 Teams 内にサードパーティ製のプラットフォームのメッセージング階層を再利用できるようにすることで、ユーザーはシームレスな方法で通信を継続し、中断することなく処理を進めることができます。

## <a name="import-overview"></a>インポートの概要

高レベルでは、インポートプロセスは次の要素で構成されます。

1. [バックタイムタイムスタンプを使用してチームを作成する](#step-one-create-a-team)
1. [バックタイムタイムスタンプを使用してチャネルを作成する](#step-two-create-a-channel)  
1. [外部のバックインタイムの日付のメッセージをインポートする](#step-three-import-messages)
1. [チームおよびチャネルの移行プロセスを完了する](#step-four-complete-migration-mode)
1. [チームメンバーを追加する](#step-five-add-team-members)

## <a name="necessary-requirements"></a>必要な要件

### <a name="analyze-and-prepare-message-data"></a>メッセージデータを分析して準備する

✔では、サードパーティのデータを確認して、移行対象を決定します。  
✔サードパーティのチャットシステムから選択されたデータを抽出します。  
✔、移行に必要な形式にインポートデータを変換します。  
✔、サードパーティのチャット構造を Teams 構造にマップします。

### <a name="set-up-your-office-365-tenant"></a>Office 365 テナントのセットアップ

✔インポートデータに Office 365 テナントが存在することを確認してください。 Teams 用の Office 365 テナントの設定の詳細については、「 [office 365 テナントを準備](../../concepts/build-and-test/prepare-your-o365-tenant.md)する *」を参照してください*。  
✔チームメンバーが Azure Active Directory (AAD) に含まれていることを確認します。  詳細につい*て*[は、](/azure/active-directory/fundamentals/add-users-azure-active-directory) 「Azure Active Directory に新しいユーザーを追加する」を参照してください。

## <a name="step-one-create-a-team"></a>手順 1: チームを作成する

既存のデータは移行されているため、移行プロセス中の元のメッセージのタイムスタンプを維持し、メッセージングの動作を防ぐために、ユーザーの既存のメッセージフローを Teams に再作成するための鍵となります。 これは次のようにして実現されます。

1. チームリソースプロパティを使用して、タイムスタンプを持つ[新しいチームを作成](/graph/api/team-post?view=graph-rest-beta&tabs=http)し `createdDateTime` ます。  

1. `migration mode`移行プロセスが完了するまで、チーム内のほとんどのアクティビティからのユーザーを表示する特別な状態で、新しいチームをに配置します。 `teamCreationMode` `migration` 移行のために作成される新しいチームを明示的に識別するために、POST 要求に値のインスタンス属性を含めます。  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意|対象となるエンティティ/Api|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行を管理する|Microsoft Teams への移行のためのリソースの作成、管理|**アプリケーション専用**|**はい**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>要求 (移行状態でチームを作成する)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a>エラー メッセージ

```http
400 Bad Request
```

* `createdDateTime`  将来のために設定します。
* `createdDateTime`  正しく指定されていますが、 `teamCreationMode`  インスタンス属性がないか、無効な値に設定されています。

## <a name="step-two-create-a-channel"></a>手順 2: チャネルを作成する

インポートされたメッセージのチャネルの作成は、「チームを作成する」シナリオに似ています。 

1. Channel リソースプロパティを使用して、タイムスタンプがある[新しいチャネルを作成](/graph/api/channel-post?view=graph-rest-beta&tabs=http)し `createdDateTime` ます。

1. 新しいチャネルを `migration mode` 、移行プロセスが完了するまで、チャネル内のほとんどのチャットアクティビティからのユーザーを示す特別な状態で、その新しいチャネルを配置します。  `channelCreationMode` `migration` 移行のために作成される新しいチームを明示的に識別するために、POST 要求に値のインスタンス属性を含めます。  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意|対象となるエンティティ/Api|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行を管理する|Microsoft Teams への移行のためのリソースの作成、管理|**アプリケーション専用**|**はい**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>要求 (移行状態でチャネルを作成する)

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a>エラー メッセージ

```http
400 Bad Request
```

* `createdDateTime`  将来のために設定します。
* `createdDateTime`  正しく指定されていますが、 `channelCreationMode`  インスタンス属性がないか、無効な値に設定されています。

## <a name="step-three-import-messages"></a>手順 3: メッセージをインポートする

チームとチャネルを作成したら、 `createdDateTime`  要求本文のキーとキーを使用して、タイムラインメッセージの送信を開始することができ `from`  ます。

#### <a name="request-post-message-that-is-text-only"></a>要求 (テキストのみの投稿メッセージ)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
    "replyToId": null,
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="request-post-a-message-with-inline-image"></a>要求 (インラインの ' image を含むメッセージを投稿する)

> **注**: 要求は chatmessage の一部であるため、このシナリオでは特別なアクセス許可スコープがありません。チャットメッセージのスコープも同様に適用されます。

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

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
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
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
    {
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a>手順 4: 移行モードを完了する

メッセージの移行プロセスが完了すると、チームとチャネルの両方が、メソッドを使用して移行モードから除外され  `completeMigration`  ます。 この手順では、チームメンバーによって一般的に使用されるチームとチャネルのリソースを開きます。 アクションはインスタンスにバインドされ `team` ます。

#### <a name="request-end-team-migration-mode"></a>要求 (エンドチーム移行モード)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>要求 (エンドチャネル移行モード)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a>エラー応答

```http
400 Bad Request
```

* に呼び出され `team` た、または `channel` のでないアクション `migrationMode` 。

## <a name="step-five-add-team-members"></a>手順 5: チームメンバーを追加する

Teams UI または Microsoft Graph [add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API[を使用して](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)、チームにメンバーを追加することができます。

#### <a name="request-add-member"></a>要求 (メンバーの追加)

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>ヒントと追加情報

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Teams に含まれていないユーザーからメッセージをインポートできます。

* `completeMigration`要求が行われると、チームにさらにメッセージをインポートすることはできません。

* チームメンバーは、 `completeMigration` 要求が正常な応答を返した後は、新しいチームにのみ追加できます。

* 調整: チャネルごとに5個の RPS でメッセージがインポートされます。

* 移行結果に訂正を加える必要がある場合は、チームを削除して、チームとチャネルを作成してメッセージを再移行するための手順を繰り返す必要があります。

> [!NOTE]
> 現在、インライン画像は、インポートメッセージ API スキーマでサポートされている唯一の種類のメディアです。

##### <a name="import-content-scope"></a>コンテンツスコープのインポート

|範囲内 | 現在スコープ外|
|----------|--------------------------|
|チームおよびチャネルのメッセージ|1:1 およびグループチャットメッセージ|
|元のメッセージの作成日時|プライベート チャネル|
|メッセージの一部としてのインライン画像|メンション|
|SPO/OneDrive の既存ファイルへのリンク|感想|
|リッチテキスト付きのメッセージ|動画|
|メッセージの返信チェーン|お知らせ|
|高スループット処理|コード スニペット|
||アダプティブカード|
||シール|
||絵文字|
||括る|
||チャネル間でのクロス投稿|

> [!div class="nextstepaction"]
>[Microsoft Graph と Teams の統合の詳細情報](/graph/teams-concept-overview)
