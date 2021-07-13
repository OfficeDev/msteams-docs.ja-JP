---
title: アプリ コードのサンプル
description: 開発者向けプラットフォームのサンプル アプリケーションのMicrosoft Teams説明
localization_priority: Normal
ms.topic: reference
keywords: Microsoft Teamsサンプル
ms.openlocfilehash: 09369123f23fc76b5e8c9fe3d5e89df56763d21f
ms.sourcegitcommit: 10380fc80d7f281d2892b3514f87d1bd05180496
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2021
ms.locfileid: "53373915"
---
# <a name="overview"></a><span data-ttu-id="1cb16-104">概要</span><span class="sxs-lookup"><span data-stu-id="1cb16-104">Overview</span></span>

<span data-ttu-id="1cb16-105">このチュートリアルでは、React、Blazor、SPFx、C#、.NET、Node.js、および Yeoman Generator を使用してアプリを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1cb16-105">In this tutorial, you will learn how to create an app using React, Blazor, SPFx, C# or .NET, Node.js, and Yeoman Generator.</span></span> <span data-ttu-id="1cb16-106">また、最初のボットとメッセージング拡張機能を作成する方法も学習します。</span><span class="sxs-lookup"><span data-stu-id="1cb16-106">You will also learn to create your first bot and messaging extension.</span></span> <span data-ttu-id="1cb16-107">このチュートリアルでは、タブ、ボット、メッセージング拡張機能、Webhooks とコネクタ、およびアプリのカスタマイズと構成に役立つ Graph API 用の複数のコード サンプルについて説明します。</span><span class="sxs-lookup"><span data-stu-id="1cb16-107">This tutorial will take you through multiple Code Samples for Tabs, Bots, Messaging Extensions, Webhooks and Connectors, and Graph APIs that will help you to customize and configure your apps.</span></span> <span data-ttu-id="1cb16-108">さらに、「Microsoft Learn」セクションを参照して、カスタム アプリを作成することで、開発者Teams機能を拡張することもできます。</span><span class="sxs-lookup"><span data-stu-id="1cb16-108">In addition, you can also refer to the Microsoft Learn sections where you can extend the Teams developer platform capabilities by creating custom apps.</span></span>  

## <a name="getting-started-with-microsoft-learn"></a><span data-ttu-id="1cb16-109">Microsoft Learn の使用を開始する</span><span class="sxs-lookup"><span data-stu-id="1cb16-109">Getting started with Microsoft Learn</span></span>

| <span data-ttu-id="1cb16-110">**機能**</span><span class="sxs-lookup"><span data-stu-id="1cb16-110">**Capability**</span></span>| <span data-ttu-id="1cb16-111">**Learn モジュール**</span><span class="sxs-lookup"><span data-stu-id="1cb16-111">**Learn module**</span></span>|
|--------|-------------|
| <span data-ttu-id="1cb16-112">タブ - 埋め込み Web エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="1cb16-112">Tabs  — embedded web experiences</span></span>  |  [<span data-ttu-id="1cb16-113">Microsoft Teams のタブによる埋め込み Web エクスペリエンスの作成</span><span class="sxs-lookup"><span data-stu-id="1cb16-113">Create embedded web experiences with tabs for Microsoft Teams</span></span>](/learn/modules/embedded-web-experiences/) |
| <span data-ttu-id="1cb16-114">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="1cb16-114">Webhooks and connectors</span></span>  |  [<span data-ttu-id="1cb16-115">Webhook と Office 365 コネクタを使用して Web サービスを Microsoft Teams に接続する</span><span class="sxs-lookup"><span data-stu-id="1cb16-115">Connect web services to Microsoft Teams with webhooks and Office 365 Connectors</span></span>](/learn/modules/msteams-webhooks-connectors/) |
|<span data-ttu-id="1cb16-116">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1cb16-116">Messaging extensions</span></span>  | [<span data-ttu-id="1cb16-117">メッセージング拡張機能による Microsoft Teams でのタスク指向の相互作用</span><span class="sxs-lookup"><span data-stu-id="1cb16-117">Task-oriented interactions in Microsoft Teams with messaging extensions</span></span>](/learn/modules/msteams-messaging-extensions/)  |
| <span data-ttu-id="1cb16-118">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="1cb16-118">Task modules</span></span> |  [<span data-ttu-id="1cb16-119">タスク モジュールを使用Microsoft Teams入力を収集する</span><span class="sxs-lookup"><span data-stu-id="1cb16-119">Collect input in Microsoft Teams with Task Modules</span></span>](/learn/modules/msteams-task-modules/) |
| <span data-ttu-id="1cb16-120">会話型ボット</span><span class="sxs-lookup"><span data-stu-id="1cb16-120">Conversational bots</span></span>  | [<span data-ttu-id="1cb16-121">Microsoft Teams 向けの対話型ボットの作成</span><span class="sxs-lookup"><span data-stu-id="1cb16-121">Create interactive conversational bots for Microsoft Teams</span></span>](/learn/modules/msteams-conversation-bots/)  |

