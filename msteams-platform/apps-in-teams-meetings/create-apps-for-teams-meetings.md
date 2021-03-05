---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール API
ms.openlocfilehash: bd0f53ae34a23bdbbdc2e6f3992c7dd0836e9f28
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449494"
---
# <a name="create-apps-for-teams-meetings"></a>Teams 会議用のアプリを作成する

## <a name="prerequisites-and-considerations"></a>前提条件と考慮事項

* 会議のアプリには、Teams アプリ開発に関する基本的 [な知識が必要です](../overview.md)。 会議内のアプリは、タブ、[](../tabs/what-are-tabs.md)ボット、[](../bots/what-are-bots.md)メッセージング拡張機能の機能[](../messaging-extensions/what-are-messaging-extensions.md)で構成され、アプリが会議で使用できるかどうかを示すために[Teams](#update-your-app-manifest)アプリ マニフェストの更新が必要になります。

* アプリが会議のライフサイクルでタブとして機能するには [、groupchat](../resources/schema/manifest-schema.md#configurabletabs) スコープで構成可能なタブをサポートする必要があります (「グループ タブを作成する方法」 [を参照](../build-your-first-app/build-channel-tab.md))。 スコープを `groupchat` サポートすると、会議前および[](teams-apps-in-meetings.md#pre-meeting-app-experience)会議後のチャットで[アプリを](teams-apps-in-meetings.md#post-meeting-app-experience)有効にできます。

* 会議 API の URL パラメーターには、Teams クライアント SDK とボット アクティビティの一部として使用できる 、、 `meetingId` `userId` および [tenantId](/onedrive/find-your-office-365-tenant-id) が必要な場合があります。 さらに、ユーザー ID とテナント ID の信頼できる情報は、Tab SSO 認証を使用 [して取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 会議 API の中には、認証トークンを生成するためにボット登録と `GetParticipant` [ID](../build-your-first-app/build-bot.md) が必要な場合があります。

* 会議前および会議後のシナリオでは、一般的な [Teams](../tabs/design/tabs.md) タブ設計ガイドラインに従う必要があります。 会議中のエクスペリエンスについては、「会議内タブ」と [「](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) 会議内ダイアログ [の設計ガイドライン」を](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) 参照してください。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。 これらのイベントは、会議中のダイアログ (完了パラメーターを参照) 内に含め、会議のライフサイクル全体にわたって他 `bot Id` `Notification Signal API` のサーフェスを使用できます。

## <a name="meeting-apps-api-reference"></a>会議アプリ API リファレンス

|API|説明|要求|ソース|
|---|---|----|---|
|**GetUserContext**| 関連するコンテンツを Teams タブに表示するコンテキスト情報を取得します。 |_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_|Microsoft Teams クライアント SDK|
|**GetParticipant**|この API を使用すると、ボットは会議 ID と参加者 ID によって参加者情報をフェッチできます。|**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |会議シグナルは、次の既存の会話通知 API (ユーザー ボット チャット用) を使用して配信されます。 この API を使用すると、開発者はエンド ユーザー のアクションに基づいて、会議中のダイアログ バブルを表示できます。|**POST** _**/v3/conversation/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

タブ コンテンツのコンテキスト情報の特定と取得に関するガイダンスについては [、Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) タブドキュメントのコンテキストの取得を参照してください。 会議の機能拡張の一環として、応答ペイロードに新しい値が追加されました。

✔ **meetingId**: 会議コンテキストで実行するときにタブによって使用されます。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * 会議開催者は任意の時点で役割を変更できるので、参加者の役割をキャッシュしない。
>
> * Teams は現在、API の大きな配布リストや 350 人を超える参加者の名簿サイズをサポート `GetParticipant` していない。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| 文字列 | はい | 会議識別子は、ボットの呼び出しと Teams クライアント SDK を使用して使用できます。|
|**participantId**| 文字列 | はい | participantId はユーザー ID です。 これは、Tab SSO、Bot Invoke、Teams クライアント SDK で使用できます。 Tab SSO から参加者 Id を取得することを強くお勧めします。 |
|**tenantId**| 文字列 | はい | テナント ユーザーには tenantId が必要です。 これは、Tab SSO、Bot Invoke、Teams クライアント SDK で使用できます。 Tab SSO から tenantId を取得することを強くお勧めします。 |

#### <a name="example"></a>例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
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

応答本文は次の場合です。

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

* * *

#### <a name="response-codes"></a>応答コード

* **403**: アプリで参加者情報を取得できない。 これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。 たとえば、テナント管理者がアプリを無効にした場合や、生活者の軽減中にブロックされている場合などです。
* **200**: 参加者情報が正常に取得されました。
* **401**: トークンが無効です。
* **404**: 参加者が見つかりません。
* **500**: 会議の有効期限が切れているか (会議が終了して 60 日を超える) か、参加者が自分の役割に基づいてアクセス許可を持っていません。


**近日公開**

* **404**: 会議の有効期限が切れているか、参加者が見つかりません。


### <a name="notificationsignal-api"></a>NotificationSignal API

会議のすべてのユーザーは、NotificationSignal API を介して送信された通知を受け取ります。

> [!NOTE]
> 現在、ターゲット通知の送信はサポートされていません。
> 会議中のダイアログが呼び出されると、同じコンテンツもチャット メッセージとして表示されます。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| 文字列 | はい | 会話識別子は、ボットの呼び出しの一部として使用できます。 |

#### <a name="example"></a>例

は `Bot ID` マニフェストで宣言され、ボットは結果オブジェクトを受け取ります。 次の例では、要求 `completionBotId` されたペイロードのパラメーター `externalResourceUrl` は省略可能です。

> [!NOTE]
> * 幅 `externalResourceUrl` と高さのパラメーターはピクセル単位である必要があります。 寸法が許容される制限内にあるか確認するには、「設計ガイドライン [」を参照してください](design/designing-apps-in-meetings.md)。
> * URL は、会議内ダイアログに表示 `<iframe>` されるページです。 ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列にある必要があります。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

* **201**: シグナルを含むアクティビティが正常に送信されます。 
* **401**: トークンが無効です。
* **403**: アプリが信号を送信できません。 これは、テナント管理者がアプリを無効にし、アプリがライブ サイトの移行中にブロックされるなど、さまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれています。 
* **404**: 会議チャットが存在しません。
 

## <a name="enable-your-app-for-teams-meetings"></a>Teams 会議でアプリを有効にする

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、構成可能な **Tabs** スコープとコンテキスト配列を使用してアプリ マニフェスト  ->  **で****宣言** されます。 *スコープ* は、アプリ *を使用できる* 場所を定義するユーザーとコンテキストを定義します。

> [!NOTE]
> アプリ マニフェストで [Developer Previewマニフェスト スキーマ](../resources/schema/manifest-schema-dev-preview.md) を使用してください。

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
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a>Context プロパティ

タブと `context` プロパティ `scopes` は調和して機能し、アプリを表示する場所を決定できます。 またはスコープ内 `team` のタブ `groupchat` には、複数のコンテキストを指定できます。 context プロパティで使用できる値は次のとおりです。

* **channelTab**: チーム チャネルのヘッダー内のタブ。
* **privateChatTab**: チームや会議のコンテキストではない一連のユーザー間のグループ チャットのヘッダー内のタブ。
* **meetingChatTab**: スケジュールされた会議のコンテキスト内の一連のユーザー間のグループ チャットのヘッダー内のタブ。
* **meetingDetailsTab:** 予定表の会議の詳細ビューのヘッダーにあるタブ。
* **meetingSidePanel**: 統合バー (u-bar) を介して開いた会議内パネル。

> [!NOTE]
> "Context" プロパティは現在サポートされていないので、モバイル クライアントでは無視されます

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

> [!NOTE]
> * タブ ギャラリーにアプリを表示するには、構成可能なタブとグループ チャット **スコープをサポート****する必要があります**。
>
> * モバイル クライアントは、会議表面の事前および投稿でのみタブをサポートします。 モバイルでの会議中のエクスペリエンス (会議中のダイアログとタブ) は近日公開されます。 モバイル用 [のタブを作成する場合は、モバイル](../tabs/design/tabs-mobile.md) 上のタブのガイダンスに従います。

### <a name="before-a-meeting"></a>会議の前に

開催者または発表者の役割を持つユーザーは、会議チャットと会議の詳細ページのプラス ➕ボタンを使用して、会議にタブ **を追加** します。 メッセージング拡張機能は、チャット内のメッセージの作成領域 &#x25CF;&#x25CF;&#x25CF; 下にある省略記号/オーバーフロー メニューを介して追加されます。 "" キーを使用して [ボットの取得] を選択すると、ボット **@** が会議チャット **に追加されます**。

✔ユーザー ID は *、Tabs* SSO を介して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。 この認証の後、アプリは GetParticipant API を介してユーザー ロールを取得できます。

 ✔ユーザー ロールに基づいて、アプリはロール固有のエクスペリエンスを表示する機能を持つ必要があります。 たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。

> **メモ**: 役割の割り当ては、会議の進行中に変更できます。  *「Teams* [会議での役割」を参照してください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。 

### <a name="during-a-meeting"></a>会議中

#### <a name="sidepanel"></a>**sidePanel**

✔ アプリ マニフェストで、前述のようにコンテキスト配列に **sidePanel** を追加します。 

✔ 会議だけでなく、すべてのシナリオで、アプリは幅が 320px の会議内タブに表示されます。 このためにタブを最適化する必要があります。 *「FrameContext*[インターフェイス」を参照してください。](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔に応じて要求をルーティングするために **userContext** API を使用するために [Teams SDK](../tabs/how-to/access-teams-context.md#user-context)に参照します。

✔タブについては [、「Teams 認証フロー」を参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。 タブの認証フローは、Web サイトの認証フローと非常に似ています。 したがって、タブは OAuth 2.0 を直接使用できます。 *「Microsoft* [IDENTITY プラットフォーム」および「OAuth 2.0 承認コード フロー」も参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

✔メッセージ拡張機能は、ユーザーが会議内ビューに表示され、メッセージ内線カードの作成を投稿できる場合に期待通り機能する必要があります。

✔ AppName の会議中 - ツールヒントに、会議内のアプリ名の U バーが表示されます。

#### <a name="in-meeting-dialog"></a>**会議中ダイアログ**

✔会議中のダイアログデザインガイドライン [に従う必要があります](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

✔タブについては [、「Teams 認証フロー」を参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。

✔ [NotificationSignal API を](create-apps-for-teams-meetings.md#notificationsignal-api) 使用して、バブル通知をトリガーする必要があるという通知を送信します。

✔通知要求ペイロードの一部として、紹介するコンテンツがホストされている URL を含める。

✔会議中のダイアログでは、タスク モジュールを使用することはできません。

> [!NOTE]
>
> * これらの通知は、自然の中で永続的です。 ユーザーが Web ビューでアクションを実行した後 [**、submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動終了する必要があります。 これは、アプリの申請に必要な要件です。 *「Teams* [SDK: タスク モジュール」も参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
>
> * アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、オブジェクト内の (ユーザーの ID) 要求メタデータに依存する必要があります。(ユーザーの `from.id` `from` Azure Active Directory `from.aadObjectId` ID) 要求メタデータは使用しない必要があります。 *「タブ*[でのタスク モジュールの使用」および「](../task-modules-and-cards/task-modules/task-modules-tabs.md)[タスク モジュールの作成と送信」を参照してください](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="after-a-meeting"></a>会議の後

会議後と会議前の構成は同等です。

## <a name="meeting-app-sample"></a>会議アプリのサンプル

 > [!div class="nextstepaction"]
> [会議トークンジェネレーター アプリ](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
