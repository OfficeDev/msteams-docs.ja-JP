---
title: ボットのコマンド メニューを作成する
author: surbhigupta
description: コード サンプルを使用して、Microsoft Teams ボットのコマンド メニューを作成する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
keywords: コマンド メニューでメッセージ会話@mentionを作成する
ms.openlocfilehash: 6f4b9cdac76fc9beb42a39dde3b320036ea580b5
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102555"
---
# <a name="bot-command-menus"></a>Bot コマンド メニュー

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

ボットが応答できる一連のコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加します。 コマンドの一覧は、ボットと会話しているときに、メッセージ作成領域のユーザーに表示されます。 一覧からコマンドを選択して、メッセージの作成ボックスにコマンド文字列を挿入し、[ **送信**] を選択します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

![Bot コマンド メニュー](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[モバイル](#tab/mobile)

![モバイル ボットのコマンド メニュー](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>ボットのコマンド メニューを作成する

コマンド メニューは、アプリ マニフェストで定義されます。 **App Studio** を使用して作成するか、アプリ マニフェストに手動で追加できます。

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>App Studio を使用してボットのコマンド メニューを作成する

ボットのコマンド メニューを作成するための前提条件は、既存のアプリ マニフェストを編集する必要があるということです。 コマンド メニューを追加する手順は、新しいマニフェストを作成するか、既存のマニフェストを編集するかに関係なく、同じです。

**App Studio を使用してボットのコマンド メニューを作成するには**

1. Teams開き、左側のウィンドウで **[アプリ**] を選択します。 [ **アプリ]** ページで App **Studio** を検索し、[ **開く**] を選択します。
   > [!NOTE]
   > **App Studio** をお持ちでない場合は、ダウンロードできます。 詳細については、 [App Studio のインストールに関するページを](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)参照してください。

    :::image type="content" source="/media/AppStudio.png" alt-text="アプリ スタジオのインストール"lightbox="media/AppStudio.png"border="true":::

2. **App Studio** で、[**マニフェスト エディター**] タブを選択します。既存のアプリ パッケージがない場合は、既存のアプリを作成またはインポートできます。 詳細については、「 [アプリ パッケージの更新」を](~/get-started/deploy-csharp-app-studio.md)参照してください。

3. **マニフェスト エディター** の左側のウィンドウで、[**機能**] セクションで [**ボット**] を選択します。

4. **マニフェスト エディター** の右側のウィンドウで、[**コマンド**] セクションで [**追加**] を選択します。 **[新しいコマンド]** 画面が表示されます。

    :::image type="content" source="/media/AppStudio-CommandMenu-Add.png" alt-text="アプリ パッケージを選択する"lightbox="/media/AppStudio-CommandMenu-Add.png"border="true":::

5. ボットの **コマンド** メニューとして表示する必要があるコマンド テキストを入力します。

6. メニューのコマンド テキストの下に表示する必要がある **ヘルプ** テキストを入力します。 **ヘルプ テキスト** は、コマンドの目的を簡単に説明する必要があります。

7. [ **スコープ** ] チェック ボックスをオンにして、このコマンド メニューを表示する必要がある場所を選択し、[保存] を選択 **します**。

:::image type="content" source="/media/AppStudio-NewCommandMenu.png" alt-text="App Studio の [新しいコマンド] メニュー ボタン"lightbox="/media/AppStudio-NewCommandMenu.png"border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Manifest.json を編集してボットのコマンド メニューを作成する

コマンド メニューを作成するもう 1 つの方法は、ボットのソース コードの開発中にマニフェスト ファイルに直接作成することです。 このメソッドを使用するには、次の点に従います。

* 各メニューでは、最大 10 個のコマンドがサポートされます。
* すべてのスコープで動作する 1 つのコマンド メニューを作成します。
* スコープごとに異なるコマンド メニューを作成します。

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>両方のスコープの単一メニューのマニフェストの例

両方のスコープの単一メニューのマニフェストサンプル コードは次のとおりです。

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>各スコープのメニューのマニフェストの例

各スコープのメニューのマニフェストコード例は次のとおりです。

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

ユーザーからのメッセージを処理するときは、ボット コード内のメニュー コマンドを処理する必要があります。 メッセージ テキストのメンション部分を解析することで、**\@** ボット コード内のメニュー コマンドを処理できます。

## <a name="handle-menu-commands-in-your-bot-code"></a>ボット コードでメニュー コマンドを処理する

グループまたはチャネル内のボットは、メッセージに記載されている `@botname` 場合にのみ応答します。 グループスコープまたはチャネル スコープ内でボットによって受信されたすべてのメッセージには、メッセージ テキストにその名前が含まれています。 返されるコマンドを処理する前に、メッセージ解析でボットが受信したメッセージをその名前で処理する必要があります。

> [!NOTE]
> コード内のコマンドを処理するために、通常のメッセージとしてボットに送信されます。 ユーザーからの他のメッセージを処理する場合と同様に、それらを処理する必要があります。 コード内のコマンドは、テキスト ボックスに事前構成されたテキストを挿入します。 その後、ユーザーはそのテキストを他のメッセージと同様に送信する必要があります。

# <a name="c"></a>[C#](#tab/dotnet)

Microsoft Bot Frameworkで提供される静的メソッドを使用して、メッセージ テキストのメンション部分を解析できます。**\@** という名前`RemoveRecipientMention`のクラスの`Activity`メソッドです。

メッセージ テキストのメンション部分を **\@** 解析する C# コードは次のとおりです。

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Bot Framework で提供される静的メソッドを **\@** 使用して、メッセージ テキストのメンション部分を解析できます。 という名前`removeMentionText`のクラスの`TurnContext`メソッドです。

メッセージ テキストのメンション部分を **\@** 解析する JavaScript コードは次のとおりです。

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Bot Framework で提供される静的メソッドを使用して、メッセージ テキストの **@Mention** 部分を解析できます。 という名前`remove_recipient_mention`のクラスの`TurnContext`メソッドです。

メッセージ テキストのメンション部分を **\@** 解析する Python コードは次のとおりです。

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

ボット コードの円滑な機能を有効にするには、従う必要があるベスト プラクティスがいくつかあります。

## <a name="command-menu-best-practices"></a>コマンド メニューのベスト プラクティス

コマンド メニューのベスト プラクティスを次に示します。

* シンプルに保つ: ボット メニューは、ボットの主要な機能を示すために使用されます。
* 短くしてください。メニュー オプションは長くすることはできません。複雑な自然言語ステートメントにすることはできません。 単純なコマンドである必要があります。
* 呼び出し可能な状態に保つ: ボットのメニュー アクションまたはコマンドは、会話の状態やボットのダイアログに関係なく、常に使用できる必要があります。

> [!NOTE]
> マニフェストからコマンドを削除する場合は、変更を実装するためにアプリを再デプロイする必要があります。 一般に、マニフェストに変更を加える場合は、アプリを再デプロイする必要があります。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [チャネルとグループ会話](~/bots/how-to/conversations/channel-and-group-conversations.md)
