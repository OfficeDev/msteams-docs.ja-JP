---
title: Microsoft Teams Toolkit と Visual Studio コードを使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio Code 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio code toolkit
ms.date: 06/30/2020
ms.openlocfilehash: 96293a2166e56495a8f775cb0142f721605cfdae
ms.sourcegitcommit: 3e94edba28e9e1252b6a6ba35d4df32710dfc5d4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "46531260"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="ad2f7-104">Microsoft Teams Toolkit と Visual Studio コードを使用してアプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-104">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="ad2f7-105">Microsoft Teams Toolkit を使用すると、カスタム Teams アプリを Visual Studio Code 環境内で直接作成することができます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="ad2f7-106">このツールキットは、このプロセスを順を追って説明しており、Teams アプリを構築、デバッグ、および起動するために必要なすべての情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="ad2f7-107">Teams ツールキットをインストールする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="ad2f7-108">Microsoft Teams Toolkit for Visual studio code は、visual [Studio Marketplace](https://aka.ms/teams-toolkit)からダウンロードするか、Visual studio code 内の拡張機能として直接ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="ad2f7-109">インストール後に、Visual Studio Code アクティビティバーに Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="ad2f7-110">表示されていない場合は、アクティビティバー内を右クリックし、[ **Microsoft Teams** ] を選択して、簡単にアクセスできるようにツールキットを固定します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="ad2f7-111">ツールキットの使用</span><span class="sxs-lookup"><span data-stu-id="ad2f7-111">Using the toolkit</span></span>

