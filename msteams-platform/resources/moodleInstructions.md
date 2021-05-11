---
title: Moodle LMS のインストール
description: アプリの Moodle 統合アプリをインストールして構成するMicrosoft Teams
keywords: TeamsMoodle アプリ統合プラグイン
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 2a99acbe9bc618ea940af3bbe898b30d342ad0cf
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058356"
---
# <a name="install-moodle-lms"></a>Moodle LMS のインストール

Moodle は、一般的なオープン ソース学習管理システム (LMS) です。 この機能は現在、Microsoft Teams。 この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をし、通知を直接通知Teams。

IT 管理者が簡単にこの統合をセットアップするために、オープン ソース Microsoft 365 Moodle Plugin は次の機能で更新されます。

* Moodle サーバーの自動登録 (Azure Azure Active Directory) を使用AD。 [](https://azure.microsoft.com/services/active-directory/)
* Moodle Assistant ボットの Azure への展開を 1 回クリックで行います。
* チームの自動プロビジョニングと、すべてのチーム登録の自動同期、または [Moodle コース] の選択が可能です。
* [Moodle] タブと [Moodle アシスタント ボット] を同期された各チームに自動インストールします。

この統合で提供される機能の詳細については、「Microsoft Teams[と Moodle」を参照してください](https://education.microsoft.com/resource/3dffb3a8)。

## <a name="prerequisites"></a>前提条件

Moodle アプリケーションをインストールして構成するための前提条件を次に示します。 

1. Moodle 管理者の資格情報。

1. Azure AD資格情報を使用します。

1. 新しいリソースを作成できる Azure サブスクリプション。

**Moodle アプリケーションをインストールして構成するには** 

次の手順を実行して、Moodle アプリケーションをインストールして構成します。 

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Moodle プラグインMicrosoft 365インストールする

このツールの Moodle 統合Microsoft Teams、Moodle プラグイン セットのオープンソース[Microsoft 365を使用します](https://github.com/Microsoft/o365-moodle)。 Moodle サーバーにプラグインをインストールするには、次のアプリケーションがインストールされている必要があります。

1. 現在 [の安定版の Moodle](https://download.moodle.org/releases/latest/)です。

1. Moodle [OpenID Connect、Microsoft 365](https://moodle.org/plugins/auth_oidc)にダウンロード[](https://moodle.org/plugins/local_o365)して保存された統合プラグインを使用します。

   > [!NOTE]
   > OpenID の統合ConnectインストールMicrosoft 365統合プラグインのインストールTeams必要です。 さらに、テーマ プラグイン[Microsoft 365 Teams強](https://moodle.org/plugins/theme_boost_o365teams)くお勧めします。

1. 管理者として Moodle サーバーにサインインし、左側の[ナビゲーション](https://docs.moodle.org/22/en/Settings_block)パネルにある [設定] ブロックから [サイトの管理] を選択します。

1. [プラグイン] **タブを選択** し、[プラグインのインストール **] を選択します**。

1. [ZIP ファイル **からプラグインをインストールする] セクションで、[** ファイルの **選択] ボタンを選択** します。

1. 左側 **アップロードファイル オプション** を選択し、ダウンロードしたファイルを参照し、このファイルのアップロード **選択します**。

1. 左側の **ナビゲーション パネルから** [サイトの管理] を選択して、管理ダッシュボードに戻ります。 [ローカル プラグイン] まで **下にスクロールし、[** 統合 **] リンクMicrosoft 365選択** します。 

> [!IMPORTANT]
>
> * プロセスをMicrosoft 365ページのセットに戻す必要がある場合は、別のブラウザー タブで[Moodle Plugin]構成ページを開いた状態にしてください。  <br/><br/>
> * 既存の Moodle サイトをお持ちではない場合は、Azure [repo](https://github.com/azure/moodle) で Moodle をチェックアウトして、Moodle インスタンスをすばやく展開し、ニーズに合わせてカスタマイズできます。

## <a name="2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>2. Microsoft 365 プラグインと Azure Active Directory (Azure AD)

Moodle を Azure サーバーにアプリケーションとして登録するAD。 PowerShell スクリプトを使用してこのプロセスを完了します。 PowerShell スクリプトは、新しい Azure AD アプリケーションをMicrosoft 365、このアプリケーションは Moodle プラグインMicrosoft 365します。 スクリプトは、Microsoft 365 テナント用にアプリをプロビジョニングし、プロビジョニングされたアプリに必要な返信 URL とアクセス許可を設定し、およびを返 `AppID` します `Key` 。 生成された[Moodle プラグイン] セットアップ ページMicrosoft 365を使用して、Azure サーバー を使用して Moodle サーバー サイト `AppID` `Key` を構成AD。

> [!IMPORTANT]
> * PowerShell スクリプトは最新の構成項目で更新されないので、Moodle [3.8.0.4 および 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) および [3.8.0.5 および 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って構成を手動で完了する必要があります。 </br></br>
> * PowerShell スクリプトが自動化している手動手順の詳細については、「アプリケーションとして Moodle インスタンスを登録する [」を参照してください](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>[情報フロー] の [Microsoft Teams] タブ

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. [統合Microsoft 365] ページで、[セットアップ] タブ **を選択** します。

1. **[PowerShell スクリプトのダウンロード] ボタンを** 選択し、ローカル コンピューターに保存します。

1. ZIP ファイルから PowerShell スクリプトを準備する必要があります。 ZIP ファイルから PowerShell スクリプトを準備するには、次の手順を実行します。

    1. ファイルをダウンロードして抽出 `Moodle-AzureAD-Powershell.zip` します。
    1. 抽出したフォルダーを開きます。
    1. ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` プロパティ] を **選択します**。
    1. [プロパティ **] ウィンドウの**[全般] タブで、ウィンドウの下部にある Security 属性の横にあるボックス `Unblock` をオンにします。
    1. **[OK]** を選択します。
    1. ディレクトリ パスを抽出したフォルダーにコピーします。

1. 管理者として PowerShell を実行します。

    1. [開始] を選択します。
    1. 「PowerShell」と入力します。
    1. [ファイル] を右クリックWindows PowerShell。
    1. [管理者 **として実行] を選択します**。

1. ディレクトリへのパスを where と入力して、未設定 `cd .../.../Moodle-AzureAD-Powershell` `.../...` のディレクトリに移動します。

1. PowerShell スクリプトを実行します。

    1. を `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` 入力します。
    1. を `./Moodle-AzureAD-Script.ps1` 入力します。
    1. ポップアップ ウィンドウでMicrosoft 365管理者アカウントにサインインします。
    1. Azure AD アプリケーションの名前 (例: Moodle/Moodle プラグイン) を入力します。
    1. Moodle サーバーの URL を入力します。
    1. スクリプトによって **生成された** アプリケーション ID と **アプリケーション キー** をコピーして保存します。

1. 次に、Moodle プラグイン `AppID` `Key` を追加し、Microsoft 365する必要があります。 プラグインの管理ページに戻ります。 フローは、サイト管理とプラグイン➡統合➡ Microsoft 365です。

1. [セットアップ **] タブで** 、前にコピーした **アプリケーション ID** と **アプリケーション** キーを追加し、[変更の保存] **を選択します**。

1. ページが更新された後、新しいセクション [接続方法の選択 **] が表示されます**。 [既定値] というラベルの **付いたチェック ボックスをオン** にし、[変更の **保存] を再度選択** します。

1. ページが更新された後、別の新しいセクション [管理者の同意] が表示 **され&情報が表示されます**。
    1. [**管理者の同意の提供**] リンクを選択し、グローバル管理者Microsoft 365資格情報を入力し、[**同意** する] を選択してアクセス許可を付与します。
    1. [Azure ADテナント] **フィールドの横** にある [検出] **ボタンを選択** します。
    1. [URL] の **横OneDrive for Business[** 検出] ボタン **を選択** します。
    1. フィールドが設定された後、もう一度 [変更の **保存] ボタンを** 選択します。

1. [更新] **ボタンを** 選択してインストールを確認し、[変更の保存 **] を選択します**。

1. Moodle サーバーと Azure サーバー間でユーザーを同期AD。 環境に応じて、この段階でさまざまなオプションを選択できます。 次の手順をお試しください。
    1. [同期]**タブに設定する**
    1. [Azure **ユーザーとユーザーを同期AD]** セクションで、環境に適用するチェック ボックスをオンにします。 次の項目を選択する必要があります。  

        ✔ Azure のユーザー向け Moodle でアカウントを作成AD。 
        ✔ Azure アカウントのユーザーに対して、Moodle のすべてのアカウントを更新AD。  

    1. [ユーザー **作成の制限] セクション** で、Moodle に同期AD Azure ユーザーを制限するフィルターをセットアップできます。
    1. [ **ユーザー フィールド マッピング]** セクションでは、Azure のユーザー プロファイルADを Moodle ユーザー プロファイル フィールド マッピングにカスタマイズできます。
    1. [同期 **Teams]** セクションで、既存の Moodle コースの一部またはすべてのチームなどのグループを自動的に作成する場合に選択できます。

> [!NOTE]
> Moodle [Cron はタスク](https://docs.moodle.org/310/en/Cron) スケジュールに従って実行されます。 既定のスケジュールは 1 日 1 回です。 ただし、すべての同期を維持するには、cron の実行頻度を高くする必要があります。

13. cron ジョブ [を検証し](https://docs.moodle.org/310/en/Cron)、最初の実行に対して手動で実行するには **、[Azure** とユーザーを同期する] セクションの [スケジュールされたタスクの管理] ADします。 これにより、[スケジュールされたタスク] **ページに移動** します。

    1. 下にスクロールして、Azure ユーザーと **同期するジョブをADし、[今すぐ** 実行] **を選択します**。
    1. 既存のコースに基づいてグループを作成する場合は、ユーザー グループを作成するジョブ **Microsoft 365** することもできます。

1. プラグインの管理ページに戻ります。 ナビゲーション フローは、サイト管理とプラグイン➡ Integratio ➡ Microsoft 365です。 次に、[選択] ページ **Teams 設定** します。 アプリの統合を有効にするには、いくつかのTeamsする必要があります。

    1. **OpenID** Connectを有効にするには、[認証の管理] リンクを選択し、灰色で表示されている場合は **、OpenId** Connectで目のアイコンを選択します。
    1. フレームの埋め込みを有効にする。 **[HTTP セキュリティ] リンクを選択** し、[フレームの埋め込みを許可する] の **横にあるチェック ボックスをオンにします**。
    1. Moodle API 機能を有効にする Web サービスを有効にする。 [高度 **な機能] リンクを** 選択し、[Web サービスを有効にする] の横にある **チェック ボックスがオンになっていることを** 確認します。
    1. 外部サービスを有効にMicrosoft 365。 次に、[ **外部サービス] リンク** を選択します。  

        ✔ **[Moodle] ページの**[編集] **Microsoft 365選択** します。  
        ✔ [有効] の横にあるチェック ボックスを **オンにし、[** 変更の保存] **を選択します。**

    1. 認証されたユーザーのアクセス許可を編集して、Web サービス トークンの作成を許可します。 [編集] **役割の [認証されたユーザー] リンクを選択** します。 下にスクロールして、[Web サービス **トークンの作成] 機能を見** つけて、[許可] チェック ボックス **をオン** にします。

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Moodle アシスタント ボットを Azure に展開する

無料の Moodle アシスタント ボットMicrosoft Teams教師と学生が、Moodle のコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。 ボットは、このボット内の生徒や教師に、Moodle 通知Teams。 ボットは、Microsoft が管理するオープン ソース プロジェクトであり、このプロジェクトで[GitHub。](https://github.com/microsoft/Moodle-Teams-Bot)

> [!NOTE]
> * このセクションでは、リソースを Azure サブスクリプションに展開する必要があります。 無料レベルを使用して構成されたすべての **リソース ウェア** 。 ボットの使用状況に応じて、これらのリソースをスケーリングする必要があります。
> * ボットなしで [Moodle] タブを使用するには [、4 にスキップします](#4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>Moodle ボットの情報フロー

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

ボットをインストールするには、Microsoft Identity Platform に [ボットを登録する必要があります](https://identity.microsoft.com/Landing)。 これにより、ボットは Microsoft エンドポイントに対して認証できます。 

**ボットを登録するには:**

1. プラグインの管理ページに移動します。 [プラグイン **] に移動します**。 [統合 **Microsoft 365] の** 下で、[統合]**タブTeams 設定** 選択します。

1. [Microsoft **アプリケーション登録ポータル] リンクを選択** し、Microsoft ID でサインインします。

1. アプリの名前 (MoodleBot など) を入力し、[作成] ボタン **を選択** します。

1. アプリケーション ID **をコピーし**、[チーム] ページの [ボット アプリケーション **ID]** **フィールドに貼り設定** します。

1. [新しい **パスワードの生成] ボタンを** 選択します。 生成されたパスワードをコピーし、[チーム] ページの [**ボット アプリケーション** パスワード **] フィールドに貼り設定** します。

1. フォームの下部までスクロールし、[変更の保存] **を選択します**。

アプリケーション ID とパスワードを生成すると、次にボットを Azure に展開します。

> [!div class="checklist"]
> * [Azure **に展開する**] ボタンを選択し、必要な情報 (ボット アプリケーション ID、ボット アプリケーション パスワード、Moodle シークレットなど) を含むフォームをチーム 設定 ページ **に入力** します。 Azure の情報は、[セットアップ] **ページに表示** されます)。 
> * フォームが完成した後、チェック ボックスをオンにして、利用規約に同意します。
> * [購入] **ボタンを選択** します。 すべての Azure リソースが無料層に展開されます。

リソースが Azure への展開を完了したら、メッセージング エンドポイントを使用してMicrosoft 365 Moodle プラグインを構成する必要があります。 Azure でボットからエンドポイントを取得する必要があります。

**メッセージング エンドポイントMicrosoft 365 Moodle プラグインを構成する**  
1. [Azure portal](https://portal.azure.com) にサインインします。

1. 左側のウィンドウで、[リソース グループ **] を** 選択し、ボットの展開中に使用または作成したリソース グループを選択します。

1. グループ内 **のリソースの一** 覧から WebApp Bot リソースを選択します。

1. [概要 **] セクションからメッセージング** エンドポイント **をコピー** します。

1. Moodle で、使用している **Moodle プラグイン設定**[チーム] ページMicrosoft 365開きます。

1. [ボット **エンドポイント] フィールド** に、コピーした URL を貼り付け、単語メッセージを *webhook に変更します*。  URL は次のように表示されます。 `https://botname.azurewebsites.net/api/webhook`

1. [変更 **の保存] を選択します**。

1. 変更を保存した後、[**チーム**] タブ設定戻り、[マニフェスト ファイルのダウンロード] ボタンを選択し、さらに使用するためにアプリ マニフェスト パッケージをコンピューターに保存します。

## <a name="4-deploy-your-microsoft-teams-app"></a>4. アプリをMicrosoft Teamsする

ボットが Azure に展開され、Moodle サーバーと話をするように構成された後、アプリを展開するMicrosoft Teamsがあります。 これを行うには、前の手順の [ムードル プラグイン チーム] ページからダウンロードMicrosoft 365アプリ マニフェスト 設定読み込む必要があります。

アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。 これを行うには、「テナントの準備」の[「Teams」の手順Microsoft 365従](../concepts/build-and-test/prepare-your-o365-tenant.md)います。 次の手順を実行して、アプリを展開できます。 

**アプリを展開するには**

1. [ファイル **Microsoft Teams] を開きます**。 

1. ナビゲーション バー **の** 左下の領域にある [アプリ] アイコンを選択します。

1. オプションの **アップロードからカスタム アプリ** リンクを選択します。

   > [!NOTE]
   > グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。それ以外の場合は、メンバーであるチームのアプリのみを読み込む必要があります。

4. 以前に `manifest.zip` ダウンロードしたパッケージを選択し、[保存] を **選択します**。 アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle のプラグイン構成ページの [チーム 設定] タブからダウンロードできます。

アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。 これを行うには、チャネルに移動し、 **プラス記号** (➕) を選択し、一覧からアプリを選択します。 プロンプトに従って、チャネルへの Moodle コース タブの追加を完了します。

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. [自動作成] ウィンドウで [Moodle] タブをMicrosoft Teams

[Moodle] タブは、Microsoft Teamsで手動で作成しますが、チームがコース同期から作成されると、自動的に作成できます。 これを行うには、Moodle でアップロードされたアプリの ID をMicrosoft Teamsする必要があります。

1. Microsoft Teams を開きます。

1. ナビゲーション バーの左下の領域から [アプリ] アイコンを選択します。

1. アップロードした **Moodle アプリを見つけて➡** オプション アイコン **を** 選択し➡コピー リンクを **選択します**。

1. テキスト エディターで、コピーしたコンテンツを貼り付けます。 これは、ht ファイルなどの URL を含&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。 URL の最後の部分 (アプリの ID など) `00112233-4455-6677-8899-aabbccddeeff` をMicrosoft Teamsします。

1. Moodle で、[Moodle プラグインの構成 **] Teams** ページから [ムードル アプリMicrosoft 365] タブを開きます。

1. アプリの ID を [Moodle Microsoft Teams ID] フィールドに貼り付け、変更を保存します。

Moodle コースが同期されている場合、Microsoft Teams は自動的にチームに Moodle アプリをインストールし、Teams の [全般] チャネルに [Moodle] タブを作成し、同期する Moodle コースのコース ページを含む構成を行います。 これで、お客様の Moodle コースの操作を、お客様のアカウントから直接Microsoft Teams。

機能の要求やフィードバックを共有するには、User Voice [ページをご覧ください](https://microsoftteams.uservoice.com/forums/916759-moodle)。

## <a name="see-also"></a>関連項目

- [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)

- [Moodle](https://moodle.org/)

- [Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins).
