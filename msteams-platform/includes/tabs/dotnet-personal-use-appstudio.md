## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="c2b0f-101">アプリ Studio を使用して、タブを Teams にアップロードする</span><span class="sxs-lookup"><span data-stu-id="c2b0f-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="c2b0f-102">アプリ Studio を使用して、 **manifest.xml**ファイルを編集し、完成したパッケージを Teams にアップロードします。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="c2b0f-103">必要に応じて、 **manifest**を手動で編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="c2b0f-104">その場合は、もう一度ソリューションをビルドして、アップロードする**タブ .zip**ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="c2b0f-105">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="c2b0f-106">[Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="c2b0f-107">App studio を開き、[**マニフェストエディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="c2b0f-108">[マニフェストエディター] の [**既存のアプリ**タイルをインポートする] を選択して、タブのアプリパッケージの更新を開始します。ソースコードには、部分的に完成したマニフェストがあります。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="c2b0f-109">アプリパッケージの名前は、**タブ .zip**です。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="c2b0f-110">この場所は、ここから入手できます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- <span data-ttu-id="c2b0f-111">**タブ .zip**を App Studio にアップロードします。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="c2b0f-112">マニフェストエディターを使用してアプリパッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="c2b0f-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="c2b0f-113">アプリパッケージをアプリ Studio にアップロードしたら、構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="c2b0f-114">マニフェストエディターのウェルカムページの右パネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="c2b0f-115">マニフェストエディターの左側と右側に、各手順の値を指定する必要があるプロパティの一覧が表示され、それらの手順の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="c2b0f-116">*マニフェスト*によって提供される情報の多くは、更新する必要があるフィールドがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="c2b0f-117">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="c2b0f-117">Details: App details</span></span>

<span data-ttu-id="c2b0f-118">[*アプリの詳細*] セクションで、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-118">In the *App details* section:</span></span>

- <span data-ttu-id="c2b0f-119">[*識別*] で [**生成**] を選択して、アプリの新しいアプリ Id を生成します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-119">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="c2b0f-120">[*開発者向け情報*] で、 *ngrok* HTTPS url を使用して**web サイトの url**を更新します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-120">Under *Developer information* update the **Website URL** with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="c2b0f-121">*アプリ url*の下で、**プライバシー**に`https://<yourngrokurl>/privacy`関する声明と**使用条件**を> に`https://<yourngrokurl>/tou`更新します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-121">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="c2b0f-122">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="c2b0f-122">Capabilities: Tabs</span></span>

<span data-ttu-id="c2b0f-123">[*タブ*] セクションで、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="c2b0f-124">[*個人用タブの追加] で、* [***追加***] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-124">Under *Add a personal tab* select ***Add***.</span></span> <span data-ttu-id="c2b0f-125">ポップアップダイアログウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="c2b0f-126">[*名前*] フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-126">Complete the *Name* field.</span></span>

- <span data-ttu-id="c2b0f-127">[*エンティティ Id* ] フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-127">Complete the *Entity Id* field.</span></span>

- <span data-ttu-id="c2b0f-128">[*コンテンツの URL* ] フィールドを`https://<yourngrokurl>/personalTab`に更新します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-128">Update the *Content URL* field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="c2b0f-129">[ *Web サイトの URL* ] フィールドは空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-129">Leave the *Website URL* field blank.</span></span>

- <span data-ttu-id="c2b0f-130">[***保存***] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-130">Select ***Save***.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="c2b0f-131">[完了]: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="c2b0f-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="c2b0f-132">[*ドメインと権限*] セクションの [*タブからのドメイン*] フィールドに、NGROK の URL が HTTPS プレフィックスなし`<yourngrokurl>.ngrok.io/`で含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-132">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="c2b0f-133">完了: テストと配布</span><span class="sxs-lookup"><span data-stu-id="c2b0f-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="c2b0f-134">右側の [**説明**] フィールドに、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="c2b0f-135">&#9888; "**validDomains ' 配列は、トンネリングサイトを含むことはできません...**"</span><span class="sxs-lookup"><span data-stu-id="c2b0f-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="c2b0f-136">タブのテスト中は、この警告を無視できます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="c2b0f-137">[*テストと配布*] セクションで、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-137">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="c2b0f-138">**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-138">Select **Install**.</span></span>

- <span data-ttu-id="c2b0f-139">ポップアップウィンドウで、[*ユーザーに追加*する *] が [はい]* に設定されていることを確認し、[*チームに追加*] を [*いいえ*] に設定します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-139">In the pop-up window make sure that *Add for you* is set to *Yes* and *Add to a team or chat* is set to *No*.</span></span>

- <span data-ttu-id="c2b0f-140">**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-140">Select **Install**.</span></span>

- <span data-ttu-id="c2b0f-141">次のポップアップウィンドウで [**開く**] を選択すると、タブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="c2b0f-142">個人用タブの表示</span><span class="sxs-lookup"><span data-stu-id="c2b0f-142">View your personal tab</span></span>

- <span data-ttu-id="c2b0f-143">Teams アプリの左端にあるナビゲーションバーで、 `...`メニューを選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="c2b0f-144">個人用アプリの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="c2b0f-145">表示するリストからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="c2b0f-145">Select your tab from the list to view.</span></span>
