---
title: アダプティブ カード タブを構築する
author: KirtiPereira
description: このモジュールでは、アクティビティの呼び出し、タスク モジュールのワークフローの理解、認証など、コード例を含むアダプティブ カードを使用したタブの作成について学習します。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 48415f4cba1a748dafd9d21e8429a59414769b98
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558178"
---
# <a name="build-tabs-with-adaptive-cards"></a>アダプティブ カードを使用してタブをビルドする

> [!IMPORTANT]
>
> * アダプティブ カードを含むタブは、現在、個人用アプリとしてのみサポートされています。

従来の方法を使用してタブを開発する場合、次の問題が発生する可能性があります。

* HTML と CSS
* 読み込み時間が遅い
* iFrame 制約
* サーバーのメンテナンスとコスト

アダプティブ カード タブは、Teams でタブを作成する新しい方法です。 IFrame に Web コンテンツを埋め込む代わりに、アダプティブ カードをタブにレンダリングできます。フロント エンドはアダプティブ カードでレンダリングされますが、バックエンドはボットによって供給されます。 ボットは、要求を受け入れ、レンダリングされるアダプティブ カードで適切に応答する役割を担います。

デスクトップ、Web、モバイルでネイティブな既製のユーザー インターフェイス (UI) 構成要素を使用してタブを構築できます。 この記事は、アプリ マニフェストに対して行う必要がある変更を理解するのに役立ちます。 また、この記事では、呼び出しアクティビティがアダプティブ カードを使用してタブで情報を要求して送信する方法と、タスク モジュール ワークフローに対する影響についても説明します。

次の図は、デスクトップとモバイルのアダプティブ カードを含むビルド タブを示しています。

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="タブでレンダリングされるアダプティブ カードの例。":::

## <a name="prerequisites"></a>前提条件

アダプティブ カードを使用してタブを作成する前に、次の作業を行う必要があります。

