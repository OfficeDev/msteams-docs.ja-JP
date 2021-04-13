---
title: Microsoft Teams タブの DevTools
description: Microsoft Teams デスクトップ クライアントを使用する場合に DevTools にアクセスする方法について説明します。
ms.topic: how-to
keywords: devtools デバッグ モバイル クロム デスクトップ クライアント開発者ツール
ms.openlocfilehash: 7bd9403a74fd33619a2f8ac1b4b3a4c74a21175d
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654392"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="c8ec0-104">Microsoft Teams タブの DevTools</span><span class="sxs-lookup"><span data-stu-id="c8ec0-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="c8ec0-105">Teams がブラウザーで実行されている場合、ブラウザーの DevTools: F12 on Windows または Command-Option-I on MacOS に簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="c8ec0-106">DevTools を使用すると、次の情報にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="c8ec0-107">コンソール ログを表示します。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-107">View console logs.</span></span>
1. <span data-ttu-id="c8ec0-108">実行時に HTML、CSS、およびネットワーク要求を表示または変更します。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="c8ec0-109">JavaScript コードにブレークポイントを追加し、対話的なデバッグを実行します。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="c8ec0-110">この機能は、デスクトップクライアントと Android クライアントで使用できるのは、Developer Preview **後のみです** 。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="c8ec0-111">詳細については、「開発者プレビューを [有効にする方法」を参照してください](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-in-the-desktop"></a><span data-ttu-id="c8ec0-112">デスクトップで DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="c8ec0-112">Access DevTools in the Desktop</span></span>

<span data-ttu-id="c8ec0-113">Web バージョンとデスクトップ バージョンの Teams はほぼ同じですが、認証にはいくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="c8ec0-114">時には、何が起こっているのかを把握する唯一の方法は、DevTools を使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="c8ec0-115">デスクトップ クライアントで DevTools を使用するには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="c8ec0-116">開発者プレビューが有効 [になっているか確認します](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="c8ec0-117">タブを開き、DevTools で検査する必要があるものがあります。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="c8ec0-118">次のいずれかの方法で DevTools を開きます。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-118">Open the DevTools in one of the following ways:</span></span>
    * <span data-ttu-id="c8ec0-119">**Windows**: デスクトップ トレイで Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-119">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="c8ec0-120">**macOS**: ドックで Teams アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-120">**macOS**: Select the Teams icon in the Dock.</span></span>
 
   <span data-ttu-id="c8ec0-121">次の図は、タブ構成ダイアログで要素を検査する DevTools を示しています。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-121">The following image shows DevTools inspecting an element in a tab configuration dialog:</span></span>

   ![Tab と DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a><span data-ttu-id="c8ec0-123">Android クライアントから DevTools にアクセスする</span><span class="sxs-lookup"><span data-stu-id="c8ec0-123">Access DevTools from an Android client</span></span>

<span data-ttu-id="c8ec0-124">Teams Android クライアントから DevTools を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-124">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="c8ec0-125">DevTools を有効にするには、次の必要があります。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-125">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="c8ec0-126">開発者プレビュー [を有効にする](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-126">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="c8ec0-127">デバイスをデスクトップ コンピューターに接続し、リモート デバッグ用に Android デバイス [をセットアップします](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-127">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="c8ec0-128">Chrome ブラウザーで開きます `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="c8ec0-129">次 **の図** のように、デバッグするタブの下にある [検査] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c8ec0-129">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
