---
title: アプリの概要をテストする
description: Teamsカスタム アプリをテストするプロセスMicrosoft 365
ms.topic: how-to
localization_priority: Normal
keywords: テスト アプリMicrosoft 365アップロードTeamsテナントを構成する
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565187"
---
# <a name="test-your-app"></a><span data-ttu-id="09c3d-104">アプリのテスト</span><span class="sxs-lookup"><span data-stu-id="09c3d-104">Test your app</span></span>

<span data-ttu-id="09c3d-105">アプリをMicrosoft Teamsに統合したら、アプリを公開する前にテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="09c3d-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="09c3d-106">最終的な目標は、アプリのユーザー数をできるだけ多く取得し、ユーザーが使用できる複数のデバイスでアプリをテストすることです。</span><span class="sxs-lookup"><span data-stu-id="09c3d-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="09c3d-107">アプリのテスト:</span><span class="sxs-lookup"><span data-stu-id="09c3d-107">For testing your app:</span></span>

* <span data-ttu-id="09c3d-108">Microsoft 365テナントを準備します。</span><span class="sxs-lookup"><span data-stu-id="09c3d-108">Prepare your Microsoft 365 tenant.</span></span>
* <span data-ttu-id="09c3d-109">アプリをテストおよびデバッグするワークスペースを選択します。</span><span class="sxs-lookup"><span data-stu-id="09c3d-109">Choose a workspace to test and debug your app.</span></span>
* <span data-ttu-id="09c3d-110">Microsoft 365テナントにテスト データを追加します。</span><span class="sxs-lookup"><span data-stu-id="09c3d-110">Add test data to your Microsoft 365 tenant.</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="09c3d-111">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="09c3d-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="09c3d-112">アプリのテストを開始する前に、Microsoft 365テスト テナントを準備し、カスタム Teams アプリを有効にすると、アプリをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="09c3d-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="09c3d-113">開発者プログラムMicrosoft 365サインアップし、組織のTeams設定を管理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="09c3d-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="09c3d-114">開発者サブスクリプションを設定し[、Microsoft 365テナントを準備して構成します](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="09c3d-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="09c3d-115">テストとデバッグ</span><span class="sxs-lookup"><span data-stu-id="09c3d-115">Test and debug</span></span>

<span data-ttu-id="09c3d-116">アプリをテストおよびデバッグするには、少なくとも 1 つのワークスペースを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="09c3d-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="09c3d-117">ローカル ホストやクラウドベースのホストなど、テストのセットアップを選択して、アプリをテストおよびデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="09c3d-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="09c3d-118">アプリの読み込みと実行にTeamsアプリをデバッグするためのガイダンスが提供されます。</span><span class="sxs-lookup"><span data-stu-id="09c3d-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="09c3d-119">詳細については、「[設定を選択して、Microsoft Teams アプリを実行する」を](~/concepts/build-and-test/debug.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="09c3d-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="09c3d-120">ボットをローカルでテストします。</span><span class="sxs-lookup"><span data-stu-id="09c3d-120">Test your bot locally.</span></span> <span data-ttu-id="09c3d-121">詳細については、「 IDE を [使用してボットをローカルでデバッグする](~/bots/how-to/debug/locally-with-an-ide.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="09c3d-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="09c3d-122">検査 [ミドルウェア](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) や [適応ツール](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)を使用してボットをデバッグすることもできます。</span><span class="sxs-lookup"><span data-stu-id="09c3d-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="09c3d-123">コンソール ログを表示したり、実行時に html、css、およびネットワーク要求を表示または変更したりするには、JavaScript コードにブレークポイントを追加し、デバッグに関する対話的なアクセスを実行します。</span><span class="sxs-lookup"><span data-stu-id="09c3d-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="09c3d-124">詳細については、「 [Teamsの DevTools タブにアクセスする](~/tabs/how-to/developer-tools.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="09c3d-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="09c3d-125">Microsoft 365テナントにテスト データを追加する</span><span class="sxs-lookup"><span data-stu-id="09c3d-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="09c3d-126">テスト データをテスト テナントに追加Microsoft 365。</span><span class="sxs-lookup"><span data-stu-id="09c3d-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="09c3d-127">詳細については、「テスト[データを Office 365テスト テナントに追加する」](~/concepts/build-and-test/test-data.md)を参照し、テスト データのアップロードを開始する前にすべての前提条件を完了します。</span><span class="sxs-lookup"><span data-stu-id="09c3d-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="09c3d-128">関連項目</span><span class="sxs-lookup"><span data-stu-id="09c3d-128">See also</span></span>

- [<span data-ttu-id="09c3d-129">タブをデバッグする</span><span class="sxs-lookup"><span data-stu-id="09c3d-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
- [<span data-ttu-id="09c3d-130">ボットをデバッグする</span><span class="sxs-lookup"><span data-stu-id="09c3d-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

- [<span data-ttu-id="09c3d-131">RSC 権限のテスト</span><span class="sxs-lookup"><span data-stu-id="09c3d-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="09c3d-132">次の手順</span><span class="sxs-lookup"><span data-stu-id="09c3d-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09c3d-133">Microsoft 365 テナントを準備する</span><span class="sxs-lookup"><span data-stu-id="09c3d-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
