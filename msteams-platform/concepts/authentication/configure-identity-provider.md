---
title: OAuth 2.0 ID プロバイダーを構成する
description: Azure AD に重点を置き、ID プロバイダーを構成する方法について説明AD
ms.topic: how-to
keywords: Teams 認証 AAD oauth ID プロバイダー
ms.openlocfilehash: b5ffd6c4c1edd2c4315ea1e31474a626de53aba1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014468"
---
# <a name="configure-identity-providers"></a>ID プロバイダーを構成する

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Azure Active Directory を ID プロバイダーとして使用するようにアプリケーションを構成する

OAuth 2.0 をサポートする ID プロバイダーは、不明なアプリケーションからの要求を認証します。アプリケーションは、前もって登録する必要があります。 Azure ADでこれを行うには、次の手順を実行します。

1. アプリケーション登録 [ポータルを開きます](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)。

2. アプリを選択してプロパティを表示するか、[新しい登録] ボタンをクリックします。 アプリの **リダイレクト URI セクション** を見つける。

3. ドロップダウン メニューで **、Web** が選択されている必要があります。 認証エンドポイントの URL を更新します。 GitHub 上の TypeScript/Node.js および C# サンプル アプリの場合、リダイレクト URL は次のような結果を示します。

    リダイレクト URL: `https://<hostname>/bot-auth/simple-start`

実際 `<hostname>` のホストに置き換える。 これは、Azure、Glitch などの専用のホスティング サイトや、開発用コンピューターで localhost に使用する ngrok トンネルなどです `abcd1234.ngrok.io` 。 アプリ (または上記のサンプル アプリ) を完了またはホストしていない場合は、この情報がまだない可能性がありますが、その情報が既知の場合は、いつでもこのページに戻ります。

## <a name="other-authentication-providers"></a>その他の認証プロバイダー

* **LinkedIn** LinkedIn アプリケーションの [構成に関する手順に従います。](https://developer.linkedin.com/docs/oauth2)

* **Google** Google API コンソールから OAuth 2.0 クライアント資格情報 [を取得する](https://console.developers.google.com/)
