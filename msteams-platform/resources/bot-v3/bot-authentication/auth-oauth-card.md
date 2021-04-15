---
title: Teams での Azure Bot Service の認証の使用
description: Azure Bot Service OAuthCard と、それが認証に使用される方法について説明します。
ms.topic: conceptual
keywords: teams 認証 OAuthCard OAuth カード Azure Bot Service
ms.openlocfilehash: 6e609daba1374f4e971e1634810d3b217ce55371
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696676"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Teams での Azure Bot Service の認証の使用

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Azure Bot Service の OAuthCard がない場合、ボットに認証を実装する方法は複雑です。 Web エクスペリエンスの構築、外部 OAuth プロバイダーとの統合、トークン管理、および認証フローを安全に完了するための適切なサーバー間 API 呼び出しの処理が含まれます。 これにより、"マジック ナンバー" の入力が必要な不格好なエクスペリエンスが発生する可能性があります。

Azure Bot Service の OAuthCard を使用すると、Teams ボットがユーザーにサインインし、外部データ プロバイダーにアクセスしやすくなります。 既に認証を実装済みで、より簡単なものに切り替える場合も、ボット サービスに初めて認証を追加する場合でも、OAuthCard を使用すると、簡単に行えます。

[認証][](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)の他のトピックでは、OAuthCard を使用せずに認証を記述します。そのため、Teams での認証を深く理解する場合や、OAuthCard を使用できない状況がある場合は、引き続きこれらのトピックを参照できます。

## <a name="support-for-the-oauthcard"></a>OAuthCard のサポート

現在、OAuthCard を使用できる場所にはいくつかの制限があります。 これには、次のものが含まれます。

* カードはゲスト アクセスでは [機能しません](/MicrosoftTeams/guest-access)
* Microsoft Teams 無料では [動作しません](https://products.office.com/microsoft-teams/free)
* ボット認証にのみ使用できます
* Azure Bot Service に登録されているボットでのみ [機能します。](https://azure.microsoft.com/services/bot-service/)

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Azure Bot Service は認証を行う上でどのように役立ちますか?

OAuthCard を使用した完全なドキュメントについては、「Azure Bot Service 経由でボットに認証を追加する [」を参照してください](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)。 このトピックは Azure Bot Framework のドキュメント セットに含まれていますが、Teams に固有のトピックではありません。

次のセクションでは、Teams で OAuthCard を使用する方法について説明します。

## <a name="main-benefits-for-teams-developers"></a>Teams 開発者の主な利点

OAuthCard は、次の方法で認証に役立ちます。

* アウトオブボックスの Web ベース認証フローを提供します。外部ログイン エクスペリエンスに移動したり、リダイレクトを提供したりするために、Web ページを作成してホストする必要がなくなりました。
* エンド ユーザーはシームレスです。Teams 内で完全なサインイン エクスペリエンスを完了します。
* 簡単なトークン管理が含まれています。トークン ストレージ システムを実装する必要がなくなりました。代わりに、Bot Service はトークンキャッシュを処理し、これらのトークンをフェッチするための安全なメカニズムを提供します。
* 完全な SDK でサポートされています。ボット サービスから簡単に統合して使用できます。
* Azure AD/MSA、Facebook、Google など、多くの一般的な OAuth プロバイダーをサポートしています。

## <a name="when-should-i-implement-my-own-solution"></a>自分のソリューションをいつ実装する必要がありますか?

アクセス トークンは機密情報であるため、外部サービスに保存する必要はありません。 この場合も、Teams 認証の他のトピックで説明するように、独自のトークン管理システムとログイン エクスペリエンスを [Teams](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) 内に実装することができます。

## <a name="getting-started-with-oauthcard-in-teams"></a>Teams での OAuthCard の使用を開始する

> [!NOTE]
> このガイドでは、Bot Framework v3 SDK を使用しています。 v4 実装は、こちらを参照 [してください](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。 それ以外の場合は [サインイン] ボタンが認証ウィンドウを開かないので、マニフェストを作成し、セクションに token.botframework.com を含める `validDomains` 必要があります。 App [Studio を使用して](~/concepts/build-and-test/app-studio-overview.md) マニフェストを生成します。

まず、外部認証プロバイダーをセットアップするように Azure ボット サービスを構成する必要があります。 詳細な [手順については、「ID プロバイダーの構成](~/concepts/authentication/configure-identity-provider.md) 」を参照してください。

Azure Bot Service を使用して認証を有効にするには、コードに次の追加を行う必要があります。

1. Teams token.botframework.com ボット サービスのログイン ページが埋め込まれるため、アプリ マニフェストのセクションにアプリ マニフェストを `validDomains` 含める必要があります。
2. ボットが認証されたリソースにアクセスする必要がある場合は常に、ボット サービスからトークンをフェッチします。 トークンが使用できない場合は、OAuthCard を含むメッセージを外部サービスへのログインを要求するユーザーに送信します。
3. ログイン完了アクティビティを処理します。 これにより、認証要求とトークンがボットと現在対話しているユーザーに関連付けられる。
4. 外部 REST API の呼び出しなど、ボットが認証されたアクションを実行する必要がある場合は常にトークンを取得します。

ダイアログ コードで、次のスニペット (C#) を追加する必要があります。これは、既存のアクセス トークンをチェックします。

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

ログイン完了アクティビティを処理するには、この Invoke を処理する必要があります。

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

ダイアログ コードで、ボット認証サービスからトークンを取得できます。

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

Azure Bot Service を使用して、サードパーティ プロバイダーをメッセージング拡張機能に接続することもできます。 フローはボットと同じですが、OAuthCard を返す代わりに、サービスはログイン プロンプトを返します。

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

上記の例では、プロパティに対して直接呼び出し `GetSignInLinkAsync` を行う必要 `client.OAuthApi` があります。

ユーザーがログイン シーケンスを正常に完了すると、サービスは元のユーザー クエリを含む別の Invoke 要求と、"マジック コード" を含む状態パラメーター文字列を受け取ります。 これで、ユーザー ID と接続名と共に、この文字列を使用してトークンをフェッチできます。

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
