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
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="89b37-104">Microsoft Teams bot でユーザーを認証する</span><span class="sxs-lookup"><span data-stu-id="89b37-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="89b37-105">Teams アプリ内で使用する必要があるサービスは多数ありますが、これらのサービスのほとんどは、サービスへのアクセスを取得するために認証と承認を必要とします。</span><span class="sxs-lookup"><span data-stu-id="89b37-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="89b37-106">サービスには、Facebook、Twitter、およびコースチームが含まれます。</span><span class="sxs-lookup"><span data-stu-id="89b37-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="89b37-107">Teams のユーザーは、Microsoft Graph を使用して Azure Active Directory (Azure AD) に格納されているユーザープロファイル情報を持っています。</span><span class="sxs-lookup"><span data-stu-id="89b37-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="89b37-108">この記事では、Azure AD を使用してこの情報にアクセスするための認証に重点を置いて説明します。</span><span class="sxs-lookup"><span data-stu-id="89b37-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="89b37-109">OAuth 2.0 は、Azure AD とその他の多くのサービスプロバイダーによって使用される、オープンスタンダードの認証です。</span><span class="sxs-lookup"><span data-stu-id="89b37-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="89b37-110">OAuth 2.0 については、Teams および Azure AD で認証を処理するための前提条件となります。</span><span class="sxs-lookup"><span data-stu-id="89b37-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="89b37-111">次の例では、最終的に Azure AD と Microsoft Graph からユーザーのプロファイル情報を読み取るという目標を持つ OAuth 2.0 暗黙的な付与フローを使用します。</span><span class="sxs-lookup"><span data-stu-id="89b37-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="89b37-112">この記事に記載されている認証フローはタブの場合とよく似ていますが、タブでは web ベースの認証フローを使用できるため、ボットはコードからの認証を必要とします。</span><span class="sxs-lookup"><span data-stu-id="89b37-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="89b37-113">この記事の概念は、モバイルプラットフォームから認証を実装する場合にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="89b37-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="89b37-114">Bot の認証フローの一般的な概要については、「 [bot での認証フロー](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="89b37-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="89b37-115">Id プロバイダーを構成する</span><span class="sxs-lookup"><span data-stu-id="89b37-115">Configuring identity providers</span></span>

<span data-ttu-id="89b37-116">Azure Active Directory を id プロバイダーとして使用する場合は、「 [id プロバイダー](~/concepts/authentication/configure-identity-provider.md)を構成する」の「OAuth 2.0 コールバック URL を構成する」の詳細な手順については、このトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="89b37-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="89b37-117">認証フローの開始</span><span class="sxs-lookup"><span data-stu-id="89b37-117">Initiate authentication flow</span></span>

<span data-ttu-id="89b37-118">認証フローは、ユーザーの操作によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="89b37-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="89b37-119">これにより、ブラウザーのポップアップブロックがトリガーされ、ユーザーが混乱する可能性があるので、自動的に認証ポップアップを開かないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="89b37-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="89b37-120">認証を開始するための UI を追加する</span><span class="sxs-lookup"><span data-stu-id="89b37-120">Add UI to start authentication</span></span>

<span data-ttu-id="89b37-121">ユーザーが必要に応じてサインインできるようにするために、bot に UI を追加します。</span><span class="sxs-lookup"><span data-stu-id="89b37-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="89b37-122">ここでは、TypeScript のサムネイルカードから実行します。</span><span class="sxs-lookup"><span data-stu-id="89b37-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="89b37-123">英雄カードには、サインイン、プロファイルの表示、サインアウトの3つのボタンが追加されました。</span><span class="sxs-lookup"><span data-stu-id="89b37-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="89b37-124">でユーザーを署名する</span><span class="sxs-lookup"><span data-stu-id="89b37-124">Sign the user in</span></span>

<span data-ttu-id="89b37-125">検証はセキュリティ上の理由と、Teams のモバイルバージョンのサポートのために実行する必要があるので、ここではコードを示しませんが、[ユーザーが [サインイン] ボタンを押したときにプロセスを開始するコードの例を以下](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)に示します。</span><span class="sxs-lookup"><span data-stu-id="89b37-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="89b37-126">検証とモバイルサポートについては、「 [bot の認証フロー](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)」で説明されています。</span><span class="sxs-lookup"><span data-stu-id="89b37-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="89b37-127">認証リダイレクト URL のドメインをマニフェストの[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)セクションに追加してください。</span><span class="sxs-lookup"><span data-stu-id="89b37-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="89b37-128">省略した場合、ログインポップアップは表示されません。</span><span class="sxs-lookup"><span data-stu-id="89b37-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="89b37-129">ユーザープロファイル情報の表示</span><span class="sxs-lookup"><span data-stu-id="89b37-129">Showing user profile information</span></span>

<span data-ttu-id="89b37-130">アクセストークンの取得は、異なる web サイト間のすべての移行と、対処する必要のあるセキュリティの問題によって困難ですが、トークンを取得すると、Azure Active Directory から情報を取得するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="89b37-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="89b37-131">Bot は、アクセストークンを使用`me`して Graph エンドポイントに呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="89b37-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="89b37-132">Graph は、ログインしたユーザーのユーザー情報で応答します。</span><span class="sxs-lookup"><span data-stu-id="89b37-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="89b37-133">応答からの情報は、ボットカードを作成して送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="89b37-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="89b37-134">ユーザーがサインインしていない場合は、メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="89b37-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="89b37-135">ユーザーをサインアウトする</span><span class="sxs-lookup"><span data-stu-id="89b37-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="89b37-136">その他のサンプル</span><span class="sxs-lookup"><span data-stu-id="89b37-136">Other samples</span></span>

<span data-ttu-id="89b37-137">Bot 認証プロセスを示すサンプルコードについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="89b37-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="89b37-138">Microsoft Teams bot 認証のサンプル</span><span class="sxs-lookup"><span data-stu-id="89b37-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
