---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: 3bfbcd0eed1bd287303315ae57cd2f0db039890c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630181"
---
# <a name="create-apps-for-teams-meetings"></a>Teams 会議用のアプリを作成する

## <a name="prerequisites-and-considerations"></a>前提条件と考慮事項

会議のアプリを作成Teams、次の情報を理解している必要があります。

* アプリを開発する方法に関する知識Teamsがあります。 詳細については、「アプリ開発の[Teams」を参照してください](../overview.md)。

* アプリが会議でTeamsを示すために、アプリ マニフェストを更新する必要があります。 詳細については、「アプリ マニフェスト [」を参照してください](#update-your-app-manifest)。

* アプリが会議のライフサイクルでタブとして機能するには、グループチャット スコープで構成可能なタブをサポートする必要があります。 詳細については[、「groupchat スコープ」を参照し、](../resources/schema/manifest-schema.md#configurabletabs)[グループ タブを作成するを参照してください](../build-your-first-app/build-channel-tab.md)。

* 会議前および会議後のシナリオTeams一般的なタブ設計ガイドラインに従う必要があります。 会議中のエクスペリエンスについては、「会議内タブ」と「会議内ダイアログの設計ガイドライン」を参照してください。 詳細については、「[タブデザイン](../tabs/design/tabs.md)Teams、会議中のタブデザインガイドライン、[](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)会議中のダイアログデザインガイドライン[」を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 会議前および会議後のチャットでアプリを有効にするには、この `groupchat` 範囲をサポートする必要があります。 会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。 会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果やフィードバックなど、会議の結果を表示できます。

* 会議 API の URL パラメーターには、、 `meetingId` 、 `userId` および を指定する必要があります `tenantId` 。 これらは、クライアント SDK およびボット アクティビティTeams使用できます。 さらに、ユーザー ID とテナント ID の信頼できる情報は、Tab SSO 認証を使用 [して取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 認証 `GetParticipant` トークンを生成するには、API にボット登録と ID が必要です。 詳細については、「ボットの登録 [と ID」を参照してください](../build-your-first-app/build-bot.md)。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議内] ダイアログ ボックスについては、「で完了パラメーター」 `bot Id` を参照してください `Notification Signal API` 。

## <a name="meeting-apps-api-reference"></a>会議アプリ API リファレンス

|API|説明|要求|ソース|
|---|---|----|---|
|**GetUserContext**| この API を使用すると、コンテキスト情報を取得して、関連するコンテンツを [コンテンツ] タブTeamsできます。 |_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_|Microsoft Teams SDK|
|**GetParticipant**| この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報を取得できます。 |**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot FrameworkSDK|
|**NotificationSignal** | この API を使用すると、ユーザー ボット チャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。 これにより、会議中のダイアログ ボックスを表示するユーザー アクションに基づいて信号を送信できます。 |**POST** _**/v3/conversation/{conversationId}/activities**_|Microsoft Bot FrameworkSDK|

### <a name="getusercontext"></a>GetUserContext

タブ コンテンツのコンテキスト情報を特定して取得するには[、「get context for your Teams タブ」を参照してください](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`は、会議コンテキストで実行するときにタブで使用され、応答ペイロードに追加されます。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * 会議の開催者がいつでも役割を変更できるので、参加者の役割をキャッシュしない。
> * Teams現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズはサポート `GetParticipant` されていません。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| 文字列 | はい | 会議識別子は、ボットの呼び出しとクライアント SDK Teams使用できます。|
|**participantId**| 文字列 | はい | 参加者 ID はユーザー ID です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO から参加者 ID を取得する方法をお勧めします。 |
|**tenantId**| 文字列 | はい | テナントユーザーにはテナント ID が必要です。 これは、Tab SSO、Bot Invoke、およびクライアント SDK Teams使用できます。 Tab SSO からテナント ID を取得する方法をお勧めします。 |

#### <a name="example"></a>例

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

|応答コード|説明|
|---|---|
| **403** | アプリは参加者情報の取得を許可されません。 これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。 たとえば、テナント管理者によってアプリが無効になっている場合や、ライブ サイトの移行中にブロックされている場合などです。|
| **200** | 参加者情報が正常に取得されます。|
| **401** | アプリは無効なトークンで応答します。|
| **404** | 会議の有効期限が切れているか、参加者が見つかりません。|
| **500** | 会議が終了して 60 日以上経過した場合、または参加者が自分の役割に基づくアクセス許可を持っていません。|

### <a name="notificationsignal-api"></a>NotificationSignal API

会議のすべてのユーザーは、API を介して送信された通知を受け取 `NotificationSignal` る。

> [!NOTE]
> * 会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。
> * 現在、ターゲット通知の送信はサポートされていません。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| 文字列 | はい | 会話識別子は、ボットの呼び出しの一部として使用できます。 |

#### <a name="example"></a>例

は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。

> [!NOTE]
> * 要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、the のパラメーターは省略可能です。 `Bot ID` はマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。
> * 幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。 寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。
> * URL は、会議中のダイアログ ボックスに表示 `<iframe>` されるページです。 ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。

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

* * *

#### <a name="response-codes"></a>応答コード

|応答コード|説明|
|---|---|
| **201** | シグナルを含むアクティビティが正常に送信されます。 |
| **401** | アプリは無効なトークンで応答します。 |
| **403** | アプリは信号を送信できません。 これは、テナント管理者がアプリを無効にし、アプリがライブ サイトの移行中にブロックされるなど、さまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれています。 |
| **404** | 会議チャットが存在しません。 |

## <a name="enable-your-app-for-teams-meetings"></a>会議でアプリを有効Teamsする

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、、 、および配列を使用してアプリ マニフェスト `configurableTabs` `scopes` で宣言 `context` されます。 スコープは、アプリを使用できる場所を定義するユーザーとコンテキストを定義します。

> [!NOTE]
> マニフェスト スキーマを使用してアプリ マニフェストを [更新してみてください](../resources/schema/manifest-schema-dev-preview.md)。
> 会議のアプリには、 *グループチャットスコープが必要* です。 チーム *スコープは* 、チャネル内のタブでのみ機能します。

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> `meetingStage` は現在、開発者プレビューでのみ使用できます。

### <a name="context-property"></a>Context プロパティ

タブと `context` プロパティ `scopes` を使用すると、アプリを表示する必要がある場所を特定できます。 またはスコープ内 `team` のタブ `groupchat` には、複数のコンテキストを指定できます。 値のすべてまたは一部を使用できるプロパティの値を `context` 次に示します。

|値|説明|
|---|---|
| **channelTab** | チーム チャネルのヘッダー内のタブ。 |
| **privateChatTab** | チームまたは会議のコンテキストではない一連のユーザー間のグループ チャットのヘッダー内のタブ。 |
| **meetingChatTab** | スケジュールされた会議のコンテキスト内の一連のユーザー間のグループ チャットのヘッダー内のタブ。 |
| **meetingDetailsTab** | 予定表の会議の詳細ビューのヘッダーにあるタブ。 |
| **meetingSidePanel** | 統合バー (U バー) を介して開いた会議内パネル。 |
| **meetingStage** | サイドパネルのアプリを会議ステージに共有できます。 |

> [!NOTE]
> `Context` プロパティは現在、モバイル クライアントではサポートされていません。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

> [!NOTE]
> * タブ ギャラリーにアプリを表示するには、構成可能なタブとグループ チャットスコープをサポートする必要があります。
> * モバイル クライアントは、会議の開催前と開催後のステージでのみタブをサポートします。
> * 現在、モバイル クライアントでは、会議中のダイアログ ボックスとタブである会議内エクスペリエンスはサポートされていません。 詳細については、「モバイル用の [タブを作成する際の](../tabs/design/tabs-mobile.md) モバイルタブのガイダンス」を参照してください。

### <a name="before-a-meeting"></a>会議の前に

会議の前に、ユーザーはタブ、ボット、メッセージング拡張機能を会議に追加できます。 開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。

**タブを会議に追加するには**

1. 予定表で、タブを追加する会議を選択します。
1. [詳細] **タブを選択** し、[プラス] を選択します。 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. タブ ギャラリーが表示されます。

    ![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

1. タブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 アプリはタブとしてインストールされます。
    > [!NOTE] 
    > 現在、会議タブでは、会議の詳細と参加者情報の取得はサポートされていません。

**会議にメッセージング拡張機能を追加するには**

1. チャット内のメッセージの作成 &#x25CF;&#x25CF;&#x25CF; にある省略記号またはオーバーフロー メニューを選択します。
1. 追加するアプリを選択し、必要に応じて手順に従います。 アプリはメッセージング拡張機能としてインストールされます。

**ボットを会議に追加するには**

会議チャットでキーを入力し **@** 、[ボットの取得 **] を選択します**。

> [!NOTE]
> * ユーザー ID は、Tabs SSO を使用して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。 認証後、アプリは API を使用してユーザー ロールを取得 `GetParticipant` できます。
> * ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。 たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。
> * 会議の進行中に役割の割り当てを変更できます。 詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

### <a name="during-a-meeting"></a>会議中

#### <a name="sidepanel"></a>sidePanel

sidePanel を使用すると、会議のエクスペリエンスをカスタマイズして、開催者と発表者が異なるビューとアクションのセットを持つ事が可能です。 アプリ マニフェストで、コンテキスト配列に sidePanel を追加する必要があります。 会議およびすべてのシナリオで、アプリは幅 320 ピクセルの会議内タブに表示されます。 詳細については [、「FrameContext インターフェイス」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。

API を使用して要求を必要に応じてルーティングするには、「SDK `userContext` Teams[参照してください](../tabs/how-to/access-teams-context.md#user-context)。 タブについては[Teams認証フローを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。 タブの認証フローは、Web サイトの認証フローと非常に似ています。 したがって、タブは OAuth 2.0 を直接使用できます。 参照[、Microsoft ID プラットフォーム OAuth 2.0 承認コード フローを参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

メッセージング拡張機能は、ユーザーが会議内ビューにいて、ユーザーが作成メッセージ拡張カードを投稿できる場合に期待通り動作します。 AppName in-meeting は、会議中の U バーのアプリ名を示すツールヒントです。

> [!NOTE]
> バージョン 1.7.0 以上の[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用します。前のバージョンではサイド パネルはサポートされていません。

#### <a name="in-meeting-dialog"></a>会議中ダイアログ

[会議中] ダイアログ ボックスを使用すると、会議中に参加者を引き付け、会議中に情報やフィードバックを収集できます。 API を [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) 使用して、バブル通知をトリガーする必要があります。 通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含める。

会議中のダイアログでは、タスク モジュールを使用することはできません。 タスク モジュールは、会議チャットでは呼び出されません。 外部リソース URL を使用して、会議にコンテンツ バブルを表示します。 このメソッドを使用 `submitTask` して、会議チャットでデータを送信できます。

> [!NOTE]
> * ユーザーが Web ビューでアクションを実行した後に自動的に終了するには [、submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出す必要があります。 これは、アプリの申請に必要な要件です。 詳細については、「SDK タスク モジュール[Teamsを参照してください](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)。
> * アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、要求メタデータではなく、オブジェクト内の要求メタデータ `from.id` `from` に `from.aadObjectId` 依存する必要があります。 `from.id`はユーザー ID であり `from.aadObjectId` 、ユーザー Azure Active Directory (AAD) ID です。 詳細については、「タブでタスク [モジュールを使用する」を参照し](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、 [タスク モジュールを作成して送信します](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

#### <a name="share-to-stage"></a>ステージ間の共有 

> [!NOTE]
> * この機能は現在、開発者プレビューでのみ使用できます。
> * この機能を使用するには、アプリが会議中のサイドパネルをサポートしている必要があります。


この機能により、開発者はアプリを会議ステージに共有できます。 会議ステージへの共有を有効にすると、会議の参加者はリアルタイムで共同作業できます。 

必要なコンテキストは `meetingStage` 、アプリ マニフェスト内です。 このための前提条件は、コンテキストを持 `meetingSidePanel` つ必要があります。 これにより、 **サイドパネルの** [共有] ボタンが次の図で切り離されます。

  ![share_to_stage_during_meetingエクスペリエンス](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

この機能を有効にするために必要なマニフェストの変更は次のとおりです。 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a>会議の後

会議後と会議前の構成は同等です。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| 会議の機能拡張 | Microsoft Teams渡しに関する会議機能拡張サンプル。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会議コンテンツ バブル ボット | Microsoft Teamsでコンテンツ バブル ボットを操作するための会議機能拡張サンプルを作成します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Meeting SidePanel | Microsoft Teams会議のサイド パネルで iteracting の会議機能拡張サンプルを作成します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
