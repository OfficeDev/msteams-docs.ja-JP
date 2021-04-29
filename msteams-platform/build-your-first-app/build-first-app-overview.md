---
title: 概要 - 最初のアプリの概要と前提条件を構築する
author: girliemac
description: Microsoft Teams アプリ開発を開始し、環境をセットアップする方法について説明します。
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: 3bc99c535ea659f046b65dc26d9a60de0dd49cab
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068572"
---
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="56611-103">Microsoft Teams アプリ開発の開始</span><span class="sxs-lookup"><span data-stu-id="56611-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="56611-104">Teams アプリ開発の基本を学ぶ簡単なアプリを構築します。</span><span class="sxs-lookup"><span data-stu-id="56611-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="56611-105">「Hello, World!」と表示された後、一般的なツール、基本的な概念、高度な機能の詳細については、他の開始記事を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="56611-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="56611-106">学習する情報</span><span class="sxs-lookup"><span data-stu-id="56611-106">What you'll learn</span></span>

* <span data-ttu-id="56611-107">Teams コード拡張機能である Teams ToolkitをVisual Studio実行する</span><span class="sxs-lookup"><span data-stu-id="56611-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension</span></span> 
* <span data-ttu-id="56611-108">App Studio でアプリを構成する</span><span class="sxs-lookup"><span data-stu-id="56611-108">Configure your app with App Studio</span></span> 
* <span data-ttu-id="56611-109">Teams 開発者ツールと SDK について理解する</span><span class="sxs-lookup"><span data-stu-id="56611-109">Get familiar with Teams developer tools and SDKs</span></span>
* <span data-ttu-id="56611-110">認証や設計のベスト プラクティスなど、Teams アプリの重要な概念を検討する</span><span class="sxs-lookup"><span data-stu-id="56611-110">Consider important Teams app concepts, such as authentication and design best practices</span></span>

<span data-ttu-id="56611-111">コマンド ライン インターフェイス (CLI) など、任意のテクノロジを使用して Teams アプリをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="56611-111">You can build Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="56611-112">ただし、これらの記事は、次の推奨ツールとテクノロジを使い始めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="56611-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="56611-113">Teams ToolkitコードVisual Studio拡張機能</span><span class="sxs-lookup"><span data-stu-id="56611-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="56611-114">React.jsの詳細</span><span class="sxs-lookup"><span data-stu-id="56611-114">React.js for tabs</span></span>
* <span data-ttu-id="56611-115">Node.jsおよびメッセージング拡張機能の詳細</span><span class="sxs-lookup"><span data-stu-id="56611-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="56611-116">Teams アプリの基本</span><span class="sxs-lookup"><span data-stu-id="56611-116">Teams app fundamentals</span></span>

<span data-ttu-id="56611-117">自分、組織のユーザー、または世界中のユーザー用にカスタム Teams アプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="56611-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="56611-118">開始する前に、Teams アプリ開発に関する次の基本的な概念を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56611-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="56611-119">アプリの一般的な使用例</span><span class="sxs-lookup"><span data-stu-id="56611-119">Common app use cases</span></span>

<span data-ttu-id="56611-120">カスタム Teams アプリで役立つ一般的なシナリオは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="56611-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="56611-121">Web アプリや Web サイトの一部などの Web ベースのコンテンツを Teams クライアントに埋め込む</span><span class="sxs-lookup"><span data-stu-id="56611-121">Embed web-based content, such as a web app or part of a website, in the Teams client</span></span>
* <span data-ttu-id="56611-122">別のシステムで情報をすばやく参照し、Teams の会話に追加する</span><span class="sxs-lookup"><span data-stu-id="56611-122">Look up information quickly in another system and adding it to a Teams conversation</span></span> 
* <span data-ttu-id="56611-123">会話で言ったことからワークフローとプロセスを直接トリガーする</span><span class="sxs-lookup"><span data-stu-id="56611-123">Trigger workflows and processes directly from what's said in a conversation</span></span> 

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="56611-124">アプリの機能とツール</span><span class="sxs-lookup"><span data-stu-id="56611-124">App capabilities and tools</span></span>

