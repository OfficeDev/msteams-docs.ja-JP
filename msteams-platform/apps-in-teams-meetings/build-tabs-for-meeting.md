---
title: 会議のタブを作成する
author: surbhigupta
description: Microsoft Teams 会議で会議チャット、会議サイド パネル、会議ステージのタブを作成する方法について説明します。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: d86f0931cb6338ef331f2afe3a4a5fdb217bb316
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615432"
---
# <a name="build-tabs-for-meeting"></a>会議のタブを作成する

それぞれのチームには、コミュニケーションとタスクの共同作業を行うそれぞれの方法があります。 これらのさまざまなタスクを達成するために、会議用アプリを使用して Teams をカスタマイズします。 Teams 会議用のアプリを有効にし、アプリマニフェスト内の会議スコープでアプリを使用できるようにアプリを構成します。

## <a name="tabs-in-teams-meetings"></a>Teams 会議のタブ

タブを使用すると、会議参加者は会議内の特定のスペース内のサービスとコンテンツにアクセスできます。 Microsoft Teams タブ開発を初めて使用する場合は、「 [Teams のビルド タブ](/microsoftteams/platform/tabs/what-are-tabs)」を参照してください。

会議タブを作成する前に、会議チャット ビュー、会議の詳細ビュー、会議サイド パネル ビュー、会議ステージ ビューをターゲットにできるサーフェスについて学習することが重要です。

### <a name="meeting-details-view"></a>会議の詳細ビュー

1. 予定表で、タブを追加する会議を選択します。
1. [ **詳細** ] タブを選択し、 を選択します :::image type="icon" source="../assets/icons/add-icon.png" Border = "false":::。 アプリ ギャラリーが表示されます。

   :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="このスクリーンショットは、Teams 会議での会議前アプリエクスペリエンスを示しています。":::

1. アプリ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 タブが会議の詳細ページに追加されます。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

次の図は、Teams デスクトップ クライアントの会議の詳細ページに追加されたタブを示しています。

   :::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="スクリーンショットは、Teams 会議の会議の詳細ビューのデスクトップ Teams タブを示しています。":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

次の図は、Teams モバイル クライアントの会議の詳細ページに追加されたタブを示しています。

   :::image type="content" source="../assets/images/mobile-tab.png" alt-text="スクリーンショットは、Teams 会議の会議の詳細ビューにモバイル Teams タブを示しています。":::

---

### <a name="meeting-chat-view"></a>会議チャット ビュー

1. Teams チャット パネルで、会議チャット ビューを選択します。

1. 選択 :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: すると、アプリ ギャラリーが表示されます。

1. アプリ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 タブが会議チャットに追加されます。

   :::image type="content" source="../assets/images/apps-in-meetings/meeting-chat-view.png" alt-text="スクリーンショットは、Teams 会議の会議チャット ビューを示しています。":::

### <a name="meeting-side-panel-view"></a>会議側パネル ビュー

1. 会議中に、[Teams の会議] ウィンドウから **[アプリ**] を選択:::image type="icon" source="../assets/icons/add-icon.png" Border = "false":::して、会議にアプリを追加できます。

   :::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="このスクリーンショットは、Teams 会議ウィンドウにアプリを追加する方法を示しています。":::

1. アプリ ギャラリーで、追加するアプリを選択し、必要に応じて手順に従います。 アプリが会議のサイド パネルに追加されます。

   :::image type="content" source="../assets/images/side-panel-view.png" alt-text="このスクリーンショットは、アプリの一覧を含むサイド パネル ビューを示しています。":::

### <a name="meeting-stage-view"></a>会議ステージ ビュー

1. 会議のサイド パネルにタブを追加したら、グローバル アプリ共有を選択できるようになりました。

1. これにより、会議のすべての参加者のステージの [レンダリング] タブが表示されます。

   :::image type="content" source="../assets/images/meeting-stage-view.png" alt-text="このスクリーンショットは、会議に共有したアプリの会議ステージ ビューを示しています。":::

### <a name="apps-in-channel-meeting"></a>チャネル会議のアプリ

パブリックスケジュールされたチャネル会議には、親チームと同じアプリの一覧があります。 チャネル会議にアプリをインストールすると、親チームで利用できるようになります。また、その逆も同様です。

