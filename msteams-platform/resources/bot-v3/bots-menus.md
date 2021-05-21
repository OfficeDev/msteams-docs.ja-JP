---
title: ボット メニューの追加
description: ボットのメニューを作成する方法について説明Microsoft Teams
keywords: teams ボット メニューの作成
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: da6f36e1b7071b92f6411ab7d2afdccb795946b7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566769"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="5e266-104">[ボット] メニューを [Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5e266-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="5e266-105">検出を支援し、ボットの機能についてユーザーを教育するために、ユーザーがボットを操作するたびに表示されるメニューを追加できます。</span><span class="sxs-lookup"><span data-stu-id="5e266-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="5e266-106">メニューにはコマンド テキストが表示され、使用例やコマンドの目的の説明などのヘルプ テキストも表示されます。</span><span class="sxs-lookup"><span data-stu-id="5e266-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![ボット メニューのスクリーンショット](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="5e266-108">ユーザーがメニュー項目を選択すると、ボット メッセージのユーザー完了を支援するために、コマンド文字列がテキスト ボックスに挿入されます。</span><span class="sxs-lookup"><span data-stu-id="5e266-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="5e266-109">モバイル アプリでのボット メニュー Teamsサポート</span><span class="sxs-lookup"><span data-stu-id="5e266-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="5e266-110">ボット メニューはモバイル デバイスに表示されません。</span><span class="sxs-lookup"><span data-stu-id="5e266-110">Bot menus are not displayed on mobile devices.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="5e266-111">アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="5e266-111">App manifest</span></span>

<span data-ttu-id="5e266-112">ボット メニューを作成するには、ボット セクションの下に新 [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) しいオブジェクトをアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="5e266-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="5e266-113">ボットがサポートするスコープごとに個別のコマンドを使用して個別のメニューを宣言できます ( 、、または ) 各メニューは、最大 10 個のコマンド `personal` `groupChat` `team` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="5e266-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat`, or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="5e266-114">マニフェストの抜粋 - 両方のスコープの単一メニュー</span><span class="sxs-lookup"><span data-stu-id="5e266-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="5e266-115">マニフェストの抜粋 - スコープごとに個別のメニュー</span><span class="sxs-lookup"><span data-stu-id="5e266-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="5e266-116">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="5e266-116">Best practices</span></span>

* <span data-ttu-id="5e266-117">シンプルに保つ: ボット メニューは、ボットの主要な機能を提示することを目的とします。</span><span class="sxs-lookup"><span data-stu-id="5e266-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="5e266-118">短くしてください:メニュー オプションは、極端に長く複雑な自然言語ステートメントである必要があります。単純なコマンドである必要があります。</span><span class="sxs-lookup"><span data-stu-id="5e266-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="5e266-119">常に使用可能: ボット メニューのアクション/コマンドは、会話の状態やボットのダイアログに関係なく、常に呼び出し可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="5e266-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