- [<span data-ttu-id="ad2f7-112">新しいプロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="ad2f7-113">既存のプロジェクトをインポートする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="ad2f7-114">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="ad2f7-115">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="ad2f7-116">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-116">Run your app in Teams</span></span>](#run-your-app-in-teams)
- [<span data-ttu-id="ad2f7-117">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-117">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="ad2f7-118">アプリを発行する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-118">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="ad2f7-119">新しい Teams プロジェクトをセットアップする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-119">Set up a new Teams project</span></span>

1. <span data-ttu-id="ad2f7-120">ローカル環境でプロジェクトのワークスペース/フォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-120">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="ad2f7-121">Visual Studio Code で、Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-121">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="ad2f7-123">ウィンドウの左側にあるアクティビティバーから。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-123">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="ad2f7-124">[コマンド] メニューから [ **Microsoft Teams Toolkit** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-124">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="ad2f7-125">[コマンド] メニューから [**新しい Teams アプリの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-125">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="ad2f7-126">メッセージが表示されたら、ワークスペースの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-126">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="ad2f7-127">これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-127">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="ad2f7-128">**Enter**キーを押すと、[**機能の追加**] 画面が表示され、新しいアプリのプロパティを構成します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-128">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="ad2f7-129">[**完了**] ボタンを選択して、構成プロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-129">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="ad2f7-130">既存の Teams アプリプロジェクトをインポートする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-130">Import an existing Teams app project</span></span>

1. <span data-ttu-id="ad2f7-131">Visual Studio Code で、Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-131">In Visual Studio Code, select the Teams icon</span></span> ![Teams アイコン](../assets/icons/favicon-16x16.png) <span data-ttu-id="ad2f7-133">ウィンドウの左側にあるアクティビティバーから。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-133">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="ad2f7-134">[コマンド] メニューから [**アプリパッケージのインポート**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-134">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="ad2f7-135">既存の[Teams アプリパッケージ](../concepts/build-and-test/apps-package.md)の zip ファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-135">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="ad2f7-136">**[発行パッケージの選択**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-136">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="ad2f7-137">これで、ツールキットの [構成] タブにアプリの詳細が設定されます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-137">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="ad2f7-138">Visual studio code で、[**ファイル**] [  ->  **ワークスペースへのフォルダーの追加**] を選択して、ソースコードディレクトリを visual studio code Workspace に追加します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-138">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="ad2f7-139">アプリを構成する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-139">Configure your app</span></span>

<span data-ttu-id="ad2f7-140">主に、Teams アプリは3つのコンポーネントをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-140">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="ad2f7-141">ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-141">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="ad2f7-142">Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-142">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="ad2f7-143">3つのファイルで構成される Teams[アプリパッケージ](/concepts/build-and-test/apps-package.md):</span><span class="sxs-lookup"><span data-stu-id="ad2f7-143">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="ad2f7-144">manifest.js</span><span class="sxs-lookup"><span data-stu-id="ad2f7-144">The manifest.json</span></span> 
  > - <span data-ttu-id="ad2f7-145">パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="ad2f7-145">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="ad2f7-146">Teams アクティビティバーに表示するための[アウトラインアイコン](../resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-146">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="ad2f7-147">アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-147">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="ad2f7-148">アプリを構成するには、Visual Studio Code の [ **Microsoft Teams Toolkit** ] タブに移動します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-148">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="ad2f7-149">[**アプリパッケージの編集**] を選択して、[**アプリの詳細**] ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-149">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="ad2f7-150">[アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-150">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="ad2f7-151">詳細情報</span><span class="sxs-lookup"><span data-stu-id="ad2f7-151">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="ad2f7-152">アプリをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-152">Package your app</span></span>

<span data-ttu-id="ad2f7-153">**アプリの詳細**ページを変更するか、**マニフェスト**を更新するか、またはアプリの**publish**フォルダー内の**env**ファイルを変更すると、 **Development.zip**ファイルが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-153">Modifying your the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="ad2f7-154">同じフォルダーに[2 つのアイコン](../concepts/build-and-test/apps-package.md#icons)を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-154">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="ad2f7-155">アプリをローカルにインストールして実行する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-155">Install and run your app locally</span></span>

<span data-ttu-id="ad2f7-156">アプリのパッケージ化とテストの詳細な手順については、「プロジェクトホームページのコンテンツを*ビルドして実行*する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-156">Refer to the \**Build and Run* content in your project homepage for detailed instructions for packaging and testing your app.</span></span> <span data-ttu-id="ad2f7-157">一般に、アプリのサーバーをインストールし、実行して、トンネリングソリューションをセットアップして、Teams が localhost から実行されているコンテンツにアクセスできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-157">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

## <a name="add-a-trusted-certificate-for-localhost"></a><span data-ttu-id="ad2f7-158">Localhost の信頼できる証明書を追加する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-158">Add a trusted certificate for localhost</span></span>

<span data-ttu-id="ad2f7-159">Https を使用して localhost でタブベースのアプリをデバッグする場合は、localhost の証明書を catalog に追加する必要があり `Trusted Root Certification Authorities` ます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-159">If you wish to debug your tab based app on localhost using https, you will need to add a certificate for localhost to `Trusted Root Certification Authorities` catalog.</span></span> <span data-ttu-id="ad2f7-160">この手順は、コンピューターごとに1回だけ実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-160">You only need to complete this step once per machine.</span></span></br></br>

<span data-ttu-id="ad2f7-161">**信頼できる証明書を作成してインストールします。**
<details>
  </span><span class="sxs-lookup"><span data-stu-id="ad2f7-161">**Create and install a trusted certificate:**
<details>
  </span></span><summary><span data-ttu-id="ad2f7-162">展開する場所</span><span class="sxs-lookup"><span data-stu-id="ad2f7-162">Expand here</span></span></summary>

* <span data-ttu-id="ad2f7-163">アプリの作成と実行</span><span class="sxs-lookup"><span data-stu-id="ad2f7-163">Build and run your app</span></span>
  * <span data-ttu-id="ad2f7-164">プロジェクト Readme の「**ビルドと実行**」セクションの instuctions に従って、そのサービスが提供されるように https://localhost:3000/tab します。一般的には、次のようにして実行します。 `npm install``npm start`</span><span class="sxs-lookup"><span data-stu-id="ad2f7-164">Follow the instuctions in the **Build and Run** section of your project Readme so that it's being served from https://localhost:3000/tab. Generally, this will involve executing `npm install` then `npm start`</span></span>
  * <span data-ttu-id="ad2f7-165">https://localhost:3000/tabGoogle Chrome または Edge Chromium から移動します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-165">Navigate to https://localhost:3000/tab from Google Chrome or Edge Chromium.</span></span>

* <span data-ttu-id="ad2f7-166">SSL 証明書を取得します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-166">Acquire the SSL certificate:</span></span>
  * <span data-ttu-id="ad2f7-167">[Chrome 開発者ツール] ウィンドウ () を開き `ctrl + shift + i`  /  `cmd + option + i` ます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-167">Open the Chrome Developer Tools window (`ctrl + shift + i` / `cmd + option + i`).</span></span>
  * <span data-ttu-id="ad2f7-168">タブをクリックします。 `Security`</span><span class="sxs-lookup"><span data-stu-id="ad2f7-168">Click on the `Security` tab</span></span>
  * <span data-ttu-id="ad2f7-169">[] `View certificate` をクリックすると、OS X でデスクトップに証明書をドラッグするか、または Windows のタブをクリックして、次のボタンをクリックすることによって、証明書をダウンロードすることができます。 `Details``Copy to File…`</span><span class="sxs-lookup"><span data-stu-id="ad2f7-169">Click on `View certificate` and you’ll have the option to download the certificate — either by dragging it to your desktop in OS X, or by clicking on the `Details` tab in Windows and clicking `Copy to File…`</span></span>
  * <span data-ttu-id="ad2f7-170">ファイルに*任意*の> <名前を付け、書き込み操作を実行するために管理者の同意を必要としないフォルダーに保存します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-170">Name the file <*anything*>.cer and save it to a folder that doesn't require admin consent to perform a write action.</span></span>
  
* <span data-ttu-id="ad2f7-171">**Windows**に証明書をインストールする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-171">Install the certificate on **Windows**</span></span>
  * <span data-ttu-id="ad2f7-172">`DER encoded binary X.509 (.CER)`オプション (最初の1つ) を選択し、保存します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-172">Choose the `DER encoded binary X.509 (.CER)` option (the first one) and save it.</span></span>
  * <span data-ttu-id="ad2f7-173">証明書をダブルクリックしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-173">Double click on the certificate and install it.</span></span>
  * <span data-ttu-id="ad2f7-174">[`Local Machine`</span><span class="sxs-lookup"><span data-stu-id="ad2f7-174">Choose `Local Machine`</span></span>
  * <span data-ttu-id="ad2f7-175">選択`Place all certificates in the following store`</span><span class="sxs-lookup"><span data-stu-id="ad2f7-175">Select `Place all certificates in the following store`</span></span>
  * <span data-ttu-id="ad2f7-176">[`Trusted Root Certification Authorities`</span><span class="sxs-lookup"><span data-stu-id="ad2f7-176">Choose `Trusted Root Certification Authorities`</span></span>
  * <span data-ttu-id="ad2f7-177">インストールを確認する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-177">Confirm your installation</span></span>
  
* <span data-ttu-id="ad2f7-178">**MAC OS X**の証明書をインストールする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-178">Install the certificate **Mac OS X**</span></span>
  * <span data-ttu-id="ad2f7-179">OS X で、キーチェーンアクセスユーティリティを開き、 `System` 左側のメニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-179">On OS X, open the Keychain Access utility and select `System` from the menu on the left.</span></span> <span data-ttu-id="ad2f7-180">ロックアイコンをクリックして、変更を有効にします。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-180">Click the lock icon to enable changes.</span></span>
  * <span data-ttu-id="ad2f7-181">下部にあるプラスボタンをクリックして新しい証明書を追加し、 `localhost.cer` デスクトップにドラッグしたファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-181">Click the plus button near the bottom to add a new certificate, and select the `localhost.cer` file you dragged to the desktop.</span></span> <span data-ttu-id="ad2f7-182">`Always Trust`表示されるダイアログボックスをクリックします。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-182">Click `Always Trust` in the dialog that appears.</span></span>
  * <span data-ttu-id="ad2f7-183">システムキーチェーンに証明書を追加した後、証明書をダブルクリックして、[ `Trust` 証明書の詳細] セクションを展開します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-183">After adding the certificate to the system keychain, double-click the certificate and expand the `Trust` section of the certificate details.</span></span> <span data-ttu-id="ad2f7-184">[ `Always Trust` すべて] オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-184">Select `Always Trust` for every option.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad2f7-185">セキュリティ証明書の警告が表示された場合は、に移動 https://localhost:3000/tab します。サイトが依然として信頼されていない場合は、コンピューターを再起動し、localhost を信頼できるユーザーとして承認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-185">If you receive a security certificate warning, navigate to https://localhost:3000/tab. If the site is still not trusted, reboot your machine and localhost should be accepted as trusted.</span></span>
</details>

## <a name="run-your-app-in-teams"></a><span data-ttu-id="ad2f7-186">Teams でアプリを実行する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-186">Run your app in Teams</span></span>
- <span data-ttu-id="ad2f7-187">前提条件:</span><span class="sxs-lookup"><span data-stu-id="ad2f7-187">Prerequisites:</span></span>
  - [<span data-ttu-id="ad2f7-188">Teams 開発者プレビューモードを有効にする</span><span class="sxs-lookup"><span data-stu-id="ad2f7-188">Enable Teams developer preview mode</span></span>](https://aka.ms/teams-toolkit-enable-devpreview)

1. <span data-ttu-id="ad2f7-189">Visual Studio の [コード] ウィンドウの左側にあるアクティビティバーに移動します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-189">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="ad2f7-190">[実行 **] アイコンを**選択して、[**実行] および [デバッグ**] ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-190">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="ad2f7-191">キーボードショートカットを使用することもでき `Ctrl+Shift+D` ます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-191">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="ad2f7-192">アプリを検証する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-192">Validate your app</span></span>

<span data-ttu-id="ad2f7-193">[**検証**] ページでは、アプリを appsource に提出する前にアプリパッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-193">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="ad2f7-194">マニフェストパッケージをアップロードすると、検証ツールによって、マニフェスト関連のすべてのテストケースに対してアプリがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-194">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="ad2f7-195">失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-195">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="ad2f7-196">自動化が困難なテストの場合、最も一般的な失敗したテストケースの7つの**事前チェックリスト**と、完全な提出チェックリストへのリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-196">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="ad2f7-197">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="ad2f7-197">Publish your app to Teams</span></span>

<span data-ttu-id="ad2f7-198">プロジェクトのホームページでは、アプリをチームにアップロードしたり、アプリを組織内のユーザーに対して会社のカスタムアプリストアに提出したり、アプリをアプリソースに提出してすべての Teams ユーザーに提供したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-198">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="ad2f7-199">IT 管理者は、これらの送信を確認します。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-199">Your IT admin will review these submissions.</span></span> <span data-ttu-id="ad2f7-200">[*発行*] ページに戻り、送信の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認することができます。これは、アプリに更新を送信するか、現在アクティブな提出を取り消すこともできます。</span><span class="sxs-lookup"><span data-stu-id="ad2f7-200">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad2f7-201">次のステップ: 公開アプリの管理とサポート</span><span class="sxs-lookup"><span data-stu-id="ad2f7-201">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
