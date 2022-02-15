---
title: アプリ ユーザーの認証
description: アプリでの認証Teamsおよびアプリで使用する方法について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 認証 OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 79b50b8e2ba91d8b141cb36b38f0d94713131d43
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821361"
---
# <a name="authenticate-users-in-microsoft-teams"></a>ユーザーを認証Microsoft Teams

> [!Note]
> モバイル クライアントでの Web ベース認証には、JavaScript クライアント SDK のバージョン 1.4.1 以降Teams必要です。

アプリは、Facebook や Twitter Azure ADサービスからデータにアクセスするために、ユーザーによって保護されたユーザー情報にアクセスするために、これらのプロバイダーとの信頼できる接続を確立します。 アプリがユーザー スコープで Microsoft Graph API を使用する場合は、適切な認証トークンを取得するためにユーザーを認証します。

このTeams、アプリには 2 つの異なる認証フローがあります。 タブ、構成ページ、またはタスク モジュールに埋[](~/tabs/how-to/create-tab-pages/content-page.md)め込まれたコンテンツ ページで、従来の Web ベース認証フローを実行します。 アプリに会話ボットが含まれている場合、OAuthPrompt フロー (およびオプションの Azure Bot Framework のトークン サービス) を使用して、会話の一部としてユーザーを認証することができます。

## <a name="web-based-authentication-flow"></a>Web ベースの認証フロー

タブに Web ベースの認証[フローを使用](~/tabs/what-are-tabs.md)し、会話型ボットまたは[](~/bots/what-are-bots.md)メッセージング拡張機能で使用[するように選択します](~/messaging-extensions/what-are-messaging-extensions.md)。 Web コンテンツ [ページMicrosoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用して認証を有効にします。 認証を有効にした後、コンテンツ ページをタブ、構成ページ、またはタスク モジュールに埋め込みます。 Web ベース認証フローの詳細については、以下を参照してください。

* [ボットに認証をTeams、](~/bots/how-to/authentication/add-authentication.md)会話型ボットで Web ベースの認証フローを使用する方法について説明します。
* [タブでの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)では、Teams でのタブ認証の仕組みを説明しています。 これは、タブに使用される一般的な Web ベース認証フローを示しています。
* [Azure AD認証では](~/tabs/how-to/authentication/auth-tab-AAD.md)、アプリ内のタブ内からAzure ADに接続する方法について説明Teams。
* [サイレント認証Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md)、アプリでサインインまたは同意のプロンプトを減らす方法について説明します。Azure AD。
* [.Net または C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript または Node.jsは ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) 、Web ベース認証のサンプルを提供します。

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

アプリの認証フローに関係なく、ID プロバイダーがアプリと通信Teamsします。 ほとんどのサンプルとウォークスルーでは、主に id プロバイダー Azure ADを使用します。 ただし、概念は ID プロバイダーに関係なく適用されます。 

詳細については、「ID プロバイダー [の構成」を参照してください](~/concepts/authentication/configure-identity-provider.md)。

## <a name="third-party-cookies-on-ios"></a>iOS 上のサード パーティ Cookie

iOS 14 の更新後、Apple は既定ですべてのアプリのサードパーティ [Cookie](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) アクセスをブロックしました。 したがって、チャネルタブまたはチャット タブおよび個人用アプリの認証にサードパーティの Cookie を利用するアプリは、iOS クライアント上で認証ワークフローをTeamsされません。 プライバシーとセキュリティの要件に準拠するには、トークン ベースのシステムに移動するか、ユーザー認証ワークフローにファースト パーティ Cookie を使用する必要があります。

## <a name="see-also"></a>関連項目

* [Microsoft Teamsの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)
* [ボットのシングル サインオンのサポート](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [メッセージング拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)