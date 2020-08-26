---
title: 公開開発者プレビューの機能
description: Microsoft Teams の公開開発者プレビューの機能について説明します。
keywords: teams のプレビュー開発者向け機能
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874843"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="2d8e0-104">Microsoft Teams の公開開発者プレビューの機能</span><span class="sxs-lookup"><span data-stu-id="2d8e0-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="2d8e0-105">開発者プレビューには、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="2d8e0-106">タブシングルサインオン (SSO)</span><span class="sxs-lookup"><span data-stu-id="2d8e0-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="2d8e0-107">[シングルサインオン (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、デスクトップおよびモバイルでユーザーのログインと認証を行うことができます。これには、web コンテンツページから TEAMS JavaScript SDK を使用します。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="2d8e0-108">利点の1つは、ユーザーがサインインする必要がないことです。また、プロファイルを使用してアプリに同意されると、そのタブ (mobile を含む) に自動的にサインインします。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="2d8e0-109">開発者向けプレビューは、1.5 以上のマニフェストバージョンで利用できます。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="2d8e0-110">現在の実装では、限られた量のグラフ Api しか取得できませんが、既存の認証 API を使用して追加の Graph Api を取得するための回避策を提供しています。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="2d8e0-111">通話とオンライン会議のボット</span><span class="sxs-lookup"><span data-stu-id="2d8e0-111">Calls and online meeting bots</span></span>

<span data-ttu-id="2d8e0-112">Microsoft [Graph api を呼び出しとオンライン会議に](/graph/api/resources/communications-api-overview?view=graph-rest-beta)追加することで、microsoft Teams アプリは音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="2d8e0-113">これらの Api を使用すると、対話式音声応答 (IVR)、通話コントロール、通話と会議のリアルタイムの音声/ビデオストリームへのアクセス、デスクトップやアプリの共有など、新しいアプリ機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="2d8e0-114">通話とオンライン会議のボットを作成して開発する方法について、 [概要](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)から始まる新しいセクションを追加しました。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="2d8e0-115">画像の拡大サポート</span><span class="sxs-lookup"><span data-stu-id="2d8e0-115">Image enlarge support</span></span>

<span data-ttu-id="2d8e0-116">Teams のアダプティブカードで共有されている画像を拡大することができます。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="2d8e0-117">これは、ユーザーにとって特に難しい bot から、詳細なステップごとのビジュアルガイドを共有する場合などに便利です。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="2d8e0-118">画像を展開可能にするには、次のようにフラグを設定し `allowExpand: true` ます。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="2d8e0-119">これにより、Teams の web/デスクトップクライアントは、画像をポイントしたときに、イメージを拡張するための要素を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="2d8e0-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

