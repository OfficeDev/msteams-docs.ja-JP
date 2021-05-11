---
title: Moodle LMS のインストール
description: アプリの Moodle 統合アプリをインストールして構成するMicrosoft Teams
keywords: TeamsMoodle アプリ統合プラグイン
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 2a99acbe9bc618ea940af3bbe898b30d342ad0cf
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058356"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="f357c-104">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="f357c-104">Install Moodle LMS</span></span>

<span data-ttu-id="f357c-105">Moodle は、一般的なオープン ソース学習管理システム (LMS) です。</span><span class="sxs-lookup"><span data-stu-id="f357c-105">Moodle is a popular open-source Learning Management System (LMS).</span></span> <span data-ttu-id="f357c-106">この機能は現在、Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="f357c-106">It is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="f357c-107">この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をし、通知を直接通知Teams。</span><span class="sxs-lookup"><span data-stu-id="f357c-107">This integration helps educators and teachers to collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

<span data-ttu-id="f357c-108">IT 管理者が簡単にこの統合をセットアップするために、オープン ソース Microsoft 365 Moodle Plugin は次の機能で更新されます。</span><span class="sxs-lookup"><span data-stu-id="f357c-108">To help IT admins easily set-up this integration, open-source Microsoft 365 Moodle Plugin is updated with the following capabilities:</span></span>

