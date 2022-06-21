---
title: メッセージ拡張機能検索コマンドを定義する
author: surbhigupta
description: このモジュールでは、Teams アプリのメッセージ拡張機能検索コマンドについて説明し、アプリ マニフェストを使用して手動で検索コマンドを作成します。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 10bb71580ac67db155bd14b74325635ae22e6840
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189616"
---
# <a name="define-message-extension-search-commands"></a>メッセージ拡張機能検索コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

メッセージ拡張機能の検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカードの形式でメッセージに挿入できます。 このドキュメントでは、検索コマンドの呼び出し場所を選択し、検索コマンドをアプリ マニフェストに追加する方法について説明します。

> [!NOTE]
> 結果カードのサイズ制限は 28 KB です。 カードのサイズが 28 KB を超えると、カードは送信されません。

メッセージ拡張機能検索コマンドを定義する方法については、次のビデオを参照してください。
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIvK]
<br>

## <a name="select-search-command-invoke-locations"></a>検索コマンドの呼び出し場所を選択する

検索コマンドは、次のいずれかの場所または両方の場所から呼び出されます。

* メッセージ作成領域: 作成メッセージ領域の下部にあるボタン。
* コマンド ボックス: コマンド ボックスで@mentioningします。

  メッセージ作成領域から検索コマンドが呼び出されると、ユーザーは結果を会話に送信します。 コマンド ボックスから呼び出されると、ユーザーは結果のカードを操作するか、他の場所で使用するためにコピーします。

次の図は、検索コマンドの呼び出し場所を示しています。

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="検索コマンドの呼び出し場所":::

## <a name="add-the-search-command-to-your-app-manifest"></a>検索コマンドをアプリ マニフェストに追加する

検索コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON の最上位レベルに新しい `composeExtension` オブジェクトを追加する必要があります。 検索コマンドは、App Studio の助けを借りて追加することも、手動で追加することもできます。

### <a name="create-a-search-command-using-app-studio"></a>App Studio を使用して検索コマンドを作成する

検索コマンドを作成するための前提条件は、メッセージ拡張機能を既に作成している必要があるということです。 メッセージ拡張機能を作成する方法については、「[メッセージ拡張機能の作成](~/messaging-extensions/how-to/create-messaging-extension.md)」を参照してください。

検索コマンドを作成するには:

1. Microsoft Teams クライアントから **App Studio** を開き、**[マニフェスト エディター]** タブを選択します。
1. **App Studio** でアプリ パッケージを既に作成している場合は、一覧から選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートしたら、[機能] で **[メッセージ拡張機能** ] を選択 **します**。 メッセージ拡張機能を設定するためのポップアップ ウィンドウが表示されます。
1. ウィンドウで **[セットアップ]** を選択して、アプリ エクスペリエンスにメッセージ拡張機能を含めます。 次の図は、メッセージ拡張機能の設定ページを示しています。

    :::image type="content" source="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt-text="メッセージング拡張機能設定":::

1. メッセージ拡張機能を作成するには、Microsoft 登録ボットが必要です。 既存のボットを使用するか、新しいボットを作成できます。 **[新しいボットの作成]** オプションを選択し、新しいボットの名前を付けて、**[作成]** を選択します。 次の図は、メッセージ拡張機能のボット作成を示しています。

    :::image type="content" source="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt-text="メッセージング拡張機能用のボットを作成する":::

1. 既存のボットを使用するには、**[既存のボットを使用する]** を選択し、**[既存のボットのいずれかを選択する]** を選択してドロップダウンから既存のボットを選択し、**[ボット名]** を指定し、ボット ID がすでに作成されている場合は **[保存]** を選択するか、**[別のボット ID に接続する]** を選択し、**[ボット名]** を指定して **[保存]** を選択します。

    :::image type="content" source="~/assets/images/messaging-extension/use-existing-bot.png" alt-text="メッセージング拡張機能に既存のボットを使用する":::

1. メッセージ拡張機能の動作を決定するコマンドを含めるには、メッセージ拡張機能ページの [**コマンド] セクション** で [**追加]** を選択します。
次の画像は、メッセージ拡張機能のコマンドの追加を表示します。

    :::image type="content" source="~/assets/images/messaging-extension/include-command.png" alt-text="コマンドを含める":::

1. [ **ユーザーがサービスに対して情報のクエリを実行できるようにする] を選択し、メッセージに挿入します**。 次の図は、検索コマンド パラメーターの選択を示しています。

    :::image type="content" source="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt-text="検索コマンド パラメーターの選択":::

1. **[コマンド ID]** と **[タイトル]** を追加します。
1. 検索コマンドを呼び出す必要がある場所を選択します。 次の図は、検索コマンドの呼び出し場所を示しています。

    :::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt-text="検索コマンド呼び出し場所の選択":::

1. 検索パラメーターを追加し、[ **保存**] を選択します。

### <a name="create-a-search-command-manually"></a>検索コマンドを手動で作成する

メッセージ拡張機能検索コマンドをアプリ マニフェストに手動で追加するには、オブジェクトの配列に次のパラメーターを `composeExtension.commands` 追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このプロパティは、検索コマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれています。 | はい | 1.0 |
| `title` | このプロパティはコマンド名です。 この値は、ユーザー インターフェイス (UI) に表示されます。 | はい | 1.0 |
| `description` | このプロパティは、このコマンドの動作を示すヘルプ テキストです。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | このプロパティは 、 `query`. | いいえ | 1.4 |
|`initialRun` | このプロパティが **true** に設定されている場合は、ユーザーが UI でこのコマンドを選択するとすぐに、このコマンドを実行する必要があることを示します。 | いいえ | 1.0 |
| `context` | このプロパティは、検索アクションを使用できるコンテキストを定義する値の省略可能な配列です。 使用可能な値: `message`、`compose`、`commandBox`。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

Teams クライアントでユーザーに表示されるテキストを定義する検索パラメーターの詳細を追加する必要があります。

| プロパティ名 | 用途 | は必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | このプロパティは、コマンドのパラメーターの静的な一覧を定義します。 | いいえ | 1.0 |
| `parameter.name` | このプロパティは、パラメーターの名前を説明します。 これは、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このプロパティは、パラメーターの目的または指定する必要がある値の例を記述します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | このプロパティは、ユーザー フレンドリな短いパラメーターのタイトルまたはラベルです。 | はい | 1.0 |
| `parameter.inputType` | このプロパティは、必要な入力の種類に設定されます。 使用可能な値には`text`、, , `textarea`, `number`, `date`, `time``toggle`. 既定値は .`text` | いいえ | 1.4 |

#### <a name="example"></a>例

次のセクションは、検索コマンドを定義するオブジェクトの `composeExtensions` 単純なアプリ マニフェストの例です。

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

完全なアプリ マニフェストについては、「 [アプリ マニフェスト スキーマ」](~/resources/schema/manifest-schema.md)を参照してください。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams メッセージ拡張機能検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ステップ [バイ ステップ ガイド](../../../sbs-messagingextension-searchcommand.yml) に従って、検索ベースのメッセージ拡張機能を構築します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [検索コマンドに応答します](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。
