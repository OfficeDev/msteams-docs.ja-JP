---
title: メッセージング拡張機能のアクション コマンドを定義する
author: clearab
description: メッセージング拡張機能アクション コマンドの概要
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: be2135477c4234187f374aef215f90e8329fb74e
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778402"
---
# <a name="define-messaging-extension-action-commands"></a>メッセージング拡張機能のアクション コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

操作コマンドを使用すると、情報を収集または表示するためのモーダル ポップアップ (Teams ではタスク モジュールと呼びます) をユーザーに表示し、対話を処理した後 Teams に情報を送り返すことができます。 コマンドを作成する前に、以下を決定する必要があります。

1. アクション コマンドはどこから実行できますか?
1. タスク モジュールの作成方法
1. 最後のメッセージまたはカードがボットからチャネルに送信されるのか、それともユーザーが送信するメッセージ作成領域にメッセージまたはカードが挿入されるのか。

## <a name="choose-action-command-invoke-locations"></a>操作コマンドの呼び出し場所を選択する

最初に決定する必要があるのは、アクション コマンドをトリガーできる場所 (具体的には呼び出し) *です*。 アプリ マニフェストでコマンドを指定すると、次の 1 つ以上の場所 `context` からコマンドを呼び出すことができます。

* メッセージ作成領域の下部にあるボタン。
* コマンド @mentioningでアプリを開きます。 注: メッセージング拡張機能がコマンド ボックスから呼び出された場合、会話にボット メッセージを直接挿入して応答することはできません。
* ... を介して既存のメッセージから直接メッセージのオーバーフロー メニュー。 注: ボットに対する最初の呼び出しには、呼び出されたメッセージを含む JSON オブジェクトが含まれます。このオブジェクトは、タスク モジュールを表示する前に処理できます。

## <a name="choose-how-to-build-your-task-module"></a>タスク モジュールの作成方法を選択する

コマンドを呼び出すことができる場所を選択する以外に、ユーザーのタスク モジュールでフォームにデータを入力する方法も選択する必要があります。 タスク モジュール内でレンダリングされるフォームを作成するには、次の 3 つのオプションがあります。

* **パラメーターの静的リスト** - これは最も簡単なオプションです。 アプリ マニフェストで、Teams クライアントがレンダリングするパラメーター (入力フィールド) の一覧を定義できます。 このオプションでは書式設定を制御できません。
* **アダプティブ カード** - アダプティブ カードの使用を選択できます。アダプティブ カードを使って UI を詳細に制御できますが、使用可能なコントロールと書式設定オプションは制限されます。
* **埋め込み Web ビュー** - UI とコントロールを完全に制御する必要がある場合は、タスク モジュールにカスタム Web ビューを埋め込む方法を選択できます。

パラメーターの静的リストを使用してタスク モジュールを作成する場合、メッセージング拡張機能への最初の呼び出しは、ユーザーがタスク モジュールを送信するときに行います。 埋め込み Web ビューまたはアダプティブ カードを使用する場合、メッセージング拡張機能は、ユーザーからの最初の呼び出しイベントを処理し、タスク モジュールを作成して、それをクライアントに返す必要があります。

## <a name="choose-how-the-final-message-will-be-sent"></a>最後のメッセージの送信方法を選択する

ほとんどの場合、アクション コマンドを実行すると、メッセージの作成ボックスにカードが挿入されます。 その後、ユーザーはチャネルまたはチャットに送信できます。 この場合のメッセージはユーザーから送信され、ボットはそれ以上カードの編集や更新を行えなされません。

メッセージング拡張機能が作成ボックスまたはメッセージから直接トリガーされた場合、Web サービスは最後の応答をチャネルまたはチャットに直接挿入できます。 この場合、アダプティブ カードはボットから提供され、ボットはボットを更新し、必要に応じてボットも会話スレッドに返信できます。 同じ ID を使用してアプリ マニフェストにオブジェクトを追加し、適切なスコープ `bot` を定義する必要があります。

## <a name="add-the-command-to-your-app-manifest"></a>アプリ マニフェストにコマンドを追加する

これで、ユーザーがアクション コマンドを操作する方法が決まったので、次にアプリ マニフェストに追加します。 これを行うには、アプリ マニフェスト JSON のトップ レベルに新 `composeExtension` しいオブジェクトを追加します。 これを行うには、App Studio の支援を受けるか、手動で行います。

### <a name="create-a-command-using-app-studio"></a>App Studio を使用してコマンドを作成する

次の手順では、メッセージング拡張機能が [既に作成済みである必要があります](~/messaging-extensions/how-to/create-messaging-extension.md)。

