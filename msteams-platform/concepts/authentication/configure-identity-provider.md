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
# <a name="configuring-identity-providers"></a><span data-ttu-id="11297-104">Id プロバイダーを構成する</span><span class="sxs-lookup"><span data-stu-id="11297-104">Configuring identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="11297-105">Azure Active Directory を id プロバイダーとして使用するようにアプリケーションを構成する</span><span class="sxs-lookup"><span data-stu-id="11297-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="11297-106">OAuth 2.0 をサポートしている id プロバイダーは、不明なアプリケーションからの要求を認証しません。アプリケーションは事前に登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11297-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="11297-107">Azure AD でこれを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="11297-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="11297-108">[アプリケーション登録ポータル](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)を開きます。</span><span class="sxs-lookup"><span data-stu-id="11297-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="11297-109">アプリを選択してプロパティを表示するか、[新しい登録] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="11297-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="11297-110">アプリの**リダイレクト URI**セクションを見つけます。</span><span class="sxs-lookup"><span data-stu-id="11297-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="11297-111">ドロップダウンメニューで、[ **Web** ] が選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="11297-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="11297-112">認証エンドポイントの URL を更新します。</span><span class="sxs-lookup"><span data-stu-id="11297-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="11297-113">GitHub の TypeScript/node.js および C# サンプルアプリの場合、リダイレクト Url は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="11297-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="11297-114">リダイレクト Url:`https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="11297-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="11297-115">を`<hostname>`実際のホストに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="11297-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="11297-116">これは、Azure、エラー、などの開発用コンピューター上の localhost への ngrok トンネルなど、専用のホスティングサイト`abcd1234.ngrok.io`である場合があります。</span><span class="sxs-lookup"><span data-stu-id="11297-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="11297-117">アプリ (または上記のサンプルアプリ) を完了していない場合、またはホストしていない場合は、この情報がわかっている場合は、このページにいつでも戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="11297-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="11297-118">その他の認証プロバイダー</span><span class="sxs-lookup"><span data-stu-id="11297-118">Other authentication providers</span></span>

* <span data-ttu-id="11297-119">**LinkedIn**「 [LinkedIn アプリケーションを構成する](https://developer.linkedin.com/docs/oauth2)」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="11297-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="11297-120">**Google**[GOOGLE API コンソール](https://console.developers.google.com/)から OAuth 2.0 クライアント資格情報を取得する</span><span class="sxs-lookup"><span data-stu-id="11297-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
