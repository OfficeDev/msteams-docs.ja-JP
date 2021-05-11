---
title: カスタム アプリの設計
author: heath-hamilton
description: アプリを設計するMicrosoft Teamsします。 リソースには、MICROSOFT TEAMS UI キット、ベスト プラクティス、例などがあります。
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: ab311b6b9b8494308916ef602ee98785ab6de61e
ms.sourcegitcommit: 808a203fb963eeade3a8e32db88d64677e37df7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2021
ms.locfileid: "52304027"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="be246-104">アプリのMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="be246-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="設計ガイドラインに関するMicrosoft Teams概念図。":::

<span data-ttu-id="be246-106">低コード ツールを使用しているデザイナー、製品マネージャー、開発者、メーカーなど、これらのガイドラインは、Microsoft Teams アプリに対して適切な設計上の意思決定を迅速に行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="be246-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="be246-107">Teamsの設計原則</span><span class="sxs-lookup"><span data-stu-id="be246-107">Teams app design principles</span></span>

<span data-ttu-id="be246-108">Teamsアプリは、ユーザーが一緒に達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="be246-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="be246-109">設計をガイドするには、次の原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="be246-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="be246-110">共同作業</span><span class="sxs-lookup"><span data-stu-id="be246-110">Collaborative</span></span>

<span data-ttu-id="be246-111">Teamsアプリは、ユーザーが一緒に達成するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="be246-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="be246-112">設計をガイドするには、次の原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="be246-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="be246-113">信頼できる</span><span class="sxs-lookup"><span data-stu-id="be246-113">Trustworthy</span></span>

<span data-ttu-id="be246-114">アプリは安全で準拠しています。</span><span class="sxs-lookup"><span data-stu-id="be246-114">The app is secure and compliant.</span></span> <span data-ttu-id="be246-115">ユーザーは、プライバシーに関する情報を簡単に見つくことができます。</span><span class="sxs-lookup"><span data-stu-id="be246-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="be246-116">グローバルに包括的</span><span class="sxs-lookup"><span data-stu-id="be246-116">Globally inclusive</span></span>

<span data-ttu-id="be246-117">すべてのバックグラウンド、スキルセット、および専門分野のユーザーは、アプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="be246-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="be246-118">文化的、人種的、社会的に認識しています。</span><span class="sxs-lookup"><span data-stu-id="be246-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="be246-119">低負荷</span><span class="sxs-lookup"><span data-stu-id="be246-119">Light</span></span>

<span data-ttu-id="be246-120">アプリは、ワークフローとブレンドするコア シナリオTeamsしています。</span><span class="sxs-lookup"><span data-stu-id="be246-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="be246-121">ネイティブまたは個別</span><span class="sxs-lookup"><span data-stu-id="be246-121">Native or distinct</span></span>

<span data-ttu-id="be246-122">アプリは、ネイティブ のTeamsコンポーネントまたは独自のコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="be246-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="be246-123">配色、コントロールなどのブレンドはありません。</span><span class="sxs-lookup"><span data-stu-id="be246-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="be246-124">役に立つ</span><span class="sxs-lookup"><span data-stu-id="be246-124">Useful</span></span>

<span data-ttu-id="be246-125">アプリは、ユーザーがユーザーが必要とするシナリオに基づいて、Teams。</span><span class="sxs-lookup"><span data-stu-id="be246-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="be246-126">使いやすい</span><span class="sxs-lookup"><span data-stu-id="be246-126">Easy to use</span></span>

<span data-ttu-id="be246-127">UI はわかりやすいので、見た目とトーンが快適で、ユーザーの生産性が向上します。</span><span class="sxs-lookup"><span data-stu-id="be246-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="be246-128">速い</span><span class="sxs-lookup"><span data-stu-id="be246-128">Responsive</span></span>

<span data-ttu-id="be246-129">アプリはデバイスであり、画面に依存しない。</span><span class="sxs-lookup"><span data-stu-id="be246-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="be246-130">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="be246-130">Accessible</span></span>

<span data-ttu-id="be246-131">このアプリは、Teams、ナビゲーションの代替など、ユーザー補助の要件を満たしています。</span><span class="sxs-lookup"><span data-stu-id="be246-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="be246-132">よく説明</span><span class="sxs-lookup"><span data-stu-id="be246-132">Well described</span></span>

<span data-ttu-id="be246-133">テキスト、アイコン、画像を使用すると、アプリが何を使用し、どのように使うのかを明確にできます。</span><span class="sxs-lookup"><span data-stu-id="be246-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="be246-134">一つ一つのエクスペリエンスを作成する</span><span class="sxs-lookup"><span data-stu-id="be246-134">Creating a cohesive experience</span></span>

<span data-ttu-id="be246-135">アプリのTeamsは、従来の Web アプリの設計と同じですが、少し異なります。</span><span class="sxs-lookup"><span data-stu-id="be246-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="be246-136">効果的な設計では、アプリの固有の属性を強調しながら、アプリの機能やコンテキストTeams自然にフィットします。</span><span class="sxs-lookup"><span data-stu-id="be246-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="be246-137">これらのガイドラインとリソースは、バランスを取る際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="be246-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="be246-138">アプリを設計するときに何を行い、何を回避Teams (タブ内の複数レベルのナビゲーションなど) が分かっています。</span><span class="sxs-lookup"><span data-stu-id="be246-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="be246-139">アプリの計画</span><span class="sxs-lookup"><span data-stu-id="be246-139">Planning your app</span></span>

