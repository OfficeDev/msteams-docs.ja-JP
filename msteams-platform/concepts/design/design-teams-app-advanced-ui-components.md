---
title: 高度な UI コンポーネントを使用してアプリを設計する
author: heath-hamilton
description: 各コンポーネントで使用される UI コンポーネントTeams。
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 6f2bd9cd237751adb15db45bbd6e3cdfea35ce09
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328080"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a><span data-ttu-id="0a7ac-103">高度な UI Microsoft Teamsを使用したアプリの設計</span><span class="sxs-lookup"><span data-stu-id="0a7ac-103">Designing your Microsoft Teams app with advanced UI components</span></span>

<span data-ttu-id="0a7ac-104">次のコンポーネントは、ナビゲーションなどの一[](~/concepts/design/design-teams-app-basic-ui-components.md)般的な設計状況で使用Teams UI コンポーネントの組み合わせです。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-104">The following components are a combination of [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md) that you can use for common Teams design situations, such as navigation.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0a7ac-105">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="0a7ac-105">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0a7ac-106">UI に<a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>キットには、Microsoft Teamsアプリを構築するために特別に設計されたコンポーネントとTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-106">Based on <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>, the Microsoft Teams UI Kit includes components and patterns that are designed specifically for building Teams apps.</span></span> <span data-ttu-id="0a7ac-107">UI キットでは、ここに示すコンポーネントを直接デザインに挿入し、各コンポーネントの使い方の例を確認できます。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-107">In the UI kit, you can grab and insert the components listed here directly into your design and see more examples of how to use each component.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a7ac-108">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="0a7ac-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a><span data-ttu-id="0a7ac-109">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="0a7ac-109">Breadcrumb</span></span>

<span data-ttu-id="0a7ac-110">Breadcrumbs は、アプリの階層を伝えるナビゲーション支援です。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-110">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="0a7ac-111">ユーザーは、表示しているページが全体的なエクスペリエンスに適合する方法を理解し、その階層内の上位レベルへの 1 回のクリックアクセスを許可するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-111">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0a7ac-112">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="0a7ac-112">Top use cases</span></span>

* <span data-ttu-id="0a7ac-113">コミュニケーション階層</span><span class="sxs-lookup"><span data-stu-id="0a7ac-113">Communicate hierarchy</span></span>
* <span data-ttu-id="0a7ac-114">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="0a7ac-114">Navigation</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0a7ac-115">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-115">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、デスクトップ上のパンくずテンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0a7ac-117">モバイル</span><span class="sxs-lookup"><span data-stu-id="0a7ac-117">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="例は、モバイル上のパンくずテンプレートを示しています。" border="false":::

---

## <a name="left-nav"></a><span data-ttu-id="0a7ac-119">左ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="0a7ac-119">Left nav</span></span>

<span data-ttu-id="0a7ac-120">左側のナビゲーションを使用して、[ページ] タブ内の複数Teamsします。次の例では、左側のナビゲーションはチャネル リストとタブ コンテンツの間にあります。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-120">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0a7ac-121">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="0a7ac-121">Top use cases</span></span>

* <span data-ttu-id="0a7ac-122">[ページ] タブ内の複数Teams参照します。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-122">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="0a7ac-123">複雑なアプリを複数のページに分割します。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-123">Break down complex apps into multiple pages.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0a7ac-124">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、デスクトップ上の左側のナビゲーション テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0a7ac-126">モバイル</span><span class="sxs-lookup"><span data-stu-id="0a7ac-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="例は、モバイル上の左ナビゲーション テンプレートを示しています。" border="false":::

---

## <a name="notification-bar"></a><span data-ttu-id="0a7ac-128">通知バー</span><span class="sxs-lookup"><span data-stu-id="0a7ac-128">Notification bar</span></span>

<span data-ttu-id="0a7ac-129">通知バーは、ユーザーが即座にアクションを実行する必要が生じない、簡潔で重要なメッセージを表示するための専用の領域です。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-129">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="0a7ac-130">特定の背景色とアイコンは、特定の種類のメッセージに関連付けられる (以下を参照)。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-130">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0a7ac-131">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="0a7ac-131">Top use cases</span></span>

