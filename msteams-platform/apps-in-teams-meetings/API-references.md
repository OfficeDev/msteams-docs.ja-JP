---
title: 会議アプリ API リファレンス
author: surbhigupta
description: 例とコード サンプルを使用して会議アプリ API 参照を識別する
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams apps 会議 ユーザー参加者ロール api usercontext 通知シグナル クエリ
ms.openlocfilehash: 29e0e797b3b55dd3fa25071929072957c8d43fd8
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887707"
---
# <a name="meeting-apps-api-references"></a>会議アプリ API リファレンス

会議の機能の向上は、会議のエクスペリエンスを変革する API を提供します。

* 会議のライフサイクル内でアプリを構築したり、既存のアプリを統合したりします。
* API を使用して、アプリに会議を認識させる。
* 会議のエクスペリエンスを強化するために使用する API を選択します。

次の表に、API の一覧を示します。

|API|説明|要求|ソース|
|---|---|----|---|
|**GetUserContext**| この API を使用すると、コンテキスト情報を取得して、関連するコンテンツを [コンテンツ] タブTeamsできます。 |_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_|Microsoft Teamsクライアント SDK|
|**GetParticipant**| この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。 |**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot FrameworkSDK|
|**NotificationSignal** | この API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。 これにより、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。 |**POST** _**/v3/conversation/{conversationId}/activities**_|Microsoft Bot FrameworkSDK|
|**会議の詳細** | この API を使用すると、静的な会議のメタデータを取得できます。 |**GET** _**/v1/meetings/{meetingId}**_| ボット SDK |

次の表に、API の Bot Framework SDK メソッドを示します。

|API|Bot Framework SDK メソッド|
|---|---|
|**GetParticipant**| `GetMeetingParticipantAsync (Microsoft.Bot.Builder.ITurnContext turnContext, string meetingId = default, string participantId = default, string tenantId = default, System.Threading.CancellationToken cancellationToken = default);` |
|**NotificationSignal** | `activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<title>&completionBotId=BOT_APP_ID");` |
|**会議の詳細** | `TeamsMeetingInfo (string id = default);` |

## <a name="getusercontext-api"></a>GetUserContext API

