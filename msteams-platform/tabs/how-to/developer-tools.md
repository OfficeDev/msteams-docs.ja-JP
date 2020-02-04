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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="057d9-104">Microsoft Teams タブの DevTools</span><span class="sxs-lookup"><span data-stu-id="057d9-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="057d9-105">Teams がブラウザーで実行されている場合、ブラウザーの DevTools (Windows 上) またはコマンドオプション-I (MacOS 上) に簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="057d9-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="057d9-106">DevTools を使用すると、次のものにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="057d9-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="057d9-107">コンソールログを表示します。</span><span class="sxs-lookup"><span data-stu-id="057d9-107">View console logs.</span></span>
1. <span data-ttu-id="057d9-108">実行時に html、css、およびネットワーク要求を表示/変更します。</span><span class="sxs-lookup"><span data-stu-id="057d9-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="057d9-109">JavaScript コードにブレークポイントを追加し、対話型デバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="057d9-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="057d9-110">この機能は、開発者プレビューが有効になっている場合にのみ、デスクトップおよび Android クライアントで使用できます。</span><span class="sxs-lookup"><span data-stu-id="057d9-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="057d9-111">詳細については、「[開発者プレビューを有効にする方法](~/resources/dev-preview/developer-preview-intro.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="057d9-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="057d9-112">デスクトップの DevTools へのアクセス</span><span class="sxs-lookup"><span data-stu-id="057d9-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="057d9-113">Teams の web 版とデスクトップ版の teams はほぼ同じですが、特に認証に関していくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="057d9-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="057d9-114">状況に応じて、DevTools を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="057d9-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="057d9-115">Teams デスクトップクライアントからこれらのユーザーにアクセスする方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="057d9-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="057d9-116">デスクトップクライアントで DevTools を使用するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="057d9-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="057d9-117">[開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md)が有効になっていることを確認する</span><span class="sxs-lookup"><span data-stu-id="057d9-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="057d9-118">[] タブを開いて、DevTools で検査する内容を確認します。</span><span class="sxs-lookup"><span data-stu-id="057d9-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="057d9-119">DevTools を開く</span><span class="sxs-lookup"><span data-stu-id="057d9-119">Open the DevTools</span></span>
    * <span data-ttu-id="057d9-120">Windows では、デスクトップトレイの Microsoft Teams アイコンを使用して、DevTools を開きます。</span><span class="sxs-lookup"><span data-stu-id="057d9-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![右クリックして [DevTools] を開きます。](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="057d9-122">MacOS で、ドックの Microsoft Teams アイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="057d9-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="057d9-123">DevTools を開いて、要素を選択すると、サンプルタブは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="057d9-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab および DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="057d9-125">Android クライアントからの DevTools へのアクセス</span><span class="sxs-lookup"><span data-stu-id="057d9-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="057d9-126">Teams Android クライアントから DevTools を有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="057d9-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="057d9-127">これを行うには、以下のようにします:</span><span class="sxs-lookup"><span data-stu-id="057d9-127">To do so:</span></span>

1. <span data-ttu-id="057d9-128">[開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md)が有効になっていることを確認する</span><span class="sxs-lookup"><span data-stu-id="057d9-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="057d9-129">デバイスをデスクトップコンピューターに接続し、[リモートデバッグ](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)用の Android デバイスをセットアップする</span><span class="sxs-lookup"><span data-stu-id="057d9-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="057d9-130">Chrome ブラウザーで、を開き`chrome://inspect/#devices`ます。</span><span class="sxs-lookup"><span data-stu-id="057d9-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="057d9-131">次のスクリーンショットに示すように、デバッグするタブの下の [**検査**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="057d9-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
