### <a name="_layoutcshtml"></a><span data-ttu-id="7e492-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="7e492-101">_Layout.cshtml</span></span>

<span data-ttu-id="7e492-102">タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e492-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="7e492-103">次に、タブとクライアントがTeams方法を示します。</span><span class="sxs-lookup"><span data-stu-id="7e492-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="7e492-104">[共有] **フォルダーに** 移動し **、_Layout.cshtml** を開き、次の項目をタグに追加 `<head>` します。</span><span class="sxs-lookup"><span data-stu-id="7e492-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
><span data-ttu-id="7e492-105">URL が最新バージョンを表していない可能性がある場合は、このページの URL をコピー/ `<script src="...">` 貼り付けは行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e492-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="7e492-106">SDK の最新バージョンを取得するには、常に JavaScript API のMicrosoft Teams[に移動します](https://www.npmjs.com/package/@microsoft/teams-js)。</span><span class="sxs-lookup"><span data-stu-id="7e492-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="7e492-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="7e492-107">Tab.cshtml</span></span>

<span data-ttu-id="7e492-108">**Tab.cshtml を開** き、埋め込みファイルを次のように `<script>` 更新します。</span><span class="sxs-lookup"><span data-stu-id="7e492-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="7e492-109">スクリプトの上部で、 を呼び出します `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="7e492-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="7e492-110">タブへの HTTPS ngrok URL を使用して、各関数の値 `websiteUrl` `contentUrl` と値を更新します。</span><span class="sxs-lookup"><span data-stu-id="7e492-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="7e492-111">**y8rCgT2b を ngrok** URL に置き換えたコードは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7e492-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="7e492-112">更新された **Tab.cshtml を保存してください**。</span><span class="sxs-lookup"><span data-stu-id="7e492-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="7e492-113">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="7e492-113">Build and run your application</span></span>

- <span data-ttu-id="7e492-114">[Visual Studio **F5 キーを押** するか、[デバッグ] メニューから [**デバッグ** の開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="7e492-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="7e492-115">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して **、ngrok** が正常に実行され、正常に動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7e492-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="7e492-116">このクイック スタートを完了するには、アプリケーションVisual Studio ngrok の両方を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e492-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="7e492-117">アプリケーションの実行を停止する必要がある場合Visual Studio ngrok を実行 **し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="7e492-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="7e492-118">引き続きリッスンし、アプリケーションの要求がサーバーで再起動されると、アプリケーションの要求のルーティングVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="7e492-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="7e492-119">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e492-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="7e492-120">アップロードを App Studio でTeamsに移動する</span><span class="sxs-lookup"><span data-stu-id="7e492-120">Upload your tab to Teams with App Studio</span></span>

>[!Note]
> <span data-ttu-id="7e492-121">App Studio を使用して、ファイルmanifest.js **編集し**、完成したパッケージをアップロードしてファイルにTeams。</span><span class="sxs-lookup"><span data-stu-id="7e492-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="7e492-122">必要に応じて、ファイルmanifest.js **手動** で編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="7e492-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="7e492-123">その場合は、必ずソリューションを再度ビルドして、アップロードする **ファイルtab.zip作成** してください。</span><span class="sxs-lookup"><span data-stu-id="7e492-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="7e492-124">クライアントを開Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="7e492-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="7e492-125">Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="7e492-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="7e492-126">App studio を開き、[マニフェスト エディター **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="7e492-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="7e492-127">マニフェスト エディター **で [既存のアプリの** インポート] タイルを選択して、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。</span><span class="sxs-lookup"><span data-stu-id="7e492-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="7e492-128">アプリ パッケージの名前は次 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="7e492-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="7e492-129">この情報は、次の場所に表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e492-129">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="7e492-130">アップロードtab.zipApp  Studio にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="7e492-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="7e492-131">マニフェスト エディターを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="7e492-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="7e492-132">アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージの構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e492-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="7e492-133">マニフェスト エディターのウェルカム ページの右側のパネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="7e492-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="7e492-134">マニフェスト エディターの左側にある手順の一覧と、右側には、これらの各手順の値を持つ必要があるプロパティの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="7e492-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="7e492-135">この情報の多くが、manifest.jsによって提供されているが、更新する必要があるフィールドがいくつかある。</span><span class="sxs-lookup"><span data-stu-id="7e492-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="7e492-136">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="7e492-136">Details: App details</span></span>

- <span data-ttu-id="7e492-137">*[Id]* で [\***Generate** _] を選択して、プレースホルダー ID をタブに必要な GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7e492-137">Under *Identification* select \***Generate** _ to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="7e492-138">[_Developer情報\* は **、ngrok HTTPS** URL を使用して [Web サイトの URL] *フィールドを* 更新します。</span><span class="sxs-lookup"><span data-stu-id="7e492-138">Under _Developer information\* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="7e492-139">[*アプリ URL] で\*\*\*、ngrok*\* HTTPS URL を使用して [プライバシーに関する声明] および [使用 **条件]** URL フィールド *を* 更新します。</span><span class="sxs-lookup"><span data-stu-id="7e492-139">Under *App URLs* update the **Privacy statement** and **Terms of use** URL fields with your *ngrok* HTTPS URL.</span></span> <span data-ttu-id="7e492-140">URL の末尾 *に /privacy* パスと */tou* パスを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e492-140">Remember to include the */privacy* and */tou* paths at the end of the URLs.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="7e492-141">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="7e492-141">Capabilities: Tabs</span></span>

<span data-ttu-id="7e492-142">[タブ *] セクションで、次の設定を* 行います。</span><span class="sxs-lookup"><span data-stu-id="7e492-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="7e492-143">[チーム *タブ] で[* 追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="7e492-143">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="7e492-144">[チーム] タブのポップアップ ウィンドウで、構成 *URL をに更新* します `https://<yourngrokurl>/tab` 。</span><span class="sxs-lookup"><span data-stu-id="7e492-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="7e492-145">最後に、構成を更新 *できるか確認してください。[チーム*] と *[グループ チャット]* ボックスがオンで、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="7e492-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="7e492-146">完了: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="7e492-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="7e492-147">[ドメイン *とアクセス許可*] セクションの[タブのドメイン] フィールドには、HTTPS プレフィックスを使用せずに ngrok URL を含む必要があります `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="7e492-147">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="test-and-distribute-test-and-distribute"></a><span data-ttu-id="7e492-148">テストと配布: テストと配布</span><span class="sxs-lookup"><span data-stu-id="7e492-148">Test and distribute: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="7e492-149">右側の **[説明** ] フィールドに、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e492-149">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="7e492-150">&#9888; "**'validDomains' 配列にはトンネリング サイトを含めできません。..**</span><span class="sxs-lookup"><span data-stu-id="7e492-150">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="7e492-151">この警告は、タブのテスト中に無視できます。</span><span class="sxs-lookup"><span data-stu-id="7e492-151">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="7e492-152">[テストと *配布] セクションで、次の設定を* 行います。</span><span class="sxs-lookup"><span data-stu-id="7e492-152">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="7e492-153">[**インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7e492-153">Select **Install**.</span></span>

- <span data-ttu-id="7e492-154">ポップアップ ウィンドウの [チームまたはチャットに追加] フィールドにチームを入力し、[インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="7e492-154">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="7e492-155">次のポップアップ ウィンドウで、タブを表示するチーム チャネルを選択し、[セットアップ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="7e492-155">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="7e492-156">最後のポップアップ ウィンドウで、タブ ページの値 (赤または灰色のアイコン) を選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="7e492-156">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="7e492-157">タブを表示するには、そのタブをインストールしたチームに移動し、タブ バーから選択します。</span><span class="sxs-lookup"><span data-stu-id="7e492-157">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="7e492-158">構成時に選択したページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e492-158">The page that you chose during configuration should be displayed.</span></span>
