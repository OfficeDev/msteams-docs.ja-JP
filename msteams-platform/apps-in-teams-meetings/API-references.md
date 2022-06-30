---
title: 会議アプリ API リファレンス
author: surbhigupta
description: 例とコード サンプルを使用して会議アプリ API 参照を識別する方法について説明します。Teams アプリ会議ユーザー ロール API ユーザー コンテキスト通知シグナル クエリ。
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
ms.openlocfilehash: ba0f3758cf08649100cbc564c60eab3a86e3d155
ms.sourcegitcommit: 779aa3220f6448a9dbbaea57e667ad95b5c39a2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66561610"
---
# <a name="meeting-apps-api-references"></a>会議アプリ API リファレンス

会議の拡張性では、会議のエクスペリエンスを向上させるための API が提供されます。 掲載されている API のヘルプを使用すると、次のことを実行できます。

* 会議のライフサイクル内でアプリをビルドしたり、既存のアプリを統合したりする。
* API を使用して、アプリに会議を認識させる。
* 会議のエクスペリエンスを向上させるために必要な API を選択する。

> [!NOTE]
> 会議のサイド パネルで SSO を動作させるには、Teams [JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) (*バージョン*: 1.10 以降) を使用します。

次の表に、Microsoft Teams クライアント (MSTC) および Microsoft Bot Framework (MSBF) SDK で使用可能な API の一覧を示します。

