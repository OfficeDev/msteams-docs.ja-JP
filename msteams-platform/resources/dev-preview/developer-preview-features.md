---
title: パブリック サービスのDeveloper Preview
description: Microsoft Teams パブリック サービスの機能のDeveloper Preview
ms.topic: reference
keywords: Teams プレビュー開発者向け機能
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014356"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="b4599-104">Microsoft Teams のパブリック Developer Preview機能</span><span class="sxs-lookup"><span data-stu-id="b4599-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="b4599-105">開発者プレビューには、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="b4599-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="b4599-106">タブ のシングル サインオン (SSO)</span><span class="sxs-lookup"><span data-stu-id="b4599-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="b4599-107">シングル サインオン [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) を使用して、Web コンテンツ ページから Teams JavaScript SDK を使用して、デスクトップとモバイルでユーザーをログインおよび認証できます。</span><span class="sxs-lookup"><span data-stu-id="b4599-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="b4599-108">その利点の 1 つは、ユーザーがサインインする必要がなさらないという利点の 1 つです。プロファイルを使ってアプリに同意すると、タブ (モバイルを含む) に自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="b4599-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="b4599-109">開発者プレビューは、マニフェスト バージョン 1.5 以上で利用できます。</span><span class="sxs-lookup"><span data-stu-id="b4599-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="b4599-110">現在の実装では、Graph API の量は限られていますが、既存の認証 API を使用して追加の Graph API を取得するための回避策を提供しています。</span><span class="sxs-lookup"><span data-stu-id="b4599-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="b4599-111">通話とオンライン会議ボット</span><span class="sxs-lookup"><span data-stu-id="b4599-111">Calls and online meeting bots</span></span>

<span data-ttu-id="b4599-112">通話やオンライン会議用 [の Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta)が追加されたので、Microsoft Teams アプリは音声とビデオを使用して豊富な方法でユーザーと対話できます。</span><span class="sxs-lookup"><span data-stu-id="b4599-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="b4599-113">これらの API を使用すると、対話型音声応答 (IVR)、通話制御、通話や、通話や会議のリアルタイムの音声ストリームやビデオ ストリーム (デスクトップやアプリ共有など) へのアクセスなどの新しいアプリ機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="b4599-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="b4599-114">概要から始め、通話とオンライン会議ボットを作成および開発する方法に関する新しいセクションを追加 [しました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b4599-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="b4599-115">画像の拡大サポート</span><span class="sxs-lookup"><span data-stu-id="b4599-115">Image enlarge support</span></span>

<span data-ttu-id="b4599-116">ボットは、Teams のアダプティブ カードで共有されている画像を拡大できる画像を示す機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="b4599-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="b4599-117">これは、ユーザーにとって読みにくい詳細な視覚的ガイドをボット経由で共有するなどのシナリオで役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b4599-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="b4599-118">イメージを展開可能にする場合は、次のようにフラグ `allowExpand: true` を設定します。</span><span class="sxs-lookup"><span data-stu-id="b4599-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="b4599-119">これにより、Teams Web/デスクトップ クライアントは、ユーザーがイメージを展開するために、イメージの上にホバーした時点で要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="b4599-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

