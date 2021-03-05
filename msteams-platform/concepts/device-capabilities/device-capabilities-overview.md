---
title: デバイス機能の概要
description: ネイティブ デバイス機能の概要。
keywords: カメラ イメージ メディア マイク マイク QR コード qrcode バーコード バーコード スキャン スキャナーの場所マップ機能ネイティブ デバイスのアクセス許可
ms.topic: overview
ms.openlocfilehash: 4c826d1705dfeea1feea21b02e7be51789817e48
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449592"
---
# <a name="device-capabilities"></a><span data-ttu-id="f025b-104">デバイス機能</span><span class="sxs-lookup"><span data-stu-id="f025b-104">Device capabilities</span></span> 

<span data-ttu-id="f025b-105">Microsoft Teams プラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。</span><span class="sxs-lookup"><span data-stu-id="f025b-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="f025b-106">強化された Teams プラットフォームを使用すると、パートナーは、カメラ、QR、バーコード スキャナー、フォト ギャラリー、マイク、場所などのデバイス機能を Web アプリと統合できます。</span><span class="sxs-lookup"><span data-stu-id="f025b-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="f025b-107">この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティの新しいシナリオや使用例が作成されます。</span><span class="sxs-lookup"><span data-stu-id="f025b-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="f025b-108">ネイティブ デバイスの機能</span><span class="sxs-lookup"><span data-stu-id="f025b-108">Native device capabilities</span></span>

<span data-ttu-id="f025b-109">モバイルデバイスまたはデスクトップ デバイスには、機能と呼ばれるカメラやマイクなどの組み込みデバイスがあります。</span><span class="sxs-lookup"><span data-stu-id="f025b-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="f025b-110">Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、モバイルまたはデスクトップで次の [デバイス機能にアクセスできます](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f025b-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="f025b-111">メディア機能 (次のような)</span><span class="sxs-lookup"><span data-stu-id="f025b-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="f025b-112">カメラ</span><span class="sxs-lookup"><span data-stu-id="f025b-112">Camera</span></span>
    * <span data-ttu-id="f025b-113">マイク</span><span class="sxs-lookup"><span data-stu-id="f025b-113">Microphone</span></span>
    * <span data-ttu-id="f025b-114">ギャラリー</span><span class="sxs-lookup"><span data-stu-id="f025b-114">Gallery</span></span>
    * <span data-ttu-id="f025b-115">QR またはバーコード スキャナー</span><span class="sxs-lookup"><span data-stu-id="f025b-115">QR or barcode scanner</span></span>
* <span data-ttu-id="f025b-116">Location</span><span class="sxs-lookup"><span data-stu-id="f025b-116">Location</span></span>

<span data-ttu-id="f025b-117">デバイス機能にアクセスした後、それらを Teams プラットフォームと統合して、共同作業のエクスペリエンスを強化できます。</span><span class="sxs-lookup"><span data-stu-id="f025b-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="f025b-118">デバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="f025b-118">Request device permissions</span></span>

<span data-ttu-id="f025b-119">[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK にあるツールを使用[](native-device-permissions.md)して、ネイティブ デバイス機能にアクセスするために必要なアクセス許可を要求します。</span><span class="sxs-lookup"><span data-stu-id="f025b-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="f025b-120">これらの機能へのアクセスは、最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用している機能について Teams に通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f025b-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="f025b-121">この更新プログラムを使用すると、アプリが Teams モバイル またはデスクトップ クライアントで実行されている間にアクセス許可を要求できます。</span><span class="sxs-lookup"><span data-stu-id="f025b-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="f025b-122">デバイス機能の統合</span><span class="sxs-lookup"><span data-stu-id="f025b-122">Integrate device capabilities</span></span>

<span data-ttu-id="f025b-123">デバイス機能にアクセスした後、Teams メディア機能 API を使用[](mobile-camera-image-permissions.md)して、メディア機能を Teams プラットフォームと統合してユーザー エクスペリエンスを向上します。</span><span class="sxs-lookup"><span data-stu-id="f025b-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="f025b-124">これらの統合機能を使用すると、アプリは次の機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="f025b-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="f025b-125">画像のキャプチャと共有</span><span class="sxs-lookup"><span data-stu-id="f025b-125">Capture and share images</span></span>
* <span data-ttu-id="f025b-126">スキャナーコントロールを使用して QR またはバーコード [をスキャンする](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="f025b-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md)</span></span>
* <span data-ttu-id="f025b-127">マイクでオーディオを録音する</span><span class="sxs-lookup"><span data-stu-id="f025b-127">Record audio through microphone</span></span>
* <span data-ttu-id="f025b-128">場所ピッカーを使用 [して場所を共有します](location-capability.md)。</span><span class="sxs-lookup"><span data-stu-id="f025b-128">Share location using [location picker](location-capability.md).</span></span>
