---
title: 検索ベースのメッセージ拡張機能のユニバーサル アクション
author: v-ypalikila
description: この記事では、検索ベースのメッセージ拡張機能のユニバーサル アクションとアダプティブ カードの自動更新について説明します。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: b8515ca2a84d3c29ddfb384fde5038a68d953c33
ms.sourcegitcommit: 19f3e4e9088d0a07c9b567e76640d498b9d1981f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2022
ms.locfileid: "67787199"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>検索ベースのメッセージ拡張機能のユニバーサル アクション

検索ベースのメッセージ拡張機能のアダプティブ カードでユニバーサル アクションがサポートされるようになりました。 検索ベースのメッセージ拡張機能でユニバーサル アクションを有効にするには、アプリが [アダプティブ カードのユニバーサル アクションのスキーマ](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) と、次の要件に準拠している必要があります。

1. アプリには、アプリ マニフェストで会話ボットが定義されている必要があります。
1. 会話型ボットが既にある場合は、メッセージ拡張機能で使用されているのと同じボットを使用する必要があります。
1. カードがグループで送信された場合、アプリはマニフェストでボットを指定するかスコープを指定 `team` する `groupchat` 必要があります。

次の値を含む JSON スキーマの`team``groupchat`例:

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
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

## <a name="automatic-refresh-for-adaptive-cards-in-search-based-message-extensions"></a>検索ベースのメッセージ拡張機能のアダプティブ カードの自動更新

検索ベースのメッセージ拡張機能でアダプティブ カードの自動更新を有効にして、ユーザーが常に最新の情報を表示できるようにします。 有効にするには、プロパティで配列を`29:<ID>`定義`userIds`します`8:orgid:<AAD ID>``refresh`。 詳細については、「 [アダプティブ カードのユニバーサル アクションの操作」を](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh)参照してください。

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
> グループ チャットまたはチャネル内のすべてのユーザーが 60 人以下の場合 *、自動更新が* 有効になります。 60 を超えるユーザーを含む会話 (グループ チャットまたはチャネル) の場合、ユーザーはメッセージ オプション メニューの更新ボタンを使用して最新の結果を取得できます。

プロパティの`Action.Execute``refresh`例:

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

Just-In-Time (JIT) を使用すると、グループ チャットまたはチャネルに複数のユーザーのカードまたはメッセージ拡張機能をインストールできます。 検索ベースのメッセージ拡張機能でユニバーサル アクションをサポートするために、ボットはユーザーによってカード (と共 `Action.Execute`に) が送信される会話に追加されます。

ユーザーがカードを選択してグループ チャットまたはチャネルで送信すると、 **JIT** インストール プロンプトが表示されます。 ユーザーが **送信** オプションを選択すると、バックグラウンドでチャットまたはチャネル内のすべてのユーザーに対してアプリが追加されます。

> [!NOTE]
> スキーマが定義されていない`Action.Execute``refresh`アプリの場合、インストール プロンプトはユーザーに表示されません。

動的 ME と JIT のインストール ユーザー フローの例:

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF には、動的メッセージ拡張機能と JIT インストールのユーザー フローが表示されます。":::

## <a name="see-also"></a>関連項目

* [メッセージの拡張機能](../../what-are-messaging-extensions.md)
* [アダプティブ カードのユニバーサル アクション](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
