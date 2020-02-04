---
title: メッセージング拡張機能の操作コマンドを定義する
author: clearab
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7eb734258aa34c69fa34d1413b2d3dab88e0113a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674684"
---
# <a name="define-messaging-extension-action-commands"></a>メッセージング拡張機能の操作コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

アクションコマンドを使用すると、ユーザーにモーダルポップアップ (Teams でタスクモジュールと呼ばれる) を提示して、情報を収集または表示した後、その操作を処理して、情報を Teams に送信することができます。 コマンドを作成する前に、次のことを決定する必要があります。

1. アクションコマンドはどこからトリガーされますか?
1. タスクモジュールはどのように作成されますか?
1. 最終的なメッセージやカードは bot からチャネルに送信されるか、またはメッセージまたはカードが [メッセージの作成] 領域に挿入されて、ユーザーが送信できるようになりますか。

## <a name="choose-action-command-invoke-locations"></a>アクションコマンドの呼び出し場所を選択する

最初に決定する必要があるのは、アクションコマンドをトリガーする (または、より具体的に*呼び出す*) 方法です。 アプリマニフェスト`context`でを指定することで、コマンドを次の1つ以上の場所から呼び出すことができます。

* [メッセージの作成] 領域の下部にあるボタン。
* [コマンド] ボックスでアプリを @mentioning します。 注: メッセージング拡張機能が [コマンド] ボックスから呼び出された場合、直接会話に挿入された bot メッセージで応答することはできません。
* 既存のメッセージから直接使用する...メッセージのオーバーフローメニュー。 注: bot への最初の呼び出しには、呼び出し元のメッセージが含まれる JSON オブジェクトが含まれています。これは、タスクモジュールで提供する前に処理できます。

## <a name="choose-how-to-build-your-task-module"></a>タスクモジュールの作成方法を選択する

でコマンドを起動する場所を選択することに加えて、ユーザーのタスクモジュールでフォームにデータを入力する方法も選択する必要があります。 タスクモジュール内にレンダリングされるフォームを作成するには、次の3つのオプションがあります。

* **パラメーターの静的リスト**-これは最も簡単なオプションです。 Teams クライアントが表示するアプリマニフェストにパラメータ (入力フィールド) のリストを定義することができます。 このオプションを使用して書式設定を制御することはできません。
* **アダプティブカード**-アダプティブカードを使用することもできますが、UI をより詳細に制御することができますが、使用可能なコントロールと書式設定のオプションには制限があります。
* **埋め込み web ビュー** -UI とコントロールを完全に制御する必要がある場合は、タスクモジュールにカスタム web ビューを埋め込むことを選択できます。

パラメーターの静的リストを使用してタスクモジュールを作成する場合は、ユーザーがタスクモジュールを送信するときに、メッセージング拡張機能の最初の呼び出しが行われます。 埋め込まれた web ビューまたはアダプティブカードを使用する場合、メッセージング拡張機能では、ユーザーからの初期 invoke イベントを処理し、タスクモジュールを作成して、クライアントに戻す必要があります。

## <a name="choose-how-the-final-message-will-be-sent"></a>最終メッセージが送信される方法を選択する

ほとんどの場合、アクションコマンドによって、作成メッセージボックスにカードが挿入されます。 その後、ユーザーはチャネルまたはチャットに送信するかどうかを決定できます。 この例のメッセージはユーザーからのものであり、bot はカードをさらに編集または更新することはできません。

メッセージング拡張機能が [新規作成] ボックスから、または直接メッセージからトリガーされる場合、web サービスは直接チャネルまたはチャットに最終的な応答を挿入できます。 この場合、adaptive card は bot からのものであり、bot が更新できるようになります。また、必要に応じて、ボットが会話スレッドに応答することもできます。 同じ Id を使用して`bot`アプリケーションマニフェストにオブジェクトを追加し、適切なスコープを定義する必要があります。

## <a name="add-the-command-to-your-app-manifest"></a>アプリケーションマニフェストにコマンドを追加する

ユーザーがアクションコマンドを操作する方法を決定したので、それをアプリのマニフェストに追加します。 これを行うには、アプリマニフェスト`composeExtension` JSON の最上位レベルに新しいオブジェクトを追加します。 そのためには、アプリ Studio のヘルプを使用するか、手動で行うことができます。

### <a name="create-a-command-using-app-studio"></a>アプリ Studio を使用してコマンドを作成する

次の手順では、[メッセージング拡張機能が](~/messaging-extensions/how-to/create-messaging-extension.md)既に作成済みであることを前提としています。

