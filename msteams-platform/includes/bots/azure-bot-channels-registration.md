1. <span data-ttu-id="20457-101">[Azure portal](https://ms.portal.azure.com/#home) の [Azure サービス] で、**[リソースの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20457-101">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select **Create a resource**.</span></span>
1. <span data-ttu-id="20457-102">検索ボックスに「ボット」と入力します。</span><span class="sxs-lookup"><span data-stu-id="20457-102">In the search box enter "bot".</span></span> <span data-ttu-id="20457-103">ドロップダウン リストで、**[ボット チャネルの登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20457-103">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="20457-104">**[作成]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="20457-104">Select the **Create** button.</span></span>
1. <span data-ttu-id="20457-105">**[ボット チャネルの登録]** ブレードで、ボットについて要求された情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="20457-105">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="20457-106">**[メッセージング エンドポイント]** ボックスは今のところ空のままにしておきます。ボットを展開した後、必要な URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="20457-106">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="20457-107">次の図は、登録設定の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="20457-107">The following picture shows an example of the registration settings:</span></span>

    ![ボット アプリ チャネルの登録](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="20457-109">**[Microsoft アプリ ID とパスワード]** をクリックしてから、**[新規作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-109">Click **Microsoft App ID and password** and then **Create New**.</span></span>

    <span data-ttu-id="20457-110">![[Microsoft アプリ ID を作成する]](../../assets/images/authentication/CreateMicrosoftAppID.png) ![[新しい Microsoft アプリ ID を作成する]](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span><span class="sxs-lookup"><span data-stu-id="20457-110">![Create Microsoft App ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span></span>    

1. <span data-ttu-id="20457-111">**[App Registration Portal でアプリ ID を作成する]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-111">Click **Create App ID in the App Registration Portal** link.</span></span>

   ![アプリの登録](../../assets/images/authentication/AppRegistration.png)
   
1. <span data-ttu-id="20457-113">表示された **[アプリ登録]** ウィンドウで、左上の **[新規登録]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-113">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="20457-114">登録するボット アプリケーションの名前を入力します。*BotTeamsAuth* を使用しました (独自の一意の名前を選択する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="20457-114">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="20457-115">**[サポートされているアカウントの種類]** の場合は、*[任意の組織のディレクトリ内のアカウント (任意の Azure AD ディレクトリ - マルチテナント) と個人用の Microsoft アカウント (例: Skype、 Xbox)]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="20457-115">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="20457-116">**[登録]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-116">Click the **Register** button.</span></span> <span data-ttu-id="20457-117">完了すると、Azure はアプリケーションの *[概要]* ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="20457-117">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="20457-118">**[アプリケーション (クライアント) ID]** の値をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="20457-118">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="20457-119">左側のパネルで、**[証明書とシークレット]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-119">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="20457-120">*[クライアント シークレット]* で、**[新しいクライアント シークレット]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-120">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="20457-121">このアプリ用に作成する可能性のある他のユーザーからこのシークレットを識別するための説明を追加します。</span><span class="sxs-lookup"><span data-stu-id="20457-121">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="20457-122">*[期限切れ]* を選択に設定します。</span><span class="sxs-lookup"><span data-stu-id="20457-122">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="20457-123">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-123">Click **Add**.</span></span>
    1. <span data-ttu-id="20457-124">クライアント シークレットをコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="20457-124">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="20457-125">**[ボット チャネルの登録]** ウィンドウに戻り、**[Microsoft アプリ ID]** では *[アプリ ID]*、**[パスワード]** ボックスでは *[クライアント シークレット]* をそれぞれコピーします。</span><span class="sxs-lookup"><span data-stu-id="20457-125">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="20457-126">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-126">Click **OK**.</span></span>
1. <span data-ttu-id="20457-127">最後に、**[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-127">Finally, click **Create**.</span></span>

<span data-ttu-id="20457-128">Azure が登録リソースを作成すると、リソース グループ リストに含まれます。</span><span class="sxs-lookup"><span data-stu-id="20457-128">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![ボット アプリ チャネル登録グループ](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

<span data-ttu-id="20457-130">ボット チャネルの登録が作成されたら、Teams チャネルを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="20457-130">Once your bot channels registration is created, you'll need to enable the Teams channel.</span></span>

1. <span data-ttu-id="20457-131">[Azure portal](https://ms.portal.azure.com/#home) の [Azure サービス] で、作成した **[ボット チャネルの登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20457-131">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select the **Bot Channel Registration** you just created.</span></span>
1. <span data-ttu-id="20457-132">左側のパネルで、**[チャンネル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="20457-132">In the left panel, click **Channels**.</span></span>
1. <span data-ttu-id="20457-133">Microsoft Teams アイコンをクリックし、**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="20457-133">Click the Microsoft Teams icon, then choose **Save**.</span></span>
