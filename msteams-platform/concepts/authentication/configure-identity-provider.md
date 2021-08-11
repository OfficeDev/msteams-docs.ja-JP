---
title: OAuth 2.0 ID プロバイダーの構成
description: Azure プロバイダーを中心に ID プロバイダーを構成する方法についてAD
ms.topic: how-to
localization_priority: Normal
keywords: teams 認証 AAD oauth IDENTITY プロバイダー
ms.openlocfilehash: f41e03717c24095b527adc471a89f8aee5de3a3ddba8773376fca49ee12bbbcc
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705567"
---
# <a name="configure-identity-providers"></a>ID プロバイダーを構成する

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>ID プロバイダーとしてアプリケーションを使用Azure Active Directory構成する

OAuth 2.0 をサポートする ID プロバイダーは、不明なアプリケーションからの要求を認証しない。アプリケーションは、前もって登録する必要があります。 Azure ADでこれを行うには、次の手順を実行します。

1. アプリケーション登録 [ポータルを開きます](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)。

2. アプリを選択してプロパティを表示するか、[新しい登録] ボタンをクリックします。 アプリの **[リダイレクト URI]** セクションを探します。

3. ドロップダウン メニューで **、[Web]** が選択されている必要があります。 認証エンドポイントへの URL を更新します。 TypeScript/Node.jsおよび C#サンプル アプリGitHub、リダイレクト URL は次に似ています。

    リダイレクト URL: `https://<hostname>/bot-auth/simple-start`

実際 `<hostname>` のホストに置き換える。 これは、Azure、Glitch などの専用のホスティング サイト、または開発マシン上の localhost への ngrok トンネルなどです `abcd1234.ngrok.io` 。 アプリ (または上記のサンプル アプリ) を完了またはホストしていない場合は、この情報がまだない場合がありますが、その情報が知られているときにいつでもこのページに戻ります。

## <a name="other-authentication-providers"></a>その他の認証プロバイダー

* **LinkedIn** 「LinkedIn アプリケーションの [構成」の手順に従います。](/linkedin/talent/apply-with-linkedin)

* **Google** Google API コンソールから OAuth 2.0 クライアント資格情報 [を取得する](https://console.developers.google.com/)
