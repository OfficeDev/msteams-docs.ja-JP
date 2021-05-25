---
title: タブリンクの分岐解除とステージ ビュー
author: Rajeshwari-v
description: リンクのリンクを解除し、ステージ ビューを開き、アプリでタブをピン留Microsoft Teamsします。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 7dfabfa58c49237e776af37a1ee40d707783d0dc
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631346"
---
# <a name="tabs-link-unfurling-and-stage-view"></a><span data-ttu-id="af6d2-103">タブリンクの分岐解除とステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="af6d2-103">Tabs link unfurling and Stage View</span></span>

> [!NOTE]
> <span data-ttu-id="af6d2-104">この機能は、パブリック開発者 [プレビューでのみ使用](../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-104">This feature is available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="af6d2-105">ステージ ビューは、新しい UI コンポーネントであり、このコンポーネントを使用すると、タブとして固定され、Teams画面で開いているコンテンツをレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-105">Stage View is a new UI component, which allows you to render the content that is opened in full screen in Teams and pinned as a tab.</span></span>
 
> [!NOTE]
> <span data-ttu-id="af6d2-106">現時点では、Teamsクライアントはサポート タブリンクを開き、ステージ ビューをリンクしません。</span><span class="sxs-lookup"><span data-stu-id="af6d2-106">Currently, Teams mobile clients do no support tabs link unfurling and Stage View.</span></span> <span data-ttu-id="af6d2-107">モバイル クライアントは、 `websiteUrl` 開発者が提供する属性を使用して、デバイスの Web ブラウザーでページを開きます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-107">Mobile clients use the `websiteUrl` attribute provided by the developer to open the page in the device's web browser.</span></span>

## <a name="stage-view"></a><span data-ttu-id="af6d2-108">ステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="af6d2-108">Stage View</span></span>

<span data-ttu-id="af6d2-109">ステージ ビューは、Web コンテンツを表示するために呼び出すフルスクリーン UI コンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="af6d2-109">Stage View is a full screen UI component that you can invoke to surface your web content.</span></span> <span data-ttu-id="af6d2-110">既存のリンク解除サービスが更新され、アダプティブ カードとチャット サービスを使用して URL をタブに変換するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-110">The existing link unfurling service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="af6d2-111">ユーザーがチャットまたはチャネルで URL を送信すると、その URL はアダプティブ カードにリンク解除されます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-111">When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card.</span></span> <span data-ttu-id="af6d2-112">ユーザーはカードで **[表示]** を選択し、ステージ ビューから直接コンテンツをタブとしてピン留めできます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-112">The user can select **View** in the card, and pin the content as a tab directly from the Stage View.</span></span>

## <a name="advantage-of-stage-view"></a><span data-ttu-id="af6d2-113">ステージ ビューの利点</span><span class="sxs-lookup"><span data-stu-id="af6d2-113">Advantage of Stage View</span></span>

<span data-ttu-id="af6d2-114">ステージ ビューを使用すると、コンテンツを表示するエクスペリエンスをシームレスにTeams。</span><span class="sxs-lookup"><span data-stu-id="af6d2-114">Stage View helps provide a more seamless experience of viewing content in Teams.</span></span> <span data-ttu-id="af6d2-115">ユーザーは、コンテキストを離れることなくアプリが提供するコンテンツを開いて表示し、コンテンツをチャットまたはチャネルにピン留めして、将来の迅速なアクセスを可能にできます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-115">Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access.</span></span> <span data-ttu-id="af6d2-116">これにより、アプリとのユーザーエンゲージメントが向上します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-116">This leads to a higher user engagement with your app.</span></span>

##  <a name="stage-view-vs-task-module"></a><span data-ttu-id="af6d2-117">ステージ ビューとタスク モジュール</span><span class="sxs-lookup"><span data-stu-id="af6d2-117">Stage View vs. Task module</span></span>

|<span data-ttu-id="af6d2-118">ステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="af6d2-118">Stage View</span></span>|<span data-ttu-id="af6d2-119">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="af6d2-119">Task module</span></span>|
|:-----------|:-----------|
|<span data-ttu-id="af6d2-120">ステージ ビューは、ページ、ダッシュボード、ファイルなど、ユーザーに表示するリッチ コンテンツがある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="af6d2-120">Stage View is useful when you have a rich content to display to the users, such as a page, a dashboard, a file, and so on.</span></span> <span data-ttu-id="af6d2-121">これは、フルスクリーンキャンバスでコンテンツをレンダリングするのに役立つ最大の不動産を提供します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-121">It provides  maximum real estate that helps to render your content in the full-screen canvas.</span></span>|<span data-ttu-id="af6d2-122">[タスク モジュールは](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、ユーザーの注意が必要なメッセージを表示したり、次の手順に進むのに必要な情報を収集したりするために特に便利です。</span><span class="sxs-lookup"><span data-stu-id="af6d2-122">[Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that requires user's attention, or collect information required to move to the next step.</span></span>|
  
## <a name="invoke-the-stage-view"></a><span data-ttu-id="af6d2-123">ステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="af6d2-123">Invoke the Stage View</span></span>

<span data-ttu-id="af6d2-124">ステージ ビューは、次の方法で呼び出します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-124">You can invoke the Stage View in the following  ways:</span></span> 

* [<span data-ttu-id="af6d2-125">アダプティブ カードからステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="af6d2-125">Invoke Stage View from Adaptive Card</span></span>](#invoke-stage-view-from-adaptive-card)
* [<span data-ttu-id="af6d2-126">深いリンクを介してステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="af6d2-126">Invoke Stage View through deep link</span></span>](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a><span data-ttu-id="af6d2-127">アダプティブ カードからステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="af6d2-127">Invoke Stage View from Adaptive Card</span></span>

<span data-ttu-id="af6d2-128">ユーザーが Teams デスクトップ クライアントで URL を入力すると、ボットが呼び出され、ステージ[](../task-modules-and-cards/cards/cards-actions.md)内で URL を開くオプションを持つアダプティブ カードが返されます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-128">When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage.</span></span> <span data-ttu-id="af6d2-129">ステージが起動して渡された後、ステージをタブとしてピン留 `tabInfo` めする機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-129">After a stage is launched and the `tabInfo` is passed in, you can add the ability to pin the stage as a tab.</span></span>  

<span data-ttu-id="af6d2-130">次の画像は、アダプティブ カードから開いたステージを表示します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-130">The following images display a stage opened from an Adaptive Card:</span></span>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="400"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="400"/>

### <a name="example"></a><span data-ttu-id="af6d2-131">例</span><span class="sxs-lookup"><span data-stu-id="af6d2-131">Example</span></span> 

<span data-ttu-id="af6d2-132">アダプティブ カードからステージを開くコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-132">Following is the code to open a stage from an Adaptive Card:</span></span>

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

<span data-ttu-id="af6d2-133">要求 `invoke` の種類は、 である必要があります `composeExtension/queryLink` 。</span><span class="sxs-lookup"><span data-stu-id="af6d2-133">The `invoke` request type must be `composeExtension/queryLink`.</span></span> 

> [!NOTE]
> * <span data-ttu-id="af6d2-134">`invoke` ワークフローは、現在のワークフローと似 `appLinking` ています。</span><span class="sxs-lookup"><span data-stu-id="af6d2-134">`invoke` workflow is similar to the current `appLinking` workflow.</span></span> 
> * <span data-ttu-id="af6d2-135">一貫性を保つには、 という名前を付けをおすすめします `Action.Submit` `View` 。</span><span class="sxs-lookup"><span data-stu-id="af6d2-135">To maintain consistency, it is recommended to name the `Action.Submit` as `View`.</span></span>
> * <span data-ttu-id="af6d2-136">`websiteUrl` は、オブジェクトに渡す必要があるプロパティ `TabInfo` です。</span><span class="sxs-lookup"><span data-stu-id="af6d2-136">`websiteUrl` is a required property to be passed in the `TabInfo` object.</span></span>

<span data-ttu-id="af6d2-137">**ステージ ビューを呼び出すプロセス**</span><span class="sxs-lookup"><span data-stu-id="af6d2-137">**Process to invoke Stage View**</span></span>

1. <span data-ttu-id="af6d2-138">ユーザーが [表示] を **選択すると**、ボットは要求を受け取 `invoke` ります。</span><span class="sxs-lookup"><span data-stu-id="af6d2-138">When the user selects **View**, the bot receives an `invoke` request.</span></span> <span data-ttu-id="af6d2-139">要求の種類はです `composeExtension/queryLink` 。</span><span class="sxs-lookup"><span data-stu-id="af6d2-139">The request type is `composeExtension/queryLink`.</span></span>
1. <span data-ttu-id="af6d2-140">`invoke` ボットからの応答には、型が含まれるアダプティブ カード `tab/tabInfoAction` が含まれる。</span><span class="sxs-lookup"><span data-stu-id="af6d2-140">`invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.</span></span>
1. <span data-ttu-id="af6d2-141">ボットはコードで応答 `200` します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-141">The bot responds with a `200` code.</span></span>

> [!NOTE]
> <span data-ttu-id="af6d2-142">現在、Teamsクライアントはステージ ビュー機能をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="af6d2-142">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="af6d2-143">ユーザーがモバイル クライアント **で [表示** ] を選択すると、ユーザーはデバイスのブラウザーに移動されます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-143">When a user selects **View** on a mobile client, the user is taken to the device's browser.</span></span> <span data-ttu-id="af6d2-144">ブラウザーは、オブジェクトのパラメーターで指定 `websiteUrl` された URL を開 `TabInfo` きます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-144">The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.</span></span>

## <a name="invoke-stage-view-through-deep-link"></a><span data-ttu-id="af6d2-145">深いリンクを介してステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="af6d2-145">Invoke Stage View through deep link</span></span>

<span data-ttu-id="af6d2-146">タブからディープ リンクを介してステージ ビューを呼び出す場合は、API でディープ リンク URL をラップする必要 `microsoftTeams.executeDeeplink(url)` があります。</span><span class="sxs-lookup"><span data-stu-id="af6d2-146">To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `microsoftTeams.executeDeeplink(url)` API.</span></span> <span data-ttu-id="af6d2-147">ディープリンクは、カード内の `OpenURL` アクションを介して渡される場合があります。</span><span class="sxs-lookup"><span data-stu-id="af6d2-147">The deeplink can also be passed through an `OpenURL` action in the card.</span></span>

<span data-ttu-id="af6d2-148">次の図は、ディープ リンクを介して呼び出されるステージ ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-148">The following image displays a Stage View invoked through a deep link:</span></span>

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a><span data-ttu-id="af6d2-149">構文</span><span class="sxs-lookup"><span data-stu-id="af6d2-149">Syntax</span></span> 

<span data-ttu-id="af6d2-150">ディープリンク構文を次に示します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-150">Following is the deeplink syntax:</span></span>  
 
<span data-ttu-id="af6d2-151"> https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":""[contentUrl]","websiteUrl":"[websiteUrl]","name":"[name]"}</span><span class="sxs-lookup"><span data-stu-id="af6d2-151">https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”:”[contentUrl]”,“websiteUrl”:”[websiteUrl]”,“name”:”[name]”}</span></span>

### <a name="examples"></a><span data-ttu-id="af6d2-152">例</span><span class="sxs-lookup"><span data-stu-id="af6d2-152">Examples</span></span>

<span data-ttu-id="af6d2-153">ユーザーが URL を入力すると、アダプティブ カードにリンク解除されます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-153">When a user enters a URL, it is unfurled into an Adaptive card.</span></span>
<span data-ttu-id="af6d2-154">ステージ ビューを呼び出すディープ リンクの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-154">Following are the deep link examples to invoke the Stage View:</span></span>

<span data-ttu-id="af6d2-155">**例 1**</span><span class="sxs-lookup"><span data-stu-id="af6d2-155">**Example 1**</span></span>

<span data-ttu-id="af6d2-156"> https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="af6d2-156">https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

<span data-ttu-id="af6d2-157">**例 2**</span><span class="sxs-lookup"><span data-stu-id="af6d2-157">**Example 2**</span></span>

<span data-ttu-id="af6d2-158"> https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="af6d2-158">https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

> [!NOTE]
> * <span data-ttu-id="af6d2-159">ディープ `name` リンクではオプションです。</span><span class="sxs-lookup"><span data-stu-id="af6d2-159">The `name` is optional in deep link.</span></span> <span data-ttu-id="af6d2-160">含まれていない場合は、アプリ名が置き換わります。</span><span class="sxs-lookup"><span data-stu-id="af6d2-160">If not included, the app name replaces it.</span></span> 
> * <span data-ttu-id="af6d2-161">ディープ リンクは、アクションを介して渡 `OpenURL` される場合があります。</span><span class="sxs-lookup"><span data-stu-id="af6d2-161">The deep link can also be passed through  an `OpenURL` action.</span></span>
> * <span data-ttu-id="af6d2-162">現在、Teamsクライアントはステージ ビュー機能をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="af6d2-162">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="af6d2-163">ユーザーがステージ ビューへのディープ リンクを選択すると、デバイスの Web ブラウザーにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="af6d2-163">When users selects a deep link to a Stage View, they are taken to their device's web browser.</span></span> <span data-ttu-id="af6d2-164">Web ブラウザーは、ディープ リンクのパラメーターで指定された URL `websiteUrl` を開きます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-164">The web browser opens the URL specified in the `websiteUrl` parameter of the deep link.</span></span>
> * <span data-ttu-id="af6d2-165">特定のコンテキストからステージを起動する場合は、そのコンテキストでアプリが動作します。</span><span class="sxs-lookup"><span data-stu-id="af6d2-165">When you launch a Stage from a certain context, ensure that your app works in that context.</span></span> <span data-ttu-id="af6d2-166">たとえば、個人用アプリからステージ ビューを起動する場合は、アプリに個人用スコープが設定されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="af6d2-166">For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.</span></span>

## <a name="tab-information-property"></a><span data-ttu-id="af6d2-167">タブ情報プロパティ</span><span class="sxs-lookup"><span data-stu-id="af6d2-167">Tab information property</span></span>

| <span data-ttu-id="af6d2-168">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="af6d2-168">Property name</span></span> | <span data-ttu-id="af6d2-169">種類</span><span class="sxs-lookup"><span data-stu-id="af6d2-169">Type</span></span> | <span data-ttu-id="af6d2-170">文字数</span><span class="sxs-lookup"><span data-stu-id="af6d2-170">Number of characters</span></span> | <span data-ttu-id="af6d2-171">説明</span><span class="sxs-lookup"><span data-stu-id="af6d2-171">Description</span></span> |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | <span data-ttu-id="af6d2-172">String</span><span class="sxs-lookup"><span data-stu-id="af6d2-172">String</span></span> | <span data-ttu-id="af6d2-173">64</span><span class="sxs-lookup"><span data-stu-id="af6d2-173">64</span></span> | <span data-ttu-id="af6d2-174">このプロパティは、タブが表示されるエンティティの一意の識別子です。</span><span class="sxs-lookup"><span data-stu-id="af6d2-174">This property is a  unique identifier for the entity that the tab displays.</span></span> <span data-ttu-id="af6d2-175">これは必須フィールドです。</span><span class="sxs-lookup"><span data-stu-id="af6d2-175">This is a required field.</span></span>|
| `name` | <span data-ttu-id="af6d2-176">String</span><span class="sxs-lookup"><span data-stu-id="af6d2-176">String</span></span> | <span data-ttu-id="af6d2-177">128</span><span class="sxs-lookup"><span data-stu-id="af6d2-177">128</span></span> | <span data-ttu-id="af6d2-178">このプロパティは、チャネル インターフェイスのタブの表示名です。</span><span class="sxs-lookup"><span data-stu-id="af6d2-178">This property is the display name of the tab in the channel interface.</span></span> <span data-ttu-id="af6d2-179">この入力フィールドは省略できます。</span><span class="sxs-lookup"><span data-stu-id="af6d2-179">This is an optional field.</span></span>|
| `contentUrl` | <span data-ttu-id="af6d2-180">String</span><span class="sxs-lookup"><span data-stu-id="af6d2-180">String</span></span> | <span data-ttu-id="af6d2-181">2048</span><span class="sxs-lookup"><span data-stu-id="af6d2-181">2048</span></span> | <span data-ttu-id="af6d2-182">このプロパティは、https:// キャンバスに表示するエンティティ UI をポイントするTeamsです。</span><span class="sxs-lookup"><span data-stu-id="af6d2-182">This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span> <span data-ttu-id="af6d2-183">これは必須フィールドです。</span><span class="sxs-lookup"><span data-stu-id="af6d2-183">This is a required field.</span></span>|
| `websiteUrl?` | <span data-ttu-id="af6d2-184">String</span><span class="sxs-lookup"><span data-stu-id="af6d2-184">String</span></span> | <span data-ttu-id="af6d2-185">2048</span><span class="sxs-lookup"><span data-stu-id="af6d2-185">2048</span></span> | <span data-ttu-id="af6d2-186">ユーザーがブラウザーで表示 https:// 場合、このプロパティは参照先の URL です。</span><span class="sxs-lookup"><span data-stu-id="af6d2-186">This property is the https:// URL to point at, if a user selects to view in a browser.</span></span> <span data-ttu-id="af6d2-187">これは必須フィールドです。</span><span class="sxs-lookup"><span data-stu-id="af6d2-187">This is a required field.</span></span>|
| `removeUrl?` | <span data-ttu-id="af6d2-188">String</span><span class="sxs-lookup"><span data-stu-id="af6d2-188">String</span></span> | <span data-ttu-id="af6d2-189">2048</span><span class="sxs-lookup"><span data-stu-id="af6d2-189">2048</span></span> | <span data-ttu-id="af6d2-190">このプロパティは、https:// を削除するときに表示される UI を示す URL です。これはオプションのフィールドです。</span><span class="sxs-lookup"><span data-stu-id="af6d2-190">This property is the https:// URL that points to the UI to be displayed when the user deletes the tab. This is an optional field.</span></span>|

## <a name="see-also"></a><span data-ttu-id="af6d2-191">関連項目</span><span class="sxs-lookup"><span data-stu-id="af6d2-191">See also</span></span>

[<span data-ttu-id="af6d2-192">メッセージング拡張機能リンクの分岐解除</span><span class="sxs-lookup"><span data-stu-id="af6d2-192">Messaging extensions link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)


