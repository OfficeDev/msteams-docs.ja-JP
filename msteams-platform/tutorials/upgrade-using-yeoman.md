---
title: チュートリアル - Microsoft Teams Yeoman ジェネレーターを使用した Teams のアップグレード
description: Microsoft Teams Yeoman ジェネレーターを使用して Teams をアップグレードする方法について説明します。
ms.topic: tutorial
ms.openlocfilehash: 0c52dd15703000a1c0f99ddd28401dd686e1b1bb
ms.sourcegitcommit: afe4bc0336663e496d03c52e4b206217c02fae63
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "50528636"
---
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a>Microsoft Teams Yeoman ジェネレーターを使用して Teams をアップグレードする
このチュートリアルでは、Microsoft Teams Yeoman ジェネレーターを使用して、現在の Microsoft Teams アプリのバージョンを最新バージョンにアップグレードできます。

## <a name="get-current-version-of-teams"></a>Teams の現在のバージョンを取得する
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a>Teams の更新
yo コマンドは、プロジェクトの作成からジェネレーターの更新に至るまで、さまざまなオプションを一覧表示します。 更新プログラムジェネレーターを選択するには、次のコマンドを使用します。
```PowerShell
 yo
```

矢印キーを使用して [ジェネレーターの更新 **] を選択します**。
![YoSelectUpdatGen の画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

一覧には、使用可能なすべてのジェネレーターが表示されます。 使用可能なオプションから Teams のバージョンを選択または選択解除するには、スペース バーを使用 **して特定の** ジェネレーターを選択します。
![UseSpaceToSelectGenerators のイメージ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)

Teams のインストールが完了するには数秒から数分かかります。

インストールが完了したら、次のコマンドを使用してインストールされているバージョンを確認します。

```PowerShell
yo teams --version
```

![FindVersionAfterInstallation のイメージ](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

おめでとう! Microsoft Teams をアップグレードしました。

