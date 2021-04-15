---
title: ボット メニューの追加
description: Microsoft Teams でボットのメニューを作成する方法について説明します。
keywords: teams ボット メニューの作成
ms.topic: how-to
ms.date: 05/20/2019
ms.openlocfilehash: 3623d85c1531b9942633af940c5e41ac1c574441
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696144"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Microsoft Teams でボット メニューを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

検出を支援し、ボットの機能についてユーザーを教育するために、ユーザーがボットを操作するたびに表示されるメニューを追加できます。 メニューにはコマンド テキストが表示され、使用例やコマンドの目的の説明などのヘルプ テキストも表示されます。

![ボット メニューのスクリーンショット](~/assets/images/bots/bot-menus-bot-menu-sample.png)

ユーザーがメニュー項目を選択すると、ボット メッセージのユーザー完了を支援するために、コマンド文字列がテキスト ボックスに挿入されます。

## <a name="bot-menu-support-on-teams-mobile-app"></a>Teams モバイル アプリでのボット メニューのサポート
> [!NOTE] 
> ボット メニューがモバイル デバイスに表示されない

## <a name="app-manifest"></a>アプリ マニフェスト

ボット メニューを作成するには、ボット セクションの下に新 [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) しいオブジェクトをアプリ マニフェストに追加します。 ボットがサポートするスコープごとに個別のコマンドを使用して個別のメニューを宣言できます (または) 各メニューは、最大 10 個のコマンド `personal` `groupChat` `team` をサポートします。

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>マニフェストの抜粋 - 両方のスコープの単一メニュー

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>マニフェストの抜粋 - スコープごとに個別のメニュー

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

* シンプルに保つ: ボット メニューは、ボットの主要な機能を提示することを目的とします。
* 短くしてください:メニュー オプションは、極端に長く複雑な自然言語ステートメントである必要があります。単純なコマンドである必要があります。
* 常に使用可能: ボット メニューのアクション/コマンドは、会話の状態やボットのダイアログに関係なく、常に呼び出し可能である必要があります。
