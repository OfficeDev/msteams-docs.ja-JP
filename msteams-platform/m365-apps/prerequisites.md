---
title: Teams アプリを Microsoft 365 全体に拡張するための開発環境を設定する
description: Teams アプリを Microsoft 365 全体に拡張するためのプレビュー ビルドを実行するために必要な前提条件について説明します。
ms.date: 05/24/2022
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: c0a1b265d4bc1aeb71232717ebc363d1b046da81
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189315"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張するための開発環境を設定する

Microsoft 365 全体に Teams アプリを拡張するための開発環境は、Microsoft Teams 開発に似ています。 この記事では、Outlook および Office で実行されている Teams アプリをプレビューするために、Microsoft Teams および Microsoft Office アプリケーションのプレビュー ビルドを実行するために必要な特定の構成について説明します。

開発環境をセットアップするには:

> [!div class="checklist"]
>
> * [Microsoft 365 開発者 (サンドボックス) テナントを取得し、サイドローディングを有効にします](#prepare-a-developer-tenant-for-testing)
> * [*Office 365ターゲット リリース* に Microsoft 365 テナントを登録する](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [テスト環境に Microsoft 365 Apps のベータ チャネル ビルドをインストールします](#install-office-apps-in-your-test-environment)
> * [Teams の [開発者プレビュー] バージョンに切り替える](#switch-to-the-developer-preview-version-of-teams)
> * [*省略可能*] [Microsoft Visual Studio Code 用のTeams Toolkit 拡張機能をインストールする](#install-visual-studio-code-and-teams-toolkit-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>テスト用に開発者テナントを準備する

開発環境を設定するには、Microsoft 365 開発者サブスクリプション サンドボックス テナントが必要です。 まだお持ちでない場合は、 [サンドボックス テナント](/office/developer-program/microsoft-365-developer-program-get-started) を作成するか、組織を通じてテスト テナントを取得します。

また、テナントのサイドローディングを有効にする必要もあります。

1. Microsoft 365 管理センター (https://admin.microsoft.com) テストテナントの認証情報でサインインし、サイドパネルから **Teams** を選択し、*Microsoft Teams 管理センター* を開きます。
1. 選択: ［Teams アプリ］ > [アプリの管理] > **［組織全体のアプリ設定］**。
1. **［カスタム アプリ］** で、オプションの *［カスタム アプリとの対話］* トグルを切り替えます。

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="Teams 管理センターからカスタム アプリのサイドローディングを有効にします":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Office 365 対象のリリースの開発者テナントを登録する

> [!Important]
> [Microsoft 365 開発者サンドボックス テナント](/office/developer-program/microsoft-365-developer-program-get-started) を作成し、[Office 365 Targeted リリース](#enroll-your-developer-tenant-for-office-365-targeted-releases) に登録すると、サイドロードされた Teams アプリが Outlook と Office に表示されるまでに最大 5 日かかる場合があります。

Office 365 対象のリリースにテスト テナントを登録するには:

1. 管理者の資格情報で [Microsoft 365 管理センター](https://admin.microsoft.com)にサインインします。
1. **[設定]** > **[組織設定]** > **[組織プロファイル]** の順に移動します。
1. **[リリースの基本設定]** を選択します。
1. 任意の *[ターゲット リリース]* の基本設定を選択します。
    1. **すべてのユーザー向けのターゲット リリース**
    1. **選択したユーザーのターゲット リリース**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="ターゲット リリース オプションが選択された Microsoft 365 管理センターの [リリース設定] メニュー":::

1. **[保存]** を選択します。

Office 365 リリース オプションの詳細については、*Microsoft 365 管理センター ヘルプ* の「[標準またはターゲット リリース オプションのセットアップ](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)」を参照してください。

## <a name="install-office-apps-in-your-test-environment"></a>Office アプリをテスト環境にインストールする

最近の *ベータ チャネル ビルド* を使用して、Windows デスクトップ上の Outlook で実行されている Teams アプリをプレビューできます。 テスト テナントの [Microsoft 365 Apps 更新チャネルを変更して](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)、Office 365 ベータ チャネル ビルドをインストールする必要があるかどうかを確認します。

テスト環境で Office 365 ベータ チャネル アプリケーションをインストールするには:

1. テスト テナントの資格情報を使用して、テスト環境にサインインします。
1. [[Office 展開ツール]](https://www.microsoft.com/download/details.aspx?id=49117) をダウンロードし、ローカル フォルダーに展開します。
1. ローカル フォルダーに移動し、テキスト エディターで *configuration-Office365-x86.xml* (または環境によっては **x64.xml*) を開き、*[チャネル]* 値を `BetaChannel` に更新します。
1. コマンド プロンプトを開き、ローカル フォルダーのパスに移動します。
1. `setup.exe /configure configuration-Office365-x86.xml` を実行します (または、設定によっては **x64.xml* ファイルを使用します)。
1. Outlook (デスクトップ クライアント) を開き、テスト テナント資格情報を使用してメール アカウントを設定します。
1. **［ファイル］** > **［Office アカウント］** > **［Outlook について］** を開き、Outlook の Microsoft 365 *［ベータ チャネル］* ビルドを実行していることを確認します。

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="Office アカウントから [Outlook について] にアクセスして、ベータ チャネル ビルドを実行していることを確認します。":::

1. *Microsoft Edge WebView2 ランタイム* がインストールされていることを確認します。 Windows の **［スタート］** > **［アプリと機能］** を開、**webview** を検索します。

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="windows の ［設定］ で [アプリと機能] から 「webview」 を検索します":::

    一覧に表示されない場合は、テスト環境に [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) をインストールします。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Teams の開発者プレビュー バージョンに切り替える

Microsoft Teams クライアントから [[パブリック開発者プレビュー]](../resources/dev-preview/developer-preview-intro.md) に切り替える必要があります。

1. サンドボックス テナントの資格情報を使用して Teams にサインインします。
1. ユーザープロファイルの横にある省略記号 (**...**) メニューから、**[詳細]** > **[開発者プレビュー]** の順に選択します。 ダイアログが表示されたら、**[開発者プレビューに切り替える]** を選択します。
1. Teams アプリが再起動したら、ユーザー プロファイルの横にある省略記号 (**...**) メニューに移動し、**[開発者プレビュー]** が選択されているかどうかを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams のパブリック開発者プレビュー オプション":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>Visual Studio Code と Teams Toolkit 拡張機能をインストールする

必要に応じて、[Visual Studio Code](https://code.visualstudio.com/)を使用して、Teams アプリを Office と Outlook に拡張できます。

拡張機能 [Teams Toolkit for Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` 以降) には、Outlook および Office と互換性のある既存の Teams コードを変更するのに役立つコマンドが用意されています。詳細については、「[Office および Outlook 用の Teams 個人用タブを有効にする](extend-m365-teams-personal-tab.md)」 を参照してください。

## <a name="next-step"></a>次のステップ

Microsoft 365 間で実行する Teams アプリを作成または更新します。

> [!div class="nextstepaction"]
> [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
> [!div class="nextstepaction"]
> [Outlook の Teams メッセージング 拡張機能を有効にする](extend-m365-teams-message-extension.md)
