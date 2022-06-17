---
title: ユーザー固有のビュー
description: このモジュールでは、コード サンプルと adaptiveCard/action invoke response card を使用したユニバーサル アクションを使用したユーザー固有のビューについて説明します
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: a3fdc937ba1528a2bf9aa304bf484bbcae68b5c6
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143922"
---
# <a name="user-specific-views"></a>ユーザー固有のビュー

以前、アダプティブ カードがTeams会話で送信された場合、すべてのユーザーにまったく同じカード コンテンツが表示されます。 ユニバーサル アクション モデルと `refresh` アダプティブ カードの導入により、ボット開発者はアダプティブ カードのユーザー固有のビューをユーザーに提供できるようになりました。 同じアダプティブ カードをユーザー固有のアダプティブ カードに更新できるようになりました。 アダプティブ カードは、承認、投票作成者コントロール、チケット発行、インシデント管理、プロジェクト管理カードなどの強力なシナリオを提供します。

> [!NOTE]
>
> * ユーザー固有のビューは、ボットによって送信されるアダプティブ カードでサポートされ、ユニバーサル アクションに依存します。
> * 最大 60 人の異なるユーザーが、追加情報やアクションを含む異なるバージョンのカードを表示できます。

たとえば、Contoso の安全検査員である Megan は、インシデントを作成し、それを Alex に割り当てたいと考えています。 また、Megan は、チーム内のすべてのユーザーにインシデントについて認識してもらいたいと考えています。 Megan では、アダプティブ カード用のユニバーサル アクションを搭載した Contoso インシデント レポート メッセージ拡張機能を使用します。

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="モバイル ユーザー固有のビュー" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>アダプティブ カードのユーザー固有のビュー

次のコードは、アダプティブ カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
            "refresh info": "<refresh info>"
      }
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

アダプティブ カードを送信するには、ユーザー固有のビューを更新し、ボットに要求を呼び出します。

1. Megan が新しいインシデントを作成すると、ボットは、Teams会話にインシデントの詳細を含むアダプティブ カードまたは共通カードを送信します。
2. このカードは、Megan と Alex のユーザー固有のビューに自動的に更新されます。 Alex と Megan のユーザー MRI は、Adaptive Card JSON の`refresh`プロパティに追加`userIds`されます。 このカードは、会話内の他のユーザーと同じままです。
3. Megan の場合、自動更新によって `adaptiveCard/action` ボットへの呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答として、ボタンを含む `Edit` インシデント作成者カードを返すことができます。
4. Alex の場合と同様に、自動更新によってボットに対する別 `adaptiveCard/action` の呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答としてインシデント所有者カード `Resolve` ボタンを返すことができます。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>クライアントからボットに送信された要求Teams呼び出す

次のコードは、Alex と Megan のTeams クライアントからボットに送信される呼び出し要求の例を示しています。

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action invoke response card

次のコードは、Megan の adaptiveCard/action invoke 応答カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action invoke response card for Alex

次のコードは、Alex の adaptiveCard/action invoke 応答カードの例を示しています。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>アダプティブ カードを返す応答を呼び出す

次のコードは、アダプティブ カードを返す呼び出し応答の例を示しています。

### <a name="c"></a>[C#](#tab/C)

```csharp
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
var card = "<adaptive card json>";
 
const cardRes = {
        statusCode: 200,
        type: 'application/vnd.microsoft.card.adaptive',
        value: card
    };
    const res = {
        status: 200,
        body: cardRes
    };
    return res;

```

***

次の一覧では、ユーザー固有のビューのカード設計ガイドラインを示します。

* 更新動作: スレッドに送信された特定のカードに対して、プロパティでユーザー固有のビューを指定することで、最大 60 個のユーザー固有ビューを`userIds``Refresh`作成できます。

  * このフィールドが`userIds`プロパティに`Refresh`指定されていない場合、Teams クライアントは、会話に 60 人以下のメンバーがいる場合、すべてのユーザーの更新を自動的にトリガーできます。

  * ユーザーがカードの更新を手動でトリガーするには、メッセージ オプション メニューから **[更新** ] を選択できます。 これは、会話内のメンバーが 60 人未満の場合、または会話に 60 人以下のユーザーがいる場合にリストに `userIds` 指定されていないユーザーのセットに対して発生します。

* 基本カード: ボットはメッセージを送信します。このメッセージには、カードの基本バージョンが埋め込まれています。 会話のすべてのメンバーは、同じ内容を表示できます。 ボットは、その後、セクションで指定したユーザーの更新を通じてユーザー固有のカードを `userIds` フェッチします。

* 更新タイムアウト: Teams クライアントは、更新を介して、または **[実行**] を選択して、2 つの方法で **更新** をトリガーします。 更新は、最後の呼び出しのカードが 1 分より前の場合にのみトリガーされます。 更新されたカードを送信する前に、データ バッグにタイムスタンプを追加して確認することで、更新動作を制御できます。

* メッセージの更新を使用して、ベース カードを更新し、同時にユーザー固有のカードを更新できます。 チャットまたはチャネルを開くと、更新が有効になっているユーザーのカードも **更新** されます。

* ユーザーがアクションのビューに切り替える大規模なグループを使用するシナリオでは、レスポンダーの動的な更新が必要な場合は、最大 60 人のユーザーを `userIds` リストに追加し続けることができます。 61 番目のユーザーが応答したときに、最初のレスポンダーをリストから削除できます。 リストから削除されたユーザーには、最新の結果を `userIds` 取得するための手動 **の更新** を指定できます。

* ユーザー固有のビューを取得するようにユーザーに求めるメッセージを表示します。このビューには、カードまたは一部のアクションの特定のビューのみが表示されます。

> [!NOTE]
> ボットから返されたユーザー固有のカードは、そのカードを要求した特定のクライアントにのみ送信されます。 たとえば、ユーザーがデスクトップからモバイルなどの別のクライアントに切り替えた場合、更新されたカードをフェッチするために別の呼び出しイベントがトリガーされます。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| シーケンシャル ワークフロー アダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新のビュー](Up-To-Date-Views.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