タブ コンテンツのコンテキスト情報を特定して取得するには[、「get context for your Teams タブ」を参照してください](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`は、会議コンテキストで実行するときにタブで使用され、応答ペイロードに追加されます。

## <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * 会議の開催者がいつでも役割を変更できるので、参加者の役割をキャッシュしない。
> * Teams現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズはサポート `GetParticipant` されていません。

API `GetParticipant` を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。 API には、クエリ パラメーター、例、および応答コードが含まれています。

### <a name="query-parameters"></a>クエリ パラメーター

`GetParticipant`API には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。|
|**participantId**| String | はい | 参加者 ID はユーザー ID です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO から参加者 ID を取得する方法をお勧めします。 |
|**tenantId**| String | はい | テナントユーザーにはテナント ID が必要です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO からテナント ID を取得する方法をお勧めします。 | 

### <a name="example"></a>例

`GetParticipant`API には、次の例が含まれています。

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

---

API の JSON 応答 `GetParticipant` 本文は次の形式です。

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
      "isGroup":true
   }
}
```

### <a name="response-codes"></a>応答コード

`GetParticipant`API は、次の応答コードを返します。

|応答コード|説明|
|---|---|
| **403** | 参加者情報の取得がアプリと共有されていない。 アプリが会議にインストールされていない場合、最も一般的なエラー応答 403 がトリガーされます。 テナント管理者がライブ サイトの移行中にアプリを無効またはブロックすると、403 エラー応答がトリガーされます。 |
| **200** | 参加者情報が正常に取得されます。|
| **401** | アプリは無効なトークンで応答します。|
| **404** | 会議の有効期限が切れているか、参加者が見つかりません。|

## <a name="notificationsignal-api"></a>NotificationSignal API

会議のすべてのユーザーは、API を介して送信された通知を受け取 `NotificationSignal` る。

> [!NOTE]
> * 会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。
> * 現在、ターゲット通知の送信はサポートされていません。

`NotificationSignal` API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。 この API を使用すると、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。 API には、クエリ パラメーター、例、および応答コードが含まれます。

### <a name="query-parameter"></a>クエリ パラメーター

`NotificationSignal`API には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| String | はい | 会話識別子は、ボット呼び出しの一部として使用できます。 |

### <a name="examples"></a>例

は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。

> [!NOTE]
> * 要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、the のパラメーターは省略可能です。 `Bot ID` はマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。
> * 幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。 寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。
> * URL は、会議中のダイアログ ボックスに表示 `<iframe>` されるページです。 ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。

`NotificationSignal`API には、次の例が含まれています。

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

### <a name="response-codes"></a>応答コード

`NotificationSignal`API には、次の応答コードが含まれています。

|応答コード|説明|
|---|---|
| **201** | シグナルを含むアクティビティが正常に送信されます。 |
| **401** | アプリは無効なトークンで応答します。 |
| **403** | アプリは信号を送信できません。 403 応答コードは、テナント管理者がライブ サイトの移行中にアプリを無効にし、ブロックするなど、さまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれています。 |
| **404** | 会議チャットが存在しません。 |

## <a name="meeting-details-api"></a>会議の詳細 API

> [!NOTE]
> この機能は現在、パブリック開発者 [プレビューでのみ利用](../resources/dev-preview/developer-preview-intro.md) できます。

会議の詳細 API を使用すると、アプリは静的な会議のメタデータを取得できます。 メタデータは、動的に変更しないデータ ポイントを提供します。
API はボット サービスを通じて利用できます。

### <a name="prerequisite"></a>前提条件

会議の詳細 API を使用するには、RSC アクセス許可を取得する必要があります。 アプリ マニフェストのプロパティを構成するには、次の例を使用 `webApplicationInfo` します。

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
### <a name="query-parameter"></a>クエリ パラメーター

会議の詳細 API には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。 |

### <a name="example"></a>例

会議の詳細 API には、次の例が含まれています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

使用不可

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

会議の詳細 API の JSON 応答本文は次のとおりです。

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a>リアルタイムの会議Teamsイベント

ユーザーはリアルタイムの会議イベントを受信できます。 アプリが会議に関連付けられるとすぐに、実際の会議の開始時刻と終了時刻がボットと共有されます。

会議の実際の開始時刻と終了時刻は、スケジュールされた開始時刻と終了時刻とは異なります。 会議の詳細 API は、スケジュールされた開始時刻と終了時刻を提供します。 イベントは、実際の開始時刻と終了時刻を提供します。

### <a name="prerequisite"></a>前提条件

アプリ マニフェストには、会議の開始 `webApplicationInfo` イベントと終了イベントを受信するプロパティが必要です。 マニフェストを構成するには、次の例を使用します。

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

### <a name="example-of-meeting-start-event-payload"></a>会議の開始イベント ペイロードの例

次のコードは、会議の開始イベント ペイロードの例を示しています。

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

### <a name="example-of-meeting-end-event-payload"></a>会議の終了イベント ペイロードの例

次のコードは、会議の終了イベント ペイロードの例を示しています。

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

### <a name="example-of-getting-metadata-of-a-meeting"></a>会議のメタデータを取得する例

ボットはハンドラーを介してイベントを受け取 `OnEventActivityAsync` ります。

json ペイロードを逆シリアル化するために、会議のメタデータを取得するためにモデル オブジェクトが導入されます。 会議のメタデータは、イベント ペイロード `value` 内のプロパティにあります。 model `MeetingStartEndEventvalue` オブジェクトが作成され、メンバー変数はイベント ペイロード内のプロパティの `value` キーに対応します。
     
> [!NOTE]      
> * から会議 ID を取得します `turnContext.ChannelData` 。    
> * 会議 ID として会話 ID を使用しない。     
> * 会議イベントペイロードから会議 ID を使用しない `turncontext.activity.value` 。 
      
次のコードは、会議の開始/終了イベントのメタデータをキャプチャする方法を `MeetingType` `Title` `Id` `JoinUrl` `StartTime` `EndTime` 示しています。

会議の開始イベント
```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
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

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js | 
|----------------|-----------------|--------------|--------------|
| 会議の機能拡張 | Microsoft Teams渡しに関する会議機能拡張サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会議コンテンツ バブル ボット | Microsoft Teamsでコンテンツ バブル ボットを操作するための会議機能拡張サンプルを作成します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| MeetingSidePanel | Microsoft Teamsのサイド パネルを操作するための会議機能拡張サンプルを作成します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| 会議の [詳細] タブ | Microsoft Teamsの詳細タブを操作するための会議機能拡張サンプルを作成します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|会議イベントのサンプル|会議イベントをリアルタイムで表示Teamsアプリ|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|会議の採用サンプル|採用シナリオの会議エクスペリエンスを表示するサンプル アプリ。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|QR コードを使用したアプリのインストール|QR コードを生成し、QR コードを使用してアプリをインストールするサンプル アプリ|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>関連項目

* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [会議のTeamsアプリ](teams-apps-in-meetings.md)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [会議で使用するアプリを有効Teamsする](enable-and-configure-your-app-for-teams-meetings.md)