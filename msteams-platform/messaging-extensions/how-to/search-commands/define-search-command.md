---
title: メッセージング拡張機能の検索コマンドを定義する
author: clearab
description: Microsoft Teams アプリのメッセージング拡張機能検索コマンドを定義します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449270"
---
# <a name="define-messaging-extension-search-commands"></a>メッセージング拡張機能の検索コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

メッセージング拡張機能検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカード形式でメッセージに挿入できます。

> [!NOTE]
> 結果のカード サイズの制限は 28 KB です。 カードのサイズが 28 KB を超える場合、カードは送信されません。 

## <a name="choose-messaging-extension-invoke-locations"></a>メッセージング拡張機能の呼び出し場所の選択

最初に決定する必要があるのは、検索コマンドをトリガーできる場所 (具体的には呼び *出し先*) です。 検索コマンドは、次のいずれかの場所または両方から呼び出すことができます。

* 作成メッセージ領域の下部にあるボタン
* コマンド @mentioningを使用して

作成メッセージ領域から呼び出されると、ユーザーは結果を会話に送信できます。 コマンド ボックスから呼び出されると、ユーザーは結果のカードを操作したり、別の場所で使用するためにコピーすることができます。

## <a name="add-the-command-to-your-app-manifest"></a>アプリ マニフェストにコマンドを追加する

ユーザーが検索コマンドを操作する方法を決めたので、それをアプリ マニフェストに追加します。 これを行うには、アプリ マニフェスト JSON のトップ レベルに新 `composeExtension` しいオブジェクトを追加します。 これを行うには、App Studio のヘルプを使用するか、手動で実行します。

### <a name="create-a-command-using-app-studio"></a>App Studio を使用してコマンドを作成する

検索コマンドを作成するには、メッセージング拡張機能を既に作成する必要があります。 メッセージング拡張機能を作成する方法の詳細については、「Create [a messaging extension 」を参照してください](~/messaging-extensions/how-to/create-messaging-extension.md)。

**検索コマンドを作成するには**

1. Microsoft Teams クライアントで App Studio を **開** き、[マニフェスト エディター] **タブを選択** します。
1. App Studio でアプリ パッケージを既に作成している **場合** は、一覧からアプリ パッケージを選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートした後、[機能] で [ **メッセージング拡張機能]** **を選択します**。
1. [ **メッセージング拡張機能** ] **ページの [コマンド** ] セクションで [追加] を選択します。
1. [ **ユーザーにサービスの情報のクエリを許可する] を選択し、メッセージに挿入します**。
1. コマンド ID **と Title** を **追加します**。
1. 検索コマンドをトリガーする必要がある場所を選択します。 メッセージを **選択しても** 、現在、検索コマンドの動作は変更されません。
1. 検索パラメーターを追加し、[保存] を **選択します**。
 
### <a name="manually-create-a-command"></a>コマンドを手動で作成する

メッセージング拡張機能の検索コマンドをアプリ マニフェストに手動で追加するには、次のパラメーターをオブジェクトの配列 `composeExtension.commands` に追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このコマンドに割り当てる一意の ID。 ユーザー要求には、この ID が含まれます。 | はい | 1.0 |
| `title` | コマンド名。 この値は UI に表示されます。 | はい | 1.0 |
| `description` | このコマンドの動作を示すヘルプ テキスト。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | にする必要があります。 | いいえ | 1.4 |
|`initialRun` | true に **設定されている場合** は、ユーザーが UI でこのコマンドを選択するとすぐにこのコマンドを実行する必要があります。 | いいえ | 1.0 |
| `context` | 検索アクションが使用できるコンテキストを定義する値の任意の配列。 指定できる値 `message` は `compose` 、、、または `commandBox` です。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

また、Teams クライアントでユーザーに表示されるテキストを定義する検索パラメーターの詳細を追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | コマンドのパラメーターの静的リスト。 | いいえ | 1.0 |
| `parameter.name` | パラメーターの名前です。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | 指定する必要がある値のこのパラメーターの目的または例について説明します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | 短いユーザーフレンドリーなパラメーターのタイトルまたはラベル。 | はい | 1.0 |
| `parameter.inputType` | 必要な入力の種類に設定します。 可能な値 `text` には `textarea` 、、 `number` 、 、 、 、 `date` `time` が含まれます `toggle` 。 既定値はに設定されています `text` | いいえ | 1.4 |

#### <a name="app-manifest-example"></a>アプリ マニフェストの例

検索コマンドを定義する `composeExtensions` オブジェクトの例を次に示します。 完全なマニフェストの例ではありません。完全なアプリ マニフェスト スキーマについては、「アプリ マニフェスト [スキーマ」を参照してください](~/resources/schema/manifest-schema.md)。

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```

## <a name="next-steps"></a>次の手順

検索コマンドが追加されたので、検索要求を [処理する必要があります](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
