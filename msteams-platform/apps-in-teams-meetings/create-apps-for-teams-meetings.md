---
title: Teams 会議用のアプリを作成する
author: laujan
description: teams 会議用のアプリを作成する
ms.topic: conceptual
ms.author: lajanuar
keywords: teams アプリ会議ユーザー参加者ロール api
ms.openlocfilehash: a086050b7cdef671fcbd187b68d707280e8df359
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605232"
---
# <a name="create-apps-for-teams-meetings"></a>Teams 会議用のアプリを作成する

## <a name="prerequisites-and-considerations"></a>前提条件と考慮事項

1. 会議のアプリには、 [Teams アプリ開発](../overview.md)に関する基本的な知識が必要です。 会議のアプリは、 [タブ](../tabs/what-are-tabs.md)、 [ボット](../bots/what-are-bots.md)、および [メッセージングの拡張](../messaging-extensions/what-are-messaging-extensions.md) 機能で構成され、Teams アプリの [マニフェスト](#update-your-app-manifest) を更新して、アプリが会議で利用できることを示す必要があります。

1. アプリが会議のライフサイクルでタブとして機能するには、 [groupchat スコープ](../resources/schema/manifest-schema.md#configurabletabs)で構成可能なタブをサポートする必要があります。 *「* [カスタムタブを使用して Teams アプリを拡張する](../tabs/how-to/add-tab.md)」を参照してください。スコープをサポートすること `groupchat` で、 [プレミーティング](teams-apps-in-meetings.md#pre-meeting-app-experience) および [ミーティング後](teams-apps-in-meetings.md#post-meeting-app-experience) のチャットでアプリを有効にすることができます。

1. ミーティング API URL パラメーターには、、が必要な場合があり `meetingId` `userId` ます。また、 [TenantId](/onedrive/find-your-office-365-tenant-id) は Teams クライアント SDK および bot アクティビティの一部として使用できます。 さらに、 [TAB SSO 認証](../tabs/how-to/authentication/auth-aad-sso.md)を使用して、ユーザー id とテナント id の信頼できる情報を取得できます。

1. などの一部の会議 Api で `GetParticipant` は、 [ボット登録と BOT アプリ ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) が認証トークンを生成する必要があります。

1. 開発者は、teams の会議中にトリガー[される会議](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)中のダイアログに加えて、会議前およびミーティング後のシナリオについて、teams の一般的な[タブデザインガイドライン](../tabs/design/tabs.md)に従う必要があります。

1. アプリをリアルタイムで更新するためには、会議のイベントアクティビティに基づいて最新の状態になっている必要があります。 これらのイベントは、会議中のダイアログ (の「完了パラメーター」を参照してください `bot Id` `Notification Signal API` ) および会議ライフサイクル全体のその他のサーフェス内に存在することができます。

## <a name="meeting-apps-api-reference"></a>会議アプリ API リファレンス

|API|説明|要求|ソース|
|---|---|----|---|
|**GetUserContext**| 関連するコンテンツを Teams タブに表示するためのコンテキスト情報を取得します。 |_**getContext (() => {/*...*/ } )**_|Microsoft Teams クライアント SDK|
|**GetParticipant**|この API を使用すると、ボットはミーティング id と参加者 id で参加者情報を取得できます。|/V1/meetings/{meetingId}/participants/{participantId} を **取得** する ( _**tenantid** )_ |Microsoft Bot フレームワーク SDK|
|**NotificationSignal** |ミーティング信号は、次の既存の会話通知 API を使用して配信されます (ユーザーのためのチャット)。 この API を使用すると、開発者はエンドユーザーのアクションに基づいて、会議中のダイアログで通知を表示することができます。|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot フレームワーク SDK|

### <a name="getusercontext"></a>GetUserContext

タブコンテンツのコンテキスト情報を識別して取得するためのガイダンスについては、「 [Teams のコンテキストの取得」タブ](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) のドキュメントを参照してください。 会議機能拡張の一部として、応答ペイロードに新しい値が追加されました。

✔の会議 **id**: 会議のコンテキストで実行している場合にタブで使用されます。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * 会議の開催者はいつでも役割を変更できるため、参加者の役割をキャッシュしないでください。
>
> * 現時点では、Teams は、API のために350以上の参加者の大きな配布リストまたは名簿サイズをサポートしていません `GetParticipant` 。
>
> * Bot Framework SDK のサポートは近日に予定されています。


#### <a name="request"></a>要求

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

[Bot フレームワーク API リファレンス](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)を *参照してください*。

<!-- markdownlint-disable MD025 -->

**C# の例**

```csharp
   // Get role for the user who sent a message to your bot
   var senderRole = await TeamsInfo.GetMeetingParticipantAsync(turnContext);
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**meetingId**| 文字列 | はい | 会議識別子は、ボット Invoke および Teams クライアント SDK を介して利用できます。|
|**participantId**| 文字列 | はい | このフィールドはユーザー ID であり、タブ SSO、Bot 呼び出し、Teams クライアント SDK で使用できます。 タブ SSO を強くお勧めします。|
|**tenantId**| 文字列 | はい | これは、テナントのユーザーに必要です。 これは、タブ SSO、Bot 呼び出し、Teams クライアント SDK で利用できます。 タブ SSO を強くお勧めします。|

#### <a name="response-payload"></a>応答ペイロード
<!-- markdownlint-disable MD036 -->

[ミーティング] の下の **役割** は、*開催者*、*発表者*、または *出席* 者になることができます。

**例 1**

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name":"Allan Deyoung",
      "givenName":"Allan",
      "surname":"Deyoung",
      "email":"Allan.Deyoung@microsoft.com",
      "userPrincipalName":"Allan.Deyoung@microsoft.com",
      "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
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

**403**: アプリは、参加者情報を取得することを許可されていません。 これは、最も一般的なエラー応答であり、アプリがテナント管理者によって無効にされた場合や、ライブサイトの移行中にブロックされた場合など、会議にインストールされていない場合にトリガーされます。  
**200**: 参加者情報が正常に取得されました。  
**401**: 無効なトークンです。  
**404**: 参加者が見つかりません。 
**500**: 会議は有効期限が切れています (会議が終了してからの経過期間は60日を超えています)。または、参加者が役割に基づいてアクセス許可を持っていません。

**近日公開**

**404**: 会議の有効期限が切れているか、参加者が見つかりません。 

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> 会議中のダイアログが呼び出されると、同じコンテンツがチャットメッセージとして表示されることもあります。

#### <a name="request"></a>要求

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a>クエリ パラメーター

|値|型|必須|説明|
|---|---|----|---|
|**conversationId**| 文字列 | はい | 会話 id は bot 呼び出しの一部として使用できます。 |

#### <a name="request-payload"></a>要求のペイロード

> [!NOTE]
>
> *  次に示す要求されたペイロードで `completionBotId` は、のパラメーター `externalResourceUrl` は省略可能です。 これは、 `Bot ID` マニフェストで宣言されているです。 Bot は result オブジェクトを受け取ります。
> * ExternalResourceUrl の幅と高さのパラメーターは、ピクセル単位でなければなりません。 ディメンションが許容範囲内にあることを確認するには、 [設計ガイドライン](design/designing-apps-in-meetings.md) を参照してください。
> * URL は、 `<iframe>` [会議中] ダイアログボックスの内側に読み込まれるページです。 URL のドメインは、アプリのマニフェストのアプリの配列に含まれている必要があり `validDomains` ます。


# <a name="json"></a>[JSON](#tab/json)

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

* * *

> [!IMPORTANT]
> コンテンツバブル (taskInfo URL) 内の URL は、Teams アプリマニフェストに含まれている [有効なドメイン](../resources/schema/manifest-schema.md#validdomains) の一覧に含まれている必要があります。

#### <a name="response-codes"></a>応答コード

**201**: シグナルが正常に送信されたアクティビティ  
**401**: 無効なトークン  
**403**: アプリは、シグナルを送信することを許可されていません。 この場合、ペイロードに詳細なエラーメッセージが含まれている必要があります。 多くの理由が考えられます。これは、テナント管理者によって無効にされたアプリ、運用サイトの移行中にブロックされたなどです。  
**404**: 会議チャットが存在しません  

## <a name="enable-your-app-for-teams-meetings"></a>Teams 会議でアプリを有効にする

### <a name="update-your-app-manifest"></a>アプリのマニフェストを更新する

ミーティングアプリの機能は、[アプリケーションマニフェスト] の [セキュリティの定義]**タブ**  ->  **スコープ** と **コンテキスト** 配列を使用して宣言されています。 *スコープ* は、アプリが使用可能になる場所と *コンテキスト* を定義します。

> [!NOTE]
> * [開発者プレビューマニフェストスキーマ](../resources/schema/manifest-schema-dev-preview.md)を使用して、アプリマニフェストでこれを試してください。

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

Tab `context` およびプロパティは、 `scopes` アプリを表示する場所を決定できるようにするために、ハーモニーで機能します。 またはの範囲内のタブに `team` は、 `groupchat` 複数のコンテキストを含めることができます。 Context プロパティに指定できる値は次のとおりです。

* [ **Channeltab タブ**: チームチャネルのヘッダーのタブ。
* **privateChatTab**: チームまたは会議のコンテキストではないユーザーのセット間のグループチャットのヘッダーにあるタブ。
* **meetingChatTab**: 予約された会議のコンテキスト内のユーザーのセット間のグループチャットのヘッダーにあるタブ。
* [会議詳細]**タブ: 予定** 表の会議の詳細ビューのヘッダーにあるタブ。
* 会議の **sidepanel**: 統合バー (u バー) によって開かれた会議中のパネル。

> [!NOTE]
> "Context" プロパティは現在サポートされていないため、モバイルクライアントでは無視されます。

## <a name="configure-your-app-for-meeting-scenarios"></a>アプリを構成してシナリオをミーティングする

> [!NOTE]
> * アプリケーションがタブギャラリーに表示されるようにするには、 **構成可能なタブ** と **グループチャットスコープ** をサポートする必要があります。
>
> * モバイルクライアントは、会議のプレおよびポストの表面でのみタブをサポートします。 モバイルの会議中のエクスペリエンス (会議中のダイアログおよびタブ) は近日中に利用可能になります。 モバイル用のタブを作成するときに、 [[モバイル] のタブのガイダンス](../tabs/design/tabs-mobile.md) に従ってください。

### <a name="before-a-meeting"></a>会議の前

開催者または発表者の役割を持つユーザーは、会議 **チャット** および会議の **詳細** ページのプラス➕ボタンを使用して、会議にタブを追加します。 メッセージング拡張機能は、[会話の作成メッセージ] 領域の下にある [楕円/オーバーフロー] メニュー &#x25CF;&#x25CF;&#x25CF; 経由で追加されます。 Bot は、"" キーを使用して会議チャットに追加され、[ **@** **ボットを取得**] を選択します。

ユーザー id は、[タブ SSO](../tabs/how-to/authentication/auth-aad-sso.md)を使用して確認する *必要があり*✔。 この認証の後、アプリは GetParticipant API を使用してユーザーロールを取得できます。

 ✔ユーザーの役割に基づいて、アプリに役割固有のエクスペリエンスを提供する機能が用意されました。 たとえば、投票アプリでは、開催者と発表者のみが新しい投票を作成できるようにすることができます。

> **注**: 役割の割り当ては、会議の進行中に変更できます。  *「* [Teams Meeting の役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。 

### <a name="during-a-meeting"></a>会議中

#### <a name="sidepanel"></a>**sidePanel**

アプリマニフェスト内の✔前述のように、**コンテキスト** 配列に **sidepanel** を追加します。

会議の✔とすべてのシナリオにおいて、アプリは、ため320px ですの幅で表示される [会議中] タブに表示されます。 このためにタブを最適化する必要があります。 *参照*、 [framecontext インターフェイス](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

**UserContext** API を使用して要求を適切にルーティングするには、 [Teams SDK](../tabs/how-to/access-teams-context.md#user-context)を参照してください✔。

✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。 タブの認証フローは、web サイトの認証フローとよく似ています。 そのため、タブは OAuth 2.0 を直接使用できます。 「 [Microsoft identity platform And OAuth 2.0 認証コードフロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow) *」も参照して* ください。

ユーザーが会議中のビューを使用していて、作成のメッセージ拡張カードを投稿できるようにするには、✔メッセージ拡張子が期待どおりに機能する必要があります。

[会議中のアプリケーション名を指定してください✔の場合は、会議の U バーでアプリ名を指定する必要があります。

#### <a name="in-meeting-dialog"></a>**会議中ダイアログ**

✔ [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)に従う必要があります。

✔ [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)を参照してください。

✔ [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API を使用して、バブル通知がトリガーされる必要があることを通知します。

✔通知要求のペイロードの一部として、紹介するコンテンツがホストされる URL を含めます。

会議中のダイアログ✔は、タスクモジュールを使用できません。

> [!NOTE]
>
> * これらの通知は、本質的に永続的なものです。 ユーザーが web ビューでアクションを実行した後に、 [**Submittask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出して自動消去する必要があります。 これは、アプリを送信するための要件です。 「 [TEAMS SDK: タスクモジュール](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true) *」も参照してください*。
>
> * アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求のペイロードは、( `from.id` `from` `from.aadObjectId` ユーザーの AZURE Active Directory ID) 要求メタデータではなく、オブジェクト内の (ユーザーの ID) 要求メタデータに依存している必要があります。 *「* [タスクモジュールを使用して](../task-modules-and-cards/task-modules/task-modules-tabs.md) タスク [モジュールを作成し、送信](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)する」を参照してください。

### <a name="after-a-meeting"></a>会議の後

ポストミーティングと事前会議の構成は同等です。

## <a name="meeting-app-sample"></a>会議アプリのサンプル

 > [!div class="nextstepaction"]
> [会議トークン生成アプリ](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
