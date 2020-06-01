---
title: 設計ガイドラインのリファレンス
description: 個人用アプリの設計ガイドラインについて説明します。
keywords: teams の設計ガイドラインリファレンスフレームワーク個人用アプリ
ms.openlocfilehash: f66691234149afa56a6753dd51379c9f2355318e
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455500"
---
# <a name="personal-apps"></a><span data-ttu-id="23a8b-104">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="23a8b-104">Personal apps</span></span>

> [!NOTE]
> <span data-ttu-id="23a8b-105">Teams では、モバイルクライアントでのタブの完全なサポートがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="23a8b-105">Full support for tabs on mobile clients is supported in Teams.</span></span> <span data-ttu-id="23a8b-106">モバイルプラットフォームのタブを作成するときは、「 [mobile のタブのガイダンス](../../tabs/design/tabs-mobile.md)」に従ってください。</span><span class="sxs-lookup"><span data-stu-id="23a8b-106">You should follow the [guidance for tabs on mobile](../../tabs/design/tabs-mobile.md) when creating tabs for mobile platforms.</span></span>

<span data-ttu-id="23a8b-107">個人用アプリは、個人のスコープを持つ Teams アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="23a8b-107">A personal app is a Teams application with a personal scope.</span></span>  <span data-ttu-id="23a8b-108">アプリ開発者は、1人のユーザーとの対話に焦点を当てたバージョンのアプリを提供するオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-108">As an app developer, you have the option to provide a version of your app that focuses on interactions with a single user.</span></span> <span data-ttu-id="23a8b-109">[対話](../../bots/what-are-bots.md)式を使用して、ユーザーまたは[個人用タブ](../../tabs/what-are-tabs.md)で1対1の会話を行い、組み込みの web 環境を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-109">It can be a [conversational bot](../../bots/what-are-bots.md) to engage in one-to-one conversations with a user or a [personal tab](../../tabs/what-are-tabs.md) providing an embedded web experience.</span></span> <span data-ttu-id="23a8b-110">個人用アプリを使用すると、ユーザーが選択したコンテンツを1つの場所に表示できます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-110">Personal apps enable users to view their select content in one place.</span></span> <span data-ttu-id="23a8b-111">次のスクリーンショットでは、Contoso は個人用アプリのポップアップにある個人用アプリです。</span><span class="sxs-lookup"><span data-stu-id="23a8b-111">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![アプリのオーバーフローメニューのイメージ](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="23a8b-113">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="23a8b-113">Guidelines</span></span>

<span data-ttu-id="23a8b-114">個人用アプリには通常、次のタブが含まれています。</span><span class="sxs-lookup"><span data-stu-id="23a8b-114">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="23a8b-115">タブ</span><span class="sxs-lookup"><span data-stu-id="23a8b-115">Your tab</span></span>

<span data-ttu-id="23a8b-116">これで、ユーザーにすべてのアイテムが表示されます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-116">This is where your users will see all their stuff.</span></span> <span data-ttu-id="23a8b-117">個人のスペースです。</span><span class="sxs-lookup"><span data-stu-id="23a8b-117">It's their personal space.</span></span> <span data-ttu-id="23a8b-118">このタブは、リスト、グリッド、列、または1つのキャンバスとして配置できます。アプリケーションにとって最適なものは何か。</span><span class="sxs-lookup"><span data-stu-id="23a8b-118">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="23a8b-119">有効なタブの設計の詳細については、「 [tabs design](../../tabs/design/tabs.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="23a8b-119">For additional information on designing effective tabs see: [Tabs design](../../tabs/design/tabs.md).</span></span>

<span data-ttu-id="23a8b-120">このタブには複数のチャネルのアイテムが表示されることがあるので、各アイテムには自分のチーム、チャネル、およびタブが表示され、ユーザーは自分の元の場所を簡単に確認できます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-120">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![[個人用タスク] タブ](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="23a8b-122">最新</span><span class="sxs-lookup"><span data-stu-id="23a8b-122">Recent</span></span>

