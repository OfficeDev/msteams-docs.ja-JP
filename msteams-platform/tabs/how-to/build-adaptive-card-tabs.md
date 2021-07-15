---
title: アダプティブ カード タブの作成
author: KirtiPereira
description: アダプティブ カードを使用してタブを作成する
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: aaa6ae00e4a70ea27c27638ed9475bc7edec25da
ms.sourcegitcommit: e327c9766dfa05abb468cdc71319e3cba7c6c79f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2021
ms.locfileid: "53428717"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="7c769-103">アダプティブ カードを使用してタブをビルドする</span><span class="sxs-lookup"><span data-stu-id="7c769-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7c769-104">この機能はパブリック [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) デスクトップとモバイルでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7c769-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="7c769-105">Web ブラウザーでのサポートは近日公開予定です。</span><span class="sxs-lookup"><span data-stu-id="7c769-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="7c769-106">アダプティブ カード付きタブは現在、個人用アプリとしてのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7c769-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="7c769-107">従来の方法を使用してタブを開発する場合、HTML と CSS の考慮事項、読み込み時間の遅れ、iFrame の制約、サーバーのメンテナンスとコストなど、これらの問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7c769-107">When developing a tab using the traditional method, you might run into these issues, such as HTML and CSS considerations, slow load times, iFrame constraints, and server maintenance and costs.</span></span> <span data-ttu-id="7c769-108">アダプティブ カード タブは、新しい方法でタブを作成Teams。</span><span class="sxs-lookup"><span data-stu-id="7c769-108">Adaptive Card tabs is a new way to build tabs in Teams.</span></span> <span data-ttu-id="7c769-109">IFrame に Web コンテンツを埋め込む代わりに、アダプティブ カードをタブにレンダリングできます。フロントエンドはアダプティブ カードでレンダリングされる一方で、バックエンドの電源はボットによって行います。</span><span class="sxs-lookup"><span data-stu-id="7c769-109">Instead of embedding web content in an IFrame, you can render Adaptive Cards to a tab. While the front-end is rendered with Adaptive Cards, the backend is powered by a bot.</span></span> <span data-ttu-id="7c769-110">ボットは、要求を受け入れ、レンダリングされるアダプティブ カードで適切に応答する責任があります。</span><span class="sxs-lookup"><span data-stu-id="7c769-110">The bot is responsible for accepting requests and responding appropriately with the Adaptive Card that is rendered.</span></span>

<span data-ttu-id="7c769-111">デスクトップ、Web、モバイルでネイティブに見える既製のユーザー インターフェイス (UI) 構成要素を使用してタブを構築できます。</span><span class="sxs-lookup"><span data-stu-id="7c769-111">You can build your tabs with ready-made user interface (UI) building blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="7c769-112">この記事では、アプリ マニフェストに対して行う必要がある変更、アクティビティの呼び出しがアダプティブ カードを使用してタブで情報を要求および送信する方法、およびタスク モジュールワークフローへの影響を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7c769-112">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span>

<span data-ttu-id="7c769-113">次の図は、デスクトップとモバイルのアダプティブ カードを含むビルド タブを示しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-113">The following image depicts build tabs with Adaptive Cards in desktop and mobile:</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="タブでレンダリングされるアダプティブ カードの例。" border="false":::

## <a name="prerequisites"></a><span data-ttu-id="7c769-115">前提条件</span><span class="sxs-lookup"><span data-stu-id="7c769-115">Prerequisites</span></span>

<span data-ttu-id="7c769-116">アダプティブ カードを使用してタブを作成する前に、次の条件を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c769-116">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="7c769-117">ボット開発、[アダプティブ カード](../../bots/what-are-bots.md)、[および](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)タスク モジュール[](../../task-modules-and-cards/task-modules/task-modules-bots.md)に精通Teams。</span><span class="sxs-lookup"><span data-stu-id="7c769-117">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [task modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="7c769-118">開発に必要なTeamsボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="7c769-118">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="7c769-119">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7c769-119">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="7c769-120">アプリ マニフェストの変更点</span><span class="sxs-lookup"><span data-stu-id="7c769-120">Changes to app manifest</span></span>

