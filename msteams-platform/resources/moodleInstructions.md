---
title: Microsoft Teams との取り組み
description: Microsoft Teams 用のLesle 統合アプリをインストールして構成する方法
keywords: Teams の Teams の Teams 用アプリ統合プラグイン
ms.topic: how-to
ms.author: lajanuar
author: laujan
ms.openlocfilehash: bb3de6b3897105ff3564ecd332cba28a0db85b0f
ms.sourcegitcommit: a16590b2ccc46e1b6d17cbb367762a3c16ff779c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2021
ms.locfileid: "50115742"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>Microsoft Teams との取り組み

人気のあるオープン ソースの学習管理システム (LMS) である[Hedle](https://moodle.org/)は、Microsoft Teams と統合されました。 この統合により、教師と教師は、Teams 内で、レベルや課題に関する共同作業、成績や課題に関する質問、通知を直接使用して最新の情報を得る際に役立ちます。

IT 管理者が簡単にこの統合をセットアップするために、Microsoft 365 のオープン ソースの、次の機能を備える、Microsoft 365 のグループプラグインを更新しました。

* [Azure Active Directory (Azure](https://azure.microsoft.com/services/active-directory/) AD) を使用して、使用しているのが、使用しているのが、Azure Active Directory サーバーの自動登録AD。
* Azure への、1 回のクリックで、あなたのLesure アシスタント ボットの展開を行います。
* チームの自動プロビジョニングと、すべてのチーム登録の自動同期、または選択した 、すべての Teams コースに対する Teams 登録の自動同期。
* 同期された各チームに、[リキードル] タブと [リキードル アシスタント ボット] を自動インストールします。

この統合が提供する機能の詳細については[、Microsoft Teams との「リピドル」を参照してください](https://education.microsoft.com/resource/3dffb3a8)。

## <a name="prerequisites"></a>前提条件

このアプリケーションをインストールして構成するには、以下が必要です。

1. 管理者の資格情報を使用します。

1. Azure AD管理者の資格情報。

1. 新しいリソースを作成できる Azure サブスクリプション。

## <a name="step-1-install-the-microsoft-365-moodle-plugins"></a>手順 1: Microsoft 365 のLesle プラグインをインストールする

Microsoft Teams でのリムードルの統合は、オープン ソース [の Microsoft 365 のグループプラグイン セットによって動作します](https://github.com/Microsoft/o365-moodle)。 このプラグインを使用する場合は、次のコードをインストールする必要があります。

1. 現在 [安定しているバージョンのLesle](https://download.moodle.org/releases/latest/)。

1. ローカル コンピューターにダウンロードされ、保存された、近くの Microsoft 365 統合プラグインと、1 つの使い方を示す、使い方が分からない [OpenID](https://moodle.org/plugins/auth_oidc) Connect プラグインと [Microsoft 365](https://moodle.org/plugins/local_o365) 統合プラグイン。

> [!NOTE]
> Teams 統合には、OpenID Connect プラグインと Microsoft 365 統合プラグインのインストールが必要です。 さらに [、Microsoft 365 Teams テーマ プラグイン](https://moodle.org/plugins/theme_boost_o365teams) を強くお勧めします。

3. 管理者として、使用しているグループのサーバーにログインし、左側のナビゲーション[](https://docs.moodle.org/22/en/Settings_block)パネルにある [設定] ブロックから [サイトの管理] を選択します。

1. [プラグイン **] タブを選択** し、[プラグインのインストール **] を選択します**。

1. [ZIP ファイル **からのプラグインのインストール] セクションで** 、[ファイルの選択 **] ボタンを選択** します。

1. 左側の **ナビゲーションから [ファイルの** アップロード] オプションを選択し、上記でダウンロードしたファイルを参照して、[このファイルのアップロード **] を選択します**。

1. 左側の **ナビゲーション パネルから** [サイトの管理] オプションを選択して、管理ダッシュボードに戻ります。 ローカル プラグインまで **下にスクロールし、Microsoft** **365 統合リンクを選択** します。 **インストール プロセスを通じて、この構成ページは別のブラウザー タブで開いた状態に保ちます**。

詳細については、下書きドキュメントを参照 [してください](https://docs.moodle.org/34/en/Installing_plugins)。

> [!IMPORTANT]
>
> * Microsoft 365 の PageLe Plugin 構成ページは、別のブラウザー タブで開いた状態に保ちます。プロセスを通じて、この一連のページに戻ります。  <br/><br/>
>* 既存のLesure サイトをお持ちない場合は、Azure のレポで、お客様のニーズに合わせて、簡単に、また、そのインスタンスをカスタマイズできる、Azure の [Repo](https://github.com/azure/moodle) で、使い方を確認できます。

## <a name="step-2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>手順 2: Microsoft 365 プラグインと Azure Active Directory (Azure AD) の間の接続を構成する

次に、Azure AD で、アプリケーションとして、取り扱いを行う必要AD。 このプロセスの完了に役立つ PowerShell スクリプトが用意されています。 PowerShell スクリプトは、Microsoft 365 テナント用の新しい Azure AD アプリケーションをプロビジョニングします。このアプリケーションは、Microsoft 365 のグループ プラグインで使用されます。 スクリプトは、Microsoft 365 テナント用にアプリをプロビジョニングし、プロビジョニングされたアプリに必要な応答 URL とアクセス許可を設定して `AppID` 、 `Key` 生成された Microsoft 365 の Pagele プラグインのセットアップ ページを使用して、Azure AD を使用して、Pagele サーバー サイト `AppID` `Key` を構成できます。

>[!IMPORTANT]
> PowerShell スクリプトは最新の構成項目で更新されないので、この構成は [、3.8.0.4 および 3.9.1 および 3.8.0.5](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) および [3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) リリース ページで説明されている手順に従って手動で完了する必要があります。 </br></br>
> PowerShell スクリプトが自動化している手動の手順を詳細に表示するには、「[アプリケーションとして使うのに用](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)件を登録する」を参照してください。

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Microsoft Teams の情報フローの [ダイアログ] タブ

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. Microsoft 365 統合プラグインページで、[セットアップ] タブ **を選択** します。

1. **[PowerShell スクリプトのダウンロード] ボタンを** 選択し、ローカル コンピューターに保存します。

1. ZIP ファイルから PowerShell スクリプトを準備する必要があります。 これを行うには、以下のようにします。

    * ファイルをダウンロードして展開 `Moodle-AzureAD-Powershell.zip` します。
    * 抽出されたフォルダーを開きます。
    * ファイルを右クリックし、[ `Moodle-AzureAD-Script.ps1` プロパティ] を選択 **します**。
    * [プロパティ **] ウィンドウ** の [全般] タブで、ウィンドウの下部にある Security 属性の横にある `Unblock` チェック ボックスをオンにします。 
    * **[OK]** を選択します。
    * ディレクトリ パスを、抽出されたフォルダーにコピーします。

1. 次に、管理者として PowerShell を実行します。

    * [開始] を選択します。
    * 「PowerShell」と入力します。
    * ウィンドウを右クリックWindows PowerShell。
    * [管理者として実行] を選択します。

1. ディレクトリへのパスの場所を入力して、未定義 `cd .../.../Moodle-AzureAD-Powershell` `.../...` のディレクトリに移動します。

1. PowerShell スクリプトを実行します。

    * Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` キーを押します。
    * Enter `./Moodle-AzureAD-Script.ps1` キーを押します。
    * ポップアップ ウィンドウで Microsoft 365 管理者アカウントにログインします。
    * Azure AD アプリケーションの名前を入力します (例:、グループ/プラグインを使用します)。
    * 使用しているのが、使用しているのが、あなたのLesle サーバーの URL を入力します。
    * スクリプトによって **生成された** アプリケーション ID **とアプリケーション** キーをコピーし、保存します。

1. 次に ` AppID` `Key` 、Microsoft 365 のグループプラグインと Microsoft 365 のLe プラグインに追加する必要があります。 プラグインの管理ページ (Microsoft 365 統合➡プラグイン➡管理) に戻ります。

1. [セットアップ **] タブ** で、前にコピーした **アプリケーション ID** と **アプリケーション** キーを追加し、[変更の保存] **を選択します**。

1. ページが更新された後、新しいセクションが表示されます接続方法 **を選択します**。 [既定] というラベルのチェック **ボックスを** オンにし、[変更の保存 **] を再び選択** します。

1. ページが更新された後、別の新しいセクション管理者の同意が表示され **&情報が表示されます**。
    * [管理者の **同意の** 提供] リンクを選択し、Microsoft 365グローバル管理者の資格情報を入力し、[承諾] を選択してアクセス許可を付与します。
    * Azure AD **テナント フィールドの横** にある [検出] ボタン **を選択** します。
    * **OneDrive for Business URL の横にある [** 検出] ボタン **を選択** します。
    * フィールドにデータが入力された後、[変更の保存] **ボタンを** 再度選択します。

1. [更新] **ボタンを** 選択してインストールを確認し、[変更の保存 **] をクリックします**。

1. 次に、ユーザーを、使用しているのが、Azure サーバーと Azure サーバーの間で同期AD。 環境に応じて、この段階で異なるオプションを選択できます。 次の手順をお試しください。
    * [同期設定] **タブに切り替える**
    * [Azure **ユーザーと同期] セクションAD、** 環境に適用するチェック ボックスをオンにします。 通常、少なくとも次の項目を選択します。  

        ✔ Azure AD でユーザーのアカウントを作成します。 
        ✔ Azure AD のユーザーの、グループのすべてのアカウントを更新します。  

    * [ **ユーザー作成の制限** ] セクションでは、フィルターを設定して、Filterle に同期される Azure ADユーザーを制限できます。
    * [ **ユーザー フィールド マッピング]** セクションでは、Azure ユーザー プロファイルとADユーザー プロファイル のフィールド マッピングをカスタマイズできます。
    * Teams **の同期セクション** では、既存のLeele コースの一部またはすべてについて、グループ (チーム) を自動的に作成できます。

> [!NOTE]
> (既定では [1](https://docs.moodle.org/310/en/Cron) 日に 1 回) タスク のスケジュールに従って、1 つが実行されます。 ただし、すべての同期を維持するために、cron の実行頻度を高くする必要があります。

13. 最初の [実行のために、cron](https://docs.moodle.org/310/en/Cron)ジョブを検証する (または手動で実行する) には、[Azure AD] セクションの [ユーザーの同期] で [スケジュールされたタスク管理]**ページのリンクを選択** します。 これにより、[スケジュールされたタスク] **ページに移動** します。

    * 下にスクロールして **、Azure** AD同期ユーザーを検索し、[今すぐ **実行] を選択します**。
    * 既存のコースに基づいてグループを作成することを選択した場合は **、Microsoft 365** でユーザー グループの作成ジョブを実行することもできます。

1. プラグインの管理ページ (Microsoft 365 統合➡プラグイン➡管理) に戻り、[Teams の設定] ページ **を選択** します。 Teams アプリの統合を有効にするには、いくつかの設定を構成する必要があります。

    * **OpenID Connect を有効にするには**、[認証の管理] リンクを選択し **、OpenId Connect** 行の目のアイコンが灰色表示されている場合は選択します。 
    * 次に、フレーム埋め込み機能を有効にする必要があります。 **[HTTP セキュリティ] リンクを** 選択し、[フレームの埋め込みを許可する] の横にある **チェック ボックスをオンにします**。
    * 次の手順では、ブラウザー API 機能を有効にする Web サービスを有効にします。 [高度 **な機能]** リンクを選択し、[Web サービスを有効にする] の横にあるチェック **ボックスがオンになっていることを** 確認します。
    * 最後に、Microsoft 365 の外部サービスを有効にする必要があります。 次に、[ **外部サービス] リンク** を選択します。  

        ✔Microsoft  **365 Webservices 行で [編集] を選択** します。  
        ✔を有効にする] チェック ボックスを **オンにし**、[変更の保存] **を選択します。**

    * 次に、認証されたユーザーのアクセス許可を編集して、Web サービス トークンの作成を許可する必要があります。 編集役割 **の [認証されたユーザー] リンクを選択** します。 下にスクロールして **[Web** サービス トークンの作成] 機能を見つけ、[許可] チェック ボックス **をオン** にします。

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>手順 3: Azure にLesure アシスタント ボットを展開する

Microsoft Teams 用の無料のリズル アシスタント ボットは、教師と学生が、コース、課題、成績、その他の情報に関する質問に対して、リムードルで回答するのに役立ちます。 ボットは、Teams 内の学生と教師にも、通知を送信します。 ボットは Microsoft が管理するオープン ソース プロジェクトであり [、GitHub で利用できます](https://github.com/microsoft/Moodle-Teams-Bot)。

> [!NOTE]
> このセクションでは、Azure サブスクリプションにリソースを展開します。 すべてのリソースは、無料の階層を使用 **して構成** されます。 ボットの使用状況によっては、これらのリソースのスケーリングが必要な場合があります。
> ボットなしで [色] タブを使用する場合は、手順 [4 に進みます](#step-4-deploy-your-microsoft-teams-app)。

### <a name="moodle-bot-information-flow"></a>リムードル ボット情報フロー

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

ボットをインストールするには、最初に Microsoft Identity Platform にボットを [登録する必要があります](https://identity.microsoft.com/Landing)。 これにより、ボットは Microsoft エンドポイントに対して認証できます。 ボットを登録するには:

1. プラグインの管理ページ (Microsoft 365 統合➡プラグイン➡管理) に戻り、[Teams の設定] タブ **を選択** します。

1. Microsoft アプリケーション **登録ポータルのリンクを選択** し、Microsoft ID でログインします。

1. アプリの名前 (例: MoodleBot) を入力し、[作成] ボタン **を選択** します。

1. アプリケーション **ID をコピーし** 、[チームの設定] ページの **[Bot Application ID]** フィールド **に貼り付** けます。

1. [新しい **パスワードの生成] ボタンを選択** します。 生成されたパスワードをコピーし、[チームの設定] ページの **[Bot Application Password]** フィールド **に貼り付** けます。

1. フォームの下部までスクロールし、[変更の保存] **を選択します**。

アプリケーション ID とパスワードを生成し、次にボットを Azure に展開します。

> [!div class="checklist"]
> * [Azure **に展開** ] ボタンを選択し、必要な情報を含むフォームに入力します (Bot Application ID、Bot Application Password、および、および、取り込みシークレットが [チームの設定] ページに **表示** されます)。 Azure の情報は、[セットアップ] **ページに表示** されます。 
> * フォームが完成したら、チェック ボックスをオンにして使用条件に同意します。
> * [ **購入] ボタン** を選択します (すべての Azure リソースが無料層に展開されます)。

リソースが Azure への展開を完了したら、メッセージング エンドポイントを使用して Microsoft 365 の取り決めプラグインを構成する必要があります。 Azure のボットからエンドポイントを取得する必要があります。

1. Azure Portal に [ログインします](https://portal.azure.com)。

1. 左側のウィンドウで [ **リソース** グループ] を選択し、ボットの展開中に使用した (または作成した) リソース グループを選択します。

1. グループ内 **のリソースの** 一覧から WebApp Bot リソースを選択します。

1. [概要 **] セクションから** メッセージング エンドポイント **をコピー** します。

1. In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugin.

1. ボット エンドポイント **フィールドに**、コピーした URL を貼り付け、単語メッセージを *webhook に変更します*。 URL は次のように表示されます。  `https://botname.azurewebsites.net/api/webhook`

1. [変更 **の保存] を選択します**。

1. 変更を保存したら、[チームの設定] タブに戻り、[マニフェストファイルのダウンロード] ボタンを選択して、アプリ マニフェスト パッケージをコンピューターに保存します (次のセクションで使用します)。

## <a name="step-4-deploy-your-microsoft-teams-app"></a>手順 4: Microsoft Teams アプリを展開する

ボットが Azure に展開され、次に、使用しているのが、リピドル サーバーと話をするように構成されたので、次に Microsoft Teams アプリを展開します。 これを行うには、前の手順で Microsoft 365 の Pagele Plugin チーム設定ページからダウンロードしたアプリ マニフェスト ファイルを読み込みます。

アプリをインストールする前に、外部アプリとアプリのアップロードが有効になっている必要があります。 これを行うには、Teams で [Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) テナントのドキュメントを準備する手順に従います。 外部アプリを有効にしたら、次の手順に従ってアプリを展開できます。

1. **Microsoft Teams を開きます**。 

1. ナビゲーション バー **の** 左下の領域にある [アプリ] アイコンを選択します。

1. オプションの **一覧から [カスタム アプリの** アップロード] リンクを選択します。

> [!Note]
> グローバル管理者としてログインしている場合は、組織のアプリ カタログにアプリをアップロードするオプションがあります。そうしないと、自分がメンバーであるチームのアプリのみを読み込む事が可能になります。

4. 以前にダウンロード `manifest.zip` したパッケージを選択し、[保存] を **選択します**。 アプリ マニフェスト パッケージをダウンロードしていない場合は、Pluginle のプラグイン構成ページの [ **チーム** 設定] タブからダウンロードできます。

アプリがインストールされたので、アクセスできる任意のチャネルにタブを追加できます。 これを行うには、チャネルに移動し、 **プラス記号** (➕) を選択し、一覧からアプリを選択します。 画面の指示に従って、チャネルへの [Le のコース] タブの追加を完了します。

## <a name="step-5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>手順 5: Microsoft Teams で 、自動的に [Le] タブを作成することを許可する

Microsoft Teams では 、Teams のタブを手動で作成することもできますが、コースの同期からチームを作成するときに自動的に作成することもできます。 これを行うには、アップロードされた Microsoft Teams アプリの ID を次のページで構成します。

1. Microsoft Teams を開きます。

1. ナビゲーション バーの左下の領域から [アプリ] アイコンを選択します。

1. アップロードされた **Happle アプリを見つけて➡** オプション アイコンを選択し➡リンク **を選択します**。 

1. テキスト エディターで、コピーしたコンテンツを貼り付けます。 ht などの URL を含&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff。 URL の最後の部分 (Microsoft Teams アプリの ID など) `00112233-4455-6677-8899-aabbccddeeff` をコピーします。

1. リシェルで **、Microsoft** 365 の Page.365 の [Plugin] 構成ページから Teams の [Teams 用の Teams のページ] タブを開きます。

1. Microsoft Teams アプリの ID を [表示] アプリ ID フィールドに貼り付け、変更を保存します。

今度は、Teamsle のコースが同期すると、Microsoft Teams は自動的にチームに Pagele アプリをインストールし、Teams の一般チャネルに [Pagele] タブを作成し、同期の対象となる、Pagele コースのコース ページを含む設定を行います。

### <a name="thats-it-you-and-your-team-can-now-start-working-with-your-moodle-courses-directly-from-microsoft-teams"></a>手順は以上です。 これで、お客様とチームは、Microsoft Teams から直接、自分の Teamsle コースの操作を開始できます。

機能に関するリクエストやフィードバックを共有するには、User Voice ページ [にアクセスしてください](https://microsoftteams.uservoice.com/forums/916759-moodle)。
