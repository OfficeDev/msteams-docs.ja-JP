---
title: Moodle LMS のインストール
description: Microsoft Teams 用の Moodle 統合アプリをインストールして構成する方法
keywords: Teams Moodle アプリ統合プラグイン
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 091192054c5add7cfbdc1e7baabc86e34cef7631
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020593"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="227db-104">Moodle LMS のインストール</span><span class="sxs-lookup"><span data-stu-id="227db-104">Install Moodle LMS</span></span>

<span data-ttu-id="227db-105">Moodle は、一般的なオープン ソース学習管理システム (LMS) です。</span><span class="sxs-lookup"><span data-stu-id="227db-105">Moodle is a popular open-source Learning Management System (LMS).</span></span> <span data-ttu-id="227db-106">これで、Microsoft Teams と統合されました。</span><span class="sxs-lookup"><span data-stu-id="227db-106">It is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="227db-107">この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をし、Teams 内で直接通知を更新できます。</span><span class="sxs-lookup"><span data-stu-id="227db-107">This integration helps educators and teachers to collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

<span data-ttu-id="227db-108">IT 管理者が簡単にこの統合をセットアップするために、オープンソースの Microsoft 365 Moodle Plugin は次の機能で更新されます。</span><span class="sxs-lookup"><span data-stu-id="227db-108">To help IT admins easily set-up this integration, open-source Microsoft 365 Moodle Plugin is updated with the following capabilities:</span></span>