|メソッド| 説明| ソース|
|---|---|----|
|[**ユーザー コンテキストを取得する**](#get-user-context-api)| コンテキスト情報を取得して、関連するコンテンツを Microsoft Teams タブに表示します。| [MSTC SDK](/microsoftteams/platform/tabs/how-to/access-teams-context#get-context-by-using-the-microsoft-teams-javascript-library) |
|[**参加者を取得する**](#get-participant-api)| 会議 ID と参加者 ID によって参加者情報を取得します。 | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetingparticipantasync?view=botbuilder-dotnet-stable&preserve-view=true)
|[**会議中の通知を送信する**](#send-an-in-meeting-notification)| ユーザー ボット チャット用の既存の会話通知 API を使用して会議のシグナルを提供し、会議中の通知を示すユーザー アクションを通知できます。 | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityextensions.teamsnotifyuser?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**会議の詳細を取得する**](#get-meeting-details-api)| 会議の静的メタデータを取得します。 | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetinginfoasync?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**リアルタイム キャプションを送信する**](#send-real-time-captions-api)| 進行中の会議にリアルタイム キャプションを送信します。 | [MSTC SDK](/azure/cognitive-services/speech-service/speech-sdk?tabs=nodejs%2Cubuntu%2Cios-xcode%2Cmac-xcode%2Candroid-studio#get-the-speech-sdk&preserve-view=true) |
|[**アプリ コンテンツをステージに共有する**](#share-app-content-to-stage-api)| 会議でアプリのサイド パネルからアプリの特定の部分を会議ステージに対して共有します。 | [MSTC SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |
|[**アプリ コンテンツ ステージの共有状態を取得する**](#get-app-content-stage-sharing-state-api)| 会議ステージでアプリの共有状態に関する情報を取得します。 | [MSTC SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting.iappcontentstagesharingstate?view=msteams-client-js-latest&preserve-view=true) |
|[**アプリ コンテンツ ステージの共有機能を取得する**](#get-app-content-stage-sharing-capabilities-api)| 共有のためのアプリの機能を会議ステージに取得します。 | [MSTC SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting.iappcontentstagesharingcapabilities?view=msteams-client-js-latest&preserve-view=true) |
|[**リアルタイムの Teams 会議イベントを取得する**](#get-real-time-teams-meeting-events-api)|実際の開始時刻や終了時刻など、リアルタイムの会議イベントを取得します。| [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable&preserve-view=true) |

## <a name="get-user-context-api"></a>ユーザー コンテキストを取得する API 

タブ コンテンツのコンテキスト情報を識別して取得するには、[Teams タブのコンテキストを取得する方法](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)に関するページを参照してください。`meetingId` は、会議コンテキストで実行されているタブによって使用され、応答ペイロードに追加されます。

## <a name="get-participant-api"></a>参加者を取得する API

`GetParticipant` API には、認証トークンを生成するために、ボットの登録と ID が必要です。 詳細については、[ボットの登録と ID](../build-your-first-app/build-bot.md) に関するページを参照してください。

> [!NOTE]
>
> * 会議の開催者はいつでもロールを変更できるため、参加者のロールをキャッシュしないでください。
> * 現在、`GetParticipant` API は、参加者が 350 人未満の配布リストまたは名簿でのみサポートされています。

### <a name="query-parameters"></a>クエリ パラメーター

> [!TIP]
> 参加者 ID とテナント ID は、[タブの SSO 認証](../tabs/how-to/authentication/tab-sso-overview.md)から取得します。

`Meeting` API には、URL パラメーターとして `meetingId`、`participantId`、`tenantId` が必要です。 これらのパラメーターは、Teams クライアント SDK とボット アクティビティの一部として使用できます。

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、Bot Invoke および Teams クライアント SDK を通して入手できます。|
|**participantId**| String | はい | 参加者 ID はユーザー ID です。 タブ SSO、Bot Invoke、および Teams クライアント SDK で入手できます。 タブ SSO から参加者 ID を取得することをお勧めします。 |
|**tenantId**| String | はい | テナント ユーザーにはテナント ID が必要です。 タブ SSO、Bot Invoke、および Teams クライアント SDK で入手できます。 タブ SSO からテナント ID を取得することをお勧めします。 |

### <a name="example"></a>例

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = await TeamsInfo.GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourParticipantTenantId").ConfigureAwait(false);
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "conversationType": "groupChat", 
      "isGroup":true
   }
}
```

---

| プロパティ名 | 用途 |
|---|---|
| **user.id** | ユーザーの ID。 |
| **user.aadObjectId** | ユーザーの Azure Active Directory オブジェクト ID。 |
| **user.name** | ユーザーの名前 |
| **user.givenName** | ユーザーの名。|
| **user.surname** | ユーザーの姓。 |
| **user.email** | ユーザーのメール ID。 |
| **user.userPrincipalName** | ユーザーの UPN。 |
| **user.tenantId** | Azure Active Directory テナント ID。 |
| **user.userRole** | ユーザーのロール (例: 'admin' または 'user')。 |
| **meeting.role** | 会議の参加者の役割。 例: 'Organizer' または 'Presenter' または 'Attendee'。 |
| **meeting.inMeeting** | 参加者が会議に参加しているかどうかを示す値。 |
| **conversation.id** | 会議チャット ID。 |
| **conversation.isGroup** | 会話に 2 人以上の参加者があるかどうかを示すブール値。 |

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **403** | 参加者情報の取得がアプリと共有されていません。 アプリが会議にインストールされていない場合は、エラー応答 403 がトリガーされます。 ライブ サイト移行中にテナント管理者がアプリを無効化またはブロックすると、エラー応答 403 がトリガーされます。 |
| **200** | 参加者の情報が正常に取得されました。|
| **401** | アプリは無効なトークンで応答しました。|
| **404** | 会議の有効期限が切れているか、参加者が利用できません。|

## <a name="send-an-in-meeting-notification"></a>会議中の通知を送信する

会議のすべてのユーザーは、会議中の通知のペイロードを通して送信された通知を受け取ります。 会議中の通知のペイロードは、会議中の通知をトリガーし、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議シグナルを提供することができます。 ユーザーの操作に基づいて、会議中の通知を送信できます。 ペイロードは Bot Service を通して入手できます。

> [!NOTE]
>
> * 会議中の通知が呼び出されると、コンテンツはチャット メッセージとして提示されます。
> * 現在、対象を指定した通知の送信と、Web アプリのサポートはサポートされていません。
> * ユーザーが Web ビューでアクションを実行した後に自動的に閉じるには、[submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) 関数を呼び出す必要があります。 これは、アプリの申請の要件です。 詳細については、[Teams SDK のタスク モジュール](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)をご覧ください。
> * アプリで匿名ユーザーをサポートする場合は、最初の呼び出し要求ペイロードが、`from.aadObjectId` 要求メタデータではなく、`from` オブジェクトの `from.id` 要求メタデータに依存している必要があります。 `from.id` はユーザー ID であり、`from.aadObjectId` はユーザーの Microsoft Azure Active Directory (Azure AD) ID です。 詳細については、「[タブでタスク モジュールを使用する](../task-modules-and-cards/task-modules/task-modules-tabs.md)」と「[タスク モジュールの作成と送信](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)」をご覧ください。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| String | はい | 会話識別子は Bot Invoke の一部として入手できます。 |

### <a name="examples"></a>例

`Bot ID` はマニフェスト内で宣言され、ボットは結果オブジェクトを受け取ります。

> [!NOTE]
>
> * 要求されたペイロードの例では、`externalResourceUrl` の `completionBotId` パラメーターは省略可能です。
> * `externalResourceUrl` の幅と高さのパラメーターは、ピクセル単位にする必要があります。 詳細については、[デザイン ガイドライン](design/designing-apps-in-meetings.md)のページをご覧ください。
> * URL は、会議中の通知に `<iframe>` として読み込まれるページです。 ドメインは、アプリのマニフェストでアプリの `validDomains` 配列に含まれている必要があります。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

# <a name="json"></a>[JSON](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities
```

```json

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

---

| プロパティ名 | 用途 |
|---|---|
| **type** | 動作状況の種類。 |
| **text** | メッセージのテキスト コンテンツ。 |
| **summary** | メッセージの概要テキスト。 |
| **channelData.notification.alertInMeeting** | 会議中に通知をユーザーに表示するかどうかを示すブール値。 |
| **channelData.notification.externalResourceUrl** | 通知の外部リソース URL の値。|
| **replyToId** | スレッドの親メッセージまたはルート メッセージの ID。 |

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **201** | シグナルを含むアクティビティが正常に送信されました。 |
| **401** | アプリは無効なトークンで応答しました。 |
| **403** | アプリがシグナルを送信できません。 403 応答コードは、ライブ サイト移行中にテナント管理者がアプリを無効にしてブロックするなど、さまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれています。 |
| **404** | 会議チャットが存在しません。 |

## <a name="get-meeting-details-api"></a>会議の詳細を取得する API

会議の詳細 API を使用すると、アプリで会議の静的メタデータを取得できます。 このメタデータは、動的には変更されないデータ ポイントを提供します。 この API は、Bot Service を通して利用できます。 現在、プライベートのスケジュールされた会議と定期的な会議、チャネルのスケジュールされた会議と定期的な会議の両方で、それぞれ異なる RSC アクセス許可を使用した API がサポートされています。

`Meeting Details` API には、ボットの登録とボット ID が必要です。 Bot SDK で `TurnContext` を取得する必要があります。 会議の詳細 API を使用するには、プライベート会議やチャネル会議など、会議の範囲に基づいて異なる RSC アクセス許可を取得する必要があります。

### <a name="prerequisite"></a>前提条件

会議の詳細 API を使用するには、プライベート会議やチャネル会議など、会議の範囲に基づいて異なる RSC アクセス許可を取得する必要があります。

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 以降の場合</b></summary>

次の例では、プライベート会議についてアプリ マニフェストの `webApplicationInfo` および `authorization` プロパティを構成します。

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]
    }
}
 ```

次の例では、チャネル会議についてアプリ マニフェストの `webApplicationInfo` および `authorization` プロパティを構成します。

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChannelMeeting.ReadBasic.Group",
                "type": "Application"
            }
        ]
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.11 以前の場合</b></summary>

次の例では、プライベート会議についてアプリ マニフェストの `webApplicationInfo` プロパティを構成します。

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

次の例では、チャネル会議についてアプリ マニフェストの `webApplicationInfo` プロパティを構成します。

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "ChannelMeeting.ReadBasic.Group"
    ]
}
 ```

<br>

</details>

> [!NOTE]
>
> * ボットは、RSC アクセス許可のマニフェストに `ChannelMeeting.ReadBasic.Group` を追加することで、すべてのチャネルで作成されたすべての会議から会議の開始イベントまたは終了イベントを自動的に受信できます。
>
> * 1 対 1 の通話 `organizer` の場合はチャットのイニシエーターであり、グループ通話の場合 `organizer` は通話イニシエーターです。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、Bot Invoke および Teams クライアント SDK を通して入手できます。 |

### <a name="example"></a>例

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

Not available

```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

Meeting Details API の JSON 応答本文は次のとおりです。

* **スケジュールされた会議:**

    ```json

    {
       "details":  { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "Scheduled" 
         },
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
             }, 
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    } 
    ```

* **1 対 1 の呼び出し:**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "OneToOneCall"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer  ": {
             "id": "<organizer user ID>",
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **グループ呼び出し:**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "GroupCall",
             "joinUrl": "https://teams.microsoft.com/l/xx"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer": {
             "id": "<organizer user ID>",
             "objectId": "<organizer object ID>",
             "aadObjectId": "<AAD object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **インスタント会議:**

    ```json
    { 
       "details": { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "MeetNow" 
         }, 
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
         },
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>", 
             "tenantId": "<Tenant ID>" ,
             "objectId": "<organizer object ID>"
         }
    }
    
    ```

---

| プロパティ名 | 用途 |
|---|---|
| **details.id** | BASE64 文字列としてエンコードされた会議の ID。 |
| **details.msGraphResourceId** | MS Graph API呼び出しに特に使用される MsGraphResourceId。 |
| **details.scheduledStartTime** | 会議のスケジュールされた開始時刻 (UTC)。 |
| **details.scheduledEndTime** | 会議のスケジュールされた終了時刻 (UTC)。 |
| **details.joinUrl** | 会議に参加するために使用される URL。 |
| **details.title** | 会議のタイトル。 |
| **details.type** | 会議の種類 ( GroupCall、OneToOneCall、Adhoc、Broadcast、MeetNow、定期的、スケジュール、不明など)。 |
| **conversation.isGroup** | 会話に 2 人以上の参加者があるかどうかを示すブール値。 |
| **conversation.conversationType** | 会話の種類。 |
| **conversation.id** | 会議チャット ID。 |
| **organizer.id** | 開催者のユーザー ID。 |
| **organizer.aadObjectId** | 開催者の Azure Active Directory オブジェクト ID。 |
| **organizer.tenantId** | 開催者の Azure Active Directory テナント ID。 |

定期的な会議の種類の場合は、

**startDate**: パターンの適用を開始する日付を指定します。 startDate の値は、イベント リソースの start プロパティの日付値に対応している必要があります。 パターンと一致しない場合、会議の最初の回はこの日付には発生しないことにご注意ください。

**endDate**: パターンの適用を停止する日付を指定します。 パターンと一致しない場合、会議の最後の回はこの日付には発生しないことにご注意ください。

## <a name="send-real-time-captions-api"></a>リアルタイム キャプション API を送信する

送信リアルタイム キャプション API は、Teams コミュニケーション アクセスリアルタイム翻訳 (CART) のキャプション、人間型のクローズド キャプションの POST エンドポイントを公開します。 このエンドポイントに送信されたテキスト コンテンツは、キャプションが有効になっている Teams 会議のエンド ユーザーに表示されます。

### <a name="cart-url"></a>CART URL

POST エンドポイントの CART URL は、Teams **会議の [会議オプション** ] ページから取得できます。 詳細については、「[Microsoft Teams 会議での CART キャプション](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47)」をご覧ください。 CART キャプションを使用するために CART URL を変更する必要はありません。

#### <a name="query-parameter"></a>クエリ パラメーター

CART URL には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|----|
|**meetingId**| String | はい |会議識別子は、Bot Invoke および Teams クライアント SDK を通して入手できます。 <br/>例: meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**token**| String | はい |認可トークン。<br/> 例: token=04751eac |

#### <a name="example"></a>例

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>メソッド

|Resource|メソッド|説明|
|----|----|----|
|/cartcaption|POST|開始された会議のキャプションを処理します|

> [!NOTE]
> すべての要求のコンテンツ タイプが UTF-8 エンコードのプレーンテキストであることを確認してください。 要求の本文には、キャプションのみが含まれます。

#### <a name="example"></a>例

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> POST 要求ごとに、キャプションの新しい行が生成されます。エンド ユーザーがコンテンツを読む十分な時間を確保するために、各 POST 要求本文を 80 から 120 文字に制限します。

### <a name="error-codes"></a>エラー コード

次の表に、エラー コードを示します。

|エラー コード|説明|
|---|---|
| **400** | 要求が正しくありません。 応答本文に、詳細な情報があります。 たとえば、必要なパラメーターの一部が提示されていません。|
| **401** | 承認されていません。不適切な/期限切れのトークンです。このエラーが発生した場合は、Teams で新しい CART URL を生成してください。 |
| **404** | 会議が見つからないか、開始されていません。 このエラーが発生した場合は、会議を開始してキャプションの開始を選択したことを確認してください。 会議でキャプションを有効にした後、会議へのキャプションの POST を開始できます。|
| **500** |内部サーバー エラーです。詳細については、「[サポートにお問い合わせいただくかフィードバックをお寄せください](../feedback.md)」を参照してください。|

## <a name="share-app-content-to-stage-api"></a>アプリ コンテンツをステージに共有する API

`shareAppContentToStage` API を使用すると、アプリの特定の部分を会議ステージに対して共有できます。 この API は、Teams クライアント SDK を通して使用できます。

### <a name="prerequisite"></a>前提条件

* `shareAppContentToStage` API を使用するには、RSC アクセス許可を取得する必要があります。 アプリ マニフェストで、`authorization` プロパティと、`resourceSpecific` フィールドの `name` および `type` を構成します。 次に例を示します。

    ```json
    "authorization": {
        "permissions": { 
        "resourceSpecific": [
        { 
        "name": "MeetingStage.Write.Chat",
        "type": "Delegated"
        }
        ]
    }
    }
    ```

* `appContentUrl` は、manifest.json 内の `validDomains` 配列で許可されている必要があります。それ以外の場合、API は 501 を返します。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれています。 *エラー* には、エラーの種類 *SdkError* が含まれるか、共有が成功した場合は null が含まれます。 *結果* には、共有が成功した場合は true の値が含まれ、共有が失敗した場合は null が含まれます。|
|**appContentURL**| String | はい | ステージ上で共有される URL。|

### <a name="example"></a>例

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **501** | API は現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="get-app-content-stage-sharing-state-api"></a>アプリ コンテンツ ステージの共有状態を取得する API

`getAppContentStageSharingState` API を使用すると、会議ステージでのアプリの共有に関する情報を取得できます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれています。 *エラー* には、エラーの場合はエラーの種類 *SdkError* が含まれ、共有が成功した場合は null が含まれます。 *結果* には、取得に成功したことを示す `AppContentStageSharingState` オブジェクトが含まれるか、取得に失敗したことを示す null が含まれます。|

### <a name="example"></a>例

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

`getAppContentStageSharingState` API の JSON 応答本文は次のとおりです。

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **501** | API は現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>アプリ コンテンツ ステージの共有機能を取得する API

`getAppContentStageSharingCapabilities` API を使用すると、会議ステージに対して共有するためのアプリの機能を取得できます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれています。 *エラー* には、エラーの種類 *SdkError* が含まれるか、共有が成功した場合は null が含まれます。 結果には、取得に成功したことを示す `AppContentStageSharingState` オブジェクトが含まれるか、取得に失敗したことを示す null が含まれます。|

### <a name="example"></a>例

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

`getAppContentStageSharingCapabilities` API の JSON 応答本文は次のとおりです。

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **1000** | アプリには、共有のステージングを許可するアクセス許可がありません。|

## <a name="get-real-time-teams-meeting-events-api"></a>リアルタイムの Teams 会議イベントを取得する API

> [!NOTE]
> リアルタイム Teams 会議イベントは、スケジュールされた会議でのみサポートされます。

ユーザーはリアルタイムの会議イベントを受信できます。 アプリが会議に関連付けられるとすぐに、実際の会議の開始時刻と終了時刻がボットと共有されます。 会議の実際の開始時刻と終了時刻は、スケジュールされた開始時刻と終了時刻とは異なります。 会議の詳細 API は、スケジュールされた開始時刻と終了時刻を提供します。 イベントは、実際の開始時刻と終了時刻を提供します。

Bot SDK を通して使用できる `TurnContext` オブジェクトに精通している必要があります。 `TurnContext` 内の `Activity` オブジェクトには、実際の開始時刻と終了時刻が入ったペイロードが含まれています。 リアルタイム会議イベントには、Teams プラットフォームからの登録されたボット ID が必要です。 ボットは、マニフェストに `ChannelMeeting.ReadBasic.Group` を追加することで、会議の開始イベントまたは終了イベントを自動的に受信できます。

### <a name="prerequisite"></a>前提条件

アプリ マニフェストには、会議の開始イベントと終了イベントを受信するための `webApplicationInfo` プロパティが必要です。 マニフェストを構成するには、次の例を使用します。

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 以降の場合</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]    
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.11 以前の場合</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

