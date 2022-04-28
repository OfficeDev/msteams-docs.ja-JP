---
title: アダプティブ カード タブを作成する
author: KirtiPereira
description: アクティビティの呼び出し、タスク モジュールのワークフローの理解、認証など、コード例を使用してアダプティブ カードを使用してタブを構築する方法について説明します。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: アダプティブ カードの個人用アプリ認証データ フロー
ms.openlocfilehash: 95507373671f9044bec788e981f66931b4588705
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104526"
---
# <a name="build-tabs-with-adaptive-cards"></a>アダプティブ カードを使用してタブをビルドする

> [!IMPORTANT]
>
> * アダプティブ カードを含むタブは、現在、個人用アプリとしてのみサポートされています。

従来の方法を使用してタブを開発する場合、次の問題が発生する可能性があります。

* HTML と CSS に関する考慮事項
* 読み込み時間が遅い
* iFrame 制約
* サーバーのメンテナンスとコスト

アダプティブ カード タブは、Teamsでタブを作成する新しい方法です。 IFrame に Web コンテンツを埋め込む代わりに、アダプティブ カードをタブにレンダリングできます。フロントエンドはアダプティブ カードでレンダリングされますが、バックエンドはボットによって供給されます。 ボットは、要求を受け入れ、レンダリングされるアダプティブ カードで適切に応答する役割を担います。

デスクトップ、Web、モバイルでネイティブな既製のユーザー インターフェイス (UI) 構成要素を使用してタブを構築できます。 この記事は、アプリ マニフェストに対して行う必要がある変更を理解するのに役立ちます。 また、この記事では、呼び出しアクティビティがアダプティブ カードを使用してタブで情報を要求して送信する方法と、タスク モジュール ワークフローに対する影響についても説明します。

次の図は、デスクトップとモバイルのアダプティブ カードを含むビルド タブを示しています。

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="タブでレンダリングされるアダプティブ カードの例。" border="false":::

## <a name="prerequisites"></a>前提条件

アダプティブ カードを使用してタブを作成する前に、次の作業を行う必要があります。

