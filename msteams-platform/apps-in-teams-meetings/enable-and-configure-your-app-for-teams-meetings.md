---
title: Teams会議用にアプリを有効にして構成する
author: surbhigupta
description: Teams会議やさまざまな会議シナリオ用にアプリを有効にして構成する、アプリ マニフェストを更新する、機能を構成する (会議内ダイアログ、共有会議ステージ、会議サイドパネルなど)
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 1f77d0924eec9c52dc2f3d10566010c2953bd66b
ms.sourcegitcommit: 5201e7f390fbb2a9190cae1781c2f09e1746c8f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2022
ms.locfileid: "64820196"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>Teams会議用にアプリを有効にして構成する

すべてのチームには、タスクのコミュニケーションと共同作業の方法が異なります。 これらのさまざまなタスクを実現するには、会議用のアプリを使用してTeamsをカスタマイズします。 Teams会議用にアプリを有効にし、アプリマニフェスト内の会議スコープで使用できるようにアプリを構成します。

## <a name="prerequisites"></a>前提条件

Teams会議用のアプリを使用すると、会議のライフサイクル全体でアプリの機能を拡張できます。 Teams会議用のアプリを操作する前に、次の前提条件を満たす必要があります。

* Teams アプリを開発する方法について説明します。 Teams アプリを開発する方法の詳細については、アプリ[の開発Teams](../overview.md)参照してください。