## <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="1cb16-122">アプリの最初のMicrosoft Teamsを作成する</span><span class="sxs-lookup"><span data-stu-id="1cb16-122">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="1cb16-123">開始方法 **のレッスン** では、基本的なアプリを作成するTeamsします。</span><span class="sxs-lookup"><span data-stu-id="1cb16-123">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="1cb16-124">各チュートリアルでは、一般的なツール、基本的な概念、より高度な機能を紹介しながら、Teams実際のアプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1cb16-124">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

### <a name="teams-app-fundamentals"></a><span data-ttu-id="1cb16-125">Teamsアプリの基本</span><span class="sxs-lookup"><span data-stu-id="1cb16-125">Teams app fundamentals</span></span>

<span data-ttu-id="1cb16-126">開発者[Teamsを使用すると、](../overview.md)カスタム アプリをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="1cb16-126">The [Teams developer platform](../overview.md) lets you build custom apps.</span></span> <span data-ttu-id="1cb16-127">Microsoft Teams のカスタム アプリが役立つ一般的なシナリオには、以下のようなシナリが含まれます。</span><span class="sxs-lookup"><span data-stu-id="1cb16-127">Some common scenarios that a custom Microsoft Teams app can help with are:</span></span>

* <span data-ttu-id="1cb16-128">Web サイトまたは Web アプリを Teams クライアントに直接埋め込む。</span><span class="sxs-lookup"><span data-stu-id="1cb16-128">Embed your website or web app directly in the Teams client.</span></span>
* <span data-ttu-id="1cb16-129">ユーザーが別のシステムで情報をすばやく検索し、その結果を別のシステムの会話に追加Teams。</span><span class="sxs-lookup"><span data-stu-id="1cb16-129">Help users quickly look up information in another system and add the results to a conversation in Teams.</span></span>
* <span data-ttu-id="1cb16-130">Teams での会話に基づいてワークフローとプロセスをトリガーし、会話のコンテキストを保持する。</span><span class="sxs-lookup"><span data-stu-id="1cb16-130">Trigger workflows and processes based on a conversation in Teams, preserving the context of the conversation.</span></span>

<span data-ttu-id="1cb16-131">チュートリアルを開始する前に、アプリの作成に関する以下の情報をTeams。</span><span class="sxs-lookup"><span data-stu-id="1cb16-131">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="app-capabilities"></a><span data-ttu-id="1cb16-132">アプリの機能</span><span class="sxs-lookup"><span data-stu-id="1cb16-132">App capabilities</span></span>

