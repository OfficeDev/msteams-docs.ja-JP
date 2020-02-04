---
title: Microsoft Teams との Moodle の統合をインストールする
description: Microsoft Teams 用の Moodle 統合アプリをインストールして構成する方法
keywords: Teams Moodle app integration plugin
ms.date: 01/31/2019
ms.openlocfilehash: 012d6e9c979386e892b5a47b7655208eca95e11a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674595"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>Microsoft Teams との Moodle の統合をインストールする

> [!VIDEO https://www.youtube.com/embed/OHlPt22nKoE]

世界で最も人気の[ある、および](https://moodle.org/)オープンソースの学習管理システム (LMS) は、Microsoft Teams と統合されました。 この統合により、教育者や教師が Moodle のコースに関する質問を行ったり、成績や課題について質問したり、Teams 内で通知を更新したりすることができます。

IT 管理者がこの統合を簡単に設定できるようにするため、次の機能を使用して、オープンソースの Office 365 Moodle プラグインを更新しました。

* Azure AD での Moodle サーバーの自動登録。
* Moodle Assistant bot を Azure に1回クリックして展開します。
* すべてのまたは選択した Moodle のコースに対して、teams の自動プロビジョニングとチーム登録の自動同期を行います。
* 同期された各チームへの Moodle タブと Moodle アシスタントの自動インストール。 (近日中)
* ワンクリックで Moodle アプリをプライベート Teams アプリストアに発行します。 (近日中)

この統合によって提供される機能の詳細については、[ここ](https://education.microsoft.com/courses-and-resources/resources/microsoft-teams-moodle)を参照してください。

## <a name="prerequisites"></a>前提条件

このアプリケーションをインストールして構成するには、次のものが必要になります。

1. Moodle 管理者の資格情報
2. Azure AD 管理者の資格情報
3. Azure サブスクリプションでは、新しいリソースを作成できます。

## <a name="step-1-install-the-office-365-moodle-plugin"></a>手順 1: Office 365 Moodle プラグインをインストールする

> [!VIDEO https://www.youtube.com/embed/SETEC5nzMgk]

Microsoft Teams の Moodle の統合は、オープンソースの[Office 365 Moodle プラグインセット](https://github.com/Microsoft/o365-moodle)によって提供されています。 Moodle サーバーにプラグインをインストールするには、次のようにします。

1. 最初に、 [Office 365 プラグインセット](https://moodle.org/plugins/pluginversions.php?plugin=local_o365)をダウンロードして、ローカルコンピューターに保存します。 バージョン3.5 以降を使用する必要があります。
    * Local_o365 プラグインをインストールすると、 [auth_oidc](https://moodle.org/plugins/auth_oidc)と[boost_o365Teams](https://moodle.org/plugins/pluginversions.php?plugin=theme_boost_o365teams)プラグインもインストールされます。
1. Moodle サーバーに管理者としてログインし、左側のナビゲーションパネルから [**サイトの管理**] を選択します。
1. [**プラグイン**] タブを選択し、[**プラグインのインストール**] をクリックします。
1. [ **ZIP ファイルからプラグインをインストール**する] セクションで、[**ファイルの選択**] ボタンをクリックします。
1. 左側のナビゲーションから [**ファイルのアップロード**] オプションを選択し、上記の手順でダウンロードしたファイルを参照して、[**このファイルをアップロード**] をクリックします。
1. 左側のナビゲーションパネルからもう一度 [**サイトの管理**] オプションを選択して、管理者ダッシュボードに戻ります。 **ローカルプラグイン**までスクロールし、[ **Microsoft Office 365 統合**] リンクをクリックします。 この構成ページは、このプロセスの残りの部分で使用するのと同じように、別のブラウザーのタブで開いたままにしておきます。

Moodle プラグインをインストールする方法の詳細については、 [Moodle のドキュメント](https://docs.moodle.org/34/en/Installing_plugins)を参照してください。

**重要な注意事項:** このプロセス全体を通してこのページセットに戻るように、Office 365 Moodle Plugin 構成ページは別のブラウザータブで開いたままにしておきます。

*Moodle サイトを既に持っていない場合* Moodle インスタンスを Azure にすばやく展開して、ニーズに合わせてカスタマイズできる Azure[リポジトリ](https://github.com/azure/moodle)で Moodle を確認することをお勧めします。

## <a name="step-2-configure-the-connection-between-the-office-365-plugin-and-azure-active-directory"></a>手順 2: Office 365 プラグインと Azure Active Directory との間の接続を構成する

> [!VIDEO https://www.youtube.com/embed/FpGEezaJ3SA]

次に、Azure Active Directory のアプリケーションとして Moodle を登録する必要があります。 このプロセスを完了するために役立つ PowerShell スクリプトが提供されています。 PowerShell スクリプトは、office 365 Moodle プラグインによって使用される Office 365 テナント用に新しい Azure AD アプリケーションをプロビジョニングします。 このスクリプトは、O365 テナント用のアプリを準備し、プロビジョニングされたアプリに必要な応答 Url とアクセス許可をすべて設定し、AppID とキーを返します。 O365 Moodle Plugin セットアップページで生成された AppID とキーを使用して、Moodle サーバーを Azure AD で構成できます。 PowerShell スクリプトによって自動化される詳細な手動手順については、「[プラグインの](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)完全なドキュメント」を参照してください。

### <a name="moodle-tab-for-microsoft-teams-information-flow"></a>Microsoft Teams の情報フローの Moodle タブ

<img width="530px" src="~/assets/images/MoodleTabInformationFlow.png" title="Microsoft Teams の情報フローの Moodle タブ" />

1. [Microsoft Office 365 Integration plugin] ページで、[**セットアップ**] タブを選択します。
1. [ **PowerShell スクリプトをダウンロード**] ボタンをクリックして、ローカルコンピューターに保存します。
1. この ZIP ファイルから PowerShell スクリプトを準備する必要があります。 これを行うには、以下のようにします:
    * ファイルを`Moodle-AzureAD-Powershell.zip`ダウンロードして展開します。
    * 抽出したフォルダーを開きます。
    * `Moodle-AzureAD-Script.ps1`ファイルを右クリックし、[**プロパティ**] を選択します。
    * [プロパティ] ウィンドウの [**全般**] タブで、 `Unblock`下部にある [ **Security** ] 属性の横のチェックボックスをオンにします。
    * **[OK]** をクリックします。
    * 抽出したフォルダーのディレクトリパスをコピーします。
1. 次に、PowerShell を管理者として実行します。
    * [開始] をクリックします。
    * PowerShell と入力します。
    * [Windows PowerShell] を右クリックします。
    * [管理者として実行] をクリックします。
1. フォルダーへのパスを入力`cd ...\...\Moodle-AzureAD-Powershell` `...\...`して、解凍後のディレクトリに移動します。
1. 次の方法で PowerShell スクリプトを実行します。
    * Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`キーを押します。
    * Enter `.\Moodle-AzureAD-Script.ps1`キーを押します。
    * ポップアップウィンドウで、O365 管理者アカウントにログインします。
    * Azure AD アプリケーションの名前を入力します (例、 Moodle/Moodle プラグイン)。
    * Moodle サーバーの URL を入力します。
    * スクリプトによって生成された**アプリケーション ID**と**アプリケーションキー**をコピーして保存します。
1. 次に、Office 365 Moodle プラグインに Id とキーを追加する必要があります。 [プラグインの管理] ページ ([サイトの管理 > プラグイン > Microsoft Office 365 統合) に戻ります。
1. [**セットアップ**] タブで、先ほどコピーした**アプリケーション Id**と**アプリケーションキー**を追加し、[**変更の保存**] をクリックします。
1. ページが更新されると、 **[connection メソッドの選択**] という新しいセクションが表示されるようになります。 [**既定**] のチェックボックスをオンにし、[**変更の保存**] をもう一度クリックします。
1. ページが更新されると、[管理者の同意] という別の新しいセクションが**追加情報 &** 表示されます。
    * [**管理者の同意を提供**する] リンクをクリックして、Office3 365 のグローバル管理者の資格情報を入力し、**同意**してアクセス許可を付与します。
    * [ **AZURE AD テナント**] フィールドの横にある [**検出**] ボタンをクリックします。
    * [ **OneDrive For business の URL** ] の横にある [**検出**] ボタンをクリックします。
    * フィールドが読み込まれたら、[**変更の保存**] ボタンをもう一度クリックします。
1. [**更新**] ボタンをクリックしてインストールを確認し、**変更を保存**します。
1. 次に、Moodle サーバーと Azure Active Directory の間でユーザーを同期する必要があります。 ご使用の環境によっては、この段階でさまざまなオプションを選択できます。 ここで設定した構成は、各 Moodle cron 実行 (通常は1日に1回) によって実行され、すべてが同期状態に保たれることに注意してください。まず、次のようにします。
    * [同期の**設定] タブ**に切り替える
    * [ **AZURE AD とのユーザーの同期**] セクションで、環境に適用するチェックボックスをオンにします。 通常は、少なくとも次のものを選択します。
        * Azure AD のユーザー用に Moodle でアカウントを作成する
        * Azure AD のユーザー用に Moodle のすべてのアカウントを更新する
    * [**ユーザーの作成の制限**] セクションでは、Moodle に同期することによって Azure AD ユーザーを制限するためのフィルターを設定できます。
    * [**ユーザーフィールドマッピング**] セクションでは、Azure AD を Moodle のユーザープロファイルフィールドマッピングにカスタマイズできます。
    * [ **Teams Sync** ] セクションでは、既存の Moodle コースの一部または全部に対してグループ (Teams) を自動的に作成することを選択できます。
1. Cron ジョブを検証する (初回実行時に必要に応じて手動で実行する場合) には、[**ユーザーを AZURE AD と同期**する] セクションの [**タスク管理ページ**] リンクをクリックします。 これにより、[**タスクのスケジュール**] ページに移動します。
    * 下にスクロールして、[ **AZURE AD ジョブを使用**してユーザーを同期します] ジョブを見つけ、[**今すぐ実行**] をクリックします。
    * 既存のコースに基づいてグループを作成することを選択した場合は、 **Office 365 ジョブで [ユーザーグループの作成**] を実行することもできます。
1. [プラグインの管理] ページ ([サイトの管理 > プラグイン > Microsoft Office 365 統合]) に戻り、[ **Teams の設定**] ページを選択します。 Teams アプリの統合を有効にするには、いくつかのセキュリティ設定を構成する必要があります。
    * OpenID Connect を有効にするには、[**認証の管理**] リンクをクリックして、 **openid connect**行が淡色で設定されている場合は、[目] アイコンをクリックします。
    * 次に、フレームの埋め込みを有効にする必要があります。 [ **HTTP セキュリティ**] リンクをクリックして、[**フレームの埋め込みを許可**する] の横にあるチェックボックスをオンにします。
    * 次の手順では、Moodle API の機能を有効にする web サービスを有効にします。 [**高度な機能**] リンクをクリックし、[ **Web サービスを有効**にする] の横にあるチェックボックスがオンになっていることを確認します。
    * 最後に、Office 365 の外部サービスを有効にする必要があります。 [**外部サービス**] リンクをクリックします。
        * **Moodle Office 365**の [アプリケーション] 行の [**編集**] をクリックします。
        * チェックボックスに [**有効**] をマークし、[**変更の保存**] をクリックします。
    * 次に、認証済みユーザーのアクセス許可を編集して、web サービストークンを作成できるようにする必要があります。 [**役割の認証済みユーザーの編集**] リンクをクリックします。 下にスクロールして [ **web サービストークンの作成**] 機能を見つけ、[**許可**] チェックボックスをオンにします。

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>手順 3: Moodle Assistant Bot を Azure に展開する

> [!VIDEO https://www.youtube.com/embed/gbkJxf8FlfY]

Microsoft Teams 用の無料の Moodle アシスタント Bot は、教師や学生が Moodle のコース、課題、成績、その他の情報についての質問に答える際に役立てることができます。 Bot は、Teams 内で Moodle 通知を学生と教師にも送信します。 この bot は、Microsoft によって管理されているオープンソースプロジェクトであり、 [GitHub で利用でき](https://github.com/microsoft/Moodle-Teams-Bot)ます。

> [!NOTE]
> このセクションでは、Azure サブスクリプションにリソースを展開し、すべてのリソースを**free**層を使用して構成します。 Bot の使用状況によっては、これらのリソースを拡張する必要がある場合があります。
> Bot を使用せずに Moodle タブのみを使用する場合は、[手順 4](#step-4-deploy-your-microsoft-teams-app)に進みます。

### <a name="moodle-bot-information-flow"></a>Moodle bot 情報フロー

<img width="530px" src="~/assets/images/MoodleBotInformationFlow.png" title="Moodle bot for Microsoft Teams 情報フロー" />

Bot をインストールするには、最初に[Microsoft Identity Platform](https://identity.microsoft.com/Landing)に登録する必要があります。 これにより、ボットは Microsoft エンドポイントに対して認証を受けることができます。 Bot を登録するには

1. [プラグインの管理] ページ ([サイトの管理 > プラグイン > Microsoft Office 365 統合]) に戻り、[ **Teams の設定**] タブを選択します。
1. **Microsoft アプリケーション登録ポータル**のリンクをクリックして、microsoft Id でログインします。
1. アプリの名前を入力します (例: MoodleBot) をクリックし、[**作成**] ボタンをクリックします。
1. **アプリケーション id**をコピーして、[**チーム設定**] ページの [ **Bot アプリケーション id** ] フィールドに貼り付けます。
1. [**新しいパスワードの生成**] ボタンをクリックします。 生成されたパスワードをコピーして、[**チーム設定**] ページの [ **Bot アプリケーションパスワード**] フィールドに貼り付けます。
1. フォームの一番下までスクロールし、[**変更の保存**] をクリックします。

アプリケーション Id とパスワードが生成されたので、ボットを Azure に展開します。 [ **Azure に展開する**] ボタンをクリックして、フォームに必要な情報 (Bot アプリケーション Id、Bot アプリケーションパスワード、および Moodle シークレットが [**チーム設定**] ページにあり、Azure information が [**セットアップ**] ページにあります) を入力します。 フォームに入力したら、使用条件に同意するには、チェックボックスをクリックして、[**購入**] ボタンをクリックします (すべての Azure リソースは free 層に展開されます)。

Azure へのリソースの展開が終了したら、そのメッセージングエンドポイントを使用して Office 365 Moodle プラグインを構成する必要があります。 最初に、Azure の Bot からエンドポイントを取得する必要があります。 そのためには、次の操作を行います。

1. まだサインインしていない場合は、 [Azure portal](https://portal.azure.com)にログインします。
2. 左側のウィンドウで、[**リソースグループ**] を選択します。
3. リストから、Bot を展開するときに使用した (または作成した) リソースグループを選択します。
4. グループ内のリソースのリストから**WebApp Bot**リソースを選択します。
5. [**概要**] セクションから**メッセージングエンドポイント**をコピーします。
6. Moodle で、Office 365 Moodle プラグインの [**チーム設定**] ページを開きます。
7. **Bot エンドポイント**フィールドにコピーした URL を貼り付け、word*メッセージ*を*webhook*に変更します。 URL は次のようになります。`https://botname.azurewebsites.net/api/webhook`
8. [**変更の保存**] をクリックします。
9. 変更を保存したら、[**チームの設定**] タブに戻り、[**マニフェストファイルのダウンロード**] ボタンをクリックして、マニフェストパッケージをコンピューターに保存します (次のセクションで使用します)。

## <a name="step-4-deploy-your-microsoft-teams-app"></a>手順 4: Microsoft Teams アプリを展開する

> [!VIDEO https://www.youtube.com/embed/2rMb7gtM_ZM]

Bot を Azure に展開して、Moodle サーバーと通信するように構成したので、今度は Microsoft Teams アプリを展開します。 これを行うには、前の手順の「Office 365 Moodle Plugin Team Settings」ページからダウンロードしたマニフェストファイルを読み込みます。

アプリをインストールする前に、外部アプリとアプリのアップロードが有効になっていることを確認する必要があります。 そのためには、次[の手順](https://docs.microsoft.com/microsoftteams/platform/get-started/get-started-tenant)を実行します。 外部アプリが有効になっていることを確認したら、次の手順に従ってアプリを展開できます。

1. Microsoft Teams を開きます。
2. ナビゲーションバーの左下にある [**ストア**] アイコンをクリックします。
3. オプションの一覧から [**カスタムアプリのアップロード**] リンクをクリックします。 *注:* グローバル管理者としてログインしている場合は、組織のアプリストアにアプリをアップロードするオプションがあります。そうしないと、自分がメンバーになっているチームに対してのみアプリを読み込むことができます。
4. 以前に`manifest.zip`ダウンロードしたパッケージを選択し、[**保存**] をクリックします。 マニフェストパッケージをまだダウンロードしていない場合は、Moodle の [プラグインの構成] ページの [**チームの設定**] タブから実行できます。

これで、アプリがインストールされました。これで、アクセスできるチャネルにタブを追加することができます。 これを行うには、チャネルに移動し**+** 、シンボルをクリックして、リストからアプリを選択します。 画面に表示される指示に従って、チャネルへの Moodle コースタブの追加を完了します。

するだけです。 お客様とチームは、Microsoft Teams から直接 Moodle コースで作業を開始できるようになります。

機能の要求やフィードバックをお客様と共有するには、[ユーザーの音声ページ](https://microsoftteams.uservoice.com/forums/916759-moodle)にアクセスしてください。
