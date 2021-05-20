---
title: カスタム アプリの設計
author: heath-hamilton
description: Microsoft Teamsアプリを設計する方法については、こちらをご覧ください。 リソースには、Microsoft Teams UI キット、ベスト プラクティス、例などが含まれます。
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565117"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="ec03c-104">Microsoft Teams アプリの設計</span><span class="sxs-lookup"><span data-stu-id="ec03c-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams設計ガイドラインを紹介する概念図。":::

<span data-ttu-id="ec03c-106">デザイナー、プロダクト マネージャー、開発者、またはメーカーが低コード ツールを使用している場合でも、これらのガイドラインは、Microsoft Teams アプリに適したデザインの決定をすばやく行う上で役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="ec03c-107">Teamsアプリの設計原則</span><span class="sxs-lookup"><span data-stu-id="ec03c-107">Teams app design principles</span></span>

<span data-ttu-id="ec03c-108">Teamsアプリは、人々がより多くを一緒に達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="ec03c-109">これらの原則を使用して、設計を導きます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="ec03c-110">コラボレイティブ</span><span class="sxs-lookup"><span data-stu-id="ec03c-110">Collaborative</span></span>

<span data-ttu-id="ec03c-111">Teamsアプリは、人々がより多くを一緒に達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="ec03c-112">これらの原則を使用して、設計を導きます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="ec03c-113">頼もしい</span><span class="sxs-lookup"><span data-stu-id="ec03c-113">Trustworthy</span></span>

<span data-ttu-id="ec03c-114">アプリは安全で準拠しています。</span><span class="sxs-lookup"><span data-stu-id="ec03c-114">The app is secure and compliant.</span></span> <span data-ttu-id="ec03c-115">ユーザーは、プライバシーに関する情報を簡単に見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="ec03c-116">グローバルインクルーシブ</span><span class="sxs-lookup"><span data-stu-id="ec03c-116">Globally inclusive</span></span>

<span data-ttu-id="ec03c-117">すべての背景、スキルセット、および専門分野のユーザーは、アプリを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="ec03c-118">それは文化的、人種的、社会的に認識しています。</span><span class="sxs-lookup"><span data-stu-id="ec03c-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="ec03c-119">低負荷</span><span class="sxs-lookup"><span data-stu-id="ec03c-119">Light</span></span>

<span data-ttu-id="ec03c-120">アプリは、Teamsワークフローとブレンドコア シナリオに焦点を当てています。</span><span class="sxs-lookup"><span data-stu-id="ec03c-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="ec03c-121">ネイティブまたは個別</span><span class="sxs-lookup"><span data-stu-id="ec03c-121">Native or distinct</span></span>

<span data-ttu-id="ec03c-122">アプリは、ネイティブTeams設計コンポーネントまたは独自のコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="ec03c-123">配色やコントロールなどのブレンドはありません。</span><span class="sxs-lookup"><span data-stu-id="ec03c-123">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="ec03c-124">便利</span><span class="sxs-lookup"><span data-stu-id="ec03c-124">Useful</span></span>

<span data-ttu-id="ec03c-125">アプリは、ユーザーがTeamsで行う必要があるシナリオに基づいています。</span><span class="sxs-lookup"><span data-stu-id="ec03c-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="ec03c-126">使いやすい</span><span class="sxs-lookup"><span data-stu-id="ec03c-126">Easy to use</span></span>

<span data-ttu-id="ec03c-127">UI は理解しやすく、見た目やトーンが楽しく、人々の生産性を向上させます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="ec03c-128">速い</span><span class="sxs-lookup"><span data-stu-id="ec03c-128">Responsive</span></span>

<span data-ttu-id="ec03c-129">アプリはデバイスと画面に依存しません。</span><span class="sxs-lookup"><span data-stu-id="ec03c-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="ec03c-130">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="ec03c-130">Accessible</span></span>

<span data-ttu-id="ec03c-131">アプリは、色のコントラスト、ナビゲーションの代替、および多くの点でTeamsアクセシビリティ要件を満たしています。</span><span class="sxs-lookup"><span data-stu-id="ec03c-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="ec03c-132">よく説明</span><span class="sxs-lookup"><span data-stu-id="ec03c-132">Well described</span></span>

<span data-ttu-id="ec03c-133">テキスト、アイコン、および画像により、アプリの目的と使用方法が明確になります。</span><span class="sxs-lookup"><span data-stu-id="ec03c-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="ec03c-134">まとまりのあるエクスペリエンスを作成する</span><span class="sxs-lookup"><span data-stu-id="ec03c-134">Creating a cohesive experience</span></span>

<span data-ttu-id="ec03c-135">Teamsアプリの設計は、従来の Web アプリの設計と似ていますが、少し異なります。</span><span class="sxs-lookup"><span data-stu-id="ec03c-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="ec03c-136">効果的なデザインでは、アプリの独自の属性を強調しながら、Teams機能とコンテキストに自然に適合します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="ec03c-137">これらのガイドラインとリソースは、そのバランスを取る際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="ec03c-138">Teams アプリを設計する際の操作と回避方法 (タブ内の複数レベルのナビゲーションなど) を把握できます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="ec03c-139">アプリの計画</span><span class="sxs-lookup"><span data-stu-id="ec03c-139">Planning your app</span></span>

