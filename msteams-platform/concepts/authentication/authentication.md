---
title: アプリ ユーザーの認証
description: Teams での認証とアプリでの認証の使い方について説明します。
ms.topic: conceptual
keywords: Teams 認証 OAuth SSO AAD
ms.openlocfilehash: 33ef0c55842c495ca44495bc0653a47b147ebbfc
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995996"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Microsoft Teams でユーザーを認証する

> [!NOTE]
> モバイル クライアントでの Web ベース認証には、Microsoft Teams JavaScript SDK のバージョン 1.4.1 以降が必要です。

Azure Active Directory (AAD) によって保護されたユーザー情報にアクセスし、Facebook や Twitter のようなサービスからデータにアクセスするために、アプリはそれらのプロバイダーとの信頼できる接続を確立します。 アプリがユーザー スコープで Microsoft Graph API を使用する場合は、ユーザーを認証して適切な認証トークンを取得します。

Teams では、アプリに対して 2 つの異なる認証フローがあります。 タブ、構成ページ、またはタスク モジュールに[](~/tabs/how-to/create-tab-pages/content-page.md)埋め込まれたコンテンツ ページで、従来の Web ベース認証フローを実行します。 アプリに会話ボットが含まれている場合、OAuthPrompt フロー (およびオプションの Azure Bot Framework のトークン サービス) を使用して、会話の一部としてユーザーを認証することができます。

## <a name="web-based-authentication-flow"></a>Web ベースの認証フロー

タブに Web ベースの認証[](~/tabs/what-are-tabs.md)フローを使用し、会話型[](~/bots/what-are-bots.md)ボットまたはメッセージング拡張機能で使用[するように選択します](~/messaging-extensions/what-are-messaging-extensions.md)。 認証を [有効にするには、Web](/javascript/api/overview/msteams-client) コンテンツ ページで Microsoft Teams JavaScript クライアント SDK を使用します。 認証を有効にした後、コンテンツ ページをタブ、構成ページ、またはタスク モジュールに埋め込みます。 Web ベース認証フローの詳細については、以下を参照してください。

* [Teams ボットに認証を追加するには](~/bots/how-to/authentication/add-authentication.md) 、会話型ボットで Web ベースの認証フローを使用する方法について説明します。
* [タブでの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)では、Teams でのタブ認証の仕組みを説明しています。 これは、タブに使用される一般的な Web ベース認証フローを示しています。
* [タブ内の AAD 認証では](~/tabs/how-to/authentication/auth-tab-AAD.md) 、Teams のアプリのタブ内から AAD に接続する方法について説明します。
* [サイレント認証 AAD は、AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) を使用してアプリのサインインまたは同意のプロンプトを減らす方法について説明します。
* [.Net または C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript または ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) Node.jsは、Web ベース認証のサンプルを提供します。

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>会話ボットの OAuthPrompt フロー

Azure Bot Framework の OAuthPrompt で、会話ボットを使用したアプリの認証が簡単になります。 Azure Bot Framework のトークン サービスを利用して、トークン キャッシュをアシストします。

OAuthPrompt の使用の詳細については、以下を参照してください。

* [ボット認証フローの概要では](~/bots/how-to/authentication/auth-flow-bot.md) 、Teams のアプリでボット内で認証がどのように機能するのかについて説明します。 これは、Teams Web、デスクトップ アプリ、およびモバイル アプリ上のボットに使用される、Web ベース以外の認証フローを示しています。
* [ボット認証では](~/bots/how-to/authentication/add-authentication.md) 、Teams ボットに OAuth 認証を追加する方法について説明します。

## <a name="code-sample"></a>コード サンプル

ボット認証 v3 SDK サンプルを提供します。

| **サンプル名** | **説明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| ボット認証 | このサンプルでは、Microsoft Teams のボットでの認証を開始する方法を示します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |

## <a name="configure-the-identity-provider"></a>ID プロバイダーを構成する

アプリの認証フローに関係なく、Teams アプリと通信するために ID プロバイダーを構成します。 ほとんどのサンプルとチュートリアルでは、主に ID プロバイダーとして AAD を使用します。 ただし、この概念は ID プロバイダーに関係なく適用されます。

詳細については、「ID プロバイダー [の構成」を参照してください](~/concepts/authentication/configure-identity-provider.md)。
