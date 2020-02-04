---
title: Teams でユーザーを認証する
description: Teams での認証とアプリでの使用方法について説明します。
keywords: teams 認証 OAuth SSO AAD
ms.openlocfilehash: d3ae57d9937c6794fb743b44ca8210a5afd181bf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674743"
---
# <a name="authentication-in-teams"></a>Teams での認証

> [!Note]
> モバイルクライアントでの Web ベース認証には、Teams JavaScript SDK のバージョン1.4.1 以降が必要です。

アプリが Azure Active Directory によって保護されたユーザー情報にアクセスしたり、Facebook や Twitter などの他のサービスからデータにアクセスしたりするには、アプリがこれらのプロバイダーとの信頼された接続を確立する必要があります。 アプリでユーザースコープで Microsoft Graph Api を使用する必要がある場合は、ユーザーを認証して、適切な認証トークンを取得する必要もあります。

Microsoft Teams では、アプリに対して2つの異なる認証フローがあり、を利用できます。 タブ、構成ページ、またはタスクモジュールに埋め込まれた[コンテンツページ](~/tabs/how-to/create-tab-pages/content-page.md)で従来の web ベースの認証フローを実行することができます。 アプリに会話の bot が含まれている場合は、OAuthPrompt フロー (およびオプションで Azure Bot フレームワークのトークンサービス) を使用して、会話の一部としてユーザーを認証できます。

## <a name="web-based-authentication-flow"></a>Web ベースの認証フロー

[タブ](~/tabs/what-are-tabs.md)では、web ベースの認証フローを使用し、[会話 bot](~/bots/what-are-bots.md)または[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)で使用するかどうかを選択することができます。 Web コンテンツページの[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)を使用して認証を有効にし、そのコンテンツページをタブ、構成ページ、またはタスクモジュールに埋め込むことができます。 話し言葉の bot で web ベースの認証フローを使用する場合は、[ボット付きのタスクモジュールを使用](~/task-modules-and-cards/task-modules/task-modules-bots.md)する必要があります。

* [タブの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md) Teams でのタブ認証のしくみについて説明します。 これは、タブで使用される一般的な web ベースの認証フローを示しています。
* [タブの AZURE AD 認証](~/tabs/how-to/authentication/auth-tab-AAD.md)Teams のアプリのタブ内から Azure Active Directory に接続する方法について説明します。
* [サイレント認証 (AZURE AD)](~/tabs/how-to/authentication/auth-silent-AAD.md) Azure Active Directory を使用してアプリでのサインイン/同意プロンプトを減らす方法について説明します。
* [Dotnet/C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)または[JavaScript/node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)での Web ベース認証

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>会話の bot の OAuthPrompt フロー

Azure Bot フレームワークの OAuthPrompt を使用すると、会話のボットを使用するアプリの認証が容易になります。 Azure Bot フレームワークのトークンサービスを活用して、トークンキャッシュもサポートすることができます。

OAuthPrompt の使用の詳細については、次を参照してください。

* [Bot 認証フローの概要](~/bots/how-to/authentication/auth-flow-bot.md)アプリ内で Teams 内で認証が機能する方法について説明します。 これは、すべてのバージョンの Teams (web、デスクトップアプリ、モバイルアプリ) で bot に対して使用されている web ベース以外の認証フローを示しています。
* [Bot 認証](~/bots/how-to/authentication/add-authentication.md)
* [Dotnet/C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)または[JavaScript/node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)の BOT 認証 (v3 SDK) のサンプル

## <a name="configure-your-identity-provider"></a>Id プロバイダーを構成する

アプリケーションが使用している認証フロー (両方を使用している場合もあります) に関係なく、Teams アプリと通信するように id プロバイダーを構成する必要があります。 ここに記載されているサンプルとチュートリアルの大部分は、主に、id プロバイダーとして Azure Active Directory を使用することで対処できます。 ただし、この概念は、どの id プロバイダーを使用するかに関係なく適用されます。

詳細について[は、「id プロバイダーを構成](~/concepts/authentication/configure-identity-provider.md)する」を参照してください。
