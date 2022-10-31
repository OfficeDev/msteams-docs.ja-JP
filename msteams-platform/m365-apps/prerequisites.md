---
title: Teams アプリを Microsoft 365 全体に拡張するための開発環境を設定する
description: Microsoft 365 全体で Teams アプリを拡張するための開発環境を設定するための要件。 Microsoft Teams および Microsoft Office アプリケーションのビルドを実行するために必要な構成を把握します。
ms.date: 05/24/2022
ms.custom: m365apps
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 99050d8b8db4fac38e9d36c42a6c3efe7f1bf28d
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789913"
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

テナントのサイドローディングも有効にする必要があります。

 1. テスト テナントの資格情報を使用して [Teams 管理センター](https://admin.teams.microsoft.com/dashboard) にサインインします。

 1. **[Teams アプリ] [アプリ** > **の管理] の順** に移動します。

 1. 右上の [ **組織全体のアプリ設定**] を選択します。

 1. [カスタム アプリ] で、[ **カスタム アプリとの対話]** トグルと **[保存]** をオンにします。

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="スクリーンショットは、Teams 管理 センターからのカスタム アプリのサイドローディングを有効にする例です":::

 1. 組織全体のアプリ設定とは別に、カスタム アプリ ポリシー設定では、ユーザーがカスタム アプリを Teams にアップロードすることもできます。 詳細については、「 [カスタム アプリ のポリシーと設定を管理する](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)」を参照してください。

 1. Teams 管理センターで、[ **Teams アプリ** > **のセットアップ ポリシー**] に移動し、[ **グローバル (組織全体の既定)] ポリシー** を選択します。

 1. [ **カスタム アプリのアップロード**] をオンにし、[保存] を選択 **します**。

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

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="スクリーンショットは、ターゲット リリース オプションが選択された [リリース設定] メニュー Microsoft 365 管理センターを示す例です。":::

1. **[保存]** を選択します。

Office 365リリース オプションの詳細については、ヘルプ [の「Standard または Targeted リリース オプションの設定](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)*」Microsoft 365 管理センター* 参照してください。

## <a name="install-office-apps-in-your-test-environment"></a>Office アプリをテスト環境にインストールする

### <a name="desktop"></a>Desktop

最近の *ベータ チャネル ビルド* を使用して、Windows デスクトップ上の Outlook で実行されている Teams アプリをプレビューできます。 テスト テナントの[Microsoft 365 Apps更新チャネルを変更](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)して、Office 365 Beta Channel ビルドをインストールする必要があるかどうかを確認します。

テスト環境で Office 365 ベータ チャネル アプリケーションをインストールするには:

1. テスト テナントの資格情報を使用して、テスト環境にサインインします。
1. [[Office 展開ツール]](https://www.microsoft.com/download/details.aspx?id=49117) をダウンロードし、ローカル フォルダーに展開します。
1. ローカル フォルダーに移動し、テキスト エディターで *configuration-Office365-x86.xml* (または環境によっては **x64.xml*) を開き、*[チャネル]* 値を `BetaChannel` に更新します。
1. コマンド プロンプトを開き、ローカル フォルダー パスに移動します。
1. `setup.exe /configure configuration-Office365-x86.xml` を実行します (または、設定によっては **x64.xml* ファイルを使用します)。
1. Outlook (デスクトップ クライアント) を開き、テスト テナント資格情報を使用してメール アカウントを設定します。
1. **［ファイル］** > **［Office アカウント］** > **［Outlook について］** を開き、Outlook の Microsoft 365 *［ベータ チャネル］* ビルドを実行していることを確認します。

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="スクリーンショットは、ベータ チャネル ビルドを実行していることを確認するための Outlook の例です。":::

1. *Microsoft Edge WebView2 ランタイム* がインストールされていることを確認します。 Windows の **［スタート］** > **［アプリと機能］** を開、**webview** を検索します。

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="スクリーンショットは、Windows 設定の検索フィールドを示す例です。":::

    一覧に表示されない場合は、テスト環境に [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) をインストールします。

### <a name="mobile"></a>Mobile

ベータ プログラムに参加することで、Android 用 Office アプリで実行されている Teams の個人用タブをプレビューできます。

最新の Office アプリ ベータ版をインストールするには、物理 Android デバイスまたは Android エミュレーターにビルドします。

1. Google Play [でサポートされている Android デバイス](https://support.google.com/googleplay/answer/1727131)を使用していることを確認します。
1. Android デバイスで **Play ストア** を起動します。
1. Office を検索し、[ **Microsoft Office: 編集] & [共有**] を選択します。
1. [ **インストール** ] ボタンを選択します。

    :::image type="content" source="images/office-android-install.png" alt-text="スクリーンショットは、Microsoft Office の [Edit & Share app in Google Play Store] の [インストール] ボタンを示す例です。":::

1. インストールが完了 **したら、[ベータ版に参加する] セクション** で **[参加**] を選択します。

    :::image type="content" source="images/office-android-join-beta.png" alt-text="スクリーンショットは、[ベータ版に参加する] 画面を示す例です。":::

1. Office アプリを起動し、テスト テナントの資格情報を使用してサインインします。
1. [ **設定] >プロファイル (Me)** を開き、メニューの下部までスクロールします。
2. Android 用の Office アプリ バージョン 16.0.15726.20000 以降を使用していることを確認します。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Teams の開発者プレビュー バージョンに切り替える

Microsoft Teams クライアントから [[パブリック開発者プレビュー]](../resources/dev-preview/developer-preview-intro.md) に切り替える必要があります。

1. サンドボックス テナントの資格情報を使用して Teams にサインインします。
1. ユーザープロファイルの横にある省略記号 (**...**) メニューから、**[詳細]** > **[開発者プレビュー]** の順に選択します。 ダイアログが表示されたら、**[開発者プレビューに切り替える]** を選択します。
1. Teams アプリが再起動したら、ユーザー プロファイルの横にある省略記号 (**...**) メニューに移動し、**[開発者プレビュー]** が選択されているかどうかを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="スクリーンショットは、Teams のパブリック開発者プレビュー オプションを示す例です。":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>Visual Studio Code と Teams Toolkit 拡張機能をインストールする

必要に応じて、[Visual Studio Code](https://code.visualstudio.com/)を使用して、Teams アプリを Office と Outlook に拡張できます。

The extension [Teams Toolkit for Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` or later) provides commands that can help modify your existing Teams code to be compatible with Outlook and Office. For more information, see [enable Teams personal tab for Office and Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-step"></a>次のステップ

Microsoft 365 間で実行する Teams アプリを作成または更新します。

> [!div class="nextstepaction"]
> [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
> [!div class="nextstepaction"]
> [Outlook の Teams メッセージング 拡張機能を有効にする](extend-m365-teams-message-extension.md)
