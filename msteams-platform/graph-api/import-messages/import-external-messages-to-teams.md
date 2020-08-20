---
title: Microsoft Graph を使用して外部プラットフォームのメッセージを Teams にインポートする
description: Microsoft Graph を使用して、外部プラットフォームから Teams にメッセージをインポートする方法について説明します
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 'Teams Slack インポート メッセージ API グラフ: Microsoft が移行後の移行を行います'
ms.openlocfilehash: 8e8b21c9a38570d7ede745e27b9316b7aba29956
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46820370"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Microsoft Graph を使用して、サードパーティのプラットフォームのメッセージを Teams にインポートする

>[!IMPORTANT]
> Microsoft Graph と Microsoft Teams のパブリック プレビューは、すでにアクセスしてフィードバックを行います。 このリリースは、拡張的なテストを受けてきてきてきませんが、運用環境での使用を意図したものではありません。

Microsoft Graph では、ユーザーの既存のメッセージ履歴とデータを外部システムから Teams チャネルに移行できます。 サードパーティ プラットフォームのメッセージング階層を Teams 内で再作成できるようにすれば、ユーザーは中断することなく通信をシームレスに続行し、操作を続行できます。

## <a name="import-overview"></a>インポートの概要

大まかに説明したインポート プロセスは次のとおりです。

