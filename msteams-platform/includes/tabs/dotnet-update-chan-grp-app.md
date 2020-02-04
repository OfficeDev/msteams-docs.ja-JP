### <a name="_layoutcshtml"></a><span data-ttu-id="64d94-101">_Layout cshtml</span><span class="sxs-lookup"><span data-stu-id="64d94-101">_Layout.cshtml</span></span>

<span data-ttu-id="64d94-102">タブを Teams に表示するには、 **Microsoft Teams JavaScript クライアント SDK**を含める必要があります。また`microsoftTeams.initialize()` 、ページが読み込まれた後の呼び出しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="64d94-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="64d94-103">ここでは、タブと Teams クライアントが通信する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="64d94-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="64d94-104">**共有**フォルダーに移動し **_Layout cshtml**を開き、 `<head>`タグに以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="64d94-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
><span data-ttu-id="64d94-105">このページでは、 `<script src="...">`最新のバージョンではない可能性があるので、url をコピー/貼り付けないでください。</span><span class="sxs-lookup"><span data-stu-id="64d94-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="64d94-106">SDK の最新バージョンを入手するには、「 [Microsoft Teams JAVASCRIPT API](https://www.npmjs.com/package/@microsoft/teams-js.com)」に常にアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="64d94-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js.com).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="64d94-107">Tab. cshtml</span><span class="sxs-lookup"><span data-stu-id="64d94-107">Tab.cshtml</span></span>

<span data-ttu-id="64d94-108">**Tab**を開いて、埋め込み`<script>`を次のように更新します。</span><span class="sxs-lookup"><span data-stu-id="64d94-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="64d94-109">スクリプトの先頭に、を呼び出し`microsoftTeams.initialize()`ます。</span><span class="sxs-lookup"><span data-stu-id="64d94-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="64d94-110">HTTPS ngrok `websiteUrl` URL `contentUrl`を使用して、各関数の値と値をタブに更新します。</span><span class="sxs-lookup"><span data-stu-id="64d94-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="64d94-111">コードは、 **y8rCgT2b**で次のようになり、ngrok URL に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="64d94-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="64d94-112">更新した Tab を必ず保存してください **。**</span><span class="sxs-lookup"><span data-stu-id="64d94-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="64d94-113">アプリケーションをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="64d94-113">Build and run your application</span></span>

