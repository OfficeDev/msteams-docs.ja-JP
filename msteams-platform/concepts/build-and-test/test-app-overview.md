---
title: アプリの概要をテストする
description: Microsoft 365 で Teams カスタム アプリをテストするプロセスについて説明します。
ms.topic: how-to
keywords: テスト アプリをアップロードする Microsoft 365 テナント Teams を構成する
ms.openlocfilehash: b199ca4be31b546364091b754cdb890c8c0dd7d0
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634780"
---
# <a name="test-your-app"></a><span data-ttu-id="9049a-104">アプリのテスト</span><span class="sxs-lookup"><span data-stu-id="9049a-104">Test your app</span></span>

<span data-ttu-id="9049a-105">アプリを Microsoft Teams と統合した後、アプリを発行する前にテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9049a-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="9049a-106">最終的な目標は、アプリのユーザー数を多く取得し、ユーザーが使用できる複数のデバイスでアプリをテストする方法です。</span><span class="sxs-lookup"><span data-stu-id="9049a-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="9049a-107">アプリをテストする場合:</span><span class="sxs-lookup"><span data-stu-id="9049a-107">For testing your app:</span></span>

* <span data-ttu-id="9049a-108">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="9049a-108">Prepare your Microsoft 365 tenant</span></span>
* <span data-ttu-id="9049a-109">アプリをテストおよびデバッグするワークスペースを選択する</span><span class="sxs-lookup"><span data-stu-id="9049a-109">Choose a workspace to test and debug your app</span></span>
* <span data-ttu-id="9049a-110">テスト データを Microsoft 365 テナントに追加する</span><span class="sxs-lookup"><span data-stu-id="9049a-110">Add test data to your Microsoft 365 tenant</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="9049a-111">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="9049a-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="9049a-112">アプリのテストを開始する前に、Microsoft 365 テスト テナントを準備し、カスタム Teams アプリを有効にしてアプリをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="9049a-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="9049a-113">Microsoft 365 開発者プログラムにサインアップし、組織の Teams 設定を管理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9049a-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="9049a-114">開発者サブスクリプションをセットアップし [、Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)テナントを準備して構成します。</span><span class="sxs-lookup"><span data-stu-id="9049a-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="9049a-115">テストとデバッグ</span><span class="sxs-lookup"><span data-stu-id="9049a-115">Test and debug</span></span>

<span data-ttu-id="9049a-116">アプリをテストおよびデバッグするには、少なくとも 1 つのワークスペースを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9049a-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="9049a-117">アプリをテストおよびデバッグするために、ローカル ホストやクラウドベースのホストなどのテストセットアップを選択できます。</span><span class="sxs-lookup"><span data-stu-id="9049a-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="9049a-118">Teams アプリをデバッグするガイダンスは、アプリ エクスペリエンスを読み込み、実行するために提供されます。</span><span class="sxs-lookup"><span data-stu-id="9049a-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="9049a-119">詳細については、「セットアップを [選択して Microsoft Teams アプリを実行する」を参照してください](~/concepts/build-and-test/debug.md)。</span><span class="sxs-lookup"><span data-stu-id="9049a-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="9049a-120">ボットをローカルでテストします。</span><span class="sxs-lookup"><span data-stu-id="9049a-120">Test your bot locally.</span></span> <span data-ttu-id="9049a-121">詳細については [、「IDE を使用してボットをローカルでデバッグする」を参照してください](~/bots/how-to/debug/locally-with-an-ide.md)。</span><span class="sxs-lookup"><span data-stu-id="9049a-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="9049a-122">検査ミドルウェアとアダプティブ ツールを使用 [してボット](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) を [デバッグすることもできます](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="9049a-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="9049a-123">コンソール ログを表示したり、実行時に html、css、およびネットワーク要求を表示または変更したりするには、JavaScript コードにブレークポイントを追加し、DevTools への対話的なデバッグ アクセスを実行します。</span><span class="sxs-lookup"><span data-stu-id="9049a-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="9049a-124">詳細については [、「Access the DevTools for Teams」タブを参照してください](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="9049a-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="9049a-125">テスト データを Microsoft 365 テナントに追加する</span><span class="sxs-lookup"><span data-stu-id="9049a-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="9049a-126">テスト データを Microsoft 365 テスト テナントに追加します。</span><span class="sxs-lookup"><span data-stu-id="9049a-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="9049a-127">詳細については、「テスト データを Office [365](~/concepts/build-and-test/test-data.md)テスト テナントに追加し、テスト データのアップロードを開始する前に、すべての前提条件を完了する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9049a-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="9049a-128">関連項目</span><span class="sxs-lookup"><span data-stu-id="9049a-128">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9049a-129">タブをデバッグする</span><span class="sxs-lookup"><span data-stu-id="9049a-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="9049a-130">ボットのデバッグ</span><span class="sxs-lookup"><span data-stu-id="9049a-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="9049a-131">RSC のアクセス許可をテストする</span><span class="sxs-lookup"><span data-stu-id="9049a-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="9049a-132">次の手順</span><span class="sxs-lookup"><span data-stu-id="9049a-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9049a-133">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="9049a-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
