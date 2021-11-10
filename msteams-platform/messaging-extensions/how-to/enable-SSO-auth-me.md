---
title: メッセージング拡張機能の SSO サポート
author: KirtiPereira
description: コード サンプルを使用してメッセージング拡張機能の SSO サポートを有効にする方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: cccd27f5507125d0525c5a2d180379dad213dcae
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889392"
---
# <a name="single-sign-on-support-for-messaging-extensions"></a>メッセージング拡張機能のシングル サインオンのサポート
 
シングル サインオン (SSO) のサポートは、メッセージング拡張機能とリンク解除で利用できます。 メッセージング拡張機能のシングル サインオンを既定で有効にすると、認証トークンが更新され、Microsoft Teams のサインイン資格情報を入力する必要がある回数が最小限に抑Microsoft Teams。

このドキュメントでは、SSO を有効にして、必要に応じて認証トークンを保存する方法についてガイドします。

## <a name="prerequisites"></a>前提条件

メッセージング拡張機能とリンクの分岐解除に SSO を有効にする前提条件は次のとおりです。
* Azure アカウントが [必要](https://azure.microsoft.com/free/) です。
* AAD ポータルを使用してアプリを構成し、Teams ポータルを使用してアプリを登録するで定義されているボットのアプリケーション マニフェストAAD[する必要があります](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)。

> [!NOTE]
> Azure アカウントの作成とアプリ マニフェストの更新の詳細については、「ボットのシングル サインオン [(SSO) サポート」を参照してください](../../bots/how-to/authentication/auth-aad-sso-bots.md)。

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>メッセージング拡張機能の SSO を有効にし、リンクを解除する

前提条件が完了したら、メッセージング拡張機能の SSO を有効にし、リンクを解除できます。

**SSO を有効にするには**
1. Azure portal で [ボットの OAuth 接続](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) の詳細を更新します。
2. メッセージング拡張機能 [のサンプルをダウンロードし、](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) ウィザードによって提供されるセットアップ手順に従います。
   > [!NOTE]
   > メッセージング拡張機能を設定する場合は、ボットの OAuth 接続を使用します。
3. [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs)ファイルで、および/またはで *auth* から *silentAuth* に値を `OnTeamsMessagingExtensionQueryAsync` 更新します `OnTeamsAppBasedLinkQueryAsync` 。  

    > [!NOTE]
    > `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` TeamsMessagingExtensionsSearchAuthConfigBot.cs ファイル以外の他のハンドラー SSO はサポートされていません。
   
4. 次に示す SSO を有効にするシナリオに応じて、ペイロード内またはペイロード内のハンドラーでトークン `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` を受け取る。

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
                tokenExchangeResponse = await (turnContext.Adapter as IExtendedUserTokenProvider).ExchangeTokenAsync(
                 turnContext,
                 _connectionName,
                 turnContext.Activity.From.Id,
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
