---
title: Teams 会議用のアプリを作成する
author: laujan
description: チーム会議用アプリの作成
ms.topic: conceptual
ms.author: lajanuar
keywords: Teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: 7f6d8fec735aa21033c6bcb2462c20458634f10a
ms.sourcegitcommit: 843da1730443ff8474a05295f60a6b376ed140da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "50073097"
---
# <a name="create-apps-for-teams-meetings"></a>Teams 会議用のアプリを作成する

## <a name="prerequisites-and-considerations"></a>前提条件と考慮事項

* 会議のアプリには、Teams アプリ開発に関する基本的な [知識が必要です](../overview.md)。 会議内のアプリは、タブ、[](../tabs/what-are-tabs.md)ボット、[](../bots/what-are-bots.md)メッセージング拡張機能の機能[](../messaging-extensions/what-are-messaging-extensions.md)で構成できます。また[、Teams](#update-your-app-manifest)アプリ マニフェストを更新して、アプリが会議で利用できる状態を示す必要があります。

* アプリをタブとして会議のライフサイクルで機能するには、 [グループ](../resources/schema/manifest-schema.md#configurabletabs) チャット スコープで構成可能なタブをサポートする必要があります (グループ タブを作成する方法 [を参照してください](../build-your-first-app/build-channel-tab.md))。 スコープを `groupchat` サポートすると、会議前および[](teams-apps-in-meetings.md#pre-meeting-app-experience)会議後のチャット[でアプリを](teams-apps-in-meetings.md#post-meeting-app-experience)有効にできます。

* 会議 API URL パラメーターには、必要な場合があります。tenantId これらは、Teams クライアント SDK およびボット アクティビティの一 `meetingId` `userId` 部として利用できます。 [](/onedrive/find-your-office-365-tenant-id) さらに、タブ SSO 認証を使用して、ユーザー ID とテナント ID の信頼性の高い [情報を取得できます](../tabs/how-to/authentication/auth-aad-sso.md)。

* 会議 API の中には、認証トークンを生成するためにボット登録と `GetParticipant` [ID](../build-your-first-app/build-bot.md) が必要な場合があります。

* 会議前および会議後の [シナリオでは、Teams タブの設計](../tabs/design/tabs.md) に関する一般的なガイドラインに従う必要があります。 会議中のエクスペリエンスについては、 [会議内タブ](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) と会議内ダイアログ [の](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) 設計ガイドラインを参照してください。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。 これらのイベントは、会議のライフサイクル全体にわたって、会議内ダイアログ (完了パラメーターを参照) 内に含め、その他 `bot Id` `Notification Signal API` のサーフェスにできます。

## <a name="meeting-apps-api-reference"></a>会議アプリ API リファレンス

|API|説明|要求|Source|
|---|---|----|---|
|**GetUserContext**| 関連するコンテンツを Teams タブに表示するコンテキスト情報を取得します。 |_**microsoftTeams.getContext( ( ) => { /*...*/ } )**_|Microsoft Teams クライアント SDK|
|**GetParticipant**|この API を使用すると、ボットは会議 ID と参加者 ID で参加者情報を取得できます。|**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |会議のシグナルは、次の既存の会話通知 API (ユーザーボット チャット用) を使用して配信されます。 この API を使用すると、開発者はエンドユーザーのアクションに基づいてシグナルを送信し、会議中のダイアログ バブルを表示できます。|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

タブ コンテンツのコンテキスト情報の特定と取得に関するガイダンスについては [、Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) タブのドキュメントのコンテキストの取得を参照してください。 会議の拡張性の一環として、応答ペイロードに新しい値が追加されました。

✔ **meetingId**: 会議コンテキストで実行するときにタブによって使用されます。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * 会議の開催者は任意の時点で役割を変更できるので、参加者の役割をキャッシュに入らない。
>
> * Teams は現在、API の参加者が 350 人を超える大規模な配布リストや名簿サイズをサポート `GetParticipant` していない。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| 文字列 | はい | 会議識別子は、Bot Invoke と Teams クライアント SDK から利用できます。|
|**participantId**| 文字列 | はい | participantId はユーザー ID です。 タブ SSO、ボット呼び出し、および Teams クライアント SDK で利用できます。 Tab SSO から participantId を取得することを強くお勧めします。 |
|**tenantId**| 文字列 | はい | テナント ユーザーには tenantId が必要です。 これは、タブ SSO、ボット呼び出し、および Teams クライアント SDK で利用できます。 Tab SSO から tenantId を取得することを強くお勧めします。 |

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
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

応答本文は次の場所に含されます。

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

* **403**: アプリは、参加者の情報を取得する許可されません。  これは最も一般的なエラー応答であり、アプリが会議にインストールされていない場合にトリガーされます。 たとえば、テナント管理者によってアプリが無効になっている場合や、ライブ サイトの移行中にブロックされた場合です。
* **200**: 参加者の情報が正常に取得されました。
* **401**: 無効なトークンです。
* **404**: 参加者が見つかりません。
* **500**: 会議の有効期限が切れているか (会議の終了から 60 日を超える) か、参加者の役割に基づいてアクセス許可が付与されていない。


**近日公開**

* **404**: 会議の有効期限が切れているか、参加者が見つかりません。


### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> 会議中ダイアログが呼び出されると、同じコンテンツがチャット メッセージとして表示されます。

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| 文字列 | はい | 会話識別子はボット呼び出しの一部として使用できます。 |

#### <a name="example"></a>例

> [!NOTE]
>
要求 `completionBotId` されたペイロードの `externalResourceUrl` 例では、パラメーターは省略可能です。 `Bot ID` がマニフェストで宣言され、ボットが結果オブジェクトを受け取ります。
> * externalResourceUrl の幅と高さのパラメーターはピクセル単位である必要があります。 サイズが [許容される制限](design/designing-apps-in-meetings.md) の範囲内にあるかについては、設計ガイドラインを参照してください。
> * URL は、会議中ダイアログで読 `<iframe>` み込まれたページです。 ドメインは、アプリ マニフェスト内のアプリ `validDomains` の配列に含む必要があります。

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

* **201**: シグナルを含むアクティビティが正常に送信される  
* **401**: 無効なトークン  
* **201**: シグナルを含むアクティビティが正常に送信されます。 
* **401**: 無効なトークンです。
* **403**: アプリは信号を送信できません。 これは、テナント管理者がアプリを無効にし、ライブ サイトの移行中にアプリがブロックされるなどのさまざまな理由で発生する可能性があります。 この場合、ペイロードには詳細なエラー メッセージが含まれます。 
* **404**: 会議チャットが存在しません。
 

## <a name="enable-your-app-for-teams-meetings"></a>Teams 会議用にアプリを有効にする

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は **、configurableTabs** スコープとコンテキスト配列を介してアプリ マニフェスト  ->  で **宣言** されます。 *スコープ* は、アプリを利用できる場所 *を* 定義するユーザーとコンテキストを定義します。

> [!NOTE]
> アプリ マニフェスト [でDeveloper Previewマニフェスト](../resources/schema/manifest-schema-dev-preview.md) スキーマを使用して試してください。

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

タブとプロパティは調和して機能し、アプリを表示する `context` `scopes` 場所を決定できます。 スコープ内の `team` タブ `groupchat` は、複数のコンテキストを持つ場合があります。 コンテキスト プロパティに使用できる値は次のとおりです。

* **channelTab**: チーム チャネルのヘッダー内のタブ。
* **privateChatTab**: チームまたは会議のコンテキスト内に存在しない一連のユーザー間のグループ チャットのヘッダー内のタブ。
* **meetingChatTab**: スケジュールされた会議のコンテキスト内の一連のユーザー間のグループ チャットのヘッダー内のタブ。
* **meetingDetailsTab**: 予定表の会議詳細ビューのヘッダー内のタブ。
* **meetingSidePanel**: 統合バー (u-bar) 経由で開いた会議内パネル。

> [!NOTE]
> "Context" プロパティは現在サポートされていないので、モバイル クライアントでは無視されます。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

> [!NOTE]
> * アプリをタブ ギャラリーに表示するには、構成可能なタブとグループ **チャットスコープ** をサポート **する必要があります**。
>
> * モバイル クライアントは、会議前サーフェスと会議後サーフェスでのみタブをサポートします。 モバイルでの会議中のエクスペリエンス (会議中のダイアログとタブ) は間もなく利用できます。 モバイル用 [のタブを作成する場合は、モバイル](../tabs/design/tabs-mobile.md) のタブのガイダンスに従います。

### <a name="before-a-meeting"></a>会議の前に

開催者または発表者の役割を持つユーザーは、会議チャットおよび会議の詳細ページのプラス ➕ ボタンを使用して、会議に **タブを****追加** します。 メッセージング拡張機能は、チャットのメッセージ作成領域 &#x25CF;&#x25CF;&#x25CF; 下にある省略記号/オーバーフロー メニューを介して追加されます。 ボットは、"" キーを使用して [ボットの取得] を選択して会議 **@** チャット **に追加されます**。

✔は、Tabs SSO *を使用* して確認 [する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。 この認証の後、アプリは GetParticipant API を介してユーザー ロールを取得できます。

 ✔ユーザー ロールに基づいて、アプリはロール固有のエクスペリエンスを表示する機能を備えています。 たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。

> **注**: 会議の進行中は、役割の割り当てを変更できます。  *「Teams* [会議での役割」を参照してください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。 

### <a name="during-a-meeting"></a>会議中

#### <a name="sidepanel"></a>**sidePanel**

✔マニフェストで、上記のようにコンテキスト配列に **sidePanel** を追加します。

✔、すべてのシナリオで、アプリは幅 320 ピクセルの会議内タブにレンダリングされます。 このためには、タブを最適化する必要があります。 *「参照*[」、FrameContext インターフェイス](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔に応じて[、userContext](../tabs/how-to/access-teams-context.md#user-context) API を使用して要求をルーティングするために Teams SDK に参照します。

✔タブの Teams 認証 [フローを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。 タブの認証フローは、Web サイトの認証フローと非常に似ています。 したがって、タブは OAuth 2.0 を直接使用できます。 *Microsoft ID* プラットフォーム [と OAuth 2.0 認証コード フローも参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

✔は、ユーザーが会議中のビューで、作成メッセージの内線カードを投稿できる場合に、期待通り動作する必要があります。

✔ AppName in meeting - ツールヒントには、会議中の U バーにアプリ名が表示されます。

#### <a name="in-meeting-dialog"></a>**会議中ダイアログ**

✔、会議中のダイアログの [設計ガイドラインに従う必要があります](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

✔タブの Teams 認証 [フローを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。

✔ [NotificationSignal API を](create-apps-for-teams-meetings.md#notificationsignal-api) 使用して、バブル通知をトリガーする必要がある場合に通知します。

✔要求ペイロードの一部として、紹介するコンテンツがホストされている URL を含める必要があります。

✔ダイアログでタスク モジュールを使用することはできません。

> [!NOTE]
>
> * これらの通知は、実際には永続的です。 ユーザーが Web ビューでアクションを実行した後 [**、submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動終了する必要があります。 これは、アプリの申請の要件です。 *「Teams* [SDK: タスク モジュール」も参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
>
> * アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、(ユーザーの Azure Active Directory ID) 要求メタデータではなく、オブジェクト内の `from.id` `from` (ユーザーの `from.aadObjectId` ID) 要求メタデータに依存する必要があります。 *「タブ*[でのタスク モジュールの使用」と「](../task-modules-and-cards/task-modules/task-modules-tabs.md)タスク モジュールを作成 [して送信する」を参照してください](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="after-a-meeting"></a>会議後

会議後と会議前の構成は同等です。

## <a name="meeting-app-sample"></a>会議アプリのサンプル

 > [!div class="nextstepaction"]
> [会議トークンジェネレーター アプリ](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
