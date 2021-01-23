---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者はサインイン カードまたは Azure Bot サービスを OAuth カードのサポートと一緒に使用できます。
keywords: トークン, ユーザー トークン, ボットの SSO サポート
ms.topic: conceptual
ms.openlocfilehash: 55b930ba50eede6ac970fbe0f901d418605f3f91
ms.sourcegitcommit: 5662bf23fafdbcc6d06f826a647f3696cd17f5e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2021
ms.locfileid: "49935255"
---
# <a name="single-sign-on-sso-support-for-bots"></a>ボットのシングル サインオン (SSO) のサポート

Azure Active Directory (AAD) のシングル サインオン認証では、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンをサイレント 更新します。 ユーザーがアプリの使用に同意した場合、別のデバイスでもう一度同意する必要はありません。また、自動的にサインインできます。 フローは[Microsoft Teams](../../../tabs/how-to/authentication/auth-aad-sso.md)タブ SSO サポートのフローと似ていますが、ボットがトークンを要求して[](#request-a-bot-token)応答を受信する方法のプロトコルが[異なっています](#receive-the-bot-token)。

>[!NOTE]
> OAuth 2.0 は、AAD および他の多くの ID プロバイダーで使用される認証と承認のオープン標準です。 OAuth 2.0 の基本的な理解は、Teams で認証を操作する場合の前提条件です。

## <a name="bot-sso-at-runtime"></a>実行時の Bot SSO

![実行時のボット SSO の図](../../../assets/images/bots/bots-sso-diagram.png)

認証トークンとボット アプリケーション トークンを取得するには、次の手順を実行します。

1. ボットは、プロパティを含む OAuthCard でメッセージを送信 `tokenExchangeResource` します。 ボット アプリケーションの認証トークンを取得するために Teams に指示します。 ユーザーは、すべてのアクティブなユーザー エンドポイントでメッセージを受信します。

    > [!NOTE]
    >* ユーザーは一度に複数のアクティブなエンドポイントを持つ可能性があります。
    >* ボット トークンは、すべてのアクティブユーザー エンドポイントから受信されます。
    >* SSO をサポートするには、アプリを個人用スコープでインストールする必要があります。

2. 現在のユーザーがボット アプリケーションを初めて使用する場合は、次のいずれかの操作をユーザーに要求する要求プロンプトが表示されます。
    * 必要に応じて同意を提供します。
    * 2 要素認証などのステップ アップ認証を処理します。

3. Teams は、現在のユーザーの AAD エンドポイントからボット アプリケーション トークンを要求します。

4. AAD はボット アプリケーション トークンを Teams アプリケーションに送信します。

5. Teams は、サインイン **/トークンExchange** という名前で、呼び出しアクティビティによって返される値オブジェクトの一部としてボットにトークンを送信します。
  
6. ボット アプリケーションで解析されたトークンは、ユーザーの電子メール アドレスなどの必要な情報を提供します。
  
## <a name="develop-an-sso-teams-bot"></a>SSO Teams ボットを開発する
  
SSO Teams ボットを開発するには、次の手順を実行します。

1. [AAD ポータルからアプリを登録します](#register-your-app-through-the-aad-portal)。
2. [ボットの Teams アプリケーション マニフェストを更新します](#update-your-teams-application-manifest-for-your-bot)。
3. [ボット トークンを要求および受信するコードを追加します](#add-the-code-to-request-and-receive-a-bot-token)。

### <a name="register-your-app-through-the-aad-portal"></a>AAD ポータルを通じてアプリを登録する

AAD ポータルを通じてアプリを登録する手順は、タブ SSO フロー [に似ています](../../../tabs/how-to/authentication/auth-aad-sso.md)。 アプリを登録するには、次の手順を実行します。

1. Azure Active Directory アプリ登録ポータルに [新しいアプリケーションを登録](https://go.microsoft.com/fwlink/?linkid=2083908) します。
2. [新規 **登録] を選択します**。 [ **アプリケーションの登録] ページ** が表示されます。
3. [アプリケーション **の登録] ページで** 、次の値を入力します。
    1. アプリの **名前** を入力します。
    2. サポートされている **アカウントの種類を選択し、** 単一テナントアカウントまたはマルチテナント アカウントの種類を選択します。

        > [!NOTE]
        >
        > AAD アプリが Teams で認証要求を行っているのと同じテナントに登録されている場合、ユーザーは同意を求めではなく、アクセス トークンを直接付与されます。 ただし、AAD アプリが別のテナントに登録されている場合、ユーザーはアクセス許可に同意する必要があります。

    3. **[登録]** を選択します。
4. 概要ページで、アプリケーション **(クライアント) ID をコピーして保存します**。 後で Teams アプリケーション マニフェストを更新するときに必要になります。
5. [**管理**] で [**API の公開**] を選択します。 

   > [!IMPORTANT]
    > * スタンドアロン ボットを作成する場合は、次のようにアプリケーション ID URI を入力します `api://botid-{YourBotId}` 。 ここで **、YourBotId** は AAD アプリケーション ID です。
    > * ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次のように入力します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

5. アプリケーションが AAD エンドポイントに必要とするアクセス許可と、必要に応じて Microsoft Graph に必要なアクセス許可を選択します。
6. Teams[のデスクトップ、Web、](/azure/active-directory/develop/v2-permissions-and-consent)モバイル アプリケーションのアクセス許可を付与します。
7. **[スコープの追加]** を選択します。
8. 開くパネルで、スコープ名として入力してクライアント `access_as_user` アプリを **追加します**。

    >[!NOTE]
    > クライアント アプリのaccess_as_user "管理者とユーザー" のスコープです。
    >
    > 次の重要な制限に注意する必要があります。
    >
    > * ユーザー レベルの Microsoft Graph API のアクセス許可 (メール、プロファイル、offline_access、OpenId など) だけがサポートされます。 その他の Microsoft Graph スコープにアクセスする必要がある場合 (または、推奨される回避策 `User.Read` `Mail.Read` [を参照してください](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes))。
    > * アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じである必要があります。
    > * 現在、アプリごとに複数のドメインはサポートされていません。
    > * ドメインを使用するアプリケーションは、一般的であり、セキュリティ上のリスクが `azurewebsites.net` 高い可能性からサポートされていません。

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>OAuth 接続を使用して Azure Portal を更新する

OAuth 接続を使用して Azure Portal を更新するには、次の手順を実行します。

1. Azure Portal で、ボット チャネル登録 **に移動します**。

2. API の **アクセス許可に移動します**。 [Microsoft Graph **委任されたアクセス** 許可のアクセス許可の追加] を選択し、Microsoft Graph API から次のアクセス  >    >  許可を追加します。
    * User.Read (既定で有効)
    * メール
    * offline_access
    * OpenId
    * プロフィール

3. 左側 **のウィンドウで [** 設定] を選択し、[OAuth 接続 **の設定]** セクションで [ **設定の追加] を選択** します。

    ![SSOBotHandle2 ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

4. [新しい接続設定] フォームを完了するには **、次の手順を実行** します。

    >[!NOTE]
    > **AAD アプリケーション** では暗黙的な許可が必要になる場合があります。

    1. [新しい **接続設定** ] **ページに名前を入力** します。 これは、実行時に Bot SSO の手順 *5* でボット サービス コードの設定内で参照される [名前です](#bot-sso-at-runtime)。
    2. [サービス **プロバイダー] ドロップダウンから****、Azure Active Directory v2 を選択します**。
    3. AAD アプリケーションのクライアント **ID** や **クライアント** シークレットなどのクライアント資格情報を入力します。
    4. トークン交換 **URL の場合は**、「ボットの Teams アプリケーション マニフェストを更新 [する」で定義されているスコープ値を使用します](#update-your-teams-application-manifest-for-your-bot)。 Token Exchange URL は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示します。
    5. [テナント **ID] ボックスに** 「共通」と *入力します*。
    6. AAD **アプリケーションのダウンストリーム** API へのアクセス許可を指定するときに構成されたスコープを追加します。 クライアント ID とクライアント シークレットが提供された場合、トークン ストアは、定義されたアクセス許可を持つグラフ トークンのトークンを交換します。
    7. [**保存**] を選択します。

    ![VuSSOBotConnection 設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>ボットの Teams アプリケーション マニフェストを更新する

アプリケーションにスタンドアロン ボットが含まれている場合は、次のコードを使用して新しいプロパティを Teams アプリケーション マニフェストに追加します。

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
アプリケーションにボットとタブが含まれている場合は、次のコードを使用して新しいプロパティを Teams アプリケーション マニフェストに追加します。

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** は、次の要素の親です。

* **id** - アプリケーションのクライアント ID。 これは、アプリケーションを AAD に登録する一部として取得したアプリケーション ID です。
* **resource** - アプリケーションのドメインとサブドメイン。 これは `api://` `scope` [、AAD](#register-your-app-through-the-aad-portal)ポータルからアプリを登録するときに登録したプロトコルを含め、同じ URI です。 リソースにパスを `access_as_user` 含めずにしてください。 この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用されるドメインとサブドメインと一致している必要があります。

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>ボット トークンを要求して受信するコードを追加する

#### <a name="request-a-bot-token"></a>ボット トークンを要求する

トークンを取得する要求は、既存のメッセージ スキーマを使用した通常の POST メッセージ要求です。 OAuthCard の添付ファイルに含まれています。 OAuthCard クラスのスキーマは Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義され、サインイン カードに似ています。 カードにプロパティが設定されている場合、Teams は、この要求をサイレント トークン取得 `TokenExchangeResource` として処理します。 Teams チャネルでは、トークン要求を一意に識別するプロパティ `Id` だけが使用されます。

>[!NOTE]
> Microsoft Bot Framework または SSO `OAuthPrompt` `MultiProviderAuthDialog` 認証がサポートされています。

ユーザーがアプリケーションを初めて使用し、ユーザーの同意が必要な場合は、次のダイアログ ボックスが表示され、同意エクスペリエンスが続行されます。

![[同意] ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

ユーザーが [続行] を選択 **すると**、次のイベントが発生します。

* ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリーム内の OAuth カード ボタンからのサインイン フローと同様にトリガーされます。 開発者は、ユーザーの同意を必要とするアクセス許可を決定する必要があります。 この方法は、それ以上のアクセス許可を持つトークンが必要な場合に推奨されます `openId` 。 たとえば、グラフ リソースのトークンを交換する場合です。

* ボットが OAuth カードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットに対してユーザーの同意が必要です。 このトークンは、基本認証やユーザーの電子メール アドレスの取得に役立ちます。

##### <a name="c-token-request-without-a-sign-in-button"></a>サインイン ボタンのない C# トークン要求

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

#### <a name="receive-the-bot-token"></a>ボット トークンを受信する

トークンを含む応答は、ボットが現在受け取る他の呼び出しアクティビティと同じスキーマを持つ呼び出しアクティビティを通じて送信されます。 唯一の違いは、呼び出し名、**サインイン/トークンExchange、****および値** フィールドです。 値 **フィールド** には **、Id、** トークンとトークン フィールドを取得する最初の要求の文字列、トークンを含む文字列値が含まれます。

>[!NOTE]
> ユーザーが複数のアクティブなエンドポイントを持つ場合、特定の要求に対して複数の応答を受け取る場合があります。 トークンを使用して応答を重複排除する必要があります。

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

`turnContext.activity.value` [TokenExchangeInvokeRequest 型](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)であり、ボットでさらに使用できるトークンが含まれます。 パフォーマンス上の理由からトークンを保存し、更新する必要があります。

### <a name="update-the-auth-sample"></a>認証サンプルを更新する

[Teams 認証サンプルを開](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)き、次の手順を実行して更新します。

1. 次のコードを含めて、受信要求の重複を処理するために TeamsBot を更新します。

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
  
2. `appsettings.json`「OAuth 接続を使用して Azure portal を更新する」で定義されている接続名 、パスワード `botId` [を含める更新](#update-the-azure-portal-with-the-oauth-connection)。
3. マニフェストを更新し、有効 `token.botframework.com` なドメインの一覧に含まれています。 詳細については [、Teams 認証サンプルを参照してください](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。
4. マニフェストをプロファイル イメージと一緒に Zip し、Teams にインストールします。

#### <a name="additional-code-samples"></a>その他のコード サンプル

* [Bot Framework SDK を使用した C# サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。
