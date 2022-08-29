---
title: コラボレーション コントロール アプリのタスク、会議、ファイルの仮想テーブル
author: surbhigupta
description: このモジュールでは、Microsoft Teams のコラボレーション コントロール アプリのタスク、会議、ファイルの仮想テーブルについて説明します。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 1913b379e9f24d36948a05190a4ae1804a8ec728
ms.sourcegitcommit: 442d2c8e80a2605b6d0215c973557471f18f8121
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2022
ms.locfileid: "67314596"
---
# <a name="virtual-tables-for-tasks-meetings-files"></a>タスク、会議、ファイルの仮想テーブル

このリリースの新しい機能は、一連の仮想テーブルです。 これにより、開発者は OData API を使用して Graph と対話できます。

コラボレーション コントロールのコア ソリューションには、コラボレーション コントロールによって作成されたデータへのプログラムによるアクセスに使用できる一連の [仮想テーブル](/power-apps/developer/data-platform/virtual-entities/get-started-ve)が含まれています。

> [!NOTE]
> 現在、コラボレーション コントロールは [、パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

> [!TIP]
> [仮想テーブル](/power-apps/developer/data-platform/virtual-entities/get-started-ve) は仮想エンティティとも呼ばれ、外部システムに存在するデータを、データのレプリケーションなしで、多くの場合はカスタム コーディングなしで、Microsoft Dataverse のテーブルとしてシームレスに表すことによって統合できます。

コラボレーション コントロールで使用される外部システムは Microsoft Graph です。 グループ 予定表イベント、予約予定、プランナー プランまたはタスク、SharePoint ドライブ、フォルダー、ファイル用の仮想テーブルがあります。

この記事では、Dataverse REST API を使用して仮想テーブルにアクセスして CRUD (作成、読み取り、更新、および削除) 操作を実行する方法を示すサンプルを提供します。

> [!TIP]
> Dataverse REST API の詳細については、 [Microsoft Dataverse Web API の使用に関するページを](/power-apps/developer/data-platform/webapi/overview)参照してください。

* 仮想テーブルは標準の Dataverse Web API を使用するため、仮想テーブルを使用してアプリケーションにデータを簡単に設定できます。
* 仮想テーブルでは、コラボレーション コントロールをサポートするために必要な複雑なワークフローが実装され、最適なパフォーマンスを得るために Microsoft データ センター内で実行されます。  
* 仮想テーブルでは、標準の Dataverse ログ機能と監視機能が使用されます。

コラボレーション コントロールをインストールした後、仮想テーブルは、依存できるアプリケーションの別のサービスとして扱うことができます。

:::image type="content" source="~/assets/images/collaboration-control/vt-overview.png" alt-text="仮想テーブルの概要":::

**前提条件**

この記事に従うには、次のものが必要です。

1. コラボレーション コントロールがインストールされている Dataverse 環境。
1. Dataverse 環境内のユーザー アカウント。 **これには、コラボレーション コントロールのユーザー** ロールが割り当てられています。
1. たとえば、サード パーティのツール: Microsoft Dataverse インスタンスに対して認証を行い、Web API 要求を作成して送信し、応答を表示できる、ユーザーまたはカスタム C# コードを投稿します。  

> [!TIP]
> Microsoft では、Dataverse インスタンスに接続し、Postman を使用して Web API で操作を実行する Postman 環境を構成する方法について説明します。 [Microsoft Dataverse Web API で Postman を使用する方法に関するページを](/power-apps/developer/data-platform/webapi/use-postman-web-api)参照してください。

## <a name="virtual-tables-sample-scenario"></a>仮想テーブルのサンプル シナリオ

このガイドで説明するシナリオでは、Planner プランとタスクの仮想テーブルを使用します。 説明されているシナリオは、タスク コラボレーション コントロールで使用されているものと同じです。 ユーザーの視点から見ると、シナリオは Planner プランと複数のタスクがどのように作成され、特定のビジネス レコードに関連付けられているかを示します。 このシナリオでは、ビジネス レコードに関連付けられているタスクを取得する方法と、特定のプランナー タスクを読み取り、更新、削除する方法を示します。

次のシーケンス図では、タスク コラボレーション コントロール、 [コラボレーション API](/rest/api/industry/collaboration-controls/) 、Planner プランおよびタスク仮想テーブルなど、クライアント間の相互作用について説明します。

:::image type="content" source="~/assets/images/collaboration-control/vt-sequence.png" alt-text="仮想テーブルのシーケンス図":::

## <a name="virtual-tables-basic-operations"></a>仮想テーブルの基本的な操作

このセクションでは、サンプル シナリオの各ステップの HTTP 要求と応答について説明します。

**タスク 1: グループ ID を取得する**

コラボレーションの設定で使用されるグループ ID [を取得します](~/samples/app-with-collaboration-controls.md#define-settings-for-your-collaboration)。

> [!NOTE]
> 後続のタスクでプランの作成に使用するユーザーは、このグループのメンバーである必要があります。 そうしないと、403 Forbidden 応答が返されます。

**タスク 2: コラボレーション セッションを開始する**

コラボレーション セッションはコラボレーション ルート テーブルのレコードです。これにより、タスク、イベント、予定などの複数のコラボレーションをビジネス レコードに関連付けることができます。

コラボレーション セッションでは、検査アプリケーションなど、ビジネス レコードに関連付けられている予定表イベントの一覧などの操作を実行できます。

# <a name="request"></a>[要求](#tab/request)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_begincollaborationsession  
```

```json
{
    "applicationName": "{{applicationName}}", 
    "collaborationRootEntityId": "{{collaborationRootEntityId}}", 
    "collaborationRootEntityName": "{{entityName}}" 
}
```

* `applicationName`: アプリケーションの一意の名前
* `collaborationRootEntityName`: ビジネス レコード エンティティの名前  
* `collaborationRootEntityId`: 特定のビジネス レコードの主キー (ID)

# <a name="response"></a>[Response](#tab/response)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.m365_begincollaborationsessionResponse", 
    "collaborationRootId": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
}
```

---

後続の `collaborationRootId` 要求で必要となるので、追跡します。

**タスク 3: Planner プランを作成する**

Planner プランを作成し、上記 `Group ID` で作成したコラボレーション セッションと `collaborationRootId`関連付けます。

# <a name="request"></a>[要求](#tab/request1)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannerplans  
```

```json

{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_owner": "{{groupId}}", 
    "m365_title": "{{planTitle}}" 
}

```

* `collaborationRootId`: このプランを関連付けるコラボレーション セッションを識別し、タスク 2 の値を使用します。

* `groupId`: このプランを所有するグループを識別し、手順 1 の値を使用します。

* `planTitle`: プランのタイトル

# <a name="response"></a>[Response](#tab/response1)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#m365_graphplannerplans/$entity", 
    "@odata.etag": "W/\"JzEtUGxhbiAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:33.1833561Z", 
    "m365_owner": "03614cef-8f5b-4265-9944-080d013c55d6", 
    "m365_title": "Multi-byte plan", 
    "m365_id": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannerplanid": "5c9c3ecf-f157-0f67-dcd9-733a77ad593e", 
    "m365_details": null 
} 

```

---

後続の`m365_id` 要求で必要となるので、追跡します。

**タスク 4: Planner タスクを作成する**

とを使用して Planner タスクを `PlanId` 作成します `collaborationRootId`。 複数の Planner タスクを作成し、前に作成したコラボレーション セッションに関連付けることができます。

# <a name="request"></a>[要求](#tab/request2)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json
{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
} 

```

* `collaborationRootId`: このプランを関連付けるコラボレーション セッションを識別し、タスク 2 の値を指定します。
* `planId`: このタスクが割り当てられるプランを識別し、前の手順の値を使用します。
* `taskTitle`: タスクのタイトル

# <a name="response"></a>[Response](#tab/response2)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488865579062167", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-16T16:58:47.571364+00:00\",\"orderHint\":\"8585488866179218449P`\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:47Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_hasdescription": false, 
    "m365_orderhint": "8585488865579062167", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Team-oriented discrete time-frame", 
    "m365_id": "8WSKWaEqAU-aZV4h9VUn0GUALXbH", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannertaskid": "0a2115b9-8b03-90ee-b450-42005d906ce8", 
    "m365_completedby": null, 
    "m365_details": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
} 

```

---

後続の `m365_graphplannertaskid` 要求で必要となるので、追跡します。

> [!NOTE]
> Planner `m365_graphplannertaskid` Task 仮想テーブル内のレコードの主キーです。 このレコードと対話するために仮想テーブルに対するすべての後続の要求では、この主キーを使用する必要があります。 これは、このドキュメントの以降の `plannerTaskId` 手順と呼ばれます。

この手順を繰り返して、プラン内に複数のタスクを作成する必要があります。

**タスク 5: 関連する Planner タスクを取得する**

以前に作成したコラボレーション セッションに `collaborationRootId` 関連付けられた関連付けられた Planner タスクを取得します。

# <a name="request"></a>[要求](#tab/request3)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

* `$filter`: $filter システム クエリを使用して、コラボレーション セッションに関連付けられているレコードを要求します (コラボレーション ルート レコードの ID を指定します)。
* `$select`: $select システム クエリ オプションを使用して、特定のプロパティを要求します。

# <a name="response"></a>[Response](#tab/response3)

```http
    HTTP/1.1 200 OK 
```

```json

{ 

    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks(m365_graphplannertaskid,m365_title,m365_createddatetime)", 
    "value": [ 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "8537731e-9414-1091-8d7d-ce5b74fc2477", 
            "m365_title": "Diverse executive core", 
            "m365_createddatetime": "2022-05-16T16:58:45Z", 
            "m365_id": "N_A2qmo3j0uvZZY1yd6V_GUADDEg", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "4a89895a-050e-9165-a6e4-19c3850f22ec", 
            "m365_title": "Cloned didactic open architecture", 
            "m365_createddatetime": "2022-05-16T16:58:41Z", 
            "m365_id": "--U0zbgsO0us084C0yCyEWUALbWw", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "20a08b8c-394b-b3fb-f9d1-47496df7a67b", 
            "m365_title": "Synergized zero defect interface", 
            "m365_createddatetime": "2022-05-16T16:58:43Z", 
            "m365_id": "AMn3RtbmV0m6cvkp5HKDCWUAKI0_", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        } 
    ] 
} 

