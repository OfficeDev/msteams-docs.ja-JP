### <a name="_layoutcshtml"></a><span data-ttu-id="cd4c2-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="cd4c2-101">_Layout.cshtml</span></span>

<span data-ttu-id="cd4c2-102">タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="cd4c2-103">次に、タブとクライアントがTeams方法を示します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-103">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="cd4c2-104">[共有] **フォルダーに移動** し **、_Layout.cshtml** を開き、次の項目をタグに追加 `<head>` します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-104">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> <span data-ttu-id="cd4c2-105">このページの URL は最新バージョンを表していない可能性がありますので、コピーして貼 `<script src="...">` り付けは行ないます。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-105">Do not copy and paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="cd4c2-106">SDK の最新バージョンを取得するには、常に[JavaScript API Microsoft Teams移動します](https://www.npmjs.com/package/@microsoft/teams-js)。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-106">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="cd4c2-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="cd4c2-107">Tab.cshtml</span></span>

<span data-ttu-id="cd4c2-108">**埋め込みスクリプトを更新するには**</span><span class="sxs-lookup"><span data-stu-id="cd4c2-108">**To update the embedded script**</span></span>

1. <span data-ttu-id="cd4c2-109">このVisual Studio **Tab.cshtml を** 開き、埋め込みファイルを更新します `<script>` 。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-109">In Visual Studio, open **Tab.cshtml** to update the embedded `<script>`.</span></span>

1. <span data-ttu-id="cd4c2-110">スクリプトの上部で、 を呼び出します `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-110">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="cd4c2-111">タブへの HTTPS ngrok URL を使用して、各関数の値 `websiteUrl` `contentUrl` と値を更新します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-111">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="cd4c2-112">**y8rCgT2b を ngrok** URL に置き換えたコードは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-112">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

    ```javascript
        microsoftTeams.initialize();
    
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. <span data-ttu-id="cd4c2-113">更新された **Tab.cshtml を保存してください**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-113">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="cd4c2-114">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="cd4c2-114">Build and run your application</span></span>