<span data-ttu-id="56611-125">アプリは、1 つ以上の Teams 機能とユーザー操作ポイントで構成されます。</span><span class="sxs-lookup"><span data-stu-id="56611-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="56611-126">開発ツールセットは、必要な機能によって異なります。</span><span class="sxs-lookup"><span data-stu-id="56611-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="56611-127">**アプリの機能**</span><span class="sxs-lookup"><span data-stu-id="56611-127">**App capabilities**</span></span>| <span data-ttu-id="56611-128">**対話ポイント**</span><span class="sxs-lookup"><span data-stu-id="56611-128">**Interaction points**</span></span> | <span data-ttu-id="56611-129">**推奨されるツール**</span><span class="sxs-lookup"><span data-stu-id="56611-129">**Recommended tools**</span></span> | <span data-ttu-id="56611-130">**SDK**</span><span class="sxs-lookup"><span data-stu-id="56611-130">**SDKs**</span></span> | <span data-ttu-id="56611-131">**テクノロジ スタック**</span><span class="sxs-lookup"><span data-stu-id="56611-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="56611-132">タブ</span><span class="sxs-lookup"><span data-stu-id="56611-132">Tabs</span></span> | <span data-ttu-id="56611-133">ユーザーが個人用および共有コンテキストで埋め込み Web コンテンツを操作できるスペース</span><span class="sxs-lookup"><span data-stu-id="56611-133">Spaces where users can interact with embedded web content in personal and shared contexts</span></span> | <span data-ttu-id="56611-134">Vs Code with Teams Toolkitまたは Yeoman Generator</span><span class="sxs-lookup"><span data-stu-id="56611-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="56611-135">Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="56611-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="56611-136">一般的な Web テクノロジ (HTML、CSS、JavaScript) または React.js</span><span class="sxs-lookup"><span data-stu-id="56611-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="56611-137">ボット</span><span class="sxs-lookup"><span data-stu-id="56611-137">Bots</span></span> | <span data-ttu-id="56611-138">個人と共有のコンテキストでユーザーと対話するチャットボット</span><span class="sxs-lookup"><span data-stu-id="56611-138">Chatbots that interact with users in personal and shared contexts</span></span> | <span data-ttu-id="56611-139">Vs Code with Teams Toolkitまたは Yeoman Generator</span><span class="sxs-lookup"><span data-stu-id="56611-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="56611-140">Bot Franework SDK</span><span class="sxs-lookup"><span data-stu-id="56611-140">Bot Franework SDK</span></span> | <span data-ttu-id="56611-141">Node.js、C#、または Python</span><span class="sxs-lookup"><span data-stu-id="56611-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="56611-142">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="56611-142">Messaging extensions</span></span> | <span data-ttu-id="56611-143">会話から離れることなく、アプリ コンテンツを挿入したり、メッセージに対して操作したりするためのショートカット</span><span class="sxs-lookup"><span data-stu-id="56611-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation</span></span> | <span data-ttu-id="56611-144">Vs Code with Teams Toolkitまたは Yeoman Generator</span><span class="sxs-lookup"><span data-stu-id="56611-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="56611-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="56611-145">Bot Framework SDK</span></span> | <span data-ttu-id="56611-146">Node.js、C#、または Python</span><span class="sxs-lookup"><span data-stu-id="56611-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="56611-147">Teams がアプリをホストしない</span><span class="sxs-lookup"><span data-stu-id="56611-147">Teams doesn't host your app</span></span>

<span data-ttu-id="56611-148">ユーザーが Teams にアプリをインストールする場合、構成ファイル (アプリ マニフェストとも呼ばれる) とアプリのアイコンを含むアプリ パッケージのみをインストールします。</span><span class="sxs-lookup"><span data-stu-id="56611-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="56611-149">アプリのロジックとデータ ストレージは、開発中に Azure Web Services や localhost など、他の場所でホストされます。</span><span class="sxs-lookup"><span data-stu-id="56611-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="56611-150">Teams は HTTPS を介してこれらのリソースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="56611-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Teams でアプリを示す図は、クラウド サーバー内のアプリ ロジックを指しています。":::

## <a name="next-step"></a><span data-ttu-id="56611-152">次の手順</span><span class="sxs-lookup"><span data-stu-id="56611-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56611-153">最初の Teams アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="56611-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
