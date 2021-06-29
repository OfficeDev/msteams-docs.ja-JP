## <a name="upload-your-tab-with-app-studio"></a><span data-ttu-id="32b62-101">アップロード App Studio でタブを開く</span><span class="sxs-lookup"><span data-stu-id="32b62-101">Upload your tab with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="32b62-102">App **Studio を使用して**、ファイル上manifest.js **編集し**、完成したパッケージをファイルにアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="32b62-102">We use **App Studio** to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="32b62-103">また、手動で編集することもできます **manifest.jsをオンにしてください**。</span><span class="sxs-lookup"><span data-stu-id="32b62-103">You can also manually edit **manifest.json**.</span></span> <span data-ttu-id="32b62-104">その場合は、ソリューションを再度ビルドして、アップロードする **Tab.zip作成してください** 。</span><span class="sxs-lookup"><span data-stu-id="32b62-104">If you do, ensure that you build the solution again to create the **Tab.zip** file to upload.</span></span>

<span data-ttu-id="32b62-105">**App Studio でタブをアップロードするには**</span><span class="sxs-lookup"><span data-stu-id="32b62-105">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="32b62-106">[次へ] にMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="32b62-106">Go to Microsoft Teams.</span></span> <span data-ttu-id="32b62-107">Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="32b62-107">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="32b62-108">[App **Studio] に移動し** 、[マニフェスト エディター **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="32b62-108">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="32b62-109">[ **マニフェスト エディターで既存のアプリ** をインポートする] **を選択して** 、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。</span><span class="sxs-lookup"><span data-stu-id="32b62-109">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="32b62-110">アプリ パッケージの名前は次 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="32b62-110">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="32b62-111">これは、次のパスから使用できます。</span><span class="sxs-lookup"><span data-stu-id="32b62-111">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="32b62-112">アップロードtab.zipApp  **Studio にアクセスします**。</span><span class="sxs-lookup"><span data-stu-id="32b62-112">Upload **tab.zip** to **App Studio**.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="32b62-113">マニフェスト エディターを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="32b62-113">Update your app package with Manifest editor</span></span>

<span data-ttu-id="32b62-114">アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32b62-114">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="32b62-115">マニフェスト エディターのウェルカム ページの右側のパネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="32b62-115">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="32b62-116">マニフェスト エディターの左側にある手順の一覧と、右側には、これらの各手順の値が必要なプロパティの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="32b62-116">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="32b62-117">この情報の多くが、ユーザーのmanifest.js **によって** 提供されますが、更新する必要があるフィールドがあります。</span><span class="sxs-lookup"><span data-stu-id="32b62-117">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="32b62-118">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="32b62-118">Details: App details</span></span>

<span data-ttu-id="32b62-119">[アプリ **の詳細] セクションで、次の内容を実行** します。</span><span class="sxs-lookup"><span data-stu-id="32b62-119">In the **App details** section:</span></span>

1. <span data-ttu-id="32b62-120">**[Id] で**、[**生成] を** 選択して、アプリの新しいアプリ ID を生成します。</span><span class="sxs-lookup"><span data-stu-id="32b62-120">Under **Identification**, select **Generate** to generate a new App Id for your app.</span></span>

1. <span data-ttu-id="32b62-121">[ **開発者情報]** で **、ngrok** HTTPS URL を使用 **して Web サイトを** 更新します。</span><span class="sxs-lookup"><span data-stu-id="32b62-121">Under **Developer information**, update the **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="32b62-122">[**アプリの URL] で**、[プライバシーに関する **声明] と**[使用条件] を更新して、>。 `https://<yourngrokurl>/privacy`  `https://<yourngrokurl>/tou`</span><span class="sxs-lookup"><span data-stu-id="32b62-122">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="32b62-123">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="32b62-123">Capabilities: Tabs</span></span>

<span data-ttu-id="32b62-124">[タブ **] セクションで、次の設定を** 行います。</span><span class="sxs-lookup"><span data-stu-id="32b62-124">In the **Tabs** section:</span></span>

1. <span data-ttu-id="32b62-125">[個人用 **タブの追加] で、[** 追加] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="32b62-125">Under **Add a personal tab**, select **Add**.</span></span> <span data-ttu-id="32b62-126">ポップアップ ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="32b62-126">A pop-up dialog box appears.</span></span>

1. <span data-ttu-id="32b62-127">[名前] に個人用タブの名前を **入力します**。</span><span class="sxs-lookup"><span data-stu-id="32b62-127">Enter a name for the personal tab in **Name**.</span></span>

1. <span data-ttu-id="32b62-128">エンティティ **ID を入力します**。</span><span class="sxs-lookup"><span data-stu-id="32b62-128">Enter the **Entity ID**.</span></span>

1. <span data-ttu-id="32b62-129">で **コンテンツ URL を** 更新 `https://<yourngrokurl>/personalTab` します。</span><span class="sxs-lookup"><span data-stu-id="32b62-129">Update **Content URL** with `https://<yourngrokurl>/personalTab`.</span></span>

    <span data-ttu-id="32b62-130">[Web サイト **の URL] フィールドは** 空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="32b62-130">Leave the **Website URL** field blank.</span></span>

1. <span data-ttu-id="32b62-131">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="32b62-131">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="32b62-132">完了: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="32b62-132">Finish: Domains and permissions</span></span>

<span data-ttu-id="32b62-133">[ドメイン **とアクセス許可**] セクションの[タブのドメイン] フィールドには、HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="32b62-133">In the **Domains and permissions** section, the **Domains from your tabs** field must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="32b62-134">完了: テストと配布</span><span class="sxs-lookup"><span data-stu-id="32b62-134">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="32b62-135">右側の [説明] **で**、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="32b62-135">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="32b62-136">&#9888; **'validDomains' 配列にトンネリング サイトを含めすることはできません。..**</span><span class="sxs-lookup"><span data-stu-id="32b62-136">&#9888; **The 'validDomains' array cannot contain a tunneling site...**</span></span>
>
><span data-ttu-id="32b62-137">この警告は、タブのテスト中に無視できます。</span><span class="sxs-lookup"><span data-stu-id="32b62-137">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="32b62-138">[テストと **配布] セクションで、[** インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="32b62-138">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="32b62-139">ポップアップ ダイアログ ボックスで、[追加] を **選択し、** タブに 2 つのオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="32b62-139">In the pop-up dialog box, select **Add** and your tab is displayed with two options.</span></span>

1. <span data-ttu-id="32b62-140">タブのオプションから、[灰色の選択] または [ **赤の選択]** **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="32b62-140">From the options in the tab, choose either **Select Gray** or **Select Red**.</span></span> <span data-ttu-id="32b62-141">タブは、選択した色に従って表示されます。</span><span class="sxs-lookup"><span data-stu-id="32b62-141">The tab is displayed according to the color you selected.</span></span>
 
    ![[個人用] タブの ASPNETMVC がアップロードされました](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a><span data-ttu-id="32b62-143">個人用タブを表示する</span><span class="sxs-lookup"><span data-stu-id="32b62-143">View your personal tab</span></span>

1. <span data-ttu-id="32b62-144">アプリの左上にあるナビゲーション バーで、Teamsを選択 &#x25CF;&#x25CF;&#x25CF;。</span><span class="sxs-lookup"><span data-stu-id="32b62-144">In the navigation bar located at the far left of the Teams app, select the ellipses &#x25CF;&#x25CF;&#x25CF;.</span></span> <span data-ttu-id="32b62-145">個人用アプリの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="32b62-145">A list of personal apps is shown.</span></span>

1. <span data-ttu-id="32b62-146">リストからタブを選択して表示します。</span><span class="sxs-lookup"><span data-stu-id="32b62-146">Select your tab from the list to view it.</span></span>
