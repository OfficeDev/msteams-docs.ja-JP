---
title: Teams 開発者プラットフォーム
author: clearab
description: 開発者が Teams プラットフォームを使用して Microsoft Teams の機能を拡張およびカスタマイズする方法の概要について説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d127acb33212f23dff9cf0dd83a1936044c10d5e
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652058"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="2bee6-103">Microsoft Teams の構築</span><span class="sxs-lookup"><span data-stu-id="2bee6-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="2bee6-104">Microsoft Teams アプリは、ユーザーが収集、学習、作業を徐々に行うことができるように、重要な情報、共通ツール、および信頼されたプロセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="2bee6-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="2bee6-105">アプリは、ニーズに合わせて Teams を拡張する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2bee6-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="2bee6-106">Teams で新しいものを作成したり、お気に入りのアプリやサービスで機能を統合したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="2bee6-106">You can create something brand new for Teams or simply integrate features in your favorite apps and services.</span></span>

## <a name="what-can-teams-apps-do"></a><span data-ttu-id="2bee6-107">Teams アプリで実行できること</span><span class="sxs-lookup"><span data-stu-id="2bee6-107">What can Teams apps do?</span></span>

<span data-ttu-id="2bee6-108">ユーザーは、一連のプラットフォーム [機能](capabilities-overview.md)を通じて Teams アプリを見つけて使用します。</span><span class="sxs-lookup"><span data-stu-id="2bee6-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="2bee6-109">単純な (通知を送信する) アプリもあれば、複雑なものもあります (患者の記録の表示)。</span><span class="sxs-lookup"><span data-stu-id="2bee6-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="2bee6-110">アプリを計画するときは、Teams がコラボレーションハブであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2bee6-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="2bee6-111">最良の Teams アプリを使用すると、ユーザーが自分を表現し、連携しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="2bee6-111">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="get-information-more-conveniently"></a><span data-ttu-id="2bee6-112">情報をより簡単に取得する</span><span class="sxs-lookup"><span data-stu-id="2bee6-112">Get information more conveniently</span></span>

<span data-ttu-id="2bee6-113">場合によっては、わかりやすくする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2bee6-113">Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="2bee6-114">重要な web ページを [タブ](doc-links/what-are-tabs.md)で表示します。これにより、チーム内の静的および動的なコンテンツについて全画面 web を利用できます。</span><span class="sxs-lookup"><span data-stu-id="2bee6-114">Display an important webpage in a [tab](doc-links/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

