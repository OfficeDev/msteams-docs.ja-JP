---
title: メッセージング拡張機能の検索コマンドを定義する
author: surbhigupta
description: アプリのメッセージング拡張機能検索コマンドをMicrosoft Teamsします。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 6333840e6817761911b2b5acd4b53849448b5b68
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068911"
---
# <a name="define-messaging-extension-search-commands"></a>メッセージング拡張機能の検索コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

メッセージング拡張機能の検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカード形式のメッセージに挿入できます。 このドキュメントでは、検索コマンドの呼び出し場所を選択し、検索コマンドをアプリ マニフェストに追加する方法について説明します。

> [!NOTE]
> 結果のカード サイズの制限は 28 KB です。 カードのサイズが 28 KB を超える場合、カードは送信されません。

## <a name="select-search-command-invoke-locations"></a>検索コマンドの呼び出し場所を選択する

検索コマンドは、次のいずれかの場所または両方から呼び出されます。

* メッセージの作成領域: 作成メッセージ領域の下部にあるボタン。
* コマンド ボックス: コマンド @mentioningを使用します。

メッセージの作成領域から検索コマンドが呼び出されると、ユーザーは結果を会話に送信します。 コマンド ボックスから呼び出されると、ユーザーは結果のカードを操作するか、別の場所で使用するためにコピーします。

次の図は、検索コマンドの呼び出し場所を表示します。

![search コマンドの呼び出し場所](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a>アプリ マニフェストに検索コマンドを追加する

検索コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON のトップ レベルに新しいオブジェクト `composeExtension` を追加する必要があります。 検索コマンドは、App Studio の助けを借りて追加するか、手動で追加できます。

### <a name="create-a-search-command-using-app-studio"></a>App Studio を使用して検索コマンドを作成する

検索コマンドを作成する前提条件は、メッセージング拡張機能を既に作成している必要があります。 メッセージング拡張機能を作成する方法の詳細については、「Create [a messaging extension 」を参照してください](~/messaging-extensions/how-to/create-messaging-extension.md)。

**検索コマンドを作成するには**

1. クライアント **から App Studio** をMicrosoft Teamsし、[マニフェスト エディター]**タブを選択** します。
1.  App Studio でアプリ パッケージを既に作成している **場合** は、一覧から選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートした後、[機能] **で [メッセージング拡張機能]** **を選択します**。 メッセージング拡張機能を設定するポップアップ ウィンドウが表示されます。
1. ウィンドウ **で [セットアップ** ] を選択して、メッセージング拡張機能をアプリ エクスペリエンスに含めます。 次の図は、メッセージング拡張機能のセットアップ ページを表示します。 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. メッセージング拡張機能を作成するには、Microsoft 登録済みのボットが必要です。 既存のボットを使用するか、新しいボットを作成できます。 [ **新しいボットの作成]** オプションを選択し、新しいボットの名前を付け、[作成] を **選択します**。 次の図は、メッセージング拡張機能のボットの作成を表示します。

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. [ **メッセージング拡張機能** ] **ページの [コマンド** ] セクションで [追加] を選択して、メッセージング拡張機能の動作を決定するコマンドを含めます。   
次の図は、メッセージング拡張機能のコマンド追加を表示します。

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. [ **ユーザーがサービスに情報を照会し、メッセージに挿入する] を選択します**。 次の図は、検索コマンド パラメーターの選択を表示します。

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. コマンド ID **と Title** を **追加します**。
1. 検索コマンドを呼び出す必要がある場所を選択します。 メッセージを **選択しても** 、現在、検索コマンドの動作は変更されません。 次の図は、検索コマンドの呼び出し場所を表示します。

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. 検索パラメーターを追加し、[保存] を **選択します**。

### <a name="create-a-search-command-manually"></a>手動で検索コマンドを作成する 

メッセージング拡張機能検索コマンドをアプリ マニフェストに手動で追加するには、次のパラメーターをオブジェクトの配列 `composeExtension.commands` に追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このプロパティは、検索コマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれます。 | はい | 1.0 |
| `title` | このプロパティはコマンド名です。 この値は、ユーザー インターフェイス (UI) に表示されます。 | はい | 1.0 |
| `description` | このプロパティは、このコマンドの動作を示すヘルプ テキストです。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | このプロパティは、 である必要があります `query` 。 | いいえ | 1.4 |
|`initialRun` | このプロパティを true に **設定すると**、ユーザーが UI でこのコマンドを選択するとすぐにこのコマンドを実行する必要があります。 | いいえ | 1.0 |
| `context` | このプロパティは、検索アクションが使用できるコンテキストを定義する値のオプションの配列です。 使用可能な値: `message`、`compose`、`commandBox`。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

検索クライアントでユーザーに表示されるテキストを定義する検索パラメーターの詳細を追加Teamsがあります。

| プロパティ名 | 用途 | 必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | このプロパティは、コマンドのパラメーターの静的リストを定義します。 | いいえ | 1.0 |
| `parameter.name` | このプロパティは、パラメーターの名前を表します。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このプロパティは、パラメーターの目的または指定する必要がある値の例を示します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | このプロパティは、短いユーザーフレンドリーなパラメーターのタイトルまたはラベルです。 | はい | 1.0 |
| `parameter.inputType` | このプロパティは、必要な入力の種類に設定されます。 可能な値 `text` には `textarea` 、、 `number` 、 、 、 、 `date` `time` が含まれます `toggle` 。 既定値は に設定されています `text` 。 | いいえ | 1.4 |

#### <a name="example"></a>例

次のセクションでは、検索コマンドを定義するオブジェクトの単純 `composeExtensions` なアプリ マニフェストの例を示します。 

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
完全なアプリ マニフェストについては、「アプリ マニフェスト [スキーマ」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams拡張アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams拡張機能の検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [検索コマンドに応答します](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。

