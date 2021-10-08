---
title: 最新のビュー
description: ユニバーサル ボットを使用した最新のビューのサンプル
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 96f87f8795fdd2fed2276b2d67e58d1c394b05f6
ms.sourcegitcommit: d0f1333d5dc5aede963dc59cfb1c2eca70aaf521
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2021
ms.locfileid: "60238238"
---
# <a name="up-to-date-cards"></a>最新のカード

アダプティブ カードでユーザーに最新情報を提供できます。 更新とメッセージの編集を組み合わせて、Teams。 サービスに変更がある場合と同様に、ユーザー固有のビューを最新の状態に動的に更新します。 たとえば、プロジェクト管理カードやチケット カードの場合は、コメントとタスクの状態を更新します。 承認の場合、最新の状態が反映され、区別された情報とアクションも提供されます。

たとえば、ユーザーは、スレッド内にアセット承認要求をTeamsできます。 Alex は承認要求を作成し、それを Megan と Nestor に割り当てる。 承認要求を作成する 2 つの部分を次に示します。

* アダプティブ カードのプロパティを使用して、ユーザー `refresh` 固有のビューを適用できます。
ユーザー固有のビューを使用すると、一連のユーザーに [承認] または [拒否] ボタンを含むカードを表示し、他のユーザーにこれらのボタンのないカードを表示できます。

* カードの状態を常に更新するには、Teams編集メカニズムを使用できます。 たとえば、承認ごとにボットは、すべてのユーザーに対してメッセージの編集をトリガーできます。 このボット メッセージの編集は、更新されたユーザー固有のカードでボットが応答できる、すべての自動更新ユーザーに対する呼び出し `adaptiveCard/action` 要求をトリガーします。

詳細については、「ボット メッセージの [編集方法」を参照してください](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)。

## <a name="approval-base-card"></a>承認ベース カード

次のコードは、承認ベース カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a>[承認] ボタンと [拒否] ボタンを含む承認カード

次のコードは、[承認] ボタンと [拒否] ボタンを含 **む承認** カード **の例を** 示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

承認要求に応じてユーザーに表示される 2 つの役割を次に示します。

* 承認基本カード: 承認者リストの一部ではなく、要求がまだ承認または拒否されていないユーザーに表示され、アダプティブ カード JSON のプロパティのリストの一部 `userIds` `refresh` ではありません。
* [承認] または **[** 拒否] ボタンを持つ承認カード: 承認者リストの一部であるユーザーとアダプティブ カード JSON のプロパティの一覧 `userIds` `refresh` に表示されます。

**資産承認要求を送信するには**

1. Alex は、スレッド内で資産承認要求をTeamsし、それを Megan と Nestor に割り当てる。
2. ボットは、会話で承認ベース カードを送信します。
3. 会話内の他のすべてのユーザーには、ボットから送信されたカードが表示されます。 Megan と Nestor で自動更新がトリガーされ、アダプティブ カードのプロパティの一覧にユーザーの MRIs が追加されると、[承認] ボタンまたは [拒否] ボタンが表示されるユーザー固有のカードが表示されます。 `userIds` `refresh`

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="ユーザー固有のビュー":::

4. Nestor は [承認]**ボタンを選択** します。 `Action.Execute` ボットは、応答 `adaptiveCard/action` でアダプティブ カードを返す呼び出し要求を取得します。
5. ボットは、更新されたカードでメッセージ編集をトリガーします。これは、Megan の承認が保留されている間に Nestor が要求を承認したとします。
6. ボット メッセージの編集では、Megan の自動更新がトリガーされ、更新されたユーザー固有のカードが表示され、Nestor は要求を承認しましたが、[承認]または[拒否] ボタンも表示されます。 Nestor のユーザーの MRI は、手順 4 と 5 のこのアダプティブ カード JSON のプロパティのリストから `userIds` `refresh` 削除されます。 これで、自動更新は Megan でのみトリガーされます。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="最新のユーザー固有のビュー":::

7. これで、Megan は [承認] **ボタンを選択** します。このボタンの電源 `Action.Execute` は . ボットは、応答 `adaptiveCard/action` でアダプティブ カードを返す呼び出し要求を取得します。
8. ボットは、更新されたカードを使用してメッセージ編集をトリガーします。このカードでは、Nestor と Megan が要求を承認しました。
9. ボット メッセージの編集では、自動更新はトリガーされません。 Megan のユーザーの MRI は、手順 7 と 8 のこのアダプティブ カード JSON のプロパティのリストから `userIds` `refresh` 削除されます。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="最新のビュー":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>アダプティブ カードの応答として送信 `adaptiveCard/action` され、 `message edit`

次のコードは、手順 4 と 5 の応答として送信されるアダプティブ カードの `adaptiveCard/action` `message edit` 例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

次のコードは、手順 6 の自動更新を介して呼び出しの応答として送信されるアダプティブ `adaptiveCard/action` カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

次のコードは、手順 7 と 8 の応答として送信されるアダプティブ `adaptiveCard/action` `message edit` カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| シーケンシャル ワークフローアダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [ユーザー固有のビュー](User-Specific-Views.md)
