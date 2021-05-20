---
title: ボットのシングル サインオンのサポート
description: ユーザー トークンを取得する方法について説明します。 現在、ボット開発者は、OAuth カードのサポートを使用して、サインイン カードまたは Azure ボット サービスを使用できます。
keywords: トークン、ユーザー トークン、ボットの SSO サポート
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a43c2a46561149ff97d039a3ba8fe9f4472e2073
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566095"
---
# <a name="single-sign-on-sso-support-for-bots"></a>ボットのシングル サインオン (SSO) サポート

Azure Active Directory (AAD) のシングル サインオン認証では、認証トークンをサイレントに更新することで、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑えることができます。 ユーザーがアプリの使用に同意すると、別のデバイスでもう一度同意する必要はありません。自動的にサインインできます。 フローは[[Microsoft Teamsタブ SSO サポート](../../../tabs/how-to/authentication/auth-aad-sso.md)と似ていますが、違いは、ボットが[トークンを要求](#request-a-bot-token)して応答を[受け取る](#receive-the-bot-token)方法のプロトコルにあります。

>[!NOTE]
> OAuth 2.0 は、AAD および他の多くの ID プロバイダーによって使用される認証と承認のためのオープンスタンダードです。 OAuth 2.0 の基本知識は、Teamsで認証を操作するための前提条件です。

## <a name="bot-sso-at-runtime"></a>実行時のボット SSO

![実行時のボット SSO 図](../../../assets/images/bots/bots-sso-diagram.png)

認証およびボット アプリケーション トークンを取得するには、次の手順を実行します。

1. ボットが、`tokenExchangeResource`プロパティを含む OAuthCard でメッセージを送信します。 Teamsに対して、ボット アプリケーションの認証トークンを取得するように指示します。 ユーザーは、アクティブなすべてのユーザー エンドポイントでメッセージを受信します。

    > [!NOTE]
    >* ユーザーは、一度に複数のアクティブなエンドポイントを持つ可能性があります。
    >* ボット トークンは、すべてのアクティブなユーザーのエンドポイントから受信されます。
    >* SSO をサポートするには、アプリを個人用のスコープにインストールする必要があります。

1. 現在のユーザーが初めてボット アプリケーションを使用している場合は、次のいずれかの操作を要求する要求プロンプトが表示されます。
    * 必要に応じて、同意を提供します。
    * 2 要素認証などのステップ アップ認証を処理します。

1. Teamsは、現在のユーザーの AAD エンドポイントからボット アプリケーション トークンを要求します。

1. AAD は、ボット アプリケーション トークンをTeams アプリケーションに送信します。

1. Teamsは、名前 **サインイン/tokenExchange** を使用して、invoke アクティビティによって返される値オブジェクトの一部としてトークンをボットに送信します。
  
1. ボット アプリケーションの解析されたトークンは、ユーザーのメール アドレスなど、必要な情報を提供します。
  
## <a name="develop-an-sso-teams-bot"></a>SSO Teamsボットの開発
  
SSO Teams ボットを開発するには、次の手順を実行します。

1. [AAD ポータル を使用してアプリを登録する](#register-your-app-through-the-aad-portal)。
1. [Teamsアプリケーション マニフェストをボット用に更新します](#update-your-teams-application-manifest-for-your-bot)。
1. [ボット トークンを要求して受け取るコードを追加](#add-the-code-to-request-and-receive-a-bot-token)します。

### <a name="register-your-app-through-the-aad-portal"></a>AAD ポータルを使用してアプリを登録する

AAD ポータルを通じてアプリを登録する手順は、 [SSO フロー タブ](../../../tabs/how-to/authentication/auth-aad-sso.md)に似ています。 アプリを登録するには、次の手順を実行します。

1. Azure Active Directory – アプリ登録ポータルで新しい[アプリケーションを登録します](https://go.microsoft.com/fwlink/?linkid=2083908)。
2. [ **新規登録 ]** を選択します。 [ **アプリケーションの登録]** ページが表示されます。
3. [ **アプリケーションの登録]** ページで、次の値を入力します。
    1. アプリの **[名前] を** 入力します。
    2. [ **サポートされているアカウントの種類**] を選択し、[シングル テナント] または [マルチテナント アカウントの種類] を選択します。

        > [!NOTE]
        >
        > AAD アプリがTeamsで認証要求を行っているテナントと同じテナントに登録されている場合、ユーザーは同意を求めらなくて、すぐにアクセス トークンが付与されます。 ただし、AAD アプリが別のテナントに登録されている場合は、ユーザーがアクセス許可に同意する必要があります。

    3. **[登録]** を選択します。
4. 概要ページで、 **アプリケーション (クライアント) ID** をコピーして保存します。 後でTeamsアプリケーション マニフェストを更新するときに必要になります。
5. [**管理**] で [**API の公開**] を選択します。 

   > [!IMPORTANT]
    > * スタンドアロン ボットを構築する場合は、アプリケーション ID URI を `api://botid-{YourBotId}` として入力します。 ここで **YourBotId** は AAD アプリケーション ID です。
    > * ボットとタブを使用してアプリをビルドする場合は、アプリケーション ID URI を `api://fully-qualified-domain-name.com/botid-{YourBotId}` として入力します。

5. アプリケーションが AAD エンドポイントに必要なアクセス許可を選択し、必要に応じて Microsoft Graph用に選択します。
6. デスクトップ、Web、モバイルアプリケーションTeamsの[アクセス許可を付与](/azure/active-directory/develop/v2-permissions-and-consent)します。
7. **[スコープの追加]** を選択します。
8. 開いたパネルで、スコープ名 と入力してクライアント アプリケーション `access_as_user` を追加します。

    >[!NOTE]
    > クライアント アプリを追加するために使用される "access_as_user" スコープは、"管理者とユーザー" 用です。
    >
    > 次の重要な制限事項に注意する必要があります。
    >
    > * 電子メール、プロファイル、offline_access、OpenId などのユーザー レベルの Microsoft Graph API のアクセス許可のみがサポートされます。 または などの他の Microsoft Graph スコープにアクセスする必要がある場合 `User.Read` `Mail.Read` は、「[回避策](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)」を参照してください。
    > * アプリケーションのドメイン名は、AAD アプリケーションに登録したドメイン名と同じである必要があります。
    > * 現在、アプリごとに複数のドメインがサポートされていません。
    > * ドメインを使用するアプリケーション `azurewebsites.net` は、一般的であり、セキュリティ上のリスクがあるため、サポートされません。

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>OAuth 接続を使用して Azure ポータルを更新する

OAuth 接続で Azure ポータルを更新するには、次の手順を実行します。

1. Azure ポータルで、[ **アプリの登録**] に移動します。

2. API **の権限** に移動します。 [Microsoft   >  **Graph**  >  **委任されたアクセス許可** を追加する] を選択し、Microsoft Graph API から次のアクセス許可を追加します。
    * ユーザー.読み取り(デフォルトで有効)
    * メール
    * offline_access
    * オープンID
    * profile

3. Azure ポータルで、[ボット **チャネルの登録**] に移動します。

4. 左側のペインで **設定** を選択し **、[OAuth 接続設定** セクションの下にある **[設定の追加**] を選択します。

    ![ビュー](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. 次の手順を実行して、 **新しい接続設定** フォームを完成させます。

    >[!NOTE]
    > **AAD アプリケーションでは、暗黙的な許可** が必要な場合があります。

    1. **[新しい接続設定]** ページに **[名前**] を入力します。 これは、実行時に Bot [SSO](#bot-sso-at-runtime)の *ステップ 5* でボット サービス コードの設定の内部で参照される名前です。
    2. [**サービス プロバイダ**] ドロップダウンから **、[v2 Azure Active Directory]** を選択します。
    3. AAD アプリケーションのクライアント ID や **クライアント シークレット** などの **クライアント** 資格情報を入力します。
    4. [**トークン Exchangeの URL]** には [、「Teams アプリケーション マニフェストをボットに更新する](#update-your-teams-application-manifest-for-your-bot)」で定義されているスコープ値を使用します。 トークン Exchange URL は、この AAD アプリケーションが SSO 用に構成されていることを SDK に示します。
    5. [ **テナント ID]** ボックスに「 *共通*」と入力します。
    6. AAD アプリケーションのダウンストリーム API へのアクセス許可を指定するときに構成されたすべての **スコープ** を追加します。 クライアント ID とクライアント シークレットが提供されている場合、トークン ストアは、定義されたアクセス許可を持つグラフ トークンのトークンを交換します。
    7. **[保存]** を選択します。

    ![設定ビュー](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>ボットのTeams アプリケーション マニフェストを更新する

アプリケーションにスタンドアロン ボットが含まれている場合は、次のコードを使用して、Teams アプリケーション マニフェストに新しいプロパティを追加します。

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
アプリケーションにボットとタブが含まれている場合は、次のコードを使用して、Teamsアプリケーション マニフェストに新しいプロパティを追加します。

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**は** 、次の要素の親です。

* **id** - アプリケーションのクライアント ID。 これは、AAD にアプリケーションを登録する際に取得したアプリケーション ID です。
* **resource** - アプリケーションのドメインとサブドメイン。 これは `api://` `scope` [、AAD ポータルを使用してアプリを登録](#register-your-app-through-the-aad-portal)する で作成したときに登録したプロトコルを含む、同じ URI です。 リソースにパスを含める必要はありません `access_as_user` 。 この URI のドメイン部分は、Teamsアプリケーション マニフェストの URL で使用されるドメインとサブドメインと一致する必要があります。

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>ボット トークンを要求して受け取るコードを追加する

#### <a name="request-a-bot-token"></a>ボット トークンのリクエスト

トークンを取得する要求は、既存のメッセージ スキーマを使用する通常の POST メッセージ要求です。 OAuthCard の添付ファイルに含まれています。 OAuthCard クラスのスキーマは [、Microsoft Bot スキーマ 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) で定義されており、サインイン カードに似ています。 Teamsは `TokenExchangeResource` 、プロパティがカードに設定されている場合、この要求をサイレント トークン取得として扱います。 Teams チャネルでは、 `Id` トークン要求を一意に識別するプロパティのみが受け入れられます。

>[!NOTE]
> Microsoft Bot Framework `OAuthPrompt` または は `MultiProviderAuthDialog` 、SSO 認証でサポートされています。

ユーザーが初めてアプリケーションを使用していて、ユーザーの同意が必要な場合は、次のダイアログ ボックスが同意の操作を続行するように表示されます。

![同意ダイアログ ボックス](../../../assets/images/bots/bots-consent-dialogbox.png)

ユーザーが **[続行する]** を選択すると、次のイベントが発生します。

* ボットがサインイン ボタンを定義している場合、ボットのサインイン フローは、メッセージ ストリームの OAuth カード ボタンからのサインイン フローと同様にトリガーされます。 開発者は、ユーザーの同意が必要なアクセス許可を決定する必要があります。 この方法は、 以外のアクセス許可を持つトークンが必要な場合にお勧めします `openId` 。 たとえば、グラフ リソースにトークンを交換する場合です。

* ボットが OAuth カードにサインイン ボタンを提供していない場合は、最小限のアクセス許可セットにユーザーの同意が必要です。 このトークンは、基本認証やユーザーの電子メール アドレスの取得に役立ちます。

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

トークンを含む応答は、今日ボットが受信する他の呼び出しアクティビティと同じスキーマを持つ invoke アクティビティを通じて送信されます。 唯一の違いは、呼び出し名、 **サインイン/トークン交換** 、および **値** フィールドです。 **値** フィールドには、 **Id** トークンを取得するための最初の要求の文字列と **トークン** フィールドが含まれます。

>[!NOTE]
> ユーザーが複数のアクティブなエンドポイントを持っている場合、特定の要求に対して複数の応答を受け取る場合があります。 トークンを使用して応答を重複除去する必要があります。

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

`turnContext.activity.value`型は[TokenExchangeInvokeRequest であり](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)、ボットでさらに使用できるトークンが含まれています。 パフォーマンス上の理由からトークンを保存し、更新する必要があります。

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

トークン交換が同意プロンプトをトリガーできなかった場合にボットが何をするのかを理解するには、次の手順を参照してください。

>[!NOTE]
> トークン交換が失敗したときにボットがアクションを実行するので、ユーザーの操作は必要ありません。

1. クライアントは、OAuth シナリオをトリガーするボットとの会話を開始します。
2. ボットは OAuth カードをクライアントに返送します。
3. クライアントは、OAuth カードをユーザーに表示する前にインターセプトし、プロパティが含まれているかどうかを確認 `TokenExchangeResource` します。
4. プロパティが存在する場合、クライアントは `TokenExchangeInvokeRequest` ボットに送信します。 クライアントは、Azure AD v2 トークンで、対象ユーザーがプロパティと同じである必要がある、ユーザーに交換可能なトークンを持っている必要があります `TokenExchangeResource.Uri` 。 クライアントは、次のコードを使用して、呼び出しアクティビティをボットに送信します。

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

5. ボットは を処理 `TokenExchangeInvokeRequest` し、 `TokenExchangeInvokeResponse` クライアントに戻ります。 クライアントは、 を受け取るまで待つ必要があります `TokenExchangeInvokeResponse` 。

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

6. が `TokenExchangeInvokeResponse` が を持つ `status` `200` 場合、クライアントは OAuth カードを表示しません。 通常の [フロー画像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)を参照してください。 その他の場合 `status` 、または `TokenExchangeInvokeResponse` が受信されていない場合、クライアントは OAuth カードをユーザーに表示します。 フォールバック [フロー イメージ](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)を参照してください。 これにより、エラーやユーザーの同意などの未適合の依存関係が発生した場合に、SSO フローが通常の OAuthCard フローにフォールバックされます。


### <a name="update-the-auth-sample"></a>認証サンプルの更新

[認証サンプルTeams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)開き、次の手順を実行して更新します。

1. 次のコードを含めることによって、受信要求の複製を処理するように TeamsBot を更新します。

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
  
2. 更新 `appsettings.json` プログラムを使用して `botId` [、「OAuth 接続で Azure ポータルを更新](#update-the-azure-portal-with-the-oauth-connection)する 」で定義されている、パスワード、および接続名を含めます。
3. マニフェストを更新し、 `token.botframework.com` 有効なドメインリストに含まれるようにします。 詳細については、「[認証のサンプルTeams」](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)を参照してください。
4. プロファイル イメージをマニフェストに zip して、Teamsにインストールします。

## <a name="code-sample"></a>コード サンプル
|**サンプル名** | **説明** |**.NET** | 
|----------------|-----------------|--------------|
|ボット フレームワーク SDK | ボット フレームワーク SDK の使用例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