![Teams クライアントでタブがどのように表示されるかを概念として表します。](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a><span data-ttu-id="2bee6-116">コンテキストを切り替えずにリンクを共有する</span><span class="sxs-lookup"><span data-stu-id="2bee6-116">Share links without switching context</span></span>

<span data-ttu-id="2bee6-117">情報を会話にプルし、Teams から退出させない。</span><span class="sxs-lookup"><span data-stu-id="2bee6-117">Pull information into a conversation and never leave Teams.</span></span> <span data-ttu-id="2bee6-118">たとえば、 [メッセージング拡張機能](doc-links/what-are-messaging-extensions.md) を使用すると、[メッセージの作成] ボックスを使用して、外部システムから簡単に digestible コンテンツを共有できます。</span><span class="sxs-lookup"><span data-stu-id="2bee6-118">For example, with [messaging extensions](doc-links/what-are-messaging-extensions.md) you can share rich, easily digestible content from an external system using the message compose box.</span></span>

![Teams クライアントでメッセージング拡張機能がどのように表示されるかを概念的に表現する](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a><span data-ttu-id="2bee6-120">単語をアクションに変換する</span><span class="sxs-lookup"><span data-stu-id="2bee6-120">Turn words into actions</span></span>

<span data-ttu-id="2bee6-121">会話では、多くの場合、何らかの処理 (注文の作成、自分のコードのレビューなど) が必要になります。</span><span class="sxs-lookup"><span data-stu-id="2bee6-121">Conversations often result in the need to do something (create an order, review my code, etc.).</span></span> <span data-ttu-id="2bee6-122">[Bot](doc-links/what-are-bots.md)は、Teams 内でこれらの種類のワークフローを直接開始できます。</span><span class="sxs-lookup"><span data-stu-id="2bee6-122">A [bot](doc-links/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

![Teams クライアントでどのような bot が表示されるかを概念的に表現する](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a><span data-ttu-id="2bee6-124">外部のアプリとサービスと通信する</span><span class="sxs-lookup"><span data-stu-id="2bee6-124">Communicate with external apps and services</span></span>

<span data-ttu-id="2bee6-125">[受信 web フック](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) は、別のアプリから Teams チャネルまたはチャットに通知を自動的に送信する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="2bee6-125">[Incoming webhooks](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send alerts from another app to a Teams channel or chat.</span></span> <span data-ttu-id="2bee6-126">[送信 web フック](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks)を使用すると、@mention を使用して web サービスにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="2bee6-126">With [outgoing webhooks](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), you can send a message to your web service with an @mention.</span></span>

![Teams クライアントでどのコネクタが表示されるかを概念として表します。](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a><span data-ttu-id="2bee6-128">Teams データを利用する</span><span class="sxs-lookup"><span data-stu-id="2bee6-128">Utilize Teams data</span></span>

<span data-ttu-id="2bee6-129">[Teams 用の Microsoft GRAPH REST API](https://docs.microsoft.com/graph/teams-concept-overview)には、teams、チャネル、ユーザー、およびメッセージに関する情報へのアクセスが用意されており、アプリの機能を作成または拡張する際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2bee6-129">The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

![「Teams 用の Microsoft Graph REST API の概念図](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a><span data-ttu-id="2bee6-131">構築を開始する</span><span class="sxs-lookup"><span data-stu-id="2bee6-131">Start building</span></span>

   <span data-ttu-id="2bee6-132">シンプルなアプリを作成し、よく使用されるいくつかの機能を追加することで、Teams の構築にすばやく慣れることができます。</span><span class="sxs-lookup"><span data-stu-id="2bee6-132">Quickly familiarize yourself with building for Teams by creating a simple app and adding a couple commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="2bee6-133">今すぐ最初のアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2bee6-133">Build your first app now</span></span>](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a><span data-ttu-id="2bee6-134">すべてをまとめる</span><span class="sxs-lookup"><span data-stu-id="2bee6-134">Bring it all together</span></span>

   <span data-ttu-id="2bee6-135">組織のお気に入りの web アプリケーション、サービス、およびシステムを Teams の共同作業機能でブレンディングすることにより、ユーザーのプロセスとワークフローを簡素化します。</span><span class="sxs-lookup"><span data-stu-id="2bee6-135">Simplify processes and workflows for users by blending your organization's favorite web apps, services, and systems with Teams collaborative features.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="2bee6-136">既存のアプリを統合する</span><span class="sxs-lookup"><span data-stu-id="2bee6-136">Integrate an existing app</span></span>](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a><span data-ttu-id="2bee6-137">プロセスを信頼する</span><span class="sxs-lookup"><span data-stu-id="2bee6-137">Trust the process</span></span>

   <span data-ttu-id="2bee6-138">Teams プラットフォーム開発プロセス全体を理解し、組織または他のユーザーのためにアプリを効果的に計画、設計、構築、および発行します。</span><span class="sxs-lookup"><span data-stu-id="2bee6-138">Understand the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="2bee6-139">アプリの計画を開始する</span><span class="sxs-lookup"><span data-stu-id="2bee6-139">Start planning your app</span></span>](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a><span data-ttu-id="2bee6-140">コードなし、心配なし</span><span class="sxs-lookup"><span data-stu-id="2bee6-140">No code, no worries</span></span>

   <span data-ttu-id="2bee6-141">魅力的なアプリを構築するためにプログラマである必要はありません。</span><span class="sxs-lookup"><span data-stu-id="2bee6-141">You don't need to be a programmer to build a great app.</span></span> <span data-ttu-id="2bee6-142">Microsoft Power Platform を使用して、ほとんどコードを持たない Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="2bee6-142">Create a Teams app with little to no code using the Microsoft Power Platform.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="2bee6-143">電源プラットフォームアプリのインポート</span><span class="sxs-lookup"><span data-stu-id="2bee6-143">Import a Power Platform app</span></span>](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a><span data-ttu-id="2bee6-144">リソース</span><span class="sxs-lookup"><span data-stu-id="2bee6-144">Resources</span></span>

* <span data-ttu-id="2bee6-145">[Web サイトに [Teams に共有] ボタンを追加する](doc-links/share-to-teams.md)</span><span class="sxs-lookup"><span data-stu-id="2bee6-145">[Add a Share to Teams button to your website](doc-links/share-to-teams.md)</span></span>
* [<span data-ttu-id="2bee6-146">推奨ガイドラインを使用してアプリを設計する</span><span class="sxs-lookup"><span data-stu-id="2bee6-146">Design your app using recommended guidelines</span></span>](doc-links/designing-overview.md)
* [<span data-ttu-id="2bee6-147">Fluent UI デザインシステム</span><span class="sxs-lookup"><span data-stu-id="2bee6-147">Fluent UI Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="2bee6-148">Microsoft Teams JavaScript クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="2bee6-148">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* <span data-ttu-id="2bee6-149">[JavaScript のボット FRAMEWORK sdk](https://github.com/Microsoft/botbuilder-js)および[bot framework sdk (.net](https://github.com/Microsoft/botbuilder-dotnet/) )</span><span class="sxs-lookup"><span data-stu-id="2bee6-149">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
