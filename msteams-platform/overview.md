---
title: Microsoft Teams 開発者プラットフォーム
author: clearab
description: Microsoft Teams 開発者向けプラットフォーム、および Microsoft Teams 用アプリの作成を開始する方法について説明する概要ページです。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: cb9d91f2de29bac00f4cdcd9672adf9d7d4ee734
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675120"
---
# <a name="what-are-microsoft-teams-apps"></a><span data-ttu-id="100dc-103">Microsoft Teams アプリとは</span><span class="sxs-lookup"><span data-stu-id="100dc-103">What are Microsoft Teams apps?</span></span>

<span data-ttu-id="100dc-104">Microsoft Teams は、Office 365 のコラボレーションワークスペースで、ユーザーが共同作業を行うために使用するアプリやサービスと統合されています。</span><span class="sxs-lookup"><span data-stu-id="100dc-104">Microsoft Teams is a collaboration workspace in Office 365 that integrates with apps and services people use to get work done together.</span></span> <span data-ttu-id="100dc-105">Microsoft Teams 開発者プラットフォームを使用すると、開発者は自分のアプリやサービスを統合して生産性を向上させ、意思決定を迅速に行い、フォーカスを得ることができるようになります (コンテキスト切り替えが減少します)。また、既存のコンテンツを中心にコラボレーションを作成することも可能です。ワークフロー.</span><span class="sxs-lookup"><span data-stu-id="100dc-105">The Microsoft Teams developer platform makes it easy for developers to integrate their own apps and services to improve productivity, make decisions faster, provide focus (by reducing context switching), and create collaboration around existing content and workflows.</span></span> <span data-ttu-id="100dc-106">Microsoft Teams プラットフォーム上に構築されたアプリは、Teams クライアントとサービスおよびワークフロー間の橋渡しをします。コラボレーションプラットフォームのコンテキストに直接組み込む。</span><span class="sxs-lookup"><span data-stu-id="100dc-106">Apps built on the Microsoft Teams platform are bridges between the Teams client and your services and workflows; bringing them directly into the context of your collaboration platform.</span></span>

## <a name="what-can-teams-apps-do"></a><span data-ttu-id="100dc-107">Teams アプリは何を行うことができますか?</span><span class="sxs-lookup"><span data-stu-id="100dc-107">What can Teams apps do?</span></span>

<span data-ttu-id="100dc-108">Microsoft Teams プラットフォームで構築されたアプリは、主にコラボレーションの向上と生産性の向上に重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="100dc-108">Apps built on the Microsoft Teams platform primarily focus on increasing collaboration and improving productivity.</span></span> <span data-ttu-id="100dc-109">アプリは、他のシステムからの通知や複雑な複数ファセットアプリケーションなどの単純なものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="100dc-109">Your app can be something simple, like posting notifications from other systems, or complex multi-faceted applications.</span></span> <span data-ttu-id="100dc-110">Teams は、ソーシャルコラボレーションプラットフォームであることに注意してください。最適なアプリは、ユーザーの個性を深め、共同作業を支援することに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="100dc-110">Just keep in mind that Teams is a social collaboration platform; the best apps focus on helping people express themselves and work better together.</span></span>

* <span data-ttu-id="100dc-111">**外部システムのアイテムに対して共同作業を行います。**</span><span class="sxs-lookup"><span data-stu-id="100dc-111">**Collaborate on items in external systems.**</span></span> <span data-ttu-id="100dc-112">カスタム Teams アプリの中心的なシナリオの1つは、情報またはアイテムを別の場所から Teams に取り込み、それに関する会話を行うことです。</span><span class="sxs-lookup"><span data-stu-id="100dc-112">One of the core scenarios for a custom Teams app is to bring information or items into Teams from some other place, and have a conversation around it.</span></span> <span data-ttu-id="100dc-113">情報を Teams にプッシュし、ユーザーが必要に応じてその情報を検索して取得できるようにしたり、埋め込み web ビューで利用できるようにしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="100dc-113">You can push information into Teams, enable your users to search for and pull it on demand, or make it available in an embedded web view.</span></span>

