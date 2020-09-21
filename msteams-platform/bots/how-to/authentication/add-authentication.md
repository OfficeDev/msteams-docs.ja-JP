---
title: Teams の bot に認証を追加する
author: clearab
description: Microsoft Teams の bot に OAuth 認証を追加する方法。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 403072efeccdd09e46ac93e2e811ee2d10131668
ms.sourcegitcommit: aabfd65a67e1889ec16f09476bc757dd4a46ec5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "48097887"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="514d9-103">Teams の bot に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="514d9-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="514d9-104">メールサービスなど、ユーザーの代わりにリソースにアクセスできる、Microsoft Teams でボットを作成しなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="514d9-105">この記事では、OAuth 2.0 に基づいて Azure Bot サービス v4 SDK 認証を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="514d9-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="514d9-106">これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットを開発するのが容易になります。</span><span class="sxs-lookup"><span data-stu-id="514d9-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="514d9-107">すべてのキーこれは、後で説明するように、 **id プロバイダー**を使用していることです。</span><span class="sxs-lookup"><span data-stu-id="514d9-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="514d9-108">OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。</span><span class="sxs-lookup"><span data-stu-id="514d9-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="514d9-109">OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。</span><span class="sxs-lookup"><span data-stu-id="514d9-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="514d9-110">基本的な理解と、完全な仕様の[oauth 2.0](https://oauth.net/2/)については、「 [Oauth 2 の単純化](https://aka.ms/oauth2-simplified)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="514d9-111">Azure Bot サービスが認証を処理する方法の詳細については、「 [会話内のユーザー認証](https://aka.ms/azure-bot-authentication)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="514d9-112">この記事では、以下について説明します。</span><span class="sxs-lookup"><span data-stu-id="514d9-112">In this article you'll learn:</span></span>

- <span data-ttu-id="514d9-113">**認証を有効にした bot を作成する方法**。</span><span class="sxs-lookup"><span data-stu-id="514d9-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="514d9-114">ユーザーのサインイン資格情報と認証トークンの生成を処理するには、 [cs-auth-サンプル][teams-auth-bot-cs] を使用します。</span><span class="sxs-lookup"><span data-stu-id="514d9-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="514d9-115">**Bot を Azure に展開し、id プロバイダーに関連付ける方法について説明**します。</span><span class="sxs-lookup"><span data-stu-id="514d9-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="514d9-116">プロバイダーは、ユーザーのサインイン資格情報に基づいてトークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="514d9-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="514d9-117">Bot は、トークンを使用して、メールサービスなど、認証を必要とするリソースにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="514d9-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="514d9-118">詳細については、「  [ボットの Microsoft Teams 認証フロー](auth-flow-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="514d9-119">**Microsoft Teams 内で bot を統合する方法**。</span><span class="sxs-lookup"><span data-stu-id="514d9-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="514d9-120">Bot が統合されたら、チャットでサインインしてメッセージを交換することができます。</span><span class="sxs-lookup"><span data-stu-id="514d9-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="514d9-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="514d9-121">Prerequisites</span></span>

- <span data-ttu-id="514d9-122">ボットの [基礎][concept-basics]知識、 [状態の管理][concept-state]、 [ダイアログライブラリ][concept-dialogs]、 [シーケンシャルな会話フローを実装][simple-dialog]する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="514d9-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="514d9-123">Azure および OAuth 2.0 の開発に関する知識。</span><span class="sxs-lookup"><span data-stu-id="514d9-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="514d9-124">現在のバージョンの Visual Studio および Git。</span><span class="sxs-lookup"><span data-stu-id="514d9-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="514d9-125">Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="514d9-125">Azure account.</span></span> <span data-ttu-id="514d9-126">必要に応じて、 [Azure 無料アカウント](https://azure.microsoft.com/free/)を作成できます。</span><span class="sxs-lookup"><span data-stu-id="514d9-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="514d9-127">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="514d9-127">The following sample.</span></span>

    | <span data-ttu-id="514d9-128">サンプル</span><span class="sxs-lookup"><span data-stu-id="514d9-128">Sample</span></span> | <span data-ttu-id="514d9-129">BotBuilder のバージョン</span><span class="sxs-lookup"><span data-stu-id="514d9-129">BotBuilder version</span></span> | <span data-ttu-id="514d9-130">もの</span><span class="sxs-lookup"><span data-stu-id="514d9-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="514d9-131">**Bot authentication** [(Cs 認証)-auth-サンプル][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="514d9-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="514d9-132">ipv4</span><span class="sxs-lookup"><span data-stu-id="514d9-132">v4</span></span> | <span data-ttu-id="514d9-133">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="514d9-133">OAuthCard support</span></span> |
    | <span data-ttu-id="514d9-134">Js の**ボット認証** [-auth-サンプル][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="514d9-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="514d9-135">ipv4</span><span class="sxs-lookup"><span data-stu-id="514d9-135">v4</span></span>| <span data-ttu-id="514d9-136">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="514d9-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="514d9-137">Py での**Bot 認証**-[サンプル][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="514d9-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="514d9-138">ipv4</span><span class="sxs-lookup"><span data-stu-id="514d9-138">v4</span></span> | <span data-ttu-id="514d9-139">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="514d9-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="514d9-140">リソースグループを作成する</span><span class="sxs-lookup"><span data-stu-id="514d9-140">Create the resource group</span></span>

<span data-ttu-id="514d9-141">リソースグループとサービスプランは厳密には必要ありませんが、作成したリソースを容易に解放することができます。</span><span class="sxs-lookup"><span data-stu-id="514d9-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="514d9-142">これは、リソースを整理して管理できるようにするための適切な方法です。</span><span class="sxs-lookup"><span data-stu-id="514d9-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="514d9-143">リソースグループを使用して、Bot フレームワークの個々のリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="514d9-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="514d9-144">パフォーマンスを確保するために、これらのリソースが同じ Azure 地域にあることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="514d9-145">ブラウザーで、 [**Azure portal**][azure-portal]にサインインします。</span><span class="sxs-lookup"><span data-stu-id="514d9-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="514d9-146">左側のナビゲーションパネルで、[ **リソースグループ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="514d9-147">表示されたウィンドウの左上で、[タブの **追加** ] を選択して新しいリソースグループを作成します。</span><span class="sxs-lookup"><span data-stu-id="514d9-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="514d9-148">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="514d9-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="514d9-149">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="514d9-149">**Subscription**.</span></span> <span data-ttu-id="514d9-150">既存のサブスクリプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="514d9-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="514d9-151">**リソースグループ**。</span><span class="sxs-lookup"><span data-stu-id="514d9-151">**Resource group**.</span></span> <span data-ttu-id="514d9-152">リソースグループの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-152">Enter the name for the resource group.</span></span> <span data-ttu-id="514d9-153">例として、  *Teamsresourcegroup*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="514d9-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="514d9-154">名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="514d9-155">[ **地域** ] ドロップダウンメニューから [ *West US*] を選択するか、アプリケーションに近い地域を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="514d9-156">[ **確認して作成** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-156">Select the **Review and create** button.</span></span> <span data-ttu-id="514d9-157">*検証が成功*したことを示すバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="514d9-158">[ **作成** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-158">Select the **Create** button.</span></span> <span data-ttu-id="514d9-159">リソースグループの作成には、数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="514d9-160">このチュートリアルの後の方で作成するリソースと同様に、このリソースグループをダッシュボードに固定して簡単にアクセスできるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="514d9-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="514d9-161">これを行う場合は、pin アイコン & # 128204; を選びます。ダッシュボードの右上にあります。</span><span class="sxs-lookup"><span data-stu-id="514d9-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="514d9-162">サービスプランを作成する</span><span class="sxs-lookup"><span data-stu-id="514d9-162">Create the service plan</span></span>

1. <span data-ttu-id="514d9-163">[**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[**リソースの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="514d9-164">[検索] ボックスに「 *App Service Plan*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="514d9-165">検索結果から **App Service プラン** カードを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="514d9-166">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-166">Select **Create**.</span></span>
1. <span data-ttu-id="514d9-167">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="514d9-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="514d9-168">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="514d9-168">**Subscription**.</span></span> <span data-ttu-id="514d9-169">既存のサブスクリプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="514d9-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="514d9-170">**リソースグループ**。</span><span class="sxs-lookup"><span data-stu-id="514d9-170">**Resource Group**.</span></span> <span data-ttu-id="514d9-171">前に作成したグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="514d9-172">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="514d9-172">**Name**.</span></span> <span data-ttu-id="514d9-173">サービスプランの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-173">Enter the name for the service plan.</span></span> <span data-ttu-id="514d9-174">例としては、  *Teamsserviceplan*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="514d9-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="514d9-175">グループ内の名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="514d9-176">**オペレーティングシステム**。</span><span class="sxs-lookup"><span data-stu-id="514d9-176">**Operating System**.</span></span> <span data-ttu-id="514d9-177">*Windows*または該当する OS を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="514d9-178">**地域**。</span><span class="sxs-lookup"><span data-stu-id="514d9-178">**Region**.</span></span> <span data-ttu-id="514d9-179">[ *WEST US* ] または [アプリケーションに近い地域] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="514d9-180">**価格レベル**。</span><span class="sxs-lookup"><span data-stu-id="514d9-180">**Pricing Tier**.</span></span> <span data-ttu-id="514d9-181">*標準 S1*が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="514d9-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="514d9-182">これは既定値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-182">This should be the default value.</span></span>
    1. <span data-ttu-id="514d9-183">[ **確認して作成** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-183">Select the **Review and create** button.</span></span> <span data-ttu-id="514d9-184">*検証が成功*したことを示すバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="514d9-185">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-185">Select **Create**.</span></span> <span data-ttu-id="514d9-186">App service プランを作成するには、数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="514d9-187">計画がリソースグループに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="514d9-188">Bot チャネル登録を作成する</span><span class="sxs-lookup"><span data-stu-id="514d9-188">Create the bot channels registration</span></span>

<span data-ttu-id="514d9-189">Bot チャネル登録は、Microsoft アプリ Id とアプリパスワード (クライアントシークレット) がある場合に、ボットフレームワークを使用して web サービスをボットとして登録します。</span><span class="sxs-lookup"><span data-stu-id="514d9-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="514d9-190">Bot が Azure でホストされていない場合にのみ、ボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="514d9-191">Azure ポータルを使用して [ボットを作成](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) した場合は、既にサービスに登録されています。</span><span class="sxs-lookup"><span data-stu-id="514d9-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="514d9-192">Bot [フレームワーク](https://dev.botframework.com/bots/new) または [appstudio](~/concepts/build-and-test/app-studio-overview.md) を使用して bot を作成した場合、その bot は Azure に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="514d9-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="514d9-193">Bot チャネル登録リソースは、[West US] を選択した場合でも、 **グローバル** 地域を表示します。</span><span class="sxs-lookup"><span data-stu-id="514d9-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="514d9-194">これは正常な動作です。</span><span class="sxs-lookup"><span data-stu-id="514d9-194">This is expected.</span></span>

<span data-ttu-id="514d9-195">詳細については、「 [Teams の bot を作成する](../create-a-bot-for-teams.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="514d9-196">Id プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="514d9-196">Create the identity provider</span></span>

<span data-ttu-id="514d9-197">認証に使用できる id プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="514d9-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="514d9-198">この手順では、Azure AD プロバイダーを使用します。他の Azure AD でサポートされている id プロバイダーを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="514d9-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="514d9-199">[**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[ **azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="514d9-200">アプリケーションによって要求されたアクセス許可の委任を承認するには、この Azure AD リソースを作成してテナントに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="514d9-201">テナントを作成する手順については、「 [ポータルにアクセスし、テナントを作成](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="514d9-202">左側のパネルで、[ **アプリの登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="514d9-203">右パネルで、左上にある [ **新しい登録** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="514d9-204">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="514d9-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="514d9-205">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="514d9-205">**Name**.</span></span> <span data-ttu-id="514d9-206">アプリケーションの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-206">Enter the name for the application.</span></span> <span data-ttu-id="514d9-207">例として、  *BotTeamsIdentity*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="514d9-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="514d9-208">名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="514d9-209">アプリケーションに対し **てサポートされているアカウントの種類** を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="514d9-210">*任意の組織ディレクトリ (任意の AZURE AD ディレクトリ-マルチテナント) と個人の Microsoft アカウント (Skype、Xbox など) でアカウント*を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="514d9-211">**リダイレクト URI**の場合:</span><span class="sxs-lookup"><span data-stu-id="514d9-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="514d9-212">[ **Web**] を &#x2713;選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="514d9-213">&#x2713; URL をに設定 `https://token.botframework.com/.auth/web/redirect` します。</span><span class="sxs-lookup"><span data-stu-id="514d9-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="514d9-214">[**登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-214">Select **Register**.</span></span>

1. <span data-ttu-id="514d9-215">作成されたアプリの **概要** ページが Azure に表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="514d9-216">次の情報をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="514d9-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="514d9-217">**アプリケーション (クライアント) ID**値。</span><span class="sxs-lookup"><span data-stu-id="514d9-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="514d9-218">この値は、この Azure id アプリケーションを bot に登録するときに、 *クライアント ID* として後で使用します。</span><span class="sxs-lookup"><span data-stu-id="514d9-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="514d9-219">**ディレクトリ (テナント) ID**の値。</span><span class="sxs-lookup"><span data-stu-id="514d9-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="514d9-220">この値を後で *テナント id* として使用して、この Azure id アプリケーションを bot に登録することもできます。</span><span class="sxs-lookup"><span data-stu-id="514d9-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="514d9-221">左側のパネルで、[ **証明書 & シークレット** ] を選択して、アプリケーションのクライアントシークレットを作成します。</span><span class="sxs-lookup"><span data-stu-id="514d9-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="514d9-222">[ **クライアントシークレット**] で、[ **新しいクライアントシークレット**&#x2795;] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="514d9-223">このシークレットを、 *Teams の Bot id アプリ*など、このアプリ用に作成する必要がある他のユーザーから識別するための説明を追加します。</span><span class="sxs-lookup"><span data-stu-id="514d9-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="514d9-224">選択範囲に **期限** を設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="514d9-225">**[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-225">Select **Add**.</span></span>
   1. <span data-ttu-id="514d9-226">このページを終了する前に、 **シークレットを録音して**ください。</span><span class="sxs-lookup"><span data-stu-id="514d9-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="514d9-227">この値は、ボットを使用して Azure AD アプリケーションを登録するときに、 _クライアントシークレット_ として後で使用します。</span><span class="sxs-lookup"><span data-stu-id="514d9-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="514d9-228">Id プロバイダー接続を構成し、bot に登録する</span><span class="sxs-lookup"><span data-stu-id="514d9-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="514d9-229">注: サービスプロバイダーには、次の2つのオプションがあります。 Azure AD V1 と Azure AD V2。</span><span class="sxs-lookup"><span data-stu-id="514d9-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="514d9-230">[ここ](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)では、2つのプロバイダー間の相違点について要約していますが、通常、バージョン V2 は bot のアクセス許可の変更に関してより柔軟に対応しています。</span><span class="sxs-lookup"><span data-stu-id="514d9-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="514d9-231">Graph API のアクセス許可は、[範囲] フィールドに一覧表示されており、新しいものが追加されたときに、ボットを使用すると、ユーザーは次のサインイン時に新しいアクセス許可に同意することができます。</span><span class="sxs-lookup"><span data-stu-id="514d9-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="514d9-232">V1 の場合、新しい権限を OAuth ダイアログで確認するには、ユーザーが bot の同意を削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="514d9-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="514d9-233">Azure AD V1</span></span>

1. <span data-ttu-id="514d9-234">[**Azure portal**][azure-portal]で、ダッシュボードからリソースグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="514d9-235">Bot チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="514d9-236">[リソース] ページで、[ **設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-236">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="514d9-237">ページの下部付近にある [ **OAuth 接続設定** ] で、[ **設定の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-237">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="514d9-238">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-238">Complete the form as follows:</span></span>

    1. <span data-ttu-id="514d9-239">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="514d9-239">**Name**.</span></span> <span data-ttu-id="514d9-240">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-240">Enter a name for the connection.</span></span> <span data-ttu-id="514d9-241">この名前は、ファイル内の bot で使用し `appsettings.json` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-241">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="514d9-242">たとえば、 *BotTeamsAuthADv1*のようになります。</span><span class="sxs-lookup"><span data-stu-id="514d9-242">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="514d9-243">**サービスプロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="514d9-243">**Service Provider**.</span></span> <span data-ttu-id="514d9-244">[**Azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-244">Select **Azure Active Directory**.</span></span> <span data-ttu-id="514d9-245">このチェックボックスをオンにすると、Azure AD 固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-245">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="514d9-246">**クライアント id**。前述の手順で、Azure id プロバイダアプリ用に記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-246">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="514d9-247">**クライアントシークレット**。</span><span class="sxs-lookup"><span data-stu-id="514d9-247">**Client secret**.</span></span> <span data-ttu-id="514d9-248">前述の手順で、Azure id プロバイダアプリ用に記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-248">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="514d9-249">**許可の種類**。</span><span class="sxs-lookup"><span data-stu-id="514d9-249">**Grant Type**.</span></span> <span data-ttu-id="514d9-250">Enter キーを押し `authorization_code` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-250">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="514d9-251">**ログイン URL**。</span><span class="sxs-lookup"><span data-stu-id="514d9-251">**Login URL**.</span></span> <span data-ttu-id="514d9-252">Enter キーを押し `https://login.microsoftonline.com` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-252">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="514d9-253">[**テナント id**] は、id プロバイダーアプリの作成時に選択したサポートされるアカウントの種類**に応じて**、前の手順で Azure id アプリ用に記録した**ディレクトリ (テナント) id**を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-253">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="514d9-254">割り当てる値を決定するには、次の条件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-254">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="514d9-255">[ *この組織ディレクトリにあるアカウント] のみ (microsoft only-単一テナント)* または *任意の組織ディレクトリのアカウント (microsoft AAD ディレクトリ-マルチテナント)* を選択した場合は、AAD アプリの前に記録した **テナント ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-255">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="514d9-256">これは、認証が可能なユーザーに関連付けられているテナントになります。</span><span class="sxs-lookup"><span data-stu-id="514d9-256">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="514d9-257">任意の組織ディレクトリでアカウントを選択した場合 *(任意の AAD ディレクトリ-マルチテナントおよび個人の Microsoft アカウント (Skype、Xbox、Outlook など)* の場合は、テナント ID ではなく **common** という単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-257">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="514d9-258">それ以外の場合、AAD アプリは、ID が選択されたテナントを経由して検証し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="514d9-258">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="514d9-259">h.</span><span class="sxs-lookup"><span data-stu-id="514d9-259">h.</span></span> <span data-ttu-id="514d9-260">[ **リソースの URL**] で、と入力し `https://graph.microsoft.com/` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-260">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="514d9-261">これは、現在のコードサンプルでは使用されません。</span><span class="sxs-lookup"><span data-stu-id="514d9-261">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="514d9-262">i.</span><span class="sxs-lookup"><span data-stu-id="514d9-262">i.</span></span> <span data-ttu-id="514d9-263">**範囲**を空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="514d9-263">Leave **Scopes** blank.</span></span> <span data-ttu-id="514d9-264">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-264">The following image is an example:</span></span>

    ![teams bot app auth 接続文字列 adv1 ビュー](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="514d9-266">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-266">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="514d9-267">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="514d9-267">Azure AD V2</span></span>

1. <span data-ttu-id="514d9-268">[**Azure portal**][azure-portal]で、ダッシュボードからリソースグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-268">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="514d9-269">Bot チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-269">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="514d9-270">[リソース] ページで、[ **設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-270">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="514d9-271">ページの下部付近にある [ **OAuth 接続設定** ] で、[ **設定の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-271">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="514d9-272">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-272">Complete the form as follows:</span></span>

    1. <span data-ttu-id="514d9-273">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="514d9-273">**Name**.</span></span> <span data-ttu-id="514d9-274">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-274">Enter a name for the connection.</span></span> <span data-ttu-id="514d9-275">この名前は、ファイル内の bot で使用し `appsettings.json` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-275">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="514d9-276">たとえば、 *BotTeamsAuthADv2*のようになります。</span><span class="sxs-lookup"><span data-stu-id="514d9-276">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="514d9-277">**サービスプロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="514d9-277">**Service Provider**.</span></span> <span data-ttu-id="514d9-278">[ **Azure Active Directory v2**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-278">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="514d9-279">このチェックボックスをオンにすると、Azure AD 固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-279">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="514d9-280">**クライアント id**。前述の手順で、Azure id プロバイダアプリ用に記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-280">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="514d9-281">**クライアントシークレット**。</span><span class="sxs-lookup"><span data-stu-id="514d9-281">**Client secret**.</span></span> <span data-ttu-id="514d9-282">前述の手順で、Azure id プロバイダアプリ用に記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-282">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="514d9-283">**トークン交換 URL**。</span><span class="sxs-lookup"><span data-stu-id="514d9-283">**Token Exchange URL**.</span></span> <span data-ttu-id="514d9-284">空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="514d9-284">Leave this blank.</span></span>
    1. <span data-ttu-id="514d9-285">[**テナント id**] は、id プロバイダーアプリの作成時に選択したサポートされるアカウントの種類**に応じて**、前の手順で Azure id アプリ用に記録した**ディレクトリ (テナント) id**を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-285">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="514d9-286">割り当てる値を決定するには、次の条件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-286">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="514d9-287">[ *この組織ディレクトリにあるアカウント] のみ (microsoft only-単一テナント)* または *任意の組織ディレクトリのアカウント (microsoft AAD ディレクトリ-マルチテナント)* を選択した場合は、AAD アプリの前に記録した **テナント ID** を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-287">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="514d9-288">これは、認証が可能なユーザーに関連付けられているテナントになります。</span><span class="sxs-lookup"><span data-stu-id="514d9-288">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="514d9-289">任意の組織ディレクトリでアカウントを選択した場合 *(任意の AAD ディレクトリ-マルチテナントおよび個人の Microsoft アカウント (Skype、Xbox、Outlook など)* の場合は、テナント ID ではなく **common** という単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-289">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="514d9-290">それ以外の場合、AAD アプリは、ID が選択されたテナントを経由して検証し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="514d9-290">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="514d9-291">**範囲**には、このアプリケーションに必要な graph のアクセス許可のスペースで区切られたリストを入力します。たとえば、ユーザーです。すべてのメールを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="514d9-291">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="514d9-292">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-292">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="514d9-293">接続をテストする</span><span class="sxs-lookup"><span data-stu-id="514d9-293">Test the connection</span></span>

1. <span data-ttu-id="514d9-294">接続エントリを選択して、作成したばかりの接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="514d9-294">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="514d9-295">[**サービスプロバイダ接続設定**] パネルの上部にある [**テスト接続**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-295">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="514d9-296">最初にこの操作を行うと、新しいブラウザーウィンドウが開き、アカウントを選択するように求められます。</span><span class="sxs-lookup"><span data-stu-id="514d9-296">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="514d9-297">使用するものを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-297">Select the one you want to use.</span></span>
1. <span data-ttu-id="514d9-298">次に、id プロバイダーがデータ (資格情報) を使用することを許可するように求められます。</span><span class="sxs-lookup"><span data-stu-id="514d9-298">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="514d9-299">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-299">The following image is an example:</span></span>

    ![teams bot 認証接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="514d9-301">**[同意する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-301">Select **Accept**.</span></span>
1. <span data-ttu-id="514d9-302">これで、[ **テスト接続は \<your-connection-name> 成功しまし** た] ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="514d9-302">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="514d9-303">エラーが表示された場合は、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="514d9-303">Refresh the page if you get an error.</span></span> <span data-ttu-id="514d9-304">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-304">The following image is an example:</span></span>

  ![teams bot app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="514d9-306">接続名は、ユーザー認証トークンを取得するために bot コードによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-306">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="514d9-307">Bot サンプルコードを準備する</span><span class="sxs-lookup"><span data-stu-id="514d9-307">Prepare the bot sample code</span></span>

<span data-ttu-id="514d9-308">事前設定を完了したら、この記事で使用する bot の作成に重点を置いて説明します。</span><span class="sxs-lookup"><span data-stu-id="514d9-308">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="514d9-309">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="514d9-309">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="514d9-310">複製の [cs-auth-サンプル][teams-auth-bot-cs]。</span><span class="sxs-lookup"><span data-stu-id="514d9-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="514d9-311">Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-311">Launch Visual Studio.</span></span>
1. <span data-ttu-id="514d9-312">ツールバーの [ **ファイル]-> [> プロジェクト/ソリューション** ] を選択し、bot プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="514d9-312">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="514d9-313">C# Update では、次 \*\* のようにappsettings.js\*\* ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-313">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="514d9-314">`ConnectionName`Bot チャネル登録に追加した id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-314">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="514d9-315">この例で使用した名前は *BotTeamsAuthADv1*です。</span><span class="sxs-lookup"><span data-stu-id="514d9-315">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="514d9-316">`MicrosoftAppId`Bot チャネル登録時に保存した**BOT アプリ ID**に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-316">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="514d9-317">`MicrosoftAppPassword`Bot チャネル登録時に保存した**お客様のシークレット**に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-317">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="514d9-318">`ConnectionName`を id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-318">Set the `ConnectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="514d9-319">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-319">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="514d9-320">たとえば、任意のアンパサンド (&) をとしてエンコードする必要があり `&amp;` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-320">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="514d9-321">ソリューションエクスプローラーで、フォルダーに移動して、 `TeamsAppManifest` `manifest.json` `id` `botId` ボットチャネルの登録時に保存した **bot アプリ ID** を開き、設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-321">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="514d9-322">JavaScript</span><span class="sxs-lookup"><span data-stu-id="514d9-322">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="514d9-323">クローン [ノード-auth-サンプル][teams-auth-bot-js]。</span><span class="sxs-lookup"><span data-stu-id="514d9-323">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="514d9-324">コンソールで、プロジェクトに移動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-324">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="514d9-325">モジュールをインストールする</span><span class="sxs-lookup"><span data-stu-id="514d9-325">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="514d9-326">次のようにして、 **env** 構成を更新します。</span><span class="sxs-lookup"><span data-stu-id="514d9-326">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="514d9-327">`MicrosoftAppId`Bot チャネル登録時に保存した**BOT アプリ ID**に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-327">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="514d9-328">`MicrosoftAppPassword`Bot チャネル登録時に保存した**お客様のシークレット**に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-328">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="514d9-329">`connectionName`を id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-329">Set the `connectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="514d9-330">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-330">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="514d9-331">たとえば、任意のアンパサンド (&) をとしてエンコードする必要があり `&amp;` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-331">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="514d9-332">フォルダーで `teamsAppManifest` 、 `manifest.json` `id` **Microsoft アプリ id** を開き、 `botId` ボットチャネル登録時に保存した **bot アプリ id** を設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-332">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="514d9-333">Python</span><span class="sxs-lookup"><span data-stu-id="514d9-333">Python</span></span>](#tab/python)

1. <span data-ttu-id="514d9-334">Github リポジトリからの複製 [py-サンプル][teams-auth-bot-py] 。</span><span class="sxs-lookup"><span data-stu-id="514d9-334">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="514d9-335">**Config.py**を更新します。</span><span class="sxs-lookup"><span data-stu-id="514d9-335">Update **config.py**:</span></span>

    - <span data-ttu-id="514d9-336">`ConnectionName`Bot に追加した OAuth 接続設定の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-336">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="514d9-337">`MicrosoftAppId` `MicrosoftAppPassword` Bot のアプリ ID とアプリシークレットを設定します。</span><span class="sxs-lookup"><span data-stu-id="514d9-337">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="514d9-338">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-338">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="514d9-339">たとえば、任意のアンパサンド (&) をとしてエンコードする必要があり `&amp;` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-339">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="514d9-340">Bot を Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="514d9-340">Deploy the bot to Azure</span></span>

<span data-ttu-id="514d9-341">Bot を展開するには、「 [Azure に bot を展開](https://aka.ms/azure-bot-deployment-cli)する方法」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="514d9-341">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="514d9-342">または、Visual Studio では、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="514d9-342">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="514d9-343">Visual Studio の *ソリューションエクスプローラー* で、プロジェクト名を選択して、ホールド (または右クリック) します。</span><span class="sxs-lookup"><span data-stu-id="514d9-343">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="514d9-344">ドロップダウンメニューで、[ **発行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-344">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="514d9-345">表示されたウィンドウで、 **新しい** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-345">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="514d9-346">ダイアログウィンドウで、左側にある [ **App Service** ] を選択し、右側に [ **新規作成** ] を作成します。</span><span class="sxs-lookup"><span data-stu-id="514d9-346">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="514d9-347">[ **発行** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-347">Select the **Publish** button.</span></span>
1. <span data-ttu-id="514d9-348">次のダイアログウィンドウで、必要な情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-348">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="514d9-349">例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="514d9-349">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="514d9-351">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-351">Select **Create**.</span></span>
1. <span data-ttu-id="514d9-352">展開が正常に完了すると、Visual Studio に反映されたことがわかります。</span><span class="sxs-lookup"><span data-stu-id="514d9-352">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="514d9-353">さらに、 *ボットの準備ができ*たことを示すページが既定のブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-353">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="514d9-354">URL は、次のようになり `https://botteamsauth.azurewebsites.net/` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-354">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="514d9-355">ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="514d9-355">Save it to a file.</span></span>
1. <span data-ttu-id="514d9-356">ブラウザーで [**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-356">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="514d9-357">リソースグループを確認すると、bot が他のリソースと共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-357">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="514d9-358">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-358">The following image is an example:</span></span>

    ![teams-auth-service-グループ](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="514d9-360">[リソース] グループで、bot チャネル登録名 (リンク) を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-360">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="514d9-361">左側のパネルで、[ **設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-361">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="514d9-362">[ **メッセージングエンドポイント** ] ボックスに、上で取得した URL に続けてを入力し `api/messages` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-362">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="514d9-363">次に例を示します `https://botteamsauth.azurewebsites.net/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="514d9-363">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="514d9-364">左上隅にある [ **保存** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-364">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="514d9-365">エミュレーターを使用して bot をテストする</span><span class="sxs-lookup"><span data-stu-id="514d9-365">Test the bot using the Emulator</span></span>

<span data-ttu-id="514d9-366">まだ行っていない場合は、 [Microsoft Bot フレームワークエミュレーター](https://aka.ms/bot-framework-emulator-readme)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="514d9-366">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="514d9-367">「 [エミュレーターを使用してデバッグする](https://aka.ms/bot-framework-emulator-debug-with-emulator)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-367">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="514d9-368">Bot のサンプルログインを機能させるには、以下のようにエミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-368">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="514d9-369">認証用にエミュレーターを構成する</span><span class="sxs-lookup"><span data-stu-id="514d9-369">Configure the Emulator for authentication</span></span>

<span data-ttu-id="514d9-370">Bot が認証を必要とする場合は、以下に示すように、エミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-370">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="514d9-371">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-371">Start the Emulator.</span></span>
1. <span data-ttu-id="514d9-372">エミュレーターで、左下の歯車アイコン &#9881;、または右上の [ **エミュレーターの設定** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-372">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="514d9-373">チェックボックスをオンにするには、 **バージョン1.0 の認証トークンを使用**します。</span><span class="sxs-lookup"><span data-stu-id="514d9-373">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="514d9-374">**Ngrok**ツールへのローカルパスを入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-374">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="514d9-375">Bot フレームワークエミュレーター/ngrok トンネリング統合[Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="514d9-375">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="514d9-376">ツールの詳細については、「 [ngrok](https://ngrok.com/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="514d9-376">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="514d9-377">**エミュレーター起動時に ngrok を実行**してチェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="514d9-377">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="514d9-378">[ **保存** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-378">Select the **Save** button.</span></span>

<span data-ttu-id="514d9-379">Bot がサインインカードを表示し、ユーザーがサインインボタンを選択すると、ユーザーが認証プロバイダーでサインインするために使用できるページがエミュレーターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-379">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="514d9-380">ユーザーがこれを実行すると、プロバイダーはユーザートークンを生成して bot に送信します。</span><span class="sxs-lookup"><span data-stu-id="514d9-380">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="514d9-381">その後、bot はユーザーの代わりに行動することができます。</span><span class="sxs-lookup"><span data-stu-id="514d9-381">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="514d9-382">Bot をローカルでテストする</span><span class="sxs-lookup"><span data-stu-id="514d9-382">Test the bot locally</span></span>

<span data-ttu-id="514d9-383">認証メカニズムを構成した後は、実際の bot テストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="514d9-383">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="514d9-384">Visual Studio を使用して、お使いのコンピューターでローカルに bot サンプルを実行します。</span><span class="sxs-lookup"><span data-stu-id="514d9-384">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="514d9-385">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-385">Start the Emulator.</span></span>
1. <span data-ttu-id="514d9-386">[ **Open bot** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-386">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="514d9-387">Bot の **url**に bot のローカル url を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-387">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="514d9-388">通常は、 `http://localhost:3978/api/messages` です。</span><span class="sxs-lookup"><span data-stu-id="514d9-388">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="514d9-389">**Microsoft アプリ id**で、bot のアプリ id をから入力し `appsettings.json` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-389">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="514d9-390">**Microsoft App パスワード**に、からの bot のアプリパスワードを入力し `appsettings.json` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-390">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="514d9-391">[ **接続**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-391">Select **Connect**.</span></span>
1. <span data-ttu-id="514d9-392">Bot が起動して実行されたら、サインインカードを表示するテキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-392">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="514d9-393">**[サインイン]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-393">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="514d9-394">開いている **URL を確認**するポップアップダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-394">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="514d9-395">これにより、ボットのユーザー (ユーザー) が認証されるようになります。</span><span class="sxs-lookup"><span data-stu-id="514d9-395">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="514d9-396">[ **確認**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-396">Select **Confirm**.</span></span>
1. <span data-ttu-id="514d9-397">要求された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-397">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="514d9-398">エミュレーターで使用した構成に応じて、次のいずれかを取得します。</span><span class="sxs-lookup"><span data-stu-id="514d9-398">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="514d9-399">**サインイン確認コードの使用**</span><span class="sxs-lookup"><span data-stu-id="514d9-399">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="514d9-400">検証コードを表示するウィンドウが開かれて &#x2713; ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-400">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="514d9-401">サインインを完了するには、&#x2713; コピーして、検証コードを [チャット] ボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-401">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="514d9-402">**認証トークンを使用**します。</span><span class="sxs-lookup"><span data-stu-id="514d9-402">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="514d9-403">資格情報に基づいてログインしている &#x2713;。</span><span class="sxs-lookup"><span data-stu-id="514d9-403">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="514d9-404">次の図は、ログインした後の bot UI の例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-404">The following image is an example of the bot UI after you've logged in:</span></span>

    ![auth bot ログインエミュレーター](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="514d9-406">Bot から*トークンを表示するよう*求められたときに **[はい**] を選択すると、次のような応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-406">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![auth bot ログインエミュレータートークン](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="514d9-408">サインアウトするには、[チャットの入力] ボックスに「 **ログアウト** 」と入力します。これにより、ユーザートークンが解放され、再びサインインするまでは、お客様の代わりに bot を操作することはできません。</span><span class="sxs-lookup"><span data-stu-id="514d9-408">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="514d9-409">Bot 認証には、 **Bot コネクタサービス**を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-409">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="514d9-410">サービスは bot の bot チャネル登録情報にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="514d9-410">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="514d9-411">展開した bot をテストする</span><span class="sxs-lookup"><span data-stu-id="514d9-411">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="514d9-412">ブラウザーで [**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-412">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="514d9-413">リソースグループを検索します。</span><span class="sxs-lookup"><span data-stu-id="514d9-413">Find your resource group.</span></span>
1. <span data-ttu-id="514d9-414">[リソース] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-414">Select the resource link.</span></span> <span data-ttu-id="514d9-415">[リソース] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-415">The resource page is displayed.</span></span>
1. <span data-ttu-id="514d9-416">[リソース] ページで、[ **Web チャットでテスト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-416">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="514d9-417">Bot が開始し、定義済みの案内応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-417">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="514d9-418">[チャット] ボックスに何か入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-418">Type anything in the chat box.</span></span>
1. <span data-ttu-id="514d9-419">[ **サインイン** ] ボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-419">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="514d9-420">開いている **URL を確認**するポップアップダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-420">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="514d9-421">これにより、ボットのユーザー (ユーザー) が認証されるようになります。</span><span class="sxs-lookup"><span data-stu-id="514d9-421">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="514d9-422">[ **確認**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-422">Select **Confirm**.</span></span>
1. <span data-ttu-id="514d9-423">要求された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-423">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="514d9-424">次の図は、ログインした後の bot UI の例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-424">The following image is an example of the bot UI after you have logged in:</span></span>

    ![auth bot ログインの展開](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="514d9-426">.</span><span class="sxs-lookup"><span data-stu-id="514d9-426">.</span></span>

1. <span data-ttu-id="514d9-427">[ **はい** ] ボタンを選択して、認証トークンを表示します。</span><span class="sxs-lookup"><span data-stu-id="514d9-427">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="514d9-428">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-428">The following image is an example:</span></span>

    ![auth bot ログイン展開されたトークン](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="514d9-430">.</span><span class="sxs-lookup"><span data-stu-id="514d9-430">.</span></span>

1. <span data-ttu-id="514d9-431">サインアウトするには、「ログアウト」と入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-431">Enter logout to sign out.</span></span>

    ![auth bot が展開したログアウト](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="514d9-433">サインインで問題が発生した場合は、前の手順で説明したように、接続をもう一度テストしてください。</span><span class="sxs-lookup"><span data-stu-id="514d9-433">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="514d9-434">これにより、認証トークンが再作成されることがあります。</span><span class="sxs-lookup"><span data-stu-id="514d9-434">This could recreate the authentication token.</span></span>
> <span data-ttu-id="514d9-435">「Azure の Bot フレームワーク Web チャットクライアント」では、認証が正しく設定される前に、数回サインインする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-435">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="514d9-436">Teams に bot をインストールしてテストする</span><span class="sxs-lookup"><span data-stu-id="514d9-436">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="514d9-437">Bot プロジェクトで、フォルダーにとファイルが含まれていることを確認し `TeamsAppManifest` `manifest.json` `outline.png` `color.png` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-437">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="514d9-438">ソリューションエクスプローラーで、フォルダーに移動し `TeamsAppManifest` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-438">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="514d9-439">`manifest.json`次の値を割り当てることによって編集します。</span><span class="sxs-lookup"><span data-stu-id="514d9-439">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="514d9-440">Bot チャネル登録時に受信した **Bot アプリ ID** がおよびに割り当てられていることを確認し `id` `botId` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-440">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="514d9-441">次の値を割り当てます。 `validDomains: [ "token.botframework.com" ]`</span><span class="sxs-lookup"><span data-stu-id="514d9-441">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="514d9-442">、、およびファイルを選択して **zip** にし `manifest.json` `outline.png` `color.png` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-442">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="514d9-443">**Microsoft Teams**を開きます。</span><span class="sxs-lookup"><span data-stu-id="514d9-443">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="514d9-444">左側のパネルで、下部にある [ **アプリ] アイコン**を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-444">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="514d9-445">右側のパネルで、下部にある [ **カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-445">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="514d9-446">フォルダーに移動 `TeamsAppManifest` し、zip マニフェストをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="514d9-446">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="514d9-447">次のウィザードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-447">The following wizard is displayed:</span></span>

    ![auth bot teams のアップロード](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="514d9-449">**[チームに追加]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-449">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="514d9-450">次のウィンドウで、ボットを使用するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-450">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="514d9-451">[ **Bot の設定** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-451">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="514d9-452">左側のパネルで、3つのドット (&#x25cf;&#x25cf;&#x25cf;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-452">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="514d9-453">次に、[ **App Studio** ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-453">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="514d9-454">[ **マニフェストエディター** ] タブを選択します。アップロードした bot のアイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-454">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="514d9-455">また、bot とのメッセージの交換に使用できる連絡先として、その bot が連絡先として表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="514d9-455">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="514d9-456">Teams でボットをローカルにテストする</span><span class="sxs-lookup"><span data-stu-id="514d9-456">Testing the bot locally in Teams</span></span>

<span data-ttu-id="514d9-457">Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからアクセスできるようにするには、すべてのサービスがアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-457">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="514d9-458">そのため、ボット (サンプル) を Teams で使用できるようにするには、選択したクラウドにコードを発行するか、または **トンネル** ツールを使用して、ローカルに実行しているインスタンスを外部からアクセス可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-458">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="514d9-459">[Ngrok](https://ngrok.com/download)を使用することをお勧めします。この URL は、コンピューター上でローカルに開いたポートに対して、外部アドレス指定可能な URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="514d9-459">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="514d9-460">Microsoft Teams アプリをローカルで実行する準備として ngrok をセットアップするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="514d9-460">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="514d9-461">ターミナルウィンドウで、がインストールされているディレクトリに移動し `ngrok.exe` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-461">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="514d9-462">これを指すように、 *環境変数* のパスを設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="514d9-462">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="514d9-463">たとえば、を実行 `ngrok http 3978 --host-header=localhost:3978` します。</span><span class="sxs-lookup"><span data-stu-id="514d9-463">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="514d9-464">必要に応じてポート番号を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="514d9-464">Replace the port number as needed.</span></span>
<span data-ttu-id="514d9-465">これにより、指定したポートをリッスンする ngrok が起動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-465">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="514d9-466">これにより、ngrok が実行されている限り、外部的にアドレス指定可能な URL が得られます。</span><span class="sxs-lookup"><span data-stu-id="514d9-466">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="514d9-467">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-467">The following image is an example:</span></span>

    ![teams bot アプリ認証の接続文字列 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="514d9-469">.</span><span class="sxs-lookup"><span data-stu-id="514d9-469">.</span></span>

1. <span data-ttu-id="514d9-470">転送用の HTTPS アドレスをコピーします。</span><span class="sxs-lookup"><span data-stu-id="514d9-470">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="514d9-471">これは、次のようになり `https://dea822bf.ngrok.io/` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-471">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="514d9-472">`/api/messages`取得する追加 `https://dea822bf.ngrok.io/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="514d9-472">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="514d9-473">これは、コンピューター上でローカルに実行されていて、Microsoft Teams のチャットで web 経由でアクセスできる bot の **メッセージエンドポイント** です。</span><span class="sxs-lookup"><span data-stu-id="514d9-473">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="514d9-474">最後に実行する手順の1つは、展開した bot のメッセージエンドポイントを更新することです。</span><span class="sxs-lookup"><span data-stu-id="514d9-474">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="514d9-475">この例では、bot を Azure に展開しました。</span><span class="sxs-lookup"><span data-stu-id="514d9-475">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="514d9-476">そのため、以下の手順を実行してみましょう。</span><span class="sxs-lookup"><span data-stu-id="514d9-476">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="514d9-477">ブラウザーで [**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-477">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="514d9-478">**Bot チャネル登録**を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-478">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="514d9-479">左側のパネルで、[ **設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="514d9-479">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="514d9-480">右側のパネルの [ **メッセージングエンドポイント** ] ボックスに、ngrok URL (この例では) を入力し `https://dea822bf.ngrok.io/api/messages` ます。</span><span class="sxs-lookup"><span data-stu-id="514d9-480">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="514d9-481">Visual Studio デバッグモードなどで、ボットをローカルに起動します。</span><span class="sxs-lookup"><span data-stu-id="514d9-481">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="514d9-482">Bot フレームワークポータルの **テスト Web チャット**を使用して、ローカルで実行中に bot をテストします。</span><span class="sxs-lookup"><span data-stu-id="514d9-482">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="514d9-483">エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="514d9-483">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="514d9-484">が実行されているターミナルウィンドウで、 `ngrok` ボットと web チャットクライアント間の HTTP トラフィックを確認できます。</span><span class="sxs-lookup"><span data-stu-id="514d9-484">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="514d9-485">より詳細な表示が必要な場合は、ブラウザーウィンドウで `http://127.0.0.1:4040` 以前のターミナルウィンドウから取得した情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="514d9-485">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="514d9-486">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="514d9-486">The following image is an example:</span></span>

    ![auth bot teams ngrok テスト](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="514d9-488">.</span><span class="sxs-lookup"><span data-stu-id="514d9-488">.</span></span>

> [!NOTE]
> <span data-ttu-id="514d9-489">Ngrok を停止してから再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-489">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="514d9-490">プロジェクトで ngrok を使用し、使用している機能に応じて、すべての URL 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-490">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="514d9-491">追加情報</span><span class="sxs-lookup"><span data-stu-id="514d9-491">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="514d9-492">TeamsAppManifest/manifest.js</span><span class="sxs-lookup"><span data-stu-id="514d9-492">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="514d9-493">このマニフェストには、Microsoft Teams が bot と接続するために必要な情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="514d9-493">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

<span data-ttu-id="514d9-494">認証を使用すると、以下に説明するように、Teams は他のチャネルとはやや異なる方法で動作します。</span><span class="sxs-lookup"><span data-stu-id="514d9-494">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="514d9-495">呼び出しアクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="514d9-495">Handling Invoke Activity</span></span>

<span data-ttu-id="514d9-496">**呼び出しアクティビティ**は、他のチャネルによって使用されるイベントアクティビティではなく bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-496">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="514d9-497">これは、 **Activityhandler**のサブクラスによって実行されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-497">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="514d9-498">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="514d9-498">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="514d9-499">**ボット/の bot**</span><span class="sxs-lookup"><span data-stu-id="514d9-499">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="514d9-500">**ボット/TeamsBot**</span><span class="sxs-lookup"><span data-stu-id="514d9-500">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="514d9-501">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-501">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="514d9-502">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="514d9-502">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="514d9-503">JavaScript</span><span class="sxs-lookup"><span data-stu-id="514d9-503">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="514d9-504">**bot/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="514d9-504">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="514d9-505">**bot/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="514d9-505">**bots/teamsBot.js**</span></span>

<span data-ttu-id="514d9-506">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-506">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="514d9-507">**ダイアログ/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="514d9-507">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="514d9-508">ダイアログステップで、を使用し `beginDialog` て OAuth プロンプトを開始します。これにより、ユーザーにサインインするように求められます。</span><span class="sxs-lookup"><span data-stu-id="514d9-508">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="514d9-509">ユーザーが既にサインインしている場合は、ユーザーに確認を求めることなく、トークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-509">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="514d9-510">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-510">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="514d9-511">Azure Bot サービスは、ユーザーがサインインしようとした後に、トークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="514d9-511">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="514d9-512">次のダイアログステップでは、前の手順の結果にトークンが存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="514d9-512">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="514d9-513">Null でない場合、ユーザーは正常にサインインしています。</span><span class="sxs-lookup"><span data-stu-id="514d9-513">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="514d9-514">**bot/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="514d9-514">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="514d9-515">Python</span><span class="sxs-lookup"><span data-stu-id="514d9-515">Python</span></span>](#tab/python-sample)

<span data-ttu-id="514d9-516">**ボット/dialog_bot py**</span><span class="sxs-lookup"><span data-stu-id="514d9-516">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="514d9-517">**ボット/teams_bot py**</span><span class="sxs-lookup"><span data-stu-id="514d9-517">**bots/teams_bot.py**</span></span>

<span data-ttu-id="514d9-518">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="514d9-518">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="514d9-519">**ダイアログ/main_dialog py**</span><span class="sxs-lookup"><span data-stu-id="514d9-519">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="514d9-520">ダイアログステップで、を使用し `begin_dialog` て OAuth プロンプトを開始します。これにより、ユーザーにサインインするように求められます。</span><span class="sxs-lookup"><span data-stu-id="514d9-520">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="514d9-521">ユーザーが既にサインインしている場合は、ユーザーに確認を求めることなく、トークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-521">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="514d9-522">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="514d9-522">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="514d9-523">Azure Bot サービスは、ユーザーがサインインしようとした後に、トークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="514d9-523">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="514d9-524">次のダイアログステップでは、前の手順の結果にトークンが存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="514d9-524">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="514d9-525">Null でない場合、ユーザーは正常にサインインしています。</span><span class="sxs-lookup"><span data-stu-id="514d9-525">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="514d9-526">**ダイアログ/logout_dialog py**</span><span class="sxs-lookup"><span data-stu-id="514d9-526">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="514d9-527">Azure Bot サービスによる追加認証の追加について説明します。</span><span class="sxs-lookup"><span data-stu-id="514d9-527">Learn about adding adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