1. Microsoft Teams クライアントから App **Studio** を開き、[マニフェスト エディター] **タブを選択** します。
2. App Studio で既にアプリ パッケージを作成している場合は、一覧からアプリ パッケージを選択します。 インポートされていない場合は、既存のアプリ パッケージをインポートできます。
3. [コマンド] **セクション** の [追加] ボタンをクリックします。
4. **Choose Allow users to trigger actions in external services while inside of Teams**.
5. 静的なパラメーター セットを使用してタスク モジュールを作成する場合は、そのオプションを選択します。 それ以外の場合は、 **ボットからパラメーターの動的セットをフェッチします**。
6. コマンド ID **とタイトル** を追加 **します**。
7. アクション コマンドをトリガーする場所を選択します。
8. タスク モジュールのパラメーターを使用している場合は、最初のパラメーターを追加します。
9. Click Save
10. パラメーターを追加する必要がある場合は、[パラメーター  ] セクションの [追加]**ボタンをクリック** して追加します。

### <a name="manually-create-a-command"></a>コマンドを手動で作成する

アクション ベースのメッセージング拡張機能コマンドをアプリ マニフェストに手動で追加するには、オブジェクトの配列に次のパラメーター `composeExtension.commands` を追加する必要があります。

| プロパティ名 | 用途 | 必須 | 最小マニフェスト バージョン |
|---|---|---|---|
| `id` | このコマンドに割り当てる一意の ID。 ユーザー要求には、この ID が含まれます。 | はい | 1.0 |
| `title` | コマンド名。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | にする必要があります。 | いいえ | 1.4 |
| `fetchTask` | `true`タスク モジュール用のアダプティブ カードビューまたは埋め込み Web ビュー用、パラメーターの静的リスト用、または `false``taskInfo` | いいえ | 1.4 |
| `context` | メッセージング拡張機能を呼び出すことができる場所を定義する値のオプションの配列。 指定できる値 `message` は `compose` 、,, または `commandBox` です。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

静的なパラメーターの一覧を使用している場合は、パラメーターも追加します。

| プロパティ名 | 用途 | 必須 | 最小マニフェスト バージョン |
|---|---|---|---|
| `parameters` | コマンドのパラメーターの静的リスト。 次の場合にのみ使用 `fetchTask` します。 `false` | いいえ | 1.0 |
| `parameter.name` | パラメーターの名前です。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このパラメーターの目的、または指定する値の例について説明します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | 短いユーザー フレンドリーなパラメータータイトルまたはラベル。 | はい | 1.0 |
| `parameter.inputType` | 必要な入力の種類に設定します。 使用できる値 `text` は `textarea` 、 , , , , `number` , `date` , `time` `toggle` . 既定値は次の値に設定されます。 `text` | いいえ | 1.4 |

埋め込み Web ビューを使用している場合は、必要に応じて、ボットを直接呼び出さずに Web ビューをフェッチするオブジェクト `taskInfo` を追加できます。 このオプションを使用する場合の動作は、ボットとの最初の対話がタスク モジュールの送信アクションに応答するという点で、静的なパラメーターの一覧を使用するのと [似ています](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。 オブジェクトを使用している場合 `taskInfo` は、パラメーターも必ず次の値に `fetchTask` 設定してください `false` 。

| プロパティ名 | 用途 | 必須 | 最小マニフェスト バージョン |
|---|---|---|---|
|`taskInfo`|メッセージング拡張機能コマンドを使用するときにプリロードするタスク モジュールを指定する| いいえ | 1.4 |
|`taskInfo.title`|初期タスク モジュールのタイトル|いいえ | 1.4 |
|`taskInfo.width`|タスク モジュールの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、'small' など)|いいえ | 1.4 |
|`taskInfo.height`|タスク モジュールの高さ - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、'small' など)|いいえ | 1.4 |
|`taskInfo.url`|初期 Web ビューの URL|いいえ | 1.4 |

#### <a name="app-manifest-example"></a>アプリ マニフェストの例

2 つのアクション コマンドを定義 `composeExtensions` するオブジェクトの例を次に示します。 完全なマニフェストの例ではありません。完全なアプリ マニフェスト スキーマについては、「アプリ マニフェスト スキーマ」 [を参照してください](~/resources/schema/manifest-schema.md)。

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

## <a name="next-steps"></a>次の手順

オブジェクトを使わずにアダプティブ カードまたは埋め込み Web ビューを使う場合は、次の `taskInfo` 方法があります。

* [タスク モジュールを作成して応答する](~/messaging-extensions/how-to/action-commands/create-task-module.md)

パラメーターまたは埋め込み Web ビューをオブジェクトと一緒に使用している場合は、次の `taskInfo` 手順で次の手順を実行します。

* [タスク モジュールの送信に応答する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
