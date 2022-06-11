---
title: App Studio を使用してメッセージングの拡張機能を作成する
author: surbhigupta
description: App Studio を使用してMicrosoft Teamsメッセージング拡張機能を作成する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 09bc7a7884f69c7c3ac4c8e195e5ac6d14d20990
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032782"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>App Studio を使用してメッセージングの拡張機能を作成する

> [!TIP]
> より速く作業を開始する方法をお探しですか? Microsoft Teams Toolkitを使用して[メッセージング拡張機能](../build-your-first-app/build-messaging-extension.md)を作成します。

高いレベルでは、メッセージング拡張機能を作成するには、次の手順を完了する必要があります。

1. 開発環境を準備する
2. Web サービスを作成してデプロイする (開発中は、ngrok などのトンネリング サービスを使用してローカルで実行する)
3. Web サービスを Bot Framework に登録する
4. アプリ パッケージを作成する
5. Microsoft Teams にアプリ パッケージをアップロードする

Web サービスの作成、アプリ パッケージの作成、Web サービスの Bot Framework への登録は、任意の順序で行うことができます。 これらの 3 つの部分は非常に絡み合っているため、どの順序で行っても、他の部分を更新するには戻る必要があります。 登録にはデプロイされた Web サービスのメッセージング エンドポイントが必要であり、Web サービスには登録から作成された ID とパスワードが必要です。 また、アプリ マニフェストでは、Teamsを Web サービスに接続するためにその ID も必要です。

メッセージング拡張機能を構築するときに、アプリ マニフェストの変更と Web サービスへのコードのデプロイの間を定期的に移動します。 アプリ マニフェストを使用する場合は、JSON ファイルを手動で変更するか、App Studio を使用して変更できることを確認します。 いずれの場合も、マニフェストに変更を加える際にアプリをTeamsに再デプロイ (アップロード) する必要がありますが、Web サービスに変更をデプロイする場合は、その必要はありません。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Web サービスを作成する

メッセージング拡張機能の中心は、Web サービスです。 通常、すべての要求を受信する単一のルート `/api/messages`が定義されます。 最初から作業を開始する場合は、いくつかのオプションから選択できます。