* Teams の[ボット開発](../../bots/what-are-bots.md)、[アダプティブ カード](https://adaptivecards.io/)、[タスク モジュール](../../task-modules-and-cards/task-modules/task-modules-bots.md)について理解してください。
* 開発用の Teams でボットを実行します。

## <a name="changes-to-app-manifest"></a>アプリ マニフェストの変更

タブをレンダリングする個人用アプリには、アプリ マニフェストに `staticTabs` 配列を含める必要があります。 アダプティブ カード タブは、`contentBotId` プロパティが `staticTab` 定義で指定されたときにレンダリングされます。 静的タブ定義には、アダプティブ カード タブを指定する `contentBotId` または一般的なホストされた Web コンテンツ タブ エクスペリエンスを指定する `contentUrl` のいずれかが含まれている必要があります。

> [!NOTE]
> この `contentBotId` プロパティは現在、マニフェスト バージョン 1.9 以降で使用できます。

[アダプティブ カード] タブが通信する必要のある `botId` を `contentBotId` プロパティに指定します。 [アダプティブ カード] タブ用に構成された `entityId` は、各呼び出し要求の `tabContext` パラメーターで送信され、同じボットから電力を供給されるアダプティブ カード タブを区別するために使用できます。 その他の静的タブ定義フィールドの詳細については、[[マニフェスト スキーマ]](../../resources/schema/manifest-schema.md#statictabs) を参照してください。

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

## <a name="invoke-activities"></a>アクティビティを呼び出す

アダプティブ カード タブとボット間の通信は、`invoke` アクティビティを通じて行われます。 各 `invoke` アクティビティには、対応する **名前** が付けられます。 各アクティビティの名前を使用して、各要求を区別します。 `tab/fetch` と `tab/submit` は、このセクションで取り上げるアクティビティです。

> [!NOTE]
>
> * ボットは、すべての応答を [サービス URL](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true) に送信する必要があります。 サービス URL は、着信 `activity` ペイロードの一部として受信されます。
> * 呼び出しペイロード のサイズが 80kb に増加しました。

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>タブにレンダリングするアダプティブ カードをフェッチする

`tab/fetch` は、ユーザーがアダプティブ カード タブを開いたときにボットが受信する最初の呼び出し要求です。 ボットがリクエストを受信すると、タブ **[続行]** 応答またはタブ **[認証]** 応答のいずれかを送信します。
**[続行]** 応答には **[カード]** の配列が含まれており、配列の順序でタブに垂直方向にレンダリングされます。

> [!NOTE]
> **[認証]** 応答の詳細については、「[認証](#authentication)」を参照してください。

次のコードは、`tab/fetch` 要求と応答の例を示しています。

**`tab/fetch`要求**

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

**`tab/fetch`応答**

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
                },
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a>アダプティブ カードからの送信を処理する

アダプティブ カードがタブにレンダリングされると、ユーザーの操作に応答できます。 この応答は、`tab/submit` 呼び出し要求によって処理されます。

ユーザーが [アダプティブ カード] タブのボタンを選択すると、アダプティブ カードの `Action.Submit` 機能を使用して、対応するデータを使用してボットに `tab/submit` 要求が トリガーされます。 アダプティブ カード データは、`tab/submit` 要求のデータ プロパティを使用して使用できます。 要求に対して次のいずれかの応答を受け取ります。

* 本文のない HTTP 状態コード `200` 応答。 空の 200 応答では、クライアントによってアクションが実行されることはありません。
* [アダプティブ カードのフェッチ](#fetch-adaptive-card-to-render-to-a-tab)で説明されているように、標準 `200` タブは応答を **続行** します。 タブの応答を **続行** すると、クライアントはレンダリングされたアダプティブ カード タブを、**継続** 応答のカード配列に用意されたアダプティブ カードで更新します。

次のコードは、`tab/submit` 要求と応答の例を示しています。

**`tab/submit`要求**

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

**`tab/submit`応答**

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

## <a name="understand-task-module-workflow"></a>タスク モジュールのワークフローを理解する

タスクモジュールはまた、アダプティブカードを使用して `task/fetch` および `task/submit` の要求と応答を呼び出します。 詳細については、「[Microsoft Teams ボットでのタスク モジュールの使用](../../task-modules-and-cards/task-modules/task-modules-bots.md)」を参照してください。

[アダプティブ カード] タブの導入により、ボットが `task/submit` リクエストに応答する方法が変更されました。 [アダプティブ カード] タブを使用している場合、ボットは `task/submit` 呼び出し要求に標準タブの **[続行]** 応答で応答し、タスク モジュールを閉じます。 [アダプティブ カード] タブは、**[続行]** タブの応答本文で提供されるカードの新しいリストをレンダリングすることで更新されます。

### <a name="invoke-taskfetch"></a>`task/fetch` を呼び出す

次のコードは、`task/fetch` 要求と応答の例を示しています。

**`task/fetch`要求**

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

**`task/fetch`応答**

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

### <a name="invoke-tasksubmit"></a>`task/submit` を呼び出す

次のコードは、`task/submit` 要求と応答の例を示しています。

**`task/submit`要求**

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

**`task/submit` Tab 応答の種類**

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

前のセクションでは、ほとんどの開発パラダイムをタスク モジュールの要求と応答からタブの要求と応答に拡張できることを確認しました。 認証の処理に関しては、[アダプティブ カード] タブのワークフローは、メッセージ拡張の認証パターンに従います。 詳細については、「[認証の追加](../../messaging-extensions/how-to/add-authentication.md)」を参照してください。

`tab/fetch` 要求には、**[続行]** または **[認証]** レスポンスのいずれかを含めることができます。 `tab/fetch` 要求がトリガーされ、タブ **[認証]** 応答を受信すると、サインイン ページがユーザーに表示されます。

**`tab/fetch`[呼び出し]** を使用して認証コードを取得するには

1. アプリを開きます。 サインイン ページが表示されます。

    > [!NOTE]
    > アプリ のロゴは、アプリ マニフェストで定義されている `icon` プロパティを通じて提供されます。 ロゴの後に表示されるタイトルは、タブ **[認証]** 応答本文に返される `title` プロパティで定義されています。

1. [**サインイン**] を選びます。 **[認証]** 応答本文の `value` プロパティで提供される認証 URL にリダイレクトされます。
1. ポップアップ ウィンドウが表示されます。 このポップアップ ウィンドウでは、認証 URL を使用して Web ページをホストします。
1. サインインした後、ウィンドウを閉じます。 **認証コード** は、Teams クライアントに送信されます。
1. その後、Teams クライアントはサービスへの`tab/fetch`要求を再発行します。これには、ホストされている Web ページによって提供される認証コードが含まれます。

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` 認証データ フロー

次の図は、`tab/fetch` 呼び出しに対する認証データ フローのしくみの概要を示しています。

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="アダプティブ カード タブ認証フローの例。":::

**`tab/fetch` 認証応答**

次のコードは、`tab/fetch` 認証応答の例を示しています。

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
| [Teams] タブにアダプティブ カードを表示する | Microsoft Teams タブ サンプル コードです。これは、Teams でアダプティブ カードを表示する方法を示しています。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>関連項目

* [アダプティブ カード](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
