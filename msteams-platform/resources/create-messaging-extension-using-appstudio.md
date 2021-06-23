---
title: App Studio を使用してメッセージングの拡張機能を作成する
author: surbhigupta
description: App Studio を使用してメッセージング拡張機能Microsoft Teams作成する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 61bfed969b981bd5000bdb6eca0bbd77196e8086
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069220"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>App Studio を使用してメッセージングの拡張機能を作成する

> [!TIP]
> 早く始める方法をお探しですか? ユーザー設定を[使用してメッセージング](../build-your-first-app/build-messaging-extension.md)拡張機能をMicrosoft Teams Toolkit。

高レベルでは、メッセージング拡張機能を作成するには、次の手順を実行する必要があります。

1. 開発環境を準備する
2. Web サービスを作成して展開する (開発中は ngrok のようなトンネリング サービスを使用してローカルで実行する)
3. Web サービスを Bot Framework に登録する
4. アプリ パッケージを作成する
5. Microsoft Teams にアプリ パッケージをアップロードする

Web サービスの作成、アプリ パッケージの作成、ボット フレームワークへの Web サービスの登録は、任意の順序で実行できます。 これらの 3 つのピースは非常に相互に絡み合うので、どの順序で行っても、他の部分を更新するには戻る必要があります。 登録には、展開された Web サービスからのメッセージング エンドポイントが必要であり、Web サービスには登録から作成された ID とパスワードが必要です。 アプリ マニフェストには、Web サービスに接続するための id Teamsも必要です。

メッセージング拡張機能を構築する場合、アプリ マニフェストの変更と Web サービスへのコードの展開の間を定期的に移動します。 アプリ マニフェストを操作する場合は、JSON ファイルを手動で操作するか、App Studio で変更を加えることができます。 いずれにしろ、マニフェストに変更を加える場合は Teams でアプリを再展開 (アップロード) する必要がありますが、Web サービスに変更を展開する場合は、アプリを再展開する必要はありません。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Web サービスを作成する

メッセージング拡張機能の中心は、Web サービスです。 通常、すべての要求を受信する単一 `/api/messages` のルートを定義します。 最初から始める場合は、いくつかのオプションから選択できます。

