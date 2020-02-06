1. <span data-ttu-id="87ab3-101">[Azure portal] [azure-ポータル] の左側のナビゲーションパネルで、[**リソースの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-101">In the [Azure portal][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="87ab3-102">右パネルの [選択] ボックスで、「bot」と入力します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-102">In the right panel selection box enter "bot".</span></span> <span data-ttu-id="87ab3-103">ボックスの一覧で、[ **Bot チャネル登録**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-103">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="87ab3-104">[**作成**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-104">Click the **Create** button.</span></span>
1. <span data-ttu-id="87ab3-105">**Bot チャネル登録**ブレードで、ボットに関する要求された情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-105">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="87ab3-106">[**メッセージングエンドポイント**] ボックスは空のままにしておき、bot の展開後に必要な URL を入力することになります。</span><span class="sxs-lookup"><span data-stu-id="87ab3-106">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="87ab3-107">次の図は、登録設定の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="87ab3-107">The following picture shows an example of the registration settings:</span></span>

    ![bot アプリチャネル登録](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="87ab3-109">[ **Microsoft アプリ ID とパスワード**] をクリックし、[**新規作成**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-109">Click **Microsoft App ID and password** and then **Create New**.</span></span>
1. <span data-ttu-id="87ab3-110">[**アプリ登録ポータル] リンクの [アプリ ID の作成] を**クリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-110">Click **Create App ID in the App Registration Portal** link.</span></span>
1. <span data-ttu-id="87ab3-111">表示された [**アプリの登録**] ウィンドウで、左上にある [**新しい登録**] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-111">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="87ab3-112">登録する bot アプリケーションの名前を入力します。 *BotTeamsAuth*を使用しています (独自の一意の名前を選択する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="87ab3-112">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="87ab3-113">**サポートされているアカウントの種類**については、*任意の組織ディレクトリ (任意の Azure AD ディレクトリのマルチテナント) と個人の Microsoft アカウント (Skype、Xbox など) でアカウント*を選択します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-113">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="87ab3-114">[**登録**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-114">Click the **Register** button.</span></span> <span data-ttu-id="87ab3-115">完了すると、アプリケーションの*概要*ページが Azure に表示されます。</span><span class="sxs-lookup"><span data-stu-id="87ab3-115">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="87ab3-116">[**アプリケーション (クライアント) ID** ] の値をコピーしてファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-116">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="87ab3-117">左側のパネルで、[**証明書とシークレット**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-117">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="87ab3-118">[*クライアントシークレット*] で、[**新しいクライアントシークレット**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-118">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="87ab3-119">このアプリ用に作成する必要がある他のユーザーからこのシークレットを識別するための説明を追加します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-119">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="87ab3-120">選択範囲に*期限*を設定します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-120">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="87ab3-121">[**追加**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-121">Click **Add**.</span></span>
    1. <span data-ttu-id="87ab3-122">クライアントシークレットをコピーして、ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="87ab3-122">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="87ab3-123">[ **Bot チャネル登録**] ウィンドウに戻り、[ **Microsoft app id** ] ボックスと [**パスワード**] ボックスに、*アプリ id*と*クライアントシークレット*をそれぞれコピーします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-123">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="87ab3-124">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-124">Click **OK**.</span></span>
1. <span data-ttu-id="87ab3-125">最後に、[**作成**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="87ab3-125">Finally, click **Create**.</span></span>