---
title: カスタム アプリの設計
author: heath-hamilton
description: Microsoft Teams アプリを設計する方法について説明します。 リソースには、Microsoft Teams UI キット、ベスト プラクティス、例などがあります。
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: d7f3e89ce5ad51fb1a8cecddf0b22d59544ecc09
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019882"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="0f08c-104">Microsoft Teams アプリの設計</span><span class="sxs-lookup"><span data-stu-id="0f08c-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams の設計ガイドラインを紹介する概念図。":::

<span data-ttu-id="0f08c-106">低コード ツールを使用しているデザイナー、製品マネージャー、開発者、メーカーなど、これらのガイドラインは、Microsoft Teams アプリに対して適切な設計上の意思決定を迅速に行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="0f08c-107">Teams アプリの設計原則</span><span class="sxs-lookup"><span data-stu-id="0f08c-107">Teams app design principles</span></span>

<span data-ttu-id="0f08c-108">Teams アプリは、ユーザーが一緒に多くの成果を達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="0f08c-109">設計をガイドするには、次の原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="0f08c-110">共同作業</span><span class="sxs-lookup"><span data-stu-id="0f08c-110">Collaborative</span></span>

<span data-ttu-id="0f08c-111">Teams アプリは、ユーザーが一緒に多くの成果を達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="0f08c-112">設計をガイドするには、次の原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="0f08c-113">信頼できる</span><span class="sxs-lookup"><span data-stu-id="0f08c-113">Trustworthy</span></span>

<span data-ttu-id="0f08c-114">アプリは安全で準拠しています。</span><span class="sxs-lookup"><span data-stu-id="0f08c-114">The app is secure and compliant.</span></span> <span data-ttu-id="0f08c-115">ユーザーは、プライバシーに関する情報を簡単に見つくことができます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="0f08c-116">グローバルに包括的</span><span class="sxs-lookup"><span data-stu-id="0f08c-116">Globally inclusive</span></span>

<span data-ttu-id="0f08c-117">すべてのバックグラウンド、スキルセット、および専門分野のユーザーは、アプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="0f08c-118">文化的、人種的、社会的に認識しています。</span><span class="sxs-lookup"><span data-stu-id="0f08c-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="0f08c-119">低負荷</span><span class="sxs-lookup"><span data-stu-id="0f08c-119">Light</span></span>

<span data-ttu-id="0f08c-120">このアプリは、Teams ワークフローと組み合うコア シナリオに焦点を当てしています。</span><span class="sxs-lookup"><span data-stu-id="0f08c-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="0f08c-121">ネイティブまたは個別</span><span class="sxs-lookup"><span data-stu-id="0f08c-121">Native or distinct</span></span>

<span data-ttu-id="0f08c-122">アプリは、ネイティブの Teams デザイン コンポーネントまたは独自のコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="0f08c-123">配色、コントロールなどのブレンドはありません。</span><span class="sxs-lookup"><span data-stu-id="0f08c-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="0f08c-124">役に立つ</span><span class="sxs-lookup"><span data-stu-id="0f08c-124">Useful</span></span>

<span data-ttu-id="0f08c-125">アプリは、Teams でユーザーが行う必要があるシナリオに基づいて作成されます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="0f08c-126">使いやすい</span><span class="sxs-lookup"><span data-stu-id="0f08c-126">Easy to use</span></span>

<span data-ttu-id="0f08c-127">UI はわかりやすいので、見た目とトーンが快適で、ユーザーの生産性が向上します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="0f08c-128">速い</span><span class="sxs-lookup"><span data-stu-id="0f08c-128">Responsive</span></span>

<span data-ttu-id="0f08c-129">アプリはデバイスであり、画面に依存しない。</span><span class="sxs-lookup"><span data-stu-id="0f08c-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="0f08c-130">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="0f08c-130">Accessible</span></span>

<span data-ttu-id="0f08c-131">アプリは、色のコントラスト、ナビゲーションの選択肢など、Teams のアクセシビリティ要件を満たしています。</span><span class="sxs-lookup"><span data-stu-id="0f08c-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="0f08c-132">よく説明</span><span class="sxs-lookup"><span data-stu-id="0f08c-132">Well described</span></span>

<span data-ttu-id="0f08c-133">テキスト、アイコン、画像を使用すると、アプリが何を使用し、どのように使うのかを明確にできます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="0f08c-134">一つ一つのエクスペリエンスを作成する</span><span class="sxs-lookup"><span data-stu-id="0f08c-134">Creating a cohesive experience</span></span>

<span data-ttu-id="0f08c-135">Teams アプリの設計は、従来の Web アプリの設計と似たものですが、少し異なります。</span><span class="sxs-lookup"><span data-stu-id="0f08c-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="0f08c-136">効果的な設計は、Teams の機能とコンテキストに自然に適合しながら、アプリの固有の属性を強調します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="0f08c-137">これらのガイドラインとリソースは、バランスを取る際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="0f08c-138">Teams アプリを設計する際の操作と回避方法 (タブ内のマルチレベル ナビゲーションなど) が分かっています。</span><span class="sxs-lookup"><span data-stu-id="0f08c-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="0f08c-139">アプリの計画</span><span class="sxs-lookup"><span data-stu-id="0f08c-139">Planning your app</span></span>

