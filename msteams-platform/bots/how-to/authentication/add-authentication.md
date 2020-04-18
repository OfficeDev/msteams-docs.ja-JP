---
title: Teams の bot に認証を追加する
author: clearab
description: Microsoft Teams の bot に OAuth 認証を追加する方法。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: f5eae27de45cd0932e4d2ed62fa954429a48aa6d
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550979"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="ff7e4-103">Teams の bot に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="ff7e4-104">メールサービスなど、ユーザーの代わりにリソースにアクセスできる、Microsoft Teams でボットを作成しなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="ff7e4-105">この記事では、OAuth 2.0 に基づいて Azure Bot サービス v4 SDK 認証を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="ff7e4-106">これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットを開発するのが容易になります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="ff7e4-107">すべてのキーこれは、後で説明するように、 **id プロバイダー**を使用していることです。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="ff7e4-108">OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="ff7e4-109">OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="ff7e4-110">基本的な理解と、完全な仕様の[oauth 2.0](https://oauth.net/2/)については、「 [Oauth 2 の単純化](https://aka.ms/oauth2-simplified)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="ff7e4-111">Azure Bot サービスが認証を処理する方法の詳細については、「[会話内のユーザー認証](https://aka.ms/azure-bot-authentication)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="ff7e4-112">この記事では、以下について説明します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-112">In this article you'll learn:</span></span>

