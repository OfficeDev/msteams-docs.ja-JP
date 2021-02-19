---
title: デバイス機能の概要
description: ネイティブ デバイス機能の概要。
keywords: カメラ イメージ メディア マイク マイク QR コード qrcode バーコード バーコード スキャン スキャナー機能ネイティブ デバイスのアクセス許可
ms.topic: overview
ms.openlocfilehash: 03ce0267f7160772e30ec88de2c29f81886b5280
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294727"
---
# <a name="device-capabilities"></a>デバイス機能 

Microsoft Teams プラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。 強化された Teams プラットフォームを使用すると、パートナーは、カメラ、QR、バーコード スキャナー、フォト ギャラリー、マイク、場所などのデバイス機能を Web アプリと統合できます。 この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティの新しいシナリオや使用例が作成されます。

## <a name="native-device-capabilities"></a>ネイティブ デバイスの機能

モバイルデバイスまたはデスクトップ デバイスには、機能と呼ばれるカメラやマイクなどの組み込みデバイスがあります。 Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、モバイルまたはデスクトップで次の [デバイス機能にアクセスできます](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)。
* メディア機能 (次のような)
    * カメラ
    * マイク
    * ギャラリー
    * QR またはバーコード スキャナー
* Location

デバイス機能にアクセスした後、それらを Teams プラットフォームと統合して、共同作業のエクスペリエンスを強化できます。 

## <a name="request-device-permissions"></a>デバイスのアクセス許可を要求する

[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK にあるツールを使用[](native-device-permissions.md)して、ネイティブ デバイス機能にアクセスするために必要なアクセス許可を要求します。 これらの機能へのアクセスは、最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用している機能について Teams に通知する必要があります。 この更新プログラムを使用すると、アプリが Teams モバイル またはデスクトップ クライアントで実行されている間にアクセス許可を要求できます。
 
 ## <a name="integrate-device-capabilities"></a>デバイス機能の統合

デバイス機能にアクセスした後、Teams メディア機能 API を使用[](mobile-camera-image-permissions.md)して、メディア機能を Teams プラットフォームと統合してユーザー エクスペリエンスを向上します。 これらの統合機能を使用すると、アプリは次の機能を使用できます。

* 画像のキャプチャと共有
* スキャナーコントロールを使用して QR またはバーコード [をスキャンする](qr-barcode-scanner-capability.md)
* マイクでオーディオを録音する
* 位置情報を共有する
