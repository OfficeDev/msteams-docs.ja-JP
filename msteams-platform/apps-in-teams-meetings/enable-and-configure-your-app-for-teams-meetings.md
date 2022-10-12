---
title: Teams 会議用アプリを有効化して構成する
author: surbhigupta
description: Teams 会議やさまざまな会議シナリオのためのアプリを有効化して構成し、アプリ マニフェストを更新し、機能などを構成する方法について説明します。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: b551513d61e7bb9ab2b9c118f756b3ce5232dde4
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537585"
---
# <a name="enable-and-configure-apps-for-meetings"></a>会議用アプリを有効にして構成する

それぞれのチームには、コミュニケーションとタスクの共同作業を行うそれぞれの方法があります。 これらのさまざまなタスクを達成するために、会議用アプリを使用して Teams をカスタマイズします。 Teams 会議用アプリを有効にし、アプリ マニフェスト内の会議スコープで使用できるようにアプリを構成します。

## <a name="prerequisites"></a>前提条件

Teams 会議用アプリを使用すると、アプリの機能を会議のライフサイクル全体に拡張できます。 Teams 会議用アプリで作業する前に、次の前提条件を満たす必要があります。

* Teams アプリを開発する方法について理解します。 Teams アプリを開発する方法の詳細については、「[Teams アプリの開発](../overview.md)」を参照してください。

