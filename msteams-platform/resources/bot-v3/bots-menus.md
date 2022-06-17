---
title: ボット メニューを追加する
description: このモジュールでは、Microsoft Teamsにボット メニューを追加し、Microsoft Teamsでボットのメニューを作成する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: ed65699b930d3e5334dd7fbb03da18a1482d6e5d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143383"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Microsoft Teamsでボット メニューを追加する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

検出を支援し、ボットの機能についてユーザーを教育するために、ユーザーがボットと対話するたびに表示されるメニューを追加できるようになりました。 メニューにはコマンド テキストが表示され、使用例やコマンドの目的の説明などのヘルプ テキストも提供されます。

![ボット メニューのスクリーンショット](~/assets/images/bots/bot-menus-bot-menu-sample.png)

ユーザーがメニュー項目を選択すると、コマンド文字列がテキスト ボックスに挿入され、ユーザーがボット メッセージを入力できるようにします。

## <a name="bot-menu-support-on-teams-mobile-app"></a>モバイル アプリでのボット メニューのサポートTeams

> [!NOTE]
> モバイル デバイスでは、ボット メニューは表示されません。

## <a name="app-manifest"></a>アプリ マニフェスト

ボット メニューを作成するには、ボット セクションの下のアプリ マニフェストに新しい [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) オブジェクトを追加します。 ボットがサポートするスコープ (または `team`) ごとに個別のコマンドを使用して個々のメニューを宣言できます。`personal``groupChat`各メニューでは、最大 10 個のコマンドをサポートします。

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

* シンプルに保つ: ボット メニューは、ボットの主要な機能を示す意味があります。
* 簡単に説明します。メニュー オプションは、非常に長く複雑な自然言語ステートメントにしないでください。単純なコマンドである必要があります。
* 常に使用可能: ボットメニューのアクション/コマンドは、会話の状態やボットが配置されているダイアログに関係なく、常に呼び出し可能である必要があります。
