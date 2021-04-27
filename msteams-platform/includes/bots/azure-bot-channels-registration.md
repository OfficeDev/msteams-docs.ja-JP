---
title: Azure ボット チャネル登録
description: 登録用の Azure ボット チャネルについて説明します
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020950"
---
1. <span data-ttu-id="f369a-103">Azure ポータル [の [Azure サービス](https://ms.portal.azure.com/#home)] で、[リソースの作成] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f369a-103">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select **Create a resource**.</span></span>
1. <span data-ttu-id="f369a-104">検索ボックスに「bot」と入力します。</span><span class="sxs-lookup"><span data-stu-id="f369a-104">In the search box enter "bot".</span></span> <span data-ttu-id="f369a-105">ドロップダウン リストで、[ボット チャネル登録] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f369a-105">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="f369a-106">[作成] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="f369a-106">Select the **Create** button.</span></span>
1. <span data-ttu-id="f369a-107">[ボット チャネル **登録] ブレード** で、ボットに関する要求された情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="f369a-107">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="f369a-108">[メッセージング **エンドポイント] ボックスを** 空のままにしておき、ボットの展開後に必要な URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="f369a-108">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="f369a-109">次の図は、登録設定の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="f369a-109">The following picture shows an example of the registration settings:</span></span>

    ![ボット アプリ チャネルの登録](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="f369a-111">[Microsoft **App ID とパスワード] をクリックし、[** 新規作成 **] をクリックします**。</span><span class="sxs-lookup"><span data-stu-id="f369a-111">Click **Microsoft App ID and password** and then **Create New**.</span></span>

    <span data-ttu-id="f369a-112">![Create Microsoft App ID ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span><span class="sxs-lookup"><span data-stu-id="f369a-112">![Create Microsoft App ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span></span>    

1. <span data-ttu-id="f369a-113">[アプリ **登録ポータル] リンクの [アプリ ID の作成] を** クリックします。</span><span class="sxs-lookup"><span data-stu-id="f369a-113">Click **Create App ID in the App Registration Portal** link.</span></span>

   ![アプリの登録](../../assets/images/authentication/AppRegistration.png)
   
1. <span data-ttu-id="f369a-115">表示されたアプリ **登録ウィンドウで** 、左上の **[新規登録** ] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f369a-115">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="f369a-116">登録するボット アプリケーションの名前を入力します *。BotTeamsAuth* を使用しました (独自の一意の名前を選択する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="f369a-116">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="f369a-117">[サポート **されているアカウント** の種類] で、[任意の組織ディレクトリのアカウント] (任意の Azure AD ディレクトリ - マルチテナント) と個人用 Microsoft アカウント *(Skype、Xbox など) を選択します*。</span><span class="sxs-lookup"><span data-stu-id="f369a-117">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="f369a-118">[登録] **ボタンをクリック** します。</span><span class="sxs-lookup"><span data-stu-id="f369a-118">Click the **Register** button.</span></span> <span data-ttu-id="f369a-119">完了すると、Azure はアプリケーションの *[概要* ] ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="f369a-119">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="f369a-120">アプリケーション (クライアント) ID 値 **をファイルにコピーして保存** します。</span><span class="sxs-lookup"><span data-stu-id="f369a-120">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="f369a-121">左側のパネルで、[証明書とシークレット **] をクリックします**。</span><span class="sxs-lookup"><span data-stu-id="f369a-121">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="f369a-122">[ *クライアント シークレット] で、[* 新しい **クライアント シークレット] をクリックします**。</span><span class="sxs-lookup"><span data-stu-id="f369a-122">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="f369a-123">このアプリ用に作成する必要がある他のユーザーからこのシークレットを識別するための説明を追加します。</span><span class="sxs-lookup"><span data-stu-id="f369a-123">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="f369a-124">[ *有効期限] を選択* に設定します。</span><span class="sxs-lookup"><span data-stu-id="f369a-124">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="f369a-125">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f369a-125">Click **Add**.</span></span>
    1. <span data-ttu-id="f369a-126">クライアント シークレットをコピーし、ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="f369a-126">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="f369a-127">[ボット チャネル登録 **] ウィンドウ** に戻り、アプリ IDとクライアント シークレットをそれぞれ [Microsoft アプリ *ID]* ボックスと **[** パスワード] ボックスにコピーします。 </span><span class="sxs-lookup"><span data-stu-id="f369a-127">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="f369a-128">[**OK**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f369a-128">Click **OK**.</span></span>
1. <span data-ttu-id="f369a-129">最後に、[作成] を **クリックします**。</span><span class="sxs-lookup"><span data-stu-id="f369a-129">Finally, click **Create**.</span></span>

<span data-ttu-id="f369a-130">Azure が登録リソースを作成すると、リソース グループの一覧に含まれます。</span><span class="sxs-lookup"><span data-stu-id="f369a-130">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![ボット アプリ チャネル登録グループ](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

<span data-ttu-id="f369a-132">ボット チャネルの登録が作成されると、Teams チャネルを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f369a-132">Once your bot channels registration is created, you'll need to enable the Teams channel.</span></span>

1. <span data-ttu-id="f369a-133">Azure ポータル [の [Azure](https://ms.portal.azure.com/#home)サービス] で、作成 **したボット チャネル登録** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f369a-133">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select the **Bot Channel Registration** you just created.</span></span>
1. <span data-ttu-id="f369a-134">左側のパネルで、[チャネル] を **クリックします**。</span><span class="sxs-lookup"><span data-stu-id="f369a-134">In the left panel, click **Channels**.</span></span>
1. <span data-ttu-id="f369a-135">[Microsoft Teams] アイコンをクリックし、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f369a-135">Click the Microsoft Teams icon, then choose **Save**.</span></span>
