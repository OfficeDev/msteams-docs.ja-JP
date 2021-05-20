---
title: ユーザー固有のビュー
description: ユニバーサル アクションを使用したユーザー固有ビューのサンプル
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

以前は、Teams会話でアダプティブ カードが送信された場合、すべてのユーザーにまったく同じカード コンテンツが表示されます。 ユニバーサルアクションモデルと `refresh` アダプティブカードの導入により、ボット開発者はユーザーにアダプティブカードのユーザ固有のビューを提供できるようになりました。 同じアダプティブ カードをユーザー固有のアダプティブ カードに更新できるようになりました。

たとえば、Contoso 社の安全検査官である Megan は、インシデントを作成して Alex に割り当てる必要があります。 彼女はまた、チームの全員に事件について気づいてもらいたいと考えています。 Megan は、アダプティブ カードのユニバーサル アクションを使用して、Contoso インシデント レポート メッセージ拡張機能を使用します。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー":::

## <a name="user-specific-views-for-adaptive-cards"></a>アダプティブ カードのユーザ固有のビュー

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

**アダプティブ カードを送信し、ユーザー固有のビューを更新し、ボットに要求を呼び出すには**

1. Megan が新しいインシデントを作成すると、ボットは、Teams会話でインシデントの詳細を含むアダプティブ カードまたは共通カードを送信します。
2. これで、このカードは、Megan と Alex のユーザー固有ビューに自動的に更新されます。 アレックスとメーガンのユーザーMRIは、 `userIds` `refresh` アダプティブカードJSONのプロパティのプロパティに追加されます。 カードは、会話内の他のユーザーに対して同じままです。
3. Megan の場合、自動更新は `adaptiveCard/action` ボットへの呼び出し要求をトリガーします。 ボットは、 `Edit` この呼び出し要求への応答として、ボタン付きのインシデント作成者カードを返すことができます。
4. 同様に、Alexの場合も、自動リフレッシュによって `adaptiveCard/action` ボットに対する別の呼び出し要求がトリガーされます。 ボットは、 `Resolve` この呼び出し要求への応答としてインシデント所有者カード ボタンを返すことができます。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>クライアントからボットに送信Teams要求を呼び出す

次のコードは、Alex と Megan のTeamsクライアントからボットに送信される呼び出し要求の例を示しています。

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

## <a name="adaptivecardaction-invoke-response-card"></a>アダプティブカード/アクション呼び出し応答カード

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>アダプティブカード/アクション呼び出し応答カードアレックス

次のコードは、Alexのアダプティブカード/アクション呼び出しレスポンスカードの例を示しています。

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

ユーザー固有のビューを設計する際に留意するカード設計ガイドライン:

* チャットまたはチャンネルに送信される特定のカードに対して、最大 60 個の **ユーザー固有ビュー** を作成するには `userIds` `refresh` 、そのカードをセクションで指定します。
* **ベースカード:** ボット開発者がチャットに送信するカードの基本バージョン。 これは、セクションで指定されていないすべてのユーザーのアダプティブ カードのバージョンです `userIds` 。
* メッセージの更新または編集を使用してベースカードを更新し、同時にユーザー固有のカードを更新することができます。

## <a name="see-also"></a>関連項目

* [アダプティブ カードのユニバーサル アクションの操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新のビュー](Up-To-Date-Views.md)
