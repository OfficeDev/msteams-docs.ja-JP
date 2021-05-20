---
title: Microsoft Teamsドキュメントへの貢献
description: Teams ドキュメントを作成および公開する手順
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: 52253bb096857e2cb883295c8ae6b58518506d9a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566230"
---
# <a name="contributing-to-microsoft-teams-documentation"></a><span data-ttu-id="128e3-103">Microsoft Teamsドキュメントへの貢献</span><span class="sxs-lookup"><span data-stu-id="128e3-103">Contributing to Microsoft Teams documentation</span></span>

<span data-ttu-id="128e3-104">[Teams ドキュメント](/microsoftteams/platform/overview)は[、Microsoft Docs](https://docs.microsoft.com/)テクニカル ドキュメント ライブラリの一部です。</span><span class="sxs-lookup"><span data-stu-id="128e3-104">[Teams documentation](/microsoftteams/platform/overview) is part of the [Microsoft Docs](https://docs.microsoft.com/) technical documentation library.</span></span> <span data-ttu-id="128e3-105">コンテンツは docsets と呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。</span><span class="sxs-lookup"><span data-stu-id="128e3-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="128e3-106">同じドキュメントセット内のアーティクルは *、ドキュメント <span></span> .microsoft.com* の後に同じ URL パス拡張子を持ちます。</span><span class="sxs-lookup"><span data-stu-id="128e3-106">Articles in the same docset have the same URL path extension after *docs<span></span>.microsoft.com*.</span></span>  <span data-ttu-id="128e3-107">たとえば `/docs.microsoft.com/microsoftteams/...` 、docset ファイルパスの先頭Teams。</span><span class="sxs-lookup"><span data-stu-id="128e3-107">For example,  `/docs.microsoft.com/microsoftteams/...`   is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="128e3-108">Teams記事は[MarkDown](#markdown-reference)構文で記述され[、GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)でホストされます。</span><span class="sxs-lookup"><span data-stu-id="128e3-108">Teams articles are written in  [MarkDown](#markdown-reference) syntax and hosted on [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="128e3-109">ワークスペースを設定する</span><span class="sxs-lookup"><span data-stu-id="128e3-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="128e3-110">[Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="128e3-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="128e3-111">[Visual Studio Code](https://code.visualstudio.com/) (VS Code) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="128e3-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="128e3-112">[ドキュメントオーサリングパックを](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)VS Codeマーケットプレースから直接インストールします。</span><span class="sxs-lookup"><span data-stu-id="128e3-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.</span></span>
<br><span data-ttu-id="128e3-113">&emsp;&emsp; 又は</span><span class="sxs-lookup"><span data-stu-id="128e3-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="128e3-114">VS Code内からインストールする:</span><span class="sxs-lookup"><span data-stu-id="128e3-114">Install from within VS Code:</span></span>

   1. <span data-ttu-id="128e3-115">サイドアクティビティバーの **[拡張機能]アイコン** を選択するか、[ **表示 =>拡張** ]コマンド(Ctrl +Shift+X)を使用して *ドキュメントオーサリングパック* (Microsoft)を検索します。</span><span class="sxs-lookup"><span data-stu-id="128e3-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command (Ctrl+Shift+X) and search for the *Docs Authoring Pack* (Microsoft).</span></span>
   1. <span data-ttu-id="128e3-116">[ **インストール** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="128e3-116">Select the **Install** button.</span></span>
   1. <span data-ttu-id="128e3-117">インストールが完了すると、[ **インストール** ]ボタンが[歯車の **管理** ]ボタンに変わります。</span><span class="sxs-lookup"><span data-stu-id="128e3-117">Once installation is complete, the **Install** button will change to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="128e3-118">マイクロソフト ドキュメント寄稿者ガイドを確認する</span><span class="sxs-lookup"><span data-stu-id="128e3-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="128e3-119">[寄稿者ガイド](/contribute)では、Microsoft Docs プラットフォーム上での技術的なコンテンツの作成、公開、および更新の手順を示します。</span><span class="sxs-lookup"><span data-stu-id="128e3-119">The [contributors guide](/contribute) offers direction for creating, publishing, and updating technical content on the Microsoft Docs platform.</span></span>

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="128e3-120">マイクロソフトライティングガイド、スタイルガイド、コンテンツガイド</span><span class="sxs-lookup"><span data-stu-id="128e3-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="128e3-121">**[マイクロソフトライティングスタイルガイド](/style-guide/welcome)**.</span><span class="sxs-lookup"><span data-stu-id="128e3-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**.</span></span> <span data-ttu-id="128e3-122">このオンライン ガイドをブラウザ **のお気に入り** メニューに追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="128e3-122">Consider adding this online guide  to your browser's **Favorites** menu.</span></span> <span data-ttu-id="128e3-123">これは、今日の技術的な執筆のための包括的なリソースであり、音声とスタイルに対するマイクロソフトの現代的なアプローチを反映しています。</span><span class="sxs-lookup"><span data-stu-id="128e3-123">It is a comprehensive resource for today's technical writing and reflects Microsoft's modern approach to voice and style.</span></span>

* <span data-ttu-id="128e3-124">**[開発者コンテンツの作成](/style-guide/developer-content/)**:</span><span class="sxs-lookup"><span data-stu-id="128e3-124">**[Writing developer content](/style-guide/developer-content/)**.</span></span> <span data-ttu-id="128e3-125">Teams固有のコンテンツは、プログラミングの概念とプロセスを基本的に理解している開発者の対象読者を対象としています。</span><span class="sxs-lookup"><span data-stu-id="128e3-125">Teams-specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="128e3-126">マイクロソフトのトーンとスタイルを維持しながら、明確で技術的に正確な情報を説得力のある方法で提供することが重要です。</span><span class="sxs-lookup"><span data-stu-id="128e3-126">It is important that you provide clear, technically-accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="128e3-127">**[ステップバイステップの手順を書く](/style-guide/procedures-instructions/writing-step-by-step-instructions)**.</span><span class="sxs-lookup"><span data-stu-id="128e3-127">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**.</span></span> <span data-ttu-id="128e3-128">開発者が Microsoft 製品やテクノロジについて理解するには、応用エクスペリエンスと対話型エクスペリエンスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="128e3-128">Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="128e3-129">複雑なプロシージャや単純なプロシージャをプログレッシブ形式で提示するのは自然で、ユーザーフレンドリーです。</span><span class="sxs-lookup"><span data-stu-id="128e3-129">Presenting complex or simple procedures in a progressive format is natural and user-friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="128e3-130">マークダウン リファレンス</span><span class="sxs-lookup"><span data-stu-id="128e3-130">MarkDown reference</span></span>

 <span data-ttu-id="128e3-131">マイクロソフトドキュメントページは、マークダウン構文で記述され、 [マークディグ](https://github.com/lunet-io/markdig) エンジンを介して解析されます。</span><span class="sxs-lookup"><span data-stu-id="128e3-131">Microsoft Docs pages are written in MarkDown syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="128e3-132">特定のタグと書式規則 *については*[、ドキュメントマークダウンのリファレンス](/contribute/markdown-reference)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="128e3-132">Please *see* [Docs Markdown reference](/contribute/markdown-reference) for specific tags and formatting conventions.</span></span>

## <a name="file-paths"></a><span data-ttu-id="128e3-133">ファイル パス</span><span class="sxs-lookup"><span data-stu-id="128e3-133">File Paths</span></span>

<span data-ttu-id="128e3-134">特に、相対パスを使用して他のドキュメントセットへのリンクを作成する場合は、ドキュメント内のハイパーリンクに有効なファイル パスを設定するのが難しい場合があります。</span><span class="sxs-lookup"><span data-stu-id="128e3-134">Setting a valid file path for hyperlinks in your documentation can be a challenge, especially when using relative paths and creating links to other docsets.</span></span>  <span data-ttu-id="128e3-135">ファイル パスが正しくない場合や無効な場合、ビルドはGitHubで成功しません。</span><span class="sxs-lookup"><span data-stu-id="128e3-135">Your build won't succeed on GitHub if the file path is incorrect or invalid.</span></span>

<span data-ttu-id="128e3-136">ハイパーリンクとファイル パスの詳細については、 [ドキュメントのリンクを使用するを参照してください](/contribute/how-to-write-links)。</span><span class="sxs-lookup"><span data-stu-id="128e3-136">For more information on hyperlinks and file paths, see [Use links in documentation](/contribute/how-to-write-links).</span></span>

>[!IMPORTANT]
> <span data-ttu-id="128e3-137">Teamsプラットフォームの docset *の一部* である記事を参照するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="128e3-137">To reference an article that is *part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="128e3-138">&emsp;&#x2714;先頭のスラッシュを付けずに相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="128e3-138">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="128e3-139">&emsp;&#x2714; マークダウン ファイル拡張子を含めます。</span><span class="sxs-lookup"><span data-stu-id="128e3-139">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="128e3-140">Ex:  **親ディレクトリ/ディレクトリ/パスから article.md へ** -> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span><span class="sxs-lookup"><span data-stu-id="128e3-140">Ex:  **parent directory/directory/path-to-article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span></span> <br><br>
> <span data-ttu-id="128e3-141">Teams プラットフォームのドキュメントセットに *含まれていない* Microsoft Docs ライブラリの記事を参照するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="128e3-141">To reference a Microsoft Docs library article that *is not part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="128e3-142">&emsp;&#x2714; スラッシュで始まる相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="128e3-142">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="128e3-143">&emsp;&#x2714; ファイル拡張子を含まない</span><span class="sxs-lookup"><span data-stu-id="128e3-143">&emsp;&#x2714; Don't include the file extension.</span></span> <br> <span data-ttu-id="128e3-144">指定する場所:  **/docset/アドレスからファイルへの場所** -> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span><span class="sxs-lookup"><span data-stu-id="128e3-144">Ex:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span></span><br><br>
> <span data-ttu-id="128e3-145">GitHubなどの Microsoft Docs ライブラリの外部にあるページを参照するには、完全 `https` なファイル パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="128e3-145">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="128e3-146">コード サンプルとスニペット</span><span class="sxs-lookup"><span data-stu-id="128e3-146">Code Samples and Snippets</span></span>

<span data-ttu-id="128e3-147">コード サンプルは、開発者が API と SDK を正常に使用するうえで重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="128e3-147">Code samples play an important role in helping developers successfully use APIs and SDKs.</span></span> <span data-ttu-id="128e3-148">適切に提示されたコード サンプルは、説明テキストや説明情報よりも、物事の動作を明確に伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="128e3-148">Well-presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="128e3-149">コード サンプルは、正確で簡潔で、十分に文書化されていて、最も重要なのは読者に優しい必要があります。</span><span class="sxs-lookup"><span data-stu-id="128e3-149">Your code samples should be accurate, concise, well-documented, and, most importantly, reader-friendly.</span></span> <span data-ttu-id="128e3-150">読みやすいコードは、理解、テスト、デバッグ、保守、変更、拡張も簡単です。</span><span class="sxs-lookup"><span data-stu-id="128e3-150">Code that is easy-to-read is also easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="128e3-151">詳細については、「 [docs にコードを含める方法](/contribute/code-in-docs)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="128e3-151">For more information, see [How to include code in docs](/contribute/code-in-docs).</span></span>

## <a name="see-also"></a><span data-ttu-id="128e3-152">関連項目</span><span class="sxs-lookup"><span data-stu-id="128e3-152">See also</span></span>

* [<span data-ttu-id="128e3-153">ドキュメントスタイルと音声クイックスタート</span><span class="sxs-lookup"><span data-stu-id="128e3-153">Docs style and voice quick start</span></span>](/contribute/style-quick-start)
* <span data-ttu-id="128e3-154">[最先端: ソースコードの読みやすヒント。](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)</span><span class="sxs-lookup"><span data-stu-id="128e3-154">[Cutting Edge : Source Code Readability Tips](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="128e3-155">マイクロソフト ドキュメントの更新プログラムと最新のお知らせを入手する</span><span class="sxs-lookup"><span data-stu-id="128e3-155">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
