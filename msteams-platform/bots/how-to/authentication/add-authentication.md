---
title: Teamsボットに認証を追加する
author: clearab
description: Microsoft Teamsで OAuth 認証をボットに追加する方法。
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 36cb6f3de6f97af1d01512175923b79f69f630ad
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566007"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="c567d-103">Teamsボットに認証を追加する</span><span class="sxs-lookup"><span data-stu-id="c567d-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="c567d-104">メール サービスなど、ユーザーの代わりにリソースにアクセスできるボットをMicrosoft Teamsで作成する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="c567d-105">この記事では、OAuth 2.0 に基づいて Azure Bot サービス v4 SDK 認証を使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="c567d-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="c567d-106">これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットを簡単に開発できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="c567d-107">このすべてのキーは、後で説明する **ID プロバイダーの** 使用です。</span><span class="sxs-lookup"><span data-stu-id="c567d-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="c567d-108">OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。</span><span class="sxs-lookup"><span data-stu-id="c567d-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="c567d-109">OAuth 2.0 の基本知識は、Teamsで認証を操作するための前提条件です。</span><span class="sxs-lookup"><span data-stu-id="c567d-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="c567d-110">基本的な理解については [OAuth 2 の簡略化](https://aka.ms/oauth2-simplified) 、および完全な仕様については [OAuth 2.0](https://oauth.net/2/) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="c567d-111">Azure Bot サービスが認証を処理する方法の詳細については、「 [会話内のユーザー認証](https://aka.ms/azure-bot-authentication)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="c567d-112">この記事では、以下について説明します。</span><span class="sxs-lookup"><span data-stu-id="c567d-112">In this article you'll learn:</span></span>

- <span data-ttu-id="c567d-113">**認証が有効なボットを作成する方法**。</span><span class="sxs-lookup"><span data-stu-id="c567d-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="c567d-114">[cs-auth-sample][teams-auth-bot-cs]を使用して、ユーザーサインイン資格情報と認証トークンの生成を処理します。</span><span class="sxs-lookup"><span data-stu-id="c567d-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="c567d-115">**ボットを Azure にデプロイし、ID プロバイダーに関連付ける方法**。</span><span class="sxs-lookup"><span data-stu-id="c567d-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="c567d-116">プロバイダーは、ユーザーサインイン資格情報に基づいてトークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="c567d-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="c567d-117">ボットは、認証を必要とするメール サービスなどのリソースにアクセスするために、トークンを使用できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="c567d-118">詳細については、「[ボットの認証フロー Microsoft Teams」を](auth-flow-bot.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="c567d-119">**Microsoft Teams内でボットを統合する方法**.</span><span class="sxs-lookup"><span data-stu-id="c567d-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="c567d-120">ボットが統合されたら、ログインしてチャットでメッセージを交換できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c567d-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="c567d-121">Prerequisites</span></span>

- <span data-ttu-id="c567d-122">ボットの [基本][concept-basics]知識 、 [状態の管理][concept-state]、 ダイアログ [ライブラリ][concept-dialogs]、および [シーケンシャルな会話フローの実装][simple-dialog]方法 。</span><span class="sxs-lookup"><span data-stu-id="c567d-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="c567d-123">Azure および OAuth 2.0 開発に関する知識。</span><span class="sxs-lookup"><span data-stu-id="c567d-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="c567d-124">Visual Studioと Git の現在のバージョン。</span><span class="sxs-lookup"><span data-stu-id="c567d-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="c567d-125">Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="c567d-125">Azure account.</span></span> <span data-ttu-id="c567d-126">必要に応じて [、Azure 無料アカウント](https://azure.microsoft.com/free/)を作成できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="c567d-127">次の例を示します。</span><span class="sxs-lookup"><span data-stu-id="c567d-127">The following sample:</span></span>

    | <span data-ttu-id="c567d-128">サンプル</span><span class="sxs-lookup"><span data-stu-id="c567d-128">Sample</span></span> | <span data-ttu-id="c567d-129">ボットビルダーバージョン</span><span class="sxs-lookup"><span data-stu-id="c567d-129">BotBuilder version</span></span> | <span data-ttu-id="c567d-130">示します</span><span class="sxs-lookup"><span data-stu-id="c567d-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="c567d-131">[cs 認証サンプルでの][teams-auth-bot-cs]**ボット認証**</span><span class="sxs-lookup"><span data-stu-id="c567d-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="c567d-132">v4</span><span class="sxs-lookup"><span data-stu-id="c567d-132">v4</span></span> | <span data-ttu-id="c567d-133">OAuthカードのサポート</span><span class="sxs-lookup"><span data-stu-id="c567d-133">OAuthCard support</span></span> |
    | <span data-ttu-id="c567d-134">[js 認証サンプルでの][teams-auth-bot-js]**ボット認証**</span><span class="sxs-lookup"><span data-stu-id="c567d-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="c567d-135">v4</span><span class="sxs-lookup"><span data-stu-id="c567d-135">v4</span></span>| <span data-ttu-id="c567d-136">OAuthカードのサポート</span><span class="sxs-lookup"><span data-stu-id="c567d-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="c567d-137">[py-auth サンプルでの][teams-auth-bot-py]**ボット認証**</span><span class="sxs-lookup"><span data-stu-id="c567d-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="c567d-138">v4</span><span class="sxs-lookup"><span data-stu-id="c567d-138">v4</span></span> | <span data-ttu-id="c567d-139">OAuthカードのサポート</span><span class="sxs-lookup"><span data-stu-id="c567d-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="c567d-140">リソース グループを作成する</span><span class="sxs-lookup"><span data-stu-id="c567d-140">Create the resource group</span></span>

<span data-ttu-id="c567d-141">リソース グループとサービス計画は厳密には必要ありませんが、作成したリソースを簡単に解放できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="c567d-142">これは、リソースを整理して管理しやすい状態に保つには、適切な方法です。</span><span class="sxs-lookup"><span data-stu-id="c567d-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="c567d-143">リソース グループを使用して、Bot Framework の個々のリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="c567d-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="c567d-144">パフォーマンスを確保するには、これらのリソースが同じ Azure リージョンに配置されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="c567d-145">ブラウザーで [**、Azure ポータル**][azure-portal]にサインインします。</span><span class="sxs-lookup"><span data-stu-id="c567d-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="c567d-146">左側のナビゲーション パネルで、[ **リソース グループ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="c567d-147">表示されたウィンドウの左上で、[タブの **追加** ] を選択して新しいリソース グループを作成します。</span><span class="sxs-lookup"><span data-stu-id="c567d-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="c567d-148">次の情報を入力するよう求められます。</span><span class="sxs-lookup"><span data-stu-id="c567d-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="c567d-149">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="c567d-149">**Subscription**.</span></span> <span data-ttu-id="c567d-150">既存のサブスクリプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="c567d-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="c567d-151">**リソース グループ**。</span><span class="sxs-lookup"><span data-stu-id="c567d-151">**Resource group**.</span></span> <span data-ttu-id="c567d-152">リソース グループの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-152">Enter the name for the resource group.</span></span> <span data-ttu-id="c567d-153">たとえば、  *チームリソースグループ* を挙します。</span><span class="sxs-lookup"><span data-stu-id="c567d-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="c567d-154">名前は一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="c567d-155">[ **地域** ] ドロップダウン メニューから、[ *米国西部*] またはアプリケーションに近いリージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="c567d-156">[ **レビューと作成** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-156">Select the **Review and create** button.</span></span> <span data-ttu-id="c567d-157">*検証が渡された* というバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="c567d-158">[ **作成** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-158">Select the **Create** button.</span></span> <span data-ttu-id="c567d-159">リソース グループの作成には数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="c567d-160">このチュートリアルの後半で作成するリソースと同様に、このリソース グループをダッシュボードにピン留めして簡単にアクセスすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c567d-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="c567d-161">これを行う場合は、ピン アイコン &#128204を選択します。ダッシュボードの右上に表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="c567d-162">サービス計画の作成</span><span class="sxs-lookup"><span data-stu-id="c567d-162">Create the service plan</span></span>

1. <span data-ttu-id="c567d-163">左側のナビゲーション パネルの [**[Azure Portal]**][azure-portal]で、[ **リソースの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="c567d-164">検索ボックスに *「App Service プラン*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="c567d-165">検索結果から **[App Service プラン]** カードを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="c567d-166">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-166">Select **Create**.</span></span>
1. <span data-ttu-id="c567d-167">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c567d-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="c567d-168">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="c567d-168">**Subscription**.</span></span> <span data-ttu-id="c567d-169">既存のサブスクリプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="c567d-170">**リソース グループ**。</span><span class="sxs-lookup"><span data-stu-id="c567d-170">**Resource Group**.</span></span> <span data-ttu-id="c567d-171">以前に作成したグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="c567d-172">**名前**.</span><span class="sxs-lookup"><span data-stu-id="c567d-172">**Name**.</span></span> <span data-ttu-id="c567d-173">サービスプランの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-173">Enter the name for the service plan.</span></span> <span data-ttu-id="c567d-174">たとえば、  *チームサービスプランを挙げる* 場合があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="c567d-175">グループ内で名前が一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="c567d-176">**オペレーティング システム**:</span><span class="sxs-lookup"><span data-stu-id="c567d-176">**Operating System**.</span></span> <span data-ttu-id="c567d-177">*Windows* または該当する OS を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="c567d-178">**地域**.</span><span class="sxs-lookup"><span data-stu-id="c567d-178">**Region**.</span></span> <span data-ttu-id="c567d-179">[ *米国西部* ] またはアプリケーションに近いリージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="c567d-180">**価格レベル**:</span><span class="sxs-lookup"><span data-stu-id="c567d-180">**Pricing Tier**.</span></span> <span data-ttu-id="c567d-181">*[標準 S1]* が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c567d-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="c567d-182">これはデフォルト値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-182">This should be the default value.</span></span>
    1. <span data-ttu-id="c567d-183">[ **レビューと作成** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-183">Select the **Review and create** button.</span></span> <span data-ttu-id="c567d-184">*検証が渡された* というバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="c567d-185">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-185">Select **Create**.</span></span> <span data-ttu-id="c567d-186">アプリ サービス プランの作成には数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="c567d-187">計画はリソース グループに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="c567d-188">ボット チャネル登録の作成</span><span class="sxs-lookup"><span data-stu-id="c567d-188">Create the bot channels registration</span></span>

<span data-ttu-id="c567d-189">ボット チャネル登録は、Microsoft アプリ ID とアプリ パスワード (クライアント シークレット) がある場合、ボット フレームワークに Web サービスをボットとして登録します。</span><span class="sxs-lookup"><span data-stu-id="c567d-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c567d-190">Azure でホストされていない場合にのみ、ボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="c567d-191">Azure ポータルを通じて [ボットを作成](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) した場合は、サービスに既に登録されています。</span><span class="sxs-lookup"><span data-stu-id="c567d-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="c567d-192">[ボット フレームワーク](https://dev.botframework.com/bots/new)または[AppStudio](~/concepts/build-and-test/app-studio-overview.md)を使用してボットを作成した場合、ボットは Azure に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="c567d-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="c567d-193">[米国西部] を選択した場合でも、ボット チャネル登録リソースに **グローバル** リージョンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="c567d-194">これは正常な動作です。</span><span class="sxs-lookup"><span data-stu-id="c567d-194">This is expected.</span></span>

<span data-ttu-id="c567d-195">詳細については、「 [Teamsのボットの作成](../create-a-bot-for-teams.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="c567d-196">ID プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="c567d-196">Create the identity provider</span></span>

<span data-ttu-id="c567d-197">認証に使用できる ID プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="c567d-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="c567d-198">この手順では、Azure AD プロバイダーを使用します。他の Azure AD でサポートされている ID プロバイダーも使用できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="c567d-199">Azure [**ポータル**][azure-portal]の左側のナビゲーション パネルで **、[Azure Active Directory]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="c567d-200">アプリケーションによって要求されたアクセス許可を委任することに同意できるテナントに、この Azure AD リソースを作成して登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="c567d-201">テナントの作成方法については、「 [ポータルにアクセスしてテナントを作成する](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="c567d-202">左側のパネルで、[ **アプリの登録] を** 選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="c567d-203">右のパネルで、左上の **新規登録** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="c567d-204">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c567d-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="c567d-205">**名前**.</span><span class="sxs-lookup"><span data-stu-id="c567d-205">**Name**.</span></span> <span data-ttu-id="c567d-206">アプリケーションの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-206">Enter the name for the application.</span></span> <span data-ttu-id="c567d-207">例としては、  *ボットチーム ID を挙します*。</span><span class="sxs-lookup"><span data-stu-id="c567d-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="c567d-208">名前は一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="c567d-209">アプリケーションの **[サポートされるアカウントの種類]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="c567d-210">*組織ディレクトリ (任意の Azure AD ディレクトリ - マルチテナント) と個人の Microsoft アカウント (xbox* など) のアカウントSkype選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="c567d-211">リダイレクト **URI** の場合:</span><span class="sxs-lookup"><span data-stu-id="c567d-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="c567d-212">&#x2713;**Web** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="c567d-213">&#x2713; URL を に設定 `https://token.botframework.com/.auth/web/redirect` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="c567d-214">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-214">Select **Register**.</span></span>

1. <span data-ttu-id="c567d-215">作成されると、Azure はアプリの **[概要** ] ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="c567d-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="c567d-216">次の情報をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="c567d-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="c567d-217">**アプリケーション (クライアント) ID の** 値。</span><span class="sxs-lookup"><span data-stu-id="c567d-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="c567d-218">この Azure ID アプリケーションをボットに登録する場合は、この値を *後でクライアント ID* として使用します。</span><span class="sxs-lookup"><span data-stu-id="c567d-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="c567d-219">**ディレクトリ (テナント) ID の** 値。</span><span class="sxs-lookup"><span data-stu-id="c567d-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="c567d-220">この値は、後で *テナント ID* として使用して、この Azure ID アプリケーションをボットに登録します。</span><span class="sxs-lookup"><span data-stu-id="c567d-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="c567d-221">左側のパネルで、[ **証明書&シークレット** ] を選択して、アプリケーションのクライアント シークレットを作成します。</span><span class="sxs-lookup"><span data-stu-id="c567d-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="c567d-222">[ **クライアント シークレット**] で 、[ **新しいクライアント シークレット**&#x2795; ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="c567d-223">このアプリ用に作成する必要がある他のユーザー *(Teams の Bot ID アプリ* など) からこのシークレットを識別するための説明を追加します。</span><span class="sxs-lookup"><span data-stu-id="c567d-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="c567d-224">[ **有効期限]** を選択に設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="c567d-225">**[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-225">Select **Add**.</span></span>
   1. <span data-ttu-id="c567d-226">このページを出る前 **に、秘密を記録します**。</span><span class="sxs-lookup"><span data-stu-id="c567d-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="c567d-227">この値は、後で Azure AD アプリケーションをボットに登録するときに _、クライアント シークレット_ として使用します。</span><span class="sxs-lookup"><span data-stu-id="c567d-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="c567d-228">ID プロバイダー接続を構成し、ボットに登録する</span><span class="sxs-lookup"><span data-stu-id="c567d-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="c567d-229">注: サービス プロバイダーの 2 つのオプションは、Azure AD V1 と Azure AD V2 です。</span><span class="sxs-lookup"><span data-stu-id="c567d-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="c567d-230">2 つのプロバイダーの違い [は、ここで](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)要約しますが、一般的に、V2 は、ボットのアクセス許可の変更に関してより柔軟に対応できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-230">The differences between the two providers are summarized [here](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="c567d-231">GraphAPI のアクセス許可はスコープ フィールドに一覧表示され、新しいアクセス許可が追加されると、ボットはユーザーが次のサインインで新しいアクセス許可に同意できるようにします。</span><span class="sxs-lookup"><span data-stu-id="c567d-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="c567d-232">V1 の場合、OAuth ダイアログで新しいアクセス許可を求めるユーザーがボットの同意を削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="c567d-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="c567d-233">Azure AD V1</span></span>

1. <span data-ttu-id="c567d-234">Azure [**ポータル**][azure-portal]で、ダッシュボードからリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="c567d-235">ボット チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="c567d-236">リソース ページを開き、[**設定**] の下の **[構成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="c567d-237">**[OAuth 接続設定の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="c567d-238">次の図は、リソース ページで対応する選択を示しています。</span><span class="sxs-lookup"><span data-stu-id="c567d-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="c567d-239">![設定](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="c567d-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="c567d-240">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="c567d-241">**名前**.</span><span class="sxs-lookup"><span data-stu-id="c567d-241">**Name**.</span></span> <span data-ttu-id="c567d-242">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-242">Enter a name for the connection.</span></span> <span data-ttu-id="c567d-243">この名前は、ファイル内のボットで使用 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="c567d-244">たとえば *、ボットチーム認証1*.</span><span class="sxs-lookup"><span data-stu-id="c567d-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="c567d-245">**サービス プロバイダ**:</span><span class="sxs-lookup"><span data-stu-id="c567d-245">**Service Provider**.</span></span> <span data-ttu-id="c567d-246">[**Azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="c567d-247">これを選択すると、Azure AD 固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="c567d-248">**クライアント ID**.上記の手順で、Azure ID プロバイダー アプリ用に記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="c567d-249">**クライアント シークレット**:</span><span class="sxs-lookup"><span data-stu-id="c567d-249">**Client secret**.</span></span> <span data-ttu-id="c567d-250">上記の手順で、Azure ID プロバイダー アプリに記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="c567d-251">**許可の種類**:</span><span class="sxs-lookup"><span data-stu-id="c567d-251">**Grant Type**.</span></span> <span data-ttu-id="c567d-252">`authorization_code`を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="c567d-253">**ログイン URL**:</span><span class="sxs-lookup"><span data-stu-id="c567d-253">**Login URL**.</span></span> <span data-ttu-id="c567d-254">`https://login.microsoftonline.com`を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="c567d-255">**[テナント ID]** には、ID プロバイダー アプリの作成時に選択したサポート対象アカウントの種類に応じて、Azure ID アプリまたは **共通** のアカウント ID に以前に記録した **ディレクトリ (テナント) ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="c567d-256">割り当てる値を決定するには、次の基準に従います。</span><span class="sxs-lookup"><span data-stu-id="c567d-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="c567d-257">*この組織ディレクトリのアカウントのみ (Microsoft のみ - シングル テナント)* または *任意の組織ディレクトリ (Microsoft AAD ディレクトリ - マルチ テナント) のアカウントのいずれかを* 選択した場合は、AAD アプリの前に記録した **テナント ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="c567d-258">これは、認証可能なユーザーに関連付けられたテナントになります。</span><span class="sxs-lookup"><span data-stu-id="c567d-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="c567d-259">*組織のディレクトリで [アカウント] を選択した場合 ([任意の AAD ディレクトリ - マルチ テナント] および [Skype、Xbox、Outlookなど] の Microsoft 個人アカウントなど) は、* テナント ID ではなく **共通** という単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="c567d-260">それ以外の場合、AAD アプリは ID が選択されたテナントを通じて検証し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="c567d-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="c567d-261">h.</span><span class="sxs-lookup"><span data-stu-id="c567d-261">h.</span></span> <span data-ttu-id="c567d-262">[ **リソース URL]** に を入力 `https://graph.microsoft.com/` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="c567d-263">これは、現在のコード サンプルでは使用されていません。</span><span class="sxs-lookup"><span data-stu-id="c567d-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="c567d-264">i.</span><span class="sxs-lookup"><span data-stu-id="c567d-264">i.</span></span> <span data-ttu-id="c567d-265">**[スコープ] は空白のままにします**。</span><span class="sxs-lookup"><span data-stu-id="c567d-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="c567d-266">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-266">The following image is an example:</span></span>

    ![チームボットアプリ認証接続文字列 adv1 ビュー](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="c567d-268">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="c567d-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="c567d-269">Azure AD V2</span></span>

1. <span data-ttu-id="c567d-270">Azure [**ポータル**][azure-portal]で、ダッシュボードからリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="c567d-271">ボット チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="c567d-272">リソース ページを開き、[**設定**] の下の **[構成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="c567d-273">**[OAuth 接続設定の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="c567d-274">次の図は、リソース ページで対応する選択を示しています。</span><span class="sxs-lookup"><span data-stu-id="c567d-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="c567d-275">![設定](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="c567d-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="c567d-276">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="c567d-277">**名前**.</span><span class="sxs-lookup"><span data-stu-id="c567d-277">**Name**.</span></span> <span data-ttu-id="c567d-278">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-278">Enter a name for the connection.</span></span> <span data-ttu-id="c567d-279">この名前は、ファイル内のボットで使用 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="c567d-280">たとえば *、ボットチーム認証2*.</span><span class="sxs-lookup"><span data-stu-id="c567d-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="c567d-281">**サービス プロバイダ**:</span><span class="sxs-lookup"><span data-stu-id="c567d-281">**Service Provider**.</span></span> <span data-ttu-id="c567d-282">**[v2 Azure Active Directory]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="c567d-283">これを選択すると、Azure AD 固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="c567d-284">**クライアント ID**.上記の手順で、Azure ID プロバイダー アプリ用に記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="c567d-285">**クライアント シークレット**:</span><span class="sxs-lookup"><span data-stu-id="c567d-285">**Client secret**.</span></span> <span data-ttu-id="c567d-286">上記の手順で、Azure ID プロバイダー アプリに記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="c567d-287">**トークン Exchange URL**:</span><span class="sxs-lookup"><span data-stu-id="c567d-287">**Token Exchange URL**.</span></span> <span data-ttu-id="c567d-288">空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="c567d-288">Leave this blank.</span></span>
    1. <span data-ttu-id="c567d-289">**[テナント ID]** には、ID プロバイダー アプリの作成時に選択したサポート対象アカウントの種類に応じて、Azure ID アプリまたは **共通** のアカウント ID に以前に記録した **ディレクトリ (テナント) ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="c567d-290">割り当てる値を決定するには、次の基準に従います。</span><span class="sxs-lookup"><span data-stu-id="c567d-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="c567d-291">*この組織ディレクトリのアカウントのみ (Microsoft のみ - シングル テナント)* または *任意の組織ディレクトリ (Microsoft AAD ディレクトリ - マルチ テナント) のアカウントのいずれかを* 選択した場合は、AAD アプリの前に記録した **テナント ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="c567d-292">これは、認証可能なユーザーに関連付けられたテナントになります。</span><span class="sxs-lookup"><span data-stu-id="c567d-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="c567d-293">*組織のディレクトリで [アカウント] を選択した場合 ([任意の AAD ディレクトリ - マルチ テナント] および [Skype、Xbox、Outlookなど] の Microsoft 個人アカウントなど) は、* テナント ID ではなく **共通** という単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="c567d-294">それ以外の場合、AAD アプリは ID が選択されたテナントを通じて検証し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="c567d-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="c567d-295">**[スコープ]** に、このアプリケーションが必要とするグラフのアクセス許可のスペース区切りのリストを入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="c567d-296">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="c567d-297">接続をテストする</span><span class="sxs-lookup"><span data-stu-id="c567d-297">Test the connection</span></span>

1. <span data-ttu-id="c567d-298">接続エントリを選択して、作成した接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="c567d-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="c567d-299">**[サービス プロバイダー接続設定**] パネルの上部にある [**テスト** 接続] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="c567d-300">初めてこれを行うと、新しいブラウザウィンドウが開き、アカウントを選択するよう求める。</span><span class="sxs-lookup"><span data-stu-id="c567d-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="c567d-301">使用する 1 つを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="c567d-302">次に、ID プロバイダーにデータ (資格情報) の使用を許可するように求められます。</span><span class="sxs-lookup"><span data-stu-id="c567d-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="c567d-303">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-303">The following image is an example:</span></span>

    ![チームボット認証接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="c567d-305">**[同意する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-305">Select **Accept**.</span></span>
1. <span data-ttu-id="c567d-306">これで、[ **接続のテストに \<your-connection-name> 成功** しました] ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="c567d-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="c567d-307">エラーが発生した場合は、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="c567d-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="c567d-308">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-308">The following image is an example:</span></span>

    ![チームボットアプリ認証接続 str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="c567d-310">接続名は、ボット コードがユーザー認証トークンを取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="c567d-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="c567d-311">ボットサンプルコードの準備</span><span class="sxs-lookup"><span data-stu-id="c567d-311">Prepare the bot sample code</span></span>

<span data-ttu-id="c567d-312">予備的な設定が完了したら、この記事で使用するボットの作成に焦点を当てましょう。</span><span class="sxs-lookup"><span data-stu-id="c567d-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c567d-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c567d-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="c567d-314">[クローン cs 認証サンプル][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="c567d-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="c567d-315">Visual Studioを起動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="c567d-316">ツール バーで **[ファイル - >開く -> Project/ソリューション] を** 選択し、ボット プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="c567d-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="c567d-317">C# で次の **appsettings.jsを** 更新します。</span><span class="sxs-lookup"><span data-stu-id="c567d-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="c567d-318">`ConnectionName`ボット チャネル登録に追加した ID プロバイダー接続の名前を設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="c567d-319">この例で使用した名前は *、ボットハウザDv1* です。</span><span class="sxs-lookup"><span data-stu-id="c567d-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="c567d-320">`MicrosoftAppId`ボット チャネル登録時に保存した **ボット アプリ ID** に設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="c567d-321">`MicrosoftAppPassword`ボットチャネル登録時に保存した **顧客の秘密** に設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="c567d-322">ボット シークレットの文字によっては、パスワードをエスケープする XML が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="c567d-323">たとえば、アンパサンド (&) は `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="c567d-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="c567d-324">ソリューション エクスプローラーで、フォルダーに移動 `TeamsAppManifest` し、ボット `manifest.json` `id` `botId` チャネル登録時に保存した **ボット アプリ ID** を開いて設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="c567d-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c567d-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="c567d-326">クローン [ノード認証サンプル][teams-auth-bot-js]:</span><span class="sxs-lookup"><span data-stu-id="c567d-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="c567d-327">コンソールで、プロジェクトに移動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="c567d-328">モジュールのインストール</span><span class="sxs-lookup"><span data-stu-id="c567d-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="c567d-329">次のように **.env** の構成を更新します。</span><span class="sxs-lookup"><span data-stu-id="c567d-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="c567d-330">`MicrosoftAppId`ボット チャネル登録時に保存した **ボット アプリ ID** に設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="c567d-331">`MicrosoftAppPassword`ボットチャネル登録時に保存した **顧客の秘密** に設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="c567d-332">ID `connectionName` プロバイダー接続の名前に を設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="c567d-333">ボット シークレットの文字によっては、パスワードをエスケープする XML が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="c567d-334">たとえば、アンパサンド (&) は `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="c567d-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="c567d-335">フォルダーで `teamsAppManifest` 、Microsoft `manifest.json` アプリ `id` **ID** と `botId` **、ボット** チャネル登録時に保存したボット アプリ ID を開いて設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="c567d-336">Python</span><span class="sxs-lookup"><span data-stu-id="c567d-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="c567d-337">github リポジトリから [py 認証サンプル][teams-auth-bot-py] を複製します。</span><span class="sxs-lookup"><span data-stu-id="c567d-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="c567d-338">**config.py** の更新 :</span><span class="sxs-lookup"><span data-stu-id="c567d-338">Update **config.py**:</span></span>

    - <span data-ttu-id="c567d-339">`ConnectionName`ボットに追加した OAuth 接続設定の名前を設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="c567d-340">`MicrosoftAppId` `MicrosoftAppPassword` ボットのアプリ ID とアプリシークレットを設定します。</span><span class="sxs-lookup"><span data-stu-id="c567d-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="c567d-341">ボット シークレットの文字によっては、パスワードをエスケープする XML が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="c567d-342">たとえば、アンパサンド (&) は `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="c567d-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="c567d-343">ボットを Azure にデプロイする</span><span class="sxs-lookup"><span data-stu-id="c567d-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="c567d-344">ボットをデプロイするには [、「Azure にボットをデプロイ](https://aka.ms/azure-bot-deployment-cli)する方法」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="c567d-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="c567d-345">または、Visual Studio中に、次の手順を実行できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="c567d-346">ソリューション *エクスプローラー* Visual Studioプロジェクト名を選択して保持 (または右クリック) します。</span><span class="sxs-lookup"><span data-stu-id="c567d-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="c567d-347">ドロップダウン メニューで、[ **発行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="c567d-348">表示されたウィンドウで、[ **新規** ] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="c567d-349">ダイアログウィンドウで、左側の **[App Service]** を選択し、右側に **[新規作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="c567d-350">[ **公開** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="c567d-351">次のダイアログ ウィンドウで、必要な情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="c567d-352">例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c567d-352">The following is an example:</span></span>

    ![認証アプリサービス](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="c567d-354">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-354">Select **Create**.</span></span>
1. <span data-ttu-id="c567d-355">展開が正常に完了すると、Visual Studioに反映されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="c567d-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="c567d-356">さらに、あなたの *ボットの準備* ができているというページがデフォルトのブラウザに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="c567d-357">URL は次のようになります `https://botteamsauth.azurewebsites.net/` 。</span><span class="sxs-lookup"><span data-stu-id="c567d-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="c567d-358">ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="c567d-358">Save it to a file.</span></span>
1. <span data-ttu-id="c567d-359">ブラウザーで [**、Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="c567d-360">リソース グループを確認すると、ボットが他のリソースと共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="c567d-361">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-361">The following image is an example:</span></span>

    ![チームボット認証アプリサービスグループ](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="c567d-363">リソース グループで、ボット チャネル登録名 (リンク) を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="c567d-364">左側のパネルで[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="c567d-365">[ **メッセージング エンドポイント** ] ボックスに、上記で取得した URL を入力し、その後に `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="c567d-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="c567d-366">これは、例です `https://botteamsauth.azurewebsites.net/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="c567d-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="c567d-367">左上の **[保存]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="c567d-368">エミュレーターを使用してボットをテストする</span><span class="sxs-lookup"><span data-stu-id="c567d-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="c567d-369">まだ実行していない場合は[、Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c567d-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="c567d-370">[「エミュレータを使用してデバッグする](https://aka.ms/bot-framework-emulator-debug-with-emulator)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="c567d-371">ボットサンプルログインが機能するためには、エミュレータを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-371">In order for the bot sample login to work you must configure the Emulator.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="c567d-372">認証用のエミュレーターの構成</span><span class="sxs-lookup"><span data-stu-id="c567d-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="c567d-373">ボットで認証が必要な場合は、エミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-373">If a bot requires authentication, you must configure the Emulator.</span></span> <span data-ttu-id="c567d-374">構成するには:</span><span class="sxs-lookup"><span data-stu-id="c567d-374">To configure:</span></span>

1. <span data-ttu-id="c567d-375">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-375">Start the Emulator.</span></span>
1. <span data-ttu-id="c567d-376">エミュレーターで、左下にある歯車アイコン&#9881;、または右上の **[エミュレーター 設定]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-376">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="c567d-377">[ **バージョン 1.0 認証トークンを使用する**] のチェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="c567d-377">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="c567d-378">**ngrok** ツールへのローカル パスを入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-378">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="c567d-379">Bot Framework Emulator / ngrok トンネリング統合 [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="c567d-379">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="c567d-380">ツールの詳細については [、ngrok](https://ngrok.com/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c567d-380">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="c567d-381">**エミュレータが起動したら、実行 ngrok のチェックボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="c567d-381">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="c567d-382">[ **保存** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-382">Select the **Save** button.</span></span>

<span data-ttu-id="c567d-383">ボットがサインイン カードを表示し、ユーザーがサインイン ボタンを選択すると、ユーザーが認証プロバイダーでサインインするために使用できるページがエミュレーターによって開かれます。</span><span class="sxs-lookup"><span data-stu-id="c567d-383">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="c567d-384">ユーザーがトークンを生成すると、プロバイダーはユーザー トークンを生成し、ボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="c567d-384">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="c567d-385">その後、ボットはユーザーの代わりに動作できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-385">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="c567d-386">ボットをローカルでテストする</span><span class="sxs-lookup"><span data-stu-id="c567d-386">Test the bot locally</span></span>

<span data-ttu-id="c567d-387">認証メカニズムを構成した後、実際のボット テストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-387">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="c567d-388">たとえば、Visual Studioを使用して、ボット サンプルをコンピューターでローカルに実行します。</span><span class="sxs-lookup"><span data-stu-id="c567d-388">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="c567d-389">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-389">Start the Emulator.</span></span>
1. <span data-ttu-id="c567d-390">[ **ボットを開く** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-390">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="c567d-391">[ **ボット URL]** ボックスに、ボットのローカル URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-391">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="c567d-392">通常、 `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="c567d-392">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="c567d-393">Microsoft **アプリ ID** に、 からボットのアプリ ID を入力 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-393">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="c567d-394">Microsoft **アプリ のパスワード** に、 からボットのアプリ パスワードを入力 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-394">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="c567d-395">**[Connect]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-395">Select **Connect**.</span></span>
1. <span data-ttu-id="c567d-396">ボットが起動して実行されたら、サインイン カードを表示するテキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-396">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="c567d-397">**[サインイン]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-397">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="c567d-398">ポップアップ ダイアログが表示され **、[URL を開く確認]** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-398">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="c567d-399">これは、ボットのユーザー (ユーザー) の認証を許可するためです。</span><span class="sxs-lookup"><span data-stu-id="c567d-399">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="c567d-400">**[確認]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-400">Select **Confirm**.</span></span>
1. <span data-ttu-id="c567d-401">確認された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-401">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="c567d-402">エミュレータに使用した構成に応じて、次のいずれかを取得します。</span><span class="sxs-lookup"><span data-stu-id="c567d-402">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="c567d-403">**サインイン確認コードの使用**</span><span class="sxs-lookup"><span data-stu-id="c567d-403">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="c567d-404">&#x2713; 検証コードを表示するウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="c567d-404">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="c567d-405">&#x2713; サインインを完了するために、検証コードをコピーしてチャット ボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-405">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="c567d-406">**認証トークンの使用**:</span><span class="sxs-lookup"><span data-stu-id="c567d-406">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="c567d-407">&#x2713; 資格情報に基づいてログインしています。</span><span class="sxs-lookup"><span data-stu-id="c567d-407">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="c567d-408">次の図は、ログインした後のボット UI の例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-408">The following image is an example of the bot UI after you've logged in:</span></span>

    ![認証ボットログインエミュレータ](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="c567d-410">ボットが *[トークンを表示しますか? ]* をクリックすると、次のような応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-410">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![認証ボットログインエミュレータトークン](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="c567d-412">入力チャットボックスに **ログアウト** を入力してサインアウトします。これによりユーザー トークンが解放され、再度サインインするまでボットはユーザーに代わって行動できなくなります。</span><span class="sxs-lookup"><span data-stu-id="c567d-412">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="c567d-413">ボット認証では **、Bot コネクタ サービス** を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-413">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="c567d-414">サービスは、ボットのボット チャネル登録情報にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c567d-414">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="c567d-415">展開されたボットをテストする</span><span class="sxs-lookup"><span data-stu-id="c567d-415">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="c567d-416">ブラウザーで [**、Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-416">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="c567d-417">リソース グループを検索します。</span><span class="sxs-lookup"><span data-stu-id="c567d-417">Find your resource group.</span></span>
1. <span data-ttu-id="c567d-418">リソースリンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-418">Select the resource link.</span></span> <span data-ttu-id="c567d-419">リソース ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-419">The resource page is displayed.</span></span>
1. <span data-ttu-id="c567d-420">リソース ページで **、[Web チャットでテスト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-420">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="c567d-421">ボットが起動し、定義済みの案内応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-421">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="c567d-422">チャットボックスに何でも入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-422">Type anything in the chat box.</span></span>
1. <span data-ttu-id="c567d-423">[サインイン] ボックス **を** 選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-423">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="c567d-424">ポップアップ ダイアログが表示され **、[URL を開く確認]** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-424">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="c567d-425">これは、ボットのユーザー (ユーザー) の認証を許可するためです。</span><span class="sxs-lookup"><span data-stu-id="c567d-425">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="c567d-426">**[確認]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-426">Select **Confirm**.</span></span>
1. <span data-ttu-id="c567d-427">確認された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-427">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="c567d-428">次の図は、ログインした後のボット UI の例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-428">The following image is an example of the bot UI after you have logged in:</span></span>

    ![認証ボットログインが展開されました](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="c567d-430">.</span><span class="sxs-lookup"><span data-stu-id="c567d-430">.</span></span>

1. <span data-ttu-id="c567d-431">[ **はい** ] をクリックして認証トークンを表示します。</span><span class="sxs-lookup"><span data-stu-id="c567d-431">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="c567d-432">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-432">The following image is an example:</span></span>

    ![認証ボット ログイン展開トークン](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="c567d-434">.</span><span class="sxs-lookup"><span data-stu-id="c567d-434">.</span></span>

1. <span data-ttu-id="c567d-435">ログアウトを入力してサインアウトします。</span><span class="sxs-lookup"><span data-stu-id="c567d-435">Enter logout to sign out.</span></span>

    ![認証ボットのデプロイ済みログアウト](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="c567d-437">サインインに問題がある場合は、前の手順で説明したように接続を再度テストしてみてください。</span><span class="sxs-lookup"><span data-stu-id="c567d-437">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="c567d-438">これにより、認証トークンが再作成される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-438">This could recreate the authentication token.</span></span>
> <span data-ttu-id="c567d-439">Azure の Bot Framework Web Chat クライアントでは、認証が正しく確立される前に、何度かサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-439">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="c567d-440">Teamsでボットをインストールしてテストする</span><span class="sxs-lookup"><span data-stu-id="c567d-440">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="c567d-441">ボット プロジェクトで、フォルダーに 、 `TeamsAppManifest` `manifest.json` と ファイルが含まれていることを確認 `outline.png` `color.png` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-441">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="c567d-442">ソリューション エクスプローラーで、フォルダーに移動 `TeamsAppManifest` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-442">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="c567d-443">`manifest.json`次の値を割り当てて編集します。</span><span class="sxs-lookup"><span data-stu-id="c567d-443">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="c567d-444">ボット チャネル登録時に受け取った **ボット アプリ ID** が に割り当てられていることを確認 `id` `botId` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-444">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="c567d-445">この値を割り当てます `validDomains: [ "token.botframework.com" ]` : 。</span><span class="sxs-lookup"><span data-stu-id="c567d-445">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="c567d-446">、  `manifest.json` 、および ファイルを選択して圧縮 `outline.png` `color.png` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-446">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="c567d-447">**Microsoft Teams** を開きます。</span><span class="sxs-lookup"><span data-stu-id="c567d-447">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="c567d-448">左側のパネルの下部にある **[アプリ**] アイコン を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-448">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="c567d-449">右側のパネルの下部にある [カスタム **アプリアップロード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-449">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="c567d-450">フォルダーに移動 `TeamsAppManifest` し、zip 形式のマニフェストをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="c567d-450">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="c567d-451">次のウィザードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-451">The following wizard is displayed:</span></span>

    ![認証ボットチームのアップロード](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="c567d-453">**[チームに追加]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-453">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="c567d-454">次のウィンドウで、ボットを使用するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-454">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="c567d-455">[ **ボットのセットアップ** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-455">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="c567d-456">左側のパネルで3つの点(&#x25cf;&#x25cf;&#x25cf;)を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-456">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="c567d-457">次に **、アプリケーションスタジオアイコンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-457">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="c567d-458">[ **マニフェスト エディター** ] タブを選択します。アップロードしたボットのアイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-458">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="c567d-459">また、ボットとメッセージを交換するために使用できるチャット リストに連絡先としてリストされているボットを表示できるはずです。</span><span class="sxs-lookup"><span data-stu-id="c567d-459">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="c567d-460">Teamsでボットをローカルにテストする</span><span class="sxs-lookup"><span data-stu-id="c567d-460">Testing the bot locally in Teams</span></span>

<span data-ttu-id="c567d-461">Microsoft Teams完全にクラウドベースの製品であり、アクセスするすべてのサービスを HTTPS エンドポイントを使用してクラウドから利用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-461">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="c567d-462">そのため、ボット (サンプル) がTeamsで動作できるようにするには、コードを選択したクラウドに発行するか、またはローカルで実行されているインスタンスを **トンネリング** ツールを介して外部からアクセスできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-462">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="c567d-463">マシン上でローカルに開くポートの外部アドレス指定可能な URL を作成する  [ngrok](https://ngrok.com/download)をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c567d-463">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="c567d-464">Microsoft Teams アプリをローカルで実行する準備として ngrok を設定するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="c567d-464">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="c567d-465">ターミナル ウィンドウで、インストールしたディレクトリに移動 `ngrok.exe` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-465">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="c567d-466">*環境変数* のパスを指し示す設定を行うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c567d-466">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="c567d-467">たとえば、 を実行 `ngrok http 3978 --host-header=localhost:3978` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-467">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="c567d-468">必要に応じてポート番号を交換します。</span><span class="sxs-lookup"><span data-stu-id="c567d-468">Replace the port number as needed.</span></span>
<span data-ttu-id="c567d-469">指定したポートでリッスンする ngrok が起動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-469">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="c567d-470">その代わりに、ngrok が実行されている間有効な、外部アドレス指定可能な URL が提供されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-470">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="c567d-471">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-471">The following image is an example:</span></span>

    ![チームボットアプリ認証接続文字列adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="c567d-473">.</span><span class="sxs-lookup"><span data-stu-id="c567d-473">.</span></span>

1. <span data-ttu-id="c567d-474">転送 HTTPS アドレスをコピーします。</span><span class="sxs-lookup"><span data-stu-id="c567d-474">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="c567d-475">次のような値を指定します `https://dea822bf.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="c567d-475">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="c567d-476">を `/api/messages` 取得するために追加 `https://dea822bf.ngrok.io/api/messages` します。</span><span class="sxs-lookup"><span data-stu-id="c567d-476">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="c567d-477">これは、マシン上でローカルに実行され、Microsoft Teamsのチャットで Web 経由で到達可能なボットの **メッセージ エンドポイント** です。</span><span class="sxs-lookup"><span data-stu-id="c567d-477">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="c567d-478">最後に実行する手順は、デプロイされたボットのメッセージ エンドポイントを更新することです。</span><span class="sxs-lookup"><span data-stu-id="c567d-478">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="c567d-479">この例では、Azure にボットをデプロイしました。</span><span class="sxs-lookup"><span data-stu-id="c567d-479">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="c567d-480">だから\*\*次の手順を実行してみましょう:</span><span class="sxs-lookup"><span data-stu-id="c567d-480">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="c567d-481">ブラウザーで [**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-481">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="c567d-482">**[ボット チャネル登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-482">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="c567d-483">左側のパネルで[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c567d-483">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="c567d-484">右側のパネルの [ **メッセージング エンドポイント** ] ボックスに ngrok URL `https://dea822bf.ngrok.io/api/messages` を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-484">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="c567d-485">デバッグ モードなどで、ボットVisual Studioローカルに起動します。</span><span class="sxs-lookup"><span data-stu-id="c567d-485">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="c567d-486">Bot Framework ポータルのテスト **Web チャット** を使用して、ローカルで実行しながらボットをテストします。</span><span class="sxs-lookup"><span data-stu-id="c567d-486">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="c567d-487">エミュレーターと同様に、このテストでは、Teams固有の機能にアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="c567d-487">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="c567d-488">実行中のターミナル ウィンドウでは `ngrok` 、ボットと Web チャット クライアント間の HTTP トラフィックを確認できます。</span><span class="sxs-lookup"><span data-stu-id="c567d-488">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="c567d-489">より詳細なビューが必要な場合は、ブラウザウィンドウに `http://127.0.0.1:4040` 、前のターミナルウィンドウから取得した画面を入力します。</span><span class="sxs-lookup"><span data-stu-id="c567d-489">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="c567d-490">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="c567d-490">The following image is an example:</span></span>

    ![認証ボットチーム ngrok テスト](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="c567d-492">.</span><span class="sxs-lookup"><span data-stu-id="c567d-492">.</span></span>

> [!NOTE]
> <span data-ttu-id="c567d-493">ngrok を停止して再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-493">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="c567d-494">プロジェクトで ngrok を使用し、使用している機能に応じて、すべての URL 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-494">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="c567d-495">追加情報</span><span class="sxs-lookup"><span data-stu-id="c567d-495">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="c567d-496">チームアプリマニフェスト/manifest.jsオン</span><span class="sxs-lookup"><span data-stu-id="c567d-496">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="c567d-497">このマニフェストには、Microsoft Teamsがボットに接続するために必要な情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c567d-497">This manifest contains information needed by Microsoft Teams to connect with the bot:</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

<span data-ttu-id="c567d-498">認証では、Teamsは、以下で説明するとおり、他のチャネルとは若干異なる動作をします。</span><span class="sxs-lookup"><span data-stu-id="c567d-498">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="c567d-499">呼び出しアクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="c567d-499">Handling Invoke Activity</span></span>

<span data-ttu-id="c567d-500">**呼び出しアクティビティ** は、他のチャネルで使用されるイベント アクティビティではなく、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-500">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="c567d-501">これは **、アクティビティ ハンドラ** をサブクラス化することによって行われます。</span><span class="sxs-lookup"><span data-stu-id="c567d-501">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c567d-502">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c567d-502">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="c567d-503">**ボット/ダイアログボット.cs**</span><span class="sxs-lookup"><span data-stu-id="c567d-503">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="c567d-504">**ボット/チームボット.cs**</span><span class="sxs-lookup"><span data-stu-id="c567d-504">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="c567d-505">**OAuthPrompt** が使用されている場合は、*呼び出しアクティビティ* をダイアログに転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="c567d-506">チームアクティビティハンドラー.cs</span><span class="sxs-lookup"><span data-stu-id="c567d-506">TeamsActivityHandler.cs</span></span>

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[<span data-ttu-id="c567d-507">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c567d-507">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="c567d-508">**ボット/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="c567d-508">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="c567d-509">**ボット/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="c567d-509">**bots/teamsBot.js**</span></span>

<span data-ttu-id="c567d-510">**OAuthPrompt** が使用されている場合は、*呼び出しアクティビティ* をダイアログに転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-510">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="c567d-511">**ダイアログ/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="c567d-511">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="c567d-512">ダイアログ ステップ内でを使用 `beginDialog` して、ユーザーにサインインを求める OAuth プロンプトを開始します。</span><span class="sxs-lookup"><span data-stu-id="c567d-512">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="c567d-513">ユーザーが既にサインインしている場合、ユーザーに確認メッセージを表示せずにトークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-513">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="c567d-514">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-514">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="c567d-515">Azure Bot サービスは、ユーザーがサインインを試みた後にトークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="c567d-515">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="c567d-516">次のダイアログ ステップで、前の手順の結果にトークンが存在するかどうか確認します。</span><span class="sxs-lookup"><span data-stu-id="c567d-516">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="c567d-517">null でない場合、ユーザーは正常にサインインしました。</span><span class="sxs-lookup"><span data-stu-id="c567d-517">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="c567d-518">**ボット/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="c567d-518">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="c567d-519">Python</span><span class="sxs-lookup"><span data-stu-id="c567d-519">Python</span></span>](#tab/python-sample)

<span data-ttu-id="c567d-520">**ボット/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="c567d-520">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="c567d-521">**ボット/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="c567d-521">**bots/teams_bot.py**</span></span>

<span data-ttu-id="c567d-522">**OAuthPrompt** が使用されている場合は、*呼び出しアクティビティ* をダイアログに転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c567d-522">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="c567d-523">**ダイアログ/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="c567d-523">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="c567d-524">ダイアログ ステップ内でを使用 `begin_dialog` して、ユーザーにサインインを求める OAuth プロンプトを開始します。</span><span class="sxs-lookup"><span data-stu-id="c567d-524">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="c567d-525">ユーザーが既にサインインしている場合、ユーザーに確認メッセージを表示せずにトークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-525">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="c567d-526">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c567d-526">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="c567d-527">Azure Bot サービスは、ユーザーがサインインを試みた後にトークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="c567d-527">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="c567d-528">次のダイアログ ステップで、前の手順の結果にトークンが存在するかどうか確認します。</span><span class="sxs-lookup"><span data-stu-id="c567d-528">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="c567d-529">null でない場合、ユーザーは正常にサインインしました。</span><span class="sxs-lookup"><span data-stu-id="c567d-529">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="c567d-530">**ダイアログ/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="c567d-530">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a><span data-ttu-id="c567d-531">関連項目</span><span class="sxs-lookup"><span data-stu-id="c567d-531">See also</span></span>

[<span data-ttu-id="c567d-532">Azure ボット サービスを使用して認証を追加する</span><span class="sxs-lookup"><span data-stu-id="c567d-532">Add authentication through Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
