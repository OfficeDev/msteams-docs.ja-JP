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
# <a name="device-capabilities"></a>デバイス機能

Microsoft Teamsプラットフォームは、組み込みのファーストパーティ エクスペリエンスに合わせて開発者の機能を継続的に強化しています。 強化されたTeamsプラットフォームにより、パートナーは、カメラ、QRまたはバーコードスキャナ、フォトギャラリー、マイク、位置情報などのデバイス機能をWebアプリと統合できます。 この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティに新しいシナリオやユースケースが生まれます。

## <a name="native-device-capabilities"></a>ネイティブ デバイスの機能

モバイルデバイスまたはデスクトップデバイスには、機能と呼ばれるカメラやマイクなどのデバイスが組み込まれています。 モバイルまたはデスクトップ上の以下のデバイス機能には[、JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)で使用できる専用の API Microsoft Teamsアクセスできます。
* メディア機能 (次の例)
    * カメラ
    * マイク
    * ギャラリー
    * QRまたはバーコードスキャナ
* 場所

デバイス機能にアクセスした後、それらをTeamsプラットフォームと統合して、コラボレーションエクスペリエンスを強化できます。 

## <a name="request-device-permissions"></a>デバイスのアクセス許可を要求する

[JavaScript クライアント SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)に用意されているツールを使用して、ネイティブ デバイスの機能にアクセスするために必要な[アクセス許可](native-device-permissions.md)を要求します。 これらの機能へのアクセスは、最新の Web ブラウザーでは標準的ですが、アプリ マニフェストを更新して、使用している機能についてTeamsに通知する必要があります。 この更新プログラムを使用すると、モバイルまたはデスクトップ クライアントでアプリを実行しているときに、アクセス許可Teams要求できます。
 
 ## <a name="integrate-device-capabilities"></a>デバイス機能の統合

デバイス機能にアクセスしたら、Teamsメディア機能 API を使用して[、メディア機能](mobile-camera-image-permissions.md)をTeamsプラットフォームと統合して、ユーザー エクスペリエンスを向上させます。 これらの統合機能により、アプリは次の機能を利用できます。

* 画像をキャプチャして共有します。
* [スキャナコントロール](qr-barcode-scanner-capability.md)を使用してQRまたはバーコードをスキャンします。
* マイクを通してオーディオを録音します。
* [場所の選択を](location-capability.md)使用して場所を共有します。
