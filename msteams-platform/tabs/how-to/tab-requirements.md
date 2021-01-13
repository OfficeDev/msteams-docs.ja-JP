---
title: タブの要件について
author: laujan
description: Microsoft Teams のすべてのタブは、これらの要件に従う必要があります。
keywords: teams タブ グループ チャネルを構成可能
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1f5a3eaa8ca16878944288d5dbbfa78cfe9fa3ce
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797943"
---
# <a name="tab-requirements"></a><span data-ttu-id="2b0b8-104">タブの要件</span><span class="sxs-lookup"><span data-stu-id="2b0b8-104">Tab requirements</span></span>

<span data-ttu-id="2b0b8-105">Teams のタブは、次の要件に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="2b0b8-106">X-Frame-Options や Content-Security-Policy HTTP 応答ヘッダーを介して、タブ ページを iFrame で提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="2b0b8-107">ヘッダーを設定します。 `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="2b0b8-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="2b0b8-108">11 Internet Explorerについては、同様に `X-Content-Security-Policy` 設定します。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="2b0b8-109">または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="2b0b8-110">このヘッダーは廃止されましたが、ほとんどのブラウザーで引き続き使用されています。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="2b0b8-111">通常、クリックジャッキーに対する保護策として、ログイン ページは iFrame では表示されません。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="2b0b8-112">したがって、認証ロジックではリダイレクト以外の方法を使用する必要があります (トークン ベースの認証や Cookie ベースの認証を使用する場合など)。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-112">Therefore, your authentication logic needs to use a method other than redirect (e.g., use token-based or cookie-based authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="2b0b8-113">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-113">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="2b0b8-114">既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-114">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="2b0b8-115">「[SameSite Cookie 属性 (2020 更新プログラム)](../../resources/samesite-cookie-update.md)」を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-115">*See* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="2b0b8-116">ブラウザーは、Web ページにサービスを提供したドメインとは異なるドメインに対して Web ページが要求を行うのを防ぐため、同一発生元ポリシーの制限に従います。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-116">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="2b0b8-117">ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-117">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="2b0b8-118">クロスドメイン ナビゲーション ロジックでは、Teams クライアントがタブを読み込むまたはタブと通信するときに、アプリ マニフェストの静的 validDomains リストに対して原点を検証できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-118">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="2b0b8-119">シームレスなエクスペリエンスを作成するには、Teams クライアントのテーマ、デザイン、および意図に基づいてタブのスタイルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-119">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="2b0b8-120">通常、タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てながら構築されている場合に最適に動作します。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-120">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="2b0b8-121">コンテンツ ページ内で、スクリプト タグを使用 [して Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-121">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="2b0b8-122">ページの読み込み後、呼び出しを行います `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-122">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="2b0b8-123">表示しない場合、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="2b0b8-123">Your page will not be displayed if you do not.</span></span>
