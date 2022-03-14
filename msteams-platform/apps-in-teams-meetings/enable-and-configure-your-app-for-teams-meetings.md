---
title: 会議のアプリを有効にしてTeamsする
author: surbhigupta
description: Teams 会議やさまざまな会議シナリオ用のアプリの有効化と構成、アプリ マニフェストの更新、会議内ダイアログ、共有会議ステージ、会議サイドパネルなどの機能の構成
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 0211cb1458b13a0727fce9915d1a50d227ed1a53
ms.sourcegitcommit: ca902f505a125641c379a917ee745ab418bd1ce6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2022
ms.locfileid: "63464360"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>会議のアプリを有効にしてTeamsする

すべてのチームは、タスクのコミュニケーションと共同作業の異なる方法を持っています。 これらの異なるタスクを実現するには、会議Teamsをカスタマイズします。 アプリを会議にTeamsし、アプリ マニフェスト内の会議スコープで使用できるアプリを構成します。

## <a name="prerequisites"></a>必須条件

会議のTeamsを使用すると、会議のライフサイクル全体にわたってアプリの機能を拡張できます。 会議のアプリを使用するTeams、次の前提条件を満たす必要があります。

* アプリを開発するTeamsします。 アプリの開発方法の詳細については、「Teams開発[」Teams参照してください](../overview.md)。

