### <a name="optional-adjust-your-browser-launch-settings"></a><span data-ttu-id="cdd6b-101">(省略可能)ブラウザーの起動設定を調整する</span><span class="sxs-lookup"><span data-stu-id="cdd6b-101">(Optional) Adjust your browser launch settings</span></span>

<span data-ttu-id="cdd6b-102">アプリを開発Teams、別の開発者テナントまたは代替資格情報を使用してアプリを実行するのが一般的です。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-102">When developing a Teams app, it is common to run your app in an alternate developer tenant or with alternate credentials.</span></span>  <span data-ttu-id="cdd6b-103">ブラウザー Microsoft Edge Google Chrome には、ブラウザーの起動設定を調整する機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-103">Both Microsoft Edge and Google Chrome provide facilities to adjust the launch settings for your browser.</span></span>  <span data-ttu-id="cdd6b-104">たとえば、プロジェクトを更新して InPrivate モード (Microsoft Edge) をサポートするには、プロジェクトで `.vscode/launch.json` ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-104">For example, to update the project to support InPrivate mode (Microsoft Edge), open the `.vscode/launch.json` file in your project.</span></span>  <span data-ttu-id="cdd6b-105">適切な起動設定を探し、各ブロックに次のブロックを追加します。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-105">Look for the appropriate launch settings, and add the following block to each one:</span></span>

``` json
"runtimeArgs": [ "--inprivate" ]
```

<span data-ttu-id="cdd6b-106">たとえば、ローカルで実行する起動設定は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-106">For instance, the launch setting for running locally looks like this:</span></span>

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

<span data-ttu-id="cdd6b-107">または、最後の既知のプロファイルを使用するブラウザーを構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-107">Alternatively, you can configure your browser to use the last known profile.</span></span> <span data-ttu-id="cdd6b-108">[新しいプロファイルを作成Microsoft Edge。](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435)</span><span class="sxs-lookup"><span data-stu-id="cdd6b-108">[Create a new profile](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) in Microsoft Edge.</span></span>  <span data-ttu-id="cdd6b-109">次に、新しいリンクに最後の既知のプロファイルを使用する設定を調整します。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-109">Then adjust the settings to use the last known profile for new links:</span></span>

- <span data-ttu-id="cdd6b-110">[Microsoft Edge] を開きます `edge://settings/profiles/multiProfileSettings` 。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-110">In Microsoft Edge, open `edge://settings/profiles/multiProfileSettings`.</span></span>
- <span data-ttu-id="cdd6b-111">[プロファイルの **自動切り替え] をオフにします**。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-111">Turn off **Automatic profile switching**.</span></span>
- <span data-ttu-id="cdd6b-112">[外部リンク **の既定のプロファイル] で、[** 前回使用] **(既定) を選択します**。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-112">For the **Default profile for external links**, select **Last used (default)**.</span></span>

<span data-ttu-id="cdd6b-113">アプリをデバッグする前に、ブラウザーが正しいプロファイルに開かされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="cdd6b-113">Ensure your browser is opened to the correct profile before debugging your app.</span></span>
