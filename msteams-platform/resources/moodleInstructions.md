---
title: Moodle LMS のインストール
description: アプリの Moodle 統合アプリをインストールして構成するMicrosoft Teams
keywords: TeamsMoodle アプリ統合プラグイン
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: e5f33fa9146d0abb735e9f76aeaecea2dbdd230efe81251f9b7dcaf5700a907a
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706007"
---
# <a name="install-moodle-lms"></a>Moodle LMS のインストール

この記事では、Moodle LMS をインストールする方法について学習します。

> [!NOTE]
> IT 管理者が簡単に Moodle と Teams統合をセットアップMicrosoft 365、次の情報が更新されます。
>
> * Moodle サーバーの自動登録[(Azure Azure Active Directory) を使用AD。](https://azure.microsoft.com/services/active-directory/)
>
> * Moodle Assistant ボットの Azure への展開を 1 回クリックで行います。
>
> * チームの自動プロビジョニングと、すべてのチーム登録の自動同期、または [Moodle コース] の選択が可能です。
>
> * [Moodle] タブと [Moodle アシスタント ボット] を同期された各チームに自動インストールします。
>
> この統合で提供される機能の詳細については、「Microsoft Teams[と Moodle」を参照してください](https://education.microsoft.com/resource/3dffb3a8)。

## <a name="prerequisites"></a>前提条件

Moodle をインストールするための前提条件は次のとおりです。

* Moodle 管理者の資格情報。

* Azure AD資格情報を使用します。

* 新しいリソースを作成できる Azure サブスクリプション。

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Moodle プラグインMicrosoft 365インストールする

Moodle プラグインセットMicrosoft Teamsオープンソースの機能を使用して、Microsoft 365[の統合を行います](https://github.com/Microsoft/o365-moodle)。

### <a name="requisite-applications-and-plugins"></a>必要なアプリケーションとプラグイン

Moodle プラグインのインストールに進む前に、次のMicrosoft 365ダウンロードしてください。

1. 現在の安定版 [の Moodle をインストールしてください](https://download.moodle.org/releases/latest/)。

1. Moodle [OpenID](https://moodle.org/plugins/auth_oidc)プラグインとConnect統合[Microsoft 365](https://moodle.org/plugins/local_o365)をローカル コンピューターにダウンロードして保存します。

    > [!NOTE]
    > OpenID の統合ConnectインストールMicrosoft 365統合プラグインのインストールTeams必要です。
    >
    > さらに、テーマ[プラグインMicrosoft 365 Teams強](https://moodle.org/plugins/theme_boost_o365teams)くお勧めします。

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365Moodle プラグイン

1. 管理者として Moodle サーバーにサインインし、左側の[ナビゲーション](https://docs.moodle.org/22/en/Settings_block)パネルにある [設定] ブロックから [サイトの管理] を選択します。

1. [プラグイン] **タブを選択** し、[プラグインのインストール **] を選択します**。

1. [ZIP ファイル **からプラグインをインストールする] セクションで、[** ファイルの **選択] を選択します**。

1. 左側 **アップロードからファイル** オプションを選択し、ダウンロードしたファイルを参照し、このファイルアップロード **選択します**。

1. 左側 **のナビゲーション パネルから** [サイトの管理] を選択して、管理ダッシュボードに戻ります。 [ローカル プラグイン] まで **下にスクロールし、[** 統合 **] リンクMicrosoft 365選択** します。

    > [!IMPORTANT]
    >
    > * プロセスをMicrosoft 365ページのセットに戻す必要がある場合は、別のブラウザー タブで [Moodle Plugins] 構成ページを開いた状態にしてください。  
    >
    > * 既存の Moodle サイトをお持ちではない場合は、Azure repo の [Moodle](https://github.com/azure/moodle) に移動し、Moodle インスタンスをすばやく展開し、ニーズに合わせてカスタマイズします。

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a>2. Microsoft 365 プラグインと Azure Active Directory (Azure AD)

アプリケーション プラグインと Azure プラグイン間の接続Microsoft 365構成する必要AD。

### <a name="requisites"></a>前提条件

PowerShell スクリプトを使用して、Azure ADアプリケーションとして Moodle を登録します。 Powershell スクリプトは、次の情報を準備します。

* 新しい Azure ADアプリケーションは、Microsoft 365 Moodle プラグインで使用される、Microsoft 365テナント用です。
* テナントのアプリMicrosoft 365、プロビジョニングされたアプリに必要な返信 URL とアクセス許可を設定し、および `AppID` を返します `Key` 。

生成され、お使Microsoft 365の [Moodle プラグイン] セットアップ ページで、Azure サーバー を使用して Moodle サーバー サイトを `AppID` `Key` 構成AD。

> [!IMPORTANT]
>
> * PowerShell スクリプトは最新の構成項目で更新されないので、Moodle [3.8.0.4 および 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) および [3.8.0.5 および 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って手動で構成を完了する必要があります。
>
> * Moodle インスタンスを手動で登録する方法の詳細については、「アプリケーションとして Moodle インスタンスを登録する [」を参照してください](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>[情報フロー] の [Microsoft Teams] タブ

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. [統合Microsoft 365] ページで、[セットアップ] タブ **を選択** します。

1. **[PowerShell スクリプトのダウンロード] ボタン** を選択し、ローカル コンピューターに ZIP フォルダーとして保存します。

1. ZIP ファイルから PowerShell スクリプトを次のように準備します。 

    1. ファイルをダウンロードして抽出 `Moodle-AzureAD-Powershell.zip` します。
    1. 抽出したフォルダーを開きます。
    1. ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` プロパティ] を **選択します**。
    1. [プロパティ **] ウィンドウの**[全般] タブで、ウィンドウの下部にあるセキュリティ属性の横にあるチェック `Unblock` ボックスをオンにします。
    1. **[OK]** をクリックします。
    1. ディレクトリ パスを抽出したフォルダーにコピーします。

1. 管理者として PowerShell を実行します。

    1. [開始] を選択します。
    1. 「PowerShell」と入力します。
    1. [次へ] を **右クリックWindows PowerShell** します。
    1. [管理者 **として実行] を選択します**。

1. ディレクトリへのパスを where と入力して、未設定 `cd .../.../Moodle-AzureAD-Powershell` `.../...` のディレクトリに移動します。

1. PowerShell スクリプトを実行します。

    1. を `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 入力します。
    1. を `./Moodle-AzureAD-Script.ps1` 入力します。
    1. ポップアップ ウィンドウでMicrosoft 365管理者アカウントにサインインします。
    1. たとえば、Moodle プラグインや Moodle プラグインなど、Azure ADアプリケーションの名前を入力します。
    1. Moodle サーバーの URL を入力します。
    1. スクリプトによって **生成されたアプリケーション ID ( `AppID` )** と Application **Key( `Key` )** をコピーして保存します。

1. 次に `AppID` 、Moodle `Key` プラグインを追加し、Microsoft 365する必要があります。 [プラグインの管理] ページの [サイト管理] >統合> Microsoft 365します。

1. [セットアップ **] タブ** で、前にコピーした項目を追加し、[ `AppID` `Key` 変更の保存] **を選択します**。 ページが更新された後、新しいセクション [接続方法の選択 **] が表示されます**。

1. [接続方法 **の選択] で**、[既定]というラベルの付いたチェック ボックスをオンにし、[変更の保存 **] を再度選択** します。

1. ページが更新された後、別の新しいセクション [管理者の同意] が表示 **され&情報が表示されます**。
    1. [**管理者の同意の提供**] リンクを選択し、グローバル管理者Microsoft 365資格情報を入力し、[**同意** する] を選択してアクセス許可を付与します。
    1. [Azure ADテナント] **フィールドの横** にある [検出] **ボタンを選択** します。
    1. [URL] の **横OneDrive for Business[** 検出] ボタン **を選択** します。
    1. フィールドが設定された後、もう一度 [変更の **保存] ボタンを** 選択します。

1. [更新] **ボタンを** 選択してインストールを確認し、[変更の保存] **を選択します**。

1. Moodle サーバーと Azure サーバー間でユーザーを同期AD。 次の手順をお試しください。

    > [!NOTE]
    > 環境に応じて、この段階でさまざまなオプションを選択できます。

1. Moodle サーバーと Azure サーバー間でユーザーを同期AD。 環境に応じて、この段階でさまざまなオプションを選択できます。 次の手順をお試しください。
    1. [同期] タブ **に設定します**。

    1. [Azure **ユーザーとユーザーを同期AD]** セクションで、環境に適用するチェック ボックスをオンにします。 次の項目を選択する必要があります。  

        ✔ Azure のユーザー向け Moodle でアカウントを作成AD。

        ✔ Azure アカウントのユーザーに対して、Moodle のすべてのアカウントを更新AD。

    1. [ユーザー **作成の制限] セクション** で、Moodle に同期AD Azure ユーザーを制限するフィルターをセットアップできます。
    1. [ **ユーザー フィールド マッピング]** セクションでは、Azure のユーザー プロファイルADを Moodle ユーザー プロファイル フィールド マッピングにカスタマイズできます。
    1. [同期 **Teams]** セクションで、既存の Moodle コースの一部またはすべてのチームなどのグループを自動的に作成する場合に選択できます。

13. cron ジョブ [を検証し](https://docs.moodle.org/310/en/Cron)、最初の実行に対して手動で実行するには **、[Azure** とユーザーを同期する] セクションの [スケジュールされたタスクの管理] ADします。 これにより、[スケジュールされたタスク] **ページに移動** します。

    1. 下にスクロールして、Azure ユーザーと **同期するジョブをADし、[今すぐ** 実行] **を選択します**。
    1. 既存のコースに基づいてグループを作成する場合は、ユーザー グループを作成するジョブ **Microsoft 365** することもできます。

    > [!NOTE]
    >
    > Moodle [Cron はタスク](https://docs.moodle.org/310/en/Cron) スケジュールに従って実行されます。 既定のスケジュールは 1 日 1 回です。 ただし、すべての同期を維持するには、cron の実行頻度を高くする必要があります。

1. [プラグインの管理] ページの [**サイト**>統合> Microsoft 365に戻り、[プラグイン]**ページTeams 設定します**。

1. [アプリの **Teams 設定]** ページで、アプリの統合を有効にするために必要なTeams構成します。

    1. **OpenID** Connectを有効にするには、[認証の管理] リンクを選択し、灰色で表示されている場合は **、OpenId** Connectで目のアイコンを選択します。
    1. フレーム埋め込みを有効にするには **、[HTTP セキュリティ** ] リンクを選択し、[フレームの埋め込みを許可する] の横にあるチェック **ボックスをオンにします**。
    1. Moodle API 機能を有効にする Web サービスを有効にするには、[高度な機能] リンクを選択し、[Web サービスを有効にする] の横にあるチェック ボックスがオンになっていることを確認します。
    1. 外部サービスを有効にするには、[外部Microsoft 365]**リンクを選択** し、次の項目を選択します。  

        ✔ **[Moodle] ページの**[編集] **Microsoft 365選択** します。

        ✔ [有効] の横にあるチェック ボックス **をオンにして**、[変更の保存] **を選択します。**

    1. 認証されたユーザーのアクセス許可を編集して、Web サービス トークンの作成を許可します。

        ✔ [編集] **役割の [認証済みユーザー] リンクを選択** します。

        ✔下にスクロールし **、[Web** サービス トークンの作成] 機能を見つけて、[許可] チェック ボックス **をオン** にします。

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Moodle アシスタント ボットを Azure に展開する

無料の Moodle アシスタント ボット Microsoft Teams教師と学生が、Moodle のコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。 ボットは、このボット内の生徒や教師に、Moodle 通知Teams。 ボットは、Microsoft が管理するオープン ソース プロジェクトであり、このプロジェクトで[GitHub。](https://github.com/microsoft/Moodle-Teams-Bot)

> [!NOTE]
>
> * リソースを Azure サブスクリプションに展開します。 すべてのリソースは、無料レベルを使用 **して構成** されています。 ボットの使用状況によっては、これらのリソースのスケーリングが必要な場合があります。
>
> * ボットなしで [Moodle] タブを使用するには [、4 にスキップします](#4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>Moodle ボットの情報フロー

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

ボットをインストールするには、Microsoft Identity Platform に [ボットを登録する必要があります](https://identity.microsoft.com/Landing)。 これにより、ボットは Microsoft エンドポイントに対して認証できます。 

**ボットを登録するには**

1. [プラグインの管理] ページに移動し、[プラグイン] **を選択します**。 [統合 **Microsoft 365] の** 下で、[統合]**タブTeams 設定** 選択します。

1. [Microsoft **アプリケーション登録ポータル] リンクを選択** し、Microsoft ID でサインインします。

1. アプリの名前 (MoodleBot など) を入力し、[作成] ボタン **を選択** します。

1. アプリケーション ID **をコピーし**、[チーム] ページの [ボット アプリケーション **ID]** **フィールドに貼り設定** します。

1. [新しい **パスワードの生成] ボタンを** 選択します。 生成されたパスワードをコピーし、[チーム] ページの [**ボット アプリケーション** パスワード **] フィールドに貼り設定** します。

1. フォームの下部までスクロールし、[変更の保存] **を選択します**。

アプリケーション ID とパスワードを生成した後、ボットを Azure に展開します。

> [!div class="checklist"]
> * [Azure **に展開する**] を選択し、ボット アプリケーション ID、ボット アプリケーション パスワード、および [アカウント] ページの **[Moodle** シークレット] など、必要な情報を含むフォームTeams 設定します。 Azure の情報は、[セットアップ] ページ **に表示** されます。 
> * フォームが完成した後、チェックボックスをオンにして利用規約に同意します。
> * [購入 **] を選択します**。 すべての Azure リソースが無料層に展開されます。

リソースが Azure への展開を完了したら、メッセージング エンドポイントMicrosoft 365を構成する必要があります。 Azure でボットからエンドポイントを取得する必要があります。

1. [Azure portal](https://portal.azure.com) にサインインします。

1. 左側のウィンドウで、[リソース グループ **] を** 選択し、ボットの展開中に使用または作成したリソース グループを選択します。

1. グループ内 **のリソースの一** 覧から WebApp Bot リソースを選択します。

1. [概要 **] セクションからメッセージング** エンドポイント **をコピー** します。

1. Moodle で、お使 **設定の**[チーム] ページMicrosoft 365開きます。

1. [ボット **エンドポイント] フィールド** に、コピーした URL を貼り付け、単語メッセージを *webhook に変更します*。  URL は次のように表示する必要があります。 `https://botname.azurewebsites.net/api/webhook`

1. [**変更を保存**] を選択します。

1. 変更を保存した後、[**チーム**] タブ設定戻り、[マニフェスト ファイルのダウンロード] ボタンを選択し、さらに使用するためにアプリ マニフェスト パッケージをコンピューターに保存します。

## <a name="4-deploy-your-microsoft-teams-app"></a>4. アプリをMicrosoft Teamsする

ボットが Azure に展開され、Moodle サーバーと話をするように構成された後、アプリを展開するMicrosoft Teamsがあります。 これを行うには、前の手順の [Moodle Plugins Team Microsoft 365] 設定からダウンロードしたアプリ マニフェスト ファイルを読み込む必要があります。

アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。 詳細については、「Prepare [your Microsoft 365 テナント」を参照してください](../concepts/build-and-test/prepare-your-o365-tenant.md)。 

**アプリを展開するには** 

1. [ファイル **Microsoft Teams] を開きます**。 

1. ナビゲーション バー **の** 左下の領域にある [アプリ] アイコンを選択します。

1. オプションの **アップロードからカスタム アプリ** リンクを選択します。

   > [!NOTE]
   > グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。それ以外の場合は、メンバーであるチームのアプリのみを読み込む必要があります。

4. 以前に `manifest.zip` ダウンロードしたパッケージを選択し、[保存] を **選択します**。 アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle の [プラグイン構成] ページの **[** チーム 設定] タブからダウンロードできます。

アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。 これを行うには、チャネルに移動し、 **プラス記号** (➕) を選択し、一覧からアプリを選択します。 プロンプトに従って、チャネルへの Moodle コース タブの追加を完了します。

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. [自動作成] ウィンドウで [Moodle] タブをMicrosoft Teams

[Moodle] タブは、Microsoft Teamsで手動で作成しますが、チームがコース同期から作成されると、自動的に作成できます。 これを行うには、Moodle でアップロードされたアプリの ID Microsoft Teams構成する必要があります。

**Moodle タブの自動作成を許可するには**

1. Microsoft Teams を開きます。

1. ナビゲーション バーの左下の領域から [アプリ] アイコンを選択します。

1. アップロードされた **Moodle アプリを見つけて>** オプション アイコン **を** 選択し>コピー リンクを **選択します**。

1. テキスト エディターで、コピーしたコンテンツを貼り付けます。 これは、ht ファイルなどの URL を含&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。 URL の最後の部分 (アプリの ID など) `00112233-4455-6677-8899-aabbccddeeff` をMicrosoft Teamsします。

1. Moodle で、[Moodle プラグインの構成 **] ページTeams** [ムードル アプリ] タブMicrosoft 365開きます。

1. アプリの ID を [Moodle Microsoft Teams ID] フィールドに貼り付け、変更を保存します。

Moodle コースが同期されている場合、Microsoft Teams はチームに Moodle アプリを自動的にインストールし、Teams の [全般] チャネルに [Moodle] タブを作成し、同期する Moodle コースのコース ページを含む構成を行います。 これで、お客様の Moodle コースの操作を、お客様のアカウントから直接Microsoft Teams。

> [!NOTE]
> 機能の要求やフィードバックを共有するには、User Voice [ページをご覧ください](https://microsoftteams.uservoice.com/forums/916759-moodle)。

## <a name="see-also"></a>関連項目

- [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
- [Moodle](https://moodle.org/)
- [Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins).

