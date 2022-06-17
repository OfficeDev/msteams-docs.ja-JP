---
title: 最新のビュー
description: このモジュールでは、ユニバーサル ボットとコード サンプルを使用した最新のカード ビューについてMicrosoft Teams
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5c6f7d13cd884baf9ffbc1fd30cafb7cfab33295
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143621"
---
# <a name="up-to-date-cards"></a>最新のカード

アダプティブ カードでユーザーに最新の情報を提供できるようになりました。 Teamsに更新とメッセージの編集の組み合わせを含めます。 サービスに変更がある場合と同様に、ユーザー固有のビューを最新の状態に動的に更新します。 たとえば、プロジェクト管理カードやチケット カードの場合は、コメントとタスクの状態を更新します。 承認の場合は、最新の状態が反映され、差別化された情報とアクションも提供されます。

たとえば、ユーザーはTeams会話で資産承認要求を作成できます。 Alex は承認要求を作成し、Megan と Nestor に割り当てます。 承認要求を作成する 2 つの部分を次に示します。

* アダプティブ カードのプロパティを使用して、 `refresh` ユーザー固有のビューを適用できます。
ユーザー固有のビューを使用すると、 **承認** ボタンまたは **拒否** ボタンを持つカードを一連のユーザーに表示し、これらのボタンのないカードを他のユーザーに表示できます。

* カードの状態を常に更新し続けるために、Teamsメッセージ編集メカニズムを使用できます。 たとえば、すべての承認について、ボットはすべてのユーザーに対してメッセージ編集をトリガーできます。 このボット メッセージ編集により、すべての自動更新ユーザーに対する `adaptiveCard/action` 呼び出し要求がトリガーされ、更新されたユーザー固有のカードでボットが応答できるようになります。

詳細については、 [ボット メッセージの編集を行う方法に関する](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)説明を参照してください。

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

## <a name="approval-card-with-approve-and-reject-buttons"></a>[承認] ボタンと [拒否] ボタンが付いた承認カード

次のコードは、[ **承認** ] ボタンと [ **拒否]** ボタンを含む承認カードの例を示しています。

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

承認要求に応じてユーザーに表示される 2 つのロールを次に示します。

* 承認ベース カード: 承認者リストの一部ではなく、要求がまだ承認または拒否されておらず、アダプティブ カード JSON のプロパティの`userIds``refresh`リストに含まれていないユーザーに表示されます。
* **[承認**] または **[拒否]** ボタンが付いた承認カード: 承認者リストの一部であるユーザーと`userIds`、アダプティブ カード JSON のプロパティの`refresh`一覧に表示されます。

資産承認要求を送信するには:

1. Alex は、Teams会話で資産承認要求を発生させ、Megan と Nestor に割り当てます。
2. ボットは、会話内の承認ベース カードを送信します。
3. 会話内の他のすべてのユーザーには、ボットによって送信されたカードが表示されます。 Megan と Nestor に対して自動更新がトリガーされ、アダプティブ カードのプロパティの一覧`refresh`にユーザーの MRI が追加`userIds`されると、[**承認****] または [拒否]** ボタンを持つユーザー固有のカードが表示されるようになりました。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="ユーザー固有のビュー":::

4. Nestor が [ **承認** ] ボタンを選択します。このボタンは `Action.Execute`、 . ボットは、応答で `adaptiveCard/action` アダプティブ カードを返すことができる呼び出し要求を取得します。
5. ボットは、更新されたカードでメッセージの編集をトリガーします。これは、Megan の承認が保留されている間に Nestor が要求を承認したことを示します。
6. ボット メッセージの編集によって Megan の自動更新がトリガーされ、更新されたユーザー固有のカードが表示されます。これは、Nestor が要求を承認したが、[ **承認** ] ボタンまたは **[拒否]** ボタンも表示されます。 Nestor のユーザーの MRI は、手順 4 と 5 で`refresh`、このアダプティブ カード JSON のプロパティの一覧から`userIds`削除されます。 ここで、自動更新は Megan に対してのみトリガーされます。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="最新のユーザー固有ビュー":::

7. これで、Megan は **[承認** ] ボタンを選択します。このボタンには `Action.Execute`、 . ボットは、応答で `adaptiveCard/action` アダプティブ カードを返すことができる呼び出し要求を取得します。
8. ボットは、Nestor と Megan が要求を承認したことを示す、更新されたカードでメッセージの編集をトリガーします。
9. ボット メッセージの編集では、自動更新はトリガーされません。 Megan のユーザーの MRI は、手順 7 と手順 8 で`refresh`、このアダプティブ カード JSON のプロパティの一覧から`userIds`削除されます。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="最新のビュー":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>の応答 `adaptiveCard/action` として送信されたアダプティブ カード `message edit`

次のコードは、手順 4 と手順 5 の応答として送信されるアダプティブ カードの`adaptiveCard/action``message edit`例を示しています。

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

次のコードは、手順 6 の自動更新を介して呼び出しの応答として送信されるアダプティブ カードの `adaptiveCard/action` 例を示しています。

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

次のコードは、手順 7 と手順 8 の応答として送信されるアダプティブ カードの`adaptiveCard/action``message edit`例を示しています。

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
| シーケンシャル ワークフロー アダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [ユーザー固有のビュー](User-Specific-Views.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
