---
title: デバイス機能 - 概要
author: Rajeshwari-v
description: カメラ、画像、メディア、マイク、マイク、QR コードなどのネイティブ デバイス機能の概要。
ms.author: surbhigupta
keywords: カメラ イメージ メディア マイク マイク QR コード qrcode バーコード バーコード スキャン スキャナーの場所マップ機能ネイティブ デバイスのアクセス許可
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 51f09880d638e1da48233aa2b6ff396f9908fa23
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889140"
---
# <a name="device-capabilities"></a>デバイス機能

Microsoft Teamsプラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。 拡張されたTeamsプラットフォームを使用すると、パートナーはカメラ、QR、バーコード スキャナー、フォト ギャラリー、マイク、場所などのデバイス機能を Web アプリと統合できます。 この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティの新しいシナリオや使用例が作成されます。

ブラウザーでは、デバイスのアクセス許可が異なります。 詳細については、「ブラウザー デバイス [のアクセス許可」を参照してください](browser-device-permissions.md)。

## <a name="native-device-capabilities"></a>ネイティブ デバイスの機能

モバイルまたはデスクトップには、機能と呼ばれるカメラやマイクなどの組み込みのデバイスがあります。 JavaScript クライアント SDK で使用できる専用 API を使用して、モバイルまたはデスクトップで次Microsoft Teams[アクセスできます](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)。
* メディア機能 (次のような)
    * カメラ
    * マイク
    * ギャラリー
    * QR またはバーコード スキャナー
* 場所

デバイス機能へのアクセスを取得した後、それらを Teamsプラットフォームと統合して、共同作業のエクスペリエンスを向上できます。 

## <a name="request-device-permissions"></a>デバイスのアクセス許可を要求する

[JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK にMicrosoft Teamsツールを使用して、ネイティブ デバイス[](native-device-permissions.md)機能にアクセスするために必要なアクセス許可を要求します。 これらの機能へのアクセスは、最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新してTeams機能についてユーザーに通知する必要があります。 この更新プログラムを使用すると、モバイル クライアントまたはデスクトップ クライアントでアプリをTeamsアクセス許可を要求できます。
 
 ## <a name="integrate-device-capabilities"></a>デバイス機能の統合

デバイス機能にアクセスした後、Teams メディア機能 API を使用して、[](mobile-camera-image-permissions.md)メディア機能を Teams プラットフォームに統合して、ユーザー エクスペリエンスを向上します。 これらの統合機能を使用すると、アプリは次の機能を使用できます。

* 画像をキャプチャして共有します。
* スキャナー コントロールを使用して QR またはバーコード [をスキャンします](qr-barcode-scanner-capability.md)。
* マイクを介してオーディオを録音します。
* 場所ピッカーを使用 [して場所を共有します](location-capability.md)。

また、ユーザーが Web アプリ エクスペリエンス[](people-picker-capability.md)Teamsユーザーを検索および選択できるユーザー選択コントロールを統合することもできます。
