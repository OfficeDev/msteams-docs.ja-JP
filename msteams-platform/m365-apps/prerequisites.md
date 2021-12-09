---
title: アプリケーション全体でアプリを拡張Teams環境をMicrosoft 365
description: アプリを複数のユーザーにまたがって拡張Teams前提条件を次に示Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.custom: m365apps
ms.openlocfilehash: 967e45bb59c431476ead902e1413ab743c566779
ms.sourcegitcommit: 239807b74aa222452559509d49c4f2808cd9c9ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391347"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365-preview"></a>M365 全体でアプリを拡張Teams環境をセットアップする (プレビュー)

複数のアプリをTeamsするMicrosoft 365環境は、ユーザーが開発に使用するMicrosoft Teams似ています。 この記事では、Outlook および Office で実行されている Teams アプリをプレビューするために、Microsoft Teams および Microsoft Office アプリケーションのプレビュー ビルドを実行するために必要な特定の構成について説明します。 開発環境をセットアップするには、次の必要があります。

> [!div class="checklist"]
> * [M365 開発者 (サンドボックス) テナントを取得し、サイドローディングを有効にする](#prepare-a-developer-tenant-for-testing)
> * [M365 テナントをターゲット *リリースOffice 365登録する*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [プレビュー バージョンのプレビュー バージョンにアクセスするアカウントを構成OutlookおよびOffice](#install-office-apps-in-your-test-environment)
> * [バージョンの Developer Previewに切り替Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*省略可能*][ユーザーのTeams Toolkit拡張機能をインストールVisual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>テスト用に開発者テナントを準備する

まだ存在しない場合は、開発者サブスクリプション サンドボックス[](/office/developer-program/microsoft-365-developer-program-get-started)テナントMicrosoft 365を作成するか、組織を通じてテスト テナントを取得します。

テナントを作成した後 [、Microsoft 365 管理センター](https://admin.microsoft.com)にサインインし [](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)、[すべての > Teams > Teams アプリの表示] > セットアップ ポリシー > に移動して、テナントのサイド **ローディングを有効** にする必要があります。  [カスタム アプリ **アップロードを切り替える] と** **[保存] をオンにします**。

既存のテナントがある場合は、サインインして [アプリ] を選択してサイドローディングが有効Teams確認 **します**。 テナントでサイドローディング **がアップロード** 場合は、カスタム アプリ オプションの一覧が表示されます。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="[アプリ] パネルから [カスタム アプリをアップロードする] オプションが表示Teamsテナントでサイドローディングが有効になります。":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>ターゲットリリースの開発者テナントOffice 365登録する

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365 開発者](https://devblogs.microsoft.com/microsoft365dev/category/teams/)向けブログの最新情報を参照して、outlook.com および office.com アプリの Teams サポートがテスト テナントで利用可能か確認してください。

テスト Teamsまたは outlook.com で office.com するアプリをプレビューするには、テスト テナントで対象Office 365[を選択します](/microsoft-365/admin/manage/release-options-in-office-365#targeted-release)。

1. テスト テナントの資格情報Microsoft 365 管理センター使用してサインインし、[組織プロファイル] タブ *([* 組織の設定] 設定 )) に [](https://admin.microsoft.com/AdminPortal/Home?#/Settings/OrganizationProfile)  >    >>  **移動** します。 [ **リリースの基本設定] を選択** し、[対象のリリース *] 基本設定のいずれかを* 選択します。

  :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Microsoft 365 管理センターターゲット リリース オプションを選択した場合の [リリースの基本設定] メニュー":::

  リリース オプションの詳細についてはOffice 365ヘルプの「標準 [](/microsoft-365/admin/manage/release-options-in-office-365)リリース オプションまたはターゲット リリース オプションを設定する」*をMicrosoft 365 管理センターしてください*。

1. テスト テナントの資格情報でサインインTeamsして、office.com および outlook.com で実行されている個人用タブのサポートがテナントに含まれています。 サイド バーに省略記号 (**...**) オプションが表示される場合 (サイドロードされた Teams個人用タブのエントリ ポイント) は、テナントでサポートされています。

  :::image type="content" source="images/outlook-web-ellipses.png" alt-text="省略記号 '...'エントリ ポイントからサイドロードTeamsタブ アプリ outlook.com":::

1. メッセージの作成領域で [その他のアプリ outlook.com を確認して、Outlookメッセージング拡張機能のテスト テナントのサポートを確認します。 

> [!NOTE]
> 対象のリリースにオプトインしているが、これらのオプションが表示されていない場合は、プレビュー機能のサポートがまだテナントに展開中である可能性があります。 最新の更新プログラムについては、「開発者[ブログMicrosoft Teamsを参照してください](https://devblogs.microsoft.com/microsoft365dev/category/teams/)。

## <a name="install-office-apps-in-your-test-environment"></a>テストOfficeアプリをインストールする

> [!IMPORTANT]
> 最新の Microsoft Teams [- Microsoft 365 開発者](https://devblogs.microsoft.com/microsoft365dev/category/teams/)向けブログを参照して、Teams メッセージ拡張機能の Outlook デスクトップ サポートがテスト テナントで利用できるWindows を確認します。

最近のベータTeamsビルドを使用して、OutlookデスクトップWindowsアプリを *プレビュー* できます。 テスト環境にOutlookベータ チャネル ビルドをインストールするには、テスト テナントの更新チャネルMicrosoft 365 Apps変更する[](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)必要があります。

テスト環境にベータ チャネル アプリケーションOffice 365 *インストール* する手順を次に示します。

1. テスト テナント アカウントを使用してテスト環境にログインします。
1. [展開Office[をダウンロードし](https://www.microsoft.com/download/details.aspx?id=49117)、ローカル フォルダーに展開します。
1. テキスト *configuration-Office365-x86.xml* (または環境に応 *じて*、 *x64.xml) を開き、[チャネル] の値をに *更新* します `BetaChannel` 。
1. 管理者特権のコマンド プロンプトで、セットアップに応じて `setup.exe /configure configuration-Office365-x86.xml` 、*x64.xmlファイルを実行します。**
1. [Outlook (デスクトップ クライアント) を開き、テスト テナントの資格情報を使用してメール アカウントを設定します。
1. [Outlook] で、[ファイルOffice アカウントの概要] Outlook を開き、現在ベータ チャネルに参加し、ビルド番号が  >    >  **14416** 以上である必要があります。
1. クライアント ウィンドウの **隅にある**[近日Outlook切り替えます。

   :::image type="content" source="images/outlook-coming-soon.png" alt-text="デスクトップの [近日公開] Outlook 'On'} に切り替え":::

  > [!NOTE]
  > [近日] ボタンOutlookコンピューターを閉じて再起動 *する必要がある* 場合があります。

テナントが Outlook for Windows デスクトップで実行されている Teams 個人用タブをサポートしている場合は、テスト テナントの資格情報でサインインし、サイド バー (サイドロードされた Teams 個人用タブのエントリ ポイント) の省略記号 (**...**) オプションを探します。

:::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="省略記号 '...'デスクトップ用にサイドロードTeamsタブ アプリOutlookエントリ ポイント":::

同様に、Outlook Windows デスクトップのメッセージング拡張機能に対するテスト テナントのサポートを確認するには、Outlook 新規作成メッセージリボンの [その他のアプリ] オプションを確認します。

> [!NOTE]
> ベータ チャネル リリースにオプトインしているが、これらの省略記号のオプションが表示されていない場合は、プレビュー機能のサポートがまだテナントに展開中である可能性があります。 最新の更新プログラムについては、「開発者[ブログMicrosoft Teamsを参照してください](https://devblogs.microsoft.com/microsoft365dev/category/teams/)。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>バージョンの Developer Previewに切り替Teams

クライアントからパブリック サーバーにオプト [*インDeveloper Preview*](../resources/dev-preview/developer-preview-intro.md)確認Microsoft Teamsします。

1. サンドボックス テナント アカウントTeamsにサインインします。
1. ユーザー プロファイルの横にある省略記号 (**...**) メニューから、[概要] を選択し、[ **開発者プレビュー]** **オプションを選択** します。
1. ダイアログが表示されたら、[開発者プレビューに切り替える] を選択してTeamsを再起動し、Developer Previewが有効になっているか確認します。

:::image type="content" source="images/teams-dev-preview.png" alt-text="[省略Teams] メニューの [概要] を開き、[Developer Preview] オプションがオンに設定されているのを確認します。":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>プレビュー拡張機能Visual Studio CodeインストールTeams Toolkitインストールする

必要に応じて、アプリをVisual Studio Code[し](https://code.visualstudio.com/)、Teamsにアプリを拡張Office活用Outlook。

Teams Toolkit [(Visual Studio Code](https://aka.ms/teams-toolkit)以降) の拡張機能は、既存の Teams コードを変更して、Outlook および Office と互換性を持つコマンドを `v2.10.0` 提供します。 引き続[き、Teamsの個人用タブを有効Office、Outlook](extend-m365-teams-personal-tab.md)を参照してください。

## <a name="next-steps"></a>次の手順

- [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
- [Outlook の Teams メッセージングの拡張機能を有効にする](extend-m365-teams-message-extension.md)