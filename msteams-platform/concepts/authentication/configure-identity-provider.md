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
# <a name="configure-identity-providers"></a><span data-ttu-id="f4cf8-104">ID プロバイダーを構成する</span><span class="sxs-lookup"><span data-stu-id="f4cf8-104">Configure identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="f4cf8-105">Azure Active Directory を ID プロバイダーとして使用するようにアプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="f4cf8-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="f4cf8-106">OAuth 2.0 をサポートする ID プロバイダーは、不明なアプリケーションからの要求を認証します。アプリケーションは、前もって登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="f4cf8-107">Azure ADでこれを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="f4cf8-108">アプリケーション登録 [ポータルを開きます](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="f4cf8-109">アプリを選択してプロパティを表示するか、[新しい登録] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="f4cf8-110">アプリの **リダイレクト URI セクション** を見つける。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="f4cf8-111">ドロップダウン メニューで **、Web** が選択されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="f4cf8-112">認証エンドポイントの URL を更新します。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="f4cf8-113">GitHub 上の TypeScript/Node.js および C# サンプル アプリの場合、リダイレクト URL は次のような結果を示します。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="f4cf8-114">リダイレクト URL: `https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="f4cf8-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="f4cf8-115">実際 `<hostname>` のホストに置き換える。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="f4cf8-116">これは、Azure、Glitch などの専用のホスティング サイトや、開発用コンピューターで localhost に使用する ngrok トンネルなどです `abcd1234.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="f4cf8-117">アプリ (または上記のサンプル アプリ) を完了またはホストしていない場合は、この情報がまだない可能性がありますが、その情報が既知の場合は、いつでもこのページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="f4cf8-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="f4cf8-118">その他の認証プロバイダー</span><span class="sxs-lookup"><span data-stu-id="f4cf8-118">Other authentication providers</span></span>

* <span data-ttu-id="f4cf8-119">**LinkedIn** LinkedIn アプリケーションの [構成に関する手順に従います。](https://developer.linkedin.com/docs/oauth2)</span><span class="sxs-lookup"><span data-stu-id="f4cf8-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="f4cf8-120">**Google** Google API コンソールから OAuth 2.0 クライアント資格情報 [を取得する](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="f4cf8-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
