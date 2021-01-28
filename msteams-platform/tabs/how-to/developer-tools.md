---
title: Microsoft Teams タブの DevTools
description: Microsoft Teams デスクトップ クライアントを使用するときに DevTools にアクセスする方法について説明します。
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 8f23a5d56faa00d40451d2bbeadde32f6a5d0f7f
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014580"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft Teams タブの DevTools

Teams がブラウザーで実行されている場合、ブラウザーの DevTools: F12 (Windows の場合) または Command-Option-I (MacOS の場合) に簡単にアクセスできます。 DevTools を使用すると、次の機能にアクセスできます。

1. コンソール ログを表示します。
1. 実行時に html、css、およびネットワーク要求を表示/変更します。
1. JavaScript コードにブレークポイントを追加し、対話型デバッグを実行します。

この機能は、デスクトップクライアントと Android クライアントでのみ使用できます。Developer Preview有効にした後です。 詳細 [については、「この機能を有効Developer Preview](~/resources/dev-preview/developer-preview-intro.md) 方法」を参照してください。

## <a name="accessing-devtools-in-the-desktop"></a>デスクトップでの DevTools へのアクセス

Teams の Web バージョンとデスクトップ バージョンのチームはほとんど同じですが、特に認証に関していくつかの違いがあります。 場合によっては、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。 Teams デスクトップ クライアントからアクセスする方法を次に示します。 デスクトップ クライアントで DevTools を使用するには:

1. 開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)
1. DevTools で検査する必要があるタブを開きます。
1. DevTools を開く
    * Windows では、デスクトップ トレイの Microsoft Teams アイコンを使って DevTools を開きます。

  ![右クリックして DevTools を開く](~/assets/images/dev-preview/devtools-right-click.png)

    * MacOS で、ドックの Microsoft Teams アイコンをクリックします。

DevTools が開き、要素が選択されている場合のサンプル タブは次のように表示されます。

![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Android クライアントから DevTools にアクセスする

Teams Android クライアントから DevTools を有効にできます。 これを行うには、以下のようにします。

1. 開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)
1. デバイスをデスクトップ コンピューターに接続し、リモート デバッグ用に Android デバイス [をセットアップする](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. Chrome ブラウザーで開きます `chrome://inspect/#devices` 。
1. 次 **のスクリーンショット** のように、デバッグするタブの下にある [inspect] をクリックします。

![Android DevTools](~/assets/images/android-devtools.png)