<span data-ttu-id="be246-140">高品質のアプリをTeamsするには、まずアプリが何を行うのか、ユーザーがアプリを使用すると思う方法を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be246-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="be246-141">まだ計画していない場合は、アプリを適切に計画 [するために少し時間を取ってください](../../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="be246-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="be246-142">デザインの基本事項</span><span class="sxs-lookup"><span data-stu-id="be246-142">Design fundamentals</span></span>

<span data-ttu-id="be246-143">レイアウト[、配色Teamsなど、](design-teams-app-fundamentals.md)アプリ設計の基本について学習します。</span><span class="sxs-lookup"><span data-stu-id="be246-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="be246-144">ユーザーの基本的な Fluent UI コンポーネントTeams</span><span class="sxs-lookup"><span data-stu-id="be246-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="be246-145">Fluent UI に基づいて、使い慣れたインターフェイス[を作成するためのTeamsです](design-teams-app-basic-ui-components.md)。</span><span class="sxs-lookup"><span data-stu-id="be246-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="be246-146">UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="be246-146">UI templates</span></span>

<span data-ttu-id="be246-147">一般的な使用例やワークフロー用のテンプレートを使用して、複雑で忠実[度Teamsをすばやく作成します](design-teams-app-ui-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="be246-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="be246-148">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="be246-148">App capabilities</span></span>

<span data-ttu-id="be246-149">ユーザーがアプリを追加、使用、管理する方法Teams設計の各機能を有効に利用する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="be246-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="be246-150">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="be246-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="be246-151">タブ</span><span class="sxs-lookup"><span data-stu-id="be246-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="be246-152">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="be246-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="be246-153">ボット</span><span class="sxs-lookup"><span data-stu-id="be246-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="be246-154">ミーディング拡張機能</span><span class="sxs-lookup"><span data-stu-id="be246-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="be246-155">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="be246-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="be246-156">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="be246-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="be246-157">アプリのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="be246-157">App customization</span></span>

<span data-ttu-id="be246-158">管理者が組織Teamsに基づいてアプリをカスタマイズまたは再ブランド化する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="be246-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="be246-159">このカスタマイズは、マニフェスト スキーマで定義 `configurableProperties` する場合に有効になります。</span><span class="sxs-lookup"><span data-stu-id="be246-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="be246-160">詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="be246-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="be246-161">アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれたアプリの外観を変更できます。</span><span class="sxs-lookup"><span data-stu-id="be246-161">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="be246-162">たとえば、管理者Teams Contoso から *Contoso* *エージェント* にアプリの名前をカスタマイズすると、ユーザーに Contoso *Agent* という新しい名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="be246-162">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="be246-163">ただし、チャットにコネクタを追加している間、一覧でコネクタは引き続きアプリの名前を Contoso として表示 *します*。</span><span class="sxs-lookup"><span data-stu-id="be246-163">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="be246-164">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be246-164">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="be246-165">詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="be246-165">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="be246-166">ツールとサンプル</span><span class="sxs-lookup"><span data-stu-id="be246-166">Tools and samples</span></span>

<span data-ttu-id="be246-167">次のツールは、デザイナーと開発者が始めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="be246-167">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="be246-168">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="be246-168">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="be246-169">UI コンポーネントTeamsテンプレート、および必要に応じてドラッグ、ドロップ、および変更できる例を含むアプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="be246-169">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="be246-170">UI キットには、さまざまなシナリオでのアプリの外観と動作に関する包括的なTeams含まれています。</span><span class="sxs-lookup"><span data-stu-id="be246-170">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be246-171">UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="be246-171">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="be246-172">Microsoft TeamsUI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="be246-172">Microsoft Teams UI Library</span></span>

<span data-ttu-id="be246-173">ブラウザーで UI テンプレートTeams関連するコンポーネントを個別に表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="be246-173">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be246-174">UI ライブラリ (プレイグラウンド) を試す</span><span class="sxs-lookup"><span data-stu-id="be246-174">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="be246-175">これらのテンプレートと関連コンポーネントをアプリ プロジェクトに直接Teamsインポートします。</span><span class="sxs-lookup"><span data-stu-id="be246-175">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be246-176">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="be246-176">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="be246-177">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="be246-177">Sample app</span></span>

<span data-ttu-id="be246-178">サンプル アプリをインストールして、UI テンプレートの外観と動作を各コンテキストTeamsします。</span><span class="sxs-lookup"><span data-stu-id="be246-178">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be246-179">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="be246-179">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="be246-180">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="be246-180">Other resources</span></span>

<span data-ttu-id="be246-181">詳細については、次のいずれかのリソースを試してください。</span><span class="sxs-lookup"><span data-stu-id="be246-181">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="be246-182">Fluent UI のドキュメント</span><span class="sxs-lookup"><span data-stu-id="be246-182">Fluent UI documentation</span></span>

<span data-ttu-id="be246-183">ユーザー エクスペリエンスの構築に使用される Fluent UI ベースのコンポーネントのコード サンプルと実装Teams取得します。</span><span class="sxs-lookup"><span data-stu-id="be246-183">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be246-184">UI Teams試す (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="be246-184">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="be246-185">アダプティブ カード デザイナー</span><span class="sxs-lookup"><span data-stu-id="be246-185">Adaptive Cards designer</span></span>

<span data-ttu-id="be246-186">Web ベースのツールでアダプティブ カードを設計します。</span><span class="sxs-lookup"><span data-stu-id="be246-186">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="be246-187">アダプティブ カード デザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="be246-187">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
