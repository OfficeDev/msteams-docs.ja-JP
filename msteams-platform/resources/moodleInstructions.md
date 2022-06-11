---
title: Moodle LMS のインストール
description: Microsoft Teams用の Moodle 統合アプリをインストールして構成する方法
keywords: Teams Moodle アプリ統合プラグイン
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: b5e023041ad732c7580b8b01cd62bc7159a52887
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2022
ms.locfileid: "66033058"
---
# <a name="install-moodle-lms"></a>Moodle LMS のインストール

この記事では、Moodle LMS をインストールする方法について説明します。

> [!NOTE]
> IT 管理者が Moodle とTeamsの統合を簡単にセットアップできるように、オープンソースの Microsoft 365 Moodle プラグインは次のように更新されます。
>
> * [Microsoft Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) を使用した Moodle サーバーの自動登録。
>
> * Moodle Assistant ボットを Azure にワンクリックでデプロイします。
>
> * チームの自動プロビジョニングと、すべてまたは選択した Moodle コースのチーム登録の自動同期。
>
> * [Moodle] タブと Moodle アシスタント ボットを同期された各チームに自動インストールします。
>
> この統合によって提供される機能の詳細については、[Microsoft Teamsと Moodle](https://education.microsoft.com/resource/3dffb3a8) に関するページを参照してください。

## <a name="prerequisites"></a>前提条件

Moodle をインストールするための前提条件を次に示します。

* Moodle 管理者の資格情報。

* Azure AD 管理者の資格情報。

* 新しいリソースを作成できる Azure サブスクリプション。

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Microsoft 365 Moodle プラグインをインストールする

Microsoft Teamsでの Moodle の統合は、[オープンソース Microsoft 365 Moodle プラグインセット](https://github.com/Microsoft/o365-moodle)によって強化されます。

### <a name="requisite-applications-and-plugins"></a>必要なアプリケーションとプラグイン

Microsoft 365 Moodle プラグインのインストールに進む前に、必ず以下をインストールしてダウンロードしてください。

1. [現在の安定したバージョンの Moodle](https://download.moodle.org/releases/latest/) をインストールしてください。

1. Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc)と [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) プラグインをダウンロードしてローカル コンピューターに保存します。

    > [!NOTE]
    > Teams統合には、OpenID ConnectプラグインとMicrosoft 365統合プラグインのインストールが必要です。
    >
    > さらに、[Microsoft 365 Teamsテーマ](https://moodle.org/plugins/theme_boost_o365teams) プラグインを強くお勧めします。

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365 Moodle プラグイン

1. 管理者として Moodle サーバーにサインインし、左側のナビゲーション パネルにある [設定 ブロック](https://docs.moodle.org/22/en/Settings_block)から **[サイト管理**] を選択します。

1. [プラグイン] タブ **を** 選択し、[ **プラグインのインストール**] を選択します。

1. [ **ZIP ファイルからプラグインをインストールする** ] セクションで、[ **ファイルの選択**] を選択します。

1. 左側 **の** ナビゲーション パネルからファイル オプションアップロード選択し、ダウンロードしたファイルを参照して、**このファイルアップロード** 選択します。

1. 左側のナビゲーション パネルから [ **サイト管理** ] を選択して、管理者ダッシュボードに戻ります。 **ローカル プラグイン** まで下にスクロールし、**Microsoft 365統合** リンクを選択します。

    > [!IMPORTANT]
    >
    > * プロセス全体を通じてこのページのセットに戻る必要があるため、Microsoft 365 Moodle Plugins 構成ページを別のブラウザー タブで開いたままにします。  
    >
    > * 既存の Moodle サイトがない場合は、Azure リポジトリの [Moodle に](https://github.com/azure/moodle) 移動し、Moodle インスタンスをすばやくデプロイしてニーズに合わせてカスタマイズします。

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-ad"></a>2. Microsoft 365 プラグインと Azure AD 間の接続を構成する

Microsoft 365 プラグインと Azure AD 間の接続を構成する必要があります。

### <a name="requisites"></a>前提 条件

PowerShell スクリプトを使用して、Azure AD で Moodle をアプリケーションとして登録します。 スクリプトでは、次のものがプロビジョニングされます。

* Microsoft 365 Moodle プラグインによって使用される、Microsoft 365 テナント用の新しい Azure AD アプリケーション。
* Microsoft 365 テナントのアプリで、プロビジョニングされたアプリに必要な応答 URL とアクセス許可を設定し、次の値を`AppID``Key`返します。

生成された `AppID` `Key` [Microsoft 365 Moodle Plugins] セットアップ ページを使用して、Azure AD を使用して Moodle サーバー サイトを構成します。

> [!IMPORTANT]
>
> * PowerShell スクリプトは最新の構成項目では更新されないため、Moodle [3.8.0.4 および 3.9.1 および 3.8.0.5](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) [および 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って手動で構成を完了する必要があります。
>
> * Moodle インスタンスを手動で登録する方法の詳細については、「 [Moodle インスタンスをアプリケーションとして登録する」を参照してください](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Microsoft Teams情報フローの [Moodle] タブ

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. Microsoft 365統合プラグイン ページで、[**セットアップ]** タブを選択します。

1. **[PowerShell スクリプトのダウンロード**] ボタンを選択し、ZIP フォルダーとしてローカル コンピューターに保存します。

1. ZIP ファイルから PowerShell スクリプトを次のように準備します。

    1. ファイルをダウンロードして展開します `Moodle-AzureAD-Powershell.zip` 。
    1. 抽出されたフォルダーを開きます。
    1. ファイルを `Moodle-AzureAD-Script.ps1` 右クリックし、[ **プロパティ**] を選択します。
    1. プロパティ ウィンドウの [**全般**] タブで、ウィンドウの`Unblock`下部にある **[セキュリティ**] 属性の横にあるチェック ボックスをオンにします。
    1. **[OK]** を選択します。
    1. 抽出されたフォルダーにディレクトリ パスをコピーします。

1. PowerShell を管理者として実行します。

    1. [開始] を選択します。
    1. PowerShell と入力します。
    1. **Windows PowerShell** を右クリックします。
    1. [ **管理者として実行]** を選択します。

1. ディレクトリへのパスを入力`cd .../.../Moodle-AzureAD-Powershell``.../...`して、解凍されたディレクトリに移動します。

1. PowerShell スクリプトを実行します。

    1. `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` を入力します。
    1. `./Moodle-AzureAD-Script.ps1` を入力します。
    1. ポップアップ ウィンドウでMicrosoft 365管理者アカウントにサインインします。
    1. Azure AD アプリケーションの名前 (Moodle プラグインや Moodle プラグインなど) を入力します。
    1. Moodle サーバーの URL を入力します。
    1. スクリプトによって生成された **アプリケーション ID (`AppID`)** と **Application Key(`Key`)** をコピーして保存します。

1. 次に、Microsoft 365 Moodle プラグインに`Key`追加`AppID`する必要があります。 プラグイン管理ページに戻り、サイト管理>プラグイン> Microsoft 365統合します。

1. [**セットアップ**] タブで、前にコピーした内容を`AppID``Key`追加し、[**変更の保存]** を選択します。 ページが更新されると、新しいセクション **[接続方法の選択]** が表示されます。

1. **[接続の選択] メソッド** で、[**既定**] というラベルの付いたチェック ボックスをオンにし、もう一度 [**変更の保存]** を選択します。

1. ページが更新されると、別の新しいセクション **管理者の同意&追加情報** が表示されます。
    1. [**管理者の同意の提供**] リンクを選択し、Microsoft 365グローバル管理者の資格情報を入力し、[**同意]** を選択してアクセス許可を付与します。
    1. **Azure AD テナント** フィールドの横にある [**検出**] ボタンを選択します。
    1. **OneDrive for Business URL** の横にある [**検出**] ボタンを選択します。
    1. フィールドが設定されたら、もう一度 [ **変更の保存]** ボタンを選択します。

1. [ **更新]** ボタンを選択してインストールを確認し、[ **変更の保存]** を選択します。

1. Moodle サーバーと Azure AD の間でユーザーを同期します。 次の手順をお試しください。

    > [!NOTE]
    > 環境に応じて、この段階でさまざまなオプションを選択できます。

1. Moodle サーバーと Azure AD の間でユーザーを同期します。 環境に応じて、この段階でさまざまなオプションを選択できます。 次の手順をお試しください。
    1. **[同期設定] タブ** に切り替えます。

    1. [ **ユーザーと Azure AD の同期** ] セクションで、環境に適用するチェック ボックスをオンにします。 次を選択する必要があります。  

        ✔ Azure AD でユーザーのアカウントを Moodle に作成します。

        ✔ Azure AD のユーザーに対して、Moodle のすべてのアカウントを更新します。

    1. [ **ユーザー作成の制限** ] セクションでは、Moodle に同期される Azure AD ユーザーを制限するフィルターを設定できます。
    1. **[ユーザー フィールド マッピング]** セクションでは、Azure AD を Moodle ユーザー プロファイル フィールド マッピングにカスタマイズできます。
    1. **[Teams同期**] セクションで、既存の Moodle コースの一部または全部のチームなどのグループを自動的に作成するように選択できます。

13. [cron](https://docs.moodle.org/310/en/Cron) ジョブを検証し、最初の実行に対して手動で実行するには、[**Azure AD でユーザーを同期** する] セクションの **[スケジュールされたタスク管理] ページ** のリンクを選択します。 [ **スケジュールされたタスク]** ページに移動します。

    1. 下にスクロールし、 **Azure AD ジョブでユーザーを同期** し、[ **今すぐ実行**] を選択します。
    1. 既存のコースに基づいてグループを作成することを選択した場合は、**Microsoft 365ジョブでユーザー グループの作成を** 実行することもできます。

    > [!NOTE]
    >
    > Moodle [Cron](https://docs.moodle.org/310/en/Cron) は、タスク スケジュールに従って実行されます。 既定のスケジュールは 1 日に 1 回です。 ただし、すべての同期を維持するには、cron をより頻繁に実行する必要があります。

1. [プラグイン管理] ページに戻り、[**サイト管理] > [プラグイン> Microsoft 365統合] に** 戻り、**Teams 設定** ページを選択します。

1. **Teams 設定** ページで、Teams アプリ統合を有効にするために必要な設定を構成します。

    1. **OpenID Connect** を有効にするには、[**認証の管理**] リンクを選択し、使用できない場合は **OpenId Connect** 行の目のアイコンを選択します。
    1. フレームの埋め込みを有効にするには、[ **HTTP セキュリティ** ] リンクを選択し、[ **フレームの埋め込みを許可** する] の横にあるチェック ボックスをオンにします。
    1. Moodle API 機能を有効にする Web サービスを有効にするには、[ **高度な機能** ] リンクを選択し、[ **Web サービスを有効にする** ] の横にあるチェック ボックスがオンになっていることを確認します。
    1. Microsoft 365の外部サービスを有効にするには、[**外部サービス**] リンクを選択し、次の操作を行います。  

        ✔ **[Moodle Microsoft 365 Webservices**] 行で **[編集] を** 選択します。

        ✔ [**有効]** の横にあるチェック ボックスをオンにし、[**変更の保存]** を選択します。

    1. 認証されたユーザーのアクセス許可を編集して、Web サービス トークンを作成できるようにします。

        ✔ [ **編集ロール認証されたユーザー** ] リンクを選択します。

        ✔ 下にスクロールし、[ **Web サービス トークンの作成** ] 機能を見つけて、[ **許可** ] チェック ボックスをオンにします。

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Moodle Assistant Bot を Azure にデプロイする

Microsoft Teams用の無料の Moodle アシスタント ボットは、教師と学生が Moodle のコース、課題、成績、その他の情報に関する質問に答えるのに役立ちます。 ボットは、Teams内の学生と教師に Moodle 通知も送信します。 ボットは Microsoft によって管理されているオープンソース プロジェクトであり、[GitHub](https://github.com/microsoft/Moodle-Teams-Bot)で利用できます。

> [!NOTE]
>
> * Azure サブスクリプションにリソースをデプロイします。 すべてのリソースは **、Free** レベルを使用して構成されました。 ボットの使用状況によっては、これらのリソースのスケーリングが必要になる場合があります。
>
> * ボットなしで [Moodle] タブを使用するには、4 に進 [びます](#4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>Moodle ボット情報フロー

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

ボットをインストールするには、 [それを Microsoft Identity Platform](https://identity.microsoft.com/Landing) に登録する必要があります。 これにより、ボットは Microsoft エンドポイントに対して認証できます。

ボットを登録するには:

1. プラグイン管理ページに移動し、 **プラグイン** を選択します。 **[Microsoft 365統合**] で、[**Teams 設定**] タブを選択します。

1. **Microsoft アプリケーション登録ポータル** のリンクを選択し、Microsoft ID でサインインします。

1. MoodleBot などのアプリの名前を入力し、[ **作成** ] ボタンを選択します。

1. **アプリケーション ID を** コピーし、**チーム 設定** ページの **ボット アプリケーション ID** フィールドに貼り付けます。

1. [ **新しいパスワードの生成** ] ボタンを選択します。 生成されたパスワードをコピーし、**チーム 設定** ページの **[Bot Application Password**] フィールドに貼り付けます。

1. フォームの下部までスクロールし、[変更の **保存]** を選択します。

アプリケーション ID とパスワードを生成した後、ボットを Azure にデプロイします。

> [!div class="checklist"]
>
> * [**Azure へのデプロイ]** を選択し、必要な情報 (ボット アプリケーション ID、ボット アプリケーション パスワード、**Teams 設定** ページの Moodle シークレットなど) をフォームに入力します。 Azure の情報は **、[セットアップ]** ページにあります。
> * フォームに入力したら、チェック ボックスをオンにして使用条件に同意します。
> * [ **購入**] を選択します。 すべての Azure リソースは、Free レベルにデプロイされます。

リソースの Azure へのデプロイが完了したら、メッセージング エンドポイントを使用して Microsoft 365 Moodle プラグインを構成する必要があります。 Azure のボットからエンドポイントを取得する必要があります。

1. [Microsoft Azure ポータル](https://portal.azure.com)にサインインします。

1. 左側のウィンドウで、[ **リソース グループ** ] を選択し、ボットのデプロイ中に使用または作成したリソース グループを選択します。

1. グループ内のリソースの一覧から **WebApp Bot** リソースを選択します。

1. **[概要**] セクションから **メッセージング エンドポイント** をコピーします。

1. Moodle で、Microsoft 365 Moodle プラグインの **[チーム** 設定] ページを開きます。

1. **[ボット エンドポイント]** フィールドに、コピーした URL を貼り付け、*単語メッセージ* を *webhook* に変更します。 URL は次のように表示する必要があります。 `https://botname.azurewebsites.net/api/webhook`

1. [**変更を保存**] を選択します。

1. 変更を保存した後、[**チーム 設定**] タブに戻り、[**マニフェスト ファイルのダウンロード**] ボタンを選択し、アプリ マニフェスト パッケージをコンピューターに保存してさらに使用します。

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Microsoft Teams アプリをデプロイする

ボットを Azure にデプロイし、Moodle サーバーと通信するように構成したら、Microsoft Teams アプリをデプロイする必要があります。 これを行うには、前の手順で Microsoft 365 Moodle Plugins Team 設定 ページからダウンロードしたアプリ マニフェスト ファイルを読み込む必要があります。

アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。 詳細については、「[Microsoft 365 テナントを準備する](../concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。

アプリをデプロイするには:

1. **Microsoft Teams** を開きます。

1. ナビゲーション バーの左下領域にある **[アプリ** ] アイコンを選択します。

1. オプションの一覧から **カスタム アプリ** のリンクアップロードを選択します。

   > [!NOTE]
   > グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。それ以外の場合は、メンバーであるチームのアプリのみを読み込むことができます。

4. 以前にダウンロードした `manifest.zip` パッケージを選択し、[ **保存]** を選択します。 アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle のプラグイン構成ページの [**チーム 設定**] タブからダウンロードできます。

アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。 これを行うには、チャネルに移動し、 **プラス** 記号 (➕) を選択し、一覧からアプリを選択します。 メッセージに従って、チャネルへの Moodle コース タブの追加を完了します。

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Microsoft Teamsで Moodle タブの自動作成を許可する

Moodle タブはMicrosoft Teamsで手動で作成されますが、コース同期からチームを作成するときに自動的に作成することができます。 これを行うには、Moodle でアップロードされたMicrosoft Teams アプリの ID を構成する必要があります。

Moodle タブの自動作成を許可するには:

1. Microsoft Teams を開きます。

1. ナビゲーション バーの左下領域から [アプリ] アイコンを選択します。

1. アップロードされた **Moodle アプリ** を探> **オプション** アイコンを選択> **コピー リンク** を選択します。

1. テキスト エディターで、コピーしたコンテンツを貼り付けます。 次のような `https://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff`URL が含まれている必要があります。 URL の最後の部分 (Microsoft Teams アプリの ID など`00112233-4455-6677-8899-aabbccddeeff`) をコピーします。

1. Moodle で、**Microsoft 365 Moodle** プラグインの構成ページから [Teams Moodle アプリ] タブを開きます。

1. Microsoft Teams アプリの ID を [Moodle アプリ ID] フィールドに貼り付け、変更を保存します。

Moodle コースが同期されると、Microsoft Teamsチームに Moodle アプリが自動的にインストールされ、Teamsの [全般] チャネルに [Moodle] タブが作成され、同期元の Moodle コースのコース ページが含まれるようになります。 これで、Microsoft Teamsから直接 Moodle コースの操作を開始できます。

> [!NOTE]
> 機能の要求やフィードバックを Microsoft と共有するには、 [ユーザー音声ページ](https://microsoftteams.uservoice.com/forums/916759-moodle)を参照してください。

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [Moodle](https://moodle.org/)
* [Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins)。
