---
title: Teams アプリを Microsoft 365 全体に拡張するための開発環境を設定する
description: Microsoft 365 全体に Teams アプリを拡張するための開発環境を設定するための要件。 Microsoft Teams と Microsoft Office アプリケーションのビルドを実行するために必要な構成について説明します。
ms.date: 05/24/2022
ms.custom: m365apps
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 64caf4784286cd3eaf2c32a28a3fe655ba88bcc7
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100954"
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

 1. テスト テナントの資格情報を使用して [Teams 管理センター](https://admin.teams.microsoft.com/dashboard) にサインインします。

 1. **Teams アプリ****の管理アプリ** > に移動します。

 1. 右上で、[ **組織全体のアプリ設定**] を選択します。

 1. [カスタム アプリ] で、[ **カスタム アプリとの対話** ] トグルをオンにして保存します。

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="スクリーンショットは、Teams 管理 センターからカスタム アプリのサイドローディングを有効にする例です":::

 1. 組織全体のアプリ設定とは別に、カスタム アプリ ポリシー設定では、ユーザーが Teams にカスタム アプリをアップロードすることもできます。 詳細については、「 [カスタム アプリ のポリシーと設定の管理](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)」を参照してください。

 1. Teams 管理センターで、 **Teams アプリ** > **のセットアップ ポリシー** に移動し、 **グローバル (組織全体の既定) ポリシー** を選択します。

 1. **[カスタム アプリのアップロード**] をオンにし、[保存] を選択 **します**。

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Office 365 対象のリリースの開発者テナントを登録する

> [!IMPORTANT]
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

### <a name="desktop"></a>Desktop

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

### <a name="mobile"></a>Mobile

ベータ プログラムに参加することで、Office アプリ for Android で実行されている Teams 個人用タブをプレビューできます。

最新の Office アプリ ベータ ビルドを物理 Android デバイスまたは Android エミュレーターにインストールするには:

1. Google Play で [サポートされている Android デバイスを](https://support.google.com/googleplay/answer/1727131)使用していることを確認します。
1. Android デバイスで **Play ストア** を起動します。.
1. Office を検索し、 **Microsoft Office: [編集] & [共有]** を選択します。
1. [ **インストール** ] ボタンを選択します。

    :::image type="content" source="images/office-android-install.png" alt-text="Microsoft Office のスクリーンショット: Google Play ストアでアプリ&共有を編集する":::

1. インストールが完了 **したら、[ベータ版への参加] セクション** で [**参加**] を選択します。

    :::image type="content" source="images/office-android-join-beta.png" alt-text="ベータ版に参加する画面のスクリーンショット":::

1. Office アプリを起動し、テスト テナントの資格情報を使用してサインインします。
1. プロファイル **(Me) >設定** を開き、メニューの下部までスクロールします。
2. Android で Office アプリ バージョン 16.0.15726.20000 以降を使用していることを確認します。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Teams の開発者プレビュー バージョンに切り替える

Microsoft Teams クライアントから [[パブリック開発者プレビュー]](../resources/dev-preview/developer-preview-intro.md) に切り替える必要があります。

1. サンドボックス テナントの資格情報を使用して Teams にサインインします。
1. ユーザープロファイルの横にある省略記号 (**...**) メニューから、**[詳細]** > **[開発者プレビュー]** の順に選択します。 ダイアログが表示されたら、**[開発者プレビューに切り替える]** を選択します。
1. Teams アプリが再起動したら、ユーザー プロファイルの横にある省略記号 (**...**) メニューに移動し、**[開発者プレビュー]** が選択されているかどうかを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams のパブリック開発者プレビュー オプション":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>Visual Studio Code と Teams Toolkit 拡張機能をインストールする

必要に応じて、[Visual Studio Code](https://code.visualstudio.com/)を使用して、Teams アプリを Office と Outlook に拡張できます。

The extension [Teams Toolkit for Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` or later) provides commands that can help modify your existing Teams code to be compatible with Outlook and Office. For more information, see [enable Teams personal tab for Office and Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-step"></a>次のステップ

Microsoft 365 間で実行する Teams アプリを作成または更新します。

> [!div class="nextstepaction"]
> [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
> [!div class="nextstepaction"]
> [Outlook の Teams メッセージング 拡張機能を有効にする](extend-m365-teams-message-extension.md)