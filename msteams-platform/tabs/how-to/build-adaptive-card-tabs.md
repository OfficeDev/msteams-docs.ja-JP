---
title: アダプティブ カード タブの作成
author: KirtiPereira
description: アダプティブ カードを使用してタブを作成する
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 8f1b8bbc27a2b10d8e4fbca8e87c75eeb29c8c36efacd6eb3cf921295e27b88b
ms.sourcegitcommit: 569ff24cc41c46d886b913a916401b18e0eb1439
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2021
ms.locfileid: "57823229"
---
# <a name="build-tabs-with-adaptive-cards"></a>アダプティブ カードを使用してタブをビルドする

> [!IMPORTANT]
> * アダプティブ カード付きタブは現在、個人用アプリとしてのみサポートされています。

従来のメソッドを使用してタブを開発する場合、次の問題が発生する可能性があります。

* HTML と CSS の考慮事項
* 読み込み時間が遅い
* iFrame の制約
* サーバーのメンテナンスとコスト

アダプティブ カード タブは、新しい方法でタブを作成する方法Teams。 IFrame に Web コンテンツを埋め込む代わりに、アダプティブ カードをタブにレンダリングできます。フロントエンドがアダプティブ カードでレンダリングされている間、バックエンドはボットによって駆動されます。 ボットは、要求を受け入れ、レンダリングされるアダプティブ カードで適切に応答する責任があります。

デスクトップ、Web、モバイルでネイティブな既製のユーザー インターフェイス (UI) 構成要素を使用してタブを構築できます。 この記事では、アプリ マニフェストに加える必要がある変更を理解するのに役立ちます。 また、呼び出しアクティビティがアダプティブ カードを使用してタブ内の情報を要求および送信する方法と、タスク モジュール ワークフローに対する影響も示します。

次の図は、デスクトップとモバイルのアダプティブ カードを含むビルド タブを示しています。

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="タブでレンダリングされるアダプティブ カードの例。" border="false":::

## <a name="prerequisites"></a>前提条件

アダプティブ カードを使用してタブを作成する前に、次の条件を実行する必要があります。

* ボット開発、[アダプティブ カード](../../bots/what-are-bots.md)、[および](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)タスク モジュール[](../../task-modules-and-cards/task-modules/task-modules-bots.md)に精通Teams。
* 開発に必要なTeamsボットを作成します。

## <a name="changes-to-app-manifest"></a>アプリ マニフェストの変更点

タブをレンダリングする個人用アプリには、アプリ マニフェスト `staticTabs` に配列を含める必要があります。 アダプティブ カード タブは、プロパティが `contentBotId` 定義で提供されている場合に表示 `staticTab` されます。 静的タブ定義には、アダプティブ カード タブを指定する 、またはホストされる一般的な Web コンテンツ タブ エクスペリエンスを指定する 、 のいずれかを `contentBotId` `contentUrl` 含む必要があります。

> [!NOTE]
> この `contentBotId` プロパティは現在、マニフェスト バージョン 1.9 以降で使用できます。

[アダプティブ `contentBotId` カード] タブが `botId` 通信する必要があるプロパティを指定します。 [アダプティブ カード] タブ用に構成された設定は、各呼び出し要求のパラメーターに送信され、同じボットを使用するアダプティブ カード タブを `entityId` `tabContext` 区別するために使用できます。 その他の静的タブ定義フィールドの詳細については、「マニフェスト スキーマ」 [を参照してください](../../resources/schema/manifest-schema.md#statictabs)。

アダプティブ カード タブ マニフェストの例を次に示します。

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "id": "00000000-0000-0000-0000-000000000000",
  "version": "0.0.1",
  "packageName": "acprototype",
  "developer": {
    "name": "Contoso",
    "websiteUrl": "https://contoso.yourwebsite.com",
    "privacyUrl": "https://contoso.yourwebsite.com/privacy.html",
    "termsOfUseUrl": "https://contoso.yourwebsite.com/terms.html"
  },
  "name": {
    "short": "Contoso",
    "full": "Contoso Home"
  },
  "description": {
    "short": "Add short description here",
    "full": "Add full description here"
  },
  "icons": {
    "outline": "icon-outline.png",
    "color": "icon-color.png"
  },
  "accentColor": "#D85028",
  "configurableTabs": [],
  "staticTabs": [
    {
      "entityId": "homeTab",
      "name": "Home",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    },
    {
      "entityId": "moreTab",
      "name": "More",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    }
  ],
  "connectors": [],
  "composeExtensions": [],
  "permissions": ["identity", "messageTeamMembers"],
  "validDomains": [
    "contoso.yourwebsite.com",
    "token.botframework.com"
  ]
}
```

## <a name="invoke-activities"></a>アクティビティの呼び出し

アダプティブ カード タブとボット間の通信は、アクティビティを通じて行 `invoke` われます。 各 `invoke` アクティビティには、対応する名前 **があります**。 各要求を区別するには、各アクティビティの名前を使用します。 `tab/fetch` この `tab/submit` セクションで説明するアクティビティを示します。

> [!NOTE]
> ボットはサービス URL に対してすべての応答を [送信する必要があります](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true)。 サービス URL は、受信ペイロードの一部として受信 `activity` されます。

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>タブにレンダリングするアダプティブ カードのフェッチ

`tab/fetch`は、ユーザーがアダプティブ カード タブを開いたときにボットが受け取る最初の呼び出し要求です。ボットが要求を受信すると、タブ続行応答またはタブ **認証応答が送信** されます。
継続 **応答** には、カードの配列 **が含** まれます。これは、配列の順序でタブに垂直にレンダリングされます。

> [!NOTE]
> 認証応答の詳細 **については、「認証** 」を [参照してください](#authentication)。

次のコードは、要求と応答 `tab/fetch` の例を示しています。

**`tab/fetch` 要求**

```json
// tab/fetch POST request: agents/{botId}/invoke
{
    "name": "tab/fetch",
    "value: {
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        },
        "context": {
            "theme": "default"
            }
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/fetch` 応答**

```json
// tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
                {
                    "card": adaptiveCard1,
                },
                {
                    "card": adaptiveCard2,
                }
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a>アダプティブ カードからの送信の処理

