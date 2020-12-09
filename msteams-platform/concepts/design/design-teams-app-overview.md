---
title: カスタムアプリを設計する
author: heath-hamilton
description: Microsoft Teams アプリを設計する方法について説明します。 リソースには、Microsoft Teams UI Kit、ベストプラクティス、例などが含まれます。
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0160a59ed4ebc51e900acbb5d74735ccae0b6083
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606015"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="98593-104">Microsoft Teams アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="98593-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Microsoft Teams 設計ガイドラインの概要を説明するイメージ。":::

<span data-ttu-id="98593-106">低コードツールを使用して、デザイナー、製品マネージャー、開発者、または開発者であるかどうかにかかわらず、これらのガイドラインは、Microsoft Teams アプリに対して適切な設計上の決定を迅速に行うのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="98593-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="98593-107">Teams アプリ設計の原則</span><span class="sxs-lookup"><span data-stu-id="98593-107">Teams app design principles</span></span>

<span data-ttu-id="98593-108">Teams アプリは、ユーザーがより多くのことを実現するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="98593-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="98593-109">設計をガイドするには、これらの原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="98593-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="98593-110">業務</span><span class="sxs-lookup"><span data-stu-id="98593-110">Collaborative</span></span>

<span data-ttu-id="98593-111">Teams アプリは、ユーザーがより多くのことを実現するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="98593-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="98593-112">設計をガイドするには、これらの原則を使用します。</span><span class="sxs-lookup"><span data-stu-id="98593-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="98593-113">信用</span><span class="sxs-lookup"><span data-stu-id="98593-113">Trustworthy</span></span>

<span data-ttu-id="98593-114">アプリはセキュリティで保護され、準拠しています。</span><span class="sxs-lookup"><span data-stu-id="98593-114">The app is secure and compliant.</span></span> <span data-ttu-id="98593-115">ユーザーは、プライバシーに関する情報を簡単に見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="98593-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="98593-116">グローバル包括</span><span class="sxs-lookup"><span data-stu-id="98593-116">Globally inclusive</span></span>

<span data-ttu-id="98593-117">すべての背景、skillsets、および分野の人々は、アプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="98593-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="98593-118">カルチャ、racially、および socially に対応します。</span><span class="sxs-lookup"><span data-stu-id="98593-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="98593-119">低負荷</span><span class="sxs-lookup"><span data-stu-id="98593-119">Light</span></span>

<span data-ttu-id="98593-120">アプリは、Teams ワークフローと組み合わせたコアシナリオに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="98593-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="98593-121">ネイティブまたは個別</span><span class="sxs-lookup"><span data-stu-id="98593-121">Native or distinct</span></span>

<span data-ttu-id="98593-122">アプリでは、ネイティブの Teams デザインコンポーネントまたは独自のコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="98593-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="98593-123">配色パターン、コントロールなどは混在していません。</span><span class="sxs-lookup"><span data-stu-id="98593-123">There’s no blend of color schemes, controls, etc.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="98593-124">とき</span><span class="sxs-lookup"><span data-stu-id="98593-124">Useful</span></span>

<span data-ttu-id="98593-125">アプリは、ユーザーが Teams で行う必要のあるシナリオに基づいています。</span><span class="sxs-lookup"><span data-stu-id="98593-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="98593-126">使いやすい</span><span class="sxs-lookup"><span data-stu-id="98593-126">Easy to use</span></span>

<span data-ttu-id="98593-127">UI は、わかりやすく、ルックアンドトーンがよく、ユーザーの生産性を向上させるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="98593-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="98593-128">速い</span><span class="sxs-lookup"><span data-stu-id="98593-128">Responsive</span></span>

<span data-ttu-id="98593-129">アプリはデバイスと画面に依存しません。</span><span class="sxs-lookup"><span data-stu-id="98593-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="98593-130">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="98593-130">Accessible</span></span>

<span data-ttu-id="98593-131">アプリは、色のコントラスト、移動方法など、Teams のアクセシビリティ要件を満たしています。</span><span class="sxs-lookup"><span data-stu-id="98593-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="98593-132">よく説明</span><span class="sxs-lookup"><span data-stu-id="98593-132">Well described</span></span>

<span data-ttu-id="98593-133">テキスト、アイコン、画像によって、アプリの用途と使用方法が明確になります。</span><span class="sxs-lookup"><span data-stu-id="98593-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="98593-134">凝集した環境を作成する</span><span class="sxs-lookup"><span data-stu-id="98593-134">Creating a cohesive experience</span></span>

