---
title: はじめに - 最初のアプリの概要と前提条件を構築する
author: girliemac
description: アプリ開発の開始方法Microsoft Teams、環境を設定する方法について説明します。
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565880"
---
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="89007-103">アプリ開発Microsoft Teams始める</span><span class="sxs-lookup"><span data-stu-id="89007-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="89007-104">アプリ開発の基本を学ぶ簡単なアプリTeams構築します。</span><span class="sxs-lookup"><span data-stu-id="89007-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="89007-105">"Hello, World!"が表示されたら、一般的なツール、基本的な概念、高度な機能の詳細については、他の概要記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="89007-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="89007-106">あなたが学ぶこと</span><span class="sxs-lookup"><span data-stu-id="89007-106">What you'll learn</span></span>

* <span data-ttu-id="89007-107">Teams Toolkit、Visual Studio Code拡張機能で迅速に起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="89007-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension.</span></span> 
* <span data-ttu-id="89007-108">アプリスタジオでアプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="89007-108">Configure your app with App Studio.</span></span>
* <span data-ttu-id="89007-109">開発者ツールと SDK Teamsについて理解する。</span><span class="sxs-lookup"><span data-stu-id="89007-109">Get familiar with Teams developer tools and SDKs.</span></span>
* <span data-ttu-id="89007-110">認証や設計のベスト プラクティスなど、重要なTeamsアプリの概念を考慮します。</span><span class="sxs-lookup"><span data-stu-id="89007-110">Consider important Teams app concepts, such as authentication and design best practices.</span></span>

