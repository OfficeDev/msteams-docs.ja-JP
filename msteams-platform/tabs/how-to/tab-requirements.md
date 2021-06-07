---
title: タブの要件
author: laujan
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 50d529697a80ca9ba78921009405f18fa021e802
ms.sourcegitcommit: 45c66faef8145abb903ef7118b9fa914c12aba2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2021
ms.locfileid: "52736762"
---
# <a name="tab-requirements"></a><span data-ttu-id="03d78-104">タブの要件</span><span class="sxs-lookup"><span data-stu-id="03d78-104">Tab requirements</span></span>

<span data-ttu-id="03d78-105">Teamsタブは、次の要件に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="03d78-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="03d78-106">X-Frame-Options および Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame で提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="03d78-106">You must allow your tab pages to be served in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="03d78-107">ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="03d78-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="03d78-108">11 Internet Explorer互換性の場合は、 を設定します `X-Content-Security-Policy` 。</span><span class="sxs-lookup"><span data-stu-id="03d78-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="03d78-109">または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="03d78-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="03d78-110">このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き受け入れ可能です。</span><span class="sxs-lookup"><span data-stu-id="03d78-110">This header is deprecated but still accepted by most browsers.</span></span>
* <span data-ttu-id="03d78-111">通常、クリック ジャッキに対するセーフガードとして、ログイン ページは iFrames でレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="03d78-111">Typically, as a safeguard against click-jacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="03d78-112">認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="03d78-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="03d78-113">たとえば、トークンベースまたは Cookie ベースの認証を使用します。</span><span class="sxs-lookup"><span data-stu-id="03d78-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="03d78-114">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="03d78-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="03d78-115">既定のブラウザー動作に依存するのではなく、Cookie の使用目的を設定することを推奨します。</span><span class="sxs-lookup"><span data-stu-id="03d78-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="03d78-116">詳細については [、「SameSite cookie attribute 2020 update」を参照してください](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="03d78-116">For more information, see [SameSite cookie attribute 2020 update](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="03d78-117">ブラウザーは、Web ページが Web ページにサービスを提供したドメインとは異なるドメインに対して要求を行うのを防ぐ同一発生元ポリシーの制限に従います。</span><span class="sxs-lookup"><span data-stu-id="03d78-117">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="03d78-118">ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトできます。</span><span class="sxs-lookup"><span data-stu-id="03d78-118">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="03d78-119">クロスドメイン ナビゲーション ロジックでは、Teams クライアントがタブの読み込みまたは通信時にアプリ マニフェストの静的な validDomains リストに対して原点を検証できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="03d78-119">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="03d78-120">シームレスなエクスペリエンスを作成するには、クライアントのテーマ、デザイン、および意図に基づいてTeamsスタイルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="03d78-120">To create a seamless experience, you must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="03d78-121">通常、タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="03d78-121">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="03d78-122">コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="03d78-122">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="03d78-123">ページの読み込み後に、呼び出し `microsoftTeams.initialize()` を行います。それ以外の場合、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="03d78-123">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="03d78-124">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="03d78-124">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="03d78-125">モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="03d78-125">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="03d78-126">[MS Teams] タブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="03d78-126">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="next-step"></a><span data-ttu-id="03d78-127">次の手順</span><span class="sxs-lookup"><span data-stu-id="03d78-127">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03d78-128">カスタム 個人用タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="03d78-128">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)
