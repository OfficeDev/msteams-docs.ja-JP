---
title: Moodle LMS のインストール
description: Microsoft Teamsの Moodle 統合アプリをインストールして構成する方法
keywords: TeamsMoodleアプリ統合プラグイン
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: d7fddad80ca08fd4ca8dee352cdcbc46e8e97dcd
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566720"
---
# <a name="install-moodle-lms"></a>Moodle LMS のインストール

この記事では、Moodle LMS のインストール方法について説明します。

> [!NOTE]
> IT 管理者が Moodle とTeams統合を簡単にセットアップできるように、オープンソースMicrosoft 365 Moodle プラグインは次の機能に更新されます。
>
> * moodle サーバーの自動登録を[Azure Active Directory (Azure AD) に](https://azure.microsoft.com/services/active-directory/)自動登録する 。
>
> * 1 回のクリックで、ムードル アシスタント ボットを Azure にデプロイします。
>
> * チームの自動プロビジョニングとチーム登録の自動同期をすべての人に対して行うか、Moodleコースを選択します。
>
> * 各同期チームに Moodle タブと Moodle アシスタントボットの自動インストール。
>
> この統合が提供する機能の詳細については、「 [Microsoft Teams と Moodle](https://education.microsoft.com/resource/3dffb3a8)」を参照してください。

## <a name="prerequisites"></a>前提条件

Moodle をインストールするための前提条件は次のとおりです。

* ムード管理者の資格情報。

* Azure AD 管理者の資格情報。

* 新しいリソースを作成できる Azure サブスクリプション。

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Microsoft 365のMoodleプラグインをインストールする

Microsoft TeamsのMoodle統合は[、MoodleプラグインセットMicrosoft 365](https://github.com/Microsoft/o365-moodle)オープンソースによって供給されます。

### <a name="requisite-applications-and-plugins"></a>必要なアプリケーションとプラグイン

Microsoft 365 Moodle プラグインのインストールを続行する前に、以下をインストールしてダウンロードしてください。

1. [Moodle の現在の安定版を](https://download.moodle.org/releases/latest/)インストールすることを確認します。

1. Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc)と[Microsoft 365統合](https://moodle.org/plugins/local_o365)プラグインをダウンロードしてローカルコンピュータに保存します。

    > [!NOTE]
    > Teams統合には、OpenID ConnectとMicrosoft 365統合プラグインのインストールが必要です。
    >
    > さらに[、Microsoft 365 Teamsテーマ](https://moodle.org/plugins/theme_boost_o365teams)プラグインを強くお勧めします。

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365ムードルプラグイン

1. 管理者として Moodle サーバーにサインインし、左側のナビゲーション パネルにある [設定 ブロック](https://docs.moodle.org/22/en/Settings_block)から [**サイト管理**] を選択します。

1. [プラグイン] タブ **を** 選択し、[ **プラグインのインストール**] を選択します。

1. [ZIP **ファイルからプラグインをインストール]** セクションで、[ **ファイルの選択**] を選択します。

1. 左側 **の** ナビゲーション パネルからファイル オプションアップロード選択し、ダウンロードしたファイルを参照して、[**このファイルアップロード]** を選択します。

1. 左側のナビゲーション パネルから [ **サイト管理]** を選択して、管理ダッシュボードに戻ります。 **ローカルプラグイン** までスクロールダウンし **、Microsoft 365統合** リンクを選択します。

    > [!IMPORTANT]
    >
    > * プロセス全体を通してこのページのセットに戻る必要がある場合は、Microsoft 365 Moodle Plugins 設定ページを別のブラウザタブで開いたままにします。  
    >
    > * 既存の Moodle サイトがない場合は、Azure レポ [の Moodle に](https://github.com/azure/moodle) 移動し、すぐに Moodle インスタンスをデプロイしてニーズに合わせてカスタマイズします。

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a>2. Microsoft 365 プラグインとAzure Active Directory間の接続を構成する (Azure AD)

Microsoft 365 プラグインと Azure AD 間の接続を構成する必要があります。

### <a name="requisites"></a>前提 条件

PowerShell スクリプトを使用して、アプリケーションとしてアプリケーションとして Moodle を登録します。 Powershell スクリプトは、次の項目をプロビジョニングします。

* Microsoft 365のテナント用の新しい Azure AD アプリケーションで、Microsoft 365 Moodle プラグインで使用されます。
* Microsoft 365テナント用のアプリは、プロビジョニングされたアプリに必要な応答 URL とアクセス許可を設定し、 `AppID` と を返します `Key` 。

生成された Microsoft 365 `AppID` `Key` Moodle プラグインのセットアップ ページで、Azure AD を使用して Moodle サーバー サイトを構成します。

> [!IMPORTANT]
>
> * PowerShell スクリプトは最新の構成項目で更新されないため、Moodle [3.8.0.4 および 3.9.1 および 3.8.0.5 および](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) [3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って、構成を手動で完了する必要があります。
>
> * Moodle インスタンスを手動で登録する方法の詳細については [、「Moodle インスタンスをアプリケーションとして登録する](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)」を参照してください。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>情報フローのMicrosoft Teamsの [Moodle] タブ

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. [Microsoft 365統合プラグイン] ページで、[**設定**] タブを選択します。

1. **[PowerShell スクリプトのダウンロード**] ボタンを選択し、ZIP フォルダーとしてローカル コンピューターに保存します。

1. 次のように ZIP ファイルから PowerShell スクリプトを準備します。 

    1. ファイルをダウンロードして解凍 `Moodle-AzureAD-Powershell.zip` します。
    1. 展開したフォルダを開きます。
    1. ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` **プロパティ ]** を選択します。
    1. [プロパティ] ウィンドウの [ **全般** ] タブで、 `Unblock` ウィンドウの下部にある **[セキュリティ** ] 属性の横にあるチェックボックスをオンにします。
    1. **[OK]** を選択します。
    1. 展開したフォルダにディレクトリ パスをコピーします。

1. 管理者として PowerShell を実行します。

    1. [開始] を選択します。
    1. 「パワーシェル」と入力します。
    1. **Windows PowerShell** を右クリックします。
    1. [ **管理者として実行**] を選択します。

1. 解凍したディレクトリに移動するには `cd .../.../Moodle-AzureAD-Powershell` `.../...` 、ディレクトリへのパスを入力します。

1. 次のコマンドを実行します。

    1. `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`を入力します。
    1. `./Moodle-AzureAD-Script.ps1`を入力します。
    1. ポップアップ ウィンドウでMicrosoft 365管理者アカウントにサインインします。
    1. Azure AD アプリケーションの名前を入力します(たとえば、Moodle プラグインや Moodle プラグインなど)。
    1. Moodle サーバーの URL を入力します。
    1. スクリプトによって生成された **アプリケーション ID ( `AppID` )** と **アプリケーション キー ( ) `Key` を** コピーして保存します。

1. 次に、 `AppID` `Key` ムードルプラグインを追加し、Microsoft 365に追加する必要があります。 プラグイン管理ページ、サイト管理>プラグイン> Microsoft 365統合に戻ります。

1. [ **セットアップ** ] タブで、 `AppID` を追加し `Key` 、以前にコピーした後、[ **変更の保存**] を選択します。 ページが更新されると、新しいセクションの **接続方法を選択** するを見ることができます。

1. [ **接続方法の選択**] で、[ **既定**] というラベルのチェック ボックスをオンにし、[ **変更を保存]** を再度選択します。

1. ページが更新されると、別の新しいセクション **[管理者の同意&追加情報** が表示されます。
    1. [**管理者同意の提供**] リンクを選択し、Microsoft 365のグローバル管理者資格情報を入力し、[**承諾]** をクリックしてアクセス許可を付与します。
    1. **[Azure AD テナント]** フィールドの横にある [**検出**] ボタンを選択します。
    1. **[OneDrive for Business URL]** の横にある [**検出**] ボタンを選択します。
    1. フィールドが入力されたら、[変更を **保存** ] ボタンをもう一度選択します。

1. [ **更新** ] ボタンを選択してインストールを確認し、[ **変更の保存**] を選択します。

1. Moodle サーバーと Azure AD の間でユーザーを同期します。 次の手順をお試しください。

    > [!NOTE]
    > 環境に応じて、このステージで異なるオプションを選択できます。

1. Moodle サーバーと Azure AD の間でユーザーを同期します。 環境に応じて、このステージで異なるオプションを選択できます。 次の手順をお試しください。
    1. [**同期設定] タブ** に切り替えます。

    1. [ **ユーザーと Azure AD の同期** ] セクションで、環境に適用するチェック ボックスをオンにします。 次の項目を選択する必要があります。  

        ✔ Azure AD のユーザーのムードルでアカウントを作成します。

        ✔ Azure AD のユーザーの Moodle のすべてのアカウントを更新します。

    1. [ **ユーザーの作成の制限]** セクションでは、Moodle に同期される Azure AD ユーザーを制限するフィルターを設定できます。
    1. **[ユーザー フィールド マッピング]** セクションでは、Azure AD から Moodle ユーザー プロファイル フィールド マッピングをカスタマイズできます。
    1. [Teams **同期**] セクションでは、既存の Moodle コースの一部または全部のチームなどのグループを自動的に作成することを選択できます。

13. [cron](https://docs.moodle.org/310/en/Cron)ジョブを検証し、最初の実行に対して手動で実行するには **、[Azure AD とユーザーを同期** する] セクションの **[スケジュールされたタスク管理] ページ** のリンクを選択します。 [ **スケジュールされたタスク** ] ページに移動します。

    1. 下にスクロールして **、[Azure AD とユーザーを同期** する] ジョブを見つけて、[ **今すぐ実行**] を選択します。
    1. 既存のコースに基づいてグループを作成する場合は、ジョブ **でユーザーグループを作成Microsoft 365実行** することもできます。

    > [!NOTE]
    >
    > Moodle [Cron](https://docs.moodle.org/310/en/Cron) はタスクスケジュールに従って実行されます。 デフォルトのスケジュールは 1 日 1 回です。 ただし、cron は、すべてを同期させるために、より頻繁に実行する必要があります。

1. プラグイン管理ページの **[サイト管理> プラグイン > Microsoft 365統合**] に戻り **、Teams 設定** ページを選択します。

1. Teams 設定ページ **で**、Teamsアプリ統合を有効にする必要な設定を構成します。

    1. **OpenID Connect** を有効にするには、[**認証の管理**] リンクを選択し、灰色表示の場合は **OpenId Connect** 行の目のアイコンを選択します。
    1. フレーム埋め込みを有効にするには **、[HTTP セキュリティ** ] リンクを選択し、[フレームの **埋め込みを許可** する] の横にあるチェックボックスをオンにします。
    1. Moodle API 機能を有効にする Web サービスを有効にするには、[ **高度な機能]** リンクを選択し **、[Web サービスを有効にする** ] の横にあるチェックボックスが選択されていることを確認します。
    1. Microsoft 365の外部サービスを有効にするには、[**外部サービス**] リンクを選択し、次の操作を行います。  

        ✔ **[ムードル Microsoft 365 Web サービス**] 行で **[編集**] を選択します。

        ✔ **[有効]** の横にあるチェックボックスをオンにし、[**変更の保存**] を選択します。

    1. 認証されたユーザー権限を編集して、Web サービストークンの作成を許可します。

        ✔ **編集ロール認証済みユーザーリンクを選択します** 。

        ✔ 下にスクロールして **[Web サービス トークンを作成する** ]機能を見つけ、[ **許可** ]チェックボックスを選択します。

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Azure にムードアシスタントボットをデプロイする

Microsoft Teams用の無料のMoodleアシスタントボットは、教師と学生がMoodleのコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。 ボットは、Teams内の学生や教師にMoodle通知を送信します。 ボットは Microsoft が管理するオープンソース プロジェクトであり[、GitHub](https://github.com/microsoft/Moodle-Teams-Bot)で入手できます。

> [!NOTE]
>
> * リソースを Azure サブスクリプションにデプロイします。 すべてのリソースは **、free** レベルを使用して構成されました。 ボットの使用状況によっては、これらのリソースをスケーリングする必要があります。
>
> * ボットを使用せずに Moodle タブを使用するには [、4](#4-deploy-your-microsoft-teams-app)に進んでください。

### <a name="moodle-bot-information-flow"></a>ムードボット情報フロー

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

ボットをインストールするには、Microsoft [ID プラットフォーム](https://identity.microsoft.com/Landing)に登録する必要があります。 これにより、ボットは Microsoft エンドポイントに対して認証を受けられます。 

**ボットを登録するには**

1. プラグイン管理ページに移動し、プラグイン **を** 選択します。 **[Microsoft 365統合**] で **、[Teams 設定]** タブを選択します。

1. **[Microsoft アプリケーション登録ポータル**] リンクを選択し、Microsoft ID でサインインします。

1. MoodleBot などのアプリの名前を入力し、[ **作成** ] ボタンを選択します。

1. アプリケーション **ID** をコピーし、[**チーム 設定]** ページの **[Bot アプリケーション ID]** フィールドに貼り付けます。

1. [ **新しいパスワードの生成]** ボタンを選択します。 生成されたパスワードをコピーし、[**チーム 設定]** ページの **[Bot アプリケーション パスワード]** フィールドに貼り付けます。

1. フォームの一番下までスクロールし、[ **変更を保存]** を選択します。

アプリケーション ID とパスワードを生成したら、次の手順でボットを Azure にデプロイします。

> [!div class="checklist"]
> * [Azure **にデプロイ]** を選択し **、Teams 設定** ページの Bot アプリケーション ID、ボット アプリケーション パスワード、Moodle シークレットなどの必要な情報をフォームに入力します。 Azure の情報は **[セットアップ** ] ページにあります。 
> * フォームに記入したら、チェックボックスを選択して利用規約に同意します。
> * [ **購入**] を選択します。 すべての Azure リソースは、無料のレベルにデプロイされます。

リソースが Azure へのデプロイを完了したら、メッセージング エンドポイントを使用して Microsoft 365 Moodle プラグインを構成する必要があります。 Azure のボットからエンドポイントを取得する必要があります。

1. [Azure portal](https://portal.azure.com) にサインインします。

1. 左側のウィンドウで [ **リソース グループ** ] を選択し、ボットのデプロイ中に使用または作成したリソース グループを選択します。

1. グループ内のリソースのリストから **WebApp Bot** リソースを選択します。

1. 「**概要**」セクションから **メッセージング・エンドポイント** をコピーします。

1. Moodleで、Microsoft 365のMoodleプラグインの **チーム設定** ページを開きます。

1. [ **ボット エンドポイント** ] フィールドに、コピーした URL を貼り付け *、メッセージという* 単語を *webhook* に変更します。 URL は次のように表示される必要があります。 `https://botname.azurewebsites.net/api/webhook`

1. [ **変更の保存 ] を** 選択します。

1. 変更を保存したら、[**チーム 設定]** タブに戻り、[**マニフェスト ファイルのダウンロード**] ボタンを選択して、アプリ マニフェスト パッケージをコンピューターに保存して、さらに使用します。

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Microsoft Teams アプリを展開する

ボットが Azure にデプロイされ、Moodle サーバーとの会話をするように構成された後、Microsoft Teamsアプリをデプロイする必要があります。 これを行うには、前の手順でMicrosoft 365 Moodle プラグイン チーム 設定 ページからダウンロードしたアプリ マニフェスト ファイルを読み込む必要があります。

アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。 詳細については、「 [Microsoft 365 テナントの準備](../concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。 

**アプリを展開するには** 

1. **Microsoft Teams** を開きます。 

1. ナビゲーションバーの左下の領域にある **アプリ** アイコンを選択します。

1. オプションの一覧から **、カスタム アプリのリンクをアップロード** を選択します。

   > [!NOTE]
   > グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。

4. `manifest.zip`以前にダウンロードしたパッケージを選択し、[**保存 ]** を選択します。 アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle のプラグイン構成ページの **[チーム 設定]** タブからダウンロードできます。

これでアプリがインストールされ、アクセスできる任意のチャネルにタブを追加できます。 これを行うには、チャンネルに移動し、 **プラス** 記号 (➕) を選択し、一覧からアプリを選択します。 プロンプトに従って、Moodleコースタブをチャンネルに追加します。

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Microsoft Teamsで Moodle タブの自動作成を許可する

Moodle タブはMicrosoft Teamsで手動で作成されますが、コースの同期からチームを作成するときに自動的に作成することもできます。 これを行うには、Moodle でアップロードされたMicrosoft Teamsアプリの ID を構成する必要があります。

**Moodleタブの自動作成を許可するには**

1. Microsoft Teams を開きます。

1. ナビゲーションバーの左下の領域から[アプリ]アイコンを選択します。

1. アップロードされた **Moodle アプリ** を探> **オプション** アイコンを選択 **>、コピー リンク** を選択します。

1. テキスト エディタで、コピーしたコンテンツを貼り付けます。 これは、ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff などの URL を含んでいる必要があります。 Microsoft Teams アプリの ID である など、URL `00112233-4455-6677-8899-aabbccddeeff` の最後の部分をコピーします。

1. Moodleで **、Microsoft 365 Moodleプラグイン設定ページからTeams Moodleアプリ** タブを開きます。

1. Microsoft Teamsアプリの ID を Moodle アプリ ID フィールドに貼り付け、変更を保存します。

Moodle コースが同期されると、チームに Moodle アプリが自動的にインストールMicrosoft Teams、Teamsの一般チャネルに Moodle タブが作成され、同期元の Moodle コースのコースページが含まれる構成が行われます。 Microsoft Teamsから直接Moodleコースで作業を開始できるようになりました。

> [!NOTE]
> 機能のリクエストやフィードバックを当社と共有するには、 [ユーザーの声ページ](https://microsoftteams.uservoice.com/forums/916759-moodle)にアクセスしてください。

## <a name="see-also"></a>関連項目

- [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
- [ムードル](https://moodle.org/)
- [Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins)。

