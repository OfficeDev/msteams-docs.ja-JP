---
title: 概要 - 最初のアプリの概要と前提条件を構築する
author: girliemac
description: アプリの開発を開始しMicrosoft Teams環境をセットアップする方法について学習します。
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
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="ff29d-103">アプリ開発Microsoft Teams開始する</span><span class="sxs-lookup"><span data-stu-id="ff29d-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="ff29d-104">シンプルなアプリを構築して、アプリ開発の基本Teams学ぶ。</span><span class="sxs-lookup"><span data-stu-id="ff29d-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="ff29d-105">「Hello, World!」と表示された後、一般的なツール、基本的な概念、高度な機能の詳細については、他の開始記事を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="ff29d-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="ff29d-106">学習する情報</span><span class="sxs-lookup"><span data-stu-id="ff29d-106">What you'll learn</span></span>

* <span data-ttu-id="ff29d-107">新しい拡張機能である Teams Toolkitを使用してVisual Studio Code実行します。</span><span class="sxs-lookup"><span data-stu-id="ff29d-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension.</span></span> 
* <span data-ttu-id="ff29d-108">App Studio を使用してアプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="ff29d-108">Configure your app with App Studio.</span></span>
* <span data-ttu-id="ff29d-109">開発者向けツールTeams SDK について理解する。</span><span class="sxs-lookup"><span data-stu-id="ff29d-109">Get familiar with Teams developer tools and SDKs.</span></span>
* <span data-ttu-id="ff29d-110">認証やTeamsなど、アプリの概念に関する重要な点を検討してください。</span><span class="sxs-lookup"><span data-stu-id="ff29d-110">Consider important Teams app concepts, such as authentication and design best practices.</span></span>

<span data-ttu-id="ff29d-111">コマンド ライン インターフェイス (CLI) などTeams任意のテクノロジを使用して、アプリをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="ff29d-111">You can build a Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="ff29d-112">ただし、これらの記事は、次の推奨ツールとテクノロジを使い始めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ff29d-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="ff29d-113">Teams Toolkit、Visual Studio Code拡張子</span><span class="sxs-lookup"><span data-stu-id="ff29d-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="ff29d-114">React.jsの詳細</span><span class="sxs-lookup"><span data-stu-id="ff29d-114">React.js for tabs</span></span>
* <span data-ttu-id="ff29d-115">Node.jsおよびメッセージング拡張機能の詳細</span><span class="sxs-lookup"><span data-stu-id="ff29d-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="ff29d-116">Teamsアプリの基本</span><span class="sxs-lookup"><span data-stu-id="ff29d-116">Teams app fundamentals</span></span>

<span data-ttu-id="ff29d-117">自分、組織Teams、世界中のユーザー向けカスタム アプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ff29d-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="ff29d-118">開始する前に、アプリ開発に関する次の基本的なTeams理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff29d-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="ff29d-119">アプリの一般的な使用例</span><span class="sxs-lookup"><span data-stu-id="ff29d-119">Common app use cases</span></span>

<span data-ttu-id="ff29d-120">カスタム アプリで役立つ一Teamsシナリオは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ff29d-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="ff29d-121">Web アプリや Web サイトの一部などの Web ベースのコンテンツをクライアントに埋め込Teamsします。</span><span class="sxs-lookup"><span data-stu-id="ff29d-121">Embed web-based content, such as a web app or part of a website, in the Teams client.</span></span>
* <span data-ttu-id="ff29d-122">別のシステムで情報をすばやく参照し、その情報を別のTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ff29d-122">Look up information quickly in another system and adding it to a Teams conversation.</span></span>
* <span data-ttu-id="ff29d-123">会話で言ったことからワークフローとプロセスを直接トリガーします。</span><span class="sxs-lookup"><span data-stu-id="ff29d-123">Trigger workflows and processes directly from what's said in a conversation.</span></span>

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="ff29d-124">アプリの機能とツール</span><span class="sxs-lookup"><span data-stu-id="ff29d-124">App capabilities and tools</span></span>

