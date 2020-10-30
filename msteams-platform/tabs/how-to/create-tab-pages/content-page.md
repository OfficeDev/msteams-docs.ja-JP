---
title: コンテンツ ページを作成する
author: laujan
description: コンテンツページを作成する方法
keywords: teams タブグループチャネルの構成可能な静的
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 62a398c87b681013c89e540d2bdc463c97877307
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796317"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="bf326-104">タブのコンテンツページを作成する</span><span class="sxs-lookup"><span data-stu-id="bf326-104">Create a content page for your tab</span></span>

<span data-ttu-id="bf326-105">コンテンツページは、Teams クライアント内でレンダリングされる web ページです。</span><span class="sxs-lookup"><span data-stu-id="bf326-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="bf326-106">通常は、次の一部です。</span><span class="sxs-lookup"><span data-stu-id="bf326-106">Typically these are part of:</span></span>

* <span data-ttu-id="bf326-107">このインスタンスでは、個人を対象範囲とするカスタムタブ。コンテンツページは、ユーザーが最初に検出したページです。</span><span class="sxs-lookup"><span data-stu-id="bf326-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="bf326-108">チャネル/グループカスタムタブ-ユーザーが適切なコンテキストでタブを固定して構成すると、[コンテンツ] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bf326-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="bf326-109">[タスクモジュール](~/task-modules-and-cards/what-are-task-modules.md)-コンテンツページを作成し、それをタスクモジュール内の webview として埋め込むことができます。</span><span class="sxs-lookup"><span data-stu-id="bf326-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="bf326-110">ページはモーダルポップアップ内にレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="bf326-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="bf326-111">この記事では、コンテンツページをタブとして使用する方法について説明します。ただし、ここに示すガイダンスの大部分は、エンドユーザーにコンテンツページを表示する方法に関係なく適用されます。</span><span class="sxs-lookup"><span data-stu-id="bf326-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="bf326-112">タブの内容とスタイルのガイドライン</span><span class="sxs-lookup"><span data-stu-id="bf326-112">Tab content and style guidelines</span></span>

<span data-ttu-id="bf326-113">タブの全体的な目的は、実用的な価値と明確な目的を持つ、有意義で魅力的なコンテンツへのアクセスを提供することです。</span><span class="sxs-lookup"><span data-stu-id="bf326-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="bf326-114">見栄えの良いスタイルを先送りする必要があるわけではありませんが、タブデザインをすっきりさせ、ナビゲーションを直観的に、コンテンツのイマーシブ化を行うことによって、乱雑さを最小化することを重視する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf326-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="bf326-115">タブおよび[Microsoft Teams アプリ承認プロセスガイダンス](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)[を使用して、コンテンツと会話を一度にすべて](~/tabs/design/tabs.md)表示</span><span class="sxs-lookup"><span data-stu-id="bf326-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="bf326-116">コードを Teams と統合する</span><span class="sxs-lookup"><span data-stu-id="bf326-116">Integrate your code with Teams</span></span>

<span data-ttu-id="bf326-117">ページを Teams に表示するには、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latestadd &preserve-view=true) を含み、ページの読み込み後にの呼び出しを含める必要があり `microsoftTeams.initialize()` ます。</span><span class="sxs-lookup"><span data-stu-id="bf326-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latestadd &preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="bf326-118">ページと Teams クライアントが通信する方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="bf326-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="bf326-119">その他のコンテンツへのアクセス</span><span class="sxs-lookup"><span data-stu-id="bf326-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="bf326-120">SDK を使用して Teams を操作する</span><span class="sxs-lookup"><span data-stu-id="bf326-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="bf326-121">[Teams クライアント JAVASCRIPT SDK](~/tabs/how-to/using-teams-client-sdk.md)には、コンテンツページの開発時に役立つ可能性がある多くの追加機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="bf326-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="bf326-122">ディープ リンク</span><span class="sxs-lookup"><span data-stu-id="bf326-122">Deep links</span></span>

<span data-ttu-id="bf326-123">Teams のエンティティへの詳細なリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="bf326-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="bf326-124">通常、これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。「 [Microsoft Teams のコンテンツと機能への詳細なリンクを作成する」を](~/concepts/build-and-test/deep-links.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="bf326-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="bf326-125">タスクモジュール</span><span class="sxs-lookup"><span data-stu-id="bf326-125">Task Modules</span></span>

