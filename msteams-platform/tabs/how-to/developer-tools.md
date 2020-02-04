---
title: Microsoft Teams タブの DevTools
description: Microsoft Teams デスクトップクライアントを使用しているときに DevTools にアクセスする方法について説明します。
keywords: devtools デバッグモバイル chrome デスクトップクライアント開発者ツール
ms.openlocfilehash: 6c8ac15caf64c979b23155be847e8791988486e6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674873"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft Teams タブの DevTools

Teams がブラウザーで実行されている場合、ブラウザーの DevTools (Windows 上) またはコマンドオプション-I (MacOS 上) に簡単にアクセスできます。 DevTools を使用すると、次のものにアクセスできます。

1. コンソールログを表示します。
1. 実行時に html、css、およびネットワーク要求を表示/変更します。
1. JavaScript コードにブレークポイントを追加し、対話型デバッグを実行します。

この機能は、開発者プレビューが有効になっている場合にのみ、デスクトップおよび Android クライアントで使用できます。 詳細については、「[開発者プレビューを有効にする方法](~/resources/dev-preview/developer-preview-intro.md)」を参照してください。

## <a name="accessing-devtools-in-the-desktop"></a>デスクトップの DevTools へのアクセス

Teams の web 版とデスクトップ版の teams はほぼ同じですが、特に認証に関していくつかの違いがあります。 状況に応じて、DevTools を使用することもできます。 Teams デスクトップクライアントからこれらのユーザーにアクセスする方法は次のとおりです。 デスクトップクライアントで DevTools を使用するには、次のようにします。

1. [開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md)が有効になっていることを確認する
1. [] タブを開いて、DevTools で検査する内容を確認します。
1. DevTools を開く
    * Windows では、デスクトップトレイの Microsoft Teams アイコンを使用して、DevTools を開きます。

  ![右クリックして [DevTools] を開きます。](~/assets/images/dev-preview/devtools-right-click.png)

    * MacOS で、ドックの Microsoft Teams アイコンをクリックします。

DevTools を開いて、要素を選択すると、サンプルタブは次のようになります。

![Tab および DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Android クライアントからの DevTools へのアクセス

Teams Android クライアントから DevTools を有効にすることもできます。 これを行うには、以下のようにします:

1. [開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md)が有効になっていることを確認する
1. デバイスをデスクトップコンピューターに接続し、[リモートデバッグ](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)用の Android デバイスをセットアップする
1. Chrome ブラウザーで、を開き`chrome://inspect/#devices`ます。
1. 次のスクリーンショットに示すように、デバッグするタブの下の [**検査**] をクリックします。

![Android DevTools](~/assets/images/android-devtools.png)
