---
title: Teams 会議アプリへの前提条件と API リファレンス
author: surbhigupta
description: 会議のアプリをTeamsする
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 3a3b2fc13f67d2ca3b061a165248fa2458058441
ms.sourcegitcommit: f62634c59b697107e5bb3c38867b21007d328b1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53196237"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a>Teams 会議アプリへの前提条件と API リファレンス

会議のライフサイクル全体にわたってアプリの機能を拡張するには、Teams会議用のアプリTeamsできます。 前提条件を確認し、会議アプリ API 参照を使用して会議のエクスペリエンスを向上させる必要があります。

## <a name="prerequisites"></a>前提条件

会議のアプリをTeams前に、次の情報を理解している必要があります。

* アプリを開発する方法に関する知識Teamsがあります。 詳細については、「アプリ開発の[Teams」を参照してください](../overview.md)。

* アプリが会議でTeamsを示すために、アプリ マニフェストを更新する必要があります。 詳細については、「アプリ マニフェスト [」を参照してください](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* アプリが会議のライフサイクルでタブとして機能するには、アプリが groupchat スコープで構成可能なタブをサポートしている必要があります。詳細については[、「groupchat スコープ」を参照し、](../resources/schema/manifest-schema.md#configurabletabs)[グループ タブを作成するを参照してください](../build-your-first-app/build-channel-tab.md)。

* 会議前および会議後のシナリオTeams一般的なタブデザインガイドラインに従う必要があります。 会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。 詳細については、「[タブデザイン](../tabs/design/tabs.md)Teams、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)および会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 会議前および会議後のチャットでアプリを有効にするには、この `groupchat` 範囲をサポートする必要があります。 会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。 会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果やフィードバックなど、会議の結果を表示できます。

* 会議 API の URL パラメーターには、、 `meetingId` 、 `userId` および を指定する必要があります `tenantId` 。 これらは、クライアント SDK およびボット アクティビティTeams使用できます。 さらに、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼 [できる情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 認証 `GetParticipant` トークンを生成するには、API にボット登録と ID が必要です。 詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議内] ダイアログ ボックスについては、「API の完了 `bot Id` パラメーター」を参照 `NotificationSignal` してください。

* 会議の詳細 API には、ボット登録とボット ID が必要です。 ボット SDK を取得する必要があります `TurnContext` 。

* リアルタイムの会議イベントの場合は、ボット SDK で使用できる `TurnContext` オブジェクトに精通している必要があります。 オブジェクト `Activity` には、 `TurnContext` 実際の開始時刻と終了時刻を含むペイロードが含まれます。 リアルタイム会議イベントでは、会議プラットフォームから登録済みのボット ID がTeamsされます。

前提条件を満たした後、会議アプリ API リファレンス 、、および会議の詳細 API を使用して、属性を使用して情報にアクセスし、関連するコンテンツ `GetUserContext` `GetParticipant` `NotificationSignal` を表示できます。

## <a name="meeting-apps-api-references"></a>会議アプリ API の参照

新しい会議の機能は、会議のエクスペリエンスを変革する API を提供します。 この新しい機能を使用すると、会議のライフサイクル内でアプリを構築したり、既存のアプリを統合することができます。 API を使用すると、アプリで会議を認識できます。 会議のエクスペリエンスを強化するために使用する API を選択できます。

次の表に、これらの API の一覧を示します。

|API|説明|要求|ソース|
|---|---|----|---|
|**GetUserContext**| この API を使用すると、コンテキスト情報を取得して、関連するコンテンツを [コンテンツ] タブTeamsできます。 |_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_|Microsoft Teamsクライアント SDK|
|**GetParticipant**| この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。 |**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot FrameworkSDK|
|**NotificationSignal** | この API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。 これにより、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。 |**POST** _**/v3/conversation/{conversationId}/activities**_|Microsoft Bot FrameworkSDK|
|**会議の詳細** | この API を使用すると、静的な会議のメタデータを取得できます。 |**GET** _**/v1/meetings/{meetingId}**_| ボット SDK |

### <a name="getusercontext-api"></a>GetUserContext API

タブ コンテンツのコンテキスト情報を特定して取得するには[、「get context for your Teams タブ」を参照してください](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`は、会議コンテキストで実行するときにタブで使用され、応答ペイロードに追加されます。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * 会議の開催者がいつでも役割を変更できるので、参加者の役割をキャッシュしない。
> * Teams現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズはサポート `GetParticipant` されていません。

API `GetParticipant` を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。 API には、クエリ パラメーター、例、および応答コードが含まれています。

#### <a name="query-parameters"></a>クエリ パラメーター

`GetParticipant`API には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。|
|**participantId**| String | はい | 参加者 ID はユーザー ID です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO から参加者 ID を取得する方法をお勧めします。 |
|**tenantId**| String | はい | テナントユーザーにはテナント ID が必要です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO からテナント ID を取得する方法をお勧めします。 |

#### <a name="example"></a>例

`GetParticipant`API には、次の例が含まれています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
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

* * *

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

#### <a name="response-codes"></a>応答コード

`GetParticipant`API には、次の応答コードが含まれています。

|応答コード|説明|
|---|---|
| **403** | アプリは参加者情報の取得を許可されません。 これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。 たとえば、テナント管理者によってアプリが無効になっている場合や、ライブ サイトの移行中にブロックされている場合などです。|
| **200** | 参加者情報が正常に取得されます。|
| **401** | アプリは無効なトークンで応答します。|
| **404** | 会議の有効期限が切れているか、参加者が見つかりません。|
| **500** | 会議が終了した後、会議の有効期限が切れている (60 日を超える) か、参加者が自分の役割に基づいてアクセス許可を持っていません。|

### <a name="notificationsignal-api"></a>NotificationSignal API

会議のすべてのユーザーは、API を介して送信された通知を受け取 `NotificationSignal` る。

> [!NOTE]
> * 会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。
> * 現在、ターゲット通知の送信はサポートされていません。

`NotificationSignal` API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。 この API を使用すると、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。 API には、クエリ パラメーター、例、および応答コードが含まれます。

#### <a name="query-parameter"></a>クエリ パラメーター

`NotificationSignal`API には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| String | はい | 会話識別子は、ボット呼び出しの一部として使用できます。 |

#### <a name="examples"></a>例

は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。

> [!NOTE]
> * 要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、the のパラメーターは省略可能です。 `Bot ID` はマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。
> * 幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。 寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。
> * URL は、会議中のダイアログ ボックスに表示 `<iframe>` されるページです。 ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。

`NotificationSignal`API には、次の例が含まれています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
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

#### <a name="response-codes"></a>応答コード

`NotificationSignal`API には、次の応答コードが含まれています。

|応答コード|説明|
|---|---|
| **201** | シグナルを含むアクティビティが正常に送信されます。 |
| **401** | アプリは無効なトークンで応答します。 |
| **403** | アプリは信号を送信できません。 これは、テナント管理者がアプリを無効にし、アプリがライブ サイトの移行中にブロックされるなど、さまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれています。 |
| **404** | 会議チャットが存在しません。 |

### <a name="meeting-details-api"></a>会議の詳細 API

> [!NOTE]
> この機能は現在、パブリック開発者 [プレビューでのみ利用](../resources/dev-preview/developer-preview-intro.md) できます。

会議の詳細 API を使用すると、アプリは静的な会議のメタデータを取得できます。 これらは、動的に変更されないデータ ポイントです。
API はボット サービスを通じて利用できます。

#### <a name="prerequisite"></a>前提条件

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

#### <a name="query-parameter"></a>クエリ パラメーター

会議の詳細 API には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。 |

#### <a name="example"></a>例

会議の詳細 API には、次の例が含まれています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
var connectorClient = parameters.TurnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

利用不可

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

> [!NOTE]
> この機能は現在、パブリック開発者 [プレビューでのみ利用](../resources/dev-preview/developer-preview-intro.md) できます。

ユーザーはリアルタイムの会議イベントを受信できます。 アプリが会議に関連付けられるとすぐに、実際の会議の開始時刻と会議の終了時刻がボットと共有されます。

会議の実際の開始時刻と終了時刻は、スケジュールされた開始時刻と終了時刻とは異なります。 会議の詳細 API はスケジュールされた開始時刻と終了時刻を提供し、イベントは実際の開始時刻と終了時刻を提供します。

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
        "Id":"meeting id", 
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

json ペイロードを逆シリアル化するために、会議のメタデータを取得するためにモデル オブジェクトが導入されます。 会議のメタデータは、イベント ペイロード `value` 内のプロパティに存在します。 model `MeetingStartEndEventvalue` オブジェクトが作成され、メンバー変数はイベント ペイロード内のプロパティの `value` キーに対応します。

次のコードは、会議の開始イベントと終了イベントのメタデータをキャプチャする方法 `MeetingType` `Title` `Id` `JoinUrl` `StartTime` `EndTime` を示しています。

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

MeetingStartEndEventvalue.cs には、次のコードが含まれています。

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| 会議の機能拡張 | Microsoft Teams渡しに関する会議機能拡張サンプル。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会議コンテンツ バブル ボット | Microsoft Teamsでコンテンツ バブル ボットを操作するための会議機能拡張サンプルを作成します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| MeetingSidePanel | Microsoft Teamsのサイド パネルを操作するための会議機能拡張サンプルを作成します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| 会議の [詳細] タブ | Microsoft Teamsの詳細タブで iteracting の会議機能拡張サンプルを作成します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [会議のTeamsアプリ](teams-apps-in-meetings.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会議で使用するアプリを有効Teamsする](enable-and-configure-your-app-for-teams-meetings.md)
