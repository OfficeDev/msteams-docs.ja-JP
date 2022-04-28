---
title: メッセージ拡張機能のアクション コマンドを定義する
author: surbhigupta
description: アプリ マニフェストの例を使用したメッセージ拡張機能アクション コマンドの概要
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: ae0c39136b69b2759908bbbc54d1fff244eae0af
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103946"
---
# <a name="define-message-extension-action-commands"></a>メッセージ拡張機能のアクション コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

アクション コマンドを使用すると、Teamsでタスク モジュールと呼ばれるモーダル ポップアップをユーザーに表示できます。 タスク モジュールは、情報を収集または表示し、対話を処理し、Teamsに情報を返送します。 このドキュメントでは、アクション コマンドの呼び出し場所の選択、タスク モジュールの作成、最終メッセージまたはカードの送信、App Studio を使用したアクション コマンドの作成、手動での作成の方法について説明します。

アクション コマンドを作成する前に、次の要因を決定する必要があります。

1. [アクション コマンドはどこからトリガーできますか?](#select-action-command-invoke-locations)
1. [タスク モジュールはどのように作成されますか?](#select-how-to-create-your-task-module)
1. [最後のメッセージまたはカードはボットからチャネルに送信されますか、またはユーザーが送信するためにメッセージまたはカードを作成メッセージ領域に挿入しますか?](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>アクション コマンドの呼び出し場所を選択する

まず、アクション コマンドを呼び出す必要がある場所を決定する必要があります。 アプリ マニフェストでコマンドを `context` 指定すると、次の 1 つ以上の場所からコマンドを呼び出すことができます。

* メッセージ作成領域: 作成メッセージ領域の下部にあるボタン。

    コマンド コンテキスト = compose

* コマンド ボックス: コマンド ボックスにアプリを@mentioningします。

    コマンド コンテキスト = commandBox

   > [!NOTE]
   > メッセージ拡張機能がコマンド ボックスから呼び出された場合、会話に直接挿入されたボット メッセージで応答することはできません。

* メッセージ: メッセージのオーバーフロー メニューを使用して、既存の `...` メッセージから直接。

    コマンド コンテキスト = メッセージ

    > [!NOTE]
    > ボットへの最初の呼び出しには、その呼び出し元のメッセージを含む JSON オブジェクトが含まれます。 タスク モジュールを使用してメッセージを表示する前に、メッセージを処理できます。

次の図は、アクション コマンドが呼び出された場所を示しています。

![action コマンドの呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>タスク モジュールを作成する方法を選択する

コマンドの呼び出し元を選択するだけでなく、ユーザーのタスク モジュールでフォームを設定する方法も選択する必要があります。 タスク モジュール内でレンダリングされるフォームを作成するには、次の 3 つのオプションがあります。

* **静的なパラメーターの一覧**: これは最も簡単なメソッドです。 アプリマニフェストのパラメーターの一覧は、Teams クライアントのレンダリングを定義できますが、この場合は書式設定を制御できません。
* **アダプティブ カード**: アダプティブ カードを使用するように選択できます。これにより、UI をより細かく制御できますが、使用可能なコントロールと書式設定オプションは制限されます。
* **埋め込み Web ビュー**: カスタム Web ビューをタスク モジュールに埋め込んで、UI とコントロールを完全に制御することができます。

パラメーターの静的リストを使用してタスク モジュールを作成することを選択した場合、ユーザーがタスク モジュールを送信すると、メッセージ拡張機能が呼び出されます。 埋め込み Web ビューまたはアダプティブ カードを使用する場合、メッセージ拡張機能はユーザーからの初期呼び出しイベントを処理し、タスク モジュールを作成してクライアントに返す必要があります。

## <a name="select-how-the-final-message-is-sent"></a>最後のメッセージの送信方法を選択する

ほとんどの場合、アクション コマンドにより、メッセージの作成ボックスにカードが挿入されます。 ユーザーは、チャネルまたはチャットに送信できます。 この場合、メッセージはユーザーから送信され、ボットはカードをさらに編集または更新できません。

メッセージ拡張機能が作成ボックスから、またはメッセージから直接呼び出された場合、Web サービスは最終的な応答をチャネルまたはチャットに直接挿入できます。 この場合、アダプティブ カードはボットから取得され、ボットはそれを更新し、必要に応じて会話スレッドに返信します。 同じ ID を `bot` 使用し、適切なスコープを定義して、オブジェクトをアプリ マニフェストに追加する必要があります。

## <a name="add-the-action-command-to-your-app-manifest"></a>アプリ マニフェストにアクション コマンドを追加する

アクション コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON の最上位レベルに新しい `composeExtension` オブジェクトを追加する必要があります。 これを行うには、次のいずれかの方法を使用します。

* [App Studio を使用してアクション コマンドを作成する](#create-an-action-command-using-app-studio)
* [アクション コマンドを手動で作成する](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>App Studio を使用してアクション コマンドを作成する

**App Studio** または **Developer Portal** を使用してアクション コマンドを作成できます。

> [!NOTE]
> App Studio はまもなく廃止されます。 新しい[開発者ポータル](https://dev.teams.microsoft.com/)を使用して Teams アプリを構成、配布および管理する。

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> アクション コマンドを作成するための前提条件は、メッセージ拡張機能を既に作成していることです。 メッセージ拡張機能を作成する方法については、「メッセージ拡張機能 [の作成](~/messaging-extensions/how-to/create-messaging-extension.md)」を参照してください。

**アクション コマンドを作成するには**

1. Microsoft Teams クライアントから **App Studio** を開き、[**マニフェスト エディター**] タブを選択します。
1. **App Studio** でアプリ パッケージを既に作成している場合は、一覧から選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートしたら、[機能] で **[メッセージ拡張機能** ] を選択 **します**。 メッセージ拡張機能を設定するためのポップアップ ウィンドウが表示されます。
1. ウィンドウで **[セットアップ** ] を選択して、アプリ エクスペリエンスにメッセージ拡張機能を含めます。 次の図は、メッセージ拡張機能のセットアップ ウィンドウを表示します。

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. メッセージ拡張機能を作成するには、Microsoft 登録ボットが必要です。 既存のボットを使用するか、新しいボットを作成できます。 [ **新しいボットの作成** ] オプションを選択し、新しいボットの名前を付けて、[作成] を選択 **します**。 次の図は、メッセージ拡張機能のボットの作成を示しています。

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. メッセージ拡張機能の動作を決定するコマンドを含めるには、メッセージ拡張機能ページの [**コマンド] セクション** で [**追加]** を選択します。
次の図は、メッセージ拡張機能のコマンドの追加を表示します。

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. [**ユーザーがTeams内で外部サービスでアクションをトリガーできるようにする**] を選択します。 次の図は、アクション コマンドの選択を示しています。

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>

1. 静的パラメーター セットを使用してタスク モジュールを作成するには、 **コマンドの静的パラメーターのセットを定義するを選択します**。

    次の図は、action コマンドの静的パラメーターの選択を示しています。

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/>

    次の図は、静的パラメーターの設定例を示しています。

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    次の図は、静的パラメーターのテストの例を示しています。

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. 動的パラメーターを使用するには、 **ボットからパラメーターの動的セットをフェッチ** することを選択します。 次の図は、アクション コマンド パラメーターの選択を示しています。

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>

1. **コマンド ID と** タイトルを追加 **します**。
1. アクション コマンドを呼び出す場所を選択します。 次の図は、アクション コマンドの呼び出し場所を示しています。

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. **[保存]** を選択します。
1. さらにパラメーターを追加するには、[パラメーター] セクションの [**追加]** ボタンを選択します。

### <a name="create-an-action-command-manually"></a>アクション コマンドを手動で作成する

アクション ベースのメッセージ拡張機能コマンドをアプリ マニフェストに手動で追加するには、オブジェクトの配列に次のパラメーターを `composeExtension.commands` 追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このプロパティは、このコマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれています。 | はい | 1.0 |
| `title` | このプロパティはコマンド名です。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | このプロパティは 、 `action`. | いいえ | 1.4 |
| `fetchTask` | このプロパティは、 `true` タスク モジュールのアダプティブ カードまたは埋め込み Web ビュー、および`false` パラメーターの静的な一覧、または Web ビュー `taskInfo`を読み込むときに 、. | いいえ | 1.4 |
| `context` | このプロパティは、メッセージ拡張機能の呼び出し元を定義する値の省略可能な配列です。 使用可能な値: `message`、`compose`、`commandBox`。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

パラメーターの静的リストを使用している場合は、次のパラメーターも追加する必要があります。

| プロパティ名 | 用途 | 必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | このプロパティでは、コマンドのパラメーターの静的な一覧について説明します。 次の`false`場合`fetchTask`にのみ使用します。 | いいえ | 1.0 |
| `parameter.name` | このプロパティは、パラメーターの名前を記述します。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このプロパティは、指定する必要がある値のパラメーターの目的または例を説明します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | このプロパティは、ユーザー フレンドリな短いパラメーターのタイトルまたはラベルです。 | はい | 1.0 |
| `parameter.inputType` | このプロパティは、必要な入力の種類に設定されます。 指定できる値には`text`、, , , `textarea``number`, `date`, `time``toggle`. 既定値は .`text` | いいえ | 1.4 |

埋め込み Web ビューを使用している場合は、必要に応じて、ボットを `taskInfo` 直接呼び出さずに Web ビューをフェッチするオブジェクトを追加できます。 このオプションを選択した場合の動作は、パラメーターの静的な一覧を使用する動作と似ています。 ボットとの最初の対話が [タスク モジュール送信アクションに応答](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)するという点で。 オブジェクトを使用`taskInfo`している場合は、パラメーター`false`を `fetchTask` .

| プロパティ名 | 用途 | 必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
|`taskInfo`|メッセージ拡張コマンドを使用するときにプリロードするタスク モジュールを指定します。 | いいえ | 1.4 |
|`taskInfo.title`|初期タスク モジュールのタイトル。 |いいえ | 1.4 |
|`taskInfo.width`|タスク モジュールの幅(数値 (ピクセル単位)、または既定のレイアウト (例: `large`、 、 `medium`.`small` |いいえ | 1.4 |
|`taskInfo.height`|タスク モジュールの高さ(ピクセル単位の数値)、または既定のレイアウト (例: `large`、 `medium`または `small`.|なし | 1.4 |
|`taskInfo.url`|初期 Web ビュー URL。|いいえ | 1.4 |

#### <a name="app-manifest-example"></a>アプリ マニフェストの例

次のセクションは、2 つのアクション コマンドを `composeExtensions` 定義するオブジェクトの例です。 完全なマニフェストの例ではありません。 完全なアプリ マニフェスト スキーマについては、「 [アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md)」を参照してください。

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": true,
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
      }
    ]
  }
]
...
```

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams メッセージ拡張機能アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップ バイ ステップ ガイドに](../../../sbs-meetingextension-action.yml)従って、アクション ベースのメッセージ拡張機能Teams構築します。

## <a name="next-step"></a>次の手順

アダプティブ カードまたは埋め込み Web ビューをオブジェクトなしで `taskInfo` 使用している場合は、次の手順を実行します。

> [!div class="nextstepaction"]
> [タスク モジュールを使用して作成して応答する](~/messaging-extensions/how-to/action-commands/create-task-module.md)

パラメーターまたは埋め込み Web ビューをオブジェクトと共に `taskInfo` 使用する場合は、次の手順に進みます。

> [!div class="nextstepaction"]
> [タスク モジュールの送信に応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
