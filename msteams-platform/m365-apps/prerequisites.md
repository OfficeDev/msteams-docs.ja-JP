---
title: 複数のアプリを拡張するために、Teams環境をMicrosoft 365
description: アプリを複数のユーザーにまたがって拡張Teams前提条件を次に示Microsoft 365
ms.date: 02/11/2022
ms.openlocfilehash: eec44e149e81b420c507b0580896d2c5a4a99cc2
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356001"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>複数のアプリを拡張するために、Teams環境をMicrosoft 365

> [!NOTE]
> 現在公開されている開発者プレビュー Microsoft 365 Teams アプリを拡張[します](~/resources/dev-preview/developer-preview-intro.md)。

アプリを複数のアプリケーションにTeamsするMicrosoft 365環境は、Microsoft Teams似ています。 この記事では、Microsoft Teams および Microsoft Office で実行されている Teams Outlook アプリをプレビューするために、Microsoft Teams および Microsoft Office アプリケーションのプレビュー ビルドを実行するために必要な特定 Officeの構成について説明します。

開発環境をセットアップするには:

> [!div class="checklist"]
> * [開発者 (Microsoft 365) テナントを取得し、サイドローディングを有効にする](#prepare-a-developer-tenant-for-testing)
> * [ターゲットリリースMicrosoft 365にOffice 365 *テナントを登録する*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [プレビュー バージョンのプレビュー バージョンにアクセスするアカウントを構成Outlook Office](#install-office-apps-in-your-test-environment)
> * [バージョンの Developer Previewに切り替Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*省略可能*][コードTeams Toolkit拡張機能をMicrosoft Visual Studioする](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>テスト用に開発者テナントを準備する

開発環境をMicrosoft 365するには、開発者サブスクリプション サンドボックス テナントが必要です。 まだテナントを持ってない場合は、サンドボックス テナントを作成 [するか、組織](/office/developer-program/microsoft-365-developer-program-get-started) を通じてテスト テナントを取得します。

テナントを作成した後、テナントのサイドローディングを有効にする必要があります。「サイドローディングを有効 [にする」を参照してください](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。 サイドローディングが有効になっているか確認するには、Teamsにサインインし、[アプリ] を選択し、カスタム アプリ オプションアップロード **確認** します。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="アップロードアプリ オプションを選択する":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>ターゲットリリースの開発者テナントOffice 365登録する

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365 開発者](https://devblogs.microsoft.com/microsoft365dev/)ブログの最新の更新プログラムを参照して、Outlook.com および Office.com の Teams アプリのサポートがテスト テナントで利用可能か確認してください。

対象となるリリースのテスト テナントOffice 365登録するには、次のOffice 365使用します。

1. テスト テナント資格情報を[Microsoft 365 管理センター](https://admin.microsoft.com)サインインします。
1. [Org **設定** > **Organization 設定** > **] に移動します**。
1. [リリース **の基本設定] を選択します**。
1. ターゲットリリース *の基本設定を選択* します。
    1. **すべてのユーザーのターゲット リリース**
    1. **選択したユーザーのターゲット リリース**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Microsoft 365 管理センターを選択した場合の [リリースの基本設定] メニュー":::
    
1. **[保存]** を選択します。

リリース オプションの詳細Office 365、ヘルプの「標準リリースオプションまたはターゲット リリース オプションを設定 [する」](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)*をMicrosoft 365 管理センターしてください*。

## <a name="install-office-apps-in-your-test-environment"></a>テストOfficeアプリをインストールする

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) 開発者向けブログの最新の更新プログラムを参照して、Teams メッセージング拡張機能の Windows Outlook デスクトップ サポートがテスト テナントで利用可能か確認してください。

最近のベータTeamsビルドをOutlookデスクトップWindowsアプリを *プレビューできます*。 テスト テナントの更新チャネルを[変更Microsoft 365 Apps](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)ベータ チャネル ビルドをインストールする必要Office 365確認します。

テスト環境Office 365ベータ チャネル アプリケーションをインストールするには、次の手順を実行します。

1. テスト テナント資格情報を使用してテスト環境にサインインします。
1. 展開ツール[Officeをダウンロードし](https://www.microsoft.com/download/details.aspx?id=49117)、ローカル フォルダーに展開します。
1. ローカル フォルダーに移動し、テキスト *エディター* でconfiguration-Office365-x86.xml(*または *x64.xml*) を開き、[チャネル] の値をに *更新* します `BetaChannel`。
1. コマンド プロンプトを開き、ローカル フォルダー パスに移動します。
1. セットアップ `setup.exe /configure configuration-Office365-x86.xml` に応じて、実行 *(または *x64.xml* ファイルを使用します)。
1. [Outlook (デスクトップ クライアント) を開き、テスト テナント資格情報を使用してメール アカウントを設定します。
1. ファイル **を開** > **Office** **AccountAbout** >  Outlook。  
   ビルド番号が **14416** 以上で、チャネルがベータ チャネルの場合は、ベータ Microsoft 365ビルドを実行しています。
1. 右上隅で、[近日] トグル **をオン** にします。
    
    :::image type="content" source="images/outlook-coming-soon.png" alt-text="[近日公開] トグル オプション (Outlook":::

> [!NOTE]
> [近日] ボタンが表示Outlookコンピューターを閉じて再起動 *する必要がある* 場合があります。

テナント アカウントのテスト テナントのサポートを確認できます。

* Teams デスクトップ用に office.com、outlook.com、および Outlook Windows で実行されている Teams 個人用タブの場合は、テスト テナントの資格情報でサインインし、Office または Outlook の左側のサイドバーで省略記号 (**....**) オプションを確認します。

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="省略記号 ('...') オプションは、ページの左側のサイドバー Outlook":::

* outlook.com および Outlook Windows のメッセージング拡張機能については、メッセージ作成ウィンドウの下部にある [その他Outlook] オプションを確認します。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="[メッセージの作成] ウィンドウの [その他のOutlook] オプション":::

> [!NOTE]
> ベータ チャネル リリースにオプトインしているが、これらの省略記号オプションが表示されていない場合は、プレビュー機能のサポートがテナントに展開中である可能性があります。 最新の更新プログラムについては、「開発者[ブログMicrosoft Teams参照してください](https://devblogs.microsoft.com/microsoft365dev/)。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>バージョンの Developer Previewに切り替Teams

クライアントからパブリック サーバーに[切りDeveloper Preview](../resources/dev-preview/developer-preview-intro.md)確認Microsoft Teamsします。

1. サンドボックス テナント資格情報を使用Teamsサインインします。
1. ユーザー プロファイルの横にある省略記号 (**...)** メニューから、[**AboutDeveloper** >  **プレビュー] を選択します**。 ダイアログが表示されたら、[開発者プレビューに **切り替える] を選択します**。
1. アプリのTeamsしたら、ユーザー プロファイルの横にある省略記号 (**....**) メニューに移動し、ユーザー プロファイルが選択Developer Preview確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="[パブリック開発者プレビュー] オプション (Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>プレビュー拡張機能Visual Studio CodeインストールTeams Toolkitインストールする

必要に応じて[、Visual Studio Codeを](https://code.visualstudio.com/)使用して、TeamsアプリをOfficeおよびOutlook。

Teams Toolkit (`v2.10.0`[Visual Studio Code](https://aka.ms/teams-toolkit)以降) の拡張機能は、既存の Teams コードを変更して、Outlook および Office と互換性を持つコマンドを提供します。 詳細については、「ユーザーとユーザー[の個人Teamsを有効にするOffice」を参照Outlook](extend-m365-teams-personal-tab.md)。

## <a name="next-steps"></a>次の手順

- [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
- [Outlook の Teams メッセージングの拡張機能を有効にする](extend-m365-teams-message-extension.md)
