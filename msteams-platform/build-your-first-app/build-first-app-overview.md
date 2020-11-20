---
title: はじめにアプリの概要と前提条件を最初に作成する
author: heath-hamilton
description: Microsoft Teams アプリ開発を開始する方法と、環境をセットアップする方法について説明します。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: e2e73e755c45fa3bff3b6320dfbf0999a575fe99
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346813"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="25108-103">最初の Microsoft Teams アプリの概要を作成する</span><span class="sxs-lookup"><span data-stu-id="25108-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="25108-104">最初の **アプリ** のレッスンを構築するには、基本的な Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="25108-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="25108-105">各チュートリアルでは、一般的なツール、基本概念、および高度な機能について紹介しながら、簡単な現実世界の Teams アプリを構築する方法について順を追って説明します。</span><span class="sxs-lookup"><span data-stu-id="25108-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="25108-106">学習内容</span><span class="sxs-lookup"><span data-stu-id="25108-106">What you'll learn</span></span>

<span data-ttu-id="25108-107">レッスンを修了した後に知っておくべきことについては、次のアイデアを参照してください。</span><span class="sxs-lookup"><span data-stu-id="25108-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="25108-108">**Teams ツールキットを使用** して迅速に作業を開始します。 Visual Studio 用の Microsoft Teams toolkit は、アプリプロジェクトとスキャフォールディングを作成するためのものであり、実行中のアプリを数分で利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="25108-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="25108-109">App **Studio を使用してアプリを構成する**: Teams アプリで使用する機能とサービスを指定します。</span><span class="sxs-lookup"><span data-stu-id="25108-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="25108-110">**アプリの対象ユーザーの範囲** を作成します。個人利用、グループ作業、またはその両方用の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="25108-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="25108-111">Teams の **ツールと sdk を使用** して、Teams の JavaScript SDK のヘルプを使用してアプリをカスタマイズします (たとえば、その配色を teams のテーマに合わせて変更するなど)。</span><span class="sxs-lookup"><span data-stu-id="25108-111">**Get experience with Teams tools and SDKs**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="25108-112">また、ボットを作成および管理するための一般的なツールについても説明します。</span><span class="sxs-lookup"><span data-stu-id="25108-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="25108-113">**アプリの展開**: レッスン全体を通して、よくある関連トピック (認証やデザインのガイドラインなど) について説明します。</span><span class="sxs-lookup"><span data-stu-id="25108-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="25108-114">Teams アプリの基礎</span><span class="sxs-lookup"><span data-stu-id="25108-114">Teams app fundamentals</span></span>

<span data-ttu-id="25108-115">チュートリアルを開始する前に、Teams 用のアプリの作成に関する以下の情報を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="25108-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="25108-116">アプリには複数の機能とエントリポイントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="25108-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="25108-117">Teams アプリは、1つ以上の [プラットフォーム機能](../concepts/capabilities-overview.md) (アプリを使用する方法) と [エントリポイント](../concepts/extensibility-points.md) (ユーザーがアプリを検出する) で構成されます。</span><span class="sxs-lookup"><span data-stu-id="25108-117">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people discover the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="25108-118">Teams がアプリをホストしていない</span><span class="sxs-lookup"><span data-stu-id="25108-118">Teams doesn't host your app</span></span>

<span data-ttu-id="25108-119">Teams アプリには、次の重要な要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="25108-119">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="25108-120">アプリに電力を供給するロジック、データストレージ、および API 呼び出し。</span><span class="sxs-lookup"><span data-stu-id="25108-120">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="25108-121">これらのサービスは Teams でホストされるものではなく、HTTPS 経由でアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="25108-121">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="25108-122">ユーザーがアプリを使用する Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="25108-122">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="25108-123">アプリ ID は、アプリをアプリ Studio で構成できます。</span><span class="sxs-lookup"><span data-stu-id="25108-123">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="25108-124">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="25108-124">Get prerequisites</span></span>

<span data-ttu-id="25108-125">Teams アプリを作成するための適切なアカウントを持っており、いくつかの推奨される開発ツールをインストールしていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="25108-125">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="25108-126">開発アカウントをセットアップする</span><span class="sxs-lookup"><span data-stu-id="25108-126">Set up your development account</span></span>

