---
title: 前提条件
author: surbhigupta
description: これらの要件にMicrosoft Teamsする必要があります。
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b54fc7235132a9253f6eecc62417f786bf4aa45c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140188"
---
# <a name="prerequisites"></a><span data-ttu-id="95675-104">前提条件</span><span class="sxs-lookup"><span data-stu-id="95675-104">Prerequisites</span></span>

<span data-ttu-id="95675-105">Teamsは、次の前提条件に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="95675-105">Teams tabs must adhere to the following prerequisites:</span></span>

* <span data-ttu-id="95675-106">X-Frame-Options と Content-Security-Policy HTTP 応答ヘッダーを使用して、タブ ページを iFrame に表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95675-106">You must allow your tab pages to be shown in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="95675-107">ヘッダーの設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="95675-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="95675-108">11 Internet Explorer互換性の場合は、 を設定します `X-Content-Security-Policy` 。</span><span class="sxs-lookup"><span data-stu-id="95675-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="95675-109">または、ヘッダーを設定します `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="95675-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="95675-110">このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き受け入れ可能です。</span><span class="sxs-lookup"><span data-stu-id="95675-110">This header is deprecated but still accepted by most browsers.</span></span>

* <span data-ttu-id="95675-111">通常、クリックジャックに対する保護手段として、ログイン ページは iFrames では表示されません。</span><span class="sxs-lookup"><span data-stu-id="95675-111">Typically, as a safeguard against clickjacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="95675-112">認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95675-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="95675-113">たとえば、トークンベースまたは Cookie ベースの認証を使用します。</span><span class="sxs-lookup"><span data-stu-id="95675-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95675-114">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="95675-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="95675-115">既定のブラウザー動作に依存するのではなく、Cookie の使用目的を設定することを推奨します。</span><span class="sxs-lookup"><span data-stu-id="95675-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="95675-116">詳細については [、「SameSite cookie 属性」を参照してください](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="95675-116">For more information, see [SameSite cookie attribute](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="95675-117">ブラウザーは、同じオリジン ポリシーの制限に従います。</span><span class="sxs-lookup"><span data-stu-id="95675-117">Browsers adhere to a same-origin policy restriction.</span></span> <span data-ttu-id="95675-118">Web ページが、提供された Web ページとは異なるドメインに対して要求を行うのを防ぐ。</span><span class="sxs-lookup"><span data-stu-id="95675-118">It prevents webpages from making requests to different domains than the served web page.</span></span> <span data-ttu-id="95675-119">ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトできます。</span><span class="sxs-lookup"><span data-stu-id="95675-119">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="95675-120">クロスドメイン ナビゲーション ロジックを使用すると、Teams クライアントは、タブの読み込みまたは通信時にアプリ マニフェストの静的リストに対して原点を `validDomains` 検証できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="95675-120">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static `validDomains` list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="95675-121">クライアントのテーマ、デザイン、および意図Teamsに基づいてタブのスタイルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95675-121">You must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="95675-122">通常、タブは、特定の必要性に対処し、小さなタスクセットまたはタブのチャネルの場所に関連するデータのサブセットに焦点を当てするために構築されている場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="95675-122">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="95675-123">コンテンツ ページ内で、スクリプト タグを使用Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="95675-123">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="95675-124">ページの読み込み後に、呼び出し `microsoftTeams.initialize()` を行います。それ以外の場合、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="95675-124">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="95675-125">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="95675-125">For authentication to work on mobile clients, you must upgrade Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="95675-126">モバイル クライアントにチャネルまたはグループ タブを表示Teams場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="95675-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="95675-127">[MS Teams] タブでは、自己署名証明書を使用するイントラネット Web サイトを読み込む機能はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="95675-127">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="see-also"></a><span data-ttu-id="95675-128">関連項目</span><span class="sxs-lookup"><span data-stu-id="95675-128">See also</span></span>

* [<span data-ttu-id="95675-129">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="95675-129">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* <span data-ttu-id="95675-130">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="95675-130">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="95675-131">コンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="95675-131">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="95675-132">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="95675-132">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="95675-133">タブの削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="95675-133">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="95675-134">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="95675-134">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="95675-135">タブのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="95675-135">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="95675-136">アダプティブ カードを使用してタブをビルドする</span><span class="sxs-lookup"><span data-stu-id="95675-136">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="95675-137">タブのリンクの展開とステージ ビュー</span><span class="sxs-lookup"><span data-stu-id="95675-137">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="95675-138">会話タブを作成する</span><span class="sxs-lookup"><span data-stu-id="95675-138">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="95675-139">タブ余白の変更</span><span class="sxs-lookup"><span data-stu-id="95675-139">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="95675-140">次の手順</span><span class="sxs-lookup"><span data-stu-id="95675-140">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95675-141">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="95675-141">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
