---
title: メッセージ拡張機能のアクション コマンドを定義する
author: surbhigupta
description: このモジュールでは、Microsoft Teams でアプリ マニフェストの例を使用してメッセージング拡張機能アクション コマンドを定義する方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0b51d34aaacfe38c077b03b5df8bb6a9227c5b61
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363460"
---
# <a name="define-message-extension-action-commands"></a>メッセージ拡張機能のアクション コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> メッセージ アクションが開始されると、添付ファイルの詳細は呼び出しアクティビティの `turncontext` 一部として送信されません。

アクション コマンドを使用すると、Teams のタスク モジュールと呼ばれるモーダル ポップアップをユーザーに表示できます。 タスク モジュールは、情報を収集または表示し、対話を処理し、Teams に情報を送信します。 このドキュメントでは、操作コマンドを呼び出す場所の選択、タスク モジュールの作成、最終メッセージまたはカードの送信、App Studio を使用した操作コマンドの作成、手動での作成方法について説明します。

操作コマンドを作成する前に、次の要因を決定する必要があります。

1. [操作コマンドはどこからトリガーできますか?](#select-action-command-invoke-locations)
1. [タスク モジュールはどのように作成されますか?](#select-how-to-create-your-task-module)
1. [最終メッセージまたはカードはボットからチャネルに送信されるか、またはユーザーが送信するためにメッセージまたはカードを作成メッセージ領域に挿入しますか?](#select-how-the-final-message-is-sent)

メッセージ拡張アクション コマンドを定義する方法については、次のビデオを参照してください。
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OANG]
<br>

## <a name="select-action-command-invoke-locations"></a>操作コマンドを呼び出す場所を選択する

まず、操作コマンドを呼び出す必要がある場所を決定する必要があります。 アプリ マニフェストで `context` を指定すると、コマンドで次の複数の場所からコマンドを呼び出すことができます。

* メッセージ作成領域: 作成メッセージ領域の下部にあるボタン。

    コマンド コンテキスト = 入力

* コマンド ボックス: コマンド ボックスにアプリを@メンションします。

    コマンド コンテキスト = commandBox

   > [!NOTE]
   > メッセージ拡張機能がコマンド ボックスから呼び出された場合、会話に直接挿入されたボット メッセージで応答することはできません。

* メッセージ: メッセージの `...` オーバーフロー メニュー経由で既存のメッセージから直接送信。

    コマンド コンテキスト = メッセージ

    > [!NOTE]
    > ボットへの最初の呼び出しには、その呼び出し元のメッセージを含む JSON オブジェクトが含まれます。 タスク モジュールを使用してメッセージを表示する前に、メッセージを処理できます。

次の画像は、操作コマンドが呼び出される場所を示しています。

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="操作コマンドを呼び出す場所":::

## <a name="select-how-to-create-your-task-module"></a>タスク モジュールの作成方法を選択する

コマンドの呼び出し元の選択に加えて、ユーザーのタスク モジュールでフォームを入力する方法も選択する必要があります。 タスク モジュール内でレンダリングされるフォームを作成するには、次の 3 つのオプションがあります。

* **静的なパラメーターの一覧**: これは最も簡単なメソッドです。 アプリ マニフェストで Teams クライアントがレンダリングするパラメーターの一覧を定義できますが、この場合は書式設定を制御できません。
* **アダプティブ カード**: UI をより細かく制御できるアダプティブ カードの使用を選択できますが、使用可能な制御および書式設定オプションは制限されます。
* **埋め込み Web ビュー**: カスタム Web ビューをタスク モジュールに埋め込んで、UI とコントロールを完全に制御することができます。

パラメーターの静的リストを使用してタスク モジュールを作成することを選択した場合、ユーザーがタスク モジュールを送信すると、メッセージ拡張機能が呼び出されます。 埋め込み Web ビューまたはアダプティブ カードを使用する場合、メッセージ拡張機能はユーザーからの初期呼び出しイベントを処理し、タスク モジュールを作成してクライアントに返す必要があります。

## <a name="select-how-the-final-message-is-sent"></a>最終メッセージの送信方法を選択する

ほとんどの場合、操作コマンドにより、メッセージの作成ボックスにカードが挿入されます。 ユーザーは、チャネルやチャットに送信できます。 この場合、メッセージはユーザーから送信され、ボットはカードをさらに編集または更新できません。

メッセージ拡張機能が作成ボックスまたはメッセージから直接呼び出された場合、Web サービスは最終的な応答をチャネルまたはチャットに直接挿入できます。 この場合、アダプティブ カードはボットから取得され、ボットはそれを更新し、必要に応じて会話スレッドに返信します。 同じ ID を使用し、適切な範囲を定義して、`bot` オブジェクトをアプリ マニフェストに追加する必要があります。

## <a name="add-the-action-command-to-your-app-manifest"></a>アプリ マニフェストに操作コマンドを追加する

操作コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON の最上位レベルに新しい `composeExtension` オブジェクトを追加する必要があります。これを行うには、次のいずれかの方法を使用します。

* [開発者ポータルを使用してアクション コマンドを作成する](#create-an-action-command-using-developer-portal)
* [操作コマンドを手動で作成する](#create-an-action-command-manually)

### <a name="create-an-action-command-using-developer-portal"></a>開発者ポータルを使用してアクション コマンドを作成する

**開発者ポータル** を使用してアクション コマンドを作成できます。

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> 操作コマンドを作成するための前提条件は、メッセージ拡張機能をすでに作成していることです。 メッセージ拡張機能を作成する方法については、「[メッセージ拡張機能の作成](~/messaging-extensions/how-to/create-messaging-extension.md)」を参照してください。

アクション コマンドを作成するには:

1. Microsoft Teams クライアントから **開発者ポータル** を開き、[ **アプリ** ] タブを選択します。 **開発者ポータル** でアプリ パッケージを既に作成している場合は、一覧から選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートしたら、[アプリ **の機能**] で **[メッセージ拡張機能**] を選択します。
1. メッセージ拡張機能を作成するには、Microsoft 登録ボットが必要です。 既存のボットを使用するか、新しいボットを作成できます。 [ **新しいボットの作成** ] オプションを選択し、新しいボットに名前を付けてから、[ **作成**] を選択します。

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="このスクリーンショットは、開発者ポータルでボットを作成する方法を示しています。":::

1. 既存のボットを使用するには、 **既存のボットを選択** し、ドロップダウン リストから既存のボットを選択するか、ボット ID が既に作成されている場合は **[ボット ID の入力** ] を選択します。

1. メッセージング拡張機能のスコープを選択し、[保存] を選択 **します**。

1. [**コマンド**] セクションで **[コマンドの追加]** を選択して、メッセージ拡張機能の動作を決定するコマンドを含めます。

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="スクリーンショットは、メッセージ拡張機能の動作を定義するコマンドを追加する方法を示しています。":::

1. **[アクション]** を選択し、パラメーターの種類を選択します。

1. **コマンド ID**、**コマンド タイトル**、および **コマンドの説明** を入力します。

1. すべてのパラメーターを入力し、ドロップダウン リストから入力の種類を選択します。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="スクリーンショットは、メッセージ拡張機能のコマンドを定義するパラメーターを追加する方法を示しています。":::

1. **[プレビュー リンク****] で [ドメインの追加]** を選択します。

1. 有効なドメインを入力し、[ **追加**] を選択します。

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="スクリーンショットは、リンク解除用の有効なドメインをメッセージング拡張機能に追加する方法を示しています。":::

1. **[保存]** を選択します。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="スクリーンショットは、メッセージ拡張機能のすべての設定とパラメーターを保存する方法を示しています。":::

**追加のパラメーターを追加するには**

1. コマンド セクションで省略記号を選択し、 **パラメーターの編集** を選択します。

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="スクリーンショットは、メッセージ拡張機能のパラメーターを追加する方法を示しています。":::

1. [ **パラメーターの追加]** を選択し、すべてのパラメーターを入力します。

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="スクリーンショットは、メッセージ拡張機能のパラメーターを追加する方法を示しています。"lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

### <a name="create-an-action-command-manually"></a>操作コマンドを手動で作成する

操作ベースのメッセージ拡張機能コマンドをアプリ マニフェストに手動で追加するには、オブジェクトの `composeExtension.commands` 配列に次のパラメーターを追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このプロパティは、このコマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれています。 | はい | 1.0 |
| `title` | このプロパティはコマンド名です。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | このプロパティは `action` である必要があります。 | いいえ | 1.4 |
| `fetchTask` | このプロパティは、タスク モジュールのアダプティブ カードまたは埋め込み Web ビューの `true` に設定し、パラメーターの静的な一覧、または `taskInfo` によって Web ビューを読み込む場合に `false` | いいえ | 1.4 |
| `context` | このプロパティは、メッセージ拡張機能の呼び出し元を定義する値の省略可能な配列です。 使用可能な値: `message`、`compose`、`commandBox`。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

パラメーターの静的リストを使用している場合は、次のパラメーターも追加する必要があります。

| プロパティ名 | 用途 | は必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | このプロパティでは、コマンドのパラメーターの静的な一覧について説明します。`fetchTask` が `false` である場合にのみ使用します。 | いいえ | 1.0 |
| `parameter.name` | このプロパティは、パラメーターの名前を説明します。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このプロパティは、指定する必要がある値のパラメーターの目的または例を説明します。この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | このプロパティは、ユーザー フレンドリな短いパラメーターのタイトルまたはラベルです。 | はい | 1.0 |
| `parameter.inputType` | このプロパティは、必要な入力の種類に設定されます。 指定できる値には`text`、`textarea`、`number`、`date`、`time`、`toggle` などがあります。 既定値は `text` に設定されていません。 | いいえ | 1.4 |

埋め込み Web ビューを使用している場合は、必要に応じて、ボットを `taskInfo` 直接呼び出さずに Web ビューをフェッチするオブジェクトを追加できます。 このオプションを選択した場合、動作はパラメーターの静的な一覧を使用する動作と類似します。 ボットとの最初の対話が [タスク モジュール送信アクションに応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)場合。 オブジェクトを使用している場合は、パラメーター`false`を `taskInfo` `fetchTask` .

| プロパティ名 | 用途 | は必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
|`taskInfo`|メッセージ拡張コマンドを使用するときにプリロードするタスク モジュールを指定します。 | いいえ | 1.4 |
|`taskInfo.title`|初期タスク モジュール タイトル。 |いいえ | 1.4 |
|`taskInfo.width`|タスク モジュールの幅 - ピクセル単位の数値、または `large`、`medium`、`small` などの既定のレイアウト。 |いいえ | 1.4 |
|`taskInfo.height`|タスク モジュールの高さ - ピクセル単位の数値、または `large`、`medium`、`small` などの既定のレイアウト。|いいえ | 1.4 |
|`taskInfo.url`|初期 Web ビュー URL。|いいえ | 1.4 |

#### <a name="app-manifest-example"></a>アプリ マニフェストの例

次のセクションは、2 つのアクション コマンドを定義する `composeExtensions` オブジェクトの例です。 完全なマニフェストの例ではありません。 完全なアプリ マニフェスト スキーマについては、「[アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md)」を参照してください。

```json
...
"composeExtensions": [
  {
    "botId": "c8fa3cf6-b1f0-4ba8-a5bf-a241bc29adf3",
    "scopes": [
      "personal",
      "groupchat"
    ],
    "commands": [
      {
        "id": "To do",
        "type": "action",
        "title": "Create To do",
        "description": "Create a To do",
        "initialRun": true,
        "fetchTask": false,
        "context": [
          "commandBox",
          "compose"
        ],
        "parameters": [
          {
            "name": "Name",
            "title": "Title",
            "description": "To do Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "title": "Description",
            "description": "Description of the task",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "title": "Date",
            "description": "Due date for the task",
            "inputType": "date"
          }
        ]
      }
    ],
    "canUpdateConfiguration": true,
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "yourapp.onmicrosoft.com"
          ]
        }
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

[ステップ バイ ステップ ガイド](../../../sbs-meetingextension-action.yml)に従って、アクション ベースのメッセージ拡張機能を構築します。

## <a name="next-step"></a>次の手順

アダプティブ カードまたは埋め込み Web ビューをオブジェクトなしで `taskInfo` 使用する場合は、次の手順に進みます。

> [!div class="nextstepaction"]
> [タスク モジュールを使用した作成と応答](~/messaging-extensions/how-to/action-commands/create-task-module.md)

パラメーターまたは埋め込み Web ビューをオブジェクトと共 `taskInfo` に使用する場合は、次の手順に進みます。

> [!div class="nextstepaction"]
> [タスク モジュールの送信アクションへの応答](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