* groupchat スコープで構成可能なタブをサポートするアプリを使用します。 詳細については、「グループ チャットスコープ [」と「グループ](../resources/schema/manifest-schema.md#configurabletabs) [タブの作成」を参照してください](../build-your-first-app/build-channel-tab.md)。

* 会議前および[会議Teamsの](../tabs/design/tabs.md)一般的なタブ設計ガイドラインに従います。 会議中のエクスペリエンスについては、会議 [中のタブ](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) デザインガイドラインと会議内ダイアログの設計ガイドライン [を参照してください](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいてアプリを最新の情報に更新する必要があります。 これらのイベントは、会議のライフサイクル全体にわたって、会議内のダイアログ ボックスや他のステージ内に含めできます。 [会議内] ダイアログ ボックスについては、「会議内 `completionBotId` 通知ペイロードの [パラメーター」を参照してください](API-references.md#send-an-in-meeting-notification)。

## <a name="enable-your-app-for-teams-meetings"></a>会議でアプリをTeamsする

会議でアプリを有効にするにはTeamsマニフェストを更新し、コンテキスト プロパティを使用してアプリを表示する場所を決定します。

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、、 、および配列を使用してアプリ マニフェスト`configurableTabs``scopes`で宣言`context`されます。 スコープは、アクセスできるユーザーを定義し、コンテキストによってアプリが利用可能な場所を定義します。

> [!NOTE]
>
> * マニフェスト スキーマを使用してアプリ マニフェストを [更新する必要があります](../resources/schema/manifest-schema-dev-preview.md)。
> * 会議のアプリにはスコープが必要 `groupchat` です。 スコープ `team` は、チャネル内のタブでのみ機能します。

アプリ マニフェストには、次のコード スニペットが含まれる必要があります。

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

プロパティ `context` は、ユーザーがアプリを呼び出す場所に応じて、ユーザーが会議でアプリを呼び出す際に表示する必要がある内容を決定します。 タブとプロパティ `context` を `scopes` 使用すると、アプリを表示する必要がある場所を特定できます。 スコープ内のタブ `team` には `groupchat` 、複数のコンテキストを指定できます。

会議前 `groupchat` および会議後のチャットでアプリを有効にするスコープをサポートします。 会議前アプリエクスペリエンスを使用すると、会議アプリを検索して追加し、会議前のタスクを実行できます。 会議後のアプリ エクスペリエンスを使用すると、アンケートのアンケート結果や料金など、会議の結果を表示できます。

 値のすべてまたは一部を `context` 使用できるプロパティの値を次に示します。

|値|説明|
|---|---|
| **channelTab** | チーム チャネルのヘッダー内のタブ。 |
| **privateChatTab** | チームまたは会議のコンテキストではなく、一連のユーザー間のグループ チャットのヘッダーにあるタブ。 |
| **meetingChatTab** | スケジュールされた会議の一連のユーザー間のグループ チャットのヘッダー内のタブ。 **meetingChatTab** または **meetingDetailsTab** のいずれかを指定すると、アプリがモバイルで動作します。 |
| **meetingDetailsTab** | 予定表の会議の詳細ビューのヘッダーにあるタブ。 **meetingChatTab** または **meetingDetailsTab** のいずれかを指定すると、アプリがモバイルで動作します。 |
| **meetingSidePanel** | 統合バー (U バー) を介して開いた会議内パネル。 |
| **meetingStage** | アプリを会議 `meetingSidePanel` ステージに共有できます。 このアプリは、モバイル クライアントでも Teams Room クライアントでも使用できません。 |

会議に対してアプリを有効Teams、会議の前、会議中、会議後にアプリを構成する必要があります。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

Teams会議は、組織に共同作業のエクスペリエンスを提供します。 さまざまな会議シナリオ用にアプリを構成し、会議のエクスペリエンスを強化します。 これで、次の会議シナリオで実行できるアクションを特定できます。

* [会議の前](#before-a-meeting)
* [会議中](#during-a-meeting)
* [会議後](#after-a-meeting)

### <a name="before-a-meeting"></a>会議の前

会議の前に、ユーザーはタブ、ボット、メッセージング拡張機能を追加できます。 開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。

タブを会議に追加するには、次の方法を使用します。

1. 予定表で、タブを追加する会議を選択します。
1. [詳細] **タブを選択** し、[ <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting.png" alt="Pre-meeting experience" width="900"/>

1. 表示されるタブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 アプリはタブとしてインストールされます。

メッセージング拡張機能を会議に追加するには、次の方法を使用します。

1. チャット内のメッセージ &#x25CF;&#x25CF;&#x25CF; にある省略記号を選択します。
1. 追加するアプリを選択し、必要に応じて手順に従います。 アプリはメッセージング拡張機能としてインストールされます。

ボットを会議に追加するには、次の方法を使用します。

会議チャットで、キーを入力し、[ **@** ボットの取得 **] を選択します**。

> [!NOTE]
>
> * コンテンツ バブルは、ユーザーがアクセスできるアダプティブ カードまたはカードを会議チャットに同時に投稿します。 これにより、会議または会議アプリが最小化Teamsユーザーに役立ちます。
> * ユーザー ID は、Tabs SSO を使用して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。 認証後、アプリは API を使用してユーザー ロールを取得 `GetParticipant` できます。
> * ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。 たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。
> * 会議の進行中に役割の割り当てを変更できます。 詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

### <a name="during-a-meeting"></a>会議中

会議中に、会議中または `meetingSidePanel` 会議中の通知を使用して、アプリに固有のエクスペリエンスを構築できます。

#### <a name="meeting-sidepanel"></a>Meeting SidePanel

開催 `meetingSidePanel` 者と発表者が異なる一連のビューとアクションを持つ会議のエクスペリエンスをカスタマイズできます。 アプリ マニフェストで、コンテキスト配列に `meetingSidePanel` 追加する必要があります。 会議およびすべてのシナリオで、アプリは幅 320 ピクセルの会議内タブに表示されます。 詳細については、「 [FrameContext インターフェイス」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。

API を使用して要求`userContext`をルーティングするには、「SDK のTeams[してください](../tabs/how-to/access-teams-context.md#user-context)。 詳細については、「タブの認証[フロー Teamsを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。 タブの認証フローは、Web サイトの認証フローに似ています。 したがって、タブは OAuth 2.0 を直接使用できます。 詳細については、「Microsoft ID プラットフォーム [OAuth 2.0 認証コード フロー」を参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

メッセージング拡張機能は、ユーザーが会議中のビューに表示されている場合に期待通り動作します。 ユーザーは、作成メッセージ拡張カードを投稿できます。 AppName in-meeting は、会議中の U バーのアプリ名を示すツールヒントです。

> [!NOTE]
> バージョン 1.7.0 以上の Teams SDK を使用します[。](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)前のバージョンではサイド パネルはサポートされていません。

#### <a name="in-meeting-notification"></a>会議中の通知

会議中の通知は、会議中に参加者を引き付け、会議中に情報やフィードバックを収集するために使用されます。 会議内 [通知ペイロードを使用して](API-references.md#send-an-in-meeting-notification) 会議内通知をトリガーします。 通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含める。

会議中の通知では、タスク モジュールを使用しなける必要があります。 タスク モジュールは、会議チャットでは呼び出されません。 会議中の通知を表示するには、外部リソースの URL を使用します。 このメソッドを使用して `submitTask` 、会議チャットでデータを送信できます。

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="例は、会議内ダイアログを使用する方法を示しています。" border="true":::

#### <a name="shared-meeting-stage"></a>共有会議ステージ

共有会議ステージを使用すると、会議参加者はアプリ コンテンツをリアルタイムで操作し、共同作業できます。 次の方法で、共同作業の会議ステージにアプリを共有できます。

* [アプリ全体を共有し、](#share-entire-app-to-stage)クライアントで [共有からステージへ] ボタンを使用Teamsします。
* [アプリの特定の部分を共有し、](#share-specific-parts-of-the-app-to-stage)クライアント SDK で API を使用Teamsします。

##### <a name="share-entire-app-to-stage"></a>アプリ全体をステージに共有する

参加者は、アプリ側パネルの [共有からステージへの共有] ボタンを使用して、アプリ全体を共同作業の会議ステージに共有できます。

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

アプリ全体をステージ間で共有するには、アプリ マニフェスト`meetingStage``meetingSidePanel`でフレーム コンテキストとして構成する必要があります。 例:

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

詳細については、「アプリ マニフェスト [」を参照してください](../resources/schema/manifest-schema-dev-preview.md#configurabletabs)。

##### <a name="share-specific-parts-of-the-app-to-stage"></a>アプリの特定の部分をステージに共有する

参加者は、共有を使用して API をステージ化することで、アプリの特定の部分を共同作業の会議ステージに共有できます。 API は、クライアント SDK 内Teamsアプリ側パネルから呼び出されます。

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

アプリの特定の部分をステージ間で共有するには、クライアント SDK ライブラリで関連する API をTeamsする必要があります。 詳細については、「API リファレンス [」を参照してください](API-references.md)。

アプリで匿名ユーザーをサポート`from.id``from`する場合、最初の呼び出し要求ペイロードは、要求メタデータではなく、オブジェクト内の要求メタデータに依存する`from.aadObjectId`必要があります。 `from.id`はユーザー ID であり`from.aadObjectId`、ユーザー Azure AD ID です。 詳細については、「タブでタスク [モジュールを使用する」を参照し](../task-modules-and-cards/task-modules/task-modules-tabs.md)[、タスク モジュールを作成して送信します](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="after-a-meeting"></a>会議後

会議の後と前の [構成は](#before-a-meeting) 同じです。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会議アプリ | 会議トークン ジェネレーター アプリを使用してトークンを要求する方法を示します。 トークンが順番に生成され、各参加者が会議に参加する公平な機会を得る。 トークンは、スクラム会議や Q セッションのような状況&役立ちます。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|会議ステージのサンプル | コラボレーション用の会議ステージにタブを表示するサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|会議のサイド パネル | 会議サイド パネルに議題を追加する方法を示すサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>ステップ バイ ステップのガイド

* ステップ バイ [ステップ ガイドに従って](../sbs-meeting-token-generator.yml)、会議で会議トークンを生成Teamsします。
* ステップ バイ [ステップ ガイドに従って](../sbs-meetings-sidepanel.yml)、会議のサイドパネルを生成Teamsします。
* ステップ バイ [ステップ ガイドに従って](../sbs-meetings-stage-view.yml)、会議の会議で会議ステージ ビュー Teamsします。
* ステップ バイ [ステップ ガイドに従って](../sbs-meeting-content-bubble.yml)、会議で会議コンテンツバブルを生成Teamsします。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [会議アプリ API リファレンス](API-references.md)

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [共有会議ステージエクスペリエンスの設計ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Microsoft Web サイトを介して会議にアプリを追加Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
