---
title: デバイス機能 - 概要
author: Rajeshwari-v
description: ネイティブ デバイス機能の概要。
ms.author: surbhigupta
keywords: カメラ イメージ メディア マイク マイク QR コード qrcode バーコード バーコード スキャン スキャナーの場所マップ機能ネイティブ デバイスのアクセス許可
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 069bd27057784076b3b701d013ead209ec6fa3a9
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211584"
---
# <a name="device-capabilities"></a>デバイス機能

Microsoft Teamsプラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。 拡張されたTeamsプラットフォームを使用すると、パートナーはカメラ、QR、バーコード スキャナー、フォト ギャラリー、マイク、場所などのデバイス機能を Web アプリと統合できます。 この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティの新しいシナリオや使用例が作成されます。

## <a name="native-device-capabilities"></a>ネイティブ デバイスの機能

モバイルデバイスまたはデスクトップ デバイスには、機能と呼ばれるカメラやマイクなどの組み込みデバイスがあります。 JavaScript クライアント SDK で使用できる専用 API を使用して、モバイルまたはデスクトップで次Microsoft Teams[アクセスできます](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)。
* メディア機能 (次のような)
    * カメラ
    * マイク
    * ギャラリー
    * QR またはバーコード スキャナー
* 場所

デバイス機能へのアクセスを取得した後、これらの機能を Teamsプラットフォームと統合して、共同作業のエクスペリエンスを向上できます。 

## <a name="request-device-permissions"></a>デバイスのアクセス許可を要求する

[JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK にMicrosoft Teamsツールを使用して、ネイティブ デバイス[](native-device-permissions.md)機能にアクセスするために必要なアクセス許可を要求します。 これらの機能へのアクセスは、最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新してTeams機能についてユーザーに通知する必要があります。 この更新プログラムを使用すると、モバイル クライアントまたはデスクトップ クライアントでアプリをTeamsアクセス許可を要求できます。
 
 ## <a name="integrate-device-capabilities"></a>デバイス機能の統合

デバイス機能にアクセスした後、Teams メディア機能 API を使用して、メディア[](mobile-camera-image-permissions.md)機能を Teams プラットフォームに統合して、ユーザー エクスペリエンスを向上します。 これらの統合機能を使用すると、アプリは次の機能を使用できます。

* 画像をキャプチャして共有します。
* スキャナー コントロールを使用して QR またはバーコード [をスキャンします](qr-barcode-scanner-capability.md)。
* マイクを介してオーディオを録音します。
* 場所ピッカーを使用 [して場所を共有します](location-capability.md)。

また、ユーザーが Web アプリ エクスペリエンス[](people-picker-capability.md)Teamsユーザーを検索および選択できるユーザー選択コントロールを統合することもできます。
