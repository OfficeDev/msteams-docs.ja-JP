---
title: サーバーを使用したボットAzure Active Directory
description: Azure AD認証Teamsボットで使用する方法について説明します。
keywords: teams 認証ボット AAD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: c3f2f7fe3eb6b10faef2b24b3212081a881d6f8f
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156520"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>ボットでユーザーをMicrosoft Teamsする

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Teams アプリ内で使用するサービスは多数あるので、サービスにアクセスするには認証と承認が必要です。 サービスには、Facebook、Twitter、およびもちろんTeams。 ユーザーはTeamsを使用して、ユーザー プロファイル情報を Azure Active Directory (Azure AD) にGraph。 この記事では、この情報にアクセスするために Azure ADを使用した認証に焦点を当てる。

OAuth 2.0 は、Azure および他の多くのサービス プロバイダーが使用する認証AD標準です。 OAuth 2.0 を理解する必要があります認証を操作するには、Teams Azure AD。 次の例では、OAuth 2.0 暗黙的な許可フローを使用して、最終的に Azure AD および Microsoft Graph からユーザーのプロファイル情報を読み取る目的で使用します。

この記事で説明する認証フローは、タブで Web ベースの認証フローを使用できる点と、ボットがコードから駆動する認証を必要とする点を除き、タブの認証フローと非常に似ています。 この記事の概念は、モバイル プラットフォームから認証を実装する場合にも役立ちます。

ボットの認証フローの概要については、「ボットの認証フロー [」を参照してください](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。

## <a name="configuring-identity-providers"></a>ID プロバイダーの構成

ID プロバイダーとして[OAuth](~/concepts/authentication/configure-identity-provider.md) 2.0 コールバック リダイレクト URL を構成する方法の詳細については、「Azure Active Directory ID プロバイダーの構成」を参照してください。

## <a name="initiate-authentication-flow"></a>認証フローの開始

認証フローは、ユーザー アクションによってトリガーされる必要があります。 これは、ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性が高いので、認証ポップアップを自動的に開く必要があります。

## <a name="add-ui-to-start-authentication"></a>認証を開始するための UI の追加

ボットに UI を追加して、必要に応じてユーザーがサインインできます。 ここでは、TypeScript のサムネイル カードから行います。

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

ヒーロー カードには、サインイン、プロファイルの表示、サインアウトの 3 つのボタンが追加されています。

## <a name="sign-the-user-in"></a>ユーザーのサインイン

セキュリティ上の理由から実行する必要がある検証とモバイル バージョンの Teams のサポートのため、コードはここに表示されませんが、ユーザーが [サインイン][](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)ボタンを押すとプロセスを開始するコードの例を次に示します。

検証とモバイル サポートについては、「ボットの [認証フロー」を参照してください](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。

認証リダイレクト URL のドメインをマニフェストのセクション [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) に必ず追加してください。 そうしない場合、ログイン ポップアップは表示されません。

## <a name="showing-user-profile-information"></a>ユーザー プロファイル情報の表示

アクセス トークンの取得は困難ですが、さまざまな Web サイト間のすべての切り替えと、対処する必要があるセキュリティの問題のため、トークンを取得すると、Azure Active Directory から情報を取得することは簡単です。 ボットは、アクセス トークンを使用してGraph `me` エンドポイントを呼び出します。 Graphしたユーザーのユーザー情報に応答します。 応答からの情報は、ボット カードを作成して送信するために使用されます。

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

ユーザーがサインインしていない場合は、サインインするように求めるメッセージが表示されます。

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

ボット認証プロセスを示すサンプル コードについては、以下を参照してください。

* [Microsoft Teamsボット認証のサンプル](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
