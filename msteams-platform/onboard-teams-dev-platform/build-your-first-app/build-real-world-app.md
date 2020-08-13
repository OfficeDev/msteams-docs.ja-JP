---
title: 初めて Teams アプリを作成する
author: heath-hamilton
description: 現実の Microsoft Teams アプリを構築するためのチュートリアル
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655675"
---
# <a name="learn-how-to-build-your-first-teams-app"></a><span data-ttu-id="ffa5d-103">最初の Teams アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-103">Learn how to build your first Teams app</span></span>

<span data-ttu-id="ffa5d-104">**最初のアプリ**を作成するときに、チュートリアルを使用して基本的な Teams アプリを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-104">In **Build your first app**, you learn how to create a basic Teams app through tutorials.</span></span> <span data-ttu-id="ffa5d-105">各レッスンは相互に構築されており、簡単な実世界の Teams アプリを作成する手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-105">The lessons build on each other, walking you through each step of creating a simple, real-world Teams app.</span></span> <span data-ttu-id="ffa5d-106">一般的なツール、基本概念、および便利なリンクについて紹介します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-106">We introduce you to common tools, fundamental concepts, and useful links along the way.</span></span>

<span data-ttu-id="ffa5d-107">最初に、"Hello, World!" の作成と実行について説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-107">You'll start with creating and running a "Hello, World!"</span></span> <span data-ttu-id="ffa5d-108">タブアプリ</span><span class="sxs-lookup"><span data-stu-id="ffa5d-108">tab app.</span></span> <span data-ttu-id="ffa5d-109">次に、いくつかの簡単な UI を作成し、Microsoft Teams Javascript SDK を使用して役に立つコンテキストを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-109">You'll then create some simple UI and learn how to get useful context with the Microsoft Teams Javascript SDK.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ffa5d-110">学習内容</span><span class="sxs-lookup"><span data-stu-id="ffa5d-110">What you'll learn</span></span>

> [!div class="checklist"]
  >
  > - <span data-ttu-id="ffa5d-111">**Teams ツールキットを使用**して迅速に作業を開始します。 Visual Studio 用の Microsoft Teams toolkit は、アプリプロジェクトとスキャフォールディングを作成するためのものであり、実行中のアプリを数分で利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-111">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > - <span data-ttu-id="ffa5d-112">**マニフェストを使用**してアプリを定義します。マニフェストは、Teams アプリが使用する機能とサービスを指定する青写真です。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-112">**Define your app with the manifest**: The manifest is a blueprint where you specify the capabilities and services your Teams app uses.</span></span>
  > - <span data-ttu-id="ffa5d-113">**対象ユーザーの範囲**: 個人使用またはコラボレーション用に Teams アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-113">**Scope your audience**: You can build a Teams app for personal use or collaboration.</span></span> <span data-ttu-id="ffa5d-114">このチュートリアルでは、チャネルまたはチャットで、個々のユーザーまたはユーザーグループにタブを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-114">In the tutorials, you'll learn how build a tab for individual users or a group of people in a channel or chat.</span></span>
  > - <span data-ttu-id="ffa5d-115">**TEAMS sdk を利用してコンテキストを取得**する: Microsoft TEAMS JavaScript SDK を使用してテーマの変更を実行する方法と構成の操作を設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-115">**Utilize Teams SDK to get context**: Learn how to use the Microsoft Teams JavaScript SDK to perform theme change or set up configuration experience</span></span>  
  > - <span data-ttu-id="ffa5d-116">**アプリの展開**: チュートリアル全体を通して、よくある関連トピックにリンクしています (認証とデザインのガイドラインを含む)。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-116">**Expand on your app**: Throughout the tutorials, we link to related topics you're probably interested in (some of which include authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="ffa5d-117">Teams アプリの基礎</span><span class="sxs-lookup"><span data-stu-id="ffa5d-117">Teams app fundamentals</span></span>

<span data-ttu-id="ffa5d-118">チュートリアルを開始する前に、Teams 用のアプリの作成に関する以下の情報を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-118">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities"></a><span data-ttu-id="ffa5d-119">アプリは複数の機能を持つことができる</span><span class="sxs-lookup"><span data-stu-id="ffa5d-119">Apps can have multiple capabilities</span></span>

<span data-ttu-id="ffa5d-120">Teams アプリは、[タブ](../doc-links/what-are-tabs.md)、[ボット](../doc-links/what-are-bots.md )、[メッセージング拡張](../doc-links/what-are-messaging-extensions.md)機能、および[webhook やコネクタ](../doc-links/what-are-webhooks-and-connectors.md)など、1つ以上の[プラットフォーム機能](../capabilities-overview.md)で構成されます。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-120">Teams apps are made up of one or more [platform capabilities](../capabilities-overview.md), including [tabs](../doc-links/what-are-tabs.md), [bots](../doc-links/what-are-bots.md ), [messaging extensions](../doc-links/what-are-messaging-extensions.md), and [webhooks and connectors](../doc-links/what-are-webhooks-and-connectors.md).</span></span> <span data-ttu-id="ffa5d-121">Teams アプリには、カード、タスクモジュール、詳細なリンクなど、多くの[UI 規則や要素](../doc-links/teams-ui-conventions.md)があります。これを使用して、最高のユーザー環境を構築することができます。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-121">Teams apps also have many [UI conventions and elements](../doc-links/teams-ui-conventions.md), such as cards, task modules, and deep linking, you can use to build the best possible user experience.</span></span>

<span data-ttu-id="ffa5d-122">このチュートリアルでは、タブのみを作成しますが、ボットまたはその他の機能をアプリに追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-122">For these tutorials, you'll build only tabs but can add a bot or other capability to your app as you like.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="ffa5d-123">Teams がアプリをホストしていない</span><span class="sxs-lookup"><span data-stu-id="ffa5d-123">Teams doesn't host your app</span></span>  

<span data-ttu-id="ffa5d-124">Teams アプリは 3 つの主要な部分で構成されています。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-124">A Teams app consists of three major pieces:</span></span>

1. <span data-ttu-id="ffa5d-125">ユーザーがアプリと対話する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-125">The Microsoft Teams client (web, desktop, or mobile) where users interact with your app.</span></span>
1. <span data-ttu-id="ffa5d-126">アプリ、サービス、ワークフロー、または web サイトで、必要なロジック、データストレージ、および API 呼び出しを実行してアプリの電源を入れます。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-126">Your app, service, workflow, or website that performs the necessary logic, data storage, and API calls to power your app.</span></span>
1. <span data-ttu-id="ffa5d-127">アプリパッケージ。 Teams にアプリをインストールするために使用します。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-127">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="ffa5d-128">このファイルには、アプリのメタデータ (名前、アイコンなど) と、サービスへのポインターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-128">It contains app metadata (name, icons, etc.) and pointers to your services.</span></span>

## <a name="next-step"></a><span data-ttu-id="ffa5d-129">次の手順</span><span class="sxs-lookup"><span data-stu-id="ffa5d-129">Next step</span></span>

<span data-ttu-id="ffa5d-130">これですべてが始まったので、始めましょう。</span><span class="sxs-lookup"><span data-stu-id="ffa5d-130">That's all for now, let's get started!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ffa5d-131">最初のアプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="ffa5d-131">Build and run your first app</span></span>](build-and-run-with-toolkit.md)