* groupchat スコープで構成可能なタブをサポートするアプリを使用します。 詳細については、「 [グループ チャット スコープ](../resources/schema/manifest-schema.md#configurabletabs) 」を参照し、 [グループ タブを作成します](../build-your-first-app/build-channel-tab.md)。

* 会議の前後のシナリオに関する一般的な[Teamsタブ設計ガイドライン](../tabs/design/tabs.md)に従います。 会議中のエクスペリエンスについては、 [会議内タブの設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) と [会議内ダイアログの設計ガイドライン](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)を参照してください。

* アプリをリアルタイムで更新するには、会議のイベント アクティビティに基づいて最新の状態にする必要があります。 これらのイベントは、会議のライフサイクル全体で、会議内のダイアログ ボックスや他のステージ内に含めることができます。 会議中のダイアログ ボックスについては、会議[中の通知ペイロードのパラメーターに関する説明を](API-references.md#send-an-in-meeting-notification)参照してください`completionBotId`。

## <a name="enable-your-app-for-teams-meetings"></a>Teams会議用にアプリを有効にする

アプリでTeams会議を有効にするには、アプリ マニフェストを更新し、コンテキストプロパティを使用してアプリの表示場所を決定します。

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

会議アプリの機能は、および`context`配列を使用して`configurableTabs``scopes`、アプリ マニフェストで宣言されます。 スコープはアクセスできるユーザーを定義し、コンテキストはアプリを使用できる場所を定義します。

> [!NOTE]
>
> * マニフェスト [スキーマ](../resources/schema/manifest-schema-dev-preview.md)を使用してアプリ マニフェストを更新する必要があります。
> * 会議のアプリにはスコープが必要 `groupchat` です。 スコープは `team` 、チャネル内のタブでのみ機能します。

アプリ マニフェストには、次のコード スニペットを含める必要があります。

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

このプロパティは `context` 、ユーザーがアプリを呼び出す場所に応じて、ユーザーが会議でアプリを呼び出すときに何を表示する必要があるかを決定します。 タブ `context` と `scopes` プロパティを使用すると、アプリの表示場所を決定できます。 スコープ`groupchat`内の`team`タブには、複数のコンテキストを含めることができます。

会議前および会議後の `groupchat` チャットでアプリを有効にするスコープをサポートします。 会議前アプリエクスペリエンスを使用すると、会議アプリを見つけて追加し、会議前のタスクを実行できます。 会議後アプリエクスペリエンスを使用すると、アンケートの結果や料金など、会議の結果を表示できます。

 値のすべてまたは一部を `context` 使用できるプロパティの値を次に示します。

|値|説明|
|---|---|
| **channelTab** | チーム チャネルのヘッダーのタブ。 |
| **privateChatTab** | チームや会議のコンテキストではなく、一連のユーザー間でグループ チャットのヘッダーにあるタブ。 |
| **meetingChatTab** | スケジュールされた会議の一連のユーザー間でのグループ チャットのヘッダーのタブ。 アプリがモバイルで動作するように、 **meetingChatTab** または **meetingDetailsTab** を指定できます。 |
| **meetingDetailsTab** | 予定表の会議の詳細ビューのヘッダーにあるタブ。 アプリがモバイルで動作するように、 **meetingChatTab** または **meetingDetailsTab** を指定できます。 |
| **meetingSidePanel** | 統合バー (U バー) を介して開かれた会議内パネル。 |
| **meetingStage** | 会議ステージに `meetingSidePanel` アプリを共有できます。 このアプリは、モバイル クライアントでも Teams Room クライアントでも使用できません。 |

Teams会議用にアプリを有効にした後は、会議の前、会議中、会議の後にアプリを構成する必要があります。

## <a name="configure-your-app-for-meeting-scenarios"></a>会議のシナリオ用にアプリを構成する

Teams会議は、組織のコラボレーション エクスペリエンスを提供します。 さまざまな会議シナリオに合わせてアプリを構成し、会議のエクスペリエンスを向上させます。 次の会議シナリオで実行できるアクションを特定できるようになりました。

* [会議の前](#before-a-meeting)
* [会議中](#during-a-meeting)
* [会議後](#after-a-meeting)

### <a name="before-a-meeting"></a>会議の前

会議の前に、ユーザーはタブ、ボット、メッセージング拡張機能を追加できます。 開催者ロールと発表者ロールを持つユーザーは、会議にタブを追加できます。

会議にタブを追加するには:

1. 予定表で、タブを追加する会議を選択します。
1. [ **詳細** ] タブを選択し、 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting.png" alt="Pre-meeting experience" width="900"/>

1. 表示されるタブ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 アプリはタブとしてインストールされます。

会議にメッセージング拡張機能を追加するには:

1. チャットの作成メッセージ領域にある省略記号 &#x25CF;&#x25CF;&#x25CF; を選択します。
1. 追加するアプリを選択し、必要に応じて手順に従います。 アプリはメッセージング拡張機能としてインストールされます。

会議にボットを追加するには:

会議チャットでキーを入力し、[ボットの **@** 取得] を選択 **します**。

> [!NOTE]
>
> * コンテンツ バブルは、ユーザーがアクセスできる会議チャットにアダプティブ カードまたはカードを同時に投稿します。 これは、会議やTeams アプリが最小化されたときにユーザーを支援します。
> * ユーザー ID は [、Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md) を使用して確認する必要があります。 認証後、アプリは API を使用してユーザー ロールを `GetParticipant` 取得できます。
> * ユーザー ロールに基づいて、アプリにはロール固有のエクスペリエンスを提供する機能があります。 たとえば、ポーリング アプリでは、開催者と発表者のみが新しい投票を作成できます。
> * 会議の進行中は、ロールの割り当てを変更できます。 詳細については、[Teams会議のロールを](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)参照してください。

### <a name="during-a-meeting"></a>会議中

会議中に、会議中の通知または会議中の通知を使用 `meetingSidePanel` して、アプリに固有のエクスペリエンスを構築できます。

#### <a name="meeting-sidepanel"></a>Meeting SidePanel

これにより `meetingSidePanel` 、開催者と発表者が異なるビューとアクションのセットを持つ会議のエクスペリエンスをカスタマイズできます。 アプリ マニフェストで、コンテキスト配列に追加 `meetingSidePanel` する必要があります。 会議とすべてのシナリオでは、アプリは 320 ピクセルの幅の会議内タブにレンダリングされます。 詳細については、「 [FrameContext インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)」を参照してください。

API を`userContext`使用して要求をルーティングするには、[SDK Teams](../tabs/how-to/access-teams-context.md#user-context)参照してください。 詳細については、[タブのTeams認証フローに関するページを参照してください](../tabs/how-to/authentication/auth-flow-tab.md)。 タブの認証フローは、Web サイトの認証フローに似ています。 そのため、タブでは OAuth 2.0 を直接使用できます。 詳細については、「[Microsoft ID プラットフォームおよび OAuth 2.0 承認コード フロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow)」を参照してください。

メッセージング拡張機能は、ユーザーが会議中ビューに表示されている場合に期待どおりに機能します。 ユーザーは、メッセージ拡張カードの作成を投稿できます。 会議中の AppName は、会議中の U バーのアプリ名を示すツールヒントです。

> [!NOTE]
> バージョン 1.7.0 以降の [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) は、以前のバージョンではサイド パネルがサポートされていないため、使用してください。

#### <a name="in-meeting-notification"></a>会議中の通知

会議内通知は、会議中に参加者を参加させたり、会議中に情報やフィードバックを収集したりするために使用されます。 [会議内通知ペイロード](API-references.md#send-an-in-meeting-notification)を使用して、会議内通知をトリガーします。 通知要求ペイロードの一部として、表示するコンテンツがホストされている URL を含めます。

会議中の通知では、タスク モジュールを使用しないでください。 タスク モジュールは会議チャットでは呼び出されません。 外部リソース URL は、会議中の通知を表示するために使用されます。 このメソッドを `submitTask` 使用して、会議チャットでデータを送信できます。

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="例は、会議中ダイアログを使用する方法を示しています。" border="true":::

#### <a name="shared-meeting-stage"></a>共有会議ステージ

共有会議ステージを使用すると、会議参加者はアプリ コンテンツとリアルタイムで対話し、共同作業を行うことができます。 アプリは、次の方法で共同作業会議ステージに共有できます。

* Teams クライアントの [ステージに共有] ボタンを使用して[、アプリ全体](#share-entire-app-to-stage)を共有してステージングします。
* Teams クライアント SDK の API を使用して[、アプリの特定の部分を共有してステージング](#share-specific-parts-of-the-app-to-stage)します。

##### <a name="share-entire-app-to-stage"></a>アプリ全体をステージに共有する

参加者は、アプリ側パネルの [共有からステージへ] ボタンを使用して、アプリ全体を共同作業会議ステージに共有できます。

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

ステージするアプリ全体を共有するには、アプリ マニフェストでフレーム コンテキストとして構成 `meetingStage` する `meetingSidePanel` 必要があります。 例:

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

詳細については、「 [アプリ マニフェスト](../resources/schema/manifest-schema-dev-preview.md#configurabletabs)」を参照してください。

##### <a name="share-specific-parts-of-the-app-to-stage"></a>ステージにアプリの特定の部分を共有する

参加者は、共有を使用して API をステージングすることで、アプリの特定の部分をコラボレーション会議ステージに共有できます。 API は、Teams クライアント SDK 内で使用でき、アプリのサイド パネルから呼び出されます。

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

ステージにアプリの特定の部分を共有するには、Teams クライアント SDK ライブラリで関連する API を呼び出す必要があります。 詳細については、 [API リファレンスを参照してください](API-references.md)。

> [!NOTE]
> * ステージするアプリの特定の部分を共有するには、マニフェスト バージョン 1.12 以降Teams使用します。
> * アプリの特定の部分をステージに共有することは、Teamsデスクトップ クライアントでのみサポートされています。

### <a name="after-a-meeting"></a>会議後

[会議](#before-a-meeting)の前後の構成は同じです。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会議アプリ | 会議トークン ジェネレーター アプリを使用してトークンを要求する方法を示します。 トークンは、各参加者が会議に参加する公平な機会を得られるように、順番に生成されます。 このトークンは、スクラム会議や Q&A セッションなどの状況で役立ちます。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|会議ステージのサンプル | コラボレーション用の会議ステージでタブを表示するサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|会議のサイド パネル | 会議のサイド パネルに議題を追加する方法を示すサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>ステップ バイ ステップのガイド

* [ステップ バイ ステップ ガイド](../sbs-meeting-token-generator.yml)に従って、Teams会議で会議トークンを生成します。
* [ステップ バイ ステップ ガイド](../sbs-meetings-sidepanel.yml)に従って、Teams会議で会議サイドパネルを生成します。
* [ステップ バイ ステップ ガイドに](../sbs-meetings-stage-view.yml)従って、Teams会議で会議のステージ ビューを共有します。
* [ステップ バイ ステップ ガイドに](../sbs-meeting-content-bubble.yml)従って、Teams会議で会議コンテンツバブルを生成します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [会議アプリ API リファレンス](API-references.md)

## <a name="see-also"></a>関連項目

* [会議中ダイアログの設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [タブの認証フローをTeamsする](../tabs/how-to/authentication/auth-flow-tab.md)
* [共有会議ステージ エクスペリエンスの設計ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Microsoft Graphを使用して会議にアプリを追加する](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
