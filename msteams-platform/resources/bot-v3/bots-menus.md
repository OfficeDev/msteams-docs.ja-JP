---
title: Bot メニューを追加する
description: Microsoft Teams でボットのメニューを作成する方法について説明します。
keywords: teams の bot メニューの作成
ms.date: 05/20/2019
ms.openlocfilehash: 36a224dc21cccc5fcd1047e45e3d749e7ca19ea7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674662"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="96222-104">Microsoft Teams で bot メニューを追加する</span><span class="sxs-lookup"><span data-stu-id="96222-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="96222-105">ユーザーが bot との対話を行うときに、検出を支援し、ユーザーに bot の機能について理解を助けるために、メニューを追加できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="96222-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="96222-106">メニューにはコマンドテキストが表示され、使用例やコマンドの目的の説明などのヘルプテキストも表示されます。</span><span class="sxs-lookup"><span data-stu-id="96222-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Bot メニューのスクリーンショット](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="96222-108">ユーザーがメニュー項目を選択すると、そのコマンド文字列がテキストボックスに挿入されて、bot メッセージのユーザーの入力を助けることができます。</span><span class="sxs-lookup"><span data-stu-id="96222-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="96222-109">Teams モバイルアプリでの Bot メニューのサポート</span><span class="sxs-lookup"><span data-stu-id="96222-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="96222-110">モバイルデバイスに Bot メニューが表示されない</span><span class="sxs-lookup"><span data-stu-id="96222-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="96222-111">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="96222-111">App manifest</span></span>

<span data-ttu-id="96222-112">Bot メニューを作成するには、アプリ[`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists)マニフェストの bot セクションの下に新しいオブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="96222-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="96222-113">各メニューでは、`personal` `groupChat`各メニューで最大10個のコマンドをサポートして`team`います (または)。</span><span class="sxs-lookup"><span data-stu-id="96222-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="96222-114">マニフェストの抜粋-両方のスコープの単一メニュー</span><span class="sxs-lookup"><span data-stu-id="96222-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="96222-115">マニフェストの抜粋-スコープごとに個別のメニュー</span><span class="sxs-lookup"><span data-stu-id="96222-115">Manifest excerpt - separate menu per scope</span></span>

```json
{
  ...
  "bots":[
    {
      "botId":"[Microsoft app ID for your bot]",
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

## <a name="best-practices"></a><span data-ttu-id="96222-116">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="96222-116">Best practices</span></span>

* <span data-ttu-id="96222-117">簡単にお勧めします。 bot メニューは、ボットの主要な機能を提供することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="96222-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="96222-118">短くしてください。メニューオプションが非常に長くて複雑な自然言語ステートメントである必要はありません。これらは単純なコマンドである必要があります。</span><span class="sxs-lookup"><span data-stu-id="96222-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="96222-119">常に利用可能: ボットメニューアクション/コマンドは、会話の状態や bot が配置されているダイアログに関係なく、常に被呼び出し可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="96222-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
