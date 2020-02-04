---
title: Teams の bot に認証を追加する
author: clearab
description: Microsoft Teams の bot に OAuth 認証を追加する方法。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 63d06100f69a5dc3777bdfb20b3231a85dce1f04
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674784"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="d0b77-103">Teams の bot に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="d0b77-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="d0b77-104">メールサービスなど、ユーザーの代わりにリソースにアクセスできる、Microsoft Teams でボットを作成しなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="d0b77-105">この記事では、OAuth 2.0 に基づいて Azure Bot サービス v4 SDK 認証を使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="d0b77-106">これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットを開発するのが容易になります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="d0b77-107">すべてのキーこれは、後で説明するように、 **id プロバイダー**を使用していることです。</span><span class="sxs-lookup"><span data-stu-id="d0b77-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="d0b77-108">OAuth 2.0 は、Azure Active Directory (Azure AD) とその他の多くの id プロバイダーによって使用される認証と承認のためのオープン標準です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="d0b77-109">OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="d0b77-110">基本的な理解と、完全な仕様の[oauth 2.0](https://oauth.net/2/)については、「 [Oauth 2 の単純化](https://aka.ms/oauth2-simplified)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="d0b77-111">Azure Bot サービスが認証を処理する方法の詳細については、「[会話内のユーザー認証](https://aka.ms/azure-bot-authentication)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="d0b77-112">この記事では、以下について説明します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-112">In this article you'll learn:</span></span>

- <span data-ttu-id="d0b77-113">**認証を有効にした bot を作成する方法**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="d0b77-114">ユーザーのサインイン資格情報と認証トークンの生成を処理するには、 [cs-auth-サンプル][teams-auth-bot]を使用します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-114">You'll use [cs-auth-sample][teams-auth-bot] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="d0b77-115">**Bot を Azure に展開し、id プロバイダーに関連付ける方法について説明**します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="d0b77-116">プロバイダーは、ユーザーのサインイン資格情報に基づいてトークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="d0b77-117">Bot は、トークンを使用して、メールサービスなど、認証を必要とするリソースにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="d0b77-118">詳細については、「[ボットの Microsoft Teams 認証フロー](auth-flow-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="d0b77-119">**Microsoft Teams 内で bot を統合する方法**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="d0b77-120">Bot が統合されたら、チャットでサインインしてメッセージを交換することができます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0b77-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="d0b77-121">Prerequisites</span></span>

