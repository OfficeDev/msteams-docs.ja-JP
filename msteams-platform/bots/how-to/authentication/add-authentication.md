---
title: Teams の bot に認証を追加する
author: clearab
description: Microsoft Teams の bot に OAuth 認証を追加する方法。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 2b9765a2f295e85dc9b4d2c1b1ddcae4d642e268
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590873"
---
# <a name="add-authentication-to-your-teams-bot"></a>Teams の bot に認証を追加する

メールサービスなど、ユーザーの代わりにリソースにアクセスできる、Microsoft Teams でボットを作成しなければならない場合があります。

この記事では、OAuth 2.0 に基づいて Azure Bot サービス v4 SDK 認証を使用する方法について説明します。 これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットを開発するのが容易になります。 すべてのキーこれは、後で説明するように、 **id プロバイダー**を使用していることです。

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。

基本的な理解と、完全な仕様の[oauth 2.0](https://oauth.net/2/)については、「 [Oauth 2 の単純化](https://aka.ms/oauth2-simplified)」を参照してください。

Azure Bot サービスが認証を処理する方法の詳細については、「[会話内のユーザー認証](https://aka.ms/azure-bot-authentication)」を参照してください。

この記事では、以下について説明します。

- **認証を有効にした bot を作成する方法**。 ユーザーのサインイン資格情報と認証トークンの生成を処理するには、 [cs-auth-サンプル][teams-auth-bot-cs]を使用します。
- **Bot を Azure に展開し、id プロバイダーに関連付ける方法について説明**します。 プロバイダーは、ユーザーのサインイン資格情報に基づいてトークンを発行します。 Bot は、トークンを使用して、メールサービスなど、認証を必要とするリソースにアクセスできます。 詳細については、「[ボットの Microsoft Teams 認証フロー](auth-flow-bot.md)」を参照してください。
- **Microsoft Teams 内で bot を統合する方法**。 Bot が統合されたら、チャットでサインインしてメッセージを交換することができます。

## <a name="prerequisites"></a>前提条件

- ボットの[基礎][concept-basics]知識、[状態の管理][concept-state]、[ダイアログライブラリ][concept-dialogs]、[シーケンシャルな会話フローを実装][simple-dialog]する方法を理解します。
- Azure および OAuth 2.0 の開発に関する知識。
- 現在のバージョンの Visual Studio および Git。
- Azure アカウント。 必要に応じて、 [Azure 無料アカウント](https://azure.microsoft.com/free/)を作成できます。
- 次に例を示します。

    | サンプル | BotBuilder のバージョン | もの |
    |:---|:---:|:---|
    | **Bot authentication** [(Cs 認証)-auth-サンプル][teams-auth-bot-cs] | ipv4 | OAuthCard のサポート |
    | Js の**ボット認証** [-auth-サンプル][teams-auth-bot-js] | ipv4| OAuthCard のサポート  |
    | Py での**Bot 認証**-[サンプル][teams-auth-bot-py] | ipv4 | OAuthCard のサポート |

## <a name="create-the-resource-group"></a>リソースグループを作成する

リソースグループとサービスプランは厳密には必要ありませんが、作成したリソースを容易に解放することができます。 これは、リソースを整理して管理できるようにするための適切な方法です。

リソースグループを使用して、Bot フレームワークの個々のリソースを作成します。 パフォーマンスを確保するために、これらのリソースが同じ Azure 地域にあることを確認してください。

1. ブラウザーで、 [**Azure portal**][azure-portal]にサインインします。
1. 左側のナビゲーションパネルで、[**リソースグループ**] を選択します。
1. 表示されたウィンドウの左上で、[タブの**追加**] を選択して新しいリソースグループを作成します。 次の情報を入力するように求められます。
    1. **サブスクリプション**。 既存のサブスクリプションを使用します。
    1. **リソースグループ**。 リソースグループの名前を入力します。 例として、 *Teamsresourcegroup*が考えられます。 名前は一意である必要があることに注意してください。
    1. [**地域**] ドロップダウンメニューから [ *West US*] を選択するか、アプリケーションに近い地域を選択します。
    1. [**確認して作成**] ボタンを選択します。 *検証が成功*したことを示すバナーが表示されます。
    1. [**作成**] ボタンを選択します。 リソースグループの作成には、数分かかる場合があります。

> [!TIP]
> このチュートリアルの後の方で作成するリソースと同様に、このリソースグループをダッシュボードに固定して簡単にアクセスできるようにすることをお勧めします。 これを行う場合は、pin アイコン & # 128204; を選びます。ダッシュボードの右上にあります。

## <a name="create-the-service-plan"></a>サービスプランを作成する

1. [**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[**リソースの作成**] を選択します。
1. [検索] ボックスに「 *App Service Plan*」と入力します。 検索結果から**App Service プラン**カードを選択します。
1. **[作成]** を選択します。
1. 次の情報を入力するように求められます。
    1. **サブスクリプション**。 既存のサブスクリプションを使用できます。
    1. **リソースグループ**。 前に作成したグループを選択します。
    1. **名前**です。 サービスプランの名前を入力します。 例としては、 *Teamsserviceplan*が考えられます。 グループ内の名前は一意である必要があることに注意してください。
    1. **オペレーティングシステム**。 *Windows*または該当する OS を選択します。
    1. **地域**。 [ *WEST US* ] または [アプリケーションに近い地域] を選択します。
    1. **価格レベル**。 *標準 S1*が選択されていることを確認します。 これは既定値である必要があります。
    1. [**確認して作成**] ボタンを選択します。 *検証が成功*したことを示すバナーが表示されます。
    1. **[作成]** を選択します。 App service プランを作成するには、数分かかる場合があります。 計画がリソースグループに一覧表示されます。

## <a name="create-the-bot-channels-registration"></a>Bot チャネル登録を作成する

Bot チャネル登録は、Microsoft アプリ Id とアプリパスワード (クライアントシークレット) がある場合に、ボットフレームワークを使用して web サービスをボットとして登録します。

> [!IMPORTANT]
> Bot が Azure でホストされていない場合にのみ、ボットを登録する必要があります。 Azure ポータルを使用して[ボットを作成](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0)した場合は、既にサービスに登録されています。 Bot[フレームワーク](https://dev.botframework.com/bots/new)または[appstudio](~/concepts/build-and-test/app-studio-overview.md)を使用して bot を作成した場合、その bot は Azure に登録されていません。

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> Bot チャネル登録リソースは、[West US] を選択した場合でも、**グローバル**地域を表示します。 これは正常な動作です。

詳細については、「 [Teams の bot を作成する](../create-a-bot-for-teams.md)」を参照してください。

## <a name="create-the-identity-provider"></a>Id プロバイダーを作成する

認証に使用できる id プロバイダーが必要です。
この手順では、Azure AD プロバイダーを使用します。他の Azure AD でサポートされている id プロバイダーを使用することもできます。

1. [**Azure portal**][azure-portal]の左側のナビゲーションパネルで、[ **azure Active Directory**] を選択します。
    > [!TIP]
    > アプリケーションによって要求されたアクセス許可の委任を承認するには、この Azure AD リソースを作成してテナントに登録する必要があります。
    > テナントを作成する手順については、「[ポータルにアクセスし、テナントを作成](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)する」を参照してください。
1. 左側のパネルで、[**アプリの登録**] を選択します。
1. 右パネルで、左上にある [**新しい登録**] タブを選択します。
1. 次の情報を入力するように求められます。
   1. **名前**です。 アプリケーションの名前を入力します。 例として、 *BotTeamsIdentity*が考えられます。 名前は一意である必要があることに注意してください。
   1. アプリケーションに対し**てサポートされているアカウントの種類**を選択します。 *任意の組織ディレクトリ (任意の AZURE AD ディレクトリ-マルチテナント) と個人の Microsoft アカウント (Skype、Xbox など) でアカウント*を選択します。
   1. **リダイレクト URI**の場合:<br/>
       [ **Web**] を &#x2713;選択します。 <br/>
       &#x2713; URL をに設定 `https://token.botframework.com/.auth/web/redirect` します。
   1. **[登録]** を選択します。

1. 作成されたアプリの**概要**ページが Azure に表示されます。 次の情報をコピーしてファイルに保存します。

    1. **アプリケーション (クライアント) ID**値。 この値は、この Azure id アプリケーションを bot に登録するときに、*クライアント ID*として後で使用します。
    1. **ディレクトリ (テナント) ID**の値。 この値を後で*テナント id*として使用して、この Azure id アプリケーションを bot に登録することもできます。

1. 左側のパネルで、[**証明書 & シークレット**] を選択して、アプリケーションのクライアントシークレットを作成します。

   1. [**クライアントシークレット**] で、[**新しいクライアントシークレット**&#x2795;] を選択します。
   1. このシークレットを、 *Teams の Bot id アプリ*など、このアプリ用に作成する必要がある他のユーザーから識別するための説明を追加します。
   1. 選択範囲に**期限**を設定します。
   1. **[追加]** を選択します。
   1. このページを終了する前に、**シークレットを録音して**ください。 この値は、ボットを使用して Azure AD アプリケーションを登録するときに、_クライアントシークレット_として後で使用します。

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>Id プロバイダー接続を構成し、bot に登録する

1. [**Azure portal**][azure-portal]で、ダッシュボードからリソースグループを選択します。
1. Bot チャネル登録リンクを選択します。
1. [リソース] ページで、[**設定**] を選択します。
1. ページの下部付近にある [ **OAuth 接続設定**] で、[**設定の追加**] を選択します。
1. フォームに次のように入力します。

    1. **名前**です。 接続の名前を入力します。 この名前は、ファイル内の bot で使用し `appsettings.json` ます。 たとえば、 *BotTeamsAuthADv1*のようになります。
    1. **サービスプロバイダー**。 [**Azure Active Directory**] を選択します。 このチェックボックスをオンにすると、Azure AD 固有のフィールドが表示されます。
    1. **クライアント id**。前述の手順で、Azure id プロバイダアプリ用に記録したアプリケーション (クライアント) ID を入力します。
    1. **クライアントシークレット**。 前述の手順で、Azure id プロバイダアプリ用に記録したシークレットを入力します。
    1. **許可の種類**。 Enter キーを押し `authorization_code` ます。
    1. **ログイン URL**。 Enter キーを押し `https://login.microsoftonline.com` ます。
    1. [**テナント id**] は、id プロバイダーアプリの作成時に選択したサポートされるアカウントの種類**に応じて**、前の手順で Azure id アプリ用に記録した**ディレクトリ (テナント) id**を入力します。 割り当てる値を決定するには、次の条件を満たす必要があります。

        - [*この組織ディレクトリにあるアカウント] のみ (microsoft only-単一テナント)* または*任意の組織ディレクトリのアカウント (microsoft AAD ディレクトリ-マルチテナント)* を選択した場合は、AAD アプリの前に記録した**テナント ID**を入力します。 これは、認証が可能なユーザーに関連付けられているテナントになります。

        - 任意の組織ディレクトリでアカウントを選択した場合 *(任意の AAD ディレクトリ-マルチテナントおよび個人の Microsoft アカウント (Skype、Xbox、Outlook など)* の場合は、テナント ID ではなく**common**という単語を入力します。 それ以外の場合、AAD アプリは、ID が選択されたテナントを経由して検証し、個人の Microsoft アカウントを除外します。

    h. [**リソースの URL**] で、と入力し `https://graph.microsoft.com/` ます。 これは、現在のコードサンプルでは使用されません。  
    i. **範囲**を空白のままにします。 次の画像は例です。

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. [**保存**] を選択します。

### <a name="test-the-connection"></a>接続をテストする

1. 接続エントリを選択して、作成したばかりの接続を開きます。
1. [**サービスプロバイダ接続設定**] パネルの上部にある [**テスト接続**] を選択します。
1. 最初にこの操作を行うと、新しいブラウザーウィンドウが開き、アカウントを選択するように求められます。 使用するものを選択します。
1. 次に、id プロバイダーがデータ (資格情報) を使用することを許可するように求められます。 次の画像は例です。

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. **[同意する]** を選択します。
1. これで、[**テスト接続は \<your-connection-name> 成功しまし**た] ページにリダイレクトされます。 エラーが表示された場合は、ページを更新します。 次の画像は例です。

  ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

接続名は、ユーザー認証トークンを取得するために bot コードによって使用されます。

## <a name="prepare-the-bot-sample-code"></a>Bot サンプルコードを準備する

事前設定を完了したら、この記事で使用する bot の作成に重点を置いて説明します。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. 複製の[cs-auth-サンプル][teams-auth-bot-cs]。
1. Visual Studio を起動します。
1. ツールバーの [**ファイル]-> [> プロジェクト/ソリューション**] を選択し、bot プロジェクトを開きます。
1. C# では、次のようにして**appsettings**を更新します。

    - `ConnectionName`Bot チャネル登録に追加した id プロバイダー接続の名前に設定します。 この例で使用した名前は*BotTeamsAuthADv1*です。
    - `MicrosoftAppId`Bot チャネル登録時に保存した**BOT アプリ ID**に設定します。
    - `MicrosoftAppPassword`Bot チャネル登録時に保存した**お客様のシークレット**に設定します。
    - `ConnectionName`を id プロバイダー接続の名前に設定します。

    Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。 たとえば、任意のアンパサンド (&) をとしてエンコードする必要があり `&amp;` ます。

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. ソリューションエクスプローラーで、フォルダーに移動して、 `TeamsAppManifest` `manifest.json` `id` `botId` ボットチャネルの登録時に保存した**bot アプリ ID**を開き、設定します。

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. クローン[ノード-auth-サンプル][teams-auth-bot-js]。
1. コンソールで、プロジェクトに移動します。 </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. モジュールをインストールする</br></br>
`npm install`
1. 次のようにして、 **env**構成を更新します。

    - `MicrosoftAppId`Bot チャネル登録時に保存した**BOT アプリ ID**に設定します。
    - `MicrosoftAppPassword`Bot チャネル登録時に保存した**お客様のシークレット**に設定します。
    - `connectionName`を id プロバイダー接続の名前に設定します。

    Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。 たとえば、任意のアンパサンド (&) をとしてエンコードする必要があり `&amp;` ます。

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. フォルダーで `teamsAppManifest` 、 `manifest.json` `id` **Microsoft アプリ id**を開き、 `botId` ボットチャネル登録時に保存した**bot アプリ id**を設定します。

# <a name="python"></a>[Python](#tab/python)

1. Github リポジトリからの複製[py-サンプル][teams-auth-bot-py]。
1. **Config.py**を更新します。

    - `ConnectionName`Bot に追加した OAuth 接続設定の名前に設定します。
    - `MicrosoftAppId` `MicrosoftAppPassword` Bot のアプリ ID とアプリシークレットを設定します。

      Bot シークレットの文字によっては、パスワードを XML エスケープする必要があります。 たとえば、任意のアンパサンド (&) をとしてエンコードする必要があり `&amp;` ます。

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>Bot を Azure に展開する

Bot を展開するには、「 [Azure に bot を展開](https://aka.ms/azure-bot-deployment-cli)する方法」の手順に従います。

または、Visual Studio では、次の手順を実行します。

1. Visual Studio の*ソリューションエクスプローラー*で、プロジェクト名を選択して、ホールド (または右クリック) します。
1. ドロップダウンメニューで、[**発行**] を選択します。
1. 表示されたウィンドウで、**新しい**リンクを選択します。
1. ダイアログウィンドウで、左側にある [ **App Service** ] を選択し、右側に [**新規作成**] を作成します。
1. [**発行**] ボタンを選択します。
1. 次のダイアログウィンドウで、必要な情報を入力します。 例を次に示します。

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. **[作成]** を選択します。
1. 展開が正常に完了すると、Visual Studio に反映されたことがわかります。 さらに、*ボットの準備ができ*たことを示すページが既定のブラウザーに表示されます。 URL は、次のようになり `https://botteamsauth.azurewebsites.net/` ます。 ファイルに保存します。
1. ブラウザーで[**Azure ポータル**][azure-portal]に移動します。
1. リソースグループを確認すると、bot が他のリソースと共に一覧表示されます。 次の画像は例です。

    ![teams-auth-service-グループ](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. [リソース] グループで、bot チャネル登録名 (リンク) を選択します。
1. 左側のパネルで、[**設定**] を選択します。
1. [**メッセージングエンドポイント**] ボックスに、上で取得した URL に続けてを入力し `api/messages` ます。 次に例を示します `https://botteamsauth.azurewebsites.net/api/messages` 。
1. 左上隅にある [**保存**] ボタンを選択します。

## <a name="test-the-bot-using-the-emulator"></a>エミュレーターを使用して bot をテストする

まだ行っていない場合は、 [Microsoft Bot フレームワークエミュレーター](https://aka.ms/bot-framework-emulator-readme)をインストールします。 「[エミュレーターを使用してデバッグする](https://aka.ms/bot-framework-emulator-debug-with-emulator)」も参照してください。

Bot のサンプルログインを機能させるには、以下のようにエミュレーターを構成する必要があります。

### <a name="configure-the-emulator-for-authentication"></a>認証用にエミュレーターを構成する

Bot が認証を必要とする場合は、以下に示すように、エミュレーターを構成する必要があります。

1. エミュレーターを起動します。
1. エミュレーターで、左下の歯車アイコン &#9881;、または右上の [**エミュレーターの設定**] タブを選択します。
1. チェックボックスをオンにするには、**バージョン1.0 の認証トークンを使用**します。
1. **Ngrok**ツールへのローカルパスを入力します。 Bot フレームワークエミュレーター/ngrok トンネリング統合[Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))を*参照してください*。 ツールの詳細については、「 [ngrok](https://ngrok.com/)」を参照してください。
1. **エミュレーター起動時に ngrok を実行**してチェックボックスをオンにします。
1. [**保存**] ボタンを選択します。

Bot がサインインカードを表示し、ユーザーがサインインボタンを選択すると、ユーザーが認証プロバイダーでサインインするために使用できるページがエミュレーターに表示されます。
ユーザーがこれを実行すると、プロバイダーはユーザートークンを生成して bot に送信します。 その後、bot はユーザーの代わりに行動することができます。

### <a name="test-the-bot-locally"></a>Bot をローカルでテストする

認証メカニズムを構成した後は、実際の bot テストを実行できます。  

1. Visual Studio を使用して、お使いのコンピューターでローカルに bot サンプルを実行します。
1. エミュレーターを起動します。
1. [ **Open bot** ] ボタンを選択します。
1. Bot の**url**に bot のローカル url を入力します。 通常は、 `http://localhost:3978/api/messages` です。
1. **Microsoft アプリ id**で、bot のアプリ id をから入力し `appsettings.json` ます。
1. **Microsoft App パスワード**に、からの bot のアプリパスワードを入力し `appsettings.json` ます。
1. [**接続**] を選択します。
1. Bot が起動して実行されたら、サインインカードを表示するテキストを入力します。
1. **[サインイン]** ボタンを選択します。
1. 開いている**URL を確認**するポップアップダイアログが表示されます。 これにより、ボットのユーザー (ユーザー) が認証されるようになります。  
1. [**確認**] を選択します。
1. 要求された場合は、該当するユーザーのアカウントを選択します。
1. エミュレーターで使用した構成に応じて、次のいずれかを取得します。
    1. **サインイン確認コードの使用**  
      検証コードを表示するウィンドウが開かれて &#x2713; ます。  
      サインインを完了するには、&#x2713; コピーして、検証コードを [チャット] ボックスに入力します。
    1. **認証トークンを使用**します。  
      資格情報に基づいてログインしている &#x2713;。

    次の図は、ログインした後の bot UI の例です。

    ![auth bot ログインエミュレーター](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. Bot から*トークンを表示するよう*求められたときに **[はい**] を選択すると、次のような応答が表示されます。

    ![auth bot ログインエミュレータートークン](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. サインアウトするには、[チャットの入力] ボックスに「**ログアウト**」と入力します。これにより、ユーザートークンが解放され、再びサインインするまでは、お客様の代わりに bot を操作することはできません。

> [!NOTE]
> Bot 認証には、 **Bot コネクタサービス**を使用する必要があります。 サービスは bot の bot チャネル登録情報にアクセスします。

## <a name="test-the-deployed-bot"></a>展開した bot をテストする

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. ブラウザーで[**Azure ポータル**][azure-portal]に移動します。
1. リソースグループを検索します。
1. [リソース] リンクを選択します。 [リソース] ページが表示されます。
1. [リソース] ページで、[ **Web チャットでテスト**] を選択します。 Bot が開始し、定義済みの案内応答が表示されます。
1. [チャット] ボックスに何か入力します。
1. [**サインイン**] ボックスを選択します。
1. 開いている**URL を確認**するポップアップダイアログが表示されます。 これにより、ボットのユーザー (ユーザー) が認証されるようになります。  
1. [**確認**] を選択します。
1. 要求された場合は、該当するユーザーのアカウントを選択します。
    次の図は、ログインした後の bot UI の例です。

    ![auth bot ログインの展開](../../../assets/images/authentication/auth-bot-login-deployed.PNG).

1. [**はい**] ボタンを選択して、認証トークンを表示します。 次の画像は例です。

    ![auth bot ログイン展開されたトークン](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG).

1. サインアウトするには、「ログアウト」と入力します。

    ![auth bot が展開したログアウト](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> サインインで問題が発生した場合は、前の手順で説明したように、接続をもう一度テストしてください。 これにより、認証トークンが再作成されることがあります。
> 「Azure の Bot フレームワーク Web チャットクライアント」では、認証が正しく設定される前に、数回サインインする必要がある場合があります。

## <a name="install-and-test-the-bot-in-teams"></a>Teams に bot をインストールしてテストする

1. Bot プロジェクトで、フォルダーにとファイルが含まれていることを確認し `TeamsAppManifest` `manifest.json` `outline.png` `color.png` ます。
1. ソリューションエクスプローラーで、フォルダーに移動し `TeamsAppManifest` ます。 `manifest.json`次の値を割り当てることによって編集します。
    1. Bot チャネル登録時に受信した**Bot アプリ ID**がおよびに割り当てられていることを確認し `id` `botId` ます。
    1. 次の値を割り当てます。 `validDomains: [ "token.botframework.com" ]`
1. 、、およびファイルを選択して**zip**にし `manifest.json` `outline.png` `color.png` ます。
1. **Microsoft Teams**を開きます。
1. 左側のパネルで、下部にある [**アプリ] アイコン**を選択します。
1. 右側のパネルで、下部にある [**カスタムアプリのアップロード**] を選択します。
1. フォルダーに移動 `TeamsAppManifest` し、zip マニフェストをアップロードします。
次のウィザードが表示されます。

    ![auth bot teams のアップロード](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. **[チームに追加]** ボタンを選択します。
1. 次のウィンドウで、ボットを使用するチームを選択します。
1. [ **Bot の設定**] ボタンを選択します。
1. 左側のパネルで、3つのドット (&#x25cf;&#x25cf;&#x25cf;) を選択します。 次に、[ **App Studio** ] アイコンを選択します。
1. [**マニフェストエディター** ] タブを選択します。アップロードした bot のアイコンが表示されます。
1. また、bot とのメッセージの交換に使用できる連絡先として、その bot が連絡先として表示されることがあります。

### <a name="testing-the-bot-locally-in-teams"></a>Teams でボットをローカルにテストする

Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからアクセスできるようにするには、すべてのサービスがアクセスする必要があります。 そのため、ボット (サンプル) を Teams で使用できるようにするには、選択したクラウドにコードを発行するか、または**トンネル**ツールを使用して、ローカルに実行しているインスタンスを外部からアクセス可能にする必要があります。 [Ngrok](https://ngrok.com/download)を使用することをお勧めします。この URL は、コンピューター上でローカルに開いたポートに対して、外部アドレス指定可能な URL を作成します。
Microsoft Teams アプリをローカルで実行する準備として ngrok をセットアップするには、次の手順を実行します。

1. ターミナルウィンドウで、がインストールされているディレクトリに移動し `ngrok.exe` ます。 これを指すように、*環境変数*のパスを設定することをお勧めします。
1. たとえば、を実行 `ngrok http 3978 --host-header=localhost:3978` します。 必要に応じてポート番号を置き換えます。
これにより、指定したポートをリッスンする ngrok が起動します。 これにより、ngrok が実行されている限り、外部的にアドレス指定可能な URL が得られます。 次の画像は例です。

    ![teams ボット app auth 接続文字列 adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG).

1. 転送用の HTTPS アドレスをコピーします。 これは、次のようになり `https://dea822bf.ngrok.io/` ます。
1. `/api/messages`取得する追加 `https://dea822bf.ngrok.io/api/messages` 。 これは、コンピューター上でローカルに実行されていて、Microsoft Teams のチャットで web 経由でアクセスできる bot の**メッセージエンドポイント**です。
1. 最後に実行する手順の1つは、展開した bot のメッセージエンドポイントを更新することです。 この例では、bot を Azure に展開しました。 そのため、以下の手順を実行してみましょう。
    1. ブラウザーで[**Azure ポータル**][azure-portal]に移動します。
    1. **Bot チャネル登録**を選択します。
    1. 左側のパネルで、[**設定**] を選択します。
    1. 右側のパネルの [**メッセージングエンドポイント**] ボックスに、ngrok URL (この例では) を入力し `https://dea822bf.ngrok.io/api/messages` ます。
1. Visual Studio デバッグモードなどで、ボットをローカルに起動します。
1. Bot フレームワークポータルの**テスト Web チャット**を使用して、ローカルで実行中に bot をテストします。 エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスすることはできません。
1. が実行されているターミナルウィンドウで、 `ngrok` ボットと web チャットクライアント間の HTTP トラフィックを確認できます。 より詳細な表示が必要な場合は、ブラウザーウィンドウで `http://127.0.0.1:4040` 以前のターミナルウィンドウから取得した情報を入力します。 次の画像は例です。

    ![auth bot teams ngrok テスト](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png).

> [!NOTE]
> Ngrok を停止してから再起動すると、URL が変更されます。 プロジェクトで ngrok を使用し、使用している機能に応じて、すべての URL 参照を更新する必要があります。

## <a name="additional-information"></a>追加情報

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest

このマニフェストには、Microsoft Teams が bot と接続するために必要な情報が含まれています。  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

認証を使用すると、以下に説明するように、Teams は他のチャネルとはやや異なる方法で動作します。

### <a name="handling-invoke-activity"></a>呼び出しアクティビティの処理

**呼び出しアクティビティ**は、他のチャネルによって使用されるイベントアクティビティではなく bot に送信されます。
これは、 **Activityhandler**のサブクラスによって実行されます。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**ボット/の bot**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**ボット/TeamsBot**

**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a>TeamsActivityHandler.cs

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[JavaScript](#tab/node-js-dialog-sample)

**bot/のボット**

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

**ボット/teamsBot**

**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**ダイアログ/mainDialog .js**

ダイアログステップで、を使用し `beginDialog` て OAuth プロンプトを開始します。これにより、ユーザーにサインインするように求められます。

- ユーザーが既にサインインしている場合は、ユーザーに確認を求めることなく、トークン応答イベントが生成されます。
- それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。 Azure Bot サービスは、ユーザーがサインインしようとした後に、トークン応答イベントを送信します。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

次のダイアログステップでは、前の手順の結果にトークンが存在するかどうかを確認します。 Null でない場合、ユーザーは正常にサインインしています。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**ボット/logoutDialog .js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**ボット/dialog_bot py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**ボット/teams_bot py**

**Oauthprompt**を使用している場合は、ダイアログに*呼び出しアクティビティ*を転送する必要があります。

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**ダイアログ/main_dialog py**

ダイアログステップで、を使用し `begin_dialog` て OAuth プロンプトを開始します。これにより、ユーザーにサインインするように求められます。

- ユーザーが既にサインインしている場合は、ユーザーに確認を求めることなく、トークン応答イベントが生成されます。
- それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。 Azure Bot サービスは、ユーザーがサインインしようとした後に、トークン応答イベントを送信します。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

次のダイアログステップでは、前の手順の結果にトークンが存在するかどうかを確認します。 Null でない場合、ユーザーは正常にサインインしています。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**ダイアログ/logout_dialog py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [Azure Bot サービスによる追加認証の追加について説明します。](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
