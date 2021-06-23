---
title: 会議で使用するアプリを有効Teamsする
author: surbhigupta
description: 会議で使用するアプリを有効Teamsする
ms.topic: conceptual
ms.openlocfilehash: e31e241a61f40a8dc2b8a1221765bd4755d346ed
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068642"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>会議で使用するアプリを有効Teamsする

すべてのチームは、タスクのコミュニケーションと共同作業の異なる方法を持っています。 これらの異なるタスクを実現するには、会議Teamsをカスタマイズします。 異なるタスクをカスタマイズして達成するには、アプリを会議に対して有効にし、Teamsマニフェスト内の会議スコープで使用できるアプリを構成する必要があります。

## <a name="enable-your-app-for-teams-meetings"></a>会議でアプリを有効Teamsする

会議でアプリを有効にするにはTeamsマニフェストを更新し、コンテキスト プロパティを使用してアプリを表示する場所を決定する必要があります。

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、、 、および配列を使用してアプリ マニフェスト `configurableTabs` `scopes` で宣言 `context` されます。 スコープは、アプリを使用できる場所を定義するユーザーとコンテキストを定義します。

> [!NOTE]
> * マニフェスト スキーマを使用してアプリ マニフェストを [更新してみてください](../resources/schema/manifest-schema-dev-preview.md)。
> * 会議のアプリには、グループチャットスコープが必要です。 チーム スコープは、チャネル内のタブでのみ機能します。

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

> [!NOTE]
> `meetingStage` は現在、開発者 [プレビューでのみ使用](../resources/dev-preview/developer-preview-intro.md) できます。

### <a name="context-property"></a>Context プロパティ

プロパティは、ユーザーがアプリを呼び出す場所に応じて、ユーザーが会議でアプリを呼び出す際に表示 `context` する必要がある内容を決定します。 タブと `context` プロパティ `scopes` を使用すると、アプリを表示する必要がある場所を特定できます。 またはスコープ内 `team` のタブ `groupchat` には、複数のコンテキストを指定できます。 値のすべてまたは一部を使用できるプロパティの値を `context` 次に示します。

|値|説明|
|---|---|
| **channelTab** | チーム チャネルのヘッダー内のタブ。 |
| **privateChatTab** | チームまたは会議のコンテキストではなく、一連のユーザー間のグループ チャットのヘッダーにあるタブ。 |
| **meetingChatTab** | スケジュールされた会議のコンテキスト内の一連のユーザー間のグループ チャットのヘッダー内のタブ。 |
| **meetingDetailsTab** | 予定表の会議の詳細ビューのヘッダーにあるタブ。 |
| **meetingSidePanel** | 統合バー (U バー) を介して開いた会議内パネル。 |
| **meetingStage** | meetingSidePanel のアプリを会議ステージに共有できます。 |

> [!NOTE]
> `Context` プロパティは現在、モバイル クライアントではサポートされていません。

会議でアプリを有効Teams、会議の前、会議中、会議の後にアプリを構成する必要があります。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議シナリオ用にアプリを構成する

> [!NOTE]
> * タブ ギャラリーにアプリを表示するには、構成可能なタブとグループ チャット スコープをサポートする必要があります。
> * モバイル クライアントは、会議の開催前と開催後のステージでのみタブをサポートします。
> * 現在、モバイル クライアントでは、会議中のダイアログ ボックスとタブである会議内エクスペリエンスはサポートされていません。 詳細については、「モバイル用の [タブを作成する際の](../tabs/design/tabs-mobile.md) モバイルタブのガイダンス」を参照してください。

