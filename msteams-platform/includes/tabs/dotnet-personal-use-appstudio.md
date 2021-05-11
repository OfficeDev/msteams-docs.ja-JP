## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="8ae4e-101">アップロードを App Studio でTeamsに移動する</span><span class="sxs-lookup"><span data-stu-id="8ae4e-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="8ae4e-102">App Studio を使用して、ファイルmanifest.js **編集し**、完成したパッケージをアップロードしてファイルにTeams。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="8ae4e-103">必要に応じて、manifest.js **手動** で編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="8ae4e-104">その場合は、必ずソリューションを再度ビルドして、アップロードする **ファイルTab.zip作成** してください。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="8ae4e-105">クライアントを開Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="8ae4e-106">Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="8ae4e-107">App studio を開き、[マニフェスト エディター **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="8ae4e-108">マニフェスト エディター **で [既存のアプリの** インポート] タイルを選択して、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="8ae4e-109">アプリ パッケージの名前は次 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="8ae4e-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="8ae4e-110">この情報は、次の場所に表示されます。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- <span data-ttu-id="8ae4e-111">アップロードTab.zipApp  Studio にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="8ae4e-112">マニフェスト エディターを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="8ae4e-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="8ae4e-113">アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージの構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="8ae4e-114">マニフェスト エディターのウェルカム ページの右側のパネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="8ae4e-115">マニフェスト エディターの左側にある手順の一覧と、右側には、これらの各手順の値を持つ必要があるプロパティの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="8ae4e-116">この情報の多くが、manifest.jsによって提供されているが、更新する必要があるフィールドがいくつかある。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="8ae4e-117">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="8ae4e-117">Details: App details</span></span>

<span data-ttu-id="8ae4e-118">[アプリ *の詳細] セクションで、次の内容を実行* します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-118">In the *App details* section:</span></span>

- <span data-ttu-id="8ae4e-119">*[Id] で*[**生成]** を選択して、アプリの新しいアプリ ID を生成します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-119">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="8ae4e-120">[*開発者情報] で\*\*\*、ngrok HTTPS*\* URL を使用して Web サイトの URL *を* 更新します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-120">Under *Developer information* update the **Website URL** with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="8ae4e-121">[*アプリの URL] で*、[プライバシーに関する **声明] と**[使用条件] を更新 `https://<yourngrokurl>/privacy` して `https://<yourngrokurl>/tou` 、>。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-121">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="8ae4e-122">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="8ae4e-122">Capabilities: Tabs</span></span>

<span data-ttu-id="8ae4e-123">[タブ *] セクションで、次の設定を* 行います。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="8ae4e-124">[個人用 *タブの追加] で、[追加* ] ***を選択します***。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-124">Under *Add a personal tab* select ***Add***.</span></span> <span data-ttu-id="8ae4e-125">ポップアップ ダイアログ ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="8ae4e-126">[名前] *フィールドに入力* します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-126">Complete the *Name* field.</span></span>

- <span data-ttu-id="8ae4e-127">[エンティティ *ID] フィールドに入力* します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-127">Complete the *Entity Id* field.</span></span>

- <span data-ttu-id="8ae4e-128">[コンテンツ *URL] フィールドを* に更新します `https://<yourngrokurl>/personalTab` 。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-128">Update the *Content URL* field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="8ae4e-129">[Web サイト *の URL] フィールドは* 空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-129">Leave the *Website URL* field blank.</span></span>

- <span data-ttu-id="8ae4e-130">***[保存]*** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-130">Select ***Save***.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="8ae4e-131">完了: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="8ae4e-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="8ae4e-132">[ドメイン *とアクセス許可*] セクションの[タブのドメイン] フィールドには、HTTPS プレフィックスを使用せずに ngrok URL を含む必要があります `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-132">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="8ae4e-133">完了: テストと配布</span><span class="sxs-lookup"><span data-stu-id="8ae4e-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="8ae4e-134">右側の **[説明** ] フィールドに、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="8ae4e-135">&#9888; "**'validDomains' 配列にはトンネリング サイトを含めできません。..**</span><span class="sxs-lookup"><span data-stu-id="8ae4e-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="8ae4e-136">この警告は、タブのテスト中に無視できます。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="8ae4e-137">[テストと *配布] セクションで、次の設定を* 行います。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-137">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="8ae4e-138">[**インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-138">Select **Install**.</span></span>

- <span data-ttu-id="8ae4e-139">ポップアップ ウィンドウで、[Add for *you]* が [はい] に設定され、[チームまたはチャットに追加] が [いいえ] に設定されている必要 *があります*。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-139">In the pop-up window make sure that *Add for you* is set to *Yes* and *Add to a team or chat* is set to *No*.</span></span>

- <span data-ttu-id="8ae4e-140">[**インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-140">Select **Install**.</span></span>

- <span data-ttu-id="8ae4e-141">次のポップアップ ウィンドウで、[開く] **を選択** すると、タブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="8ae4e-142">個人用タブを表示する</span><span class="sxs-lookup"><span data-stu-id="8ae4e-142">View your personal tab</span></span>

- <span data-ttu-id="8ae4e-143">アプリの左上にあるナビゲーション バーで、Teamsを選択 `...` します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="8ae4e-144">個人用アプリの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="8ae4e-145">表示するリストからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="8ae4e-145">Select your tab from the list to view.</span></span>
