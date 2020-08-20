---
title: パブリック サーバーの機能Developer Preview
description: Microsoft Teams の一般のパブリック コンテンツDeveloper Previewについて説明します
keywords: Teams のプレビュー開発者向け機能
ms.openlocfilehash: e607a6c65253a5fd94f8a805f1264a567bb8fd24
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819176"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="58084-104">Microsoft Teams のパブリック web サイトDeveloper Preview機能</span><span class="sxs-lookup"><span data-stu-id="58084-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="58084-105">開発者プレビューには、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="58084-105">The developer preview includes the following new features:</span></span>

## <a name="adaptive-cards-v12-support"></a><span data-ttu-id="58084-106">アダプティブ カード v1.2 のサポート</span><span class="sxs-lookup"><span data-stu-id="58084-106">Adaptive cards v1.2 support</span></span>

<span data-ttu-id="58084-107">Teams での [アダプティブ カード v1.2 の](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) サポートが、一般のパブリックで利用可能になりました。</span><span class="sxs-lookup"><span data-stu-id="58084-107">Support for [Adaptive cards v1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) in Teams is now available to the general public.</span></span> <span data-ttu-id="58084-108">ただし [、Teams プラットフォームの](https://adaptivecards.io/explorer/Media.html) アダプティブ カード v1.2 では、現在、Media 要素はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="58084-108">However, [Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="58084-109">タブ シングル サインオン (SSO)</span><span class="sxs-lookup"><span data-stu-id="58084-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="58084-110">シングル サインオン [(SSO) を使用して、Web コンテンツ](~/tabs/how-to/authentication/auth-aad-sso.md) ページからの Teams JavaScript SDK を使用して、デスクトップおよびモバイル上のユーザーのログインおよび認証を行うことができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="58084-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="58084-111">その利点の 1 つに、ユーザーがサインインする必要がないことです。プロファイルを使ってアプリに同意した後は、そのタブ (モバイルを含む) に自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="58084-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="58084-112">当社の開発者プレビューは、1.5 以降のマニフェスト バージョンで利用可能です。</span><span class="sxs-lookup"><span data-stu-id="58084-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="58084-113">現在の実装では、限定された量の Graph API しか取得できませんが、既存の認証 API を使用して追加の Graph API を取得するための回避策が提供されています。</span><span class="sxs-lookup"><span data-stu-id="58084-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="58084-114">通話ボットとオンライン会議ボット</span><span class="sxs-lookup"><span data-stu-id="58084-114">Calls and online meeting bots</span></span>

<span data-ttu-id="58084-115">通話およびオンライン会議 [用の Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta)が追加されているため、Microsoft Teams アプリは、音声やビデオを使用して豊富な方法でユーザーと対話できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="58084-115">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="58084-116">これらの API を使用すると、インタブル音声応答 (IVR)、通話コントロール、通話や会議でのリアルタイムのオーディオやビデオ ストリームへのアクセスなどの新しいアプリ機能 (デスクトップやアプリの共有など) を追加できます。</span><span class="sxs-lookup"><span data-stu-id="58084-116">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="58084-117">通話およびオンライン会議ボットの作成方法について、概要から新しいセクションが追加 [されました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="58084-117">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>