```

---

後続の `m365_id‘s` 要求で ID が必要になるのを追跡します。

**タスク 6: Planner タスクを取得する**

先ほど作成したプランナー タスク `PlannerTaskID` の 1 つに対して読み取り操作を実行するために使用する Planner タスクを取得します。

# <a name="request"></a>[要求](#tab/request4)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})  
```

* `plannerTaskId`: Planner タスク レコードの主キーはプロパティです `m365_graphplannertaskid` 。

# <a name="response"></a>[Response](#tab/response4)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488204334528131", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-17T11:20:52.0247676+00:00\",\"orderHint\":\"8585488204934840644P2\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-17T11:20:52Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_orderhint": "8585488204334528131", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Secured content-based customer loyalty", 
    "m365_id": "SXmz1hxiOk-E3MKJUyhj0mUABvix", 
    "m365_details": "{\"@odata.context\":\"https://graph.microsoft.com/beta/$metadata#planner/tasks('SXmz1hxiOk-E3MKJUyhj0mUABvix')/details/$entity\",\"@odata.etag\":\"W/\\\"JzEtVGFza0RldGFpbHMgQEBAQEBAQEBAQEBAQEBARCc=\\\"\",\"description\":null,\"previewType\":\"automatic\",\"id\":\"SXmz1hxiOk-E3MKJUyhj0mUABvix\",\"references\":{},\"checklist\":{}}", 
    "m365_graphplannertaskid": "1b326015-bb43-945c-85bc-9b2a4ed16c73", 
    "m365_completedby": null, 
    "m365_hasdescription": null, 
    "m365_collaborationrootid": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
}

