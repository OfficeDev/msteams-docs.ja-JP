---
title: ボットメニューを追加する
description: Microsoft Teamsでボットのメニューを作成する方法について説明します。
keywords: チームボットメニュー作成
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
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Microsoft Teamsでボットメニューを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットの機能を発見し、ユーザーを教育するために、ユーザーがボットとやり取りするたびに表示されるメニューを追加できるようになりました。 メニューにはコマンド テキストが表示され、使用例やコマンドの目的の説明などのヘルプ テキストも表示されます。

![ボットメニューのスクリーンショット](~/assets/images/bots/bot-menus-bot-menu-sample.png)

ユーザーがメニュー項目を選択すると、ボット メッセージのユーザーの完了を支援するために、コマンド文字列がテキスト ボックスに挿入されます。

## <a name="bot-menu-support-on-teams-mobile-app"></a>モバイル アプリでのボット メニュー Teamsサポート
> [!NOTE] 
> ボットメニューはモバイルデバイスでは表示されません。

## <a name="app-manifest"></a>アプリ マニフェスト

ボット メニューを作成するには、ボット [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) セクションのアプリ マニフェストに新しいオブジェクトを追加します。 各メニューは、ボットがサポートするスコープごとに個別のコマンドで宣言できます ( `personal` `groupChat` , 、または ) `team` 各メニューは最大 10 個のコマンドをサポートします。

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

* シンプルにする: ボットメニューは、ボットの主要な機能を示すことを目的とします。
* 短くする:メニューオプションは非常に長くて複雑な自然言語のステートメントであってはなりません - 彼らは簡単なコマンドでなければなりません。
* 常に使用可能: ボットの会話の状態や、ボットが含まれるダイアログに関係なく、ボットメニューのアクション/コマンドは常に呼び出し可能である必要があります。
