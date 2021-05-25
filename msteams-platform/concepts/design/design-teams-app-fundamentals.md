---
title: アプリを設計する - デザイン システムについて
description: レイアウト、配色など、Microsoft Teamsアプリの設計の基本について説明します。
author: heath-hamilton
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0af2a22200e62be9289f167b0306c9769366e46a
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630843"
---
# <a name="microsoft-teams-app-design-system"></a><span data-ttu-id="458f7-103">Microsoft Teamsデザイン システム</span><span class="sxs-lookup"><span data-stu-id="458f7-103">Microsoft Teams app design system</span></span>

<span data-ttu-id="458f7-104">アプリ設計の基本Teamsすぐに学ぶ。</span><span class="sxs-lookup"><span data-stu-id="458f7-104">Quickly learn about the fundamentals of Teams app design.</span></span> <span data-ttu-id="458f7-105">包括的なガイダンスと例については、「UI<a href="https://www.figma.com/community/file/916836509871353159" target="_blank">キット (Figma)Microsoft Teamsを参照してください</a>。</span><span class="sxs-lookup"><span data-stu-id="458f7-105">You can find comprehensive guidance and examples in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma)</a>.</span></span>

## <a name="layout"></a><span data-ttu-id="458f7-106">レイアウト</span><span class="sxs-lookup"><span data-stu-id="458f7-106">Layout</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="458f7-107">Teamsは、デザイン コンポーネント間の一貫性と優雅な関係を確保するためにグリッド レイアウトに依存しています。</span><span class="sxs-lookup"><span data-stu-id="458f7-107">Teams relies on a grid layout to ensure consistent and elegant relationships between design components.</span></span> <span data-ttu-id="458f7-108">グリッドの 4 ピクセルベースユニットを使用すると、コンポーネントは、すべてのディスプレイ サイズにわたって一貫してスケールTeams。</span><span class="sxs-lookup"><span data-stu-id="458f7-108">The grid’s 4-pixel base unit allows components to scale consistently across all display sizes in Teams.</span></span>

      * [<span data-ttu-id="458f7-109">完全なレイアウト ガイドライン (Figma) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="458f7-109">See full layout guidelines (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)
      * [<span data-ttu-id="458f7-110">レイアウトの実装 (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="458f7-110">Implement layout (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/layout)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-layout.png" alt-text="レイアウトの概Teamsイメージ。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="avatars"></a><span data-ttu-id="458f7-112">アバター</span><span class="sxs-lookup"><span data-stu-id="458f7-112">Avatars</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="458f7-113">アバターは、ユーザー、チーム、ボット、またはエンティティのグラフィックTeams。</span><span class="sxs-lookup"><span data-stu-id="458f7-113">An avatar is a graphical representation of a person, team, bot, or entity in Teams.</span></span> <span data-ttu-id="458f7-114">アバター グループは、多くの場合、垂直空間を保持する方法で、ライブ アクティビティまたは名簿を表す場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="458f7-114">An avatar group is often used to convey live activity or a represent a roster in a way that preserves vertical space.</span></span> 

      * <span data-ttu-id="458f7-115"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なアバター ガイドライン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="458f7-115"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full avatar guidelines (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-avatars.png" alt-text="アバターの概念Teamsイメージ。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="icons"></a><span data-ttu-id="458f7-117">アイコン</span><span class="sxs-lookup"><span data-stu-id="458f7-117">Icons</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="458f7-118">アプリのプライマリ アイコンは、ユーザーにブランドを伝えるのに長いTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="458f7-118">Your app's primary icon can go a long way in conveying your brand to Teams users.</span></span> <span data-ttu-id="458f7-119">アイコンのデザインを正しい方法で取得する[](../../concepts/build-and-test/apps-package.md)方法は、アプリをアプリストアに発行Teams重要です。</span><span class="sxs-lookup"><span data-stu-id="458f7-119">Getting your icon design right is also important for [publishing your app](../../concepts/build-and-test/apps-package.md) to the Teams store.</span></span>

      <span data-ttu-id="458f7-120">アプリ全体で Fluent UI アイコンを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="458f7-120">You also can use Fluent UI icons throughout your app:</span></span>

      * <span data-ttu-id="458f7-121"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">最新の Fluent アイコン セットを取得する (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="458f7-121"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">Get the latest Fluent icon set (Figma)</a></span></span>
      * [<span data-ttu-id="458f7-122">アイコンの実装 (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="458f7-122">Implement the icons (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/icons)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-iconography.png" alt-text="アイコンの概Teamsイメージ。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="type"></a><span data-ttu-id="458f7-124">種類</span><span class="sxs-lookup"><span data-stu-id="458f7-124">Type</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="458f7-125">Teamsは、Segoe UI を使用して、その種類のランプと異なるフォント サイズと重みを使用して、階層を作成し、読みやすさを確保します。</span><span class="sxs-lookup"><span data-stu-id="458f7-125">Teams uses Segoe UI for its type ramp and different font sizes and weights to help create hierarchy and ensure readability.</span></span>

      * <span data-ttu-id="458f7-126"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全な種類のガイドライン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="458f7-126"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full type guidelines (Figma)</a></span></span>
      * [<span data-ttu-id="458f7-127">タイポグラフィの実装 (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="458f7-127">Implement typography (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/typography)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-typography.png" alt-text="タイポグラフィのTeamsイメージ。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="colors"></a><span data-ttu-id="458f7-129">色</span><span class="sxs-lookup"><span data-stu-id="458f7-129">Colors</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="458f7-130">Teams Web とデスクトップは既定の (明るいテーマ、暗いテーマ、ハイコントラストテーマ) をサポートしますが、Teamsは明るいテーマと暗いテーマをサポートします。</span><span class="sxs-lookup"><span data-stu-id="458f7-130">Teams web and desktop supports default (light), dark, and high-contrast themes, while Teams mobile supports light and dark themes.</span></span> <span data-ttu-id="458f7-131">各テーマには独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="458f7-131">Each theme has its own color scheme.</span></span>

      * <span data-ttu-id="458f7-132"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">フル カラー ガイドラインと使用可能なカラー トークン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="458f7-132"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full color guidelines and available color tokens (Figma)</a></span></span>
      * [<span data-ttu-id="458f7-133">色の実装 (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="458f7-133">Implement colors (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/0.51.7/colors)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-color.png" alt-text="色の概Teamsイメージ。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="shape-and-elevation"></a><span data-ttu-id="458f7-135">図形と標高</span><span class="sxs-lookup"><span data-stu-id="458f7-135">Shape and elevation</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="458f7-136">図形と昇格を使用して、アプリに追加の階層を作成できます。</span><span class="sxs-lookup"><span data-stu-id="458f7-136">You can use shape and elevation to create additional hierarchy in your app.</span></span> 

      * <span data-ttu-id="458f7-137"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全な図形と高度のガイドライン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="458f7-137"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full shape and elevation guidelines (Figma)</a></span></span>
      * [<span data-ttu-id="458f7-138">図形と昇格を実装する (Fluent UI)</span><span class="sxs-lookup"><span data-stu-id="458f7-138">Implement shape and elevation (Fluent UI)</span></span>](https://developer.microsoft.com/fluentui#/styles/web/elevation)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/shape-and-elevation.png" alt-text="図形と標高の概念。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="copy-and-content"></a><span data-ttu-id="458f7-140">コピーとコンテンツ</span><span class="sxs-lookup"><span data-stu-id="458f7-140">Copy and content</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="458f7-141">アプリの一部Teams、アプリ のコピーは、一般に、暖かくリラックスした、鮮明で明確で、手を貸す準備ができているという[Microsoft](/style-guide/brand-voice-above-all-simple-human)音声の原則に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="458f7-141">To feel part of Teams, your app copy in general should follow these [Microsoft voice principles](/style-guide/brand-voice-above-all-simple-human): warm and relaxed, crisp and clear, and ready to lend hand.</span></span>

      * <span data-ttu-id="458f7-142"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なコピーとコンテンツのガイドライン (ボット用の書き込みを含む) を参照してください (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="458f7-142"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full copy and content guidelines—including writing for bots (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-copy-and-content.png" alt-text="コピーとコンテンツの概念イメージ。" border="false":::

   :::column-end:::
:::row-end:::