ただし、チャネル会議のタブ インスタンスは、チャネル自体のタブとは別です。 たとえば、 *開発* チャネルに *[Polly* ] タブがあるとします。そのチャネルで *Standup* 会議を作成する場合、その会議に明示的にタブを追加するまで、その会議には *Polly* [タブ](#meeting-details-view)はありません。

パブリックスケジュールチャネル会議では、会議タブが追加された後、会議の詳細ページで会議オブジェクトを選択してタブにアクセスできます。

:::image type="content" source="~/assets/images/apps-in-meetings/after-a-meeting1.png" alt-text="会議後":::

> [!NOTE]
> モバイルでは、匿名ユーザーはスケジュールされたパブリック チャネル会議でアプリにアクセスできません。

### <a name="app-manifest-settings-for-tabs-in-meeting"></a>会議のタブのアプリ マニフェスト設定

関連するコンテキスト プロパティを使用して [アプリ マニフェスト](/microsoftteams/platform/resources/schema/manifest-schema) を更新し、さまざまなタブ ビューを構成します。 会議アプリの機能は、configurableTabs セクションのスコープとコンテキスト配列を使用して、アプリ マニフェストで宣言されます。

#### <a name="scope"></a>範囲

スコープは、アプリにアクセスできるユーザーを定義します。

* `groupchat` スコープを使用すると、アプリをグループ スコープで使用できるようになり、アプリを通話または会議 (スケジュールされたプライベート会議またはインスタント会議) に追加できます。

* `team` スコープを使用すると、アプリをチーム スコープで使用できるようになり、アプリをチームまたはチャネルまたはスケジュールされたチャネル会議に追加できます。

#### <a name="context"></a>Context

このプロパティは `context` 、インストールと構成後にアプリを特定のビューで使用できるかどうかを決定します。 値のすべてまたは一部を `context` 使用できるプロパティの値を次に示します。

|値|説明|
|---|---|
| **channelTab** | チーム チャネルのヘッダーのタブ。 |
| **privateChatTab** | チームや会議のコンテキストではない一連のユーザー間のグループ チャットのヘッダーにあるタブ。 |
| **meetingChatTab** | スケジュールされた会議の一連のユーザー間のグループ チャットのヘッダーにあるタブ。 **meetingChatTab** または **meetingDetailsTab** を指定すると、アプリをモバイルで実行できるようになります。 |
| **meetingDetailsTab** | 予定表の会議の詳細ビューのヘッダーにあるタブ。 **meetingChatTab** または **meetingDetailsTab** を指定すると、アプリをモバイルで実行できるようになります。 |
| **meetingSidePanel** | 統合バー (U バー) 経由で開かれる会議内パネル。 |
| **meetingStage** | 会議ステージに共有できる `meetingSidePanel` からのアプリ。 このアプリは、モバイル クライアントでも Teams Room クライアントでも使用できません。 |

#### <a name="configure-tab-app-for-a-meeting"></a>会議のタブ アプリを構成する

会議のアプリでは、次のコンテキストを使用できます: `meetingChatTab`、`meetingDetailsTab`、`meetingSidePanel`、`meetingStage`。 会議参加者がアプリをインストールし、会議のタブを構成すると、特定の会議のアプリの他のすべてのコンテキストがタブのレンダリングを開始します。

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

---

#### <a name="other-examples"></a>その他の例

タブの既定のコンテキスト (指定されていない場合) は次のとおりです。  

```json
"context":[ 
  "channelTab", 
  "privateChatTab", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

アプリが会議グループ以外のチャットで表示されないようにするには、次のコンテキストを設定する必要があります。

```json
"context":[ 
  "meetingSidePanel", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

会議中のサイド パネルエクスペリエンスの場合のみ:  

```json
"context":[ 
  "meetingSidePanel" 
     ] 
```

### <a name="advanced-tab-sdk-apis"></a>Advanced Tab SDK API

Microsoft Teams JavaScript クライアント SDK は、JavaScript を使用してタブを作成するために使用される豊富な SDK です。 Teams、Office、および Outlook で作業するには、最新の TeamsJS (V.2.0 以降) を使用します。 詳細については、「[Teams JavaScript クライアント SDK](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk?tabs=javascript%2Cmanifest-teams-toolkit)」を参照してください。

### <a name="frame-context"></a>フレーム コンテキスト

Microsoft Teams JavaScript ライブラリでは、会議タブの URL が getContext API に読み込まれる frameContext が公開されます。 frameContext の使用可能な値は、コンテンツ、タスク、設定、削除、sidePanel、meetingStage です。 これにより、アプリがレンダリングされる場所に基づいてカスタマイズされたエクスペリエンスを構築できます。 たとえば、特定のコラボレーションに焦点を当てた UI をチャット タブ (`content`) に`meetingStage`表示し、別の会議準備 UI を表示します。 詳細については、「 [getContext API](/microsoftteams/platform/tabs/how-to/access-teams-context?tabs=teamsjs-v2)」を参照してください。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会議アプリ | 会議トークン ジェネレーター アプリを使用してトークンを要求する方法を示します。 各参加者が会議に参加する機会を公平に得られるように、トークンは順次生成されます。 このトークンは、スクラム会議や Q&A セッションなどの状況で役立ちます。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会議ステージのサンプル | 共同作業のために会議ステージでタブを表示するサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| 会議のサイド パネル | 会議のサイド パネルに議題を追加する方法を示すサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|
| 会議中の通知 | ボットを使用して会議内通知を実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| 会議中のドキュメント署名 | ドキュメント署名 Teams アプリを実装する方法を示します。 ステージ、Teams SSO、ユーザー固有のステージ ビューへの特定のアプリ コンテンツの共有が含まれます。 | [表示](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | 該当なし |

> [!NOTE]
>
> * 会議アプリ (サイド パネルと会議ステージ) は、Teams デスクトップ クライアントでサポートされています。
> * Teams Web クライアントの会議アプリ (サイド パネルと会議ステージ) は、 [開発者プレビューが有効になっている](/microsoftteams/platform/resources/dev-preview/developer-preview-intro#enable-developer-preview)場合にのみサポートされます。

## <a name="step-by-step-guides"></a>ステップ バイ ステップのガイド

* [ステップバイステップ ガイド](../sbs-meeting-token-generator.yml)に従って、Teams 会議で会議トークンを生成します。
* ステップ [バイ ステップ ガイドに](../sbs-meetings-sidepanel.yml) 従って、Teams 会議で会議のサイド パネルを生成します。
* [ステップバイステップ ガイド](../sbs-meetings-stage-view.yml)に従って、Teams 会議で会議ステージ ビューを共有します。
* ステップ [バイ ステップ ガイド](../sbs-meeting-content-bubble.yml) に従って、Teams 会議で会議内通知を生成します。

## <a name="see-also"></a>関連項目

* [会議中の通知の設計ガイドライン](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [共有会議ステージ エクスペリエンスの設計ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Microsoft Graph を使用して会議にアプリを追加する](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
