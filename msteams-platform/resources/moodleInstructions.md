---
title: Microsoft Teams との取り組み
description: Microsoft Teams 用のLesle 統合アプリをインストールして構成する方法
keywords: Teams の Teams の Teams 用アプリ統合プラグイン
ms.topic: how-to
ms.author: lajanuar
author: laujan
ms.openlocfilehash: bb3de6b3897105ff3564ecd332cba28a0db85b0f
ms.sourcegitcommit: a16590b2ccc46e1b6d17cbb367762a3c16ff779c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2021
ms.locfileid: "50115742"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a><span data-ttu-id="1f942-104">Microsoft Teams との取り組み</span><span class="sxs-lookup"><span data-stu-id="1f942-104">Installing the Moodle integration with Microsoft Teams</span></span>

<span data-ttu-id="1f942-105">人気のあるオープン ソースの学習管理システム (LMS) である[Hedle](https://moodle.org/)は、Microsoft Teams と統合されました。</span><span class="sxs-lookup"><span data-stu-id="1f942-105">[Moodle](https://moodle.org/), a popular open-source Learning Management System (LMS), is now integrated with Microsoft Teams.</span></span> <span data-ttu-id="1f942-106">この統合により、教師と教師は、Teams 内で、レベルや課題に関する共同作業、成績や課題に関する質問、通知を直接使用して最新の情報を得る際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="1f942-106">This integration helps educators and teachers collaborate around Moodle courses, ask questions about grades and assignments, and stay updated with notifications directly within Teams.</span></span>

<span data-ttu-id="1f942-107">IT 管理者が簡単にこの統合をセットアップするために、Microsoft 365 のオープン ソースの、次の機能を備える、Microsoft 365 のグループプラグインを更新しました。</span><span class="sxs-lookup"><span data-stu-id="1f942-107">To help IT admins easily set this integration up, we have updated our open-source Microsoft 365 Moodle Plugin with the following capabilities:</span></span>

* <span data-ttu-id="1f942-108">[Azure Active Directory (Azure](https://azure.microsoft.com/services/active-directory/) AD) を使用して、使用しているのが、使用しているのが、Azure Active Directory サーバーの自動登録AD。</span><span class="sxs-lookup"><span data-stu-id="1f942-108">Auto-registration of your Moodle server with [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).</span></span>
* <span data-ttu-id="1f942-109">Azure への、1 回のクリックで、あなたのLesure アシスタント ボットの展開を行います。</span><span class="sxs-lookup"><span data-stu-id="1f942-109">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
* <span data-ttu-id="1f942-110">チームの自動プロビジョニングと、すべてのチーム登録の自動同期、または選択した 、すべての Teams コースに対する Teams 登録の自動同期。</span><span class="sxs-lookup"><span data-stu-id="1f942-110">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
* <span data-ttu-id="1f942-111">同期された各チームに、[リキードル] タブと [リキードル アシスタント ボット] を自動インストールします。</span><span class="sxs-lookup"><span data-stu-id="1f942-111">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>

<span data-ttu-id="1f942-112">この統合が提供する機能の詳細については[、Microsoft Teams との「リピドル」を参照してください](https://education.microsoft.com/resource/3dffb3a8)。</span><span class="sxs-lookup"><span data-stu-id="1f942-112">To learn more about the functionality this integration provides, please *see* [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f942-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="1f942-113">Prerequisites</span></span>

<span data-ttu-id="1f942-114">このアプリケーションをインストールして構成するには、以下が必要です。</span><span class="sxs-lookup"><span data-stu-id="1f942-114">In order to install and configure this application you'll need:</span></span>

1. <span data-ttu-id="1f942-115">管理者の資格情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="1f942-115">Moodle administrator credentials.</span></span>

1. <span data-ttu-id="1f942-116">Azure AD管理者の資格情報。</span><span class="sxs-lookup"><span data-stu-id="1f942-116">Azure AD administrator credentials.</span></span>

1. <span data-ttu-id="1f942-117">新しいリソースを作成できる Azure サブスクリプション。</span><span class="sxs-lookup"><span data-stu-id="1f942-117">An Azure subscription where you can create new resources.</span></span>

## <a name="step-1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="1f942-118">手順 1: Microsoft 365 のLesle プラグインをインストールする</span><span class="sxs-lookup"><span data-stu-id="1f942-118">Step 1: Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="1f942-119">Microsoft Teams でのリムードルの統合は、オープン ソース [の Microsoft 365 のグループプラグイン セットによって動作します](https://github.com/Microsoft/o365-moodle)。</span><span class="sxs-lookup"><span data-stu-id="1f942-119">The Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugin set](https://github.com/Microsoft/o365-moodle).</span></span> <span data-ttu-id="1f942-120">このプラグインを使用する場合は、次のコードをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-120">To install the plugin in your Moodle server you need to have the following installed:</span></span>

1. <span data-ttu-id="1f942-121">現在 [安定しているバージョンのLesle](https://download.moodle.org/releases/latest/)。</span><span class="sxs-lookup"><span data-stu-id="1f942-121">A [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="1f942-122">ローカル コンピューターにダウンロードされ、保存された、近くの Microsoft 365 統合プラグインと、1 つの使い方を示す、使い方が分からない [OpenID](https://moodle.org/plugins/auth_oidc) Connect プラグインと [Microsoft 365](https://moodle.org/plugins/local_o365) 統合プラグイン。</span><span class="sxs-lookup"><span data-stu-id="1f942-122">The Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins downloaded and saved to your local computer.</span></span>

> [!NOTE]
> <span data-ttu-id="1f942-123">Teams 統合には、OpenID Connect プラグインと Microsoft 365 統合プラグインのインストールが必要です。</span><span class="sxs-lookup"><span data-stu-id="1f942-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span> <span data-ttu-id="1f942-124">さらに [、Microsoft 365 Teams テーマ プラグイン](https://moodle.org/plugins/theme_boost_o365teams) を強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1f942-124">Additionally the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugin is highly recommended.</span></span>

3. <span data-ttu-id="1f942-125">管理者として、使用しているグループのサーバーにログインし、左側のナビゲーション[](https://docs.moodle.org/22/en/Settings_block)パネルにある [設定] ブロックから [サイトの管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-125">Login to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="1f942-126">[プラグイン **] タブを選択** し、[プラグインのインストール **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-126">Select the **Plugins** tab, and then choose **Install plugins**.</span></span>

1. <span data-ttu-id="1f942-127">[ZIP ファイル **からのプラグインのインストール] セクションで** 、[ファイルの選択 **] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-127">Under the **Install plugin from ZIP file** section select the **Choose a file** button.</span></span>

1. <span data-ttu-id="1f942-128">左側の **ナビゲーションから [ファイルの** アップロード] オプションを選択し、上記でダウンロードしたファイルを参照して、[このファイルのアップロード **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-128">Select the **Upload a file** options from the left navigation, browse for the file you downloaded above, and choose **Upload this file**.</span></span>

1. <span data-ttu-id="1f942-129">左側の **ナビゲーション パネルから** [サイトの管理] オプションを選択して、管理ダッシュボードに戻ります。</span><span class="sxs-lookup"><span data-stu-id="1f942-129">Select the **Site administration** option from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="1f942-130">ローカル プラグインまで **下にスクロールし、Microsoft** **365 統合リンクを選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-130">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span> <span data-ttu-id="1f942-131">**インストール プロセスを通じて、この構成ページは別のブラウザー タブで開いた状態に保ちます**。</span><span class="sxs-lookup"><span data-stu-id="1f942-131">**Keep this configuration page open in a separate browser tab throughout the installation process**.</span></span>

<span data-ttu-id="1f942-132">詳細については、下書きドキュメントを参照 [してください](https://docs.moodle.org/34/en/Installing_plugins)。</span><span class="sxs-lookup"><span data-stu-id="1f942-132">You can find more information on how to install Moodle plugins in the [Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="1f942-133">Microsoft 365 の PageLe Plugin 構成ページは、別のブラウザー タブで開いた状態に保ちます。プロセスを通じて、この一連のページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="1f942-133">Keep your Microsoft 365 Moodle Plugin configuration page open in a separate browser tab — you'll be returning to this set of pages throughout the process.</span></span>  <br/><br/>
>* <span data-ttu-id="1f942-134">既存のLesure サイトをお持ちない場合は、Azure のレポで、お客様のニーズに合わせて、簡単に、また、そのインスタンスをカスタマイズできる、Azure の [Repo](https://github.com/azure/moodle) で、使い方を確認できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-134">If you don't have an existing Moodle site, you can check out Moodle on Azure [repo](https://github.com/azure/moodle) where you can quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="step-2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a><span data-ttu-id="1f942-135">手順 2: Microsoft 365 プラグインと Azure Active Directory (Azure AD) の間の接続を構成する</span><span class="sxs-lookup"><span data-stu-id="1f942-135">Step 2: Configure the connection between the Microsoft 365 plugin and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="1f942-136">次に、Azure AD で、アプリケーションとして、取り扱いを行う必要AD。</span><span class="sxs-lookup"><span data-stu-id="1f942-136">Next, you'll need to register Moodle as an application in your Azure AD.</span></span> <span data-ttu-id="1f942-137">このプロセスの完了に役立つ PowerShell スクリプトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="1f942-137">We've provided a PowerShell script to help you complete this process.</span></span> <span data-ttu-id="1f942-138">PowerShell スクリプトは、Microsoft 365 テナント用の新しい Azure AD アプリケーションをプロビジョニングします。このアプリケーションは、Microsoft 365 のグループ プラグインで使用されます。</span><span class="sxs-lookup"><span data-stu-id="1f942-138">The PowerShell script provisions a new Azure AD application for your Microsoft 365 tenant, which will be used by the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="1f942-139">スクリプトは、Microsoft 365 テナント用にアプリをプロビジョニングし、プロビジョニングされたアプリに必要な応答 URL とアクセス許可を設定して `AppID` 、 `Key`</span><span class="sxs-lookup"><span data-stu-id="1f942-139">The script will provision the app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and return the `AppID` and `Key`.</span></span> <span data-ttu-id="1f942-140">生成された Microsoft 365 の Pagele プラグインのセットアップ ページを使用して、Azure AD を使用して、Pagele サーバー サイト `AppID` `Key` を構成できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-140">You can use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugin setup page to configure your Moodle server site with Azure AD.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="1f942-141">PowerShell スクリプトは最新の構成項目で更新されないので、この構成は [、3.8.0.4 および 3.9.1 および 3.8.0.5](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) および [3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って手動で完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-141">The PowerShell script is not updated with the latest configuration items, so you'll have to complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span> </br></br>
> <span data-ttu-id="1f942-142">PowerShell スクリプトが自動化している手動の手順を詳細に表示するには、「[アプリケーションとして使うのに用](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)件を登録する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1f942-142">To view the manual steps that the PowerShell script is automating in detail , *see* [Register your Moodle instance as an Application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="1f942-143">Microsoft Teams の情報フローの [ダイアログ] タブ</span><span class="sxs-lookup"><span data-stu-id="1f942-143">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="1f942-144">Microsoft 365 統合プラグインページで、[セットアップ] タブ **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-144">From the Microsoft 365 Integration plugin page select the **Setup** tab.</span></span>

1. <span data-ttu-id="1f942-145">**[PowerShell スクリプトのダウンロード] ボタンを** 選択し、ローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="1f942-145">Select the **Download PowerShell Script** button and save it to your local computer.</span></span>

1. <span data-ttu-id="1f942-146">ZIP ファイルから PowerShell スクリプトを準備する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-146">You'll need to prepare the PowerShell script from the ZIP file.</span></span> <span data-ttu-id="1f942-147">これを行うには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="1f942-147">To do so:</span></span>

    * <span data-ttu-id="1f942-148">ファイルをダウンロードして展開 `Moodle-AzureAD-Powershell.zip` します。</span><span class="sxs-lookup"><span data-stu-id="1f942-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    * <span data-ttu-id="1f942-149">抽出されたフォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="1f942-149">Open the extracted folder.</span></span>
    * <span data-ttu-id="1f942-150">ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` プロパティ] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    * <span data-ttu-id="1f942-151">[プロパティ **] ウィンドウ** の [全般] タブで、ウィンドウの下部にある Security 属性の横にある `Unblock` チェック ボックスをオンにします。 </span><span class="sxs-lookup"><span data-stu-id="1f942-151">Under the **General** tab of the Properties window, check the `Unblock` box next to the **Security** attribute located at the bottom of the window.</span></span>
    * <span data-ttu-id="1f942-152">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-152">Select **OK**.</span></span>
    * <span data-ttu-id="1f942-153">ディレクトリ パスを、抽出されたフォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="1f942-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="1f942-154">次に、管理者として PowerShell を実行します。</span><span class="sxs-lookup"><span data-stu-id="1f942-154">Next you'll run PowerShell as an administrator:</span></span>

    * <span data-ttu-id="1f942-155">[開始] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-155">Select Start.</span></span>
    * <span data-ttu-id="1f942-156">「PowerShell」と入力します。</span><span class="sxs-lookup"><span data-stu-id="1f942-156">Type PowerShell.</span></span>
    * <span data-ttu-id="1f942-157">ウィンドウを右クリックWindows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1f942-157">Right-click Windows PowerShell.</span></span>
    * <span data-ttu-id="1f942-158">[管理者として実行] を選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-158">Select "Run as Administrator".</span></span>

1. <span data-ttu-id="1f942-159">ディレクトリへのパスの場所を入力して、未定義 `cd .../.../Moodle-AzureAD-Powershell` `.../...` のディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="1f942-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="1f942-160">PowerShell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="1f942-160">Execute the PowerShell script:</span></span>

    * <span data-ttu-id="1f942-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` キーを押します。</span><span class="sxs-lookup"><span data-stu-id="1f942-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    * <span data-ttu-id="1f942-162">Enter `./Moodle-AzureAD-Script.ps1` キーを押します。</span><span class="sxs-lookup"><span data-stu-id="1f942-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    * <span data-ttu-id="1f942-163">ポップアップ ウィンドウで Microsoft 365 管理者アカウントにログインします。</span><span class="sxs-lookup"><span data-stu-id="1f942-163">Login to your Microsoft 365 administrator account in the pop-up window.</span></span>
    * <span data-ttu-id="1f942-164">Azure AD アプリケーションの名前を入力します (例:、グループ/プラグインを使用します)。</span><span class="sxs-lookup"><span data-stu-id="1f942-164">Enter the name of the Azure AD Application (e.g., Moodle/Moodle plugin).</span></span>
    * <span data-ttu-id="1f942-165">使用しているのが、使用しているのが、あなたのLesle サーバーの URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="1f942-165">Enter the URL for your Moodle server.</span></span>
    * <span data-ttu-id="1f942-166">スクリプトによって **生成された** アプリケーション ID **とアプリケーション** キーをコピーし、保存します。</span><span class="sxs-lookup"><span data-stu-id="1f942-166">Copy the **Application ID** and **Application Key** generated by the script and save them.</span></span>

1. <span data-ttu-id="1f942-167">次に ` AppID` `Key` 、Microsoft 365 のグループプラグインと Microsoft 365 のLe プラグインに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-167">Next you'll need to add the` AppID` and `Key` to the Microsoft 365 Moodle Plugin.</span></span> <span data-ttu-id="1f942-168">プラグインの管理ページ (Microsoft 365 統合➡プラグイン➡管理) に戻ります。</span><span class="sxs-lookup"><span data-stu-id="1f942-168">Return to the plugin administration page (Site administration ➡ Plugins ➡ Microsoft 365 Integration).</span></span>

1. <span data-ttu-id="1f942-169">[セットアップ **] タブ** で、前にコピーした **アプリケーション ID** と **アプリケーション** キーを追加し、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-169">On the **Setup** tab add the **Application ID** and **Application Key** you copied previously, then select **Save changes**.</span></span>

1. <span data-ttu-id="1f942-170">ページが更新された後、新しいセクションが表示されます接続方法 **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-170">Once the page refreshes you should see a new section **Choose connection method**.</span></span> <span data-ttu-id="1f942-171">[既定] というラベルのチェック **ボックスを** オンにし、[変更の保存 **] を再び選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-171">Select the checkbox labeled **Default** and then select **Save changes** again.</span></span>

1. <span data-ttu-id="1f942-172">ページが更新された後、別の新しいセクション管理者の同意が表示され **&情報が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="1f942-172">Once the page refreshes you will see another new section **Admin consent & additional information**.</span></span>
    * <span data-ttu-id="1f942-173">[管理者の **同意の** 提供] リンクを選択し、Microsoft 365グローバル管理者の資格情報を入力し、[承諾] を選択してアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="1f942-173">Select the **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    * <span data-ttu-id="1f942-174">Azure AD **テナント フィールドの横** にある [検出] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-174">Next to the **Azure AD Tenant** field select the **Detect** button.</span></span>
    * <span data-ttu-id="1f942-175">**OneDrive for Business URL の横にある [** 検出] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-175">Next to the **OneDrive for Business URL** select the **Detect** button.</span></span>
    * <span data-ttu-id="1f942-176">フィールドにデータが入力された後、[変更の保存] **ボタンを** 再度選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-176">Once the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="1f942-177">[更新] **ボタンを** 選択してインストールを確認し、[変更の保存 **] をクリックします**。</span><span class="sxs-lookup"><span data-stu-id="1f942-177">Select the **Update** button to verify the installation, then **Save changes**.</span></span>

1. <span data-ttu-id="1f942-178">次に、ユーザーを、使用しているのが、Azure サーバーと Azure サーバーの間で同期AD。</span><span class="sxs-lookup"><span data-stu-id="1f942-178">Next, you'll need to synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="1f942-179">環境に応じて、この段階で異なるオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-179">Depending on your environment, you may select different options during this stage.</span></span> <span data-ttu-id="1f942-180">次の手順をお試しください。</span><span class="sxs-lookup"><span data-stu-id="1f942-180">To get started:</span></span>
    * <span data-ttu-id="1f942-181">[同期設定] **タブに切り替える**</span><span class="sxs-lookup"><span data-stu-id="1f942-181">Switch to the **Sync Settings tab**</span></span>
    * <span data-ttu-id="1f942-182">[Azure **ユーザーと同期] セクションAD、** 環境に適用するチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="1f942-182">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="1f942-183">通常、少なくとも次の項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-183">Typically, you would, at a minimum, select the following:</span></span>  

        <span data-ttu-id="1f942-184">✔ Azure AD でユーザーのアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="1f942-184">✔ Create accounts in Moodle for users in Azure AD .</span></span> 
        <span data-ttu-id="1f942-185">✔ Azure AD のユーザーの、グループのすべてのアカウントを更新します。</span><span class="sxs-lookup"><span data-stu-id="1f942-185">✔ Update all accounts in Moodle for users in Azure AD.</span></span>  

    * <span data-ttu-id="1f942-186">[ **ユーザー作成の制限** ] セクションでは、フィルターを設定して、Filterle に同期される Azure ADユーザーを制限できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-186">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that will be synced to Moodle.</span></span>
    * <span data-ttu-id="1f942-187">[ **ユーザー フィールド マッピング]** セクションでは、Azure ユーザー プロファイルとADユーザー プロファイル のフィールド マッピングをカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="1f942-187">The **User Field Mapping** section will allow you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    * <span data-ttu-id="1f942-188">Teams **の同期セクション** では、既存のLeele コースの一部またはすべてについて、グループ (チーム) を自動的に作成できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-188">In the **Teams Sync** section you can choose to automatically create Groups (i.e. teams) for some, or all, of your existing Moodle courses.</span></span>

> [!NOTE]
> <span data-ttu-id="1f942-189">(既定では [1](https://docs.moodle.org/310/en/Cron) 日に 1 回) タスク のスケジュールに従って、1 つが実行されます。</span><span class="sxs-lookup"><span data-stu-id="1f942-189">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) will run according to the task schedule (once a day by default).</span></span> <span data-ttu-id="1f942-190">ただし、すべての同期を維持するために、cron の実行頻度を高くする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-190">However, the cron should run more frequently to keep everything in sync.</span></span>

13. <span data-ttu-id="1f942-191">最初の [実行のために、cron](https://docs.moodle.org/310/en/Cron)ジョブを検証する (または手動で実行する) には、[Azure AD] セクションの [ユーザーの同期] で [スケジュールされたタスク管理]**ページのリンクを選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-191">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs (and/or run them manually for the first run) select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="1f942-192">これにより、[スケジュールされたタスク] **ページに移動** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-192">This will take you to the **Scheduled Tasks** page.</span></span>

    * <span data-ttu-id="1f942-193">下にスクロールして **、Azure** AD同期ユーザーを検索し、[今すぐ **実行] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-193">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    * <span data-ttu-id="1f942-194">既存のコースに基づいてグループを作成することを選択した場合は **、Microsoft 365** でユーザー グループの作成ジョブを実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="1f942-194">If you chose to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

1. <span data-ttu-id="1f942-195">プラグインの管理ページ (Microsoft 365 統合➡プラグイン➡管理) に戻り、[Teams の設定] ページ **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-195">Return to the plugin administration page (Site administration ➡ Plugins ➡ Microsoft 365 Integration) and select the **Teams Settings** page.</span></span> <span data-ttu-id="1f942-196">Teams アプリの統合を有効にするには、いくつかの設定を構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-196">You'll need to configure some settings to enable the Teams app integration.</span></span>

    * <span data-ttu-id="1f942-197">**OpenID Connect を有効にするには**、[認証の管理] リンクを選択し **、OpenId Connect** 行の目のアイコンが灰色表示されている場合は選択します。 </span><span class="sxs-lookup"><span data-stu-id="1f942-197">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    * <span data-ttu-id="1f942-198">次に、フレーム埋め込み機能を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-198">Next, you'll need to enable frame embedding.</span></span> <span data-ttu-id="1f942-199">**[HTTP セキュリティ] リンクを** 選択し、[フレームの埋め込みを許可する] の横にある **チェック ボックスをオンにします**。</span><span class="sxs-lookup"><span data-stu-id="1f942-199">Select the **HTTP Security** link, then select the checkbox next to **Allow frame embedding**.</span></span>
    * <span data-ttu-id="1f942-200">次の手順では、ブラウザー API 機能を有効にする Web サービスを有効にします。</span><span class="sxs-lookup"><span data-stu-id="1f942-200">The next step is to enable web services which will enable the Moodle API features.</span></span> <span data-ttu-id="1f942-201">[高度 **な機能]** リンクを選択し、[Web サービスを有効にする] の横にあるチェック **ボックスがオンになっていることを** 確認します。</span><span class="sxs-lookup"><span data-stu-id="1f942-201">Select the **Advanced Features** link, then make sure the checkbox next to **Enable web services** is checked.</span></span>
    * <span data-ttu-id="1f942-202">最後に、Microsoft 365 の外部サービスを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-202">Finally, you'll need to enable the external services for Microsoft 365.</span></span> <span data-ttu-id="1f942-203">次に、[ **外部サービス] リンク** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-203">Select the **External services** link then next:</span></span>  

        <span data-ttu-id="1f942-204">✔Microsoft  **365 Webservices 行で [編集] を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-204">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>  
        <span data-ttu-id="1f942-205">✔を有効にする] チェック ボックスを **オンにし**、[変更の保存] **を選択します。**</span><span class="sxs-lookup"><span data-stu-id="1f942-205">✔ Mark the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    * <span data-ttu-id="1f942-206">次に、認証されたユーザーのアクセス許可を編集して、Web サービス トークンの作成を許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-206">Next, you'll need to edit your authenticated user permissions to allow them to create web service tokens.</span></span> <span data-ttu-id="1f942-207">編集役割 **の [認証されたユーザー] リンクを選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-207">Select the **Editing role 'Authenticated user'** link.</span></span> <span data-ttu-id="1f942-208">下にスクロールして **[Web** サービス トークンの作成] 機能を見つけ、[許可] チェック ボックス **をオン** にします。</span><span class="sxs-lookup"><span data-stu-id="1f942-208">Scroll down and find the **Create a web service token** capability and mark the **Allow** checkbox.</span></span>

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="1f942-209">手順 3: Azure にLesure アシスタント ボットを展開する</span><span class="sxs-lookup"><span data-stu-id="1f942-209">Step 3: Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="1f942-210">Microsoft Teams 用の無料のリズル アシスタント ボットは、教師と学生が、コース、課題、成績、その他の情報に関する質問に対して、リムードルで回答するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="1f942-210">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades and other information in Moodle.</span></span> <span data-ttu-id="1f942-211">ボットは、Teams 内の学生と教師にも、通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="1f942-211">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="1f942-212">ボットは Microsoft が管理するオープン ソース プロジェクトであり [、GitHub で利用できます](https://github.com/microsoft/Moodle-Teams-Bot)。</span><span class="sxs-lookup"><span data-stu-id="1f942-212">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
> <span data-ttu-id="1f942-213">このセクションでは、Azure サブスクリプションにリソースを展開します。</span><span class="sxs-lookup"><span data-stu-id="1f942-213">In this section you'll deploy resources to your Azure subscription.</span></span> <span data-ttu-id="1f942-214">すべてのリソースは、無料の階層を使用 **して構成** されます。</span><span class="sxs-lookup"><span data-stu-id="1f942-214">All resources will be configured using the **free** tier.</span></span> <span data-ttu-id="1f942-215">ボットの使用状況によっては、これらのリソースのスケーリングが必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-215">Depending on the usage of your bot, you may need to scale these resources.</span></span>
> <span data-ttu-id="1f942-216">ボットなしで [色] タブを使用する場合は、手順 [4 に進みます](#step-4-deploy-your-microsoft-teams-app)。</span><span class="sxs-lookup"><span data-stu-id="1f942-216">If you want to use the Moodle tab without the bot, skip to [step 4](#step-4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="1f942-217">リムードル ボット情報フロー</span><span class="sxs-lookup"><span data-stu-id="1f942-217">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="1f942-218">ボットをインストールするには、最初に Microsoft Identity Platform にボットを [登録する必要があります](https://identity.microsoft.com/Landing)。</span><span class="sxs-lookup"><span data-stu-id="1f942-218">To install the bot, you'll first need to register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="1f942-219">これにより、ボットは Microsoft エンドポイントに対して認証できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-219">This allows your bot to authenticate against your Microsoft endpoints.</span></span> <span data-ttu-id="1f942-220">ボットを登録するには:</span><span class="sxs-lookup"><span data-stu-id="1f942-220">To register your bot:</span></span>

1. <span data-ttu-id="1f942-221">プラグインの管理ページ (Microsoft 365 統合➡プラグイン➡管理) に戻り、[Teams の設定] タブ **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-221">Return to the plugin administration page (Site administration ➡ Plugins ➡ Microsoft 365 Integration) and select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="1f942-222">Microsoft アプリケーション **登録ポータルのリンクを選択** し、Microsoft ID でログインします。</span><span class="sxs-lookup"><span data-stu-id="1f942-222">Select the **Microsoft Application Registration Portal** link and login with your Microsoft ID.</span></span>

1. <span data-ttu-id="1f942-223">アプリの名前 (例: MoodleBot) を入力し、[作成] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-223">Enter a name for your app (e.g., MoodleBot) and select the **Create** button.</span></span>

1. <span data-ttu-id="1f942-224">アプリケーション **ID をコピーし** 、[チームの設定] ページの **[Bot Application ID]** フィールド **に貼り付** けます。</span><span class="sxs-lookup"><span data-stu-id="1f942-224">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="1f942-225">[新しい **パスワードの生成] ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-225">Select the **Generate New Password** button.</span></span> <span data-ttu-id="1f942-226">生成されたパスワードをコピーし、[チームの設定] ページの **[Bot Application Password]** フィールド **に貼り付** けます。</span><span class="sxs-lookup"><span data-stu-id="1f942-226">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="1f942-227">フォームの下部までスクロールし、[変更の保存] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-227">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="1f942-228">アプリケーション ID とパスワードを生成し、次にボットを Azure に展開します。</span><span class="sxs-lookup"><span data-stu-id="1f942-228">Now that you've generated your Application ID and Password, it's time to deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f942-229">[Azure **に展開** ] ボタンを選択し、必要な情報を含むフォームに入力します (Bot Application ID、Bot Application Password、および、および、取り込みシークレットが [チームの設定] ページに **表示** されます)。</span><span class="sxs-lookup"><span data-stu-id="1f942-229">Select the **Deploy to Azure** button and complete the form with the necessary information (the Bot Application ID, Bot Application Password and the Moodle Secret are on the **Team Settings** page.</span></span> <span data-ttu-id="1f942-230">Azure の情報は、[セットアップ] **ページに表示** されます。</span><span class="sxs-lookup"><span data-stu-id="1f942-230">The Azure information is on the **Setup** page).</span></span> 
> * <span data-ttu-id="1f942-231">フォームが完成したら、チェック ボックスをオンにして使用条件に同意します。</span><span class="sxs-lookup"><span data-stu-id="1f942-231">Once you have the form completed, select the check box to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="1f942-232">[ **購入] ボタン** を選択します (すべての Azure リソースが無料層に展開されます)。</span><span class="sxs-lookup"><span data-stu-id="1f942-232">Select the **Purchase** button (all Azure resources are deployed to the free tier).</span></span>

<span data-ttu-id="1f942-233">リソースが Azure への展開を完了したら、メッセージング エンドポイントを使用して Microsoft 365 の取り決めプラグインを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-233">Once the resources have completed deploying to Azure, you'll need to configure the Microsoft 365 Moodle plugin with a messaging endpoint.</span></span> <span data-ttu-id="1f942-234">Azure のボットからエンドポイントを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-234">You'll need to get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="1f942-235">Azure Portal に [ログインします](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1f942-235">Log into the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="1f942-236">左側のウィンドウで [ **リソース** グループ] を選択し、ボットの展開中に使用した (または作成した) リソース グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-236">In the left pane select **Resource groups** and choose the resource group you used (or created) while deploying your bot.</span></span>

1. <span data-ttu-id="1f942-237">グループ内 **のリソースの** 一覧から WebApp Bot リソースを選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-237">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="1f942-238">[概要 **] セクションから** メッセージング エンドポイント **をコピー** します。</span><span class="sxs-lookup"><span data-stu-id="1f942-238">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="1f942-239">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugin.</span><span class="sxs-lookup"><span data-stu-id="1f942-239">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugin.</span></span>

1. <span data-ttu-id="1f942-240">ボット エンドポイント **フィールドに**、コピーした URL を貼り付け、単語メッセージを *webhook に変更します*。</span><span class="sxs-lookup"><span data-stu-id="1f942-240">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="1f942-241">URL は次のように表示されます。  `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="1f942-241">The URL should now appear as follows:  `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="1f942-242">[変更 **の保存] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-242">Select **Save Changes**.</span></span>

1. <span data-ttu-id="1f942-243">変更を保存したら、[チームの設定] タブに戻り、[マニフェストファイルのダウンロード] ボタンを選択して、アプリ マニフェスト パッケージをコンピューターに保存します (次のセクションで使用します)。</span><span class="sxs-lookup"><span data-stu-id="1f942-243">Once your changes have been saved, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer (you'll use it in the next section).</span></span>

## <a name="step-4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="1f942-244">手順 4: Microsoft Teams アプリを展開する</span><span class="sxs-lookup"><span data-stu-id="1f942-244">Step 4: Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="1f942-245">ボットが Azure に展開され、次に、使用しているのが、リピドル サーバーと話をするように構成されたので、次に Microsoft Teams アプリを展開します。</span><span class="sxs-lookup"><span data-stu-id="1f942-245">Now that you have your bot deployed to Azure and configured to talk to your Moodle server, it's time to deploy your Microsoft Teams app.</span></span> <span data-ttu-id="1f942-246">これを行うには、前の手順で Microsoft 365 の Pagele Plugin チーム設定ページからダウンロードしたアプリ マニフェスト ファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="1f942-246">To do this you'll load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugin Team Settings page in the previous step.</span></span>

<span data-ttu-id="1f942-247">アプリをインストールする前に、外部アプリとアプリのアップロードが有効になっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f942-247">Before you can install the app you'll need to make sure external apps and uploading of apps is enabled.</span></span> <span data-ttu-id="1f942-248">これを行うには、Teams で [Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) テナントのドキュメントを準備する手順に従います。</span><span class="sxs-lookup"><span data-stu-id="1f942-248">To do so, you can follow the steps in the Teams [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md) documentation.</span></span> <span data-ttu-id="1f942-249">外部アプリを有効にしたら、次の手順に従ってアプリを展開できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-249">Once you've ensured that external apps are enabled, you can follow the steps below to deploy your app:</span></span>

1. <span data-ttu-id="1f942-250">**Microsoft Teams を開きます**。</span><span class="sxs-lookup"><span data-stu-id="1f942-250">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="1f942-251">ナビゲーション バー **の** 左下の領域にある [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-251">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="1f942-252">オプションの **一覧から [カスタム アプリの** アップロード] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-252">Select the **Upload a custom app** link from the list of options.</span></span>

> [!Note]
> <span data-ttu-id="1f942-253">グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションがあります。そうしないと、自分がメンバーであるチームのアプリのみを読み込む事が可能になります。</span><span class="sxs-lookup"><span data-stu-id="1f942-253">If you're logged in as a global administrator you'll have the option of uploading the app to your organization's app catalog, otherwise you'll only be able to load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="1f942-254">以前にダウンロード `manifest.zip` したパッケージを選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="1f942-254">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="1f942-255">アプリ マニフェスト パッケージをダウンロードしていない場合は、Pluginle のプラグイン構成ページの [ **チーム** 設定] タブからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="1f942-255">If you haven't downloaded the app manifest package, you can do so from the **Team Settings** tab of the plugin configuration page in Moodle.</span></span>

<span data-ttu-id="1f942-256">アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-256">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="1f942-257">これを行うには、チャネルに移動し、 **プラス記号** (➕) を選択し、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-257">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="1f942-258">画面の指示に従って、チャネルへの [Le のコース] タブの追加を完了します。</span><span class="sxs-lookup"><span data-stu-id="1f942-258">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="step-5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="1f942-259">手順 5: Microsoft Teams で 、自動的に [Le] タブを作成することを許可する</span><span class="sxs-lookup"><span data-stu-id="1f942-259">Step 5: Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="1f942-260">Microsoft Teams では 、Teams のタブを手動で作成することもできますが、コースの同期からチームを作成するときに自動的に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="1f942-260">Although the Moodle tabs can be created manually in Microsoft Teams, you may decide to have them automatically created when teams are created from course synchronization.</span></span> <span data-ttu-id="1f942-261">これを行うには、アップロードされた Microsoft Teams アプリの ID を次のページで構成します。</span><span class="sxs-lookup"><span data-stu-id="1f942-261">To do this, you'll configure the ID of the uploaded Microsoft Teams app in Moodle:</span></span>

1. <span data-ttu-id="1f942-262">Microsoft Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="1f942-262">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="1f942-263">ナビゲーション バーの左下の領域から [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="1f942-263">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="1f942-264">アップロードされた **Happle アプリを見つけて➡** オプション アイコンを選択し➡リンク **を選択します**。 </span><span class="sxs-lookup"><span data-stu-id="1f942-264">Locate the uploaded **Moodle app** ➡ select the **options** icon ➡ select **copy link**.</span></span>

1. <span data-ttu-id="1f942-265">テキスト エディターで、コピーしたコンテンツを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="1f942-265">In a text editor, paste the copied content.</span></span> <span data-ttu-id="1f942-266">ht などの URL を含&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。</span><span class="sxs-lookup"><span data-stu-id="1f942-266">It should contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="1f942-267">URL の最後の部分 (Microsoft Teams アプリの ID など) `00112233-4455-6677-8899-aabbccddeeff` をコピーします。</span><span class="sxs-lookup"><span data-stu-id="1f942-267">Copy the last part of the URL, e.g. `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="1f942-268">リシェルで **、Microsoft** 365 の Page.365 の [Plugin] 構成ページから Teams の [Teams 用の Teams のページ] タブを開きます。</span><span class="sxs-lookup"><span data-stu-id="1f942-268">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugin configuration page.</span></span>

1. <span data-ttu-id="1f942-269">Microsoft Teams アプリの ID を [表示] アプリ ID フィールドに貼り付け、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="1f942-269">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="1f942-270">今度は、Teamsle のコースが同期すると、Microsoft Teams は自動的にチームに Pagele アプリをインストールし、Teams の一般チャネルに [Pagele] タブを作成し、同期の対象となる、Pagele コースのコース ページを含む設定を行います。</span><span class="sxs-lookup"><span data-stu-id="1f942-270">Now when a Moodle course is synced, Microsoft Teams will automatically install the Moodle app in the team, create a Moodle tab in the General channel of Teams, and configure it to contain the course page for the Moodle course from which it is synced.</span></span>

### <a name="thats-it-you-and-your-team-can-now-start-working-with-your-moodle-courses-directly-from-microsoft-teams"></a><span data-ttu-id="1f942-271">手順は以上です。</span><span class="sxs-lookup"><span data-stu-id="1f942-271">That's it!</span></span> <span data-ttu-id="1f942-272">これで、お客様とチームは、Microsoft Teams から直接、自分の Teamsle コースの操作を開始できます。</span><span class="sxs-lookup"><span data-stu-id="1f942-272">You and your team, can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

<span data-ttu-id="1f942-273">機能に関するリクエストやフィードバックを共有するには、User Voice ページ [にアクセスしてください](https://microsoftteams.uservoice.com/forums/916759-moodle)。</span><span class="sxs-lookup"><span data-stu-id="1f942-273">To share any feature requests or feedback with us, please visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>
