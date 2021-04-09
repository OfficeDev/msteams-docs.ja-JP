---
title: Microsoft Teams タブの DevTools
description: Microsoft Teams デスクトップ クライアントを使用する場合に DevTools にアクセスする方法について説明します。
ms.topic: how-to
keywords: devtools デバッグ モバイル クロム デスクトップ クライアント開発者ツール
ms.openlocfilehash: 1c540c94adc080d9495097f8e3b427eeb14c56d8
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634742"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft Teams タブの DevTools

Teams がブラウザーで実行されている場合、ブラウザーの DevTools: F12 on Windows または Command-Option-I on MacOS に簡単にアクセスできます。 DevTools を使用すると、次の情報にアクセスできます。

1. コンソール ログを表示します。
1. 実行時に HTML、CSS、およびネットワーク要求を表示または変更します。
1. JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。

> [!NOTE]
> この機能は、デスクトップクライアントと Android クライアントでのみ使用できます **。Developer Preview** が有効になっています。 詳細については、「開発者プレビューを [有効にする方法」を参照してください](~/resources/dev-preview/developer-preview-intro.md)。

## <a name="access-devtools-in-the-desktop"></a>デスクトップで DevTools にアクセスする

Web バージョンとデスクトップ バージョンの Teams はほぼ同じですが、認証に関していくつかの違いがあります。 時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。 デスクトップ クライアントで DevTools を使用するには、次の必要があります。

1. 開発者プレビューが有効 [になっているか確認します](~/resources/dev-preview/developer-preview-intro.md)。
1. タブを開き、DevTools で検査する必要があるものがあります。
1. 次のいずれかの方法で DevTools を開きます。
    * **Windows**: デスクトップ トレイで Teams アイコンを選択します。
    * **MacOS**: ドックで Teams アイコンを選択します。
 
   次の図は、タブ構成ダイアログで要素を検査する DevTools を示しています。

   ![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a>Android クライアントから DevTools にアクセスする

Teams Android クライアントから DevTools を有効にできます。 DevTools を有効にするには、次の必要があります。

1. 開発者プレビュー [を有効にする](~/resources/dev-preview/developer-preview-intro.md)。
1. デバイスをデスクトップ コンピューターに接続し、リモート デバッグ用に Android デバイス [をセットアップします](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。
1. Chrome ブラウザーで開きます `chrome://inspect/#devices` 。
1. 次 **の図** のように、デバッグするタブの下にある [検査] を選択します。

   ![Android DevTools](~/assets/images/android-devtools.png)
