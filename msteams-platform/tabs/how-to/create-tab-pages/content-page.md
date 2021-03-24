---
title: コンテンツ ページを作成する
author: laujan
description: コンテンツ ページを作成する方法
keywords: teams タブ グループ チャネル構成可能静的
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c33f58197e8b49ac7122178e154724cc5186bcb1
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034699"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="f66ea-104">タブのコンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="f66ea-104">Create a content page for your tab</span></span>

<span data-ttu-id="f66ea-105">コンテンツ ページは、Teams クライアント内でレンダリングされる Web ページです。</span><span class="sxs-lookup"><span data-stu-id="f66ea-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="f66ea-106">通常、これらは次の一部です。</span><span class="sxs-lookup"><span data-stu-id="f66ea-106">Typically these are part of:</span></span>

* <span data-ttu-id="f66ea-107">個人用スコープのカスタム タブ - このインスタンスでは、コンテンツ ページはユーザーが最初に表示するページです。</span><span class="sxs-lookup"><span data-stu-id="f66ea-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="f66ea-108">チャネル/グループ のカスタム タブ - ユーザーが適切なコンテキストでタブをピンで固定して構成すると、コンテンツ ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="f66ea-109">タスク [モジュール](~/task-modules-and-cards/what-are-task-modules.md) - コンテンツ ページを作成し、それをタスク モジュール内の Web ビューとして埋め込みできます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="f66ea-110">モーダル ポップアップ内にページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="f66ea-111">この記事では、コンテンツ ページをタブとして使用する方法について説明します。ただし、ここでのガイダンスの大部分は、コンテンツ ページがエンド ユーザーに提示される方法に関係なく適用されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="f66ea-112">タブのコンテンツとスタイルのガイドライン</span><span class="sxs-lookup"><span data-stu-id="f66ea-112">Tab content and style guidelines</span></span>

