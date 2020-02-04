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
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Microsoft Teams で bot メニューを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ユーザーが bot との対話を行うときに、検出を支援し、ユーザーに bot の機能について理解を助けるために、メニューを追加できるようになりました。 メニューにはコマンドテキストが表示され、使用例やコマンドの目的の説明などのヘルプテキストも表示されます。

![Bot メニューのスクリーンショット](~/assets/images/bots/bot-menus-bot-menu-sample.png)

ユーザーがメニュー項目を選択すると、そのコマンド文字列がテキストボックスに挿入されて、bot メッセージのユーザーの入力を助けることができます。

## <a name="bot-menu-support-on-teams-mobile-app"></a>Teams モバイルアプリでの Bot メニューのサポート
> [!NOTE] 
> モバイルデバイスに Bot メニューが表示されない

## <a name="app-manifest"></a>アプリマニフェスト

Bot メニューを作成するには、アプリ[`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists)マニフェストの bot セクションの下に新しいオブジェクトを追加します。 各メニューでは、`personal` `groupChat`各メニューで最大10個のコマンドをサポートして`team`います (または)。

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>マニフェストの抜粋-両方のスコープの単一メニュー

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>マニフェストの抜粋-スコープごとに個別のメニュー

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

## <a name="best-practices"></a>ベスト プラクティス

* 簡単にお勧めします。 bot メニューは、ボットの主要な機能を提供することを目的としています。
* 短くしてください。メニューオプションが非常に長くて複雑な自然言語ステートメントである必要はありません。これらは単純なコマンドである必要があります。
* 常に利用可能: ボットメニューアクション/コマンドは、会話の状態や bot が配置されているダイアログに関係なく、常に被呼び出し可能にする必要があります。
