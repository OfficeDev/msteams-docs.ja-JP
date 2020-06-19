---
title: Microsoft Teams ドキュメントへの投稿
description: Teams ドキュメントを作成して発行するための手順
author: laujan
ms.author: lajanuar
ms.topic: how to
ms.openlocfilehash: 5e76c6521792d7db1b589d7e6ad3fe0ac2bd8479
ms.sourcegitcommit: 6c692734a382865531a83b9ebd6f604212f484fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "44801193"
---
# <a name="contributing-to-microsoft-teams-documentation"></a><span data-ttu-id="ccea0-103">Microsoft Teams ドキュメントへの投稿</span><span class="sxs-lookup"><span data-stu-id="ccea0-103">Contributing to Microsoft Teams documentation</span></span>

<span data-ttu-id="ccea0-104">[Teams ドキュメント](/microsoftteams/platform/overview)は、 [Microsoft Docs](https://docs.microsoft.com/)技術ドキュメントライブラリに含まれています。</span><span class="sxs-lookup"><span data-stu-id="ccea0-104">[Teams documentation](/microsoftteams/platform/overview) is part of the [Microsoft Docs](https://docs.microsoft.com/) technical documentation library.</span></span> <span data-ttu-id="ccea0-105">コンテンツは、docsets と呼ばれるグループに整理され、それぞれが1つのエンティティとして管理する関連ドキュメントのグループを表します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="ccea0-106">同じ docset の記事には、 \* <span></span> microsoft.com\*の後に同じ URL パス拡張があります。</span><span class="sxs-lookup"><span data-stu-id="ccea0-106">Articles in the same docset have the same URL path extension after *docs<span></span>.microsoft.com*.</span></span>  <span data-ttu-id="ccea0-107">たとえば、 `/docs.microsoft.com/microsoftteams/...` は Teams docset ファイルパスの先頭です。</span><span class="sxs-lookup"><span data-stu-id="ccea0-107">For example,  `/docs.microsoft.com/microsoftteams/...`   is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="ccea0-108">Teams の記事は[MarkDown](#markdown-reference)構文で記述され、 [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)でホストされます。</span><span class="sxs-lookup"><span data-stu-id="ccea0-108">Teams articles are written in  [MarkDown](#markdown-reference) syntax and hosted on [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="ccea0-109">ワークスペースの設定</span><span class="sxs-lookup"><span data-stu-id="ccea0-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ccea0-110">[Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="ccea0-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="ccea0-111">[Visual Studio code](https://code.visualstudio.com/) (VS コード) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="ccea0-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="ccea0-112">[ドキュメント作成パック](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)を VS Code Marketplace から直接インストールする</span><span class="sxs-lookup"><span data-stu-id="ccea0-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace</span></span>
<br><span data-ttu-id="ccea0-113">&emsp;&emsp;や</span><span class="sxs-lookup"><span data-stu-id="ccea0-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ccea0-114">VS Code 内からのインストール:</span><span class="sxs-lookup"><span data-stu-id="ccea0-114">Install from within VS Code:</span></span>

   1. <span data-ttu-id="ccea0-115">サイドアクティビティバーで [ **extensions] アイコン**を選択するか、[**表示 => extensions** ] コマンド (Ctrl + Shift + X) を使用して、 *Docs Authoring Pack* (Microsoft) を検索します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command (Ctrl+Shift+X) and search for the *Docs Authoring Pack* (Microsoft).</span></span>
   1. <span data-ttu-id="ccea0-116">[**インストール**] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-116">Select the **Install** button.</span></span>
   1. <span data-ttu-id="ccea0-117">インストールが完了すると、[**インストール**] ボタンが [歯車の**管理**] ボタンに変わります。</span><span class="sxs-lookup"><span data-stu-id="ccea0-117">Once installation is complete, the **Install** button will change to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="ccea0-118">Microsoft Docs コントリビューターガイドを確認する</span><span class="sxs-lookup"><span data-stu-id="ccea0-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="ccea0-119">[投稿者ガイド](/contribute)は、Microsoft/docの技術的なコンテンツを作成、発行、更新するための指示を提供します。「 [Docs Style」および「voice quick Start](/contribute/style-quick-start) *」も参照してください*。</span><span class="sxs-lookup"><span data-stu-id="ccea0-119">The [contributors guide](/contribute) offers direction for creating, publishing, and updating technical content on Microsoft /docs. *See also*, [Docs style and voice quick start](/contribute/style-quick-start) .</span></span>

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="ccea0-120">Microsoft の書き方、スタイル、およびコンテンツガイド</span><span class="sxs-lookup"><span data-stu-id="ccea0-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="ccea0-121">**[Microsoft の書き方のスタイルガイド](/style-guide/welcome)** です。</span><span class="sxs-lookup"><span data-stu-id="ccea0-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**.</span></span> <span data-ttu-id="ccea0-122">このオンラインガイドをブラウザーの [**お気に入り**] メニューに追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="ccea0-122">Consider adding this online guide  to your browser's **Favorites** menu.</span></span> <span data-ttu-id="ccea0-123">これは、今日の技術的な執筆に関する包括的なリソースであり、音声とスタイルに対する Microsoft の先進のアプローチを反映しています。</span><span class="sxs-lookup"><span data-stu-id="ccea0-123">It is a comprehensive resource for today's technical writing and reflects Microsoft's modern approach to voice and style.</span></span>

* <span data-ttu-id="ccea0-124">**[開発者向けコンテンツを書く](/style-guide/developer-content/)**。</span><span class="sxs-lookup"><span data-stu-id="ccea0-124">**[Writing developer content](/style-guide/developer-content/)**.</span></span> <span data-ttu-id="ccea0-125">Teams 固有のコンテンツは、プログラミングの概念とプロセスについて基本的に理解している開発者を対象としています。</span><span class="sxs-lookup"><span data-stu-id="ccea0-125">Teams-specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="ccea0-126">Microsoft の語調とスタイルを維持しながら、わかりやすく技術的に正確な情報を提供することが重要です。</span><span class="sxs-lookup"><span data-stu-id="ccea0-126">It is important that you provide clear, technically-accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="ccea0-127">ステップ**[ごとの指示を記述](/style-guide/procedures-instructions/writing-step-by-step-instructions)** します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-127">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**.</span></span> <span data-ttu-id="ccea0-128">適用された対話的なエクスペリエンスは、開発者が Microsoft の製品とテクノロジについて理解するのに便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="ccea0-128">Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="ccea0-129">複雑な手順や単純な手順をプログレッシブ形式で表現することは、自然でわかりやすいものです。</span><span class="sxs-lookup"><span data-stu-id="ccea0-129">Presenting complex or simple procedures in a progressive format is natural and user-friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="ccea0-130">MarkDown リファレンス</span><span class="sxs-lookup"><span data-stu-id="ccea0-130">MarkDown reference</span></span>

 <span data-ttu-id="ccea0-131">Microsoft Docs ページは、MarkDown 構文で記述され、 [Markdig](https://github.com/lunet-io/markdig)エンジンで解析されます。</span><span class="sxs-lookup"><span data-stu-id="ccea0-131">Microsoft Docs pages are written in MarkDown syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="ccea0-132">特定のタグと書式設定規則については、 *「* [Docs Markdown reference](/contribute/markdown-reference) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ccea0-132">Please *see* [Docs Markdown reference](/contribute/markdown-reference) for specific tags and formatting conventions.</span></span>

## <a name="file-paths"></a><span data-ttu-id="ccea0-133">ファイルパス</span><span class="sxs-lookup"><span data-stu-id="ccea0-133">File Paths</span></span>

<span data-ttu-id="ccea0-134">ドキュメントでハイパーリンクに有効なファイルパスを設定することは、特に相対パスを使用して他の docsets へのリンクを作成する場合には、課題になることがあります。</span><span class="sxs-lookup"><span data-stu-id="ccea0-134">Setting a valid file path for hyperlinks in your documentation can be a challenge, especially when using relative paths and creating links to other docsets.</span></span>  <span data-ttu-id="ccea0-135">ファイルパスが正しくないか、無効な場合は、GitHub でのビルドは成功しません。</span><span class="sxs-lookup"><span data-stu-id="ccea0-135">Your build won't succeed on GitHub if the file path is incorrect or invalid.</span></span>

<span data-ttu-id="ccea0-136">ハイパーリンクとファイルパスの詳細については、 *「* [ドキュメントでのリンクの使用](/contribute/how-to-write-links)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ccea0-136">For more information on  hyperlinks and file paths, please *see* [Use links in documentation](/contribute/how-to-write-links).</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ccea0-137">Teams のプラットフォーム docset*の一部*である記事を参照するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-137">To reference an article that is *part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="ccea0-138">&emsp;&#x2714; には、スラッシュを先頭に付けずに相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-138">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="ccea0-139">&emsp;Markdown ファイル拡張子が含まれている&#x2714;。</span><span class="sxs-lookup"><span data-stu-id="ccea0-139">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="ccea0-140">Ex:**親ディレクトリ/ディレクトリ/パス名**: >`[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span><span class="sxs-lookup"><span data-stu-id="ccea0-140">Ex:  **parent directory/directory/path-to-article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span></span> <br><br>
> <span data-ttu-id="ccea0-141"><https://docs.microsoft.com/>Teams のプラットフォーム docset に含まれて*いない*Microsoft Docs library () の記事を参照するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-141">To reference a Microsoft Docs library (<https://docs.microsoft.com/>) article that *isn't part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="ccea0-142">&emsp;&#x2714; スラッシュで始まる相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="ccea0-142">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="ccea0-143">&emsp;&#x2714; ファイル拡張子は含めないでください。</span><span class="sxs-lookup"><span data-stu-id="ccea0-143">&emsp;&#x2714; Don't include the file extension.</span></span> <br> <span data-ttu-id="ccea0-144">Ex: **/docset/addressofflocation** — >`[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span><span class="sxs-lookup"><span data-stu-id="ccea0-144">Ex:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span></span>
>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="ccea0-145">コードサンプルとスニペット</span><span class="sxs-lookup"><span data-stu-id="ccea0-145">Code Samples and Snippets</span></span>

<span data-ttu-id="ccea0-146">コードサンプルは、開発者が Api と Sdk を正常に使用するのに役立つ重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="ccea0-146">Code samples play an important role in helping developers successfully use APIs and SDKs.</span></span> <span data-ttu-id="ccea0-147">適切に表示されているコードサンプルは、説明テキストと説明情報だけではなく、どのように機能するかを伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="ccea0-147">Well-presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="ccea0-148">コードサンプルは正確で簡潔で、ドキュメント化されている必要があります。また、最も重要なのは閲覧者フレンドリです。</span><span class="sxs-lookup"><span data-stu-id="ccea0-148">Your code samples should be accurate, concise, well-documented, and, most importantly, reader-friendly.</span></span> <span data-ttu-id="ccea0-149">読みやすいコードも理解しやすく、テスト、デバッグ、保守、変更、拡張が簡単です。</span><span class="sxs-lookup"><span data-stu-id="ccea0-149">Code that is easy-to-read is also easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="ccea0-150">*「* [ドキュメントにコードを含める方法」を](/contribute/code-in-docs)参照してください。読みやすさのヒントについては、「[切削エッジ: ソースコードの読みやすさのヒント](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips) *」も参照*してください。</span><span class="sxs-lookup"><span data-stu-id="ccea0-150">*See* [How to include code in docs](/contribute/code-in-docs). For readability tips, please *see also* [Cutting Edge : Source Code Readability Tips](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ccea0-151">Microsoft Docs の更新プログラムと最新のアナウンスを入手する</span><span class="sxs-lookup"><span data-stu-id="ccea0-151">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