```

---

更新操作または削除操作を `@odata.etag` 実行するために必要なプロパティと`m365_graphplannertaskid` プロパティを追跡します。

**タスク 7: Planner タスクを更新する**

Planner タスクを更新して、前の手順で `PlannerTask ID` 作成したプランナー タスクの 1 つに対して更新操作を実行します。 Planner タスクを更新するには、次の要求を実行します。

# <a name="request"></a>[要求](#tab/request5)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* ヘッダー: If-Match: {{@odata.etag}}

```json

{
    "m365_title": "{{$planTitle}}" 
}   

```

* `@odata.etag`: タスクの Etag は、最新バージョンを取得するために読み取りを実行する必要があります。

* `planTitle`: タスクのタイトルを更新しました

# <a name="response"></a>[Response](#tab/response5)

```http
    HTTP/1.1 204 No Content 
```

---

**タスク 8: Planner タスクを削除する**

前の手順で `PlannerTask ID` 作成したプランナー タスクの 1 つに対して、削除操作を実行する Planner タスクを削除します。 Planner タスクを削除するには、次の要求を実行します。

# <a name="request"></a>[要求](#tab/request6)

```http
    HTTP/1.1 DELETE https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* `@odata.etag`: タスクの Etag は、最新バージョンを取得するために読み取りを実行する必要があります。

