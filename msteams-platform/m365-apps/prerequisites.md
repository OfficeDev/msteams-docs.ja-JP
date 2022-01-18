---
title: アプリケーション全体でアプリを拡張Teams環境をMicrosoft 365
description: アプリを複数のユーザーにまたがって拡張Teams前提条件を次に示Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: cd9136b2442b8b39169592be13071136ab39c645
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059729"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365"></a>M365 全体でアプリを拡張Teams環境をセットアップする

> [!NOTE]
> 現在公開されている開発者プレビューでのみMicrosoft 365 Teams アプリを拡張[します](~/resources/dev-preview/developer-preview-intro.md)。

アプリを複数のアプリケーションにTeamsするMicrosoft 365は、Microsoft Teams似ています。 この記事では、Outlook および Office で実行されている Teams アプリをプレビューするために、Microsoft Teams および Microsoft Office アプリケーションのプレビュー ビルドを実行するために必要な特定の構成について説明します。

開発環境をセットアップするには:

> [!div class="checklist"]
> * [M365 Developer (Sandbox) テナントを取得し、サイドローディングを有効にする](#prepare-a-developer-tenant-for-testing)
> * [M365 テナントをターゲット *リリースOffice 365登録する*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [プレビュー バージョンのプレビュー バージョンにアクセスするアカウントを構成OutlookおよびOffice](#install-office-apps-in-your-test-environment)
> * [バージョンの Developer Previewに切り替Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*省略可能*][ユーザーのTeams Toolkit拡張機能をインストールVisual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>テスト用に開発者テナントを準備する

開発環境をMicrosoft 365するには、開発者サブスクリプション サンドボックス テナントが必要です。 まだテナントを持ってない場合は、サンドボックス テナントを作成 [するか、組織](/office/developer-program/microsoft-365-developer-program-get-started) を通じてテスト テナントを取得します。

テナントを作成した後、テナントのサイドローディングを有効にする必要があります。「enable [sideloading」を参照してください](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。 サイドローディングが有効になっているか確認するには、Teamsにサインインし、[アプリ]を選択し、カスタム アプリ アップロード **を確認** します。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="アップロードアプリ オプションを選択する":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>ターゲットリリースの開発者テナントOffice 365登録する

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/)開発者向けブログの最新の更新プログラムを参照して、Outlook.com および Office.com の Teams アプリのサポートがテスト テナントで利用可能か確認してください。

対象となるリリースのテスト テナントOffice 365登録するには、次の方法を実行します。

1. テスト テナント資格情報[をMicrosoft 365 管理センター](https://admin.microsoft.com)サインインします。
1. [組織の **組織**  >  **設定] 設定**  >  **に移動します**。
1. [リリース **の基本設定] を選択します**。
1. ターゲットリリース *の基本設定を選択* します。
    1. **すべてのユーザーのターゲット リリース**
    1. **選択したユーザーのターゲット リリース**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Microsoft 365 管理センターターゲット リリース オプションを選択した場合の [リリースの基本設定] メニュー":::
    
1. **[保存]** を選択します。

リリース オプションの詳細についてはOffice 365ヘルプの「標準 [](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)リリース オプションまたはターゲット リリース オプションを設定する」*をMicrosoft 365 管理センターしてください*。

## <a name="install-office-apps-in-your-test-environment"></a>テストOfficeアプリをインストールする

> [!IMPORTANT]
> Microsoft Teams - Microsoft 365[開発者](https://devblogs.microsoft.com/microsoft365dev/)ブログの最新の更新プログラムを参照して、Teams メッセージ拡張機能の Outlook デスクトップ サポートがテスト テナントで利用可能Windows を確認します。

最近のベータTeamsビルドを使用して、OutlookデスクトップWindowsで実行しているアプリを *プレビューできます*。 テスト テナントの更新プログラム チャネル[Microsoft 365 Apps](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)変更してベータ チャネル ビルドをインストールする必要Office 365確認します。

テスト環境Office 365ベータ チャネル アプリケーションをインストールするには、次の手順を実行します。

1. テスト テナント資格情報を使用してテスト環境にサインインします。
1. [展開Office[をダウンロードし](https://www.microsoft.com/download/details.aspx?id=49117)、ローカル フォルダーに展開します。
1. ローカル フォルダーに移動し、テキスト *エディターで* configuration-Office365-x86.xml(または *** x64.xml) を開き、[チャネル] の値をに *更新* します `BetaChannel` 。
1. コマンド プロンプトを開き、ローカル フォルダー パスに移動します。
1. セットアップ `setup.exe /configure configuration-Office365-x86.xml` に応じて、実行 (または **x64.xml* ファイルを使用します)。
1. [Outlook (デスクトップ クライアント) を開き、テスト テナントの資格情報を使用してメール アカウントを設定します。
1. Open **File Office**  >  **アカウント** 約  >  **Outlook**.  
   ビルド番号が **14416** 以上で、チャネルがベータチャネルの場合は、ベータ Microsoft 365ビルドを実行しています。
1. 右上隅で、[近日] トグル **をオン** にします。
    
    :::image type="content" source="images/outlook-coming-soon.png" alt-text="その他のアプリ":::

> [!NOTE]
> [近日] ボタンOutlookコンピューターを閉じて再起動 *する必要がある* 場合があります。

テナント アカウントのテスト テナントのサポートを確認できます。

* Windows デスクトップ用に office.com、outlook.com、および Outlook で実行されている Teams 個人用タブの場合は、テスト テナントの資格情報でサインインし、左下のウィンドウで省略記号 (**...**) オプションを確認します。

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="省略記号" lightbox="images/outlook-desktop-ellipses.png":::

* outlook.com および Outlook Windowsのメッセージング拡張機能については、[メッセージの作成] リボンの [その他のアプリOutlook確認してください。

> [!NOTE]
> ベータ チャネル リリースにオプトインしているが、これらの省略記号オプションが表示されていない場合は、プレビュー機能のサポートがテナントに展開中である可能性があります。 最新の更新プログラムについては、「開発者[ブログMicrosoft Teamsを参照してください](https://devblogs.microsoft.com/microsoft365dev/)。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>バージョンの Developer Previewに切り替Teams

クライアントからパブリック サーバーに[切りDeveloper Preview](../resources/dev-preview/developer-preview-intro.md)確認Microsoft Teamsします。

1. サンドボックス テナントの資格情報Teamsサインインして、ユーザーにサインインします。
1. ユーザー プロファイルの横にある省略記号 (**...**) メニューから、[開発者プレビューについて **]**  >  **を選択します**。 ダイアログが表示されたら、[開発者プレビューに **切り替える] を選択します**。
1. アプリのTeamsしたら、ユーザー プロファイルの横にある省略記号 (**...**) メニューに移動し、ユーザープロファイルが選択Developer Preview確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="開発者向けパブリック プレビュー" lightbox="images/teams-dev-preview.png":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>プレビュー拡張機能Visual Studio CodeインストールTeams Toolkitインストールする

必要に応じて、Visual Studio Code[を使用](https://code.visualstudio.com/)して、TeamsアプリをOfficeおよびOutlook。

Teams Toolkit [(Visual Studio Code](https://aka.ms/teams-toolkit)以降) の拡張機能は、既存の Teams コードを変更して、Outlook および Office と互換性を持つコマンドを `v2.10.0` 提供します。 詳細については、「ユーザーとユーザー[の個人用Teamsを有効にする」をOfficeを参照Outlook。](extend-m365-teams-personal-tab.md)

## <a name="next-steps"></a>次の手順

- [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
- [Outlook の Teams メッセージングの拡張機能を有効にする](extend-m365-teams-message-extension.md)