## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="66ebc-101">アプリを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="66ebc-101">Deploy your app to Azure</span></span>

<span data-ttu-id="66ebc-102">展開は 2 つの手順で構成されます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-102">Deployment consists of two steps.</span></span>  <span data-ttu-id="66ebc-103">まず、必要なクラウド リソース (プロビジョニングとも呼ばれる) が作成され、アプリを構成するコードが作成されたクラウド リソースにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-103">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="66ebc-104">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="66ebc-104">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="66ebc-105">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-105">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="66ebc-106">サイドバーからTeams Toolkitアイコンを選択してTeamsします。</span><span class="sxs-lookup"><span data-stu-id="66ebc-106">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="66ebc-107">[クラウド **でプロビジョニング] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="66ebc-107">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="プロビジョニング コマンドを示すスクリーンショット":::

1. <span data-ttu-id="66ebc-109">必要に応じて、Azure リソースに使用するサブスクリプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="66ebc-109">If required, select a subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="66ebc-110">アプリのホスティングに使用される Azure リソースは常にいくつかある。</span><span class="sxs-lookup"><span data-stu-id="66ebc-110">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="66ebc-111">Azure でリソースを実行するときにコストが発生する可能性があるという警告がダイアログで表示されます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-111">A dialog warns you that costs may be incurred when running resources in Azure.</span></span>  <span data-ttu-id="66ebc-112">[プロビジョニング **] を押します**。</span><span class="sxs-lookup"><span data-stu-id="66ebc-112">Press **Provision**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="プロビジョニング ダイアログのスクリーンショット。":::

   <span data-ttu-id="66ebc-114">プロビジョニング プロセスによって、Azure クラウドにリソースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-114">The provisioning process will create resources in the Azure cloud.</span></span>  <span data-ttu-id="66ebc-115">これには時間がかかるでしょう。</span><span class="sxs-lookup"><span data-stu-id="66ebc-115">This will take some time.</span></span>  <span data-ttu-id="66ebc-116">右下隅のダイアログを見て、進行状況を監視できます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-116">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="66ebc-117">数分後、次の通知が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-117">After a few minutes, you will see the following notice:</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="プロビジョニング完了ダイアログを示すスクリーンショット。":::

1. <span data-ttu-id="66ebc-119">プロビジョニングが完了したら、[クラウドに **展開する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="66ebc-119">Once provisioning is complete, select **Deploy to the Cloud**.</span></span>  <span data-ttu-id="66ebc-120">プロビジョニングと同様に、このプロセスには時間がかかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="66ebc-120">As with provisioning, this process takes some time.</span></span>  <span data-ttu-id="66ebc-121">右下隅にあるダイアログを見て、プロセスを監視できます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-121">You can monitor the process by watching the dialogs in the bottom right corner.</span></span> <span data-ttu-id="66ebc-122">数分後、完了通知が表示されます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-122">After a few minutes, you will see a completion notice.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="66ebc-123">Command Line/コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="66ebc-123">Command Line</span></span>](#tab/cli)

<span data-ttu-id="66ebc-124">ターミナル ウィンドウで次の設定を行います。</span><span class="sxs-lookup"><span data-stu-id="66ebc-124">In your terminal window:</span></span>

1. <span data-ttu-id="66ebc-125">`teamsfx provision` を実行します。</span><span class="sxs-lookup"><span data-stu-id="66ebc-125">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="66ebc-126">Azure サブスクリプションにログインするように求めるメッセージが表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="66ebc-126">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="66ebc-127">必要に応じて、Azure リソースに使用する Azure サブスクリプションを選択するように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66ebc-127">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="66ebc-128">アプリのホスティングに使用される Azure リソースは常にいくつかある。</span><span class="sxs-lookup"><span data-stu-id="66ebc-128">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="66ebc-129">`teamsfx deploy` を実行します。</span><span class="sxs-lookup"><span data-stu-id="66ebc-129">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> <span data-ttu-id="66ebc-130">**プロビジョニングと展開の違いは何ですか?**</span><span class="sxs-lookup"><span data-stu-id="66ebc-130">**What's the difference between Provision and Deploy?**</span></span>
>
> <span data-ttu-id="66ebc-131">プロビジョニング **手順** では、アプリの Azure と M365 にリソースが作成されますが、コード (HTML、CSS、JavaScript など) はリソースにコピーされません。</span><span class="sxs-lookup"><span data-stu-id="66ebc-131">The **Provision** step will create resources in Azure and M365 for your app, but no code (HTML, CSS, JavaScript, etc.) is copied to the resources.</span></span>  <span data-ttu-id="66ebc-132">[ **展開]** 手順では、プロビジョニング 手順で作成したリソースにアプリのコードをコピーします。</span><span class="sxs-lookup"><span data-stu-id="66ebc-132">The **Deploy** step will copy the code for your app to the resources you created during the provision step.</span></span>  <span data-ttu-id="66ebc-133">新しいリソースをプロビジョニングせずに複数回展開するのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="66ebc-133">It is common to deploy multiple times without provisioning new resources.</span></span> <span data-ttu-id="66ebc-134">プロビジョニング 手順の完了には時間がかかる場合があります。展開手順とは別の手順です。</span><span class="sxs-lookup"><span data-stu-id="66ebc-134">Since the provision step can take some time to complete, it is separate from the deployment step.</span></span>

<span data-ttu-id="66ebc-135">プロビジョニングと展開の手順が完了したら、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="66ebc-135">Once the provisioning and deployment steps are finished:</span></span>

1. <span data-ttu-id="66ebc-136">[Visual Studio Codeから、デバッグ パネルを開きます **(Ctrl+Shift+D**  /  **[ctrl]+[--D]** または [実行>**表示**)</span><span class="sxs-lookup"><span data-stu-id="66ebc-136">From Visual Studio Code, open the debug panel (**Ctrl+Shift+D** / **⌘⇧-D** or **View > Run**)</span></span>
1. <span data-ttu-id="66ebc-137">[起動 **構成] ドロップダウンから [リモート** の起動 ] (エッジ) を選択します。</span><span class="sxs-lookup"><span data-stu-id="66ebc-137">Select **Launch Remote (Edge)** from the launch configuration drop-down.</span></span>
1. <span data-ttu-id="66ebc-138">[再生] ボタンを押してアプリを起動します 。Azure からリモートで実行中です。</span><span class="sxs-lookup"><span data-stu-id="66ebc-138">Press the Play button to launch your app - now running remotely from Azure!</span></span>