# <a name="response"></a>[Response](#tab/response6)

```http
    HTTP/1.1 204 No Content
```

---

**タスク 9: Planner タスクの詳細を更新する**

Planner タスクを更新して、前の手順で `PlannerTask ID` 作成したプランナー タスクの 1 つに対して更新操作を実行します。

# <a name="request"></a>[要求](#tab/request7)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

ヘッダー: If-Match: {{@odata.etag}}

```json

{ 

    "m365_title": "{{$planTitle}}", 
    "m365_details": "{\"@odata.etag\":\"{{details.etag}}\",\"description\":\"Updated Task Description\"}" 

}   
```

* `@odata.etag`: タスクの Etag は、最新バージョンを取得するために読み取りを実行する必要があります。
* `planTitle`: タスクのタイトルを更新しました。
* `@details.etag`: タスクの詳細については、クエリ $selectクエリ パラメーターを使用して読み取りを実行して、最新バージョンを取得する列を含める `m365_details` 必要があります。 この値は、応答の `m365_details` 列に含まれます。 Planner バックエンドではタスクとその詳細が個別に `@odata.etag` 格納されるため、この値は同じではありません。

# <a name="response"></a>[Response](#tab/response7)

```http
HTTP/1.1 204 No Content 
```

---

> [!NOTE]
> ヘッダーを `If-Match` '*' に設定すると、etag 値を指定する必要はありませんが、変更によってタスクが常に上書きされ、詳細が表示されます。

## <a name="virtual-tables-authorization"></a>仮想テーブルの承認

コラボレーション コントロール ソリューションの仮想テーブルを使用して HTTP 要求を行うために必要な承認手順を次に示します。

### <a name="azure-app-registration"></a>Azure アプリの登録

正しいベアラー トークンを取得するには、Azure でのアプリ登録が必要です。 アプリの登録の詳細については、「 [アプリの登録」を](/azure/active-directory/develop/quickstart-register-app)参照してください。

1. 認証するアプリの登録をAzure portalに作成します。
1. **[証明書&シークレット]** に移動します。
1. 新しいクライアント シークレットを作成します。

     > [!IMPORTANT]
     > シークレット値をコピーし、後で使用できるように格納してください。 現在のページを離れると、もう一度アクセスできなくなります。

1. **API アクセス許可** を参照します。
1. Dynamics CRM から委任されたアクセス許可 **user_impersonation** 追加します。
1. このアクセス許可に対する管理者の同意を付与します。

     :::image type="content" source="../assets/images/collaboration-control/power-automate-api-permission.png" alt-text="スクリーンショットは、Power Automate API のアクセス許可を示す例です":::

1. マニフェストに移動 **します**。
1. 次の属性の値を true に設定します。

   * oauth2AllowIdTokenImplicitFlow
   * oauth2AllowImplicitFlow

1. [保存] を選択します。

     :::image type="content" source="../assets/images/collaboration-control/power-automate-manifest.png" alt-text="スクリーンショットは、Power Automate マニフェストを示す例です":::

### <a name="powerapps-environment-permissions"></a>PowerApps 環境のアクセス許可

アプリの登録が設定されたら、PowerApps 環境でアプリケーション ユーザーを設定する必要があります。 これにより、前に構成した正しい Dynamics スコープを使用して認証できます。

