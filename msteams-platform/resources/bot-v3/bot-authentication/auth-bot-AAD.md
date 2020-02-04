---
title: Azure Active Directory を使用したボットの認証
description: Teams での Azure AD 認証と bot での使用方法について説明します。
keywords: teams 認証ボット AAD
ms.date: 03/01/2018
ms.openlocfilehash: 268af02c51b21b65214bce4673b54ac564a125ae
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674930"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Microsoft Teams bot でユーザーを認証する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Teams アプリ内で使用する必要があるサービスは多数ありますが、これらのサービスのほとんどは、サービスへのアクセスを取得するために認証と承認を必要とします。 サービスには、Facebook、Twitter、およびコースチームが含まれます。 Teams のユーザーは、Microsoft Graph を使用して Azure Active Directory (Azure AD) に格納されているユーザープロファイル情報を持っています。 この記事では、Azure AD を使用してこの情報にアクセスするための認証に重点を置いて説明します。

OAuth 2.0 は、Azure AD とその他の多くのサービスプロバイダーによって使用される、オープンスタンダードの認証です。 OAuth 2.0 については、Teams および Azure AD で認証を処理するための前提条件となります。 次の例では、最終的に Azure AD と Microsoft Graph からユーザーのプロファイル情報を読み取るという目標を持つ OAuth 2.0 暗黙的な付与フローを使用します。

この記事に記載されている認証フローはタブの場合とよく似ていますが、タブでは web ベースの認証フローを使用できるため、ボットはコードからの認証を必要とします。 この記事の概念は、モバイルプラットフォームから認証を実装する場合にも役立ちます。

Bot の認証フローの一般的な概要については、「 [bot での認証フロー](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)」を参照してください。

## <a name="configuring-identity-providers"></a>Id プロバイダーを構成する

Azure Active Directory を id プロバイダーとして使用する場合は、「 [id プロバイダー](~/concepts/authentication/configure-identity-provider.md)を構成する」の「OAuth 2.0 コールバック URL を構成する」の詳細な手順については、このトピックを参照してください。

## <a name="initiate-authentication-flow"></a>認証フローの開始

認証フローは、ユーザーの操作によってトリガーされます。 これにより、ブラウザーのポップアップブロックがトリガーされ、ユーザーが混乱する可能性があるので、自動的に認証ポップアップを開かないようにする必要があります。

## <a name="add-ui-to-start-authentication"></a>認証を開始するための UI を追加する

ユーザーが必要に応じてサインインできるようにするために、bot に UI を追加します。 ここでは、TypeScript のサムネイルカードから実行します。

```typescript
// Show prompt of options
protected async promptForAction(session: builder.Session): Promise<void> {
    let msg = new builder.Message(session)
        .addAttachment(new builder.ThumbnailCard(session)
            .title(this.providerDisplayName)
            .buttons([
                 builder.CardAction.messageBack(session, "{}", "Sign in")
                     .text("SignIn")
                     .displayText("Sign in"),
                  builder.CardAction.messageBack(session, "{}", "Show profile")
                     .text("ShowProfile")
                     .displayText("Show profile"),
                  builder.CardAction.messageBack(session, "{}", "Sign out")
                     .text("SignOut")
                     .displayText("Sign out"),
            ]));
    session.send(msg);
}
```

英雄カードには、サインイン、プロファイルの表示、サインアウトの3つのボタンが追加されました。

## <a name="sign-the-user-in"></a>でユーザーを署名する

検証はセキュリティ上の理由と、Teams のモバイルバージョンのサポートのために実行する必要があるので、ここではコードを示しませんが、[ユーザーが [サインイン] ボタンを押したときにプロセスを開始するコードの例を以下](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)に示します。

検証とモバイルサポートについては、「 [bot の認証フロー](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)」で説明されています。

認証リダイレクト URL のドメインをマニフェストの[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)セクションに追加してください。 省略した場合、ログインポップアップは表示されません。

## <a name="showing-user-profile-information"></a>ユーザープロファイル情報の表示

アクセストークンの取得は、異なる web サイト間のすべての移行と、対処する必要のあるセキュリティの問題によって困難ですが、トークンを取得すると、Azure Active Directory から情報を取得するのは簡単です。 Bot は、アクセストークンを使用`me`して Graph エンドポイントに呼び出しを行います。 Graph は、ログインしたユーザーのユーザー情報で応答します。 応答からの情報は、ボットカードを作成して送信するために使用されます。

```typescript
// Show user profile
protected async showUserProfile(session: builder.Session): Promise<void> {
    let azureADApi = this.authProvider as AzureADv1Provider;
    let userToken = this.getUserToken(session);

    if (userToken) {
        let profile = await azureADApi.getProfileAsync(userToken.accessToken);
        let profileCard = new builder.ThumbnailCard()
            .title(profile.displayName)
            .subtitle(profile.mail)
            .text(`${profile.jobTitle}<br/> ${profile.officeLocation}`);
        session.send(new builder.Message().addAttachment(profileCard));
    } else {
        session.send("Please sign in to AzureAD so I can access your profile.");
    }

    await this.promptForAction(session);
}

// Helper function to make the Graph API call
public async getProfileAsync(accessToken: string): Promise<any> {
    let options = {
        url: "https://graph.microsoft.com/v1.0/me",
        json: true,
        headers: {
            "Authorization": `Bearer ${accessToken}`,
        },
    };
    return await request.get(options);
}
```

ユーザーがサインインしていない場合は、メッセージが表示されます。

## <a name="sign-the-user-out"></a>ユーザーをサインアウトする

```typescript
// Handle user logout request
private async handleLogout(session: builder.Session): Promise<void> {
    if (!utils.getUserToken(session, this.providerName)) {
        session.send(`You're already signed out of ${this.providerDisplayName}.`);
    } else {
        utils.setUserToken(session, this.providerName, null);
        session.send(`You're now signed out of ${this.providerDisplayName}.`);
    }

    await this.promptForAction(session);
}
```

## <a name="other-samples"></a>その他のサンプル

Bot 認証プロセスを示すサンプルコードについては、以下を参照してください。

* [Microsoft Teams bot 認証のサンプル](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
