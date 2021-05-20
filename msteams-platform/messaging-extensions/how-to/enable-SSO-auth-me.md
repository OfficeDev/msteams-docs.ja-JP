---
title: メッセージング拡張機能の SSO サポート
author: KirtiPereira
description: メッセージング拡張機能の SSO サポートを有効にする方法
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 02d08506a07e955693531908f4f3cf16573a02c0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566202"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a>メッセージング拡張機能のシングル サインオン (SSO) サポート
 
シングル サインオンのサポートは、メッセージング拡張機能とリンクの展開で使用できるようになりました。 メッセージング拡張機能のシングル サインオン (SSO) を有効にすると、認証トークンがサイレントモードで更新されるため、Microsoft Teamsにサインイン資格情報を入力する必要がある回数が最小限に抑えられます。

このドキュメントでは、SSO を有効にし、必要に応じて認証トークンを保存する方法について説明します。

## <a name="prerequisites"></a>前提条件

メッセージング拡張機能およびリンクの展開に対して SSO を有効にする前提条件は次のとおりです。
* [Azure](https://azure.microsoft.com/en-us/free/)アカウントが必要です。
* AAD ポータルを使用してアプリを構成し[、AAD ポータルを通じてアプリを登録](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)するに定義されているとおりに、ボットのTeams アプリケーション マニフェストを更新する必要があります。

> [!NOTE]
> Azure アカウントの作成とアプリ マニフェストの更新の詳細については、「 [ボットのシングル サインオン (SSO) サポート](../../bots/how-to/authentication/auth-aad-sso-bots.md)」を参照してください。

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>メッセージング拡張機能およびリンクの展開に対して SSO を有効にする

前提条件が完了したら、メッセージング拡張機能およびリンクの展開に対して SSO を有効にできます。

**SSO を有効にするには**
1. Azure ポータルでボット [OAuth 接続](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) の詳細を更新します。
2. [メッセージング拡張機能のサンプルを](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)ダウンロードし、ウィザードのセットアップ手順に従います。
   > [!NOTE]
   > メッセージング拡張機能を設定する際に、ボット OAuth 接続を使用します。
3. ファイルで[.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs)ファイルで、および/または .  `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync`  

    > [!NOTE]
    > 他のハンドラー SSO はサポートされていませんが、 `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` チーム メッセージングエクステンションサーチオーポフィ.csファイルを除きます。
   
4. `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` SSO を有効にするシナリオに応じて、ペイロードまたは のハンドラーでトークンを受け取 `OnTeamsAppBasedLinkQueryAsync` ります。

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    OAuth 接続を使用している場合は、ストア内のトークンを更新または追加する.csファイルに次のコードを追加します。
    
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

