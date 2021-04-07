---
title: Microsoft Teams タブの DevTools
description: Microsoft Teams デスクトップ クライアントを使用する場合に DevTools にアクセスする方法について説明します。
ms.topic: how-to
keywords: devtools デバッグ モバイル クロム デスクトップ クライアント開発者ツール
ms.openlocfilehash: 1bf7d246136a24316309ae144ac9552c5fd4f57d
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596274"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft Teams タブの DevTools

Teams がブラウザーで実行されている場合、ブラウザーの DevTools: F12 (Windows 上) または Command-Option-I (MacOS 上) に簡単にアクセスできます。 DevTools を使用すると、次の情報にアクセスできます。

1. コンソール ログを表示します。
1. 実行時に html、css、およびネットワーク要求を表示/変更します。
1. JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。

この機能は、デスクトップクライアントと Android クライアントでのみ使用できます。Developer Previewが有効になっています。 詳細 [については、「How do I enable Developer Preview」](~/resources/dev-preview/developer-preview-intro.md) を参照してください。

## <a name="accessing-devtools-in-the-desktop"></a>デスクトップでの DevTools へのアクセス

Teams の Web バージョンとデスクトップ バージョンのチームはほぼ同じですが、特に認証に関していくつかの違いがあります。 時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。 Teams デスクトップ クライアントからアクセスする方法を次に示します。 デスクトップ クライアントで DevTools を使用するには、次のコマンドを実行します。

1. 開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)
1. タブを開き、DevTools で検査する必要があるものがあります。
1. DevTools を開く方法は次のとおりです。
    * **Windows**: デスクトップ トレイで Teams アイコンを選択します。
    * **macOS**: ドックで Teams アイコンを選択します。

次のスクリーンショットは、タブ構成ダイアログで要素を検査する DevTools を示しています。

![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Android クライアントから DevTools にアクセスする

Teams Android クライアントから DevTools を有効にできます。

1. 開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)
1. デバイスをデスクトップ コンピューターに接続し、リモート デバッグ用に Android デバイス [をセットアップする](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. Chrome ブラウザーで開きます `chrome://inspect/#devices` 。
1. 下 **のスクリーンショット** のように、デバッグするタブの下にある [検査] をクリックします。

![Android DevTools](~/assets/images/android-devtools.png)
