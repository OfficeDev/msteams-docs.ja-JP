---
title: デバイス機能の概要
description: ネイティブ デバイス機能の概要。
keywords: カメラ イメージ メディア マイク機能ネイティブ デバイスのアクセス許可
ms.topic: overview
ms.openlocfilehash: 8b2f92cb4586d646bde02742883122bb009847ea
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50232850"
---
# <a name="device-capabilities"></a><span data-ttu-id="7bc61-104">デバイス機能</span><span class="sxs-lookup"><span data-stu-id="7bc61-104">Device capabilities</span></span> 

<span data-ttu-id="7bc61-105">Microsoft Teams プラットフォームは、組み込みのファースト パーティエクスペリエンスに合わせて、開発者の機能を継続的に強化しています。</span><span class="sxs-lookup"><span data-stu-id="7bc61-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="7bc61-106">強化された Teams プラットフォームにより、パートナーはカメラ、フォト ギャラリー、マイク、位置情報などのデバイス機能を Web アプリと統合できます。</span><span class="sxs-lookup"><span data-stu-id="7bc61-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, photo gallery, microphone, and location, with their web apps.</span></span> <span data-ttu-id="7bc61-107">この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティの新しいシナリオや使用事例が作成されます。</span><span class="sxs-lookup"><span data-stu-id="7bc61-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="7bc61-108">ネイティブ デバイスの機能</span><span class="sxs-lookup"><span data-stu-id="7bc61-108">Native device capabilities</span></span>

<span data-ttu-id="7bc61-109">モバイルデバイスまたはデスクトップ デバイスには、機能と呼ばれるカメラやマイクなどの組み込みデバイスがあります。</span><span class="sxs-lookup"><span data-stu-id="7bc61-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="7bc61-110">Microsoft Teams JavaScript クライアント SDK で利用可能な専用 API を使用して、モバイルまたはデスクトップで次のデバイス [機能にアクセスできます](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7bc61-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="7bc61-111">メディア機能 (次に例を示します)</span><span class="sxs-lookup"><span data-stu-id="7bc61-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="7bc61-112">カメラ</span><span class="sxs-lookup"><span data-stu-id="7bc61-112">Camera</span></span>
    * <span data-ttu-id="7bc61-113">マイク</span><span class="sxs-lookup"><span data-stu-id="7bc61-113">Microphone</span></span>
    * <span data-ttu-id="7bc61-114">ギャラリー</span><span class="sxs-lookup"><span data-stu-id="7bc61-114">Gallery</span></span>
* <span data-ttu-id="7bc61-115">場所</span><span class="sxs-lookup"><span data-stu-id="7bc61-115">Location</span></span>

<span data-ttu-id="7bc61-116">デバイスの機能にアクセスした後、Teams プラットフォームと統合して共同作業のエクスペリエンスを強化できます。</span><span class="sxs-lookup"><span data-stu-id="7bc61-116">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="7bc61-117">デバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="7bc61-117">Request device permissions</span></span>

<span data-ttu-id="7bc61-118">[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK に用意されているツール[](native-device-permissions.md)を使用して、ネイティブ デバイス機能にアクセスするために必要なアクセス許可を要求します。</span><span class="sxs-lookup"><span data-stu-id="7bc61-118">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to  request the required  [permissions](native-device-permissions.md) for  accessing the native device capabilities.</span></span> <span data-ttu-id="7bc61-119">これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して、使用している機能について Teams に通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7bc61-119">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="7bc61-120">この更新プログラムでは、アプリが Teams モバイルまたはデスクトップ クライアントで実行されている間にアクセス許可を要求できます。</span><span class="sxs-lookup"><span data-stu-id="7bc61-120">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="7bc61-121">デバイス機能の統合</span><span class="sxs-lookup"><span data-stu-id="7bc61-121">Integrate device capabilities</span></span>

<span data-ttu-id="7bc61-122">デバイス機能にアクセスした後 **、Teams** のメディア機能 API を [](mobile-camera-image-permissions.md)使用して Teams プラットフォームと機能を統合し、ユーザー エクスペリエンスを強化します。</span><span class="sxs-lookup"><span data-stu-id="7bc61-122">After getting access to device capabilities,use **Teams media capability APIs** to [integrate the capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="7bc61-123">これらの統合された機能を使って、アプリは次の機能を実行できます。</span><span class="sxs-lookup"><span data-stu-id="7bc61-123">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="7bc61-124">画像のキャプチャと共有</span><span class="sxs-lookup"><span data-stu-id="7bc61-124">Capture and share images</span></span>
* <span data-ttu-id="7bc61-125">マイクを使用してオーディオを録音する</span><span class="sxs-lookup"><span data-stu-id="7bc61-125">Record audio through microphone</span></span>
* <span data-ttu-id="7bc61-126">場所情報を共有する</span><span class="sxs-lookup"><span data-stu-id="7bc61-126">Share the location information</span></span>


