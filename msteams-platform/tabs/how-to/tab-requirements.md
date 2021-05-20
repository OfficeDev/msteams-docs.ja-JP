---
title: タブの要件について
author: laujan
description: Microsoft Teamsのすべてのタブは、これらの要件に準拠している必要があります。
keywords: チーム タブ グループ チャネルの構成可能
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
# <a name="tab-requirements"></a><span data-ttu-id="97c27-104">タブの要件</span><span class="sxs-lookup"><span data-stu-id="97c27-104">Tab requirements</span></span>

<span data-ttu-id="97c27-105">Teamsタブは、次の要件に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="97c27-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="97c27-106">タブページを、X フレーム オプションまたはコンテンツ セキュリティ ポリシー HTTP 応答ヘッダーを介して iFrame で提供できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="97c27-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="97c27-107">ヘッダーを設定: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="97c27-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="97c27-108">Internet Explorer 11 の互換性のためにも設定 `X-Content-Security-Policy` します。</span><span class="sxs-lookup"><span data-stu-id="97c27-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="97c27-109">または、ヘッダを設定 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` します。</span><span class="sxs-lookup"><span data-stu-id="97c27-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="97c27-110">このヘッダーは非推奨ですが、ほとんどのブラウザーでは引き続き使用されます。</span><span class="sxs-lookup"><span data-stu-id="97c27-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="97c27-111">通常、クリックジャッキングに対する保護手段として、ログインページはiFrameでレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="97c27-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="97c27-112">したがって、認証ロジックでは、リダイレクト以外のメソッドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97c27-112">Therefore, your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="97c27-113">たとえば、トークンベースまたはクッキーベースの認証を使用します。</span><span class="sxs-lookup"><span data-stu-id="97c27-113">For example, use token-based or cookie-based authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="97c27-114">Chrome 80 (2020 年初頭にリリース予定) では、新しい Cookie 値を紹介し、既定で Cookie ポリシーを設定します。</span><span class="sxs-lookup"><span data-stu-id="97c27-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="97c27-115">既定のブラウザーの動作を利用するのではなく、Cookie に対して使用する目的を設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="97c27-115">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="97c27-116">詳細については、 [SameSite クッキー属性 (2020 更新)](../../resources/samesite-cookie-update.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97c27-116">For more information, see [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="97c27-117">ブラウザは、Web ページが Web ページを提供したドメインとは異なるドメインに対して要求を行うことを防ぐ、同一生成元ポリシーの制限に従います。</span><span class="sxs-lookup"><span data-stu-id="97c27-117">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="97c27-118">ただし、構成ページまたはコンテンツ ページを別のドメインまたはサブドメインにリダイレクトする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="97c27-118">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="97c27-119">クロスドメイン ナビゲーション ロジックでは、Teams クライアントが、タブの読み込み時またはタブとの通信時に、アプリ マニフェストの静的な validDomains リストに対して元のドメインを検証できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="97c27-119">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="97c27-120">シームレスなエクスペリエンスを作成するには、Teamsクライアントのテーマ、デザイン、および意図に基づいてタブのスタイルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97c27-120">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="97c27-121">通常、タブは、特定のニーズに対応し、タブのチャネルの場所に関連する一連のタスクまたはデータのサブセットに焦点を当てるために作成されている場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="97c27-121">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="97c27-122">コンテンツ ページ内で、スクリプト タグを使用して[、Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="97c27-122">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="97c27-123">ページの読み込みに続いて、 に電話をかけることができます `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="97c27-123">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="97c27-124">表示しない場合は、ページは表示されません。</span><span class="sxs-lookup"><span data-stu-id="97c27-124">Your page will not be displayed if you do not.</span></span>

* <span data-ttu-id="97c27-125">モバイル クライアントで認証を実行するには、JavaScript SDK Teams少なくともバージョン 1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="97c27-125">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="97c27-126">モバイル クライアントにチャンネルタブまたはグループ タブを表示Teams選択した場合、 `setSettings()` 設定にはプロパティの値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="97c27-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

## <a name="next-step"></a><span data-ttu-id="97c27-127">次の手順</span><span class="sxs-lookup"><span data-stu-id="97c27-127">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97c27-128">Node.jsとヨーマンジェネレータを使用してカスタムパーソナルタブを作成Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="97c27-128">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)