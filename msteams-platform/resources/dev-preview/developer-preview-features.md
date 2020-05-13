---
title: 公開開発者プレビューの機能
description: Microsoft Teams の公開開発者プレビューの機能について説明します。
keywords: teams のプレビュー開発者向け機能
ms.openlocfilehash: 7ed442072779917dcc5db3ebcb4afaac9db0407f
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210702"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="58621-104">Microsoft Teams の公開開発者プレビューの機能</span><span class="sxs-lookup"><span data-stu-id="58621-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="58621-105">開発者プレビューには、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="58621-105">The developer preview includes the following new features:</span></span>

## <a name="adaptive-cards-v12-support"></a><span data-ttu-id="58621-106">アダプティブカード1.2 のサポート</span><span class="sxs-lookup"><span data-stu-id="58621-106">Adaptive cards v1.2 support</span></span>

<span data-ttu-id="58621-107">Teams での[アダプティブカード](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)v2.0 のサポートは、一般公開されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="58621-107">Support for [Adaptive cards v1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) in Teams is now available to the general public.</span></span> <span data-ttu-id="58621-108">ただし、 [Media 要素](https://adaptivecards.io/explorer/Media.html)は、Teams プラットフォームのアダプティブカード v2.0 では現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="58621-108">However, [Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="58621-109">タブシングルサインオン (SSO)</span><span class="sxs-lookup"><span data-stu-id="58621-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="58621-110">[シングルサインオン (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、デスクトップおよびモバイルでユーザーのログインと認証を行うことができます。これには、web コンテンツページから TEAMS JavaScript SDK を使用します。</span><span class="sxs-lookup"><span data-stu-id="58621-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="58621-111">利点の1つは、ユーザーがサインインする必要がないことです。また、プロファイルを使用してアプリに同意されると、そのタブ (mobile を含む) に自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="58621-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="58621-112">開発者向けプレビューは、1.5 以上のマニフェストバージョンで利用できます。</span><span class="sxs-lookup"><span data-stu-id="58621-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="58621-113">現在の実装では、限られた量のグラフ Api しか取得できませんが、既存の認証 API を使用して追加の Graph Api を取得するための回避策を提供しています。</span><span class="sxs-lookup"><span data-stu-id="58621-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a><span data-ttu-id="58621-114">モバイルで有効になっている個人用アプリ (静的タブと1-1 ボット)</span><span class="sxs-lookup"><span data-stu-id="58621-114">Personal apps (static tabs and 1-1 bots) enabled on mobile</span></span>

<span data-ttu-id="58621-115">インストールされている個人用アプリ (静的タブと1-1 ボット) は、モバイルデバイスのアプリトレイで利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="58621-115">Installed personal apps (static tabs and 1-1 bots) are now available in the app tray on mobile devices.</span></span> <span data-ttu-id="58621-116">設計ガイダンスについては、「[モバイルの設計ガイドライン](~/tabs/design/tabs-mobile.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="58621-116">See [Design guidelines for mobile](~/tabs/design/tabs-mobile.md) for design guidance.</span></span> <span data-ttu-id="58621-117">アプリは、デスクトップまたは web クライアントからのみインストールでき、インストール後にモバイルで利用できるようになるまで最大4時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="58621-117">Apps can only be installed from a desktop or web client, and can take up to 4 hours to be available on mobile after installation.</span></span>

<span data-ttu-id="58621-118">これには、システム管理者が[アプリのセットアップポリシー](/microsoftteams/teams-app-setup-policies)を使用してアプリを事前にピン留めする機能が含まれます。</span><span class="sxs-lookup"><span data-stu-id="58621-118">This includes the ability for a system administrator to pre-pin an app via [app setup policies](/microsoftteams/teams-app-setup-policies).</span></span> <span data-ttu-id="58621-119">固定されたアプリは、アプリのドロアーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="58621-119">Apps that have pinned will be displayed in the app drawer.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="58621-120">通話とオンライン会議のボット</span><span class="sxs-lookup"><span data-stu-id="58621-120">Calls and online meeting bots</span></span>

<span data-ttu-id="58621-121">Microsoft [Graph api を呼び出しとオンライン会議に](/graph/api/resources/communications-api-overview?view=graph-rest-beta)追加することで、microsoft Teams アプリは音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="58621-121">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="58621-122">これらの Api を使用すると、対話式音声応答 (IVR)、通話コントロール、通話と会議のリアルタイムの音声/ビデオストリームへのアクセス、デスクトップやアプリの共有など、新しいアプリ機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="58621-122">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="58621-123">通話とオンライン会議のボットを作成して開発する方法について、[概要](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)から始まる新しいセクションを追加しました。</span><span class="sxs-lookup"><span data-stu-id="58621-123">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>
