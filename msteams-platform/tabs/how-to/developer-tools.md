---
title: Microsoft Teams タブの DevTools
description: デスクトップ クライアントを使用してデバッグするときに DevTools にアクセスMicrosoft Teams説明します。
ms.localizationpriority: medium
ms.topic: how-to
keywords: devtools debug mobile chrome デスクトップ クライアント開発者向けツール タブ
ms.openlocfilehash: bec7b94b1db2492de9eaaa38ff62c0783c972f6e
ms.sourcegitcommit: d9daad3d5818d5774911b96fdc7bde45b04c9908
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2022
ms.locfileid: "64511223"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft Teams タブの DevTools

ブラウザー Teams実行している場合、ブラウザーの DevTools: F12 on Windows または Command-Option-I on MacOS に簡単にアクセスできます。 DevTools を使用すると、次の情報にアクセスできます。

1. コンソール ログを表示します。
1. 実行時に HTML、CSS、およびネットワーク要求を表示または変更します。
1. JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。

> [!NOTE]
> この機能は、デスクトップクライアントと Android クライアントが有効 **になっているDeveloper Previewでのみ** 使用できます。 詳細については、「開発者プレビューを有効[にする操作方法を参照してください](~/resources/dev-preview/developer-preview-intro.md)。

## <a name="access-devtools-on-the-desktop"></a>デスクトップ上の DevTools にアクセスする

Web バージョンとデスクトップ バージョンの Teamsはほぼ同じですが、認証に関していくつかの違いがあります。 時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。 デスクトップ クライアントで DevTools を使用するには、次の必要があります。

1. 開発者プレビューが [有効になっているか確認します](~/resources/dev-preview/developer-preview-intro.md)。
1. タブを開き、DevTools で検査する必要があるものがあります。
1. DevTools を開く方法は次のとおりです。
    * このWindows、デスクトップ トレイの [Microsoft Teams] アイコンを使用して DevTools を開きます。

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * MacOS で、ドックMicrosoft Teamsアイコンを選択します。

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

次の例は、DevTools を開いてタブ構成ダイアログを検査する例を示しています。

   [![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Android デバイスから DevTools にアクセスする

また、Android クライアントから DevTools をTeamsできます。 DevTools を有効にするには、次の必要があります。

1. 開発者プレビュー [を有効にする](~/resources/dev-preview/developer-preview-intro.md)。
1. Connectデスクトップ コンピューターにデバイスをインストールし、リモート デバッグ用に Android デバイス[をセットアップします](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。
1. Chrome ブラウザーで開きます `chrome://inspect/#devices`。
1. 次 **の図** のように、デバッグするタブの下にある [検査] を選択します。

   ![Android DevTools](~/assets/images/android-devtools.png)