- <span data-ttu-id="64d94-114">Visual Studio で**F5**キーを押すか、[**デバッグ**] メニューの [**デバッグ開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="64d94-115">ブラウザーを開き、コマンドプロンプトウィンドウで提供された ngrok HTTPS URL を使用してコンテンツページにアクセスすることにより、 **ngrok**が実行されて正常に動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="64d94-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="64d94-116">このクイックスタートを完了するには、Visual Studio と ngrok の両方のアプリケーションが実行されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="64d94-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="64d94-117">Visual Studio でのアプリケーションの実行を停止する必要がある場合は、 **ngrok の実行を継続**します。</span><span class="sxs-lookup"><span data-stu-id="64d94-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="64d94-118">Visual Studio で再起動すると、アプリケーションの要求のルーティングが続行され、再開されます。</span><span class="sxs-lookup"><span data-stu-id="64d94-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="64d94-119">Ngrok サービスを再起動する必要がある場合は、新しい URL を返し、新しい URL を使用してアプリケーションを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="64d94-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="64d94-120">アプリ Studio を使用して、タブを Teams にアップロードする</span><span class="sxs-lookup"><span data-stu-id="64d94-120">Upload your tab to Teams with App Studio</span></span>

>[!Note]
> <span data-ttu-id="64d94-121">アプリ Studio を使用して、 **manifest.xml**ファイルを編集し、完成したパッケージを Teams にアップロードします。</span><span class="sxs-lookup"><span data-stu-id="64d94-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="64d94-122">必要に応じて、**マニフェストの json**ファイルを手動で編集することもできます。</span><span class="sxs-lookup"><span data-stu-id="64d94-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="64d94-123">その場合は、もう一度ソリューションをビルドして、アップロードする**タブ .zip**ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="64d94-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="64d94-124">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="64d94-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="64d94-125">[Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="64d94-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="64d94-126">App studio を開き、[**マニフェストエディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="64d94-127">[マニフェストエディター] の [**既存のアプリ**タイルをインポートする] を選択して、タブのアプリパッケージの更新を開始します。ソースコードには、部分的に完成したマニフェストがあります。</span><span class="sxs-lookup"><span data-stu-id="64d94-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="64d94-128">アプリパッケージの名前は、**タブ .zip**です。</span><span class="sxs-lookup"><span data-stu-id="64d94-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="64d94-129">この場所は、ここから入手できます。</span><span class="sxs-lookup"><span data-stu-id="64d94-129">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="64d94-130">**タブ .zip**を App Studio にアップロードします。</span><span class="sxs-lookup"><span data-stu-id="64d94-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="64d94-131">マニフェストエディターを使用してアプリパッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="64d94-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="64d94-132">アプリパッケージをアプリ Studio にアップロードしたら、構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="64d94-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="64d94-133">マニフェストエディターのウェルカムページの右パネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="64d94-134">マニフェストエディターの左側と右側に、各手順の値を指定する必要があるプロパティの一覧が表示され、それらの手順の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="64d94-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="64d94-135">*マニフェスト*によって提供される情報の多くは、更新する必要があるフィールドがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="64d94-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="64d94-136">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="64d94-136">Details: App details</span></span>

- <span data-ttu-id="64d94-137">[*識別*] で、[***生成***] を選択して、プレースホルダー id をタブの必須の GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="64d94-137">Under *Identification* select ***Generate*** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="64d94-138">[*開発者情報*] の下で、 *ngrok* HTTPS url を使用して**web サイトの url**フィールドを更新します。</span><span class="sxs-lookup"><span data-stu-id="64d94-138">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="64d94-139">[*アプリの url* ] の下にある*ngrok* HTTPS url を使用して、プライバシーに関する**声明**と**Terms of use** url フィールドを更新します。</span><span class="sxs-lookup"><span data-stu-id="64d94-139">Under *App URLs* update the **Privacy statement** and **Terms of use** URL fields with your *ngrok* HTTPS URL.</span></span> <span data-ttu-id="64d94-140">Url の末尾には、「 */privacy* *」および「/」* のパスを必ず含めてください。</span><span class="sxs-lookup"><span data-stu-id="64d94-140">Remember to include the */privacy* and */tou* paths at the end of the URLs.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="64d94-141">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="64d94-141">Capabilities: Tabs</span></span>

<span data-ttu-id="64d94-142">[*タブ*] セクションで、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="64d94-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="64d94-143">[*チーム] タブ*で、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-143">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="64d94-144">[チーム] タブのポップアップウィンドウで、*構成 URL*をに`https://<yourngrokurl>/tab`更新します。</span><span class="sxs-lookup"><span data-stu-id="64d94-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="64d94-145">最後に、が*構成を更新できるかどうかを確認します。チーム*および*グループのチャット*ボックスがチェックされ、[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="64d94-146">[完了]: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="64d94-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="64d94-147">[*ドメインと権限*] セクションの [*タブからのドメイン*] フィールドに、NGROK の URL が HTTPS プレフィックスなし`<yourngrokurl>.ngrok.io/`で含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="64d94-147">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="test-and-distribute-test-and-distribute"></a><span data-ttu-id="64d94-148">テストと配布: テストと配布</span><span class="sxs-lookup"><span data-stu-id="64d94-148">Test and distribute: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="64d94-149">右側の [**説明**] フィールドに、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="64d94-149">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="64d94-150">&#9888; "**validDomains ' 配列は、トンネリングサイトを含むことはできません...**"</span><span class="sxs-lookup"><span data-stu-id="64d94-150">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="64d94-151">タブのテスト中は、この警告を無視できます。</span><span class="sxs-lookup"><span data-stu-id="64d94-151">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="64d94-152">[*テストと配布*] セクションで、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="64d94-152">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="64d94-153">**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-153">Select **Install**.</span></span>

- <span data-ttu-id="64d94-154">ポップアップウィンドウの [*チームまたはチャットに追加する*] フィールドにチームを入力し、[**インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-154">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="64d94-155">次のポップアップウィンドウで、タブを表示するチームチャネルを選択し、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-155">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="64d94-156">最後のポップアップウィンドウで、タブページ (赤または灰色のアイコン) の値を選択し、[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-156">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="64d94-157">タブを表示するには、タブをインストールしたチームに移動し、タブバーからそれを選択します。</span><span class="sxs-lookup"><span data-stu-id="64d94-157">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="64d94-158">構成時に選択したページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="64d94-158">The page that you chose during configuration should be displayed.</span></span>
