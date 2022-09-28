---
title: ボット用のコマンド メニューを作成する
author: surbhigupta
description: Microsoft Teams ボットのコマンド メニューを作成して処理する方法とベスト プラクティスについて説明します。 マニフェストからコマンドを削除する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 0e0f9ce9ada0cde0aa6f7b6b29c7badb07dd7db9
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100904"
---
# <a name="create-a-commands-menu"></a>コマンド メニューを作成する

> [!NOTE]
> Teams 用の新しい世代開発ツールを使用して JavaScript を使用してコマンド ボットをビルドする手順に従って [、コマンド ボット](../../sbs-gs-commandbot.yml) を作成することをお勧めします。 Teams Toolkit の詳細については、「 [Visual Studio Code の Teams Toolkit の概要」と「Visual Studio](../../toolkit/teams-toolkit-fundamentals.md) [の Teams Toolkit の概要」を](../../toolkit/teams-toolkit-overview-visual-studio.md)参照してください。

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットが応答できる一連のコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加します。 コマンドの一覧は、ボットと会話しているときに、メッセージ作成領域のユーザーに表示されます。 一覧からコマンドを選択して、メッセージの作成ボックスにコマンド文字列を挿入し、**[送信]** を選択します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="conversations/Media/bot-menu-sample.png" alt-text="Bot-command-menu":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="conversations/Media/mobile-bot-menu-sample.png" alt-text="Mobile-bot-command-menu":::

* * *

## <a name="create-a-command-menu-for-your-bot"></a>ボット用のコマンド メニューを作成する

コマンド メニューは、アプリ マニフェスト内で定義されます。 **開発者ポータル** を使用して作成するか、アプリ マニフェストに手動で追加できます。

### <a name="create-a-command-menu-for-your-bot-using-developer-portal"></a>開発者ポータルを使用してボットのコマンド メニューを作成する

ボットのコマンド メニューを作成するための前提条件は、既存のアプリ マニフェストを編集する必要があるということです。 コマンド メニューを追加する手順は、新しいマニフェストを作成するか、それとも既存のマニフェストを編集するかに関わらず、同じです。

開発者ポータルを使用してボットのコマンド メニューを作成するには:

1. Teams を開き、左側のウィンドウから **[アプリ]** を選択します。 [ **アプリ** ] ページで **、開発者ポータル** を検索し、[ **開く**] を選択します。

   :::image type="content" source="../../assets/images/tdp/add-dev-portal.png" alt-text="スクリーンショットは、Teams クライアントに開発者ポータルを追加する方法を示しています。":::
  
1. **開発者ポータル** で、[**アプリ**] タブを選択します。既存のアプリ パッケージがない場合は、既存のアプリを作成またはインポートできます。 詳細については、「 [Teams 用開発者ポータル](../../concepts/build-and-test/teams-developer-portal.md)」を参照してください。

1. [ **アプリ** ] タブを選択し、左側のウィンドウで **[アプリの機能** ] を選択し、[ **ボット**] を選択します。

1. [ **コマンド] セクションで [コマンドの追加]** **を** 選択します。

   :::image type="content" source="../../assets/images/tdp/add-a-bot-command.png" alt-text="スクリーンショットは、開発者ポータルでボットのコマンドを追加する方法を示しています。":::

1. ボットの **コマンド** メニューとして表示されるコマンドを入力します。

1. メニューのコマンド テキストの下に表示される **説明** を入力します。 **説明** は、コマンドの目的の簡単な説明である必要があります。

1. [ **スコープ** ] チェック ボックスをオンにし、[ **追加**] を選択します。
   これにより、コマンド メニューを表示する必要がある場所が定義されます。

   :::image type="content" source="../../assets/images/tdp/bot-command.png" alt-text="スクリーンショットは、ボットのコマンド、説明、スコープを追加する方法を示しています。":::

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