* <span data-ttu-id="0a7ac-132">重大なメッセージ、エラー、および警告</span><span class="sxs-lookup"><span data-stu-id="0a7ac-132">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="0a7ac-133">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-133">Success messages</span></span>
* <span data-ttu-id="0a7ac-134">情報メッセージまたはプロモーション メッセージ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-134">Informational or promotional messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0a7ac-135">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、デスクトップ上の通知バーの UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0a7ac-137">モバイル</span><span class="sxs-lookup"><span data-stu-id="0a7ac-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="例では、モバイルの通知バー UI テンプレートを表示します。" border="false":::

---

## <a name="stage"></a><span data-ttu-id="0a7ac-139">ステージ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-139">Stage</span></span>

<span data-ttu-id="0a7ac-140">ステージを使用すると、ユーザーはコンテキストを切り替えることなく、画像、ファイル、web サイトなど、コンテンツを大規模なTeams表示できます。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-140">Stage lets users view content—like an image, file, or website—on a large surface in Teams without switching context.</span></span> <span data-ttu-id="0a7ac-141">ステージは、主にコンテンツを表示する目的です。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-141">Stage is primarily for viewing content.</span></span> <span data-ttu-id="0a7ac-142">複雑な対話にはステージを使用しない。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-142">Don’t use stage for complex interactions.</span></span>

<span data-ttu-id="0a7ac-143">ステージを実装する方法について [学習します](~/tabs/tabs-link-unfurling.md)。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-143">Learn how to implement [stage](~/tabs/tabs-link-unfurling.md).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0a7ac-144">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="0a7ac-144">Top use cases</span></span>

* <span data-ttu-id="0a7ac-145">別のアプリまたはブラウザーではなく、Teams内の大きなサーフェスにコンテンツを表示する</span><span class="sxs-lookup"><span data-stu-id="0a7ac-145">Display content in a large surface within Teams instead of another app or browser</span></span>
* <span data-ttu-id="0a7ac-146">スポットライト メディアまたは他のリッチ コンテンツ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-146">Spotlight media or other rich content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0a7ac-147">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-147">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="例は、デスクトップ上のステージ テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0a7ac-149">モバイル</span><span class="sxs-lookup"><span data-stu-id="0a7ac-149">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="0a7ac-150">アプリは、アダプティブ カード、共有リンク、またはビジュアル コンポーネント (グラフなど) からステージを起動できます。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-150">Your app can launch a stage from an Adaptive Card, shared link, or visual components (such as a chart).</span></span>

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="例は、モバイル上のステージ テンプレートを示しています。" border="false":::

---

## <a name="toolbar"></a><span data-ttu-id="0a7ac-152">ツール バー</span><span class="sxs-lookup"><span data-stu-id="0a7ac-152">Toolbar</span></span>

<span data-ttu-id="0a7ac-153">ツールバーは、コントロールのセットをグループ化するコンテナーです。</span><span class="sxs-lookup"><span data-stu-id="0a7ac-153">A toolbar is a container for grouping a set of controls.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="0a7ac-154">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="0a7ac-154">Top use cases</span></span>

* <span data-ttu-id="0a7ac-155">アプリ コンテンツに関するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="0a7ac-155">Contextual actions on app content</span></span>
* <span data-ttu-id="0a7ac-156">コンテキスト フィルターと検索</span><span class="sxs-lookup"><span data-stu-id="0a7ac-156">Contextual filter and find</span></span>
* <span data-ttu-id="0a7ac-157">ナビゲーションとパンくず</span><span class="sxs-lookup"><span data-stu-id="0a7ac-157">Navigation and breadcrumbs</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0a7ac-158">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="0a7ac-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="例は、デスクトップ上のツール バー テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0a7ac-160">モバイル</span><span class="sxs-lookup"><span data-stu-id="0a7ac-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="例は、モバイルのツール バー テンプレートを示しています。" border="false":::

---
