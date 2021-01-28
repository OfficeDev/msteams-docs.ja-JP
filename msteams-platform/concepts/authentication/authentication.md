---
title: アプリ ユーザーの認証
description: Teams での認証と、アプリでの認証の使用方法について説明します
ms.topic: conceptual
keywords: Teams 認証 OAuth SSO AAD
ms.openlocfilehash: 6ddcd8a9e847d9216b7e2dcc12733a6cd413b48e
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014293"
---
# <a name="authenticating-users-in-microsoft-teams"></a>Microsoft Teams でのユーザーの認証

> [!Note]
> モバイル クライアントでの Web ベースの認証には、Teams JavaScript SDK のバージョン 1.4.1 以降が必要です。

アプリが Azure Active Directory で保護されたユーザー情報にアクセスしたり、Facebook や Twitter などの他のサービスからデータにアクセスしたりするには、アプリがそれらのプロバイダーとの間に信頼された接続を確立する必要があります。 アプリがユーザーのスコープ内で Microsoft Graph API を使用する必要がある場合、適切な認証トークンを取得するためにユーザーを認証する必要もあります。

Microsoft Teams には、アプリが利用できる 2 つの異なる認証フローがあります。 タブ、構成ページ、タスク モジュールに埋め込まれた[コンテンツ ページ](~/tabs/how-to/create-tab-pages/content-page.md)で、従来の Web ベースの認証フローを実行できます。 アプリに会話ボットが含まれている場合、OAuthPrompt フロー (およびオプションの Azure Bot Framework のトークン サービス) を使用して、会話の一部としてユーザーを認証することができます。

## <a name="web-based-authentication-flow"></a>Web ベースの認証フロー

[タブ](~/tabs/what-are-tabs.md)には Web ベースの認証フローを使用する必要がありますが、[会話ボット](~/bots/what-are-bots.md)や[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)との併用を選択することもできます。 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を Web コンテンツ ページで使用して認証を有効にし、次にそのコンテンツ ページを、タブ、構成ページ、タスク モジュールに埋め込みます。 Web ベースの認証フローと会話ボットを併用する場合には、[タスク モジュールとボットを併用する](~/task-modules-and-cards/task-modules/task-modules-bots.md)必要があります。

* [タブでの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)では、Teams でのタブ認証の仕組みを説明しています。 ここでは、タブに使用される一般的な Web ベースの認証フローを示しています。
* [タブでの Azure AD 認証](~/tabs/how-to/authentication/auth-tab-AAD.md)では、Teams のアプリ内のタブから Azure Active Directory に接続する方法を説明しています。
* [サイレント認証 (Azure AD)](~/tabs/how-to/authentication/auth-silent-AAD.md) では、アプリ内でのサインイン/同意プロンプトを Azure Active Directory を使用して減らす方法を説明しています。
* [dotnet/C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) または [JavaScript/Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) での Web ベースの認証

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>会話ボットの OAuthPrompt フロー

Azure Bot Framework の OAuthPrompt で、会話ボットを使用したアプリの認証が簡単になります。 Azure Bot Framework のトークン サービスを利用して、トークン キャッシュをアシストすることもできます。

OAuthPrompt の使用の詳細については、次を参照してください。

* [ボット認証フローの概要](~/bots/how-to/authentication/auth-flow-bot.md)では、Teams のアプリ内のボットでの認証の仕組みを説明しています。 ここでは、Teams のすべてのバージョン (Web、デスクトップ アプリ、モバイル アプリ) でボットに使用される非 Web ベースの認証フローを示しています。
* [ボット認証](~/bots/how-to/authentication/add-authentication.md)
* [dotnet/C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) または [JavaScript/Node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) でのボット認証 (v3 SDK) のサンプル

## <a name="configure-your-identity-provider"></a>ID プロバイダーを構成する

アプリがどちらの認証フローを使用しているかにかかわらず (両方を使用している可能性もあります)、Teams アプリと通信を行うには ID プロバイダーを構成する必要があります。 ここで紹介するサンプルやチュートリアルの大半では、主に Azure Active Directory を ID プロバイダーとして使用しています。 ただし、この概念は、どの ID プロバイダーを使用するかにかかわらず適用されます。

詳細については、「[configuring an identity provider (ID プロバイダーの構成)](~/concepts/authentication/configure-identity-provider.md)」を参照してください
