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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="36fd3-104">Microsoft Teams タブの DevTools</span><span class="sxs-lookup"><span data-stu-id="36fd3-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="36fd3-105">Teams がブラウザーで実行されている場合、ブラウザーの DevTools: F12 (Windows の場合) または Command-Option-I (MacOS の場合) に簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="36fd3-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="36fd3-106">DevTools を使用すると、次の機能にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="36fd3-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="36fd3-107">コンソール ログを表示します。</span><span class="sxs-lookup"><span data-stu-id="36fd3-107">View console logs.</span></span>
1. <span data-ttu-id="36fd3-108">実行時に html、css、およびネットワーク要求を表示/変更します。</span><span class="sxs-lookup"><span data-stu-id="36fd3-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="36fd3-109">JavaScript コードにブレークポイントを追加し、対話型デバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="36fd3-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="36fd3-110">この機能は、デスクトップクライアントと Android クライアントでのみ使用できます。Developer Preview有効にした後です。</span><span class="sxs-lookup"><span data-stu-id="36fd3-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="36fd3-111">詳細 [については、「この機能を有効Developer Preview](~/resources/dev-preview/developer-preview-intro.md) 方法」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="36fd3-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="36fd3-112">デスクトップでの DevTools へのアクセス</span><span class="sxs-lookup"><span data-stu-id="36fd3-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="36fd3-113">Teams の Web バージョンとデスクトップ バージョンのチームはほとんど同じですが、特に認証に関していくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="36fd3-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="36fd3-114">場合によっては、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="36fd3-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="36fd3-115">Teams デスクトップ クライアントからアクセスする方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="36fd3-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="36fd3-116">デスクトップ クライアントで DevTools を使用するには:</span><span class="sxs-lookup"><span data-stu-id="36fd3-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="36fd3-117">開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="36fd3-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="36fd3-118">DevTools で検査する必要があるタブを開きます。</span><span class="sxs-lookup"><span data-stu-id="36fd3-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="36fd3-119">DevTools を開く</span><span class="sxs-lookup"><span data-stu-id="36fd3-119">Open the DevTools</span></span>
    * <span data-ttu-id="36fd3-120">Windows では、デスクトップ トレイの Microsoft Teams アイコンを使って DevTools を開きます。</span><span class="sxs-lookup"><span data-stu-id="36fd3-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![右クリックして DevTools を開く](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="36fd3-122">MacOS で、ドックの Microsoft Teams アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="36fd3-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="36fd3-123">DevTools が開き、要素が選択されている場合のサンプル タブは次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="36fd3-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="36fd3-125">Android クライアントから DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="36fd3-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="36fd3-126">Teams Android クライアントから DevTools を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="36fd3-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="36fd3-127">これを行うには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="36fd3-127">To do so:</span></span>

1. <span data-ttu-id="36fd3-128">開発者プレビューが有効 [になっているか確認する](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="36fd3-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="36fd3-129">デバイスをデスクトップ コンピューターに接続し、リモート デバッグ用に Android デバイス [をセットアップする](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="36fd3-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="36fd3-130">Chrome ブラウザーで開きます `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="36fd3-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="36fd3-131">次 **のスクリーンショット** のように、デバッグするタブの下にある [inspect] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="36fd3-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
