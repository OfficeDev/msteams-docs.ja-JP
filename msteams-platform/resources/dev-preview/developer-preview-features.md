---
title: パブリック サービスのDeveloper Preview
description: '[パブリック] ページの機能Microsoft Teams詳細Developer Preview'
ms.topic: reference
localization_priority: Normal
keywords: teams プレビュー開発者向け機能
ms.openlocfilehash: 84683420a5c61bb1eb493f8191bfbcbe97f6fb46
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230905"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="fa131-104">パブリック サービスの機能Developer Preview Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fa131-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="fa131-105">このページは 2021 年 6 月に廃止される予定です。</span><span class="sxs-lookup"><span data-stu-id="fa131-105">This page will be deprecated in June 2021.</span></span> <span data-ttu-id="fa131-106">開発者プレビューで利用できる機能の詳細については、「 [新機能」を参照してください。](~/whats-new.md)</span><span class="sxs-lookup"><span data-stu-id="fa131-106">For information on features available for developer preview, see [What's new?](~/whats-new.md)</span></span>

<span data-ttu-id="fa131-107">開発者プレビューには、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="fa131-107">The developer preview includes the following new features:</span></span>

## <a name="app-customization"></a><span data-ttu-id="fa131-108">アプリのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="fa131-108">App customization</span></span>

<span data-ttu-id="fa131-109">これで、組織のニーズに基づいて、Teamsをカスタマイズまたは再ブランド化できるプロパティの選択セットを定義できます。</span><span class="sxs-lookup"><span data-stu-id="fa131-109">You can now define a select set of properties, which a Teams admin can customize or rebrand based on their organization's need.</span></span> <span data-ttu-id="fa131-110">詳細については、「アプリのカスタマイズ [機能」を参照してください](~/concepts/design/design-teams-app-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="fa131-110">For more information, see [app customization feature](~/concepts/design/design-teams-app-overview.md).</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="fa131-111">タブのシングル サインオン (SSO)</span><span class="sxs-lookup"><span data-stu-id="fa131-111">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="fa131-112">シングル サインオン[(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md)を使用して、Web コンテンツ ページから javaScript SDK の Teamsを使用してデスクトップとモバイルでユーザーにログインして認証できます。</span><span class="sxs-lookup"><span data-stu-id="fa131-112">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="fa131-113">利点の 1 つは、ユーザーがサインインする必要がなさったことです。プロファイルを使用してアプリに同意すると、自動的にタブ (モバイルを含む) にサインインします。</span><span class="sxs-lookup"><span data-stu-id="fa131-113">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="fa131-114">開発者向けプレビューは、マニフェスト バージョン 1.5 以上で利用できます。</span><span class="sxs-lookup"><span data-stu-id="fa131-114">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="fa131-115">現在の実装では、限られた量の API のみを取得Graph、既存の認証 API を使用して追加の API を取得Graph回避策を提供します。</span><span class="sxs-lookup"><span data-stu-id="fa131-115">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="fa131-116">通話とオンライン会議ボット</span><span class="sxs-lookup"><span data-stu-id="fa131-116">Calls and online meeting bots</span></span>

<span data-ttu-id="fa131-117">通話やオンライン会議用[の Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)が追加されたので、Microsoft Teams アプリは音声とビデオを使用して豊富な方法でユーザーとやり取りできます。</span><span class="sxs-lookup"><span data-stu-id="fa131-117">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="fa131-118">これらの API を使用すると、対話型音声応答 (IVR)、通話制御、デスクトップやアプリ共有などの通話や会議のリアルタイムオーディオストリームやビデオ ストリームへのアクセスなどの新しいアプリ機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="fa131-118">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="fa131-119">概要から始まる通話とオンライン会議ボットを作成および開発する方法に関する新しいセクションが追加 [されました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="fa131-119">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>


## <a name="image-enlarge-support"></a><span data-ttu-id="fa131-120">画像の拡大サポート</span><span class="sxs-lookup"><span data-stu-id="fa131-120">Image enlarge support</span></span>

<span data-ttu-id="fa131-121">ボットは、アダプティブ カード内で共有されているイメージを拡大Teams可能です。</span><span class="sxs-lookup"><span data-stu-id="fa131-121">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="fa131-122">これは、ボットを介して詳細な詳細な視覚的ガイドを共有するなどのシナリオで役立ちます。それ以外の場合はユーザーにとって読みにくい場合があります。</span><span class="sxs-lookup"><span data-stu-id="fa131-122">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="fa131-123">イメージを展開可能にするには、次のようにフラグ `allowExpand: true` を設定します。</span><span class="sxs-lookup"><span data-stu-id="fa131-123">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="fa131-124">これにより、web/Teamsクライアントがイメージにカーソルを合わせると、ユーザーがイメージを展開できます。</span><span class="sxs-lookup"><span data-stu-id="fa131-124">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>
