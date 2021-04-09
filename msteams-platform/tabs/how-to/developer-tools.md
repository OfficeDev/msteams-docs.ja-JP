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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="ea1ff-104">Microsoft Teams タブの DevTools</span><span class="sxs-lookup"><span data-stu-id="ea1ff-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="ea1ff-105">Teams がブラウザーで実行されている場合、ブラウザーの DevTools: F12 on Windows または Command-Option-I on MacOS に簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="ea1ff-106">DevTools を使用すると、次の情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="ea1ff-107">コンソール ログを表示します。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-107">View console logs.</span></span>
1. <span data-ttu-id="ea1ff-108">実行時に HTML、CSS、およびネットワーク要求を表示または変更します。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="ea1ff-109">JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="ea1ff-110">この機能は、デスクトップクライアントと Android クライアントでのみ使用できます **。Developer Preview** が有効になっています。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-110">The feature is only available in desktop and Android clients after **Developer Preview** has been enabled.</span></span> <span data-ttu-id="ea1ff-111">詳細については、「開発者プレビューを [有効にする方法」を参照してください](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-in-the-desktop"></a><span data-ttu-id="ea1ff-112">デスクトップで DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="ea1ff-112">Access DevTools in the Desktop</span></span>

<span data-ttu-id="ea1ff-113">Web バージョンとデスクトップ バージョンの Teams はほぼ同じですが、認証に関していくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-113">While the web version and the desktop version of Teams are almost exactly the same, there are some differences with respect to authentication.</span></span> <span data-ttu-id="ea1ff-114">時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="ea1ff-115">デスクトップ クライアントで DevTools を使用するには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="ea1ff-116">開発者プレビューが有効 [になっているか確認します](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="ea1ff-117">タブを開き、DevTools で検査する必要があるものがあります。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="ea1ff-118">次のいずれかの方法で DevTools を開きます。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-118">Open the DevTools in one of the following ways:</span></span>
    * <span data-ttu-id="ea1ff-119">**Windows**: デスクトップ トレイで Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-119">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="ea1ff-120">**MacOS**: ドックで Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-120">**MacOS**: Select the Teams icon in the Dock.</span></span>
 
   <span data-ttu-id="ea1ff-121">次の図は、タブ構成ダイアログで要素を検査する DevTools を示しています。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-121">The following image shows DevTools inspecting an element in a tab configuration dialog:</span></span>

   ![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a><span data-ttu-id="ea1ff-123">Android クライアントから DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="ea1ff-123">Access DevTools from an Android client</span></span>

<span data-ttu-id="ea1ff-124">Teams Android クライアントから DevTools を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-124">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="ea1ff-125">DevTools を有効にするには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-125">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="ea1ff-126">開発者プレビュー [を有効にする](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-126">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="ea1ff-127">デバイスをデスクトップ コンピューターに接続し、リモート デバッグ用に Android デバイス [をセットアップします](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-127">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="ea1ff-128">Chrome ブラウザーで開きます `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="ea1ff-129">次 **の図** のように、デバッグするタブの下にある [検査] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ea1ff-129">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
