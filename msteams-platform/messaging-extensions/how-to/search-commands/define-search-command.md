---
title: メッセージ拡張機能の検索コマンドを定義する
author: surbhigupta
description: Teams アプリのメッセージ拡張機能検索コマンドについて説明します。アプリ マニフェストを使用して検索コマンドを作成し、手動で作成します。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 9ec7ea734e331fcfb563702d18284f4831c369f6
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820179"
---
# <a name="define-message-extension-search-commands"></a>メッセージ拡張機能の検索コマンドを定義する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

メッセージ拡張検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカードの形式でメッセージに挿入できます。 このドキュメントでは、検索コマンドの呼び出し場所を選択し、検索コマンドをアプリ マニフェストに追加する方法について説明します。

> [!NOTE]
> 結果カードのサイズ制限は 28 KB です。 カードのサイズが 28 KB を超える場合、カードは送信されません。

メッセージ拡張機能の検索コマンドを定義する方法については、次のビデオを参照してください。
<br>

> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4OIvK>]
<br>

## <a name="select-search-command-invoke-locations"></a>検索コマンド呼び出しの場所を選択する

検索コマンドは、次のいずれかの場所または両方から呼び出されます。

* メッセージ作成領域: 作成メッセージ領域の下部にあるボタン。
* コマンド ボックス: コマンド ボックスに@mentioningします。

新規作成メッセージ領域から検索コマンドが呼び出されると、ユーザーは結果を会話に送信します。 コマンド ボックスから呼び出されると、ユーザーは結果のカードと対話するか、別の場所で使用するためにコピーします。

次の図は、検索コマンドの呼び出し場所を示しています。

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="Teams チャネルの検索コマンドの呼び出し場所を示すスクリーンショット。":::

## <a name="add-the-search-command-to-your-app-manifest"></a>アプリ マニフェストに検索コマンドを追加する

検索コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON の最上位に新しい `composeExtension` オブジェクトを追加する必要があります。 検索コマンドは、開発者ポータルの助けを借りて追加することも、手動で追加することもできます。

### <a name="create-a-search-command-using-developer-portal"></a>開発者ポータルを使用して検索コマンドを作成する

検索コマンドを作成するための前提条件は、メッセージ拡張機能を既に作成している必要があるということです。 メッセージ拡張機能を作成する方法については、「[メッセージ拡張機能の作成](~/messaging-extensions/how-to/create-messaging-extension.md)」を参照してください。

**操作コマンドを作成するには**

1. Microsoft Teams クライアントから **開発者ポータル** を開き、[ **アプリ** ] タブを選択します。 **開発者ポータル** でアプリ パッケージを既に作成している場合は、一覧から選択します。 アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。
1. アプリ パッケージをインポートした後、[アプリ **の機能**] で [**メッセージ拡張機能**] を選択します。
1. メッセージ拡張機能を作成するには、Microsoft 登録ボットが必要です。 既存のボットを使用するか、新しいボットを作成できます。 [ **新しいボットの作成** ] オプションを選択し、新しいボットに名前を付けて、[ **作成**] を選択します。

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="Teams 開発者ポータルでアプリのボットを構成するオプションを示すスクリーンショット。":::

1. 既存のボットを使用するには、[ **既存のボットの選択** ] を選択し、ドロップダウン リストから既存のボットを選択するか、ボット ID が既に作成されている場合は **[ボット ID の入力** ] を選択します。

1. メッセージング拡張機能のスコープを選択し、[保存] を選択 **します**。

1. [**コマンド**] セクションで [**コマンドの追加]** を選択して、メッセージ拡張機能の動作を決定するコマンドを含めます。
次の画像は、メッセージ拡張機能のコマンドの追加を表示します。

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="Teams 開発者ポータルでコマンドを追加してメッセージ拡張機能の動作を定義する方法を示すスクリーンショット。":::

1. [ **検索** ] を選択し、 **コマンド ID**、 **コマンド タイトル**、および **コマンドの説明** を入力します。

1. すべてのパラメーターを入力し、ドロップダウン リストから入力の種類を選択します。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="メッセージ拡張機能の Teams 開発者ポータルでコマンドを定義するパラメーターを追加する方法を示すスクリーンショット。":::

1. [**プレビュー リンク**] **で [ドメインの追加]** を選択します。

