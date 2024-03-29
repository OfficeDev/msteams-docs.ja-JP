---
title: 検索ベースのメッセージ拡張機能のユニバーサル アクション
author: v-ypalikila
description: この記事では、検索ベースのメッセージ拡張機能のアダプティブ カードのユニバーサル アクションと自動更新について説明します。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: 18f5b783797d69144aac82e5ebd95fc30dad57a2
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819969"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>検索ベースのメッセージ拡張機能のユニバーサル アクション

検索ベースのメッセージ拡張機能のアダプティブ カードでユニバーサル アクションがサポートされるようになりました。 検索ベースのメッセージ拡張機能に対してユニバーサル アクションを有効にするには、アプリが [アダプティブ カードのユニバーサル アクションのスキーマ](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) と次の要件に準拠している必要があります。

1. アプリには、アプリ マニフェストで会話ボットが定義されている必要があります。
1. 既に会話ボットがある場合は、メッセージ拡張機能で使用されているのと同じボットを使用する必要があります。
1. カードがグループで送信される場合、アプリはマニフェストでボットに対してまたは`groupchat`スコープを指定`team`する必要があります。

と `groupchat` の値を持つ `team` JSON スキーマの例:

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "scopes": [
                    "team",
                    "personal",
                    "groupchat"
                ]
        }
    ],
    "composeExtensions": [
        {
            "canUpdateConfiguration": true,
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%", // Use the same bot as what is specified in the bots section above
        }
    ]
}
```

## <a name="automatic-refresh-for-adaptive-cards-in-search-based-message-extensions"></a>検索ベースのメッセージ拡張機能でのアダプティブ カードの自動更新

検索ベースのメッセージ拡張機能でアダプティブ カードの自動更新を有効にして、ユーザーが常に最新の情報を確実に表示できるようにします。 有効にするには、 プロパティで または `8:orgid:<AAD ID>` 形式の`29:<ID>`配列を`refresh`定義`userIds`します。 詳細については、「 [アダプティブ カードのユニバーサル アクションの操作」を](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh)参照してください。

プロパティ内の配列の`userIds``refresh`例:

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "userIds": [
                "8:orgid:<AADID>",
                "29:<id>"
            ],
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

> [!NOTE]
> 自動更新は、60 ユーザー以下のグループ チャットまたはチャネル内のすべてのユーザー *に対して* 有効になります。 60 人を超えるユーザーとの会話 (グループ チャットまたはチャネル) の場合、ユーザーはメッセージ オプション メニューの [更新] ボタンを使用して最新の結果を取得できます。

プロパティ内の の`Action.Execute``refresh`例:

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

## <a name="just-in-time-install"></a>Just-In-Time インストール

Just-In-Time (JIT) を使用すると、グループ チャットまたはチャネルに複数のユーザーのカードまたはメッセージ拡張機能をインストールできます。 検索ベースのメッセージ拡張機能でユニバーサル アクションをサポートするために、ボットが会話に追加され、カード (と ) `Action.Execute`がユーザーによって送信されます。

ユーザーがカードを選択してグループ チャットまたはチャネルで送信すると、 **JIT** インストール プロンプトが表示されます。 ユーザーが **送信** オプションを選択すると、バックグラウンドでチャットまたはチャネル内のすべてのユーザーに対してアプリが追加されます。

> [!NOTE]
> と スキーマが定義されていない`Action.Execute``refresh`アプリの場合、インストール プロンプトはユーザーに表示されません。

動的 ME および JIT インストール ユーザー フローの例:

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF は、動的メッセージ拡張機能と JIT インストールのユーザー フローを示します。":::

## <a name="see-also"></a>関連項目

* [メッセージの拡張機能](../../what-are-messaging-extensions.md)
* [アダプティブ カード](../../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [アダプティブ カードのユニバーサル アクション](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
