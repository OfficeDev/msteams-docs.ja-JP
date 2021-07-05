---
title: ボットのコマンド メニューを作成する
author: surbhigupta
description: カスタム ボットのコマンド メニューをMicrosoft Teamsする方法
ms.topic: how-to
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 4ee8c48b2f3b10c8924b0e81dae0a0c1f6014414
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254315"
---
# <a name="bot-command-menus"></a><span data-ttu-id="e22e4-103">ボット コマンド メニュー</span><span class="sxs-lookup"><span data-stu-id="e22e4-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="e22e4-104">ボットが応答できる一連のコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-104">To define a set of core commands that your bot can respond to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="e22e4-105">コマンドの一覧は、ボットと会話するときに、作成メッセージ領域のユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-105">The list of commands is presented to the users in the compose message area when they are in conversation with your bot.</span></span> <span data-ttu-id="e22e4-106">一覧からコマンドを選択して、コマンド文字列をメッセージ作成ボックスに挿入し、[送信] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="e22e4-106">Select a command from the list to insert the command string into the compose message box and select **Send**.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e22e4-107">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="e22e4-107">Desktop</span></span>](#tab/desktop)

![ボット コマンド メニュー](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[<span data-ttu-id="e22e4-109">モバイル</span><span class="sxs-lookup"><span data-stu-id="e22e4-109">Mobile</span></span>](#tab/mobile)

![モバイル ボットのコマンド メニュー](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="e22e4-111">ボットのコマンド メニューを作成する</span><span class="sxs-lookup"><span data-stu-id="e22e4-111">Create a command menu for your bot</span></span>

<span data-ttu-id="e22e4-112">コマンド メニューは、アプリ マニフェストで定義されます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-112">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="e22e4-113">App Studio を使用 **して作成するか** 、アプリ マニフェストに手動で追加できます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-113">You can either use **App Studio** to create them or add them manually in the app manifest.</span></span>

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="e22e4-114">App Studio を使用してボットのコマンド メニューを作成する</span><span class="sxs-lookup"><span data-stu-id="e22e4-114">Create a command menu for your bot using App Studio</span></span>

<span data-ttu-id="e22e4-115">ボットのコマンド メニューを作成するには、既存のアプリ マニフェストを編集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-115">A prerequisite to create a command menu for your bot is that you must edit an existing app manifest.</span></span> <span data-ttu-id="e22e4-116">新しいマニフェストを作成するか、既存のマニフェストを編集するかに関して、コマンド メニューを追加する手順は同じです。</span><span class="sxs-lookup"><span data-stu-id="e22e4-116">The steps to add a command menu are the same, whether you create a new manifest or edit an existing one.</span></span>

<span data-ttu-id="e22e4-117">**App Studio を使用してボットのコマンド メニューを作成するには**</span><span class="sxs-lookup"><span data-stu-id="e22e4-117">**To create a command menu for your bot using App Studio**</span></span>

1. <span data-ttu-id="e22e4-118">[アプリTeams開き、左側 **のウィンドウから**[アプリ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-118">Open Teams and select **Apps** from the left pane.</span></span> <span data-ttu-id="e22e4-119">[アプリ **] ページで** App Studio を検索 **し、[開** く] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="e22e4-119">In the **Apps** page, search for **App Studio**, and select **Open**.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="e22e4-120">App Studio をお持ち **ではない場合** は、ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-120">If you do not have **App Studio**, you can download it.</span></span> <span data-ttu-id="e22e4-121">詳細については [、「App Studio のインストール」を参照してください](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)。</span><span class="sxs-lookup"><span data-stu-id="e22e4-121">For more information, see [installing App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="e22e4-123">**App Studio で、[** マニフェスト エディター]**タブを選択** します。既存のアプリ パッケージをお持ちではない場合は、既存のアプリを作成またはインポートできます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-123">In **App Studio**, select the **Manifest editor** tab. If you do not have an existing app package, you can create or import an existing app.</span></span> <span data-ttu-id="e22e4-124">詳細については、「アプリ パッケージの [更新」を参照してください](~/get-started/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)。</span><span class="sxs-lookup"><span data-stu-id="e22e4-124">For more information, see [update an app package](~/get-started/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span></span>

3. <span data-ttu-id="e22e4-125">マニフェスト エディターの左側のウィンドウ **で** 、[機能] セクションで **[ボット** ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="e22e4-125">In the left pane of the **Manifest editor** and in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="e22e4-126">マニフェスト エディターの右側のウィンドウ **で、[コマンド** ] セクション **で、[追加** ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="e22e4-126">In the right pane of the **Manifest editor** and in the **Commands** section, select **Add**.</span></span> <span data-ttu-id="e22e4-127">[ **新しいコマンド]** 画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-127">The **New Command** screen appears.</span></span>

    ![App Studio コマンド メニュー [追加] ボタン](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="e22e4-129">ボットの **コマンド メニュー** として表示する必要がある Command テキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-129">Enter the **Command text** that must appear as the command menu for your bot.</span></span>

6. <span data-ttu-id="e22e4-130">メニューの **コマンド テキストの** 下に表示する必要があるヘルプ テキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-130">Enter the **Help text** that must appear under the command text in the menu.</span></span> <span data-ttu-id="e22e4-131">**ヘルプ テキスト** は、コマンドの目的を簡単に説明する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-131">**Help text** must be a brief explanation of the purpose of the command.</span></span>

7. <span data-ttu-id="e22e4-132">[スコープ **] チェック** ボックスをオンにして、このコマンド メニューを表示する必要がある場所を選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="e22e4-132">Select the **Scope** check boxes to select where this command menu must appear, and select **Save**.</span></span>

    ![App Studio の [新しいコマンド] メニュー ボタン](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="e22e4-134">ボットのコマンド メニューを作成するには、[オン] をManifest.jsします。</span><span class="sxs-lookup"><span data-stu-id="e22e4-134">Create a command menu for your bot by editing Manifest.json</span></span>

<span data-ttu-id="e22e4-135">コマンド メニューを作成するもう 1 つの方法は、ボットソース コードの開発中にマニフェスト ファイルに直接作成することです。</span><span class="sxs-lookup"><span data-stu-id="e22e4-135">Another way to create a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="e22e4-136">このメソッドを使用するには、次の点に従います。</span><span class="sxs-lookup"><span data-stu-id="e22e4-136">To use this method, follow these points:</span></span>

* <span data-ttu-id="e22e4-137">各メニューは、最大 10 個のコマンドをサポートします。</span><span class="sxs-lookup"><span data-stu-id="e22e4-137">Each menu supports up to ten commands.</span></span>
* <span data-ttu-id="e22e4-138">すべてのスコープで機能する 1 つのコマンド メニューを作成します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-138">Create a single command menu that works in all scopes.</span></span>
* <span data-ttu-id="e22e4-139">スコープごとに異なるコマンド メニューを作成します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-139">Create a different command menu for each scope.</span></span>

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a><span data-ttu-id="e22e4-140">両方のスコープの単一メニューのマニフェスト例</span><span class="sxs-lookup"><span data-stu-id="e22e4-140">Manifest example for single menu for both scopes</span></span>

<span data-ttu-id="e22e4-141">両方のスコープの単一メニューのマニフェストのコード例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e22e4-141">The manifest example code for single menu for both scopes is as follows:</span></span>

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a><span data-ttu-id="e22e4-142">各スコープのメニューのマニフェスト例</span><span class="sxs-lookup"><span data-stu-id="e22e4-142">Manifest example for the menu for each scope</span></span>

<span data-ttu-id="e22e4-143">各スコープのメニューのマニフェストのコード例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e22e4-143">The manifest example code for the menu for each scope is as follows:</span></span>

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

<span data-ttu-id="e22e4-144">ユーザーからのメッセージを処理する場合は、ボット コードでメニュー コマンドを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-144">You must handle menu commands in your bot code as you handle any message from users.</span></span> <span data-ttu-id="e22e4-145">メッセージ テキストのメンション部分を解析することで、ボット コード内の **\@ メニュー** コマンドを処理できます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-145">You can handle menu commands in your bot code by parsing out the **\@Mention** portion of the message text.</span></span>

## <a name="handle-menu-commands-in-your-bot-code"></a><span data-ttu-id="e22e4-146">ボット コードでメニュー コマンドを処理する</span><span class="sxs-lookup"><span data-stu-id="e22e4-146">Handle menu commands in your bot code</span></span>

<span data-ttu-id="e22e4-147">グループまたはチャネル内のボットは、メッセージに記載されている場合 `@botname` にのみ応答します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-147">Bots in a group or channel respond only when they are mentioned `@botname` in a message.</span></span> <span data-ttu-id="e22e4-148">グループスコープまたはチャネル スコープ内でボットが受信したメッセージには、返されるメッセージ テキストに名前が含まれるすべてのメッセージが含まれる。</span><span class="sxs-lookup"><span data-stu-id="e22e4-148">Every message received by a bot when in a group or channel scope contains its name in the message text returned.</span></span> <span data-ttu-id="e22e4-149">返されるコマンドを処理する前に、メッセージ解析でボットが受信したメッセージの名前を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-149">Before handling the command being returned, your message parsing must handle the message received by a bot with its name.</span></span>

> [!NOTE]
> <span data-ttu-id="e22e4-150">コード内のコマンドを処理するために、通常のメッセージとしてボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-150">To handle the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="e22e4-151">ユーザーからの他のメッセージを処理する場合と同じ方法で処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-151">You must handle them as you would handle any other message from your users.</span></span> <span data-ttu-id="e22e4-152">コード内のコマンドは、あらかじめ構成されたテキストをテキスト ボックスに挿入します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-152">The commands in code insert pre-configured text into the text box.</span></span> <span data-ttu-id="e22e4-153">その後、ユーザーはそのテキストを他のメッセージと同じ方法で送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-153">The user must then send that text as they do for any other message.</span></span>

# <a name="c"></a>[<span data-ttu-id="e22e4-154">C#</span><span class="sxs-lookup"><span data-stu-id="e22e4-154">C#</span></span>](#tab/dotnet)

<span data-ttu-id="e22e4-155">メッセージ テキストの **\@ メンション部分** を解析するには、メッセージ テキストに用意されている静的メソッドをMicrosoft Bot Framework。</span><span class="sxs-lookup"><span data-stu-id="e22e4-155">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework.</span></span> <span data-ttu-id="e22e4-156">という名前のクラス `Activity` のメソッドです `RemoveRecipientMention` 。</span><span class="sxs-lookup"><span data-stu-id="e22e4-156">It is a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

<span data-ttu-id="e22e4-157">メッセージ C#メンション部分を解析するコード **\@** は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e22e4-157">The C# code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[<span data-ttu-id="e22e4-158">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e22e4-158">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="e22e4-159">ボット フレームワークで提供される **\@ 静的** メソッドを使用して、メッセージ テキストのメンション部分を解析できます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-159">You can parse out the **\@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="e22e4-160">という名前のクラス `TurnContext` のメソッドです `removeMentionText` 。</span><span class="sxs-lookup"><span data-stu-id="e22e4-160">It is a method of the `TurnContext` class named `removeMentionText`.</span></span>

<span data-ttu-id="e22e4-161">メッセージ テキストのメンション部分を解析する **\@ JavaScript** コードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e22e4-161">The JavaScript code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="e22e4-162">Python</span><span class="sxs-lookup"><span data-stu-id="e22e4-162">Python</span></span>](#tab/python)

<span data-ttu-id="e22e4-163">ボット フレームワークで提供される **静的@Mention** を使用して、メッセージ テキストの一部を解析できます。</span><span class="sxs-lookup"><span data-stu-id="e22e4-163">You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="e22e4-164">という名前のクラス `TurnContext` のメソッドです `remove_recipient_mention` 。</span><span class="sxs-lookup"><span data-stu-id="e22e4-164">It is a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

<span data-ttu-id="e22e4-165">メッセージ テキストの Mention 部分を解析する **\@ Python** コードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e22e4-165">The Python code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

<span data-ttu-id="e22e4-166">ボット コードの円滑な機能を有効にするには、従う必要があるベスト プラクティスがいくつかある。</span><span class="sxs-lookup"><span data-stu-id="e22e4-166">To enable smooth functioning of your bot code, there are few best practices that you must follow.</span></span>

## <a name="command-menu-best-practices"></a><span data-ttu-id="e22e4-167">コマンド メニューのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="e22e4-167">Command menu best practices</span></span>

<span data-ttu-id="e22e4-168">コマンド メニューのベスト プラクティスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="e22e4-168">Following are the command menu best practices:</span></span>

* <span data-ttu-id="e22e4-169">シンプルに保つ: ボット メニューは、ボットの主要な機能を提示することを目的とします。</span><span class="sxs-lookup"><span data-stu-id="e22e4-169">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="e22e4-170">短くしてください:メニュー オプションは長くする必要があります。また、複雑な自然言語ステートメントで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-170">Keep it short: Menu options must not be long and must not be complex natural language statements.</span></span> <span data-ttu-id="e22e4-171">単純なコマンドである必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-171">They must be simple commands.</span></span>
* <span data-ttu-id="e22e4-172">呼び出し可能な状態を維持する: ボット メニューの操作またはコマンドは、会話の状態やボットが含むダイアログに関係なく、常に使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-172">Keep it invokable: Bot menu actions or commands must always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> [!NOTE]
> <span data-ttu-id="e22e4-173">マニフェストからコマンドを削除する場合は、変更を実装するためにアプリを再展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-173">If you remove any commands from your manifest, you must redeploy your app to implement the changes.</span></span> <span data-ttu-id="e22e4-174">一般に、マニフェストに対する変更を行う場合は、アプリを再展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22e4-174">In general, any changes to the manifest require you to redeploy your app.</span></span>

## <a name="next-step"></a><span data-ttu-id="e22e4-175">次の手順</span><span class="sxs-lookup"><span data-stu-id="e22e4-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e22e4-176">チャネルとグループ会話</span><span class="sxs-lookup"><span data-stu-id="e22e4-176">Channel and group conversations</span></span>](~/bots/how-to/conversations/channel-and-group-conversations.md)
