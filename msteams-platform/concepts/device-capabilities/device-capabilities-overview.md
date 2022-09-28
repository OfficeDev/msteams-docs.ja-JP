---
title: デバイス機能 - 概要
author: Rajeshwari-v
description: 場所やメディア (カメラ、マイク、ギャラリー、QR、バーコード スキャナー) などのネイティブ デバイス機能を Microsoft Teams アプリと統合する方法について説明します。
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 04ae1a0b21c12ef7dda5d4bf8dfa799ac5726d15
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100568"
---
# <a name="device-capabilities"></a>デバイス機能

Microsoft Teams プラットフォームは、組み込みのファーストパーティ エクスペリエンスに合わせて開発者機能を継続的に強化しています。 強化された Teams プラットフォームを使用すると、パートナーは、カメラ、QR またはバーコード スキャナー、フォト ギャラリー、マイク、場所などのデバイス機能を Web アプリと統合できます。 この統合により、アプリ開発の障壁が減り、開発サイクルが短縮され、開発者コミュニティの新しいシナリオやユース ケースが作成されます。

デバイスのアクセス許可はブラウザーによって異なります。 以前は、ブラウザーでアクセス許可を付与する方法が処理され、Teams でこれらのアクセス許可が処理されるようになりました。 詳細については、「[ブラウザー デバイスのアクセス許可](browser-device-permissions.md)」を参照してください。

## <a name="native-device-capabilities"></a>ネイティブ デバイス機能

モバイルまたはデスクトップには、機能と呼ばれるカメラやマイクなどのデバイスが組み込まれています。 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) で使用できる専用 API を使用して、モバイルまたはデスクトップで次のデバイス機能にアクセスできます。

* メディア機能 (次のように)
  * カメラ
  * マイク
  * ギャラリー
  * QR またはバーコード スキャナー
* 場所

デバイス機能にアクセスした後は、Teams プラットフォームと統合してコラボレーション エクスペリエンスを強化できます。

## <a name="request-device-permissions"></a>デバイスのアクセス許可を要求する

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) に用意されているツールを使用して、ネイティブ デバイス機能にアクセスするために必要な[アクセス許可](native-device-permissions.md)を要求します。 これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用している機能について Teams に通知する必要があります。 この更新プログラムを使用すると、Teams モバイルクライアントまたはデスクトップ クライアントでアプリを実行している間にアクセス許可を要求できます。

## <a name="integrate-device-capabilities"></a>デバイスの機能を統合する

デバイス機能にアクセスしたら、Teams メディア機能 API を使用して [、メディア機能](media-capabilities.md) を Teams プラットフォームと統合して、ユーザー エクスペリエンスを向上させます。 これらの統合機能を使用すると、アプリは次のことができるようになります。

* 画像をキャプチャして共有します。
* [スキャナー コントロール](qr-barcode-scanner-capability.md)を使用して QR またはバーコードをスキャンします。
* マイクを使用してオーディオを録音します。
* [場所ピッカー](location-capability.md)を使用して場所を共有します。

また、ユーザーが Web アプリ エクスペリエンスでユーザーを検索して選択できるようにする Teams ネイティブユーザー [ピッカー コントロール](people-picker-capability.md) を統合することもできます。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | Node.js    |
|:---------------------|:--------------|:---------|
|デバイス アクセス許可 | デバイスのアクセス許可に関する Teams タブ サンプル アプリを示す方法について説明します。 |[表示](<https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs>)|
