---
title: 会議アプリ API
author: v-sdhakshina
description: この記事では、Teams クライアントと Bot Framework SDK で使用できる会議アプリの API リファレンスについて、例、コード サンプル、応答コードについて説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: f3d44317dbc8ea317e8fe3c5bdeb19404df75265
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789864"
---
# <a name="meeting-apps-apis"></a>会議アプリ API

会議機能拡張は、会議エクスペリエンスを強化するための API を提供します。 掲載されている API のヘルプを使用すると、次のことを実行できます。

* 会議のライフサイクル内でアプリをビルドしたり、既存のアプリを統合したりする。
* API を使用して、アプリに会議を認識させる。
* 会議のエクスペリエンスを向上させるために必要な API を選択する。

> [!NOTE]
> 会議のサイド パネルで SSO を動作させるには、Teams [JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) (*バージョン*: 1.10 以降) を使用します。

次の表に、Microsoft Teams JavaScript ライブラリとMicrosoft Bot Framework SDK で使用できる API の一覧を示します。

|メソッド| 説明| ソース|
|---|---|----|
|[**ユーザー コンテキストを取得する**](#get-user-context-api)| コンテキスト情報を取得して、Microsoft Teams タブに関連するコンテンツを表示します。| [Microsoft Teams JavaScript ライブラリ SDK](/microsoftteams/platform/tabs/how-to/access-teams-context#get-context-by-using-the-microsoft-teams-javascript-library) |
|[**参加者を取得する**](#get-participant-api)| 会議 ID と参加者 ID によって参加者情報を取得します。 | [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetingparticipantasync?view=botbuilder-dotnet-stable&preserve-view=true)
|[**会議中の通知を送信する**](#send-an-in-meeting-notification)| ユーザー ボット チャット用の既存の会話通知 API を使用して会議のシグナルを提供し、会議中の通知を示すユーザー アクションを通知できます。 | [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityextensions.teamsnotifyuser?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**会議の詳細を取得する**](#get-meeting-details-api)| 会議の静的メタデータを取得します。 | [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetinginfoasync?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**リアルタイム キャプションを送信する**](#send-real-time-captions-api)| 進行中の会議にリアルタイム キャプションを送信します。 | [Microsoft Teams JavaScript ライブラリ SDK](/azure/cognitive-services/speech-service/speech-sdk?tabs=nodejs%2Cubuntu%2Cios-xcode%2Cmac-xcode%2Candroid-studio#get-the-speech-sdk&preserve-view=true) |
|[**アプリ コンテンツをステージに共有する**](build-apps-for-teams-meeting-stage.md#share-app-content-to-stage-api)| 会議でアプリのサイド パネルからアプリの特定の部分を会議ステージに対して共有します。 | [Microsoft Teams JavaScript ライブラリ SDK](/javascript/api/@microsoft/teams-js/meeting) |
|[**リアルタイムの Teams 会議イベントを取得する**](#get-real-time-teams-meeting-events-api)|実際の開始時刻や終了時刻など、リアルタイムの会議イベントを取得します。| [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable&preserve-view=true) |
| [**受信オーディオの状態を取得する**](#get-incoming-audio-state) | アプリが会議ユーザーの受信オーディオ状態設定を取得できるようにします。| [Microsoft Teams JavaScript ライブラリ SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |
| [**受信オーディオを切り替える**](#toggle-incoming-audio) | アプリで会議ユーザーの受信オーディオ状態設定をミュートからミュート解除、またはその逆に切り替えることができます。| [Microsoft Teams JavaScript ライブラリ SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |

## <a name="get-user-context-api"></a>ユーザー コンテキストを取得する API 

タブ コンテンツのコンテキスト情報を識別して取得するには、[Teams タブのコンテキストを取得する方法](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)に関するページを参照してください。`meetingId` は、会議コンテキストで実行されているタブによって使用され、応答ペイロードに追加されます。

## <a name="get-participant-api"></a>参加者を取得する API

`GetParticipant` API には、認証トークンを生成するために、ボットの登録と ID が必要です。 詳細については、[ボットの登録と ID](../build-your-first-app/build-bot.md) に関するページを参照してください。

> [!NOTE]
>
> * ユーザーの種類は **getParticipantRole** API に含まれていません。
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

| プロパティ名 | 説明 |
|---|---|
| **user.id** | ユーザーの ID。 |
| **user.aadObjectId** | ユーザーの Azure Active Directory オブジェクト ID。 |
| **user.name** | ユーザーの名前 |
| **user.givenName** | ユーザーの名。|
| **user.surname** | ユーザーの姓。 |
| **user.email** | ユーザーのメール ID。 |
| **user.userPrincipalName** | ユーザーの UPN。 |
| **user.tenantId** | Azure Active Directory テナント ID。 |
| **user.userRole** | ユーザーのロール。 たとえば、'admin' や 'user' などです。 |
| **meeting.role** | 会議での参加者の役割。 たとえば、"開催者" や "発表者" や "出席者" などです。 |
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
| **404** | 会議の有効期限が切れているか、参加者が使用できません。|

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
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&<completionBotId>=<BOT_APP_ID>"
        }
    },
    "replyToId": "1493070356924"
}
```

---

| プロパティ名 | 説明 |
|---|---|
| **type** | 動作状況の種類。 |
| **text** | メッセージのテキスト コンテンツ。 |
| **summary** | メッセージの概要テキスト。 |
| **channelData.notification.alertInMeeting** | 会議中に通知をユーザーに表示するかどうかを示すブール値。 |
| **channelData.notification.externalResourceUrl** | 通知の外部リソース URL の値。|
| **replyToId** | スレッドの親メッセージまたはルート メッセージの ID。 |
| **APP_ID** | マニフェストで宣言されたアプリ ID。 |
| **completionBotId** | ボット アプリ ID |

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
> * 1 対 1 の呼び出し `organizer` の場合はチャットの発信側であり、グループ呼び出しの場合は呼び出 `organizer` しのイニシエーターです。 パブリック チャネル会議 `organizer` の場合は、チャネル投稿を作成したユーザーです。

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

* **スケジュールされたチャネル会議:**

    ```json
    { 
        "details": { 
        "msGraphResourceId": "MSoxNmUwYjdiYi05M2Q1LTQzNTItOTllMC0yM2VlNWYyZmZmZTIqMTY2MDc1ODYwNzc0MCoqMTk6a0RtQkpEWFZsYWl0QWhHcVB2SzBtRExZbHVTWnJub01WX1MxeFNkTjQxNDFAdGhyZWFkLnRhY3Yy", 
        "scheduledStartTime": "2022-08-17T18:00:00Z", 
        "scheduledEndTime": "2022-08-17T18:30:00Z", 
        "type": "ChannelScheduled", 
        "id": "MCMxOTprRG1CSkRYVmxhaXRBaEdxUHZLMG1ETFlsdVNacm5vTVZfUzF4U2RONDE0MUB0aHJlYWQudGFjdjIjMTY2MDc1ODYwNzc0MA==", 
        "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3akDmBJDXVlaitAhGqPvK0mDLYluSZrnoMV_S1xSdN4141%40thread.tacv2/1660758607740?context=%7b%22Tid%22%3a%229f044231-b634-4bdd-b29d-2776e3dbd699%22%2c%22Oid%22%3a%2216e0b7bb-93d5-4352-99e0-23ee5f2fffe2%22%7d", 
        "title": "Test channel meeting"
    }, 
    "conversation": { 
        "isGroup": true, 
        "conversationType": "channel", 
        "id": "19:kDmBJDXVlaitAhGqPvK0mDLYluSZrnoMV_S1xSdN4141@thread.tacv2;messageid=1660758607740"
    }, 
    "organizer": { 
        "tenantId": "9f044231-b634-4bdd-b29d-2776e3dbd699", 
        "objectId": "16e0b7bb-93d5-4352-99e0-23ee5f2fffe2", 
        "id": "29:1q4D6ekLXEAALkrqyLXUIcwtVSdXx31bf6vMdfahmkTb9euYVYSsN9x4133pXLV_I2idpVriFe40e19XEZt57bQ", 
        "aadObjectId": "16e0b7bb-93d5-4352-99e0-23ee5f2fffe2"
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

| プロパティ名 | 説明 |
|---|---|
| **details.id** | BASE64 文字列としてエンコードされた会議の ID。 |
| **details.msGraphResourceId** | MSGraphResourceId。MS Graph API呼び出しに特に使用されます。 |
| **details.scheduledStartTime** | 会議のスケジュールされた開始時刻 (UTC)。 |
| **details.scheduledEndTime** | 会議のスケジュールされた終了時刻 (UTC)。 |
| **details.joinUrl** | 会議に参加するために使用する URL。 |
| **details.title** | 会議のタイトル。 |
| **details.type** | 会議の種類 (OneToOneCall、GroupCall、Scheduled、Recurring、MeetNow、ChannelScheduled、ChannelRecurring)。 |
| **conversation.isGroup** | 会話に 2 人以上の参加者があるかどうかを示すブール値。 |
| **conversation.conversationType** | 会話の種類。 |
| **conversation.id** | 会議チャット ID。 |
| **organizer.id** | 開催者のユーザー ID。 |
| **organizer.aadObjectId** | 開催者の Azure Active Directory オブジェクト ID。 |
| **organizer.tenantId** | 開催者の Azure Active Directory テナント ID。 |

定期的な会議の種類の場合は、

**startDate**: パターンの適用を開始する日付を指定します。 startDate の値は、イベント リソースの start プロパティの日付値に対応している必要があります。 パターンに合わない場合、この日付に最初に会議が発生しない可能性があることに注意してください。

**endDate**: パターンの適用を停止する日付を指定します。 この日付に会議の最後の出現がパターンに合わない場合は発生しないことに注意してください。

## <a name="send-real-time-captions-api"></a>リアルタイム キャプション API を送信する

リアルタイム キャプションの送信 API は、Teams コミュニケーション アクセス リアルタイム翻訳 (CART) キャプション (人間型のクローズド キャプション) の POST エンドポイントを公開します。 このエンドポイントに送信されるテキスト コンテンツは、キャプションが有効になっていると、Teams 会議のエンド ユーザーに表示されます。

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

> [!NOTE]  
> Each POST request generates a new line of captions. To ensure that the end user has enough time to read the content, limit each POST request body to 80-120 characters.

### <a name="error-codes"></a>エラー コード

次の表に、エラー コードを示します。

|エラー コード|説明|
|---|---|
| **400** | 要求が正しくありません。 応答本文に、詳細な情報があります。 たとえば、必要なパラメーターの一部が提示されていません。|
| **401** | Unauthorized. Bad or expired token. If you receive this error, generate a new CART URL in Teams. |
| **404** | 会議が見つからないか、開始されていません。 このエラーが発生した場合は、会議を開始してキャプションの開始を選択したことを確認してください。 会議でキャプションを有効にした後、会議へのキャプションの POST を開始できます。|
| **500** |内部サーバー エラー。 詳細については、[サポートにお問い合わせいただくか、フィードバックをお寄せください](../feedback.md)。|

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

| プロパティ名 | 説明 |
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
| **entities.locale** | ロケールに関するメタデータを含むエンティティ。 |
| **entities.country** | 国に関するメタデータを含むエンティティ。 |
| **entities.type** | クライアントに関するメタデータを含むエンティティ。 |
| **channelData.tenant.id** | Azure Active Directory テナント ID。 |
| **channelData.source** | イベントが発生または呼び出されるソース名。 |
| **channelData.meeting.id** | 会議に関連付けられている既定の ID。 |
| **値。MeetingType** | 会議の種類。 |
| **値。タイトル** | 会議の件名。 |
| **値。Id** | 会議に関連付けられている既定の ID。 |
| **値。JoinUrl** | 会議の参加 URL。 |
| **値。Starttime** | UTC での会議の開始時刻。 |
| **値。Endtime** | 会議の終了時刻 (UTC)。 |
| **locale**| クライアントによって設定されたメッセージのロケール。 |

## <a name="get-incoming-audio-state"></a>受信オーディオの状態を取得する

`getIncomingClientAudioState` API を使用すると、アプリは会議ユーザーの受信オーディオ状態設定を取得できます。 この API は、Teams クライアント SDK を通して使用できます。

> [!NOTE]
>
> * モバイル用 API は `getIncomingClientAudioState` 現在、 [パブリック開発者プレビュー](../resources/dev-preview/developer-preview-intro.md)で利用できます。
> * マニフェスト バージョン 1.12 以降のバージョンではリソース固有の同意を使用できるため、この API はマニフェスト バージョン 1.11 以前のバージョンでは機能しません。

### <a name="manifest"></a>マニフェスト

```JSON
"authorization": {
    "permissions": {
      "resourceSpecific": [
        {
          "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
          "type": "Delegated"
        }
      ]
    }
  }
```
  
### <a name="example"></a>例

```javascript
callback = (errcode, result) => {
        if (errcode) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }

microsoftTeams.meeting.getIncomingClientAudioState(this.callback)
```

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、2 つのパラメーター `error` と が `result`含まれています。 エラーには、 *エラー* の種類 `SdkError` 、または `null` オーディオのフェッチが成功した場合に含めることができます。 *結果* には、オーディオフェッチが成功した場合は true または false 値、オーディオフェッチが失敗した場合は null を含めることができます。 結果が true の場合は受信オーディオがミュートされ、結果が false の場合はミュート解除されます。 |
  
### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **501** | API は、現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="toggle-incoming-audio"></a>受信オーディオを切り替える

`toggleIncomingClientAudio` API を使用すると、会議ユーザーの受信オーディオ状態設定をミュートからミュート解除、またはその逆に切り替えることができます。 この API は、Teams クライアント SDK を通して使用できます。

> [!NOTE]
>
> * モバイル用 API は `toggleIncomingClientAudio` 現在、 [パブリック開発者プレビュー](../resources/dev-preview/developer-preview-intro.md)で利用できます。
> * マニフェスト バージョン 1.12 以降のバージョンではリソース固有の同意を使用できるため、この API はマニフェスト バージョン 1.11 以前のバージョンでは機能しません。

### <a name="manifest"></a>マニフェスト

```JSON
"authorization": {
 "permissions": {
  "resourceSpecific": [
   {
    "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
    "type": "Delegated"
   }
  ]
 }
}
```

### <a name="example"></a>例

```javascript
callback = (error, result) => {
        if (error) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }

microsoftTeams.meeting.toggleIncomingClientAudio(this.callback)
```
  
### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、2 つのパラメーター `error` と が `result`含まれています。 エラーには、 *エラー* の種類 `SdkError` または `null` トグルが成功した場合に含めることができます。 *結果* には、トグルが成功した場合は true または false 値、トグルが失敗した場合は null を含めることができます。 結果が true の場合は受信オーディオがミュートされ、結果が false の場合はミュート解除されます。
  
### <a name="response-code"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **501** | API は、現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| 会議の拡張性 | トークンを渡すための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会議コンテンツ バブル ボット | 会議でコンテンツ バブル ボットと対話するための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| 会議のサイド パネル | 会議内のサイド パネルと対話するための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| 会議の [詳細] タブ | 会議内の [詳細] タブを操作するための Teams 会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
| 会議イベントのサンプル | リアルタイムの Teams 会議イベントを示すサンプル アプリ|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
| 採用会議のサンプル |採用シナリオの会議エクスペリエンスを示すサンプル アプリ。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
| QR コードを使用したアプリのインストール |QR コードを生成し、QR コードを使用してアプリをインストールするサンプル アプリ|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>関連項目

* [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会議用アプリ](teams-apps-in-meetings.md)
* [Live Share SDK](teams-live-share-overview.md)
* [Teams のクラウド会議の記録](/microsoftteams/cloud-recording)

## <a name="next-steps"></a>次の手順

[会議用のビルド タブ](build-tabs-for-meeting.md)