<span data-ttu-id="89007-111">任意のテクノロジ (たとえば、コマンド ライン インターフェイス (CLI) を使用して、Teams アプリをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="89007-111">You can build a Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="89007-112">ただし、これらの記事は、次の推奨ツールとテクノロジを使用する際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="89007-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="89007-113">Teams Toolkit、Visual Studio Code拡張</span><span class="sxs-lookup"><span data-stu-id="89007-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="89007-114">タブのReact.js</span><span class="sxs-lookup"><span data-stu-id="89007-114">React.js for tabs</span></span>
* <span data-ttu-id="89007-115">ボットとメッセージング拡張機能のNode.js</span><span class="sxs-lookup"><span data-stu-id="89007-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="89007-116">アプリの基礎をTeamsする</span><span class="sxs-lookup"><span data-stu-id="89007-116">Teams app fundamentals</span></span>

<span data-ttu-id="89007-117">カスタム Teams アプリケーションは、自分自身、組織内のユーザー、または世界中のユーザー用に構築できます。</span><span class="sxs-lookup"><span data-stu-id="89007-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="89007-118">開始する前に、アプリ開発に関する次の基本概念Teams理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="89007-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="89007-119">一般的なアプリのユース ケース</span><span class="sxs-lookup"><span data-stu-id="89007-119">Common app use cases</span></span>

<span data-ttu-id="89007-120">カスタム Teams アプリが役立つ一般的なシナリオは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="89007-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="89007-121">web アプリや Web サイトの一部などの Web ベースのコンテンツをTeams クライアントに埋め込みます。</span><span class="sxs-lookup"><span data-stu-id="89007-121">Embed web-based content, such as a web app or part of a website, in the Teams client.</span></span>
* <span data-ttu-id="89007-122">別のシステムで情報をすばやく検索し、Teams会話に追加します。</span><span class="sxs-lookup"><span data-stu-id="89007-122">Look up information quickly in another system and adding it to a Teams conversation.</span></span>
* <span data-ttu-id="89007-123">会話で言ったことから直接ワークフローとプロセスをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="89007-123">Trigger workflows and processes directly from what's said in a conversation.</span></span>

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="89007-124">アプリの機能とツール</span><span class="sxs-lookup"><span data-stu-id="89007-124">App capabilities and tools</span></span>

<span data-ttu-id="89007-125">アプリは、1 つ以上のTeams機能とユーザー操作ポイントで構成されます。</span><span class="sxs-lookup"><span data-stu-id="89007-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="89007-126">開発ツールセットは、必要な機能によって異なります。</span><span class="sxs-lookup"><span data-stu-id="89007-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="89007-127">**アプリの機能**</span><span class="sxs-lookup"><span data-stu-id="89007-127">**App capabilities**</span></span>| <span data-ttu-id="89007-128">**相互作用ポイント**</span><span class="sxs-lookup"><span data-stu-id="89007-128">**Interaction points**</span></span> | <span data-ttu-id="89007-129">**推奨ツール**</span><span class="sxs-lookup"><span data-stu-id="89007-129">**Recommended tools**</span></span> | <span data-ttu-id="89007-130">**SDK**</span><span class="sxs-lookup"><span data-stu-id="89007-130">**SDKs**</span></span> | <span data-ttu-id="89007-131">**テクノロジースタック**</span><span class="sxs-lookup"><span data-stu-id="89007-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="89007-132">タブ</span><span class="sxs-lookup"><span data-stu-id="89007-132">Tabs</span></span> | <span data-ttu-id="89007-133">ユーザーが、個人コンテキストおよび共有コンテキストで埋め込み Web コンテンツを操作できるスペース。</span><span class="sxs-lookup"><span data-stu-id="89007-133">Spaces where users can interact with embedded web content in personal and shared contexts.</span></span> | <span data-ttu-id="89007-134">Teams Toolkit拡張またはヨーマンジェネレータを備えたVS Code</span><span class="sxs-lookup"><span data-stu-id="89007-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="89007-135">Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="89007-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="89007-136">一般的な Web テクノロジ (HTML、CSS、および JavaScript) またはReact.js</span><span class="sxs-lookup"><span data-stu-id="89007-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="89007-137">ボット</span><span class="sxs-lookup"><span data-stu-id="89007-137">Bots</span></span> | <span data-ttu-id="89007-138">個人コンテキストおよび共有コンテキストでユーザーと対話するチャットボット。</span><span class="sxs-lookup"><span data-stu-id="89007-138">Chatbots that interact with users in personal and shared contexts.</span></span> | <span data-ttu-id="89007-139">Teams Toolkit拡張またはヨーマンジェネレータを備えたVS Code</span><span class="sxs-lookup"><span data-stu-id="89007-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="89007-140">ボット フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="89007-140">Bot Framework SDK</span></span> | <span data-ttu-id="89007-141">Node.js、C# または Python</span><span class="sxs-lookup"><span data-stu-id="89007-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="89007-142">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="89007-142">Messaging extensions</span></span> | <span data-ttu-id="89007-143">会話から離れることなく、アプリコンテンツを挿入したり、メッセージに対して操作を行ったりするためのショートカット。</span><span class="sxs-lookup"><span data-stu-id="89007-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> | <span data-ttu-id="89007-144">Teams Toolkit拡張またはヨーマンジェネレータを備えたVS Code</span><span class="sxs-lookup"><span data-stu-id="89007-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="89007-145">ボット フレームワーク SDK</span><span class="sxs-lookup"><span data-stu-id="89007-145">Bot Framework SDK</span></span> | <span data-ttu-id="89007-146">Node.js、C# または Python</span><span class="sxs-lookup"><span data-stu-id="89007-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="89007-147">Teamsアプリをホストしない</span><span class="sxs-lookup"><span data-stu-id="89007-147">Teams doesn't host your app</span></span>

<span data-ttu-id="89007-148">ユーザーがアプリをTeamsにインストールすると、構成ファイル (アプリ マニフェストとも呼ばれます) とアプリのアイコンを含むアプリ パッケージのみがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="89007-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="89007-149">アプリのロジックとデータ ストレージは、開発中に Azure Web サービスやローカル ホストなどの他の場所でホストされます。</span><span class="sxs-lookup"><span data-stu-id="89007-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="89007-150">Teams HTTPS を介してこれらのリソースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="89007-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="アプリをTeamsに示す図は、クラウド サーバーでアプリ ロジックを指しています。":::

## <a name="next-step"></a><span data-ttu-id="89007-152">次の手順</span><span class="sxs-lookup"><span data-stu-id="89007-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89007-153">初めてのTeamsアプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="89007-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
