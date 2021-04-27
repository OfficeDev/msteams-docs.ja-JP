---
title: Teams ボットに認証を追加する
author: clearab
description: Microsoft Teams のボットに OAuth 認証を追加する方法。
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: d54d7fadb13626bb38de3a907b966f026cc6c485
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020955"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="af781-103">Teams ボットに認証を追加する</span><span class="sxs-lookup"><span data-stu-id="af781-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="af781-104">メール サービスなど、ユーザーの代わりにリソースにアクセスできるボットを Microsoft Teams で作成する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="af781-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="af781-105">この記事では、OAuth 2.0 に基づいて Azure Bot Service v4 SDK 認証を使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="af781-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="af781-106">これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットの開発が容易になります。</span><span class="sxs-lookup"><span data-stu-id="af781-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="af781-107">このすべてで重要なのは、後で **説明** する ID プロバイダーの使用です。</span><span class="sxs-lookup"><span data-stu-id="af781-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="af781-108">OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。</span><span class="sxs-lookup"><span data-stu-id="af781-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="af781-109">OAuth 2.0 の基本的な理解は、Teams での認証を操作する前提条件です。</span><span class="sxs-lookup"><span data-stu-id="af781-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="af781-110">完全 [な仕様については、「OAuth 2 簡](https://aka.ms/oauth2-simplified) 体字」、OAuth [2.0](https://oauth.net/2/) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="af781-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="af781-111">Azure Bot Service が認証を処理する方法の詳細については、「 [会話内のユーザー認証」を参照してください](https://aka.ms/azure-bot-authentication)。</span><span class="sxs-lookup"><span data-stu-id="af781-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="af781-112">この記事では、以下について説明します。</span><span class="sxs-lookup"><span data-stu-id="af781-112">In this article you'll learn:</span></span>

- <span data-ttu-id="af781-113">**認証が有効なボットを作成する方法**。</span><span class="sxs-lookup"><span data-stu-id="af781-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="af781-114">[cs-auth-sample][teams-auth-bot-cs]を使用して、ユーザーサインイン資格情報と認証トークンの生成を処理します。</span><span class="sxs-lookup"><span data-stu-id="af781-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="af781-115">**ボットを Azure に展開し、ID プロバイダーに関連付ける方法**。</span><span class="sxs-lookup"><span data-stu-id="af781-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="af781-116">プロバイダーは、ユーザー サインイン資格情報に基づいてトークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="af781-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="af781-117">ボットはトークンを使用して、認証が必要なメール サービスなどのリソースにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="af781-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="af781-118">詳細については  [、「Microsoft Teams 認証フロー for bots」を参照してください](auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="af781-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="af781-119">**Microsoft Teams 内でボットを統合する方法**。</span><span class="sxs-lookup"><span data-stu-id="af781-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="af781-120">ボットが統合された後は、サインインしてチャットでメッセージとメッセージを交換できます。</span><span class="sxs-lookup"><span data-stu-id="af781-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af781-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="af781-121">Prerequisites</span></span>

- <span data-ttu-id="af781-122">ボットの[基本、状態][concept-basics][の管理、][concept-state]ダイアログ ライブラリ[][concept-dialogs]、および連続した会話フローの[実装方法に関する知識][simple-dialog]。</span><span class="sxs-lookup"><span data-stu-id="af781-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="af781-123">Azure と OAuth 2.0 の開発に関する知識。</span><span class="sxs-lookup"><span data-stu-id="af781-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="af781-124">現在のバージョンの Visual Studio Git。</span><span class="sxs-lookup"><span data-stu-id="af781-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="af781-125">Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="af781-125">Azure account.</span></span> <span data-ttu-id="af781-126">必要に応じて、Azure 無料アカウント [を作成できます](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="af781-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="af781-127">次のサンプル。</span><span class="sxs-lookup"><span data-stu-id="af781-127">The following sample.</span></span>

    | <span data-ttu-id="af781-128">サンプル</span><span class="sxs-lookup"><span data-stu-id="af781-128">Sample</span></span> | <span data-ttu-id="af781-129">BotBuilder のバージョン</span><span class="sxs-lookup"><span data-stu-id="af781-129">BotBuilder version</span></span> | <span data-ttu-id="af781-130">デモンストレーション</span><span class="sxs-lookup"><span data-stu-id="af781-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="af781-131"> [cs-auth-sample でのボット認証][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="af781-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="af781-132">v4</span><span class="sxs-lookup"><span data-stu-id="af781-132">v4</span></span> | <span data-ttu-id="af781-133">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="af781-133">OAuthCard support</span></span> |
    | <span data-ttu-id="af781-134"> [js-auth-sample でのボット認証][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="af781-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="af781-135">v4</span><span class="sxs-lookup"><span data-stu-id="af781-135">v4</span></span>| <span data-ttu-id="af781-136">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="af781-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="af781-137"> [py-auth-sample でのボット認証][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="af781-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="af781-138">v4</span><span class="sxs-lookup"><span data-stu-id="af781-138">v4</span></span> | <span data-ttu-id="af781-139">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="af781-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="af781-140">リソース グループを作成する</span><span class="sxs-lookup"><span data-stu-id="af781-140">Create the resource group</span></span>

<span data-ttu-id="af781-141">リソース グループとサービス プランは厳密には必要ありませんが、作成したリソースを簡単に解放できます。</span><span class="sxs-lookup"><span data-stu-id="af781-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="af781-142">これは、リソースを整理して管理し続ける場合の良い方法です。</span><span class="sxs-lookup"><span data-stu-id="af781-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="af781-143">リソース グループを使用して、ボット フレームワークの個々のリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="af781-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="af781-144">パフォーマンスを向上するには、これらのリソースが同じ Azure 地域に含めらされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="af781-145">ブラウザーで、Azure portal に [**サインインします**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="af781-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="af781-146">左側のナビゲーション パネルで、[リソース グループ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="af781-147">表示されるウィンドウの左上にある [追加] タブを **選択して、** 新しいリソース グループを作成します。</span><span class="sxs-lookup"><span data-stu-id="af781-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="af781-148">次の情報を入力するように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="af781-149">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="af781-149">**Subscription**.</span></span> <span data-ttu-id="af781-150">既存のサブスクリプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="af781-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="af781-151">**リソース グループ**。</span><span class="sxs-lookup"><span data-stu-id="af781-151">**Resource group**.</span></span> <span data-ttu-id="af781-152">リソース グループの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-152">Enter the name for the resource group.</span></span> <span data-ttu-id="af781-153">たとえば  *、TeamsResourceGroup です*。</span><span class="sxs-lookup"><span data-stu-id="af781-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="af781-154">名前は一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="af781-155">[地域 **] ドロップダウン** メニューから、[ *米国* 西部] またはアプリケーションに近い地域を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="af781-156">[レビューと **作成] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-156">Select the **Review and create** button.</span></span> <span data-ttu-id="af781-157">検証が渡されたというバナーが *表示されます*。</span><span class="sxs-lookup"><span data-stu-id="af781-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="af781-158">[作成] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-158">Select the **Create** button.</span></span> <span data-ttu-id="af781-159">リソース グループの作成に数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="af781-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="af781-160">このチュートリアルの後半で作成するリソースと同様に、このリソース グループをダッシュボードにピン留めして簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="af781-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="af781-161">これを行う場合は、ピン アイコンを選択&#128204。をダッシュボードの右上に表示します。</span><span class="sxs-lookup"><span data-stu-id="af781-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="af781-162">サービス プランの作成</span><span class="sxs-lookup"><span data-stu-id="af781-162">Create the service plan</span></span>

1. <span data-ttu-id="af781-163">Azure portal [**の左側の**][azure-portal]ナビゲーション パネルで、[リソースの作成 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="af781-164">検索ボックスに *「App Service Plan」と入力します*。</span><span class="sxs-lookup"><span data-stu-id="af781-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="af781-165">検索結果から **[App Service プラン** ] カードを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="af781-166">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-166">Select **Create**.</span></span>
1. <span data-ttu-id="af781-167">次の情報の入力を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="af781-168">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="af781-168">**Subscription**.</span></span> <span data-ttu-id="af781-169">既存のサブスクリプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="af781-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="af781-170">**リソース グループ**。</span><span class="sxs-lookup"><span data-stu-id="af781-170">**Resource Group**.</span></span> <span data-ttu-id="af781-171">前に作成したグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="af781-172">**Name**.</span><span class="sxs-lookup"><span data-stu-id="af781-172">**Name**.</span></span> <span data-ttu-id="af781-173">サービス プランの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-173">Enter the name for the service plan.</span></span> <span data-ttu-id="af781-174">たとえば  *、TeamsServicePlan です*。</span><span class="sxs-lookup"><span data-stu-id="af781-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="af781-175">名前はグループ内で一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="af781-176">**オペレーティング システム**.</span><span class="sxs-lookup"><span data-stu-id="af781-176">**Operating System**.</span></span> <span data-ttu-id="af781-177">*[Windows] または* 該当する OS を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="af781-178">**地域**.</span><span class="sxs-lookup"><span data-stu-id="af781-178">**Region**.</span></span> <span data-ttu-id="af781-179">[ *米国西部]* またはアプリケーションに近い地域を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="af781-180">**価格レベル**.</span><span class="sxs-lookup"><span data-stu-id="af781-180">**Pricing Tier**.</span></span> <span data-ttu-id="af781-181">[標準 *S1] が選択* されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="af781-182">これは既定値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-182">This should be the default value.</span></span>
    1. <span data-ttu-id="af781-183">[レビューと **作成] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-183">Select the **Review and create** button.</span></span> <span data-ttu-id="af781-184">検証が渡されたというバナーが *表示されます*。</span><span class="sxs-lookup"><span data-stu-id="af781-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="af781-185">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-185">Select **Create**.</span></span> <span data-ttu-id="af781-186">アプリ サービス プランの作成に数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="af781-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="af781-187">計画はリソース グループに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="af781-188">ボット チャネルの登録を作成する</span><span class="sxs-lookup"><span data-stu-id="af781-188">Create the bot channels registration</span></span>

<span data-ttu-id="af781-189">Microsoft App Id とアプリ パスワード (クライアント シークレット) がある場合は、ボット チャネル登録によって Web サービスがボット フレームワークにボットとして登録されます。</span><span class="sxs-lookup"><span data-stu-id="af781-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af781-190">ボットが Azure でホストされていない場合にのみ、ボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="af781-191">Azure ポータル [を使用して](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) ボットを作成した場合、そのボットは既にサービスに登録されています。</span><span class="sxs-lookup"><span data-stu-id="af781-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="af781-192">ボット フレームワークまたは[AppStudio](~/concepts/build-and-test/app-studio-overview.md)を使用してボットを作成した場合、ボットは Azure に登録されません。 [](https://dev.botframework.com/bots/new)</span><span class="sxs-lookup"><span data-stu-id="af781-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="af781-193">[ボット チャネル登録] リソースには、米国西部を **選択** した場合でもグローバル地域が表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="af781-194">これは正常な動作です。</span><span class="sxs-lookup"><span data-stu-id="af781-194">This is expected.</span></span>

<span data-ttu-id="af781-195">詳細については [、「Create a bot for Teams」を参照してください](../create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="af781-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="af781-196">ID プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="af781-196">Create the identity provider</span></span>

<span data-ttu-id="af781-197">認証に使用できる ID プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="af781-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="af781-198">この手順では、Azure プロバイダーを使用ADします。他の Azure ADサポートされている ID プロバイダーも使用できます。</span><span class="sxs-lookup"><span data-stu-id="af781-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="af781-199">Azure portal [**の左側**][azure-portal]のナビゲーション パネルで **、[Azure Active Directory] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="af781-200">この Azure AD リソースを作成して、アプリケーションから要求されたアクセス許可を委任する同意を得る必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="af781-201">テナントの作成方法については、「ポータルにアクセスしてテナントを作成 [する」を参照してください](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)。</span><span class="sxs-lookup"><span data-stu-id="af781-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="af781-202">左側のパネルで、[アプリの登録 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="af781-203">右側のパネルで、左上の **[新規登録** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="af781-204">次の情報の入力を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="af781-205">**Name**.</span><span class="sxs-lookup"><span data-stu-id="af781-205">**Name**.</span></span> <span data-ttu-id="af781-206">アプリケーションの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-206">Enter the name for the application.</span></span> <span data-ttu-id="af781-207">たとえば  *、BotTeamsIdentity を指定できます*。</span><span class="sxs-lookup"><span data-stu-id="af781-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="af781-208">名前は一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="af781-209">アプリケーションの **[サポートされているアカウントの種類** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="af781-210">任意の組織ディレクトリ (任意の Azure AD ディレクトリ - マルチテナント) および個人用 Microsoft アカウント *(Skype、Xbox など) で [アカウント] を選択します*。</span><span class="sxs-lookup"><span data-stu-id="af781-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="af781-211">リダイレクト **URI の場合**:</span><span class="sxs-lookup"><span data-stu-id="af781-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="af781-212">&#x2713;Web を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="af781-213">&#x2713; URL をに設定します `https://token.botframework.com/.auth/web/redirect` 。</span><span class="sxs-lookup"><span data-stu-id="af781-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="af781-214">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-214">Select **Register**.</span></span>

1. <span data-ttu-id="af781-215">アプリが作成されると、アプリの **[概要** ] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="af781-216">次の情報をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="af781-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="af781-217">アプリケーション **(クライアント) の ID** 値。</span><span class="sxs-lookup"><span data-stu-id="af781-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="af781-218">この Azure ID アプリケーションをボットに登録する場合は、後でクライアント *ID* としてこの値を使用します。</span><span class="sxs-lookup"><span data-stu-id="af781-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="af781-219">ディレクトリ **(テナント) ID** の値。</span><span class="sxs-lookup"><span data-stu-id="af781-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="af781-220">この値は、後でテナント ID として使用して、この Azure *ID* アプリケーションをボットに登録します。</span><span class="sxs-lookup"><span data-stu-id="af781-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="af781-221">左側のパネルで、[証明書] & **を選択して** 、アプリケーションのクライアント シークレットを作成します。</span><span class="sxs-lookup"><span data-stu-id="af781-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="af781-222">[ **クライアント シークレット] で**、[新しい&#x2795; **シークレット] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="af781-223">Teams のボット ID アプリなど、このアプリ用に作成する必要がある他のユーザーからこのシークレットを *識別するための説明を追加します*。</span><span class="sxs-lookup"><span data-stu-id="af781-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="af781-224">[ **有効期限] を選択** に設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="af781-225">**[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-225">Select **Add**.</span></span>
   1. <span data-ttu-id="af781-226">このページを離れる前に、 **シークレットを記録します**。</span><span class="sxs-lookup"><span data-stu-id="af781-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="af781-227">この値は、Azure アプリケーションをボットに登録するときに、後でクライアント AD使用します。</span><span class="sxs-lookup"><span data-stu-id="af781-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="af781-228">ID プロバイダー接続を構成し、ボットに登録する</span><span class="sxs-lookup"><span data-stu-id="af781-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="af781-229">注:Service Providers here-Azure v1 と Azure AD V2 には 2 ADがあります。</span><span class="sxs-lookup"><span data-stu-id="af781-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="af781-230">2 つのプロバイダー間の違いについては、[](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)ここで要約しますが、一般に、V2 はボットのアクセス許可の変更に関して柔軟性を提供します。</span><span class="sxs-lookup"><span data-stu-id="af781-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="af781-231">グラフ API のアクセス許可はスコープ フィールドに一覧表示され、新しいアクセス許可が追加されるに合って、ボットはユーザーが次のサインインの新しいアクセス許可に同意できます。</span><span class="sxs-lookup"><span data-stu-id="af781-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="af781-232">V1 の場合、OAuth ダイアログで新しいアクセス許可を求めるには、ボットの同意をユーザーが削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="af781-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="af781-233">Azure AD V1</span></span>

1. <span data-ttu-id="af781-234">Azure portal [**で、**][azure-portal]ダッシュボードからリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="af781-235">ボット チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="af781-236">リソース ページで、[設定] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-236">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="af781-237">ページ **の下部近くの [OAuth 接続設定** ] で、[設定の追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-237">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="af781-238">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-238">Complete the form as follows:</span></span>

    1. <span data-ttu-id="af781-239">**Name**.</span><span class="sxs-lookup"><span data-stu-id="af781-239">**Name**.</span></span> <span data-ttu-id="af781-240">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-240">Enter a name for the connection.</span></span> <span data-ttu-id="af781-241">この名前は、ファイル内のボットで使用 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="af781-241">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="af781-242">たとえば *、BotTeamsAuthADv1 .*</span><span class="sxs-lookup"><span data-stu-id="af781-242">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="af781-243">**サービス プロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="af781-243">**Service Provider**.</span></span> <span data-ttu-id="af781-244">[**Azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-244">Select **Azure Active Directory**.</span></span> <span data-ttu-id="af781-245">これを選択すると、Azure AD固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-245">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="af781-246">**クライアント ID**。上記の手順で、Azure ID プロバイダー アプリに記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-246">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="af781-247">**クライアント シークレット**。</span><span class="sxs-lookup"><span data-stu-id="af781-247">**Client secret**.</span></span> <span data-ttu-id="af781-248">上記の手順で、Azure ID プロバイダー アプリに記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-248">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="af781-249">**Grant Type**.</span><span class="sxs-lookup"><span data-stu-id="af781-249">**Grant Type**.</span></span> <span data-ttu-id="af781-250">を `authorization_code` 入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-250">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="af781-251">**ログイン URL**。</span><span class="sxs-lookup"><span data-stu-id="af781-251">**Login URL**.</span></span> <span data-ttu-id="af781-252">を `https://login.microsoftonline.com` 入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-252">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="af781-253">**テナント ID** は、Id プロバイダー アプリの作成時に選択されたサポートされているアカウントの種類に応じて、Azure ID アプリまたは共通の前に記録したディレクトリ **(テナント) ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-253">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="af781-254">割り当てる値を決定するには、次の条件に従います。</span><span class="sxs-lookup"><span data-stu-id="af781-254">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="af781-255">この組織ディレクトリ内の [アカウントのみ] *(Microsoft のみ - シングル* テナント) または任意の組織ディレクトリの [アカウント] *(Microsoft AAD ディレクトリ - マルチ* テナント) のいずれかを選択した場合は、AAD アプリ用に前に記録したテナント **ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-255">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="af781-256">これは、認証できるユーザーに関連付けられたテナントになります。</span><span class="sxs-lookup"><span data-stu-id="af781-256">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="af781-257">組織ディレクトリで [アカウント] を選択した場合 (任意の AAD ディレクトリ - マルチ テナントアカウントと個人 Microsoft アカウント *(Skype、Xbox、Outlook など)* は、テナント ID の代わりに **共通** の単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-257">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="af781-258">それ以外の場合、AAD アプリは ID が選択されたテナントを通じて確認し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="af781-258">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="af781-259">h.</span><span class="sxs-lookup"><span data-stu-id="af781-259">h.</span></span> <span data-ttu-id="af781-260">[ **リソース URL]** に、 を入力します `https://graph.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="af781-260">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="af781-261">これは、現在のコード サンプルでは使用されません。</span><span class="sxs-lookup"><span data-stu-id="af781-261">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="af781-262">i.</span><span class="sxs-lookup"><span data-stu-id="af781-262">i.</span></span> <span data-ttu-id="af781-263">[ **スコープ] は空白** のままにします。</span><span class="sxs-lookup"><span data-stu-id="af781-263">Leave **Scopes** blank.</span></span> <span data-ttu-id="af781-264">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="af781-264">The following image is an example:</span></span>

    ![teams bots アプリの認証接続文字列 adv1 ビュー](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="af781-266">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-266">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="af781-267">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="af781-267">Azure AD V2</span></span>

1. <span data-ttu-id="af781-268">Azure portal [**で、**][azure-portal]ダッシュボードからリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-268">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="af781-269">ボット チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-269">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="af781-270">リソース ページで、[設定] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-270">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="af781-271">ページ **の下部近くの [OAuth 接続設定** ] で、[設定の追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-271">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="af781-272">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-272">Complete the form as follows:</span></span>

    1. <span data-ttu-id="af781-273">**Name**.</span><span class="sxs-lookup"><span data-stu-id="af781-273">**Name**.</span></span> <span data-ttu-id="af781-274">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-274">Enter a name for the connection.</span></span> <span data-ttu-id="af781-275">この名前は、ファイル内のボットで使用 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="af781-275">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="af781-276">たとえば *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="af781-276">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="af781-277">**サービス プロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="af781-277">**Service Provider**.</span></span> <span data-ttu-id="af781-278">[Azure **Active Directory v2] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-278">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="af781-279">これを選択すると、Azure AD固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-279">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="af781-280">**クライアント ID**。上記の手順で、Azure ID プロバイダー アプリに記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-280">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="af781-281">**クライアント シークレット**。</span><span class="sxs-lookup"><span data-stu-id="af781-281">**Client secret**.</span></span> <span data-ttu-id="af781-282">上記の手順で、Azure ID プロバイダー アプリに記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-282">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="af781-283">**トークン Exchange の URL**。</span><span class="sxs-lookup"><span data-stu-id="af781-283">**Token Exchange URL**.</span></span> <span data-ttu-id="af781-284">空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="af781-284">Leave this blank.</span></span>
    1. <span data-ttu-id="af781-285">**テナント ID** は、Id プロバイダー アプリの作成時に選択されたサポートされているアカウントの種類に応じて、Azure ID アプリまたは共通の前に記録したディレクトリ **(テナント) ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-285">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="af781-286">割り当てる値を決定するには、次の条件に従います。</span><span class="sxs-lookup"><span data-stu-id="af781-286">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="af781-287">この組織ディレクトリ内の [アカウントのみ] *(Microsoft のみ - シングル* テナント) または任意の組織ディレクトリの [アカウント] *(Microsoft AAD ディレクトリ - マルチ* テナント) のいずれかを選択した場合は、AAD アプリ用に前に記録したテナント **ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-287">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="af781-288">これは、認証できるユーザーに関連付けられたテナントになります。</span><span class="sxs-lookup"><span data-stu-id="af781-288">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="af781-289">組織ディレクトリで [アカウント] を選択した場合 (任意の AAD ディレクトリ - マルチ テナントアカウントと個人 Microsoft アカウント *(Skype、Xbox、Outlook など)* は、テナント ID の代わりに **共通** の単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-289">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="af781-290">それ以外の場合、AAD アプリは ID が選択されたテナントを通じて確認し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="af781-290">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="af781-291">[ **スコープ]** に、このアプリケーションで必要なグラフのアクセス許可のスペースで区切られたリストを入力します。User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="af781-291">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="af781-292">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-292">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="af781-293">接続をテストする</span><span class="sxs-lookup"><span data-stu-id="af781-293">Test the connection</span></span>

1. <span data-ttu-id="af781-294">接続エントリを選択して、作成した接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="af781-294">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="af781-295">[ **サービス プロバイダーの接続設定** ] パネルの上部にある **[接続のテスト] を選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-295">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="af781-296">これを初めて実行すると、アカウントの選択を求める新しいブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="af781-296">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="af781-297">使用する 1 つを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-297">Select the one you want to use.</span></span>
1. <span data-ttu-id="af781-298">次に、ID プロバイダーにデータ (資格情報) の使用を許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-298">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="af781-299">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="af781-299">The following image is an example:</span></span>

    ![teams bot auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="af781-301">**[同意する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-301">Select **Accept**.</span></span>
1. <span data-ttu-id="af781-302">その後、テスト接続を **[成功] ページ \<your-connection-name> にリダイレクト** します。</span><span class="sxs-lookup"><span data-stu-id="af781-302">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="af781-303">エラーが発生した場合は、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="af781-303">Refresh the page if you get an error.</span></span> <span data-ttu-id="af781-304">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="af781-304">The following image is an example:</span></span>

  ![teams bots アプリの認証接続 str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="af781-306">接続名は、ボット コードによってユーザー認証トークンを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="af781-306">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="af781-307">ボットのサンプル コードを準備する</span><span class="sxs-lookup"><span data-stu-id="af781-307">Prepare the bot sample code</span></span>

<span data-ttu-id="af781-308">事前設定が完了したら、この記事で使用するボットの作成に注目します。</span><span class="sxs-lookup"><span data-stu-id="af781-308">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="af781-309">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="af781-309">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="af781-310">[cs-auth-sample のクローンを作成します][teams-auth-bot-cs]。</span><span class="sxs-lookup"><span data-stu-id="af781-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="af781-311">起動Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="af781-311">Launch Visual Studio.</span></span>
1. <span data-ttu-id="af781-312">ツール バーの [ファイル] **-> [開>プロジェクト/** ソリューション] を選択し、ボット プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="af781-312">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="af781-313">[C#更新 **appsettings.js次のように** オンにします。</span><span class="sxs-lookup"><span data-stu-id="af781-313">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="af781-314">ボット `ConnectionName` チャネル登録に追加した ID プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-314">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="af781-315">この例で使用した名前は *BotTeamsAuthADv1 です*。</span><span class="sxs-lookup"><span data-stu-id="af781-315">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="af781-316">ボット `MicrosoftAppId` チャネル **登録時に** 保存したボット アプリ ID に設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-316">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="af781-317">ボット `MicrosoftAppPassword` チャネル登録 **時に** 保存した顧客シークレットに設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-317">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="af781-318">ボット シークレットの文字によっては、XML でパスワードをエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-318">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="af781-319">たとえば、アンパサンド (&) はとしてエンコードする必要があります `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="af781-319">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="af781-320">ソリューション エクスプローラーで、フォルダーに移動し、ボット チャネル登録時に保存したボット アプリ ID を `TeamsAppManifest` `manifest.json` 開いて `id` `botId` 設定します。 </span><span class="sxs-lookup"><span data-stu-id="af781-320">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="af781-321">JavaScript</span><span class="sxs-lookup"><span data-stu-id="af781-321">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="af781-322">ノード [の複製-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="af781-322">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="af781-323">コンソールで、プロジェクトに移動します。</span><span class="sxs-lookup"><span data-stu-id="af781-323">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="af781-324">モジュールのインストール</span><span class="sxs-lookup"><span data-stu-id="af781-324">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="af781-325">**.env 構成を次** のように更新します。</span><span class="sxs-lookup"><span data-stu-id="af781-325">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="af781-326">ボット `MicrosoftAppId` チャネル **登録時に** 保存したボット アプリ ID に設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-326">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="af781-327">ボット `MicrosoftAppPassword` チャネル登録 **時に** 保存した顧客シークレットに設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-327">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="af781-328">id プロバイダー `connectionName` 接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-328">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="af781-329">ボット シークレットの文字によっては、XML でパスワードをエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-329">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="af781-330">たとえば、アンパサンド (&) はとしてエンコードする必要があります `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="af781-330">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="af781-331">フォルダーで、Microsoft App ID とボット チャネル登録時に保存したボット アプリ ID を開いて `teamsAppManifest` `manifest.json` `id`  `botId` 設定します。 </span><span class="sxs-lookup"><span data-stu-id="af781-331">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="af781-332">Python</span><span class="sxs-lookup"><span data-stu-id="af781-332">Python</span></span>](#tab/python)

1. <span data-ttu-id="af781-333">github [リポジトリから py-auth-sample][teams-auth-bot-py] を複製します。</span><span class="sxs-lookup"><span data-stu-id="af781-333">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="af781-334">更新 **config.py:**</span><span class="sxs-lookup"><span data-stu-id="af781-334">Update **config.py**:</span></span>

    - <span data-ttu-id="af781-335">ボット `ConnectionName` に追加した OAuth 接続設定の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-335">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="af781-336">ボット `MicrosoftAppId` の `MicrosoftAppPassword` アプリ ID とアプリ シークレットを設定します。</span><span class="sxs-lookup"><span data-stu-id="af781-336">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="af781-337">ボット シークレットの文字によっては、XML でパスワードをエスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-337">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="af781-338">たとえば、アンパサンド (&) はとしてエンコードする必要があります `&amp;` 。</span><span class="sxs-lookup"><span data-stu-id="af781-338">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="af781-339">ボットを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="af781-339">Deploy the bot to Azure</span></span>

<span data-ttu-id="af781-340">ボットを展開するには、「Azure にボットを展開する方法」 [の手順に従います](https://aka.ms/azure-bot-deployment-cli)。</span><span class="sxs-lookup"><span data-stu-id="af781-340">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="af781-341">または、次のVisual Studioを実行できます。</span><span class="sxs-lookup"><span data-stu-id="af781-341">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="af781-342">[Visual Studio *エクスプローラーで* 、プロジェクト名を選択したまま (または右クリック) します。</span><span class="sxs-lookup"><span data-stu-id="af781-342">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="af781-343">ドロップダウン メニューで、[発行] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-343">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="af781-344">表示されたウィンドウで、[新規] リンク **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-344">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="af781-345">ダイアログ ウィンドウで、左側の **[App Service]** を選択し、右側 **の [新しい作成** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-345">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="af781-346">[発行] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-346">Select the **Publish** button.</span></span>
1. <span data-ttu-id="af781-347">次のダイアログ ウィンドウで、必要な情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-347">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="af781-348">例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="af781-348">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="af781-350">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-350">Select **Create**.</span></span>
1. <span data-ttu-id="af781-351">展開が正常に完了した場合は、展開がサーバーに反映Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="af781-351">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="af781-352">さらに、既定のブラウザーに、ボットの準備が完了した *というページが表示されます*。</span><span class="sxs-lookup"><span data-stu-id="af781-352">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="af781-353">URL は次に似ています `https://botteamsauth.azurewebsites.net/` 。</span><span class="sxs-lookup"><span data-stu-id="af781-353">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="af781-354">ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="af781-354">Save it to a file.</span></span>
1. <span data-ttu-id="af781-355">ブラウザーで、Azure portal に [**移動します**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="af781-355">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="af781-356">リソース グループを確認すると、ボットが他のリソースと共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-356">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="af781-357">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="af781-357">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="af781-359">リソース グループで、ボット チャネル登録名 (リンク) を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-359">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="af781-360">左側のパネルで、[設定] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-360">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="af781-361">[メッセージング **エンドポイント] ボックスに** 、上記で取得した URL を入力し、その後に `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="af781-361">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="af781-362">次に例を示します `https://botteamsauth.azurewebsites.net/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="af781-362">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="af781-363">左上の **[保存** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-363">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="af781-364">エミュレーターを使用してボットをテストする</span><span class="sxs-lookup"><span data-stu-id="af781-364">Test the bot using the Emulator</span></span>

<span data-ttu-id="af781-365">まだ実行していない場合は [、Microsoft Bot Framework エミュレーターをインストールします](https://aka.ms/bot-framework-emulator-readme)。</span><span class="sxs-lookup"><span data-stu-id="af781-365">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="af781-366">「エミュレーター [を使用したデバッグ」も参照してください](https://aka.ms/bot-framework-emulator-debug-with-emulator)。</span><span class="sxs-lookup"><span data-stu-id="af781-366">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="af781-367">ボット サンプル ログインを機能するには、次に示すようにエミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-367">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="af781-368">認証用にエミュレーターを構成する</span><span class="sxs-lookup"><span data-stu-id="af781-368">Configure the Emulator for authentication</span></span>

<span data-ttu-id="af781-369">ボットで認証が必要な場合は、次に示すようにエミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-369">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="af781-370">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="af781-370">Start the Emulator.</span></span>
1. <span data-ttu-id="af781-371">エミュレーターで、左下の歯車&#9881;、右上の [ **エミュレーター** の設定] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-371">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="af781-372">[バージョン **1.0 認証トークンを使用する] のチェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="af781-372">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="af781-373">ngrok ツールへのローカル **パスを入力** します。</span><span class="sxs-lookup"><span data-stu-id="af781-373">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="af781-374">*ボット* フレームワーク エミュレーター / ngrok トンネリング統合 Wiki を [参照してください](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))。</span><span class="sxs-lookup"><span data-stu-id="af781-374">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="af781-375">ツールの詳細については [、「ngrok」を参照してください](https://ngrok.com/)。</span><span class="sxs-lookup"><span data-stu-id="af781-375">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="af781-376">エミュレーターの起動時に **ngrok を実行してチェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="af781-376">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="af781-377">[保存] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-377">Select the **Save** button.</span></span>

<span data-ttu-id="af781-378">ボットがサインイン カードを表示し、ユーザーがサインイン ボタンを選択すると、エミュレーターは、ユーザーが認証プロバイダーでサインインするために使用できるページを開きます。</span><span class="sxs-lookup"><span data-stu-id="af781-378">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="af781-379">ユーザーがそうすると、プロバイダーはユーザー トークンを生成し、ボットに送信します。</span><span class="sxs-lookup"><span data-stu-id="af781-379">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="af781-380">その後、ボットはユーザーに代わって行動できます。</span><span class="sxs-lookup"><span data-stu-id="af781-380">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="af781-381">ボットをローカルでテストする</span><span class="sxs-lookup"><span data-stu-id="af781-381">Test the bot locally</span></span>

<span data-ttu-id="af781-382">認証メカニズムを構成した後、実際のボット テストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="af781-382">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="af781-383">たとえば、コンピューターでボット サンプルをローカルで実行Visual Studio使用します。</span><span class="sxs-lookup"><span data-stu-id="af781-383">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="af781-384">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="af781-384">Start the Emulator.</span></span>
1. <span data-ttu-id="af781-385">[ボットを **開く] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-385">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="af781-386">ボットの **URL に**、ボットのローカル URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-386">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="af781-387">通常 `http://localhost:3978/api/messages` 、.</span><span class="sxs-lookup"><span data-stu-id="af781-387">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="af781-388">Microsoft App **ID に、ボット** のアプリ ID を入力します `appsettings.json` 。</span><span class="sxs-lookup"><span data-stu-id="af781-388">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="af781-389">Microsoft App **のパスワードで、** からボットのアプリ パスワードを入力 `appsettings.json` します。</span><span class="sxs-lookup"><span data-stu-id="af781-389">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="af781-390">[接続 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-390">Select **Connect**.</span></span>
1. <span data-ttu-id="af781-391">ボットが稼働した後、任意のテキストを入力してサインイン カードを表示します。</span><span class="sxs-lookup"><span data-stu-id="af781-391">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="af781-392">**[サインイン]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-392">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="af781-393">[開く URL の確認] にポップアップ **ダイアログが表示されます**。</span><span class="sxs-lookup"><span data-stu-id="af781-393">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="af781-394">これは、ボットのユーザー (ユーザー) が認証を許可するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="af781-394">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="af781-395">**[確認]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-395">Select **Confirm**.</span></span>
1. <span data-ttu-id="af781-396">確認された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-396">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="af781-397">エミュレーターに使用した構成に応じて、次のいずれかを取得します。</span><span class="sxs-lookup"><span data-stu-id="af781-397">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="af781-398">**サインイン検証コードの使用**</span><span class="sxs-lookup"><span data-stu-id="af781-398">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="af781-399">&#x2713;検証コードを表示するウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="af781-399">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="af781-400">&#x2713;入力規則コードをコピーしてチャット ボックスに入力し、サインインを完了します。</span><span class="sxs-lookup"><span data-stu-id="af781-400">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="af781-401">**認証トークンの使用**.</span><span class="sxs-lookup"><span data-stu-id="af781-401">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="af781-402">&#x2713;資格情報に基づいてログインしています。</span><span class="sxs-lookup"><span data-stu-id="af781-402">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="af781-403">次の図は、ログインした後のボット UI の例です。</span><span class="sxs-lookup"><span data-stu-id="af781-403">The following image is an example of the bot UI after you've logged in:</span></span>

    ![認証ボットのログイン エミュレーター](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="af781-405">ボットが要求 **するときに [は** い] を選択した場合、トークンを表示しますか *?* を選択すると、次のような応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="af781-405">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![認証ボットのログイン エミュレーター トークン](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="af781-407">入力 **チャット ボックスに** ログアウトと入力してサインアウトします。これにより、ユーザー トークンが解放され、再度サインインするまでボットは代理で動作できません。</span><span class="sxs-lookup"><span data-stu-id="af781-407">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="af781-408">ボット認証では、ボット コネクタ サービス **を使用する必要があります**。</span><span class="sxs-lookup"><span data-stu-id="af781-408">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="af781-409">サービスは、ボットのボット チャネル登録情報にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="af781-409">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="af781-410">展開されたボットをテストする</span><span class="sxs-lookup"><span data-stu-id="af781-410">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="af781-411">ブラウザーで、Azure portal に [**移動します**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="af781-411">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="af781-412">リソース グループを検索します。</span><span class="sxs-lookup"><span data-stu-id="af781-412">Find your resource group.</span></span>
1. <span data-ttu-id="af781-413">リソース リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-413">Select the resource link.</span></span> <span data-ttu-id="af781-414">リソース ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-414">The resource page is displayed.</span></span>
1. <span data-ttu-id="af781-415">リソース ページで、[Web チャットで **テスト] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-415">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="af781-416">ボットは、定義済みの案内応答を開始して表示します。</span><span class="sxs-lookup"><span data-stu-id="af781-416">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="af781-417">チャット ボックスに何かを入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-417">Type anything in the chat box.</span></span>
1. <span data-ttu-id="af781-418">[サインイン **] ボックスを選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-418">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="af781-419">[開く URL の確認] にポップアップ **ダイアログが表示されます**。</span><span class="sxs-lookup"><span data-stu-id="af781-419">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="af781-420">これは、ボットのユーザー (ユーザー) が認証を許可するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="af781-420">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="af781-421">**[確認]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-421">Select **Confirm**.</span></span>
1. <span data-ttu-id="af781-422">確認された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-422">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="af781-423">次の図は、ログインした後のボット UI の例です。</span><span class="sxs-lookup"><span data-stu-id="af781-423">The following image is an example of the bot UI after you have logged in:</span></span>

    ![auth bot login deployed](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="af781-425">.</span><span class="sxs-lookup"><span data-stu-id="af781-425">.</span></span>

1. <span data-ttu-id="af781-426">[はい **] ボタン** を選択して認証トークンを表示します。</span><span class="sxs-lookup"><span data-stu-id="af781-426">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="af781-427">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="af781-427">The following image is an example:</span></span>

    ![認証ボット のログイン展開トークン](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="af781-429">.</span><span class="sxs-lookup"><span data-stu-id="af781-429">.</span></span>

1. <span data-ttu-id="af781-430">ログアウトを入力してサインアウトします。</span><span class="sxs-lookup"><span data-stu-id="af781-430">Enter logout to sign out.</span></span>

    ![認証ボットが展開したログアウト](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="af781-432">サインインに問題がある場合は、前の手順で説明したように、もう一度接続をテストしてみてください。</span><span class="sxs-lookup"><span data-stu-id="af781-432">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="af781-433">これにより、認証トークンが再作成される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="af781-433">This could recreate the authentication token.</span></span>
> <span data-ttu-id="af781-434">Azure のボット フレームワーク Web チャット クライアントでは、認証が正しく確立される前に何度かサインインする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="af781-434">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="af781-435">Teams でボットをインストールしてテストする</span><span class="sxs-lookup"><span data-stu-id="af781-435">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="af781-436">ボット プロジェクトで、フォルダーにファイルと共に `TeamsAppManifest` `manifest.json` フォルダーが含まれているか `outline.png` 確認 `color.png` します。</span><span class="sxs-lookup"><span data-stu-id="af781-436">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="af781-437">ソリューション エクスプローラーで、フォルダーに移動 `TeamsAppManifest` します。</span><span class="sxs-lookup"><span data-stu-id="af781-437">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="af781-438">次の `manifest.json` 値を割り当て、編集します。</span><span class="sxs-lookup"><span data-stu-id="af781-438">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="af781-439">ボット チャネル登録 **時に受信** したボット アプリ ID がに割り当てられているか確認 `id` します `botId` 。</span><span class="sxs-lookup"><span data-stu-id="af781-439">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="af781-440">この値を割り `validDomains: [ "token.botframework.com" ]` 当てる。</span><span class="sxs-lookup"><span data-stu-id="af781-440">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="af781-441">、および **ファイルを** `manifest.json` 選択 `outline.png` して `color.png` 圧縮します。</span><span class="sxs-lookup"><span data-stu-id="af781-441">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="af781-442">**Microsoft Teams を開きます**。</span><span class="sxs-lookup"><span data-stu-id="af781-442">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="af781-443">左側のパネルで、下部にある [アプリ] アイコン **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-443">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="af781-444">右側のパネルの下部で、[カスタム アプリのアップロード **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-444">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="af781-445">フォルダーに移動 `TeamsAppManifest` し、圧縮されたマニフェストをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="af781-445">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="af781-446">次のウィザードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-446">The following wizard is displayed:</span></span>

    ![認証ボット チームのアップロード](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="af781-448">**[チームに追加]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-448">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="af781-449">次のウィンドウで、ボットを使用するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-449">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="af781-450">[ボットの **セットアップ] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="af781-450">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="af781-451">左側のパネルで 3 つのドット (&#x25cf;&#x25cf;&#x25cf;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-451">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="af781-452">次に **、[App Studio] アイコンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="af781-452">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="af781-453">[マニフェスト エディター **] タブを** 選択します。アップロードしたボットのアイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-453">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="af781-454">また、ボットとメッセージを交換するために使用できるチャット リストに、連絡先として一覧表示されているボットを確認できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-454">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="af781-455">Teams でボットをローカルでテストする</span><span class="sxs-lookup"><span data-stu-id="af781-455">Testing the bot locally in Teams</span></span>

<span data-ttu-id="af781-456">Microsoft Teams は完全にクラウドベースの製品です。HTTPS エンドポイントを使用してクラウドからアクセスするサービスはすべて利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-456">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="af781-457">そのため、ボット (サンプル) が Teams で動作するには、コードを選択したクラウドに発行するか、トンネリング ツールを介してローカルで実行中のインスタンスに外部からアクセス可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-457">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="af781-458">コンピューターで  [ローカルで開](https://ngrok.com/download)くポートの外部アドレス指定可能な URL を作成する ngrok をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="af781-458">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="af781-459">Microsoft Teams アプリをローカルで実行する準備として ngrok を設定するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="af781-459">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="af781-460">ターミナル ウィンドウで、インストールしたディレクトリに移動 `ngrok.exe` します。</span><span class="sxs-lookup"><span data-stu-id="af781-460">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="af781-461">環境変数のパスを *ポイントする* 設定をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="af781-461">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="af781-462">たとえば、実行します `ngrok http 3978 --host-header=localhost:3978` 。</span><span class="sxs-lookup"><span data-stu-id="af781-462">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="af781-463">必要に応じてポート番号を置き換える。</span><span class="sxs-lookup"><span data-stu-id="af781-463">Replace the port number as needed.</span></span>
<span data-ttu-id="af781-464">これにより、ngrok が起動して、指定したポートでリッスンします。</span><span class="sxs-lookup"><span data-stu-id="af781-464">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="af781-465">その代り、ngrok が実行されている限り有効な外部アドレス指定可能な URL が提供されます。</span><span class="sxs-lookup"><span data-stu-id="af781-465">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="af781-466">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="af781-466">The following image is an example:</span></span>

    ![teams ボット アプリ認証接続文字列 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="af781-468">.</span><span class="sxs-lookup"><span data-stu-id="af781-468">.</span></span>

1. <span data-ttu-id="af781-469">転送 HTTPS アドレスをコピーします。</span><span class="sxs-lookup"><span data-stu-id="af781-469">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="af781-470">これは、次のようになります `https://dea822bf.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="af781-470">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="af781-471">取得 `/api/messages` するには、追加 `https://dea822bf.ngrok.io/api/messages` します。</span><span class="sxs-lookup"><span data-stu-id="af781-471">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="af781-472">これは、 **コンピューター上でローカル** に実行され、Microsoft Teams のチャットで Web を使用して到達可能なボットのメッセージ エンドポイントです。</span><span class="sxs-lookup"><span data-stu-id="af781-472">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="af781-473">実行する最後の手順の 1 つは、展開されたボットのメッセージ エンドポイントを更新する方法です。</span><span class="sxs-lookup"><span data-stu-id="af781-473">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="af781-474">この例では、Azure にボットを展開しました。</span><span class="sxs-lookup"><span data-stu-id="af781-474">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="af781-475">次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="af781-475">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="af781-476">ブラウザーで Azure portal に [**移動します**][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="af781-476">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="af781-477">ボット チャネル **登録を選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-477">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="af781-478">左側のパネルで、[設定] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="af781-478">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="af781-479">右側のパネルの [メッセージング **エンドポイント]** ボックスに、ngrok URL を入力します。この例では、 を入力します `https://dea822bf.ngrok.io/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="af781-479">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="af781-480">たとえば、デバッグ モードでボットをローカルVisual Studio開始します。</span><span class="sxs-lookup"><span data-stu-id="af781-480">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="af781-481">ボット フレームワーク ポータルのテスト Web チャットを使用して、ローカルで実行している間 **にボットをテストします**。</span><span class="sxs-lookup"><span data-stu-id="af781-481">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="af781-482">エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="af781-482">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="af781-483">実行中のターミナル ウィンドウで、ボットと Web チャット クライアントの `ngrok` 間の HTTP トラフィックを確認できます。</span><span class="sxs-lookup"><span data-stu-id="af781-483">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="af781-484">より詳細なビューが必要な場合は、ブラウザー ウィンドウで、前 `http://127.0.0.1:4040` のターミナル ウィンドウから取得したと入力します。</span><span class="sxs-lookup"><span data-stu-id="af781-484">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="af781-485">次の図は、例です。</span><span class="sxs-lookup"><span data-stu-id="af781-485">The following image is an example:</span></span>

    ![認証ボット チーム ngrok テスト](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="af781-487">.</span><span class="sxs-lookup"><span data-stu-id="af781-487">.</span></span>

> [!NOTE]
> <span data-ttu-id="af781-488">ngrok を停止して再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="af781-488">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="af781-489">プロジェクトで ngrok を使用するには、使用している機能に応じて、すべての URL 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="af781-489">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="af781-490">追加情報</span><span class="sxs-lookup"><span data-stu-id="af781-490">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="af781-491">TeamsAppManifest/manifest.jsオン</span><span class="sxs-lookup"><span data-stu-id="af781-491">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="af781-492">このマニフェストには、ボットに接続するために Microsoft Teams が必要とする情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="af781-492">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

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

<span data-ttu-id="af781-493">認証では、Teams の動作は、以下で説明する他のチャネルとは若干異なります。</span><span class="sxs-lookup"><span data-stu-id="af781-493">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="af781-494">Invoke アクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="af781-494">Handling Invoke Activity</span></span>

<span data-ttu-id="af781-495">Invoke **Activity は** 、他のチャネルで使用されるイベント アクティビティではなく、ボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="af781-495">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="af781-496">これは、ActivityHandler をサブクラス **化して行います**。</span><span class="sxs-lookup"><span data-stu-id="af781-496">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="af781-497">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="af781-497">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="af781-498">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="af781-498">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="af781-499">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="af781-499">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="af781-500">**OAuthPrompt** を使用する場合は、Invoke Activity をダイアログに転送する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="af781-500">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="af781-501">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="af781-501">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="af781-502">JavaScript</span><span class="sxs-lookup"><span data-stu-id="af781-502">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="af781-503">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="af781-503">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="af781-504">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="af781-504">**bots/teamsBot.js**</span></span>

<span data-ttu-id="af781-505">**OAuthPrompt** を使用する場合は、Invoke Activity をダイアログに転送する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="af781-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="af781-506">**dialogs/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="af781-506">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="af781-507">ダイアログ ステップ内で、OAuth プロンプトを開始し、ユーザーにサインイン `beginDialog` を求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="af781-507">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="af781-508">ユーザーが既にサインインしている場合は、ユーザーにメッセージを表示せずにトークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="af781-508">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="af781-509">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-509">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="af781-510">Azure Bot Service は、ユーザーがサインインを試みた後にトークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="af781-510">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="af781-511">次のダイアログ ステップで、前の手順の結果にトークンが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="af781-511">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="af781-512">null 以外の場合、ユーザーは正常にサインインします。</span><span class="sxs-lookup"><span data-stu-id="af781-512">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="af781-513">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="af781-513">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="af781-514">Python</span><span class="sxs-lookup"><span data-stu-id="af781-514">Python</span></span>](#tab/python-sample)

<span data-ttu-id="af781-515">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="af781-515">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="af781-516">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="af781-516">**bots/teams_bot.py**</span></span>

<span data-ttu-id="af781-517">**OAuthPrompt** を使用する場合は、Invoke Activity をダイアログに転送する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="af781-517">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="af781-518">**dialogs/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="af781-518">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="af781-519">ダイアログ ステップ内で、OAuth プロンプトを開始し、ユーザーにサインイン `begin_dialog` を求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="af781-519">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="af781-520">ユーザーが既にサインインしている場合は、ユーザーにメッセージを表示せずにトークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="af781-520">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="af781-521">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="af781-521">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="af781-522">Azure Bot Service は、ユーザーがサインインを試みた後にトークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="af781-522">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="af781-523">次のダイアログ ステップで、前の手順の結果にトークンが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="af781-523">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="af781-524">null 以外の場合、ユーザーは正常にサインインします。</span><span class="sxs-lookup"><span data-stu-id="af781-524">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="af781-525">**dialogs/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="af781-525">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="af781-526">Azure Bot Service による認証の追加の詳細</span><span class="sxs-lookup"><span data-stu-id="af781-526">Learn about adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

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