<br>

</details>

### <a name="example-of-getting-meetingstartendeventvalue"></a>`MeetingStartEndEventvalue` を取得する例

ボットは `OnEventActivityAsync` ハンドラーを通してイベントを受け取ります。 JSON ペイロードを逆シリアル化するために、会議のメタデータを取得するモデル オブジェクトが導入されます。 会議のメタデータは、イベント ペイロード内の `value` プロパティにあります。 `MeetingStartEndEventvalue` モデル オブジェクトが作成され、そのメンバー変数はイベント ペイロード内の `value` プロパティの下のキーに対応します。

> [!NOTE]
>
> * 会議 ID は `turnContext.ChannelData` から取得します。
> * 会話 ID は会議 ID として使用しないでください。
> * 会議イベント ペイロード `turncontext.activity.value` からの会議 ID は使用しないでください。

次のコードは、会議の開始および終了イベントから、会議のメタデータである `MeetingType`、`Title`、`Id`、`JoinUrl`、`StartTime`、`EndTime` をキャプチャする方法を示しています。

会議の開始イベント

```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingStartEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

会議の終了イベント

```csharp
protected override async Task OnTeamsMeetingEndAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

### <a name="example-of-meeting-start-event-payload"></a>会議の開始イベントのペイロードの例

次のコードは、会議の開始イベントのペイロードの例を示しています。

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id": "meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a>会議の終了イベントのペイロードの例