* groupchat またはチーム スコープで構成可能なタブをサポートするアプリを使用します。 詳細については、 [スコープ](../resources/schema/manifest-schema.md#configurabletabs) を参照し、 [最初のタブ アプリをビルドします](../build-your-first-app/build-channel-tab.md)。

* 会議前後のシナリオのための一般的な [Teams タブ デザイン ガイドライン](../tabs/design/tabs.md)に準拠している必要があります。 会議中のエクスペリエンスについては、「[[会議内] タブの設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)」および「[会議中ダイアログの設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)」を参照してください。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいて最新の状態にする必要があります。 これらのイベントは、会議のライフサイクル全体で、会議内ダイアログやその他のステージ内に含めることができます。 会議内ダイアログについては、「[会議中の通知ペイロード](API-references.md#send-an-in-meeting-notification)」で `completionBotId` パラメーターを参照してください。

## <a name="enable-your-app-for-teams-meetings"></a>Teams 会議用アプリを有効にする

Teams 会議用アプリを有効にするには、アプリ マニフェストを更新し、コンテキスト プロパティを使用してアプリの表示場所を決定します。

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、`configurableTabs`、`scopes`、`context` 配列を使用して、アプリ マニフェストで宣言されます。 スコープはアクセスできるユーザーを定義し、コンテキストはアプリを使用できる場所を定義します。

> [!NOTE]
>
> * 会議のアプリでは、必要またはスコープが必要 `groupchat` です `team` 。 スコープは `team` 、チャネルまたはチャネル会議のタブに対して機能します。
> * スケジュールされたチャネル会議でのタブの追加をサポートするには、アプリ マニフェストのスコープ セクションで **チーム** **スコープ** を指定します。 **チーム** スコープがない場合、アプリはチャネル会議のポップアップに表示されません。
> * 会議のアプリでは、次のコンテキストを使用できます: `meetingChatTab`、`meetingDetailsTab`、`meetingSidePanel`、`meetingStage`。
> * 委任された RSC のアクセス許可 `MeetingStage.Write.Chat` であり、 `ChannelMeetingStage.Write.Group` 会議ステージの共有を有効にするためにマニフェストに必要です。

次のコード スニペットは、Teams 会議のアプリで使用される構成可能なタブの例です。

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

### <a name="context-property"></a>Context プロパティ

`context` プロパティは、ユーザーが会議中にアプリを呼び出す場合に、呼び出す場所によって、表示するコンテンツを決定します。 タブ `context` と `scopes` プロパティを使用すると、アプリの表示場所を決定できます。 `team` または `groupchat` スコープ内のタブには、複数のコンテキストを含めることができます。

会議前および会議後のチャットでアプリを有効にするには、`groupchat` スコープをサポートします。 会議前のアプリ エクスペリエンスでは、会議アプリを検索して追加し、会議前のタスクを実行できます。 会議後のアプリ エクスペリエンスでは、ユーザーは、投票されたアンケート結果やフィードバックなどの会議の結果を表示できます。

 `context` プロパティの値を次に示します。これらの値は、すべて使用することも、一部を使用することもできます。

|値|説明|
|---|---|
| **channelTab** | チーム チャネルのヘッダーのタブ。 |
| **privateChatTab** | チームや会議のコンテキストではない一連のユーザー間のグループ チャットのヘッダーにあるタブ。 |
| **meetingChatTab** | スケジュールされた会議の一連のユーザー間のグループ チャットのヘッダーにあるタブ。 **meetingChatTab** または **meetingDetailsTab** を指定すると、アプリをモバイルで実行できるようになります。 |
| **meetingDetailsTab** | 予定表の会議の詳細ビューのヘッダーにあるタブ。 **meetingChatTab** または **meetingDetailsTab** を指定すると、アプリをモバイルで実行できるようになります。 |
| **meetingSidePanel** | 統合バー (U バー) 経由で開かれる会議内パネル。 |
| **meetingStage** | 会議ステージに共有できる `meetingSidePanel` からのアプリ。 このアプリは、モバイル クライアントでも Teams Room クライアントでも使用できません。 |

Teams 会議用アプリを有効にしたら、会議の前、会議中、会議後にアプリを構成する必要があります。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

Teams 会議は、組織の共同作業エクスペリエンスを提供します。 さまざまな会議シナリオに合わせてアプリを構成し、会議エクスペリエンスを向上させます。 次の会議シナリオで実行できるアクションを特定できるようになりました。

* [会議の前](#before-a-meeting)
* [会議中](#during-a-meeting)
* [会議後](#after-a-meeting)

### <a name="before-a-meeting"></a>会議の前

会議の前に、ユーザーはタブ、ボット、メッセージ拡張機能を追加できます。 開催者ロールと発表者ロールを持つユーザーは、会議にタブを追加できます。

会議にタブを追加するには:

1. 予定表で、タブを追加する会議を選択します。
1. **[詳細]** タブを選択し、次を選択します: <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting1.png" alt="Pre-meeting experience" width="900"/>

1. In the tab gallery that appears, select the app that you want to add and follow the steps as required. The app is installed as a tab.

会議にメッセージ拡張機能を追加するには:

1. チャットのメッセージ作成領域にある省略記号 &#x25CF;&#x25CF;&#x25CF; を選択します。
1. 追加するアプリを選択し、必要に応じて手順に従います。 アプリはメッセージ拡張機能としてインストールされます。

会議にボットを追加するには:

会議チャットで **@** キーを入力し、**[ボットを取得]** を選択します。

> [!NOTE]
>
> * 会議内ダイアログでは、会議中のダイアログが表示され、ユーザーがアクセスできるアダプティブ カードが会議チャットに同時に投稿されます。 会議チャットのアダプティブ カードは、会議に出席しているユーザーや、Teams アプリが最小化されている場合に役立ちます。
> * ユーザー ID は[タブ SSO](../tabs/how-to/authentication/tab-sso-overview.md) を使用して確認する必要があります。 認証後、アプリは `GetParticipant` API を使用してユーザー ロールを取得できます。
> * ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。 たとえば、ポーリング アプリでは、開催者と発表者のみが新しい投票を作成できます。
> * ロールの割り当ては会議中に変更できます。 詳細については、「[Teams 会議での役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)」を参照してください。

### <a name="during-a-meeting"></a>会議中

会議中に、`meetingSidePanel` または会議中の通知を使用して、アプリに固有のエクスペリエンスを構築できます。

#### <a name="meeting-sidepanel"></a>会議の SidePanel

`meetingSidePanel` では、開催者と発表者が異なるビューとアクションのセットを使用できるように、会議のエクスペリエンスをカスタマイズできます。 アプリ マニフェストで、`meetingSidePanel` をコンテキスト配列に追加する必要があります。 会議とすべてのシナリオでは、アプリは幅が 320 ピクセルの会議内タブにレンダリングされます。 詳細については、「 [FrameInfo インターフェイス](/javascript/api/@microsoft/teams-js/frameinfo) (TeamsJS v.2.0.0 より前は `FrameContext` と呼ばれていました)」を参照してください。

[ユーザーのコンテキストを使用して、リクエストをルーティング](../tabs/how-to/access-teams-context.md#user-context)できます。 詳細については、「[タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)」を参照してください。 タブの認証フローは、Web サイトの認証フローに似ています。 タブは OAuth 2.0 を直接使用できます。 詳細については、「[Microsoft ID プラットフォームと OAuth 2.0 認証コード フロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow)」を参照してください。

メッセージ拡張機能は、ユーザーが会議中ビューを使用しているとき、期待どおりに機能します。 ユーザーは、メッセージ拡張カードを作成して投稿できます。 会議中の AppName は、会議中のアプリ名の U バーを示すツールヒントです。

> [!NOTE]
> バージョン 1.7.0 より前のバージョンではサイド パネルがサポートされていないため、このバージョン以降の [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を使用してください。

#### <a name="in-meeting-notification"></a>会議中の通知

会議中の通知は、会議中に参加者が参加できるようにしたり、会議中に情報やフィードバックを収集したりするために使用します。 会議中の通知をトリガーするには、[会議中の通知ペイロード](API-references.md#send-an-in-meeting-notification)を使用します。 通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含めます。

会議中の通知では、タスク モジュールを使用しないでください。 タスク モジュールは会議チャットでは呼び出されません。 会議中の通知を表示するには、外部リソース URL を使用します。 会議チャットでデータを送信するには、`submitTask` メソッドを使用します。

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="会議中ダイアログを使用する方法を示す例。":::

また、Teams の表示画像と連絡先カードを、ユーザーのMRI とペイロードで渡された表示名を持つトークン `onBehalfOf` に基づいて、会議中の通知に追加することもできます。 ペイロードの例を次に示します:

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="例は、会議中ダイアログで Teams 表示画像と連絡先カードを表示する方法を示しています。" border="true":::

#### <a name="shared-meeting-stage"></a>共有会議ステージ

共有会議ステージを使用すると、会議参加者はアプリ コンテンツの操作と共同作業をリアルタイムで行うことができます。 次の方法で、共同作業会議ステージにアプリを共有できます。

* Teams クライアントの会議のサイド パネルまたは [[ディープ リンク](#generate-a-deep-link-to-share-content-to-stage-in-meetings)] を使用して、アプリ[全体](#share-entire-app-to-stage)を共有してステージを設定します。
* Teams クライアント SDK の API を使用して、[アプリの特定の部分をステージに共有](#share-specific-parts-of-the-app-to-stage)します。

##### <a name="share-entire-app-to-stage"></a>アプリ全体をステージに共有する

参加者は、アプリのサイド パネルの [ステージで共有] ボタンを使用して、アプリ全体を共同作業会議ステージに共有できます。

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

To share the entire app to stage, in the app manifest you must configure `meetingStage` and `meetingSidePanel` as frame contexts. For example:

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

詳細については、「[アプリ マニフェスト](../resources/schema/manifest-schema-dev-preview.md#configurabletabs)」を参照してください。

##### <a name="share-specific-parts-of-the-app-to-stage"></a>アプリの特定の部分をステージに共有する

参加者は、ステージで共有 API を使用して、アプリの特定の部分を共同作業会議ステージに共有できます。 API は、Teams クライアント SDK 内で使用でき、アプリのサイド パネルから呼び出されます。

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

To share specific parts of the app to stage, you must invoke the related APIs in the Teams client SDK library. For more information, see [API reference](API-references.md).

> [!NOTE]
>
> * アプリの特定の部分をステージに共有するには、Teams マニフェスト バージョン 1.12 以降を使用します。
> * Teams デスクトップ クライアントでのみ、アプリの特定の部分を会議ステージに共有できます。 モバイル ユーザーは、アプリの特定の部分を共有して、 [API をステージングする共有](API-references.md#share-app-content-to-stage-api)を使用してステージングできます。

### <a name="after-a-meeting"></a>会議後

[会議の前](#before-a-meeting)および会議後の構成は同じです。

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>会議のステージにコンテンツを共有するためのディープ リンクを生成する

また、ディープ リンクを生成して [アプリを共有し、会議をステージング](#share-entire-app-to-stage) して開始または参加することもできます。

> [!NOTE]
>
> * 現在、会議のステージにコンテンツを共有するためのディープ リンクは UX の改善が行われ、 [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ利用できます。
> * 会議のステージにコンテンツを共有するためのディープ リンクは、Teams デスクトップ クライアントでのみサポートされています。

進行中の会議の一部であるユーザーがアプリでディープ リンクを選択すると、アプリがステージに共有され、アクセス許可ポップアップ ウィンドウが表示されます。 ユーザーは、アプリと共同作業するための参加者へのアクセス権を付与できます。

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="スクリーンショットは、アクセス許可ポップアップ ウィンドウを示す例です。":::

ユーザーが会議に参加していない場合、ユーザーは Teams カレンダーにリダイレクトされ、会議に参加したり、インスタント会議を開始したりできます (今すぐ会議を開く)。

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="スクリーンショットは、進行中の会議がない場合のポップアップ ウィンドウを示す例です。":::

ユーザーがインスタント会議 (今すぐ会議) を開始すると、参加者を追加してアプリを操作できます。

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="スクリーンショットは、参加者を追加するオプションと、アプリを操作する方法を示す例です。":::

ステージでコンテンツを共有するためのディープ リンクを追加するには、アプリ コンテキストが必要です。 アプリ コンテキストを使用すると、Teams クライアントはアプリ マニフェストをフェッチし、ステージでの共有が可能かどうかを確認できます。 アプリ コンテキストの例を次に示します。

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

アプリ コンテキストのクエリ パラメーターは次のとおりです。

* `appID`: これは、アプリ マニフェストから取得できる ID です。
* `appSharingUrl`: ステージで共有する必要がある URL は、アプリ マニフェストで定義された有効なドメインである必要があります。 URL が有効なドメインでない場合は、エラーの説明をユーザーに提供するエラー ダイアログがポップアップ表示されます。
* `useMeetNow`: これには、true または false のブール型パラメーターが含まれます。
  * **True**: 値が `UseMeetNow` true で、進行中の会議がない場合は、新しい会議が開始されます。 進行中の会議がある場合、この値は無視されます。

  * **False**: 既定値 `UseMeetNow` は false です。つまり、ディープ リンクがステージに共有され、進行中の会議がない場合、予定表のポップアップが表示されます。 ただし、会議中は直接共有できます。

すべてのクエリ パラメーターが適切に URI エンコードされ、アプリ コンテキストを最終 URL で 2 回エンコードする必要があることを確認します。 以下に例を示します。

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

ディープ リンクは、Teams Web または Teams デスクトップ クライアントから起動できます。

* **Teams Web**: 次の形式を使用して、Teams Web からディープ リンクを起動し、ステージ上でコンテンツを共有します。

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    例: `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |ディープ リンク|フォーマット|例|
    |---------|---------|---------|
    |アプリを共有して Teams カレンダーを開くには、UseMeeetNow が **false** の場合は既定です。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |UseMeeetNow が **true** の場合、アプリを共有してインスタント会議を開始します。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **チーム デスクトップ クライアント**: 次の形式を使用して、Teams デスクトップ クライアントからディープ リンクを起動し、ステージでコンテンツを共有します。

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    例: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |ディープ リンク|フォーマット|例|
    |---------|---------|---------|
    |アプリを共有して Teams カレンダーを開くには、UseMeeetNow が **false** の場合は既定です。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |UseMeeetNow が **true** の場合、アプリを共有してインスタント会議を開始します。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

クエリ パラメーターは次のとおりです。

* `deepLinkId`: テレメトリの関連付けに使用される任意の識別子。
* `fqdn`: `fqdn` は省略可能なパラメーターで、会議の適切な環境に切り替えて、ステージ上でアプリを共有するために使用できます。 特定の環境で特定のアプリ共有が発生するシナリオをサポートします。 既定値 `fqdn` はエンタープライズ URL で、可能な値は `Teams.live.com` Teams for Life、 `teams.microsoft.com`または `teams.microsoft.us`.

ステージにアプリ全体を共有するには、アプリ マニフェストで構成し`meetingSidePanel`、フレーム コンテキストとして[アプリ マニフェストを](../resources/schema/manifest-schema.md)参照する必要があります`meetingStage`。 それ以外の場合、会議の出席者はステージ上でコンテンツを表示できない可能性があります。

> [!NOTE]
> アプリが検証に合格するには、Web サイト、Web アプリ、またはアダプティブ カードからディープ リンクを作成するときに、 **会議で共有** を文字列またはコピーとして使用します。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会議アプリ | 会議トークン ジェネレーター アプリを使用してトークンを要求する方法を示します。 各参加者が会議に参加する機会を公平に得られるように、トークンは順次生成されます。 このトークンは、スクラム会議や Q&A セッションなどの状況で役立ちます。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|会議ステージのサンプル | 共同作業のために会議ステージでタブを表示するサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|会議のサイド パネル | 会議のサイド パネルに議題を追加する方法を示すサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>ステップ バイ ステップのガイド

* [ステップバイステップ ガイド](../sbs-meeting-token-generator.yml)に従って、Teams 会議で会議トークンを生成します。
* [ステップバイステップ ガイド](../sbs-meetings-sidepanel.yml)に従って、Teams 会議で会議サイドパネルを生成します。
* [ステップバイステップ ガイド](../sbs-meetings-stage-view.yml)に従って、Teams 会議で会議ステージ ビューを共有します。
* [ステップバイステップ ガイド](../sbs-meeting-content-bubble.yml)に従って、Teams 会議で会議コンテンツ バブルを生成します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会議アプリ API リファレンス](API-references.md)

## <a name="see-also"></a>関連項目

* [会議中ダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [共有会議ステージ エクスペリエンスの設計ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Microsoft Graph を使用して会議にアプリを追加する](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