<span data-ttu-id="bf326-126">タスクモジュールとは、タブからトリガーできるモーダルなポップアップのような操作のことです。通常、コンテンツページでは、複数のページを使用してユーザーを移動する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="bf326-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="bf326-127">その代わりに、タスクモジュールを使用して、追加情報を収集するためのフォームを表示したり、リスト内のアイテムの詳細を表示したり、またはその他の時間についてユーザーに追加情報を提示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf326-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="bf326-128">タスクモジュール自体は、追加のコンテンツページにすることも、アダプティブカードを使用して完全に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="bf326-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="bf326-129">詳細については、「 [tab でタスクモジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bf326-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="bf326-130">有効なドメイン</span><span class="sxs-lookup"><span data-stu-id="bf326-130">Valid Domains</span></span>

<span data-ttu-id="bf326-131">タブで使用されているすべての URL ドメインがマニフェスト内の配列に含まれていることを確認し `validDomains` ます。 [manifest](~/concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="bf326-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="bf326-132">詳細については、「マニフェストスキーマリファレンス」の「 [Validdomains](~/resources/schema/manifest-schema.md#validdomains) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bf326-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="bf326-133">ただし、タブのコア機能は teams 内に存在し、Teams の外部ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bf326-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="bf326-134">ネイティブローディングインジケーターを表示する</span><span class="sxs-lookup"><span data-stu-id="bf326-134">Show a native loading indicator</span></span>

<span data-ttu-id="bf326-135">[マニフェストスキーマ](../../../resources/schema/manifest-schema.md)v2.0 以降では、web コンテンツが Teams ([タブのコンテンツページ](#integrate-your-code-with-teams)、[構成ページ](configuration-page.md)、[削除ページ](removal-page.md)、[タスクモジュール](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)など) に読み込まれているすべての場所で、[ネイティブの読み込みインジケーター](../../../resources/schema/manifest-schema.md#showloadingindicator)を提供できます。</span><span class="sxs-lookup"><span data-stu-id="bf326-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bf326-136">アプリマニフェストで指定する場合は、  `"showLoadingIndicator : true`  すべてのタブ構成、コンテンツ、および削除ページと、すべての iframe ベースのタスクモジュールは、以下の必須プロトコルに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf326-136">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

1. <span data-ttu-id="bf326-137">読み込みインジケーターを表示するには、 `"showLoadingIndicator": true` マニフェストにを追加します。</span><span class="sxs-lookup"><span data-stu-id="bf326-137">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="bf326-138">にお問い合わせ `microsoftTeams.initialize();` ください。</span><span class="sxs-lookup"><span data-stu-id="bf326-138">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="bf326-139">**省略可能** です。</span><span class="sxs-lookup"><span data-stu-id="bf326-139">**Optional** .</span></span> <span data-ttu-id="bf326-140">画面に印刷する準備ができていて、アプリケーションのコンテンツの残りの部分を遅延ロードする必要がある場合は、を呼び出して、読み込みインジケーターを手動で非表示にすることができます。 `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="bf326-140">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="bf326-141">**必須** 。</span><span class="sxs-lookup"><span data-stu-id="bf326-141">**Mandatory** .</span></span> <span data-ttu-id="bf326-142">最後に、 `microsoftTeams.appInitialization.notifySuccess()` アプリが正常に読み込まれたことを Teams に通知する呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="bf326-142">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="bf326-143">チームは、必要に応じて、読み込みインジケーターを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="bf326-143">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="bf326-144">`notifySuccess`が30秒以内に呼び出されない場合は、アプリがタイムアウトになり、[再試行] オプションのあるエラー画面が表示されることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="bf326-144">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="bf326-145">アプリケーションの読み込みに失敗した場合は、 `microsoftTeams.appInitialization.notifyFailure(reason);` チームにエラーがあることを知らせるための呼び出しを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="bf326-145">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="bf326-146">エラー画面がユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="bf326-146">An error screen will then be shown to the user:</span></span>

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
