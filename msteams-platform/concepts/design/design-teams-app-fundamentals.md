---
title: アプリを設計する - 基本について
description: レイアウト、配色など、Microsoft Teams アプリの設計の基本について説明します。
author: heath-hamilton
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: c0edfe7ac538fc27b7f255cdd09d2853f6f4cebc
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020773"
---
# <a name="microsoft-teams-app-design-fundamentals"></a><span data-ttu-id="3628d-103">Microsoft Teams アプリの設計の基本</span><span class="sxs-lookup"><span data-stu-id="3628d-103">Microsoft Teams app design fundamentals</span></span>

<span data-ttu-id="3628d-104">Teams アプリの設計の基本について簡単に学ぶ。</span><span class="sxs-lookup"><span data-stu-id="3628d-104">Quickly learn about the fundamentals of Teams app design.</span></span> <span data-ttu-id="3628d-105">包括的なガイダンスと例については <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">、「Microsoft Teams UI Kit (Figma)」を参照してください</a>。</span><span class="sxs-lookup"><span data-stu-id="3628d-105">You can find comprehensive guidance and examples in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma)</a>.</span></span>

## <a name="layout"></a><span data-ttu-id="3628d-106">レイアウト</span><span class="sxs-lookup"><span data-stu-id="3628d-106">Layout</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="3628d-107">Teams は、デザイン コンポーネント間の一貫したエレガントな関係を確保するために、グリッド レイアウトに依存しています。</span><span class="sxs-lookup"><span data-stu-id="3628d-107">Teams relies on a grid layout to ensure consistent and elegant relationships between design components.</span></span> <span data-ttu-id="3628d-108">グリッドの 4 ピクセルベースユニットを使用すると、コンポーネントは Teams のすべての表示サイズにわたって一貫して拡大縮小できます。</span><span class="sxs-lookup"><span data-stu-id="3628d-108">The grid’s 4-pixel base unit allows components to scale consistently across all display sizes in Teams.</span></span>

      <span data-ttu-id="3628d-109"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なレイアウト ガイドライン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="3628d-109"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full layout guidelines (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-layout.png" alt-text="Microsoft Teams UI キットの概念イメージ。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="avatars"></a><span data-ttu-id="3628d-111">アバター</span><span class="sxs-lookup"><span data-stu-id="3628d-111">Avatars</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="3628d-112">アバターは、Teams の人物、チーム、ボット、またはエンティティのグラフィック表現です。</span><span class="sxs-lookup"><span data-stu-id="3628d-112">An avatar is a graphical representation of a person, team, bot, or entity in Teams.</span></span> <span data-ttu-id="3628d-113">アバター グループは、多くの場合、垂直空間を保持する方法で、ライブ アクティビティまたは名簿を表す場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="3628d-113">An avatar group is often used to convey live activity or a represent a roster in a way that preserves vertical space.</span></span> 

      <span data-ttu-id="3628d-114"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なアバター ガイドライン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="3628d-114"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full avatar guidelines (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-avatars.png" alt-text="Teams UI キットの概念イメージ。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="colors"></a><span data-ttu-id="3628d-116">色</span><span class="sxs-lookup"><span data-stu-id="3628d-116">Colors</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="3628d-117">Teams Web とデスクトップは既定の (明るいテーマ、暗いテーマ、ハイコントラストテーマ) をサポートし、Teams モバイルは明るいテーマと暗いテーマをサポートします。</span><span class="sxs-lookup"><span data-stu-id="3628d-117">Teams web and desktop supports default (light), dark, and high-contrast themes, while Teams mobile supports light and dark themes.</span></span> <span data-ttu-id="3628d-118">各テーマには独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="3628d-118">Each theme has its own color scheme.</span></span>

      <span data-ttu-id="3628d-119"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">フル カラー ガイドラインと使用可能なカラー トークン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="3628d-119"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full color guidelines and available color tokens (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-color.png" alt-text="Microsoft Teams UI キットの概念イメージ。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="iconography"></a><span data-ttu-id="3628d-121">アイコン</span><span class="sxs-lookup"><span data-stu-id="3628d-121">Iconography</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="3628d-122">Teams アプリは、Fluent UI によって提供されるアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="3628d-122">Teams apps use icons provided by Fluent UI.</span></span>

### <a name="resources"></a><span data-ttu-id="3628d-123">リソース</span><span class="sxs-lookup"><span data-stu-id="3628d-123">Resources</span></span>

      * <span data-ttu-id="3628d-124"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">最新の Fluent アイコン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="3628d-124"><a href="https://www.figma.com/community/file/836835755999342788" target="_blank">See the latest Fluent icons (Figma)</a></span></span>
      * <span data-ttu-id="3628d-125"><a href="https://aka.ms/fluent-ui-icons" target="_blank">Fluent アイコンを試す (Fluent UI)</a></span><span class="sxs-lookup"><span data-stu-id="3628d-125"><a href="https://aka.ms/fluent-ui-icons" target="_blank">Try out Fluent icons (Fluent UI)</a></span></span>
      * <span data-ttu-id="3628d-126"><a href="https://github.com/microsoft/fluentui-system-icons" target="_blank">Fluent アイコン ライブラリを取得する (GitHub)</a></span><span class="sxs-lookup"><span data-stu-id="3628d-126"><a href="https://github.com/microsoft/fluentui-system-icons" target="_blank">Get the Fluent icon library (GitHub)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-iconography.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="typography"></a><span data-ttu-id="3628d-128">文字体裁</span><span class="sxs-lookup"><span data-stu-id="3628d-128">Typography</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="3628d-129">Teams では、Segoe UI を使用して、その種類のランプとさまざまなフォント サイズと重みを使用して、階層を作成し、読みやすさを確保します。</span><span class="sxs-lookup"><span data-stu-id="3628d-129">Teams uses Segoe UI for its type ramp and different font sizes and weights to help create hierarchy and ensure readability.</span></span>

      <span data-ttu-id="3628d-130"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なタイポグラフィ ガイドライン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="3628d-130"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full typography guidelines (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-typography.png" alt-text="Microsoft Teams UI キットの概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="copy-and-content"></a><span data-ttu-id="3628d-132">コピーとコンテンツ</span><span class="sxs-lookup"><span data-stu-id="3628d-132">Copy and content</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="3628d-133">Teams の一部を感じるには、アプリ コピー全般で、暖かくリラックスした、鮮明で明確で、手を貸す準備ができているという [Microsoft](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human)音声の原則に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="3628d-133">To feel part of Teams, your app copy in general should follow these [Microsoft voice principles](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human): warm and relaxed, crisp and clear, and ready to lend hand.</span></span>

      <span data-ttu-id="3628d-134"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なコピーとコンテンツのガイドライン (ボット用の書き込みを含む) を参照してください (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="3628d-134"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full copy and content guidelines—including writing for bots (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-copy-and-content.png" alt-text="Microsoft Teams UI キットの概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="brand-expression"></a><span data-ttu-id="3628d-136">ブランド式</span><span class="sxs-lookup"><span data-stu-id="3628d-136">Brand expression</span></span>

:::row:::

   :::column span="3":::

      <span data-ttu-id="3628d-137">アプリアイコンは、Teams ユーザーにブランドを伝えるのに長い道のりを行く可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3628d-137">Your app icon can go a long way in conveying your brand to Teams users.</span></span> <span data-ttu-id="3628d-138">アプリを AppSource に発行する場合も、アイコン [の](../../concepts/build-and-test/apps-package.md) デザインを正しい方法で取得することが重要です。</span><span class="sxs-lookup"><span data-stu-id="3628d-138">Getting your icon design right is also important for [publishing your app](../../concepts/build-and-test/apps-package.md) to AppSource.</span></span>

      <span data-ttu-id="3628d-139"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なブランド表現のガイドライン (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="3628d-139"><a href="https://www.figma.com/community/file/916836509871353159" target="_blank">See full brand expression guidelines (Figma)</a></span></span>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-branding.png" alt-text="Microsoft Teams UI キットの概念フォーム。" border="false":::

   :::column-end:::
:::row-end:::