<span data-ttu-id="98593-135">Teams アプリを設計することは、従来の web アプリの設計に似ていますが、多少異なるものです。</span><span class="sxs-lookup"><span data-stu-id="98593-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="98593-136">効果的なデザインでは、アプリの一意の属性を強調表示する一方で、Teams の機能やコンテキストを自然に調整します。</span><span class="sxs-lookup"><span data-stu-id="98593-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="98593-137">これらのガイドラインとリソースは、そのバランスを取るのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="98593-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="98593-138">Teams アプリを設計するときに何ができるか、何を回避するか (タブ内の複数レベルのナビゲーションなど) について説明します。</span><span class="sxs-lookup"><span data-stu-id="98593-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="98593-139">アプリを計画する</span><span class="sxs-lookup"><span data-stu-id="98593-139">Planning your app</span></span>

<span data-ttu-id="98593-140">高品質 Teams アプリを設計するには、まず、アプリに対して実行する操作とその使用方法を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="98593-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="98593-141">まだ作業していない場合は、アプリを正しく [計画](../../concepts/extensibility-points.md)するためにしばらく時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="98593-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="98593-142">設計の基礎</span><span class="sxs-lookup"><span data-stu-id="98593-142">Design fundamentals</span></span>

<span data-ttu-id="98593-143">レイアウト、配色など、 [Teams アプリデザインの基本事項](design-teams-app-fundamentals.md)について説明します。</span><span class="sxs-lookup"><span data-stu-id="98593-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="98593-144">Teams の基本的な Fluent UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="98593-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="98593-145">Fluent UI に基づいて、これらは [一般的な Teams インターフェイスを作成するための中心的な要素](design-teams-app-basic-ui-components.md)です。</span><span class="sxs-lookup"><span data-stu-id="98593-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="98593-146">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="98593-146">App capabilities</span></span>

<span data-ttu-id="98593-147">ユーザーがチームアプリを追加、使用、および管理して、設計の各機能を最大限に活用する方法について理解します。</span><span class="sxs-lookup"><span data-stu-id="98593-147">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="98593-148">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="98593-148">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="98593-149">タブ</span><span class="sxs-lookup"><span data-stu-id="98593-149">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="98593-150">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="98593-150">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="98593-151">ボット</span><span class="sxs-lookup"><span data-stu-id="98593-151">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="98593-152">会議の内線番号</span><span class="sxs-lookup"><span data-stu-id="98593-152">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="98593-153">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="98593-153">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="98593-154">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="98593-154">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="ui-templates"></a><span data-ttu-id="98593-155">UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="98593-155">UI templates</span></span>

<span data-ttu-id="98593-156">[一般的な Teams のユースケースとワークフローのテンプレート](design-teams-app-ui-templates.md)を使用して、複雑で忠実なデザインをすばやく作成できます。</span><span class="sxs-lookup"><span data-stu-id="98593-156">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="get-started-with-the-microsoft-teams-ui-kit"></a><span data-ttu-id="98593-157">Microsoft Teams UI キットを使用して作業を開始する</span><span class="sxs-lookup"><span data-stu-id="98593-157">Get started with the Microsoft Teams UI Kit</span></span>

<span data-ttu-id="98593-158">Microsoft Teams UI キットには、UI コンポーネント、テンプレート、および、必要に応じてドラッグ、ドロップ、および変更できる例があります。</span><span class="sxs-lookup"><span data-stu-id="98593-158">The Microsoft Teams UI Kit has UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="98593-159">UI キットには、さまざまな Teams シナリオでのアプリの外観や動作に関する包括的な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="98593-159">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98593-160">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="98593-160">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="other-resources"></a><span data-ttu-id="98593-161">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="98593-161">Other resources</span></span>

<span data-ttu-id="98593-162">詳細については、次のいずれかのリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="98593-162">To learn more, try one of the following resources.</span></span>

### <a name="fluent-ui"></a><span data-ttu-id="98593-163">Fluent UI</span><span class="sxs-lookup"><span data-stu-id="98593-163">Fluent UI</span></span>

<span data-ttu-id="98593-164">Teams エクスペリエンスの構築に使用される Fluent UI ベースコンポーネントのコードサンプルと実装の詳細を取得します。</span><span class="sxs-lookup"><span data-stu-id="98593-164">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98593-165">Teams UI コンポーネントを試す (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="98593-165">Try out Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="98593-166">アダプティブカードデザイナー</span><span class="sxs-lookup"><span data-stu-id="98593-166">Adaptive Cards designer</span></span>

<span data-ttu-id="98593-167">Web ベースのツールでアダプティブカードをデザインします。</span><span class="sxs-lookup"><span data-stu-id="98593-167">Design Adaptive Cards in a web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98593-168">アダプティブカードデザイナーを試す</span><span class="sxs-lookup"><span data-stu-id="98593-168">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