* Web サービスの [作成を](#learn-more) ガイドするクイック スタート チュートリアルのいずれかを使用します。
* Bot Framework サンプル リポジトリで使用できるメッセージング拡張機能のサンプルのいずれかを [選択します](https://github.com/Microsoft/BotBuilder-Samples) 。
* JavaScript を使用している場合は[、Yeoman](https://github.com/OfficeDev/generator-teams)ジェネレーターを使用して、Microsoft Teamsサービスを含む Teamsアプリをスキャフォールディングします。
* Web サービスを一から作成する。 お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。

## <a name="register-your-web-service-with-the-bot-framework"></a>Web サービスを Bot Framework に登録する

メッセージング拡張機能は、ボット フレームワークのメッセージング スキーマとセキュリティで保護された通信プロトコルを利用します。まだ Web サービスを持ってない場合は、ボット フレームワークに Web サービスを登録する必要があります。 Microsoft App Id (これを Teams の内部からボット ID と参照し、作業している可能性のある他のアプリ ID から識別します)、ボット フレームワークを使用した登録のメッセージング エンドポイントがメッセージング拡張機能で使用され、要求を受信して応答します。 既存の登録を使用している場合は、登録チャネルを有効[Microsoft Teamsしてください](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)。

クイック スタートの 1 つを実行するか、使用可能なサンプルの 1 つから開始する場合は、Web サービスの登録に関するガイドが表示されます。 サービスを手動で登録する場合は、3 つのオプションがあります。 Azure サブスクリプションを使用せずに登録する場合は、ボット フレームワークによって提供される簡略化された OAuth 認証フローを利用できます。 作成後に登録を Azure に移行できます。

* Azure サブスクリプションがある場合 (または新しいサブスクリプションを作成する場合) は、Azure Portal を使用して Web サービスを手動で登録できます。 "ボット チャネル登録" リソースを作成します。 無料の価格レベルを選択できます。ユーザーからのメッセージMicrosoft Teams、1 か月あたりの許容メッセージの総数にはカウントされません。
* Azure サブスクリプションを使用しない場合は、従来の登録ポータル [を使用できます](https://dev.botframework.com/bots/new)。
* App Studio は、Web サービス (ボット) の登録にも役立ちます。 App Studio を介して登録された Web サービスは Azure に登録されていません。 レガシ ポータル [を使用して](https://dev.botframework.com/bots) 、登録を表示、管理、および移行できます。

## <a name="create-your-app-manifest"></a>アプリ マニフェストを作成する

アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。

### <a name="create-your-app-manifest-using-app-studio"></a>App Studio を使用してアプリ マニフェストを作成する

アプリ マニフェストの作成に役立つアプリ Microsoft Teams App Studio アプリを使用できます。

1. Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー (**...**) から App Studio を開きます。 まだインストールされていない場合は、検索してインストールできます。
2. [マニフェスト エディター **] タブで****、[新** しいアプリの作成] を選択します (または、既存のアプリにメッセージング拡張機能を追加する場合は、アプリ パッケージをインポートできます)
3. アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。
4. [メッセージング拡張機能 **] タブで、[** セットアップ] ボタン **をクリック** します。
5. メッセージング拡張機能を使用する新しい Web サービス (ボット) を作成するか、ここで既に 1 つの select/add を登録している場合に使用できます。
6. 必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。 だいたい次のようになります: `https://someplace.com/api/messages`
7. [ **コマンド]** セクションの **[追加] ボタン** では、メッセージング拡張機能にコマンドを追加する方法について説明します。 コマンドの追加 [の詳細については](#learn-more) 、「詳細」セクションを参照してください。 メッセージング拡張機能には最大 10 のコマンドを定義できます。
8. [ **メッセージ ハンドラー] セクション** では、メッセージングがトリガーするドメインを追加できます。 詳細 [については、「リンクの分岐を](~/messaging-extensions/how-to/link-unfurling.md) 解除する」を参照してください。

[**完了] = [テスト>** 配布] タブから、アプリ パッケージ (アプリ マニフェストとアプリ アイコンを含む) をダウンロードするか、パッケージ **をインストールできます**。

### <a name="create-your-app-manifest-manually"></a>アプリ マニフェストを手動で作成する

ボットとタブと同様に、アプリのアプリ[](~/resources/schema/manifest-schema.md#composeextensions)マニフェストを更新して、メッセージング拡張機能のプロパティを含めます。 これらのプロパティは、メッセージング拡張機能がクライアントでどのように表示され、動作Microsoft Teamsします。 メッセージング拡張機能は、マニフェストの v1.0 からサポートされています。

#### <a name="declare-your-messaging-extension"></a>メッセージング拡張機能の宣言

メッセージング拡張機能を追加するには、アプリ マニフェストに新しいトップ レベルの JSON 構造をプロパティと一緒に含 `composeExtensions` めます。 アプリ用に 1 つのメッセージング拡張機能を作成し、最大 10 のコマンドを使用します。

> [!NOTE]
> マニフェストは、メッセージング拡張機能を次のように参照します `composeExtensions` 。 これは、下位互換性を維持するための方法です。

拡張定義は、次の構造を持つオブジェクトです。

| プロパティ名 | 用途 | 必須 |
|---|---|---|
| `botId` | Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 通常、これはアプリ全体の ID と同Teamsがあります。 | はい |
| `canUpdateConfiguration` | メニュー **設定** を有効にします。 | いいえ |
| `commands` | このメッセージング拡張機能がサポートするコマンドの配列。 コマンドは 10 に制限されています。 | はい |

#### <a name="define-your-commands"></a>コマンドの定義

メッセージング拡張機能は、ユーザーがメッセージング拡張機能をトリガーできる場所と操作の種類を定義する 1 つ以上のコマンドを宣言する必要があります。 メッセージング [拡張機能コマンドの](#learn-more) 詳細については、「詳細」を参照してください。

#### <a name="simple-manifest-example"></a>マニフェストの簡単な例

次の例は、検索コマンドを使用したアプリ マニフェスト内の単純なメッセージング拡張機能オブジェクトです。 これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。 完全な [例については、「アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md) 」を参照してください。

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a>アプリ マニフェストの完全な例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a>呼び出しメッセージ ハンドラーを追加する

ユーザーがメッセージング拡張機能をトリガーする場合は、最初の呼び出しメッセージを処理し、ユーザーから情報を収集し、その情報を処理し、適切に応答する必要があります。 これを行うには、まずメッセージング拡張機能に追加するコマンドの種類を決定し、アクション コマンドを追加するか、検索コマンド[](~/messaging-extensions/how-to/action-commands/define-action-command.md)を[追加する必要があります](~/messaging-extensions/how-to/search-commands/define-search-command.md)。

## <a name="messaging-extensions-in-teams-meetings"></a>会議でのメッセージングTeams拡張機能

> [!NOTE]
> 会議またはグループ チャットに名簿にユーザーがフェデレーションされている場合、Teams開催者を含むすべてのユーザーのメッセージング拡張機能へのアクセスが抑制されます。

会議が開始すると、Teams参加者は、ライブ通話中にメッセージング拡張機能と直接やり取りできます。 会議内メッセージング拡張機能を構築する場合は、次の点を考慮してください。

1. **Location**。 メッセージング拡張機能は、メッセージの作成領域、コマンド ボックス、または会議チャット@mentionedから呼び出すことができます。

1. **メタデータ**. メッセージング拡張機能が呼び出されると、ユーザーとテナントを識別 `userId` できます `tenantId` 。 `meetingId` は、`channelData` オブジェクトに含まれています。 アプリは、API 要求 `userId` とを `meetingId`  使用して `GetParticipant` ユーザー ロールを取得できます。

1. **コマンドの種類**。 メッセージ拡張機能でアクション ベースの [コマンドを使用する](../messaging-extensions/what-are-messaging-extensions.md#action-commands)場合は、タブのシングル サインオン [認証に従う必要](../tabs/how-to/authentication/auth-aad-sso.md) があります。

1. **ユーザー エクスペリエンス**。 メッセージング拡張機能は、会議の外部と同じように表示および動作する必要があります。

## <a name="next-steps"></a>次の手順

* [操作コマンドを作成する](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [検索コマンドを作成する](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [リンク展開](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>詳細情報

クイック スタートで試してみてください。

* C のクイック スタート#
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* JavaScript のクイック スタート
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

開発の概念Teams詳細を参照してください。

* [アプリTeamsについて](../concepts/capabilities-overview.md)
* [メッセージング拡張機能について](../messaging-extensions/what-are-messaging-extensions.md)