<span data-ttu-id="cd4c2-115">このVisual Studio F5 キー **を押するか、[** デバッグ] メニューから [**デバッグ** の開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-115">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="cd4c2-116">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して **、ngrok** が正常に実行され、正常に動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-116">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="cd4c2-117">アプリケーションをアプリケーションと ngrok Visual Studioする必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-117">You need to have both your application in Visual Studio and ngrok running.</span></span> <span data-ttu-id="cd4c2-118">アプリケーションの実行を停止する必要がある場合Visual Studio ngrok を実行 **し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-118">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="cd4c2-119">引き続きリッスンし、アプリケーションの要求がサーバーで再起動されると、アプリケーションの要求のルーティングVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-119">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="cd4c2-120">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-120">If you have to restart the ngrok service, it will return a new URL and you will have to update your application with the new URL.</span></span>

## <a name="upload-your-tab"></a><span data-ttu-id="cd4c2-121">アップロードを表示する</span><span class="sxs-lookup"><span data-stu-id="cd4c2-121">Upload your tab</span></span>

>[!Note]
> <span data-ttu-id="cd4c2-122">App Studio を使用すると、ファイル上のmanifest.js **を編集** し、完成したパッケージをファイルにアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-122">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="cd4c2-123">必要に応じて、ファイルmanifest.js **手動** で編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-123">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="cd4c2-124">その場合は、必ずソリューションを再度ビルドして、アップロードする **ファイルtab.zip作成** してください。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-124">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="cd4c2-125">**タブをアップロードするには**</span><span class="sxs-lookup"><span data-stu-id="cd4c2-125">**To upload your tab**</span></span>

1. <span data-ttu-id="cd4c2-126">[次へ] にMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-126">Go to Microsoft Teams.</span></span> <span data-ttu-id="cd4c2-127">Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-127">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="cd4c2-128">[App **Studio] に移動し** 、[マニフェスト エディター **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-128">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="cd4c2-129">[ **マニフェスト エディターで既存のアプリ** をインポートする] を選択して、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-129">Select **Import an existing app** in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="cd4c2-130">アプリ パッケージの名前は次 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="cd4c2-130">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="cd4c2-131">この機能は、次の場所から利用できます。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-131">It is available here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="cd4c2-132">アップロードtab.zipApp  Studio にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-132">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="cd4c2-133">マニフェスト エディターを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="cd4c2-133">Update your app package with Manifest editor</span></span>

<span data-ttu-id="cd4c2-134">アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージの構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-134">After you have uploaded your app package into App Studio, you must finish configuring it.</span></span>

<span data-ttu-id="cd4c2-135">マニフェスト エディターのウェルカム ページの右側のパネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-135">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="cd4c2-136">マニフェスト エディターの左側にある手順の一覧と、右側には、これらの各手順の値が必要なプロパティの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-136">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="cd4c2-137">この情報の多くが、manifest.jsによって提供されますが、更新する必要があるフィールドは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-137">Much of the information has been provided by your **manifest.json** but there are a few fields that you must update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="cd4c2-138">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="cd4c2-138">Details: App details</span></span>

<span data-ttu-id="cd4c2-139">[アプリ **の詳細] セクションで、次の内容を実行** します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-139">In the **App details** section:</span></span>

1. <span data-ttu-id="cd4c2-140">**[Id]** で、[**生成] を** 選択して、プレースホルダー ID をタブに必要な GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-140">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="cd4c2-141">[**開発者情報] で\*\*\*\*、ngrok** HTTPS URL を使用して Web **サイトを** 更新します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-141">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="cd4c2-142">[**アプリの URL] で**、[プライバシーに関する **声明] と**[使用条件] を更新して、>。 `https://<yourngrokurl>/privacy`  `https://<yourngrokurl>/tou`</span><span class="sxs-lookup"><span data-stu-id="cd4c2-142">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="cd4c2-143">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="cd4c2-143">Capabilities: Tabs</span></span>

<span data-ttu-id="cd4c2-144">[タブ **] セクションで、次の設定を** 行います。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-144">In the **Tabs** section:</span></span>

1. <span data-ttu-id="cd4c2-145">[チーム **] タブで、[** 追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-145">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="cd4c2-146">[チーム **] タブの** ポップアップ ウィンドウで、構成 **URL をに更新** します `https://<yourngrokurl>/tab` 。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-146">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="cd4c2-147">[構成を **更新できますか] 、[\*\*\*\*チーム]**、および [グループ **チャット]** チェック ボックスがオンになっていることを確認し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-147">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="cd4c2-148">完了: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="cd4c2-148">Finish: Domains and permissions</span></span>

<span data-ttu-id="cd4c2-149">[ドメイン **とアクセス許可**] セクションで、タブのドメインには、HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-149">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="cd4c2-150">完了: テストと配布</span><span class="sxs-lookup"><span data-stu-id="cd4c2-150">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="cd4c2-151">右側の [説明] **で**、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-151">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="cd4c2-152">&#9888; "**'validDomains' 配列にはトンネリング サイトを含めできません。..**</span><span class="sxs-lookup"><span data-stu-id="cd4c2-152">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="cd4c2-153">この警告は、タブのテスト中に無視できます。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-153">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="cd4c2-154">[テストと **配布] セクションで、[** インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-154">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="cd4c2-155">ポップアップ ダイアログ ボックスで、[チームに追加] を選択するか、ドロップダウンから [チャットに追加 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-155">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="cd4c2-156">タブを表示するチームまたはチャットを選択し、[タブの設定 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-156">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="cd4c2-157">次のポップアップ ダイアログ ボックスで、[灰色の選択]または [赤の選択] を選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-157">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="cd4c2-158">タブを表示するには、タブをインストールしたチームに移動し、タブ バーから選択します。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-158">To view your tab, go to the team where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="cd4c2-159">構成時に選択したページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="cd4c2-159">The page that you chose during configuration is displayed.</span></span>

    ![チャネル タブ ASPNETMVC アップロード](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

