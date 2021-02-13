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
# <a name="device-capabilities"></a>デバイス機能 

Microsoft Teams プラットフォームは、組み込みのファースト パーティエクスペリエンスに合わせて、開発者の機能を継続的に強化しています。 強化された Teams プラットフォームにより、パートナーはカメラ、フォト ギャラリー、マイク、位置情報などのデバイス機能を Web アプリと統合できます。 この統合により、アプリ開発の障壁が軽減され、開発サイクルが短縮され、開発者コミュニティの新しいシナリオや使用事例が作成されます。

## <a name="native-device-capabilities"></a>ネイティブ デバイスの機能

モバイルデバイスまたはデスクトップ デバイスには、機能と呼ばれるカメラやマイクなどの組み込みデバイスがあります。 Microsoft Teams JavaScript クライアント SDK で利用可能な専用 API を使用して、モバイルまたはデスクトップで次のデバイス [機能にアクセスできます](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)。
* メディア機能 (次に例を示します)
    * カメラ
    * マイク
    * ギャラリー
* 場所

デバイスの機能にアクセスした後、Teams プラットフォームと統合して共同作業のエクスペリエンスを強化できます。 

## <a name="request-device-permissions"></a>デバイスのアクセス許可を要求する

[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK に用意されているツール[](native-device-permissions.md)を使用して、ネイティブ デバイス機能にアクセスするために必要なアクセス許可を要求します。 これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して、使用している機能について Teams に通知する必要があります。 この更新プログラムでは、アプリが Teams モバイルまたはデスクトップ クライアントで実行されている間にアクセス許可を要求できます。
 
 ## <a name="integrate-device-capabilities"></a>デバイス機能の統合

デバイス機能にアクセスした後 **、Teams** のメディア機能 API を [](mobile-camera-image-permissions.md)使用して Teams プラットフォームと機能を統合し、ユーザー エクスペリエンスを強化します。 これらの統合された機能を使って、アプリは次の機能を実行できます。

* 画像のキャプチャと共有
* マイクを使用してオーディオを録音する
* 場所情報を共有する


