---
title: ボットのコマンド メニューを作成する
author: clearab
description: Microsoft Teams ボットのコマンド メニューを作成する方法
ms.topic: how-to
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: da87725fca6b4eeacd43f48f6946920251d772e9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020913"
---
# <a name="bot-command-menus"></a>ボット コマンド メニュー

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> ボット メニューはモバイル クライアントには表示されません。

ボットが応答できる一連のコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。 コマンドの一覧は、ボットと会話するときに、作成メッセージ領域のユーザーに表示されます。 一覧からコマンドを選択して、コマンド文字列をメッセージ作成ボックスに挿入し、[送信] を **選択します**。

![ボット コマンド メニュー](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>ボットのコマンド メニューを作成する

コマンド メニューは、アプリ マニフェストで定義されます。 App Studio を使用 **して作成するか** 、アプリ マニフェストに手動で追加できます。

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>App Studio を使用してボットのコマンド メニューを作成する

ボットのコマンド メニューを作成するには、既存のアプリ マニフェストを編集する必要があります。 新しいマニフェストを作成するか、既存のマニフェストを編集するかに関して、コマンド メニューを追加する手順は同じです。

**App Studio を使用してボットのコマンド メニューを作成するには**

1. Teams を開き、左側 **のウィンドウ** から [アプリ] を選択します。 [アプリ **] ページで** App Studio を検索 **し、[開** く] を **選択します**。 
   > [!NOTE]
   > App Studio をお持ち **ではない場合** は、ダウンロードできます。 詳細については [、「App Studio のインストール」を参照してください](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)。

    ![App Studio](./conversations/media/AppStudio.png)

2. **App Studio で、[** マニフェスト エディター]**タブを選択** します。既存のアプリ パッケージをお持ちではない場合は、既存のアプリを作成またはインポートできます。 詳細については、「アプリ パッケージの [更新」を参照してください](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)。

3. マニフェスト エディターの左側のウィンドウ **で** 、[機能] セクションで **[ボット** ] **を選択します**。

4. マニフェスト エディターの右側のウィンドウ **で、[コマンド** ] セクション **で、[追加** ] を **選択します**。 [ **新しいコマンド]** 画面が表示されます。

    ![App Studio コマンド メニュー [追加] ボタン](./conversations/media/AppStudio-CommandMenu-Add.png)

5. ボットの **コマンド メニュー** として表示する必要がある Command テキストを入力します。

6. メニューの **コマンド テキストの** 下に表示する必要があるヘルプ テキストを入力します。 **ヘルプ テキスト** は、コマンドの目的を簡単に説明する必要があります。

7. [スコープ **] チェック** ボックスをオンにして、このコマンド メニューを表示する必要がある場所を選択し、[保存] を **選択します**。

    ![App Studio の [新しいコマンド] メニュー ボタン](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>ボットのコマンド メニューを作成するには、[オン] をManifest.jsします。

コマンド メニューを作成するもう 1 つの方法は、ボットソース コードの開発中にマニフェスト ファイルに直接作成することです。 このメソッドを使用するには、次の点に従います。

* 各メニューは、最大 10 個のコマンドをサポートします。
* すべてのスコープで機能する 1 つのコマンド メニューを作成します。
* スコープごとに異なるコマンド メニューを作成します。

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>両方のスコープの単一メニューのマニフェスト例

両方のスコープの単一メニューのマニフェストのコード例は次のとおりです。

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>各スコープのメニューのマニフェスト例

各スコープのメニューのマニフェストのコード例は次のとおりです。

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

ユーザーからのメッセージを処理する場合は、ボット コードでメニュー コマンドを処理する必要があります。 メッセージ テキストのメンション部分を解析することで、ボット コード内の **\@ メニュー** コマンドを処理できます。

## <a name="handle-menu-commands-in-your-bot-code"></a>ボット コードでメニュー コマンドを処理する

グループまたはチャネル内のボットは、メッセージに記載されている場合 `@botname` にのみ応答します。 グループスコープまたはチャネル スコープ内でボットが受信したメッセージには、返されるメッセージ テキストに名前が含まれるすべてのメッセージが含まれる。 返されるコマンドを処理する前に、メッセージ解析でボットが受信したメッセージの名前を処理する必要があります。

> [!NOTE]
> コード内のコマンドを処理するために、通常のメッセージとしてボットに送信されます。 ユーザーからの他のメッセージを処理する場合と同じ方法で処理する必要があります。 コード内のコマンドは、あらかじめ構成されたテキストをテキスト ボックスに挿入します。 その後、ユーザーはそのテキストを他のメッセージと同じ方法で送信する必要があります。

# <a name="c"></a>[C#](#tab/dotnet)

Microsoft Bot Framework で **\@ 提供される静的** メソッドを使用して、メッセージ テキストのメンション部分を解析できます。 という名前のクラス `Activity` のメソッドです `RemoveRecipientMention` 。

メッセージ C#メンション部分を解析するコード **\@** は次のとおりです。

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

ボット フレームワークで提供される **\@ 静的** メソッドを使用して、メッセージ テキストのメンション部分を解析できます。 という名前のクラス `TurnContext` のメソッドです `removeMentionText` 。

メッセージ テキストのメンション部分を解析する **\@ JavaScript** コードは次のとおりです。

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

ボット フレームワークで提供される **静的@Mention** を使用して、メッセージ テキストの一部を解析できます。 という名前のクラス `TurnContext` のメソッドです `remove_recipient_mention` 。

メッセージ テキストの Mention 部分を解析する **\@ Python** コードは次のとおりです。

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

ボット コードの円滑な機能を有効にするには、従う必要があるベスト プラクティスがいくつかある。

## <a name="command-menu-best-practices"></a>コマンド メニューのベスト プラクティス

コマンド メニューのベスト プラクティスを次に示します。

* シンプルに保つ: ボット メニューは、ボットの主要な機能を提示することを目的とします。
* 短くしてください:メニュー オプションは長くする必要があります。また、複雑な自然言語ステートメントで指定する必要があります。 単純なコマンドである必要があります。
* 呼び出し可能な状態を維持する: ボット メニューの操作またはコマンドは、会話の状態やボットが含むダイアログに関係なく、常に使用できる必要があります。

> [!NOTE]
> マニフェストからコマンドを削除する場合は、変更を実装するためにアプリを再展開する必要があります。 一般に、マニフェストに対する変更を行う場合は、アプリを再展開する必要があります。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [チャネルとグループ会話](~/bots/how-to/conversations/channel-and-group-conversations.md)
