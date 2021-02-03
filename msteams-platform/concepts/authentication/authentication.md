---
title: アプリ ユーザーの認証
description: Teams での認証とアプリでの認証の使い方について説明します。
ms.topic: conceptual
keywords: Teams 認証 OAuth SSO AAD
ms.openlocfilehash: 88b2098b7d45444cf47bebdfccc22fae772b7c22
ms.sourcegitcommit: 843da1730443ff8474a05295f60a6b376ed140da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "50073104"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Microsoft Teams でユーザーを認証する

> [!NOTE]
> モバイル クライアントでの Web ベース認証には、Microsoft Teams JavaScript SDK のバージョン 1.4.1 以降が必要です。

Azure Active Directory (AAD) で保護されたユーザー情報にアクセスし、Facebook や Twitter のようなサービスからデータにアクセスするために、アプリはそれらのプロバイダーとの信頼できる接続を確立します。 アプリがユーザー スコープで Microsoft Graph API を使用する場合は、適切な認証トークンを取得するためにユーザーを認証します。

Teams では、アプリに対して 2 つの異なる認証フローがあります。 タブ、構成ページ、またはタスク モジュールに[](~/tabs/how-to/create-tab-pages/content-page.md)埋め込まれたコンテンツ ページで、従来の Web ベースの認証フローを実行します。 アプリに会話ボットが含まれている場合は、OAuthPrompt フローと、必要に応じて Azure Bot Framework のトークン サービスを使用して、会話の一部としてユーザーを認証します。

## <a name="web-based-authentication-flow"></a>Web ベースの認証フロー

タブの Web ベースの認証[フローを](~/tabs/what-are-tabs.md)使用し、会話ボット[](~/bots/what-are-bots.md)またはメッセージング拡張機能で使用[するように選択します](~/messaging-extensions/what-are-messaging-extensions.md)。 認証を有効 [にするには、Web コンテンツ](/javascript/api/overview/msteams-client) ページで Microsoft Teams JavaScript クライアント SDK を使用します。 認証を有効にした後、タブ、構成ページ、またはタスク モジュールにコンテンツ ページを埋め込む。 Web ベースの認証フローの詳細については、以下を参照してください。

* [Teams ボットに認証を追加すると](~/bots/how-to/authentication/add-authentication.md) 、会話ボットで Web ベースの認証フローを使用する方法について説明します。
* [タブでの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)では、Teams でのタブ認証の仕組みを説明しています。 これは、タブに使用される一般的な Web ベースの認証フローを示しています。
* [タブの AAD 認証では](~/tabs/how-to/authentication/auth-tab-AAD.md) 、Teams のアプリのタブ内から AAD に接続する方法について説明します。
* [サイレント認証 AAD は、AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) を使用してアプリでサインインまたは同意のプロンプトを減らす方法について説明します。
* [.Net、C#、JavaScript、Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)は、Web ベース認証のサンプルを提供します。 [](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>会話ボットの OAuthPrompt フロー

Azure Bot Framework の OAuthPrompt で、会話ボットを使用したアプリの認証が簡単になります。 Azure Bot Framework のトークン サービスを使用して、トークンのキャッシュを支援します。

OAuthPrompt の使用の詳細については、以下を参照してください。

* [ボット認証フローの概要では](~/bots/how-to/authentication/auth-flow-bot.md) 、Teams のアプリのボット内での認証のしくみについて説明します。 これは、Teams Web、デスクトップ アプリ、およびモバイル アプリ上のボットに使用される、Web ベースではない認証フローを示しています。
* [ボット認証では](~/bots/how-to/authentication/add-authentication.md) 、Teams ボットに OAuth 認証を追加する方法について説明します。
* [.Net、C#、JavaScript、](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)または Node.jsボット認証 v3 SDK サンプルを提供します。 [](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)

## <a name="configure-the-identity-provider"></a>ID プロバイダーを構成する

アプリの認証フローに関係なく、Teams アプリと通信するために ID プロバイダーを構成します。 ほとんどのサンプルとチュートリアルでは、主に ID プロバイダーとして AAD を使用します。 ただし、この概念は ID プロバイダーに関係なく適用されます。

詳細については、「ID プロバイダー [の構成」を参照してください](~/concepts/authentication/configure-identity-provider.md)。
