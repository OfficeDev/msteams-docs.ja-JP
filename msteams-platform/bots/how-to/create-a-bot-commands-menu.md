---
title: Bot 用のコマンドメニューを作成する
author: clearab
description: Microsoft Teams bot のコマンドメニューを作成する方法
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: ccbacc6ec6f18a38512d81dc898d0b14357d6ef7
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552487"
---
# <a name="bot-command-menus"></a><span data-ttu-id="f5cb1-103">Bot コマンドメニュー</span><span class="sxs-lookup"><span data-stu-id="f5cb1-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="f5cb1-104">Bot メニューは、モバイルクライアントに表示されません。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-104">Bot menus won't appear on mobile clients.</span></span>

<span data-ttu-id="f5cb1-105">Bot の [コマンドの追加] メニューを使用すると、bot がいつでも応答できるコアコマンドのセットを定義できます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-105">Add command menu for your bot allows you to define a set of core commands your bot can always respond to.</span></span> <span data-ttu-id="f5cb1-106">コマンドの一覧は、ユーザーが bot と conversing したときに、作成メッセージ領域の上のユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-106">The list of commands is presented to the user above the compose message area when they are conversing with your bot.</span></span> <span data-ttu-id="f5cb1-107">一覧からコマンドを選択すると、作成メッセージボックスにコマンド文字列が挿入され、すべてのユーザーが実行する必要があるのは、[ **送信**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-107">Selecting a command from the list will insert the command string into the compose message box, then all users need to do is select **Send**.</span></span>

![Bot のコマンドメニュー](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="f5cb1-109">Bot 用のコマンドメニューを作成する</span><span class="sxs-lookup"><span data-stu-id="f5cb1-109">Create a command menu for your bot</span></span>

<span data-ttu-id="f5cb1-110">コマンドメニューは、アプリマニフェストで定義されています。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="f5cb1-111">アプリの作成には、アプリ Studio を使用するか、手動で追加することができます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-111">You can either use App Studio to help you create them, or add them manually.</span></span>

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="f5cb1-112">アプリ Studio を使用して bot のコマンドメニューを作成する</span><span class="sxs-lookup"><span data-stu-id="f5cb1-112">Creating a command menu for your bot using App Studio</span></span>

<span data-ttu-id="f5cb1-113">この手順では、既存のアプリマニフェストを編集することを前提としています。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-113">The instructions here assume that you'll be editing an existing app manifest.</span></span> <span data-ttu-id="f5cb1-114">コマンドメニューを追加する手順は、新しいマニフェストを作成しているか、既存のものを編集している場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-114">The steps for adding a command menu are the same, whether you're creating a new manifest or editing an existing one.</span></span>

1. <span data-ttu-id="f5cb1-115">[アプリ Studio] を開きます。左側のナビゲーションレールのオーバーフローメニュー。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-115">Open App Studio from the ... overflow menu on the left navigation rail.</span></span> <span data-ttu-id="f5cb1-116">利用可能なアプリ Studio がない場合は、ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-116">If you don't have App Studio available you can download it.</span></span> <span data-ttu-id="f5cb1-117">アプリの使用の詳細については、「 [App studio のインストール](https://aka.ms/teams-app-studio#installing-app-studio) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-117">See [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) for more information on using App Studio.</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="f5cb1-119">App Studio で、[ **マニフェストエディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-119">Once in App Studio, select the **Manifest editor** tab.</span></span>

3. <span data-ttu-id="f5cb1-120">[ **機能** ] セクションの [マニフェストエディター] ビューの左側の列で、[ **bot**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-120">In the left column of the manifest editor view in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="f5cb1-121">マニフェストエディターの右側の列にある [ **コマンド** ] セクションで、[ **追加** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-121">In the right column of the manifest editor view in the **Commands** section, select the **Add** button.</span></span>

    ![App Studio コマンドメニューの [追加] ボタン](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="f5cb1-123">[ **新しいコマンド** ] 画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-123">The **New Command** screen appears.</span></span> <span data-ttu-id="f5cb1-124">メニューコマンドとして表示する **コマンドテキスト** を入力し、メニューのコマンドテキストのすぐ下に表示する **ヘルプテキスト** を入力します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-124">Enter the **Command text** that you want to have appear as the menu command, and the **Help text** that you want to have appear directly under the command text in the menu.</span></span> <span data-ttu-id="f5cb1-125">このコマンドの目的を簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-125">This should be a brief explanation of the purpose of the command.</span></span>

6. <span data-ttu-id="f5cb1-126">次に、このコマンドメニューを表示する範囲を選択し、[ **保存** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-126">Next, select the scope(s) where you want this command menu to appear, then select the **Save** button.</span></span>

    ![App Studio コマンドメニューの [追加] ボタン](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="f5cb1-128">**Manifest.js** を編集して bot のコマンドメニューを作成する</span><span class="sxs-lookup"><span data-stu-id="f5cb1-128">Creating a command menu for your bot by editing **Manifest.json**</span></span>

<span data-ttu-id="f5cb1-129">コマンドメニューを作成するもう1つの有効な方法は、ボットソースコードを開発する際にマニフェストファイルで直接作成することです。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-129">Another valid approach for creating a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="f5cb1-130">この方法を使用する場合は、次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-130">Here are a few things to keep in mind when using this approach:</span></span>

1. <span data-ttu-id="f5cb1-131">各メニューは最大10個のコマンドをサポートします。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-131">Each menu supports up to 10 commands.</span></span>

2. <span data-ttu-id="f5cb1-132">すべてのスコープで動作する、1つのコマンドメニューを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-132">You can create a single command menu that will work in all scopes.</span></span>

3. <span data-ttu-id="f5cb1-133">各範囲に異なるコマンドメニューを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-133">You can create a different command menu for each scope</span></span>

#### <a name="manifest-example---single-menu-for-both-scopes"></a><span data-ttu-id="f5cb1-134">マニフェストの例-両方のスコープの単一のメニュー</span><span class="sxs-lookup"><span data-stu-id="f5cb1-134">Manifest example - single menu for both scopes</span></span>

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

#### <a name="manifest-example---menu-for-each-scope"></a><span data-ttu-id="f5cb1-135">各範囲のマニフェストの例-メニュー</span><span class="sxs-lookup"><span data-stu-id="f5cb1-135">Manifest example - menu for each scope</span></span>

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

## <a name="handling-menu-commands-in-your-bot-code"></a><span data-ttu-id="f5cb1-136">Bot コードでメニューコマンドを処理する</span><span class="sxs-lookup"><span data-stu-id="f5cb1-136">Handling menu commands in your bot code</span></span>

<span data-ttu-id="f5cb1-137">グループまたはチャネル内のボットは、メッセージ内で ("@botname") 指摘された場合にのみ応答します。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-137">Bots in a group or channel respond only when they are mentioned ("@botname") in a message.</span></span> <span data-ttu-id="f5cb1-138">その結果、グループまたはチャネルスコープ内で bot が受信するすべてのメッセージには、返されるメッセージテキストに独自の名前が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-138">As a result, every message received by a bot when in a group or channel scope will contain its own name in the message text returned.</span></span> <span data-ttu-id="f5cb1-139">返されるコマンドを処理する前に、メッセージの解析によって処理されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-139">You need to ensure your message parsing handles that before handling the command being returned.</span></span>

> <span data-ttu-id="f5cb1-140">**メモ** コードでコマンドを処理するために、通常のメッセージとして bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-140">**Note** For handling the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="f5cb1-141">そのため、ユーザーからの他のメッセージの場合と同じように処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-141">So you need to handle them as you would do for any other message from your users.</span></span> <span data-ttu-id="f5cb1-142">これらは単に、事前に構成されたテキストをテキストボックスに挿入する UI 処理です。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-142">They are purely a UI treatment that inserts pre-configured text into the text box.</span></span> <span data-ttu-id="f5cb1-143">その場合は、そのテキストを他のメッセージと同じように送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-143">The user must then send that text as they would do for any other message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f5cb1-144">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f5cb1-144">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f5cb1-145">メッセージテキストの **\@ メンション** 部分は、Microsoft Bot フレームワークで提供される静的メソッド (という名前のクラスのメソッド) を使用して解析でき `Activity` `RemoveRecipientMention` ます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-145">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="f5cb1-146">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f5cb1-146">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="f5cb1-147">メッセージテキストの **\@ メンション** 部分は、Microsoft Bot フレームワークで提供される静的メソッド (という名前のクラスのメソッド) を使用して解析でき `TurnContext` `removeMentionText` ます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-147">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `removeMentionText`.</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="f5cb1-148">Python</span><span class="sxs-lookup"><span data-stu-id="f5cb1-148">Python</span></span>](#tab/python)


<span data-ttu-id="f5cb1-149">メッセージテキストの **@Mention** 部分を解析するには、Microsoft Bot フレームワークで提供される静的メソッド (という名前のクラスのメソッド) を使用し `TurnContext` `remove_recipient_mention` ます。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-149">You can parse out the **@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a><span data-ttu-id="f5cb1-150">コマンドメニューのベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="f5cb1-150">Command menu best practices</span></span>

* <span data-ttu-id="f5cb1-151">**簡単にお勧め** します。 bot メニューは、ボットの主要な機能を提供することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-151">**Keep it simple**: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="f5cb1-152">**短くして** ください。メニューオプションが非常に長くて複雑な自然言語ステートメントである必要はありません。これらは単純なコマンドである必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-152">**Keep it short**: Menu options shouldn’t be extremely long and complex natural language statements — they should be simple commands.</span></span>
* <span data-ttu-id="f5cb1-153">**被呼び出しを維持** する: ボットメニューのアクション/コマンドは、会話の状態や bot があるダイアログに関係なく、常に使用可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-153">**Keep it invokable**: Bot menu actions/commands should always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> <span data-ttu-id="f5cb1-154">**メモ** マニフェストから任意のコマンドを削除する場合は、変更を有効にするためにアプリを再展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-154">**Note** If you remove any commands from your manifest, you will need to redeploy your app for the changes to take effect.</span></span> <span data-ttu-id="f5cb1-155">通常、マニフェストを変更するには、このようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5cb1-155">In general, any changes to the manifest require this.</span></span>
