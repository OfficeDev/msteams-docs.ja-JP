## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="3656e-101">アプリスタジオでTeamsするタブをアップロード</span><span class="sxs-lookup"><span data-stu-id="3656e-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="3656e-102">App Studio を使用して **、ファイルのmanifest.js** を編集し、完成したパッケージをTeamsにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="3656e-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="3656e-103">必要に応じて **、manifest.js手動で** 編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="3656e-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="3656e-104">その場合は、アップロードする **Tab.zip** ファイルを作成するソリューションをもう一度ビルドしてください。</span><span class="sxs-lookup"><span data-stu-id="3656e-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="3656e-105">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="3656e-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="3656e-106">Web ベースの [バージョン](https://teams.microsoft.com) を使用する場合は、ブラウザーの [開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを検査できます。</span><span class="sxs-lookup"><span data-stu-id="3656e-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="3656e-107">アプリスタジオを開き、[ **マニフェストエディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="3656e-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="3656e-108">[マニフェスト エディター **で既存のアプリをインポート** する] タイルを選択して、タブのアプリ パッケージの更新を開始します。ソース コードには、独自の部分的に完全なマニフェストが付属しています。</span><span class="sxs-lookup"><span data-stu-id="3656e-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="3656e-109">アプリ パッケージの名前は **tab.zip** です。</span><span class="sxs-lookup"><span data-stu-id="3656e-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="3656e-110">それはここに見つかるはずです:</span><span class="sxs-lookup"><span data-stu-id="3656e-110">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- <span data-ttu-id="3656e-111">アップロードアプリスタジオに **Tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="3656e-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="3656e-112">マニフェスト エディターを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="3656e-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="3656e-113">アプリ パッケージをアプリ スタジオにアップロードしたら、その構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3656e-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="3656e-114">マニフェスト エディターのウェルカム ページの右側のパネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="3656e-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="3656e-115">マニフェスト エディターの左側に手順の一覧があり、右側には、これらの各ステップの値を持つ必要があるプロパティの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="3656e-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="3656e-116">情報の多くは *manifest.js* によって提供されていますが、更新が必要なフィールドがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="3656e-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="3656e-117">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="3656e-117">Details: App details</span></span>

<span data-ttu-id="3656e-118">[ **アプリの詳細]** セクションで、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="3656e-118">In the **App details** section:</span></span>

- <span data-ttu-id="3656e-119">**[ID]** で [**生成]** を選択して、アプリの新しいアプリ ID を生成します。</span><span class="sxs-lookup"><span data-stu-id="3656e-119">Under **Identification** select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="3656e-120">[ **開発者情報** ] で **、web サイトの URL** を **ngrok** HTTPS URL で更新します。</span><span class="sxs-lookup"><span data-stu-id="3656e-120">Under **Developer information** update the **Website URL** with your **ngrok** HTTPS URL.</span></span>

- <span data-ttu-id="3656e-121">[**アプリの URL] で**、**プライバシーに関する声明** `https://<yourngrokurl>/privacy` と利用規約を更新して `https://<yourngrokurl>/tou`>します。</span><span class="sxs-lookup"><span data-stu-id="3656e-121">Under **App URLs** update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="3656e-122">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="3656e-122">Capabilities: Tabs</span></span>

<span data-ttu-id="3656e-123">タブセクションで次 *の手順を実行* します。</span><span class="sxs-lookup"><span data-stu-id="3656e-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="3656e-124">[ **個人用タブの追加] で** 、[ **追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3656e-124">Under **Add a personal tab** select **Add**.</span></span> <span data-ttu-id="3656e-125">ポップアップダイアログウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3656e-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="3656e-126">[ **名前]** フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="3656e-126">Complete the **Name** field.</span></span>

- <span data-ttu-id="3656e-127">[ **エンティティ ID] フィールドに入力** します。</span><span class="sxs-lookup"><span data-stu-id="3656e-127">Complete the **Entity Id** field.</span></span>

- <span data-ttu-id="3656e-128">**[コンテンツ URL]** フィールドを に更新 `https://<yourngrokurl>/personalTab` します。</span><span class="sxs-lookup"><span data-stu-id="3656e-128">Update the **Content URL** field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="3656e-129">**[Web サイトの URL]** フィールドは空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="3656e-129">Leave the **Website URL** field blank.</span></span>

- <span data-ttu-id="3656e-130">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3656e-130">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="3656e-131">完了: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="3656e-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="3656e-132">[ **ドメインとアクセス許可** ] セクションの **[タブのドメイン** ] フィールドに、HTTPS プレフィックスを付けずに ngrok URL を含める必要があります `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="3656e-132">In the **Domains and permissions** section, the **Domains from your tabs** field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="3656e-133">完了: テストと配布</span><span class="sxs-lookup"><span data-stu-id="3656e-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="3656e-134">右側の [ **説明]** フィールドに、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3656e-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="3656e-135">&#9888;**"'validDomains' 配列にトンネリング サイトを含めることはできません**。</span><span class="sxs-lookup"><span data-stu-id="3656e-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="3656e-136">この警告は、タブのテスト中に無視できます。</span><span class="sxs-lookup"><span data-stu-id="3656e-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="3656e-137">[ **テストと配布** ] セクションで、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="3656e-137">In the **Test and distribute** section:</span></span>

- <span data-ttu-id="3656e-138">**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3656e-138">Select **Install**.</span></span>

- <span data-ttu-id="3656e-139">ポップアップ ウィンドウで、[ **追加** ] が **[はい]** に設定され、[ **チームまたはチャットに追加** ] が **[いいえ**] に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="3656e-139">In the pop-up window make sure that **Add for you** is set to **Yes** and **Add to a team or chat** is set to **No**.</span></span>

- <span data-ttu-id="3656e-140">**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="3656e-140">Select **Install**.</span></span>

- <span data-ttu-id="3656e-141">次のポップアップ ウィンドウで [ **開く** ] を選択すると、タブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3656e-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="3656e-142">個人用タブを表示する</span><span class="sxs-lookup"><span data-stu-id="3656e-142">View your personal tab</span></span>

- <span data-ttu-id="3656e-143">Teamsアプリの左端にあるナビゲーションバーで、メニューを選択 `...` します。</span><span class="sxs-lookup"><span data-stu-id="3656e-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="3656e-144">個人用アプリの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3656e-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="3656e-145">表示するタブを一覧から選択します。</span><span class="sxs-lookup"><span data-stu-id="3656e-145">Select your tab from the list to view.</span></span>
