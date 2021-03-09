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
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a><span data-ttu-id="1bcc4-103">Microsoft Teams Yeoman ジェネレーターを使用して Teams をアップグレードする</span><span class="sxs-lookup"><span data-stu-id="1bcc4-103">Upgrade Teams using Microsoft Teams Yeoman generator</span></span>
<span data-ttu-id="1bcc4-104">このチュートリアルでは、Microsoft Teams Yeoman ジェネレーターを使用して、現在の Microsoft Teams アプリのバージョンを最新バージョンにアップグレードできます。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-104">This tutorial helps you to upgrade your current Microsoft Teams app version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

## <a name="get-current-version-of-teams"></a><span data-ttu-id="1bcc4-105">Teams の現在のバージョンを取得する</span><span class="sxs-lookup"><span data-stu-id="1bcc4-105">Get current version of Teams</span></span>
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a><span data-ttu-id="1bcc4-106">Teams の更新</span><span class="sxs-lookup"><span data-stu-id="1bcc4-106">Update Teams</span></span>
<span data-ttu-id="1bcc4-107">yo コマンドは、プロジェクトの作成からジェネレーターの更新に至るまで、さまざまなオプションを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-107">The yo command lists out various options ranging from creating project to updating generator.</span></span> <span data-ttu-id="1bcc4-108">更新プログラムジェネレーターを選択するには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-108">Use the following command to select update generator:</span></span>
```PowerShell
 yo
```

<span data-ttu-id="1bcc4-109">矢印キーを使用して [ジェネレーターの更新 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-109">Use the arrow keys to choose **Update Generators**.</span></span>
<span data-ttu-id="1bcc4-110">![YoSelectUpdatGen の画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span><span class="sxs-lookup"><span data-stu-id="1bcc4-110">![image of YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span></span>

<span data-ttu-id="1bcc4-111">一覧には、使用可能なすべてのジェネレーターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-111">The list displays all the available generators.</span></span> <span data-ttu-id="1bcc4-112">使用可能なオプションから Teams のバージョンを選択または選択解除するには、スペース バーを使用 **して特定の** ジェネレーターを選択します。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-112">To select or unselect Teams version from the available options, use the **space bar** and choose a specific generator.</span></span>
<span data-ttu-id="1bcc4-113">![UseSpaceToSelectGenerators のイメージ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span><span class="sxs-lookup"><span data-stu-id="1bcc4-113">![image of UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span></span>

<span data-ttu-id="1bcc4-114">Teams のインストールが完了するには数秒から数分かかります。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-114">It takes few seconds to minutes for Teams installation to complete.</span></span>

<span data-ttu-id="1bcc4-115">インストールが完了したら、次のコマンドを使用してインストールされているバージョンを確認します。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-115">After the installation is complete, use the following command to check the installed version:</span></span>

```PowerShell
yo teams --version
```

![FindVersionAfterInstallation のイメージ](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

<span data-ttu-id="1bcc4-117">おめでとう!</span><span class="sxs-lookup"><span data-stu-id="1bcc4-117">Congrats!</span></span> <span data-ttu-id="1bcc4-118">Microsoft Teams をアップグレードしました。</span><span class="sxs-lookup"><span data-stu-id="1bcc4-118">You have upgraded Microsoft Teams.</span></span>

