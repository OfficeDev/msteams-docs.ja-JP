---
title: アプリ ユーザーの認証
description: アプリでの認証Teamsおよびアプリで使用する方法について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams 認証 OAuth SSO AAD
ms.openlocfilehash: 40d5659251b1faff087c6ee6458800ede2a5c840
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156681"
---
# <a name="authenticate-users-in-microsoft-teams"></a>ユーザーを認証Microsoft Teams

> [!Note]
> モバイル クライアントでの Web ベース認証には、JavaScript クライアント SDK のバージョン 1.4.1 以降Teams必要です。

Azure Active Directory (AAD) で保護されたユーザー情報にアクセスし、Facebook や Twitter のようなサービスからデータにアクセスするために、アプリはそれらのプロバイダーとの信頼できる接続を確立します。 アプリがユーザー スコープで Microsoft Graph API を使用する場合は、適切な認証トークンを取得するためにユーザーを認証します。

このTeams、アプリには 2 つの異なる認証フローがあります。 タブ、構成ページ、またはタスク モジュールに[](~/tabs/how-to/create-tab-pages/content-page.md)埋め込まれたコンテンツ ページで、従来の Web ベース認証フローを実行します。 アプリに会話ボットが含まれている場合、OAuthPrompt フロー (およびオプションの Azure Bot Framework のトークン サービス) を使用して、会話の一部としてユーザーを認証することができます。

## <a name="web-based-authentication-flow"></a>Web ベースの認証フロー

タブに Web ベースの認証[](~/tabs/what-are-tabs.md)フローを使用し、会話型[](~/bots/what-are-bots.md)ボットまたはメッセージング拡張機能で使用[するように選択します](~/messaging-extensions/what-are-messaging-extensions.md)。 Web コンテンツ[ページMicrosoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)を使用して認証を有効にします。 認証を有効にした後、コンテンツ ページをタブ、構成ページ、またはタスク モジュールに埋め込みます。 Web ベース認証フローの詳細については、以下を参照してください。

* [スレッド ボットに認証Teams、](~/bots/how-to/authentication/add-authentication.md)会話型ボットで Web ベースの認証フローを使用する方法について説明します。
* [タブでの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)では、Teams でのタブ認証の仕組みを説明しています。 これは、タブに使用される一般的な Web ベース認証フローを示しています。
* [タブ内の AAD 認証では](~/tabs/how-to/authentication/auth-tab-AAD.md)、アプリ内のタブ内から AAD に接続するTeams。
* [サイレント認証 AAD は、AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) を使用してアプリのサインインまたは同意のプロンプトを減らす方法について説明します。
* [.Net または C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript または ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) Node.jsは、Web ベース認証のサンプルを提供します。

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>会話ボットの OAuthPrompt フロー

Azure Bot Framework の OAuthPrompt で、会話ボットを使用したアプリの認証が簡単になります。 Azure Bot Framework のトークン サービスを利用して、トークン キャッシュをアシストします。

OAuthPrompt の使用の詳細については、以下を参照してください。

* [ボット認証フローの概要では](~/bots/how-to/authentication/auth-flow-bot.md)、アプリ内のボット内で認証がどのように機能Teams。 これは、Web、デスクトップ アプリ、モバイル アプリのボットに使用Teams Web ベース以外の認証フローを示しています。
* [ボット認証では](~/bots/how-to/authentication/add-authentication.md)、OAuth 認証をボットに追加するTeams説明します。

## <a name="code-sample"></a>コード サンプル

ボット認証 v3 SDK サンプルを提供します。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| ボット認証 | このサンプルは、ボットで認証を開始する方法を示Microsoft Teams。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| タブ、ボット、メッセージング拡張機能 (ME) SSO | このサンプルでは、Tab、Bot、ME - 検索、アクション、linkunfurl の SSO を示します。 |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 使用不可 |


## <a name="configure-the-identity-provider"></a>ID プロバイダーを構成する

アプリの認証フローに関係なく、ID プロバイダーがアプリと通信Teamsします。 ほとんどのサンプルとチュートリアルでは、主に ID プロバイダーとして AAD を使用します。 ただし、概念は ID プロバイダーに関係なく適用されます。

詳細については、「ID プロバイダー [の構成」を参照してください](~/concepts/authentication/configure-identity-provider.md)。
