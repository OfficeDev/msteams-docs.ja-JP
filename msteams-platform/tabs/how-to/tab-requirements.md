---
title: タブの要件について
author: laujan
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8013c10050ae81ada0f2a27576cd43077eafe1e0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019581"
---
# <a name="tab-requirements"></a><span data-ttu-id="9b53a-104">タブの要件</span><span class="sxs-lookup"><span data-stu-id="9b53a-104">Tab requirements</span></span>

<span data-ttu-id="9b53a-105">Teamsタブは、次の要件に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b53a-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="9b53a-106">X-Frame-Options または Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame で提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b53a-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="9b53a-107">ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="9b53a-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="9b53a-108">11 Internet Explorerの場合は、同様に `X-Content-Security-Policy` 設定します。</span><span class="sxs-lookup"><span data-stu-id="9b53a-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="9b53a-109">または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="9b53a-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="9b53a-110">このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き尊重されています。</span><span class="sxs-lookup"><span data-stu-id="9b53a-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="9b53a-111">通常、クリック ジャッキに対するセーフガードとして、ログイン ページは iFrames でレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="9b53a-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="9b53a-112">したがって、認証ロジックでは、リダイレクト以外の方法を使用する必要があります (トークンベースまたは Cookie ベースの認証を使用するなど)。</span><span class="sxs-lookup"><span data-stu-id="9b53a-112">Therefore, your authentication logic needs to use a method other than redirect (e.g., use token-based or cookie-based authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="9b53a-113">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="9b53a-113">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="9b53a-114">既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9b53a-114">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="9b53a-115">「[SameSite Cookie 属性 (2020 更新プログラム)](../../resources/samesite-cookie-update.md)」を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="9b53a-115">*See* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="9b53a-116">ブラウザーは、Web ページが Web ページにサービスを提供したドメインとは異なるドメインに対して要求を行うのを防ぐ同一発生元ポリシーの制限に従います。</span><span class="sxs-lookup"><span data-stu-id="9b53a-116">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="9b53a-117">ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="9b53a-117">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="9b53a-118">クロスドメイン ナビゲーション ロジックを使用すると、Teams クライアントは、タブの読み込みまたは通信時に、アプリ マニフェストの静的な validDomains リストに対して原点を検証できます。</span><span class="sxs-lookup"><span data-stu-id="9b53a-118">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="9b53a-119">シームレスなエクスペリエンスを作成するには、クライアントのテーマ、デザイン、および意図に基Teamsタブのスタイルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b53a-119">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="9b53a-120">通常、タブは、特定の必要性に対処し、小さな一連のタスクまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="9b53a-120">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="9b53a-121">コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="9b53a-121">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="9b53a-122">ページの読み込み後に、 を呼び出します `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="9b53a-122">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="9b53a-123">ページを表示しない場合は、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="9b53a-123">Your page will not be displayed if you do not.</span></span>

* <span data-ttu-id="9b53a-124">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b53a-124">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="9b53a-125">モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="9b53a-125">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>