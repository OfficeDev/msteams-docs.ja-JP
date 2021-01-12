---
title: 概要 - 最初のアプリの概要と前提条件を構築する
author: heath-hamilton
description: Microsoft Teams アプリの開発を開始し、環境をセットアップする方法について説明します。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 06e26c57e6f6d3fd0bbeb981ef7ab46c8217bb4a
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795462"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="d3e1e-103">最初の Microsoft Teams アプリの概要を作成する</span><span class="sxs-lookup"><span data-stu-id="d3e1e-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="d3e1e-104">最初の **アプリのレッスンを構築する** 場合は、基本的な Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="d3e1e-105">各チュートリアルでは、一般的なツール、基本的な概念、より高度な機能を紹介しながら、シンプルで実際の Teams アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d3e1e-106">学習する情報</span><span class="sxs-lookup"><span data-stu-id="d3e1e-106">What you'll learn</span></span>

<span data-ttu-id="d3e1e-107">ここでは、レッスンを行った後に知っている情報を示します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="d3e1e-108">**Teams Toolkit**: Microsoft Teams Toolkit for Visual Studio Code を使用すると、すぐにアプリ プロジェクトを作成し、スキャフォールディングを行い、数分で実行中のアプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="d3e1e-109">**App Studio でアプリを構成** する: Teams アプリで使用する機能とサービスを指定します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="d3e1e-110">**アプリの対象ユーザーの範囲を設定** する : 個人使用、コラボレーション、または両方の Teams アプリを構築します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
> * <span data-ttu-id="d3e1e-111">**Teams ツールと SDK のエクスペリエンスを得** る : Teams JavaScript クライアント SDK のヘルプを利用してアプリをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-111">**Get experience with Teams tools and SDKs**: Customize your app with help from the Teams JavaScript client SDK.</span></span> <span data-ttu-id="d3e1e-112">たとえば、Teams のテーマに合わせてアプリの配色を変更します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-112">For example, change your app's color scheme to match the Teams theme.</span></span> <span data-ttu-id="d3e1e-113">また、ボットを作成および管理するための一般的なツールについて学習します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-113">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="d3e1e-114">**アプリを展開** する: 授業全体を通じて、関心のある関連トピック (認証や設計ガイドラインなど) を確認できます。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-114">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="d3e1e-115">Teams アプリの基本</span><span class="sxs-lookup"><span data-stu-id="d3e1e-115">Teams app fundamentals</span></span>

<span data-ttu-id="d3e1e-116">チュートリアルを開始する前に、Teams 用アプリの構築に関する以下の情報を知っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-116">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="d3e1e-117">アプリは複数の機能とエントリ ポイントを持つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-117">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="d3e1e-118">Teams アプリは、1 つ以上のプラットフォーム機能 [(ユーザー](../concepts/capabilities-overview.md) がアプリを使用する方法) とエントリ ポイント [(ユーザー](../concepts/extensibility-points.md) がアプリを検出する場所) で構成されます。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-118">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people discover the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="d3e1e-119">Teams がアプリをホストしない</span><span class="sxs-lookup"><span data-stu-id="d3e1e-119">Teams doesn't host your app</span></span>

<span data-ttu-id="d3e1e-120">Teams アプリには、次の重要な部分が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-120">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="d3e1e-121">アプリを起動するロジック、データ ストレージ、API 呼び出し。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="d3e1e-122">これらのサービスは Teams によってホストされていないので、HTTPS 経由でアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="d3e1e-123">ユーザーがアプリを使用する Teams クライアント (Web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="d3e1e-124">App Studio でアプリを構成できるアプリ ID。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-124">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="d3e1e-125">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="d3e1e-125">Get prerequisites</span></span>

<span data-ttu-id="d3e1e-126">Teams アプリを構築するための適切なアカウントを持ち、推奨される開発ツールをインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-126">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="d3e1e-127">開発アカウントをセットアップする</span><span class="sxs-lookup"><span data-stu-id="d3e1e-127">Set up your development account</span></span>

