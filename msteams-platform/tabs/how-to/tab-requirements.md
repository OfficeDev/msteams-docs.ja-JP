---
title: 前提条件
author: surbhigupta
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8566bb0457db76e4639593dcd67a0442749c0a31
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179938"
---
# <a name="prerequisites"></a><span data-ttu-id="96094-104">前提条件</span><span class="sxs-lookup"><span data-stu-id="96094-104">Prerequisites</span></span>

<span data-ttu-id="96094-105">Teamsは、次の前提条件に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="96094-105">Teams tabs must adhere to the following prerequisites:</span></span>

* <span data-ttu-id="96094-106">X-Frame-Options と Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame に表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="96094-106">You must allow your tab pages to be shown in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="96094-107">ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="96094-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="96094-108">11 Internet Explorer互換性の場合は、 を設定します `X-Content-Security-Policy` 。</span><span class="sxs-lookup"><span data-stu-id="96094-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="96094-109">または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="96094-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="96094-110">このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き受け入れ可能です。</span><span class="sxs-lookup"><span data-stu-id="96094-110">This header is deprecated but still accepted by most browsers.</span></span>

* <span data-ttu-id="96094-111">通常、クリックジャックに対する保護手段として、ログイン ページは iFrames では表示されません。</span><span class="sxs-lookup"><span data-stu-id="96094-111">Typically, as a safeguard against clickjacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="96094-112">認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="96094-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="96094-113">たとえば、トークンベースまたは Cookie ベースの認証を使用します。</span><span class="sxs-lookup"><span data-stu-id="96094-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="96094-114">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="96094-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="96094-115">既定のブラウザー動作に依存するのではなく、Cookie の使用目的を設定することを推奨します。</span><span class="sxs-lookup"><span data-stu-id="96094-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="96094-116">詳細については [、「SameSite cookie 属性」を参照してください](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="96094-116">For more information, see [SameSite cookie attribute](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="96094-117">ブラウザーは、同じオリジン ポリシーの制限に従います。</span><span class="sxs-lookup"><span data-stu-id="96094-117">Browsers adhere to a same-origin policy restriction.</span></span> <span data-ttu-id="96094-118">Web ページが、提供された Web ページとは異なるドメインに対して要求を行うのを防ぐ。</span><span class="sxs-lookup"><span data-stu-id="96094-118">It prevents webpages from making requests to different domains than the served web page.</span></span> <span data-ttu-id="96094-119">ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトできます。</span><span class="sxs-lookup"><span data-stu-id="96094-119">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="96094-120">クロスドメイン ナビゲーション ロジックを使用すると、Teams クライアントは、タブの読み込みまたは通信時にアプリ マニフェストの静的リストに対して原点を `validDomains` 検証できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="96094-120">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static `validDomains` list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="96094-121">クライアントのテーマ、デザイン、および意図Teamsに基づいてタブのスタイルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="96094-121">You must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="96094-122">通常、タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="96094-122">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="96094-123">コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="96094-123">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="96094-124">ページの読み込み後に、呼び出し `microsoftTeams.initialize()` を行います。それ以外の場合、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="96094-124">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="96094-125">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="96094-125">For authentication to work on mobile clients, you must upgrade Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="96094-126">モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="96094-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="96094-127">[MS Teams] タブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="96094-127">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="see-also"></a><span data-ttu-id="96094-128">関連項目</span><span class="sxs-lookup"><span data-stu-id="96094-128">See also</span></span>

* [<span data-ttu-id="96094-129">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="96094-129">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* <span data-ttu-id="96094-130">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="96094-130">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="96094-131">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="96094-131">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="96094-132">次の手順</span><span class="sxs-lookup"><span data-stu-id="96094-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="96094-133">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="96094-133">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