- <span data-ttu-id="d0b77-122">ボットの[基礎][concept-basics]知識、[状態の管理][concept-state]、[ダイアログライブラリ][concept-dialogs]、[シーケンシャルな会話フローを実装][simple-dialog]する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="d0b77-123">Azure および OAuth 2.0 の開発に関する知識。</span><span class="sxs-lookup"><span data-stu-id="d0b77-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="d0b77-124">Visual Studio 2017 以降および Git。</span><span class="sxs-lookup"><span data-stu-id="d0b77-124">Visual Studio 2017 or later and Git.</span></span>
- <span data-ttu-id="d0b77-125">Azure アカウント。</span><span class="sxs-lookup"><span data-stu-id="d0b77-125">Azure account.</span></span> <span data-ttu-id="d0b77-126">必要に応じて、 [Azure 無料アカウント](https://azure.microsoft.com/free/)を作成できます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="d0b77-127">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-127">The following sample.</span></span>

    | <span data-ttu-id="d0b77-128">例</span><span class="sxs-lookup"><span data-stu-id="d0b77-128">Sample</span></span> | <span data-ttu-id="d0b77-129">BotBuilder のバージョン</span><span class="sxs-lookup"><span data-stu-id="d0b77-129">BotBuilder version</span></span> | <span data-ttu-id="d0b77-130">もの</span><span class="sxs-lookup"><span data-stu-id="d0b77-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="d0b77-131">\*\*\*\* [(Cs 認証)-auth-サンプル][teams-auth-bot]</span><span class="sxs-lookup"><span data-stu-id="d0b77-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot]</span></span> | <span data-ttu-id="d0b77-132">ipv4</span><span class="sxs-lookup"><span data-stu-id="d0b77-132">v4</span></span> | <span data-ttu-id="d0b77-133">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="d0b77-133">OAuthCard support</span></span> |
    | <span data-ttu-id="d0b77-134">Python の**Bot 認証**の[例][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="d0b77-134">**Bot authentication** in [python-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="d0b77-135">ipv4</span><span class="sxs-lookup"><span data-stu-id="d0b77-135">v4</span></span> | <span data-ttu-id="d0b77-136">OAuthCard のサポート</span><span class="sxs-lookup"><span data-stu-id="d0b77-136">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="d0b77-137">リソースグループを作成する</span><span class="sxs-lookup"><span data-stu-id="d0b77-137">Create the resource group</span></span>

<span data-ttu-id="d0b77-138">リソースグループとサービスプランは厳密には必要ありませんが、作成したリソースを容易に解放することができます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-138">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="d0b77-139">これは、リソースを整理して管理できるようにするための適切な方法です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-139">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="d0b77-140">リソースグループを使用して、Bot フレームワークの個々のリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-140">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="d0b77-141">パフォーマンスを確保するために、これらのリソースが同じ Azure 地域にあることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-141">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="d0b77-142">ブラウザーで、 [**Azure portal**][azure-portal]にサインインします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-142">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="d0b77-143">左側のナビゲーションパネルで、[**リソースグループ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-143">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="d0b77-144">表示されたウィンドウの左上で、[タブの**追加**] を選択して新しいリソースグループを作成します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-144">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="d0b77-145">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-145">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="d0b77-146">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-146">**Subscription**.</span></span> <span data-ttu-id="d0b77-147">既存のサブスクリプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-147">Use your existing subscription.</span></span>
    1. <span data-ttu-id="d0b77-148">**リソースグループ**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-148">**Resource group**.</span></span> <span data-ttu-id="d0b77-149">リソースグループの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-149">Enter the name for the resource group.</span></span> <span data-ttu-id="d0b77-150">例として、 *Teamsresourcegroup*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-150">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="d0b77-151">名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-151">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="d0b77-152">[**地域**] ドロップダウンメニューから [ *West US*] を選択するか、アプリケーションに近い地域を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-152">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="d0b77-153">[**確認して作成**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-153">Select the **Review and create** button.</span></span> <span data-ttu-id="d0b77-154">*検証が成功*したことを示すバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-154">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="d0b77-155">[**作成**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-155">Select the **Create** button.</span></span> <span data-ttu-id="d0b77-156">リソースグループの作成には、数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-156">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="d0b77-157">このチュートリアルの後の方で作成するリソースと同様に、このリソースグループをダッシュボードに固定して簡単にアクセスできるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-157">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="d0b77-158">これを行う場合は、pin アイコン & # 128204; を選びます。ダッシュボードの右上にあります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-158">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="d0b77-159">サービスプランを作成する</span><span class="sxs-lookup"><span data-stu-id="d0b77-159">Create the service plan</span></span>

1. <span data-ttu-id="d0b77-160">[**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[**リソースの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-160">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="d0b77-161">[検索] ボックスに「 *App Service Plan*」と入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-161">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="d0b77-162">検索結果から**App Service プラン**カードを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-162">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="d0b77-163">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-163">Select **Create**.</span></span>
1. <span data-ttu-id="d0b77-164">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-164">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="d0b77-165">**サブスクリプション**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-165">**Subscription**.</span></span> <span data-ttu-id="d0b77-166">既存のサブスクリプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-166">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="d0b77-167">**リソースグループ**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-167">**Resource Group**.</span></span> <span data-ttu-id="d0b77-168">前に作成したグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-168">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="d0b77-169">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-169">**Name**.</span></span> <span data-ttu-id="d0b77-170">サービスプランの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-170">Enter the name for the service plan.</span></span> <span data-ttu-id="d0b77-171">例としては、 *Teamsserviceplan*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-171">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="d0b77-172">グループ内の名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-172">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="d0b77-173">**オペレーティングシステム**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-173">**Operating System**.</span></span> <span data-ttu-id="d0b77-174">*Windows*または該当する OS を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-174">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="d0b77-175">**地域**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-175">**Region**.</span></span> <span data-ttu-id="d0b77-176">[ *WEST US* ] または [アプリケーションに近い地域] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-176">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="d0b77-177">**価格レベル**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-177">**Pricing Tier**.</span></span> <span data-ttu-id="d0b77-178">*標準 S1*が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-178">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="d0b77-179">これは既定値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-179">This should be the default value.</span></span>
    1. <span data-ttu-id="d0b77-180">[**確認して作成**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-180">Select the **Review and create** button.</span></span> <span data-ttu-id="d0b77-181">*検証が成功*したことを示すバナーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-181">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="d0b77-182">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-182">Select **Create**.</span></span> <span data-ttu-id="d0b77-183">App service プランを作成するには、数分かかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-183">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="d0b77-184">計画がリソースグループに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-184">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="d0b77-185">Bot チャネル登録を作成する</span><span class="sxs-lookup"><span data-stu-id="d0b77-185">Create the bot channels registration</span></span>

<span data-ttu-id="d0b77-186">Bot チャネル登録は、Microsoft アプリ Id とアプリパスワード (クライアントシークレット) がある場合に、ボットフレームワークを使用して web サービスをボットとして登録します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-186">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0b77-187">Bot が Azure でホストされていない場合にのみ、ボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-187">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="d0b77-188">Azure ポータルを使用して[ボットを作成](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0)した場合は、既にサービスに登録されています。</span><span class="sxs-lookup"><span data-stu-id="d0b77-188">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="d0b77-189">Bot[フレームワーク](https://dev.botframework.com/bots/new)または[appstudio](~/concepts/build-and-test/app-studio-overview.md)を使用して bot を作成した場合、その bot は Azure に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="d0b77-189">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="d0b77-190">Azure で登録リソースが作成されると、リソースグループリストに追加されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-190">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![bot アプリチャネル登録グループ](../../../assets/images/authentication/auth-bot-channels-registration-group.PNG)

> [!NOTE]
> <span data-ttu-id="d0b77-192">Bot チャネル登録リソースは、[West US] を選択した場合でも、**グローバル**地域を表示します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-192">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="d0b77-193">これは想定されています。</span><span class="sxs-lookup"><span data-stu-id="d0b77-193">This is expected.</span></span>

<span data-ttu-id="d0b77-194">詳細については、「 [Teams の bot を作成する](../create-a-bot-for-teams.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-194">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="d0b77-195">Id プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="d0b77-195">Create the identity provider</span></span>

<span data-ttu-id="d0b77-196">認証に使用できる id プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-196">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="d0b77-197">この手順では、Azure AD プロバイダーを使用します。他の Azure AD でサポートされている id プロバイダーを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-197">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="d0b77-198">[**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[ **azure Active Directory**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-198">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="d0b77-199">アプリケーションによって要求されたアクセス許可の委任を承認するには、この Azure AD リソースを作成してテナントに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-199">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="d0b77-200">テナントを作成する手順については、「[ポータルにアクセスし、テナントを作成](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-200">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="d0b77-201">左側のパネルで、[**アプリの登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-201">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="d0b77-202">右パネルで、左上にある [**新しい登録**] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-202">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="d0b77-203">次の情報を入力するように求められます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-203">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="d0b77-204">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-204">**Name**.</span></span> <span data-ttu-id="d0b77-205">アプリケーションの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-205">Enter the name for the application.</span></span> <span data-ttu-id="d0b77-206">例として、 *BotTeamsIdentity*が考えられます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-206">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="d0b77-207">名前は一意である必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-207">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="d0b77-208">アプリケーションに対し**てサポートされているアカウントの種類**を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-208">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="d0b77-209">*任意の組織ディレクトリ (任意の AZURE AD ディレクトリ-マルチテナント) と個人の Microsoft アカウント (Skype、Xbox など) でアカウント*を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-209">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="d0b77-210">**リダイレクト URI**の場合:</span><span class="sxs-lookup"><span data-stu-id="d0b77-210">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="d0b77-211">[ **Web**] を &#x2713;選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-211">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="d0b77-212">&#x2713; URL をに`https://token.botframework.com/.auth/web/redirect`設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-212">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="d0b77-213">[**登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-213">Select **Register**.</span></span>

1. <span data-ttu-id="d0b77-214">作成されたアプリの**概要**ページが Azure に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-214">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="d0b77-215">次の情報をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-215">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="d0b77-216">**アプリケーション (クライアント) ID**値。</span><span class="sxs-lookup"><span data-stu-id="d0b77-216">The **Application (client) ID** value.</span></span> <span data-ttu-id="d0b77-217">この値は、この Azure id アプリケーションを bot に登録するときに、*クライアント ID*として後で使用します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-217">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="d0b77-218">**ディレクトリ (テナント) ID**の値。</span><span class="sxs-lookup"><span data-stu-id="d0b77-218">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="d0b77-219">この値を後で*テナント id*として使用して、この Azure id アプリケーションを bot に登録することもできます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-219">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="d0b77-220">左側のパネルで、[**証明書 & シークレット**] を選択して、アプリケーションのクライアントシークレットを作成します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-220">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="d0b77-221">[**クライアントシークレット**] で、[**新しいクライアントシークレット**&#x2795;] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-221">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="d0b77-222">このシークレットを、 *Teams の Bot id アプリ*など、このアプリ用に作成する必要がある他のユーザーから識別するための説明を追加します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-222">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="d0b77-223">選択範囲に**期限**を設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-223">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="d0b77-224">**[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-224">Select **Add**.</span></span>
   1. <span data-ttu-id="d0b77-225">このページを終了する前に、**シークレットを録音して**ください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-225">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="d0b77-226">この値は、ボットを使用して Azure AD アプリケーションを登録するときに、_クライアントシークレット_として後で使用します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-226">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="d0b77-227">Id プロバイダー接続を構成し、bot に登録する</span><span class="sxs-lookup"><span data-stu-id="d0b77-227">Configure the identity provider connection and register it with the bot</span></span>

1. <span data-ttu-id="d0b77-228">[**Azure portal**][azure-portal]で、ダッシュボードからリソースグループを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-228">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="d0b77-229">Bot チャネル登録リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-229">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="d0b77-230">[リソース] ページで、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-230">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="d0b77-231">ページの下部付近にある [ **OAuth 接続設定**] で、[**設定の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-231">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="d0b77-232">フォームに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-232">Complete the form as follows:</span></span>

    1. <span data-ttu-id="d0b77-233">**名前**です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-233">**Name**.</span></span> <span data-ttu-id="d0b77-234">接続の名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-234">Enter a name for the connection.</span></span> <span data-ttu-id="d0b77-235">この名前は、 `appsettings.json`ファイル内の bot で使用します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-235">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="d0b77-236">たとえば、 *BotTeamsAuthADv1*のようになります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-236">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="d0b77-237">**サービスプロバイダー**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-237">**Service Provider**.</span></span> <span data-ttu-id="d0b77-238">**Azure Active Directory** を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-238">Select **Azure Active Directory**.</span></span> <span data-ttu-id="d0b77-239">このチェックボックスをオンにすると、Azure AD 固有のフィールドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-239">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="d0b77-240">**クライアント id**。前述の手順で、Azure id プロバイダアプリ用に記録したアプリケーション (クライアント) ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-240">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="d0b77-241">**クライアントシークレット**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-241">**Client secret**.</span></span> <span data-ttu-id="d0b77-242">前述の手順で、Azure id プロバイダアプリ用に記録したシークレットを入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-242">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="d0b77-243">**許可の種類**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-243">**Grant Type**.</span></span> <span data-ttu-id="d0b77-244">Enter `authorization_code`キーを押します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-244">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="d0b77-245">**ログイン URL**。</span><span class="sxs-lookup"><span data-stu-id="d0b77-245">**Login URL**.</span></span> <span data-ttu-id="d0b77-246">Enter `https://login.microsoftonline.com`キーを押します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-246">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="d0b77-247">[**テナント id**] は、id プロバイダーアプリの作成時に選択したサポートされるアカウントの種類**に応じて**、前の手順で Azure id アプリ用に記録した**ディレクトリ (テナント) id**を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-247">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="d0b77-248">割り当てる値を決定するには、次の条件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-248">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="d0b77-249">[*この組織ディレクトリにあるアカウント] のみ (microsoft only-単一テナント)* または*任意の組織ディレクトリのアカウント (microsoft AAD ディレクトリ-マルチテナント)* を選択した場合は、AAD アプリの前に記録した**テナント ID**を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-249">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="d0b77-250">これは、認証が可能なユーザーに関連付けられているテナントになります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-250">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="d0b77-251">任意の組織ディレクトリでアカウントを選択した場合 *(任意の AAD ディレクトリ-マルチテナントおよび個人の Microsoft アカウント (Skype、Xbox、Outlook など)* の場合は、テナント ID ではなく**common**という単語を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-251">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="d0b77-252">それ以外の場合、AAD アプリは、ID が選択されたテナントを経由して検証し、個人の Microsoft アカウントを除外します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-252">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="d0b77-253">h.</span><span class="sxs-lookup"><span data-stu-id="d0b77-253">h.</span></span> <span data-ttu-id="d0b77-254">[**リソースの URL**] `https://graph.microsoft.com/`で、と入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-254">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="d0b77-255">これは、現在のコードサンプルでは使用されません。</span><span class="sxs-lookup"><span data-stu-id="d0b77-255">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="d0b77-256">私。</span><span class="sxs-lookup"><span data-stu-id="d0b77-256">i.</span></span> <span data-ttu-id="d0b77-257">**範囲**を空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-257">Leave **Scopes** blank.</span></span> <span data-ttu-id="d0b77-258">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-258">The following image is an example:</span></span>

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="d0b77-260">[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-260">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="d0b77-261">接続をテストする</span><span class="sxs-lookup"><span data-stu-id="d0b77-261">Test the connection</span></span>

1. <span data-ttu-id="d0b77-262">接続エントリを選択して、作成したばかりの接続を開きます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-262">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="d0b77-263">[**サービスプロバイダ接続設定**] パネルの上部にある [**テスト接続**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-263">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="d0b77-264">最初にこの操作を行うと、新しいブラウザーウィンドウが開き、アカウントを選択するように求められます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-264">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="d0b77-265">使用するものを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-265">Select the one you want to use.</span></span>
1. <span data-ttu-id="d0b77-266">次に、id プロバイダーがデータ (資格情報) を使用することを許可するように求められます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-266">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="d0b77-267">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-267">The following image is an example:</span></span>

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="d0b77-269">[**同意**する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-269">Select **Accept**.</span></span>
1. <span data-ttu-id="d0b77-270">これにより、[**接続名> 成功] \<ページへのテスト接続**にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-270">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="d0b77-271">エラーが表示された場合は、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-271">Refresh the page if you get an error.</span></span> <span data-ttu-id="d0b77-272">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-272">The following image is an example:</span></span>

  ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="d0b77-274">接続名は、ユーザー認証トークンを取得するために bot コードによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-274">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="d0b77-275">Bot サンプルコードを準備する</span><span class="sxs-lookup"><span data-stu-id="d0b77-275">Prepare the bot sample code</span></span>

<span data-ttu-id="d0b77-276">事前設定を完了したら、この記事で使用する bot の作成に重点を置いて説明します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-276">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="d0b77-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d0b77-277">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="d0b77-278">複製の[cs-auth-サンプル][teams-auth-bot]。</span><span class="sxs-lookup"><span data-stu-id="d0b77-278">Clone [cs-auth-sample][teams-auth-bot].</span></span>
1. <span data-ttu-id="d0b77-279">Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-279">Launch Visual Studio.</span></span>
1. <span data-ttu-id="d0b77-280">ツールバーの [**ファイル]-> [> プロジェクト/ソリューション**] を選択し、bot プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-280">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="d0b77-281">C# では、次のようにして**appsettings**を更新します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-281">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="d0b77-282">Bot `ConnectionName`チャネル登録に追加した id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-282">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="d0b77-283">この例で使用した名前は*BotTeamsAuthADv1*です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-283">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="d0b77-284">Bot `MicrosoftAppId`チャネル登録時に保存した**bot アプリ ID**に設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-284">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="d0b77-285">Bot `MicrosoftAppPassword`チャネル登録時に保存した**お客様のシークレット**に設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-285">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="d0b77-286">`ConnectionName`を id プロバイダー接続の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-286">Set the `ConnectionName` to the name of the identity provider connection.</span></span> 

    <span data-ttu-id="d0b77-287">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-287">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="d0b77-288">たとえば、任意のアンパサンド (&) をとして`&amp;`エンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-288">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="d0b77-289">ソリューションエクスプローラー `TeamsAppManifest`で、フォルダーに移動して、ボット`manifest.json`チャネルの`id`登録`botId`時に保存した**bot アプリ ID**を開き、設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-289">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="pythontabpython"></a>[<span data-ttu-id="d0b77-290">Python</span><span class="sxs-lookup"><span data-stu-id="d0b77-290">Python</span></span>](#tab/python)

1. <span data-ttu-id="d0b77-291">Github リポジトリからサンプル[Teams bot 認証][teams-auth-bot-py]のクローンを作成します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-291">Clone the sample [Teams bot authentication][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="d0b77-292">**Config.py**を更新します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-292">Update **config.py**:</span></span>

    - <span data-ttu-id="d0b77-293">Bot `ConnectionName`に追加した OAuth 接続設定の名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-293">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="d0b77-294">Bot `MicrosoftAppId`の`MicrosoftAppPassword`アプリ ID とアプリシークレットを設定します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-294">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="d0b77-295">Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-295">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="d0b77-296">たとえば、任意のアンパサンド (&) をとして`&amp;`エンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-296">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="d0b77-297">Bot を Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="d0b77-297">Deploy the bot to Azure</span></span>

<span data-ttu-id="d0b77-298">Bot を展開するには、「 [Azure に bot を展開](https://aka.ms/azure-bot-deployment-cli)する方法」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="d0b77-298">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="d0b77-299">または、Visual Studio では、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-299">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="d0b77-300">Visual Studio の*ソリューションエクスプローラー*で、プロジェクト名を選択して、ホールド (または右クリック) します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-300">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="d0b77-301">ドロップダウンメニューで、[**発行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-301">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="d0b77-302">表示されたウィンドウで、**新しい**リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-302">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="d0b77-303">ダイアログウィンドウで、左側にある [ **App Service** ] を選択し、右側に [**新規作成**] を作成します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-303">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="d0b77-304">[**発行**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-304">Select the **Publish** button.</span></span>
1. <span data-ttu-id="d0b77-305">次のダイアログウィンドウで、必要な情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-305">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="d0b77-306">例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-306">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="d0b77-308">[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-308">Select **Create**.</span></span>
1. <span data-ttu-id="d0b77-309">展開が正常に完了すると、Visual Studio に反映されたことがわかります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-309">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="d0b77-310">さらに、*ボットの準備ができ*たことを示すページが既定のブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-310">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="d0b77-311">URL は、次`https://botteamsauth.azurewebsites.net/`のようになります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-311">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="d0b77-312">ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-312">Save it to a file.</span></span>
1. <span data-ttu-id="d0b77-313">ブラウザーで[**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-313">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="d0b77-314">リソースグループを確認すると、bot が他のリソースと共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-314">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="d0b77-315">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-315">The following image is an example:</span></span>

    ![teams-auth-service-グループ](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="d0b77-317">[リソース] グループで、bot チャネル登録名 (リンク) を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-317">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="d0b77-318">左側のパネルで、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-318">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="d0b77-319">[**メッセージングエンドポイント**] ボックスに、上で取得した`api/messages`URL に続けてを入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-319">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="d0b77-320">次に例を示し`https://botteamsauth.azurewebsites.net/api/messages`ます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-320">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="d0b77-321">左上隅にある [**保存**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-321">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="d0b77-322">エミュレーターを使用して bot をテストする</span><span class="sxs-lookup"><span data-stu-id="d0b77-322">Test the bot using the Emulator</span></span>

<span data-ttu-id="d0b77-323">まだ行っていない場合は、 [Microsoft Bot フレームワークエミュレーター](https://aka.ms/bot-framework-emulator-readme)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-323">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="d0b77-324">「[エミュレーターを使用してデバッグする](https://aka.ms/bot-framework-emulator-debug-with-emulator)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-324">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="d0b77-325">Bot のサンプルログインを機能させるには、以下のようにエミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-325">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="d0b77-326">認証用にエミュレーターを構成する</span><span class="sxs-lookup"><span data-stu-id="d0b77-326">Configure the Emulator for authentication</span></span>

<span data-ttu-id="d0b77-327">Bot が認証を必要とする場合は、以下に示すように、エミュレーターを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-327">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="d0b77-328">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-328">Start the Emulator.</span></span>
1. <span data-ttu-id="d0b77-329">エミュレーターで、左下の歯車アイコン &#9881;、または右上の [**エミュレーターの設定**] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-329">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="d0b77-330">チェックボックスをオンにするには、**バージョン1.0 の認証トークンを使用**します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-330">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="d0b77-331">**Ngrok**ツールへのローカルパスを入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-331">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="d0b77-332">Bot フレームワークエミュレーター/ngrok トンネリング統合[Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="d0b77-332">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="d0b77-333">ツールの詳細については、「 [ngrok](https://ngrok.com/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-333">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="d0b77-334">**エミュレーター起動時に ngrok を実行**してチェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-334">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="d0b77-335">[**保存**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-335">Select the **Save** button.</span></span>

<span data-ttu-id="d0b77-336">Bot がサインインカードを表示し、ユーザーがサインインボタンを選択すると、ユーザーが認証プロバイダーでサインインするために使用できるページがエミュレーターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-336">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="d0b77-337">ユーザーがこれを実行すると、プロバイダーはユーザートークンを生成して bot に送信します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-337">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="d0b77-338">その後、bot はユーザーの代わりに行動することができます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-338">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="d0b77-339">Bot をローカルでテストする</span><span class="sxs-lookup"><span data-stu-id="d0b77-339">Test the bot locally</span></span>

<span data-ttu-id="d0b77-340">認証メカニズムを構成した後は、実際の bot テストを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-340">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="d0b77-341">Visual Studio を使用して、お使いのコンピューターでローカルに bot サンプルを実行します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-341">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="d0b77-342">エミュレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-342">Start the Emulator.</span></span>
1. <span data-ttu-id="d0b77-343">[ **Open bot** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-343">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="d0b77-344">Bot の**url**に bot のローカル url を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-344">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="d0b77-345">通常は`http://localhost:3978/api/messages`、です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-345">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="d0b77-346">**Microsoft アプリ id**で、bot のアプリ id をから`appsettings.json`入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-346">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="d0b77-347">**Microsoft App パスワード**に、 `appsettings.json`からの bot のアプリパスワードを入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-347">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="d0b77-348">[**接続**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-348">Select **Connect**.</span></span>
1. <span data-ttu-id="d0b77-349">Bot が起動して実行されたら、サインインカードを表示するテキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-349">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="d0b77-350">[**サインイン**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-350">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="d0b77-351">開いている**URL を確認**するポップアップダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-351">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="d0b77-352">これにより、ボットのユーザー (ユーザー) が認証されるようになります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-352">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="d0b77-353">[**確認**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-353">Select **Confirm**.</span></span>
1. <span data-ttu-id="d0b77-354">要求された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-354">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="d0b77-355">エミュレーターで使用した構成に応じて、次のいずれかを取得します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-355">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="d0b77-356">**サインイン確認コードの使用**</span><span class="sxs-lookup"><span data-stu-id="d0b77-356">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="d0b77-357">検証コードを表示するウィンドウが開かれて &#x2713; ます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-357">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="d0b77-358">サインインを完了するには、&#x2713; コピーして、検証コードを [チャット] ボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-358">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="d0b77-359">**認証トークンを使用**します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-359">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="d0b77-360">資格情報に基づいてログインしている &#x2713;。</span><span class="sxs-lookup"><span data-stu-id="d0b77-360">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="d0b77-361">次の図は、ログインした後の bot UI の例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-361">The following image is an example of the bot UI after you've logged in:</span></span>

    ![auth bot ログインエミュレーター](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="d0b77-363">Bot から*トークンを表示するよう*求められたときに **[はい**] を選択すると、次のような応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-363">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![auth bot ログインエミュレータートークン](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="d0b77-365">サインアウトするには、[チャットの入力] ボックスに「**ログアウト**」と入力します。これにより、ユーザートークンが解放され、再びサインインするまでは、お客様の代わりに bot を操作することはできません。</span><span class="sxs-lookup"><span data-stu-id="d0b77-365">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="d0b77-366">Bot 認証には、 **Bot コネクタサービス**を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-366">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="d0b77-367">サービスは bot の bot チャネル登録情報にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-367">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="d0b77-368">展開した bot をテストする</span><span class="sxs-lookup"><span data-stu-id="d0b77-368">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="d0b77-369">ブラウザーで[**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-369">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="d0b77-370">リソースグループを検索します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-370">Find your resource group.</span></span>
1. <span data-ttu-id="d0b77-371">[リソース] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-371">Select the resource link.</span></span> <span data-ttu-id="d0b77-372">[リソース] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-372">The resource page is displayed.</span></span>
1. <span data-ttu-id="d0b77-373">[リソース] ページで、[ **Web チャットでテスト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-373">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="d0b77-374">Bot が開始し、定義済みの案内応答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-374">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="d0b77-375">[チャット] ボックスに何か入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-375">Type anything in the chat box.</span></span>
1. <span data-ttu-id="d0b77-376">[**サインイン**] ボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-376">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="d0b77-377">開いている**URL を確認**するポップアップダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-377">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="d0b77-378">これにより、ボットのユーザー (ユーザー) が認証されるようになります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-378">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="d0b77-379">[**確認**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-379">Select **Confirm**.</span></span>
1. <span data-ttu-id="d0b77-380">要求された場合は、該当するユーザーのアカウントを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-380">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="d0b77-381">次の図は、ログインした後の bot UI の例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-381">The following image is an example of the bot UI after you have logged in:</span></span>

    ![auth bot ログインの展開](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="d0b77-383">.</span><span class="sxs-lookup"><span data-stu-id="d0b77-383">.</span></span>

1. <span data-ttu-id="d0b77-384">[**はい**] ボタンを選択して、認証トークンを表示します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-384">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="d0b77-385">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-385">The following image is an example:</span></span>

    ![auth bot ログイン展開されたトークン](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="d0b77-387">.</span><span class="sxs-lookup"><span data-stu-id="d0b77-387">.</span></span>

1. <span data-ttu-id="d0b77-388">サインアウトするには、「ログアウト」と入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-388">Enter logout to sign out.</span></span>

    ![auth bot が展開したログアウト](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="d0b77-390">サインインで問題が発生した場合は、前の手順で説明したように、接続をもう一度テストしてください。</span><span class="sxs-lookup"><span data-stu-id="d0b77-390">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="d0b77-391">これにより、認証トークンが再作成されることがあります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-391">This could recreate the authentication token.</span></span>
> <span data-ttu-id="d0b77-392">「Azure の Bot フレームワーク Web チャットクライアント」では、認証が正しく設定される前に、数回サインインする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-392">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="d0b77-393">Teams に bot をインストールしてテストする</span><span class="sxs-lookup"><span data-stu-id="d0b77-393">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="d0b77-394">Bot プロジェクト`TeamsAppManifest`で、フォルダーに`manifest.json` `outline.png`と`color.png`ファイルが含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-394">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="d0b77-395">ソリューションエクスプローラーで、 `TeamsAppManifest`フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-395">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="d0b77-396">次`manifest.json`の値を割り当てることによって編集します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-396">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="d0b77-397">Bot チャネル登録時に受信した**Bot アプリ ID**がおよび`id` `botId`に割り当てられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-397">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="d0b77-398">次`validDomains: [ "token.botframework.com" ]`の値を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-398">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="d0b77-399">、、および`color.png`ファイル`manifest.json`を`outline.png`選択して**zip**にします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-399">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="d0b77-400">**Microsoft Teams**を開きます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-400">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="d0b77-401">左側のパネルで、下部にある [**アプリ] アイコン**を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-401">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="d0b77-402">右側のパネルで、下部にある [**カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-402">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="d0b77-403">`TeamsAppManifest`フォルダーに移動し、zip マニフェストをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-403">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="d0b77-404">次のウィザードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-404">The following wizard is displayed:</span></span>

    ![auth bot teams のアップロード](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="d0b77-406">[**チームに追加**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-406">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="d0b77-407">次のウィンドウで、ボットを使用するチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-407">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="d0b77-408">[ **Bot の設定**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-408">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="d0b77-409">左側のパネルで、3つのドット (&#x25cf;&#x25cf;&#x25cf;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-409">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="d0b77-410">次に、[ **App Studio** ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-410">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="d0b77-411">[**マニフェストエディター** ] タブを選択します。アップロードした bot のアイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-411">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="d0b77-412">また、bot とのメッセージの交換に使用できる連絡先として、その bot が連絡先として表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-412">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="d0b77-413">Teams でボットをローカルにテストする</span><span class="sxs-lookup"><span data-stu-id="d0b77-413">Testing the bot locally in Teams</span></span>

<span data-ttu-id="d0b77-414">Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからアクセスできるようにするには、すべてのサービスがアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-414">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="d0b77-415">そのため、ボット (サンプル) を Teams で使用できるようにするには、選択したクラウドにコードを発行するか、または**トンネル**ツールを使用して、ローカルに実行しているインスタンスを外部からアクセス可能にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-415">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="d0b77-416">[Ngrok](https://ngrok.com/download)を使用することをお勧めします。この URL は、コンピューター上でローカルに開いたポートに対して、外部アドレス指定可能な URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-416">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="d0b77-417">Microsoft Teams アプリをローカルで実行する準備として ngrok をセットアップするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-417">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="d0b77-418">ターミナルウィンドウで、が`ngrok.exe`インストールされているディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-418">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="d0b77-419">これを指すように、*環境変数*のパスを設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-419">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="d0b77-420">たとえば、を実行`ngrok http 3978 --host-header=localhost:3978`します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-420">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="d0b77-421">必要に応じてポート番号を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-421">Replace the port number as needed.</span></span>
<span data-ttu-id="d0b77-422">これにより、指定したポートをリッスンする ngrok が起動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-422">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="d0b77-423">これにより、ngrok が実行されている限り、外部的にアドレス指定可能な URL が得られます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-423">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="d0b77-424">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-424">The following image is an example:</span></span>

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="d0b77-426">.</span><span class="sxs-lookup"><span data-stu-id="d0b77-426">.</span></span>

1. <span data-ttu-id="d0b77-427">転送用の HTTPS アドレスをコピーします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-427">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="d0b77-428">これは、次のようになり`https://dea822bf.ngrok.io/`ます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-428">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="d0b77-429">取得`/api/messages` `https://dea822bf.ngrok.io/api/messages`する追加。</span><span class="sxs-lookup"><span data-stu-id="d0b77-429">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="d0b77-430">これは、コンピューター上でローカルに実行されていて、Microsoft Teams のチャットで web 経由でアクセスできる bot の**メッセージエンドポイント**です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-430">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="d0b77-431">最後に実行する手順の1つは、展開した bot のメッセージエンドポイントを更新することです。</span><span class="sxs-lookup"><span data-stu-id="d0b77-431">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="d0b77-432">この例では、bot を Azure に展開しました。</span><span class="sxs-lookup"><span data-stu-id="d0b77-432">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="d0b77-433">そのため、以下の手順を実行してみましょう。</span><span class="sxs-lookup"><span data-stu-id="d0b77-433">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="d0b77-434">ブラウザーで[**Azure ポータル**][azure-portal]に移動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-434">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="d0b77-435">**Bot チャネル登録**を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-435">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="d0b77-436">左側のパネルで、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-436">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="d0b77-437">右側のパネルの [**メッセージングエンドポイント**] ボックスに、ngrok URL (この例では) `https://dea822bf.ngrok.io/api/messages`を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-437">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="d0b77-438">Visual Studio デバッグモードなどで、ボットをローカルに起動します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-438">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="d0b77-439">Bot フレームワークポータルの**テスト Web チャット**を使用して、ローカルで実行中に bot をテストします。</span><span class="sxs-lookup"><span data-stu-id="d0b77-439">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="d0b77-440">エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d0b77-440">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="d0b77-441">`ngrok`が実行されているターミナルウィンドウで、ボットと web チャットクライアント間の HTTP トラフィックを確認できます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-441">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="d0b77-442">より詳細な表示が必要な場合は、ブラウザーウィンドウで`http://127.0.0.1:4040`以前のターミナルウィンドウから取得した情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-442">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="d0b77-443">次の画像は例です。</span><span class="sxs-lookup"><span data-stu-id="d0b77-443">The following image is an example:</span></span>

    ![auth bot teams ngrok テスト](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="d0b77-445">.</span><span class="sxs-lookup"><span data-stu-id="d0b77-445">.</span></span>

> [!NOTE]
> <span data-ttu-id="d0b77-446">Ngrok を停止してから再起動すると、URL が変更されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-446">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="d0b77-447">プロジェクトで ngrok を使用し、使用している機能に応じて、すべての URL 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-447">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>

## <a name="additional-information"></a><span data-ttu-id="d0b77-448">追加情報</span><span class="sxs-lookup"><span data-stu-id="d0b77-448">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="d0b77-449">TeamsAppManifest/manifest</span><span class="sxs-lookup"><span data-stu-id="d0b77-449">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="d0b77-450">このマニフェストには、Microsoft Teams が bot と接続するために必要な情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d0b77-450">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

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

<span data-ttu-id="d0b77-451">認証を使用すると、以下に説明するように、Teams は他のチャネルとはやや異なる方法で動作します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-451">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="d0b77-452">呼び出しアクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="d0b77-452">Handling Invoke Activity</span></span>

<span data-ttu-id="d0b77-453">**呼び出しアクティビティ**は、他のチャネルによって使用されるイベントアクティビティではなく bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-453">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="d0b77-454">これは、 **Activityhandler**のサブクラスによって実行されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-454">This is done by sub-classing the **ActivityHandler**.</span></span>

<span data-ttu-id="d0b77-455">**ボット/の bot**</span><span class="sxs-lookup"><span data-stu-id="d0b77-455">**Bots/DialogBot.cs**</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="d0b77-456">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d0b77-456">C#/.NET</span></span>](#tab/dotnet)

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="d0b77-457">**ボット/TeamsBot**</span><span class="sxs-lookup"><span data-stu-id="d0b77-457">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="d0b77-458">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-458">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="d0b77-459">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="d0b77-459">TeamsActivityHandler.cs</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="d0b77-460">Python</span><span class="sxs-lookup"><span data-stu-id="d0b77-460">Python</span></span>](#tab/python)

<span data-ttu-id="d0b77-461">**ボット/dialog_bot py**</span><span class="sxs-lookup"><span data-stu-id="d0b77-461">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="d0b77-462">**ボット/teams_bot py**</span><span class="sxs-lookup"><span data-stu-id="d0b77-462">**bots/teams_bot.py**</span></span>

<span data-ttu-id="d0b77-463">**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d0b77-463">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)] 

<span data-ttu-id="d0b77-464">**ダイアログ/main_dialog py**</span><span class="sxs-lookup"><span data-stu-id="d0b77-464">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="d0b77-465">ダイアログステップで、を使用`begin_dialog`して OAuth プロンプトを開始します。これにより、ユーザーにサインインするように求められます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-465">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="d0b77-466">ユーザーが既にサインインしている場合は、ユーザーに確認を求めることなく、トークン応答イベントが生成されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-466">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="d0b77-467">それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d0b77-467">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="d0b77-468">Azure Bot サービスは、ユーザーがサインインしようとした後に、トークン応答イベントを送信します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-468">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="d0b77-469">次のダイアログステップでは、前の手順の結果にトークンが存在するかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="d0b77-469">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="d0b77-470">Null でない場合、ユーザーは正常にサインインしています。</span><span class="sxs-lookup"><span data-stu-id="d0b77-470">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=54-65)]

<span data-ttu-id="d0b77-471">**ダイアログ/logout_dialog py**</span><span class="sxs-lookup"><span data-stu-id="d0b77-471">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="further-reading"></a><span data-ttu-id="d0b77-472">参考資料</span><span class="sxs-lookup"><span data-stu-id="d0b77-472">Further reading</span></span>

- [<span data-ttu-id="d0b77-473">Azure Bot サービスを使用して bot に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="d0b77-473">Add authentication to your bot via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
