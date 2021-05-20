---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: チーム アプリ 会議ユーザー参加者ロール API
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565915"
---
# <a name="create-apps-for-teams-meetings"></a>Teams 会議用のアプリを作成する

## <a name="prerequisites-and-considerations"></a>前提条件と考慮事項

Teams会議用のアプリを作成する前に、次の点を理解しておく必要があります。

* Teamsアプリの開発方法に関する知識が必要です。 詳細については、「[アプリ開発Teams」](../overview.md)を参照してください。

* アプリが会議で利用できることを示すには、Teams アプリ マニフェストを更新する必要があります。 詳細については、「アプリ [マニフェスト」を参照してください](#update-your-app-manifest)。

* アプリが会議のライフサイクルでタブとして機能するには、groupchat スコープで構成可能なタブをサポートする必要があります。 詳細については、「 [グループチャットのスコープ](../resources/schema/manifest-schema.md#configurabletabs) と [グループ タブの作成](../build-your-first-app/build-channel-tab.md)」を参照してください。

* 会議前および会議後のシナリオに関する一般的なTeamsタブ設計ガイドラインに従う必要があります。 会議中のエクスペリエンスについては、会議内のタブと会議中のダイアログ の設計ガイドラインを参照してください。 詳細については[、「Teams タブ設計ガイドライン](../tabs/design/tabs.md)、[ミーティングタブ設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)、および[ミーティングダイアログの設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)」を参照してください。

* `groupchat`会議前および会議後のチャットでアプリを有効にするには、スコープをサポートする必要があります。 会議前のアプリエクスペリエンスを使用すると、会議アプリを見つけて追加したり、会議前のタスクを実行したりできます。 会議後のアプリエクスペリエンスを使用すると、アンケート調査結果やフィードバックなど、会議の結果を表示できます。

* 会議 API の URL パラメータには `meetingId` `userId` 、 、および が必要です `tenantId` 。 これらは、クライアント SDK とボットアクティビティTeamsの一部として使用できます。 さらに、 [タブ SSO 認証](../tabs/how-to/authentication/auth-aad-sso.md)を使用して、ユーザー ID とテナント ID の信頼できる情報を取得できます。

* `GetParticipant`認証トークンを生成するには、API にボット登録と ID が必要です。 詳細については、「 [ボットの登録と ID](../build-your-first-app/build-bot.md)」を参照してください。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいて最新の状態にする必要があります。 これらのイベントは、会議のライフサイクル全体で、会議内のダイアログ ボックスやその他のステージ内に含めることができます。 [会議中] ダイアログ ボックスについては、 `bot Id` の完了パラメーターを参照してください `Notification Signal API` 。

## <a name="meeting-apps-api-reference"></a>ミーティング アプリ API リファレンス

|API|説明|要求|ソース|
|---|---|----|---|
|**ユーザーコンテキストを取得します。**| この API を使用すると、コンテキスト情報を取得して、関連するコンテンツをTeamsタブに表示できます。 |_**> { /*..*/ } )**_|クライアント SDK Microsoft Teams|
|**参加者を取得します。**| この API により、ボットはミーティング ID と参加者 ID によって参加者情報を取得できます。 |**GET** _**/v1/会議/{会議Id}/参加者/{参加者Id}?テナントId={テナントId}**_ |Microsoft Bot FrameworkSDK|
|**通知シグナル** | この API を使用すると、ユーザーボットチャット用の既存の会話通知 API を使用して配信される会議信号を提供できます。 会議中のダイアログ ボックスを表示するユーザーアクションに基づいて通知できます。 |**ポスト** _**/v3/会話/{会話Id}/アクティビティ**_|Microsoft Bot FrameworkSDK|

### <a name="getusercontext"></a>ユーザーコンテキストを取得します。

タブコンテンツのコンテキスト情報を識別して取得するには[、「Teamsタブのコンテキストを取得する](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)」を参照してください。`meetingId`は、会議コンテキストで実行しているときにタブによって使用され、応答ペイロードに追加されます。

### <a name="getparticipant-api"></a>参加者の取得 API

> [!NOTE]
> * 会議の開催者はいつでもロールを変更できるため、参加者ロールをキャッシュしないでください。
> * Teamsは現在、API の 350 を超える参加者の大規模な配布リストまたは名簿サイズをサポートしていません `GetParticipant` 。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**ミーティングID**| 文字列 | はい | 会議の識別子は、ボット呼び出しとクライアント SDK Teamsを通じて使用できます。|
|**参加者 ID**| 文字列 | はい | 参加者 ID はユーザー ID です。 タブ SSO、ボット呼び出し、およびクライアント SDK Teamsで使用できます。 タブ SSO から参加者 ID を取得することをお勧めします。 |
|**tenantId**| 文字列 | はい | テナントのユーザーにはテナント ID が必要です。 タブ SSO、ボット呼び出し、およびクライアント SDK Teamsで使用できます。 タブ SSO からテナント ID を取得することをお勧めします。 |

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

API の JSON 応答の本文 `GetParticipant` は次のとおりです。

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
| **403** | アプリは参加者情報を取得できません。 これは最も一般的なエラー応答であり、会議でアプリがインストールされていない場合にトリガーされます。 たとえば、アプリがテナント管理者によって無効にされた場合や、ライブ サイトの移行中にブロックされた場合などです。|
| **200** | 参加者情報が正常に取得されました。|
| **401** | アプリが無効なトークンで応答します。|
| **404** | 会議の期限が切れているか、参加者が見つかりません。|
| **500** | 会議の終了後 60 日以上経過したか、または参加者のロールに基づくアクセス許可がありません。|

### <a name="notificationsignal-api"></a>通知シグナル API

会議のすべてのユーザーは、API を介して送信された通知を受信します `NotificationSignal` 。

> [!NOTE]
> * 会議中のダイアログ ボックスが呼び出されると、コンテンツはチャット メッセージとして表示されます。
> * 現在、対象通知の送信はサポートされていません。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| 文字列 | はい | 会話識別子は、ボット呼び出しの一部として使用できます。 |

#### <a name="example"></a>例

`Bot ID`がマニフェストで宣言され、ボットが結果オブジェクトを受け取ります。

> [!NOTE]
> * の `completionBotId` パラメーター `externalResourceUrl` は、要求されたペイロードの例では省略可能です。 `Bot ID` がマニフェストで宣言され、ボットは結果オブジェクトを受け取ります。
> * `externalResourceUrl`幅と高さのパラメータはピクセル単位である必要があります。 寸法が許可された制限内であることを確認するには、 [設計ガイドライン](design/designing-apps-in-meetings.md)を参照してください。
> * URL は、 `<iframe>` 会議中のダイアログ ボックスに として読み込まれたページです。 ドメインは、アプリ マニフェストのアプリの `validDomains` 配列に含まれる必要があります。

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
| **201** | シグナルのあるアクティビティは正常に送信されます。 |
| **401** | アプリが無効なトークンで応答します。 |
| **403** | アプリは信号を送信できません。 これは、テナント管理者がアプリを無効にしたり、ライブ サイトの移行中にアプリがブロックされるなどのさまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれています。 |
| **404** | 会議チャットが存在しません。 |

## <a name="enable-your-app-for-teams-meetings"></a>Teams会議でアプリを有効にする

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、 、、および 配列を使用してアプリ マニフェストで宣言 `configurableTabs` `scopes` `context` されます。 スコープは、アプリが使用可能な場所を定義するユーザーとコンテキストを定義します。

> [!NOTE]
> マニフェスト [スキーマ](../resources/schema/manifest-schema-dev-preview.md)を使用してアプリ マニフェストを更新してみてください。
> 会議のアプリには *、グループチャット* のスコープが必要です。 *チーム* スコープは、チャネル内のタブでのみ機能します。

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
> `meetingStage` は、現在、開発者プレビューでのみ使用できます。

### <a name="context-property"></a>Context プロパティ

タブ `context` と `scopes` プロパティを使用すると、アプリの表示場所を決定できます。 または スコープ内のタブ `team` `groupchat` には、複数のコンテキストを含めることができます。 値のすべて `context` または一部を使用できるプロパティの値を次に示します。

|値|説明|
|---|---|
| **チャンネルタブ** | チーム チャネルのヘッダーのタブ。 |
| **プライベートチャットタブ** | チームまたは会議のコンテキストにないユーザーのセット間のグループ チャットのヘッダーのタブ。 |
| **ミーティングチャットタブ** | スケジュールされた会議のコンテキストで、グループ チャットのヘッダーのタブ。 |
| **会議の詳細タブ** | 予定表の会議詳細ビューのヘッダーのタブ。 |
| **ミーティングサイドパネル** | 会議中のパネルは、統一されたバー(Uバー)を介して開かれました。 |
| **ミーティングステージ** | サイドパネルのアプリを会議ステージに共有できます。 |

> [!NOTE]
> `Context` プロパティは、現在、モバイル クライアントではサポートされていません。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

> [!NOTE]
> * アプリをタブ ギャラリーに表示するには、構成可能なタブとグループ チャットのスコープをサポートする必要があります。
> * モバイル クライアントは、会議の前後のステージでのみタブをサポートします。
> * 会議内のダイアログ ボックスおよびタブは、現在、モバイル クライアントではサポートされていません。 詳細については、 [モバイル用のタブを作成する際のモバイルの](../tabs/design/tabs-mobile.md) タブのガイダンスを参照してください。

### <a name="before-a-meeting"></a>会議の前に

会議の前に、ユーザーはタブ、ボット、およびメッセージング拡張機能を会議に追加できます。 開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。

**会議にタブを追加するには**

1. カレンダーで、タブを追加する会議を選択します。
1. [ **詳細** ] タブを選択し、[+ ] <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. タブ ギャラリーが表示されます。

    ![事前会議の経験](../assets/images/apps-in-meetings/PreMeeting.png)

1. タブ ギャラリーで、追加するアプリを選択し、必要に応じて手順を実行します。 アプリはタブとしてインストールされます。
    > [!NOTE] 
    > 現在、[会議] タブでは、会議の詳細と参加者の情報を取得することはサポートされていません。

**会議にメッセージ拡張機能を追加するには**

1. チャットのメッセージ作成領域にある省略記号またはオーバーフロー メニュー &#x25CF;&#x25CF;&#x25CF; を選択します。
1. 追加するアプリを選択し、必要に応じて手順を実行します。 アプリは、メッセージング拡張機能としてインストールされます。

**会議にボットを追加するには**

会議チャットでキーを入力 **@** し、[ **ボットの取得**] を選択します。

> [!NOTE]
> * ユーザー ID は [、タブ SSO](../tabs/how-to/authentication/auth-aad-sso.md)を使用して確認する必要があります。 認証後、アプリは API を使用してユーザー ロールを取得できます `GetParticipant` 。
> * ユーザー ロールに基づいて、アプリはロール固有のエクスペリエンスを提供する機能を持ちます。 たとえば、ポーリング アプリでは、主催者と発表者のみが新しいポーリングを作成できます。
> * 会議の進行中にロールの割り当てを変更できます。 詳細については、「 [Teams会議でのロール](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。

### <a name="during-a-meeting"></a>会議中

#### <a name="sidepanel"></a>サイドパネル

サイドパネルを使用すると、開催者と発表者がさまざまなビューとアクションを持つことができる会議のエクスペリエンスをカスタマイズできます。 アプリ マニフェストで、コンテキスト配列に sidePanel を追加する必要があります。 会議とすべてのシナリオで、アプリは、幅 320 ピクセルの会議内タブでレンダリングされます。 詳細については、「 [フレーム コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)」を参照してください。

API を使用 `userContext` して要求をルーティングするには[、「sdk Teams」](../tabs/how-to/access-teams-context.md#user-context)を参照してください。 [タブTeams認証フローを](../tabs/how-to/authentication/auth-flow-tab.md)参照してください。 タブの認証フローは、Web サイトの認証フローとよく似ています。 したがって、タブは OAuth 2.0 を直接使用できます。 [Microsoft ID プラットフォームと OAuth 2.0 の認証コード フロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow)を参照してください。

メッセージング拡張機能は、ユーザーが会議内ビューに表示され、ユーザーがメッセージの拡張カードを作成する投稿を行う場合に、期待どおりに動作します。 会議内の AppName は、会議中のアプリ名を示すツールヒントです。

> [!NOTE]
> バージョン 1.7.0 以上の[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用する前のバージョンではサイド パネルがサポートされていません。

#### <a name="in-meeting-dialog"></a>会議中ダイアログ

会議中のダイアログ ボックスを使用して、ミーティング中に参加者を参加させ、会議中に情報やフィードバックを収集できます。 API [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) を使用して、バブル通知をトリガーする必要があることを通知します。 通知要求ペイロードの一部として、表示されるコンテンツがホストされている URL を含めます。

会議内ダイアログでは、タスク モジュールを使用しないでください。 タスク モジュールは、会議チャットでは呼び出されません。 外部リソース URL は、会議でコンテンツ バブルを表示するために使用されます。 このメソッドを使用 `submitTask` して、会議チャットでデータを送信できます。

> [!NOTE]
> * ユーザーが Web ビューでアクションを実行した後に自動的に終了するには [、submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出す必要があります。 これはアプリの申請に必要な要件です。 詳細については、「 [SDK タスク モジュールTeams」](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)を参照してください。
> * アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、 `from.id` `from` 要求メタデータではなく、オブジェクト内の要求メタデータに依存する必要があります `from.aadObjectId` 。 `from.id`はユーザー ID であり `from.aadObjectId` 、ユーザーの Azure Active Directory (AAD) ID です。 詳細については、 [タブでのタスクモジュールの使用](../task-modules-and-cards/task-modules/task-modules-tabs.md) および [タスクモジュールの作成と送信を](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)参照してください。

#### <a name="share-to-stage"></a>ステージ間で共有 

> [!NOTE]
> * この機能は、現在、開発者プレビューでのみ使用できます。
> * この機能を使用するには、アプリがミーティング中のサイドパネルをサポートしている必要があります。


この機能により、開発者は会議の段階でアプリを共有できます。 ミーティングのステージで共有を有効にすると、ミーティング参加者はリアルタイムで共同作業を行うことができます。 

必要なコンテキストは `meetingStage` 、アプリ マニフェストにあります。 この場合の前提条件は、コンテキストを持つ `meetingSidePanel` ためです。 これにより、次の図に示すように、サイドパネルの **[共有** ] ボタンが有効になります。

  ![share_to_stage_during_meeting経験](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

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

会議後と会議前の構成は同じです。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| 会議の機能拡張 | トークンを渡すための会議の機能拡張サンプルをMicrosoft Teamsします。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| ミーティング コンテンツ バブル ボット | Microsoft Teams会議でコンテンツ バブル ボットと対話するための会議機能拡張サンプルです。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| ミーティングサイドパネル | Microsoft Teams会議中のサイド パネルで反復処理を行うための会議の機能拡張サンプルです。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a>関連項目

* [会議中のダイアログデザインガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [タブのTeams認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
