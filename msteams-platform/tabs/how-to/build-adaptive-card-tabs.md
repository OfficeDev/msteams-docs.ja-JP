---
title: アダプティブ カード タブの作成
author: KirtiPereira
description: アダプティブ カードを使用してタブを作成する
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: d65fc537b5282c050d891a6a73ff114c630e2c1c
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668849"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="57fd2-103">アダプティブ カードを使用してタブを作成する</span><span class="sxs-lookup"><span data-stu-id="57fd2-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="57fd2-104">この機能はパブリック [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) デスクトップとモバイルでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="57fd2-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="57fd2-105">Web ブラウザーでのサポートは近日公開予定です。</span><span class="sxs-lookup"><span data-stu-id="57fd2-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="57fd2-106">アダプティブ カード付きタブは現在、個人用アプリとしてのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="57fd2-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="57fd2-107">アダプティブ カードを使用してタブを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-107">Use Adaptive Cards to build tabs with ease.</span></span> <span data-ttu-id="57fd2-108">デスクトップ、Web、モバイルでネイティブに見える、既製の UI レゴ ブロックを使用してタブを構築できます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-108">You can build your tabs with ready-made UI Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="57fd2-109">アダプティブ カードを使用してタブを構築すると、ボット バックエンドとアダプティブ カードのフロントエンドにTeams アプリのすべての機能が一元化され、ボットとタブの別のバックエンドが不要となります。</span><span class="sxs-lookup"><span data-stu-id="57fd2-109">Building tabs with Adaptive Cards centralizes all Teams app capabilities around a bot backend and Adaptive Card frontend, thus, eliminating the need for a different backend for your bot and tabs.</span></span> <span data-ttu-id="57fd2-110">これにより、アプリのサーバーとメンテナンスコストが大幅にTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-110">This greatly reduces server and maintenance costs of your Teams app.</span></span> <span data-ttu-id="57fd2-111">この記事では、アプリ マニフェストに対して行う必要がある変更、アクティビティの呼び出しがアダプティブ カードを使用してタブで情報を要求および送信する方法、およびタスク モジュールワークフローへの影響を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-111">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span> 

次の図は、デスクトップとモバイルのアダプティブ カードを含むビルド タブを示しています。タブでレンダリングされるアダプティブ カード :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="の例を示します。" border="false":::

## <a name="prerequisites"></a><span data-ttu-id="57fd2-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="57fd2-113">Prerequisites</span></span>

<span data-ttu-id="57fd2-114">アダプティブ カードを使用してタブを作成する前に、次の条件を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57fd2-114">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="57fd2-115">ボット開発、[アダプティブ カード、](../../bots/what-are-bots.md)タスク モジュールに[](../../task-modules-and-cards/task-modules/task-modules-bots.md)精通Teams。 [](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)</span><span class="sxs-lookup"><span data-stu-id="57fd2-115">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [Task Modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="57fd2-116">開発に必要なTeamsボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-116">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="57fd2-117">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="57fd2-117">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="57fd2-118">アプリ マニフェストの変更点</span><span class="sxs-lookup"><span data-stu-id="57fd2-118">Changes to app manifest</span></span>

<span data-ttu-id="57fd2-119">タブをレンダリングする個人用アプリには、アプリ マニフェスト `staticTabs` に配列を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="57fd2-119">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="57fd2-120">アダプティブ カード タブは、プロパティが `contentBotId` 定義で指定されている場合にレンダリング `staticTab` されます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-120">Adaptive Card Tab are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="57fd2-121">静的タブ定義には、アダプティブ カード タブを指定する 、またはホストされる一般的な Web コンテンツ タブ エクスペリエンスを指定する 、 のいずれかを `contentBotId` `contentUrl` 含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="57fd2-121">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card Tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="57fd2-122">プロパティ `contentBotId` は現在、マニフェスト バージョン 1.9 以降で使用できます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-122">The `contentBotId` property is currently available manifest version 1.9 or later.</span></span> 

