---
title: メッセージング拡張機能の SSO サポート
author: KirtiPereira
description: コード サンプルを使用してメッセージング拡張機能の SSO サポートを有効にする方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 3543d86d15755642a1617e07514db95a6a812313
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453468"
---
# <a name="single-sign-on-support-for-messaging-extensions"></a>メッセージング拡張機能のシングル サインオンのサポート

シングル サインオン (SSO) のサポートは、メッセージング拡張機能とリンク解除で利用できます。 メッセージング拡張機能のシングル サインオンを既定で有効にすると、認証トークンが更新され、Microsoft Teams のサインイン資格情報を入力する必要がある回数が最小限に抑Microsoft Teams。

このドキュメントでは、SSO を有効にして、必要に応じて認証トークンを保存する方法についてガイドします。

## <a name="prerequisites"></a>前提条件

メッセージング拡張機能とリンクの分岐解除に SSO を有効にする前提条件は次のとおりです。

* Azure アカウントが [必要](https://azure.microsoft.com/free/) です。
* Azure AD ポータルを使用してアプリを構成し、Teams ポータルを通じてアプリを登録するで定義されているボットのアプリケーション [マニフェストをAzure ADがあります](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal)。

> [!NOTE]
> Azure アカウントの作成とアプリ マニフェストの更新の詳細については、「シングル サインオン [(SSO) ボットのサポート」を参照してください](../../bots/how-to/authentication/auth-aad-sso-bots.md)。

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>メッセージング拡張機能の SSO を有効にし、リンクを解除する

前提条件が完了したら、メッセージング拡張機能の SSO を有効にし、リンクを解除できます。

SSO を有効にするには、次の方法を実行します。

1. ボットの [OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) 接続の詳細をポータルで更新Microsoft Azureします。
2. メッセージング拡張機能 [のサンプルをダウンロードし、](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) ウィザードによって提供されるセットアップ手順に従います。
   > [!NOTE]
   > メッセージング拡張機能を設定する場合は、ボットの OAuth 接続を使用します。
3. [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) ファイルで、および/またはで *auth* から *silentAuth* `OnTeamsMessagingExtensionQueryAsync` に値を更新します`OnTeamsAppBasedLinkQueryAsync`。  

    > [!NOTE]
    > TeamsMessagingExtensionsSearchAuthConfigBot.cs ファイル以外の他のハンドラー SSO `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` はサポートされていません。

4. 次に示す SSO を `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync`有効にするシナリオに応じて、ペイロード内またはペイロード内のハンドラーでトークンを受け取る。

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    OAuth 接続を使用している場合は、次のコードを TeamsMessagingExtensionsSearchAuthConfigBot.cs ファイルに追加して、トークンをストアに更新または追加します。

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

## <a name="see-also"></a>関連項目

* [メッセージング拡張機能に認証を追加する](add-authentication.md)
* [ボットに SSO を使用する](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [リンク展開](link-unfurling.md)
