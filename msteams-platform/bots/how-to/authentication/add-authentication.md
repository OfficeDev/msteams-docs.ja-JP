---
title: 認証をボットにTeamsする
author: clearab
description: OAuth 認証をボットに追加する方法は、Microsoft Teams。
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 7f171a791a9ee557e4af2e7d1e1b053046bd9db5
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101489"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="a366b-103">認証をボットにTeamsする</span><span class="sxs-lookup"><span data-stu-id="a366b-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="a366b-104">メール サービスなど、ユーザーの代わりにリソースにアクセスMicrosoft Teamsボットを作成する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="a366b-105">この記事では、OAuth 2.0 に基づいて Azure Bot Service v4 SDK 認証を使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="a366b-106">これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットの開発が容易になります。</span><span class="sxs-lookup"><span data-stu-id="a366b-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="a366b-107">このすべてで重要なのは、後で **説明** する ID プロバイダーの使用です。</span><span class="sxs-lookup"><span data-stu-id="a366b-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="a366b-108">OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。</span><span class="sxs-lookup"><span data-stu-id="a366b-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="a366b-109">OAuth 2.0 の基本的な理解は、認証を使用する場合の前提条件Teams。</span><span class="sxs-lookup"><span data-stu-id="a366b-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="a366b-110">完全 [な仕様については、「OAuth 2 簡](https://aka.ms/oauth2-simplified) 体字」、OAuth [2.0](https://oauth.net/2/) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a366b-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="a366b-111">Azure Bot Service が認証を処理する方法の詳細については、「 [会話内のユーザー認証」を参照してください](https://aka.ms/azure-bot-authentication)。</span><span class="sxs-lookup"><span data-stu-id="a366b-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="a366b-112">この記事では、以下について説明します。</span><span class="sxs-lookup"><span data-stu-id="a366b-112">In this article you'll learn:</span></span>

- <span data-ttu-id="a366b-113">**認証が有効なボットを作成する方法**。</span><span class="sxs-lookup"><span data-stu-id="a366b-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="a366b-114">[cs-auth-sample][teams-auth-bot-cs]を使用して、ユーザーサインイン資格情報と認証トークンの生成を処理します。</span><span class="sxs-lookup"><span data-stu-id="a366b-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="a366b-115">**ボットを Azure に展開し、ID プロバイダーに関連付ける方法**。</span><span class="sxs-lookup"><span data-stu-id="a366b-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="a366b-116">プロバイダーは、ユーザー サインイン資格情報に基づいてトークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="a366b-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="a366b-117">ボットはトークンを使用して、認証が必要なメール サービスなどのリソースにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a366b-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="a366b-118">詳細については、「ボット[Microsoft Teams認証フロー」を参照してください](auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="a366b-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="a366b-119">**ボットをアプリ内に統合するMicrosoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="a366b-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="a366b-120">ボットが統合された後は、サインインしてチャットでメッセージとメッセージを交換できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a366b-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="a366b-121">Prerequisites</span></span>

- <span data-ttu-id="a366b-122">ボットの[基本、状態][concept-basics][の管理、][concept-state]ダイアログ ライブラリ[][concept-dialogs]、および連続した会話フローの[実装方法に関する知識][simple-dialog]。</span><span class="sxs-lookup"><span data-stu-id="a366b-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="a366b-123">Azure と OAuth 2.0 の開発に関する知識。</span><span class="sxs-lookup"><span data-stu-id="a366b-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="a366b-124">現在のバージョンの Visual Studio Git。</span><span class="sxs-lookup"><span data-stu-id="a366b-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="a366b-125">Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="a366b-125">Azure account.</span></span> <span data-ttu-id="a366b-126">必要に応じて、Azure 無料アカウント [を作成できます](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="a366b-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="a366b-127">次のサンプル。</span><span class="sxs-lookup"><span data-stu-id="a366b-127">The following sample.</span></span>

    | <span data-ttu-id="a366b-128">サンプル</span><span class="sxs-lookup"><span data-stu-id="a366b-128">Sample</span></span> | <span data-ttu-id="a366b-129">BotBuilder のバージョン</span><span class="sxs-lookup"><span data-stu-id="a366b-129">BotBuilder version</span></span> | <span data-ttu-id="a366b-130">デモンストレーション</span><span class="sxs-lookup"><span data-stu-id="a366b-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="a366b-131"> [cs-auth-sample でのボット認証][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="a366b-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="a366b-132">v4</span><span class="sxs-lookup"><span data-stu-id="a366b-132">v4</span></span> | <span data-ttu-id="a366b-133">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="a366b-133">OAuthCard support</span></span> |
    | <span data-ttu-id="a366b-134"> [js-auth-sample でのボット認証][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="a366b-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="a366b-135">v4</span><span class="sxs-lookup"><span data-stu-id="a366b-135">v4</span></span>| <span data-ttu-id="a366b-136">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="a366b-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="a366b-137"> [py-auth-sample でのボット認証][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="a366b-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="a366b-138">v4</span><span class="sxs-lookup"><span data-stu-id="a366b-138">v4</span></span> | <span data-ttu-id="a366b-139">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="a366b-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="a366b-140">リソース グループを作成する</span><span class="sxs-lookup"><span data-stu-id="a366b-140">Create the resource group</span></span>

<span data-ttu-id="a366b-141">リソース グループとサービス プランは厳密には必要ありませんが、作成したリソースを簡単に解放できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="a366b-142">これは、リソースを整理して管理し続ける場合の良い方法です。</span><span class="sxs-lookup"><span data-stu-id="a366b-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="a366b-143">リソース グループを使用して、ボット フレームワークの個々のリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="a366b-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="a366b-144">パフォーマンスを向上するには、これらのリソースが同じ Azure 地域に含めらされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="a366b-145">ブラウザーで、Azure portal に [**サインインします**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="a366b-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="a366b-146">左側のナビゲーション パネルで、[リソース グループ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="a366b-147">表示されるウィンドウの左上にある [追加] タブを **選択して、** 新しいリソース グループを作成します。</span><span class="sxs-lookup"><span data-stu-id="a366b-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="a366b-148">次の情報を入力するように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="a366b-149">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="a366b-149">**Subscription**.</span></span> <span data-ttu-id="a366b-150">既存のサブスクリプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="a366b-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="a366b-151">**リソース グループ**。</span><span class="sxs-lookup"><span data-stu-id="a366b-151">**Resource group**.</span></span> <span data-ttu-id="a366b-152">リソース グループの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-152">Enter the name for the resource group.</span></span> <span data-ttu-id="a366b-153">たとえば  *、TeamsResourceGroup です*。</span><span class="sxs-lookup"><span data-stu-id="a366b-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="a366b-154">名前は一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="a366b-155">[地域 **] ドロップダウン** メニューから、[ *米国* 西部] またはアプリケーションに近い地域を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="a366b-156">[レビューと **作成] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-156">Select the **Review and create** button.</span></span> <span data-ttu-id="a366b-157">検証が渡されたというバナーが *表示されます*。</span><span class="sxs-lookup"><span data-stu-id="a366b-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="a366b-158">[作成] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-158">Select the **Create** button.</span></span> <span data-ttu-id="a366b-159">リソース グループの作成に数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="a366b-160">このチュートリアルの後半で作成するリソースと同様に、このリソース グループをダッシュボードにピン留めして簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a366b-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="a366b-161">これを行う場合は、ピン アイコンを選択&#128204。をダッシュボードの右上に表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="a366b-162">サービス プランの作成</span><span class="sxs-lookup"><span data-stu-id="a366b-162">Create the service plan</span></span>

1. <span data-ttu-id="a366b-163">Azure portal [**の左側の**][azure-portal]ナビゲーション パネルで、[リソースの作成 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="a366b-164">検索ボックスに *「App Service Plan」と入力します*。</span><span class="sxs-lookup"><span data-stu-id="a366b-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="a366b-165">検索結果から **[App Service プラン** ] カードを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="a366b-166">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-166">Select **Create**.</span></span>
1. <span data-ttu-id="a366b-167">次の情報の入力を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="a366b-168">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="a366b-168">**Subscription**.</span></span> <span data-ttu-id="a366b-169">既存のサブスクリプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="a366b-170">**リソース グループ**。</span><span class="sxs-lookup"><span data-stu-id="a366b-170">**Resource Group**.</span></span> <span data-ttu-id="a366b-171">前に作成したグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="a366b-172">**Name**.</span><span class="sxs-lookup"><span data-stu-id="a366b-172">**Name**.</span></span> <span data-ttu-id="a366b-173">サービス プランの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-173">Enter the name for the service plan.</span></span> <span data-ttu-id="a366b-174">たとえば  *、TeamsServicePlan です*。</span><span class="sxs-lookup"><span data-stu-id="a366b-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="a366b-175">名前はグループ内で一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="a366b-176">**オペレーティング システム**.</span><span class="sxs-lookup"><span data-stu-id="a366b-176">**Operating System**.</span></span> <span data-ttu-id="a366b-177">*[Windows* または該当する OS] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="a366b-178">**地域**.</span><span class="sxs-lookup"><span data-stu-id="a366b-178">**Region**.</span></span> <span data-ttu-id="a366b-179">[ *米国西部]* またはアプリケーションに近い地域を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="a366b-180">**価格レベル**.</span><span class="sxs-lookup"><span data-stu-id="a366b-180">**Pricing Tier**.</span></span> <span data-ttu-id="a366b-181">[標準 *S1] が選択* されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="a366b-182">これは既定値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-182">This should be the default value.</span></span>
    1. <span data-ttu-id="a366b-183">[レビューと **作成] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-183">Select the **Review and create** button.</span></span> <span data-ttu-id="a366b-184">検証が渡されたというバナーが *表示されます*。</span><span class="sxs-lookup"><span data-stu-id="a366b-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="a366b-185">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-185">Select **Create**.</span></span> <span data-ttu-id="a366b-186">アプリ サービス プランの作成に数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="a366b-187">計画はリソース グループに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="a366b-188">ボット チャネルの登録を作成する</span><span class="sxs-lookup"><span data-stu-id="a366b-188">Create the bot channels registration</span></span>

<span data-ttu-id="a366b-189">Microsoft App Id とアプリ パスワード (クライアント シークレット) がある場合は、ボット チャネル登録によって Web サービスがボット フレームワークにボットとして登録されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a366b-190">ボットが Azure でホストされていない場合にのみ、ボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="a366b-191">Azure ポータル [を使用して](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) ボットを作成した場合、そのボットは既にサービスに登録されています。</span><span class="sxs-lookup"><span data-stu-id="a366b-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="a366b-192">ボット フレームワークまたは[AppStudio](~/concepts/build-and-test/app-studio-overview.md)を使用してボットを作成した場合、ボットは Azure に登録されません。 [](https://dev.botframework.com/bots/new)</span><span class="sxs-lookup"><span data-stu-id="a366b-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="a366b-193">[ボット チャネル登録] リソースには、米国西部を **選択** した場合でもグローバル地域が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="a366b-194">これは正常な動作です。</span><span class="sxs-lookup"><span data-stu-id="a366b-194">This is expected.</span></span>

<span data-ttu-id="a366b-195">詳細については、「Create [a bot for Teams」 を参照してください](../create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="a366b-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="a366b-196">ID プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="a366b-196">Create the identity provider</span></span>

<span data-ttu-id="a366b-197">認証に使用できる ID プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="a366b-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="a366b-198">この手順では、Azure プロバイダーを使用ADします。他の Azure ADサポートされている ID プロバイダーも使用できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="a366b-199">Azure portal [**で、**][azure-portal]左側のナビゲーション パネルで 、[次 **へ]** を選択Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="a366b-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="a366b-200">この Azure AD リソースを作成して、アプリケーションから要求されたアクセス許可を委任する同意を得る必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="a366b-201">テナントの作成方法については、「ポータルにアクセスしてテナントを作成 [する」を参照してください](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)。</span><span class="sxs-lookup"><span data-stu-id="a366b-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="a366b-202">左側のパネルで、[アプリの登録 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="a366b-203">右側のパネルで、左上の **[新規登録** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="a366b-204">次の情報の入力を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="a366b-205">**Name**.</span><span class="sxs-lookup"><span data-stu-id="a366b-205">**Name**.</span></span> <span data-ttu-id="a366b-206">アプリケーションの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-206">Enter the name for the application.</span></span> <span data-ttu-id="a366b-207">たとえば  *、BotTeamsIdentity を指定できます*。</span><span class="sxs-lookup"><span data-stu-id="a366b-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="a366b-208">名前は一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="a366b-209">アプリケーションの **[サポートされているアカウントの種類** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="a366b-210">任意 *の組織ディレクトリ (Any Azure AD ディレクトリ - Multitenant)* と個人用 Microsoft アカウント (Xbox など) で [アカウント] を選択します (Skype など)。</span><span class="sxs-lookup"><span data-stu-id="a366b-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="a366b-211">リダイレクト **URI の場合**:</span><span class="sxs-lookup"><span data-stu-id="a366b-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="a366b-212">&#x2713;Web を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="a366b-213">&#x2713; URL をに設定します `https://token.botframework.com/.auth/web/redirect` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="a366b-214">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-214">Select **Register**.</span></span>

1. <span data-ttu-id="a366b-215">アプリが作成されると、アプリの **[概要** ] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="a366b-216">次の情報をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="a366b-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="a366b-217">アプリケーション **(クライアント) の ID** 値。</span><span class="sxs-lookup"><span data-stu-id="a366b-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="a366b-218">この Azure ID アプリケーションをボットに登録する場合は、後でクライアント *ID* としてこの値を使用します。</span><span class="sxs-lookup"><span data-stu-id="a366b-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="a366b-219">ディレクトリ **(テナント) ID** の値。</span><span class="sxs-lookup"><span data-stu-id="a366b-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="a366b-220">この値は、後でテナント ID として使用して、この Azure *ID* アプリケーションをボットに登録します。</span><span class="sxs-lookup"><span data-stu-id="a366b-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="a366b-221">左側のパネルで、[証明書] & **を選択して** 、アプリケーションのクライアント シークレットを作成します。</span><span class="sxs-lookup"><span data-stu-id="a366b-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="a366b-222">[ **クライアント シークレット] で**、[新しい&#x2795; **シークレット] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="a366b-223">このアプリ用に作成する必要がある他のユーザーからこのシークレットを識別するための説明を追加します 。たとえば、ボット *ID* アプリは Teams。</span><span class="sxs-lookup"><span data-stu-id="a366b-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="a366b-224">[ **有効期限] を選択** に設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="a366b-225">**[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-225">Select **Add**.</span></span>
   1. <span data-ttu-id="a366b-226">このページを離れる前に、 **シークレットを記録します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="a366b-227">この値は、Azure アプリケーションをボットに登録するときに、後でクライアント AD使用します。</span><span class="sxs-lookup"><span data-stu-id="a366b-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="a366b-228">ID プロバイダー接続を構成し、ボットに登録する</span><span class="sxs-lookup"><span data-stu-id="a366b-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="a366b-229">注:Service Providers here-Azure v1 と Azure AD V2 には 2 ADがあります。</span><span class="sxs-lookup"><span data-stu-id="a366b-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="a366b-230">2 つのプロバイダー間の違いについては、[](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)ここで要約しますが、一般に、V2 はボットのアクセス許可の変更に関して柔軟性を提供します。</span><span class="sxs-lookup"><span data-stu-id="a366b-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="a366b-231">GraphAPI アクセス許可は [スコープ] フィールドに一覧表示され、新しいアクセス許可が追加されるに合って、ボットはユーザーが次のサインインで新しいアクセス許可に同意できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="a366b-232">V1 の場合、OAuth ダイアログで新しいアクセス許可を求めるには、ボットの同意をユーザーが削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="a366b-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="a366b-233">Azure AD V1</span></span>

1. <span data-ttu-id="a366b-234">Azure portal [**で、**][azure-portal]ダッシュボードからリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="a366b-235">ボット チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="a366b-236">リソース ページを開き、[構成] の下の [**構成]** **を設定。**</span><span class="sxs-lookup"><span data-stu-id="a366b-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="a366b-237">**[OAuth 接続の追加] を設定。**</span><span class="sxs-lookup"><span data-stu-id="a366b-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="a366b-238">次の図は、リソース ページで対応する選択内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="a366b-239">![SampleAppDemoBot 構成](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="a366b-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="a366b-240">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="a366b-241">**Name**.</span><span class="sxs-lookup"><span data-stu-id="a366b-241">**Name**.</span></span> <span data-ttu-id="a366b-242">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-242">Enter a name for the connection.</span></span> <span data-ttu-id="a366b-243">この名前は、ファイル内のボットで使用 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="a366b-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="a366b-244">たとえば *、BotTeamsAuthADv1 .*</span><span class="sxs-lookup"><span data-stu-id="a366b-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="a366b-245">**サービス プロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="a366b-245">**Service Provider**.</span></span> <span data-ttu-id="a366b-246">[**Azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="a366b-247">これを選択すると、Azure AD固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="a366b-248">**クライアント ID**。上記の手順で、Azure ID プロバイダー アプリに記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="a366b-249">**クライアント シークレット**。</span><span class="sxs-lookup"><span data-stu-id="a366b-249">**Client secret**.</span></span> <span data-ttu-id="a366b-250">上記の手順で、Azure ID プロバイダー アプリに記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="a366b-251">**Grant Type**.</span><span class="sxs-lookup"><span data-stu-id="a366b-251">**Grant Type**.</span></span> <span data-ttu-id="a366b-252">を `authorization_code` 入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="a366b-253">**ログイン URL**。</span><span class="sxs-lookup"><span data-stu-id="a366b-253">**Login URL**.</span></span> <span data-ttu-id="a366b-254">を `https://login.microsoftonline.com` 入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="a366b-255">**テナント ID** は、Id プロバイダー アプリの作成時に選択されたサポートされているアカウントの種類に応じて、Azure ID アプリまたは共通の前に記録したディレクトリ **(テナント) ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="a366b-256">割り当てる値を決定するには、次の条件に従います。</span><span class="sxs-lookup"><span data-stu-id="a366b-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="a366b-257">この組織ディレクトリ内の [アカウントのみ] *(Microsoft のみ - シングル* テナント) または任意の組織ディレクトリの [アカウント] *(Microsoft AAD ディレクトリ - マルチ* テナント) のいずれかを選択した場合は、AAD アプリ用に前に記録したテナント **ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="a366b-258">これは、認証できるユーザーに関連付けられたテナントになります。</span><span class="sxs-lookup"><span data-stu-id="a366b-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="a366b-259">任意の組織ディレクトリで [アカウント] を選択した場合 (任意の AAD ディレクトリ - マルチ テナントアカウントと個人 Microsoft アカウント *(Skype、Xbox、Outlook など)* は、テナント ID の代わりに共通という単語を入力します。 </span><span class="sxs-lookup"><span data-stu-id="a366b-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="a366b-260">それ以外の場合、AAD アプリは ID が選択されたテナントを通じて確認し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="a366b-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="a366b-261">h.</span><span class="sxs-lookup"><span data-stu-id="a366b-261">h.</span></span> <span data-ttu-id="a366b-262">[ **リソース URL]** に、 を入力します `https://graph.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="a366b-263">これは、現在のコード サンプルでは使用されません。</span><span class="sxs-lookup"><span data-stu-id="a366b-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="a366b-264">i.</span><span class="sxs-lookup"><span data-stu-id="a366b-264">i.</span></span> <span data-ttu-id="a366b-265">[ **スコープ] は空白** のままにします。</span><span class="sxs-lookup"><span data-stu-id="a366b-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="a366b-266">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-266">The following image is an example:</span></span>

    ![teams bots アプリの認証接続文字列 adv1 ビュー](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="a366b-268">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="a366b-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="a366b-269">Azure AD V2</span></span>

1. <span data-ttu-id="a366b-270">Azure portal [**で、**][azure-portal]ダッシュボードからリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="a366b-271">ボット チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="a366b-272">リソース ページを開き、[構成] の下の [**構成]** **を設定。**</span><span class="sxs-lookup"><span data-stu-id="a366b-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="a366b-273">**[OAuth 接続の追加] を設定。**</span><span class="sxs-lookup"><span data-stu-id="a366b-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="a366b-274">次の図は、リソース ページで対応する選択内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="a366b-275">![SampleAppDemoBot 構成](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="a366b-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="a366b-276">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="a366b-277">**Name**.</span><span class="sxs-lookup"><span data-stu-id="a366b-277">**Name**.</span></span> <span data-ttu-id="a366b-278">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-278">Enter a name for the connection.</span></span> <span data-ttu-id="a366b-279">この名前は、ファイル内のボットで使用 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="a366b-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="a366b-280">たとえば *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="a366b-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="a366b-281">**サービス プロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="a366b-281">**Service Provider**.</span></span> <span data-ttu-id="a366b-282">v2 **Azure Active Directoryを選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="a366b-283">これを選択すると、Azure AD固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="a366b-284">**クライアント ID**。上記の手順で、Azure ID プロバイダー アプリに記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="a366b-285">**クライアント シークレット**。</span><span class="sxs-lookup"><span data-stu-id="a366b-285">**Client secret**.</span></span> <span data-ttu-id="a366b-286">上記の手順で、Azure ID プロバイダー アプリに記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="a366b-287">**トークンExchange URL**。</span><span class="sxs-lookup"><span data-stu-id="a366b-287">**Token Exchange URL**.</span></span> <span data-ttu-id="a366b-288">空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="a366b-288">Leave this blank.</span></span>
    1. <span data-ttu-id="a366b-289">**テナント ID** は、Id プロバイダー アプリの作成時に選択されたサポートされているアカウントの種類に応じて、Azure ID アプリまたは共通の前に記録したディレクトリ **(テナント) ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="a366b-290">割り当てる値を決定するには、次の条件に従います。</span><span class="sxs-lookup"><span data-stu-id="a366b-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="a366b-291">この組織ディレクトリ内の [アカウントのみ] *(Microsoft のみ - シングル* テナント) または任意の組織ディレクトリの [アカウント] *(Microsoft AAD ディレクトリ - マルチ* テナント) のいずれかを選択した場合は、AAD アプリ用に前に記録したテナント **ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="a366b-292">これは、認証できるユーザーに関連付けられたテナントになります。</span><span class="sxs-lookup"><span data-stu-id="a366b-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="a366b-293">任意の組織ディレクトリで [アカウント] を選択した場合 (任意の AAD ディレクトリ - マルチ テナントアカウントと個人 Microsoft アカウント *(Skype、Xbox、Outlook など)* は、テナント ID の代わりに共通という単語を入力します。 </span><span class="sxs-lookup"><span data-stu-id="a366b-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="a366b-294">それ以外の場合、AAD アプリは ID が選択されたテナントを通じて確認し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="a366b-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="a366b-295">[ **スコープ]** に、このアプリケーションで必要なグラフのアクセス許可のスペースで区切られたリストを入力します。User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="a366b-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="a366b-296">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="a366b-297">接続をテストする</span><span class="sxs-lookup"><span data-stu-id="a366b-297">Test the connection</span></span>

1. <span data-ttu-id="a366b-298">接続エントリを選択して、作成した接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="a366b-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="a366b-299">[ **サービス プロバイダーの接続設定** ] パネルの上部にある **[接続のテスト] を選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="a366b-300">これを初めて実行すると、アカウントの選択を求める新しいブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="a366b-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="a366b-301">使用する 1 つを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="a366b-302">次に、ID プロバイダーにデータ (資格情報) の使用を許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="a366b-303">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-303">The following image is an example:</span></span>

    ![teams bot auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="a366b-305">**[同意する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-305">Select **Accept**.</span></span>
1. <span data-ttu-id="a366b-306">その後、テスト接続を **[成功] ページ \<your-connection-name> にリダイレクト** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="a366b-307">エラーが発生した場合は、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="a366b-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="a366b-308">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-308">The following image is an example:</span></span>

  ![teams bots アプリの認証接続 str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="a366b-310">接続名は、ボット コードによってユーザー認証トークンを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="a366b-311">ボットのサンプル コードを準備する</span><span class="sxs-lookup"><span data-stu-id="a366b-311">Prepare the bot sample code</span></span>

<span data-ttu-id="a366b-312">事前設定が完了したら、この記事で使用するボットの作成に注目します。</span><span class="sxs-lookup"><span data-stu-id="a366b-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="a366b-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a366b-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="a366b-314">[cs-auth-sample のクローンを作成します][teams-auth-bot-cs]。</span><span class="sxs-lookup"><span data-stu-id="a366b-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="a366b-315">起動Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a366b-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="a366b-316">ツール バーの [ファイル] **->を開く -> Project/ソリューション**] を選択し、ボット プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="a366b-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="a366b-317">[C#更新 **appsettings.js次のように** オンにします。</span><span class="sxs-lookup"><span data-stu-id="a366b-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="a366b-318">ボット `ConnectionName` チャネル登録に追加した ID プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="a366b-319">この例で使用した名前は *BotTeamsAuthADv1 です*。</span><span class="sxs-lookup"><span data-stu-id="a366b-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="a366b-320">ボット `MicrosoftAppId` チャネル **登録時に** 保存したボット アプリ ID に設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="a366b-321">ボット `MicrosoftAppPassword` チャネル登録 **時に** 保存した顧客シークレットに設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="a366b-322">ボット シークレットの文字によっては、XML でパスワードをエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="a366b-323">たとえば、アンパサンド (&) はとしてエンコードする必要があります `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="a366b-324">ソリューション エクスプローラーで、フォルダーに移動し、ボット チャネル登録時に保存したボット アプリ ID を `TeamsAppManifest` `manifest.json` 開いて `id` `botId` 設定します。 </span><span class="sxs-lookup"><span data-stu-id="a366b-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="a366b-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a366b-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="a366b-326">ノード [の複製-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="a366b-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="a366b-327">コンソールで、プロジェクトに移動します。</span><span class="sxs-lookup"><span data-stu-id="a366b-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="a366b-328">モジュールのインストール</span><span class="sxs-lookup"><span data-stu-id="a366b-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="a366b-329">**.env 構成を次** のように更新します。</span><span class="sxs-lookup"><span data-stu-id="a366b-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="a366b-330">ボット `MicrosoftAppId` チャネル **登録時に** 保存したボット アプリ ID に設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="a366b-331">ボット `MicrosoftAppPassword` チャネル登録 **時に** 保存した顧客シークレットに設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="a366b-332">id プロバイダー `connectionName` 接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="a366b-333">ボット シークレットの文字によっては、XML でパスワードをエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="a366b-334">たとえば、アンパサンド (&) はとしてエンコードする必要があります `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="a366b-335">フォルダーで、Microsoft App ID とボット チャネル登録時に保存したボット アプリ ID を開いて `teamsAppManifest` `manifest.json` `id`  `botId` 設定します。 </span><span class="sxs-lookup"><span data-stu-id="a366b-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="a366b-336">Python</span><span class="sxs-lookup"><span data-stu-id="a366b-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="a366b-337">github [リポジトリから py-auth-sample][teams-auth-bot-py] を複製します。</span><span class="sxs-lookup"><span data-stu-id="a366b-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="a366b-338">更新 **config.py:**</span><span class="sxs-lookup"><span data-stu-id="a366b-338">Update **config.py**:</span></span>

    - <span data-ttu-id="a366b-339">ボット `ConnectionName` に追加した OAuth 接続設定の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="a366b-340">ボット `MicrosoftAppId` の `MicrosoftAppPassword` アプリ ID とアプリ シークレットを設定します。</span><span class="sxs-lookup"><span data-stu-id="a366b-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="a366b-341">ボット シークレットの文字によっては、XML でパスワードをエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="a366b-342">たとえば、アンパサンド (&) はとしてエンコードする必要があります `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="a366b-343">ボットを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="a366b-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="a366b-344">ボットを展開するには、「Azure にボットを展開する方法」 [の手順に従います](https://aka.ms/azure-bot-deployment-cli)。</span><span class="sxs-lookup"><span data-stu-id="a366b-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="a366b-345">または、次のVisual Studioを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="a366b-346">[Visual Studio *エクスプローラーで*、プロジェクト名を選択したまま (または右クリック) します。</span><span class="sxs-lookup"><span data-stu-id="a366b-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="a366b-347">ドロップダウン メニューで、[発行] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="a366b-348">表示されたウィンドウで、[新規] リンク **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="a366b-349">ダイアログ ウィンドウで、左側の **[App Service]** を選択し、右側 **の [新しい作成** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="a366b-350">[発行] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="a366b-351">次のダイアログ ウィンドウで、必要な情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="a366b-352">例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-352">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="a366b-354">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-354">Select **Create**.</span></span>
1. <span data-ttu-id="a366b-355">展開が正常に完了した場合は、展開がサーバーに反映Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a366b-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="a366b-356">さらに、既定のブラウザーに、ボットの準備が完了した *というページが表示されます*。</span><span class="sxs-lookup"><span data-stu-id="a366b-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="a366b-357">URL は次に似ています `https://botteamsauth.azurewebsites.net/` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="a366b-358">ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="a366b-358">Save it to a file.</span></span>
1. <span data-ttu-id="a366b-359">ブラウザーで、Azure portal に [**移動します**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="a366b-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="a366b-360">リソース グループを確認すると、ボットが他のリソースと共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="a366b-361">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-361">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="a366b-363">リソース グループで、ボット チャネル登録名 (リンク) を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="a366b-364">左側のパネルで、[次へ]**を設定。**</span><span class="sxs-lookup"><span data-stu-id="a366b-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="a366b-365">[メッセージング **エンドポイント] ボックスに** 、上記で取得した URL を入力し、その後に `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="a366b-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="a366b-366">次に例を示します `https://botteamsauth.azurewebsites.net/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="a366b-367">左上の **[保存** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="a366b-368">エミュレーターを使用してボットをテストする</span><span class="sxs-lookup"><span data-stu-id="a366b-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="a366b-369">まだ実行していない場合は、インストール[済みの](https://aka.ms/bot-framework-emulator-readme)Microsoft Bot Framework Emulator。</span><span class="sxs-lookup"><span data-stu-id="a366b-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="a366b-370">「エミュレーター [を使用したデバッグ」も参照してください](https://aka.ms/bot-framework-emulator-debug-with-emulator)。</span><span class="sxs-lookup"><span data-stu-id="a366b-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="a366b-371">ボット サンプル ログインを機能するには、次に示すようにエミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-371">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="a366b-372">認証用にエミュレーターを構成する</span><span class="sxs-lookup"><span data-stu-id="a366b-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="a366b-373">ボットで認証が必要な場合は、次に示すようにエミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-373">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="a366b-374">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="a366b-374">Start the Emulator.</span></span>
1. <span data-ttu-id="a366b-375">エミュレーターで、左下の歯車&#9881;、右上の [エミュレーター]**設定を選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-375">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="a366b-376">[バージョン **1.0 認証トークンを使用する] のチェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="a366b-376">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="a366b-377">ngrok ツールへのローカル **パスを入力** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-377">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="a366b-378">*詳細については*、Bot Framework Emulator/ngrok トンネリング統合 Wiki を [参照してください](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))。</span><span class="sxs-lookup"><span data-stu-id="a366b-378">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="a366b-379">ツールの詳細については [、「ngrok」を参照してください](https://ngrok.com/)。</span><span class="sxs-lookup"><span data-stu-id="a366b-379">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="a366b-380">エミュレーターの起動時に **ngrok を実行してチェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="a366b-380">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="a366b-381">[保存] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-381">Select the **Save** button.</span></span>

<span data-ttu-id="a366b-382">ボットがサインイン カードを表示し、ユーザーがサインイン ボタンを選択すると、エミュレーターは、ユーザーが認証プロバイダーでサインインするために使用できるページを開きます。</span><span class="sxs-lookup"><span data-stu-id="a366b-382">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="a366b-383">ユーザーがそうすると、プロバイダーはユーザー トークンを生成し、ボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="a366b-383">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="a366b-384">その後、ボットはユーザーに代わって行動できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-384">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="a366b-385">ボットをローカルでテストする</span><span class="sxs-lookup"><span data-stu-id="a366b-385">Test the bot locally</span></span>

<span data-ttu-id="a366b-386">認証メカニズムを構成した後、実際のボット テストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-386">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="a366b-387">たとえば、コンピューターでボット サンプルをローカルで実行Visual Studio実行します。</span><span class="sxs-lookup"><span data-stu-id="a366b-387">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="a366b-388">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="a366b-388">Start the Emulator.</span></span>
1. <span data-ttu-id="a366b-389">[ボットを **開く] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-389">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="a366b-390">ボットの **URL に**、ボットのローカル URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-390">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="a366b-391">通常 `http://localhost:3978/api/messages` 、.</span><span class="sxs-lookup"><span data-stu-id="a366b-391">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="a366b-392">Microsoft App **ID に、ボット** のアプリ ID を入力します `appsettings.json` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-392">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="a366b-393">Microsoft App **のパスワードで、** からボットのアプリ パスワードを入力 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="a366b-393">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="a366b-394">[Connect]**を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-394">Select **Connect**.</span></span>
1. <span data-ttu-id="a366b-395">ボットが稼働した後、任意のテキストを入力してサインイン カードを表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-395">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="a366b-396">**[サインイン]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-396">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="a366b-397">[開く URL の確認] にポップアップ **ダイアログが表示されます**。</span><span class="sxs-lookup"><span data-stu-id="a366b-397">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="a366b-398">これは、ボットのユーザー (ユーザー) が認証を許可するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-398">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="a366b-399">**[確認]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-399">Select **Confirm**.</span></span>
1. <span data-ttu-id="a366b-400">確認された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-400">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="a366b-401">エミュレーターに使用した構成に応じて、次のいずれかを取得します。</span><span class="sxs-lookup"><span data-stu-id="a366b-401">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="a366b-402">**サインイン検証コードの使用**</span><span class="sxs-lookup"><span data-stu-id="a366b-402">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="a366b-403">&#x2713;検証コードを表示するウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="a366b-403">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="a366b-404">&#x2713;入力規則コードをコピーしてチャット ボックスに入力し、サインインを完了します。</span><span class="sxs-lookup"><span data-stu-id="a366b-404">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="a366b-405">**認証トークンの使用**.</span><span class="sxs-lookup"><span data-stu-id="a366b-405">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="a366b-406">&#x2713;資格情報に基づいてログインしています。</span><span class="sxs-lookup"><span data-stu-id="a366b-406">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="a366b-407">次の図は、ログインした後のボット UI の例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-407">The following image is an example of the bot UI after you've logged in:</span></span>

    ![認証ボットのログイン エミュレーター](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="a366b-409">ボットが要求 **するときに [は** い] を選択した場合、トークンを表示しますか *?* を選択すると、次のような応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-409">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![認証ボットのログイン エミュレーター トークン](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="a366b-411">入力 **チャット ボックスに** ログアウトと入力してサインアウトします。これにより、ユーザー トークンが解放され、再度サインインするまでボットは代理で動作できません。</span><span class="sxs-lookup"><span data-stu-id="a366b-411">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="a366b-412">ボット認証では、ボット コネクタ サービス **を使用する必要があります**。</span><span class="sxs-lookup"><span data-stu-id="a366b-412">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="a366b-413">サービスは、ボットのボット チャネル登録情報にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="a366b-413">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="a366b-414">展開されたボットをテストする</span><span class="sxs-lookup"><span data-stu-id="a366b-414">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="a366b-415">ブラウザーで、Azure portal に [**移動します**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="a366b-415">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="a366b-416">リソース グループを検索します。</span><span class="sxs-lookup"><span data-stu-id="a366b-416">Find your resource group.</span></span>
1. <span data-ttu-id="a366b-417">リソース リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-417">Select the resource link.</span></span> <span data-ttu-id="a366b-418">リソース ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-418">The resource page is displayed.</span></span>
1. <span data-ttu-id="a366b-419">リソース ページで、[Web チャットで **テスト] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-419">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="a366b-420">ボットは、定義済みの案内応答を開始して表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-420">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="a366b-421">チャット ボックスに何かを入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-421">Type anything in the chat box.</span></span>
1. <span data-ttu-id="a366b-422">[サインイン **] ボックスを選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-422">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="a366b-423">[開く URL の確認] にポップアップ **ダイアログが表示されます**。</span><span class="sxs-lookup"><span data-stu-id="a366b-423">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="a366b-424">これは、ボットのユーザー (ユーザー) が認証を許可するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-424">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="a366b-425">**[確認]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-425">Select **Confirm**.</span></span>
1. <span data-ttu-id="a366b-426">確認された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-426">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="a366b-427">次の図は、ログインした後のボット UI の例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-427">The following image is an example of the bot UI after you have logged in:</span></span>

    ![auth bot login deployed](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="a366b-429">.</span><span class="sxs-lookup"><span data-stu-id="a366b-429">.</span></span>

1. <span data-ttu-id="a366b-430">[はい **] ボタン** を選択して認証トークンを表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-430">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="a366b-431">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-431">The following image is an example:</span></span>

    ![認証ボット のログイン展開トークン](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="a366b-433">.</span><span class="sxs-lookup"><span data-stu-id="a366b-433">.</span></span>

1. <span data-ttu-id="a366b-434">ログアウトを入力してサインアウトします。</span><span class="sxs-lookup"><span data-stu-id="a366b-434">Enter logout to sign out.</span></span>

    ![認証ボットが展開したログアウト](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="a366b-436">サインインに問題がある場合は、前の手順で説明したように、もう一度接続をテストしてみてください。</span><span class="sxs-lookup"><span data-stu-id="a366b-436">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="a366b-437">これにより、認証トークンが再作成される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-437">This could recreate the authentication token.</span></span>
> <span data-ttu-id="a366b-438">Azure のボット フレームワーク Web チャット クライアントでは、認証が正しく確立される前に何度かサインインする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-438">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="a366b-439">ボットをインストールしてテストTeams</span><span class="sxs-lookup"><span data-stu-id="a366b-439">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="a366b-440">ボット プロジェクトで、フォルダーにファイルと共に `TeamsAppManifest` `manifest.json` フォルダーが含まれているか `outline.png` 確認 `color.png` します。</span><span class="sxs-lookup"><span data-stu-id="a366b-440">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="a366b-441">ソリューション エクスプローラーで、フォルダーに移動 `TeamsAppManifest` します。</span><span class="sxs-lookup"><span data-stu-id="a366b-441">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="a366b-442">次の `manifest.json` 値を割り当て、編集します。</span><span class="sxs-lookup"><span data-stu-id="a366b-442">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="a366b-443">ボット チャネル登録 **時に受信** したボット アプリ ID がに割り当てられているか確認 `id` します `botId` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-443">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="a366b-444">この値を割り `validDomains: [ "token.botframework.com" ]` 当てる。</span><span class="sxs-lookup"><span data-stu-id="a366b-444">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="a366b-445">、および **ファイルを** `manifest.json` 選択 `outline.png` して `color.png` 圧縮します。</span><span class="sxs-lookup"><span data-stu-id="a366b-445">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="a366b-446">[ファイル **Microsoft Teams] を開きます**。</span><span class="sxs-lookup"><span data-stu-id="a366b-446">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="a366b-447">左側のパネルで、下部にある [アプリ] アイコン **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-447">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="a366b-448">右側のパネルの下部で、カスタム アプリアップロード **選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-448">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="a366b-449">フォルダーに移動 `TeamsAppManifest` し、圧縮されたマニフェストをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="a366b-449">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="a366b-450">次のウィザードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-450">The following wizard is displayed:</span></span>

    ![認証ボット チームのアップロード](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="a366b-452">**[チームに追加]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-452">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="a366b-453">次のウィンドウで、ボットを使用するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-453">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="a366b-454">[ボットの **セットアップ] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="a366b-454">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="a366b-455">左側のパネルで 3 つのドット (&#x25cf;&#x25cf;&#x25cf;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-455">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="a366b-456">次に **、[App Studio] アイコンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="a366b-456">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="a366b-457">[マニフェスト エディター **] タブを** 選択します。アップロードしたボットのアイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-457">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="a366b-458">また、ボットとメッセージを交換するために使用できるチャット リストに、連絡先として一覧表示されているボットを確認できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-458">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="a366b-459">ローカルでボットをテストTeams</span><span class="sxs-lookup"><span data-stu-id="a366b-459">Testing the bot locally in Teams</span></span>

<span data-ttu-id="a366b-460">Microsoft Teams完全にクラウドベースの製品である場合、HTTPS エンドポイントを使用してアクセスするサービスはすべてクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-460">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="a366b-461">したがって、ボット (サンプル) が Teams で動作するには、コードを選択したクラウドに発行するか、トンネリング ツールを介してローカルで実行中のインスタンスに外部からアクセス可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-461">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="a366b-462">コンピューターで  [ローカルで開](https://ngrok.com/download)くポートの外部アドレス指定可能な URL を作成する ngrok をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a366b-462">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="a366b-463">アプリをローカルで実行する準備として ngrok をMicrosoft Teamsするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="a366b-463">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="a366b-464">ターミナル ウィンドウで、インストールしたディレクトリに移動 `ngrok.exe` します。</span><span class="sxs-lookup"><span data-stu-id="a366b-464">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="a366b-465">環境変数のパスを *ポイントする* 設定をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a366b-465">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="a366b-466">たとえば、実行します `ngrok http 3978 --host-header=localhost:3978` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-466">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="a366b-467">必要に応じてポート番号を置き換える。</span><span class="sxs-lookup"><span data-stu-id="a366b-467">Replace the port number as needed.</span></span>
<span data-ttu-id="a366b-468">これにより、ngrok が起動して、指定したポートでリッスンします。</span><span class="sxs-lookup"><span data-stu-id="a366b-468">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="a366b-469">その代り、ngrok が実行されている限り有効な外部アドレス指定可能な URL が提供されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-469">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="a366b-470">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-470">The following image is an example:</span></span>

    ![teams ボット アプリ認証接続文字列 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="a366b-472">.</span><span class="sxs-lookup"><span data-stu-id="a366b-472">.</span></span>

1. <span data-ttu-id="a366b-473">転送 HTTPS アドレスをコピーします。</span><span class="sxs-lookup"><span data-stu-id="a366b-473">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="a366b-474">これは、次のようになります `https://dea822bf.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-474">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="a366b-475">取得 `/api/messages` するには、追加 `https://dea822bf.ngrok.io/api/messages` します。</span><span class="sxs-lookup"><span data-stu-id="a366b-475">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="a366b-476">これは、**コンピューター上でローカル** に実行され、コンピューター内のチャットで web を使用して到達可能なボットのメッセージ エンドポイントMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="a366b-476">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="a366b-477">実行する最後の手順の 1 つは、展開されたボットのメッセージ エンドポイントを更新する方法です。</span><span class="sxs-lookup"><span data-stu-id="a366b-477">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="a366b-478">この例では、Azure にボットを展開しました。</span><span class="sxs-lookup"><span data-stu-id="a366b-478">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="a366b-479">次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="a366b-479">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="a366b-480">ブラウザーで Azure portal に [**移動します**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="a366b-480">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="a366b-481">ボット チャネル **登録を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a366b-481">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="a366b-482">左側のパネルで、[次へ]**を設定。**</span><span class="sxs-lookup"><span data-stu-id="a366b-482">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="a366b-483">右側のパネルの [メッセージング **エンドポイント]** ボックスに、ngrok URL を入力します。この例では、 を入力します `https://dea822bf.ngrok.io/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="a366b-483">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="a366b-484">たとえば、デバッグ モードでボットをローカルVisual Studio開始します。</span><span class="sxs-lookup"><span data-stu-id="a366b-484">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="a366b-485">ボット フレームワーク ポータルのテスト Web チャットを使用して、ローカルで実行している間 **にボットをテストします**。</span><span class="sxs-lookup"><span data-stu-id="a366b-485">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="a366b-486">エミュレーターと同様に、このテストでは、ユーザーが特定のTeamsにアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="a366b-486">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="a366b-487">実行中のターミナル ウィンドウで、ボットと Web チャット クライアントの `ngrok` 間の HTTP トラフィックを確認できます。</span><span class="sxs-lookup"><span data-stu-id="a366b-487">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="a366b-488">より詳細なビューが必要な場合は、ブラウザー ウィンドウで、前 `http://127.0.0.1:4040` のターミナル ウィンドウから取得したと入力します。</span><span class="sxs-lookup"><span data-stu-id="a366b-488">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="a366b-489">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="a366b-489">The following image is an example:</span></span>

    ![認証ボット チーム ngrok テスト](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="a366b-491">.</span><span class="sxs-lookup"><span data-stu-id="a366b-491">.</span></span>

> [!NOTE]
> <span data-ttu-id="a366b-492">ngrok を停止して再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-492">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="a366b-493">プロジェクトで ngrok を使用するには、使用している機能に応じて、すべての URL 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a366b-493">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="a366b-494">追加情報</span><span class="sxs-lookup"><span data-stu-id="a366b-494">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="a366b-495">TeamsAppManifest/manifest.jsオン</span><span class="sxs-lookup"><span data-stu-id="a366b-495">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="a366b-496">このマニフェストには、ボットに接続するために必要Microsoft Teams情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a366b-496">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

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

<span data-ttu-id="a366b-497">認証では、Teams説明したように、他のチャネルとは若干異なる動作をします。</span><span class="sxs-lookup"><span data-stu-id="a366b-497">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="a366b-498">Invoke アクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="a366b-498">Handling Invoke Activity</span></span>

<span data-ttu-id="a366b-499">Invoke **Activity は** 、他のチャネルで使用されるイベント アクティビティではなく、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-499">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="a366b-500">これは、ActivityHandler をサブクラス **化して行います**。</span><span class="sxs-lookup"><span data-stu-id="a366b-500">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="a366b-501">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a366b-501">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="a366b-502">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="a366b-502">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="a366b-503">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="a366b-503">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="a366b-504">**OAuthPrompt** を使用する場合は、Invoke Activity をダイアログに転送する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="a366b-504">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="a366b-505">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="a366b-505">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="a366b-506">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a366b-506">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="a366b-507">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="a366b-507">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="a366b-508">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="a366b-508">**bots/teamsBot.js**</span></span>

<span data-ttu-id="a366b-509">**OAuthPrompt** を使用する場合は、Invoke Activity をダイアログに転送する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="a366b-509">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="a366b-510">**dialogs/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="a366b-510">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="a366b-511">ダイアログ ステップ内で、OAuth プロンプトを開始し、ユーザーにサインイン `beginDialog` を求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-511">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="a366b-512">ユーザーが既にサインインしている場合は、ユーザーにメッセージを表示せずにトークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-512">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="a366b-513">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-513">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="a366b-514">Azure Bot Service は、ユーザーがサインインを試みた後にトークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="a366b-514">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="a366b-515">次のダイアログ ステップで、前の手順の結果にトークンが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="a366b-515">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="a366b-516">null 以外の場合、ユーザーは正常にサインインします。</span><span class="sxs-lookup"><span data-stu-id="a366b-516">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="a366b-517">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="a366b-517">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="a366b-518">Python</span><span class="sxs-lookup"><span data-stu-id="a366b-518">Python</span></span>](#tab/python-sample)

<span data-ttu-id="a366b-519">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="a366b-519">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="a366b-520">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="a366b-520">**bots/teams_bot.py**</span></span>

<span data-ttu-id="a366b-521">**OAuthPrompt** を使用する場合は、Invoke Activity をダイアログに転送する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="a366b-521">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="a366b-522">**dialogs/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="a366b-522">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="a366b-523">ダイアログ ステップ内で、OAuth プロンプトを開始し、ユーザーにサインイン `begin_dialog` を求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="a366b-523">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="a366b-524">ユーザーが既にサインインしている場合は、ユーザーにメッセージを表示せずにトークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-524">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="a366b-525">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a366b-525">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="a366b-526">Azure Bot Service は、ユーザーがサインインを試みた後にトークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="a366b-526">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="a366b-527">次のダイアログ ステップで、前の手順の結果にトークンが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="a366b-527">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="a366b-528">null 以外の場合、ユーザーは正常にサインインします。</span><span class="sxs-lookup"><span data-stu-id="a366b-528">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="a366b-529">**dialogs/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="a366b-529">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="a366b-530">Azure Bot Service による認証の追加の詳細</span><span class="sxs-lookup"><span data-stu-id="a366b-530">Learn about adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
