---
title: Teams ボットに認証を追加する
author: surbhigupta
description: Azure AD を使用して Teams のボット アプリに対してサード パーティの OAuth プロバイダーを使用して認証を有効にする方法について説明します。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: db760f81195634431fe0d3415b1a9c3797b519e7
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376635"
---
# <a name="add-authentication-to-your-teams-bot"></a>Teams ボットに認証を追加する

メール サービスなど、ユーザーの代わりにリソースにアクセスできるボットを Microsoft Teams で作成しなければならない場合があります。

この記事では、OAuth 2.0 に基づいて Azure Bot Service v4 SDK 認証を使用する方法を示します。 これにより、ユーザーの資格情報に基づいて認証トークンを使用できるボットを簡単に開発できます。 このすべてのキーは、後で説明するように **ID プロバイダー** の使用です。

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 の基本的な解釈は、Teams で認証を操作するための前提条件です。

基本的な理解については、[OAuth 2 Simplified](https://aka.ms/oauth2-simplified)を参照してください。完全な仕様については、[OAuth 2.0](https://oauth.net/2/) を参照してください。

Azure Bot Service による認証の処理方法の詳細については、「[会話内のユーザー認証](https://aka.ms/azure-bot-authentication)」を参照してください。

この記事では、以下について説明します。

- **認証が有効なボットを作成する方法**。 ユーザーのサインイン資格情報と認証トークンの生成を処理するには、[cs-auth-sample][teams-auth-bot-cs] を使用します。
- **ボットを Azure にデプロイして ID プロバイダーに関連付ける方法**。 プロバイダーは、ユーザーのサインイン資格情報に基づいてトークンを発行します。 ボットはトークンを使用して、認証を必要とするメール サービスなどのリソースにアクセスできます。 詳細については、  [ボットの Microsoft Teams 認証フローに関するページを](auth-flow-bot.md)参照してください。
- **How to integrate the bot within Microsoft Teams**. Once the bot has been integrated, you can sign in and exchange messages with it in a chat.

## <a name="prerequisites"></a>前提条件

- [ボットの基礎][concept-basics]、[管理状態][concept-state]、[ダイアログ ライブラリ][concept-dialogs]、および[シーケンシャル会話フローを実装する方法][simple-dialog]について説明します。
- Azure と OAuth 2.0 の開発に関する知識。
- Microsoft Visual Studio と Git の現在のバージョン。
- Azure account. If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).
- 次のサンプル:

    | サンプル | BotBuilder のバージョン | デモ |
    |:---|:---:|:---|
    | [cs-auth-sample][teams-auth-bot-cs] での **ボット認証** | v4_4 | OAuthCard のサポート |
    | [js-auth-sample][teams-auth-bot-js] での **ボット認証** | v4_4| OAuthCard のサポート  |
    | [py-auth-sample][teams-auth-bot-py] での **ボット認証** | v4_4 | OAuthCard のサポート |

## <a name="create-the-resource-group"></a>リソース グループを作成する

リソース グループとサービス プランは厳密には必要ありませんが、作成したリソースを簡単に解放できます。 これは、リソースを整理して管理しやすいものにするための良い実践方法です。

リソース グループを使用して、Bot Framework の個々のリソースを作成します。 パフォーマンスを確保するために、これらのリソースが同じ Azure リージョンにあることを確認します。

1. ブラウザーで、[**Microsoft Azure portal**][azure-portal] にサインインします。
1. 左側のナビゲーション パネルで、**リソース グループ** を選択します。
1. In the upper left of the displayed window, select **Add** tab to create a new resource group. You'll be prompted to provide the following:
    1. **サブスクリプション**。 既存のサブスクリプションを使用します。
    1. **リソース グループ**。 リソース グループの名前を入力します。 たとえば、*TeamsResourceGroup* です。 名前は一意である必要があることに注意してください。
    1. **[リージョン]** ドロップダウン メニューから、*[米国西部]*、またはアプリケーションに近いリージョンを選択します。
    1. **[確認して作成]** ボタンを選択します。 "*検証合格*" バナーが表示されます。
    1. **[作成]** ボタンを選択します。 リソース グループの作成には数分かかる場合があります。

> [!TIP]
> このチュートリアルの後半で作成するリソースと同様に、簡単にアクセスできるようにこのリソース グループをダッシュボードにピン留めすることをお勧めします。 これを行う場合は、ピン アイコン &#128204; を選択します。ダッシュボードの右上にあります。

## <a name="create-the-service-plan"></a>サービス プランを作成する

1. [**Azure portal**][azure-portal] の左側のナビゲーション パネルで、**[リソースの作成]** を選択します。
1. 検索ボックスに、「*App Service Plan*」 と入力します。 検索結果から **App Service Plan** カードを選択します。
1. **[作成]** を選択します。
1. 次の情報を入力するように求められます:
    1. **Subscription**. You can use an existing subscription.
    1. **リソース グループ**。 前に作成したグループを選択します。
    1. **名前**。 サービス プランの名前を入力します。 たとえば、*TeamsServicePlan*。 名前はグループ内で一意である必要があることに注意してください。
    1. **オペレーティング システム**。 *Windows* または該当する OS 選択します。
    1. **リージョン**。 *[米国西部]* またはアプリケーションに近いリージョンを選択します。
    1. **価格レベル**。 *Standard S1* が選択されていることを確認します。 これは既定値である必要があります。
    1. **[確認して作成]** ボタンを選択します。 "*検証合格*" バナーが表示されます。
    1. **[作成]** を選択します。 アプリ サービス プランの作成には数分かかる場合があります。 プランがリソース グループに一覧表示されます。

## <a name="create-azure-bot-resource-registration"></a>Azure Bot リソースの登録を作成する

Azure Bot リソースの登録では、Web サービスがボットとして Bot Framework に登録され、Microsoft アプリ ID とアプリパスワード (クライアント シークレット) が提供されます。

> [!IMPORTANT]
> ボットが Azure でホストされていない場合にのみ、ボットを登録する必要があります。 Azure portal を介して[ボットを作成した](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true)場合は、サービスに既に登録されています。 [Bot Framework](https://dev.botframework.com/bots/new) または[開発者ポータル](../../../concepts/build-and-test/teams-developer-portal.md)を通じてボットを作成した場合、ボットは Azure に登録されていません。

1. [**Azure porta**][azure-portal] にアクセスし、**[リソースの作成]** セクションで **Azure Bot** を検索します。
1. **Azure Bot** を開き **[作成]** を選択します。
1. **[ボット ハンドル]** フィールドでボット ハンドル名を入力します。
1. ドロップダウン リストから **[サブスクリプション]** を選択します。
1. ドロップダウン リストから **[リソース グループ]** を選択します。
1. **Microsoft アプリ ID** の **マルチテナント** として **アプリ種類** を選択します。

   :::image type="content" source="../../../assets/images/adaptive-cards/multi-tenant.png" alt-text="このスクリーンショットは、Microsoft AppID のマルチテナントを選択する方法を示しています。":::

1. **[確認 + 作成]** を選びます。

   :::image type="content" source="../../../assets/images/adaptive-cards/create-azure-bot.png" alt-text="このスクリーンショットは、Azure ボットを作成する方法を示しています。":::

1. 検証に合格した場合は、**[作成]** を選択します。

    ボット サービスがプロビジョニングされるまで少し時間がかかります。

   :::image type="content" source="../../../assets/images/adaptive-cards/validation-pane.png" alt-text="このスクリーンショットは、Azure ボットの検証がどのように渡されるかを示しています。":::

1. [**リソースに移動**] を選びます。 ボットと関連リソースがリソース グループに一覧表示されます。

   :::image type="content" source="../../../assets/images/adaptive-cards/go-to-resource-card.png" alt-text="このスクリーンショットは、リソース グループを選択する方法を示しています。":::

    これで、Azure ボットが作成されます。

   :::image type="content" source="../../../assets/images/adaptive-cards/azure-bot-ui.png" alt-text="このスクリーンショットは、Azure ボット リソースを作成する方法を示しています。":::

クライアント シークレットを作成するには:

1. **[構成設定]** で、**[追加]** を選択します。 将来の参照のために、**Microsoft アプリ ID** (クライアント ID) を保存します。

   :::image type="content" source="../../../assets/images/adaptive-cards/config-microsoft-app-id.png" alt-text="このスクリーンショットは、クライアント シークレットを作成するために Microsoft App ID を追加する方法を示しています。":::

1. **Microsoft アプリ ID** の横にある [**管理**] を選択します。

   :::image type="content" source="~/assets/images/manage-bot-label.png" alt-text="このスクリーンショットは、ボットの管理を作成する方法を示しています。":::

1. **[クライアント シークレット]** セクションで、**[新しいクライアント シークレット]** を選択します。**[クライアント シークレットの追加]** ウィンドウが表示されます。

   :::image type="content" source="../../../assets/images/meetings-side-panel/newclientsecret.PNG" alt-text="このスクリーンショットは、新しいクライアント シークレットを作成する方法を示しています。":::

1. **[説明]** を入力し、**[追加]** を選択します。

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="スクリーンショットは、クライアント シークレットの説明を入力する方法を示しています。":::

1. **[値]** の列で、**[クリップボードにコピー]** を選択し、将来参照できるようにクライアント シークレット ID を保存します。

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret-value.png" alt-text="スクリーンショットは、今後の参照のためにクライアント シークレット ID を保存する方法を示しています。":::

Microsoft Teams チャネルに追加するには:

1. **[ホーム]** に移動します。

   :::image type="content" source="../../../assets/images/adaptive-cards/bot-home-page.png" alt-text="このスクリーンショットは、ボットのホーム ページを示しています。":::

1. **[最近使ったリソース]** セクションに一覧表示されているボット開きます。

1. 左側のウィンドウで **[チャネル]** を選択し、**Microsoft Teams**:::image type="icon" source="../../../assets/icons/teams-icon.png":::を選択します。

   :::image type="content" source="../../../assets/images/adaptive-cards/channel-teams.png" alt-text="このスクリーンショットは、チャネルで Teams を選択する方法を示しています。":::

1. サービス利用規約に同意するチェック ボックスをオンにし、**[承諾する]** を選択します。</br>

   :::image type="content" source="../../../assets/images/adaptive-cards/select-terms-of-service.png" alt-text="このスクリーンショットは、サービスの場合に用語を設定する方法を示しています。":::

1. **[保存]** を選択します。

   :::image type="content" source="../../../assets/images/adaptive-cards/select-teams.png" alt-text="このスクリーンショットは、Microsoft Teams チャネルを追加する方法を示しています。":::

詳細については、「[Microsoft Teams 用にボットを作成する](../create-a-bot-for-teams.md)」を参照してください。

## <a name="create-the-identity-provider"></a>ID プロバイダーの作成

認証に使用できる ID プロバイダーが必要です。
この手順では、Azure AD プロバイダーを使用します。他の Azure AD でサポートされている ID プロバイダーも使用できます。

1. [**Azure portal**][azure-portal] の左側のナビゲーション ウィンドウで **[Azure Active Directory]** をクリックします。
    > [!TIP]
    > この Azure AD リソースを作成して、アプリケーションによって要求されたアクセス許可を委任することに同意できるテナントに登録する必要があります。
    > テナントの作成手順については、「[ポータルにアクセスし、テナントを作成する](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)」を参照してください。
1. 左側のパネルで、**[アプリの登録]** を選択します。
1. 右側のパネルで、左上の **[新規登録]** タブを選択します。
1. 次の情報を入力するように求められます:
   1. **名前**。 アプリケーションの名前を入力します。 たとえば *BotTeamsIdentity* などです。 名前は一意である必要があることに注意してください。
   1. アプリケーションに **サポートされているアカウント** の種類を選択します。 *任意の組織ディレクトリ (任意のMicrosoft Azure Active Directory (Azure AD) - マルチテナント) および個人用 Microsoft アカウント (Skype、Xbox など) で [アカウント*] を選択します。
   1. **[リダイレクト URI]** の場合:<br/>
       &#x2713;Select **Web**. <br/>
       &#x2713; `https://token.botframework.com/.auth/web/redirect` に URL を設定します。
   1. **[登録]** を選択します。

1. 作成されると、Azure にアプリの **[概要** ] ページが表示されます。 次の情報をコピーしてファイルに保存します。

    1. The **Application (client) ID** value. You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.
    1. The **Directory (tenant) ID** value. You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.

1. 左側のパネルで **[証明書とシークレット]** を選択して、アプリケーションのクライアント シークレットを作成します。

   1. **[クライアント シークレット]** で、[&#x2795; **新しいクライアント シークレット]** を選択します。
   1. *Teams のボット ID アプリ* など、このアプリ用に作成する必要がある可能性がある他のユーザーからこのシークレットを識別する説明を追加します。
   1. **[期限切れ]** を選択に設定します。
   1. **[追加]** を選択します。
   1. Before leaving this page, **record the secret**. You'll use this value later as the *Client secret* when you register your Azure AD application with your bot.

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>ID プロバイダー接続を構成し、ボットに登録する

ここでサービス プロバイダーには、Azure AD V1 と Azure AD V2 の 2 つのオプションがあります。  2 つのプロバイダー間の違いは、[こちら](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)にまとめられていますが、一般に、V2 はボットのアクセス許可の変更に関してより柔軟です。  Graph API アクセス許可がスコープ フィールドに一覧表示され、新しいアクセス許可が追加されると、ボットによって、ユーザーは次回のサインイン時に新しいアクセス許可に同意できるようになります。  V1 の場合、OAuth ダイアログで新しいアクセス許可を要求するには、ユーザーがボットの同意を削除する必要があります。

#### <a name="microsoft-azure-active-directory-azure-ad-v1"></a>Microsoft Azure Active Directory (Azure AD) V1

1. [**Azure portal**][azure-portal] で、ダッシュボードからリソース グループを選択します。
1. ボット登録リンクを選択します。
1. リソース ページを開き、**[設定]** の下にある **[構成]** を選択します。
1. **[OAuth 接続設定の追加]** を選択します。
   次の図は、リソース ページの対応する選択を示しています。

   ![SampleAppDemoBot 構成](~/assets/images/authentication/sample-app-demo-bot-configuration.png)

1. フォームに次のように入力します。

    1. **名前**。 接続の名前を入力します。 この名前は、`appsettings.json` ファイルのボットで使用します。 たとえば、 *BotTeamsAuthADv1* です。
    1. **サービス プロバイダー**。 **[Microsoft Azure Active Directory (Azure AD)]** を選択します。 これを選択すると、Azure AD 固有のフィールドが表示されます。
    1. **クライアント ID**。上記の手順で、Azure ID プロバイダー アプリ用に記録したアプリケーション (クライアント) ID を入力します。
    1. **クライアント シークレット**。 上記の手順で、Azure ID プロバイダー アプリ用に記録したシークレットを入力します。
    1. **許可の種類**。 `authorization_code` を入力します。
    1. **ログイン URL**。 `https://login.microsoftonline.com` を入力します。
    1. **テナント ID**、ID プロバイダー アプリの作成時に選択したサポートされているアカウントの種類に応じて、先ほど Azure ID アプリ用に記録した **ディレクトリ (テナント) ID** を入力するか、**common** を入力します。 割り当てる値を決定するには、次の条件に従います。

        - *この組織ディレクトリ内のアカウントのみ (Microsoft のみ - シングル テナント)* または *任意の組織ディレクトリのアカウント (Microsoft Azure Active Directory (Azure AD) - マルチテナント)* を選択した場合は、前にMicrosoft Azure Active Directory (Azure) に記録した **テナント ID を** 入力します。AD) アプリ。 これは、認証できるユーザーに関連付けられているテナントになります。

        - *任意の組織のディレクトリで [アカウント] を選択した場合 ([任意のMicrosoft Azure Active Directory (Azure AD) - マルチテナントアカウントと個人用 Microsoft アカウント(Skype、Xbox、Outlook など)) は、* テナント ID の代わりに **共通** という単語を入力します。 それ以外の場合、Azure AD (Azure AD) アプリは、ID が選択されたテナントを介して検証し、個人用 Microsoft アカウントを除外します。

    h. **リソース URL** には、「`https://graph.microsoft.com/`」と入力します。 これは、現在のコード サンプルでは使用されません。  
    i. **[Scopes]** は空白のままにします。 次の図に例を示します。

    :::image type="content" source="../../../assets/images/authentication/auth-bot-identity-connection-adv1.PNG" alt-text="このスクリーンショットは、Teams ボット認証ボット ID 接続 adv1 を追加する方法を示しています。":::

1. **[保存]** を選択します。

#### <a name="microsoft-azure-active-directory-azure-ad-v2"></a>Microsoft Azure Active Directory (Azure AD) V2

1. [**Azure portal**][azure-portal] で、ダッシュボードから Azure Bot を選択します。
1. リソース ページで、**[設定]** にある **[構成]** を選択します。
1. **[OAuth 接続設定の追加]** を選択します。  
   次の図は、リソース ページの対応する選択を示しています。

   :::image type="content" source="../../../assets/images/authentication/sample-app-demo-bot-configuration.png" alt-text="このスクリーンショットは、リソース ページで対応する選択内容を示しています。":::

1. フォームに次のように入力します。

    1. **名前**。 接続の名前を入力します。 この名前は、`appsettings.json` ファイルのボットで使用します。 たとえば、 *BotTeamsAuthADv2* です。
    1. **サービス プロバイダー**。 **[Microsoft Azure Active Directory v2]** を選択します。 これを選択すると、Azure AD 固有のフィールドが表示されます。
    1. **クライアント ID**。上記の手順で、Azure ID プロバイダー アプリ用に記録したアプリケーション (クライアント) ID を入力します。
    1. **クライアント シークレット**。 上記の手順で、Azure ID プロバイダー アプリ用に記録したシークレットを入力します。
    1. **トークン交換 URL**。 空白のままにします。
    1. **テナント ID**、ID プロバイダー アプリの作成時に選択したサポートされているアカウントの種類に応じて、先ほど Azure ID アプリ用に記録した **ディレクトリ (テナント) ID** を入力するか、**common** を入力します。 割り当てる値を決定するには、次の条件に従います。

        - *この組織ディレクトリ内のアカウントのみ (Microsoft のみ - シングル テナント)* または *任意の組織ディレクトリのアカウント (Microsoft Azure Active directory - マルチテナント)* を選択した場合は、Azure AD アプリ用に前に記録した **テナント ID を** 入力します。 これは、認証できるユーザーに関連付けられているテナントになります。

        - *任意の組織のディレクトリで [アカウント] を選択した場合 ([任意のMicrosoft Azure Active Directory (Azure AD) - マルチテナントアカウントと個人用 Microsoft アカウント(Skype、Xbox、Outlook など)) は、* テナント ID の代わりに **共通** という単語を入力します。 それ以外の場合、Azure AD アプリは、ID が選択されたテナントを介して検証し、個人用 Microsoft アカウントを除外します。

    1. **スコープの** 場合は、このアプリケーションが必要とするグラフのアクセス許可のスペース区切りの一覧を入力します。User.Read User.ReadBasic.All Mail.Read

1. **[保存]** を選択します。

### <a name="test-the-connection"></a>接続をテストします。

1. 接続エントリを選択して、作成した接続を開きます。
1. **[サービス プロバイダー接続設定]** パネルの上部になる **[テスト接続]** を選択します。
1. The first time you do this will open a new browser window asking you to select an account. Select the one you want to use.
1. 次に、ID プロバイダーにデータ (資格情報) の使用を許可するように求められます。 次の図に例を示します。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-accept.PNG" alt-text="スクリーンショットは、Teams ボット認証接続文字列 adv1 を追加する方法を示しています。":::

1. **[同意する]** を選択します。
1. これにより、**[テスト接続] から \<your-connection-name> [成功]** ページにリダイレクトされます。 エラーが発生した場合は、ページを更新します。 次の図に例を示します。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-token.PNG" alt-text="スクリーンショットは、Teams アプリ認証接続文字列 adv1 を追加する方法を示しています。":::

接続名は、ユーザー認証トークンを取得するためにボット コードによって使用されます。

## <a name="prepare-the-bot-sample-code"></a>ボットのサンプル コードを準備する

準備の設定が完了したら、この記事で使用するボットの作成に焦点を当ててみましょう。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. [cs-auth-sample][teams-auth-bot-cs] を複製します。
1. Visual Studio を起動します。
1. ツール バーから [ **ファイル] -> [Open -> Project/Solution** ] を選択し、ボット プロジェクトを開きます。
1. C# では、 **appsettings.json** を次のように更新します。

    - `ConnectionName` を、ボット登録に追加した ID プロバイダー接続の名前に設定します。 この例で使用した名前は、*BotTeamsAuthADv1* です。
    - `MicrosoftAppId` をボット登録時に保存した **ボット アプリ ID** に設定します。
    - ボットの登録時に保存した **カスタマー シークレット** を `MicrosoftAppPassword` に設定します。

    ボット シークレットの文字によっては、パスワードの XML エスケープが必要になる場合があります。 たとえば、アンパサンド (&) はすべて、`&amp;` としてエンコードする必要があります。

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. ソリューション エクスプローラーで、フォルダーに`TeamsAppManifest`移動し、ボットの登録時に保存した **ボット アプリ ID を** 開`manifest.json`いて設定`id``botId`します。

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. [node-auth-sample][teams-auth-bot-js] を複製します。
1. コンソールで、プロジェクトに移動します。 </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. モジュールのインストール</br></br>
`npm install`
1. 次のように **.env** 構成を更新します:

    - `MicrosoftAppId` をボット登録時に保存した **ボット アプリ ID** に設定します。
    - ボットの登録時に保存した **カスタマー シークレット** を `MicrosoftAppPassword` に設定します。
    - `connectionName` を ID プロバイダー接続の名前に設定します。
    ボット シークレットの文字によっては、パスワードの XML エスケープが必要になる場合があります。 たとえば、アンパサンド (&) はすべて、`&amp;` としてエンコードする必要があります。

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. `teamsAppManifest` フォルダーで、`manifest.json` を開き `id` を **Microsoft App ID** に、`botId` をボット登録時に保存しておいた **ボット アプリ ID** に設定します。

# <a name="python"></a>[Python](#tab/python)

1. Github リポジトリから [py-auth-sample][teams-auth-bot-py] を複製します。
1. **config.py** を更新します:

    - `ConnectionName` を、ボットに追加した OAuth 接続設定の名前に設定します。
    - `MicrosoftAppId` と `MicrosoftAppPassword` をボットのアプリ ID とアプリ シークレットに設定します。

      ボット シークレットの文字によっては、パスワードの XML エスケープが必要になる場合があります。 たとえば、アンパサンド (&) はすべて、`&amp;` としてエンコードする必要があります。

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>ボットを Azure にデプロイする

ボットをデプロイするには、「 [Azure にボットをデプロイ](https://aka.ms/azure-bot-deployment-cli)する方法」の手順に従います。

または、Visual Studio の場合は、次の手順を実行できます:

1. Visual Studio *ソリューション エクスプローラー* で、プロジェクト名を選択して保持 (または右クリック) します。
1. ドロップダウン メニューで、**[公開]** を選択します。
1. 表示されたウィンドウで、**[新規]** リンクを選択します。
1. ダイアログ ウィンドウで、左側にある **アプリ サービス]** と右側にある **[新規作成]** を選択します。
1. **[公開]** ボタンをクリックします。
1. 次のダイアログ ウィンドウで、必要な情報を入力します。 例を次に示します。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service.png" alt-text="このスクリーンショットは、認証アプリ サービスに必要な情報を入力する方法を示しています。":::

1. **[作成]** を選択します。
1. デプロイが正常に完了すると、Visual Studio に反映されます。 さらに、既定のブラウザーに、"*ボットの準備ができました!*" というページが表示されます。 URL は次のようになります: `https://botteamsauth.azurewebsites.net/`。 ファイルに保存します。
1. ブラウザーで [**、Azure portal**][azure-portal]に移動します。
1. リソース グループを確認します。ボットは他のリソースと共に一覧表示されます。 次の図に例を示します。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service-in-group.png" alt-text="このスクリーンショットは、リソース グループとボットを確認する方法を示しています。":::

1. リソース グループで、ボット登録名 (リンク) を選択します。
1. 左側のウィンドウで **[設定]** を選択します。
1. **[メッセージング エンドポイント]** ボックスに、上記で取得した URL に続いて `api/messages` を入力します。 これは例です: `https://botteamsauth.azurewebsites.net/api/messages`。
    > [!NOTE]
    > 1 つのボットに対して許可されるメッセージング エンドポイントは 1 つだけです。
1. 左上の **[保存]** ボタンを選択します。

## <a name="test-the-bot-using-the-emulator"></a>エミュレーターを使用してボットをテストする

まだ実行していない場合は、[Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme) をインストールします。 「[エミュレーターを使用したデバッグ](https://aka.ms/bot-framework-emulator-debug-with-emulator)」も参照してください。

ボットのサンプル ログインを機能させるには、エミュレーターを構成する必要があります。

### <a name="configure-the-emulator-for-authentication"></a>認証用にエミュレーターを構成する

If a bot requires authentication, you must configure the Emulator. To configure:

1. エミュレーターを起動します。
1. エミュレーターで、左下にある歯車アイコン &#9881; を選択するか、右上の **[エミュレーターの設定]** タブを選択します。
1. **[バージョン 1.0 認証トークンを使用]** のチェック ボックスをオンにします。
1. **ngrok** ツールへのローカル パスを入力します。 「*Bot Framework Emulator/ngrok トンネリング統合*」の [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)) を参照してください。 ツールの詳細については、[ngrok](https://ngrok.com/) を参照してください。
1. **[エミュレーターの起動時に ngrok を実行]** チェック ボックスをオンにします。
1. [**保存**] ボタンを選択します。

ボットにサインイン カードが表示され、ユーザーがサインイン ボタンを選択すると、エミュレーターによって、ユーザーが認証プロバイダーでサインインするために使用できるページが開きます。
ユーザーが個の操作を行うと、プロバイダーによってユーザー トークンが生成され、ボットに送信されます。 その後、ユーザーの代わりにボットが動作できるようになります。

### <a name="test-the-bot-locally"></a>ボットをローカルでテストする

認証メカニズムを構成したら、実際のボット テストを実行できます。  

1. たとえば、Visual Studio を使用して、お使いのコンピューターでボット サンプルをローカルで実行します。
1. エミュレーターを起動します。
1. **[ボットを開く]** ボタンを選択します。
1. In the **Bot URL**, enter the bot's local URL. Usually, `http://localhost:3978/api/messages`.
1. **[Microsoft アプリ ID]** に `appsettings.json` からのボットのアプリ ID を入力します。
1. **[Microsoft アプリ パスワード]** に `appsettings.json` からボットのアプリ パスワードを入力します。
1. **[接続]** を選択します。
1. ボットが起動して実行されたら、任意のテキストを入力してサインイン カードを表示します。
1. **[サインイン]** ボタンを選択します。
1. **開かれた URL の確認** 用にポップアップ ダイアログが表示されます。 これは、ボットのユーザー (自分) を認証できるようにするためです。  
1. **[確認]** を選択します。
1. メッセージが表示されたら、該当するユーザーのアカウントを選択します。
1. エミュレーターに使用した構成に応じて、次のいずれかを取得します:
    1. **サインイン確認コードの使用**  
      &#x2713; 検証コードを表示するウィンドウが開かれます。  
      &#x2713; 検証コードをコピーしてチャット ボックスに入力してサインインを完了します。
    1. **認証トークンの使用**。  
      &#x2713; 資格情報に基づいてログインしています。

    次の図は、ログイン後のボット UI の例です。

    :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator.PNG" alt-text="このスクリーンショットは、ログインした後のボット UI の例を示しています。":::

1. ボットから *トークンの表示* を求められたときに **[はい**] を選択すると、次のような応答が返されます。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator-token.png" alt-text="このスクリーンショットは、同意を選択する方法を示しています。":::

1. サインアウトするには、入力チャット ボックスに「**logout**」と入力します。これによりユーザー トークンが解放され、もう一度サインインするまでボットはユーザーの代理として動作できなくなります。

> [!NOTE]
> ボット認証には、**Bot Connector Service** を使用する必要があります。 このサービスは、ボットのボット登録情報にアクセスします。

## <a name="test-the-deployed-bot"></a>デプロイされたボットをテストする

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. ブラウザーで [**、Azure portal**][azure-portal]に移動します。
1. リソース グループを見つけます。
1. リソース リンクを選択します。 リソース ページが表示されます。
1. リソース ページで、**[Web チャットでテスト]** を選択します。 ボットが起動し、事前定義された案内応答が表示されます。
1. チャット ボックスに何かを入力します。
1. **[サインイン]** ボックスを選択します。
1. **開かれた URL の確認** 用にポップアップ ダイアログが表示されます。 これは、ボットのユーザー (自分) を認証できるようにするためです。  
1. **[確認]** を選択します。
1. メッセージが表示されたら、該当するユーザーのアカウントを選択します。
    次の図は、ログイン後のボット UI の例です。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed.PNG" alt-text="このスクリーンショットは、ログインした後の Teams ボット UI の例を示しています。":::

1. **[はい]** ボタンを選択して、認証トークンを表示します。 次の図に例を示します。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed-token.PNG" alt-text="このスクリーンショットは、[はい] ボタンを選択して認証トークンを表示する方法を示しています。":::

1. 「ログアウト」と入力してサインアウトします。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-deployed-logout.PNG" alt-text="このスクリーンショットは、ログアウトを入力してサインアウトする方法を示しています。":::

> [!NOTE]
> サインインで問題が発生した場合は、前の手順で説明したように、接続を再度テストしてみてください。 これにより、認証トークンが再作成される可能性があります。
> Azure の Bot Framework Web チャット クライアントでは、認証が正しく確立される前に、何度かサインインする必要がある場合があります。

## <a name="install-and-test-the-bot-in-teams"></a>Teams でボットをインストールしてテストする

1. ボット プロジェクトで、`TeamsAppManifest` フォルダーに `manifest.json` が、`outline.png` および `color.png` と共に含まれていることを確認します。
1. ソリューション エクスプローラーで、フォルダーに`TeamsAppManifest`移動します。 次の値を割り当てて、`manifest.json` を編集します:
    1. ボットの登録時に受け取った **ボット アプリ ID** が `id` と `botId` に割り当てられていることを確認します。
    1. この値を割り当てます: `validDomains: [ "token.botframework.com" ]`。
1. `manifest.json`、`outline.png`、および `color.png` ファイルを選択して **zip** します。
1. **Microsoft Teams** を開きます。
1. 左側のパネルの下部で、**Apps アイコン** を選択します。
1. 右側のパネルの下部にある **[カスタム アプリのアップロード]** を選択します。
1. フォルダーに `TeamsAppManifest` 移動し、zip 形式のマニフェストをアップロードします。
次のウィザードが表示されます。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-upload.png" alt-text="このスクリーンショットは、Teams にアップロードされたボットの例を示しています。":::

1. **[チームに追加]** ボタンを選択します。
1. 次のウィンドウで、ボットを使用するチームを選択します。
1. **[ボットの設定]** ボタンを選択します。
1. 左のパネルにある 3 つのドット (&#x25cf;&#x25cf;&#x25cf;) を選択します。 次に、 **開発者ポータル** アイコンを選択します。
1. **[マニフェスト エディター]** タブを選択します。アップロードしたボットのアイコンが表示されます。
1. また、ボットとメッセージを交換するために使用できるボットをチャットリストに連絡先として表示できます。

### <a name="testing-the-bot-locally-in-teams"></a>Teams でボットをローカルでテストする

Teams は完全にクラウドベースの製品であり、アクセスするすべてのサービスを HTTPS エンドポイントを使用してクラウドから利用できるようにする必要があります。 そのため、ボット (サンプル) を Teams で動作させるには、任意のクラウドにコードを発行するか、**トンネリング** ツールを使用してローカルで実行されているインスタンスに外部からアクセスできるようにする必要があります。 [ngrok](https://ngrok.com/download) を使用することをお勧めします。これにより、コンピューターでローカルに開くポートの外部アドレス指定可能な URL が作成されます。
Teams アプリをローカルで実行するための準備として ngrok を設定するには、次の手順に従います。

1. ターミナル ウィンドウで、`ngrok.exe` がインストールされているディレクトリに移動します。 *環境変数* パスをポイントするように設定することをお勧めします。
1. たとえば、`ngrok http 3978 --host-header=localhost:3978` を実行します。 必要に応じてポート番号を置き換えます。
これにより、ngrok が起動し、指定したポートでリッスンします。 その返しとして、ngrok が実行されている限り有効な外部アドレス指定可能な URL が提供されます。 次の図に例を示します。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-ngrok-start.PNG" alt-text="このスクリーンショットは、Teams ボット アプリ認証接続文字列 adv1 を示しています":::

1. 転送先の HTTPS アドレスをコピーします。 次のようになるはずです: `https://dea822bf.ngrok.io/`。
1. `/api/messages` を追加して、`https://dea822bf.ngrok.io/api/messages` を取得します。 これは、コンピューター上でローカルで実行され、Teams のチャットで Web 経由で到達可能なボットの **メッセージ エンドポイント** です。
1. 実行する最後の手順の 1 つは、デプロイされたボットのメッセージ エンドポイントを更新することです。 この例では、ボットを Azure にデプロイしました。 それでは、次の手順を実行しましょう:
    1. ブラウザーで [**、Azure portal**][azure-portal]に移動します。
    1. **[ボットの登録]** を選択します。
    1. 左側のウィンドウで **[設定]** を選択します。
    1. 右側のパネルの **[メッセージング エンドポイント]** ボックスに、ngrok URL を入力します(例: `https://dea822bf.ngrok.io/api/messages`)。
1. ボットをローカルで起動します (Visual Studioデバッグ モードなど)。
1. Bot Framework ポータルの **[Web チャットのテスト]** を使用して、ローカルでの実行中にボットをテストします。 エミュレーターと同様に、このテストでは Teams 固有の機能にアクセスすることはできません。
1. `ngrok` が実行されているターミナル ウィンドウでは、ボットと Web チャット クライアントの間の HTTP トラフィックを確認できます。 より詳細なビューが必要な場合は、ブラウザー ウィンドウで、前のターミナル ウィンドウから取得した `http://127.0.0.1:4040` を入力します。 次の図に例を示します。

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png" alt-text="このスクリーンショットは、認証ボット チームの ngrok テストを示しています。":::

> [!NOTE]
> ngrok を停止して再起動すると、URL が変更されます。 プロジェクトで ngrok を使用するには、また使用している機能に応じて、すべての URL 参照を更新する必要があります。

## <a name="additional-information"></a>その他の情報

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest.json

このマニフェストには、Teams がボットに接続するために必要な情報が含まれています。  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
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

認証では、以下で説明するように、Teams の動作は他のチャネルと若干異なります。

### <a name="handling-invoke-activity"></a>呼び出しアクティビティの処理

An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.
This is done by sub-classing the **ActivityHandler**.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bots/DialogBot.cs**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bots/TeamsBot.cs**

**OAuthPrompt** を使用する場合は、*呼び出しアクティビティ* をダイアログに転送する必要があります。

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

**bots/dialogBot.js**

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

**bots/teamsBot.js**

**OAuthPrompt** を使用する場合は、*呼び出しアクティビティ* をダイアログに転送する必要があります。

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**dialogs/mainDialog.js**

ダイアログ手順内で、`beginDialog` を使用して OAuth プロンプトを開始します。これにより、ユーザーにサインインを求められます。

- ユーザーが既にサインインしている場合は、ユーザーにメッセージを表示せずにトークン応答イベントが生成されます。
- それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。 Azure Bot Service は、ユーザーがサインインを試みた後にトークン応答イベントを送信します。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

次のダイアログ ステップで、前の手順の結果にトークンが存在するかどうかを確認します。 null でない場合、ユーザーは正常にサインインします。

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bots/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bots/dialog_bot.py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bots/teams_bot.py**

**OAuthPrompt** を使用する場合は、*呼び出しアクティビティ* をダイアログに転送する必要があります。

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**dialogs/main_dialog.py**

ダイアログ手順で、`begin_dialog` を使用して OAuth プロンプトを開始します。これにより、ユーザーにサインインを求められます。

- ユーザーが既にサインインしている場合は、ユーザーにメッセージを表示せずにトークン応答イベントが生成されます。
- それ以外の場合は、ユーザーにサインインを求めるメッセージが表示されます。 Azure Bot Service は、ユーザーがサインインを試みた後にトークン応答イベントを送信します。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

次のダイアログ ステップで、前の手順の結果にトークンが存在するかどうかを確認します。 null でない場合、ユーザーは正常にサインインします。

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**dialogs/logout_dialog.py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="code-sample"></a>コード サンプル

このセクションでは、Bot 認証 v3 SDK サンプルを提供します。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| ボット認証 | このサンプルでは、Teams のボットで認証を開始する方法を示します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| タブ、ボット、メッセージ拡張機能 (ME) SSO | このサンプルは、タブ、ボット、および ME の SSO (検索、アクション、linkunfurl) を示しています。 |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 利用不可 |

## <a name="see-also"></a>関連項目

[Azure Bot Service](https://aka.ms/azure-bot-add-authentication) を使用して認証を追加する

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth
