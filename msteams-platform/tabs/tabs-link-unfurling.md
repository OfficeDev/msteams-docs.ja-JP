---
title: タブのリンクの展開とステージ ビュー
author: Rajeshwari-v
description: リンクのリンクを解除し、ステージ ビューを開き、アプリでタブをピン留Microsoft Teamsします。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 1495bba765d149d23156b136be85f39d07c2d94b
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140174"
---
# <a name="tabs-link-unfurling-and-stage-view"></a><span data-ttu-id="8c0d8-103">タブのリンクの展開とステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="8c0d8-103">Tabs link unfurling and Stage View</span></span>

> [!NOTE]
> <span data-ttu-id="8c0d8-104">この機能は、パブリック開発者 [プレビューでのみ使用](../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-104">This feature is available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="8c0d8-105">ステージ ビューは、新しいユーザー インターフェイス (UI) コンポーネントで、Teams で開き、タブとしてピン留めされたコンテンツをレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-105">Stage View is a new user interface (UI) component, which allows you to render the content that is opened in full screen in Teams and pinned as a tab.</span></span>
 
> [!NOTE]
> <span data-ttu-id="8c0d8-106">現時点では、Teamsクライアントはサポート タブリンクを開き、ステージ ビューをリンクしません。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-106">Currently, Teams mobile clients do no support tabs link unfurling and Stage View.</span></span> <span data-ttu-id="8c0d8-107">モバイル クライアントは、 `websiteUrl` 開発者が提供する属性を使用して、デバイスの Web ブラウザーでページを開きます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-107">Mobile clients use the `websiteUrl` attribute provided by the developer to open the page in the device's web browser.</span></span>

## <a name="stage-view"></a><span data-ttu-id="8c0d8-108">ステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="8c0d8-108">Stage View</span></span>

<span data-ttu-id="8c0d8-109">ステージ ビューは、Web コンテンツを表示するために呼び出すフルスクリーン UI コンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-109">Stage View is a full screen UI component that you can invoke to surface your web content.</span></span> <span data-ttu-id="8c0d8-110">既存のリンク解除サービスが更新され、アダプティブ カードとチャット サービスを使用して URL をタブに変換するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-110">The existing link unfurling service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="8c0d8-111">ユーザーがチャットまたはチャネルで URL を送信すると、その URL はアダプティブ カードにリンク解除されます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-111">When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card.</span></span> <span data-ttu-id="8c0d8-112">ユーザーは、カード **で [表示]** を選択し、ステージ ビューから直接タブとしてコンテンツをピン留めできます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-112">The user can select **View** in the card, and pin the content as a tab directly from Stage View.</span></span>

## <a name="advantage-of-stage-view"></a><span data-ttu-id="8c0d8-113">ステージ ビューの利点</span><span class="sxs-lookup"><span data-stu-id="8c0d8-113">Advantage of Stage View</span></span>

<span data-ttu-id="8c0d8-114">ステージ ビューを使用すると、コンテンツを表示するエクスペリエンスをシームレスにTeams。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-114">Stage View helps provide a more seamless experience of viewing content in Teams.</span></span> <span data-ttu-id="8c0d8-115">ユーザーは、コンテキストを離れることなくアプリが提供するコンテンツを開いて表示し、コンテンツをチャットまたはチャネルにピン留めして、将来の迅速なアクセスを可能にできます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-115">Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access.</span></span> <span data-ttu-id="8c0d8-116">これにより、アプリとのユーザーエンゲージメントが向上します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-116">This leads to a higher user engagement with your app.</span></span>

## <a name="stage-view-vs-task-module"></a><span data-ttu-id="8c0d8-117">ステージ ビューとタスク モジュール</span><span class="sxs-lookup"><span data-stu-id="8c0d8-117">Stage View vs. Task module</span></span>

|<span data-ttu-id="8c0d8-118">ステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="8c0d8-118">Stage View</span></span>|<span data-ttu-id="8c0d8-119">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="8c0d8-119">Task module</span></span>|
|:-----------|:-----------|
|<span data-ttu-id="8c0d8-120">ステージ ビューは、ページ、ダッシュボード、ファイルなど、ユーザーに表示するリッチ コンテンツがある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-120">Stage View is useful when you have rich content to display to the users, such as a page, a dashboard, a file, and so on.</span></span> <span data-ttu-id="8c0d8-121">コンテンツをフルスクリーン キャンバスでレンダリングするのに役立つ豊富な機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-121">It provides  rich features that helps to render your content in the full-screen canvas.</span></span>|<span data-ttu-id="8c0d8-122">[タスク モジュールは](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、ユーザーの注意が必要なメッセージを表示したり、次の手順に進むのに必要な情報を収集したりするために特に便利です。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-122">[Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that require user attention, or collect information required to move to the next step.</span></span>|
  
## <a name="invoke-stage-view"></a><span data-ttu-id="8c0d8-123">ステージ ビューの呼び出し</span><span class="sxs-lookup"><span data-stu-id="8c0d8-123">Invoke Stage View</span></span>

<span data-ttu-id="8c0d8-124">ステージ ビューは、次の方法で呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-124">You can invoke Stage View in the following  ways:</span></span>

* [<span data-ttu-id="8c0d8-125">アダプティブ カードからステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="8c0d8-125">Invoke Stage View from Adaptive Card</span></span>](#invoke-stage-view-from-adaptive-card)
* [<span data-ttu-id="8c0d8-126">深いリンクを介してステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="8c0d8-126">Invoke Stage View through deep link</span></span>](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a><span data-ttu-id="8c0d8-127">アダプティブ カードからステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="8c0d8-127">Invoke Stage View from Adaptive Card</span></span>

<span data-ttu-id="8c0d8-128">ユーザーが Teams デスクトップ クライアントで URL を入力すると、ボットが呼び出され、ステージ[](../task-modules-and-cards/cards/cards-actions.md)内で URL を開くオプションを持つアダプティブ カードが返されます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-128">When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage.</span></span> <span data-ttu-id="8c0d8-129">ステージを起動して指定した後、ステージをタブとしてピン留めする機能 `tabInfo` を追加できます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-129">After a stage is launched and the `tabInfo` is provided, you can add the ability to pin the stage as a tab.</span></span>  

<span data-ttu-id="8c0d8-130">次の画像は、アダプティブ カードから開いたステージを表示します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-130">The following images display a stage opened from an Adaptive Card:</span></span>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a><span data-ttu-id="8c0d8-131">例</span><span class="sxs-lookup"><span data-stu-id="8c0d8-131">Example</span></span>

<span data-ttu-id="8c0d8-132">アダプティブ カードからステージを開くコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-132">Following is the code to open a stage from an Adaptive Card:</span></span>

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

<span data-ttu-id="8c0d8-133">要求 `invoke` の種類は、 である必要があります `composeExtension/queryLink` 。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-133">The `invoke` request type must be `composeExtension/queryLink`.</span></span>

> [!NOTE]
> * <span data-ttu-id="8c0d8-134">`invoke` ワークフローは、現在のワークフローと似 `appLinking` ています。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-134">`invoke` workflow is similar to the current `appLinking` workflow.</span></span> 
> * <span data-ttu-id="8c0d8-135">一貫性を保つには、 という名前を付けをお `Action.Submit` 勧めします `View` 。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-135">To maintain consistency, it is recommended to name `Action.Submit` as `View`.</span></span>
> * <span data-ttu-id="8c0d8-136">`websiteUrl` は、オブジェクトに渡す必要があるプロパティ `TabInfo` です。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-136">`websiteUrl` is a required property to be passed in the `TabInfo` object.</span></span>

<span data-ttu-id="8c0d8-137">ステージ ビューを呼び出すプロセスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-137">Following is the process to invoke Stage View:</span></span>

* <span data-ttu-id="8c0d8-138">ユーザーが [表示] を **選択すると**、ボットは要求を受け取 `invoke` ります。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-138">When the user selects **View**, the bot receives an `invoke` request.</span></span> <span data-ttu-id="8c0d8-139">要求の種類はです `composeExtension/queryLink` 。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-139">The request type is `composeExtension/queryLink`.</span></span>
* <span data-ttu-id="8c0d8-140">`invoke` ボットからの応答には、型が含まれるアダプティブ カード `tab/tabInfoAction` が含まれる。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-140">`invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.</span></span>
* <span data-ttu-id="8c0d8-141">ボットはコードで応答 `200` します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-141">The bot responds with a `200` code.</span></span>

> [!NOTE]
> <span data-ttu-id="8c0d8-142">現在、Teamsクライアントはステージ ビュー機能をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-142">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="8c0d8-143">ユーザーがモバイル クライアント **で [表示** ] を選択すると、ユーザーはデバイスのブラウザーに移動されます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-143">When a user selects **View** on a mobile client, the user is taken to the device's browser.</span></span> <span data-ttu-id="8c0d8-144">ブラウザーは、オブジェクトのパラメーターで指定 `websiteUrl` された URL を開 `TabInfo` きます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-144">The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.</span></span>

## <a name="invoke-stage-view-through-deep-link"></a><span data-ttu-id="8c0d8-145">深いリンクを介してステージ ビューを呼び出す</span><span class="sxs-lookup"><span data-stu-id="8c0d8-145">Invoke Stage View through deep link</span></span>

<span data-ttu-id="8c0d8-146">タブからディープ リンクを介してステージ ビューを呼び出す場合は、API でディープ リンク URL をラップする必要 `microsoftTeams.executeDeeplink(url)` があります。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-146">To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `microsoftTeams.executeDeeplink(url)` API.</span></span> <span data-ttu-id="8c0d8-147">ディープ リンクは、カード内の `OpenURL` アクションを介して渡される場合があります。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-147">The deep link can also be passed through an `OpenURL` action in the card.</span></span>

<span data-ttu-id="8c0d8-148">次の図は、ディープ リンクを介して呼び出されるステージ ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-148">The following image displays a Stage View invoked through a deep link:</span></span>

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a><span data-ttu-id="8c0d8-149">構文</span><span class="sxs-lookup"><span data-stu-id="8c0d8-149">Syntax</span></span>

<span data-ttu-id="8c0d8-150">ディープリンク構文を次に示します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-150">Following is the deeplink syntax:</span></span>  
 
<span data-ttu-id="8c0d8-151"> https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":""[contentUrl]","websiteUrl":"[websiteUrl]","name":"[name]"}</span><span class="sxs-lookup"><span data-stu-id="8c0d8-151">https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”:”[contentUrl]”,“websiteUrl”:”[websiteUrl]”,“name”:”[name]”}</span></span>

### <a name="examples"></a><span data-ttu-id="8c0d8-152">例</span><span class="sxs-lookup"><span data-stu-id="8c0d8-152">Examples</span></span>

<span data-ttu-id="8c0d8-153">ユーザーが URL を入力すると、アダプティブ カードにリンク解除されます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-153">When a user enters a URL, it is unfurled into an Adaptive card.</span></span>

<span data-ttu-id="8c0d8-154">ステージ ビューを呼び出すディープ リンクの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-154">Following are the deep link examples to invoke Stage View:</span></span>

<span data-ttu-id="8c0d8-155">**例 1**</span><span class="sxs-lookup"><span data-stu-id="8c0d8-155">**Example 1**</span></span>

<span data-ttu-id="8c0d8-156"> https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="8c0d8-156">https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

<span data-ttu-id="8c0d8-157">**例 2**</span><span class="sxs-lookup"><span data-stu-id="8c0d8-157">**Example 2**</span></span>

<span data-ttu-id="8c0d8-158"> https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="8c0d8-158">https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

> [!NOTE]
> * <span data-ttu-id="8c0d8-159">ディープ `name` リンクではオプションです。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-159">The `name` is optional in deep link.</span></span> <span data-ttu-id="8c0d8-160">含まれていない場合は、アプリ名が置き換わります。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-160">If not included, the app name replaces it.</span></span>
> * <span data-ttu-id="8c0d8-161">ディープ リンクは、アクションを介して渡 `OpenURL` される場合があります。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-161">The deep link can also be passed through an `OpenURL` action.</span></span>
> * <span data-ttu-id="8c0d8-162">現在、Teamsクライアントはステージ ビュー機能をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-162">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="8c0d8-163">ユーザーがステージ ビューへのディープ リンクを選択すると、デバイスの Web ブラウザーにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-163">When users select a deep link to a Stage View, they are taken to their device's web browser.</span></span> <span data-ttu-id="8c0d8-164">Web ブラウザーは、ディープ リンクのパラメーターで指定された URL `websiteUrl` を開きます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-164">The web browser opens the URL specified in the `websiteUrl` parameter of the deep link.</span></span>
> * <span data-ttu-id="8c0d8-165">特定のコンテキストからステージを起動する場合は、そのコンテキストでアプリが動作します。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-165">When you launch a Stage from a certain context, ensure that your app works in that context.</span></span> <span data-ttu-id="8c0d8-166">たとえば、個人用アプリからステージ ビューを起動する場合は、アプリに個人用スコープが設定されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-166">For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.</span></span>

## <a name="tab-information-property"></a><span data-ttu-id="8c0d8-167">タブ情報プロパティ</span><span class="sxs-lookup"><span data-stu-id="8c0d8-167">Tab information property</span></span>

| <span data-ttu-id="8c0d8-168">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="8c0d8-168">Property name</span></span> | <span data-ttu-id="8c0d8-169">種類</span><span class="sxs-lookup"><span data-stu-id="8c0d8-169">Type</span></span> | <span data-ttu-id="8c0d8-170">文字数</span><span class="sxs-lookup"><span data-stu-id="8c0d8-170">Number of characters</span></span> | <span data-ttu-id="8c0d8-171">説明</span><span class="sxs-lookup"><span data-stu-id="8c0d8-171">Description</span></span> |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | <span data-ttu-id="8c0d8-172">String</span><span class="sxs-lookup"><span data-stu-id="8c0d8-172">String</span></span> | <span data-ttu-id="8c0d8-173">64</span><span class="sxs-lookup"><span data-stu-id="8c0d8-173">64</span></span> | <span data-ttu-id="8c0d8-174">このプロパティは、タブが表示されるエンティティの一意の識別子です。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-174">This property is a  unique identifier for the entity that the tab displays.</span></span> <span data-ttu-id="8c0d8-175">これは必須フィールドです。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-175">This is a required field.</span></span>|
| `name` | <span data-ttu-id="8c0d8-176">String</span><span class="sxs-lookup"><span data-stu-id="8c0d8-176">String</span></span> | <span data-ttu-id="8c0d8-177">128</span><span class="sxs-lookup"><span data-stu-id="8c0d8-177">128</span></span> | <span data-ttu-id="8c0d8-178">このプロパティは、チャネル インターフェイスのタブの表示名です。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-178">This property is the display name of the tab in the channel interface.</span></span> <span data-ttu-id="8c0d8-179">この入力フィールドは省略できます。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-179">This is an optional field.</span></span>|
| `contentUrl` | <span data-ttu-id="8c0d8-180">String</span><span class="sxs-lookup"><span data-stu-id="8c0d8-180">String</span></span> | <span data-ttu-id="8c0d8-181">2048</span><span class="sxs-lookup"><span data-stu-id="8c0d8-181">2048</span></span> | <span data-ttu-id="8c0d8-182">このプロパティは、https:// キャンバスに表示するエンティティ UI をポイントするTeamsです。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-182">This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span> <span data-ttu-id="8c0d8-183">これは必須フィールドです。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-183">This is a required field.</span></span>|
| `websiteUrl?` | <span data-ttu-id="8c0d8-184">String</span><span class="sxs-lookup"><span data-stu-id="8c0d8-184">String</span></span> | <span data-ttu-id="8c0d8-185">2048</span><span class="sxs-lookup"><span data-stu-id="8c0d8-185">2048</span></span> | <span data-ttu-id="8c0d8-186">ユーザーがブラウザーで表示 https:// 場合、このプロパティは参照先の URL です。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-186">This property is the https:// URL to point at, if a user selects to view in a browser.</span></span> <span data-ttu-id="8c0d8-187">これは必須フィールドです。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-187">This is a required field.</span></span>|
| `removeUrl?` | <span data-ttu-id="8c0d8-188">String</span><span class="sxs-lookup"><span data-stu-id="8c0d8-188">String</span></span> | <span data-ttu-id="8c0d8-189">2048</span><span class="sxs-lookup"><span data-stu-id="8c0d8-189">2048</span></span> | <span data-ttu-id="8c0d8-190">このプロパティは、https:// を削除するときに表示される UI を示す URL です。これはオプションのフィールドです。</span><span class="sxs-lookup"><span data-stu-id="8c0d8-190">This property is the https:// URL that points to the UI to be displayed when the user deletes the tab. This is an optional field.</span></span>|

## <a name="see-also"></a><span data-ttu-id="8c0d8-191">関連項目</span><span class="sxs-lookup"><span data-stu-id="8c0d8-191">See also</span></span>

* [<span data-ttu-id="8c0d8-192">メッセージング拡張機能リンクの分岐解除</span><span class="sxs-lookup"><span data-stu-id="8c0d8-192">Messaging extensions link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="8c0d8-193">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="8c0d8-193">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="8c0d8-194">前提条件</span><span class="sxs-lookup"><span data-stu-id="8c0d8-194">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="8c0d8-195">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="8c0d8-195">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="8c0d8-196">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="8c0d8-196">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="8c0d8-197">コンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="8c0d8-197">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="8c0d8-198">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="8c0d8-198">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="8c0d8-199">タブの削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="8c0d8-199">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="8c0d8-200">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="8c0d8-200">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="8c0d8-201">タブのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="8c0d8-201">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="8c0d8-202">アダプティブ カードを使用してタブをビルドする</span><span class="sxs-lookup"><span data-stu-id="8c0d8-202">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="8c0d8-203">タブ余白の変更</span><span class="sxs-lookup"><span data-stu-id="8c0d8-203">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="8c0d8-204">次の手順</span><span class="sxs-lookup"><span data-stu-id="8c0d8-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c0d8-205">会話タブを作成する</span><span class="sxs-lookup"><span data-stu-id="8c0d8-205">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)