* <span data-ttu-id="227db-109">[Azure Active Directory (Azure](https://azure.microsoft.com/services/active-directory/) Active Directory) を使用して Moodle サーバーを自動AD。</span><span class="sxs-lookup"><span data-stu-id="227db-109">Auto-registration of your Moodle server with [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).</span></span>
* <span data-ttu-id="227db-110">Moodle Assistant ボットの Azure への展開を 1 回クリックで行います。</span><span class="sxs-lookup"><span data-stu-id="227db-110">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
* <span data-ttu-id="227db-111">チームの自動プロビジョニングと、すべてのチーム登録の自動同期、または [Moodle コース] の選択が可能です。</span><span class="sxs-lookup"><span data-stu-id="227db-111">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
* <span data-ttu-id="227db-112">[Moodle] タブと [Moodle アシスタント ボット] を同期された各チームに自動インストールします。</span><span class="sxs-lookup"><span data-stu-id="227db-112">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>

<span data-ttu-id="227db-113">この統合で提供される機能の詳細については、「Microsoft Teams と [Moodle」を参照してください](https://education.microsoft.com/resource/3dffb3a8)。</span><span class="sxs-lookup"><span data-stu-id="227db-113">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="227db-114">前提条件</span><span class="sxs-lookup"><span data-stu-id="227db-114">Prerequisites</span></span>

<span data-ttu-id="227db-115">Moodle アプリケーションをインストールして構成するための前提条件を次に示します。</span><span class="sxs-lookup"><span data-stu-id="227db-115">Following are the prerequisites to install and configure the Moodle application:</span></span> 

1. <span data-ttu-id="227db-116">Moodle 管理者の資格情報。</span><span class="sxs-lookup"><span data-stu-id="227db-116">Moodle administrator credentials.</span></span>

1. <span data-ttu-id="227db-117">Azure AD資格情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="227db-117">Azure AD administrator credentials.</span></span>

1. <span data-ttu-id="227db-118">新しいリソースを作成できる Azure サブスクリプション。</span><span class="sxs-lookup"><span data-stu-id="227db-118">An Azure subscription where you can create new resources.</span></span>

<span data-ttu-id="227db-119">**Moodle アプリケーションをインストールして構成するには**</span><span class="sxs-lookup"><span data-stu-id="227db-119">**To install and configure the Moodle application**</span></span> 

<span data-ttu-id="227db-120">次の手順を実行して、Moodle アプリケーションをインストールして構成します。</span><span class="sxs-lookup"><span data-stu-id="227db-120">Perform the following steps to install and configure the Moodle application:</span></span> 

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="227db-121">1. Microsoft 365 Moodle プラグインをインストールする</span><span class="sxs-lookup"><span data-stu-id="227db-121">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="227db-122">Microsoft Teams での Moodle の統合には、オープンソース [の Microsoft 365 Moodle プラグイン セットが搭載されています](https://github.com/Microsoft/o365-moodle)。</span><span class="sxs-lookup"><span data-stu-id="227db-122">The Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugin set](https://github.com/Microsoft/o365-moodle).</span></span> <span data-ttu-id="227db-123">Moodle サーバーにプラグインをインストールするには、次のアプリケーションがインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-123">To install the plugin in your Moodle server you must have the following applications installed:</span></span>

1. <span data-ttu-id="227db-124">現在 [の安定版の Moodle](https://download.moodle.org/releases/latest/)です。</span><span class="sxs-lookup"><span data-stu-id="227db-124">A [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="227db-125">Moodle [OpenID Connect と](https://moodle.org/plugins/auth_oidc) [Microsoft 365 統合](https://moodle.org/plugins/local_o365) プラグインがダウンロードされ、ローカル コンピューターに保存されます。</span><span class="sxs-lookup"><span data-stu-id="227db-125">The Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins downloaded and saved to your local computer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="227db-126">Teams の統合には、OpenID Connect プラグインと Microsoft 365 統合プラグインのインストールが必要です。</span><span class="sxs-lookup"><span data-stu-id="227db-126">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span> <span data-ttu-id="227db-127">さらに [、Microsoft 365 Teams テーマ](https://moodle.org/plugins/theme_boost_o365teams) プラグインを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="227db-127">Additionally, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugin is highly recommended.</span></span>

1. <span data-ttu-id="227db-128">管理者として Moodle サーバーにサインインし、左側のナビゲーション パネルにある[[](https://docs.moodle.org/22/en/Settings_block)設定] ブロックから [サイトの管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-128">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="227db-129">[プラグイン] **タブを選択** し、[プラグインのインストール **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-129">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="227db-130">[ZIP ファイル **からプラグインをインストールする] セクションで、[** ファイルの **選択] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-130">From the **Install plugin from ZIP file** section, select **Choose a file** button.</span></span>

1. <span data-ttu-id="227db-131">左側 **のナビゲーションから [ファイルの** アップロード] オプションを選択し、ダウンロードしたファイルを参照して、[このファイルのアップロード **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-131">Select **Upload a file** option from the left navigation, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="227db-132">左側の **ナビゲーション パネルから** [サイトの管理] を選択して、管理ダッシュボードに戻ります。</span><span class="sxs-lookup"><span data-stu-id="227db-132">Select the **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="227db-133">[ローカル プラグイン] まで **下にスクロールし、[Microsoft** **365 統合** ] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-133">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span> 

> [!IMPORTANT]
>
> * <span data-ttu-id="227db-134">プロセス全体を通してこの一連のページに戻る必要がある場合は、Microsoft 365 Moodle Plugin 構成ページを別のブラウザー タブで開いた状態にしてください。</span><span class="sxs-lookup"><span data-stu-id="227db-134">Keep your Microsoft 365 Moodle Plugin configuration page open in a separate browser tab as you have to  return to this set of pages throughout the process.</span></span>  <br/><br/>
> * <span data-ttu-id="227db-135">既存の Moodle サイトをお持ちではない場合は、Azure [repo](https://github.com/azure/moodle) で Moodle をチェックアウトして、Moodle インスタンスをすばやく展開し、ニーズに合わせてカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="227db-135">If you do not have an existing Moodle site, you can check out Moodle on Azure [repo](https://github.com/azure/moodle) where you can quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a><span data-ttu-id="227db-136">2. Microsoft 365 プラグインと Azure Active Directory の間の接続を構成する (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="227db-136">2. Configure the connection between the Microsoft 365 plugin and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="227db-137">Moodle を Azure サーバーにアプリケーションとして登録するAD。</span><span class="sxs-lookup"><span data-stu-id="227db-137">You must register Moodle as an application in your Azure AD.</span></span> <span data-ttu-id="227db-138">PowerShell スクリプトを使用してこのプロセスを完了します。</span><span class="sxs-lookup"><span data-stu-id="227db-138">Use PowerShell script to complete this process.</span></span> <span data-ttu-id="227db-139">PowerShell スクリプトは、Microsoft 365 Moodle プラグインAD使用する Microsoft 365 テナント用の新しい Azure AD アプリケーションを準備します。</span><span class="sxs-lookup"><span data-stu-id="227db-139">The PowerShell script provisions a new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="227db-140">スクリプトは、Microsoft 365 テナント用にアプリをプロビジョニングし、プロビジョニングされたアプリに必要な返信 URL とアクセス許可を設定し、および `AppID` を返します `Key` 。</span><span class="sxs-lookup"><span data-stu-id="227db-140">The script provisions the app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and return the `AppID` and `Key`.</span></span> <span data-ttu-id="227db-141">生成された Microsoft `AppID` 365 Moodle Plugin セットアップ ページを使用して、Azure サーバー を使用して Moodle サーバー サイトを構成 `Key` AD。</span><span class="sxs-lookup"><span data-stu-id="227db-141">You can use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugin setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="227db-142">PowerShell スクリプトは最新の構成項目で更新されないので、Moodle [3.8.0.4 および 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) および [3.8.0.5 および 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って構成を手動で完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-142">The PowerShell script is not updated with the latest configuration items, so you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span> </br></br>
> * <span data-ttu-id="227db-143">PowerShell スクリプトが自動化している手動手順の詳細については、「アプリケーションとして Moodle インスタンスを登録する [」を参照してください](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。</span><span class="sxs-lookup"><span data-stu-id="227db-143">To view the manual steps that the PowerShell script is automating in detail, see [Register your Moodle instance as an Application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="227db-144">Microsoft Teams 情報フローの [Moodle] タブ</span><span class="sxs-lookup"><span data-stu-id="227db-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="227db-145">[Microsoft 365 統合プラグイン] ページで、[セットアップ] タブ **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-145">From the Microsoft 365 Integration plugin page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="227db-146">**[PowerShell スクリプトのダウンロード] ボタンを** 選択し、ローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="227db-146">Select the **Download PowerShell Script** button and save it to your local computer.</span></span>

1. <span data-ttu-id="227db-147">ZIP ファイルから PowerShell スクリプトを準備する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-147">You must prepare the PowerShell script from the ZIP file.</span></span> <span data-ttu-id="227db-148">ZIP ファイルから PowerShell スクリプトを準備するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="227db-148">Perform the following steps to prepare the PowerShell script from the ZIP file:</span></span>

    1. <span data-ttu-id="227db-149">ファイルをダウンロードして抽出 `Moodle-AzureAD-Powershell.zip` します。</span><span class="sxs-lookup"><span data-stu-id="227db-149">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="227db-150">抽出したフォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="227db-150">Open the extracted folder.</span></span>
    1. <span data-ttu-id="227db-151">ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` プロパティ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-151">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="227db-152">[プロパティ **] ウィンドウの**[全般] タブで、ウィンドウの下部にある Security 属性の横にあるボックス `Unblock` をオンにします。</span><span class="sxs-lookup"><span data-stu-id="227db-152">Under the **General** tab of the Properties window, check the `Unblock` box next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="227db-153">[**OK**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-153">Select **OK**.</span></span>
    1. <span data-ttu-id="227db-154">ディレクトリ パスを抽出したフォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="227db-154">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="227db-155">管理者として PowerShell を実行します。</span><span class="sxs-lookup"><span data-stu-id="227db-155">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="227db-156">[開始] を選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-156">Select Start.</span></span>
    1. <span data-ttu-id="227db-157">「PowerShell」と入力します。</span><span class="sxs-lookup"><span data-stu-id="227db-157">Type PowerShell.</span></span>
    1. <span data-ttu-id="227db-158">[ファイル] を右クリックWindows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="227db-158">Right-click Windows PowerShell.</span></span>
    1. <span data-ttu-id="227db-159">[管理者 **として実行] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-159">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="227db-160">ディレクトリへのパスを where と入力して、未設定 `cd .../.../Moodle-AzureAD-Powershell` `.../...` のディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="227db-160">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="227db-161">PowerShell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="227db-161">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="227db-162">を `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 入力します。</span><span class="sxs-lookup"><span data-stu-id="227db-162">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="227db-163">を `./Moodle-AzureAD-Script.ps1` 入力します。</span><span class="sxs-lookup"><span data-stu-id="227db-163">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="227db-164">ポップアップ ウィンドウで Microsoft 365 管理者アカウントにサインインします。</span><span class="sxs-lookup"><span data-stu-id="227db-164">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="227db-165">Azure AD アプリケーションの名前 (例: Moodle/Moodle プラグイン) を入力します。</span><span class="sxs-lookup"><span data-stu-id="227db-165">Enter the name of the Azure AD Application (e.g., Moodle/Moodle plugin).</span></span>
    1. <span data-ttu-id="227db-166">Moodle サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="227db-166">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="227db-167">スクリプトによって **生成された** アプリケーション ID と **アプリケーション キー** をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="227db-167">Copy the **Application ID** and **Application Key** generated by the script and save them.</span></span>

1. <span data-ttu-id="227db-168">次に、Microsoft `AppID` `Key` 365 Moodle プラグインとを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-168">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="227db-169">プラグインの管理ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="227db-169">Return to the plugin administration page.</span></span> <span data-ttu-id="227db-170">フローは、サイト管理と➡ Microsoft 365 ➡管理です。</span><span class="sxs-lookup"><span data-stu-id="227db-170">The flow is: Site administration ➡ Plugins ➡ Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="227db-171">[セットアップ **] タブで** 、前にコピーした **アプリケーション ID** と **アプリケーション** キーを追加し、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-171">On the **Setup** tab add the **Application ID** and **Application Key** you copied previously, then select **Save changes**.</span></span>

1. <span data-ttu-id="227db-172">ページが更新された後、新しいセクション [接続方法の選択 **] が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="227db-172">After the page refreshes, you can see a new section **Choose connection method**.</span></span> <span data-ttu-id="227db-173">[既定値] というラベルの **付いたチェック ボックスをオン** にし、[変更の **保存] を再度選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-173">Select the checkbox labeled **Default** and then select **Save changes** again.</span></span>

1. <span data-ttu-id="227db-174">ページが更新された後、別の新しいセクション [管理者の同意] が表示 **され&情報が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="227db-174">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="227db-175">[ **管理者の同意の提供** ] リンクを選択し、Microsoft 365 グローバル管理者資格情報を入力し、[ **承諾** ] を選択してアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="227db-175">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="227db-176">[Azure ADテナント] **フィールドの横** にある [検出] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-176">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="227db-177">**OneDrive for Business URL の横にある [** 検出] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-177">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="227db-178">フィールドが設定された後、もう一度 [変更の **保存] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-178">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="227db-179">[更新] **ボタンを** 選択してインストールを確認し、[変更の保存 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-179">Select the **Update** button to verify the installation, then **Save changes**.</span></span>

1. <span data-ttu-id="227db-180">Moodle サーバーと Azure サーバー間でユーザーを同期AD。</span><span class="sxs-lookup"><span data-stu-id="227db-180">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="227db-181">環境に応じて、この段階でさまざまなオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="227db-181">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="227db-182">次の手順をお試しください。</span><span class="sxs-lookup"><span data-stu-id="227db-182">To get started:</span></span>
    1. <span data-ttu-id="227db-183">[同期の設定 **] タブに切り替える**</span><span class="sxs-lookup"><span data-stu-id="227db-183">Switch to the **Sync Settings tab**</span></span>
    1. <span data-ttu-id="227db-184">[Azure **ユーザーとユーザーを同期AD]** セクションで、環境に適用するチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="227db-184">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="227db-185">次の項目を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-185">You must select the following:</span></span>  

        <span data-ttu-id="227db-186">✔ Azure のユーザー向け Moodle でアカウントを作成AD。</span><span class="sxs-lookup"><span data-stu-id="227db-186">✔ Create accounts in Moodle for users in Azure AD .</span></span> 
        <span data-ttu-id="227db-187">✔ Azure アカウントのユーザーに対して、Moodle のすべてのアカウントを更新AD。</span><span class="sxs-lookup"><span data-stu-id="227db-187">✔ Update all accounts in Moodle for users in Azure AD.</span></span>  

    1. <span data-ttu-id="227db-188">[ユーザー **作成の制限] セクション** で、Moodle に同期AD Azure ユーザーを制限するフィルターをセットアップできます。</span><span class="sxs-lookup"><span data-stu-id="227db-188">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="227db-189">[ **ユーザー フィールド マッピング]** セクションでは、Azure のユーザー プロファイルADを Moodle ユーザー プロファイル フィールド マッピングにカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="227db-189">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="227db-190">[Teams **の同期]** セクションで、既存の Moodle コースの一部またはすべてについて、チームなどのグループを自動的に作成するために選択できます。</span><span class="sxs-lookup"><span data-stu-id="227db-190">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

> [!NOTE]
> <span data-ttu-id="227db-191">Moodle [Cron はタスク](https://docs.moodle.org/310/en/Cron) スケジュールに従って実行されます。</span><span class="sxs-lookup"><span data-stu-id="227db-191">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="227db-192">既定のスケジュールは 1 日 1 回です。</span><span class="sxs-lookup"><span data-stu-id="227db-192">The default schedule is once a day.</span></span> <span data-ttu-id="227db-193">ただし、すべての同期を維持するには、cron の実行頻度を高くする必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-193">However, the cron must run more frequently to keep everything in sync.</span></span>

13. <span data-ttu-id="227db-194">cron ジョブ [を検証し](https://docs.moodle.org/310/en/Cron)、最初の実行に対して手動で実行するには **、[Azure** とユーザーを同期する] セクションの [スケジュールされたタスクの管理] ADします。</span><span class="sxs-lookup"><span data-stu-id="227db-194">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="227db-195">これにより、[スケジュールされたタスク] **ページに移動** します。</span><span class="sxs-lookup"><span data-stu-id="227db-195">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="227db-196">下にスクロールして、Azure ユーザーと **同期するジョブをADし、[今すぐ** 実行] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-196">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="227db-197">既存のコースに基づいてグループを作成する場合は **、Microsoft 365** ジョブでユーザー グループの作成を実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="227db-197">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

1. <span data-ttu-id="227db-198">プラグインの管理ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="227db-198">Return to the plugin administration page.</span></span> <span data-ttu-id="227db-199">ナビゲーション フローは、サイト管理➡ Microsoft 365 Integratio ➡プラグインです。</span><span class="sxs-lookup"><span data-stu-id="227db-199">The navigation flow is: Site administration ➡ Plugins ➡ Microsoft 365 Integratio.</span></span> <span data-ttu-id="227db-200">次に、[Teams の設定 **] ページを選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-200">Then, select the **Teams Settings** page.</span></span> <span data-ttu-id="227db-201">Teams アプリの統合を有効にするには、いくつかの設定を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-201">You must configure some settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="227db-202">**OpenID Connect を有効にするには**、[認証の管理] リンクを選択し、灰色で表示されている **場合は、OpenId Connect** 行の目のアイコンを選択します。 </span><span class="sxs-lookup"><span data-stu-id="227db-202">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="227db-203">フレームの埋め込みを有効にする。</span><span class="sxs-lookup"><span data-stu-id="227db-203">Enable frame embedding.</span></span> <span data-ttu-id="227db-204">**[HTTP セキュリティ] リンクを選択** し、[フレームの埋め込みを許可する] の **横にあるチェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="227db-204">Select the **HTTP Security** link, then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="227db-205">Moodle API 機能を有効にする Web サービスを有効にする。</span><span class="sxs-lookup"><span data-stu-id="227db-205">Enable web services which enables the Moodle API features.</span></span> <span data-ttu-id="227db-206">[高度 **な機能] リンクを** 選択し、[Web サービスを有効にする] の横にある **チェック ボックスがオンになっていることを** 確認します。</span><span class="sxs-lookup"><span data-stu-id="227db-206">Select the **Advanced Features** link, then make sure the checkbox next to **Enable web services** is checked.</span></span>
    1. <span data-ttu-id="227db-207">Microsoft 365 の外部サービスを有効にする。</span><span class="sxs-lookup"><span data-stu-id="227db-207">Enable the external services for Microsoft 365.</span></span> <span data-ttu-id="227db-208">次に、[ **外部サービス] リンク** を選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-208">Select the **External services** link then next:</span></span>  

        <span data-ttu-id="227db-209">✔ **[Moodle Microsoft 365 Webservices] 行で [編集] を選択** します。 </span><span class="sxs-lookup"><span data-stu-id="227db-209">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>  
        <span data-ttu-id="227db-210">✔ [有効] の横にあるチェック ボックスを **オンにし、[** 変更の保存] **を選択します。**</span><span class="sxs-lookup"><span data-stu-id="227db-210">✔ Mark the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="227db-211">認証されたユーザーのアクセス許可を編集して、Web サービス トークンの作成を許可します。</span><span class="sxs-lookup"><span data-stu-id="227db-211">Edit your authenticated user permissions to allow them to create web service tokens.</span></span> <span data-ttu-id="227db-212">[編集] **役割の [認証されたユーザー] リンクを選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-212">Select the **Editing role 'Authenticated user'** link.</span></span> <span data-ttu-id="227db-213">下にスクロールして、[Web サービス **トークンの作成] 機能を見** つけて、[許可] チェック ボックス **をオン** にします。</span><span class="sxs-lookup"><span data-stu-id="227db-213">Scroll down and find the **Create a web service token** capability and mark the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="227db-214">3. Moodle アシスタント ボットを Azure に展開する</span><span class="sxs-lookup"><span data-stu-id="227db-214">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="227db-215">Microsoft Teams の無料の Moodle アシスタント ボットは、教師と学生が Moodle のコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="227db-215">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades and other information in Moodle.</span></span> <span data-ttu-id="227db-216">ボットは、Teams 内の学生と教師にも、Moodle 通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="227db-216">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="227db-217">ボットは、Microsoft が管理するオープン ソース プロジェクトであり [、GitHub で利用できます](https://github.com/microsoft/Moodle-Teams-Bot)。</span><span class="sxs-lookup"><span data-stu-id="227db-217">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
> * <span data-ttu-id="227db-218">このセクションでは、リソースを Azure サブスクリプションに展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-218">In this section you must deploy resources to your Azure subscription.</span></span> <span data-ttu-id="227db-219">無料レベルを使用して構成されたすべての **リソース ウェア** 。</span><span class="sxs-lookup"><span data-stu-id="227db-219">All resources ware configured using the **free** tier.</span></span> <span data-ttu-id="227db-220">ボットの使用状況に応じて、これらのリソースをスケーリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-220">Depending on the usage of your bot, you mhave to scale these resources.</span></span>
> * <span data-ttu-id="227db-221">ボットなしで [Moodle] タブを使用するには [、4 にスキップします](#4-deploy-your-microsoft-teams-app)。</span><span class="sxs-lookup"><span data-stu-id="227db-221">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="227db-222">Moodle ボットの情報フロー</span><span class="sxs-lookup"><span data-stu-id="227db-222">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="227db-223">ボットをインストールするには、Microsoft Identity Platform に [ボットを登録する必要があります](https://identity.microsoft.com/Landing)。</span><span class="sxs-lookup"><span data-stu-id="227db-223">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="227db-224">これにより、ボットは Microsoft エンドポイントに対して認証できます。</span><span class="sxs-lookup"><span data-stu-id="227db-224">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="227db-225">**ボットを登録するには:**</span><span class="sxs-lookup"><span data-stu-id="227db-225">**To register your bot**:</span></span>

1. <span data-ttu-id="227db-226">プラグインの管理ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="227db-226">Go to the plugin administration page.</span></span> <span data-ttu-id="227db-227">[プラグイン **] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="227db-227">Go to **Plugins**.</span></span> <span data-ttu-id="227db-228">[Microsoft **365 Integration] で、[Teams** の設定] **タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-228">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="227db-229">[Microsoft **アプリケーション登録ポータル] リンクを選択** し、Microsoft ID でサインインします。</span><span class="sxs-lookup"><span data-stu-id="227db-229">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="227db-230">アプリの名前 (MoodleBot など) を入力し、[作成] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-230">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="227db-231">アプリケーション ID **をコピーし** 、[チームの設定] ページの **[ボット アプリケーション ID]** フィールド **に貼り付** けます。</span><span class="sxs-lookup"><span data-stu-id="227db-231">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="227db-232">[新しい **パスワードの生成] ボタンを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-232">Select the **Generate New Password** button.</span></span> <span data-ttu-id="227db-233">生成されたパスワードをコピーし、[チームの設定] ページの [ **ボット アプリケーション** パスワード] フィールド **に貼り付** けます。</span><span class="sxs-lookup"><span data-stu-id="227db-233">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="227db-234">フォームの下部までスクロールし、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-234">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="227db-235">アプリケーション ID とパスワードを生成すると、次にボットを Azure に展開します。</span><span class="sxs-lookup"><span data-stu-id="227db-235">As you generated your Application ID and Password, next step is to deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="227db-236">[Azure **に展開]** ボタンを選択し、ボット アプリケーション ID、ボット アプリケーション パスワード、Moodle シークレットなどの必要な情報を含むフォームに入力します。[チームの設定] ページに **表示** されます。</span><span class="sxs-lookup"><span data-stu-id="227db-236">Select the **Deploy to Azure** button and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password and the Moodle Secret are on the **Team Settings** page.</span></span> <span data-ttu-id="227db-237">Azure の情報は、[セットアップ] **ページに表示** されます)。</span><span class="sxs-lookup"><span data-stu-id="227db-237">The Azure information is on the **Setup** page).</span></span> 
> * <span data-ttu-id="227db-238">フォームが完成した後、チェック ボックスをオンにして、利用規約に同意します。</span><span class="sxs-lookup"><span data-stu-id="227db-238">After completing the form, select the check box to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="227db-239">[購入] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="227db-239">Select the **Purchase** button.</span></span> <span data-ttu-id="227db-240">すべての Azure リソースが無料層に展開されます。</span><span class="sxs-lookup"><span data-stu-id="227db-240">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="227db-241">リソースが Azure への展開を完了したら、メッセージング エンドポイントを使用して Microsoft 365 Moodle プラグインを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-241">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugin with a messaging endpoint.</span></span> <span data-ttu-id="227db-242">Azure でボットからエンドポイントを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-242">You must get the endpoint from your bot in Azure:</span></span>

<span data-ttu-id="227db-243">**メッセージング エンドポイントを使用して Microsoft 365 Moodle プラグインを構成する**</span><span class="sxs-lookup"><span data-stu-id="227db-243">**Configure the Microsoft 365 Moodle plugin with a messaging endpoint**</span></span>  
1. <span data-ttu-id="227db-244">[Azure portal](https://portal.azure.com) にサインインします。</span><span class="sxs-lookup"><span data-stu-id="227db-244">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="227db-245">左側のウィンドウで、[リソース グループ **] を** 選択し、ボットの展開中に使用または作成したリソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-245">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="227db-246">グループ内 **のリソースの一** 覧から WebApp Bot リソースを選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-246">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="227db-247">[概要 **] セクションからメッセージング** エンドポイント **をコピー** します。</span><span class="sxs-lookup"><span data-stu-id="227db-247">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="227db-248">Moodle で、Microsoft  365 Moodle プラグインの [チーム設定] ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="227db-248">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugin.</span></span>

1. <span data-ttu-id="227db-249">[ボット **エンドポイント] フィールド** に、コピーした URL を貼り付け、単語メッセージを *webhook に変更します*。 </span><span class="sxs-lookup"><span data-stu-id="227db-249">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="227db-250">URL は次のように表示されます。 `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="227db-250">The URL should now appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="227db-251">[変更 **の保存] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-251">Select **Save Changes**.</span></span>

1. <span data-ttu-id="227db-252">変更を保存した後、[チームの設定] タブに戻り、[マニフェスト ファイルのダウンロード] ボタンを選択し、さらに使用するためにアプリ マニフェスト パッケージをコンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="227db-252">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="227db-253">4. Microsoft Teams アプリを展開する</span><span class="sxs-lookup"><span data-stu-id="227db-253">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="227db-254">ボットが Azure に展開され、Moodle サーバーと話をするように構成した後、Microsoft Teams アプリを展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-254">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="227db-255">これを行うには、前の手順の [Microsoft 365 Moodle Plugin Team Settings] ページからダウンロードしたアプリ マニフェスト ファイルを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-255">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugin Team Settings page in the previous step.</span></span>

<span data-ttu-id="227db-256">アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-256">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="227db-257">これを行うには、「Teams Prepare your Microsoft [365 テナント」のドキュメントの手順に従](../concepts/build-and-test/prepare-your-o365-tenant.md) います。</span><span class="sxs-lookup"><span data-stu-id="227db-257">To do so, you can follow the steps in the Teams [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md) documentation.</span></span> <span data-ttu-id="227db-258">次の手順を実行して、アプリを展開できます。</span><span class="sxs-lookup"><span data-stu-id="227db-258">You can perform th the following steps to deploy your app:</span></span> 

<span data-ttu-id="227db-259">**アプリを展開するには**</span><span class="sxs-lookup"><span data-stu-id="227db-259">**To deploy your app**</span></span>

1. <span data-ttu-id="227db-260">**Microsoft Teams を開きます**。</span><span class="sxs-lookup"><span data-stu-id="227db-260">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="227db-261">ナビゲーション バー **の** 左下の領域にある [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-261">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="227db-262">オプションの **一覧から [カスタム アプリのアップロード** ] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-262">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="227db-263">グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。それ以外の場合は、メンバーであるチームのアプリのみを読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-263">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="227db-264">以前に `manifest.zip` ダウンロードしたパッケージを選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-264">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="227db-265">アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle のプラグイン構成ページの [ **チーム** 設定] タブからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="227db-265">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugin configuration page in Moodle.</span></span>

<span data-ttu-id="227db-266">アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="227db-266">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="227db-267">これを行うには、チャネルに移動し、 **プラス記号** (➕) を選択し、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-267">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="227db-268">プロンプトに従って、チャネルへの Moodle コース タブの追加を完了します。</span><span class="sxs-lookup"><span data-stu-id="227db-268">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="227db-269">5. Microsoft Teams で Moodle タブの自動作成を許可する</span><span class="sxs-lookup"><span data-stu-id="227db-269">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="227db-270">[Moodle] タブは Microsoft Teams で手動で作成しますが、チームがコース同期から作成されると、自動的に作成できます。</span><span class="sxs-lookup"><span data-stu-id="227db-270">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to have them automatically created when teams are created from course synchronization.</span></span> <span data-ttu-id="227db-271">これを行うには、アップロードされた Microsoft Teams アプリの ID を Moodle で構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="227db-271">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle:</span></span>

1. <span data-ttu-id="227db-272">Microsoft Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="227db-272">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="227db-273">ナビゲーション バーの左下の領域から [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="227db-273">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="227db-274">アップロードした **Moodle アプリを見つけて➡** オプション アイコン **を** 選択し➡コピー リンクを **選択します**。</span><span class="sxs-lookup"><span data-stu-id="227db-274">Locate the uploaded **Moodle app** ➡ select the **options** icon ➡ select **copy link**.</span></span>

1. <span data-ttu-id="227db-275">テキスト エディターで、コピーしたコンテンツを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="227db-275">In a text editor, paste the copied content.</span></span> <span data-ttu-id="227db-276">これは、ht ファイルなどの URL を含&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。</span><span class="sxs-lookup"><span data-stu-id="227db-276">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="227db-277">Url の最後の部分 (Microsoft Teams アプリの ID など)  `00112233-4455-6677-8899-aabbccddeeff` をコピーします。</span><span class="sxs-lookup"><span data-stu-id="227db-277">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="227db-278">Moodle で、Microsoft 365 **Moodle** プラグインの構成ページから [Teams Moodle アプリ] タブを開きます。</span><span class="sxs-lookup"><span data-stu-id="227db-278">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugin configuration page.</span></span>

1. <span data-ttu-id="227db-279">Microsoft Teams アプリの ID を [Moodle アプリ ID] フィールドに貼り付けて、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="227db-279">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="227db-280">Moodle コースを同期すると、Microsoft Teams は自動的にチームに Moodle アプリをインストールし、Teams の [全般] チャネルに [Moodle] タブを作成し、同期する Moodle コースのコース ページを含む構成を行います。</span><span class="sxs-lookup"><span data-stu-id="227db-280">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, create a Moodle tab in the General channel of Teams, and configure it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="227db-281">これで、Microsoft Teams から直接、Moodle コースの操作を開始できます。</span><span class="sxs-lookup"><span data-stu-id="227db-281">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

<span data-ttu-id="227db-282">機能の要求やフィードバックを共有するには、User Voice [ページをご覧ください](https://microsoftteams.uservoice.com/forums/916759-moodle)。</span><span class="sxs-lookup"><span data-stu-id="227db-282">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="227db-283">関連項目</span><span class="sxs-lookup"><span data-stu-id="227db-283">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="227db-284">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="227db-284">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="227db-285">Moodle</span><span class="sxs-lookup"><span data-stu-id="227db-285">Moodle</span></span>](https://moodle.org/)

> [!div class="nextstepaction"]
> <span data-ttu-id="227db-286">[Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="227db-286">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>
