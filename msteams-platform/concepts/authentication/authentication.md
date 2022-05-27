---
title: アプリ ユーザーの認証
description: Teams での認証と、アプリでの認証の使用方法について説明します
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams 認証 OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 53f258769140a2b40bb59a1232250f74ec693bee
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757158"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Microsoft Teams でユーザーを認証する

> [!Note]
> モバイル クライアントでの Web ベースの認証には、Teams JavaScript クライアント SDK のバージョン 1.4.1 以降が必要です。

Azure AD によって保護されているユーザー情報にアクセスし、Facebook や Twitter などのサービスからのデータにアクセスするために、アプリはこれらのプロバイダーとの信頼できる接続を確立します。 アプリがユーザー スコープで Microsoft Graph API を使用している場合は、ユーザーを認証して適切な認証トークンを取得します。

Teams には、アプリに 2 つの異なる認証フローがあります。 タブ、構成ページ、タスク モジュールに埋め込まれた[コンテンツ ページ](~/tabs/how-to/create-tab-pages/content-page.md)で、従来の Web ベースの認証フローを実行します。 アプリに会話ボットが含まれている場合、OAuthPrompt フロー (およびオプションの Azure Bot Framework のトークン サービス) を使用して、会話の一部としてユーザーを認証することができます。

## <a name="web-based-authentication-flow"></a>Web ベースの認証フロー

[タブ](~/tabs/what-are-tabs.md)には Web ベースの認証フローを使用し、[会話ボット](~/bots/what-are-bots.md)や[メッセージ拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)との併用を選択します。 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を Web コンテンツ ページで使用し、認証を有効にします。 認証を有効にした後、コンテンツ ページをタブ、構成ページ、またはタスク モジュールに埋め込みます。 Web ベースの認証フローの詳細については、以下を参照してください。

* [Teams ボットへの認証の追加](~/bots/how-to/authentication/add-authentication.md)では、会話ボットで Web ベースの認証フローを使用する方法について説明します。
* [タブの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)では、タブ認証がTeamsでどのように機能するかについて説明します。これは、タブに使用される一般的な Web ベースの認証フローを示しています。
* [タブでの Azure AD 認証](~/tabs/how-to/authentication/auth-tab-AAD.md)では、Teams のアプリ内のタブから Azure AD に接続する方法を説明しています。
* [サイレント認証 Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md) では、アプリ内でのサインインまたは同意プロンプトを Azure AD を使用して減らす方法を説明しています。
* [.Net または C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) または [JavaScript または Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) は、Web ベースの認証のサンプルを提供します。

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>会話ボットの OAuthPrompt フロー

Azure Bot Framework の OAuthPrompt で、会話ボットを使用したアプリの認証が簡単になります。 Azure Bot Framework のトークン サービスを利用して、トークン キャッシュをアシストします。

OAuthPrompt の使用の詳細については、次を参照してください。

* [ボット認証フローの概要](~/bots/how-to/authentication/auth-flow-bot.md)では、Teamsのアプリ内のボット内での認証のしくみについて説明します。これは、Teams Web、デスクトップ アプリ、モバイル アプリのボットに使用される非 Web ベースの認証フローを示します。
* [ボット認証](~/bots/how-to/authentication/add-authentication.md)では、Teams ボットに OAuth 認証を追加する方法について説明しています。

## <a name="code-sample"></a>コード サンプル

ボット認証 v3 SDK サンプルを提供します。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| ボット認証 | このサンプルは、Microsoft Teams のボットで認証を開始する方法を示しています。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| タブ、ボット、メッセージ拡張機能 (ME) SSO | このサンプルでは、Tab、Bot、ME の SSO (検索、アクション、リンクの展開) を示します。 |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 利用不可 |

## <a name="configure-the-identity-provider"></a>ID プロバイダーを構成する

アプリの認証フローに関係なく、Teams アプリと通信するように ID プロバイダーを構成します。 ほとんどのサンプルとウォークスルーでは、主に Azure AD を ID プロバイダーとして使用します。 ただし、この概念は ID プロバイダーに関係なく適用されます。

詳細については、「[configuring an identity provider (ID プロバイダーの構成)](~/concepts/authentication/configure-identity-provider.md)」を参照してください

## <a name="third-party-cookies-on-ios"></a>iOS のサードパーティ Cookie

iOS 14 の更新後、Apple は既定ですべてのアプリの[サードパーティ Cookie](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) アクセスをブロックしました。 そのため、チャネル タブまたはチャット タブの認証にサード パーティの Cookie を利用するアプリや個人用アプリでは、Teams iOS クライアントで認証ワークフローを完了できません。 プライバシーとセキュリティの要件に準拠するには、トークンベースのシステムに移行するか、ユーザー認証ワークフローにファーストパーティ Cookie を使用する必要があります。

## <a name="see-also"></a>関連項目

* [タブの Microsoft Teams 認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)
* [ボットのシングル サインオンのサポート](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [メッセージ拡張機能に認証を追加する](~/messaging-extensions/how-to/add-authentication.md)