<span data-ttu-id="57fd2-123">アダプティブ カード `contentBotId` タブが通信 `botId` する必要があるプロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-123">Provide the `contentBotId` property with the `botId` that the Adaptive Card Tab must communicate with.</span></span> <span data-ttu-id="57fd2-124">アダプティブ カード タブ用に構成された設定は、各呼び出し要求のパラメーターで送信され、同じボットを使用する異なるアダプティブ カード タブを `entityId` `tabContext` 区別するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-124">The `entityId` configured for the Adaptive Card Tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate different Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="57fd2-125">その他の静的タブ定義フィールドの詳細については、「マニフェスト スキーマ」 [を参照してください](../../resources/schema/manifest-schema.md#statictabs)。</span><span class="sxs-lookup"><span data-stu-id="57fd2-125">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="57fd2-126">アダプティブ カード タブ マニフェストの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-126">Following is a sample Adaptive Card Tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="57fd2-127">アクティビティの呼び出し</span><span class="sxs-lookup"><span data-stu-id="57fd2-127">Invoke activities</span></span>

<span data-ttu-id="57fd2-128">アダプティブ カード タブとボット間の通信は、アクティビティを通じて行 `invoke` われます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-128">Communication between your Adaptive Card Tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="57fd2-129">各 `invoke` アクティビティには、対応する名前 *があります*。</span><span class="sxs-lookup"><span data-stu-id="57fd2-129">Each `invoke` activity has a corresponding *name*.</span></span> <span data-ttu-id="57fd2-130">各要求を区別するには、各アクティビティの名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-130">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="57fd2-131">`tab/fetch` この `tab/submit` セクションで説明するアクティビティを示します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-131">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="57fd2-132">タブにレンダリングするアダプティブ カードのフェッチ</span><span class="sxs-lookup"><span data-stu-id="57fd2-132">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="57fd2-133">`tab/fetch` は、ユーザーがアダプティブ カード タブを開いたときにボットが受け取る最初の呼び出し要求です。</span><span class="sxs-lookup"><span data-stu-id="57fd2-133">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card Tabs.</span></span> <span data-ttu-id="57fd2-134">ボットが要求を受信すると、タブは応答を続行するか、タブ **認証応答を送信** します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-134">When your bot receives the request, it will either send a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="57fd2-135">継続 **応答** には、カードの配列 **が含** まれます。これは、配列の順序でタブに垂直にレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-135">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="57fd2-136">認証 **応答については** 、「認証」セクションで [詳しく説明](#authentication) します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-136">The **auth** response is explained in detail in the [authentication](#authentication) section.</span></span>

<span data-ttu-id="57fd2-137">次のコード スニペットは、要求と応答 `tab/fetch` の例です。</span><span class="sxs-lookup"><span data-stu-id="57fd2-137">The following code snippets are examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="57fd2-138">**`tab/fetch` 要求**</span><span class="sxs-lookup"><span data-stu-id="57fd2-138">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="57fd2-139">**`tab/fetch` 応答**</span><span class="sxs-lookup"><span data-stu-id="57fd2-139">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="57fd2-140">アダプティブ カードからの送信の処理</span><span class="sxs-lookup"><span data-stu-id="57fd2-140">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="57fd2-141">タブでアダプティブ カードがレンダリングされた後、ユーザーの操作に応答できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="57fd2-141">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="57fd2-142">この応答は、呼び出し要求 `tab/submit` によって処理されます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-142">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="57fd2-143">ユーザーがアダプティブ カード タブのボタンを選択すると、アダプティブ カードの Action.Submit 関数を使用して、対応するデータを使用してボットに要求 `tab/submit` がトリガーされます。 </span><span class="sxs-lookup"><span data-stu-id="57fd2-143">When a user selects a button on the Adaptive Card Tab, the `tab/submit` request is triggered to your bot with the corresponding data through the *Action.Submit* function of Adaptive Card.</span></span> <span data-ttu-id="57fd2-144">アダプティブ カード データは、要求の data プロパティを使用して使用 `tab/submit` できます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-144">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="57fd2-145">要求に対して次のいずれかの応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-145">You will receive either of the following responses to your request:</span></span>

* <span data-ttu-id="57fd2-146">本文がない http 状態コード `200` 応答。</span><span class="sxs-lookup"><span data-stu-id="57fd2-146">A http status code `200` response with no body.</span></span> <span data-ttu-id="57fd2-147">空の 200 応答では、クライアントによって実行されるアクションはありません。</span><span class="sxs-lookup"><span data-stu-id="57fd2-147">An empty 200 response will result in no action taken by the client.</span></span>
* <span data-ttu-id="57fd2-148">[アダプティブ カード `200` のフェッチ **] セクション** で説明したように、標準タブは応答 [を続行](#fetch-adaptive-card-to-render-to-a-tab) します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-148">The standard `200` tab **continue** response, as explained in [Fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab) section.</span></span> <span data-ttu-id="57fd2-149">タブの **応答を続行** すると、クライアントは、引き続き応答のカード配列に用意されているアダプティブ カードを使用して、レンダリングされたアダプティブ カード タブを **更新** します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-149">A tab **continue** response triggers the client to update the rendered Adaptive Card Tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="57fd2-150">次のコード スニペットは、要求と応答 `tab/submit` の例です。</span><span class="sxs-lookup"><span data-stu-id="57fd2-150">The following code snippets are examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="57fd2-151">**`tab/submit` 要求**</span><span class="sxs-lookup"><span data-stu-id="57fd2-151">**`tab/submit` request**</span></span>

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

<span data-ttu-id="57fd2-152">**`tab/submit` 応答**</span><span class="sxs-lookup"><span data-stu-id="57fd2-152">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="57fd2-153">タスク モジュールのワークフローについて</span><span class="sxs-lookup"><span data-stu-id="57fd2-153">Understand task module workflow</span></span>

<span data-ttu-id="57fd2-154">また、タスク モジュールはアダプティブ カードを使用して呼 `task/fetch` び出し `task/submit` 、要求と応答を行います。</span><span class="sxs-lookup"><span data-stu-id="57fd2-154">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="57fd2-155">詳細については、「タスク ボット[でのタスク モジュールの使用Microsoft Teams参照してください](../../task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="57fd2-155">For more information, see [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="57fd2-156">ただし、[アダプティブ カード] タブの導入により、ボットが要求に応答する方法が変 `task/submit` わります。</span><span class="sxs-lookup"><span data-stu-id="57fd2-156">However, with the introduction of Adaptive Card Tab there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="57fd2-157">アダプティブ カード タブを使用している場合、ボットは標準タブで呼び出し要求に応答し、応答を続行し、タスク モジュール `task/submit` を閉じます。 </span><span class="sxs-lookup"><span data-stu-id="57fd2-157">If you are using an Adaptive Card Tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="57fd2-158">アダプティブ カード タブは、タブで提供されるカードの新しいリストをレンダリングして、応答本文 **を** 続行することで更新されます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-158">The Adaptive Card Tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="57fd2-159">Invoke `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="57fd2-159">Invoke `task/fetch`</span></span>

<span data-ttu-id="57fd2-160">次のコード スニペットは、要求と応答 `task/fetch` の例です。</span><span class="sxs-lookup"><span data-stu-id="57fd2-160">The following code snippets are examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="57fd2-161">**`task/fetch` 要求**</span><span class="sxs-lookup"><span data-stu-id="57fd2-161">**`task/fetch` request**</span></span>
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

<span data-ttu-id="57fd2-162">**`task/fetch` 応答**</span><span class="sxs-lookup"><span data-stu-id="57fd2-162">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="57fd2-163">Invoke `task/submit`</span><span class="sxs-lookup"><span data-stu-id="57fd2-163">Invoke `task/submit`</span></span>

<span data-ttu-id="57fd2-164">次のコード スニペットは、要求と応答 `task/submit` の例です。</span><span class="sxs-lookup"><span data-stu-id="57fd2-164">The following code snippets are examples of `task/submit` request and response:</span></span>

<span data-ttu-id="57fd2-165">**`task/submit` 要求**</span><span class="sxs-lookup"><span data-stu-id="57fd2-165">**`task/submit` request**</span></span>

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

<span data-ttu-id="57fd2-166">**`task/submit` tab 応答の種類**</span><span class="sxs-lookup"><span data-stu-id="57fd2-166">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="57fd2-167">認証</span><span class="sxs-lookup"><span data-stu-id="57fd2-167">Authentication</span></span>

<span data-ttu-id="57fd2-168">この記事の前のセクションでは、開発のパラダイムのほとんどがタスク モジュールの要求と応答からタブ要求と応答に外に出される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="57fd2-168">In the previous sections of this article, you have seen that most of the development paradigms could be extrapolated from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="57fd2-169">ただし、認証の処理に関しては、アダプティブ カード タブのワークフローはメッセージング拡張機能の認証パターンに従います。</span><span class="sxs-lookup"><span data-stu-id="57fd2-169">However, when it comes to handling authentication, the workflow for Adaptive Card Tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="57fd2-170">詳細については、「認証の追加 [」を参照してください](../../messaging-extensions/how-to/add-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="57fd2-170">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span> 

<span data-ttu-id="57fd2-171">[呼 [び出しアクティビティ](#invoke-activities)] セクションでは、要求に続行応答または認証応答を持つ可能性がある `tab/fetch` **という通知が表示** されました。 </span><span class="sxs-lookup"><span data-stu-id="57fd2-171">In the [invoke activities](#invoke-activities) section, you were informed that `tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="57fd2-172">要求が `tab/fetch` トリガーされ、タブ **認証** 応答を受信すると、サインイン ページがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-172">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span> 

<span data-ttu-id="57fd2-173">**呼び出しを使用して認証コードを取得 `tab/fetch` するには**</span><span class="sxs-lookup"><span data-stu-id="57fd2-173">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="57fd2-174">アプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-174">Open your app.</span></span> <span data-ttu-id="57fd2-175">サインイン ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-175">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="57fd2-176">アプリ のロゴは、アプリ マニフェストで定義されたプロパティを介して提供され、タブ認証応答本文で返されるプロパティでロゴが定義された後に表示されるタイトルが `icon` `title` 提供されます。 </span><span class="sxs-lookup"><span data-stu-id="57fd2-176">The app logo is provided through the `icon` property defined in the app manifest, and the title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="57fd2-177">**[サインイン]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-177">Select **Sign in**.</span></span> <span data-ttu-id="57fd2-178">認証応答本文のプロパティに指定された認証 URL `value` **に** リダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-178">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span> 
1. <span data-ttu-id="57fd2-179">ポップアップ ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-179">A pop-up window appears.</span></span> <span data-ttu-id="57fd2-180">このポップアップ ウィンドウは、認証 URL を使用して Web ページをホストします。</span><span class="sxs-lookup"><span data-stu-id="57fd2-180">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="57fd2-181">サインインした後、ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-181">After you sign in, close the window.</span></span> <span data-ttu-id="57fd2-182">認証 *コードが* クライアントにTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="57fd2-182">An *authentication code* is sent to the Teams client.</span></span>
1. <span data-ttu-id="57fd2-183">次Teamsクライアントは、ホストされた Web ページによって提供される認証コードを含む、サービスへの要求 `tab/fetch` を再発行します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-183">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span> 

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="57fd2-184">`tab/fetch` 認証データ フロー</span><span class="sxs-lookup"><span data-stu-id="57fd2-184">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="57fd2-185">次の図は、呼び出しに対する認証データ フローの動作の概要を示 `tab/fetch` しています。</span><span class="sxs-lookup"><span data-stu-id="57fd2-185">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="アダプティブ カード タブ認証フローの例。" border="false":::

<span data-ttu-id="57fd2-187">**`tab/fetch` 認証応答**</span><span class="sxs-lookup"><span data-stu-id="57fd2-187">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="57fd2-188">次のコード スニペットは、認証応答 `tab/fetch` の例です。</span><span class="sxs-lookup"><span data-stu-id="57fd2-188">The following code snippet is an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="57fd2-189">例</span><span class="sxs-lookup"><span data-stu-id="57fd2-189">Example</span></span>

<span data-ttu-id="57fd2-190">次に、再発行された要求の例を示します。</span><span class="sxs-lookup"><span data-stu-id="57fd2-190">The following shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="57fd2-191">関連項目</span><span class="sxs-lookup"><span data-stu-id="57fd2-191">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57fd2-192">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="57fd2-192">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)

