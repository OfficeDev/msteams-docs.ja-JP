---
title: ボット用のコマンド メニューを作成する
author: surbhigupta
description: このモジュールでは、コード サンプルを使用して、Microsoft Teams ボットのコマンド メニューを作成して処理する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 1dff29ca48a7efb3338816394c177de7779714ee
ms.sourcegitcommit: fb0942afb8be32d92df282dec03fbb3b13f8f303
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2022
ms.locfileid: "67264177"
---
# <a name="create-a-commands-menu"></a>コマンド メニューを作成する

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットが応答できる一連のコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加します。 コマンドの一覧は、ボットと会話しているときに、メッセージ作成領域のユーザーに表示されます。 一覧からコマンドを選択して、メッセージの作成ボックスにコマンド文字列を挿入し、**[送信]** を選択します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="conversations/Media/bot-menu-sample.png" alt-text="Bot-command-menu":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="conversations/Media/mobile-bot-menu-sample.png" alt-text="Mobile-bot-command-menu":::

* * *

## <a name="create-a-command-menu-for-your-bot"></a>ボット用のコマンド メニューを作成する

コマンド メニューは、アプリ マニフェスト内で定義されます。 **App Studio** を使用して作成するか、アプリ マニフェストに手動で追加します。

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>App Studio を使用してボットのコマンド メニューを作成する

ボットのコマンド メニューを作成するための前提条件は、既存のアプリ マニフェストを編集する必要があるということです。 コマンド メニューを追加する手順は、新しいマニフェストを作成するか、それとも既存のマニフェストを編集するかに関わらず、同じです。

**App Studio を使用してボットのコマンド メニューを作成するには**

1. Teams を開き、左側のウィンドウから **[アプリ]** を選択します。 **[アプリ]** ページで **App Studio** を検索し、**[開く]** を選択します。

   > [!WARNING]
   > App Studio を使用している場合は、開発者ポータルで Teams アプリの設定、配布、管理を行うことをお勧めします。 App Studio は、2022 年 8 月 1 日に非推奨になりました。

   :::image type="content" source="conversations/Media/AppStudio.png" alt-text="appstudio-media":::

2. **App Studio** で、**[マニフェスト エディター]** タブを選択します。既存のアプリ パッケージがない場合は、既存のアプリを作成またはインポートできます。 詳細については、「 [App Studio で C# アプリ パッケージを更新する」を](../../get-started/deploy-csharp-app-studio.md)参照してください。

3. **[マニフェスト エディター]** の左側のウィンドウで、**[機能]** セクション内で **[ボット]** を選択します。

4. **[マニフェスト エディター]** の右側のウィンドウで、**[コマンド]** セクションで **[追加]** を選択します。 **[新規コマンド]** 画面が表示されます。

   :::image type="content" source="media/AppStudio-CommandMenu-Add.png" alt-text="アプリのパッケージを選択する" lightbox="media/AppStudio-CommandMenu-Add.png "border="true":::

5. ボットのコマンド メニューとして表示する必要がある **コマンド テキスト** を入力します。

6. メニューのコマンド テキストの下に表示する必要がある **ヘルプ テキスト** を入力します。 **ヘルプ テキスト** は、コマンドの目的を簡単に説明する必要があります。

7. **[スコープ]** チェック ボックスをオンにして、このコマンド メニューを表示する必要がある場所を選択し、**[保存]** を選択します。

   :::image type="content" source="media/AppStudio-NewCommandMenu.png" alt-text="App Studio の [新しいコマンド] メニュー ボタン "lightbox="media/AppStudio-NewCommandMenu.png "border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Manifest.json を編集してボットのコマンド メニューを作成する

コマンド メニューを作成する別の方法は、ボットのソース コードの開発中にマニフェスト ファイルに直接作成することです。 このメソッドを使用するには、次の項目に従います:

* 各メニューでは、最大 10 個のコマンドをサポートします。
* すべてのスコープで動作する 1 つのコマンド メニューを作成します。
* スコープごとに異なるコマンド メニューを作成します。

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>両方のスコープのための単一メニューのマニフェストの例

両方のスコープのための単一メニューのマニフェストのサンプル コードは次のとおりです:

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>各スコープのメニューのためのマニフェストの例

各スコープのメニューのためのマニフェストのサンプル コードは次のとおりです。

```json
{
  ...
  "bots":[
    {
      "botId":"<Microsoft app ID for your bot>",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

ユーザーからのどんなメッセージを処理するときも、ボット コード内のメニュー コマンドを処理する必要があります。 ボット コードでメニュー コマンドを処理するには、メッセージ テキストの **\@メンション** 部分を解析します。

## <a name="handle-menu-commands-in-your-bot-code"></a>ボット コード内でメニュー コマンドを処理する

グループまたはチャンネル内のボットは、メッセージ内で `@botname` をメンションした時のみ応答します。 グループまたはチャンネル スコープ内でボットによって受信されたすべてのメッセージには、メッセージ テキストにその名前が含まれています。 返されるコマンドを処理する前に、メッセージ解析処理で、ボットが受信した名前付きのメッセージを処理する必要があります。

> [!NOTE]
> コード内のコマンドを処理するために、通常のメッセージとしてボットに送信されます。 ユーザーからの他のメッセージを処理する場合と同様に、それらを処理する必要があります。 コード内のコマンドは、テキスト ボックスに事前構成されたテキストを挿入します。 その後、ユーザーはそのテキストを他のメッセージと同様に送信する必要があります。

# <a name="c"></a>[C#](#tab/dotnet)

Microsoft Bot Framework で提供される静的メソッドを使用して、メッセージ テキストの **\@メンション** 部分を解析できます。 `Activity`名前付きクラス`RemoveRecipientMention`のメソッドです。

メッセージ テキストの **\@メンション** 部分を解析する C# コードは次のとおりです。

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Bot Framework で提供される静的メソッドを使用して、メッセージ テキストの **\@メンション** 部分を解析できます。 `TurnContext`名前付きクラス`removeMentionText`のメソッドです。

メッセージ テキストの **\@メンション** 部分を解析する JavaScript コードは次のとおりです。

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Bot Framework で提供される静的メソッドを使用して、メッセージ テキストの **@Mention** 部分を解析できます。 `TurnContext`名前付きクラス`remove_recipient_mention`のメソッドです。

メッセージ テキストの **\@メンション** 部分を解析する Python コードは次のとおりです:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

ボット コードを円滑に機能させることを有効化するには、従う必要があるベスト プラクティスがいくつかあります。

## <a name="command-menu-best-practices"></a>コマンド メニューのベスト プラクティス

コマンド メニューのベスト プラクティスを次に示します:

* シンプルに保つ: ボット メニューは、ボットの主要な機能を示す意味があります。
* 短くしてください: メニュー オプションは長くすることはできず、また複雑ではない自然言語ステートメントでなければなりません。 単純なコマンドである必要があります。
* 実行可能な状態に保つ: ボットのメニュー アクションまたはコマンドは、会話の状態やボットのダイアログに関係なく、常に使用できる必要があります。

> [!NOTE]
> マニフェストからコマンドを削除する場合は、変更を実装するためにアプリを再デプロイする必要があります。 一般的に、マニフェストに変更を加える場合は、アプリを再デプロイする必要があります。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [チャネルとグループ会話](~/bots/how-to/conversations/channel-and-group-conversations.md)
