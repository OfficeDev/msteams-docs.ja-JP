---
title: OAuth 2.0 ID プロバイダーを構成する
description: このモジュールでは、Microsoft Azure Active Directory (Azure AD) に焦点を当てて ID プロバイダーを構成する方法について説明します
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 2d344fb5ffcbde35ad9e85eed9ea662d2a0ca9f6
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143446"
---
# <a name="configure-identity-providers"></a>ID プロバイダーを構成する

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>ID プロバイダーとして Azure AD を使用するようにアプリケーションを構成する

OAuth 2.0 をサポートする ID プロバイダーは、不明なアプリケーションからの要求を認証しません。アプリケーションは事前に登録する必要があります。 Azure AD でこれを行うには、次の手順に従います。

1. [アプリケーション登録ポータル](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)を開きます。

2. アプリを選択してプロパティを表示するか、[新しい登録] ボタンを選択します。 アプリの **リダイレクト URI** セクションを見つけます。

3. ドロップダウン メニューから **[Web** ] を選択します。 URL を認証エンドポイントに更新します。 GitHubの TypeScript/Node.js および C# サンプル アプリの場合、リダイレクト URL は次のようになります。

    リダイレクト URL: `https://<hostname>/bot-auth/simple-start`

実際のホストに置き換えます `<hostname>` 。これは、Azure、Glitch などの専用ホスティング サイト、開発マシン `abcd1234.ngrok.io`上の localhost への ngrok トンネル (. アプリ (または上記のサンプル アプリ) を完了またはホストしていない場合は、この情報がない場合がありますが、その情報がわかっている場合は、いつでもこのページに戻ることができます。

## <a name="other-authentication-providers"></a>その他の認証プロバイダー

* **Linkedin：**[LinkedIn アプリケーションの構成](/linkedin/talent/apply-with-linkedin)に関するページの手順に従います

* **Google：**[Google API コンソール](https://console.developers.google.com/)から OAuth 2.0 クライアント資格情報を取得する

* **タブからの外部 OAuth プロバイダー:** 詳細については、「[外部 OAuth プロバイダーを使用する」を](../../tabs/how-to/authentication/auth-oauth-provider.md)参照してください。

## <a name="see-also"></a>関連項目

* [Microsoft Teams ボットでユーザーを認証する](../../resources/bot-v3/bot-authentication/auth-bot-AAD.md)
* [タブのシングル サインオン (SSO) のサポート](../../tabs/how-to/authentication/tab-sso-overview.md)
* [[Microsoft Teams] タブでユーザーを認証する](../../tabs/how-to/authentication/auth-tab-aad.md)
