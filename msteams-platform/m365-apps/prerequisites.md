---
title: Microsoft 365間でTeams アプリを拡張するための開発環境を設定する
description: Teams アプリをMicrosoft 365に拡張するための前提条件を次に示します。
ms.date: 02/11/2022
ms.openlocfilehash: 094da29fdb871ef4af091e32e123e2d644b7445f
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104071"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Microsoft 365間でTeams アプリを拡張するための開発環境を設定する

> [!NOTE]
> チーム アプリをMicrosoft 365全体に拡張することは、現在[、パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ利用できます。

Microsoft 365全体にTeams アプリを拡張するための開発環境は、Microsoft Teams開発に似ています。 この記事では、OutlookおよびOfficeで実行されているTeams アプリをプレビューするために、Microsoft Teams アプリケーションとMicrosoft Office アプリケーションのプレビュー ビルドを実行するために必要な特定の構成について説明します。

開発環境をセットアップするには:

> [!div class="checklist"]
>
> * [開発者 (サンドボックス) テナントMicrosoft 365取得し、サイドローディングを有効にする](#prepare-a-developer-tenant-for-testing)
> * [*Office 365ターゲット リリースにMicrosoft 365 テナントを登録する*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [OutlookとOfficeのプレビュー バージョンにアクセスするようにアカウントを構成する](#install-office-apps-in-your-test-environment)
> * [開発者プレビュー バージョンのTeamsに切り替える](#switch-to-the-developer-preview-version-of-teams)
> * [*省略可能*][Microsoft Visual Studio Code のTeams Toolkit拡張機能をインストール](#install-visual-studio-code-and-teams-toolkit-preview-extension)する

## <a name="prepare-a-developer-tenant-for-testing"></a>テスト用に開発者テナントを準備する

開発環境を設定するには、Microsoft 365開発者サブスクリプションサンドボックス テナントが必要です。 まだお持ちでない場合は、 [サンドボックス テナント](/office/developer-program/microsoft-365-developer-program-get-started) を作成するか、組織を通じてテスト テナントを取得します。

テナントを作成したら、テナントのサイドローディングを有効にする必要があります。 [サイドローディングを有効にする](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)方法に関するページを参照してください。 サイドローディングが有効になっているかどうかを確認するには、Teamsにサインインし、[**アプリ**] を選択し、**カスタム アプリ オプションアップロード** 確認します。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="カスタム アプリ オプションをアップロードする":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Office 365対象のリリースの開発者テナントを登録する

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/) の最新の更新プログラムを参照して、Teams アプリのOutlook.com と Office.com のサポートがテスト テナントで利用できるかどうかを確認してください。

Office 365対象のリリースにテスト テナントを登録するには:

1. テスト テナントの資格情報[を使用してMicrosoft 365 管理センター](https://admin.microsoft.com)にサインインします。
1. **設定** > **Org 設定** > **Organization プロファイルに移動します**。
1. [ **リリースの基本設定]** を選択します。
1. *任意のターゲット リリース* の基本設定を選択します。
    1. **すべてのユーザー向けのターゲット リリース**
    1. **選択したユーザーのターゲット リリース**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="[ターゲット リリース] オプションが選択された [リリースの基本設定] メニューをMicrosoft 365 管理センターする":::

1. **[保存]** を選択します。

Office 365リリース オプションの詳細については、*Microsoft 365 管理センターヘルプ*[の「Standard または Targeted リリース オプションの設定](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)」を参照してください。

## <a name="install-office-apps-in-your-test-environment"></a>Office アプリをテスト環境にインストールする

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365 開発者ブログ](https://devblogs.microsoft.com/microsoft365dev/)の最新の更新プログラムを参照して、テスト テナントでTeamsメッセージ拡張機能のWindowsデスクトップ サポートのOutlookを使用できるかどうかを確認してください。

最近の *ベータ チャネル ビルド* を使用して、Windows デスクトップ上のOutlookで実行されているTeamsアプリをプレビューできます。 テスト テナントの[Microsoft 365 Apps更新チャネルを変更して、Office 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)ベータ チャネル ビルドをインストールする必要があるかどうかを確認します。

テスト環境Office 365ベータ チャネル アプリケーションをインストールするには:

1. テスト テナントの資格情報を使用して、テスト環境にサインインします。
1. [Office展開ツール](https://www.microsoft.com/download/details.aspx?id=49117)をダウンロードし、ローカル フォルダーに展開します。
1. ローカル フォルダーに移動し、テキスト エディター *でconfiguration-Office365-x86.xml* (または環境に応じて **x64.xml*) を開き、 *Channel* 値 `BetaChannel`を .
1. コマンド プロンプトを開き、ローカル フォルダーのパスに移動します。
1. セットアップに応じて、**x64.xml* ファイルを実行`setup.exe /configure configuration-Office365-x86.xml`します (または使用します)。
1. Outlook (デスクトップ クライアント) を開き、テスト テナント資格情報を使用してメール アカウントを設定します。
1. **ファイル** > **Office AccountAbout** >  **Outlookを** 開きます。  
   ビルド番号が **14416** 以上で、チャネルが *ベータ チャネル* の場合は、ベータ チャネル ビルドMicrosoft 365実行しています。
1. 右上隅にある [ **近日公開** 予定] トグルをオンにします。

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Outlookの [近日公開予定] トグル オプション":::

> [!NOTE]
> [*近日* 公開予定] ボタンを表示するには、Outlookを閉じてコンピューターを再起動する必要がある場合があります。

テナント アカウントのテスト テナント サポートを確認できます。

* Windows デスクトップの office.com、outlook.com、Outlookで実行されている個人用タブをTeamsするには、テスト テナントの資格情報でサインインし、OfficeまたはOutlookの左側のサイドバーで省略記号 (**...**) オプションを確認します。

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Outlookの左側のサイドバーにある省略記号 ('..') オプション":::

* outlook.com のメッセージ拡張機能とWindowsのOutlookについては、メッセージ作成ウィンドウの下部にある **[その他のアプリ**] オプションOutlookオンにします。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Outlook作成メッセージ ウィンドウの [その他のアプリ] オプション":::

> [!NOTE]
> ベータ チャネルリリースにオプトインしているが、これらの省略記号オプションが表示されない場合は、プレビュー機能のサポートがテナントにロールアウト中である可能性があります。 最新の更新プログラムについては、[開発者ブログMicrosoft Teams](https://devblogs.microsoft.com/microsoft365dev/)参照してください。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>開発者プレビュー バージョンのTeamsに切り替える

Microsoft Teams クライアントから[パブリック開発者プレビュー](../resources/dev-preview/developer-preview-intro.md)に切り替える必要があります。

1. サンドボックス テナントの資格情報を使用してTeamsにサインインします。
1. ユーザー プロファイルの横にある省略記号 (**...**) メニューから **AboutDeveloper プレビュー****を選択** します > 。 ダイアログが表示されたら、[ **開発者プレビューに切り替える**] を選択します。
1. Teams アプリが再起動したら、ユーザー プロファイルの横にある省略記号 (**...**) メニューに移動し、**Developer Preview** が選択されているかどうかを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teamsのパブリック開発者プレビュー オプション":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Visual Studio CodeとTeams Toolkitプレビュー拡張機能をインストールする

必要に応じて、[Visual Studio Code](https://code.visualstudio.com/)を使用して、Teams アプリをOfficeとOutlookに拡張できます。

[Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`またはそれ以降) の拡張機能Teams Toolkitには、OutlookおよびOfficeと互換性を持つ既存のTeams コードを変更するのに役立つコマンドが用意されています。 詳細については、「[OfficeとOutlookの個人用タブTeams有効にする](extend-m365-teams-personal-tab.md)」を参照してください。

## <a name="next-steps"></a>次の手順

* [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
* [OutlookのTeams メッセージ拡張機能を有効にする](extend-m365-teams-message-extension.md)