1. Microsoft Teams クライアントから、 **App Studio**を開き、[**マニフェストエディター** ] タブを選択します。
2. アプリパッケージが既にアプリ Studio で作成されている場合は、一覧から選択します。 それ以外の場合は、既存のアプリパッケージをインポートできます。
3. [コマンド] セクションの [**追加**] ボタンをクリックします。
4. [**ユーザーが Teams 内で外部サービスのアクションを開始できるようにする**] を選択します。
5. 静的パラメーターセットを使用してタスクモジュールを作成する場合は、そのオプションを選択します。 それ以外の場合は、 **bot からパラメーターの動的セットを取得**することを選択します。
6. **コマンド Id**と**タイトル**を追加します。
7. アクションコマンドを起動する場所を選択します。
8. タスクモジュールのパラメーターを使用している場合は、最初のパラメーターを追加します。
9. Click Save
10. さらにパラメーターを追加する必要がある場合は、[ **parameters** ] セクションの [**追加**] ボタンをクリックして追加します。

### <a name="manually-create-a-command"></a>コマンドを手動で作成する

アクションベースのメッセージング拡張コマンドをアプリのマニフェストに手動で追加するには、オブジェクトの`composeExtension.commands`配列に follow パラメーターを追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このコマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれます。 | はい | 1.0 |
| `title` | コマンド名を指定します。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | にする必要があります。 | いいえ | 1.4 |
| `fetchTask` | `true`作業モジュールのアダプティブカードまたは埋め込み web ビューの場合`false` 、パラメーターの静的なリスト、または web ビューを読み込むときに`taskInfo` | いいえ | 1.4 |
| `context` | メッセージング拡張機能を呼び出すことができる場所を定義する値のオプションの配列です。 可能な値`message`は`compose`、、 `commandBox`、です。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

パラメーターの静的な一覧を使用している場合は、それらも追加します。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | コマンドのパラメーターの静的リスト。 がである`fetchTask`場合にのみ使用`false` | いいえ | 1.0 |
| `parameter.name` | パラメーターの名前です。 これは、ユーザーの要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このパラメーターの目的または提供する必要がある値の例について説明します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | 簡単なユーザーフレンドリパラメーターのタイトルまたはラベル。 | はい | 1.0 |
| `parameter.inputType` | 必要な入力の種類を設定します。 可能な値`text`は`textarea`、 `number` `date` `time`、、、 `toggle`、です。 既定値はに設定されています`text` | いいえ | 1.4 |

埋め込みの web ビューを使用している場合は、必要`taskInfo`に応じて、bot を直接呼び出すことなく web ビューを取得するために、オブジェクトを追加することができます。 このオプションを使用する場合の動作は、ボットとの最初の操作が[タスクモジュール送信アクションに応答](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)するという点で、パラメータの静的なリストを使用するのと似ています。 `taskInfo`オブジェクトを使用している場合は、 `fetchTask`パラメーターもに`false`設定してください。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
|`taskInfo`|メッセージ拡張コマンドの使用時にプリロードするタスクモジュールを指定する| いいえ | 1.4 |
|`taskInfo.title`|最初のタスクモジュールタイトル|いいえ | 1.4 |
|`taskInfo.width`|タスクモジュールの幅-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。|いいえ | 1.4 |
|`taskInfo.height`|タスクモジュールの高さ-数値をピクセル単位で指定するか、' large '、' medium '、または ' small ' などの既定のレイアウトにします。|いいえ | 1.4 |
|`taskInfo.url`|最初の web ビューの URL|いいえ | 1.4 |

#### <a name="app-manifest-example"></a>アプリマニフェストの例

2つのアクションコマンドを定義`composeExtensions`するオブジェクトの例を次に示します。 完全なマニフェストの例として、完全なアプリマニフェストスキーマについては、「 [app manifest スキーマ](~/resources/schema/manifest-schema.md)」を参照してください。

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
        "fetchTask": false,
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

## <a name="next-steps"></a>次のステップ

アダプティブカードを使用している場合、またはオブジェクトを`taskInfo`持たない埋め込み web ビューを使用している場合は、次の操作を実行します。

* [タスクモジュールを作成して応答する](~/messaging-extensions/how-to/action-commands/create-task-module.md)

パラメーターを使用している場合、または`taskInfo`オブジェクトに埋め込まれた web ビューを使用している場合は、次の手順を実行します。

* [タスクモジュール送信に応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
