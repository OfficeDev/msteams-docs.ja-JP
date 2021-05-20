---
title: Moodle LMS のインストール
description: Microsoft Teamsの Moodle 統合アプリをインストールして構成する方法
keywords: TeamsMoodleアプリ統合プラグイン
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: d7fddad80ca08fd4ca8dee352cdcbc46e8e97dcd
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566720"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="74b55-104">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="74b55-104">Install Moodle LMS</span></span>

<span data-ttu-id="74b55-105">この記事では、Moodle LMS のインストール方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="74b55-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="74b55-106">IT 管理者が Moodle とTeams統合を簡単にセットアップできるように、オープンソースMicrosoft 365 Moodle プラグインは次の機能に更新されます。</span><span class="sxs-lookup"><span data-stu-id="74b55-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="74b55-107">moodle サーバーの自動登録を[Azure Active Directory (Azure AD) に](https://azure.microsoft.com/services/active-directory/)自動登録する 。</span><span class="sxs-lookup"><span data-stu-id="74b55-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="74b55-108">1 回のクリックで、ムードル アシスタント ボットを Azure にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="74b55-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="74b55-109">チームの自動プロビジョニングとチーム登録の自動同期をすべての人に対して行うか、Moodleコースを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="74b55-110">各同期チームに Moodle タブと Moodle アシスタントボットの自動インストール。</span><span class="sxs-lookup"><span data-stu-id="74b55-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="74b55-111">この統合が提供する機能の詳細については、「 [Microsoft Teams と Moodle](https://education.microsoft.com/resource/3dffb3a8)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="74b55-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74b55-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="74b55-112">Prerequisites</span></span>

<span data-ttu-id="74b55-113">Moodle をインストールするための前提条件は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="74b55-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="74b55-114">ムード管理者の資格情報。</span><span class="sxs-lookup"><span data-stu-id="74b55-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="74b55-115">Azure AD 管理者の資格情報。</span><span class="sxs-lookup"><span data-stu-id="74b55-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="74b55-116">新しいリソースを作成できる Azure サブスクリプション。</span><span class="sxs-lookup"><span data-stu-id="74b55-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="74b55-117">1. Microsoft 365のMoodleプラグインをインストールする</span><span class="sxs-lookup"><span data-stu-id="74b55-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="74b55-118">Microsoft TeamsのMoodle統合は[、MoodleプラグインセットMicrosoft 365](https://github.com/Microsoft/o365-moodle)オープンソースによって供給されます。</span><span class="sxs-lookup"><span data-stu-id="74b55-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="74b55-119">必要なアプリケーションとプラグイン</span><span class="sxs-lookup"><span data-stu-id="74b55-119">Requisite applications and plugins</span></span>

<span data-ttu-id="74b55-120">Microsoft 365 Moodle プラグインのインストールを続行する前に、以下をインストールしてダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="74b55-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="74b55-121">[Moodle の現在の安定版を](https://download.moodle.org/releases/latest/)インストールすることを確認します。</span><span class="sxs-lookup"><span data-stu-id="74b55-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="74b55-122">Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc)と[Microsoft 365統合](https://moodle.org/plugins/local_o365)プラグインをダウンロードしてローカルコンピュータに保存します。</span><span class="sxs-lookup"><span data-stu-id="74b55-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="74b55-123">Teams統合には、OpenID ConnectとMicrosoft 365統合プラグインのインストールが必要です。</span><span class="sxs-lookup"><span data-stu-id="74b55-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="74b55-124">さらに[、Microsoft 365 Teamsテーマ](https://moodle.org/plugins/theme_boost_o365teams)プラグインを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="74b55-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="74b55-125">Microsoft 365ムードルプラグイン</span><span class="sxs-lookup"><span data-stu-id="74b55-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="74b55-126">管理者として Moodle サーバーにサインインし、左側のナビゲーション パネルにある [設定 ブロック](https://docs.moodle.org/22/en/Settings_block)から [**サイト管理**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="74b55-127">[プラグイン] タブ **を** 選択し、[ **プラグインのインストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="74b55-128">[ZIP **ファイルからプラグインをインストール]** セクションで、[ **ファイルの選択**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="74b55-129">左側 **の** ナビゲーション パネルからファイル オプションアップロード選択し、ダウンロードしたファイルを参照して、[**このファイルアップロード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="74b55-130">左側のナビゲーション パネルから [ **サイト管理]** を選択して、管理ダッシュボードに戻ります。</span><span class="sxs-lookup"><span data-stu-id="74b55-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="74b55-131">**ローカルプラグイン** までスクロールダウンし **、Microsoft 365統合** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="74b55-132">プロセス全体を通してこのページのセットに戻る必要がある場合は、Microsoft 365 Moodle Plugins 設定ページを別のブラウザタブで開いたままにします。</span><span class="sxs-lookup"><span data-stu-id="74b55-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="74b55-133">既存の Moodle サイトがない場合は、Azure レポ [の Moodle に](https://github.com/azure/moodle) 移動し、すぐに Moodle インスタンスをデプロイしてニーズに合わせてカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="74b55-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="74b55-134">2. Microsoft 365 プラグインとAzure Active Directory間の接続を構成する (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="74b55-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="74b55-135">Microsoft 365 プラグインと Azure AD 間の接続を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="74b55-136">前提 条件</span><span class="sxs-lookup"><span data-stu-id="74b55-136">Requisites</span></span>

<span data-ttu-id="74b55-137">PowerShell スクリプトを使用して、アプリケーションとしてアプリケーションとして Moodle を登録します。</span><span class="sxs-lookup"><span data-stu-id="74b55-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="74b55-138">Powershell スクリプトは、次の項目をプロビジョニングします。</span><span class="sxs-lookup"><span data-stu-id="74b55-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="74b55-139">Microsoft 365のテナント用の新しい Azure AD アプリケーションで、Microsoft 365 Moodle プラグインで使用されます。</span><span class="sxs-lookup"><span data-stu-id="74b55-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="74b55-140">Microsoft 365テナント用のアプリは、プロビジョニングされたアプリに必要な応答 URL とアクセス許可を設定し、 `AppID` と を返します `Key` 。</span><span class="sxs-lookup"><span data-stu-id="74b55-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="74b55-141">生成された Microsoft 365 `AppID` `Key` Moodle プラグインのセットアップ ページで、Azure AD を使用して Moodle サーバー サイトを構成します。</span><span class="sxs-lookup"><span data-stu-id="74b55-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="74b55-142">PowerShell スクリプトは最新の構成項目で更新されないため、Moodle [3.8.0.4 および 3.9.1 および 3.8.0.5 および](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) [3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って、構成を手動で完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="74b55-143">Moodle インスタンスを手動で登録する方法の詳細については [、「Moodle インスタンスをアプリケーションとして登録する](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="74b55-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="74b55-144">情報フローのMicrosoft Teamsの [Moodle] タブ</span><span class="sxs-lookup"><span data-stu-id="74b55-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="74b55-145">[Microsoft 365統合プラグイン] ページで、[**設定**] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="74b55-146">**[PowerShell スクリプトのダウンロード**] ボタンを選択し、ZIP フォルダーとしてローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="74b55-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="74b55-147">次のように ZIP ファイルから PowerShell スクリプトを準備します。</span><span class="sxs-lookup"><span data-stu-id="74b55-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="74b55-148">ファイルをダウンロードして解凍 `Moodle-AzureAD-Powershell.zip` します。</span><span class="sxs-lookup"><span data-stu-id="74b55-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="74b55-149">展開したフォルダを開きます。</span><span class="sxs-lookup"><span data-stu-id="74b55-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="74b55-150">ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` **プロパティ ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="74b55-151">[プロパティ] ウィンドウの [ **全般** ] タブで、 `Unblock` ウィンドウの下部にある **[セキュリティ** ] 属性の横にあるチェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="74b55-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="74b55-152">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-152">Select **OK**.</span></span>
    1. <span data-ttu-id="74b55-153">展開したフォルダにディレクトリ パスをコピーします。</span><span class="sxs-lookup"><span data-stu-id="74b55-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="74b55-154">管理者として PowerShell を実行します。</span><span class="sxs-lookup"><span data-stu-id="74b55-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="74b55-155">[開始] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-155">Select Start.</span></span>
    1. <span data-ttu-id="74b55-156">「パワーシェル」と入力します。</span><span class="sxs-lookup"><span data-stu-id="74b55-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="74b55-157">**Windows PowerShell** を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="74b55-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="74b55-158">[ **管理者として実行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="74b55-159">解凍したディレクトリに移動するには `cd .../.../Moodle-AzureAD-Powershell` `.../...` 、ディレクトリへのパスを入力します。</span><span class="sxs-lookup"><span data-stu-id="74b55-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="74b55-160">次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="74b55-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="74b55-161">`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`を入力します。</span><span class="sxs-lookup"><span data-stu-id="74b55-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="74b55-162">`./Moodle-AzureAD-Script.ps1`を入力します。</span><span class="sxs-lookup"><span data-stu-id="74b55-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="74b55-163">ポップアップ ウィンドウでMicrosoft 365管理者アカウントにサインインします。</span><span class="sxs-lookup"><span data-stu-id="74b55-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="74b55-164">Azure AD アプリケーションの名前を入力します(たとえば、Moodle プラグインや Moodle プラグインなど)。</span><span class="sxs-lookup"><span data-stu-id="74b55-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="74b55-165">Moodle サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="74b55-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="74b55-166">スクリプトによって生成された **アプリケーション ID ( `AppID` )** と **アプリケーション キー ( ) `Key` を** コピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="74b55-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="74b55-167">次に、 `AppID` `Key` ムードルプラグインを追加し、Microsoft 365に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="74b55-168">プラグイン管理ページ、サイト管理>プラグイン> Microsoft 365統合に戻ります。</span><span class="sxs-lookup"><span data-stu-id="74b55-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="74b55-169">[ **セットアップ** ] タブで、 `AppID` を追加し `Key` 、以前にコピーした後、[ **変更の保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="74b55-170">ページが更新されると、新しいセクションの **接続方法を選択** するを見ることができます。</span><span class="sxs-lookup"><span data-stu-id="74b55-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="74b55-171">[ **接続方法の選択**] で、[ **既定**] というラベルのチェック ボックスをオンにし、[ **変更を保存]** を再度選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="74b55-172">ページが更新されると、別の新しいセクション **[管理者の同意&追加情報** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="74b55-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="74b55-173">[**管理者同意の提供**] リンクを選択し、Microsoft 365のグローバル管理者資格情報を入力し、[**承諾]** をクリックしてアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="74b55-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="74b55-174">**[Azure AD テナント]** フィールドの横にある [**検出**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="74b55-175">**[OneDrive for Business URL]** の横にある [**検出**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="74b55-176">フィールドが入力されたら、[変更を **保存** ] ボタンをもう一度選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="74b55-177">[ **更新** ] ボタンを選択してインストールを確認し、[ **変更の保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="74b55-178">Moodle サーバーと Azure AD の間でユーザーを同期します。</span><span class="sxs-lookup"><span data-stu-id="74b55-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="74b55-179">次の手順をお試しください。</span><span class="sxs-lookup"><span data-stu-id="74b55-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="74b55-180">環境に応じて、このステージで異なるオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="74b55-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="74b55-181">Moodle サーバーと Azure AD の間でユーザーを同期します。</span><span class="sxs-lookup"><span data-stu-id="74b55-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="74b55-182">環境に応じて、このステージで異なるオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="74b55-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="74b55-183">次の手順をお試しください。</span><span class="sxs-lookup"><span data-stu-id="74b55-183">To get started:</span></span>
    1. <span data-ttu-id="74b55-184">[**同期設定] タブ** に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="74b55-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="74b55-185">[ **ユーザーと Azure AD の同期** ] セクションで、環境に適用するチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="74b55-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="74b55-186">次の項目を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-186">You must select the following:</span></span>  

        <span data-ttu-id="74b55-187">✔ Azure AD のユーザーのムードルでアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="74b55-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="74b55-188">✔ Azure AD のユーザーの Moodle のすべてのアカウントを更新します。</span><span class="sxs-lookup"><span data-stu-id="74b55-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="74b55-189">[ **ユーザーの作成の制限]** セクションでは、Moodle に同期される Azure AD ユーザーを制限するフィルターを設定できます。</span><span class="sxs-lookup"><span data-stu-id="74b55-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="74b55-190">**[ユーザー フィールド マッピング]** セクションでは、Azure AD から Moodle ユーザー プロファイル フィールド マッピングをカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="74b55-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="74b55-191">[Teams **同期**] セクションでは、既存の Moodle コースの一部または全部のチームなどのグループを自動的に作成することを選択できます。</span><span class="sxs-lookup"><span data-stu-id="74b55-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="74b55-192">[cron](https://docs.moodle.org/310/en/Cron)ジョブを検証し、最初の実行に対して手動で実行するには **、[Azure AD とユーザーを同期** する] セクションの **[スケジュールされたタスク管理] ページ** のリンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="74b55-193">[ **スケジュールされたタスク** ] ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="74b55-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="74b55-194">下にスクロールして **、[Azure AD とユーザーを同期** する] ジョブを見つけて、[ **今すぐ実行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="74b55-195">既存のコースに基づいてグループを作成する場合は、ジョブ **でユーザーグループを作成Microsoft 365実行** することもできます。</span><span class="sxs-lookup"><span data-stu-id="74b55-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="74b55-196">Moodle [Cron](https://docs.moodle.org/310/en/Cron) はタスクスケジュールに従って実行されます。</span><span class="sxs-lookup"><span data-stu-id="74b55-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="74b55-197">デフォルトのスケジュールは 1 日 1 回です。</span><span class="sxs-lookup"><span data-stu-id="74b55-197">The default schedule is once a day.</span></span> <span data-ttu-id="74b55-198">ただし、cron は、すべてを同期させるために、より頻繁に実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="74b55-199">プラグイン管理ページの **[サイト管理> プラグイン > Microsoft 365統合**] に戻り **、Teams 設定** ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="74b55-200">Teams 設定ページ **で**、Teamsアプリ統合を有効にする必要な設定を構成します。</span><span class="sxs-lookup"><span data-stu-id="74b55-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="74b55-201">**OpenID Connect** を有効にするには、[**認証の管理**] リンクを選択し、灰色表示の場合は **OpenId Connect** 行の目のアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="74b55-202">フレーム埋め込みを有効にするには **、[HTTP セキュリティ** ] リンクを選択し、[フレームの **埋め込みを許可** する] の横にあるチェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="74b55-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="74b55-203">Moodle API 機能を有効にする Web サービスを有効にするには、[ **高度な機能]** リンクを選択し **、[Web サービスを有効にする** ] の横にあるチェックボックスが選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="74b55-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="74b55-204">Microsoft 365の外部サービスを有効にするには、[**外部サービス**] リンクを選択し、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="74b55-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="74b55-205">✔ **[ムードル Microsoft 365 Web サービス**] 行で **[編集**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="74b55-206">✔ **[有効]** の横にあるチェックボックスをオンにし、[**変更の保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="74b55-207">認証されたユーザー権限を編集して、Web サービストークンの作成を許可します。</span><span class="sxs-lookup"><span data-stu-id="74b55-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="74b55-208">✔ **編集ロール認証済みユーザーリンクを選択します** 。</span><span class="sxs-lookup"><span data-stu-id="74b55-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="74b55-209">✔ 下にスクロールして **[Web サービス トークンを作成する** ]機能を見つけ、[ **許可** ]チェックボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="74b55-210">3. Azure にムードアシスタントボットをデプロイする</span><span class="sxs-lookup"><span data-stu-id="74b55-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="74b55-211">Microsoft Teams用の無料のMoodleアシスタントボットは、教師と学生がMoodleのコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="74b55-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="74b55-212">ボットは、Teams内の学生や教師にMoodle通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="74b55-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="74b55-213">ボットは Microsoft が管理するオープンソース プロジェクトであり[、GitHub](https://github.com/microsoft/Moodle-Teams-Bot)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="74b55-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="74b55-214">リソースを Azure サブスクリプションにデプロイします。</span><span class="sxs-lookup"><span data-stu-id="74b55-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="74b55-215">すべてのリソースは **、free** レベルを使用して構成されました。</span><span class="sxs-lookup"><span data-stu-id="74b55-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="74b55-216">ボットの使用状況によっては、これらのリソースをスケーリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="74b55-217">ボットを使用せずに Moodle タブを使用するには [、4](#4-deploy-your-microsoft-teams-app)に進んでください。</span><span class="sxs-lookup"><span data-stu-id="74b55-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="74b55-218">ムードボット情報フロー</span><span class="sxs-lookup"><span data-stu-id="74b55-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="74b55-219">ボットをインストールするには、Microsoft [ID プラットフォーム](https://identity.microsoft.com/Landing)に登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="74b55-220">これにより、ボットは Microsoft エンドポイントに対して認証を受けられます。</span><span class="sxs-lookup"><span data-stu-id="74b55-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="74b55-221">**ボットを登録するには**</span><span class="sxs-lookup"><span data-stu-id="74b55-221">**To register your bot**</span></span>

1. <span data-ttu-id="74b55-222">プラグイン管理ページに移動し、プラグイン **を** 選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="74b55-223">**[Microsoft 365統合**] で **、[Teams 設定]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="74b55-224">**[Microsoft アプリケーション登録ポータル**] リンクを選択し、Microsoft ID でサインインします。</span><span class="sxs-lookup"><span data-stu-id="74b55-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="74b55-225">MoodleBot などのアプリの名前を入力し、[ **作成** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="74b55-226">アプリケーション **ID** をコピーし、[**チーム 設定]** ページの **[Bot アプリケーション ID]** フィールドに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="74b55-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="74b55-227">[ **新しいパスワードの生成]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="74b55-228">生成されたパスワードをコピーし、[**チーム 設定]** ページの **[Bot アプリケーション パスワード]** フィールドに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="74b55-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="74b55-229">フォームの一番下までスクロールし、[ **変更を保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="74b55-230">アプリケーション ID とパスワードを生成したら、次の手順でボットを Azure にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="74b55-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74b55-231">[Azure **にデプロイ]** を選択し **、Teams 設定** ページの Bot アプリケーション ID、ボット アプリケーション パスワード、Moodle シークレットなどの必要な情報をフォームに入力します。</span><span class="sxs-lookup"><span data-stu-id="74b55-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="74b55-232">Azure の情報は **[セットアップ** ] ページにあります。</span><span class="sxs-lookup"><span data-stu-id="74b55-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="74b55-233">フォームに記入したら、チェックボックスを選択して利用規約に同意します。</span><span class="sxs-lookup"><span data-stu-id="74b55-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="74b55-234">[ **購入**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-234">Select **Purchase**.</span></span> <span data-ttu-id="74b55-235">すべての Azure リソースは、無料のレベルにデプロイされます。</span><span class="sxs-lookup"><span data-stu-id="74b55-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="74b55-236">リソースが Azure へのデプロイを完了したら、メッセージング エンドポイントを使用して Microsoft 365 Moodle プラグインを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="74b55-237">Azure のボットからエンドポイントを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="74b55-238">[Azure portal](https://portal.azure.com) にサインインします。</span><span class="sxs-lookup"><span data-stu-id="74b55-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="74b55-239">左側のウィンドウで [ **リソース グループ** ] を選択し、ボットのデプロイ中に使用または作成したリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="74b55-240">グループ内のリソースのリストから **WebApp Bot** リソースを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="74b55-241">「**概要**」セクションから **メッセージング・エンドポイント** をコピーします。</span><span class="sxs-lookup"><span data-stu-id="74b55-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="74b55-242">Moodleで、Microsoft 365のMoodleプラグインの **チーム設定** ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="74b55-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="74b55-243">[ **ボット エンドポイント** ] フィールドに、コピーした URL を貼り付け *、メッセージという* 単語を *webhook* に変更します。</span><span class="sxs-lookup"><span data-stu-id="74b55-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="74b55-244">URL は次のように表示される必要があります。 `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="74b55-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="74b55-245">[ **変更の保存 ] を** 選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="74b55-246">変更を保存したら、[**チーム 設定]** タブに戻り、[**マニフェスト ファイルのダウンロード**] ボタンを選択して、アプリ マニフェスト パッケージをコンピューターに保存して、さらに使用します。</span><span class="sxs-lookup"><span data-stu-id="74b55-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="74b55-247">4. Microsoft Teams アプリを展開する</span><span class="sxs-lookup"><span data-stu-id="74b55-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="74b55-248">ボットが Azure にデプロイされ、Moodle サーバーとの会話をするように構成された後、Microsoft Teamsアプリをデプロイする必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="74b55-249">これを行うには、前の手順でMicrosoft 365 Moodle プラグイン チーム 設定 ページからダウンロードしたアプリ マニフェスト ファイルを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="74b55-250">アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="74b55-251">詳細については、「 [Microsoft 365 テナントの準備](../concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="74b55-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="74b55-252">**アプリを展開するには**</span><span class="sxs-lookup"><span data-stu-id="74b55-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="74b55-253">**Microsoft Teams** を開きます。</span><span class="sxs-lookup"><span data-stu-id="74b55-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="74b55-254">ナビゲーションバーの左下の領域にある **アプリ** アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="74b55-255">オプションの一覧から **、カスタム アプリのリンクをアップロード** を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="74b55-256">グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。</span><span class="sxs-lookup"><span data-stu-id="74b55-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="74b55-257">`manifest.zip`以前にダウンロードしたパッケージを選択し、[**保存 ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="74b55-258">アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle のプラグイン構成ページの **[チーム 設定]** タブからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="74b55-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="74b55-259">これでアプリがインストールされ、アクセスできる任意のチャネルにタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="74b55-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="74b55-260">これを行うには、チャンネルに移動し、 **プラス** 記号 (➕) を選択し、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="74b55-261">プロンプトに従って、Moodleコースタブをチャンネルに追加します。</span><span class="sxs-lookup"><span data-stu-id="74b55-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="74b55-262">5. Microsoft Teamsで Moodle タブの自動作成を許可する</span><span class="sxs-lookup"><span data-stu-id="74b55-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="74b55-263">Moodle タブはMicrosoft Teamsで手動で作成されますが、コースの同期からチームを作成するときに自動的に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="74b55-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="74b55-264">これを行うには、Moodle でアップロードされたMicrosoft Teamsアプリの ID を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="74b55-265">**Moodleタブの自動作成を許可するには**</span><span class="sxs-lookup"><span data-stu-id="74b55-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="74b55-266">Microsoft Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="74b55-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="74b55-267">ナビゲーションバーの左下の領域から[アプリ]アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="74b55-268">アップロードされた **Moodle アプリ** を探> **オプション** アイコンを選択 **>、コピー リンク** を選択します。</span><span class="sxs-lookup"><span data-stu-id="74b55-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="74b55-269">テキスト エディタで、コピーしたコンテンツを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="74b55-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="74b55-270">これは、ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff などの URL を含んでいる必要があります。</span><span class="sxs-lookup"><span data-stu-id="74b55-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="74b55-271">Microsoft Teams アプリの ID である など、URL `00112233-4455-6677-8899-aabbccddeeff` の最後の部分をコピーします。</span><span class="sxs-lookup"><span data-stu-id="74b55-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="74b55-272">Moodleで **、Microsoft 365 Moodleプラグイン設定ページからTeams Moodleアプリ** タブを開きます。</span><span class="sxs-lookup"><span data-stu-id="74b55-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="74b55-273">Microsoft Teamsアプリの ID を Moodle アプリ ID フィールドに貼り付け、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="74b55-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="74b55-274">Moodle コースが同期されると、チームに Moodle アプリが自動的にインストールMicrosoft Teams、Teamsの一般チャネルに Moodle タブが作成され、同期元の Moodle コースのコースページが含まれる構成が行われます。</span><span class="sxs-lookup"><span data-stu-id="74b55-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="74b55-275">Microsoft Teamsから直接Moodleコースで作業を開始できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="74b55-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="74b55-276">機能のリクエストやフィードバックを当社と共有するには、 [ユーザーの声ページ](https://microsoftteams.uservoice.com/forums/916759-moodle)にアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="74b55-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="74b55-277">関連項目</span><span class="sxs-lookup"><span data-stu-id="74b55-277">See also</span></span>

- [<span data-ttu-id="74b55-278">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="74b55-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="74b55-279">ムードル</span><span class="sxs-lookup"><span data-stu-id="74b55-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="74b55-280">[Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins)。</span><span class="sxs-lookup"><span data-stu-id="74b55-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

