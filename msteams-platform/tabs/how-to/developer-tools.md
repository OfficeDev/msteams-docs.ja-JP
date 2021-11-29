---
title: Microsoft Teams タブの DevTools
description: デスクトップ クライアントを使用してデバッグするときに DevTools にアクセスMicrosoft Teams説明します。
ms.localizationpriority: medium
ms.topic: how-to
keywords: devtools debug mobile chrome デスクトップ クライアント開発者向けツール タブ
ms.openlocfilehash: b9bc3f5afa43684b260f8618b5450e94c91e95f1
ms.sourcegitcommit: 85d0584877db21e2d3e49d3ee940d22675617582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/29/2021
ms.locfileid: "61216207"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft Teams タブの DevTools

ブラウザー Teams実行している場合、ブラウザーの DevTools: F12 on Windows または Command-Option-I on MacOS に簡単にアクセスできます。 DevTools を使用すると、次の情報にアクセスできます。

1. コンソール ログを表示します。
1. 実行時に HTML、CSS、およびネットワーク要求を表示または変更します。
1. JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。

> [!NOTE]
> この機能は、デスクトップクライアントと Android クライアントで使用できるのは、Developer Preview **後のみです** 。 詳細については、「開発者プレビューを [有効にする方法」を参照してください](~/resources/dev-preview/developer-preview-intro.md)。

## <a name="access-devtools-on-the-desktop"></a>デスクトップ上の DevTools にアクセスする

Web バージョンとデスクトップ バージョンTeamsほとんど同じですが、認証に関していくつかの違いがあります。 時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。 デスクトップ クライアントで DevTools を使用するには、次の必要があります。

1. 開発者プレビューが有効 [になっているか確認します](~/resources/dev-preview/developer-preview-intro.md)。
1. タブを開き、DevTools で検査する必要があるものがあります。
1. DevTools を開く方法は次のとおりです。
    * 次Windows、デスクトップ トレイの [Microsoft Teams] アイコンを使用して DevTools を開きます。<br>
  ![右クリックして DevTools を開く](~/assets/images/dev-preview/devtools-right-click.png)
    * MacOS で、[ドック] の [Microsoft Teams] アイコンをクリックします。

次の例は、DevTools を開いてタブ構成ダイアログを検査する例を示しています。

   [![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Android デバイスから DevTools にアクセスする

また、Android クライアントから DevTools をTeamsできます。 DevTools を有効にするには、次の必要があります。

1. 開発者プレビュー [を有効にする](~/resources/dev-preview/developer-preview-intro.md)。
1. Connectデスクトップ コンピューターにデバイスをインストールし、リモート デバッグ用に Android デバイス[をセットアップします](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。
1. Chrome ブラウザーで開きます `chrome://inspect/#devices` 。
1. 次 **の図** のように、デバッグするタブの下にある [検査] を選択します。

   ![Android DevTools](~/assets/images/android-devtools.png)