タブでアダプティブ カードをレンダリングすると、ユーザーの操作に応答できます。 この応答は、呼び出し要求 `tab/submit` によって処理されます。

ユーザーが [アダプティブ カード] タブのボタンを選択すると、アダプティブ カードの機能を使用して対応するデータを使用してボットに要求 `tab/submit` `Action.Submit` がトリガーされます。 アダプティブ カード データは、要求の data プロパティを使用して使用 `tab/submit` できます。 要求に対して次のいずれかの応答を受け取る。

* 本文がない HTTP `200` 状態コード応答。 空の 200 応答では、クライアントによって実行されるアクションはありません。
* アダプティブ カードの `200` フェッチ **で説明** したように、標準タブは応答 [を続行します](#fetch-adaptive-card-to-render-to-a-tab)。 タブの **応答を** 続行すると、クライアントは、引き続き応答のカード配列に用意されているアダプティブ カードを使用して、レンダリングされたアダプティブ カード タブを **更新** します。

次のコードは、要求と応答 `tab/submit` の例を示しています。

**`tab/submit` 要求**

```json
// tab/submit POST request: agents/{botId}/invoke:
{
    "name": "tab/submit",
    "value": {
        "data": {
            "type": "tab/submit",
            //...<data properties>
            },
        "context": {
            "theme": "default"
            },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
            },
        },
    "conversation": {
           "id": "{generated_conversation_id}" 
        },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/submit` 応答**

```json
//tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
              {
                "card": adaptiveCard1,
                },
              {
                "card": adaptiveCard2,
                } 
            ]
        },
    },
    "responseType": "tab"
}
```

## <a name="understand-task-module-workflow"></a>タスク モジュールのワークフローについて

また、タスク モジュールはアダプティブ カードを使用して呼 `task/fetch` び出し `task/submit` 、要求と応答を行います。 詳細については、「タスク ボット[でのタスク モジュールの使用Microsoft Teams参照してください](../../task-modules-and-cards/task-modules/task-modules-bots.md)。

[アダプティブ カード] タブの導入により、ボットが要求に応答する方法が変更 `task/submit` されます。 アダプティブ カード タブを使用している場合、ボットは標準タブで呼び出し要求に応答し、応答を続行し、タスク モジュール `task/submit` を閉じます。  [アダプティブ カード] タブは、タブで提供される新しいカードの一覧を表示して、応答本文 **を** 続行することで更新されます。

### <a name="invoke-taskfetch"></a>Invoke `task/fetch`

次のコードは、要求と応答 `task/fetch` の例を示しています。

**`task/fetch` 要求**
```json
// task/fetch POST request: agents/{botId}/invoke
{
    "name": "task/fetch",
    "value": {
        "data": {
            "type": "task/fetch"
        },
        "context": {
            "theme": "default",
        },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        }
    },
    "imdisplayname": "{user_display_name}",
    "conversation": {
        "id": "{generated_conversation_id}"
    } 
}
```

**`task/fetch` 応答**

```json
// task/fetch POST response: agents/{botId}/invoke
{
    "task": {
        "value": {
            "title": "Ninja Cat",
            "height": "small",
            "width": "small",
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": adaptiveCard,
            }
        },
    "type": "continue"
    },
    "responseType": "task"
}
```

### <a name="invoke-tasksubmit"></a>Invoke `task/submit`

次のコードは、要求と応答 `task/submit` の例を示しています。

**`task/submit` 要求**

```json
// task/submit POST request: agent/{botId}/invoke:
{
    "name": "task/submit",
    "value": {
        "data": {serialized_data_object},
        "context": {
            "theme": "default"
        },
    "tabContext": {
        "tabEntityId": "{tab_entity_id}"
        },
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}",
}
```

**`task/submit` tab 応答の種類**

```json
// tab/fetch **continue** POST response: 
{
    "task":{
        "value": {
            "tab": {
                "type": "continue",
                "value": {
                    "cards": [
                        {
                            "card": adaptiveCard1
                        },
                        {
                            "card": adaptiveCard2
                        }
                    ]
                }
            }
        },
        "type": "continue"
    },
    "responseType": "task"
}
```

## <a name="authentication"></a>認証

前のセクションでは、開発のパラダイムのほとんどをタスク モジュールの要求と応答からタブ要求と応答に拡張できます。 認証の処理に関しては、[アダプティブ カード] タブのワークフローは、メッセージング拡張機能の認証パターンに従います。 詳細については、「認証の追加 [」を参照してください](../../messaging-extensions/how-to/add-authentication.md)。

`tab/fetch`要求には、続行応答 **または****認証応答を指定** できます。 要求が `tab/fetch` トリガーされ、タブ **認証** 応答を受信すると、サインイン ページがユーザーに表示されます。

**呼び出しを使用して認証コードを取得 `tab/fetch` するには**

1. アプリを開きます。 サインイン ページが表示されます。

    > [!NOTE]
    > アプリ のロゴは、アプリ マニフェスト `icon` で定義されているプロパティを使用して提供されます。 タブ認証応答本文で返されるプロパティでロゴが定義された後に表示されるタイトル `title` 。 

1. **[サインイン]** を選びます。 認証応答本文のプロパティに指定されている認証 URL `value` **に** リダイレクトされます。
1. ポップアップ ウィンドウが表示されます。 このポップアップ ウィンドウは、認証 URL を使用して Web ページをホストします。
1. サインインした後、ウィンドウを閉じます。 認証 **コードが** クライアントにTeamsされます。
1. 次Teamsクライアントは、ホストされた Web ページによって提供される認証コードを含む、サービスへの要求 `tab/fetch` を再発行します。

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` 認証データ フロー

次の図は、呼び出しに対する認証データ フローの動作の概要を示 `tab/fetch` しています。

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="アダプティブ カード タブ認証フローの例。" border="false":::

**`tab/fetch` 認証応答**

次のコードは、認証応答の `tab/fetch` 例を示しています。

```json
// tab/auth POST response (openURL)
{
    "tab": {
        "type": "auth",
        "suggestedActions":{
            "actions":[
                {
                    "type": "openUrl",
                    "value": "https://example.com/auth",
                    "title": "Sign in to this app"
                }
            ]
        }
    }
}
```

### <a name="example"></a>例

次のコードは、再発行された要求の例を示しています。

```json
{
    "name": "tab/fetch",
    "type": "invoke",
    "timestamp": "2021-01-15T00:10:12.253Z",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "{id}",
        "name": "John Smith",
        "aadObjectId": "00000000-0000-0000-0000-000000000000"
    },
    "conversation": {
        "tenantId": "{tenantId}",
        "id": "tab:{guid}"
    },
    "recipients": {
        "id": "28:00000000-0000-0000-0000-000000000000",
        "name": "ContosoApp"
    },
    "entities": [
        {
            "locale": "en-us",
            "country": "US",
            "platform": "Windows",
            "timezone": "America/Los_Angeles",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": { "id": "00000000-0000-0000-0000-000000000000" },
        "source": { "name": "message" }
    },
    "value": {
        "tabContext": { "tabEntityId": "homeTab" },
        "state": "0.43195668034524815"
    },
    "locale": "en-US",
    "localTimeZone": "America/Los_Angeles"
}
```

## <a name="code-sample"></a>コード サンプル

|**サンプルの名前** | **説明** |**.NET** | **Node.js** |
|----------------|-----------------|--------------|--------------|
| [アダプティブ カードの表示] Teamsタブ | Microsoft Teamsタブのサンプル コードで、アダプティブ カードを表示する方法を示Teams。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [アダプティブ カード](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)
