---
title: デバイスの機能 - 概要
author: Rajeshwari-v
description: ネイティブ デバイスの機能の概要。
ms.author: surbhigupta
keywords: カメラ画像メディアマイクマイクQRコードQRコードバーコードバーコードスキャンスキャナ位置マップ機能ネイティブデバイスの権限
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 8df8341e8996e4bf380575ac59e05325da16bd0d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566195"
---
# <a name="device-capabilities"></a><span data-ttu-id="62e9d-104">デバイス機能</span><span class="sxs-lookup"><span data-stu-id="62e9d-104">Device capabilities</span></span>

<span data-ttu-id="62e9d-105">Microsoft Teamsプラットフォームは、組み込みのファーストパーティ エクスペリエンスに合わせて開発者の機能を継続的に強化しています。</span><span class="sxs-lookup"><span data-stu-id="62e9d-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="62e9d-106">強化されたTeamsプラットフォームにより、パートナーは、カメラ、QRまたはバーコードスキャナ、フォトギャラリー、マイク、位置情報などのデバイス機能をWebアプリと統合できます。</span><span class="sxs-lookup"><span data-stu-id="62e9d-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="62e9d-107">この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティに新しいシナリオやユースケースが生まれます。</span><span class="sxs-lookup"><span data-stu-id="62e9d-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="62e9d-108">ネイティブ デバイスの機能</span><span class="sxs-lookup"><span data-stu-id="62e9d-108">Native device capabilities</span></span>

<span data-ttu-id="62e9d-109">モバイルデバイスまたはデスクトップデバイスには、機能と呼ばれるカメラやマイクなどのデバイスが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="62e9d-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="62e9d-110">モバイルまたはデスクトップ上の以下のデバイス機能には[、JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)で使用できる専用の API Microsoft Teamsアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="62e9d-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="62e9d-111">メディア機能 (次の例)</span><span class="sxs-lookup"><span data-stu-id="62e9d-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="62e9d-112">カメラ</span><span class="sxs-lookup"><span data-stu-id="62e9d-112">Camera</span></span>
    * <span data-ttu-id="62e9d-113">マイク</span><span class="sxs-lookup"><span data-stu-id="62e9d-113">Microphone</span></span>
    * <span data-ttu-id="62e9d-114">ギャラリー</span><span class="sxs-lookup"><span data-stu-id="62e9d-114">Gallery</span></span>
    * <span data-ttu-id="62e9d-115">QRまたはバーコードスキャナ</span><span class="sxs-lookup"><span data-stu-id="62e9d-115">QR or barcode scanner</span></span>
* <span data-ttu-id="62e9d-116">場所</span><span class="sxs-lookup"><span data-stu-id="62e9d-116">Location</span></span>

<span data-ttu-id="62e9d-117">デバイス機能にアクセスした後、それらをTeamsプラットフォームと統合して、コラボレーションエクスペリエンスを強化できます。</span><span class="sxs-lookup"><span data-stu-id="62e9d-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="62e9d-118">デバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="62e9d-118">Request device permissions</span></span>

<span data-ttu-id="62e9d-119">[JavaScript クライアント SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)に用意されているツールを使用して、ネイティブ デバイスの機能にアクセスするために必要な[アクセス許可](native-device-permissions.md)を要求します。</span><span class="sxs-lookup"><span data-stu-id="62e9d-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="62e9d-120">これらの機能へのアクセスは、最新の Web ブラウザーでは標準的ですが、アプリ マニフェストを更新して、使用している機能についてTeamsに通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="62e9d-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="62e9d-121">この更新プログラムを使用すると、モバイルまたはデスクトップ クライアントでアプリを実行しているときに、アクセス許可Teams要求できます。</span><span class="sxs-lookup"><span data-stu-id="62e9d-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="62e9d-122">デバイス機能の統合</span><span class="sxs-lookup"><span data-stu-id="62e9d-122">Integrate device capabilities</span></span>

<span data-ttu-id="62e9d-123">デバイス機能にアクセスしたら、Teamsメディア機能 API を使用して[、メディア機能](mobile-camera-image-permissions.md)をTeamsプラットフォームと統合して、ユーザー エクスペリエンスを向上させます。</span><span class="sxs-lookup"><span data-stu-id="62e9d-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="62e9d-124">これらの統合機能により、アプリは次の機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="62e9d-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="62e9d-125">画像をキャプチャして共有します。</span><span class="sxs-lookup"><span data-stu-id="62e9d-125">Capture and share images.</span></span>
* <span data-ttu-id="62e9d-126">[スキャナコントロール](qr-barcode-scanner-capability.md)を使用してQRまたはバーコードをスキャンします。</span><span class="sxs-lookup"><span data-stu-id="62e9d-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md).</span></span>
* <span data-ttu-id="62e9d-127">マイクを通してオーディオを録音します。</span><span class="sxs-lookup"><span data-stu-id="62e9d-127">Record audio through microphone.</span></span>
* <span data-ttu-id="62e9d-128">[場所の選択を](location-capability.md)使用して場所を共有します。</span><span class="sxs-lookup"><span data-stu-id="62e9d-128">Share location using [location picker](location-capability.md).</span></span>
