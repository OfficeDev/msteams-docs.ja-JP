---
title: カスタム アプリの設計
author: heath-hamilton
description: アプリを設計するMicrosoft Teamsします。 リソースには、MICROSOFT TEAMS UI キット、ベスト プラクティス、例などがあります。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 19b8f8cbcbc52aa02ccd5d94f5bc4c088f2ae28a
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644876"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="2b02b-104">アプリのMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="2b02b-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="設計ガイドラインに関するMicrosoft Teams概念図。":::

<span data-ttu-id="2b02b-106">低コード ツールを使用しているデザイナー、製品マネージャー、開発者、メーカーなど、これらのガイドラインは、Microsoft Teams アプリに対して適切な設計上の意思決定を迅速に行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="2b02b-107">一つ一つのエクスペリエンスを作成する</span><span class="sxs-lookup"><span data-stu-id="2b02b-107">Creating a cohesive experience</span></span>

<span data-ttu-id="2b02b-108">アプリのTeamsは、従来の Web アプリの設計と同じですが、少し異なります。</span><span class="sxs-lookup"><span data-stu-id="2b02b-108">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="2b02b-109">効果的な設計では、アプリの固有の属性を強調しながら、アプリの機能やコンテキストTeams自然にフィットします。</span><span class="sxs-lookup"><span data-stu-id="2b02b-109">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="2b02b-110">これらのガイドラインとリソースは、バランスを取る際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-110">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="2b02b-111">アプリを設計するときに何を行い、何を回避Teams (タブ内の複数レベルのナビゲーションなど) が分かっています。</span><span class="sxs-lookup"><span data-stu-id="2b02b-111">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="2b02b-112">Teamsの設計原則</span><span class="sxs-lookup"><span data-stu-id="2b02b-112">Teams app design principles</span></span>

<span data-ttu-id="2b02b-113">Teamsアプリは、ユーザーが一緒に達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-113">Teams apps help people achieve more together.</span></span> <span data-ttu-id="2b02b-114">設計をガイドするには、次の原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-114">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="2b02b-115">共同作業</span><span class="sxs-lookup"><span data-stu-id="2b02b-115">Collaborative</span></span>

<span data-ttu-id="2b02b-116">Teamsアプリは、ユーザーが一緒に達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-116">Teams apps help people achieve more together.</span></span> <span data-ttu-id="2b02b-117">設計をガイドするには、次の原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-117">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="2b02b-118">信頼できる</span><span class="sxs-lookup"><span data-stu-id="2b02b-118">Trustworthy</span></span>

<span data-ttu-id="2b02b-119">アプリは安全で準拠しています。</span><span class="sxs-lookup"><span data-stu-id="2b02b-119">The app is secure and compliant.</span></span> <span data-ttu-id="2b02b-120">ユーザーは、プライバシーに関する情報を簡単に見つくことができます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-120">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="2b02b-121">グローバルに包括的</span><span class="sxs-lookup"><span data-stu-id="2b02b-121">Globally inclusive</span></span>

<span data-ttu-id="2b02b-122">すべてのバックグラウンド、スキルセット、および専門分野のユーザーは、アプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-122">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="2b02b-123">文化的、人種的、社会的に認識しています。</span><span class="sxs-lookup"><span data-stu-id="2b02b-123">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="2b02b-124">低負荷</span><span class="sxs-lookup"><span data-stu-id="2b02b-124">Light</span></span>

<span data-ttu-id="2b02b-125">アプリは、ワークフローとブレンドするコア シナリオTeamsしています。</span><span class="sxs-lookup"><span data-stu-id="2b02b-125">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="2b02b-126">ネイティブまたは個別</span><span class="sxs-lookup"><span data-stu-id="2b02b-126">Native or distinct</span></span>

<span data-ttu-id="2b02b-127">アプリは、ネイティブ のTeamsコンポーネントまたは独自のコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-127">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="2b02b-128">配色、コントロールのブレンドなどはありません。</span><span class="sxs-lookup"><span data-stu-id="2b02b-128">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="2b02b-129">役に立つ</span><span class="sxs-lookup"><span data-stu-id="2b02b-129">Useful</span></span>

<span data-ttu-id="2b02b-130">アプリは、ユーザーがユーザーが必要とするシナリオに基づいて、Teams。</span><span class="sxs-lookup"><span data-stu-id="2b02b-130">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="2b02b-131">使いやすい</span><span class="sxs-lookup"><span data-stu-id="2b02b-131">Easy to use</span></span>

<span data-ttu-id="2b02b-132">UI はわかりやすいので、見た目とトーンが快適で、ユーザーの生産性が向上します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-132">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="2b02b-133">速い</span><span class="sxs-lookup"><span data-stu-id="2b02b-133">Responsive</span></span>

<span data-ttu-id="2b02b-134">アプリはデバイスであり、画面に依存しない。</span><span class="sxs-lookup"><span data-stu-id="2b02b-134">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="2b02b-135">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="2b02b-135">Accessible</span></span>