<span data-ttu-id="25108-127">カスタムアプリのサイドロードを許可する Teams アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="25108-127">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="25108-128">(アカウントで既に提供されている場合があります。)</span><span class="sxs-lookup"><span data-stu-id="25108-128">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="25108-129">Teams アカウントを所有している場合は、Teams でアプリをサイドロードできるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="25108-129">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="25108-130">Teams クライアントで、[ **アプリ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="25108-130">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="25108-131">**カスタムアプリをアップロード** するオプションを探します。</span><span class="sxs-lookup"><span data-stu-id="25108-131">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタムアプリをアップロードできる場所を示す図":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="25108-133">サイドロードオプションが表示されない場合や、Teams アカウントを持っていない場合は、<b>ここを選択し</b>ます。</span><span class="sxs-lookup"><span data-stu-id="25108-133"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="25108-134">Microsoft 365 開発者プログラムに参加することによって、アプリのサイドロードを許可する無料の Teams テストアカウントを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="25108-134">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="25108-135">(登録プロセスには約2分かかります)。</span><span class="sxs-lookup"><span data-stu-id="25108-135">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="25108-136">[Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program)に移動します。</span><span class="sxs-lookup"><span data-stu-id="25108-136">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="25108-137">[ **今すぐ参加** ] を選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="25108-137">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="25108-138">[ようこそ] 画面が表示されたら、[ **設定] E5 サブスクリプション** を選択します。</span><span class="sxs-lookup"><span data-stu-id="25108-138">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="25108-139">管理者アカウントを設定します。</span><span class="sxs-lookup"><span data-stu-id="25108-139">Set up your administrator account.</span></span> <span data-ttu-id="25108-140">完了すると、次のような画面が表示になります。</span><span class="sxs-lookup"><span data-stu-id="25108-140">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後の表示例。":::
1. <span data-ttu-id="25108-142">設定したのと同じ管理者アカウントを使用して Teams にログインします。</span><span class="sxs-lookup"><span data-stu-id="25108-142">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="25108-143">[ **カスタムアプリをアップロード** する] オプションが選択されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="25108-143">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="25108-144">それでもアプリをサイドロードできない場合は、「 [カスタム Teams アプリを有効にする」および「カスタムアプリのアップロード](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)を有効にする」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25108-144">If you still can't sideload apps, refer to [Enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="25108-145">開発ツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="25108-145">Install your development tools</span></span>

<span data-ttu-id="25108-146">推奨ツールを使用して Teams アプリを構築することはできますが、これらのレッスンでは、Visual Studio Code for the Microsoft Teams Toolkit を使用してすぐに作業を開始する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="25108-146">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="25108-147">Teams では、アプリコンテンツは HTTPS 接続を介してのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="25108-147">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="25108-148">特定の種類のアプリをローカルでデバッグする (bot など) 場合は、ngrok を使用して Teams とアプリの間に [セキュリティで保護されたトンネルを設定](../concepts/build-and-test/debug.md#locally-hosted) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="25108-148">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="25108-149">(運用チームアプリは、クラウドでホストされます。)</span><span class="sxs-lookup"><span data-stu-id="25108-149">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="25108-150">[Node.js](https://nodejs.org/en/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="25108-150">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="25108-151">Bot またはメッセージング拡張機能の構築を計画している場合は、 [ngrok](https://ngrok.com/download) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="25108-151">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="25108-152">[Visual Studio Code](https://code.visualstudio.com/download)の最新バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="25108-152">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="25108-153">(以前のバージョンは、ツールキットでは動作しない可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="25108-153">(Earlier versions might not work with the toolkit.)</span></span>
1. Visual Studio Code で、左側のアクティビティバーにある [ **拡張機能**] を選択 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: し、 **Microsoft Teams Toolkit** をインストールします。

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Visual Studio Code の場所を示す図は、Microsoft Teams ツールキットの拡張機能をインストールできます。":::

## <a name="about-the-tutorials"></a><span data-ttu-id="25108-156">チュートリアルについて</span><span class="sxs-lookup"><span data-stu-id="25108-156">About the tutorials</span></span>

<span data-ttu-id="25108-157">**最初のアプリ** レッスンを構築する Teams のいずれかで開始できます。</span><span class="sxs-lookup"><span data-stu-id="25108-157">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="25108-158">最初にどこに行くべきかがわからない場合は、初心者フレンドリパスに従って "Hello, World!" を作成します。</span><span class="sxs-lookup"><span data-stu-id="25108-158">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="25108-159">アプリ.</span><span class="sxs-lookup"><span data-stu-id="25108-159">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Teams ' 最初のアプリのチュートリアルを構築するための学習パスを示すスキルツリー。" border="false":::

## <a name="next-step"></a><span data-ttu-id="25108-161">次の手順</span><span class="sxs-lookup"><span data-stu-id="25108-161">Next step</span></span>

<span data-ttu-id="25108-162">アカウントと環境をセットアップしたら、構築を開始できます。</span><span class="sxs-lookup"><span data-stu-id="25108-162">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="25108-163">初心者フレンドリなチュートリアル</span><span class="sxs-lookup"><span data-stu-id="25108-163">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="25108-164">"Hello, World!" アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="25108-164">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="25108-165">その他のチュートリアル</span><span class="sxs-lookup"><span data-stu-id="25108-165">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="25108-166">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="25108-166">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="25108-167">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="25108-167">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