* <span data-ttu-id="f357c-109">Moodle サーバーの自動登録 (Azure Azure Active Directory) を使用AD。 [](https://azure.microsoft.com/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="f357c-109">Auto-registration of your Moodle server with [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).</span></span>
* <span data-ttu-id="f357c-110">Moodle Assistant ボットの Azure への展開を 1 回クリックで行います。</span><span class="sxs-lookup"><span data-stu-id="f357c-110">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
* <span data-ttu-id="f357c-111">チームの自動プロビジョニングと、すべてのチーム登録の自動同期、または [Moodle コース] の選択が可能です。</span><span class="sxs-lookup"><span data-stu-id="f357c-111">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
* <span data-ttu-id="f357c-112">[Moodle] タブと [Moodle アシスタント ボット] を同期された各チームに自動インストールします。</span><span class="sxs-lookup"><span data-stu-id="f357c-112">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>

<span data-ttu-id="f357c-113">この統合で提供される機能の詳細については、「Microsoft Teams[と Moodle」を参照してください](https://education.microsoft.com/resource/3dffb3a8)。</span><span class="sxs-lookup"><span data-stu-id="f357c-113">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f357c-114">前提条件</span><span class="sxs-lookup"><span data-stu-id="f357c-114">Prerequisites</span></span>

<span data-ttu-id="f357c-115">Moodle アプリケーションをインストールして構成するための前提条件を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f357c-115">Following are the prerequisites to install and configure the Moodle application:</span></span> 

1. <span data-ttu-id="f357c-116">Moodle 管理者の資格情報。</span><span class="sxs-lookup"><span data-stu-id="f357c-116">Moodle administrator credentials.</span></span>

1. <span data-ttu-id="f357c-117">Azure AD資格情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="f357c-117">Azure AD administrator credentials.</span></span>

1. <span data-ttu-id="f357c-118">新しいリソースを作成できる Azure サブスクリプション。</span><span class="sxs-lookup"><span data-stu-id="f357c-118">An Azure subscription where you can create new resources.</span></span>

<span data-ttu-id="f357c-119">**Moodle アプリケーションをインストールして構成するには**</span><span class="sxs-lookup"><span data-stu-id="f357c-119">**To install and configure the Moodle application**</span></span> 

<span data-ttu-id="f357c-120">次の手順を実行して、Moodle アプリケーションをインストールして構成します。</span><span class="sxs-lookup"><span data-stu-id="f357c-120">Perform the following steps to install and configure the Moodle application:</span></span> 

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="f357c-121">1. Moodle プラグインMicrosoft 365インストールする</span><span class="sxs-lookup"><span data-stu-id="f357c-121">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="f357c-122">このツールの Moodle 統合Microsoft Teams、Moodle プラグイン セットのオープンソース[Microsoft 365を使用します](https://github.com/Microsoft/o365-moodle)。</span><span class="sxs-lookup"><span data-stu-id="f357c-122">The Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugin set](https://github.com/Microsoft/o365-moodle).</span></span> <span data-ttu-id="f357c-123">Moodle サーバーにプラグインをインストールするには、次のアプリケーションがインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-123">To install the plugin in your Moodle server you must have the following applications installed:</span></span>

1. <span data-ttu-id="f357c-124">現在 [の安定版の Moodle](https://download.moodle.org/releases/latest/)です。</span><span class="sxs-lookup"><span data-stu-id="f357c-124">A [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="f357c-125">Moodle [OpenID Connect、Microsoft 365](https://moodle.org/plugins/auth_oidc)にダウンロード[](https://moodle.org/plugins/local_o365)して保存された統合プラグインを使用します。</span><span class="sxs-lookup"><span data-stu-id="f357c-125">The Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins downloaded and saved to your local computer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f357c-126">OpenID の統合ConnectインストールMicrosoft 365統合プラグインのインストールTeams必要です。</span><span class="sxs-lookup"><span data-stu-id="f357c-126">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span> <span data-ttu-id="f357c-127">さらに、テーマ プラグイン[Microsoft 365 Teams強](https://moodle.org/plugins/theme_boost_o365teams)くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f357c-127">Additionally, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugin is highly recommended.</span></span>

1. <span data-ttu-id="f357c-128">管理者として Moodle サーバーにサインインし、左側の[ナビゲーション](https://docs.moodle.org/22/en/Settings_block)パネルにある [設定] ブロックから [サイトの管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-128">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="f357c-129">[プラグイン] **タブを選択** し、[プラグインのインストール **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-129">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="f357c-130">[ZIP ファイル **からプラグインをインストールする] セクションで、[** ファイルの **選択] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-130">From the **Install plugin from ZIP file** section, select **Choose a file** button.</span></span>

1. <span data-ttu-id="f357c-131">左側 **アップロードファイル オプション** を選択し、ダウンロードしたファイルを参照し、このファイルのアップロード **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-131">Select **Upload a file** option from the left navigation, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="f357c-132">左側の **ナビゲーション パネルから** [サイトの管理] を選択して、管理ダッシュボードに戻ります。</span><span class="sxs-lookup"><span data-stu-id="f357c-132">Select the **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="f357c-133">[ローカル プラグイン] まで **下にスクロールし、[** 統合 **] リンクMicrosoft 365選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-133">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span> 

> [!IMPORTANT]
>
> * <span data-ttu-id="f357c-134">プロセスをMicrosoft 365ページのセットに戻す必要がある場合は、別のブラウザー タブで[Moodle Plugin]構成ページを開いた状態にしてください。</span><span class="sxs-lookup"><span data-stu-id="f357c-134">Keep your Microsoft 365 Moodle Plugin configuration page open in a separate browser tab as you have to  return to this set of pages throughout the process.</span></span>  <br/><br/>
> * <span data-ttu-id="f357c-135">既存の Moodle サイトをお持ちではない場合は、Azure [repo](https://github.com/azure/moodle) で Moodle をチェックアウトして、Moodle インスタンスをすばやく展開し、ニーズに合わせてカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="f357c-135">If you do not have an existing Moodle site, you can check out Moodle on Azure [repo](https://github.com/azure/moodle) where you can quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a><span data-ttu-id="f357c-136">2. Microsoft 365 プラグインと Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="f357c-136">2. Configure the connection between the Microsoft 365 plugin and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="f357c-137">Moodle を Azure サーバーにアプリケーションとして登録するAD。</span><span class="sxs-lookup"><span data-stu-id="f357c-137">You must register Moodle as an application in your Azure AD.</span></span> <span data-ttu-id="f357c-138">PowerShell スクリプトを使用してこのプロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="f357c-138">Use PowerShell script to complete this process.</span></span> <span data-ttu-id="f357c-139">PowerShell スクリプトは、新しい Azure AD アプリケーションをMicrosoft 365、このアプリケーションは Moodle プラグインMicrosoft 365します。</span><span class="sxs-lookup"><span data-stu-id="f357c-139">The PowerShell script provisions a new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="f357c-140">スクリプトは、Microsoft 365 テナント用にアプリをプロビジョニングし、プロビジョニングされたアプリに必要な返信 URL とアクセス許可を設定し、およびを返 `AppID` します `Key` 。</span><span class="sxs-lookup"><span data-stu-id="f357c-140">The script provisions the app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and return the `AppID` and `Key`.</span></span> <span data-ttu-id="f357c-141">生成された[Moodle プラグイン] セットアップ ページMicrosoft 365を使用して、Azure サーバー を使用して Moodle サーバー サイト `AppID` `Key` を構成AD。</span><span class="sxs-lookup"><span data-stu-id="f357c-141">You can use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugin setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f357c-142">PowerShell スクリプトは最新の構成項目で更新されないので、Moodle [3.8.0.4 および 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) および [3.8.0.5 および 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って構成を手動で完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-142">The PowerShell script is not updated with the latest configuration items, so you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span> </br></br>
> * <span data-ttu-id="f357c-143">PowerShell スクリプトが自動化している手動手順の詳細については、「アプリケーションとして Moodle インスタンスを登録する [」を参照してください](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。</span><span class="sxs-lookup"><span data-stu-id="f357c-143">To view the manual steps that the PowerShell script is automating in detail, see [Register your Moodle instance as an Application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="f357c-144">[情報フロー] の [Microsoft Teams] タブ</span><span class="sxs-lookup"><span data-stu-id="f357c-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="f357c-145">[統合Microsoft 365] ページで、[セットアップ] タブ **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-145">From the Microsoft 365 Integration plugin page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="f357c-146">**[PowerShell スクリプトのダウンロード] ボタンを** 選択し、ローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="f357c-146">Select the **Download PowerShell Script** button and save it to your local computer.</span></span>

1. <span data-ttu-id="f357c-147">ZIP ファイルから PowerShell スクリプトを準備する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-147">You must prepare the PowerShell script from the ZIP file.</span></span> <span data-ttu-id="f357c-148">ZIP ファイルから PowerShell スクリプトを準備するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f357c-148">Perform the following steps to prepare the PowerShell script from the ZIP file:</span></span>

    1. <span data-ttu-id="f357c-149">ファイルをダウンロードして抽出 `Moodle-AzureAD-Powershell.zip` します。</span><span class="sxs-lookup"><span data-stu-id="f357c-149">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="f357c-150">抽出したフォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="f357c-150">Open the extracted folder.</span></span>
    1. <span data-ttu-id="f357c-151">ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` プロパティ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-151">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="f357c-152">[プロパティ **] ウィンドウの**[全般] タブで、ウィンドウの下部にある Security 属性の横にあるボックス `Unblock` をオンにします。</span><span class="sxs-lookup"><span data-stu-id="f357c-152">Under the **General** tab of the Properties window, check the `Unblock` box next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="f357c-153">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-153">Select **OK**.</span></span>
    1. <span data-ttu-id="f357c-154">ディレクトリ パスを抽出したフォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="f357c-154">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="f357c-155">管理者として PowerShell を実行します。</span><span class="sxs-lookup"><span data-stu-id="f357c-155">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="f357c-156">[開始] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-156">Select Start.</span></span>
    1. <span data-ttu-id="f357c-157">「PowerShell」と入力します。</span><span class="sxs-lookup"><span data-stu-id="f357c-157">Type PowerShell.</span></span>
    1. <span data-ttu-id="f357c-158">[ファイル] を右クリックWindows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f357c-158">Right-click Windows PowerShell.</span></span>
    1. <span data-ttu-id="f357c-159">[管理者 **として実行] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-159">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="f357c-160">ディレクトリへのパスを where と入力して、未設定 `cd .../.../Moodle-AzureAD-Powershell` `.../...` のディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="f357c-160">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="f357c-161">PowerShell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="f357c-161">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="f357c-162">を `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 入力します。</span><span class="sxs-lookup"><span data-stu-id="f357c-162">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="f357c-163">を `./Moodle-AzureAD-Script.ps1` 入力します。</span><span class="sxs-lookup"><span data-stu-id="f357c-163">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="f357c-164">ポップアップ ウィンドウでMicrosoft 365管理者アカウントにサインインします。</span><span class="sxs-lookup"><span data-stu-id="f357c-164">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="f357c-165">Azure AD アプリケーションの名前 (例: Moodle/Moodle プラグイン) を入力します。</span><span class="sxs-lookup"><span data-stu-id="f357c-165">Enter the name of the Azure AD Application (e.g., Moodle/Moodle plugin).</span></span>
    1. <span data-ttu-id="f357c-166">Moodle サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="f357c-166">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="f357c-167">スクリプトによって **生成された** アプリケーション ID と **アプリケーション キー** をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="f357c-167">Copy the **Application ID** and **Application Key** generated by the script and save them.</span></span>

1. <span data-ttu-id="f357c-168">次に、Moodle プラグイン `AppID` `Key` を追加し、Microsoft 365する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-168">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="f357c-169">プラグインの管理ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="f357c-169">Return to the plugin administration page.</span></span> <span data-ttu-id="f357c-170">フローは、サイト管理とプラグイン➡統合➡ Microsoft 365です。</span><span class="sxs-lookup"><span data-stu-id="f357c-170">The flow is: Site administration ➡ Plugins ➡ Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="f357c-171">[セットアップ **] タブで** 、前にコピーした **アプリケーション ID** と **アプリケーション** キーを追加し、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-171">On the **Setup** tab add the **Application ID** and **Application Key** you copied previously, then select **Save changes**.</span></span>

1. <span data-ttu-id="f357c-172">ページが更新された後、新しいセクション [接続方法の選択 **] が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="f357c-172">After the page refreshes, you can see a new section **Choose connection method**.</span></span> <span data-ttu-id="f357c-173">[既定値] というラベルの **付いたチェック ボックスをオン** にし、[変更の **保存] を再度選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-173">Select the checkbox labeled **Default** and then select **Save changes** again.</span></span>

1. <span data-ttu-id="f357c-174">ページが更新された後、別の新しいセクション [管理者の同意] が表示 **され&情報が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="f357c-174">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="f357c-175">[**管理者の同意の提供**] リンクを選択し、グローバル管理者Microsoft 365資格情報を入力し、[**同意** する] を選択してアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="f357c-175">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="f357c-176">[Azure ADテナント] **フィールドの横** にある [検出] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-176">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="f357c-177">[URL] の **横OneDrive for Business[** 検出] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-177">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="f357c-178">フィールドが設定された後、もう一度 [変更の **保存] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-178">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="f357c-179">[更新] **ボタンを** 選択してインストールを確認し、[変更の保存 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-179">Select the **Update** button to verify the installation, then **Save changes**.</span></span>

1. <span data-ttu-id="f357c-180">Moodle サーバーと Azure サーバー間でユーザーを同期AD。</span><span class="sxs-lookup"><span data-stu-id="f357c-180">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="f357c-181">環境に応じて、この段階でさまざまなオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="f357c-181">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="f357c-182">次の手順をお試しください。</span><span class="sxs-lookup"><span data-stu-id="f357c-182">To get started:</span></span>
    1. <span data-ttu-id="f357c-183">[同期]**タブに設定する**</span><span class="sxs-lookup"><span data-stu-id="f357c-183">Switch to the **Sync Settings tab**</span></span>
    1. <span data-ttu-id="f357c-184">[Azure **ユーザーとユーザーを同期AD]** セクションで、環境に適用するチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="f357c-184">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="f357c-185">次の項目を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-185">You must select the following:</span></span>  

        <span data-ttu-id="f357c-186">✔ Azure のユーザー向け Moodle でアカウントを作成AD。</span><span class="sxs-lookup"><span data-stu-id="f357c-186">✔ Create accounts in Moodle for users in Azure AD .</span></span> 
        <span data-ttu-id="f357c-187">✔ Azure アカウントのユーザーに対して、Moodle のすべてのアカウントを更新AD。</span><span class="sxs-lookup"><span data-stu-id="f357c-187">✔ Update all accounts in Moodle for users in Azure AD.</span></span>  

    1. <span data-ttu-id="f357c-188">[ユーザー **作成の制限] セクション** で、Moodle に同期AD Azure ユーザーを制限するフィルターをセットアップできます。</span><span class="sxs-lookup"><span data-stu-id="f357c-188">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="f357c-189">[ **ユーザー フィールド マッピング]** セクションでは、Azure のユーザー プロファイルADを Moodle ユーザー プロファイル フィールド マッピングにカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="f357c-189">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="f357c-190">[同期 **Teams]** セクションで、既存の Moodle コースの一部またはすべてのチームなどのグループを自動的に作成する場合に選択できます。</span><span class="sxs-lookup"><span data-stu-id="f357c-190">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

> [!NOTE]
> <span data-ttu-id="f357c-191">Moodle [Cron はタスク](https://docs.moodle.org/310/en/Cron) スケジュールに従って実行されます。</span><span class="sxs-lookup"><span data-stu-id="f357c-191">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="f357c-192">既定のスケジュールは 1 日 1 回です。</span><span class="sxs-lookup"><span data-stu-id="f357c-192">The default schedule is once a day.</span></span> <span data-ttu-id="f357c-193">ただし、すべての同期を維持するには、cron の実行頻度を高くする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-193">However, the cron must run more frequently to keep everything in sync.</span></span>

13. <span data-ttu-id="f357c-194">cron ジョブ [を検証し](https://docs.moodle.org/310/en/Cron)、最初の実行に対して手動で実行するには **、[Azure** とユーザーを同期する] セクションの [スケジュールされたタスクの管理] ADします。</span><span class="sxs-lookup"><span data-stu-id="f357c-194">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="f357c-195">これにより、[スケジュールされたタスク] **ページに移動** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-195">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="f357c-196">下にスクロールして、Azure ユーザーと **同期するジョブをADし、[今すぐ** 実行] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-196">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="f357c-197">既存のコースに基づいてグループを作成する場合は、ユーザー グループを作成するジョブ **Microsoft 365** することもできます。</span><span class="sxs-lookup"><span data-stu-id="f357c-197">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

1. <span data-ttu-id="f357c-198">プラグインの管理ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="f357c-198">Return to the plugin administration page.</span></span> <span data-ttu-id="f357c-199">ナビゲーション フローは、サイト管理とプラグイン➡ Integratio ➡ Microsoft 365です。</span><span class="sxs-lookup"><span data-stu-id="f357c-199">The navigation flow is: Site administration ➡ Plugins ➡ Microsoft 365 Integratio.</span></span> <span data-ttu-id="f357c-200">次に、[選択] ページ **Teams 設定** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-200">Then, select the **Teams Settings** page.</span></span> <span data-ttu-id="f357c-201">アプリの統合を有効にするには、いくつかのTeamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-201">You must configure some settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="f357c-202">**OpenID** Connectを有効にするには、[認証の管理] リンクを選択し、灰色で表示されている場合は **、OpenId** Connectで目のアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-202">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="f357c-203">フレームの埋め込みを有効にする。</span><span class="sxs-lookup"><span data-stu-id="f357c-203">Enable frame embedding.</span></span> <span data-ttu-id="f357c-204">**[HTTP セキュリティ] リンクを選択** し、[フレームの埋め込みを許可する] の **横にあるチェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="f357c-204">Select the **HTTP Security** link, then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="f357c-205">Moodle API 機能を有効にする Web サービスを有効にする。</span><span class="sxs-lookup"><span data-stu-id="f357c-205">Enable web services which enables the Moodle API features.</span></span> <span data-ttu-id="f357c-206">[高度 **な機能] リンクを** 選択し、[Web サービスを有効にする] の横にある **チェック ボックスがオンになっていることを** 確認します。</span><span class="sxs-lookup"><span data-stu-id="f357c-206">Select the **Advanced Features** link, then make sure the checkbox next to **Enable web services** is checked.</span></span>
    1. <span data-ttu-id="f357c-207">外部サービスを有効にMicrosoft 365。</span><span class="sxs-lookup"><span data-stu-id="f357c-207">Enable the external services for Microsoft 365.</span></span> <span data-ttu-id="f357c-208">次に、[ **外部サービス] リンク** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-208">Select the **External services** link then next:</span></span>  

        <span data-ttu-id="f357c-209">✔ **[Moodle] ページの**[編集] **Microsoft 365選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-209">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>  
        <span data-ttu-id="f357c-210">✔ [有効] の横にあるチェック ボックスを **オンにし、[** 変更の保存] **を選択します。**</span><span class="sxs-lookup"><span data-stu-id="f357c-210">✔ Mark the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="f357c-211">認証されたユーザーのアクセス許可を編集して、Web サービス トークンの作成を許可します。</span><span class="sxs-lookup"><span data-stu-id="f357c-211">Edit your authenticated user permissions to allow them to create web service tokens.</span></span> <span data-ttu-id="f357c-212">[編集] **役割の [認証されたユーザー] リンクを選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-212">Select the **Editing role 'Authenticated user'** link.</span></span> <span data-ttu-id="f357c-213">下にスクロールして、[Web サービス **トークンの作成] 機能を見** つけて、[許可] チェック ボックス **をオン** にします。</span><span class="sxs-lookup"><span data-stu-id="f357c-213">Scroll down and find the **Create a web service token** capability and mark the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="f357c-214">3. Moodle アシスタント ボットを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="f357c-214">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="f357c-215">無料の Moodle アシスタント ボットMicrosoft Teams教師と学生が、Moodle のコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f357c-215">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades and other information in Moodle.</span></span> <span data-ttu-id="f357c-216">ボットは、このボット内の生徒や教師に、Moodle 通知Teams。</span><span class="sxs-lookup"><span data-stu-id="f357c-216">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="f357c-217">ボットは、Microsoft が管理するオープン ソース プロジェクトであり、このプロジェクトで[GitHub。](https://github.com/microsoft/Moodle-Teams-Bot)</span><span class="sxs-lookup"><span data-stu-id="f357c-217">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
> * <span data-ttu-id="f357c-218">このセクションでは、リソースを Azure サブスクリプションに展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-218">In this section you must deploy resources to your Azure subscription.</span></span> <span data-ttu-id="f357c-219">無料レベルを使用して構成されたすべての **リソース ウェア** 。</span><span class="sxs-lookup"><span data-stu-id="f357c-219">All resources ware configured using the **free** tier.</span></span> <span data-ttu-id="f357c-220">ボットの使用状況に応じて、これらのリソースをスケーリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-220">Depending on the usage of your bot, you mhave to scale these resources.</span></span>
> * <span data-ttu-id="f357c-221">ボットなしで [Moodle] タブを使用するには [、4 にスキップします](#4-deploy-your-microsoft-teams-app)。</span><span class="sxs-lookup"><span data-stu-id="f357c-221">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="f357c-222">Moodle ボットの情報フロー</span><span class="sxs-lookup"><span data-stu-id="f357c-222">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="f357c-223">ボットをインストールするには、Microsoft Identity Platform に [ボットを登録する必要があります](https://identity.microsoft.com/Landing)。</span><span class="sxs-lookup"><span data-stu-id="f357c-223">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="f357c-224">これにより、ボットは Microsoft エンドポイントに対して認証できます。</span><span class="sxs-lookup"><span data-stu-id="f357c-224">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="f357c-225">**ボットを登録するには:**</span><span class="sxs-lookup"><span data-stu-id="f357c-225">**To register your bot**:</span></span>

1. <span data-ttu-id="f357c-226">プラグインの管理ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="f357c-226">Go to the plugin administration page.</span></span> <span data-ttu-id="f357c-227">[プラグイン **] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-227">Go to **Plugins**.</span></span> <span data-ttu-id="f357c-228">[統合 **Microsoft 365] の** 下で、[統合]**タブTeams 設定** 選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-228">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="f357c-229">[Microsoft **アプリケーション登録ポータル] リンクを選択** し、Microsoft ID でサインインします。</span><span class="sxs-lookup"><span data-stu-id="f357c-229">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="f357c-230">アプリの名前 (MoodleBot など) を入力し、[作成] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-230">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="f357c-231">アプリケーション ID **をコピーし**、[チーム] ページの [ボット アプリケーション **ID]** **フィールドに貼り設定** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-231">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="f357c-232">[新しい **パスワードの生成] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-232">Select the **Generate New Password** button.</span></span> <span data-ttu-id="f357c-233">生成されたパスワードをコピーし、[チーム] ページの [**ボット アプリケーション** パスワード **] フィールドに貼り設定** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-233">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="f357c-234">フォームの下部までスクロールし、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-234">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="f357c-235">アプリケーション ID とパスワードを生成すると、次にボットを Azure に展開します。</span><span class="sxs-lookup"><span data-stu-id="f357c-235">As you generated your Application ID and Password, next step is to deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f357c-236">[Azure **に展開する**] ボタンを選択し、必要な情報 (ボット アプリケーション ID、ボット アプリケーション パスワード、Moodle シークレットなど) を含むフォームをチーム 設定 ページ **に入力** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-236">Select the **Deploy to Azure** button and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password and the Moodle Secret are on the **Team Settings** page.</span></span> <span data-ttu-id="f357c-237">Azure の情報は、[セットアップ] **ページに表示** されます)。</span><span class="sxs-lookup"><span data-stu-id="f357c-237">The Azure information is on the **Setup** page).</span></span> 
> * <span data-ttu-id="f357c-238">フォームが完成した後、チェック ボックスをオンにして、利用規約に同意します。</span><span class="sxs-lookup"><span data-stu-id="f357c-238">After completing the form, select the check box to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="f357c-239">[購入] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-239">Select the **Purchase** button.</span></span> <span data-ttu-id="f357c-240">すべての Azure リソースが無料層に展開されます。</span><span class="sxs-lookup"><span data-stu-id="f357c-240">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="f357c-241">リソースが Azure への展開を完了したら、メッセージング エンドポイントを使用してMicrosoft 365 Moodle プラグインを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-241">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugin with a messaging endpoint.</span></span> <span data-ttu-id="f357c-242">Azure でボットからエンドポイントを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-242">You must get the endpoint from your bot in Azure:</span></span>

<span data-ttu-id="f357c-243">**メッセージング エンドポイントMicrosoft 365 Moodle プラグインを構成する**</span><span class="sxs-lookup"><span data-stu-id="f357c-243">**Configure the Microsoft 365 Moodle plugin with a messaging endpoint**</span></span>  
1. <span data-ttu-id="f357c-244">[Azure portal](https://portal.azure.com) にサインインします。</span><span class="sxs-lookup"><span data-stu-id="f357c-244">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="f357c-245">左側のウィンドウで、[リソース グループ **] を** 選択し、ボットの展開中に使用または作成したリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-245">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="f357c-246">グループ内 **のリソースの一** 覧から WebApp Bot リソースを選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-246">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="f357c-247">[概要 **] セクションからメッセージング** エンドポイント **をコピー** します。</span><span class="sxs-lookup"><span data-stu-id="f357c-247">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="f357c-248">Moodle で、使用している **Moodle プラグイン設定**[チーム] ページMicrosoft 365開きます。</span><span class="sxs-lookup"><span data-stu-id="f357c-248">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugin.</span></span>

1. <span data-ttu-id="f357c-249">[ボット **エンドポイント] フィールド** に、コピーした URL を貼り付け、単語メッセージを *webhook に変更します*。 </span><span class="sxs-lookup"><span data-stu-id="f357c-249">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="f357c-250">URL は次のように表示されます。 `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="f357c-250">The URL should now appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="f357c-251">[変更 **の保存] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-251">Select **Save Changes**.</span></span>

1. <span data-ttu-id="f357c-252">変更を保存した後、[**チーム**] タブ設定戻り、[マニフェスト ファイルのダウンロード] ボタンを選択し、さらに使用するためにアプリ マニフェスト パッケージをコンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="f357c-252">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="f357c-253">4. アプリをMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="f357c-253">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="f357c-254">ボットが Azure に展開され、Moodle サーバーと話をするように構成された後、アプリを展開するMicrosoft Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="f357c-254">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="f357c-255">これを行うには、前の手順の [ムードル プラグイン チーム] ページからダウンロードMicrosoft 365アプリ マニフェスト 設定読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-255">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugin Team Settings page in the previous step.</span></span>

<span data-ttu-id="f357c-256">アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-256">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="f357c-257">これを行うには、「テナントの準備」の[「Teams」の手順Microsoft 365従](../concepts/build-and-test/prepare-your-o365-tenant.md)います。</span><span class="sxs-lookup"><span data-stu-id="f357c-257">To do so, you can follow the steps in the Teams [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md) documentation.</span></span> <span data-ttu-id="f357c-258">次の手順を実行して、アプリを展開できます。</span><span class="sxs-lookup"><span data-stu-id="f357c-258">You can perform th the following steps to deploy your app:</span></span> 

<span data-ttu-id="f357c-259">**アプリを展開するには**</span><span class="sxs-lookup"><span data-stu-id="f357c-259">**To deploy your app**</span></span>

1. <span data-ttu-id="f357c-260">[ファイル **Microsoft Teams] を開きます**。</span><span class="sxs-lookup"><span data-stu-id="f357c-260">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="f357c-261">ナビゲーション バー **の** 左下の領域にある [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-261">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="f357c-262">オプションの **アップロードからカスタム アプリ** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-262">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f357c-263">グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。それ以外の場合は、メンバーであるチームのアプリのみを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-263">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="f357c-264">以前に `manifest.zip` ダウンロードしたパッケージを選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-264">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="f357c-265">アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle のプラグイン構成ページの [チーム 設定] タブからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="f357c-265">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugin configuration page in Moodle.</span></span>

<span data-ttu-id="f357c-266">アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="f357c-266">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="f357c-267">これを行うには、チャネルに移動し、 **プラス記号** (➕) を選択し、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-267">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="f357c-268">プロンプトに従って、チャネルへの Moodle コース タブの追加を完了します。</span><span class="sxs-lookup"><span data-stu-id="f357c-268">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="f357c-269">5. [自動作成] ウィンドウで [Moodle] タブをMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="f357c-269">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="f357c-270">[Moodle] タブは、Microsoft Teamsで手動で作成しますが、チームがコース同期から作成されると、自動的に作成できます。</span><span class="sxs-lookup"><span data-stu-id="f357c-270">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to have them automatically created when teams are created from course synchronization.</span></span> <span data-ttu-id="f357c-271">これを行うには、Moodle でアップロードされたアプリの ID をMicrosoft Teamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f357c-271">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle:</span></span>

1. <span data-ttu-id="f357c-272">Microsoft Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="f357c-272">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="f357c-273">ナビゲーション バーの左下の領域から [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="f357c-273">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="f357c-274">アップロードした **Moodle アプリを見つけて➡** オプション アイコン **を** 選択し➡コピー リンクを **選択します**。</span><span class="sxs-lookup"><span data-stu-id="f357c-274">Locate the uploaded **Moodle app** ➡ select the **options** icon ➡ select **copy link**.</span></span>

1. <span data-ttu-id="f357c-275">テキスト エディターで、コピーしたコンテンツを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="f357c-275">In a text editor, paste the copied content.</span></span> <span data-ttu-id="f357c-276">これは、ht ファイルなどの URL を含&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。</span><span class="sxs-lookup"><span data-stu-id="f357c-276">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="f357c-277">URL の最後の部分 (アプリの ID など) `00112233-4455-6677-8899-aabbccddeeff` をMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="f357c-277">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="f357c-278">Moodle で、[Moodle プラグインの構成 **] Teams** ページから [ムードル アプリMicrosoft 365] タブを開きます。</span><span class="sxs-lookup"><span data-stu-id="f357c-278">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugin configuration page.</span></span>

1. <span data-ttu-id="f357c-279">アプリの ID を [Moodle Microsoft Teams ID] フィールドに貼り付け、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="f357c-279">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="f357c-280">Moodle コースが同期されている場合、Microsoft Teams は自動的にチームに Moodle アプリをインストールし、Teams の [全般] チャネルに [Moodle] タブを作成し、同期する Moodle コースのコース ページを含む構成を行います。</span><span class="sxs-lookup"><span data-stu-id="f357c-280">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, create a Moodle tab in the General channel of Teams, and configure it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="f357c-281">これで、お客様の Moodle コースの操作を、お客様のアカウントから直接Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="f357c-281">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

<span data-ttu-id="f357c-282">機能の要求やフィードバックを共有するには、User Voice [ページをご覧ください](https://microsoftteams.uservoice.com/forums/916759-moodle)。</span><span class="sxs-lookup"><span data-stu-id="f357c-282">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="f357c-283">関連項目</span><span class="sxs-lookup"><span data-stu-id="f357c-283">See also</span></span>

- [<span data-ttu-id="f357c-284">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="f357c-284">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

- [<span data-ttu-id="f357c-285">Moodle</span><span class="sxs-lookup"><span data-stu-id="f357c-285">Moodle</span></span>](https://moodle.org/)

- <span data-ttu-id="f357c-286">[Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="f357c-286">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>
