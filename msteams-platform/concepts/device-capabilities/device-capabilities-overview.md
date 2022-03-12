---
title: デバイス機能 - 概要
author: Rajeshwari-v
description: カメラ、画像、メディア、マイク、マイク、QR コードなどのネイティブ デバイス機能の概要。
ms.author: surbhigupta
keywords: カメラ イメージ メディア マイク マイク QR コード qrcode バーコード バーコード スキャン スキャナーの場所マップ機能ネイティブ デバイスのアクセス許可
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 4febce3868df9fbba90cb4a94e67f6d0856606c9
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452691"
---
# <a name="device-capabilities"></a>デバイス機能

Microsoft Teamsプラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。 拡張されたTeamsプラットフォームを使用すると、パートナーは、カメラ、QR またはバーコード スキャナー、フォト ギャラリー、マイク、場所などのデバイス機能を Web アプリと統合できます。 この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティの新しいシナリオや使用例が作成されます。

デバイスのアクセス許可はブラウザーによって異なります。 以前は、ブラウザーはアクセス許可を付与する方法を処理し、これらのアクセス許可は現在、Microsoft Teams。 詳細については、「[ブラウザー デバイスのアクセス許可](browser-device-permissions.md)」を参照してください。

## <a name="native-device-capabilities"></a>ネイティブ デバイスの機能

モバイルまたはデスクトップには、機能と呼ばれるカメラやマイクなどの組み込みのデバイスがあります。 JavaScript クライアント SDK で使用できる専用 API を使用して、モバイルまたはデスクトップで次Microsoft Teams[アクセスできます](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)。

* メディア機能 (次のような)
  * カメラ
  * マイク
  * ギャラリー
  * QR またはバーコード スキャナー
* 場所

デバイス機能へのアクセスを取得した後、それらを Teamsプラットフォームと統合して、共同作業のエクスペリエンスを強化できます。

## <a name="request-device-permissions"></a>デバイスのアクセス許可を要求する

[JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) にMicrosoft Teamsツールを使用して、ネイティブ デバイス機能にアクセスするために[](native-device-permissions.md)必要なアクセス許可を要求します。 これらの機能へのアクセスは、最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して、Teams に使用する機能について通知する必要があります。 この更新プログラムを使用すると、モバイル クライアントまたはデスクトップ クライアントでアプリをTeamsアクセス許可を要求できます。

## <a name="integrate-device-capabilities"></a>デバイスの機能を統合する

デバイス機能にアクセスした後、Teams メディア機能 API を使用して、メディア機能を Teams [](mobile-camera-image-permissions.md) プラットフォームに統合して、ユーザー エクスペリエンスを向上します。 これらの統合機能を使用すると、アプリは次の機能を使用できます。

* 画像をキャプチャして共有します。
* スキャナー コントロールを使用して QR またはバーコード [をスキャンします](qr-barcode-scanner-capability.md)。
* マイクを介してオーディオを録音します。
* 場所ピッカーを使用 [して場所を共有します](location-capability.md)。

また、ユーザーが Web アプリ エクスペリエンスTeamsユーザーを検索[](people-picker-capability.md)して選択できる、ネイティブユーザー選択コントロールを統合することもできます。
