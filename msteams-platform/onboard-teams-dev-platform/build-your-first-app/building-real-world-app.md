---
title: 初めて Teams アプリの作成を始める
author: heath-hamilton
ms.author: lajanuar
description: 最初の Microsoft Teams アプリを作成するための概要と前提条件
ms.openlocfilehash: 9392096a285a43d3a1f8bed5020e3464da0f7f18
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964702"
---
# <a name="get-started-building-your-first-teams-app"></a><span data-ttu-id="c63fc-103">初めて Teams アプリの作成を始める</span><span class="sxs-lookup"><span data-stu-id="c63fc-103">Get started building your first Teams app</span></span>

<span data-ttu-id="c63fc-104">最初の **アプリ** のレッスンを構築するには、基本的な Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="c63fc-105">各チュートリアルでは、シンプルで実際の Teams アプリを構築する方法を説明しながら、一般的なツール、基本概念、およびその他の高度な機能を紹介します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and some more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c63fc-106">学習内容</span><span class="sxs-lookup"><span data-stu-id="c63fc-106">What you'll learn</span></span>

<span data-ttu-id="c63fc-107">レッスンを修了した後に知っておくべきことについては、次のアイデアを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c63fc-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="c63fc-108">**Teams ツールキットを使用**して迅速に作業を開始します。 Visual Studio 用の Microsoft Teams toolkit は、アプリプロジェクトとスキャフォールディングを作成するためのものであり、実行中のアプリを数分で利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="c63fc-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="c63fc-109">**マニフェストを使用**してアプリを定義します。アプリマニフェストは、Teams アプリが使用する機能とサービスを指定する場所です。</span><span class="sxs-lookup"><span data-stu-id="c63fc-109">**Define your app with the manifest**: The app manifest is where you specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="c63fc-110">**アプリの対象ユーザーの範囲**を作成します。個人利用、グループ作業、またはその両方用の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="c63fc-111">**フレームワークの使用**状況を把握する: アプリをカスタマイズします (たとえば、チームのテーマに合わせて配色を変更するなど)。 Teams の JavaScript SDK のヘルプを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c63fc-111">**Get experience with frameworks**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="c63fc-112">また、ボットを作成および管理するための一般的なツールについても説明します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="c63fc-113">**アプリの展開**: レッスン全体を通して、よくある関連トピック (認証やデザインのガイドラインなど) について説明します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="c63fc-114">Teams アプリの基礎</span><span class="sxs-lookup"><span data-stu-id="c63fc-114">Teams app fundamentals</span></span>

<span data-ttu-id="c63fc-115">チュートリアルを開始する前に、Teams 用のアプリの作成に関する以下の情報を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c63fc-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities"></a><span data-ttu-id="c63fc-116">アプリは複数の機能を持つことができる</span><span class="sxs-lookup"><span data-stu-id="c63fc-116">Apps can have multiple capabilities</span></span>

<span data-ttu-id="c63fc-117">Teams アプリは、1つ以上の [プラットフォーム機能](../capabilities-overview.md)で構成されています。</span><span class="sxs-lookup"><span data-stu-id="c63fc-117">Teams apps are made up of one or more [platform capabilities](../capabilities-overview.md).</span></span> <span data-ttu-id="c63fc-118">これらの機能は、さまざまなチーム固有の [UI コンポーネントと](../doc-links/teams-ui-conventions.md)、カードやタスクモジュールなどの規則を使用して表示できます。</span><span class="sxs-lookup"><span data-stu-id="c63fc-118">You can display these capabilities using a number of Teams-specific [UI components and conventions](../doc-links/teams-ui-conventions.md), such as cards and task modules.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="c63fc-119">Teams がアプリをホストしていない</span><span class="sxs-lookup"><span data-stu-id="c63fc-119">Teams doesn't host your app</span></span>

<span data-ttu-id="c63fc-120">Teams アプリには、次の3つの重要な要素があります。</span><span class="sxs-lookup"><span data-stu-id="c63fc-120">A Teams app includes three important pieces:</span></span>

* <span data-ttu-id="c63fc-121">アプリに電力を供給するロジック、データストレージ、および API 呼び出し。</span><span class="sxs-lookup"><span data-stu-id="c63fc-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="c63fc-122">これらのサービスは Teams でホストされるものではなく、HTTPS 経由でアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="c63fc-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="c63fc-123">ユーザーがアプリを使用する Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="c63fc-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="c63fc-124">アプリパッケージ。 Teams にアプリをインストールするために使用します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-124">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="c63fc-125">このファイルには、ホストされているサービスへのアプリケーションメタデータとポインターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c63fc-125">It contains app metadata and pointers to your hosted services.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="c63fc-126">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="c63fc-126">Get prerequisites</span></span>

