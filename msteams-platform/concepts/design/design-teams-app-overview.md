---
title: カスタム アプリの設計
author: heath-hamilton
description: Microsoft Teams アプリを設計する方法について説明します。 リソースには、Microsoft Teams UI Kit、ベスト プラクティス、例などがあります。
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0c791b1e4733cd2a015e443ca5c4d0c433dd4d31
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911906"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="a1c65-104">Microsoft Teams アプリの設計</span><span class="sxs-lookup"><span data-stu-id="a1c65-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams の設計ガイドラインを紹介する概念イメージ。":::

<span data-ttu-id="a1c65-106">設計者、製品マネージャー、開発者、またはメーカーが低コードツールを使用している場合でも、これらのガイドラインは、Microsoft Teams アプリの適切な設計上の決定をすばやく行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="a1c65-107">Teams アプリ設計の原則</span><span class="sxs-lookup"><span data-stu-id="a1c65-107">Teams app design principles</span></span>

<span data-ttu-id="a1c65-108">Teams アプリは、ユーザーが一緒にもっと多くの成果を達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="a1c65-109">これらの原則を使用して、設計をガイドします。</span><span class="sxs-lookup"><span data-stu-id="a1c65-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="a1c65-110">Collaborative</span><span class="sxs-lookup"><span data-stu-id="a1c65-110">Collaborative</span></span>

<span data-ttu-id="a1c65-111">Teams アプリは、ユーザーが一緒にもっと多くの成果を達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="a1c65-112">これらの原則を使用して、設計をガイドします。</span><span class="sxs-lookup"><span data-stu-id="a1c65-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="a1c65-113">信頼できる</span><span class="sxs-lookup"><span data-stu-id="a1c65-113">Trustworthy</span></span>

<span data-ttu-id="a1c65-114">アプリはセキュリティで保護され、準拠しています。</span><span class="sxs-lookup"><span data-stu-id="a1c65-114">The app is secure and compliant.</span></span> <span data-ttu-id="a1c65-115">ユーザーはプライバシーに関する情報を簡単に検索できます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="a1c65-116">グローバルに包括</span><span class="sxs-lookup"><span data-stu-id="a1c65-116">Globally inclusive</span></span>

<span data-ttu-id="a1c65-117">すべてのバックグラウンド、スキルセット、および分野のユーザーがアプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="a1c65-118">文化的、人種的、社会的な認識を持つ。</span><span class="sxs-lookup"><span data-stu-id="a1c65-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="a1c65-119">低負荷</span><span class="sxs-lookup"><span data-stu-id="a1c65-119">Light</span></span>

<span data-ttu-id="a1c65-120">このアプリは、Teams のワークフローとブレンドするコア シナリオに重点を当てはっています。</span><span class="sxs-lookup"><span data-stu-id="a1c65-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="a1c65-121">ネイティブまたは個別</span><span class="sxs-lookup"><span data-stu-id="a1c65-121">Native or distinct</span></span>

<span data-ttu-id="a1c65-122">アプリは、ネイティブの Teams 設計コンポーネントまたは独自のコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="a1c65-123">配色、コントロールなどのブレンドはありません。</span><span class="sxs-lookup"><span data-stu-id="a1c65-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="a1c65-124">役に立つ</span><span class="sxs-lookup"><span data-stu-id="a1c65-124">Useful</span></span>

<span data-ttu-id="a1c65-125">アプリは、ユーザーが Teams で行う必要があるシナリオに基づいて作成されます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="a1c65-126">使いやすい</span><span class="sxs-lookup"><span data-stu-id="a1c65-126">Easy to use</span></span>

<span data-ttu-id="a1c65-127">UI は理解が容易で、外観とトーンが楽で、ユーザーの生産性が向上します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="a1c65-128">速い</span><span class="sxs-lookup"><span data-stu-id="a1c65-128">Responsive</span></span>

<span data-ttu-id="a1c65-129">アプリはデバイスと画面に依存しない。</span><span class="sxs-lookup"><span data-stu-id="a1c65-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="a1c65-130">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="a1c65-130">Accessible</span></span>

<span data-ttu-id="a1c65-131">このアプリは、色コントラストやナビゲーションの代替手段など、Teams のアクセシビリティ要件を満たしています。</span><span class="sxs-lookup"><span data-stu-id="a1c65-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="a1c65-132">よく説明されています</span><span class="sxs-lookup"><span data-stu-id="a1c65-132">Well described</span></span>

<span data-ttu-id="a1c65-133">テキスト、アイコン、画像を使って、アプリの意味と使い方を明確に示します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="a1c65-134">コーヒーティブ なエクスペリエンスの作成</span><span class="sxs-lookup"><span data-stu-id="a1c65-134">Creating a cohesive experience</span></span>