<span data-ttu-id="0f08c-140">高品質の Teams アプリを設計するには、まずアプリで実行する操作と、ユーザーがアプリを使用すると思う方法を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f08c-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="0f08c-141">まだ計画していない場合は、アプリを適切に計画 [するために少し時間を取ってください](../../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="0f08c-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="0f08c-142">デザインの基本事項</span><span class="sxs-lookup"><span data-stu-id="0f08c-142">Design fundamentals</span></span>

<span data-ttu-id="0f08c-143">レイアウト、 [配色など、Teams](design-teams-app-fundamentals.md)アプリ設計の基本について学習します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="0f08c-144">Teams の基本的な Fluent UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="0f08c-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="0f08c-145">Fluent UI に基づいて、これらは使い慣れた Teams インターフェイス [を作成するための主要な要素です](design-teams-app-basic-ui-components.md)。</span><span class="sxs-lookup"><span data-stu-id="0f08c-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="0f08c-146">UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="0f08c-146">UI templates</span></span>

<span data-ttu-id="0f08c-147">一般的な Teams の使用例とワークフロー用のテンプレートを使用して、複雑で忠実度の高いデザイン [をすばやく作成できます](design-teams-app-ui-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="0f08c-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="0f08c-148">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="0f08c-148">App capabilities</span></span>

<span data-ttu-id="0f08c-149">ユーザーが Teams アプリを追加、使用、および管理して、デザイン内の各機能を有効に利用する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="0f08c-150">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="0f08c-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="0f08c-151">タブ</span><span class="sxs-lookup"><span data-stu-id="0f08c-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="0f08c-152">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="0f08c-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="0f08c-153">ボット</span><span class="sxs-lookup"><span data-stu-id="0f08c-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="0f08c-154">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="0f08c-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="0f08c-155">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="0f08c-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="0f08c-156">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="0f08c-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="0f08c-157">アプリのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="0f08c-157">App customization</span></span>

<span data-ttu-id="0f08c-158">Teams 管理者が組織のニーズに基づいてアプリをカスタマイズまたは再ブランド化する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="0f08c-159">このカスタマイズは、マニフェスト スキーマで定義 `configurableProperties` する場合に有効になります。</span><span class="sxs-lookup"><span data-stu-id="0f08c-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="0f08c-160">詳細については [、「Microsoft Teams でアプリをカスタマイズする」を参照してください](/MicrosoftTeams/customize-apps)。</span><span class="sxs-lookup"><span data-stu-id="0f08c-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="0f08c-161">この機能は現在、開発者プレビューでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-161">This feature is currently available in developer preview only.</span></span>
> 
> <span data-ttu-id="0f08c-162">アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれたアプリの外観を変更できます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-162">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="0f08c-163">たとえば、Teams 管理者が Contoso から *Contoso Agent* にアプリの名前をカスタマイズすると、そのアプリは Contoso *Agent* という新しい名前でユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-163">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="0f08c-164">ただし、チャットにコネクタを追加している間、一覧でコネクタは引き続きアプリの名前を Contoso として表示 *します*。</span><span class="sxs-lookup"><span data-stu-id="0f08c-164">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="0f08c-165">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f08c-165">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="0f08c-166">詳細については [、「Microsoft Teams でのアプリのカスタマイズ」を参照してください](/MicrosoftTeams/customize-apps)。</span><span class="sxs-lookup"><span data-stu-id="0f08c-166">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="0f08c-167">ツールとサンプル</span><span class="sxs-lookup"><span data-stu-id="0f08c-167">Tools and samples</span></span>

<span data-ttu-id="0f08c-168">次のツールは、デザイナーと開発者が始めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0f08c-168">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0f08c-169">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="0f08c-169">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0f08c-170">UI コンポーネント、テンプレート、および必要に応じてドラッグ、ドロップ、および変更できる例を使用して Teams アプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-170">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="0f08c-171">UI キットには、さまざまな Teams シナリオでのアプリの外観と動作に関する包括的な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="0f08c-171">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f08c-172">UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="0f08c-172">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="0f08c-173">Microsoft Teams UI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="0f08c-173">Microsoft Teams UI Library</span></span>

<span data-ttu-id="0f08c-174">ブラウザーで個々の Teams UI テンプレートと関連コンポーネントを表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="0f08c-174">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f08c-175">UI ライブラリ (プレイグラウンド) を試す</span><span class="sxs-lookup"><span data-stu-id="0f08c-175">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="0f08c-176">これらのテンプレートと関連コンポーネントを Teams アプリ プロジェクトに直接インポートします。</span><span class="sxs-lookup"><span data-stu-id="0f08c-176">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f08c-177">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="0f08c-177">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="0f08c-178">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="0f08c-178">Sample app</span></span>

<span data-ttu-id="0f08c-179">サンプル アプリをインストールして、Teams コンテキスト内での UI テンプレートの外観と動作を確認します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-179">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f08c-180">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="0f08c-180">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="0f08c-181">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="0f08c-181">Other resources</span></span>

<span data-ttu-id="0f08c-182">詳細については、次のいずれかのリソースを試してください。</span><span class="sxs-lookup"><span data-stu-id="0f08c-182">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="0f08c-183">Fluent UI のドキュメント</span><span class="sxs-lookup"><span data-stu-id="0f08c-183">Fluent UI documentation</span></span>

<span data-ttu-id="0f08c-184">Teams エクスペリエンスの構築に使用する Fluent UI ベースのコンポーネントのコード サンプルと実装の詳細を取得します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-184">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f08c-185">Teams UI コンポーネントを試す (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="0f08c-185">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="0f08c-186">アダプティブ カード デザイナー</span><span class="sxs-lookup"><span data-stu-id="0f08c-186">Adaptive Cards designer</span></span>

<span data-ttu-id="0f08c-187">Web ベースのツールでアダプティブ カードを設計します。</span><span class="sxs-lookup"><span data-stu-id="0f08c-187">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f08c-188">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="0f08c-188">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
