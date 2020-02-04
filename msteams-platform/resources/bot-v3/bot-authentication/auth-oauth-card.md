---
title: Teams での認証に Azure Bot サービスを使用する
description: Azure ボット Service OAuthCard について、および認証にどのように使用するかについて説明します。
keywords: teams 認証 OAuthCard OAuth card Azure Bot サービス
ms.openlocfilehash: 0397c45b39470d97c1158b2681462038de618a39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674931"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Teams での認証に Azure Bot サービスを使用する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Azure Bot サービスの OAuthCard を使用していない場合は、ボットに認証を実装するのは複雑です。 これは、web 環境の構築、外部 OAuth プロバイダーとの統合、トークン管理、および適切なサーバー間 API 呼び出しを処理して認証フローを安全に完了することを含む、完全なスタックの課題です。 これにより、clunky エクスペリエンスで "magic numbers" の入力が必要になることがあります。

Azure Bot サービスの OAuthCard を使用すると、Teams でユーザーにサインインして外部データプロバイダーにアクセスすることが容易になります。 既に認証を実装していて、より単純なものに切り替える必要がある場合、または初めて bot サービスに認証を追加する場合は、OAuthCard を使用すると簡単に作成できます。

[認証](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)の他のトピックでは、oauthcard を使用しない認証について説明しているため、Teams での認証をより深く理解したい場合や、oauthcard を使用できないような状況がある場合は、これらのトピックを参照することもできます。

## <a name="support-for-the-oauthcard"></a>OAuthCard のサポート

現時点では、OAuthCard の使用にはいくつかの制限があります。 これには、次のものが含まれます。

