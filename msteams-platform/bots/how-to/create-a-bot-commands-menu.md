---
title: Bot 用のコマンドメニューを作成する
author: clearab
description: Microsoft Teams bot のコマンドメニューを作成する方法
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: 81efb94fc882aa4653ab162863d5d973aeae87b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674764"
---
# <a name="bot-command-menus"></a>Bot コマンドメニュー

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> Bot メニューは、モバイルクライアントに表示されません。

Bot の [コマンドの追加] メニューを使用すると、bot がいつでも応答できるコアコマンドのセットを定義できます。 コマンドの一覧は、ユーザーが bot と conversing したときに、作成メッセージ領域の上のユーザーに表示されます。 一覧からコマンドを選択すると、作成メッセージボックスにコマンド文字列が挿入され、すべてのユーザーが実行する必要があるのは、[**送信**] を選択します。

![Bot のコマンドメニュー](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>Bot 用のコマンドメニューを作成する

コマンドメニューは、アプリマニフェストで定義されています。 アプリの作成には、アプリ Studio を使用するか、手動で追加することができます。

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a>アプリ Studio を使用して bot のコマンドメニューを作成する

この手順では、既存のアプリマニフェストを編集することを前提としています。 コマンドメニューを追加する手順は、新しいマニフェストを作成しているか、既存のものを編集している場合と同じです。

1. [アプリ Studio] を開きます。左側のナビゲーションレールのオーバーフローメニュー。 利用可能なアプリ Studio がない場合は、ダウンロードできます。 アプリの使用の詳細については、「 [App studio のインストール](https://aka.ms/teams-app-studio#installing-app-studio)」を参照してください。

    ![App Studio](./conversations/media/AppStudio.png)

2. App Studio で、[**マニフェストエディター** ] タブを選択します。

3. [**機能**] セクションの [マニフェストエディター] ビューの左側の列で、[ **bot**] を選択します。

4. マニフェストエディターの右側の列にある [**コマンド**] セクションで、[**追加**] ボタンを選択します。

    ![App Studio コマンドメニューの [追加] ボタン](./conversations/media/AppStudio-CommandMenu-Add.png)

5. [**新しいコマンド**] 画面が表示されます。 メニューコマンドとして表示する**コマンドテキスト**を入力し、メニューのコマンドテキストのすぐ下に表示する**ヘルプテキスト**を入力します。 このコマンドの目的を簡単に説明します。

6. 次に、このコマンドメニューを表示する範囲を選択し、[**保存**] ボタンを選択します。

    ![App Studio コマンドメニューの [追加] ボタン](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a>**マニフェスト**を編集して bot のコマンドメニューを作成する

コマンドメニューを作成するもう1つの有効な方法は、ボットソースコードを開発する際にマニフェストファイルで直接作成することです。 この方法を使用する場合は、次の点に注意してください。

1. 各メニューは最大10個のコマンドをサポートします。

2. すべてのスコープで動作する、1つのコマンドメニューを作成できます。

3. 各範囲に異なるコマンドメニューを作成できます。

#### <a name="manifest-example---single-menu-for-both-scopes"></a>マニフェストの例-両方のスコープの単一のメニュー

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

#### <a name="manifest-example---menu-for-each-scope"></a>各範囲のマニフェストの例-メニュー

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

## <a name="handling-menu-commands-in-your-bot-code"></a>Bot コードでメニューコマンドを処理する

グループまたはチャネル内のボットは、メッセージ内で ("@botname") 指摘された場合にのみ応答します。 その結果、グループまたはチャネルスコープ内で bot が受信するすべてのメッセージには、返されるメッセージテキストに独自の名前が含まれます。 返されるコマンドを処理する前に、メッセージの解析によって処理されるようにする必要があります。

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

メッセージテキストの** \@メンション**部分は、Microsoft Bot フレームワークで提供される静的メソッド (という名前`Activity` `RemoveRecipientMention`のクラスのメソッド) を使用して解析できます。

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

メッセージテキストの** \@メンション**部分は、Microsoft Bot フレームワークで提供される静的メソッド (という名前`TurnContext` `removeMentionText`のクラスのメソッド) を使用して解析できます。

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[Python](#tab/python)


メッセージテキストの **@Mention**部分を解析するには、Microsoft Bot フレームワークで提供される静的メソッド (という名前`TurnContext` `remove_recipient_mention`のクラスのメソッド) を使用します。

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a>コマンドメニューのベストプラクティス

* **簡単にお勧め**します。 bot メニューは、ボットの主要な機能を提供することを目的としています。
* **短くして**ください。メニューオプションが非常に長くて複雑な自然言語ステートメントである必要はありません。これらは単純なコマンドである必要があります。
* **被呼び出しを維持**する: ボットメニューのアクション/コマンドは、会話の状態や bot があるダイアログに関係なく、常に使用可能にする必要があります。
