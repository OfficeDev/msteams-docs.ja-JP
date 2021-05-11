---
title: サーバーを使用したボットAzure Active Directory
description: Azure AD認証Teamsボットで使用する方法について説明します。
keywords: teams 認証ボット AAD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: c3f2f7fe3eb6b10faef2b24b3212081a881d6f8f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020689"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="a1b84-104">ボットでユーザーをMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="a1b84-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="a1b84-105">Teams アプリ内で使用するサービスは多数あるので、サービスにアクセスするには認証と承認が必要です。</span><span class="sxs-lookup"><span data-stu-id="a1b84-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="a1b84-106">サービスには、Facebook、Twitter、およびもちろんTeams。</span><span class="sxs-lookup"><span data-stu-id="a1b84-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="a1b84-107">ユーザーはTeamsを使用して、ユーザー プロファイル情報を Azure Active Directory (Azure AD) にGraph。</span><span class="sxs-lookup"><span data-stu-id="a1b84-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="a1b84-108">この記事では、この情報にアクセスするために Azure ADを使用した認証に焦点を当てる。</span><span class="sxs-lookup"><span data-stu-id="a1b84-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="a1b84-109">OAuth 2.0 は、Azure および他の多くのサービス プロバイダーが使用する認証AD標準です。</span><span class="sxs-lookup"><span data-stu-id="a1b84-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="a1b84-110">OAuth 2.0 を理解する必要があります認証を操作するには、Teams Azure AD。</span><span class="sxs-lookup"><span data-stu-id="a1b84-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="a1b84-111">次の例では、OAuth 2.0 暗黙的な許可フローを使用して、最終的に Azure AD および Microsoft Graph からユーザーのプロファイル情報を読み取る目的で使用します。</span><span class="sxs-lookup"><span data-stu-id="a1b84-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="a1b84-112">この記事で説明する認証フローは、タブで Web ベースの認証フローを使用できる点と、ボットがコードから駆動する認証を必要とする点を除き、タブの認証フローと非常に似ています。</span><span class="sxs-lookup"><span data-stu-id="a1b84-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="a1b84-113">この記事の概念は、モバイル プラットフォームから認証を実装する場合にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a1b84-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="a1b84-114">ボットの認証フローの概要については、「ボットの認証フロー [」を参照してください](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="a1b84-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="a1b84-115">ID プロバイダーの構成</span><span class="sxs-lookup"><span data-stu-id="a1b84-115">Configuring identity providers</span></span>

<span data-ttu-id="a1b84-116">ID プロバイダーとして[OAuth](~/concepts/authentication/configure-identity-provider.md) 2.0 コールバック リダイレクト URL を構成する方法の詳細については、「Azure Active Directory ID プロバイダーの構成」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a1b84-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="a1b84-117">認証フローの開始</span><span class="sxs-lookup"><span data-stu-id="a1b84-117">Initiate authentication flow</span></span>

<span data-ttu-id="a1b84-118">認証フローは、ユーザー アクションによってトリガーされる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1b84-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="a1b84-119">これは、ブラウザーのポップアップ ブロックをトリガーし、ユーザーを混乱させる可能性が高いので、認証ポップアップを自動的に開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1b84-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="a1b84-120">認証を開始するための UI の追加</span><span class="sxs-lookup"><span data-stu-id="a1b84-120">Add UI to start authentication</span></span>

<span data-ttu-id="a1b84-121">ボットに UI を追加して、必要に応じてユーザーがサインインできます。</span><span class="sxs-lookup"><span data-stu-id="a1b84-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="a1b84-122">ここでは、TypeScript のサムネイル カードから行います。</span><span class="sxs-lookup"><span data-stu-id="a1b84-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="a1b84-123">ヒーロー カードには、サインイン、プロファイルの表示、サインアウトの 3 つのボタンが追加されています。</span><span class="sxs-lookup"><span data-stu-id="a1b84-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="a1b84-124">ユーザーのサインイン</span><span class="sxs-lookup"><span data-stu-id="a1b84-124">Sign the user in</span></span>

<span data-ttu-id="a1b84-125">セキュリティ上の理由から実行する必要がある検証とモバイル バージョンの Teams のサポートのため、コードはここに表示されませんが、ユーザーが [サインイン][](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)ボタンを押すとプロセスを開始するコードの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a1b84-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="a1b84-126">検証とモバイル サポートについては、「ボットの [認証フロー」を参照してください](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="a1b84-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="a1b84-127">認証リダイレクト URL のドメインをマニフェストのセクション [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) に必ず追加してください。</span><span class="sxs-lookup"><span data-stu-id="a1b84-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="a1b84-128">そうしない場合、ログイン ポップアップは表示されません。</span><span class="sxs-lookup"><span data-stu-id="a1b84-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="a1b84-129">ユーザー プロファイル情報の表示</span><span class="sxs-lookup"><span data-stu-id="a1b84-129">Showing user profile information</span></span>

<span data-ttu-id="a1b84-130">アクセス トークンの取得は困難ですが、さまざまな Web サイト間のすべての切り替えと、対処する必要があるセキュリティの問題のため、トークンを取得すると、Azure Active Directory から情報を取得することは簡単です。</span><span class="sxs-lookup"><span data-stu-id="a1b84-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="a1b84-131">ボットは、アクセス トークンを使用してGraph `me` エンドポイントを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a1b84-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="a1b84-132">Graphしたユーザーのユーザー情報に応答します。</span><span class="sxs-lookup"><span data-stu-id="a1b84-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="a1b84-133">応答からの情報は、ボット カードを作成して送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a1b84-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="a1b84-134">ユーザーがサインインしていない場合は、サインインするように求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a1b84-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="a1b84-135">ユーザーをサインアウトする</span><span class="sxs-lookup"><span data-stu-id="a1b84-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="a1b84-136">その他のサンプル</span><span class="sxs-lookup"><span data-stu-id="a1b84-136">Other samples</span></span>

<span data-ttu-id="a1b84-137">ボット認証プロセスを示すサンプル コードについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a1b84-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="a1b84-138">Microsoft Teamsボット認証のサンプル</span><span class="sxs-lookup"><span data-stu-id="a1b84-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
