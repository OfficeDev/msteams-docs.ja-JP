---
title: ユーザー固有のビュー
description: ユニバーサル アクションを使用したユーザー固有のビューのサンプル
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 696fc5ce25c79d749b301309bfe0c737e39ad294
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555445"
---
# <a name="user-specific-views"></a>ユーザー固有のビュー

以前は、アダプティブ カードがスレッド内で送信Teams、すべてのユーザーにまったく同じカード コンテンツが表示されます。 ユニバーサル アクション モデルとアダプティブ カードの導入により、ボット開発者はアダプティブ カードのユーザー固有のビューをユーザーに `refresh` 提供できます。 同じアダプティブ カードをユーザー固有のアダプティブ カードに更新できます。

たとえば、Contoso の安全検査官である Megan は、インシデントを作成して Alex に割り当てる必要があります。 また、チーム内のすべてのユーザーがインシデントを認識する必要があります。 Megan は、アダプティブ カードのユニバーサル アクションを利用した Contoso インシデント レポート メッセージ拡張機能を使用します。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー":::

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

**アダプティブ カードを送信するには、ユーザー固有のビューを更新し、ボットに要求を呼び出します。**

1. Megan が新しいインシデントを作成すると、ボットはアダプティブ カードまたは共通カードにインシデントの詳細を送信Teamsします。
2. これで、このカードは、Megan と Alex のユーザー固有のビューに自動的に更新されます。 Alex と Megan のユーザー MRIs は、アダプティブ カード JSON のプロパティ `userIds` `refresh` のプロパティに追加されます。 カードは、会話内の他のユーザーに対して同じままです。
3. Megan の場合、自動更新によってボットへの `adaptiveCard/action` 呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答として、ボタン付 `Edit` きインシデント作成者カードを返します。
4. Alex の場合と同様に、自動更新によってボットに対 `adaptiveCard/action` する別の呼び出し要求がトリガーされます。 ボットは、この呼び出し要求に対する応答として `Resolve` インシデント所有者カード ボタンを返します。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>クライアントからボットにTeams要求を呼び出す

次のコードは、Alex と Megan のクライアントからボットに送信される呼び出しTeams例を示しています。

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

次のコードは、Megan のアダプティブ カード/アクション呼び出し応答カードの例を示しています。

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

次のコードは、Alex のアダプティブ カード/アクション呼び出し応答カードの例を示しています。

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

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

ユーザー固有のビューを設計する際に注意するカード設計ガイドライン:

* セクションで指定することで、チャットまたはチャネルに送信される特定のカードに対して最大 **60** のユーザー固有のビュー `userIds` を作成 `refresh` できます。
* **基本カード:** ボット開発者がチャットに送信するカードの基本バージョン。 これは、セクションで指定されていないすべてのユーザーのアダプティブ カードのバージョン `userIds` です。
* メッセージの更新または編集を使用して、基本カードを更新し、同時にユーザー固有のカードを更新できます。

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新のビュー](Up-To-Date-Views.md)
