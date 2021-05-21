---
title: タブの要件について
author: laujan
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a46a80401b29b5436807c9a5b94580beca3786f0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566664"
---
# <a name="tab-requirements"></a><span data-ttu-id="10d61-104">タブの要件</span><span class="sxs-lookup"><span data-stu-id="10d61-104">Tab requirements</span></span>

<span data-ttu-id="10d61-105">Teamsタブは、次の要件に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="10d61-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="10d61-106">X-Frame-Options または Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame で提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10d61-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="10d61-107">ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="10d61-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="10d61-108">11 Internet Explorerの場合は、同様に `X-Content-Security-Policy` 設定します。</span><span class="sxs-lookup"><span data-stu-id="10d61-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="10d61-109">または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="10d61-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="10d61-110">このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き尊重されています。</span><span class="sxs-lookup"><span data-stu-id="10d61-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="10d61-111">通常、クリック ジャッキに対するセーフガードとして、ログイン ページは iFrames でレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="10d61-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="10d61-112">したがって、認証ロジックではリダイレクト以外のメソッドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10d61-112">Therefore, your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="10d61-113">たとえば、トークンベースまたは Cookie ベースの認証を使用します。</span><span class="sxs-lookup"><span data-stu-id="10d61-113">For example, use token-based or cookie-based authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="10d61-114">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="10d61-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="10d61-115">既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="10d61-115">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="10d61-116">詳細については [、「SameSite cookie 属性 (2020 update)」を参照してください](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="10d61-116">For more information, see [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="10d61-117">ブラウザーは、Web ページが Web ページにサービスを提供したドメインとは異なるドメインに対して要求を行うのを防ぐ同一発生元ポリシーの制限に従います。</span><span class="sxs-lookup"><span data-stu-id="10d61-117">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="10d61-118">ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="10d61-118">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="10d61-119">クロスドメイン ナビゲーション ロジックを使用すると、Teams クライアントは、タブの読み込みまたは通信時に、アプリ マニフェストの静的な validDomains リストに対して原点を検証できます。</span><span class="sxs-lookup"><span data-stu-id="10d61-119">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="10d61-120">シームレスなエクスペリエンスを作成するには、クライアントのテーマ、デザイン、および意図に基Teamsタブのスタイルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10d61-120">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="10d61-121">通常、タブは、特定の必要性に対処し、小さな一連のタスクまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="10d61-121">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="10d61-122">コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="10d61-122">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="10d61-123">ページの読み込み後に、 を呼び出します `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="10d61-123">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="10d61-124">ページを表示しない場合は、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="10d61-124">Your page will not be displayed if you do not.</span></span>

* <span data-ttu-id="10d61-125">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10d61-125">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="10d61-126">モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="10d61-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

## <a name="next-step"></a><span data-ttu-id="10d61-127">次の手順</span><span class="sxs-lookup"><span data-stu-id="10d61-127">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="10d61-128">カスタム 個人用タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="10d61-128">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)