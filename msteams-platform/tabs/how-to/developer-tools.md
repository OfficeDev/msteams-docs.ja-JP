---
title: Microsoft Teams タブの DevTools
description: このモジュールでは、Microsoft Teams デスクトップ クライアントとデバッグを使用するときに DevTools にアクセスする方法について説明します
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: a0d5e3ea15fd796c2c426f1cf1457171f0abe7b2
ms.sourcegitcommit: 024be23411bc0f2573d19f48f9266021f9b76f0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2022
ms.locfileid: "67488272"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft Teams タブの DevTools

Teams がブラウザーで実行されている場合は、ブラウザーの DevTools: F12 on Windows または MacOS の Command-Option-I に簡単にアクセスできます。 ダッシュボードでは、次の項目にもアクセスできます。

1. コンソール ログを表示します。
1. 実行時に HTML、CSS、およびネットワーク要求を表示または変更します。
1. JavaScript コードにブレークポイントを追加し、対話型デバッグを実行します。

> [!NOTE]
> この機能は、**[開発者プレビュー]** が有効にされた後、デスクトップ クライアントと Android クライアントでのみ使用できます。 詳細については、「[開発者プレビューを有効にする方法](~/resources/dev-preview/developer-preview-intro.md)」を参照してください。

## <a name="access-devtools-on-the-desktop"></a>デスクトップ上の DevTools にアクセスする

Web バージョンとデスクトップ バージョンの Teams はほぼ同じですが、認証にはいくつかの違いがあります。 何が起こっているかを把握する唯一の方法は、DevTools の使用　である場合があります。 デスクトップ クライアントで DevTools を使用するには、次の手順を実行する必要があります。

1. [開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)が有効になっていることを確認します。
1. DevTools で検査する内容が表示されるようにタブを開きます。
1. DevTools を開くには、次のいずれかの方法を使用します。
    * Windowsでは、デスクトップ トレイの Microsoft Teams アイコンを使用して DevTools を開きます。

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * MacOS で、Dock の Microsoft Teams アイコンを選択します。

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

次の例は、DevTools を開いてタブ構成ダイアログを検査する方法を示しています。

   [![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Android デバイスから DevTools にアクセスする

Teams Android クライアントから DevTools を有効にすることもできます。 DevTools を有効にするには、次の手順を実行する必要があります。

1. [開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)を有効にします。
1. デバイスをデスクトップ コンピューターに接続し、[リモート デバッグ](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)用に Android デバイスを設定します。
1. Chrome ブラウザーで、`chrome://inspect/#devices` を開きます。
1. 次の図のように、デバッグするタブで **検査** を選択します。

   ![Android DevTools](~/assets/images/android-devtools.png)

## <a name="see-also"></a>関連項目

[Teams クライアント キャッシュをクリアする](/microsoftteams/troubleshoot/teams-administration/clear-teams-cache)
