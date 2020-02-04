---
title: コンテンツページを作成する
author: laujan
description: ''
keywords: teams タブグループチャネルの構成可能な静的
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: ac85e000c9bdaebf28cb33143a7c82a348d3771e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674875"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="6b663-103">タブのコンテンツページを作成する</span><span class="sxs-lookup"><span data-stu-id="6b663-103">Create a content page for your tab</span></span>

<span data-ttu-id="6b663-104">コンテンツページは、Teams クライアント内でレンダリングされる web ページです。</span><span class="sxs-lookup"><span data-stu-id="6b663-104">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="6b663-105">通常は、次の一部です。</span><span class="sxs-lookup"><span data-stu-id="6b663-105">Typically these are part of:</span></span>

* <span data-ttu-id="6b663-106">このインスタンスでは、個人を対象範囲とするカスタムタブ。コンテンツページは、ユーザーが最初に検出したページです。</span><span class="sxs-lookup"><span data-stu-id="6b663-106">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="6b663-107">チャネル/グループカスタムタブ-ユーザーが適切なコンテキストでタブを固定して構成すると、[コンテンツ] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6b663-107">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="6b663-108">[タスクモジュール](~/task-modules-and-cards/what-are-task-modules.md)-コンテンツページを作成し、それをタスクモジュール内の webview として埋め込むことができます。</span><span class="sxs-lookup"><span data-stu-id="6b663-108">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="6b663-109">ページはモーダルポップアップ内にレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="6b663-109">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="6b663-110">この記事では、コンテンツページをタブとして使用する方法について説明します。ただし、ここに示すガイダンスの大部分は、エンドユーザーにコンテンツページを表示する方法に関係なく適用されます。</span><span class="sxs-lookup"><span data-stu-id="6b663-110">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="6b663-111">タブの内容とスタイルのガイドライン</span><span class="sxs-lookup"><span data-stu-id="6b663-111">Tab content and style guidelines</span></span>

<span data-ttu-id="6b663-112">タブの全体的な目的は、実用的な価値と明確な目的を持つ、有意義で魅力的なコンテンツへのアクセスを提供することです。</span><span class="sxs-lookup"><span data-stu-id="6b663-112">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="6b663-113">見栄えの良いスタイルを先送りする必要があるわけではありませんが、タブデザインをすっきりさせ、ナビゲーションを直観的に、コンテンツのイマーシブ化を行うことによって、乱雑さを最小化することを重視する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b663-113">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="6b663-114">タブおよび[Microsoft Teams アプリ承認プロセスガイダンス](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)[を使用して、コンテンツと会話を一度にすべて](~/tabs/design/tabs.md)表示</span><span class="sxs-lookup"><span data-stu-id="6b663-114">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="6b663-115">コードを Teams と統合する</span><span class="sxs-lookup"><span data-stu-id="6b663-115">Integrate your code with Teams</span></span>

<span data-ttu-id="6b663-116">ページを Teams に表示するには、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest)を含み、ページの読み込み後`microsoftTeams.initialize()`にの呼び出しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b663-116">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="6b663-117">ページと Teams クライアントが通信する方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="6b663-117">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="6b663-118">その他のコンテンツへのアクセス</span><span class="sxs-lookup"><span data-stu-id="6b663-118">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="6b663-119">SDK を使用して Teams を操作する</span><span class="sxs-lookup"><span data-stu-id="6b663-119">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="6b663-120">[Teams クライアント JAVASCRIPT SDK](~/tabs/how-to/using-teams-client-sdk.md)には、開発者がコンテンツページを開発する際に役に立つことがある、多くの追加機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="6b663-120">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="6b663-121">ディープ リンク</span><span class="sxs-lookup"><span data-stu-id="6b663-121">Deep links</span></span>

<span data-ttu-id="6b663-122">Teams のエンティティへの詳細なリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="6b663-122">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="6b663-123">通常、これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。「 [Microsoft Teams のコンテンツと機能への詳細なリンクを作成する」を](~/concepts/build-and-test/deep-links.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b663-123">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="6b663-124">タスクモジュール</span><span class="sxs-lookup"><span data-stu-id="6b663-124">Task Modules</span></span>

<span data-ttu-id="6b663-125">タスクモジュールは、タブからトリガーできるモーダルのポップアップ表示のようなものです。通常、コンテンツページでは、複数のページを介してユーザーを移動する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6b663-125">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="6b663-126">その代わりに、タスクモジュールを使用して、追加情報を収集するためのフォームを表示したり、リスト内のアイテムの詳細を表示したり、またはその他の時間についてユーザーに追加情報を提示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b663-126">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="6b663-127">タスクモジュール自体は、追加のコンテンツページにすることも、アダプティブカードを使用して完全に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="6b663-127">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="6b663-128">詳細については、「 [tab でタスクモジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b663-128">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="6b663-129">有効なドメイン</span><span class="sxs-lookup"><span data-stu-id="6b663-129">Valid Domains</span></span>

<span data-ttu-id="6b663-130">タブで使用されているすべての URL ドメインが[マニフェスト](~/concepts/build-and-test/apps-package.md)内`validDomains`の配列に含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6b663-130">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="6b663-131">詳細については、「マニフェストスキーマリファレンス」の「 [Validdomains](~/resources/schema/manifest-schema.md#validdomains) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b663-131">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="6b663-132">ただし、タブのコア機能は teams 内に存在し、Teams の外部ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6b663-132">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>
