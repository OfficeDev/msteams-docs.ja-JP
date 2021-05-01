---
title: Microsoft Teams タブの DevTools
description: デスクトップ クライアントを使用するときに DevTools にアクセスするMicrosoft Teams説明します。
localization_priority: Normal
ms.topic: how-to
keywords: devtools デバッグ モバイル クロム デスクトップ クライアント開発者ツール
ms.openlocfilehash: 70c9a2bab94ceb97e8dcd5cf5cdb98261d037f74
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101829"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="3dcd7-104">Microsoft Teams タブの DevTools</span><span class="sxs-lookup"><span data-stu-id="3dcd7-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="3dcd7-105">ブラウザー Teams実行している場合、ブラウザーの DevTools: F12 on Windows または Command-Option-I on MacOS に簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="3dcd7-106">DevTools を使用すると、次の情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="3dcd7-107">コンソール ログを表示します。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-107">View console logs.</span></span>
1. <span data-ttu-id="3dcd7-108">実行時に HTML、CSS、およびネットワーク要求を表示または変更します。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="3dcd7-109">JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="3dcd7-110">この機能は、デスクトップクライアントと Android クライアントで使用できるのは、Developer Preview **後のみです** 。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="3dcd7-111">詳細については、「開発者プレビューを [有効にする方法」を参照してください](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-on-the-desktop"></a><span data-ttu-id="3dcd7-112">デスクトップ上の DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="3dcd7-112">Access DevTools on the desktop</span></span>

<span data-ttu-id="3dcd7-113">Web バージョンとデスクトップ バージョンTeamsほとんど同じですが、認証に関していくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="3dcd7-114">時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="3dcd7-115">デスクトップ クライアントで DevTools を使用するには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="3dcd7-116">開発者プレビューが有効 [になっているか確認します](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="3dcd7-117">タブを開き、DevTools で検査する必要があるものがあります。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="3dcd7-118">DevTools を開く方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-118">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="3dcd7-119">次Windows、デスクトップ トレイの [Microsoft Teams] アイコンを使用して DevTools を開きます。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-119">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span><br>
  <span data-ttu-id="3dcd7-120">![右クリックして DevTools を開く](~/assets/images/dev-preview/devtools-right-click.png)</span><span class="sxs-lookup"><span data-stu-id="3dcd7-120">![Right-click to open DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span></span>
    * <span data-ttu-id="3dcd7-121">MacOS で、[ドック] の [Microsoft Teams] アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-121">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="3dcd7-122">次の例は、DevTools を開いてタブ構成ダイアログを検査する例を示しています。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-122">The following example shows DevTools open and inspecting a tab configuration dialog:</span></span>

   ![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a><span data-ttu-id="3dcd7-124">Android デバイスから DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="3dcd7-124">Access DevTools from an Android device</span></span>

<span data-ttu-id="3dcd7-125">また、Android クライアントから DevTools をTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-125">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="3dcd7-126">DevTools を有効にするには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-126">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="3dcd7-127">開発者プレビュー [を有効にする](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-127">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="3dcd7-128">Connectデスクトップ コンピューターにデバイスをインストールし、リモート デバッグ用に Android デバイス[をセットアップします](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-128">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="3dcd7-129">Chrome ブラウザーで開きます `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-129">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="3dcd7-130">次 **の図** のように、デバッグするタブの下にある [検査] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3dcd7-130">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
