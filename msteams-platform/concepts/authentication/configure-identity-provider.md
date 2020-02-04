---
title: OAuth 2.0 id プロバイダーの構成
description: Azure AD でフォーカスを持つ id プロバイダーを構成する方法について説明します。
keywords: teams 認証 AAD oauth id プロバイダー
ms.openlocfilehash: 799b0c20cda64456a4610acbdbedf758989bee55
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675006"
---
# <a name="configuring-identity-providers"></a>Id プロバイダーを構成する

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Azure Active Directory を id プロバイダーとして使用するようにアプリケーションを構成する

OAuth 2.0 をサポートしている id プロバイダーは、不明なアプリケーションからの要求を認証しません。アプリケーションは事前に登録する必要があります。 Azure AD でこれを行うには、次の手順を実行します。

1. [アプリケーション登録ポータル](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)を開きます。

2. アプリを選択してプロパティを表示するか、[新しい登録] ボタンをクリックします。 アプリの**リダイレクト URI**セクションを見つけます。

3. ドロップダウンメニューで、[ **Web** ] が選択されていることを確認します。 認証エンドポイントの URL を更新します。 GitHub の TypeScript/node.js および C# サンプルアプリの場合、リダイレクト Url は次のようになります。

    リダイレクト Url:`https://<hostname>/bot-auth/simple-start`

を`<hostname>`実際のホストに置き換えます。 これは、Azure、エラー、などの開発用コンピューター上の localhost への ngrok トンネルなど、専用のホスティングサイト`abcd1234.ngrok.io`である場合があります。 アプリ (または上記のサンプルアプリ) を完了していない場合、またはホストしていない場合は、この情報がわかっている場合は、このページにいつでも戻ることができます。

## <a name="other-authentication-providers"></a>その他の認証プロバイダー

* **LinkedIn**「 [LinkedIn アプリケーションを構成する](https://developer.linkedin.com/docs/oauth2)」の手順に従います。

* **Google**[GOOGLE API コンソール](https://console.developers.google.com/)から OAuth 2.0 クライアント資格情報を取得する