* <span data-ttu-id="100dc-114">**会話のワークフローをトリガーします。**</span><span class="sxs-lookup"><span data-stu-id="100dc-114">**Trigger workflows from conversations.**</span></span> <span data-ttu-id="100dc-115">多くの場合、一部のワークフローを開始したり、アクションを完了したりする必要が生じることがあります。そのことについてのメモを取り、自分のプルリクエストを確認し、それをセールスリードに変換するなど。Teams アプリは、Teams の内部にそのワークフローへのアクセス権を置くことができます。</span><span class="sxs-lookup"><span data-stu-id="100dc-115">Often conversations result in the need to kick off some workflow or complete some action; take a note about that, review my pull request, convert that to a sales lead, etc. Your Teams app can put access to that workflow right inside of Teams.</span></span>

* <span data-ttu-id="100dc-116">**重要なイベントをチームに通知します。**</span><span class="sxs-lookup"><span data-stu-id="100dc-116">**Notify your team of important events.**</span></span> <span data-ttu-id="100dc-117">電子メール通知の病欠</span><span class="sxs-lookup"><span data-stu-id="100dc-117">Sick of email notifications?</span></span> <span data-ttu-id="100dc-118">代わりにチームに通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="100dc-118">Send notifications to Teams instead!</span></span> <span data-ttu-id="100dc-119">通知をユーザー、チャネル、アクティビティフィード、またはそれらをサブスクライブしているすべてのユーザーに直接送信します。</span><span class="sxs-lookup"><span data-stu-id="100dc-119">Send notifications directly to users, to a channel, to the Activity Feed, or to anyone who subscribes to them.</span></span>

* <span data-ttu-id="100dc-120">**他のサイト/サービスの機能を埋め込む。**</span><span class="sxs-lookup"><span data-stu-id="100dc-120">**Embed functionality from other sites/services.**</span></span> <span data-ttu-id="100dc-121">アプリを見つけやすいものにすることが必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="100dc-121">Sometimes you just need to make your app easier to discover.</span></span> <span data-ttu-id="100dc-122">既存のシングルページアプリを埋め込むか、Teams 用に何かを作成します。</span><span class="sxs-lookup"><span data-stu-id="100dc-122">Embed your existing single-page app, or build something from scratch for Teams.</span></span>

## <a name="how-do-teams-apps-work"></a><span data-ttu-id="100dc-123">Teams アプリはどのように動作しますか?</span><span class="sxs-lookup"><span data-stu-id="100dc-123">How do Teams apps work?</span></span>

<span data-ttu-id="100dc-124">Microsoft Teams のカスタムアプリについて最初に知っておくべきことは、Teams がホスティングサービスではないことです。</span><span class="sxs-lookup"><span data-stu-id="100dc-124">The first thing to know about custom apps for Microsoft Teams (other than how amazing they can be), is that Teams is not a hosting service.</span></span> <span data-ttu-id="100dc-125">アプリパッケージには、アプリについてのメタデータ (名前、アイコンなど)、およびアプリの電源をホストしている web サービスへのポインターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="100dc-125">Your app package contains metadata about your app (name, icons, etc.), and pointers to the web services you host that power your app.</span></span> <span data-ttu-id="100dc-126">Microsoft Teams では、アプリで使用可能な情報や操作を拡張するために使用できる Api、UI/UX 構造、および使用できる Api について説明します。</span><span class="sxs-lookup"><span data-stu-id="100dc-126">Microsoft Teams provides the distribution mechanism, UI/UX constructs for you to take advantage of, and APIs you can use to augment the information and actions available to your app.</span></span>

<span data-ttu-id="100dc-127">Teams アプリは、次の3つの主要な要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="100dc-127">A Teams app consists of three major pieces:</span></span>

* <span data-ttu-id="100dc-128">ユーザーがアプリと対話する**Microsoft Teams クライアント (web、デスクトップ、またはモバイル)** 。</span><span class="sxs-lookup"><span data-stu-id="100dc-128">**The Microsoft Teams client (web, desktop or mobile)** where users will interact with your app.</span></span>
* <span data-ttu-id="100dc-129">ユーザーによってインストールされたアプリを作成する**Teams アプリパッケージ**。また、アプリのメタデータとサービスへのポインターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="100dc-129">**Your Teams app package** that creates the app installed by your users, and contains your app's metadata and pointers to your services.</span></span>
* <span data-ttu-id="100dc-130">アプリをパワーするために必要なロジック、データストレージ、API 呼び出しを実行する**サービス、ワークフロー、または web サイト**。</span><span class="sxs-lookup"><span data-stu-id="100dc-130">**Your service, workflow or website** which perform the necessary logic, data storage and API calls to power your app.</span></span>