<span data-ttu-id="23a8b-123">[**最近使っ**た項目] タブを使用すると、アプリで最近表示したすべての情報を他のユーザーが参照できます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-123">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="23a8b-124">これは、時系列 (最も新しいものから最も古いものまで) に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-124">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="23a8b-125">このリスト内のアイテムをクリックすると、そのアイテムのチャネルとタブに移動します。</span><span class="sxs-lookup"><span data-stu-id="23a8b-125">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![[最近使用したタブ]](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="23a8b-127">すべて</span><span class="sxs-lookup"><span data-stu-id="23a8b-127">All</span></span>

<span data-ttu-id="23a8b-128">これは、ユーザーの組織内のすべてのタブ (アクセスできるもの) の一覧です。</span><span class="sxs-lookup"><span data-stu-id="23a8b-128">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="23a8b-129">つまり、アプリが使用されているすべての場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="23a8b-129">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="23a8b-130">[**最近使っ**た項目] タブと同様に、リスト内で何かを選択すると、ユーザーは関連するチャネルとタブに直接移動します。</span><span class="sxs-lookup"><span data-stu-id="23a8b-130">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="23a8b-131">Bot</span><span class="sxs-lookup"><span data-stu-id="23a8b-131">Bot</span></span>

<span data-ttu-id="23a8b-132">Bot は必須ではありませんが、ユーザーと直接やり取りするための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="23a8b-132">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="23a8b-133">通知は個人アプリの最も重要な機能の1つで、直接的なコミュニケーションと比べてより良い通知方法ですか。</span><span class="sxs-lookup"><span data-stu-id="23a8b-133">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="23a8b-134">Bot は、メッセージをカード形式で配信します。これにより、特定の情報 (新しいコンテンツが利用可能であることを示す通知など) や広範な更新 (毎日のタスクリストなど) を提供できます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-134">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="23a8b-135">効果的なボットを設計する詳細については、「 [bot 設計](../../bots/design/bots.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="23a8b-135">For additional information on designing effective bots see: [Bot design](../../bots/design/bots.md).</span></span>

![Bot 案内応答](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="23a8b-137">ヘルプと設定</span><span class="sxs-lookup"><span data-stu-id="23a8b-137">Help and Settings</span></span>

<span data-ttu-id="23a8b-138">ヘルプコンテンツは、ユーザーがアプリの微妙な違いを見つけられるようにします。</span><span class="sxs-lookup"><span data-stu-id="23a8b-138">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="23a8b-139">[**設定**] タブを追加して、さらにカスタマイズできるようにします。</span><span class="sxs-lookup"><span data-stu-id="23a8b-139">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="23a8b-140">概要</span><span class="sxs-lookup"><span data-stu-id="23a8b-140">About</span></span>

<span data-ttu-id="23a8b-141">バージョン番号、機能、プライバシー、アクセス許可のリンクなどの情報を提供するための [**概要**] タブを含めます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-141">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="23a8b-142">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="23a8b-142">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="23a8b-143">ユーザーと直接通信する</span><span class="sxs-lookup"><span data-stu-id="23a8b-143">Communicate directly with your users</span></span>

<span data-ttu-id="23a8b-144">Bot を使用して、ユーザーに変更と新機能があることを通知します。</span><span class="sxs-lookup"><span data-stu-id="23a8b-144">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="23a8b-145">タブをカスタマイズする...</span><span class="sxs-lookup"><span data-stu-id="23a8b-145">Customize your tabs...</span></span>

<span data-ttu-id="23a8b-146">ユーザーが特定のタスクを実行するのに役立つその他のタブを自由に追加できます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-146">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="23a8b-147">...すべてのユーザーに関連するようにします。</span><span class="sxs-lookup"><span data-stu-id="23a8b-147">...and make them relevant to every user</span></span>

<span data-ttu-id="23a8b-148">アプリマニフェストで宣言したすべてのタブは、すべてのユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="23a8b-148">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="23a8b-149">たとえば、個人アプリが、マネージャーと従業員の両方で使用される経費報告ツールである場合、[**承認**] タブで、両方の役割にとって意味のあるコンテンツを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="23a8b-149">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