* カードは[ゲストアクセス](/MicrosoftTeams/guest-access)では機能しません
* [Microsoft Teams の無料](https://products.office.com/microsoft-teams/free)では機能しません
* Bot 認証にのみ使用できます
* [Azure Bot サービス](https://azure.microsoft.com/services/bot-service/)に登録されている bot に対してのみ機能します。

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Azure Bot サービスはどのように認証を行いますか?

OAuthCard を使用した完全なドキュメントについては、「 [Azure Bot サービスによる bot への認証の追加](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0)」を参照してください。 このトピックは Azure Bot フレームワークドキュメントセットに含まれており、Teams に固有ではないことに注意してください。

次のセクションでは、Teams での OAuthCard の使用方法について説明します。

## <a name="main-benefits-for-teams-developers"></a>Teams 開発者の主な利点

OAuthCard は、以下の方法で認証に役立てることができます。

* すぐに使用できる web ベースの認証フローを提供します。 web ページを作成してホストして、外部ログインのエクスペリエンスに直接アクセスしたり、リダイレクトを提供したりする必要がなくなりました。
* エンドユーザーにとってシームレスである: Teams 内の完全なサインイン機能を完全に完了します。
* 簡単なトークン管理が含まれています。トークンストレージシステムを実装する必要がなくなりました。その代わりに、ボットサービスはトークンのキャッシュを処理し、それらのトークンをフェッチするための安全なメカニズムを提供します。
* は、完全な Sdk でサポートされています。ボットサービスの統合と使用が容易です。
* Azure AD/MSA、Facebook、Google などの一般的な OAuth プロバイダーに対して、すぐにサポートが提供されます。

## <a name="when-should-i-implement-my-own-solution"></a>どのような場合に独自のソリューションを実装する必要がありますか。

アクセストークンは機密情報なので、外部サービスに格納したくない場合があります。 この場合は、teams の[認証](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)に関する他のトピックで説明されているように、チーム内で独自のトークン管理システムとログインの処理を実装してもかまいません。

## <a name="getting-started-with-oauthcard-in-teams"></a>Teams での OAuthCard の概要

> [!NOTE]
> このガイドでは、Bot Framework v3 SDK を使用しています。 V4 の実装については、[こちら](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)を参照してください。 それ以外の場合は、[サインイン] ボタンをクリックし`validDomains`ても認証ウィンドウが表示されないため、マニフェストを作成して token.botframework.com をセクションに含める必要があります。 [アプリ Studio](~/concepts/build-and-test/app-studio-overview.md)を使用して、マニフェストを生成します。

最初に、外部認証プロバイダをセットアップするために Azure bot サービスを構成する必要があります。 詳細な手順については、「 [id プロバイダーの構成](~/concepts/authentication/configure-identity-provider.md)」を参照してください。

Azure Bot サービスを使用して認証を有効にするには、コードにこれらを追加する必要があります。

1. Teams が Bot サービス`validDomains`のログインページを埋め込むため、アプリマニフェストのセクションに token.botframework.com を含めます。
2. Bot が認証済みリソースにアクセスする必要がある場合は、ボットサービスからトークンを取得します。 トークンを使用できない場合は、外部サービスへのログインを要求しているユーザーに OAuthCard というメッセージを送信します。
3. ログイン完了アクティビティを処理します。 これにより、認証要求とトークンが、現在 bot と対話しているユーザーに関連付けられます。
4. Bot が認証済みアクション (外部 REST Api の呼び出しなど) を実行する必要があるときに、トークンを取得します。

ダイアログコードでは、次のスニペット (C#) を追加する必要があります。これは、既存のアクセストークンがあるかどうかを確認します。

```CSharp
// First ask Bot Service if it already has a token for this user
var token = await context.GetUserTokenAsync(ConnectionName).ConfigureAwait(false);
if (token != null)
{
    // use the token to do exciting things!
}
else
{
    // If Bot Service does not have a token, send an OAuth card to sign in 
    await SendOAuthCardAsync(context, (Activity)context.Activity);
}
```

アクセストークンが存在しない場合、コードは OAuthCard を含むメッセージをユーザーに送信します。

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

ログイン完了アクティビティを処理するには、次の呼び出しを処理する必要があります。

```CSharp
if (activity.Name == "signin/verifyState")
{
  // We do this so that we can pass handling to the right logic in the dialog. You can
  // set this to be whatever string you want.
  activity.Text = "loginComplete";
  await Conversation.SendAsync(activity, () => new Dialogs.RootDialog());

  return Request.CreateResponse(HttpStatusCode.OK);
}
```

ダイアログコードで、Bot 認証サービスからトークンを取得できます。

```CSharp
if (text.Contains("loginComplete"))
  {
    // Handle login completion event.
    JObject ctx = activity.Value as JObject;

    if (ctx != null)
    {
      string code = ctx["state"].ToString();

      var oauthClient = activity.GetOAuthClient();
      var token = await oauthClient.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, magicCode: code).ConfigureAwait(false);
      if (token != null)
      {
        // Make whatever API calls here you want
        await context.PostAsync($"Success! You are now signed in.");
      }
    }
  // Need to respond to the Invoke.
  return;
}
```

## <a name="using-oauthcard-with-messaging-extensions"></a>メッセージング拡張機能での OAuthCard の使用

Azure Bot サービスを使用して、メッセージング拡張機能にサードパーティのプロバイダーを接続することもできます。 このフローは bot と同じですが、OAuthCard を返すのではなく、サービスからログインプロンプトが返されます。

次のスニペット (C#) は、ログイン応答を策定する方法を示しています。

```CSharp
var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName).ConfigureAwait(false);

if (token == null)
{
  // Send the login response with the auth link.
  string link = await client.OAuthApi.GetSignInLinkAsync(activity, ConnectionName);

  response = new ComposeExtensionResponse()
  {
    ComposeExtension = new ComposeExtensionResult()
  };
  response.ComposeExtension.Type = "auth";
  response.ComposeExtension.SuggestedActions = new ComposeExtensionSuggestedAction()
  {
    Actions = new List<CardAction>()
      {
        new CardAction(ActionTypes.OpenUrl, title: "Sign into this app", value: link)
      }
    };
  return response;
}
```

上記の例では、 `GetSignInLinkAsync` `client.OAuthApi`プロパティに対して直接呼び出しを行う必要があることに注意してください。

ユーザーがログインシーケンスを正常に完了すると、サービスは、元のユーザークエリを含む別の呼び出し要求と、"マジック code" を含む状態パラメーター文字列を受け取ります。 この文字列を使用してトークンを、ユーザー ID と接続名とともにフェッチできるようになりました。

```CSharp
var query = activity.GetComposeExtensionQueryData();
JObject data = activity.Value as JObject;

var client = activity.GetOAuthClient();

// Check if the request comes with login state
if (data != null && data["state"] != null)
{
  var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, data["state"].ToString());

  // Do stuff with the token here.

}
```