<span data-ttu-id="2b02b-136">このアプリは、Teams、ナビゲーションの代替など、ユーザー補助の要件を満たしています。</span><span class="sxs-lookup"><span data-stu-id="2b02b-136">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="2b02b-137">よく説明</span><span class="sxs-lookup"><span data-stu-id="2b02b-137">Well described</span></span>

<span data-ttu-id="2b02b-138">テキスト、アイコン、画像を使用すると、アプリが何を使用し、どのように使うのかを明確にできます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-138">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a><span data-ttu-id="2b02b-139">Teams設計システム</span><span class="sxs-lookup"><span data-stu-id="2b02b-139">Teams design system</span></span>

<span data-ttu-id="2b02b-140">レイアウト[、配色Teamsなど、](design-teams-app-fundamentals.md)アプリ設計の基本について学習します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-140">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="2b02b-141">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="2b02b-141">App capabilities</span></span>

<span data-ttu-id="2b02b-142">ユーザーがアプリを追加、使用、管理する方法Teams設計の各機能を有効に利用する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-142">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="2b02b-143">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="2b02b-143">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="2b02b-144">タブ</span><span class="sxs-lookup"><span data-stu-id="2b02b-144">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="2b02b-145">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="2b02b-145">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="2b02b-146">ボット</span><span class="sxs-lookup"><span data-stu-id="2b02b-146">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="2b02b-147">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="2b02b-147">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a><span data-ttu-id="2b02b-148">UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="2b02b-148">UI templates</span></span>

<span data-ttu-id="2b02b-149">一般的な使用例やワークフロー用のテンプレートを使用して、複雑で忠実[度Teamsをすばやく作成します](design-teams-app-ui-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2b02b-149">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="basic-ui-components"></a><span data-ttu-id="2b02b-150">基本的な UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="2b02b-150">Basic UI components</span></span>

<span data-ttu-id="2b02b-151">Fluent UI に基づいて、[](design-teams-app-basic-ui-components.md)これらの要素を使用して、最初からエクスペリエンスTeams作成できます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-151">Based on Fluent UI, these are the [core elements](design-teams-app-basic-ui-components.md) you can use to create Teams experiences from scratch.</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="2b02b-152">ツールとサンプル</span><span class="sxs-lookup"><span data-stu-id="2b02b-152">Tools and samples</span></span>

<span data-ttu-id="2b02b-153">次のツールは、デザイナーと開発者が始めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-153">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="2b02b-154">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="2b02b-154">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="2b02b-155">UI コンポーネントTeamsテンプレート、および必要に応じてドラッグ、ドロップ、および変更できる例を含むアプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-155">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="2b02b-156">UI キットには、さまざまなシナリオでのアプリの外観と動作に関する包括的なTeams含まれています。</span><span class="sxs-lookup"><span data-stu-id="2b02b-156">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b02b-157">UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="2b02b-157">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="2b02b-158">Microsoft TeamsUI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="2b02b-158">Microsoft Teams UI Library</span></span>

<span data-ttu-id="2b02b-159">ブラウザーで UI テンプレートTeams関連するコンポーネントを個別に表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="2b02b-159">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b02b-160">UI ライブラリ (プレイグラウンド) を試す</span><span class="sxs-lookup"><span data-stu-id="2b02b-160">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="2b02b-161">これらのテンプレートと関連コンポーネントをアプリ プロジェクトに直接Teamsインポートします。</span><span class="sxs-lookup"><span data-stu-id="2b02b-161">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b02b-162">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="2b02b-162">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="2b02b-163">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="2b02b-163">Sample app</span></span>

<span data-ttu-id="2b02b-164">サンプル アプリをアップロードして、アプリの外観と動作をクライアントで確認Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="2b02b-164">You can upload a sample app to see how apps should look and behave in the Teams client.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b02b-165">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="2b02b-165">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="2b02b-166">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="2b02b-166">Other resources</span></span>

<span data-ttu-id="2b02b-167">詳細については、次のいずれかのリソースを試してください。</span><span class="sxs-lookup"><span data-stu-id="2b02b-167">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="2b02b-168">Fluent UI のドキュメント</span><span class="sxs-lookup"><span data-stu-id="2b02b-168">Fluent UI documentation</span></span>

<span data-ttu-id="2b02b-169">ユーザー エクスペリエンスの構築に使用される基本的な Fluent UI コンポーネントのコード サンプルと実装Teams取得します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-169">Get code samples and implementation details for the basic Fluent UI components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b02b-170">UI Teams試す (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="2b02b-170">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="2b02b-171">アダプティブ カード デザイナー</span><span class="sxs-lookup"><span data-stu-id="2b02b-171">Adaptive Cards designer</span></span>

<span data-ttu-id="2b02b-172">Web ベースのツールでアダプティブ カードを設計します。</span><span class="sxs-lookup"><span data-stu-id="2b02b-172">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b02b-173">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="2b02b-173">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
