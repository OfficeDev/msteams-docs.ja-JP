---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者は、OAuth カードのサポートを受け取ってサインイン カードまたは Azure ボット サービスを使用できます。
keywords: トークン、ユーザー トークン、ボットの SSO サポート
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: e3f4c7a1c803baba2687e3803a820dc351f9ca33
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475732"
---
# <a name="single-sign-on-sso-support-for-bots"></a>ボットのシングル サインオン (SSO) のサポート

Azure Active Directory (AAD) のシングル サインオン認証では、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑え、認証トークンをサイレント モードで更新します。 ユーザーがアプリの使用に同意すると、別のデバイスでもう一度同意する必要はありません。自動的にサインインできます。 このフローは、Microsoft Teams SSO サポート[のフローと](../../../tabs/how-to/authentication/auth-aad-sso.md)似ていますが、ボットがトークンを要求して応答を受け[](#request-a-bot-token)取る方法のプロトコルに[違いがあります](#receive-the-bot-token)。

>[!NOTE]
> OAuth 2.0 は、AAD および他の多くの ID プロバイダーが使用する認証と承認のオープン標準です。 OAuth 2.0 の基本的な理解は、認証を使用する場合の前提条件Teams。

## <a name="bot-sso-at-runtime"></a>実行時のボット SSO

![実行時の図でのボット SSO](../../../assets/images/bots/bots-sso-diagram.png)

認証およびボット アプリケーション トークンを取得するには、次の手順を実行します。

1. ボットが、`tokenExchangeResource`プロパティを含む OAuthCard でメッセージを送信します。 ボット アプリケーションTeamsトークンを取得する必要があります。 ユーザーは、アクティブなすべてのユーザー エンドポイントでメッセージを受信します。

    > [!NOTE]
    >* ユーザーは、一度に複数のアクティブなエンドポイントを持つ可能性があります。
    >* ボット トークンは、すべてのアクティブなユーザーのエンドポイントから受信されます。
    >* SSO をサポートするには、アプリを個人用のスコープにインストールする必要があります。

1. 現在のユーザーが初めてボット アプリケーションを使用している場合は、要求プロンプトが表示され、ユーザーに次のいずれかの操作を要求します。
    * 必要に応じて同意を提供します。
    * 2 要素認証などのステップ アップ認証を処理します。

1. Teamsユーザーの AAD エンドポイントからボット アプリケーション トークンを要求します。

1. AAD はボット アプリケーション トークンをアプリケーションにTeamsします。

1. Teamsサインイン **/tokenExchange** という名前の呼び出しアクティビティによって返される値オブジェクトの一部として、トークンをボットに送信します。
  
1. ボット アプリケーションの解析されたトークンは、ユーザーのメール アドレスなど、必要な情報を提供します。
  
## <a name="develop-an-sso-teams-bot"></a>SSO サーバー ボットTeamsする
  
SSO ボットを開発するには、次の手順Teamsします。

1. [AAD ポータルを使用してアプリを登録します](#register-your-app-through-the-aad-portal)。
1. [ボットのTeamsアプリケーション マニフェストを更新します](#update-your-teams-application-manifest-for-your-bot)。
1. [ボット トークンを要求および受信するコードを追加します](#add-the-code-to-request-and-receive-a-bot-token)。

### <a name="register-your-app-through-the-aad-portal"></a>AAD ポータルを介してアプリを登録する

AAD ポータルを介してアプリを登録する手順は、タブ SSO フロー [に似ています](../../../tabs/how-to/authentication/auth-aad-sso.md)。 アプリを登録するには、次の手順を実行します。

1. アプリ登録ポータルで新[しいAzure Active Directoryを登録](https://go.microsoft.com/fwlink/?linkid=2083908)します。
2. [新規 **登録] を選択します**。 [ **アプリケーションの登録] ページ** が表示されます。
3. [アプリケーションの **登録] ページで** 、次の値を入力します。
    1. アプリの **[名前]** を入力します。
    2. [サポートされている **アカウントの種類] を選択し、[** 単一テナント] または [マルチテナント アカウントの種類] を選択します。

        > [!NOTE]
        >
        > AAD アプリが Teams で認証要求を行っているのと同じテナントに登録されている場合、ユーザーは同意を求めではなく、アクセス トークンが付与されます。 ただし、AAD アプリが別のテナントに登録されている場合、ユーザーはアクセス許可に同意する必要があります。

    3. **[登録]** を選択します。
4. [概要] ページで、アプリケーション **(クライアント) ID をコピーして保存します**。 後でアプリケーション マニフェストを更新するときにTeams必要です。
5. [**管理**] で [**API の公開**] を選択します。 

   > [!IMPORTANT]
    > * スタンドアロン ボットを作成する場合は、アプリケーション ID URI を次のように入力します `api://botid-{YourBotId}` 。 ここでは **、YourBotId** は AAD アプリケーション ID です。
    > * ボットとタブを使用してアプリを作成する場合は、アプリケーション ID URI を次のように入力します `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

5. アプリケーションが AAD エンドポイントに必要なアクセス許可を選択し、必要に応じて Microsoft エンドポイントGraph。
6. [デスクトップ、web、Teams](/azure/active-directory/develop/v2-permissions-and-consent)アプリケーションのアクセス許可を付与します。
7. **[スコープの追加]** を選択します。
8. 開くパネルで、スコープ名を入力してクライアント `access_as_user` アプリ **を追加します**。

    >[!NOTE]
    > クライアント アプリのaccess_as_userに使用される "管理者とユーザー" スコープは、"管理者とユーザー" です。
    >
    > 次の重要な制限に注意する必要があります。
    >
    > * 電子メール、プロファイル、Graph OpenId などのユーザー レベルの API アクセス許可offline_accessのみサポートされます。 その他の Microsoft Graph スコープ (Graphなど) へのアクセスが必要な場合は、「アクセス トークンを取得する」を参照Graph `User.Read` `Mail.Read` [してください](../../../tabs/how-to/authentication/auth-aad-sso.md#get-an-access-token-with-graph-permissions)。
    > * アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じである必要があります。
    > * アプリごとに複数のドメインは現在サポートされていません。
    > * ドメインを使用するアプリケーションは一般的であり、セキュリティ リスクである可能性があるため `azurewebsites.net` 、サポートされていません。

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>OAuth 接続を使用して Azure ポータルを更新する

OAuth 接続を使用して Azure ポータルを更新するには、次の手順を実行します。

1. Azure portal で、[アプリの登録 **] に移動します**。

2. [API の **アクセス許可] に移動します**。 [**アクセス許可を追加する]** Graph委任されたアクセス許可] を選択し、次のアクセス許可を Microsoft Graph  >    >  API に追加します。
    * User.Read (既定で有効)
    * メール
    * offline_access
    * OpenId
    * profile

3. Azure ポータルで [**、AzureBot に移動します。**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)
4. 左側の **ウィンドウで** [構成] を選択します。
5. **[OAuth 接続の追加] を設定。**

    ![SSOBotHandle2 ビュー](~/assets\Contosoairlines123.png)

6. [新しい接続設定] フォームを完了するには **、次の手順を実行** します。

    >[!NOTE]
    > **AAD アプリケーション** では暗黙的な付与が必要になる場合があります。

    1. [新しい **接続設定]** ページ **に名前を入力** します。 これは、実行時にボット SSO の手順 *5* でボット サービス コードの設定 [内で参照される名前です](#bot-sso-at-runtime)。
    2. [サービス **プロバイダー] ドロップダウン** から、[v2] **Azure Active Directory選択します**。
    3. AAD アプリケーションのクライアント **ID** や **クライアント** シークレットなどのクライアント資格情報を入力します。
    4. Token Exchange **URL の** 場合は、「Update your Teams アプリケーション マニフェスト」で定義されているスコープ値 [を使用します](#update-your-teams-application-manifest-for-your-bot)。 トークンのExchange URL は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示します。
    5. [テナント **ID] ボックスに** 「共通」と *入力します*。
    6. AAD **アプリケーションのダウンストリーム** API へのアクセス許可を指定するときに構成されたスコープを追加します。 クライアント ID とクライアント シークレットが提供されている場合、トークン ストアは、定義されたアクセス許可を持つグラフ トークンのトークンを交換します。
    7. [**保存**] を選択します。

    ![VuSSOBotConnection 設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>ボットのTeamsアプリケーション マニフェストを更新する

アプリケーションにスタンドアロン ボットが含まれている場合は、次のコードを使用して新しいプロパティをアプリケーション マニフェストTeamsします。

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
アプリケーションにボットとタブが含まれている場合は、次のコードを使用して新しいプロパティをアプリケーション マニフェストTeamsします。

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** は、次の要素の親です。

* **id** - アプリケーションのクライアント ID。 これは、アプリケーションを AAD に登録する一部として取得したアプリケーション ID です。 このアプリケーション ID を複数のアプリと共有Teamsしてください。 使用するアプリケーション マニフェストごとに新しい AAD アプリを作成します `webApplicationInfo` 。
* **resource** - アプリケーションのドメインとサブドメイン。 これは、AAD ポータルからアプリを登録するで作成するときに登録したプロトコルを含む、同じ `api://` `scope` URI [です](#register-your-app-through-the-aad-portal)。 リソースにパスを `access_as_user` 含めなけれ。 この URI のドメイン部分は、アプリケーション マニフェストの URL で使用されるドメインとサブドメインTeams必要があります。

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>ボット トークンを要求および受信するコードを追加する

#### <a name="request-a-bot-token"></a>ボット トークンの要求

トークンを取得する要求は、既存のメッセージ スキーマを使用した通常の POST メッセージ要求です。 これは、OAuthCard の添付ファイルに含まれています。 OAuthCard クラスのスキーマは Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義され、サインイン カードに似ています。 Teamsがカードに設定されている場合、この要求はサイレント トークン取得 `TokenExchangeResource` として扱います。 このチャネルTeamsトークン要求を一意に識別するプロパティだけが `Id` 受け入れされます。

>[!NOTE]
> SSO 認証Microsoft Bot Framework `OAuthPrompt` `MultiProviderAuthDialog` サポートされている場合は、SSO 認証がサポートされています。

ユーザーが初めてアプリケーションを使用し、ユーザーの同意が必要な場合は、次のダイアログ ボックスが表示され、同意エクスペリエンスが続行されます。

![[同意] ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

ユーザーが **[続行する]** を選択すると、次のイベントが発生します。

* ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリームの OAuth カード ボタンからのサインイン フローと同様にトリガーされます。 開発者は、ユーザーの同意が必要なアクセス許可を決定する必要があります。 この方法は、 を超えるアクセス許可を持つトークンが必要な場合にお勧めします `openId` 。 たとえば、グラフ リソース用にトークンを交換する場合です。

* ボットが OAuth カードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットに対してユーザーの同意が必要です。 このトークンは、基本認証やユーザーの電子メール アドレスの取得に役立ちます。

##### <a name="c-token-request-without-a-sign-in-button"></a>C#ボタンを使用せずにトークン要求を実行する

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

#### <a name="receive-the-bot-token"></a>ボット トークンの受信

トークンによる応答は、ボットが今日受け取る他の呼び出しアクティビティと同じスキーマを持つ呼び出しアクティビティを介して送信されます。 唯一の違いは、呼び出し名、**サインイン/tokenExchange、****および値** フィールドです。 値 **フィールド** には **、Id**、トークンとトークン フィールドを取得する最初の要求の文字列、トークンを含む文字列値が含まれます。

>[!NOTE]
> ユーザーが複数のアクティブなエンドポイントを持つ場合、特定の要求に対して複数の応答を受信する場合があります。 トークンを使用して応答を重複排除する必要があります。

##### <a name="c-code-to-handle-the-invoke-activity"></a>C#アクティビティを処理するコードを作成する

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

is `turnContext.activity.value` of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) と、ボットでさらに使用できるトークンが含まれます。 パフォーマンス上の理由からトークンを保存し、更新する必要があります。

### <a name="token-exchange-failure"></a>トークン交換の失敗

トークン交換に失敗した場合は、次のコードを使用します。

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

トークン交換が同意プロンプトのトリガーに失敗した場合のボットの動作を理解するには、次の手順を参照してください。

>[!NOTE]
> トークン交換が失敗した場合にボットがアクションを実行する際に、ユーザー操作を実行する必要はありません。

1. クライアントは、OAuth シナリオをトリガーするボットとの会話を開始します。
2. ボットは OAuth カードをクライアントに返します。
3. クライアントは、OAuth カードをユーザーに表示する前に傍受し、プロパティが含まれているか確認 `TokenExchangeResource` します。
4. プロパティが存在する場合、クライアントはボットに a `TokenExchangeInvokeRequest` を送信します。 クライアントは、ユーザーの交換可能なトークンを持っている必要があります。これは Azure AD v2 トークンで、対象ユーザーはプロパティと同じである必要 `TokenExchangeResource.Uri` があります。 クライアントは、次のコードを使用してボットに呼び出しアクティビティを送信します。

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

5. ボットは、クライアントを `TokenExchangeInvokeRequest` 処理し、 `TokenExchangeInvokeResponse` クライアントに戻します。 クライアントは、 を受信するまで待機する必要があります `TokenExchangeInvokeResponse` 。

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

6. a を `TokenExchangeInvokeResponse` 持 `status` つ `200` 場合、クライアントは OAuth カードを表示しない。 通常の [フロー イメージを参照してください](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。 その他の `status` 場合、または受信されていない場合、クライアントはユーザーに `TokenExchangeInvokeResponse` OAuth カードを表示します。 フォールバック フロー [イメージを参照してください](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。 これにより、ユーザーの同意のようなエラーやアンメット依存関係が発生した場合に、SSO フローが通常の OAuthCard フローに戻ります。


### <a name="update-the-auth-sample"></a>auth サンプルを更新する

認証[Teams開き](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)、次の手順を実行して更新します。

1. 次のコードを含めて、受信要求の重複排除を処理するために TeamsBot を更新します。

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
  
2. [OAuth 接続を使用して Azure portal を更新する] で定義されている 、パスワード、および接続 `appsettings.json` `botId` [名を含める更新プログラム](#update-the-azure-portal-with-the-oauth-connection)。
3. マニフェストを更新し、有効 `token.botframework.com` なドメイン一覧に含まれています。 詳細については、「Teams[認証サンプル」を参照してください](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。
4. プロファイル イメージを使用してマニフェストを圧縮し、そのマニフェストをTeams。

## <a name="code-sample"></a>コード サンプル
|**サンプルの名前** | **説明** |**.NET** | 
|----------------|-----------------|--------------|
|ボット フレームワーク SDK | ボット フレームワーク SDK を使用するサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
