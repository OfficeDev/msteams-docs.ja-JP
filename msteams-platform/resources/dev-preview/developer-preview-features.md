---
title: 公開開発者プレビューの機能
description: Microsoft Teams の公開開発者プレビューの機能について説明します。
keywords: teams のプレビュー開発者向け機能
ms.openlocfilehash: abec097d9f3b6fb48a4a50cb26d73cf811151149
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674654"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="21da7-104">Microsoft Teams の公開開発者プレビューの機能</span><span class="sxs-lookup"><span data-stu-id="21da7-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="21da7-105">開発者プレビューには、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="21da7-105">The developer preview includes the following new features:</span></span>

## <a name="mention-support-in-adaptive-cards"></a><span data-ttu-id="21da7-106">アダプティブカードでのサポートを説明します。</span><span class="sxs-lookup"><span data-stu-id="21da7-106">Mention support in Adaptive cards</span></span>

<span data-ttu-id="21da7-107">ボットとメッセージング拡張機能の応答に対して、アダプティブカードの本文内に @ メンションを追加できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="21da7-107">You can now add @ mentions within an Adaptive card body for Bots and Messaging Extension responses.</span></span> <span data-ttu-id="21da7-108">カードの @ メンションは、通常のメッセージベースのメンションと同じ通知ロジックに従い、レンダリングします。</span><span class="sxs-lookup"><span data-stu-id="21da7-108">@ mentions in cards follow the same notification logic and rendering as that of a regular message based mentions.</span></span> <span data-ttu-id="21da7-109">なお、カードベースのメンションは、現在 Web およびデスクトップクライアントでのみサポートされており、近日中にモバイルクライアントでのレンダリングをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="21da7-109">Note that card based mentions are only supported in Web and Desktop clients today, with support for rendering in mobile clients coming soon.</span></span>

## <a name="adaptive-12-support"></a><span data-ttu-id="21da7-110">アダプティブ1.2 サポート</span><span class="sxs-lookup"><span data-stu-id="21da7-110">Adaptive 1.2 Support</span></span>

<span data-ttu-id="21da7-111">Microsoft Teams では、開発者向けプレビューで[アダプティブバージョン 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="21da7-111">Microsoft Teams now supports [Adaptive version 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) in Developer Preview.</span></span> <span data-ttu-id="21da7-112">[メディア要素](https://adaptivecards.io/explorer/Media.html)はまだサポートされていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="21da7-112">Note that [Media elements](https://adaptivecards.io/explorer/Media.html) aren't supported yet.</span></span>

## <a name="tabs-single-sign-on"></a><span data-ttu-id="21da7-113">タブシングルサインオン</span><span class="sxs-lookup"><span data-stu-id="21da7-113">Tabs Single Sign-On</span></span>

<span data-ttu-id="21da7-114">[シングルサインオン (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、デスクトップおよびモバイルでユーザーのログインと認証を行うことができます。これには、web コンテンツページから TEAMS JavaScript SDK を使用します。</span><span class="sxs-lookup"><span data-stu-id="21da7-114">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="21da7-115">利点の1つは、ユーザーがサインインする必要がないことです。また、プロファイルを使用してアプリに同意されると、そのタブ (mobile を含む) に自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="21da7-115">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="21da7-116">開発者向けプレビューは、1.5 以上のマニフェストバージョンで利用できます。</span><span class="sxs-lookup"><span data-stu-id="21da7-116">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="21da7-117">現在の実装では、限られた量のグラフ Api しか取得できませんが、既存の認証 API を使用して追加の Graph Api を取得するための回避策を提供しています。</span><span class="sxs-lookup"><span data-stu-id="21da7-117">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a><span data-ttu-id="21da7-118">モバイルで有効になっている個人用アプリ (静的タブと1-1 ボット)</span><span class="sxs-lookup"><span data-stu-id="21da7-118">Personal apps (static tabs and 1-1 bots) enabled on mobile</span></span>

<span data-ttu-id="21da7-119">インストールされている個人用アプリ (静的タブと1-1 ボット) は、モバイルデバイスのアプリトレイで利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="21da7-119">Installed personal apps (static tabs and 1-1 bots) are now available in the app tray on mobile devices.</span></span> <span data-ttu-id="21da7-120">設計ガイダンスについては、「[モバイルの設計ガイドライン](~/tabs/design/tabs-mobile.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="21da7-120">See [Design guidelines for mobile](~/tabs/design/tabs-mobile.md) for design guidance.</span></span> <span data-ttu-id="21da7-121">アプリは、デスクトップまたは web クライアントからのみインストールでき、インストール後にモバイルで利用できるようになるまで最大4時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="21da7-121">Apps can only be installed from a desktop or web client, and can take up to 4 hours to be available on mobile after installation.</span></span>

<span data-ttu-id="21da7-122">これには、システム管理者が[アプリのセットアップポリシー](/microsoftteams/teams-app-setup-policies)を使用してアプリを事前にピン留めする機能が含まれます。</span><span class="sxs-lookup"><span data-stu-id="21da7-122">This includes the ability for a system administrator to pre-pin an app via [app setup policies](/microsoftteams/teams-app-setup-policies).</span></span> <span data-ttu-id="21da7-123">固定されたアプリは、アプリのドロアーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="21da7-123">Apps that have pinned will be displayed in the app drawer.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="21da7-124">通話とオンライン会議のボット</span><span class="sxs-lookup"><span data-stu-id="21da7-124">Calls and online meeting bots</span></span>

<span data-ttu-id="21da7-125">Microsoft [Graph api を呼び出しとオンライン会議に](/graph/api/resources/communications-api-overview?view=graph-rest-beta)追加することで、microsoft Teams アプリは音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="21da7-125">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="21da7-126">これらの Api を使用すると、対話式音声応答 (IVR)、通話コントロール、通話と会議のリアルタイムの音声/ビデオストリームへのアクセス、デスクトップやアプリの共有など、新しいアプリ機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="21da7-126">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="21da7-127">通話とオンライン会議のボットを作成して開発する方法について、[概要](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)から始まる新しいセクションを追加しました。</span><span class="sxs-lookup"><span data-stu-id="21da7-127">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>
