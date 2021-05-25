---
title: アクティビティ フィード通知の設計
author: heath-hamilton
description: アプリのアクティビティ フィード通知を設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 61a2a6da2a5ed0cb3126b9798094b06c575c9b6c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631359"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a><span data-ttu-id="49587-103">アプリのアクティビティ フィード通知をMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="49587-103">Designing activity feed notifications for your Microsoft Teams app</span></span>

<span data-ttu-id="49587-104">アクティビティ フィードは、ユーザーが自分の通知にアクセスする画面Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="49587-104">The activity feed is a surface for users to access their notifications in Microsoft Teams.</span></span> <span data-ttu-id="49587-105">フィードは過去 4 週間の通知を保持します。</span><span class="sxs-lookup"><span data-stu-id="49587-105">The feed retains notifications from the past four weeks.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="49587-106">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="49587-106">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="例では、アクティビティ フィードに表示されるアプリ通知Teams示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="49587-108">モバイル</span><span class="sxs-lookup"><span data-stu-id="49587-108">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="例は、モバイルのアクティビティ フィードのTeamsアプリ通知を示しています。" border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="49587-110">構造</span><span class="sxs-lookup"><span data-stu-id="49587-110">Anatomy</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="アクティビティ フィード通知のTeams構造を設計します。" border="false":::

|<span data-ttu-id="49587-112">カウンター</span><span class="sxs-lookup"><span data-stu-id="49587-112">Counter</span></span>|<span data-ttu-id="49587-113">説明</span><span class="sxs-lookup"><span data-stu-id="49587-113">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="49587-114">1</span><span class="sxs-lookup"><span data-stu-id="49587-114">1</span></span>|<span data-ttu-id="49587-115">**アバター**: アクティビティを開始したユーザーを示します。</span><span class="sxs-lookup"><span data-stu-id="49587-115">**Avatar**: Shows who initiated the activity.</span></span>|
|<span data-ttu-id="49587-116">2</span><span class="sxs-lookup"><span data-stu-id="49587-116">2</span></span>|<span data-ttu-id="49587-117">**[アクティビティの種類/アプリ] アイコン**: アクティビティの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="49587-117">**Activity type/app icon**: Depicts the type of activity.</span></span> <span data-ttu-id="49587-118">アプリ通知の場合、行アイコンはアプリ アイコンに置き換わります。</span><span class="sxs-lookup"><span data-stu-id="49587-118">For app notifications, the line icon is replaced with an app icon.</span></span>|
|<span data-ttu-id="49587-119">3</span><span class="sxs-lookup"><span data-stu-id="49587-119">3</span></span>|<span data-ttu-id="49587-120">**タイトル (最初の行): Actor + Reason**: *Actor*: アクティビティを開始したユーザーまたはアプリの名前。</span><span class="sxs-lookup"><span data-stu-id="49587-120">**Title (first line): Actor + reason**: *Actor*: Name of the user or app that initiated the activity.</span></span> <span data-ttu-id="49587-121">*理由*: アクティビティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="49587-121">*Reason*: Describes the activity.</span></span>|
|<span data-ttu-id="49587-122">4</span><span class="sxs-lookup"><span data-stu-id="49587-122">4</span></span>|<span data-ttu-id="49587-123">**タイムスタンプ**: アクティビティが発生した日時を示します。</span><span class="sxs-lookup"><span data-stu-id="49587-123">**Timestamp**: Shows when the activity happened.</span></span>|
|<span data-ttu-id="49587-124">5</span><span class="sxs-lookup"><span data-stu-id="49587-124">5</span></span>|<span data-ttu-id="49587-125">**場所 (2 行目)**: アクティビティが 2 行目で発生した場所Teams。</span><span class="sxs-lookup"><span data-stu-id="49587-125">**Location (second line)**: Shows where the activity happened in Teams.</span></span>|
|<span data-ttu-id="49587-126">6</span><span class="sxs-lookup"><span data-stu-id="49587-126">6</span></span>|<span data-ttu-id="49587-127">**第 3 の情報 (3 行目)**: オプション。</span><span class="sxs-lookup"><span data-stu-id="49587-127">**Tertiary information (third line)**: Optional.</span></span> <span data-ttu-id="49587-128">プレビュー テキストまたは追加情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="49587-128">Shows preview text or additional information.</span></span>|

## <a name="types-of-activity-feed-notification-cards"></a><span data-ttu-id="49587-129">アクティビティ フィード通知カードの種類</span><span class="sxs-lookup"><span data-stu-id="49587-129">Types of activity feed notification cards</span></span>