* Web サービスの作成をガイドする [クイック スタート](#learn-more) のチュートリアルのいずれかを使用します。
* [Bot Framework サンプル リポジトリ](https://github.com/Microsoft/BotBuilder-Samples)で使用できるメッセージング拡張機能のサンプルの 1 つを選択します。
* JavaScript を使用している場合は、[Yeoman ジェネレーター](https://github.com/OfficeDev/generator-teams)を使用してMicrosoft Teamsを使用して、Web サービスを含むTeams アプリをスキャフォールディングします。
* Web サービスを一から作成する。 お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。

## <a name="register-your-web-service-with-the-bot-framework"></a>Web サービスを Bot Framework に登録する

メッセージング拡張機能は、Bot Framework のメッセージング スキーマとセキュリティで保護された通信プロトコルを利用します。まだお持ちでない場合は、Bot Framework に Web サービスを登録する必要があります。 Microsoft アプリ ID (この ID は、Teamsの内部からボット ID として参照され、操作している可能性がある他のアプリ ID から識別します) と、Bot Framework に登録したメッセージング エンドポイントがメッセージング拡張機能で使用され、要求の受信と応答が行われます。 既存の登録を使用している場合は、[Microsoft Teams チャネルを有効に](/azure/bot-service/bot-service-manage-channels?preserve-view=true&view=azure-bot-service-4.0)していることを確認します。

クイック スタートの 1 つに従うか、使用可能なサンプルの 1 つから開始する場合は、Web サービスの登録について説明します。 サービスを手動で登録する場合は、3 つの方法があります。 Azure サブスクリプションを使用せずに登録することを選択した場合、Bot Framework によって提供される簡単な OAuth 認証フローを利用することはできません。 作成後、登録を Azure に移行できます。

* Azure サブスクリプション (または新しいサブスクリプションを作成する場合) がある場合は、Microsoft Azure ポータルを使用して Web サービスを手動で登録できます。 "Bot Channels Registration" リソースを作成します。 無料の価格レベルを選択できます。Microsoft Teamsからのメッセージは、1 か月あたりの許容されるメッセージの合計にはカウントされません。
* Azure サブスクリプションを使用しない場合は、 [レガシ登録ポータル](https://dev.botframework.com/bots/new)を使用できます。
* App Studio は、Web サービス (ボット) の登録にも役立ちます。 App Studio を介して登録された Web サービスは、Azure に登録されません。 [レガシ ポータル](https://dev.botframework.com/bots)を使用して、登録を表示、管理、および移行できます。

## <a name="create-your-app-manifest"></a>アプリ マニフェストを作成する

アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。

### <a name="create-your-app-manifest-using-app-studio"></a>App Studio を使用してアプリ マニフェストを作成する

Microsoft Teams クライアント内から App Studio アプリを使用すると、アプリ マニフェストの作成に役立ちます。

1. Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー (**...**) から App Studio を開きます。 まだインストールされていない場合は、それを検索して行うことができます。
2. [ **マニフェスト エディター** ] タブ **で [新しいアプリの作成** ] を選択します (または、既存のアプリにメッセージング拡張機能を追加する場合は、アプリ パッケージをインポートできます)
3. アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。
4. [ **メッセージング拡張機能** ] タブで、[ **セットアップ** ] ボタンを選択します。
5. メッセージング拡張機能で使用する新しい Web サービス (ボット) を作成するか、選択または追加をここで既に登録している場合に作成できます。
6. 必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。 だいたい次のようになります: `https://someplace.com/api/messages`
7. **[コマンド**] セクションの **[追加]** ボタンを使用すると、メッセージング拡張機能にコマンドを追加できます。 コマンドの追加に関する詳細については、「 [詳細情報](#learn-more) 」セクションを参照してください。 メッセージング拡張機能には最大 10 個のコマンドを定義できることに注意してください。
8. **[メッセージ ハンドラー]** セクションでは、メッセージングがトリガーするドメインを追加できます。 詳細については、 [リンクの展開](~/messaging-extensions/how-to/link-unfurling.md) を参照してください。

**[完了] => [テストと配布**] タブから、アプリ パッケージ (アプリ マニフェストとアプリ アイコンを含む) を **ダウンロード** するか、パッケージを **インストール** できます。

### <a name="create-your-app-manifest-manually"></a>アプリ マニフェストを手動で作成する

ボットとタブと同様に、 [アプリのアプリ マニフェスト](~/resources/schema/manifest-schema.md#composeextensions) を更新して、メッセージング拡張機能のプロパティを含めます。 これらのプロパティは、Microsoft Teams クライアントでのメッセージング拡張機能の表示と動作を制御します。 メッセージング拡張機能は、マニフェストの v1.0 以降でサポートされています。

#### <a name="declare-your-messaging-extension"></a>メッセージング拡張機能を宣言する

メッセージング拡張機能を追加するには、プロパティを使用してアプリ マニフェストに新しい最上位レベルの JSON 構造を `composeExtensions` 含めます。 アプリ用に 1 つのメッセージング拡張機能を作成し、最大 10 個のコマンドを使用します。

> [!NOTE]
> マニフェストは、メッセージング拡張機能 `composeExtensions`を . これは、下位互換性を維持するためです。

拡張機能定義は、次の構造を持つオブジェクトです。

| プロパティ名 | 用途 | 必須 |
|---|---|---|
| `botId` | Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは通常、Teams アプリ全体の ID と同じである必要があります。 | はい |
| `canUpdateConfiguration` | **メニュー項目設定** 有効にします。 | 不要 |
| `commands` | このメッセージング拡張機能がサポートするコマンドの配列。 コマンドは 10 個に制限されています。 | はい |

#### <a name="define-your-commands"></a>コマンドを定義する

メッセージング拡張機能では、ユーザーがメッセージング拡張機能をトリガーできる場所と対話の種類を定義する 1 つ以上のコマンドを宣言する必要があります。 メッセージング拡張機能コマンドの詳細については、 [こちらを](#learn-more) 参照してください。

#### <a name="simple-manifest-example"></a>マニフェストの簡単な例

次の例は、検索コマンドを使用したアプリ マニフェスト内の単純なメッセージング拡張機能オブジェクトです。 これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。 完全な例については、 [アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md) を参照してください。

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

#### <a name="complete-app-manifest-example"></a>完全なアプリ マニフェストの例

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

ユーザーがメッセージング拡張機能をトリガーしたら、最初の呼び出しメッセージを処理し、ユーザーから情報を収集してから、その情報を処理して適切に応答する必要があります。 これを行うには、まず、メッセージング拡張機能に追加するコマンドの種類を決定し、 [アクション コマンドを追加](~/messaging-extensions/how-to/action-commands/define-action-command.md) するか [、検索コマンドを追加](~/messaging-extensions/how-to/search-commands/define-search-command.md)する必要があります。

## <a name="messaging-extensions-in-teams-meetings"></a>Teams会議のメッセージング拡張機能

> [!NOTE]
> 会議またはグループ チャットでユーザーが名簿にフェデレーションされている場合、Teamsは、開催者を含むすべてのユーザーのメッセージング拡張機能へのアクセスを抑制します。

会議が開始されると、Teams参加者はライブ通話中にメッセージング拡張機能と直接対話できます。 会議中のメッセージング拡張機能を構築する場合は、次の点を考慮してください。

1. **Location**。 メッセージング拡張機能は、会議チャットのメッセージ作成領域、コマンド ボックス、または@mentionedから呼び出すことができます。

1. **メタデータ**。 メッセージング拡張機能が呼び出されると、ユーザーとテナント`userId``tenantId`を識別できます。 `meetingId` は、`channelData` オブジェクトに含まれています。 アプリでは、API 要求と `meetingId` API 要求を`GetParticipant`使用`userId`してユーザー ロールを取得できます。

1. **コマンドの種類**。 メッセージ拡張機能で [アクション ベースのコマンド](../messaging-extensions/what-are-messaging-extensions.md#action-commands)を使用している場合は、 [タブのシングル サインオン認証に](../tabs/how-to/authentication/tab-sso-overview.md) 従う必要があります。

1. **ユーザー エクスペリエンス**。 メッセージング拡張機能は、会議の外部と同じように見え、動作する必要があります。

## <a name="next-steps"></a>次の手順

* [操作コマンドを作成する](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [検索コマンドを作成する](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [リンク展開](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>詳細情報

クイック スタートで試してください。

* C のクイック スタート#
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* JavaScript のクイック スタート
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

Teams開発の概念について詳しくは、以下をご覧ください。

* [アプリの機能Teams理解する](../concepts/capabilities-overview.md)
* [メッセージング拡張機能について](../messaging-extensions/what-are-messaging-extensions.md)