1. [Power Platform 管理 センター](https://admin.powerplatform.microsoft.com/)を開きます。
1. [**環境** > **] Your_Environment** > **[ユーザー****アプリ ユーザー** > ] 一覧に移動します。
1. [ **新しいアプリ ユーザー** ] を選択し、Azure アプリの登録を選択します。
1. [ **セキュリティ ロールの編集]** を選択し、 **システム管理者** ロールをアプリ ユーザーに割り当てます。

   1. **システム管理者** ロールは、より低いセキュリティ ロールを持つすべてのユーザーの認証を許可するために適用されます。 たとえば、 **コラボレーションはユーザーを制御します**。
   1. これは、アプリケーションに低いロールを適用することで制限できます。 たとえば、 **コラボレーションは管理者を制御します**。

     :::image type="content" source="../assets/images/collaboration-control/power-automate-admin-center.png" alt-text="スクリーンショットは、Power Automate 管理センターを示す例です":::

### <a name="getting-the-bearer-token"></a>ベアラー トークンを取得する

Azure アプリの登録と PowerApps 環境のアクセス許可が完了したら、次の HTTP 要求を送信してベアラー トークンを取得します。

```http
POST https://login.microsoftonline.com/<AZURE_APP_TENANT_ID>/oauth2/token
```

* **Content-Type**: application/x-www-form-urlencoded
* **client_id**: <AZURE_APP_CLIENT_ID>
* **&client_secret**: <AZURE_APP_CLIENT_ID>
* **&リソース**: https://\<RESOURCEURL\>/
* **&ユーザー名**: \<USERNAME\>
* **&パスワード**: \<PASSWORD\>
* **&grant_type**: パスワード

> [!IMPORTANT]
> 必ず、リソース パラメーターに末尾のスラッシュを含めます。 そうでない場合は、仮想テーブルを呼び出すときに Graph スコープに関連するエラーが発生します。

応答ペイロードから、access_token プロパティの値 **を** コピーします。 その後、仮想テーブルに要求を行うときに、このベアラー トークンを承認ヘッダーの一部として渡すことができます。

:::image type="content" source="../assets/images/collaboration-control/power-automate-authorization.png" alt-text="スクリーンショットは、Power Automate 承認を示す例です":::

## <a name="virtual-tables-error-handling"></a>仮想テーブルのエラー処理

仮想テーブルのエラー処理では、一般的なエラー シナリオと仮想テーブルの応答方法について説明します。

### <a name="attempt-to-create-a-virtual-record-without-a-collaboration-session"></a>コラボレーション セッションなしで仮想レコードの作成を試みる

仮想レコードを作成するすべての要求には、有効なコラボレーション セッションが必要です。  仮想レコードが作成されると、仮想テーブルによってコラボレーション マップ レコードが作成されます。これには、仮想レコードの主キー、エンティティ名、および外部 ID である Graph リソース ID が含まれます。 このコラボレーション マップはコラボレーション セッションに関連付けられます。これは、コラボレーション コントロールがビジネス レコードに関連付けられているコラボレーションを追跡する方法です。

# <a name="request"></a>[要求](#tab/request8)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json

{ 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
}

```

プロパティが `collaborationRootId` 要求から欠落しています。

# <a name="response"></a>[Response](#tab/response8)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
    "error": { 
        "code": "0x80048d0b", 
        "message": "Parameter 'm365_collaborationrootid' is null, empty, or white-space." 
    } 
} 

```

---

この問題を解決するには、仮想レコードを作成するときに常に有効な `collaborationRootId` プロパティを指定する必要があります。

### <a name="attempt-to-read-a-virtual-record-without-a-collaboration-map"></a>コラボレーション マップなしで仮想レコードの読み取りを試みる

仮想テーブルを使用すると、仮想レコードのコレクションを返す要求を実行できます。 このドキュメントの前半では、特定のコラボレーション セッションに関連付けられているすべてのプランナー タスクを要求しました。 $filter=m365_planid eq`{{planId}}` のような$filterシステム クエリを使用して、特定の計画計画に関連付けられているすべてのプランナー タスクを要求することもできます。 このようなクエリを使用する場合に発生する問題の 1 つは、コラボレーション コントロールを使用する以外の方法で作成されたコラボレーション セッションに関連付けられていない Planner タスクに対してレコードが返されることです。 このようなレコードの読み取り、更新、または削除を試みると、仮想テーブルに関連付けられているコラボレーション マップが見つからないため、要求は失敗します。  

# <a name="request"></a>[要求](#tab/request9)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

この `plannerTaskId` プロパティは、Planner Web インターフェイスを使用して作成された Planner タスクに関連付けられているため、コラボレーション マップ レコードはありません。

# <a name="response"></a>[Response](#tab/response9)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "A record with the specified key values does not exist in m365_collaborationmap entity" 
    }
} 
```

---

この問題を解決するには、応答のエラー メッセージを確認する必要があります。このメッセージが上記のメッセージに設定されている場合は、仮想レコードが関連付けられていないことを意味します。 このレコードの関連付けを作成するには、 [Associate Collaboration Map - REST API](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/associate-collaboration-map) を呼び出す必要があります。

### <a name="attempt-to-read-a-virtual-record-and-the-graph-resource-has-been-deleted"></a>仮想レコードの読み取りを試み、Graph リソースが削除されました

前のエラーに関連して、Graph リソースが削除されたが、クライアントに削除された仮想レコードへの参照が残っている場合を処理する必要があります。 これは、別のユーザーがレコードを削除した場合に発生する可能性があります。 このようなレコードの読み取り、更新、または削除を試みると、仮想テーブルが Graph からリソースを取得できないため、要求は失敗します。

# <a name="request"></a>[要求](#tab/request10)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

プロパティは `plannerTaskId` 、削除された Planner タスクに関連付けられます。

# <a name="response"></a>[Response](#tab/response10)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "REST call failed because: Reason - NotFound, Full error - {\"error\":{\"code\":\"\",\"message\":\"The requested item is not found.\",\"innerError\":{\"date\":\"2022-05-17T16:30:51\",\"request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\",\"client-request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\"}}}." 
    } 
} 
```