<span data-ttu-id="a1c65-135">Teams アプリの設計は、従来の Web アプリの設計に似たものですが、少し異なります。</span><span class="sxs-lookup"><span data-stu-id="a1c65-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="a1c65-136">効果的な設計では、Teams の機能やコンテキストに自然に適合しながら、アプリの固有の属性を強調します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="a1c65-137">これらのガイドラインとリソースは、そのバランスを取る際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="a1c65-138">Teams アプリを設計する際の対応方法と避ける必要がある操作 (タブ内の複数レベルのナビゲーションなど) を確認できます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="a1c65-139">アプリの計画</span><span class="sxs-lookup"><span data-stu-id="a1c65-139">Planning your app</span></span>

<span data-ttu-id="a1c65-140">高品質の Teams アプリを設計するには、まず、アプリが何を行い、ユーザーがアプリを使用すると思うのかを理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1c65-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="a1c65-141">まだ計画していない場合は、しばらく時間を取ってアプリを [適切に計画してください](../../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="a1c65-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="a1c65-142">デザインの基本事項</span><span class="sxs-lookup"><span data-stu-id="a1c65-142">Design fundamentals</span></span>

<span data-ttu-id="a1c65-143">レイアウト [、配色など、Teams](design-teams-app-fundamentals.md)アプリ設計の基本について学習します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="a1c65-144">Teams の基本的な Fluent UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="a1c65-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="a1c65-145">Fluent UI に基づいて、これらは使い慣れた Teams インターフェイスを作成 [するための主要な要素です](design-teams-app-basic-ui-components.md)。</span><span class="sxs-lookup"><span data-stu-id="a1c65-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="a1c65-146">UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="a1c65-146">UI templates</span></span>

<span data-ttu-id="a1c65-147">一般的な Teams の使用事例とワークフロー用のテンプレートを使用して、複雑で忠実な [設計をすばやく作成できます](design-teams-app-ui-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a1c65-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="a1c65-148">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="a1c65-148">App capabilities</span></span>

<span data-ttu-id="a1c65-149">ユーザーが Teams アプリを追加、使用、管理して、設計の各機能を有効に利用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="a1c65-150">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="a1c65-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="a1c65-151">タブ</span><span class="sxs-lookup"><span data-stu-id="a1c65-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="a1c65-152">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="a1c65-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="a1c65-153">ボット</span><span class="sxs-lookup"><span data-stu-id="a1c65-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="a1c65-154">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="a1c65-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="a1c65-155">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="a1c65-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="a1c65-156">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="a1c65-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="tools-and-samples"></a><span data-ttu-id="a1c65-157">ツールとサンプル</span><span class="sxs-lookup"><span data-stu-id="a1c65-157">Tools and samples</span></span>

<span data-ttu-id="a1c65-158">以下のツールは、デザイナーや開発者の使用を開始するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a1c65-158">The following tools can help designers and developers get started.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a1c65-159">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="a1c65-159">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a1c65-160">必要に応じてドラッグ、ドロップ、変更できる UI コンポーネント、テンプレート、例を含む Teams アプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-160">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="a1c65-161">UI キットには、さまざまな Teams シナリオでのアプリの外観と動作に関する包括的な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="a1c65-161">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1c65-162">UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="a1c65-162">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="a1c65-163">Microsoft Teams UI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="a1c65-163">Microsoft Teams UI Library</span></span>

<span data-ttu-id="a1c65-164">ブラウザーで個々の Teams UI テンプレートと関連コンポーネントを表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="a1c65-164">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1c65-165">UI ライブラリ (プレイグラウンド) を試す</span><span class="sxs-lookup"><span data-stu-id="a1c65-165">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="a1c65-166">これらのテンプレートと関連コンポーネントを Teams アプリ プロジェクトに直接インポートします。</span><span class="sxs-lookup"><span data-stu-id="a1c65-166">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1c65-167">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="a1c65-167">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="a1c65-168">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="a1c65-168">Sample app</span></span>

<span data-ttu-id="a1c65-169">サンプル アプリをインストールして、Teams コンテキスト内での UI テンプレートの外観と動作を確認します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-169">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1c65-170">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="a1c65-170">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="a1c65-171">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="a1c65-171">Other resources</span></span>

<span data-ttu-id="a1c65-172">詳細については、次のいずれかのリソースを試してください。</span><span class="sxs-lookup"><span data-stu-id="a1c65-172">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="a1c65-173">Fluent UI ドキュメント</span><span class="sxs-lookup"><span data-stu-id="a1c65-173">Fluent UI documentation</span></span>

<span data-ttu-id="a1c65-174">Teams エクスペリエンスの構築に使用される Fluent UI ベースのコンポーネントのコード サンプルと実装の詳細を取得します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-174">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1c65-175">Teams UI コンポーネントを試す (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="a1c65-175">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="a1c65-176">アダプティブ カード デザイナー</span><span class="sxs-lookup"><span data-stu-id="a1c65-176">Adaptive Cards designer</span></span>

<span data-ttu-id="a1c65-177">Web ベースのツールでアダプティブ カードを設計します。</span><span class="sxs-lookup"><span data-stu-id="a1c65-177">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1c65-178">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="a1c65-178">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