<span data-ttu-id="1cb16-133">アプリTeamsは、1 つ以上の[プラットフォーム機能と](../concepts/capabilities-overview.md)ユーザー操作ポイント[で構成されます](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb16-133">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [user interaction points](../concepts/extensibility-points.md).</span></span>

<span data-ttu-id="1cb16-134">アプリに必要な機能に応じて、適切な開発ツールセットが必要です。</span><span class="sxs-lookup"><span data-stu-id="1cb16-134">Depending on what capabilities you want for your app, you will need an appropriate development toolset.</span></span>

<span data-ttu-id="1cb16-135">|アプリの機能|ユーザーの操作|推奨されるツール|SDK |テクノロジ スタック| |--------|-------------||--------||--------||--------| |タブ|フルスクリーンの埋め込み Web エクスペリエンス。</span><span class="sxs-lookup"><span data-stu-id="1cb16-135">| App capabilities | User interactions | Recommended tools | SDKs | Technology stacks | |--------|-------------||--------||--------||--------| | Tabs | A full-screen embedded web experience.</span></span> <span data-ttu-id="1cb16-136">|VS Code拡張子Teams Toolkit、または YoTeams (Yeoman Generator) |[Teams SDK |](/javascript/api/overview/msteams-client)Web テクノロジ全般、HTML、CSS、JavaScript | |ボット |メンバーと会話するチャット ボット。</span><span class="sxs-lookup"><span data-stu-id="1cb16-136">| VS Code with Teams Toolkit extension, or YoTeams (Yeoman Generator) | [Teams client SDK](/javascript/api/overview/msteams-client) | Web technology in general, HTML, CSS, and JavaScript | | Bots | A chat bot that converses with members.</span></span> <span data-ttu-id="1cb16-137">|VS Code拡張子Teams Toolkit、または YoTeams (Yeoman Generator) |[Bot Framework SDK](https://dev.botframework.com/) |Node.js、C#、または Python の| |メッセージング拡張機能|会話に外部コンテンツを挿入したり、メッセージに対してアクションを実行したりするショートカット。</span><span class="sxs-lookup"><span data-stu-id="1cb16-137">| VS Code with Teams Toolkit extension, or YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, or Python | | Messaging extensions | Shortcuts for inserting external content into a conversation or taking action on messages.</span></span> <span data-ttu-id="1cb16-138">|VS Code拡張子Teams Toolkit、または YoTeams (Yeoman Generator) |[Bot Framework SDK](https://dev.botframework.com/) |Node.js、C#、または Python の|</span><span class="sxs-lookup"><span data-stu-id="1cb16-138">| VS Code with Teams Toolkit extension, or YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, or Python |</span></span>

<span data-ttu-id="1cb16-139">[スタート] セクションでは、これらの特定のスタックの使用に限定されませんが、推奨されるツール セットと一般的に使用されるテクノロジ (Teams 拡張子を持つ Visual Studio Code、タブの場合は React.js、ボットやメッセージング拡張機能の場合は Node.js など) について説明します。</span><span class="sxs-lookup"><span data-stu-id="1cb16-139">The Get started section will take you through recommended tool sets and commonly used technologies, such as Visual Studio Code with Teams extension, React.js for tabs, and Node.js for bots and messaging extensions, although *you are not limited to using these particular stacks*.</span></span>

<span data-ttu-id="1cb16-140">コマンド ライン インターフェイス (CLI) の使用を希望する場合は、「Yeoman ジェネレーターを使用Microsoft Teamsアプリを作成する[」を参照してください](../get-started/get-started-yeoman.md)。</span><span class="sxs-lookup"><span data-stu-id="1cb16-140">If you prefer using a command-line interface (CLI), see [create your first Microsoft Teams app using the Yeoman generator](../get-started/get-started-yeoman.md).</span></span>

### <a name="teams-does-not-host-your-app"></a><span data-ttu-id="1cb16-141">Teamsアプリをホストしない</span><span class="sxs-lookup"><span data-stu-id="1cb16-141">Teams does not host your app</span></span>

<span data-ttu-id="1cb16-142">マニフェストとアプリ アイコンと呼ばれる構成ファイルを含むアプリ パッケージのみをインストールして、クライアントTeamsします。</span><span class="sxs-lookup"><span data-stu-id="1cb16-142">You will only install an app package that contains a configuration file, called manifest and app icons to Teams client.</span></span> <span data-ttu-id="1cb16-143">アプリ ロジックとデータ ストレージの残りの部分は、Azure Web Services などの他の場所でホストされます。</span><span class="sxs-lookup"><span data-stu-id="1cb16-143">The rest of the app logics and data storage are hosted elsewhere, such as Azure Web Services.</span></span> <span data-ttu-id="1cb16-144">開発中のクラウドまたは localhost 内のアプリは、HTTPS 経由でTeamsアクセスします。</span><span class="sxs-lookup"><span data-stu-id="1cb16-144">Your app in the cloud or localhost during your development accesses Teams via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="クラウド サーバーでアプリ ロジックTeams示すアプリを示す図。":::

## <a name="see-also"></a><span data-ttu-id="1cb16-146">関連項目</span><span class="sxs-lookup"><span data-stu-id="1cb16-146">See also</span></span>

* [<span data-ttu-id="1cb16-147">アプリを使用してアプリを作成React</span><span class="sxs-lookup"><span data-stu-id="1cb16-147">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="1cb16-148">Blazor を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="1cb16-148">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="1cb16-149">アプリを使用してアプリを作成SPFx</span><span class="sxs-lookup"><span data-stu-id="1cb16-149">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="1cb16-150">C# を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="1cb16-150">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="1cb16-151">Node.js を使ってアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="1cb16-151">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="1cb16-152">Yeoman ジェネレーターを使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="1cb16-152">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="1cb16-153">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="1cb16-153">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="1cb16-154">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="1cb16-154">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="1cb16-155">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="1cb16-155">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)