<span data-ttu-id="c63fc-127">Teams アプリを作成するための適切なアカウントを持っており、いくつかの推奨される開発ツールをインストールしていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-127">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="c63fc-128">開発アカウントをセットアップする</span><span class="sxs-lookup"><span data-stu-id="c63fc-128">Set up your development account</span></span>

<span data-ttu-id="c63fc-129">カスタムアプリのサイドロードを許可する Teams アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="c63fc-129">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="c63fc-130">(アカウントで既に提供されている場合があります。)</span><span class="sxs-lookup"><span data-stu-id="c63fc-130">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="c63fc-131">Teams アカウントを所有している場合は、Teams でアプリをサイドロードできるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-131">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="c63fc-132">Teams クライアントで、[ **アプリ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-132">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="c63fc-133">**カスタムアプリをアップロード**するオプションを探します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-133">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../doc-links/images/upload-custom-app-closeup.png" alt-text="サイドロードオプションビュー":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="c63fc-135">サイドロードオプションが表示されない場合や、Teams アカウントを持っていない場合は、<b>ここを選択し</b>ます。</span><span class="sxs-lookup"><span data-stu-id="c63fc-135"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="c63fc-136">Microsoft 365 開発者プログラムに参加することによって、アプリのサイドロードを許可する無料の Teams テストアカウントを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="c63fc-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="c63fc-137">(登録プロセスには約2分かかります)。</span><span class="sxs-lookup"><span data-stu-id="c63fc-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="c63fc-138">[Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program)に移動します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="c63fc-139">[ **今すぐ参加** ] を選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="c63fc-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="c63fc-140">[ようこそ] 画面が表示されたら、[ **設定] E5 サブスクリプション**を選択します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="c63fc-141">管理者アカウントを設定します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-141">Set up your administrator account.</span></span> <span data-ttu-id="c63fc-142">完了すると、次のような画面が表示になります。</span><span class="sxs-lookup"><span data-stu-id="c63fc-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../doc-links/images/dev-program-subscription.png" alt-text="開発プログラムのサブスクリプションビュー":::
1. <span data-ttu-id="c63fc-144">設定したのと同じ管理者アカウントを使用して Teams にログインします。</span><span class="sxs-lookup"><span data-stu-id="c63fc-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="c63fc-145">[ **カスタムアプリをアップロード** する] オプションが選択されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

### <a name="install-your-development-tools"></a><span data-ttu-id="c63fc-146">開発ツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="c63fc-146">Install your development tools</span></span>

<span data-ttu-id="c63fc-147">推奨ツールを使用して Teams アプリを構築することはできますが、これらのレッスンでは、Visual Studio Code for the Microsoft Teams Toolkit を使用してすぐに作業を開始する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="c63fc-148">Teams では、アプリコンテンツは HTTPS 接続を介してのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="c63fc-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="c63fc-149">最初のアプリをローカルでホストすることになるため、ngrok を使用して Teams とアプリの間に [セキュリティで保護されたトンネルを設定](../doc-links/debug.md#locally-hosted) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c63fc-149">Since you'll host your first app locally, you'll learn how to use [ngrok to set up a secure tunnel](../doc-links/debug.md#locally-hosted) between Teams and your app.</span></span>

1. <span data-ttu-id="c63fc-150">[Node.js](https://nodejs.org/en/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c63fc-150">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="c63fc-151">[Visual Studio Code](https://code.visualstudio.com/download)の最新バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="c63fc-151">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="c63fc-152">(以前のバージョンは、ツールキットでは動作しない可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="c63fc-152">(Earlier versions might not work with the toolkit.)</span></span>
1. Visual Studio Code で、左側のアクティビティバーにある [ **拡張機能**] を選択 :::image type="icon" source="../doc-links/images/vs-code-extensions.png"::: し、 **Microsoft Teams Toolkit**をインストールします。
    :::image type="content" source="../doc-links/images/vsc-install-toolkit.png" alt-text="ツールキットビューをインストールする":::
1. <span data-ttu-id="c63fc-155">[Ngrok](https://ngrok.com/download)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c63fc-155">Install [ngrok](https://ngrok.com/download).</span></span>

## <a name="next-step"></a><span data-ttu-id="c63fc-156">次の手順</span><span class="sxs-lookup"><span data-stu-id="c63fc-156">Next step</span></span>

<span data-ttu-id="c63fc-157">アカウントと環境をセットアップしたら、構築を開始できます。</span><span class="sxs-lookup"><span data-stu-id="c63fc-157">Once you set up your account and environment, you can start building.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c63fc-158">最初のアプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="c63fc-158">Build and run your first app</span></span>](../build-your-first-app/build-and-run.md)