次のコードは、会議の終了イベントのペイロードの例を示しています。

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

| プロパティ名 | 用途 |
|---|---|
| **name** | ユーザーの名前|
| **type** | アクティビティの種類。 |
| **timestamp** | ISO-8601 形式で表されるメッセージのローカル日付と時刻。 |
| **id** | アクティビティの ID。 |
| **channelId** | このアクティビティが関連付けられているチャネル。 |
| **serviceUrl** | このアクティビティへの応答を送信する必要があるサービス URL。 |
| **from.id** | 要求を送信したユーザーの ID。 |
| **from.aadObjectId** | 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
| **conversation.isGroup** | 会話に 2 人以上の参加者があるかどうかを示すブール値。 |
| **conversation.tenantId** | 会話または会議の Azure Active Directory テナント ID。 |
| **conversation.id** | 会議チャット ID。 |
| **recipient.id** | 要求を受け取るユーザーの ID。 |
| **recipient.name** | 要求を受け取るユーザーの名前。 |
| **entityes.locale** | ロケールに関するメタデータを含むエンティティ。 |
| **entityes.country** | 国に関するメタデータを含むエンティティ。 |
| **entities.type** | クライアントに関するメタデータを含むエンティティ。 |
| **channelData.tenant.id** | Azure Active Directory テナント ID。 |
| **channelData.source** | イベントが発生または呼び出されたソース名。 |
| **channelData.meeting.id** | 会議に関連付けられている既定の ID。 |
| **値。MeetingType** | 会議の種類。 |
| **値。タイトル** | 会議の件名。 |
| **値。Id** | 会議に関連付けられている既定の ID。 |
| **値。JoinUrl** | 会議の参加 URL。 |
| **値。Starttime** | 会議の開始時刻 (UTC)。 |
| **値。Endtime** | 会議の終了時刻 (UTC)。 |
| **locale**| クライアントによって設定されたメッセージのロケール。 |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| 会議の拡張性 | トークンを渡すための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会議コンテンツ バブル ボット | 会議でコンテンツ バブル ボットと対話するための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| 会議 meetingSidePanel | サイド パネルの会議内で対話するための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| 会議の [詳細] タブ | 会議内の [詳細] タブと対話するための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|会議イベントのサンプル|リアルタイムの Teams 会議イベントを示すサンプル アプリ|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|採用会議のサンプル|採用シナリオの会議エクスペリエンスを示すサンプル アプリ。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|QR コードを使用したアプリのインストール|QR コードを生成し、QR コードを使用してアプリをインストールするサンプル アプリ|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>関連項目

* [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会議用アプリ](teams-apps-in-meetings.md)
* [Live Share SDK](teams-live-share-overview.md)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Teams 会議用アプリを有効化して構成する](enable-and-configure-your-app-for-teams-meetings.md)