---

このケースは、別のユーザーが関連付けられている Graph リソースをいつでも削除できるため、仮想レコードを取得するクライアント コードで処理する必要があります。

### <a name="attempt-to-update-a-virtual-record-with-an-invalid-odataetag"></a>無効な@odata.etag を使用して仮想レコードの更新を試みる

この `@odata.etag` プロパティは、データのコンカレンシーに使用され、別のユーザーによって更新された場合に、同じレコードの上書き書き込みを防止するために使用されます。 レコードが読み取られたとき、現在の etag が返され、レコードが変更されるまで有効なままになります。 etag は更新要求に含める必要があり、操作が完了する前に確認されます。 現在のユーザーがレコードを読み取った後に別のユーザーによってレコードが変更された場合、現在のユーザーの更新要求は失敗します。

同じ@odata.etag を使用して 2 つの更新要求を実行すると、2 番目の要求は失敗します。

# <a name="request"></a>[要求](#tab/request11)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

ヘッダー: If-Match: {{@odata.etag}}

```json
{
    "m365_title": "{{$planTitle}}" 
}

```

# <a name="response"></a>[Response](#tab/response11)

```http
    HTTP/1.1 409 Conflict 
```

```json
{ 
    "error": { 
        "code": "0x80048d08", 
        "message": "REST call failed because: Reason - Conflict, Full error - {\"error\":{\"code\":\"\",\"message\":\"The attempted changes conflicted with already accepted changes. Read the latest state and resolve differences.\",\"innerError\":{\"date\":\"2022-05-18T06:54:55\",\"request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\",\"client-request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\"}}}." 
    }
} 
```

---

### <a name="querying-for-associated-virtual-records"></a>関連付けられた仮想レコードのクエリ

上記のタスク 5 では、関連する Planner タスクを取得する方法について説明しました。 この操作は、すべての仮想テーブルでサポートされています。 この要求を実行するときは、次に示すようにコラボレーション ルート ID を指定するクエリを含める `$filter` 必要があります。

# <a name="request"></a>[要求](#tab/request12)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

---

* 他のフィルターオプションをこの `$filter` クエリと組み合わせることはできません。存在する場合は無視されます。
* その他のフィルター処理は、要求からの応答に対して直接実行する必要があります。

### <a name="querying-for-virtual-records-with-required-key-attributes"></a>必要なキー属性を使用した仮想レコードのクエリ

Dataverse Web API を呼び出して、次の仮想テーブルから複数のレコードを取得する場合は、必須のキー属性が必要です。 Graph Booking Appointments には、有効 `m365_bookingbusinessid` な情報がクエリに含まれている必要があります。 key 属性が指定されていない場合、要求は次のように失敗します。

# <a name="response"></a>[Response](#tab/response13)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
  "error": { 
    "code": "0x80048d0b", 
    "message": "Key attribute is missing: 'm365_bookingbusinessid'.", 
    ….
  } 
} 

```

---

この問題を解決するには、要求を次の形式に変更します。

# <a name="request"></a>[要求](#tab/request14)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphbookingappointments?$filter=m365_bookingbusinessid eq '{{bookingBusinessId}}'
```

---

### <a name="creating-virtual-records-and-graph-access-control"></a>仮想レコードと Graph アクセス制御の作成

仮想テーブルは、Microsoft Graph に指定されたアクセス制御に従います。 仮想テーブルでは、ユーザーが Microsoft Graph APIを使用して実行できなかった操作は許可されません。 たとえば、プランの作成に使用するユーザーがタスク 3 であり、使用するグループのメンバーでない場合、403 個の禁止された応答が返されます。