<span data-ttu-id="7c769-121">タブをレンダリングする個人用アプリには、アプリ マニフェスト `staticTabs` に配列を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c769-121">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="7c769-122">アダプティブ カード タブは、プロパティが `contentBotId` 定義で提供されている場合に表示 `staticTab` されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-122">Adaptive Card tabs are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="7c769-123">静的タブ定義には、アダプティブ カード タブを指定する 、またはホストされる一般的な Web コンテンツ タブ エクスペリエンスを指定する 、 のいずれかを `contentBotId` `contentUrl` 含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c769-123">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="7c769-124">この `contentBotId` プロパティは現在、マニフェスト バージョン 1.9 以降で使用できます。</span><span class="sxs-lookup"><span data-stu-id="7c769-124">The `contentBotId` property is currently available in manifest version 1.9 or later.</span></span>

<span data-ttu-id="7c769-125">[アダプティブ `contentBotId` カード] タブが `botId` 通信する必要があるプロパティを指定します。</span><span class="sxs-lookup"><span data-stu-id="7c769-125">Provide the `contentBotId` property with the `botId` that the Adaptive Card tab must communicate with.</span></span> <span data-ttu-id="7c769-126">[アダプティブ カード] タブ用に構成された設定は、各呼び出し要求のパラメーターに送信され、同じボットを使用するアダプティブ カード タブを `entityId` `tabContext` 区別するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="7c769-126">The `entityId` configured for the Adaptive Card tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="7c769-127">その他の静的タブ定義フィールドの詳細については、「マニフェスト スキーマ」 [を参照してください](../../resources/schema/manifest-schema.md#statictabs)。</span><span class="sxs-lookup"><span data-stu-id="7c769-127">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="7c769-128">アダプティブ カード タブ マニフェストの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="7c769-128">Following is a sample Adaptive Card tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="7c769-129">アクティビティの呼び出し</span><span class="sxs-lookup"><span data-stu-id="7c769-129">Invoke activities</span></span>

<span data-ttu-id="7c769-130">アダプティブ カード タブとボット間の通信は、アクティビティを通じて行 `invoke` われます。</span><span class="sxs-lookup"><span data-stu-id="7c769-130">Communication between your Adaptive Card tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="7c769-131">各 `invoke` アクティビティには、対応する名前 **があります**。</span><span class="sxs-lookup"><span data-stu-id="7c769-131">Each `invoke` activity has a corresponding **name**.</span></span> <span data-ttu-id="7c769-132">各要求を区別するには、各アクティビティの名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="7c769-132">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="7c769-133">`tab/fetch` この `tab/submit` セクションで説明するアクティビティを示します。</span><span class="sxs-lookup"><span data-stu-id="7c769-133">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="7c769-134">ボットはサービス URL に対してすべての応答を [送信する必要があります](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7c769-134">Bots need to send all the responses to [service URL](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true).</span></span> <span data-ttu-id="7c769-135">サービス URL は、受信ペイロードの一部として受信 `activity` されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-135">Service URL is received as part of incoming `activity` payload.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="7c769-136">タブにレンダリングするアダプティブ カードのフェッチ</span><span class="sxs-lookup"><span data-stu-id="7c769-136">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="7c769-137">`tab/fetch`は、ユーザーがアダプティブ カード タブを開いたときにボットが受け取る最初の呼び出し要求です。ボットが要求を受信すると、タブ続行応答またはタブ **認証応答が送信** されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-137">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card tab. When your bot receives the request, it either sends a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="7c769-138">継続 **応答** には、カードの配列 **が含** まれます。これは、配列の順序でタブに垂直にレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="7c769-138">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="7c769-139">認証応答の詳細 **については、「認証** 」を [参照してください](#authentication)。</span><span class="sxs-lookup"><span data-stu-id="7c769-139">For more information on **auth** response, see [authentication](#authentication).</span></span>

<span data-ttu-id="7c769-140">次のコードは、要求と応答 `tab/fetch` の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-140">The following code provides examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="7c769-141">**`tab/fetch` 要求**</span><span class="sxs-lookup"><span data-stu-id="7c769-141">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="7c769-142">**`tab/fetch` 応答**</span><span class="sxs-lookup"><span data-stu-id="7c769-142">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="7c769-143">アダプティブ カードからの送信の処理</span><span class="sxs-lookup"><span data-stu-id="7c769-143">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="7c769-144">タブでアダプティブ カードがレンダリングされた後、ユーザーの操作に応答できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c769-144">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="7c769-145">この応答は、呼び出し要求 `tab/submit` によって処理されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-145">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="7c769-146">ユーザーが [アダプティブ カード] タブのボタンを選択すると、アダプティブ カードの機能を使用して対応するデータを使用してボットに要求 `tab/submit` `Action.Submit` がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="7c769-146">When a user selects a button on the Adaptive Card tab, the `tab/submit` request is triggered to your bot with the corresponding data through the `Action.Submit` function of Adaptive Card.</span></span> <span data-ttu-id="7c769-147">アダプティブ カード データは、要求の data プロパティを使用して使用 `tab/submit` できます。</span><span class="sxs-lookup"><span data-stu-id="7c769-147">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="7c769-148">要求に対して次のいずれかの応答を受け取る。</span><span class="sxs-lookup"><span data-stu-id="7c769-148">You receive either of the following responses to your request:</span></span>

* <span data-ttu-id="7c769-149">本文がない HTTP `200` 状態コード応答。</span><span class="sxs-lookup"><span data-stu-id="7c769-149">An HTTP status code `200` response with no body.</span></span> <span data-ttu-id="7c769-150">空の 200 応答では、クライアントによって実行されるアクションはありません。</span><span class="sxs-lookup"><span data-stu-id="7c769-150">An empty 200 response results in no action taken by the client.</span></span>
* <span data-ttu-id="7c769-151">アダプティブ カードの `200` フェッチ **で説明** したように、標準タブは応答 [を続行します](#fetch-adaptive-card-to-render-to-a-tab)。</span><span class="sxs-lookup"><span data-stu-id="7c769-151">The standard `200` tab **continue** response, as explained in [fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab).</span></span> <span data-ttu-id="7c769-152">タブの **応答を** 続行すると、クライアントは、引き続き応答のカード配列に用意されているアダプティブ カードを使用して、レンダリングされたアダプティブ カード タブを **更新** します。</span><span class="sxs-lookup"><span data-stu-id="7c769-152">A tab **continue** response triggers the client to update the rendered Adaptive Card tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="7c769-153">次のコードは、要求と応答 `tab/submit` の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-153">The following code provides examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="7c769-154">**`tab/submit` 要求**</span><span class="sxs-lookup"><span data-stu-id="7c769-154">**`tab/submit` request**</span></span>

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

<span data-ttu-id="7c769-155">**`tab/submit` 応答**</span><span class="sxs-lookup"><span data-stu-id="7c769-155">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="7c769-156">タスク モジュールのワークフローについて</span><span class="sxs-lookup"><span data-stu-id="7c769-156">Understand task module workflow</span></span>

<span data-ttu-id="7c769-157">また、タスク モジュールはアダプティブ カードを使用して呼 `task/fetch` び出し `task/submit` 、要求と応答を行います。</span><span class="sxs-lookup"><span data-stu-id="7c769-157">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="7c769-158">詳細については、「タスク ボット[でのタスク モジュールの使用Microsoft Teams参照してください](../../task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="7c769-158">For more information, see [using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="7c769-159">[アダプティブ カード] タブの導入により、ボットが要求に応答する方法が変 `task/submit` わります。</span><span class="sxs-lookup"><span data-stu-id="7c769-159">With the introduction of Adaptive Card tab, there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="7c769-160">アダプティブ カード タブを使用している場合、ボットは標準タブで呼び出し要求に応答し、応答を続行し、タスク モジュール `task/submit` を閉じます。 </span><span class="sxs-lookup"><span data-stu-id="7c769-160">If you are using an Adaptive Card tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="7c769-161">[アダプティブ カード] タブは、タブで提供される新しいカードの一覧を表示して、応答本文 **を** 続行することで更新されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-161">The Adaptive Card tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="7c769-162">Invoke `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="7c769-162">Invoke `task/fetch`</span></span>

<span data-ttu-id="7c769-163">次のコードは、要求と応答 `task/fetch` の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-163">The following code provides examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="7c769-164">**`task/fetch` 要求**</span><span class="sxs-lookup"><span data-stu-id="7c769-164">**`task/fetch` request**</span></span>
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

<span data-ttu-id="7c769-165">**`task/fetch` 応答**</span><span class="sxs-lookup"><span data-stu-id="7c769-165">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="7c769-166">Invoke `task/submit`</span><span class="sxs-lookup"><span data-stu-id="7c769-166">Invoke `task/submit`</span></span>

<span data-ttu-id="7c769-167">次のコードは、要求と応答 `task/submit` の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-167">The following code provides examples of `task/submit` request and response:</span></span>

<span data-ttu-id="7c769-168">**`task/submit` 要求**</span><span class="sxs-lookup"><span data-stu-id="7c769-168">**`task/submit` request**</span></span>

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

<span data-ttu-id="7c769-169">**`task/submit` tab 応答の種類**</span><span class="sxs-lookup"><span data-stu-id="7c769-169">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="7c769-170">認証</span><span class="sxs-lookup"><span data-stu-id="7c769-170">Authentication</span></span>

<span data-ttu-id="7c769-171">この記事の前のセクションでは、開発のパラダイムのほとんどをタスク モジュールの要求と応答からタブ要求と応答に拡張できます。</span><span class="sxs-lookup"><span data-stu-id="7c769-171">In the previous sections of this article, you have seen that most of the development paradigms can be extended from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="7c769-172">認証の処理に関しては、[アダプティブ カード] タブのワークフローは、メッセージング拡張機能の認証パターンに従います。</span><span class="sxs-lookup"><span data-stu-id="7c769-172">When it comes to handling authentication, the workflow for Adaptive Card tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="7c769-173">詳細については、「認証の追加 [」を参照してください](../../messaging-extensions/how-to/add-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="7c769-173">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span>

<span data-ttu-id="7c769-174">`tab/fetch`要求には、続行応答 **または\*\*\*\*認証応答を指定** できます。</span><span class="sxs-lookup"><span data-stu-id="7c769-174">`tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="7c769-175">要求が `tab/fetch` トリガーされ、タブ **認証** 応答を受信すると、サインイン ページがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-175">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span>

<span data-ttu-id="7c769-176">**呼び出しを使用して認証コードを取得 `tab/fetch` するには**</span><span class="sxs-lookup"><span data-stu-id="7c769-176">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="7c769-177">アプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="7c769-177">Open your app.</span></span> <span data-ttu-id="7c769-178">サインイン ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-178">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c769-179">アプリ のロゴは、アプリ マニフェスト `icon` で定義されているプロパティを使用して提供されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-179">The app logo is provided through the `icon` property defined in the app manifest.</span></span> <span data-ttu-id="7c769-180">タブ認証応答本文で返されるプロパティでロゴが定義された後に表示されるタイトル `title` 。 </span><span class="sxs-lookup"><span data-stu-id="7c769-180">The title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="7c769-181">**[サインイン]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="7c769-181">Select **Sign in**.</span></span> <span data-ttu-id="7c769-182">認証応答本文のプロパティに指定された認証 URL `value` **に** リダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="7c769-182">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span>
1. <span data-ttu-id="7c769-183">ポップアップ ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7c769-183">A pop-up window appears.</span></span> <span data-ttu-id="7c769-184">このポップアップ ウィンドウは、認証 URL を使用して Web ページをホストします。</span><span class="sxs-lookup"><span data-stu-id="7c769-184">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="7c769-185">サインインした後、ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="7c769-185">After you sign in, close the window.</span></span> <span data-ttu-id="7c769-186">認証 **コードが** クライアントにTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="7c769-186">An **authentication code** is sent to the Teams client.</span></span>
1. <span data-ttu-id="7c769-187">次Teamsクライアントは、ホストされた Web ページによって提供される認証コードを含む、サービスへの要求 `tab/fetch` を再発行します。</span><span class="sxs-lookup"><span data-stu-id="7c769-187">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span>

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="7c769-188">`tab/fetch` 認証データ フロー</span><span class="sxs-lookup"><span data-stu-id="7c769-188">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="7c769-189">次の図は、呼び出しに対する認証データ フローの動作の概要を示 `tab/fetch` しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-189">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="アダプティブ カード タブ認証フローの例。" border="false":::

<span data-ttu-id="7c769-191">**`tab/fetch` 認証応答**</span><span class="sxs-lookup"><span data-stu-id="7c769-191">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="7c769-192">次のコードは、認証応答の `tab/fetch` 例を示しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-192">The following code provides an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="7c769-193">例</span><span class="sxs-lookup"><span data-stu-id="7c769-193">Example</span></span>

<span data-ttu-id="7c769-194">次のコードは、再発行された要求の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="7c769-194">The following code shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7c769-195">関連項目</span><span class="sxs-lookup"><span data-stu-id="7c769-195">See also</span></span>

* [<span data-ttu-id="7c769-196">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="7c769-196">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [<span data-ttu-id="7c769-197">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="7c769-197">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="7c769-198">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="7c769-198">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="7c769-199">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="7c769-199">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="7c769-200">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="7c769-200">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="7c769-201">次の手順</span><span class="sxs-lookup"><span data-stu-id="7c769-201">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c769-202">タブのリンクの展開とステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="7c769-202">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