1. [バックタイムスタンプを持つチームを作成する](#step-one-create-a-team)
1. [バックタイムスタンプを持つチャネルを作成する](#step-two-create-a-channel)  
1. [外部の後に戻る日付付きメッセージをインポートする](#step-three-import-messages)
1. [チームとチャネルの移行プロセスを完了する](#step-four-complete-migration-mode)
1. [チーム メンバーを追加する](#step-five-add-team-members)

## <a name="necessary-requirements"></a>必要な要件

### <a name="analyze-and-prepare-message-data"></a>メッセージ データの分析と準備

✔サードパーティのデータを確認して、移行される内容を決定します。  
✔サード パーティのチャット システムから選択したデータを抽出します。  
✔必要な形式にインポート データを変換します。  
✔ーチームのチャット構造を Teams 構造にマップします。

### <a name="set-up-your-office-365-tenant"></a>Office 365 テナントのセットアップ

✔ 365 Officeがインポート データ用に存在することを確認します。 Teams に対する Office 365 テナンシーのセットアップ*see*の詳細については、「Teams の[Office 365 テナントを準備する」をご覧ください](../../concepts/build-and-test/prepare-your-o365-tenant.md)。  
✔メンバーが Azure Active Directory (AAD) に含むことを確認してください。  詳細 *については、「Azure* Active Directory [に新しいユーザー](/azure/active-directory/fundamentals/add-users-azure-active-directory) を追加する」を参照してください。

## <a name="step-one-create-a-team"></a>手順 1: チームを作成する

既存のデータを移行するので、元のメッセージ タイムスタンプを維持し、移行プロセス中のメッセージング処理を防止することが、Teams でのユーザーの既存のメッセージ フローを再作成するうえで重要です。 これは、次のように実現されます。

1. [team リソース プロパティを使用](/graph/api/team-post?view=graph-rest-beta&tabs=http) して、バックタイムタイムタイムスタンプを持つ新しいチームを作成  `createdDateTime`  します。  

1. 新しいチームを、移行 `migration mode` プロセスが完了するまでチーム内のほとんどのアクティビティのユーザーを主に主な状態にして配置します。 移行用 `teamCreationMode` に新しいチーム `migration` を明示的に識別するには、POST 要求にインスタンス属性を含めるようにします。  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意を有するか|対象エンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行を管理する|Microsoft Teams への移行に使用するリソースの作成、管理|**アプリケーションのみ**|**はい**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>要求 (移行状態のチームを作成する)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
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

* `createdDateTime`  将来設定します。
* `createdDateTime`  正しく指定されましたが `teamCreationMode`  、インスタンス属性がないか無効な値に設定されています。

## <a name="step-two-create-a-channel"></a>手順 2: チャネルを作成する

インポートされたメッセージのチャネルの作成は、チーム作成シナリオと似ています。 

1. channel[リソース プロパティを使用](/graph/api/channel-post?view=graph-rest-beta&tabs=http)して、時間内タイムスタンプを持つ新しいチャネルを作成 `createdDateTime` します。

1. 新しいチャネルは、 `migration mode` 移行プロセスが完了するまでチャネル内のほとんどのチャット アクティビティのユーザーをバーでバー表示する特別な状態になります。  移行用 `channelCreationMode` に新しいチーム `migration` を明示的に識別するには、POST 要求にインスタンス属性を含めるようにします。  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>アクセス許可

|ScopeName|DisplayName|説明|型|管理者の同意を有するか|対象エンティティ/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Microsoft Teams への移行を管理する|Microsoft Teams への移行に使用するリソースの作成、管理|**アプリケーションのみ**|**はい**|`POST /teams`|

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

* `createdDateTime`  将来設定します。
* `createdDateTime`  正しく指定された `channelCreationMode`  が、インスタンス属性がないか、無効な値に設定されています。

## <a name="step-three-import-messages"></a>手順 3: メッセージをインポートする

チームとチャネルの作成が完了したら、要求本文内のキーとキーを使用して、特定の時間 `createdDateTime` `from`  内メッセージの送信を開始できます。

#### <a name="request-post-message-that-is-text-only"></a>要求 (テキストのみの POST メッセージ)

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

#### <a name="request-post-a-message-with-inline-image"></a>要求 (インライン '画像' を含むメッセージを POST する)

> **注**: このシナリオでは要求は chatMessage に含まれます。そのため、特別なアクセス許可のスコープはありません。chatMessage のスコープもここに当てはまります。

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

メッセージの移行処理が完了すると、チームとチャネルの両方が移行モードから移行モードから移行モードから移行モードから移行モードから移行モードから移行モードで行  `completeMigration`  います。 この手順を実行すると、チームとチャネルのリソースがチーム メンバーが一般的に使用できるので開きます。 アクションはインスタンスにバインド `team` されます。

#### <a name="request-end-team-migration-mode"></a>要求 (チーム終了モード)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>応答

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>要求 (チャネル移行モードの終了)

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

* 指定されている、または `team` 存在しないアクション。 `channel` `migrationMode`

## <a name="step-five-add-team-members"></a>手順 5: チーム メンバーを追加する

Teams の UI または Microsoft Graph のメンバー追加 [API を使用して](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 、チーム [にメンバーを追加](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) できます。

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

* Teams のユーザーからメッセージをインポートできます。

* 要求が `completeMigration` 出された後に、チームにそれ以上のメッセージをインポートすることはできません。

* 要求が成功応答を返した後にのみ、チーム `completeMigration` メンバーは新しいチームに追加できます。

* 調整: メッセージはチャネルあたり 5 RPS でインポートされます。

* 移行結果を修正する必要がある場合は、チームを削除して手順を繰り返し、チームとチャネルを作成し、メッセージを再移行する必要があります。

> [!NOTE]
> 現在、インライン画像は、インポート メッセージ API スキーマでサポートされているメディアの種類のみをとしています。

##### <a name="import-content-scope"></a>コンテンツ範囲をインポートする

|スコープ内 | 現在の対象外|
|----------|--------------------------|
|チームおよびチャネル メッセージ|1 対 1 およびグループ チャット メッセージ|
|元のメッセージの作成日時|プライベート チャネル|
|メッセージの一部としてのインライン画像|メンション|
|SPO/OneDrive の既存のファイルへのリンク|Reactions|
|リッチ テキスト付きメッセージ|動画|
|メッセージ返信チェーン|お知らせ|
|高いスループット処理|コード スニペット|
||アダプティブ カード|
||ステッカー|
||Emojis|
||Quotes|
||チャネル間のクロス投稿|

> [!div class="nextstepaction"]
>[Microsoft Graph と Teams の統合に関する詳細情報](/graph/teams-concept-overview)
