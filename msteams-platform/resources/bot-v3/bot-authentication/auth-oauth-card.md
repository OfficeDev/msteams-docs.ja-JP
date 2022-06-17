---
title: Teamsでの認証に Azure Bot Serviceを使用する
description: Azure Bot Service OAuthCard と認証に使用する方法について説明します
ms.topic: conceptual
localization_priority: Normal
keywords: teams authentication OAuthCard OAuth カード Azure Bot Service
ms.openlocfilehash: 7731e4d1148e50c748d9c5e1b55371628a78dea7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143166"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Teamsでの認証に Azure Bot Serviceを使用する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Azure Bot Serviceの OAuthCard がなければ、ボットに認証を実装するのは複雑です。 Web エクスペリエンスの構築、外部 OAuth プロバイダーとの統合、トークン管理、適切なサーバー間 API 呼び出しの処理を行って認証フローを安全に完了することは、フルスタックの課題です。 これにより、"マジック ナンバー" の入力が必要な不器用なエクスペリエンスが発生する可能性があります。

Azure Bot Serviceの OAuthCard を使用すると、Teams ボットがユーザーにサインインし、外部データ プロバイダーにアクセスしやすくなります。 認証を既に実装していて、よりシンプルなものに切り替えたい場合でも、初めてボット サービスに認証を追加する場合でも、OAuthCard を使うと簡単になります。

[認証](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)の他のトピックでは、OAuthCard を使用せずに認証について説明しているため、Teamsの認証をより深く理解したい場合や、OAuthCard を使用できない状況がある場合でも、これらのトピックを参照できます。

## <a name="support-for-the-oauthcard"></a>OAuthCard のサポート

現在、OAuthCard を使用できる場所にはいくつかの制限があります。 これには、次のものが含まれます。

* カードは [ゲスト アクセス](/MicrosoftTeams/guest-access)では機能しません。
* [Microsoft Teams 無料版](https://products.office.com/microsoft-teams/free)では機能しません。
* ボット認証にのみ使用できます。
* これは、[Azure Bot Service](https://azure.microsoft.com/services/bot-service/)に登録されているボットでのみ機能します。

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Azure Bot Serviceはどのように認証を行うのに役立ちますか?

OAuthCard を使用した完全なドキュメントについては、「[Azure Bot Serviceを使用してボットに認証を追加する](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)」を参照してください。 このトピックは Azure Bot Framework ドキュメント セットに含まれており、Teamsに固有のものではありません。

以降のセクションでは、Teamsで OAuthCard を使用する方法について説明します。

## <a name="main-benefits-for-teams-developers"></a>Teams開発者にとっての主な利点

OAuthCard は、次の方法で認証に役立ちます。

* すぐに使用できる Web ベースの認証フローを提供します。外部ログイン エクスペリエンスに誘導したり、リダイレクトを提供したりするために Web ページを記述してホストする必要がなくなりました。
* エンド ユーザーにとってシームレスです。Teams内で完全なサインイン エクスペリエンスを完了します。
* 簡単なトークン管理が含まれています。トークン ストレージ システムを実装する必要がなくなりました。代わりに、Bot Serviceはトークン キャッシュを処理し、トークンをフェッチするための安全なメカニズムを提供します。
* 完全な SDK でサポートされています。ボット サービスから簡単に統合して使用できます。
* Azure AD/MSA、Facebook、Google など、多くの一般的な OAuth プロバイダーをすぐにサポートしています。

## <a name="when-should-i-implement-my-own-solution"></a>自分のソリューションを実装する必要があるのはいつですか?

アクセス トークンは機密情報であるため、外部サービスに格納したくない場合があります。 この場合、Teams[認証](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)に関するトピックの残りの部分で説明されているように、Teams内で独自のトークン管理システムとログイン エクスペリエンスを引き続き実装することもできます。

## <a name="getting-started-with-oauthcard-in-teams"></a>Teamsでの OAuthCard の概要

> [!NOTE]
> このガイドでは、Bot Framework v3 SDK を使用しています。 v4 の実装 [については、こちらを参照してください](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。 マニフェストを作成し、セクションに token.botframework.com を `validDomains` 含める必要があります。そうしないと、[サインイン] ボタンが認証ウィンドウを開かないためです。 [App Studio を](~/concepts/build-and-test/app-studio-overview.md)使用してマニフェストを生成します。

最初に、外部認証プロバイダーを設定するように Azure ボット サービスを構成する必要があります。 詳細な手順については、「 [ID プロバイダーの構成](~/concepts/authentication/configure-identity-provider.md) 」を参照してください。

Azure Bot Serviceを使用して認証を有効にするには、コードに次の追加を行う必要があります。

1. TeamsはBot Serviceのログイン ページを`validDomains`埋め込むため、アプリ マニフェストのセクションに token.botframework.com を含めます。
2. ボットが認証されたリソースにアクセスする必要がある場合は、Bot Serviceからトークンをフェッチします。 使用可能なトークンがない場合は、OAuthCard を含むメッセージをユーザーに送信し、外部サービスへのログインを要求します。
3. ログイン完了アクティビティを処理します。 これにより、認証要求とトークンが、ボットと現在対話しているユーザーに関連付けられます。
4. ボットが認証されたアクション (外部 REST API の呼び出しなど) を実行する必要がある場合は、必ずトークンを取得します。

ダイアログ コードで、既存のアクセス トークンを確認する次のスニペット (C#) を追加する必要があります。

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

アクセス トークンが存在しない場合、コードは OAuthCard を含むメッセージをユーザーに送信します。

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

ダイアログ コードで、Bot 認証サービスからトークンを取得できます。

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

Azure Bot Serviceを使用して、サード パーティのプロバイダーをメッセージング拡張機能に接続することもできます。 フローはボットと同じですが、OAuthCard を返す代わりに、サービスはログイン プロンプトを返します。

次のスニペット (C#) は、ログイン応答を作成する方法を示しています。

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

上記の例では、プロパティに対して`client.OAuthApi`直接呼び出しを`GetSignInLinkAsync`行う必要があることに注意してください。

ユーザーがログイン シーケンスを正常に完了すると、サービスは、元のユーザー クエリを含む別の Invoke 要求と、"マジック コード" を含む状態パラメーター文字列を受け取ります。 この文字列と、ユーザー ID と接続名を使用してトークンをフェッチできるようになりました。

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