- <span data-ttu-id="ff7e4-113">**認証を有効にした bot を作成する方法**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="ff7e4-114">ユーザーのサインイン資格情報と認証トークンの生成を処理するには、 [cs-auth-サンプル][teams-auth-bot-cs]を使用します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="ff7e4-115">**Bot を Azure に展開し、id プロバイダーに関連付ける方法について説明**します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="ff7e4-116">プロバイダーは、ユーザーのサインイン資格情報に基づいてトークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="ff7e4-117">Bot は、トークンを使用して、メールサービスなど、認証を必要とするリソースにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="ff7e4-118">詳細については、「[ボットの Microsoft Teams 認証フロー](auth-flow-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="ff7e4-119">**Microsoft Teams 内で bot を統合する方法**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="ff7e4-120">Bot が統合されたら、チャットでサインインしてメッセージを交換することができます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff7e4-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="ff7e4-121">Prerequisites</span></span>

- <span data-ttu-id="ff7e4-122">ボットの[基礎][concept-basics]知識、[状態の管理][concept-state]、[ダイアログライブラリ][concept-dialogs]、[シーケンシャルな会話フローを実装][simple-dialog]する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="ff7e4-123">Azure および OAuth 2.0 の開発に関する知識。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="ff7e4-124">現在のバージョンの Visual Studio および Git。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="ff7e4-125">Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-125">Azure account.</span></span> <span data-ttu-id="ff7e4-126">必要に応じて、 [Azure 無料アカウント](https://azure.microsoft.com/free/)を作成できます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="ff7e4-127">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-127">The following sample.</span></span>

    | <span data-ttu-id="ff7e4-128">例</span><span class="sxs-lookup"><span data-stu-id="ff7e4-128">Sample</span></span> | <span data-ttu-id="ff7e4-129">BotBuilder のバージョン</span><span class="sxs-lookup"><span data-stu-id="ff7e4-129">BotBuilder version</span></span> | <span data-ttu-id="ff7e4-130">もの</span><span class="sxs-lookup"><span data-stu-id="ff7e4-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="ff7e4-131">**Bot authentication** [(Cs 認証)-auth-サンプル][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="ff7e4-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="ff7e4-132">ipv4</span><span class="sxs-lookup"><span data-stu-id="ff7e4-132">v4</span></span> | <span data-ttu-id="ff7e4-133">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="ff7e4-133">OAuthCard support</span></span> |
    | <span data-ttu-id="ff7e4-134">Js の**ボット認証** [-auth-サンプル][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="ff7e4-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="ff7e4-135">ipv4</span><span class="sxs-lookup"><span data-stu-id="ff7e4-135">v4</span></span>| <span data-ttu-id="ff7e4-136">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="ff7e4-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="ff7e4-137">Py での**Bot 認証**-[サンプル][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="ff7e4-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="ff7e4-138">ipv4</span><span class="sxs-lookup"><span data-stu-id="ff7e4-138">v4</span></span> | <span data-ttu-id="ff7e4-139">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="ff7e4-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="ff7e4-140">リソースグループを作成する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-140">Create the resource group</span></span>

<span data-ttu-id="ff7e4-141">リソースグループとサービスプランは厳密には必要ありませんが、作成したリソースを容易に解放することができます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="ff7e4-142">これは、リソースを整理して管理できるようにするための適切な方法です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="ff7e4-143">リソースグループを使用して、Bot フレームワークの個々のリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="ff7e4-144">パフォーマンスを確保するために、これらのリソースが同じ Azure 地域にあることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="ff7e4-145">ブラウザーで、 [**Azure portal**][azure-portal]にサインインします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="ff7e4-146">左側のナビゲーションパネルで、[**リソースグループ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="ff7e4-147">表示されたウィンドウの左上で、[タブの**追加**] を選択して新しいリソースグループを作成します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="ff7e4-148">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="ff7e4-149">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-149">**Subscription**.</span></span> <span data-ttu-id="ff7e4-150">既存のサブスクリプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="ff7e4-151">**リソースグループ**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-151">**Resource group**.</span></span> <span data-ttu-id="ff7e4-152">リソースグループの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-152">Enter the name for the resource group.</span></span> <span data-ttu-id="ff7e4-153">例として、 *Teamsresourcegroup*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="ff7e4-154">名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="ff7e4-155">[**地域**] ドロップダウンメニューから [ *West US*] を選択するか、アプリケーションに近い地域を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="ff7e4-156">[**確認して作成**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-156">Select the **Review and create** button.</span></span> <span data-ttu-id="ff7e4-157">*検証が成功*したことを示すバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="ff7e4-158">[**作成**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-158">Select the **Create** button.</span></span> <span data-ttu-id="ff7e4-159">リソースグループの作成には、数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="ff7e4-160">このチュートリアルの後の方で作成するリソースと同様に、このリソースグループをダッシュボードに固定して簡単にアクセスできるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="ff7e4-161">これを行う場合は、pin アイコン & # 128204; を選びます。ダッシュボードの右上にあります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="ff7e4-162">サービスプランを作成する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-162">Create the service plan</span></span>

1. <span data-ttu-id="ff7e4-163">[**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[**リソースの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="ff7e4-164">[検索] ボックスに「 *App Service Plan*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="ff7e4-165">検索結果から**App Service プラン**カードを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="ff7e4-166">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-166">Select **Create**.</span></span>
1. <span data-ttu-id="ff7e4-167">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="ff7e4-168">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-168">**Subscription**.</span></span> <span data-ttu-id="ff7e4-169">既存のサブスクリプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="ff7e4-170">**リソースグループ**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-170">**Resource Group**.</span></span> <span data-ttu-id="ff7e4-171">前に作成したグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="ff7e4-172">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-172">**Name**.</span></span> <span data-ttu-id="ff7e4-173">サービスプランの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-173">Enter the name for the service plan.</span></span> <span data-ttu-id="ff7e4-174">例としては、 *Teamsserviceplan*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="ff7e4-175">グループ内の名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="ff7e4-176">**オペレーティングシステム**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-176">**Operating System**.</span></span> <span data-ttu-id="ff7e4-177">*Windows*または該当する OS を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="ff7e4-178">**地域**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-178">**Region**.</span></span> <span data-ttu-id="ff7e4-179">[ *WEST US* ] または [アプリケーションに近い地域] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="ff7e4-180">**価格レベル**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-180">**Pricing Tier**.</span></span> <span data-ttu-id="ff7e4-181">*標準 S1*が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="ff7e4-182">これは既定値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-182">This should be the default value.</span></span>
    1. <span data-ttu-id="ff7e4-183">[**確認して作成**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-183">Select the **Review and create** button.</span></span> <span data-ttu-id="ff7e4-184">*検証が成功*したことを示すバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="ff7e4-185">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-185">Select **Create**.</span></span> <span data-ttu-id="ff7e4-186">App service プランを作成するには、数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="ff7e4-187">計画がリソースグループに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="ff7e4-188">Bot チャネル登録を作成する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-188">Create the bot channels registration</span></span>

<span data-ttu-id="ff7e4-189">Bot チャネル登録は、Microsoft アプリ Id とアプリパスワード (クライアントシークレット) がある場合に、ボットフレームワークを使用して web サービスをボットとして登録します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff7e4-190">Bot が Azure でホストされていない場合にのみ、ボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="ff7e4-191">Azure ポータルを使用して[ボットを作成](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0)した場合は、既にサービスに登録されています。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="ff7e4-192">Bot[フレームワーク](https://dev.botframework.com/bots/new)または[appstudio](~/concepts/build-and-test/app-studio-overview.md)を使用して bot を作成した場合、その bot は Azure に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="ff7e4-193">Azure で登録リソースが作成されると、リソースグループリストに追加されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-193">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![bot アプリチャネル登録グループ](../../../assets/images/authentication/auth-bot-channels-registration-group.PNG)

> [!NOTE]
> <span data-ttu-id="ff7e4-195">Bot チャネル登録リソースは、[West US] を選択した場合でも、**グローバル**地域を表示します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-195">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="ff7e4-196">これは想定されています。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-196">This is expected.</span></span>

<span data-ttu-id="ff7e4-197">詳細については、「 [Teams の bot を作成する](../create-a-bot-for-teams.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-197">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="ff7e4-198">Id プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-198">Create the identity provider</span></span>

<span data-ttu-id="ff7e4-199">認証に使用できる id プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-199">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="ff7e4-200">この手順では、Azure AD プロバイダーを使用します。他の Azure AD でサポートされている id プロバイダーを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-200">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="ff7e4-201">[**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[ **azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-201">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="ff7e4-202">アプリケーションによって要求されたアクセス許可の委任を承認するには、この Azure AD リソースを作成してテナントに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-202">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="ff7e4-203">テナントを作成する手順については、「[ポータルにアクセスし、テナントを作成](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-203">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="ff7e4-204">左側のパネルで、[**アプリの登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-204">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="ff7e4-205">右パネルで、左上にある [**新しい登録**] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-205">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="ff7e4-206">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-206">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="ff7e4-207">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-207">**Name**.</span></span> <span data-ttu-id="ff7e4-208">アプリケーションの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-208">Enter the name for the application.</span></span> <span data-ttu-id="ff7e4-209">例として、 *BotTeamsIdentity*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-209">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="ff7e4-210">名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-210">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="ff7e4-211">アプリケーションに対し**てサポートされているアカウントの種類**を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-211">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="ff7e4-212">*任意の組織ディレクトリ (任意の AZURE AD ディレクトリ-マルチテナント) と個人の Microsoft アカウント (Skype、Xbox など) でアカウント*を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-212">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="ff7e4-213">**リダイレクト URI**の場合:</span><span class="sxs-lookup"><span data-stu-id="ff7e4-213">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="ff7e4-214">[ **Web**] を &#x2713;選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-214">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="ff7e4-215">&#x2713; URL をに`https://token.botframework.com/.auth/web/redirect`設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-215">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="ff7e4-216">[**登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-216">Select **Register**.</span></span>

1. <span data-ttu-id="ff7e4-217">作成されたアプリの**概要**ページが Azure に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-217">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="ff7e4-218">次の情報をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-218">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="ff7e4-219">**アプリケーション (クライアント) ID**値。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-219">The **Application (client) ID** value.</span></span> <span data-ttu-id="ff7e4-220">この値は、この Azure id アプリケーションを bot に登録するときに、*クライアント ID*として後で使用します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-220">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="ff7e4-221">**ディレクトリ (テナント) ID**の値。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-221">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="ff7e4-222">この値を後で*テナント id*として使用して、この Azure id アプリケーションを bot に登録することもできます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-222">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="ff7e4-223">左側のパネルで、[**証明書 & シークレット**] を選択して、アプリケーションのクライアントシークレットを作成します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-223">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="ff7e4-224">[**クライアントシークレット**] で、[**新しいクライアントシークレット**&#x2795;] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-224">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="ff7e4-225">このシークレットを、 *Teams の Bot id アプリ*など、このアプリ用に作成する必要がある他のユーザーから識別するための説明を追加します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-225">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="ff7e4-226">選択範囲に**期限**を設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-226">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="ff7e4-227">[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-227">Select **Add**.</span></span>
   1. <span data-ttu-id="ff7e4-228">このページを終了する前に、**シークレットを録音して**ください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-228">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="ff7e4-229">この値は、ボットを使用して Azure AD アプリケーションを登録するときに、_クライアントシークレット_として後で使用します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-229">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="ff7e4-230">Id プロバイダー接続を構成し、bot に登録する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-230">Configure the identity provider connection and register it with the bot</span></span>

1. <span data-ttu-id="ff7e4-231">[**Azure portal**][azure-portal]で、ダッシュボードからリソースグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-231">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="ff7e4-232">Bot チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-232">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="ff7e4-233">[リソース] ページで、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-233">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="ff7e4-234">ページの下部付近にある [ **OAuth 接続設定**] で、[**設定の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-234">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="ff7e4-235">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-235">Complete the form as follows:</span></span>

    1. <span data-ttu-id="ff7e4-236">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-236">**Name**.</span></span> <span data-ttu-id="ff7e4-237">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-237">Enter a name for the connection.</span></span> <span data-ttu-id="ff7e4-238">この名前は、 `appsettings.json`ファイル内の bot で使用します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-238">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="ff7e4-239">たとえば、 *BotTeamsAuthADv1*のようになります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-239">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="ff7e4-240">**サービスプロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-240">**Service Provider**.</span></span> <span data-ttu-id="ff7e4-241">[**Azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-241">Select **Azure Active Directory**.</span></span> <span data-ttu-id="ff7e4-242">このチェックボックスをオンにすると、Azure AD 固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-242">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="ff7e4-243">**クライアント id**。前述の手順で、Azure id プロバイダアプリ用に記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-243">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="ff7e4-244">**クライアントシークレット**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-244">**Client secret**.</span></span> <span data-ttu-id="ff7e4-245">前述の手順で、Azure id プロバイダアプリ用に記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-245">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="ff7e4-246">**許可の種類**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-246">**Grant Type**.</span></span> <span data-ttu-id="ff7e4-247">Enter `authorization_code`キーを押します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-247">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="ff7e4-248">**ログイン URL**。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-248">**Login URL**.</span></span> <span data-ttu-id="ff7e4-249">Enter `https://login.microsoftonline.com`キーを押します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-249">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="ff7e4-250">[**テナント id**] は、id プロバイダーアプリの作成時に選択したサポートされるアカウントの種類**に応じて**、前の手順で Azure id アプリ用に記録した**ディレクトリ (テナント) id**を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-250">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="ff7e4-251">割り当てる値を決定するには、次の条件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-251">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="ff7e4-252">[*この組織ディレクトリにあるアカウント] のみ (microsoft only-単一テナント)* または*任意の組織ディレクトリのアカウント (microsoft AAD ディレクトリ-マルチテナント)* を選択した場合は、AAD アプリの前に記録した**テナント ID**を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-252">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="ff7e4-253">これは、認証が可能なユーザーに関連付けられているテナントになります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-253">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="ff7e4-254">任意の組織ディレクトリでアカウントを選択した場合 *(任意の AAD ディレクトリ-マルチテナントおよび個人の Microsoft アカウント (Skype、Xbox、Outlook など)* の場合は、テナント ID ではなく**common**という単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-254">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="ff7e4-255">それ以外の場合、AAD アプリは、ID が選択されたテナントを経由して検証し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-255">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="ff7e4-256">h.</span><span class="sxs-lookup"><span data-stu-id="ff7e4-256">h.</span></span> <span data-ttu-id="ff7e4-257">[**リソースの URL**] `https://graph.microsoft.com/`で、と入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-257">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="ff7e4-258">これは、現在のコードサンプルでは使用されません。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-258">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="ff7e4-259">私。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-259">i.</span></span> <span data-ttu-id="ff7e4-260">**範囲**を空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-260">Leave **Scopes** blank.</span></span> <span data-ttu-id="ff7e4-261">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-261">The following image is an example:</span></span>

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="ff7e4-263">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-263">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="ff7e4-264">接続をテストする</span><span class="sxs-lookup"><span data-stu-id="ff7e4-264">Test the connection</span></span>

1. <span data-ttu-id="ff7e4-265">接続エントリを選択して、作成したばかりの接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-265">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="ff7e4-266">[**サービスプロバイダ接続設定**] パネルの上部にある [**テスト接続**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-266">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="ff7e4-267">最初にこの操作を行うと、新しいブラウザーウィンドウが開き、アカウントを選択するように求められます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-267">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="ff7e4-268">使用するものを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-268">Select the one you want to use.</span></span>
1. <span data-ttu-id="ff7e4-269">次に、id プロバイダーがデータ (資格情報) を使用することを許可するように求められます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-269">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="ff7e4-270">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-270">The following image is an example:</span></span>

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="ff7e4-272">**[同意する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-272">Select **Accept**.</span></span>
1. <span data-ttu-id="ff7e4-273">これにより、[**接続名> 成功] \<ページへのテスト接続**にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-273">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="ff7e4-274">エラーが表示された場合は、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-274">Refresh the page if you get an error.</span></span> <span data-ttu-id="ff7e4-275">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-275">The following image is an example:</span></span>

  ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="ff7e4-277">接続名は、ユーザー認証トークンを取得するために bot コードによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-277">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="ff7e4-278">Bot サンプルコードを準備する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-278">Prepare the bot sample code</span></span>

<span data-ttu-id="ff7e4-279">事前設定を完了したら、この記事で使用する bot の作成に重点を置いて説明します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-279">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ff7e4-280">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ff7e4-280">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="ff7e4-281">複製の[cs-auth-サンプル][teams-auth-bot-cs]。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-281">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="ff7e4-282">Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-282">Launch Visual Studio.</span></span>
1. <span data-ttu-id="ff7e4-283">ツールバーの [**ファイル]-> [> プロジェクト/ソリューション**] を選択し、bot プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-283">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="ff7e4-284">C# では、次のようにして**appsettings**を更新します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-284">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="ff7e4-285">Bot `ConnectionName`チャネル登録に追加した id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-285">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="ff7e4-286">この例で使用した名前は*BotTeamsAuthADv1*です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-286">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="ff7e4-287">Bot `MicrosoftAppId`チャネル登録時に保存した**bot アプリ ID**に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-287">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="ff7e4-288">Bot `MicrosoftAppPassword`チャネル登録時に保存した**お客様のシークレット**に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-288">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="ff7e4-289">`ConnectionName`を id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-289">Set the `ConnectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="ff7e4-290">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-290">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="ff7e4-291">たとえば、任意のアンパサンド (&) をとして`&amp;`エンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-291">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="ff7e4-292">ソリューションエクスプローラー `TeamsAppManifest`で、フォルダーに移動して、ボット`manifest.json`チャネルの`id`登録`botId`時に保存した**bot アプリ ID**を開き、設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-292">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="ff7e4-293">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ff7e4-293">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="ff7e4-294">クローン[ノード-auth-サンプル][teams-auth-bot-js]。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-294">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="ff7e4-295">コンソールで、プロジェクトに移動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-295">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="ff7e4-296">モジュールをインストールする</span><span class="sxs-lookup"><span data-stu-id="ff7e4-296">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="ff7e4-297">次のようにして、 **env**構成を更新します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-297">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="ff7e4-298">Bot `MicrosoftAppId`チャネル登録時に保存した**bot アプリ ID**に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-298">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="ff7e4-299">Bot `MicrosoftAppPassword`チャネル登録時に保存した**お客様のシークレット**に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-299">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="ff7e4-300">`connectionName`を id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-300">Set the `connectionName` to the name of the identity provider connection.</span></span>

    <span data-ttu-id="ff7e4-301">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-301">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="ff7e4-302">たとえば、任意のアンパサンド (&) をとして`&amp;`エンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-302">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="ff7e4-303">`teamsAppManifest` `manifest.json`フォルダーで、 **Microsoft アプリ id** `botId`を`id`開き、ボットチャネル登録時に保存した**bot アプリ id**を設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-303">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="ff7e4-304">Python</span><span class="sxs-lookup"><span data-stu-id="ff7e4-304">Python</span></span>](#tab/python)

1. <span data-ttu-id="ff7e4-305">Github リポジトリからの複製[py-サンプル][teams-auth-bot-py]。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-305">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="ff7e4-306">**Config.py**を更新します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-306">Update **config.py**:</span></span>

    - <span data-ttu-id="ff7e4-307">Bot `ConnectionName`に追加した OAuth 接続設定の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-307">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="ff7e4-308">Bot `MicrosoftAppId`の`MicrosoftAppPassword`アプリ ID とアプリシークレットを設定します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-308">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="ff7e4-309">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-309">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="ff7e4-310">たとえば、任意のアンパサンド (&) をとして`&amp;`エンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-310">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="ff7e4-311">Bot を Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-311">Deploy the bot to Azure</span></span>

<span data-ttu-id="ff7e4-312">Bot を展開するには、「 [Azure に bot を展開](https://aka.ms/azure-bot-deployment-cli)する方法」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-312">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="ff7e4-313">または、Visual Studio では、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-313">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="ff7e4-314">Visual Studio の*ソリューションエクスプローラー*で、プロジェクト名を選択して、ホールド (または右クリック) します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-314">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="ff7e4-315">ドロップダウンメニューで、[**発行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-315">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="ff7e4-316">表示されたウィンドウで、**新しい**リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-316">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="ff7e4-317">ダイアログウィンドウで、左側にある [ **App Service** ] を選択し、右側に [**新規作成**] を作成します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-317">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="ff7e4-318">[**発行**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-318">Select the **Publish** button.</span></span>
1. <span data-ttu-id="ff7e4-319">次のダイアログウィンドウで、必要な情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-319">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="ff7e4-320">例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-320">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="ff7e4-322">**[作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-322">Select **Create**.</span></span>
1. <span data-ttu-id="ff7e4-323">展開が正常に完了すると、Visual Studio に反映されたことがわかります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-323">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="ff7e4-324">さらに、*ボットの準備ができ*たことを示すページが既定のブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-324">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="ff7e4-325">URL は、次`https://botteamsauth.azurewebsites.net/`のようになります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-325">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="ff7e4-326">ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-326">Save it to a file.</span></span>
1. <span data-ttu-id="ff7e4-327">ブラウザーで[**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-327">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="ff7e4-328">リソースグループを確認すると、bot が他のリソースと共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-328">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="ff7e4-329">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-329">The following image is an example:</span></span>

    ![teams-auth-service-グループ](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="ff7e4-331">[リソース] グループで、bot チャネル登録名 (リンク) を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-331">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="ff7e4-332">左側のパネルで、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-332">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="ff7e4-333">[**メッセージングエンドポイント**] ボックスに、上で取得した`api/messages`URL に続けてを入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-333">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="ff7e4-334">次に例を示し`https://botteamsauth.azurewebsites.net/api/messages`ます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-334">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="ff7e4-335">左上隅にある [**保存**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-335">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="ff7e4-336">エミュレーターを使用して bot をテストする</span><span class="sxs-lookup"><span data-stu-id="ff7e4-336">Test the bot using the Emulator</span></span>

<span data-ttu-id="ff7e4-337">まだ行っていない場合は、 [Microsoft Bot フレームワークエミュレーター](https://aka.ms/bot-framework-emulator-readme)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-337">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="ff7e4-338">「[エミュレーターを使用してデバッグする](https://aka.ms/bot-framework-emulator-debug-with-emulator)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-338">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="ff7e4-339">Bot のサンプルログインを機能させるには、以下のようにエミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-339">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="ff7e4-340">認証用にエミュレーターを構成する</span><span class="sxs-lookup"><span data-stu-id="ff7e4-340">Configure the Emulator for authentication</span></span>

<span data-ttu-id="ff7e4-341">Bot が認証を必要とする場合は、以下に示すように、エミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-341">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="ff7e4-342">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-342">Start the Emulator.</span></span>
1. <span data-ttu-id="ff7e4-343">エミュレーターで、左下の歯車アイコン &#9881;、または右上の [**エミュレーターの設定**] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-343">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="ff7e4-344">チェックボックスをオンにするには、**バージョン1.0 の認証トークンを使用**します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-344">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="ff7e4-345">**Ngrok**ツールへのローカルパスを入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-345">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="ff7e4-346">Bot フレームワークエミュレーター/ngrok トンネリング統合[Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-346">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="ff7e4-347">ツールの詳細については、「 [ngrok](https://ngrok.com/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-347">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="ff7e4-348">**エミュレーター起動時に ngrok を実行**してチェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-348">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="ff7e4-349">[**保存**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-349">Select the **Save** button.</span></span>

<span data-ttu-id="ff7e4-350">Bot がサインインカードを表示し、ユーザーがサインインボタンを選択すると、ユーザーが認証プロバイダーでサインインするために使用できるページがエミュレーターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-350">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="ff7e4-351">ユーザーがこれを実行すると、プロバイダーはユーザートークンを生成して bot に送信します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-351">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="ff7e4-352">その後、bot はユーザーの代わりに行動することができます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-352">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="ff7e4-353">Bot をローカルでテストする</span><span class="sxs-lookup"><span data-stu-id="ff7e4-353">Test the bot locally</span></span>

<span data-ttu-id="ff7e4-354">認証メカニズムを構成した後は、実際の bot テストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-354">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="ff7e4-355">Visual Studio を使用して、お使いのコンピューターでローカルに bot サンプルを実行します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-355">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="ff7e4-356">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-356">Start the Emulator.</span></span>
1. <span data-ttu-id="ff7e4-357">[ **Open bot** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-357">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="ff7e4-358">Bot の**url**に bot のローカル url を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-358">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="ff7e4-359">通常は`http://localhost:3978/api/messages`、です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-359">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="ff7e4-360">**Microsoft アプリ id**で、bot のアプリ id をから`appsettings.json`入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-360">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="ff7e4-361">**Microsoft App パスワード**に、 `appsettings.json`からの bot のアプリパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-361">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="ff7e4-362">[**接続**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-362">Select **Connect**.</span></span>
1. <span data-ttu-id="ff7e4-363">Bot が起動して実行されたら、サインインカードを表示するテキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-363">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="ff7e4-364">**[サインイン]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-364">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="ff7e4-365">開いている**URL を確認**するポップアップダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-365">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="ff7e4-366">これにより、ボットのユーザー (ユーザー) が認証されるようになります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-366">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="ff7e4-367">[**確認**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-367">Select **Confirm**.</span></span>
1. <span data-ttu-id="ff7e4-368">要求された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-368">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="ff7e4-369">エミュレーターで使用した構成に応じて、次のいずれかを取得します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-369">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="ff7e4-370">**サインイン確認コードの使用**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-370">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="ff7e4-371">検証コードを表示するウィンドウが開かれて &#x2713; ます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-371">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="ff7e4-372">サインインを完了するには、&#x2713; コピーして、検証コードを [チャット] ボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-372">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="ff7e4-373">**認証トークンを使用**します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-373">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="ff7e4-374">資格情報に基づいてログインしている &#x2713;。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-374">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="ff7e4-375">次の図は、ログインした後の bot UI の例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-375">The following image is an example of the bot UI after you've logged in:</span></span>

    ![auth bot ログインエミュレーター](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="ff7e4-377">Bot から*トークンを表示するよう*求められたときに **[はい**] を選択すると、次のような応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-377">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![auth bot ログインエミュレータートークン](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="ff7e4-379">サインアウトするには、[チャットの入力] ボックスに「**ログアウト**」と入力します。これにより、ユーザートークンが解放され、再びサインインするまでは、お客様の代わりに bot を操作することはできません。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-379">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="ff7e4-380">Bot 認証には、 **Bot コネクタサービス**を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-380">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="ff7e4-381">サービスは bot の bot チャネル登録情報にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-381">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="ff7e4-382">展開した bot をテストする</span><span class="sxs-lookup"><span data-stu-id="ff7e4-382">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="ff7e4-383">ブラウザーで[**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-383">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="ff7e4-384">リソースグループを検索します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-384">Find your resource group.</span></span>
1. <span data-ttu-id="ff7e4-385">[リソース] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-385">Select the resource link.</span></span> <span data-ttu-id="ff7e4-386">[リソース] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-386">The resource page is displayed.</span></span>
1. <span data-ttu-id="ff7e4-387">[リソース] ページで、[ **Web チャットでテスト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-387">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="ff7e4-388">Bot が開始し、定義済みの案内応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-388">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="ff7e4-389">[チャット] ボックスに何か入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-389">Type anything in the chat box.</span></span>
1. <span data-ttu-id="ff7e4-390">[**サインイン**] ボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-390">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="ff7e4-391">開いている**URL を確認**するポップアップダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-391">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="ff7e4-392">これにより、ボットのユーザー (ユーザー) が認証されるようになります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-392">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="ff7e4-393">[**確認**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-393">Select **Confirm**.</span></span>
1. <span data-ttu-id="ff7e4-394">要求された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-394">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="ff7e4-395">次の図は、ログインした後の bot UI の例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-395">The following image is an example of the bot UI after you have logged in:</span></span>

    ![auth bot ログインの展開](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="ff7e4-397">.</span><span class="sxs-lookup"><span data-stu-id="ff7e4-397">.</span></span>

1. <span data-ttu-id="ff7e4-398">[**はい**] ボタンを選択して、認証トークンを表示します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-398">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="ff7e4-399">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-399">The following image is an example:</span></span>

    ![auth bot ログイン展開されたトークン](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="ff7e4-401">.</span><span class="sxs-lookup"><span data-stu-id="ff7e4-401">.</span></span>

1. <span data-ttu-id="ff7e4-402">サインアウトするには、「ログアウト」と入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-402">Enter logout to sign out.</span></span>

    ![auth bot が展開したログアウト](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="ff7e4-404">サインインで問題が発生した場合は、前の手順で説明したように、接続をもう一度テストしてください。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-404">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="ff7e4-405">これにより、認証トークンが再作成されることがあります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-405">This could recreate the authentication token.</span></span>
> <span data-ttu-id="ff7e4-406">「Azure の Bot フレームワーク Web チャットクライアント」では、認証が正しく設定される前に、数回サインインする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-406">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="ff7e4-407">Teams に bot をインストールしてテストする</span><span class="sxs-lookup"><span data-stu-id="ff7e4-407">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="ff7e4-408">Bot プロジェクト`TeamsAppManifest`で、フォルダーに`manifest.json` `outline.png`と`color.png`ファイルが含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-408">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="ff7e4-409">ソリューションエクスプローラーで、 `TeamsAppManifest`フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-409">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="ff7e4-410">次`manifest.json`の値を割り当てることによって編集します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-410">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="ff7e4-411">Bot チャネル登録時に受信した**Bot アプリ ID**がおよび`id` `botId`に割り当てられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-411">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="ff7e4-412">次`validDomains: [ "token.botframework.com" ]`の値を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-412">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="ff7e4-413">、、および`color.png`ファイル`manifest.json`を`outline.png`選択して**zip**にします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-413">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="ff7e4-414">**Microsoft Teams**を開きます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-414">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="ff7e4-415">左側のパネルで、下部にある [**アプリ] アイコン**を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-415">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="ff7e4-416">右側のパネルで、下部にある [**カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-416">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="ff7e4-417">`TeamsAppManifest`フォルダーに移動し、zip マニフェストをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-417">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="ff7e4-418">次のウィザードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-418">The following wizard is displayed:</span></span>

    ![auth bot teams のアップロード](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="ff7e4-420">**[チームに追加]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-420">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="ff7e4-421">次のウィンドウで、ボットを使用するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-421">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="ff7e4-422">[ **Bot の設定**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-422">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="ff7e4-423">左側のパネルで、3つのドット (&#x25cf;&#x25cf;&#x25cf;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-423">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="ff7e4-424">次に、[ **App Studio** ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-424">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="ff7e4-425">[**マニフェストエディター** ] タブを選択します。アップロードした bot のアイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-425">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="ff7e4-426">また、bot とのメッセージの交換に使用できる連絡先として、その bot が連絡先として表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-426">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="ff7e4-427">Teams でボットをローカルにテストする</span><span class="sxs-lookup"><span data-stu-id="ff7e4-427">Testing the bot locally in Teams</span></span>

<span data-ttu-id="ff7e4-428">Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからアクセスできるようにするには、すべてのサービスがアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-428">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="ff7e4-429">そのため、ボット (サンプル) を Teams で使用できるようにするには、選択したクラウドにコードを発行するか、または**トンネル**ツールを使用して、ローカルに実行しているインスタンスを外部からアクセス可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-429">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="ff7e4-430">[Ngrok](https://ngrok.com/download)を使用することをお勧めします。この URL は、コンピューター上でローカルに開いたポートに対して、外部アドレス指定可能な URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-430">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="ff7e4-431">Microsoft Teams アプリをローカルで実行する準備として ngrok をセットアップするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-431">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="ff7e4-432">ターミナルウィンドウで、が`ngrok.exe`インストールされているディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-432">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="ff7e4-433">これを指すように、*環境変数*のパスを設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-433">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="ff7e4-434">たとえば、を実行`ngrok http 3978 --host-header=localhost:3978`します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-434">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="ff7e4-435">必要に応じてポート番号を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-435">Replace the port number as needed.</span></span>
<span data-ttu-id="ff7e4-436">これにより、指定したポートをリッスンする ngrok が起動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-436">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="ff7e4-437">これにより、ngrok が実行されている限り、外部的にアドレス指定可能な URL が得られます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-437">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="ff7e4-438">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-438">The following image is an example:</span></span>

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="ff7e4-440">.</span><span class="sxs-lookup"><span data-stu-id="ff7e4-440">.</span></span>

1. <span data-ttu-id="ff7e4-441">転送用の HTTPS アドレスをコピーします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-441">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="ff7e4-442">これは、次のようになり`https://dea822bf.ngrok.io/`ます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-442">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="ff7e4-443">取得`/api/messages` `https://dea822bf.ngrok.io/api/messages`する追加。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-443">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="ff7e4-444">これは、コンピューター上でローカルに実行されていて、Microsoft Teams のチャットで web 経由でアクセスできる bot の**メッセージエンドポイント**です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-444">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="ff7e4-445">最後に実行する手順の1つは、展開した bot のメッセージエンドポイントを更新することです。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-445">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="ff7e4-446">この例では、bot を Azure に展開しました。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-446">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="ff7e4-447">そのため、以下の手順を実行してみましょう。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-447">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="ff7e4-448">ブラウザーで[**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-448">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="ff7e4-449">**Bot チャネル登録**を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-449">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="ff7e4-450">左側のパネルで、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-450">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="ff7e4-451">右側のパネルの [**メッセージングエンドポイント**] ボックスに、ngrok URL (この例では) `https://dea822bf.ngrok.io/api/messages`を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-451">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="ff7e4-452">Visual Studio デバッグモードなどで、ボットをローカルに起動します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-452">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="ff7e4-453">Bot フレームワークポータルの**テスト Web チャット**を使用して、ローカルで実行中に bot をテストします。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-453">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="ff7e4-454">エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-454">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="ff7e4-455">`ngrok`が実行されているターミナルウィンドウで、ボットと web チャットクライアント間の HTTP トラフィックを確認できます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-455">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="ff7e4-456">より詳細な表示が必要な場合は、ブラウザーウィンドウで`http://127.0.0.1:4040`以前のターミナルウィンドウから取得した情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-456">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="ff7e4-457">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-457">The following image is an example:</span></span>

    ![auth bot teams ngrok テスト](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="ff7e4-459">.</span><span class="sxs-lookup"><span data-stu-id="ff7e4-459">.</span></span>

> [!NOTE]
> <span data-ttu-id="ff7e4-460">Ngrok を停止してから再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-460">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="ff7e4-461">プロジェクトで ngrok を使用し、使用している機能に応じて、すべての URL 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-461">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>

## <a name="additional-information"></a><span data-ttu-id="ff7e4-462">追加情報</span><span class="sxs-lookup"><span data-stu-id="ff7e4-462">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="ff7e4-463">TeamsAppManifest/manifest</span><span class="sxs-lookup"><span data-stu-id="ff7e4-463">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="ff7e4-464">このマニフェストには、Microsoft Teams が bot と接続するために必要な情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-464">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

<span data-ttu-id="ff7e4-465">認証を使用すると、以下に説明するように、Teams は他のチャネルとはやや異なる方法で動作します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-465">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="ff7e4-466">呼び出しアクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="ff7e4-466">Handling Invoke Activity</span></span>

<span data-ttu-id="ff7e4-467">**呼び出しアクティビティ**は、他のチャネルによって使用されるイベントアクティビティではなく bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-467">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="ff7e4-468">これは、 **Activityhandler**のサブクラスによって実行されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-468">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ff7e4-469">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ff7e4-469">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="ff7e4-470">**ボット/の bot**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-470">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="ff7e4-471">**ボット/TeamsBot**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-471">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="ff7e4-472">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-472">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="ff7e4-473">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="ff7e4-473">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="ff7e4-474">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ff7e4-474">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="ff7e4-475">**bot/のボット**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-475">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="ff7e4-476">**ボット/teamsBot**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-476">**bots/teamsBot.js**</span></span>

<span data-ttu-id="ff7e4-477">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-477">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="ff7e4-478">**ダイアログ/mainDialog .js**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-478">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="ff7e4-479">ダイアログステップで、を使用`beginDialog`して OAuth プロンプトを開始します。これにより、ユーザーにサインインするように求められます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-479">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="ff7e4-480">ユーザーが既にサインインしている場合は、ユーザーに確認を求めることなく、トークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-480">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="ff7e4-481">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-481">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="ff7e4-482">Azure Bot サービスは、ユーザーがサインインしようとした後に、トークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-482">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="ff7e4-483">次のダイアログステップでは、前の手順の結果にトークンが存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-483">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="ff7e4-484">Null でない場合、ユーザーは正常にサインインしています。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-484">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="ff7e4-485">**ボット/logoutDialog .js**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-485">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="ff7e4-486">Python</span><span class="sxs-lookup"><span data-stu-id="ff7e4-486">Python</span></span>](#tab/python-sample)

<span data-ttu-id="ff7e4-487">**ボット/dialog_bot py**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-487">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="ff7e4-488">**ボット/teams_bot py**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-488">**bots/teams_bot.py**</span></span>

<span data-ttu-id="ff7e4-489">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-489">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="ff7e4-490">**ダイアログ/main_dialog py**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-490">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="ff7e4-491">ダイアログステップで、を使用`begin_dialog`して OAuth プロンプトを開始します。これにより、ユーザーにサインインするように求められます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-491">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="ff7e4-492">ユーザーが既にサインインしている場合は、ユーザーに確認を求めることなく、トークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-492">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="ff7e4-493">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-493">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="ff7e4-494">Azure Bot サービスは、ユーザーがサインインしようとした後に、トークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-494">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="ff7e4-495">次のダイアログステップでは、前の手順の結果にトークンが存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-495">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="ff7e4-496">Null でない場合、ユーザーは正常にサインインしています。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-496">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="ff7e4-497">**ダイアログ/logout_dialog py**</span><span class="sxs-lookup"><span data-stu-id="ff7e4-497">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff7e4-498">Azure Bot サービスによる追加認証の追加について説明します。</span><span class="sxs-lookup"><span data-stu-id="ff7e4-498">Learn about adding adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

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