<span data-ttu-id="ec03c-140">高品質のTeamsアプリを設計するには、まずアプリの実行方法と、アプリの使用方法を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ec03c-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="ec03c-141">まだお持ちの場合は、しばらく時間をかけて [アプリを適切に計画してください](../../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="ec03c-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="ec03c-142">デザインの基本事項</span><span class="sxs-lookup"><span data-stu-id="ec03c-142">Design fundamentals</span></span>

<span data-ttu-id="ec03c-143">レイアウト[、配色など、Teamsアプリデザインの基本](design-teams-app-fundamentals.md)について説明します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="ec03c-144">Teams用の基本的な Fluent UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="ec03c-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="ec03c-145">Fluent UI に基づいて、これらは[使い慣れたTeamsインターフェイスを作成するためのコア要素です](design-teams-app-basic-ui-components.md)。</span><span class="sxs-lookup"><span data-stu-id="ec03c-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="ec03c-146">UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="ec03c-146">UI templates</span></span>

<span data-ttu-id="ec03c-147">[一般的なTeamsのユースケースやワークフロー用のテンプレート](design-teams-app-ui-templates.md)を使用して、複雑で忠実度の高いデザインをすばやく作成できます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="ec03c-148">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="ec03c-148">App capabilities</span></span>

<span data-ttu-id="ec03c-149">デザインの各機能を最大限に活用するために、Teamsアプリの追加、使用、管理の方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="ec03c-150">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="ec03c-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="ec03c-151">タブ</span><span class="sxs-lookup"><span data-stu-id="ec03c-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="ec03c-152">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="ec03c-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="ec03c-153">ボット</span><span class="sxs-lookup"><span data-stu-id="ec03c-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="ec03c-154">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="ec03c-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="ec03c-155">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="ec03c-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="ec03c-156">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="ec03c-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="ec03c-157">アプリのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="ec03c-157">App customization</span></span>

<span data-ttu-id="ec03c-158">Teams管理者が組織のニーズに応じてアプリをカスタマイズまたはブランド変更する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="ec03c-159">このカスタマイズは、マニフェスト スキーマで を定義する場合 `configurableProperties` に有効になります。</span><span class="sxs-lookup"><span data-stu-id="ec03c-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="ec03c-160">詳しくは[、Microsoft Teamsでのアプリのカスタマイズを](/MicrosoftTeams/customize-apps)参照してください。</span><span class="sxs-lookup"><span data-stu-id="ec03c-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="ec03c-161">アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれるアプリのルック アンド フィールを変更できます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-161">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="ec03c-162">たとえば、Teams管理者が *Contoso* から *Contoso エージェント* にアプリの名前をカスタマイズすると、アプリは新しい名前の *Contoso エージェント* をユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-162">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="ec03c-163">ただし、チャットにコネクタを追加する間は、一覧に表示されるコネクタには、Contoso *というアプリ* の名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-163">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="ec03c-164">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ec03c-164">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="ec03c-165">詳細については、「 [Microsoft Teams でアプリをカスタマイズする](/MicrosoftTeams/customize-apps)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ec03c-165">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="ec03c-166">ツールとサンプル</span><span class="sxs-lookup"><span data-stu-id="ec03c-166">Tools and samples</span></span>

<span data-ttu-id="ec03c-167">デザイナーや開発者が使い始めるには、次のツールが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-167">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ec03c-168">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="ec03c-168">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ec03c-169">必要に応じてドラッグ、ドロップ、および変更できる UI コンポーネント、テンプレート、例を使用して、Teamsアプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-169">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="ec03c-170">UI キットには、さまざまなTeamsシナリオでアプリがどのように見え、動作するかについての包括的な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="ec03c-170">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec03c-171">UIキットを入手する(Figma)</span><span class="sxs-lookup"><span data-stu-id="ec03c-171">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="ec03c-172">Microsoft TeamsUI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="ec03c-172">Microsoft Teams UI Library</span></span>

<span data-ttu-id="ec03c-173">ブラウザーで個々のTeams UI テンプレートおよび関連コンポーネントを表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="ec03c-173">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec03c-174">UIライブラリ(プレイグラウンド)を試してみてください</span><span class="sxs-lookup"><span data-stu-id="ec03c-174">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="ec03c-175">これらのテンプレートと関連コンポーネントをTeams アプリ プロジェクトに直接インポートします。</span><span class="sxs-lookup"><span data-stu-id="ec03c-175">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec03c-176">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="ec03c-176">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="ec03c-177">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="ec03c-177">Sample app</span></span>

<span data-ttu-id="ec03c-178">サンプル アプリをインストールして、UI テンプレートの外観と動作をTeamsコンテキストで確認します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-178">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec03c-179">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="ec03c-179">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="ec03c-180">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="ec03c-180">Other resources</span></span>

<span data-ttu-id="ec03c-181">詳細については、次のいずれかのリソースを試してください。</span><span class="sxs-lookup"><span data-stu-id="ec03c-181">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="ec03c-182">流暢な UI ドキュメント</span><span class="sxs-lookup"><span data-stu-id="ec03c-182">Fluent UI documentation</span></span>

<span data-ttu-id="ec03c-183">Teams エクスペリエンスの構築に使用される Fluent UI ベースのコンポーネントのコード サンプルと実装の詳細を取得します。</span><span class="sxs-lookup"><span data-stu-id="ec03c-183">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec03c-184">UI コンポーネントTeams試す (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="ec03c-184">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="ec03c-185">アダプティブカードデザイナー</span><span class="sxs-lookup"><span data-stu-id="ec03c-185">Adaptive Cards designer</span></span>

<span data-ttu-id="ec03c-186">アダプティブカードは、ウェブベースのツールでデザインできます。</span><span class="sxs-lookup"><span data-stu-id="ec03c-186">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec03c-187">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="ec03c-187">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
