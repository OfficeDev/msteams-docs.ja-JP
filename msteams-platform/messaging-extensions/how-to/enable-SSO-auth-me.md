---
title: メッセージ拡張機能の SSO サポート
author: KirtiPereira
description: この記事では、コード サンプルを使用してメッセージング拡張機能のシングル サインオン (SSO) サポートを有効にする方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: e891e147d4cc3216b6c2acb686505dd03353b385
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189858"
---
# <a name="single-sign-on-support-for-message-extensions"></a>メッセージ拡張機能のシングル サインオンのサポート

シングル サインオン (SSO) のサポートが、メッセージ拡張機能とリンク解除で使用できるようになりました。メッセージ拡張機能のシングル サインオンを既定で有効にすると、認証トークンが更新され、Microsoft Teams のサインイン資格情報を入力する必要がある回数が最小限に抑えられます。

このドキュメントでは、SSO を有効にして、必要に応じて認証トークンを格納する方法について説明します。

## <a name="prerequisites"></a>前提条件

メッセージ拡張機能とリンクの展開に対して SSO を有効にする前提条件は次のとおりです。

* [Azure](https://azure.microsoft.com/free/) アカウントが必要です。
* Azure AD ポータルを使用してアプリを構成し、[Azure AD ポータルを使用してアプリを登録する](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal)際に定義されているとおりに Teams アプリケーション マニフェストを更新する必要があります。

> [!NOTE]
> Azure アカウントの作成とアプリ マニフェストの更新の詳細については、 [ボットのシングル サインオン (SSO) のサポート](../../bots/how-to/authentication/auth-aad-sso-bots.md)に関するページを参照してください。

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>メッセージ拡張機能の SSO を有効にし、リンクの展開を解除する

前提条件が完了したら、メッセージ拡張機能の SSO とリンク解除を有効にすることができます。

SSO を有効にするには:

1. Microsoft Azure ポータルでボットの [OAuth 接続](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection)の詳細を更新します。
2. [メッセージ拡張機能のサンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)をダウンロードし、ウィザードによって提供されるセットアップ手順に従います。
   > [!NOTE]
   > メッセージ拡張機能を設定するときは、ボットの OAuth 接続を使用します。
3. [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) ファイルで、`OnTeamsMessagingExtensionQueryAsync` または `OnTeamsAppBasedLinkQueryAsync` の値を *auth* から *silentAuth* に更新します。  

    > [!NOTE]
    > TeamsMessagingExtensionsSearchAuthConfigBot.cs ファイルの `OnTeamsMessagingExtensionQueryAsync` と `OnTeamsAppBasedLinkQueryAsync` を除いて、他のハンドラー SSO はサポートされていません。

4. 次の場合に `OnTeamsMessagingExtensionQueryAsync` SSO を有効にするシナリオに応じて、ペイロードまたはペイロード内のハンドラー `turnContext.Activity.Value` で `OnTeamsAppBasedLinkQueryAsync`トークンを受け取ります。

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    OAuth 接続を使用している場合は、TeamsMessagingExtensionsSearchAuthConfigBot.cs ファイルに次のコードを追加して、ストア内のトークンを更新または追加します。

   ```C#
   protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
            if (valueObject["authentication"] != null)
            {
                JObject authenticationObject = JObject.FromObject(valueObject["authentication"]);
                if (authenticationObject["token"] != null)
                {
                    //If the token is NOT exchangeable, then return 412 to require user consent
                    if (await TokenIsExchangeable(turnContext, cancellationToken))
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
                    }
                    else
                    {
                        var response = new InvokeResponse();
                        response.Status = 412;
                        return response;
                    }
                }
            }
            return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
        }
        private async Task<bool> TokenIsExchangeable(ITurnContext turnContext, CancellationToken cancellationToken)
        {
            TokenResponse tokenExchangeResponse = null;
            try
            {
                JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
                var tokenExchangeRequest =
                ((JObject)valueObject["authentication"])?.ToObject<TokenExchangeInvokeRequest>();
                var userTokenClient = turnContext.TurnState.Get<UserTokenClient>();
                tokenExchangeResponse = await userTokenClient.ExchangeTokenAsync(
                                turnContext.Activity.From.Id,
                                 _connectionName,
                                 turnContext.Activity.ChannelId,
                                 new TokenExchangeRequest
                 {
                     Token = tokenExchangeRequest.Token,
                 },
                  cancellationToken).ConfigureAwait(false);
            }
    #pragma warning disable CA1031 //Do not catch general exception types (ignoring, see comment below)
            catch
    #pragma warning restore CA1031 //Do not catch general exception types
            {
                //ignore exceptions
                //if token exchange failed for any reason, tokenExchangeResponse above remains null, and a failure invoke response is sent to the caller.
                //This ensures the caller knows that the invoke has failed.
            }
            if (tokenExchangeResponse == null || string.IsNullOrEmpty(tokenExchangeResponse.Token))
            {
                return false;
            }
            return true;
        }
    
    ```

## <a name="code-sample"></a>コード サンプル

このセクションでは、Bot 認証 v3 SDK サンプルを提供します。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| ボット認証 | このサンプルでは、Teams用のボットで認証を開始する方法を示します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| タブ、ボット、メッセージ拡張機能 (ME) SSO | このサンプルでは、Tab、Bot、ME の SSO (検索、アクション、リンクの展開) を示します。 |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 利用不可 |

## <a name="see-also"></a>関連項目

* [メッセージ拡張機能に認証を追加する](add-authentication.md)
* [ボットに SSO を使用する](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [リンク展開](link-unfurling.md)
