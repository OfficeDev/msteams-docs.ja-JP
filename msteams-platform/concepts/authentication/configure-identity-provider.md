---
title: OAuth 2.0 ID プロバイダーの構成
description: ID プロバイダーを構成する方法について説明します。Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 認証Azure AD Oauth ID プロバイダー
ms.openlocfilehash: b35f28f2cb306a6dfc3ae3151616925da1525069
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821354"
---
# <a name="configure-identity-providers"></a>ID プロバイダーを構成する

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>ID プロバイダーとしてAzure ADアプリケーションを構成する

OAuth 2.0 をサポートする ID プロバイダーは、不明なアプリケーションからの要求を認証しない。アプリケーションは、前もって登録する必要があります。 この操作を実行するには、次Azure AD手順を実行します。

1. アプリケーション登録 [ポータルを開きます](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)。

2. アプリを選択してプロパティを表示するか、[新しい登録] ボタンを選択します。 アプリの **[リダイレクト URI** ] セクションを探します。

3. ドロップダウン **メニューから [Web** ] を選択します。 認証エンドポイントへの URL を更新します。 TypeScript/Node.jsおよび C#サンプル アプリGitHub、リダイレクト URL は次のようになります。

    リダイレクト URL: `https://<hostname>/bot-auth/simple-start`

実際 `<hostname>` のホストに置き換える (Azure、Glitch、開発マシン上の localhost への ngrok トンネルなどの専用のホスティング サイトである可能性があります `abcd1234.ngrok.io`)。 アプリ (または上記のサンプル アプリ) を完了またはホストしていない場合は、この情報を取得できない場合がありますが、その情報が分かっているときにいつでもこのページに戻ります。

## <a name="other-authentication-providers"></a>その他の認証プロバイダー

* **LinkedIn:** 「LinkedIn アプリケーションの [構成」の手順に従います。](/linkedin/talent/apply-with-linkedin)

* **Google:** Google API コンソールから OAuth 2.0 クライアント資格情報 [を取得する](https://console.developers.google.com/)
