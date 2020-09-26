---
title: 最初の Teams アプリの作成を始める
author: heath-hamilton
description: 最初の Microsoft Teams アプリを構築するための概要と前提条件
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 7431230487f1644de8b17b0b9e143819395b7527
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279707"
---
# <a name="build-your-first-teams-app-overview"></a><span data-ttu-id="81f99-103">最初の Teams アプリの概要を作成する</span><span class="sxs-lookup"><span data-stu-id="81f99-103">Build your first Teams app overview</span></span>

<span data-ttu-id="81f99-104">最初の **アプリ** のレッスンを構築するには、基本的な Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="81f99-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="81f99-105">各チュートリアルでは、一般的なツール、基本概念、および高度な機能について紹介しながら、簡単な現実世界の Teams アプリを構築する方法について順を追って説明します。</span><span class="sxs-lookup"><span data-stu-id="81f99-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="81f99-106">学習内容</span><span class="sxs-lookup"><span data-stu-id="81f99-106">What you'll learn</span></span>

<span data-ttu-id="81f99-107">レッスンを修了した後に知っておくべきことについては、次のアイデアを参照してください。</span><span class="sxs-lookup"><span data-stu-id="81f99-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="81f99-108">**Teams ツールキットを使用**して迅速に作業を開始します。 Visual Studio 用の Microsoft Teams toolkit は、アプリプロジェクトとスキャフォールディングを作成するためのものであり、実行中のアプリを数分で利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="81f99-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="81f99-109">**マニフェストを使用**してアプリを定義します。アプリマニフェストは、Teams アプリが使用する機能とサービスを指定する場所です。</span><span class="sxs-lookup"><span data-stu-id="81f99-109">**Define your app with the manifest**: The app manifest is where you specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="81f99-110">**アプリの対象ユーザーの範囲**を作成します。個人利用、グループ作業、またはその両方用の Teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="81f99-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="81f99-111">Teams**フレームワークを使用**して作業を開始します。アプリをカスタマイズする (たとえば、チームのテーマに合わせて配色を変更するなど)、TEAMS JavaScript SDK のヘルプを参照してください。</span><span class="sxs-lookup"><span data-stu-id="81f99-111">**Get experience with Teams frameworks**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="81f99-112">また、ボットを作成および管理するための一般的なツールについても説明します。</span><span class="sxs-lookup"><span data-stu-id="81f99-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="81f99-113">**アプリの展開**: レッスン全体を通して、よくある関連トピック (認証やデザインのガイドラインなど) について説明します。</span><span class="sxs-lookup"><span data-stu-id="81f99-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="81f99-114">Teams アプリの基礎</span><span class="sxs-lookup"><span data-stu-id="81f99-114">Teams app fundamentals</span></span>

