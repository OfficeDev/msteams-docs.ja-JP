---
title: チャットボットPower Virtual Agents Teamsに追加する
author: laujan
description: Teams プラットフォームにPower Virtual Agentsチャットボットを統合する
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2a8f9c23eaa1acf2555b91cc4caf8d0f3298c114
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566118"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="057fd-103">Power Virtual Agents チャットボットを追加する</span><span class="sxs-lookup"><span data-stu-id="057fd-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="057fd-104">Power Virtual Agentsは、Teamsプラットフォームと簡単に統合できる豊富な会話型チャットボットを作成できる、コードなしのガイド付きグラフィカルインターフェイスソリューションです。</span><span class="sxs-lookup"><span data-stu-id="057fd-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="057fd-105">Power Virtual Agentsで作成されたすべてのコンテンツは、Teamsで自然にレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="057fd-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="057fd-106">Power Virtual Agentsボットは、Teamsネイティブチャットキャンバスでユーザーと交流します。</span><span class="sxs-lookup"><span data-stu-id="057fd-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="057fd-107">IT 管理者、ビジネス アナリスト、ドメイン スペシャリスト、および熟練したアプリ開発者は、開発環境をセットアップしなくても、Teams用のインテリジェント仮想エージェントを設計、開発、および公開できます。</span><span class="sxs-lookup"><span data-stu-id="057fd-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="057fd-108">Web サービスを作成することも、Bot フレームワークに直接登録することもできます。</span><span class="sxs-lookup"><span data-stu-id="057fd-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="057fd-109">このドキュメントでは、Power Virtual Agents ポータルを通じてチャットボットをTeamsで利用できるようにする方法と、App Studio を使用してボットをTeamsに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="057fd-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="057fd-110">Power Virtual Agentsを使用すると、顧客、他の従業員、またはウェブサイトやサービスへの訪問者が提起した質問に答えることができる強力なチャットボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="057fd-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="057fd-111">これらのボットは、データ サイエンティストや開発者が必要とせずに簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="057fd-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="057fd-112">Microsoft Teamsにチャットボットを追加すると、ボット コンテンツやユーザー チャット コンテンツなどの一部のデータがMicrosoft Teamsと共有されます。</span><span class="sxs-lookup"><span data-stu-id="057fd-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="057fd-113">つまり、データは [組織のコンプライアンスや地理的または地域の境界](/power-virtual-agents/data-location)の外に流れます。</span><span class="sxs-lookup"><span data-stu-id="057fd-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="057fd-114">Power Virtual Agents ポータルを介してチャットボットをTeamsで利用できるようにする</span><span class="sxs-lookup"><span data-stu-id="057fd-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="057fd-115">Power Virtual Agents ポータルを通じてチャットボットをTeamsで利用できるようにするには、次のプロセス手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="057fd-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="057fd-116">**チャットボットをTeamsで利用できるようにするには**</span><span class="sxs-lookup"><span data-stu-id="057fd-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="057fd-117">**最新のボット コンテンツを発行する**</span><span class="sxs-lookup"><span data-stu-id="057fd-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="057fd-118">Power Virtual Agents ポータルでチャットボットを作成した後、ユーザーが操作できるようにするには、Teams前にボットを公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="057fd-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="057fd-119">詳細については、「 [最新のボット コンテンツを発行する](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="057fd-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![電源仮想エージェント ポータルでの公開](../../assets/images/pva-publish.png)

1. <span data-ttu-id="057fd-121">**Teams チャネルを構成する**</span><span class="sxs-lookup"><span data-stu-id="057fd-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="057fd-122">ボットを公開したら、Teamsチャネルを追加して、ボットをTeamsユーザーが利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="057fd-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![電源仮想エージェント ポータルのチャネル](../../assets/images/pva-channels.png)