Teams会議は、組織に固有の共同作業エクスペリエンスを提供します。 さまざまな会議シナリオ用にアプリを構成する機会を提供します。 参加者の役割またはユーザーの種類に基づいて会議のエクスペリエンスを向上させるアプリを構成できます。 これで、次の会議シナリオで実行できるアクションを特定できます。
* [事前会議](#pre-meeting)
* [会議中](#in-meeting)
* [会議後](#post-meeting)

### <a name="pre-meeting"></a>事前会議

会議の前に、ユーザーはタブ、ボット、メッセージング拡張機能を追加できます。 開催者と発表者の役割を持つユーザーは、会議にタブを追加できます。

**タブを会議に追加するには**

1. 予定表で、タブを追加する会議を選択します。
1. [詳細] **タブを選択** し、[ <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    ![会議前のエクスペリエンス](../assets/images/apps-in-meetings/PreMeeting.png)

1. 表示されるタブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 アプリはタブとしてインストールされます。

    > [!NOTE]
    > 現在、会議タブでは、会議の詳細と参加者情報の取得はサポートされていません。

**会議にメッセージング拡張機能を追加するには**

1. チャット内のメッセージ &#x25CF;&#x25CF;&#x25CF; にある省略記号を選択します。
1. 追加するアプリを選択し、必要に応じて手順に従います。 アプリはメッセージング拡張機能としてインストールされます。

**ボットを会議に追加するには**

会議チャットで、キーを入力し **@** 、[ボットの取得 **] を選択します**。

> [!NOTE]
> * ユーザー ID は、Tabs SSO を使用して [確認する必要があります](../tabs/how-to/authentication/auth-aad-sso.md)。 認証後、アプリは API を使用してユーザー ロールを取得 `GetParticipant` できます。
> * ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。 たとえば、ポーリング アプリでは、開催者と発表者だけが新しいポーリングを作成できます。
> * 会議の進行中に役割の割り当てを変更できます。 詳細については、「会議での[役割」をTeamsしてください](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

### <a name="in-meeting"></a>会議中

会議中に、meetingSidePanel または会議内ダイアログ ボックスを使用して、アプリに固有のエクスペリエンスを構築できます。

#### <a name="meetingsidepanel"></a>meetingSidePanel

meetingSidePanel を使用すると、会議のエクスペリエンスをカスタマイズして、開催者と発表者が異なる一連のビューとアクションを持つ事が可能です。 アプリ マニフェストで、コンテキスト配列に meetingSidePanel を追加する必要があります。 会議およびすべてのシナリオで、アプリは幅 320 ピクセルの会議内タブに表示されます。 詳細については [、「FrameContext インターフェイス」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。

API を使用して要求を必要に応じてルーティングするには、「SDK `userContext` Teams[参照してください](../tabs/how-to/access-teams-context.md#user-context)。 詳細については、「タブの認証[フロー Teamsを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。 タブの認証フローは、Web サイトの認証フローと非常に似ています。 したがって、タブは OAuth 2.0 を直接使用できます。 詳細については、「Microsoft ID プラットフォーム[OAuth 2.0 認証コード フロー」を参照してください](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

メッセージング拡張機能は、ユーザーが会議内ビューに表示され、ユーザーが作成メッセージ内線カードを投稿できる場合に期待通り機能します。 AppName in-meeting は、会議中の U バーのアプリ名を示すツールヒントです。

> [!NOTE]
> バージョン 1.7.0 以上の[Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用します。前のバージョンではサイド パネルはサポートされていません。

#### <a name="in-meeting-dialog-box"></a>[会議内] ダイアログ ボックス

[会議中] ダイアログ ボックスを使用すると、会議中に参加者を引き付け、会議中に情報やフィードバックを収集できます。 API を [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) 使用して、バブル通知をトリガーする必要があります。 通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含める。

会議中のダイアログでは、タスク モジュールを使用することはできません。 タスク モジュールは、会議チャットでは呼び出されません。 外部リソース URL を使用して、会議にコンテンツ バブルを表示します。 このメソッドを使用 `submitTask` して、会議チャットでデータを送信できます。

> [!NOTE]
> * ユーザーが Web ビューでアクションを実行した後に自動的に終了するには [、submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 関数を呼び出す必要があります。 これは、アプリの申請に必要な要件です。 詳細については、「SDK タスク モジュール[Teamsを参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
> * アプリで匿名ユーザーをサポートする場合、最初の呼び出し要求ペイロードは、要求メタデータではなく、オブジェクト内の要求メタデータ `from.id` `from` に `from.aadObjectId` 依存する必要があります。 `from.id`はユーザー ID であり `from.aadObjectId` 、ユーザー Azure Active Directory (AAD) ID です。 詳細については、「タブでタスク [モジュールを使用する」を参照し](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、 [タスク モジュールを作成して送信します](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

#### <a name="share-to-stage"></a>ステージ間の共有

> [!NOTE]
> * この機能は現在、開発者プレビュー [でのみ使用](../resources/dev-preview/developer-preview-intro.md) できます。
> * この機能を使用するには、アプリが会議中の meetingSidePanel をサポートしている必要があります。

この機能により、開発者はアプリを会議ステージに共有できます。 会議ステージへの共有を有効にすると、会議の参加者はリアルタイムで共同作業できます。

必要なコンテキストは `meetingStage` 、アプリ マニフェスト内です。 このための前提条件は、コンテキストを持 `meetingSidePanel` つ必要があります。 これにより **、meetingSidePanel** で共有が有効です。

![会議のエクスペリエンス中にステージに共有する](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

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

### <a name="post-meeting"></a>会議後

会議後と会議 [前の](#pre-meeting) 構成は同じです。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | サンプル |
|----------------|-----------------|--------------|----------------|-----------|
| 会議アプリ | 会議トークン ジェネレーター アプリを使用してトークンを要求する方法を示します。このトークンは、各参加者が対話する公平な機会を得る機会を得る順番に生成されます。 これは、スクラム会議、Q&セッションなど、状況に役立ちます。 | [View](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a>関連項目

* [会議中のダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teamsの認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