<span data-ttu-id="f66ea-113">タブの全体的な目的は、実用的な価値と明らかな目的を持つ有意義で魅力的なコンテンツへのアクセスを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f66ea-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="f66ea-114">これは、快適なスタイルを見送る必要があるという意味ではありません。タブデザインをクリーンにし、ナビゲーションを直感的に行い、コンテンツを没入感のあるものにすることで、混乱を最小限に抑えることに集中する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f66ea-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="f66ea-115">タブと Microsoft Teams [アプリ承認プロセスの](~/tabs/design/tabs.md) ガイダンスを使用して、コンテンツと会話を [一度に表示する](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="f66ea-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="f66ea-116">コードを Teams と統合する</span><span class="sxs-lookup"><span data-stu-id="f66ea-116">Integrate your code with Teams</span></span>

<span data-ttu-id="f66ea-117">Teams にページを表示するには [、Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) クライアント SDK を含め、ページの読み込み後に呼び `microsoftTeams.initialize()` 出しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f66ea-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="f66ea-118">ページと Teams クライアントが通信する方法は次の通りです。</span><span class="sxs-lookup"><span data-stu-id="f66ea-118">That is how your page and the Teams client communicate:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="accessing-additional-content"></a><span data-ttu-id="f66ea-119">追加コンテンツへのアクセス</span><span class="sxs-lookup"><span data-stu-id="f66ea-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="f66ea-120">SDK を使用した Teams の操作</span><span class="sxs-lookup"><span data-stu-id="f66ea-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="f66ea-121">[Teams クライアント JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)には、コンテンツ ページの開発に役立つ機能が多数含まれています。</span><span class="sxs-lookup"><span data-stu-id="f66ea-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="f66ea-122">ディープ リンク</span><span class="sxs-lookup"><span data-stu-id="f66ea-122">Deep links</span></span>

<span data-ttu-id="f66ea-123">Teams のエンティティへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="f66ea-124">通常、これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。「Microsoft [Teams でコンテンツと機能へのディープ リンクを作成する」を参照してください](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="f66ea-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="f66ea-125">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="f66ea-125">Task Modules</span></span>

<span data-ttu-id="f66ea-126">タスク モジュールは、タブからトリガーできるモーダル ポップアップのようなエクスペリエンスです。通常、コンテンツ ページでは、複数のページを介してユーザーを移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f66ea-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="f66ea-127">代わりに、タスク モジュールを使用して、追加情報の収集、リスト内のアイテムの詳細の表示、またはユーザーに追加情報を提示する必要があるその他の時間を表示するためのフォームを提示します。</span><span class="sxs-lookup"><span data-stu-id="f66ea-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="f66ea-128">タスク モジュール自体は、追加のコンテンツ ページでも、アダプティブ カードを使用して完全に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="f66ea-129">詳細については [、「タブでのタスク モジュールの使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f66ea-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="f66ea-130">有効なドメイン</span><span class="sxs-lookup"><span data-stu-id="f66ea-130">Valid Domains</span></span>

<span data-ttu-id="f66ea-131">タブで使用されているすべての URL ドメインがマニフェストの配列に含 `validDomains` まれているか確認 [します](~/concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="f66ea-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="f66ea-132">詳細については、マニフェスト スキーマ [リファレンスの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f66ea-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="f66ea-133">ただし、タブのコア機能は Teams 内に存在し、Teams の外部には存在しません。</span><span class="sxs-lookup"><span data-stu-id="f66ea-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="f66ea-134">静的な個人用タブの並べ替え</span><span class="sxs-lookup"><span data-stu-id="f66ea-134">Reorder static personal tabs</span></span>

<span data-ttu-id="f66ea-135">マニフェスト バージョン 1.7 から、開発者は個人用アプリ内のすべてのタブを再配置できます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="f66ea-136">特に、開発者はボット チャットタブを移動できます。これは常に既定で最初の位置に、個人用アプリのタブ ヘッダー内の任意の場所に移動できます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="f66ea-137">2 つの予約済みタブ entityId キーワード、会話 *、およびについて* 宣言 *しました*。</span><span class="sxs-lookup"><span data-stu-id="f66ea-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="f66ea-138">個人用スコープを持つボットを *作成* すると、既定では個人用アプリの最初のタブ位置に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="f66ea-139">別の位置に移動する場合は、予約キーワードである会話を使用して静的タブ オブジェクトをマニフェストに追加する必要 *があります*。</span><span class="sxs-lookup"><span data-stu-id="f66ea-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="f66ea-140">[ *会話* ] タブは、配列に [会話] タブを追加した場所に基づいて *Web* またはデスクトップに表示 `staticTabs` されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="f66ea-141">ネイティブ読み込みインジケーターの表示</span><span class="sxs-lookup"><span data-stu-id="f66ea-141">Show a native loading indicator</span></span>

<span data-ttu-id="f66ea-142">マニフェスト スキーマ[v1.7](../../../resources/schema/manifest-schema.md)から、Web コンテンツ[](../../../resources/schema/manifest-schema.md#showloadingindicator)が Teams に読み込まれる場所 (タブ コンテンツ ページ、構成ページ、[](configuration-page.md)タブ内の[](removal-page.md)削除ページ、タスク モジュールなど) にネイティブ読み込みインジケーターを提供[できます](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。 [](#integrate-your-code-with-teams)</span><span class="sxs-lookup"><span data-stu-id="f66ea-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> 1. <span data-ttu-id="f66ea-143">モバイル クライアントでの動作は、このマニフェスト プロパティでは構成できません。</span><span class="sxs-lookup"><span data-stu-id="f66ea-143">The behavior on mobile clients is not configurable through this manifest property.</span></span> <span data-ttu-id="f66ea-144">モバイル クライアントは、コンテンツ ページと iframe ベースのタスク モジュール間で既定でネイティブ読み込みインジケーターを表示します。</span><span class="sxs-lookup"><span data-stu-id="f66ea-144">Mobile clients show a native loading indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="f66ea-145">モバイル上のこのインジケーターは、コンテンツの取得要求が行われたときに表示され、要求が完了するとすぐに却下されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-145">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>
> 2. <span data-ttu-id="f66ea-146">アプリ マニフェストで指定した場合は、すべてのタブ構成、コンテンツ、および削除ページとすべての iframe ベースのタスク モジュールは、以下の必須プロトコルに従う  `"showLoadingIndicator : true`  必要があります。</span><span class="sxs-lookup"><span data-stu-id="f66ea-146">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>


1. <span data-ttu-id="f66ea-147">読み込みインジケーターを表示するには、マニフェスト `"showLoadingIndicator": true` に追加します。</span><span class="sxs-lookup"><span data-stu-id="f66ea-147">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="f66ea-148">を呼び出す `microsoftTeams.initialize();` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="f66ea-148">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="f66ea-149">**オプション**。</span><span class="sxs-lookup"><span data-stu-id="f66ea-149">**Optional**.</span></span> <span data-ttu-id="f66ea-150">画面に印刷する準備が整い、アプリケーションの残りのコンテンツを遅延読み込みする場合は、呼び出しによって読み込みインジケーターを手動で非表示にできます `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="f66ea-150">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="f66ea-151">**必須です**。</span><span class="sxs-lookup"><span data-stu-id="f66ea-151">**Mandatory**.</span></span> <span data-ttu-id="f66ea-152">最後に、アプリが `microsoftTeams.appInitialization.notifySuccess()` 正常に読み込まれたと Teams に通知する呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="f66ea-152">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="f66ea-153">該当する場合、Teams は読み込みインジケーターを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="f66ea-153">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="f66ea-154">30 秒以内に呼び出されない場合は、アプリがタイム アウトし、再試行オプション付きエラー画面が  `notifySuccess`  表示されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-154">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="f66ea-155">アプリケーションの読み込みに失敗した場合は、Teams にエラー `microsoftTeams.appInitialization.notifyFailure(reason);` が発生したと知らせる呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="f66ea-155">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="f66ea-156">次に、エラー画面がユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f66ea-156">An error screen will then be shown to the user:</span></span>

```typescript
``
/* List of failure reasons */
export const enum FailedReason {
    AuthFailed = "AuthFailed",
    Timeout = "Timeout",
    Other = "Other"
}
```
>
