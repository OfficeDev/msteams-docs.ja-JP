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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="223a0-104">Microsoft Teams タブの DevTools</span><span class="sxs-lookup"><span data-stu-id="223a0-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="223a0-105">Teams がブラウザーで実行されている場合、ブラウザーの DevTools: F12 (Windows 上) または Command-Option-I (MacOS 上) に簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="223a0-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="223a0-106">DevTools を使用すると、次の情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="223a0-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="223a0-107">コンソール ログを表示します。</span><span class="sxs-lookup"><span data-stu-id="223a0-107">View console logs.</span></span>
1. <span data-ttu-id="223a0-108">実行時に html、css、およびネットワーク要求を表示/変更します。</span><span class="sxs-lookup"><span data-stu-id="223a0-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="223a0-109">JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="223a0-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="223a0-110">この機能は、デスクトップクライアントと Android クライアントでのみ使用できます。Developer Previewが有効になっています。</span><span class="sxs-lookup"><span data-stu-id="223a0-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="223a0-111">詳細 [については、「How do I enable Developer Preview」](~/resources/dev-preview/developer-preview-intro.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="223a0-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="223a0-112">デスクトップでの DevTools へのアクセス</span><span class="sxs-lookup"><span data-stu-id="223a0-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="223a0-113">Teams の Web バージョンとデスクトップ バージョンのチームはほぼ同じですが、特に認証に関していくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="223a0-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="223a0-114">時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="223a0-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="223a0-115">Teams デスクトップ クライアントからアクセスする方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="223a0-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="223a0-116">デスクトップ クライアントで DevTools を使用するには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="223a0-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="223a0-117">開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="223a0-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="223a0-118">タブを開き、DevTools で検査する必要があるものがあります。</span><span class="sxs-lookup"><span data-stu-id="223a0-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="223a0-119">DevTools を開く方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="223a0-119">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="223a0-120">**Windows**: デスクトップ トレイで Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="223a0-120">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="223a0-121">**macOS**: ドックで Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="223a0-121">**macOS**: Select the Teams icon in the Dock.</span></span>

<span data-ttu-id="223a0-122">次のスクリーンショットは、タブ構成ダイアログで要素を検査する DevTools を示しています。</span><span class="sxs-lookup"><span data-stu-id="223a0-122">The following screenshot shows DevTools inspecting an element in a tab configuration dialog:</span></span>

![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="223a0-124">Android クライアントから DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="223a0-124">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="223a0-125">Teams Android クライアントから DevTools を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="223a0-125">You can also enable the DevTools from the Teams Android client.</span></span>

1. <span data-ttu-id="223a0-126">開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="223a0-126">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="223a0-127">デバイスをデスクトップ コンピューターに接続し、リモート デバッグ用に Android デバイス [をセットアップする](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="223a0-127">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="223a0-128">Chrome ブラウザーで開きます `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="223a0-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="223a0-129">下 **のスクリーンショット** のように、デバッグするタブの下にある [検査] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="223a0-129">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