<span data-ttu-id="ff29d-125">アプリは、1 つ以上の機能とユーザー Teamsポイントで構成されます。</span><span class="sxs-lookup"><span data-stu-id="ff29d-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="ff29d-126">開発ツールセットは、必要な機能によって異なります。</span><span class="sxs-lookup"><span data-stu-id="ff29d-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="ff29d-127">**アプリの機能**</span><span class="sxs-lookup"><span data-stu-id="ff29d-127">**App capabilities**</span></span>| <span data-ttu-id="ff29d-128">**対話ポイント**</span><span class="sxs-lookup"><span data-stu-id="ff29d-128">**Interaction points**</span></span> | <span data-ttu-id="ff29d-129">**推奨されるツール**</span><span class="sxs-lookup"><span data-stu-id="ff29d-129">**Recommended tools**</span></span> | <span data-ttu-id="ff29d-130">**SDK**</span><span class="sxs-lookup"><span data-stu-id="ff29d-130">**SDKs**</span></span> | <span data-ttu-id="ff29d-131">**テクノロジ スタック**</span><span class="sxs-lookup"><span data-stu-id="ff29d-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="ff29d-132">タブ</span><span class="sxs-lookup"><span data-stu-id="ff29d-132">Tabs</span></span> | <span data-ttu-id="ff29d-133">ユーザーが個人および共有コンテキストで埋め込み Web コンテンツを操作できるスペース。</span><span class="sxs-lookup"><span data-stu-id="ff29d-133">Spaces where users can interact with embedded web content in personal and shared contexts.</span></span> | <span data-ttu-id="ff29d-134">VS Code拡張子Teams Toolkit Yeoman Generator</span><span class="sxs-lookup"><span data-stu-id="ff29d-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="ff29d-135">Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="ff29d-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="ff29d-136">一般的な Web テクノロジ (HTML、CSS、JavaScript) または React.js</span><span class="sxs-lookup"><span data-stu-id="ff29d-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="ff29d-137">ボット</span><span class="sxs-lookup"><span data-stu-id="ff29d-137">Bots</span></span> | <span data-ttu-id="ff29d-138">個人と共有のコンテキストでユーザーとやり取りするチャットボット。</span><span class="sxs-lookup"><span data-stu-id="ff29d-138">Chatbots that interact with users in personal and shared contexts.</span></span> | <span data-ttu-id="ff29d-139">VS Code拡張子Teams Toolkit Yeoman Generator</span><span class="sxs-lookup"><span data-stu-id="ff29d-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="ff29d-140">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="ff29d-140">Bot Framework SDK</span></span> | <span data-ttu-id="ff29d-141">Node.js、C#、または Python</span><span class="sxs-lookup"><span data-stu-id="ff29d-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="ff29d-142">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="ff29d-142">Messaging extensions</span></span> | <span data-ttu-id="ff29d-143">会話から離れることなく、アプリ コンテンツを挿入したり、メッセージに対して操作したりするためのショートカット。</span><span class="sxs-lookup"><span data-stu-id="ff29d-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> | <span data-ttu-id="ff29d-144">VS Code拡張子Teams Toolkit Yeoman Generator</span><span class="sxs-lookup"><span data-stu-id="ff29d-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="ff29d-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="ff29d-145">Bot Framework SDK</span></span> | <span data-ttu-id="ff29d-146">Node.js、C#、または Python</span><span class="sxs-lookup"><span data-stu-id="ff29d-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="ff29d-147">Teamsアプリをホストしない</span><span class="sxs-lookup"><span data-stu-id="ff29d-147">Teams doesn't host your app</span></span>

<span data-ttu-id="ff29d-148">ユーザーがアプリを Teams にインストールすると、構成ファイル (アプリ マニフェストとも呼ばれる) とアプリのアイコンを含むアプリ パッケージだけがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="ff29d-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="ff29d-149">アプリのロジックとデータ ストレージは、開発中に Azure Web Services や localhost など、他の場所でホストされます。</span><span class="sxs-lookup"><span data-stu-id="ff29d-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="ff29d-150">Teams HTTPS 経由でこれらのリソースにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="ff29d-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="クラウド サーバーでアプリ ロジックTeams示すアプリを示す図。":::

## <a name="next-step"></a><span data-ttu-id="ff29d-152">次の手順</span><span class="sxs-lookup"><span data-stu-id="ff29d-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff29d-153">最初のアプリをビルドしてTeamsする</span><span class="sxs-lookup"><span data-stu-id="ff29d-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
