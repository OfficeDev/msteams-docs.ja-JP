---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者はサインイン カードまたは Azure Bot サービスを OAuth カードのサポートと一緒に使用できます。
keywords: トークン、ユーザー トークン、ボットの SSO サポート
ms.openlocfilehash: ee9dbee063acf90f5596fc95d002caf53f88a08a
ms.sourcegitcommit: 0a9e91c65d88512eda895c21371b3cd4051dca0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/23/2020
ms.locfileid: "49729083"
---
# <a name="single-sign-on-sso-support-for-bots"></a>ボットのシングル サインオン (SSO) のサポート

Azure Active Directory (Azure AD) のシングル サインオン認証は、ユーザーがログイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンをサイレント 更新します。 ユーザーがアプリの使用に同意した場合、別のデバイスでもう一度同意する必要はありません。また、自動的にサインインします。 このフローは、Teams タブ SSO の [サポートと非常に似ています]( ../../../tabs/how-to/authentication/auth-aad-sso.md)。 違いは、ボットがトークンを要求して応答を受信する方法のプロトコルです。

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 の基本的な理解は、Teams で認証を操作する場合の前提条件です。

## <a name="bot-sso-at-runtime"></a>実行時の Bot SSO

![実行時のボット SSO の図](../../../assets/images/bots/bots-sso-diagram.png)

1. ボットは、プロパティを含む OAuthCard でメッセージを送信 `tokenExchangeResource` します。 ボット アプリケーションの認証トークンを取得するために Teams に指示します。 ユーザーは、ユーザーのすべてのアクティブなエンドポイントでメッセージを受信します。

    > [!NOTE]
    >* ユーザーは一度に複数のアクティブなエンドポイントを持つ可能性があります。  
    >* ボット トークンは、ユーザーのアクティブなエンドポイントごとに受信されます。
    >* 現在、シングル サインオンのサポートでは、アプリを個人用スコープでインストールする必要があります。

2. 現在のユーザーが初めてボット アプリケーションを使用する場合は、同意を求める要求プロンプト (同意が必要な場合) またはステップ アップ認証 (2 要素認証など) の処理を求めるプロンプトが表示されます。

3. Microsoft Teams は、現在のユーザーの Azure AD エンドポイントにボット アプリケーション トークンを要求します。

4. Azure AD、ボット アプリケーション トークンを Teams アプリケーションに送信します。

5. Microsoft Teams は、呼び出しアクティビティによって返される値オブジェクトの一部として、サインイン/トークンExchange という名前でトークンをボットに送信します。
  
6. トークンはボット アプリケーションで解析され、ユーザーの電子メール アドレスなどの必要な情報を抽出します。
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a>シングル サインオン Microsoft Teams ボットを開発する
  
SSO Microsoft Teams ボットを開発するには、次の手順が必要です。