<span data-ttu-id="49587-130">次のバリアントは、表示できるアクティビティ フィード通知カードの種類を示しています。</span><span class="sxs-lookup"><span data-stu-id="49587-130">The following variants show the kinds of activity feed notification cards you can display.</span></span> <span data-ttu-id="49587-131">アプリロゴは、アプリで生成された通知のユーザー アバターを置き換える。</span><span class="sxs-lookup"><span data-stu-id="49587-131">The app logo replaces the user avatar for app-generated notifications.</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="アクティビティ フィード Teamsのバリアント。" border="false":::

## <a name="manage-activity-feed-notifications"></a><span data-ttu-id="49587-133">アクティビティ フィード通知の管理</span><span class="sxs-lookup"><span data-stu-id="49587-133">Manage activity feed notifications</span></span>

<span data-ttu-id="49587-134">ユーザーは、[アプリの設定] ページでアプリから送信Teams管理できます。</span><span class="sxs-lookup"><span data-stu-id="49587-134">Users can manage notifications sent from your app in the Teams settings page.</span></span>

## <a name="related-system-notifications"></a><span data-ttu-id="49587-135">関連するシステム通知</span><span class="sxs-lookup"><span data-stu-id="49587-135">Related system notifications</span></span>

<span data-ttu-id="49587-136">各アクティビティは、システム通知を生成します。</span><span class="sxs-lookup"><span data-stu-id="49587-136">Each activity generates a system notification.</span></span> <span data-ttu-id="49587-137">表示される内容は、ユーザーが通知設定で構成する内容によって異なります。</span><span class="sxs-lookup"><span data-stu-id="49587-137">What displays depends on what the user configures in their notification settings.</span></span> <span data-ttu-id="49587-138">ユーザーは、オペレーティング システムに基づいて通知スタイルを選択できます。</span><span class="sxs-lookup"><span data-stu-id="49587-138">Users can also choose a notification style based on their operating system.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="49587-139">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="49587-139">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="さまざまなオペレーティング システムTeamsアクティビティ カードのバリアント。" border="false":::

|<span data-ttu-id="49587-141">カウンター</span><span class="sxs-lookup"><span data-stu-id="49587-141">Counter</span></span>|<span data-ttu-id="49587-142">説明</span><span class="sxs-lookup"><span data-stu-id="49587-142">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="49587-143">1</span><span class="sxs-lookup"><span data-stu-id="49587-143">1</span></span>|<span data-ttu-id="49587-144">Teamsカスタム</span><span class="sxs-lookup"><span data-stu-id="49587-144">Teams custom</span></span>|
|<span data-ttu-id="49587-145">2</span><span class="sxs-lookup"><span data-stu-id="49587-145">2</span></span>|<span data-ttu-id="49587-146">Windows</span><span class="sxs-lookup"><span data-stu-id="49587-146">Windows</span></span>|
|<span data-ttu-id="49587-147">3</span><span class="sxs-lookup"><span data-stu-id="49587-147">3</span></span>|<span data-ttu-id="49587-148">Mac</span><span class="sxs-lookup"><span data-stu-id="49587-148">Mac</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="49587-149">モバイル</span><span class="sxs-lookup"><span data-stu-id="49587-149">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Android および iOS Teamsアクティビティ フィード カードのバリアント。" border="false":::

|<span data-ttu-id="49587-151">カウンター</span><span class="sxs-lookup"><span data-stu-id="49587-151">Counter</span></span>|<span data-ttu-id="49587-152">説明</span><span class="sxs-lookup"><span data-stu-id="49587-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="49587-153">1</span><span class="sxs-lookup"><span data-stu-id="49587-153">1</span></span>|<span data-ttu-id="49587-154">Android</span><span class="sxs-lookup"><span data-stu-id="49587-154">Android</span></span>|
|<span data-ttu-id="49587-155">2</span><span class="sxs-lookup"><span data-stu-id="49587-155">2</span></span>|<span data-ttu-id="49587-156">iOS</span><span class="sxs-lookup"><span data-stu-id="49587-156">iOS</span></span>|

---

## <a name="next-step"></a><span data-ttu-id="49587-157">次の手順</span><span class="sxs-lookup"><span data-stu-id="49587-157">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49587-158">アクティビティ フィード通知の実装</span><span class="sxs-lookup"><span data-stu-id="49587-158">Implement activity feed notifications</span></span>](/graph/teams-send-activityfeednotifications)