* Teamsの[ボット開発](../../bots/what-are-bots.md)、[アダプティブ カード](https://adaptivecards.io/)、[タスク モジュール](../../task-modules-and-cards/task-modules/task-modules-bots.md)について理解してください。
* 開発用のTeamsでボットを実行します。

## <a name="changes-to-app-manifest"></a>アプリ マニフェストの変更

タブをレンダリングする個人用アプリには、アプリ マニフェストに配列を `staticTabs` 含める必要があります。 アダプティブ カード タブは、プロパティが定義で`contentBotId``staticTab`指定されたときにレンダリングされます。 静的タブ定義には、 `contentBotId`アダプティブ カード タブを指定するか、一 `contentUrl`般的なホスト Web コンテンツ タブ エクスペリエンスを指定する必要があります。

> [!NOTE]
> この `contentBotId` プロパティは現在、マニフェスト バージョン 1.9 以降で使用できます。

`contentBotId`アダプティブ カード タブが`botId`通信する必要があるプロパティを指定します。 `entityId`アダプティブ カード タブ用に構成されたタブは、各呼び出し要求のパラメーターで`tabContext`送信され、同じボットによって供給されるアダプティブ カード タブを区別するために使用できます。 その他の静的タブ定義フィールドの詳細については、 [マニフェスト スキーマ](../../resources/schema/manifest-schema.md#statictabs)に関するページを参照してください。

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

アダプティブ カード タブとボット間の通信は、アクティビティを通じて `invoke` 行われます。 各 `invoke` アクティビティには、対応する **名前が付けられます**。 各アクティビティの名前を使用して、各要求を区別します。 `tab/fetch` は `tab/submit` 、このセクションで取り上げるアクティビティです。

> [!NOTE]
>
> * ボットは、すべての応答を [サービス URL](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true) に送信する必要があります。 サービス URL は、受信ペイロードの一部として受信 `activity` されます。
> * 呼び出しペイロード のサイズが 80 kb に増加しました。

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>タブにレンダリングするアダプティブ カードをフェッチする

`tab/fetch` は、ユーザーがアダプティブ カード タブを開いたときにボットが受け取る最初の呼び出し要求です。ボットが要求を受信すると、タブ **の続行** 応答またはタブ **認証** 応答が送信されます。
**Continue** 応答には **カード** の配列が含まれており、配列の順序でタブに垂直方向にレンダリングされます。

> [!NOTE]
> **認証** 応答の詳細については、「[認証](#authentication)」を参照してください。

次のコードは、要求と応答の `tab/fetch` 例を示しています。

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

アダプティブ カードがタブにレンダリングされると、ユーザーの操作に応答できます。 この応答は、呼び出し `tab/submit` 要求によって処理されます。

ユーザーが [アダプティブ カード] タブのボタンを選択すると、アダプティブ カードの `tab/submit` 機能を使用して、対応するデータを使用してボットに要求が `Action.Submit` トリガーされます。 アダプティブ カード データは、要求の `tab/submit` data プロパティを使用して使用できます。 要求に対して次のいずれかの応答を受け取ります。

* 本文のない HTTP 状態コード `200` 応答。 空の 200 応答では、クライアントによってアクションが実行されることはありません。
* [アダプティブ カードのフェッチ](#fetch-adaptive-card-to-render-to-a-tab)で説明されているように、標準`200`タブは応答を **続行** します。 タブ **の応答を続行** すると、クライアントはレンダリングされたアダプティブ カード タブを、 **継続** 応答のカード配列に用意されたアダプティブ カードで更新します。

次のコードは、要求と応答の `tab/submit` 例を示しています。

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

## <a name="understand-task-module-workflow"></a>タスク モジュールのワークフローを理解する

タスク モジュールでは、アダプティブ カードを使用して、呼び出 `task/fetch` しと `task/submit` 要求と応答も行います。 詳細については、[Microsoft Teams ボットでのタスク モジュールの使用に関するページを](../../task-modules-and-cards/task-modules/task-modules-bots.md)参照してください。

アダプティブ カード タブの導入により、ボットが要求に応答する方法が `task/submit` 変更されます。 アダプティブ カード タブを使用している場合、ボットは呼び出し要求に応答し `task/submit` 、標準タブで応答を **続行** し、タスク モジュールを閉じます。 [アダプティブ カード] タブは、タブで提供されるカードの新しい一覧を表示して、応答本文を **続行** することで更新されます。

### <a name="invoke-taskfetch"></a>呼び出す `task/fetch`

次のコードは、要求と応答の `task/fetch` 例を示しています。

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

### <a name="invoke-tasksubmit"></a>呼び出す `task/submit`

次のコードは、要求と応答の `task/submit` 例を示しています。

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

前のセクションでは、ほとんどの開発パラダイムをタスク モジュールの要求と応答からタブ要求と応答に拡張できることを確認しました。 認証の処理に関しては、[アダプティブ カード] タブのワークフローは、メッセージ拡張機能の認証パターンに従います。 詳細については、「認証の [追加](../../messaging-extensions/how-to/add-authentication.md)」を参照してください。

`tab/fetch` 要求には **、続行** 応答または **認証** 応答を指定できます。 要求が `tab/fetch` トリガーされ、タブ **認証** 応答を受信すると、サインイン ページがユーザーに表示されます。

**呼び出しを使用して認証コードを `tab/fetch` 取得するには**

1. アプリを開きます。 サインイン ページが表示されます。

    > [!NOTE]
    > アプリ のロゴは、アプリ マニフェストで定義されている `icon` プロパティを通じて提供されます。 タブ **認証** 応答本文で返されるプロパティで`title`ロゴが定義された後に表示されるタイトル。

1. [**サインイン**] を選びます。 **認証** 応答本文のプロパティで`value`指定された認証 URL にリダイレクトされます。
1. ポップアップ ウィンドウが表示されます。 このポップアップ ウィンドウでは、認証 URL を使用して Web ページをホストします。
1. サインインした後、ウィンドウを閉じます。 **認証コード** は、Teams クライアントに送信されます。
1. その後、Teams クライアントはサービスへの要求を再発行`tab/fetch`します。これには、ホストされている Web ページによって提供される認証コードが含まれます。

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` 認証データ フロー

次の図は、呼び出しに対する認証データ フローのしくみの概要を `tab/fetch` 示しています。

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
| [Teams] タブにアダプティブ カードを表示する | Microsoft Teamsタブサンプル コードです。これは、Teamsでアダプティブ カードを表示する方法を示しています。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>関連項目

* [アダプティブ カード](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループの作成] タブ](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
