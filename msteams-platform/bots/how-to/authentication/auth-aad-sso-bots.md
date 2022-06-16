---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者は、OAuth カードをサポートするサインイン カードまたは Azure ボット サービスを使用できます。
keywords: トークン、ユーザー トークン、ボット向け SSO サポート、アクセス許可、Microsoft Graph、Azure AD
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: c10fe639417ad71814b060ba70e6a33c4ae4038f
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123469"
---
# <a name="single-sign-on-sso-support-for-bots"></a>ボット向けのシングル サインオン (SSO) サポート

Microsoft Azure Active Directory (Azure AD) のシングル サインオン認証では、ユーザーがサインイン資格情報の入力を必要とする回数を最小限に抑えるために、認証トークンが暗黙裡に更新されます。 ユーザーがアプリの使用に同意した場合、ユーザーは自動的にサインインするため、別のデバイスで再度同意する必要はありません。 タブとボットには、SSO のサポートに関して同様のフローがあります。 ただし、ボットは[トークンを要求](#request-a-bot-token)し、別のプロトコルで[応答](#receive-the-bot-token)を受け取ります。

>[!NOTE]
> OAuth 2.0 は、Azure AD およびその他の多くの ID プロバイダーによって使用される認証と承認のためのオープンな標準です。 OAuth 2.0 の基本的な解釈は、Teams で認証を操作するための前提条件です。

## <a name="bot-sso-at-runtime"></a>ランタイムにおけるボットの SSO

次の図は、ボットにおける SSO のフローを示しています:

![ランタイム ダイアグラムにおけるボットの SSO](../../../assets/images/bots/bots-sso-diagram.png)

次の手順は、認証とボット アプリケーション トークンに役立ちます。

1. ボットは、ボット アプリケーションのための認証トークンを取得するため、`tokenExchangeResource` を含む OAuthCard を使用して Teams にメッセージを送信します。 ユーザーは、アクティブなすべてのユーザー エンドポイントでメッセージを受信します。

   > [!NOTE]
   >
   > * ユーザーは、一度に複数のアクティブなエンドポイントを持つ可能性があります。
   > * ボット トークンは、すべてのアクティブなユーザーのエンドポイントから受信されます。
   > * SSO をサポートするには、アプリを個人用のスコープにインストールする必要があります。

1. 現在のユーザーが初めてボット アプリケーションを使用する場合、ユーザーに次のいずれかの操作を要求するプロンプトが表示されます:
    * 必要に応じて同意をしてください。
    * 2 要素認証などのステップ アップ認証を処理します。

1. Microsoft Teams は、現在のユーザーに Azure AD エンドポイントからのボット アプリケーション トークンを要求します。

1. Azure AD はボット アプリケーション トークンを Microsoft Teams アプリケーションに送信します。

1. Teams は、**サインイン/tokenExchange** の実行に伴って返される値オブジェクトの一部として、トークンをボットに送信します。
  
1. ボット アプリケーションの解析されたトークンは、ユーザーのメール アドレスなど、必要な情報を提供します。
  
## <a name="develop-an-sso-teams-bot"></a>SSO Teams ボットを開発する
  
次の手順では、SSO Teams ボットの開発をガイドします:

1. [Azure AD ポータルを使用してアプリを登録する](#register-your-app-through-the-azure-ad-portal)。
1. [ボットの Teams アプリケーション マニフェストを更新します](#update-your-teams-application-manifest-for-your-bot)。
1. [ボット トークンを要求および受信するコードを追加します](#add-the-code-to-request-and-receive-a-bot-token)。

### <a name="register-your-app-through-the-azure-ad-portal"></a>Azure AD ポータルからアプリを登録する

Azure AD ポータルを使用してアプリを登録する手順は、[タブ向けの SSO フロー](../../../tabs/how-to/authentication/tab-sso-overview.md)に似ています。 以下の手順により、アプリの登録についてガイドします:

1. [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) ポータルで新しいアプリケーションを登録します。

1. **[新規登録]** を選択します。 **[アプリケーション登録]** ページが表示されます。

    ![新規登録](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. **[アプリケーションの登録]** ページで、次の操作を行います:

   > [!NOTE]
   >
   > Azure AD アプリが Teams で認証要求を行うのと同じテナントに登録されている場合、ユーザーは同意を求められず、すぐにアクセス トークンが許可されます。 ただし、Azure AD アプリが別のテナントに登録されている場合、ユーザーはアクセス許可に同意する必要があります。

    * アプリの **名前** を入力します。
    * シングルテナントやマルチテナントなど **サポートされているアカウント タイプ** を選択します。
    * **[登録]** を選択します。

    ![アプリケーションを登録する](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. 概要ページに移動します。
1. **アプリケーション (クライアント) ID** の値をコピーします。
1. **[管理]** 以下で、**[API の露出]** を選択します。

   > [!TIP]
   > 後でアプリ マニフェストを更新するには、**アプリケーション (クライアント) ID** 値を保存します。

   > [!IMPORTANT]
   >
   > * スタンドアロン ボットをビルドする場合は、アプリケーション ID の URI を `api://botid-{YourBotId}` として入力します。 ここで *YourBotId* は Azure AD アプリケーション ID です。
   > * ボットとタブを使用してアプリをビルドしている場合は、アプリケーション ID URI と `api://fully-qualified-domain-name.com/botid-{YourBotId}` に入力します。

1. **[スコープの追加]** を選択します。
1. プロンプトが表示されるパネルで、**スコープ名** として `access_as_user` を入力します。

   >[!NOTE]
   > クライアント アプリの追加に使用される "access_as_user" スコープは、"Administrators and users" 用です。
   >
   > 次の重要な制限に注意する必要があります。
   >
   > * email、profile、offline_access、OpenId などのユーザー レベルの Microsoft Graph API アクセス許可のみがサポートされます。 他の Microsoft Graph スコープ (たとえば`User.Read``Mail.Read`、Microsoft [Graphのアクセス許可とスコープを使用してタブ アプリを拡張](../../../tabs/how-to/authentication/tab-sso-graph-api.md)する) にアクセスする必要がある場合は、「」を参照してください。
   > * アプリケーションのドメイン名は、Azure AD アプリケーションに登録したドメイン名と同じである必要があります。
   > * 現在、アプリごとに複数のドメインはサポートされていません。
   > * `azurewebsites.net` ドメインを使用するアプリケーションは大衆的であり、セキュリティ リスクである可能性があるため、サポートされていません。

1. **誰が同意できますか?** において、**管理者とユーザー** を入力します。
1. 次の詳細を入力して、スコープ `access_as_user` に適した値により管理者とユーザーの同意プロンプトを構成します。
    * **管理者同意表示名**: Teams はユーザー プロファイルにアクセスできます。
    * **管理者の同意説明:** チームは、現在のユーザーとしてアプリの Web API を呼び出すことができます。
    * **ユーザー同意表示名**: Teams は、あなたのプロファイルにアクセスすることができ、あなたの代理として要求を行うことができます。
    * **ユーザーの同意説明**: Teams は、あなたと同じ権限で、このアプリ API を呼び出すことができます。

    ![管理者とユーザー](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. 状態が **有効** に設定されていることを確認します。

    ![状態](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. **[スコープ追加]** を選択して詳細を保存します。表示される **スコープ名** のドメイン部分は、前の手順で設定した **アプリケーション ID** URI と自動的に一致する必要があり、最後の`api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`に`/access_as_user`が追加されます。

1. **[承認済みクライアント アプリケーション]** で、アプリの Web アプリケーションに対して承認するアプリケーションを特定します。
1. **[クライアント アプリケーションの追加]** を選択します。

    ![クライアント アプリケーション](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. 次の各クライアント ID を入力し、前の手順で作成した承認スコープを選択します。
    * Teams モバイル アプリケーションまたはデスクトップ アプリケーション用 `1fec8e78-bce4-4aaf-ab1b-5451cc387264`。
    * Teams Web アプリケーション用 `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`。

    ![クライアント ID](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. **[認証]** に移動します。
1. **[プラットフォームの構成]** で、**[プラットフォームの追加]** を選択します。

    ![platform](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. **[Web]** を選びます。

    ![プラットフォームを構成する](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. アプリの **[リダイレクト URI]** を入力します。

   >[!NOTE]
   > この URI は完全修飾ドメイン名である必要があります。 認証応答が送信される場合には API ルートも続きます。 Teams のサンプルのいずれかをフォローしている場合、URI は `https://token.botframework.com/.auth/web/redirect` です。 詳細については、「[OAuth 2.0 承認コード フロー](/azure/active-directory/develop/v2-oauth2-auth-code-flow)」を参照してください。

    ![リダイレクト URI:](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. 次の手順は、暗黙的な許可を有効にするために役立ちます:
    * 左側のウィンドウで **[認証]** を選択します。
    * **[アクセス トークン]** を選択し、**[ID トークン]** チェックボックスを選択します。

    ![許可フロー](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)

    * **[保存]** を選択し、変更内容を保存します。

1. 必要な **API アクセス許可** を追加します。
    * 左側のウィンドウ **[API アクセス許可]** を選択します。
    * **[プラットフォームの追加]** を選択して、User.Read など、アプリがダウンストリーム API に対して必要とするアクセス許可を追加します。

#### <a name="update-manifest-in-microsoft-azure-portal"></a>Microsoft Azure ポータルでマニフェストを更新する

次の手順では、Azure portal でボット マニフェストを更新する方法について説明します:

1. 左側のウィンドウで **[マニフェスト]** を選択します。
1. 構成項目が次に設定されていることを確認します **"accessTokenAcceptedVersion": 2**。 そうでない場合は、値を **2** に変更します。

    ![マニフェストを更新する](~/assets/images/bots/update-manifest.png)

   >[!NOTE]
   > 既に Teams でボットをテストしている場合は、このアプリからサインアウトし、Teams からサインアウトする必要があります。 その後、もう一度サインインして、この変更を確認します。

1. **[保存]** を選択します。

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>OAuth 接続を使用して Azure portal を更新します

次の手順では、OAuth 接続を使用して Azure portal を更新する方法について説明します:

1. Azure portal で、[**[Azure Bot]**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)に移動します
1. 左側のウィンドウの **[構成]** に移動します。
1. **[OAuth 接続設定の追加]** を選択します。

    ![構成設定](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. 次の手順では、**[新しい接続設定]** フォームの入力をガイドします:

   >[!NOTE]
   > Azure AD アプリケーションでは、**暗黙的な許可** が必要になる場合があります。

    * **[新しい接続設定]** ページで **[名前]** に入力します。

    >[!NOTE]
    > **[名前]** は、ボット サービス コード内の [[ランタイムにおける Bot SSO]](#bot-sso-at-runtime) における *[手順 5]* で参照されます。

    * **[サービス プロバイダー]** ドロップダウンから、**Azure Active Directory v2** を選択します。
    * Azure AD アプリケーションの **クライアント ID** や **クライアント シークレット** などのクライアント資格情報を入力します。
    * **トークンの交換 URL** の場合は、[ボットの Teams アプリケーション マニフェストを更新する](#update-your-teams-application-manifest-for-your-bot) で定義されているスコープ値を使用します。たとえば、`api://botid-<your-app-id>/`です。 トークンの交換 URL は、この Azure AD アプリケーションが SSO 用に構成されていることを SDK に示します。
    * **テナント ID** において、*共通* に入力します。
    * Azure AD アプリケーションのダウンストリーム API にアクセス許可を指定するときに構成された、すべての **スコープ** を追加します。 クライアント ID とクライアント シークレットの提供とともに、トークン ストアは、定義されたアクセス許可を持つグラフ トークンとトークンを交換します。
    * **[保存]** を選択します。
    * **[適用]** を選択します。

    ![接続設定](~/assets/images/authentication/Bot-connection-setting.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>ボットの Teams アプリケーション マニフェストを更新する

アプリケーションにスタンドアロン ボットが含まれている場合は、次のコードを使用して、Teams アプリケーション マニフェストに新しいプロパティを追加します:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```

アプリケーションにボットとタブが含まれている場合は、次のコードを使用して、Teams アプリケーション マニフェストに新しいプロパティを追加します:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** は、次の要素の親です:

* **id** - アプリケーションのクライアント ID。 これは、アプリケーションを Azure AD に登録する際に取得したアプリケーション ID です。 このアプリケーション ID を複数の Teams アプリと共有しないでください。 `webApplicationInfo`を使用するアプリケーション マニフェストごとに新しい Azure AD アプリを作成します。
* **resource** - アプリケーションのドメインとサブドメイン。 これは、[で`scope`を作成するときに登録したプロトコル `api://` を含む、Azure AD ポータル ](#register-your-app-through-the-azure-ad-portal) を使用してアプリを登録する URI と同じです。 リソースにパス `access_as_user` を含めないでください。 この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用されている任意のサブドメインを含むドメインと一致している必要があります。

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>ボット トークンを要求し、受信するコードを追加する

#### <a name="request-a-bot-token"></a>ボット トークンを要求する

アクセス トークンの取得要求は、既存のメッセージ スキーマを使用した通常の HTTP POST メッセージ要求です。 それは、OAuthCard の添付ファイルに含まれています。 OAuthCard クラスのスキーマは、[Microsoft Bot スキーマ 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義されており、サインイン カードに似ています。 プロパティ `TokenExchangeResource` がカードに設定されている場合、Teams はこの要求をサイレント トークンの取得として扱います。 Microsoft Teams チャンネルの場合、トークンの要求を一意に認識するプロパティ `Id` だけが引き受けられます。

>[!NOTE]
> Microsoft Bot Framework `OAuthPrompt` または `MultiProviderAuthDialog` は、SSO 認証でサポートされています。

ユーザーが初めてアプリケーションを使用していて、ユーザーの同意が必要な場合は、次のダイアログ ボックスが表示され、同意エクスペリエンスが続行されます:

![同意ダイアログ ボックス](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

ユーザーが **[続行する]** を選択すると、次のイベントが発生します。

* ボットがサインイン ボタンを定義した場合、ボットのサインイン フローは、メッセージ ストリームの OAuth カード ボタンからのサインイン フローと同じものが適用されます。 開発者は、ユーザーの同意が必要なアクセス許可を決定する必要があります。 `openId`を超えるアクセス許可を持つトークンが必要な場合は、この方法をお勧めします。 たとえば、グラフ リソースのトークンを交換する場合などです。

* ボットが OAuth カードにサインイン ボタンを提供しない場合、一連の最小限のアクセス許可のためにユーザーの同意が必要です。 このトークンは、基本認証とユーザーの電子メール アドレスの取得に役立ちます。

##### <a name="c-token-request-without-a-sign-in-button"></a>サインイン ボタンなしの C# トークン要求

```csharp
    var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

       await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receive-the-bot-token"></a>ボット トークンを受け取る

トークンを使用した応答は、ボットが今日受け取る他の呼び出しアクティビティと同じスキーマを持つ呼び出しアクティビティを介して送信されます。 唯一の違いは呼び出し名、 **サインイン/トークン交換**、および **値** フィールドです。 **値** フィールドには、**ID**、トークンを取得するための最初の要求の文字列、**トークン** フィールド、トークンを含む文字列値が含まれます。

>[!NOTE]
> ユーザーが複数のアクティブなエンドポイントを持っている場合、与えられた要求に対して複数の応答を受け取る場合があります。 トークンを使用して応答の重複を除去する必要があります。

##### <a name="c-code-to-handle-the-invoke-activity"></a>呼び出しアクティビティを処理する C# コード

```csharp
    protected override async Task<InvokeResponse> OnInvokeActivityAsync
    (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                try
                {
                    if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                    {
                        await OnTokenResponseEventAsync(turnContext, cancellationToken);
                        return new InvokeResponse() { Status = 200 };
                    }
                    else
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                    }
                }
                catch (InvokeResponseException e)
                {
                    return e.CreateInvokeResponse();
                }
            }
```

`turnContext.activity.value`は [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) タイプであり、ボットでさらに使用できるトークンが含まれています。 パフォーマンス上の理由からトークンを格納し、更新する必要があります。

### <a name="token-exchange-failure"></a>トークン交換エラー

トークン交換エラーが発生した場合は、次のコードを使用します:

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

トークン交換が同意プロンプトのトリガーに失敗した場合のボットの動作を理解するには、次の手順を参照してください:

>[!NOTE]
> トークン交換が失敗したときにボットがアクションを実行するため、ユーザー アクションが実行される必要はありません。

1. クライアントは、OAuth シナリオをトリガーするボットとの会話を開始します。
2. ボットは OAuth カードをクライアントに返送します。
3. クライアントは、OAuth カードをユーザーに表示する前にインターセプトし、プロパティ `TokenExchangeResource` が含まれているかどうかを確認します。
4. そのプロパティが存在する場合、クライアントはボットに `TokenExchangeInvokeRequest` を 1 つ送信します。 クライアントには、ユーザーのための交換可能なトークンが必要です。このトークンは、Azure AD v2 トークンである必要があり、対象ユーザーは `TokenExchangeResource.Uri` プロパティと同じである必要があります。 クライアントは、次のコードを使用してボットに呼び出しアクティビティを送信します:

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. ボットは `TokenExchangeInvokeRequest` を処理し、`TokenExchangeInvokeResponse` を 1 つクライアントに返します。 クライアントは、`TokenExchangeInvokeResponse` を受信するまで待機する必要があります。

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. `TokenExchangeInvokeResponse` に `200` の `status` がある場合、クライアントは OAuth カードを表示しません。 [通常のフロー イメージ](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)を参照してください。 その他の `status` の場合、または `TokenExchangeInvokeResponse` が受信されていない場合、クライアントは OAuth カードをユーザーに表示します。 [フォールバック フロー イメージ](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)を参照してください。 ユーザーの同意など、エラーや依存関係が満たされていない場合、このアクティビティにより、確実に SSO フローが通常の OAuthCard フローに戻ります。

### <a name="update-the-auth-sample"></a>認証サンプルを更新する

[Teams 認証サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)を開き、次の手順を実行してそれを更新します:

1. Teams ボットを更新し、次のコードを含めることで、受信要求の重複を除去します:

    ```csharp
        protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
        protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
    ```
  
2. `botId`、パスワード、および [OAuth 接続を使用して Azure portal を更新する](#update-the-azure-portal-with-the-oauth-connection) で定義された接続名を含めるために、`appsettings.json`を更新します。
3. マニフェストを更新し、`token.botframework.com` が有効なドメインの一覧にあることを確認します。 詳細については、[Teams 認証サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)を参照してください。
4. プロファイル イメージを使用してマニフェストを zip 形式で圧縮し、Teams にインストールします。

## <a name="code-sample"></a>コード サンプル

|**サンプルの名前** | **説明** |**.NET** |**C#** |**Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
|Bot framework SDK | このサンプル コードでは、Microsoft Teams用のボットで認証を開始する方法を示します。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/csharp_dotnetcore/BotConversationSsoQuickstart)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/js)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ステップ [バイ ステップ ガイド](../../../sbs-bots-with-sso.yml)に従って、SSO 認証を使用してボットを構築します。
