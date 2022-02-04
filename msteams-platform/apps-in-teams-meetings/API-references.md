---
title: 会議アプリ API リファレンス
author: surbhigupta
description: 例とコード サンプルを使用して会議アプリ API 参照を特定する
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams apps 会議 ユーザー参加者ロール API ユーザー コンテキスト通知シグナル クエリ
---

# <a name="meeting-apps-api-references"></a>会議アプリ API リファレンス

会議の機能拡張は、会議のエクスペリエンスを向上させる API を提供します。 リストされている API の助けを借りて、次の操作を実行できます。

* 会議のライフサイクル内でアプリを構築したり、既存のアプリを統合したりします。
* API を使用して、アプリに会議を認識させる。
* 会議のエクスペリエンスを向上させるために必要な API を選択します。

次の表に、クライアント (MSTC) と MSBF (MSBF) SDK で使用Microsoft Teams API の一覧Microsoft Bot Framework示します。

|メソッド| 説明| ソース|
|---|---|----|
|[**ユーザー コンテキストの取得**](#get-user-context-api)| コンテキスト情報を取得して、関連するコンテンツを [ページ] タブTeams表示します。| MSTC SDK|
|[**参加者を取得する**](#get-participant-api)| 会議 ID と参加者 ID で参加者情報を取得します。 |MSBF SDK|
|[**通知信号の送信**](#send-notification-signal-api)| ユーザーボット チャット用の既存の会話通知 API を使用して会議信号を提供し、会議中のダイアログ ボックスを表示するユーザーアクションを通知できます。 |MSBF SDK|
|[**会議の詳細を取得する**](#get-meeting-details-api)| 会議の静的メタデータを取得します。 |MSBF SDK |
|[**リアルタイムのキャプションを送信する**](#send-real-time-captions-api)| 進行中の会議にリアルタイムのキャプションを送信します。 |MSTC SDK|
|[**アプリのコンテンツをステージに共有する**](#share-app-content-to-stage-api)| 会議のアプリ側パネルから、アプリの特定の部分を会議ステージに共有します。 |MSTC SDK|
|[**アプリ コンテンツ ステージの共有状態を取得する**](#get-app-content-stage-sharing-state-api)| 会議ステージでアプリの共有状態に関する情報を取得します。 |MSTC SDK|
|[**アプリ コンテンツ ステージ共有機能の取得**](#get-app-content-stage-sharing-capabilities-api)| 会議ステージに共有するアプリの機能を取得します。 |MSTC SDK|
|[**会議イベントのリアルタイムTeams取得**](#get-real-time-teams-meeting-events-api)|実際の開始時刻や終了時刻など、リアルタイムの会議イベントをフェッチします。| MSBF SDK|

## <a name="get-user-context-api"></a>ユーザー コンテキスト API の取得

タブ コンテンツのコンテキスト情報を識別して取得するには、「[Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)`meetingId` タブのコンテキストを取得する」を参照してください。会議コンテキストで実行されているタブで使用され、応答ペイロードに追加されます。

## <a name="get-participant-api"></a>参加者 API の取得

> [!NOTE]
> * 会議の開催者がいつでも役割を変更できるので、参加者の役割をキャッシュしない。
> * 現在、 `GetParticipant` API は 350 人未満の参加者を持つ配布リストまたは名簿でのみサポートされています。

### <a name="query-parameters"></a>クエリ パラメーター

> [!TIP]
> Tab SSO から参加者 ID とテナント ID を取得します。

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。|
|**participantId**| String | はい | 参加者 ID はユーザー ID です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO から参加者 ID を取得する方法をお勧めします。 |
|**tenantId**| String | はい | テナントユーザーにはテナント ID が必要です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO からテナント ID を取得する方法をお勧めします。 |

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

---

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

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **403** | 参加者情報の取得がアプリと共有されていない。 アプリが会議にインストールされていない場合は、エラー応答 403 がトリガーされます。 テナント管理者がライブ サイトの移行中にアプリを無効またはブロックすると、エラー応答 403 がトリガーされます。 |
| **200** | 参加者情報が正常に取得されます。|
| **401** | アプリは無効なトークンで応答します。|
| **404** | 会議の有効期限が切れているか、参加者が利用できません。|

## <a name="send-notification-signal-api"></a>通知信号 API の送信

会議のすべてのユーザーは、API を介して送信された通知を受け取 `NotificationSignal` る。 `NotificationSignal` API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。 ユーザーの操作、会議内のダイアログ ボックスに基づいて信号を送信できます。 API には、クエリ パラメーター、例、および応答コードが含まれます。

> [!NOTE]
> * 会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。
> * 現在、ターゲット通知の送信はサポートされていません。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| String | はい | 会話識別子は、ボット呼び出しの一部として使用できます。 |

### <a name="examples"></a>例

は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。

> [!NOTE]
> * 要求 `completionBotId` されたペイロードの例 `externalResourceUrl` では、the のパラメーターは省略可能です。
> * 幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。 詳細については、「デザイン ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。
> * URL はページで、会議中の `<iframe>` ダイアログ ボックスのように読み込まれます。 ドメインは、アプリ マニフェスト内のアプリの `validDomains` 配列にある必要があります。

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

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **201** | シグナルを含むアクティビティが正常に送信されます。 |
| **401** | アプリは無効なトークンで応答します。 |
| **403** | アプリは信号を送信できません。 403 応答コードは、テナント管理者がライブ サイトの移行中にアプリを無効にし、ブロックするなど、さまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれています。 |
| **404** | 会議チャットが存在しません。 |

## <a name="get-meeting-details-api"></a>会議の詳細 API の取得

> [!NOTE]
> 現時点では、この機能はパブリック開発者 [プレビューでのみ利用](../resources/dev-preview/developer-preview-intro.md) できます。

会議の詳細 API を使用すると、アプリは会議の静的メタデータを取得できます。 メタデータは、動的に変更しないデータ ポイントを提供します。 API はボット サービスを通じて利用できます。 現在、プライベートスケジュールされた会議または定期的な会議とチャネルのスケジュールされた会議または定期的な会議の両方が、それぞれ異なる RSC アクセス許可を持つ API をサポートしています。

### <a name="prerequisite"></a>前提条件

会議の詳細 API を使用するには、プライベート会議やチャネル会議など、会議の範囲に基づいて異なる RSC アクセス許可を取得する必要があります。

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 の場合</b></summary>

次の例を使用して、プライベート会議用にアプリ マニフェストと`webApplicationInfo``authorization`プロパティを構成します。

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

次の例を使用して、チャネル会議用に`webApplicationInfo``authorization`アプリ マニフェストとプロパティを構成します。

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

次の例を使用して、プライベート会議 `webApplicationInfo` 用にアプリ マニフェストのプロパティを構成します。

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

次の例を使用して、チャネル会議用に `webApplicationInfo` アプリ マニフェストのプロパティを構成します。

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
> ボットは、RSC アクセス許可 `ChannelMeeting.ReadBasic.Group` のマニフェストに追加することで、すべてのチャネルで作成された会議から会議の開始イベントまたは終了イベントを自動的に受信できます。
 
### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターの一覧を示します。

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| String | はい | 会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。 |

### <a name="example"></a>例

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
            "conversationType": "groupchat", 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="send-real-time-captions-api"></a>リアルタイムキャプション API の送信

送信リアルタイム キャプション API は、Microsoft Teams 通信アクセスリアルタイム変換 (CART) キャプション、人間型のクローズド キャプションの POST エンドポイントを公開します。 このエンドポイントに送信されるテキスト コンテンツは、キャプションが有効になっているときに、Microsoft Teams会議のエンド ユーザーに表示されます。

### <a name="cart-url"></a>CART URL

POST エンドポイントの CART URL は、会議中の会議の [会議 **オプション**] ページMicrosoft Teamsできます。 詳細については、「会議の [CART キャプション」をMicrosoft Teamsしてください](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47)。 CART キャプションを使用するために CART URL を変更する必要はない。

#### <a name="query-parameter"></a>クエリ パラメーター

CART URL には、次のクエリ パラメーターが含まれています。

|値|型|必須|説明|
|---|---|----|----|
|**meetingId**| String | はい |会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。 <br/>たとえば、 meetingid=%7b%22tId%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241 -47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%220%222%7d|
|**トークン**| String | はい |承認トークン。<br/> たとえば、token=04751eac |

#### <a name="example"></a>例

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>メソッド

|リソース|メソッド|説明|
|----|----|----|
|/cartcaption|POST|開始された会議のキャプションを処理する|

> [!NOTE]
> すべての要求のコンテンツ タイプが、エンコードされたプレーン テキストUTF-8します。 要求の本文には、キャプションだけが含まれる。

#### <a name="example"></a>例

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> 各 POST 要求は、キャプションの新しい行を生成します。 エンド ユーザーがコンテンツを読み取るのに十分な時間を確保するには、各 POST 要求本文を 80 ~ 120 文字に制限します。

### <a name="error-codes"></a>エラー コード

次の表に、エラー コードを示します。

|エラー コード|説明|
|---|---|
| **400** | 要求が悪い。 応答本文には、より多くの情報があります。 たとえば、表示される必須パラメーターの一部ではありません。|
| **401** | 承認されていない。 トークンが無効または期限切れです。 このエラーが表示された場合は、新しい CART URL を生成して、Teams。 |
| **404** | 会議が見つからないか、開始されませんでした。 このエラーが表示された場合は、会議を開始し、[キャプションの開始] を選択してください。 会議でキャプションを有効にした後、会議に POSTing キャプションを開始できます。|
| **500** |内部サーバー エラー。 詳細については、サポート [に問い合わせ、またはフィードバックを提供してください](../feedback.md)。|

## <a name="share-app-content-to-stage-api"></a>アプリのコンテンツをステージ API に共有する

API `shareAppContentToStage` を使用すると、アプリの特定の部分を会議ステージに共有できます。 API は、クライアント SDK のTeams使用できます。

### <a name="prerequisite"></a>前提条件

API を使用するには `shareAppContentToStage` 、RSC アクセス許可を取得する必要があります。 アプリ マニフェストで、プロパティとフィールド`authorization`を`name``type`構成`resourceSpecific`します。 例:

```json
"authorization": {
    "permission": { 
    "resourceSpecific": [
      { 
      "name": "MeetingStage.Write.Chat",
      "type": "Delegated"
      }
    ]
   }
}
 ```

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれます。 この *エラーには* 、 *SdkError* 型のエラーが含まれているか、共有が成功した場合は null が含まれる場合があります。 結果 *には* 、共有が成功した場合は true の値を含め、共有が失敗した場合は null を指定できます。|
|**appContentURL**| String | はい | ステージに共有される URL。|

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
| **1000** | アプリには、共有をステージに設定するための適切なアクセス許可が付与されていない。|

## <a name="get-app-content-stage-sharing-state-api"></a>アプリ コンテンツ ステージ共有状態 API の取得

API `getAppContentStageSharingState` を使用すると、会議ステージでアプリの共有に関する情報を取得できます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれます。 エラー *には* 、エラーが発生した場合は *SdkError* 型のエラーが含まれるか、共有が成功した場合は null が含まれる場合があります。 結果 *には* 、正常に取得されたことを `AppContentStageSharingState` 示すオブジェクト、または取得に失敗したことを示す null を含められます。|

### <a name="example"></a>例

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

API の JSON 応答本文は次 `getAppContentStageSharingState` の形式です。

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
| **1000** | アプリには、共有をステージに設定するための適切なアクセス許可が付与されていない。|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>アプリ コンテンツ ステージ共有機能 API の取得

API `getAppContentStageSharingCapabilities` を使用すると、会議ステージに共有するアプリの機能をフェッチできます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれます。 この *エラーには* 、 *SdkError* 型のエラーが含まれているか、共有が成功した場合は null が含まれる場合があります。 結果には、正常に取得されたことを `AppContentStageSharingState` 示すオブジェクト、または取得に失敗したことを示す null を含められます。|

### <a name="example"></a>例

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

API の JSON 応答本文は次 `getAppContentStageSharingCapabilities` の形式です。

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
| **1000** | アプリには、ステージへの共有を許可するアクセス許可が付与されていない。|

## <a name="get-real-time-teams-meeting-events-api"></a>会議イベント API でTeamsを取得する

ユーザーはリアルタイムの会議イベントを受信できます。 アプリが会議に関連付けられるとすぐに、実際の会議の開始時刻と終了時刻がボットと共有されます。 会議の実際の開始時刻と終了時刻は、スケジュールされた開始時刻と終了時刻とは異なります。 会議の詳細 API は、スケジュールされた開始時刻と終了時刻を提供します。 イベントは、実際の開始時刻と終了時刻を提供します。

### <a name="prerequisite"></a>前提条件

アプリ マニフェストには、会議の開始イベント `webApplicationInfo` と終了イベントを受信するプロパティが必要です。 マニフェストを構成するには、次の例を使用します。

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 の場合</b></summary>

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

### <a name="example-of-getting-meetingstartendeventvalue"></a>取得の例 `MeetingStartEndEventvalue`

ボットはハンドラーを介してイベントを受け取 `OnEventActivityAsync` ります。 JSON ペイロードを逆シリアル化するために、会議のメタデータを取得するためにモデル オブジェクトが導入されます。 会議のメタデータは、イベント ペイロード `value` 内のプロパティにあります。 model `MeetingStartEndEventvalue` オブジェクトが作成され、メンバー変数はイベント `value` ペイロード内のプロパティのキーに対応します。

> [!NOTE]
> * から会議 ID を取得します `turnContext.ChannelData`。
> * 会議 ID として会話 ID を使用しない。
> * 会議イベントペイロードから会議 ID を使用しない `turncontext.activity.value`。

次のコードは、会議`MeetingType``EndTime``Title``Id``JoinUrl``StartTime`の開始/終了イベントのメタデータをキャプチャする方法を示しています。

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
* [Teams 会議用アプリ](teams-apps-in-meetings.md)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [会議で使用するアプリを有効Teamsする](enable-and-configure-your-app-for-teams-meetings.md)
