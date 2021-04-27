---
title: パブリック サービスのDeveloper Preview
description: Details the features in the Microsoft Teams Public Developer Preview
ms.topic: reference
localization_priority: Normal
keywords: teams プレビュー開発者向け機能
ms.openlocfilehash: 38acccedacb86437f5e6c949b674c0a62bbbd63c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020619"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="d335d-104">Microsoft Teams のパブリック Developer Preview機能</span><span class="sxs-lookup"><span data-stu-id="d335d-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="d335d-105">開発者プレビューには、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d335d-105">The developer preview includes the following new features:</span></span>

## <a name="app-customization"></a><span data-ttu-id="d335d-106">アプリのカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="d335d-106">App customization</span></span>

<span data-ttu-id="d335d-107">Teams 管理者が組織のニーズに基づいてカスタマイズまたは再ブランド化できるプロパティの選択セットを定義できます。</span><span class="sxs-lookup"><span data-stu-id="d335d-107">You can now define a select set of properties, which a Teams admin can customize or rebrand based on their organization's need.</span></span> <span data-ttu-id="d335d-108">詳細については、「アプリのカスタマイズ [機能」を参照してください](~/concepts/design/design-teams-app-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d335d-108">For more information, see [app customization feature](~/concepts/design/design-teams-app-overview.md).</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="d335d-109">タブのシングル サインオン (SSO)</span><span class="sxs-lookup"><span data-stu-id="d335d-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="d335d-110">Web コンテンツ ページから Teams JavaScript SDK を使用して、シングル サインオン [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) を使用してデスクトップとモバイルでユーザーにログインして認証できます。</span><span class="sxs-lookup"><span data-stu-id="d335d-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="d335d-111">利点の 1 つは、ユーザーがサインインする必要がなさったことです。プロファイルを使用してアプリに同意すると、自動的にタブ (モバイルを含む) にサインインします。</span><span class="sxs-lookup"><span data-stu-id="d335d-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="d335d-112">開発者向けプレビューは、マニフェスト バージョン 1.5 以上で利用できます。</span><span class="sxs-lookup"><span data-stu-id="d335d-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="d335d-113">現在の実装では、グラフ API の量は限られていますが、既存の認証 API を使用して追加の Graph API を取得するための回避策を提供しています。</span><span class="sxs-lookup"><span data-stu-id="d335d-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="d335d-114">通話とオンライン会議ボット</span><span class="sxs-lookup"><span data-stu-id="d335d-114">Calls and online meeting bots</span></span>

<span data-ttu-id="d335d-115">通話やオンライン会議に [Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)が追加されたので、Microsoft Teams アプリは音声とビデオを使用してユーザーと豊富なやり取りを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="d335d-115">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="d335d-116">これらの API を使用すると、対話型音声応答 (IVR)、通話制御、デスクトップやアプリ共有などの通話や会議のリアルタイムオーディオストリームやビデオ ストリームへのアクセスなどの新しいアプリ機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="d335d-116">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="d335d-117">概要から始まる通話とオンライン会議ボットを作成および開発する方法に関する新しいセクションが追加 [されました](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d335d-117">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>


## <a name="image-enlarge-support"></a><span data-ttu-id="d335d-118">画像の拡大サポート</span><span class="sxs-lookup"><span data-stu-id="d335d-118">Image enlarge support</span></span>

<span data-ttu-id="d335d-119">ボットは、Teams のアダプティブ カードで共有されているイメージを拡大して表示できます。</span><span class="sxs-lookup"><span data-stu-id="d335d-119">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="d335d-120">これは、ボットを介して詳細な詳細な視覚的ガイドを共有するなどのシナリオで役立ちます。それ以外の場合はユーザーにとって読みにくい場合があります。</span><span class="sxs-lookup"><span data-stu-id="d335d-120">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="d335d-121">イメージを展開可能にするには、次のようにフラグ `allowExpand: true` を設定します。</span><span class="sxs-lookup"><span data-stu-id="d335d-121">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="d335d-122">これにより、Teams の Web/デスクトップ クライアントは、イメージにカーソルを合わせると要素がレンダリングされ、ユーザーがイメージを展開できます。</span><span class="sxs-lookup"><span data-stu-id="d335d-122">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