1. [Azure 無料アカウントを作成する](#create-an-azure-account)
2. [Teams アプリ マニフェストを更新する](#update-your-app-manifest)
3. [ボット トークンを要求して受信するコードを追加する](#request-a-bot-token)

### <a name="create-an-azure-account"></a>Azure アカウントを作成する

この手順は、タブ [SSO フローに似ています](../../../tabs/how-to/authentication/auth-aad-sso.md)。

1. Teams の [デスクトップAD Web、](/graph/concepts/auth-register-app-v2) またはモバイル クライアントの Azure アプリケーション ID を取得します。
2. アプリケーションが Azure AD エンドポイントと、必要に応じて Microsoft Graph に必要なアクセス許可を指定します。
3. Teams[のデスクトップ、Web、](/azure/active-directory/develop/v2-permissions-and-consent)およびモバイル アプリケーションのアクセス許可を付与します。
4. **[スコープの追加]** を選択します。
5. 開くパネルで、スコープ名として入力してクライアント `access_as_user` アプリを **追加します**。

    >[!NOTE]
    > クライアント アプリのaccess_as_user "管理者とユーザー" のスコープです。

    > [!IMPORTANT]
    > * スタンドアロン ボットを作成する場合は、アプリケーション ID URI を Here に設定します `api://botid-{YourBotId}` **。YourBotId** は Azure ADアプリケーション ID を参照します。
    > * ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次に設定します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

### <a name="update-your-app-manifest"></a>アプリ マニフェストを更新する

Microsoft Teams マニフェストに新しいプロパティを追加します。

**WebApplicationInfo** - 次の要素の親。

> [!div class="checklist"]
>
> * **id** - アプリケーションのクライアント ID。 これは、Azure AD にアプリケーションを登録する一環として取得したアプリケーション ID です。
>* **resource** - アプリケーションのドメインとサブドメイン。 これは、上記の手順 6 で作成するときに登録した URI (プロトコルを含む `api://` ) `scope` と同じです。 リソースにパスを `access_as_user` 含めてはならない。 この URI のドメイン部分は、Teams アプリケーション マニフェストの URL で使用される任意のサブドメインを含むドメインと一致する必要があります。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a>ボット トークンを要求する

トークンを取得する要求は、通常の POST メッセージ要求です (既存のメッセージ スキーマを使用)。 OAuthCard の添付ファイルに含まれています。 OAuthCard クラスのスキーマは Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義され、サインイン カードに非常に似ています。 プロパティがカードに入力されている場合、Teams は、この要求をサイレント トークン取得 `TokenExchangeResource` として処理します。 Teams チャネルでは、トークン要求を一意に識別するプロパティ `Id` のみを尊重します。

>[!NOTE]
> Bot Framework `OAuthPrompt` またはシングル `MultiProviderAuthDialog` サインオン (SSO) 認証がサポートされています。

ユーザーが初めてアプリケーションを使用し、ユーザーの同意が必要な場合は、次のような同意エクスペリエンスを続行するダイアログが表示されます。 ユーザーが [ **続行**] を選択すると、ボットが定義されているかどうかと OAuthCard のサインイン ボタンに応じて、2 つの異なる処理が行われます。

![[同意] ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリーム内のカード ボタンからのサインイン フローと同様にトリガーされます。 開発者は、ユーザーに同意を求めるアクセス許可を決定します。 この方法は、たとえば、グラフ リソースのトークンを交換する場合など、アクセス許可を持つトークンが必要な `openId` 場合に推奨されます。

ボットがカードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットに対するユーザーの同意がトリガーされます。 このトークンは、基本認証とユーザーの電子メール アドレスの取得に役立ちます。

**サインイン ボタンのない C# トークン要求**:

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

#### <a name="receiving-the-token"></a>トークンの受信

トークンを持つ応答は、ボットが今日受け取るアクティビティを呼び出す他のユーザーと同じスキーマを持つ呼び出しアクティビティを通じて送信されます。 唯一の違いは、呼び出し名、**サインイン/トークンExchange、** およびトークンとトークン フィールドを取得する最初の要求の **ID** (文字列)を含む値フィールド (トークンを含む文字列値) です。  ユーザーが複数のアクティブなエンドポイントを持っている場合、特定の要求に対して複数の応答を受信する場合があります。 トークンを使用して応答を重複排除する必要があります。

**呼び出しアクティビティを処理するために応答する C# コード**:

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

`turnContext.activity.value` [TokenExchangeInvokeRequest 型](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)であり、ボットでさらに使用できるトークンが含まれます。 パフォーマンス上の理由からトークンを安全に保存し、更新します。

### <a name="update-the-azure-portal-with-the-oauth-connection"></a>OAuth 接続を使用して Azure Portal を更新する

1. Azure Portal で、ボット チャネル登録に **戻る**。

2. [設定] ブレード **に切** り替え、[OAuth 接続の設定] セクションで [設定の追加] を選択します。 

    ![SSOBotHandle2 ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. [接続設定 **] フォームに入力** します。

    > [!div class="checklist"]
    >
    > * 新しい接続設定の名前を入力します。 これは、手順 5 でボット サービス コードの設定内で参照される **名前になります**。
    > * [サービス プロバイダー] ドロップダウンで **、Azure Active Directory V2 を選択します**。
    >* AAD アプリケーションのクライアント資格情報を入力します。

    >[!NOTE]
    > **AAD アプリケーション** では暗黙的な許可が必要になる場合があります。

    >* トークン交換 URL の場合は、AAD アプリケーションの前の手順で定義したスコープ値を使用します。 Token Exchange URL の存在は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示しています。
    >* テナント ID として "common" **を指定します**。
    >* AAD アプリケーションのダウンストリーム API に対するアクセス許可を指定するときに構成されたスコープを追加します。 クライアント ID とクライアント シークレットが提供された場合、トークン ストアは、定義済みのアクセス許可を持つグラフ トークンのトークンを交換します。
    >* [**保存**] を選択します。

    ![VuSSOBotConnection 設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a>認証サンプルを更新する

まず、 [チームの認証サンプルを参照してください](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。

1. TeamsBot を更新して、次を含める。 受信要求の重複を処理するには、以下を参照してください。

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
  
2. 上記で `appsettings.json` 定義した接続名 `botId` 、パスワード、および接続名を含めるには、更新します。
3. マニフェストを更新し、有効 `token.botframework.com` なドメイン セクションに含まれています。
4. マニフェストをプロファイル イメージと一緒に Zip し、Teams にインストールします。

#### <a name="additional-code-samples"></a>その他のコード サンプル

* [Bot Framework SDK を使用した C# サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。

* [Bot Framework SDK を使用してトークン要求](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)を重複排除する C# サンプル。

* [Bot Framework SDK トークン ストアを使用しない C# サンプル](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)。
