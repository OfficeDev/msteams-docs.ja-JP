---
title: Teams アプリを Microsoft 365 全体に拡張するための開発環境を設定する
description: Teams アプリを Microsoft 365 に拡張するための前提条件を次に示します。
ms.date: 02/11/2022
ms.localizationpriority: high
ms.openlocfilehash: 483ae6982dd51a16573655ed14dc93577642ba4b
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111501"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張するための開発環境を設定する

> [!NOTE]
> Teams アプリを Microsoft 365 全体に拡張することは、現在、[パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ利用できます。

Microsoft 365 全体に Teams アプリを拡張するための開発環境は、Microsoft Teams 開発に似ています。 この記事では、Outlook および Office で実行されている Teams アプリをプレビューするために、Microsoft Teams および Microsoft Office アプリケーションのプレビュー ビルドを実行するために必要な特定の構成について説明します。

開発環境をセットアップするには:

> [!div class="checklist"]
>
> * [Microsoft 365 開発者 (サンドボックス) テナントを取得し、サイドローディングを有効にします](#prepare-a-developer-tenant-for-testing)
> * [*Office 365ターゲット リリース* に Microsoft 365 テナントを登録する](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Outlook と Office アプリのプレビュー バージョンにアクセスするようにアカウントを構成する](#install-office-apps-in-your-test-environment)
> * [Teams の [開発者プレビュー] バージョンに切り替える](#switch-to-the-developer-preview-version-of-teams)
> * [*省略可能*] [Microsoft Visual Studio Code 用のTeams Toolkit 拡張機能をインストールする](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>テスト用に開発者テナントを準備する

開発環境を設定するには、Microsoft 365 開発者サブスクリプション サンドボックス テナントが必要です。 まだお持ちでない場合は、 [サンドボックス テナント](/office/developer-program/microsoft-365-developer-program-get-started) を作成するか、組織を通じてテスト テナントを取得します。

テナントを作成したら、テナントのサイドローディングを有効にする必要があります。「[サイドローディングを有効にする](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)」を参照してください。 サイドローディングが有効になっているかどうかを確認するには、Teams にログインし、**[アプリ]** を選択してから、**[カスタム アプリのアップロード]** オプションをオンにします。

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="[カスタム アプリのアップロード]":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Office 365 対象のリリースの開発者テナントを登録する

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365 開発者向けブログ](https://devblogs.microsoft.com/microsoft365dev/) の最新の更新プログラムを参照して、Teams アプリのOutlook.com と Office.com のサポートがテスト テナントで利用できるかどうかを確認してください。

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

> [!IMPORTANT]
> テスト テナントが Outlook for Windows デスクトップで Teams メッセージ拡張機能をサポートできるかどうかを確認するには、「[Microsoft Teams - Microsoft 365 開発者ブログ](https://devblogs.microsoft.com/microsoft365dev/)」の最新の更新情報を参照してください。

最近の *ベータ チャネル ビルド* を使用して、Windows デスクトップ上の Outlook で実行されている Teams アプリをプレビューできます。 テスト テナントの [Microsoft 365 Apps 更新チャネルを変更して](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016)、Office 365 ベータ チャネル ビルドをインストールする必要があるかどうかを確認します。

テスト環境で Office 365 ベータ チャネル アプリケーションをインストールするには:

1. テスト テナントの資格情報を使用して、テスト環境にサインインします。
1. [[Office 展開ツール]](https://www.microsoft.com/download/details.aspx?id=49117) をダウンロードし、ローカル フォルダーに展開します。
1. ローカル フォルダーに移動し、テキスト エディターで *configuration-Office365-x86.xml* (または環境によっては **x64.xml*) を開き、*[チャネル]* 値を `BetaChannel` に更新します。
1. コマンド プロンプトを開き、ローカル フォルダーのパスに移動します。
1. `setup.exe /configure configuration-Office365-x86.xml` を実行します (または、設定によっては **x64.xml* ファイルを使用します)。
1. Outlook (デスクトップ クライアント) を開き、テスト テナント資格情報を使用してメール アカウントを設定します。
1. **[ファイル]** > **[Office アカウント]** > **[Outlook について]** を開きます。  
   ビルド番号が **14416** 以上で、チャネルが *[ベータ チャネル]* の場合は、ベータ チャネル ビルド Microsoft 365 を実行しています。
1. 右上隅にある **[近日公開]** トグルをオンにします。

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Outlookの [近日公開] トグル オプション":::

> [!NOTE]
> *[近日公開]* ボタンを表示するには、Outlook を閉じてコンピューターを再起動する必要がある場合があります。

テナント アカウントのテスト テナント サポートを確認できます。

* Office.com、outlook.com、および Outlook for Windows デスクトップで実行されている Teams の個人用タブの場合は、テスト テナントの資格情報を使用してサインインし、Office または Outlook の左側のサイドバーにある省略記号 (**...**) オプションを確認します。

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Outlook の左側のサイドバーにある省略記号 ('..') オプション":::

* Outlook.com および Outlook for Windows のメッセージ拡張機能については、Outlook メッセージ作成ウィンドウの下部にある **[その他のアプリ]** オプションを確認してください。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Outlook メッセージ作成ウィンドウの [その他のアプリ] オプション":::

> [!NOTE]
> ベータ チャネルリリースにオプトインしているのにこれらの省略記号オプションが表示されない場合は、プレビュー機能のサポートがテナントにロールアウト中である可能性があります。 最新の更新プログラムについては、「[Microsoft Teams 開発者ブログ](https://devblogs.microsoft.com/microsoft365dev/)」を参照してください。

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Teams の開発者プレビュー バージョンに切り替える

Microsoft Teams クライアントから [[パブリック開発者プレビュー]](../resources/dev-preview/developer-preview-intro.md) に切り替える必要があります。

1. サンドボックス テナントの資格情報を使用して Teams にサインインします。
1. ユーザープロファイルの横にある省略記号 (**...**) メニューから、**[詳細]** > **[開発者プレビュー]** の順に選択します。 ダイアログが表示されたら、**[開発者プレビューに切り替える]** を選択します。
1. Teams アプリが再起動したら、ユーザー プロファイルの横にある省略記号 (**...**) メニューに移動し、**[開発者プレビュー]** が選択されているかどうかを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams のパブリック開発者プレビュー オプション":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Visual Studio Code とTeams Toolkit プレビュー拡張機能をインストールする

必要に応じて、[Visual Studio Code](https://code.visualstudio.com/)を使用して、Teams アプリを Office と Outlook に拡張できます。

[Teams Toolkit for Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`またはそれ以降) の拡張機能には、Outlook および Office と互換性を持つ既存の Teams コードを変更するのに役立つコマンドが用意されています。 詳細については、「[Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)」を参照してください。

## <a name="next-steps"></a>次の手順

* [Office と Outlook の [Teams パーソナル] タブを有効にする](extend-m365-teams-personal-tab.md)
* [Outlook の Teams メッセージング 拡張機能を有効にする](extend-m365-teams-message-extension.md)
