---
title: 設計ガイドラインのリファレンス
description: 個人用アプリの設計ガイドラインについて説明します。
keywords: teams の設計ガイドラインリファレンスフレームワーク個人用アプリ
ms.openlocfilehash: 0d886adf926697f8920c0893589201ea4e4c3a9c
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228074"
---
# <a name="personal-apps"></a><span data-ttu-id="acd74-104">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="acd74-104">Personal apps</span></span>

> [!Important]
> <span data-ttu-id="acd74-105">モバイルクライアントでのタブの完全なサポートは、近日中に予定されています。</span><span class="sxs-lookup"><span data-stu-id="acd74-105">Full support for tabs on mobile clients is coming soon.</span></span> <span data-ttu-id="acd74-106">この変更を準備するには、タブを作成するときに[[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="acd74-106">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="acd74-107">個人用アプリ (静的タブ) は現在、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。</span><span class="sxs-lookup"><span data-stu-id="acd74-107">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="acd74-108">タブの完全なサポートがリリースされると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="acd74-108">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="acd74-109">すべてのタブがモバイルで常に使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="acd74-109">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="acd74-110">`contentUrl` **は、モバイル Teams クライアントにロードされ**ます。</span><span class="sxs-lookup"><span data-stu-id="acd74-110">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="acd74-111">[チャネル/グループ] タブでは、ユーザーは自分`websiteUrl`のを経由して別のブラウザーで`contentUrl`タブを開くことができます。ただし、は最初に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="acd74-111">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>

<span data-ttu-id="acd74-112">個人用アプリは、個人のスコープを持つアプリです。</span><span class="sxs-lookup"><span data-stu-id="acd74-112">A personal app is an app with a personal scope.</span></span> <span data-ttu-id="acd74-113">アプリ開発者は、個々のユーザー向けにビルドされたバージョンのアプリを提供するオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="acd74-113">As an app developer, you have the option to provide a version of your app that is built for the individual user.</span></span> <span data-ttu-id="acd74-114">このバージョンでは、タブのコレクション (および bot が含まれている場合は bot) は、その人物向けに設計されています。</span><span class="sxs-lookup"><span data-stu-id="acd74-114">In this version, the collection of tabs (and the bot, if you've included one), are designed for the person.</span></span> <span data-ttu-id="acd74-115">これにより、ユーザーとの1対1の操作を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="acd74-115">This way, you're able to create a one-on-one interaction with your users.</span></span>

<span data-ttu-id="acd74-116">個人用アプリは、誰かが表示されているすべてのアイテム、およびアプリで最近表示したすべてのアイテムを表示できます。</span><span class="sxs-lookup"><span data-stu-id="acd74-116">A personal app is where someone can see everything that's theirs, and all the items they've recently viewed in the app.</span></span> <span data-ttu-id="acd74-117">すべてが1つの場所に配置されます。</span><span class="sxs-lookup"><span data-stu-id="acd74-117">It puts everything in one place.</span></span> <span data-ttu-id="acd74-118">次のスクリーンショットでは、Contoso は個人用アプリのポップアップにある個人用アプリです。</span><span class="sxs-lookup"><span data-stu-id="acd74-118">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![アプリのオーバーフローメニューのイメージ](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="acd74-120">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="acd74-120">Guidelines</span></span>

<span data-ttu-id="acd74-121">個人用アプリには通常、次のタブが含まれています。</span><span class="sxs-lookup"><span data-stu-id="acd74-121">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="acd74-122">タブ</span><span class="sxs-lookup"><span data-stu-id="acd74-122">Your tab</span></span>

<span data-ttu-id="acd74-123">これで、ユーザーにすべてのアイテムが表示されます。</span><span class="sxs-lookup"><span data-stu-id="acd74-123">This is where your users will see all their stuff.</span></span> <span data-ttu-id="acd74-124">個人のスペースです。</span><span class="sxs-lookup"><span data-stu-id="acd74-124">It's their personal space.</span></span> <span data-ttu-id="acd74-125">このタブは、リスト、グリッド、列、または1つのキャンバスとして配置できます。アプリケーションにとって最適なものは何か。</span><span class="sxs-lookup"><span data-stu-id="acd74-125">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="acd74-126">有効なタブの設計の詳細については、「 [tabs design](../../tabs/design/tabs.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="acd74-126">For additional information on designing effective tabs see: [Tabs design](../../tabs/design/tabs.md).</span></span>

<span data-ttu-id="acd74-127">このタブには複数のチャネルのアイテムが表示されることがあるので、各アイテムには自分のチーム、チャネル、およびタブが表示され、ユーザーは自分の元の場所を簡単に確認できます。</span><span class="sxs-lookup"><span data-stu-id="acd74-127">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![[個人用タスク] タブ](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="acd74-129">最新</span><span class="sxs-lookup"><span data-stu-id="acd74-129">Recent</span></span>

<span data-ttu-id="acd74-130">[**最近使っ**た項目] タブを使用すると、アプリで最近表示したすべての情報を他のユーザーが参照できます。</span><span class="sxs-lookup"><span data-stu-id="acd74-130">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="acd74-131">これは、時系列 (最も新しいものから最も古いものまで) に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="acd74-131">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="acd74-132">このリスト内のアイテムをクリックすると、そのアイテムのチャネルとタブに移動します。</span><span class="sxs-lookup"><span data-stu-id="acd74-132">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![[最近使用したタブ]](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="acd74-134">すべて</span><span class="sxs-lookup"><span data-stu-id="acd74-134">All</span></span>

<span data-ttu-id="acd74-135">これは、ユーザーの組織内のすべてのタブ (アクセスできるもの) の一覧です。</span><span class="sxs-lookup"><span data-stu-id="acd74-135">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="acd74-136">つまり、アプリが使用されているすべての場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="acd74-136">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="acd74-137">[**最近使っ**た項目] タブと同様に、リスト内で何かを選択すると、ユーザーは関連するチャネルとタブに直接移動します。</span><span class="sxs-lookup"><span data-stu-id="acd74-137">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="acd74-138">Bot</span><span class="sxs-lookup"><span data-stu-id="acd74-138">Bot</span></span>

<span data-ttu-id="acd74-139">Bot は必須ではありませんが、ユーザーと直接やり取りするための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="acd74-139">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="acd74-140">通知は個人アプリの最も重要な機能の1つで、直接的なコミュニケーションと比べてより良い通知方法ですか。</span><span class="sxs-lookup"><span data-stu-id="acd74-140">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="acd74-141">Bot は、メッセージをカード形式で配信します。これにより、特定の情報 (新しいコンテンツが利用可能であることを示す通知など) や広範な更新 (毎日のタスクリストなど) を提供できます。</span><span class="sxs-lookup"><span data-stu-id="acd74-141">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="acd74-142">効果的なボットを設計する詳細については、「 [bot 設計](../../bots/design/bots.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="acd74-142">For additional information on designing effective bots see: [Bot design](../../bots/design/bots.md).</span></span>

![Bot 案内応答](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="acd74-144">ヘルプと設定</span><span class="sxs-lookup"><span data-stu-id="acd74-144">Help and Settings</span></span>

<span data-ttu-id="acd74-145">ヘルプコンテンツは、ユーザーがアプリの微妙な違いを見つけられるようにします。</span><span class="sxs-lookup"><span data-stu-id="acd74-145">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="acd74-146">[**設定**] タブを追加して、さらにカスタマイズできるようにします。</span><span class="sxs-lookup"><span data-stu-id="acd74-146">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="acd74-147">概要</span><span class="sxs-lookup"><span data-stu-id="acd74-147">About</span></span>

<span data-ttu-id="acd74-148">バージョン番号、機能、プライバシー、アクセス許可のリンクなどの情報を提供するための [**概要**] タブを含めます。</span><span class="sxs-lookup"><span data-stu-id="acd74-148">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="acd74-149">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="acd74-149">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="acd74-150">ユーザーと直接通信する</span><span class="sxs-lookup"><span data-stu-id="acd74-150">Communicate directly with your users</span></span>

<span data-ttu-id="acd74-151">Bot を使用して、ユーザーに変更と新機能があることを通知します。</span><span class="sxs-lookup"><span data-stu-id="acd74-151">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="acd74-152">タブをカスタマイズする...</span><span class="sxs-lookup"><span data-stu-id="acd74-152">Customize your tabs...</span></span>

<span data-ttu-id="acd74-153">ユーザーが特定のタスクを実行するのに役立つその他のタブを自由に追加できます。</span><span class="sxs-lookup"><span data-stu-id="acd74-153">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="acd74-154">...すべてのユーザーに関連するようにします。</span><span class="sxs-lookup"><span data-stu-id="acd74-154">...and make them relevant to every user</span></span>

<span data-ttu-id="acd74-155">アプリマニフェストで宣言したすべてのタブは、すべてのユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="acd74-155">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="acd74-156">たとえば、個人アプリが、マネージャーと従業員の両方で使用される経費報告ツールである場合、[**承認**] タブで、両方の役割にとって意味のあるコンテンツを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="acd74-156">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
