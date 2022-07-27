---
title: Azure Active Directory を使用したボットの認証
description: Teams での Azure AD 認証と、それをボットで使用する方法について説明します
keywords: teams 認証ボット Azure AD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 2b467f6a7b4678110dece3b54a67227df6beeaf7
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035164"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>Microsoft Teams ボットでユーザーを認証する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Teams アプリ内で使用するサービスは多数あります。これらのサービスのほとんどは、アクセスを取得するために認証と承認が必要です。 サービスには、Facebook、Twitter、Teams が含まれます。 Teams のユーザーは、Microsoft Graph を使用して Azure Active Directory に保存されたユーザー プロファイル情報を持っています。 このトピックでは、Azure AD を使用してアクセスを取得する認証について説明します。
OAuth 2.0 は、Azure AD や他の多くのサービス プロバイダーで使用される認証のオープン 標準です。 OAuth 2.0 について理解することは、Teams と Azure AD で認証を操作するための前提条件です。 次の例では、OAuth 2.0 暗黙的許可フローを使用して、最終的に Azure AD と Microsoft Graph からユーザーのプロファイル情報を読み取ります。

このトピックで説明する認証フローはタブに似ていますが、タブでは Web ベースの認証フローを使用でき、ボットではコードから認証を駆動する必要があります。 このトピックの概念は、モバイル プラットフォームからの認証を実装する場合にも役立ちます。

ボットの認証フローの一般的な概要については、ボット [の認証フロー](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)に関するトピックを参照してください。

## <a name="configuring-identity-providers"></a>ID プロバイダーの構成

Id プロバイダーとして Azure Active Directory を使用する場合の OAuth 2.0 コールバック リダイレクト URL の構成に関する詳細な手順については、ID [プロバイダー](~/concepts/authentication/configure-identity-provider.md) の構成に関するトピックを参照してください。

## <a name="initiate-authentication-flow"></a>認証フローを開始する

認証フローは、ユーザー アクションによってトリガーする必要があります。 ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性があるため、認証ポップアップを自動的に開かないでください。

## <a name="add-ui-to-start-authentication"></a>認証を開始する UI を追加する

ユーザーが必要に応じてサインインできるように、ボットに UI を追加します。 ここでは、TypeScript のサムネイル カードから実行されます。

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

ヒーロー カードに[サインイン]、[プロファイルの表示]、[サインアウト] の 3 つのボタンが追加されました。

## <a name="sign-the-user-in"></a>ユーザーのサインイン

セキュリティ上の理由とモバイル バージョンの Teams のサポートのために実行する必要がある検証のため、このコードはここには表示されませんが、 [ユーザーが [サインイン] ボタンを押したときにプロセスを開始するコードの例を次に示します](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)。

検証とモバイルサポートについては、「 [ボットの認証フロー](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)」のトピックで説明されています。

必ず、認証リダイレクト URL のドメインをマニフェストのセクションに [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 追加してください。 サインインしない場合、ポップアップは表示されません。

## <a name="showing-user-profile-information"></a>ユーザー プロファイル情報の表示

アクセス トークンの取得は、さまざまな Web サイト間のすべての切り替えと、対処する必要があるセキュリティの問題のために困難ですが、トークンを取得したら、Azure Active Directory から情報を取得するのは簡単です。 ボットは、アクセス トークンを使用して `me` Graph エンドポイントを呼び出します。 Graph は、ログインしたユーザーのユーザー情報と共に応答します。 応答からの情報は、ボット カードを構築するために使用され、送信されます。

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

ユーザーがサインインしていない場合は、サインインするように求められます。

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

ボット認証プロセスを示すサンプル コードについては、次を参照してください。

* [Microsoft Teams ボット認証サンプル](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
