---
title: Moodle LMS のインストール
description: アプリの Moodle 統合アプリをインストールして構成するMicrosoft Teams
keywords: TeamsMoodle アプリ統合プラグイン
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
# <a name="install-moodle-lms"></a><span data-ttu-id="aa262-104">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="aa262-104">Install Moodle LMS</span></span>

<span data-ttu-id="aa262-105">この記事では、Moodle LMS をインストールする方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="aa262-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="aa262-106">IT 管理者が簡単に Moodle と Teams統合をセットアップMicrosoft 365、次の情報が更新されます。</span><span class="sxs-lookup"><span data-stu-id="aa262-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="aa262-107">Moodle サーバーの自動登録[(Azure Azure Active Directory) を使用AD。](https://azure.microsoft.com/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="aa262-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="aa262-108">Moodle Assistant ボットの Azure への展開を 1 回クリックで行います。</span><span class="sxs-lookup"><span data-stu-id="aa262-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="aa262-109">チームの自動プロビジョニングと、すべてのチーム登録の自動同期、または [Moodle コース] の選択が可能です。</span><span class="sxs-lookup"><span data-stu-id="aa262-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="aa262-110">[Moodle] タブと [Moodle アシスタント ボット] を同期された各チームに自動インストールします。</span><span class="sxs-lookup"><span data-stu-id="aa262-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="aa262-111">この統合で提供される機能の詳細については、「Microsoft Teams[と Moodle」を参照してください](https://education.microsoft.com/resource/3dffb3a8)。</span><span class="sxs-lookup"><span data-stu-id="aa262-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa262-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="aa262-112">Prerequisites</span></span>

<span data-ttu-id="aa262-113">Moodle をインストールするための前提条件は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="aa262-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="aa262-114">Moodle 管理者の資格情報。</span><span class="sxs-lookup"><span data-stu-id="aa262-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="aa262-115">Azure AD資格情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="aa262-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="aa262-116">新しいリソースを作成できる Azure サブスクリプション。</span><span class="sxs-lookup"><span data-stu-id="aa262-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="aa262-117">1. Moodle プラグインMicrosoft 365インストールする</span><span class="sxs-lookup"><span data-stu-id="aa262-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="aa262-118">Moodle プラグインセットMicrosoft Teamsオープンソースの機能を使用して、Microsoft 365[の統合を行います](https://github.com/Microsoft/o365-moodle)。</span><span class="sxs-lookup"><span data-stu-id="aa262-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="aa262-119">必要なアプリケーションとプラグイン</span><span class="sxs-lookup"><span data-stu-id="aa262-119">Requisite applications and plugins</span></span>

<span data-ttu-id="aa262-120">Moodle プラグインのインストールに進む前に、次のMicrosoft 365ダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="aa262-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="aa262-121">現在の安定版 [の Moodle をインストールしてください](https://download.moodle.org/releases/latest/)。</span><span class="sxs-lookup"><span data-stu-id="aa262-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="aa262-122">Moodle [OpenID](https://moodle.org/plugins/auth_oidc)プラグインとConnect統合[Microsoft 365](https://moodle.org/plugins/local_o365)をローカル コンピューターにダウンロードして保存します。</span><span class="sxs-lookup"><span data-stu-id="aa262-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa262-123">OpenID の統合ConnectインストールMicrosoft 365統合プラグインのインストールTeams必要です。</span><span class="sxs-lookup"><span data-stu-id="aa262-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="aa262-124">さらに、テーマ[プラグインMicrosoft 365 Teams強](https://moodle.org/plugins/theme_boost_o365teams)くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="aa262-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="aa262-125">Microsoft 365Moodle プラグイン</span><span class="sxs-lookup"><span data-stu-id="aa262-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="aa262-126">管理者として Moodle サーバーにサインインし、左側の[ナビゲーション](https://docs.moodle.org/22/en/Settings_block)パネルにある [設定] ブロックから [サイトの管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="aa262-127">[プラグイン] **タブを選択** し、[プラグインのインストール **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="aa262-128">[ZIP ファイル **からプラグインをインストールする] セクションで、[** ファイルの **選択] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="aa262-129">左側 **アップロードからファイル** オプションを選択し、ダウンロードしたファイルを参照し、このファイルアップロード **選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="aa262-130">左側 **のナビゲーション パネルから** [サイトの管理] を選択して、管理ダッシュボードに戻ります。</span><span class="sxs-lookup"><span data-stu-id="aa262-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="aa262-131">[ローカル プラグイン] まで **下にスクロールし、[** 統合 **] リンクMicrosoft 365選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="aa262-132">プロセスをMicrosoft 365ページのセットに戻す必要がある場合は、別のブラウザー タブで [Moodle Plugins] 構成ページを開いた状態にしてください。</span><span class="sxs-lookup"><span data-stu-id="aa262-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="aa262-133">既存の Moodle サイトをお持ちではない場合は、Azure repo の [Moodle](https://github.com/azure/moodle) に移動し、Moodle インスタンスをすばやく展開し、ニーズに合わせてカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="aa262-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="aa262-134">2. Microsoft 365 プラグインと Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="aa262-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="aa262-135">アプリケーション プラグインと Azure プラグイン間の接続Microsoft 365構成する必要AD。</span><span class="sxs-lookup"><span data-stu-id="aa262-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="aa262-136">前提条件</span><span class="sxs-lookup"><span data-stu-id="aa262-136">Requisites</span></span>

<span data-ttu-id="aa262-137">PowerShell スクリプトを使用して、Azure ADアプリケーションとして Moodle を登録します。</span><span class="sxs-lookup"><span data-stu-id="aa262-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="aa262-138">Powershell スクリプトは、次の情報を準備します。</span><span class="sxs-lookup"><span data-stu-id="aa262-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="aa262-139">新しい Azure ADアプリケーションは、Microsoft 365 Moodle プラグインで使用される、Microsoft 365テナント用です。</span><span class="sxs-lookup"><span data-stu-id="aa262-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="aa262-140">テナントのアプリMicrosoft 365、プロビジョニングされたアプリに必要な返信 URL とアクセス許可を設定し、および `AppID` を返します `Key` 。</span><span class="sxs-lookup"><span data-stu-id="aa262-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="aa262-141">生成され、お使Microsoft 365の [Moodle プラグイン] セットアップ ページで、Azure サーバー を使用して Moodle サーバー サイトを `AppID` `Key` 構成AD。</span><span class="sxs-lookup"><span data-stu-id="aa262-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="aa262-142">PowerShell スクリプトは最新の構成項目で更新されないので、Moodle [3.8.0.4 および 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) および [3.8.0.5 および 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って手動で構成を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="aa262-143">Moodle インスタンスを手動で登録する方法の詳細については、「アプリケーションとして Moodle インスタンスを登録する [」を参照してください](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。</span><span class="sxs-lookup"><span data-stu-id="aa262-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="aa262-144">[情報フロー] の [Microsoft Teams] タブ</span><span class="sxs-lookup"><span data-stu-id="aa262-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="aa262-145">[統合Microsoft 365] ページで、[セットアップ] タブ **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="aa262-146">**[PowerShell スクリプトのダウンロード] ボタン** を選択し、ローカル コンピューターに ZIP フォルダーとして保存します。</span><span class="sxs-lookup"><span data-stu-id="aa262-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="aa262-147">ZIP ファイルから PowerShell スクリプトを次のように準備します。</span><span class="sxs-lookup"><span data-stu-id="aa262-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="aa262-148">ファイルをダウンロードして抽出 `Moodle-AzureAD-Powershell.zip` します。</span><span class="sxs-lookup"><span data-stu-id="aa262-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="aa262-149">抽出したフォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="aa262-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="aa262-150">ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` プロパティ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="aa262-151">[プロパティ **] ウィンドウの**[全般] タブで、ウィンドウの下部にあるセキュリティ属性の横にあるチェック `Unblock` ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="aa262-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="aa262-152">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-152">Select **OK**.</span></span>
    1. <span data-ttu-id="aa262-153">ディレクトリ パスを抽出したフォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="aa262-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="aa262-154">管理者として PowerShell を実行します。</span><span class="sxs-lookup"><span data-stu-id="aa262-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="aa262-155">[開始] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-155">Select Start.</span></span>
    1. <span data-ttu-id="aa262-156">「PowerShell」と入力します。</span><span class="sxs-lookup"><span data-stu-id="aa262-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="aa262-157">[次へ] を **右クリックWindows PowerShell** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="aa262-158">[管理者 **として実行] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="aa262-159">ディレクトリへのパスを where と入力して、未設定 `cd .../.../Moodle-AzureAD-Powershell` `.../...` のディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="aa262-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="aa262-160">PowerShell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="aa262-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="aa262-161">を `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 入力します。</span><span class="sxs-lookup"><span data-stu-id="aa262-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="aa262-162">を `./Moodle-AzureAD-Script.ps1` 入力します。</span><span class="sxs-lookup"><span data-stu-id="aa262-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="aa262-163">ポップアップ ウィンドウでMicrosoft 365管理者アカウントにサインインします。</span><span class="sxs-lookup"><span data-stu-id="aa262-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="aa262-164">たとえば、Moodle プラグインや Moodle プラグインなど、Azure ADアプリケーションの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="aa262-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="aa262-165">Moodle サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="aa262-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="aa262-166">スクリプトによって **生成されたアプリケーション ID ( `AppID` )** と Application **Key( `Key` )** をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="aa262-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="aa262-167">次に `AppID` 、Moodle `Key` プラグインを追加し、Microsoft 365する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="aa262-168">[プラグインの管理] ページの [サイト管理] >統合> Microsoft 365します。</span><span class="sxs-lookup"><span data-stu-id="aa262-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="aa262-169">[セットアップ **] タブ** で、前にコピーした項目を追加し、[ `AppID` `Key` 変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="aa262-170">ページが更新された後、新しいセクション [接続方法の選択 **] が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="aa262-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="aa262-171">[接続方法 **の選択] で**、[既定]というラベルの付いたチェック ボックスをオンにし、[変更の保存 **] を再度選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="aa262-172">ページが更新された後、別の新しいセクション [管理者の同意] が表示 **され&情報が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="aa262-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="aa262-173">[**管理者の同意の提供**] リンクを選択し、グローバル管理者Microsoft 365資格情報を入力し、[**同意** する] を選択してアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="aa262-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="aa262-174">[Azure ADテナント] **フィールドの横** にある [検出] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="aa262-175">[URL] の **横OneDrive for Business[** 検出] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="aa262-176">フィールドが設定された後、もう一度 [変更の **保存] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="aa262-177">[更新] **ボタンを** 選択してインストールを確認し、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="aa262-178">Moodle サーバーと Azure サーバー間でユーザーを同期AD。</span><span class="sxs-lookup"><span data-stu-id="aa262-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="aa262-179">次の手順をお試しください。</span><span class="sxs-lookup"><span data-stu-id="aa262-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa262-180">環境に応じて、この段階でさまざまなオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="aa262-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="aa262-181">Moodle サーバーと Azure サーバー間でユーザーを同期AD。</span><span class="sxs-lookup"><span data-stu-id="aa262-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="aa262-182">環境に応じて、この段階でさまざまなオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="aa262-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="aa262-183">次の手順をお試しください。</span><span class="sxs-lookup"><span data-stu-id="aa262-183">To get started:</span></span>
    1. <span data-ttu-id="aa262-184">[同期] タブ **に設定します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="aa262-185">[Azure **ユーザーとユーザーを同期AD]** セクションで、環境に適用するチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="aa262-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="aa262-186">次の項目を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-186">You must select the following:</span></span>  

        <span data-ttu-id="aa262-187">✔ Azure のユーザー向け Moodle でアカウントを作成AD。</span><span class="sxs-lookup"><span data-stu-id="aa262-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="aa262-188">✔ Azure アカウントのユーザーに対して、Moodle のすべてのアカウントを更新AD。</span><span class="sxs-lookup"><span data-stu-id="aa262-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="aa262-189">[ユーザー **作成の制限] セクション** で、Moodle に同期AD Azure ユーザーを制限するフィルターをセットアップできます。</span><span class="sxs-lookup"><span data-stu-id="aa262-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="aa262-190">[ **ユーザー フィールド マッピング]** セクションでは、Azure のユーザー プロファイルADを Moodle ユーザー プロファイル フィールド マッピングにカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="aa262-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="aa262-191">[同期 **Teams]** セクションで、既存の Moodle コースの一部またはすべてのチームなどのグループを自動的に作成する場合に選択できます。</span><span class="sxs-lookup"><span data-stu-id="aa262-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="aa262-192">cron ジョブ [を検証し](https://docs.moodle.org/310/en/Cron)、最初の実行に対して手動で実行するには **、[Azure** とユーザーを同期する] セクションの [スケジュールされたタスクの管理] ADします。</span><span class="sxs-lookup"><span data-stu-id="aa262-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="aa262-193">これにより、[スケジュールされたタスク] **ページに移動** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="aa262-194">下にスクロールして、Azure ユーザーと **同期するジョブをADし、[今すぐ** 実行] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="aa262-195">既存のコースに基づいてグループを作成する場合は、ユーザー グループを作成するジョブ **Microsoft 365** することもできます。</span><span class="sxs-lookup"><span data-stu-id="aa262-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="aa262-196">Moodle [Cron はタスク](https://docs.moodle.org/310/en/Cron) スケジュールに従って実行されます。</span><span class="sxs-lookup"><span data-stu-id="aa262-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="aa262-197">既定のスケジュールは 1 日 1 回です。</span><span class="sxs-lookup"><span data-stu-id="aa262-197">The default schedule is once a day.</span></span> <span data-ttu-id="aa262-198">ただし、すべての同期を維持するには、cron の実行頻度を高くする必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="aa262-199">[プラグインの管理] ページの [**サイト**>統合> Microsoft 365に戻り、[プラグイン]**ページTeams 設定します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="aa262-200">[アプリの **Teams 設定]** ページで、アプリの統合を有効にするために必要なTeams構成します。</span><span class="sxs-lookup"><span data-stu-id="aa262-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="aa262-201">**OpenID** Connectを有効にするには、[認証の管理] リンクを選択し、灰色で表示されている場合は **、OpenId** Connectで目のアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="aa262-202">フレーム埋め込みを有効にするには **、[HTTP セキュリティ** ] リンクを選択し、[フレームの埋め込みを許可する] の横にあるチェック **ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="aa262-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="aa262-203">Moodle API 機能を有効にする Web サービスを有効にするには、[高度な機能] リンクを選択し、[Web サービスを有効にする] の横にあるチェック ボックスがオンになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="aa262-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="aa262-204">外部サービスを有効にするには、[外部Microsoft 365]**リンクを選択** し、次の項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="aa262-205">✔ **[Moodle] ページの**[編集] **Microsoft 365選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="aa262-206">✔ [有効] の横にあるチェック ボックス **をオンにして**、[変更の保存] **を選択します。**</span><span class="sxs-lookup"><span data-stu-id="aa262-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="aa262-207">認証されたユーザーのアクセス許可を編集して、Web サービス トークンの作成を許可します。</span><span class="sxs-lookup"><span data-stu-id="aa262-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="aa262-208">✔ [編集] **役割の [認証済みユーザー] リンクを選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="aa262-209">✔下にスクロールし **、[Web** サービス トークンの作成] 機能を見つけて、[許可] チェック ボックス **をオン** にします。</span><span class="sxs-lookup"><span data-stu-id="aa262-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="aa262-210">3. Moodle アシスタント ボットを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="aa262-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="aa262-211">無料の Moodle アシスタント ボット Microsoft Teams教師と学生が、Moodle のコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="aa262-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="aa262-212">ボットは、このボット内の生徒や教師に、Moodle 通知Teams。</span><span class="sxs-lookup"><span data-stu-id="aa262-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="aa262-213">ボットは、Microsoft が管理するオープン ソース プロジェクトであり、このプロジェクトで[GitHub。](https://github.com/microsoft/Moodle-Teams-Bot)</span><span class="sxs-lookup"><span data-stu-id="aa262-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="aa262-214">リソースを Azure サブスクリプションに展開します。</span><span class="sxs-lookup"><span data-stu-id="aa262-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="aa262-215">すべてのリソースは、無料レベルを使用 **して構成** されています。</span><span class="sxs-lookup"><span data-stu-id="aa262-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="aa262-216">ボットの使用状況によっては、これらのリソースのスケーリングが必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="aa262-217">ボットなしで [Moodle] タブを使用するには [、4 にスキップします](#4-deploy-your-microsoft-teams-app)。</span><span class="sxs-lookup"><span data-stu-id="aa262-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="aa262-218">Moodle ボットの情報フロー</span><span class="sxs-lookup"><span data-stu-id="aa262-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="aa262-219">ボットをインストールするには、Microsoft Identity Platform に [ボットを登録する必要があります](https://identity.microsoft.com/Landing)。</span><span class="sxs-lookup"><span data-stu-id="aa262-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="aa262-220">これにより、ボットは Microsoft エンドポイントに対して認証できます。</span><span class="sxs-lookup"><span data-stu-id="aa262-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="aa262-221">**ボットを登録するには**</span><span class="sxs-lookup"><span data-stu-id="aa262-221">**To register your bot**</span></span>

1. <span data-ttu-id="aa262-222">[プラグインの管理] ページに移動し、[プラグイン] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="aa262-223">[統合 **Microsoft 365] の** 下で、[統合]**タブTeams 設定** 選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="aa262-224">[Microsoft **アプリケーション登録ポータル] リンクを選択** し、Microsoft ID でサインインします。</span><span class="sxs-lookup"><span data-stu-id="aa262-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="aa262-225">アプリの名前 (MoodleBot など) を入力し、[作成] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="aa262-226">アプリケーション ID **をコピーし**、[チーム] ページの [ボット アプリケーション **ID]** **フィールドに貼り設定** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="aa262-227">[新しい **パスワードの生成] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="aa262-228">生成されたパスワードをコピーし、[チーム] ページの [**ボット アプリケーション** パスワード **] フィールドに貼り設定** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="aa262-229">フォームの下部までスクロールし、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="aa262-230">アプリケーション ID とパスワードを生成した後、ボットを Azure に展開します。</span><span class="sxs-lookup"><span data-stu-id="aa262-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa262-231">[Azure **に展開する**] を選択し、ボット アプリケーション ID、ボット アプリケーション パスワード、および [アカウント] ページの **[Moodle** シークレット] など、必要な情報を含むフォームTeams 設定します。</span><span class="sxs-lookup"><span data-stu-id="aa262-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="aa262-232">Azure の情報は、[セットアップ] ページ **に表示** されます。</span><span class="sxs-lookup"><span data-stu-id="aa262-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="aa262-233">フォームが完成した後、チェックボックスをオンにして利用規約に同意します。</span><span class="sxs-lookup"><span data-stu-id="aa262-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="aa262-234">[購入 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-234">Select **Purchase**.</span></span> <span data-ttu-id="aa262-235">すべての Azure リソースが無料層に展開されます。</span><span class="sxs-lookup"><span data-stu-id="aa262-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="aa262-236">リソースが Azure への展開を完了したら、メッセージング エンドポイントMicrosoft 365を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="aa262-237">Azure でボットからエンドポイントを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="aa262-238">[Azure portal](https://portal.azure.com) にサインインします。</span><span class="sxs-lookup"><span data-stu-id="aa262-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="aa262-239">左側のウィンドウで、[リソース グループ **] を** 選択し、ボットの展開中に使用または作成したリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="aa262-240">グループ内 **のリソースの一** 覧から WebApp Bot リソースを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="aa262-241">[概要 **] セクションからメッセージング** エンドポイント **をコピー** します。</span><span class="sxs-lookup"><span data-stu-id="aa262-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="aa262-242">Moodle で、お使 **設定の**[チーム] ページMicrosoft 365開きます。</span><span class="sxs-lookup"><span data-stu-id="aa262-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="aa262-243">[ボット **エンドポイント] フィールド** に、コピーした URL を貼り付け、単語メッセージを *webhook に変更します*。 </span><span class="sxs-lookup"><span data-stu-id="aa262-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="aa262-244">URL は次のように表示する必要があります。 `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="aa262-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="aa262-245">[変更 **の保存] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="aa262-246">変更を保存した後、[**チーム**] タブ設定戻り、[マニフェスト ファイルのダウンロード] ボタンを選択し、さらに使用するためにアプリ マニフェスト パッケージをコンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="aa262-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="aa262-247">4. アプリをMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="aa262-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="aa262-248">ボットが Azure に展開され、Moodle サーバーと話をするように構成された後、アプリを展開するMicrosoft Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="aa262-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="aa262-249">これを行うには、前の手順の [Moodle Plugins Team Microsoft 365] 設定からダウンロードしたアプリ マニフェスト ファイルを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="aa262-250">アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="aa262-251">詳細については、「Prepare [your Microsoft 365 テナント」を参照してください](../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="aa262-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="aa262-252">**アプリを展開するには**</span><span class="sxs-lookup"><span data-stu-id="aa262-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="aa262-253">[ファイル **Microsoft Teams] を開きます**。</span><span class="sxs-lookup"><span data-stu-id="aa262-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="aa262-254">ナビゲーション バー **の** 左下の領域にある [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="aa262-255">オプションの **アップロードからカスタム アプリ** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aa262-256">グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。それ以外の場合は、メンバーであるチームのアプリのみを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="aa262-257">以前に `manifest.zip` ダウンロードしたパッケージを選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="aa262-258">アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle の [プラグイン構成] ページの **[** チーム 設定] タブからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="aa262-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="aa262-259">アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="aa262-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="aa262-260">これを行うには、チャネルに移動し、 **プラス記号** (➕) を選択し、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="aa262-261">プロンプトに従って、チャネルへの Moodle コース タブの追加を完了します。</span><span class="sxs-lookup"><span data-stu-id="aa262-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="aa262-262">5. [自動作成] ウィンドウで [Moodle] タブをMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="aa262-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="aa262-263">[Moodle] タブは、Microsoft Teamsで手動で作成しますが、チームがコース同期から作成されると、自動的に作成できます。</span><span class="sxs-lookup"><span data-stu-id="aa262-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="aa262-264">これを行うには、Moodle でアップロードされたアプリの ID Microsoft Teams構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa262-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="aa262-265">**Moodle タブの自動作成を許可するには**</span><span class="sxs-lookup"><span data-stu-id="aa262-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="aa262-266">Microsoft Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="aa262-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="aa262-267">ナビゲーション バーの左下の領域から [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="aa262-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="aa262-268">アップロードされた **Moodle アプリを見つけて>** オプション アイコン **を** 選択し>コピー リンクを **選択します**。</span><span class="sxs-lookup"><span data-stu-id="aa262-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="aa262-269">テキスト エディターで、コピーしたコンテンツを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="aa262-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="aa262-270">これは、ht ファイルなどの URL を含&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。</span><span class="sxs-lookup"><span data-stu-id="aa262-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="aa262-271">URL の最後の部分 (アプリの ID など) `00112233-4455-6677-8899-aabbccddeeff` をMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="aa262-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="aa262-272">Moodle で、[Moodle プラグインの構成 **] ページTeams** [ムードル アプリ] タブMicrosoft 365開きます。</span><span class="sxs-lookup"><span data-stu-id="aa262-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="aa262-273">アプリの ID を [Moodle Microsoft Teams ID] フィールドに貼り付け、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="aa262-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="aa262-274">Moodle コースが同期されている場合、Microsoft Teams はチームに Moodle アプリを自動的にインストールし、Teams の [全般] チャネルに [Moodle] タブを作成し、同期する Moodle コースのコース ページを含む構成を行います。</span><span class="sxs-lookup"><span data-stu-id="aa262-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="aa262-275">これで、お客様の Moodle コースの操作を、お客様のアカウントから直接Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="aa262-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="aa262-276">機能の要求やフィードバックを共有するには、User Voice [ページをご覧ください](https://microsoftteams.uservoice.com/forums/916759-moodle)。</span><span class="sxs-lookup"><span data-stu-id="aa262-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="aa262-277">関連項目</span><span class="sxs-lookup"><span data-stu-id="aa262-277">See also</span></span>

- [<span data-ttu-id="aa262-278">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="aa262-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="aa262-279">Moodle</span><span class="sxs-lookup"><span data-stu-id="aa262-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="aa262-280">[Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="aa262-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

