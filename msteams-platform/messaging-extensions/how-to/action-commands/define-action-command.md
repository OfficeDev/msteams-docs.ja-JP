---
title: メッセージング拡張機能アクション コマンドの定義
author: clearab
description: メッセージング拡張機能アクション コマンドの概要
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f49e821ecb98659b4cfd68f93b37f1a8f611a9fb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020717"
---
# <a name="define-messaging-extension-action-commands"></a>メッセージング拡張機能アクション コマンドの定義

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

アクション コマンドを使用すると、Teams のタスク モジュールと呼ばれるモーダル ポップアップをユーザーに表示できます。 タスク モジュールは、情報を収集または表示し、対話を処理し、その情報を Teams に送信します。 このドキュメントでは、アクション コマンドの呼び出し場所の選択、タスク モジュールの作成、最終メッセージまたはカードの送信、アプリ スタジオを使用したアクション コマンドの作成、または手動での作成方法について説明します。 

アクション コマンドを作成する前に、次の要素を決定する必要があります。

1. [アクション コマンドはどこからトリガーできますか?](#select-action-command-invoke-locations)
1. [タスク モジュールの作成方法](#select-how-to-create-your-task-module)
1. [最終的なメッセージまたはカードはボットからチャネルに送信されますか、それともメッセージまたはカードがユーザーが送信するメッセージの作成領域に挿入されますか?](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>Select action command invoke locations

まず、アクション コマンドを呼び出す場所を決定する必要があります。 アプリ マニフェストで指定すると、次の 1 つ以上の場所からコマンド `context` を呼び出すことができます。

* メッセージの作成領域: 作成メッセージ領域の下部にあるボタン。
* [コマンド] ボックス: @mentioningボックスにアプリを追加します。 
   > [!NOTE]
   > コマンド ボックスからメッセージング拡張機能が呼び出された場合は、ボット メッセージをスレッドに直接挿入して応答できません。

* メッセージ: 既存のメッセージから、メッセージのオーバーフロー `...` メニューから直接移動します。 
    > [!NOTE] 
    > ボットへの最初の呼び出しには、呼び出されたメッセージを含む JSON オブジェクトが含まれます。 メッセージをタスク モジュールで表示する前に、メッセージを処理できます。

次の図は、アクション コマンドが呼び出された場所を表示します。

![action コマンドの呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>タスク モジュールの作成方法を選択する

コマンドの呼び出し先を選択する以外に、ユーザーのタスク モジュールにフォームを設定する方法も選択する必要があります。 タスク モジュール内でレンダリングされるフォームを作成するには、次の 3 つのオプションがあります。   

* **パラメーターの静的な一覧**: これは最も簡単な方法です。 アプリ マニフェストで Teams クライアントがレンダリングするパラメーターの一覧を定義できますが、この場合は書式設定を制御できません。
* **アダプティブ カード**: アダプティブ カードの使用を選択すると、UI の制御が向上しますが、使用可能なコントロールと書式設定オプションは制限されます。
* **埋め込み Web ビュー**: カスタム Web ビューをタスク モジュールに埋め込み、UI とコントロールを完全に制御できます。 

パラメーターの静的リストを使用してタスク モジュールを作成する場合、ユーザーがタスク モジュールを送信すると、メッセージング拡張機能が呼び出されます。 埋め込み Web ビューまたはアダプティブ カードを使用する場合、メッセージング拡張機能は、ユーザーからの最初の呼び出しイベントを処理し、タスク モジュールを作成し、クライアントに戻す必要があります。

## <a name="select-how-the-final-message-is-sent"></a>最終メッセージの送信方法を選択する

ほとんどの場合、アクション コマンドを実行すると、作成メッセージ ボックスにカードが挿入されます。 ユーザーはチャネルまたはチャットに送信できます。 この場合、メッセージはユーザーから送信され、ボットはカードをさらに編集または更新できません。

メッセージング拡張機能が作成ボックスから、またはメッセージから直接呼び出された場合、Web サービスは最終的な応答をチャネルまたはチャットに直接挿入できます。 この場合、アダプティブ カードはボットから取得され、ボットによって更新され、必要に応じてスレッドに返信されます。 同じ ID を使用して適切なスコープを定義して、アプリ マニフェストに `bot` オブジェクトを追加する必要があります。

## <a name="add-the-action-command-to-your-app-manifest"></a>アクション コマンドをアプリ マニフェストに追加する

アクション コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON のトップ レベルに新しいオブジェクト `composeExtension` を追加する必要があります。 これを行うには、次のいずれかの方法を使用できます。

* [App Studio を使用してアクション コマンドを作成する](#create-an-action-command-using-app-studio)
* [アクション コマンドを手動で作成する](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>App Studio を使用してアクション コマンドを作成する

> [!NOTE]
> アクション コマンドを作成する前提条件は、メッセージング拡張機能を既に作成している必要があります。 メッセージング拡張機能を作成する方法の詳細については、「Create [a messaging extension 」を参照してください](~/messaging-extensions/how-to/create-messaging-extension.md)。

**アクション コマンドを作成するには**

1. Microsoft **Teams クライアントから App Studio** を開き、[マニフェスト エディター] **タブを選択** します。
1. App Studio でアプリ パッケージを既に作成している **場合** は、一覧からアプリ パッケージを選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートした後、[機能] で [ **メッセージング拡張機能]** **を選択します**。 メッセージング拡張機能を設定するポップアップ ウィンドウが表示されます。
1. ウィンドウ **で [セットアップ** ] を選択して、メッセージング拡張機能をアプリ エクスペリエンスに含めます。 次の図は、メッセージング拡張機能のセットアップ ウィンドウを表示します。

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. メッセージング拡張機能を作成するには、Microsoft 登録済みのボットが必要です。 既存のボットを使用するか、新しいボットを作成できます。 [ **新しいボットの作成]** オプションを選択し、新しいボットの名前を付け、[作成] を **選択します**。 次の図は、メッセージング拡張機能のボットの作成を表示します。

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. [ **メッセージング拡張機能** ] **ページの [コマンド** ] セクションで [追加] を選択して、メッセージング拡張機能の動作を決定するコマンドを含めます。   
次の図は、メッセージング拡張機能のコマンド追加を表示します。

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. [Teams **の内部で外部サービスのアクションをトリガーするユーザーを許可する] を選択します**。 次の図は、アクション コマンドの選択を表示します。

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. 静的な一連のパラメーターを使用してタスク モジュールを作成するには、[コマンドの静的パラメーターのセット **を定義する] を選択します**。 

    次の図は、アクション コマンドの静的パラメーターの選択を表示します。

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    次の図は、静的パラメーターのセットアップ例を示しています。 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    次の図は、静的パラメーターテストの例を示しています。

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. 動的パラメーターを使用するには、[ボットからパラメーター **の動的セットをフェッチする] を選択します**。 次の図は、アクション コマンド パラメーターの選択を表示します。

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. コマンド ID **と Title** を **追加します**。
1. アクション コマンドを呼び出す場所を選択します。 次の図は、アクション コマンドの呼び出し場所を表示します。

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. **[保存]** を選択します。
1. パラメーターを追加するには、[パラメーター] セクション **の [追加** ] ボタン **を選択** します。

### <a name="create-an-action-command-manually"></a>アクション コマンドを手動で作成する

アクション ベースのメッセージング拡張機能コマンドをアプリ マニフェストに手動で追加するには、次のパラメーターをオブジェクトの `composeExtension.commands` 配列に追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このプロパティは、このコマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれます。 | はい | 1.0 |
| `title` | このプロパティはコマンド名です。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | このプロパティは、 である必要があります `action` 。 | いいえ | 1.4 |
| `fetchTask` | このプロパティは、タスク モジュールのアダプティブ カードまたは埋め込み Web ビュー、およびパラメーターの静的リストまたは Web ビューを読み込むときにに設定 `true` `false` されます `taskInfo` 。 | いいえ | 1.4 |
| `context` | このプロパティは、メッセージング拡張機能の呼び出し先を定義する値の任意の配列です。 使用可能な値: `message`、`compose`、`commandBox`。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

静的なパラメーターの一覧を使用している場合は、次のパラメーターも追加する必要があります。

| プロパティ名 | 用途 | 必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | このプロパティは、コマンドのパラメーターの静的な一覧を示します。 の場合にのみ `fetchTask` 使用します `false` 。 | いいえ | 1.0 |
| `parameter.name` | このプロパティは、パラメーターの名前を表します。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このプロパティは、パラメーターの目的または指定する必要がある値の例を示します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | このプロパティは、短いユーザーフレンドリーなパラメーターのタイトルまたはラベルです。 | はい | 1.0 |
| `parameter.inputType` | このプロパティは、必要な入力の種類に設定されます。 指定できる値には `text` `textarea` 、、 `number` 、 、 、 `date` 、 `time` が含まれます `toggle` 。 既定値は に設定されます `text` 。 | いいえ | 1.4 |

埋め込み Web ビューを使用している場合は、ボットを直接呼び出さずに、必要に応じてオブジェクトを追加して Web ビュー `taskInfo` をフェッチできます。 このオプションを選択した場合の動作は、静的なパラメーターの一覧を使用する動作と似ています。 ボットとの最初のやり取りが [タスク モジュール送信アクションに応答しているという場合](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。 オブジェクトを使用している場合 `taskInfo` は、パラメーターをに設定 `fetchTask` する必要があります `false` 。

| プロパティ名 | 用途 | 必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
|`taskInfo`|メッセージング拡張機能コマンドを使用するときにプリロードするタスク モジュールを指定します。 | いいえ | 1.4 |
|`taskInfo.title`|初期タスク モジュールのタイトル。 |いいえ | 1.4 |
|`taskInfo.width`|タスク モジュールの幅 (ピクセル単位の数値または既定のレイアウトなど) `large` `medium` `small` |いいえ | 1.4 |
|`taskInfo.height`|タスク モジュールの高さ (ピクセル単位の数値または既定のレイアウトなど) `large` `medium` `small`|いいえ | 1.4 |
|`taskInfo.url`|初期 Web ビューの URL。|いいえ | 1.4 | 

#### <a name="app-manifest-example"></a>アプリ マニフェストの例

次のセクションは、2 つのアクション コマンド `composeExtensions` を定義するオブジェクトの例です。 完全なマニフェストの例ではありません。 完全なアプリ マニフェスト スキーマについては、「アプリ マニフェスト [スキーマ」を参照してください](~/resources/schema/manifest-schema.md)。

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
|Teams メッセージング拡張機能アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams メッセージング拡張機能の検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>次の手順

アダプティブ カードまたはオブジェクトのない埋め込み Web ビューのいずれかを使用している場合、次の `taskInfo` 手順は次のとおりです。

> [!div class="nextstepaction"]
> [タスク モジュールを使用して作成および応答する](~/messaging-extensions/how-to/action-commands/create-task-module.md)

オブジェクトでパラメーターまたは埋め込み Web ビューを使用する場合は、次 `taskInfo` の手順を実行します。

> [!div class="nextstepaction"]
> [タスク モジュールの送信に応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

