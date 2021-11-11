---
title: 会議で使用するアプリを有効Teamsする
author: surbhigupta
description: Teams 会議やさまざまな会議シナリオ用のアプリの有効化と構成、アプリ マニフェストの更新、会議内ダイアログ、共有会議ステージ、会議サイドパネルなどの機能の構成
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 17add35ef0b2d2cbb3ce2e6658d11d6d58dd8d2d
ms.sourcegitcommit: db529cdf7e9195fa45b9065c50f5381770cc3711
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2021
ms.locfileid: "60912221"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>会議で使用するアプリを有効Teamsする

すべてのチームは、タスクのコミュニケーションと共同作業の異なる方法を持っています。 これらの異なるタスクを実現するには、会議Teamsをカスタマイズします。 会議でアプリを有効Teams、アプリ マニフェスト内の会議スコープで使用できるアプリを構成します。

## <a name="enable-your-app-for-teams-meetings"></a>会議でアプリを有効Teamsする

会議でアプリを有効にするにはTeamsマニフェストを更新し、コンテキスト プロパティを使用してアプリを表示する場所を決定します。

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、、 、および配列を使用してアプリ マニフェスト `configurableTabs` `scopes` で宣言 `context` されます。 スコープは、アクセスできるユーザーを定義し、コンテキストによってアプリが利用可能な場所を定義します。

> [!NOTE]
> * マニフェスト スキーマを使用してアプリ マニフェストを [更新する必要があります](../resources/schema/manifest-schema-dev-preview.md)。
> * 会議のアプリにはスコープが `groupchat` 必要です。 スコープ `team` は、チャネル内のタブでのみ機能します。

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

プロパティは、ユーザーがアプリを呼び出す場所に応じて、ユーザーが会議でアプリを呼び出す際に表示 `context` する必要がある内容を決定します。 タブと `context` プロパティ `scopes` を使用すると、アプリを表示する必要がある場所を特定できます。 スコープ内のタブ `team` `groupchat` には、複数のコンテキストを指定できます。 値のすべてまたは一部を使用できるプロパティの値を `context` 次に示します。

|値|説明|
|---|---|
| **channelTab** | チーム チャネルのヘッダー内のタブ。 |
| **privateChatTab** | チームまたは会議のコンテキストではなく、一連のユーザー間のグループ チャットのヘッダーにあるタブ。 |
| **meetingChatTab** | スケジュールされた会議の一連のユーザー間のグループ チャットのヘッダー内のタブ。 meetingChatTab または **meetingDetailsTab** のいずれかを指定すると、アプリがモバイルで動作します。  |
| **meetingDetailsTab** | 予定表の会議の詳細ビューのヘッダーにあるタブ。 meetingChatTab または **meetingDetailsTab** のいずれかを指定すると、アプリがモバイルで動作します。  |
| **meetingSidePanel** | 統合バー (U バー) を介して開いた会議内パネル。 |
| **meetingStage** | アプリを会議 `meetingSidePanel` ステージに共有できます。 このアプリは、モバイル クライアントまたはルーム クライアントTeamsできません。 |

会議でアプリを有効Teams、会議の前、会議中、会議の後にアプリを構成する必要があります。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

Teams会議は、組織に共同作業のエクスペリエンスを提供します。 さまざまな会議シナリオ用にアプリを構成し、会議のエクスペリエンスを強化します。 これで、次の会議シナリオで実行できるアクションを特定できます。