<span data-ttu-id="100dc-131">Microsoft Teams アプリで公開する機能は、セキュリティを強化するために追加の手順を実行しない限り、インターネットを介して公開されることに留意することが重要です。</span><span class="sxs-lookup"><span data-stu-id="100dc-131">It is important to keep in mind that any functionality you expose in a Microsoft Teams app is publicly available over the internet unless you take additional steps to secure it.</span></span> <span data-ttu-id="100dc-132">機密情報または保護された情報へのアクセスを提供する場合は、アプリに接続しているエンドポイントを最低限認証するか、または[ユーザーを認証](~/concepts/authentication/authentication.md)するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="100dc-132">If you are providing access to confidential or protected information you'll want make sure your services are at a minimum authenticating the endpoint connecting to your app, or [authenticating your users](~/concepts/authentication/authentication.md).</span></span>

## <a name="how-can-you-share-your-teams-app"></a><span data-ttu-id="100dc-133">Teams アプリはどのように共有できますか?</span><span class="sxs-lookup"><span data-stu-id="100dc-133">How can you share your Teams app?</span></span>

<span data-ttu-id="100dc-134">Microsoft Teams アプリを共有する準備ができている場合は、対象ユーザーに応じて3つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="100dc-134">When you're ready to share your Microsoft Teams apps, you have three options depending on who your target audience is.</span></span>

* <span data-ttu-id="100dc-135">**[アプリを直接アップロードする](~/concepts/deploy-and-publish/apps-upload.md)** アプリをチームまたは組織内の少数の個人にのみ共有する必要がある場合は、アプリパッケージを共有し、それを直接アップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="100dc-135">**[Upload your app directly](~/concepts/deploy-and-publish/apps-upload.md)** If your app only needs to be shared to your team, or a few individuals in your organization, you can share your app package and upload it directly.</span></span>
* <span data-ttu-id="100dc-136">**[組織のアプリカタログに発行する](~/concepts/deploy-and-publish/apps-publish.md)** アプリカタログを使用して、アプリを組織全体で共有できます。</span><span class="sxs-lookup"><span data-stu-id="100dc-136">**[Publish to your organizational app catalog](~/concepts/deploy-and-publish/apps-publish.md)** You can share your app with your entire organization through your app catalog.</span></span>
* <span data-ttu-id="100dc-137">**[公開アプリストアに発行する](~/concepts/deploy-and-publish/apps-publish.md)** アプリがすべてのユーザーに対して公開されている場合は、パブリックアプリストアに発行できます。</span><span class="sxs-lookup"><span data-stu-id="100dc-137">**[Publish to the public app store](~/concepts/deploy-and-publish/apps-publish.md)** If your app is for everyone, you can publish it to our public app store.</span></span> <span data-ttu-id="100dc-138">目標に応じて、マーケティングおよびセールス支援を受けることができます。</span><span class="sxs-lookup"><span data-stu-id="100dc-138">Depending on your goals, you might be eligible for marketing and sales assistance.</span></span>

## <a name="get-started"></a><span data-ttu-id="100dc-139">作業の開始</span><span class="sxs-lookup"><span data-stu-id="100dc-139">Get started</span></span>

* [<span data-ttu-id="100dc-140">C でボットおよび tab アプリをビルドする#</span><span class="sxs-lookup"><span data-stu-id="100dc-140">Build a bot and tab app in C#</span></span>](~/tutorials/get-started-dotnet-app-studio.md)
* [<span data-ttu-id="100dc-141">JavaScript/node.js でボットおよび tab アプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="100dc-141">Build a bot and tab app in JavaScript/Node.js</span></span>](~/tutorials/get-started-nodejs-app-studio.md)

## <a name="learn-more"></a><span data-ttu-id="100dc-142">詳細情報</span><span class="sxs-lookup"><span data-stu-id="100dc-142">Learn more</span></span>

* [<span data-ttu-id="100dc-143">Teams クライアントの拡張ポイント</span><span class="sxs-lookup"><span data-stu-id="100dc-143">Extensibility points in the Teams client</span></span>](~/concepts/extensibility-points.md)
* [<span data-ttu-id="100dc-144">Teams 用アプリの作成</span><span class="sxs-lookup"><span data-stu-id="100dc-144">Building apps for Teams</span></span>](~/concepts/building-an-app.md)