1. <span data-ttu-id="057fd-124">**チャットボットのアプリ ID を生成する**</span><span class="sxs-lookup"><span data-stu-id="057fd-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="057fd-125">チャットボットにTeamsチャンネルを追加すると、ダイアログボックスに **アプリID** が生成されます。</span><span class="sxs-lookup"><span data-stu-id="057fd-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="057fd-126">アプリ ID は、マイクロソフトが生成したボットの一意の識別子です。</span><span class="sxs-lookup"><span data-stu-id="057fd-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="057fd-127">アプリ ID を保存して、Teams用のアプリ パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="057fd-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="057fd-128">アプリスタジオを使用してTeamsにボットを追加する</span><span class="sxs-lookup"><span data-stu-id="057fd-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="057fd-129">Teamsインスタンスで[カスタムアプリのアップロードが有効になっている場合、Teams](/microsoftteams/admin-settings) App Studio を使用してチャットボットを直接アップロードし、すぐに使用を開始できます。</span><span class="sxs-lookup"><span data-stu-id="057fd-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="057fd-130">チャットボットを共有するには、管理者にリクエストして、ボットをテナント アプリ カタログで利用できるようにするか、アプリ パッケージを他のユーザーに送信して、個別にアップロードするように依頼することができます。</span><span class="sxs-lookup"><span data-stu-id="057fd-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="057fd-131">**Teams に App Studio をインストールする**</span><span class="sxs-lookup"><span data-stu-id="057fd-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="057fd-132">アプリスタジオはTeamsアプリです。</span><span class="sxs-lookup"><span data-stu-id="057fd-132">App Studio is a Teams app.</span></span> <span data-ttu-id="057fd-133">Teamsでのボットの作成と登録のプロセスを簡略化するTeamsストアからアプリスタジオをインストールします。</span><span class="sxs-lookup"><span data-stu-id="057fd-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="057fd-134">インスタンスからアプリストアアイコンTeams選択し **、App Studio を** 検索します。</span><span class="sxs-lookup"><span data-stu-id="057fd-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="057fd-135">**[App Studio]** タイルを選択し、ポップアップ ダイアログ ボックスで [**インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="057fd-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="057fd-136">**アプリスタジオでTeamsアプリマニフェストを作成する**</span><span class="sxs-lookup"><span data-stu-id="057fd-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="057fd-137">Teamsのボットは、ボットとその機能に関する基本情報を提供するアプリ マニフェスト JSON ファイルによって定義されます。</span><span class="sxs-lookup"><span data-stu-id="057fd-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="057fd-138">**[App Studio]** で [**マニフェスト エディター**] を選択し、[**新しいアプリの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="057fd-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>

    ![新しいアプリを作成する](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="057fd-140">**ボットの詳細を追加する**</span><span class="sxs-lookup"><span data-stu-id="057fd-140">**Add your bot details**</span></span>  
<span data-ttu-id="057fd-141">すべての必須フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="057fd-141">Complete all the required fields.</span></span> <span data-ttu-id="057fd-142">各フィールドの詳細については、「マニフェスト [スキーマ](../../resources/schema/manifest-schema.md)定義」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="057fd-142">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>

    ![アプリの詳細を追加する](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="057fd-144">**ボットを設定する** ボットをセットアップするには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="057fd-144">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="057fd-145">**[ボット**] タブを開きます。</span><span class="sxs-lookup"><span data-stu-id="057fd-145">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="057fd-146">[  >  **既存のボットの** セットアップ] を選択し、ボットの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="057fd-146">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   ![ボットのセットアップ](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="057fd-148">次の図は、既存のボットを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="057fd-148">The following image depicts how to set-up an existing bot:</span></span>      

   ![既存のボットのセットアップ](../../assets/images/get-started/existing-bot-set-up.png)
       
1. <span data-ttu-id="057fd-150">**アプリ ID を追加する**</span><span class="sxs-lookup"><span data-stu-id="057fd-150">**Add your App ID**</span></span>  
<span data-ttu-id="057fd-151">アプリ ID を追加するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="057fd-151">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="057fd-152">**[Connect別のボット ID に** 選択し、先ほどコピーした **アプリ ID** を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="057fd-152">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="057fd-153">**[ スコープ**  >  **の個人用**  >  保存 ]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="057fd-153">Select **Scope** > **Personal** > **Save**.</span></span>

    ![アプリ ID を追加する](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="057fd-155">**ボットの有効なドメインを追加する**</span><span class="sxs-lookup"><span data-stu-id="057fd-155">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="057fd-156">この手順は、ボットでユーザーがサインインする必要がある場合にのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="057fd-156">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="057fd-157">[ **ドメインとアクセス許可] を** 選択し、[ **有効なドメイン]** フィールドに次の入力を入力します。</span><span class="sxs-lookup"><span data-stu-id="057fd-157">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

1. <span data-ttu-id="057fd-158">**ボットをテストして配布する**</span><span class="sxs-lookup"><span data-stu-id="057fd-158">**Test and distribute your bot**</span></span>  
<span data-ttu-id="057fd-159">**[テストと配布**] タブを開き、[**インストール]** を選択して、ボットをTeamsインスタンスに直接追加します。</span><span class="sxs-lookup"><span data-stu-id="057fd-159">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="057fd-160">または、完成したアプリ パッケージをダウンロードしてTeamsユーザーと共有したり、管理者に提供してボットをテナント アプリ カタログで利用できるようにしたりできます。</span><span class="sxs-lookup"><span data-stu-id="057fd-160">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

1. <span data-ttu-id="057fd-161">**チャットを開始する** </span><span class="sxs-lookup"><span data-stu-id="057fd-161">**Start a chat** </span></span>  
<span data-ttu-id="057fd-162">Power Virtual AgentsチャットボットをTeamsに追加するためのセットアッププロセスが完了しました。</span><span class="sxs-lookup"><span data-stu-id="057fd-162">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="057fd-163">これで、個人的なチャットでボットとの会話を開始できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="057fd-163">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="057fd-164">関連項目</span><span class="sxs-lookup"><span data-stu-id="057fd-164">See also</span></span>

- [<span data-ttu-id="057fd-165">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="057fd-165">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- <span data-ttu-id="057fd-166">[マイクロソフト Power Virtual Agents でTeamsするためのチャット ボットを作成](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)します。</span><span class="sxs-lookup"><span data-stu-id="057fd-166">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  

- [<span data-ttu-id="057fd-167">Power Virtual Agentsポータル</span><span class="sxs-lookup"><span data-stu-id="057fd-167">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)

- [<span data-ttu-id="057fd-168">Power Virtual Agentsボットを公開する</span><span class="sxs-lookup"><span data-stu-id="057fd-168">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)

- <span data-ttu-id="057fd-169">[Microsoft Teams のセキュリティとコンプライアンス](/MicrosoftTeams/security-compliance-overview)</span><span class="sxs-lookup"><span data-stu-id="057fd-169">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="057fd-170">次の手順</span><span class="sxs-lookup"><span data-stu-id="057fd-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="057fd-171">仮想アシスタントの作成</span><span class="sxs-lookup"><span data-stu-id="057fd-171">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