<span data-ttu-id="81f99-115">チュートリアルを開始する前に、Teams 用のアプリの作成に関する以下の情報を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="81f99-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="81f99-116">アプリには複数の機能とエントリポイントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="81f99-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="81f99-117">Teams アプリは、1つ以上の [プラットフォーム機能](../concepts/capabilities-overview.md) と [エントリポイント](../concepts/extensibility-points.md)で構成されます。</span><span class="sxs-lookup"><span data-stu-id="81f99-117">Teams apps are made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="81f99-118">さまざまなチーム固有の [UI コンポーネントと](../concepts/extensibility-points.md#ui-components)、カードやタスクモジュールなどの規則を使用して、アプリを提示することができます。</span><span class="sxs-lookup"><span data-stu-id="81f99-118">You can present your app using a number of Teams-specific [UI components and conventions](../concepts/extensibility-points.md#ui-components), such as cards and task modules.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="81f99-119">Teams がアプリをホストしていない</span><span class="sxs-lookup"><span data-stu-id="81f99-119">Teams doesn't host your app</span></span>

<span data-ttu-id="81f99-120">Teams アプリには、次の3つの重要な要素があります。</span><span class="sxs-lookup"><span data-stu-id="81f99-120">A Teams app includes three important pieces:</span></span>

* <span data-ttu-id="81f99-121">アプリに電力を供給するロジック、データストレージ、および API 呼び出し。</span><span class="sxs-lookup"><span data-stu-id="81f99-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="81f99-122">これらのサービスは Teams でホストされるものではなく、HTTPS 経由でアクセスできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="81f99-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="81f99-123">ユーザーがアプリを使用する Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="81f99-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="81f99-124">アプリパッケージ。 Teams にアプリをインストールするために使用します。</span><span class="sxs-lookup"><span data-stu-id="81f99-124">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="81f99-125">このファイルには、ホストされているサービスへのアプリケーションメタデータとポインターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="81f99-125">It contains app metadata and pointers to your hosted services.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="81f99-126">前提条件を取得する</span><span class="sxs-lookup"><span data-stu-id="81f99-126">Get prerequisites</span></span>

<span data-ttu-id="81f99-127">Teams アプリを作成するための適切なアカウントを持っており、いくつかの推奨される開発ツールをインストールしていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="81f99-127">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="81f99-128">開発アカウントをセットアップする</span><span class="sxs-lookup"><span data-stu-id="81f99-128">Set up your development account</span></span>

<span data-ttu-id="81f99-129">カスタムアプリのサイドロードを許可する Teams アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="81f99-129">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="81f99-130">(アカウントで既に提供されている場合があります。)</span><span class="sxs-lookup"><span data-stu-id="81f99-130">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="81f99-131">Teams アカウントを所有している場合は、Teams でアプリをサイドロードできるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="81f99-131">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="81f99-132">Teams クライアントで、[ **アプリ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="81f99-132">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="81f99-133">**カスタムアプリをアップロード**するオプションを探します。</span><span class="sxs-lookup"><span data-stu-id="81f99-133">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタムアプリをアップロードできる場所を示す図":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="81f99-135">サイドロードオプションが表示されない場合や、Teams アカウントを持っていない場合は、<b>ここを選択し</b>ます。</span><span class="sxs-lookup"><span data-stu-id="81f99-135"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="81f99-136">Microsoft 365 開発者プログラムに参加することによって、アプリのサイドロードを許可する無料の Teams テストアカウントを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="81f99-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="81f99-137">(登録プロセスには約2分かかります)。</span><span class="sxs-lookup"><span data-stu-id="81f99-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="81f99-138">[Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program)に移動します。</span><span class="sxs-lookup"><span data-stu-id="81f99-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="81f99-139">[ **今すぐ参加** ] を選択し、画面の指示に従います。</span><span class="sxs-lookup"><span data-stu-id="81f99-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="81f99-140">[ようこそ] 画面が表示されたら、[ **設定] E5 サブスクリプション**を選択します。</span><span class="sxs-lookup"><span data-stu-id="81f99-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="81f99-141">管理者アカウントを設定します。</span><span class="sxs-lookup"><span data-stu-id="81f99-141">Set up your administrator account.</span></span> <span data-ttu-id="81f99-142">完了すると、次のような画面が表示になります。</span><span class="sxs-lookup"><span data-stu-id="81f99-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後の表示例。":::
1. <span data-ttu-id="81f99-144">設定したのと同じ管理者アカウントを使用して Teams にログインします。</span><span class="sxs-lookup"><span data-stu-id="81f99-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="81f99-145">[ **カスタムアプリをアップロード** する] オプションが選択されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="81f99-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

### <a name="install-your-development-tools"></a><span data-ttu-id="81f99-146">開発ツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="81f99-146">Install your development tools</span></span>

<span data-ttu-id="81f99-147">推奨ツールを使用して Teams アプリを構築することはできますが、これらのレッスンでは、Visual Studio Code for the Microsoft Teams Toolkit を使用してすぐに作業を開始する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="81f99-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="81f99-148">Teams では、アプリコンテンツは HTTPS 接続を介してのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="81f99-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="81f99-149">最初のアプリをローカルにホストして時間を節約するので、ngrok を使用して Teams とアプリの間に [セキュリティで保護されたトンネルを設定](../concepts/build-and-test/debug.md#locally-hosted) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="81f99-149">Since you'll host your first app locally to save time, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="81f99-150">(運用レベルの Teams アプリは、クラウドでホストされます。)</span><span class="sxs-lookup"><span data-stu-id="81f99-150">(Production-level Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="81f99-151">[Node.js](https://nodejs.org/en/) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="81f99-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="81f99-152">[Ngrok](https://ngrok.com/download)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="81f99-152">Install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="81f99-153">[Visual Studio Code](https://code.visualstudio.com/download)の最新バージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="81f99-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="81f99-154">(以前のバージョンは、ツールキットでは動作しない可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="81f99-154">(Earlier versions might not work with the toolkit.)</span></span>
1. Visual Studio Code で、左側のアクティビティバーにある [ **拡張機能**] を選択 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: し、 **Microsoft Teams Toolkit**をインストールします。
    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Visual Studio Code の場所を示す図は、Microsoft Teams ツールキットの拡張機能をインストールできます。":::

## <a name="about-the-tutorials"></a><span data-ttu-id="81f99-157">チュートリアルについて</span><span class="sxs-lookup"><span data-stu-id="81f99-157">About the tutorials</span></span>

<span data-ttu-id="81f99-158">**最初のアプリ**レッスンを構築する Teams のいずれかで開始できます。</span><span class="sxs-lookup"><span data-stu-id="81f99-158">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="81f99-159">最初にどこに行くべきかがわからない場合は、初心者フレンドリパスに従って "Hello, World!" を作成します。</span><span class="sxs-lookup"><span data-stu-id="81f99-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="81f99-160">アプリ.</span><span class="sxs-lookup"><span data-stu-id="81f99-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Teams ' 最初のアプリのチュートリアルを構築するための学習パスを示すスキルツリー。" border="false":::

## <a name="next-step"></a><span data-ttu-id="81f99-162">次の手順</span><span class="sxs-lookup"><span data-stu-id="81f99-162">Next step</span></span>

<span data-ttu-id="81f99-163">アカウントと環境をセットアップしたら、構築を開始できます。</span><span class="sxs-lookup"><span data-stu-id="81f99-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="81f99-164">初心者フレンドリなチュートリアル</span><span class="sxs-lookup"><span data-stu-id="81f99-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81f99-165">"Hello, World!" アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="81f99-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="81f99-166">その他のチュートリアル</span><span class="sxs-lookup"><span data-stu-id="81f99-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81f99-167">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="81f99-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="81f99-168">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="81f99-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)