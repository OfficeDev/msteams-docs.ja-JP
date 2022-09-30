---
title: Moodle LMS のインストール
description: この記事では、Microsoft Teams 用の Moodle 統合アプリをインストールして構成する方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: c2276c720ca4d7014b3317365411a9c3d7fe6a73
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243179"
---
# <a name="install-moodle-lms"></a>Moodle LMS のインストール

この記事では、Moodle LMS をインストールする方法について説明します。

> [!NOTE]
> IT 管理者が Moodle と Teams の統合を簡単にセットアップできるように、オープンソースの Microsoft 365 Moodle プラグインは次のように更新されます。
>
> * [Microsoft Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) を使用した Moodle サーバーの自動登録。
>
> * Moodle Assistant ボットを Azure にワンクリックでデプロイします。
>
> * チームの自動プロビジョニングと、すべてまたは選択した Moodle コースのチーム登録の自動同期。
>
> * [Moodle] タブと Moodle アシスタント ボットを同期された各チームに自動インストールします。
>
> この統合によって提供される機能の詳細については、 [Microsoft Teams と Moodle](https://education.microsoft.com/resource/3dffb3a8) に関するページを参照してください。

## <a name="prerequisites"></a>前提条件

Moodle をインストールするための前提条件を次に示します。

* Moodle 管理者の資格情報。

* Azure AD 管理者の資格情報。

* 新しいリソースを作成できる Azure サブスクリプション。

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Microsoft 365 Moodle プラグインをインストールする

Microsoft Teams での Moodle の統合は、[Microsoft 365 Moodle プラグイン セット](https://moodle.org/plugins/browse.php?list=set&id=72)オープンソースによって強化されています。

### <a name="requisite-applications-and-plugins"></a>必要なアプリケーションとプラグイン

Microsoft 365 Moodle プラグインのインストールに進む前に、次をインストールしてダウンロードしてください。

1. [現在の安定したバージョンの Moodle](https://download.moodle.org/releases/latest/) をインストールしてください。

1. Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) と [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) プラグインをダウンロードしてローカル コンピューターに保存します。

    > [!NOTE]
    > Teams の統合には、OpenID Connect プラグインと Microsoft 365 統合プラグインのインストールが必要です。
    >
    > さらに、 [Microsoft 365 Teams テーマ](https://moodle.org/plugins/theme_boost_o365teams) プラグインを強くお勧めします。

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365 Moodle プラグイン

1. プラグインをダウンロードして抽出し、対応するフォルダーにアップロードします。 たとえば、OpenID Connect プラグイン (auth_oidc) を **oidc** という名前のフォルダーに抽出し、Moodle ドキュメント ルートの **認証** フォルダーにアップロードします。 

1. 管理者として Moodle サーバーにサインインし、[ **サイト管理**] を選択します。

1. インストールする新しいプラグインが検出されたら、Moodle は新しいプラグインのインストール ページにリダイレクトする必要があります。 これが発生しない場合は、[**サイト管理**] ページの [**全般**] タブで **[通知**] を選択すると、プラグインのインストールがトリガーされます。

1. プラグインがインストールされたら、**サイト管理者** ページの [**プラグイン**] タブに移動し、[**認証**] セクションリンクを選択して **OpenID Connect** を有効にします。 プラグイン構成を空白のままにしてもかまいません。後で入力します。

1. **サイト管理者** ページで、[**ローカル プラグイン**] セクションまで下にスクロールし、**Microsoft 365 統合** リンクを選択します。

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
* Microsoft 365 テナントのアプリで、プロビジョニングされたアプリに必要な応答 URL とアクセス許可を設定し、次の値を`Key`返`AppID`します。

生成された `AppID` `Key` Microsoft 365 Moodle Plugins セットアップ ページを使用して、Azure AD を使用して Moodle サーバー サイトを構成します。

> [!IMPORTANT]
>
> * Moodle インスタンスを手動で登録する方法の詳細については、「 [Moodle インスタンスをアプリケーションとして登録する」を参照してください](https://docs.moodle.org/400/en/Microsoft_365#Azure_App_Creation_and_Configuration)。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Microsoft Teams 情報フローの [Moodle] タブ

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. Microsoft 365 統合プラグイン ページで、[ **セットアップ]** タブを選択します。

1. **[PowerShell スクリプトのダウンロード**] ボタンを選択し、ZIP フォルダーとしてローカル コンピューターに保存します。

1. ZIP ファイルから PowerShell スクリプトを次のように準備します。

    1. ファイルをダウンロードして展開します `Moodle-AzureAD-Powershell.zip` 。
    1. 抽出されたフォルダーを開きます。
    1. ファイルを `Moodle-AzureAD-Script.ps1` 右クリックし、[ **プロパティ**] を選択します。
    1. プロパティ ウィンドウの [**全般**] タブで、ウィンドウの`Unblock`下部にある **[セキュリティ**] 属性の横にあるチェック ボックスをオンにします。
    1. **[OK]** をクリックします。
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
    1. ポップアップ ウィンドウで Microsoft 365 管理者アカウントにサインインします。
    1. Azure AD アプリケーションの名前 (Moodle プラグインや Moodle プラグインなど) を入力します。
    1. Moodle サーバーの URL を入力します。
    1. スクリプトによって生成された **アプリケーション ID (`AppID`)** と **Application Key(`Key`)** をコピーして保存します。

1. 次に、Microsoft 365 Moodle プラグインと `Key` Microsoft 365 Moodle プラグインを追加`AppID`する必要があります。 プラグイン管理ページに戻り、サイト管理>プラグイン> Microsoft 365 Integration です。

1. [ **セットアップ** ] タブで、前に `AppID` コピーした内容を `Key` 追加し、[ **変更の保存]** を選択します。 ページが更新されると、新しいセクション **[接続方法の選択]** が表示されます。

1. **[接続の選択] メソッド** で、[**既定**] というラベルの付いたチェック ボックスをオンにし、もう一度 [**変更の保存]** を選択します。

1. ページが更新されると、別の新しいセクション **管理同意&追加情報** が表示されます。
    1. [**同意の提供] リンク管理** 選択し、Microsoft 365 グローバル管理者の資格情報を入力し、[**同意]** を選択してアクセス許可を付与します。
    1. **Azure AD テナント** フィールドの横にある [**検出**] ボタンを選択します。
    1. **OneDrive for Business URL** の横にある [**検出**] ボタンを選択します。
    1. フィールドが設定されたら、もう一度 [ **変更の保存]** ボタンを選択します。

1. [ **更新]** ボタンを選択してインストールを確認し、[ **変更の保存]** を選択します。

1. Moodle サーバーと Azure AD の間でユーザーを同期します。 次の手順をお試しください。

    > [!NOTE]
    > 環境に応じて、この段階でさまざまなオプションを選択できます。

    1. **[同期設定] タブ** に切り替えます。

    1. [ **ユーザーと Azure AD の同期** ] セクションで、環境に適用するチェック ボックスをオンにします。 次を選択する必要があります。  

        ✔ Azure AD でユーザーのアカウントを Moodle に作成します。

        ✔ Azure AD のユーザーに対して、Moodle のすべてのアカウントを更新します。

    1. [ **ユーザー作成の制限** ] セクションで、Moodle に同期される Azure AD ユーザーを制限するフィルターを設定できます。

1. [cron](https://docs.moodle.org/400/en/Cron) ジョブを検証し、最初の実行に対して手動で実行するには、[**Azure AD でユーザーを同期** する] セクションの **[スケジュールされたタスク管理] ページ** のリンクを選択します。 [ **スケジュールされたタスク]** ページに移動します。

    1. 下にスクロールし、 **Azure AD ジョブでユーザーを同期** し、[ **今すぐ実行**] を選択します。
    1. 既存のコースに基づいてグループを作成することを選択した場合は、 **Microsoft 365 でユーザー グループの作成** ジョブを実行することもできます。

    > [!NOTE]
    >
    > Moodle [Cron](https://docs.moodle.org/310/en/Cron) は、タスク スケジュールに従って実行されます。 既定のスケジュールは 1 日に 1 回です。 ただし、すべての同期を維持するには、cron をより頻繁に実行する必要があります。

1. プラグイン管理ページに戻り、 **サイト管理>プラグイン> Microsoft 365 Integration** に戻り、 **Teams の設定** ページを選択します。

1. **[Teams の設定]** ページで、[**Check Moodle** settings] リンクをクリックして Teams アプリの統合を有効にするために必要な設定を構成すると、Teams 統合が機能するために必要なすべての構成が更新されます。 

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Moodle Assistant Bot を Azure にデプロイする

Microsoft Teams 用の無料の Moodle アシスタント ボットは、教師と学生が Moodle のコース、課題、成績、およびその他の情報に関する質問に答えるのに役立ちます。 ボットは、Teams 内の学生と教師に Moodle 通知も送信します。 このボットは、Microsoft によって管理されているオープンソース プロジェクトであり、 [GitHub](https://github.com/microsoft/Moodle-Teams-Bot) で入手できます。

> [!NOTE]
>
> * Azure サブスクリプションにリソースをデプロイします。 すべてのリソースは **、Free** レベルを使用して構成されました。 ボットの使用状況によっては、これらのリソースのスケーリングが必要になる場合があります。
>
> * ボットなしで [Moodle] タブを使用するには、4 に進 [びます](#4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>Moodle ボット情報フロー

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

ボットをインストールするには、 [それを Microsoft Identity Platform](https://identity.microsoft.com/Landing) に登録する必要があります。 これにより、ボットは Microsoft エンドポイントに対して認証できます。

ボットを登録するには:

1. プラグイン管理ページに移動し、 **プラグイン** を選択します。 **[Microsoft 365 統合**] で、[**Teams の設定]** タブを選択します。

1. **Microsoft アプリケーション登録ポータル** のリンクを選択し、Microsoft ID でサインインします。

1. MoodleBot などのアプリの名前を入力し、[ **作成** ] ボタンを選択します。

1. **アプリケーション ID を** コピーし、[**チームの設定]** ページの **[Bot Application ID**] フィールドに貼り付けます。

1. [ **新しいパスワードの生成** ] ボタンを選択します。 生成されたパスワードをコピーし、[**チームの設定]** ページの **[Bot Application Password**] フィールドに貼り付けます。

1. フォームの下部までスクロールし、[変更の **保存]** を選択します。

アプリケーション ID とパスワードを生成した後、ボットを Azure にデプロイします。

> [!div class="checklist"]
>
> * [ **Azure へのデプロイ]** を選択し、[ **Teams の設定]** ページで必要な情報 (ボット アプリケーション ID、ボット アプリケーション パスワード、Moodle Secret など) をフォームに入力します。 Azure の情報は **、[セットアップ]** ページにあります。
> * フォームに入力したら、チェック ボックスをオンにして使用条件に同意します。
> * [ **購入**] を選択します。 すべての Azure リソースは、Free レベルにデプロイされます。

リソースの Azure へのデプロイが完了したら、メッセージング エンドポイントを使用して Microsoft 365 Moodle プラグインを構成する必要があります。 Azure のボットからエンドポイントを取得する必要があります。

1. [Microsoft Azure ポータル](https://portal.azure.com)にサインインします。

1. 左側のウィンドウで、[ **リソース グループ** ] を選択し、ボットのデプロイ中に使用または作成したリソース グループを選択します。

1. グループ内のリソースの一覧から **WebApp Bot** リソースを選択します。

1. **[概要**] セクションから **メッセージング エンドポイント** をコピーします。

1. Moodle で、Microsoft 365 Moodle プラグインの **[チーム設定]** ページを開きます。

1. **[ボット エンドポイント]** フィールドに、コピーした URL を貼り付け、*単語メッセージ* を *webhook* に変更します。 URL は次のように表示する必要があります。 `https://botname.azurewebsites.net/api/webhook`

1. [**変更を保存**] を選択します。

1. 変更を保存したら、[ **チームの設定]** タブに戻り、[ **マニフェスト ファイルのダウンロード** ] ボタンを選択し、アプリ マニフェスト パッケージをコンピューターに保存して、さらに使用します。

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Microsoft Teams アプリを展開する

ボットが Azure にデプロイされ、Moodle サーバーと通信するように構成されたら、Microsoft Teams アプリをデプロイする必要があります。 これを行うには、前の手順で Microsoft 365 Moodle Plugins Team Settings ページからダウンロードしたアプリ マニフェスト ファイルを読み込む必要があります。

アプリをインストールする前に、外部アプリとアプリのアップロードを有効にする必要があります。 詳細については、「 [Microsoft 365 テナントの準備」を参照してください](../concepts/build-and-test/prepare-your-o365-tenant.md)。

アプリをデプロイするには:

1. **Microsoft Teams** を開きます。

1. ナビゲーション バーの左下領域にある **[アプリ** ] アイコンを選択します。

1. ナビゲーション メニューの [ **アプリの管理** ] リンクを選択します。

1. [ **アプリの発行]** をクリックし、 **組織のアプリ カタログにアプリをアップロードするを選択します**。

   > [!NOTE]
   > グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションが必要です。それ以外の場合は、メンバーであるチームのアプリのみを読み込むことができます。

4. 以前にダウンロードした `manifest.zip` パッケージを選択し、[ **保存]** を選択します。 アプリ マニフェスト パッケージをダウンロードしていない場合は、Moodle のプラグイン構成ページの **[チーム設定]** タブからダウンロードできます。

アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。 これを行うには、チャネルに移動し、 **プラス** 記号 (➕) を選択し、一覧からアプリを選択します。 メッセージに従って、チャネルへの Moodle コース タブの追加を完了します。

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Microsoft Teams で Moodle タブの自動作成を許可する

Moodle タブは Microsoft Teams で手動で作成されますが、コース同期からチームを作成するときに自動的に作成することができます。 これを行うには、Moodle でアップロードされた Microsoft Teams アプリの ID を構成する必要があります。

Moodle タブの自動作成を許可するには:

1. Moodle で、Microsoft 365 **Moodle** プラグインの構成ページから Teams Moodle アプリ タブを開きます。

1. Azure アプリに推奨されるアクセス許可がある場合は、 **Moodle アプリ ID** 設定に [ **自動検出] の値が表示され**、この値を設定にコピーします。

1. 自動的に検出された値が表示されない場合は、ページの指示に従って Moodle アプリ ID を見つけて、設定を入力します。

Moodle コースが同期されると、Teams はチームに Moodle アプリを自動的にインストールし、Teams の [全般] チャネルに [Moodle] タブを作成し、同期元の Moodle コースのコース ページを含む構成を行います。 これで、Teams から直接 Moodle コースの操作を開始できます。

> [!NOTE]
> 機能の要求やフィードバックを Microsoft と共有するには、 [ユーザー音声ページ](https://support.microsoft.com/en-us/office/uservoice-pages-430e1a78-e016-472a-a10f-dc2a3df3450a)を参照してください。

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [Moodle](https://moodle.org/)
* [Moodle のドキュメント](https://docs.moodle.org/400/en/Installing_plugins)
* [Moodle Docs の Microsoft 365 と Moodle 統合ページ](https://docs.moodle.org/400/en/Microsoft_365)
