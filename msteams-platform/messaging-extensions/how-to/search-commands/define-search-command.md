---
title: メッセージ拡張機能検索コマンドを定義する
author: surbhigupta
description: このモジュールでは、Teams アプリのメッセージ拡張機能検索コマンドについて説明し、アプリ マニフェストを使用して手動で検索コマンドを作成します。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 5cddfcc5f4fd3088e72538c6243b5f4fbf19767c
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363474"
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

検索コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON の最上位レベルに新しい `composeExtension` オブジェクトを追加する必要があります。 検索コマンドは、開発者ポータルの助けを借りて追加することも、手動で追加することもできます。

### <a name="create-a-search-command-using-developer-portal"></a>開発者ポータルを使用して検索コマンドを作成する

検索コマンドを作成するための前提条件は、メッセージ拡張機能を既に作成している必要があるということです。 メッセージ拡張機能を作成する方法については、「[メッセージ拡張機能の作成](~/messaging-extensions/how-to/create-messaging-extension.md)」を参照してください。

**操作コマンドを作成するには**

1. Microsoft Teams クライアントから **開発者ポータル** を開き、[ **アプリ** ] タブを選択します。 **開発者ポータル** でアプリ パッケージを既に作成している場合は、一覧から選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートしたら、[アプリ **の機能**] で **[メッセージ拡張機能**] を選択します。
1. メッセージ拡張機能を作成するには、Microsoft 登録ボットが必要です。 既存のボットを使用するか、新しいボットを作成できます。 [ **新しいボットの作成** ] オプションを選択し、新しいボットに名前を付けてから、[ **作成**] を選択します。

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="このスクリーンショットは、開発者ポータルでボットを作成する方法を示しています。":::

1. 既存のボットを使用するには、 **既存のボットを選択** し、ドロップダウン リストから既存のボットを選択するか、ボット ID が既に作成されている場合は **[ボット ID の入力** ] を選択します。

1. メッセージング拡張機能のスコープを選択し、[保存] を選択 **します**。

1. [**コマンド**] セクションで **[コマンドの追加]** を選択して、メッセージ拡張機能の動作を決定するコマンドを含めます。
次の画像は、メッセージ拡張機能のコマンドの追加を表示します。

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="スクリーンショットは、メッセージ拡張機能の動作を定義するコマンドを追加する方法を示しています。":::

1. [ **検索** ] を選択し、 **コマンド ID**、 **コマンド タイトル**、および **コマンドの説明** を入力します。

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
| `parameters.value` | パラメーターの初期値。 現在、値はサポートされていません | いいえ | 1.5 |

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