* [会議の前](#before-a-meeting)
* [会議中](#during-a-meeting)
* [会議後](#after-a-meeting)

### <a name="before-a-meeting"></a>会議の前

会議の前に、ユーザーはタブ、ボット、メッセージング拡張機能を追加できます。 開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。

**タブを会議に追加するには**

1. 予定表で、タブを追加する会議を選択します。
1. [詳細] **タブを選択** し、[ <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting.png" alt="Pre-meeting experience" width="900"/>

1. 表示されるタブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 アプリはタブとしてインストールされます。

**会議にメッセージング拡張機能を追加するには**

1. チャット内のメッセージ &#x25CF;&#x25CF;&#x25CF; にある省略記号を選択します。
1. 追加するアプリを選択し、必要に応じて手順に従います。 アプリはメッセージング拡張機能としてインストールされます。

**ボットを会議に追加するには**

会議チャットで、キーを入力し **@** 、[ボットの取得 **] を選択します**。

> [!NOTE]
> * コンテンツ バブルは、ユーザーがアクセスできるアダプティブ カードまたはカードを会議チャットに同時に投稿します。 これにより、会議または会議アプリが最小化Teamsユーザーに役立ちます。
> * ユーザー ID は、Tabs SSO を使用して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。 認証後、アプリは API を使用してユーザー ロールを取得 `GetParticipant` できます。
> * ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。 たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。
> * 会議の進行中に役割の割り当てを変更できます。 詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

### <a name="during-a-meeting"></a>会議中

会議中に、または会議内のダイアログ ボックスを使用して、アプリ `meetingSidePanel` に固有のエクスペリエンスを構築できます。

#### <a name="meeting-sidepanel"></a>Meeting SidePanel

開催者と発表者が異なる一連のビューとアクションを持つ会議のエクスペリエンス `meetingSidePanel` をカスタマイズできます。 アプリ マニフェストで、コンテキスト配列 `meetingSidePanel` に追加する必要があります。 会議およびすべてのシナリオで、アプリは幅 320 ピクセルの会議内タブに表示されます。 詳細については [、「FrameContext インターフェイス」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。

API を使用して `userContext` 要求をルーティングするには、「SDK のTeams[参照してください](../tabs/how-to/access-teams-context.md#user-context)。 詳細については、「タブの認証[フロー Teamsを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。 タブの認証フローは、Web サイトの認証フローに似ています。 したがって、タブは OAuth 2.0 を直接使用できます。 詳細については、「Microsoft ID プラットフォーム[OAuth 2.0 認証コード フロー」を参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

メッセージング拡張機能は、ユーザーが会議中のビューに表示されている場合に期待通り動作します。 ユーザーは、作成メッセージ拡張カードを投稿できます。 AppName in-meeting は、会議中の U バーのアプリ名を示すツールヒントです。

> [!NOTE]
> バージョン 1.7.0 以上の[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用します。前のバージョンではサイド パネルはサポートされていません。

#### <a name="in-meeting-dialog-box"></a>[会議内] ダイアログ ボックス

会議中に参加者を引き付け、会議中に情報やフィードバックを収集するために、会議内ダイアログ ボックスが使用されます。 API を使用 [`NotificationSignal`](API-references.md#notificationsignal-api) してバブル通知をトリガーします。 通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含める。

会議中のダイアログでは、タスク モジュールを使用することはできません。 タスク モジュールは、会議チャットでは呼び出されません。 外部リソース URL を使用して、会議のコンテンツ バブルを表示します。 このメソッドを使用 `submitTask` して、会議チャットでデータを送信できます。

> [!NOTE]
> * ユーザーが Web ビューでアクションを実行した後に自動的に終了するには [、submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) 関数を呼び出す必要があります。 これは、アプリの申請に必要な要件です。 詳細については、「SDK タスク モジュール[Teamsを参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
> * アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、要求メタデータではなく、オブジェクト内の要求メタデータに `from.id` `from` `from.aadObjectId` 依存する必要があります。 `from.id`はユーザー ID であり `from.aadObjectId` 、ユーザー Azure Active Directory (AAD) ID です。 詳細については、「タブでタスク [モジュールを使用する」を参照し](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、 [タスク モジュールを作成して送信します](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

#### <a name="shared-meeting-stage"></a>共有会議ステージ

共有会議ステージを使用すると、会議参加者はアプリ コンテンツをリアルタイムで操作し、共同作業できます。

必要なコンテキストは `meetingStage` 、アプリ マニフェスト内です。 前提条件は、コンテキストを持ち `meetingSidePanel` 、共有 **を有効** にしている場合です `meetingSidePanel` 。

![会議のエクスペリエンス中にステージに共有する](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

共有会議ステージを有効にするには、アプリ マニフェストを次のように構成します。

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

共有会議ステージエクスペリエンス [を設計する方法を参照してください](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

### <a name="after-a-meeting"></a>会議後

会議の後と前の [構成は](#before-a-meeting) 同じです。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会議アプリ | 会議トークン ジェネレーター アプリを使用してトークンを要求する方法を示します。 トークンが順番に生成され、各参加者が会議に参加する公平な機会を得る。 このトークンは、スクラム会議や Q セッションなど、&役立ちます。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|会議ステージのサンプル | コラボレーション用の会議ステージにタブを表示するサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [会議アプリ API リファレンス](API-references.md)

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [Microsoft サービス経由で会議にアプリを追加Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http)