1. 有効なドメインを入力し、[ **追加**] を選択します。

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="リンク展開のためにメッセージング拡張機能に有効なドメインを追加する方法を示すスクリーンショット。":::

1. **[保存]** を選択します。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="メッセージ拡張機能のすべての設定とパラメーターを保存する方法を示すスクリーンショット。":::

**パラメーターを追加するには**

1. コマンド セクションで省略記号を選択し、[ **パラメーターの編集**] を選択します。

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="メッセージ拡張機能のパラメーターを編集する方法を示すスクリーンショット。":::

1. [ **パラメーターの追加] を** 選択し、すべてのパラメーターを入力します。

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="メッセージ拡張機能のパラメーターを追加する方法を示すスクリーンショット。"lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

### <a name="create-a-search-command-manually"></a>手動で検索コマンドを作成する

メッセージ拡張機能検索コマンドをアプリ マニフェストに手動で追加するには、オブジェクトの配列に次のパラメーターを `composeExtension.commands` 追加する必要があります。

| プロパティ名 | 用途 | 必須 | マニフェストの最小バージョン |
|---|---|---|---|
| `id` | このプロパティは、検索コマンドに割り当てる一意の ID です。 ユーザー要求には、この ID が含まれています。 | はい | 1.0 |
| `title` | このプロパティはコマンド名です。 この値は、ユーザー インターフェイス (UI) に表示されます。 | はい | 1.0 |
| `description` | このプロパティは、このコマンドの動作を示すヘルプ テキストです。 この値は UI に表示されます。 | はい | 1.0 |
| `type` | このプロパティは である `query`必要があります。 | いいえ | 1.4 |
|`initialRun` | このプロパティが **true** に設定されている場合は、ユーザーが UI でこのコマンドを選択するとすぐにこのコマンドを実行する必要があることを示します。 | いいえ | 1.0 |
| `context` | このプロパティは、検索アクションが使用できるコンテキストを定義する値の省略可能な配列です。 使用可能な値: `message`、`compose`、`commandBox`。 既定値は `["compose", "commandBox"]` です。 | いいえ | 1.5 |

Teams クライアントでユーザーに表示されるテキストを定義する検索パラメーターの詳細を追加する必要があります。

| プロパティ名 | 用途 | は必須ですか? | マニフェストの最小バージョン |
|---|---|---|---|
| `parameters` | このプロパティは、 コマンドのパラメーターの静的リストを定義します。 | いいえ | 1.0 |
| `parameter.name` | このプロパティは、パラメーターの名前を説明します。 は `parameter.name` 、ユーザー要求でサービスに送信されます。 | はい | 1.0 |
| `parameter.description` | このプロパティは、パラメーターの目的または指定する必要がある値の例について説明します。 この値は UI に表示されます。 | はい | 1.0 |
| `parameter.title` | このプロパティは、ユーザー フレンドリな短いパラメーターのタイトルまたはラベルです。 | はい | 1.0 |
| `parameter.inputType` | このプロパティは、必要な入力の型に設定されます。 指定できる値には、、`number``textarea`、`date`、 `time`が`toggle`含まれます`text`。 既定値は に `text`設定されています。 | いいえ | 1.4 |
| `parameters.value` | パラメーターの初期値。 現在、値はサポートされていません | いいえ | 1.5 |

#### <a name="example"></a>例

次のセクションでは、検索コマンドを定義するオブジェクトの `composeExtensions` 単純なアプリ マニフェストの例を示します。

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

完全なアプリ マニフェストについては、「 [アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md)」を参照してください。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams メッセージ拡張機能検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

詳細 [なガイド](../../../sbs-messagingextension-searchcommand.yml) に従って、検索ベースのメッセージ拡張機能を作成します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [検索コマンドに応答します](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。

## <a name="see-also"></a>関連項目

* [カード](../../../task-modules-and-cards/what-are-cards.md)
* [タスク モジュール](../../../task-modules-and-cards/what-are-task-modules.md)
* [Teams のアプリ マニフェストのスキーマ](../../../resources/schema/manifest-schema.md)
* [Teams の開発者ポータル](../../../concepts/build-and-test/teams-developer-portal.md)
* [メッセージの拡張機能](../../what-are-messaging-extensions.md)