<span data-ttu-id="d3e1e-128">カスタム アプリのサイドローディングを許可する Teams アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-128">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="d3e1e-129">(お客様のアカウントで既に提供されている場合があります。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-129">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="d3e1e-130">Teams アカウントを持っている場合は、Teams でアプリをサイドロードできる場合は、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-130">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="d3e1e-131">Teams クライアントで、[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-131">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="d3e1e-132">カスタム アプリをアップロード **するオプションを探します**。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-132">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams 内でカスタム アプリをアップロードできる場所を示す図。":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="d3e1e-134"><b>サイドロード</b> オプションが表示できない場合、または Teams アカウントを持たなかった場合は、ここで選択します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-134"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="d3e1e-135">Microsoft 365 開発者プログラムに参加することで、アプリのサイドローディングを許可する無料の Teams テスト アカウントを取得できます。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-135">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="d3e1e-136">(登録プロセスには約 2 分かかります)。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-136">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="d3e1e-137">[Microsoft 365 開発者プログラムに移動します](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-137">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="d3e1e-138">[ **今すぐ参加] を** 選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-138">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="d3e1e-139">ようこそ画面にアクセスし、[E5 サブスクリプションのセットアップ **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-139">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="d3e1e-140">管理者アカウントを設定します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-140">Set up your administrator account.</span></span> <span data-ttu-id="d3e1e-141">完了すると、次のような画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-141">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後に表示される例。":::
1. <span data-ttu-id="d3e1e-143">セットアップした管理者アカウントを使用して Teams にログインします。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-143">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="d3e1e-144">[カスタム アプリのアップロード] **オプションが表示されたのか確認** します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-144">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="d3e1e-145">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span><span class="sxs-lookup"><span data-stu-id="d3e1e-145">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="d3e1e-146">開発ツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="d3e1e-146">Install your development tools</span></span>

<span data-ttu-id="d3e1e-147">Teams アプリは好みのツールで構築できますが、これらのレッスンでは、Microsoft Teams Toolkit for Visual Studio Code を使用してすぐに開始する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="d3e1e-148">Teams は、HTTPS 接続を通じてのみアプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="d3e1e-149">ボットなど、特定の種類のアプリをローカルでデバッグするには [、ngrok](../concepts/build-and-test/debug.md#locally-hosted) を使用して Teams とアプリの間のセキュリティで保護されたトンネルを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-149">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="d3e1e-150">(Production Teams アプリはクラウドでホストされます。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-150">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="d3e1e-151">[Node.js](https://nodejs.org/en/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="d3e1e-152">ボット [またはメッセージング拡張機能を](https://ngrok.com/download) 構築する予定の場合は、ngrok をインストールします。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-152">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="d3e1e-153">最新バージョンの Visual Studio [Code をインストールします](https://code.visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="d3e1e-154">(以前のバージョンでは、このツールキットでは動作しない可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-154">(Earlier versions might not work with the toolkit.)</span></span>
1. [Visual Studioコード] で、左側のアクティビティ バーの [拡張機能] を選択し :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: **、Microsoft Teams** Toolkit。

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="コード内で Microsoft Teams Visual Studio拡張機能をインストールできる場所を示Toolkit図。":::

## <a name="about-the-tutorials"></a><span data-ttu-id="d3e1e-157">チュートリアルについて</span><span class="sxs-lookup"><span data-stu-id="d3e1e-157">About the tutorials</span></span>

<span data-ttu-id="d3e1e-158">どの Teams でも、最初のアプリの **レッスンを構築できます** 。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-158">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="d3e1e-159">最初の場所が不明な場合は、初心者向けのパスに従って"Hello, World!" を構築します。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="d3e1e-160">app.</span><span class="sxs-lookup"><span data-stu-id="d3e1e-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Teams の「最初のアプリを構築する」チュートリアルのラーニング パスを示すスキル ツリー。" border="false":::

## <a name="next-step"></a><span data-ttu-id="d3e1e-162">次の手順</span><span class="sxs-lookup"><span data-stu-id="d3e1e-162">Next step</span></span>

<span data-ttu-id="d3e1e-163">アカウントと環境を設定したら、構築を開始できます。</span><span class="sxs-lookup"><span data-stu-id="d3e1e-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="d3e1e-164">初心者向けのチュートリアル</span><span class="sxs-lookup"><span data-stu-id="d3e1e-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3e1e-165">"Hello, World!" アプリを構築する</span><span class="sxs-lookup"><span data-stu-id="d3e1e-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="d3e1e-166">その他のチュートリアル</span><span class="sxs-lookup"><span data-stu-id="d3e1e-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3e1e-167">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="d3e1e-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="d3e1e-168">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="d3e1e-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
