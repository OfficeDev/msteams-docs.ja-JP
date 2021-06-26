---
title: ドキュメントにTeamsする
description: ドキュメントの作成と発行Teams手順
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a567b0462397780650d6173df9dae1b340a06f97
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140516"
---
# <a name="contribute-to-teams-documentation"></a><span data-ttu-id="904bf-103">ドキュメントにTeamsする</span><span class="sxs-lookup"><span data-stu-id="904bf-103">Contribute to Teams documentation</span></span>

<span data-ttu-id="904bf-104">Teamsドキュメントは **、Microsoft Docs** のテクニカル ドキュメント ライブラリの一部です。</span><span class="sxs-lookup"><span data-stu-id="904bf-104">Teams documentation is part of the **Microsoft Docs** technical documentation library.</span></span> <span data-ttu-id="904bf-105">コンテンツは docsets と呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。</span><span class="sxs-lookup"><span data-stu-id="904bf-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="904bf-106">同じドキュメントセット内の記事の URL パスの拡張子は、同じ **docs.microsoft.com。**</span><span class="sxs-lookup"><span data-stu-id="904bf-106">Articles in the same docset have the same URL path extension after **docs.microsoft.com**.</span></span> <span data-ttu-id="904bf-107">たとえば、 `/docs.microsoft.com/microsoftteams/...` ドキュメントセット ファイル パスの先頭Teamsです。</span><span class="sxs-lookup"><span data-stu-id="904bf-107">For example, `/docs.microsoft.com/microsoftteams/...` is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="904bf-108">Teams記事は Markdown 構文で記述され、この構文でホストGitHub。</span><span class="sxs-lookup"><span data-stu-id="904bf-108">Teams articles are written in Markdown syntax and hosted on GitHub.</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="904bf-109">ワークスペースのセットアップ</span><span class="sxs-lookup"><span data-stu-id="904bf-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="904bf-110">Git を [インストールします](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。</span><span class="sxs-lookup"><span data-stu-id="904bf-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="904bf-111">インストール[Visual Studio Code](https://code.visualstudio.com/) (VS Code)。</span><span class="sxs-lookup"><span data-stu-id="904bf-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="904bf-112">ドキュメント[オーサリング パックを、VS Code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) Marketplace から直接インストールします。</span><span class="sxs-lookup"><span data-stu-id="904bf-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.</span></span>
<br><span data-ttu-id="904bf-113">&emsp;&emsp; または</span><span class="sxs-lookup"><span data-stu-id="904bf-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="904bf-114">次の手順でインストールVS Code。</span><span class="sxs-lookup"><span data-stu-id="904bf-114">Install within VS Code:</span></span>

   1. <span data-ttu-id="904bf-115">サイド アクティビティ **バーの [** 拡張機能] アイコンを選択するか、[表示 **] =>** [拡張機能] コマンドまたは [Ctrl+ Shift+ X] を使用して **、Microsoft Docs Authoring Pack を検索します**。</span><span class="sxs-lookup"><span data-stu-id="904bf-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command or Ctrl+Shift+X and, search for **Microsoft Docs Authoring Pack**.</span></span>
   1. <span data-ttu-id="904bf-116">**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="904bf-116">Select **Install**.</span></span>
   1. <span data-ttu-id="904bf-117">インストール後、[インストール] **が [** 歯車の管理] **ボタンに** 変わります。</span><span class="sxs-lookup"><span data-stu-id="904bf-117">After installation, the **Install** changes to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="904bf-118">Microsoft Docs コントリビューター ガイドを確認する</span><span class="sxs-lookup"><span data-stu-id="904bf-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="904bf-119">投稿者ガイドでは、Microsoft Docs プラットフォームで技術的なコンテンツを作成、発行、更新 **する方向を示** します。</span><span class="sxs-lookup"><span data-stu-id="904bf-119">The contributors guide provides direction to create, publish, and update technical content on the **Microsoft Docs** platform.</span></span> 

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="904bf-120">Microsoft ライティング、スタイル、およびコンテンツ ガイド</span><span class="sxs-lookup"><span data-stu-id="904bf-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="904bf-121">**[Microsoft ライティング スタイル ガイド](/style-guide/welcome)**: Microsoft ライティング スタイル ガイドは、テクニカル ライティングの包括的なリソースであり、音声とスタイルに対する Microsoft の最新のアプローチを反映しています。</span><span class="sxs-lookup"><span data-stu-id="904bf-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**: Microsoft Writing Style Guide is a comprehensive resource for technical writing and reflects Microsoft's modern approach to voice and style.</span></span> <span data-ttu-id="904bf-122">簡単に参照するには、ブラウザーの [お気に入り] メニューにこのオンライン **ガイドを追加** します。</span><span class="sxs-lookup"><span data-stu-id="904bf-122">For easy reference, add this online guide to your browser's **Favorites** menu.</span></span>

* <span data-ttu-id="904bf-123">**[開発者向けコンテンツ](/style-guide/developer-content/)** の作成 : Teams特定のコンテンツの作成は、プログラミングの概念とプロセスに関する基本的な理解を持つ開発者の対象ユーザーを対象とします。</span><span class="sxs-lookup"><span data-stu-id="904bf-123">**[Writing developer content](/style-guide/developer-content/)**: Teams specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="904bf-124">Microsoft のトーンとスタイルを維持しながら、明確で技術的に正確な情報を説得力のある方法で提供することが重要です。</span><span class="sxs-lookup"><span data-stu-id="904bf-124">It is important that you must provide clear, technically accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="904bf-125">**[ステップ バイ ステップの](/style-guide/procedures-instructions/writing-step-by-step-instructions)** 手順を記述する: 適用された対話型エクスペリエンスは、開発者が Microsoft の製品とテクノロジについて学ぶのに最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="904bf-125">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="904bf-126">プログレッシブ形式で複雑な手順や簡単な手順を提示する場合は、自然でユーザーフレンドリーです。</span><span class="sxs-lookup"><span data-stu-id="904bf-126">Presenting complex or simple procedures in a progressive format is natural and user friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="904bf-127">MarkDown リファレンス</span><span class="sxs-lookup"><span data-stu-id="904bf-127">MarkDown reference</span></span>

<span data-ttu-id="904bf-128">**Microsoft Docs** ページは **MarkDown 構文で記述され、Markdig** エンジンを介 [して解析](https://github.com/lunet-io/markdig) されます。</span><span class="sxs-lookup"><span data-stu-id="904bf-128">**Microsoft Docs** pages are written in **MarkDown** syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="904bf-129">特定のタグと書式設定の規則の詳細については [、「Docs Markdown リファレンス」を参照してください](/contribute/markdown-reference)。</span><span class="sxs-lookup"><span data-stu-id="904bf-129">For more information on specific tags and formatting conventions, see [Docs Markdown reference](/contribute/markdown-reference).</span></span>

## <a name="file-paths"></a><span data-ttu-id="904bf-130">ファイル パス</span><span class="sxs-lookup"><span data-stu-id="904bf-130">File Paths</span></span>

<span data-ttu-id="904bf-131">相対パスを使用して他のドキュメントセットへのリンクを作成する場合は、ドキュメント内のハイパーリンクの有効なファイル パスを設定することが重要です。</span><span class="sxs-lookup"><span data-stu-id="904bf-131">When using relative paths and creating links to other docsets, it is important to set a valid file path for hyperlinks in your documentation.</span></span> <span data-ttu-id="904bf-132">ビルドは、ファイル パスGitHubまたは有効な場合にのみ成功します。</span><span class="sxs-lookup"><span data-stu-id="904bf-132">Your build succeeds on GitHub only if the file path is correct or valid.</span></span>
 
<span data-ttu-id="904bf-133">ハイパーリンクとファイル パスの詳細については、ドキュメントのリンク [を使用するを参照してください](/contribute/how-to-write-links)。</span><span class="sxs-lookup"><span data-stu-id="904bf-133">For more information on hyperlinks and file paths, see [use links in documentation](/contribute/how-to-write-links).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="904bf-134">プラットフォーム ドキュメントセット **の一部** であるTeams参照するには、次のTeamsします。</span><span class="sxs-lookup"><span data-stu-id="904bf-134">To reference an article that is **part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="904bf-135">&emsp;&#x2714; 先頭スラッシュを付けずに相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="904bf-135">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="904bf-136">&emsp;&#x2714; Markdown ファイル拡張子を含めます。</span><span class="sxs-lookup"><span data-stu-id="904bf-136">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="904bf-137">Ex: **parent directory/directory/path-to-article.md** —>[アプリの](../concepts/building-an-app.md)構築 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="904bf-137">Ex:  **parent directory/directory/path-to-article.md** —> [Building an app for Microsoft Teams](../concepts/building-an-app.md)</span></span> <br><br>
> <span data-ttu-id="904bf-138">Microsoft Docs ライブラリの記事を参照するには、次のプラットフォーム ドキュメントセットTeams参照してください。</span><span class="sxs-lookup"><span data-stu-id="904bf-138">To reference a Microsoft Docs library article that **is not part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="904bf-139">&emsp;&#x2714; スラッシュで始まる相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="904bf-139">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="904bf-140">&emsp;&#x2714;ファイル拡張子を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="904bf-140">&emsp;&#x2714; Do not include the file extension.</span></span> <br> <span data-ttu-id="904bf-141">例: **/docset/address-to-file-location** —> Microsoft Graph API を使用してファイル [をMicrosoft Teams](/graph/api/resources/teams-api-overview)</span><span class="sxs-lookup"><span data-stu-id="904bf-141">Ex:  **/docset/address-to-file-location** —> [Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)</span></span><br><br>
> <span data-ttu-id="904bf-142">Microsoft Docs ライブラリの外部にあるページを参照するには、GitHubパスを `https` 使用します。</span><span class="sxs-lookup"><span data-stu-id="904bf-142">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="904bf-143">コード サンプルとスニペット</span><span class="sxs-lookup"><span data-stu-id="904bf-143">Code Samples and Snippets</span></span>

<span data-ttu-id="904bf-144">コード サンプルは、API と SDK を効果的に使用する重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="904bf-144">Code samples play an important role to use APIs and SDKs effectively.</span></span> <span data-ttu-id="904bf-145">よく提示されたコード サンプルは、説明的なテキストや指示情報だけでなく、物事の動作を明確に伝えます。</span><span class="sxs-lookup"><span data-stu-id="904bf-145">Well presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="904bf-146">コード サンプルは、正確で簡潔で、十分に文書化され、読者に優しい必要があります。</span><span class="sxs-lookup"><span data-stu-id="904bf-146">Your code samples must be accurate, concise, well documented, and reader friendly.</span></span> <span data-ttu-id="904bf-147">読みやすくするコードは、理解、テスト、デバッグ、保守、変更、拡張が容易である必要があります。</span><span class="sxs-lookup"><span data-stu-id="904bf-147">Code that is easy to read must be easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="904bf-148">詳細については、「ドキュメントに [コードを含める方法」を参照してください](/contribute/code-in-docs)。</span><span class="sxs-lookup"><span data-stu-id="904bf-148">For more information, see [how to include code in docs](/contribute/code-in-docs).</span></span>

## <a name="see-also"></a><span data-ttu-id="904bf-149">関連項目</span><span class="sxs-lookup"><span data-stu-id="904bf-149">See also</span></span>

* [<span data-ttu-id="904bf-150">Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="904bf-150">Microsoft Docs</span></span>](/)
* [<span data-ttu-id="904bf-151">投稿者ガイド</span><span class="sxs-lookup"><span data-stu-id="904bf-151">contributors guide</span></span>](/contribute)
* [<span data-ttu-id="904bf-152">ドキュメント スタイルと音声クイック スタート</span><span class="sxs-lookup"><span data-stu-id="904bf-152">Docs style and voice quick start</span></span>](/contribute/style-quick-start)
* [<span data-ttu-id="904bf-153">最先端 : ソース コードの読みやすさヒント</span><span class="sxs-lookup"><span data-stu-id="904bf-153">Cutting Edge : Source Code Readability Tips</span></span>](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [<span data-ttu-id="904bf-154">Teamsドキュメント</span><span class="sxs-lookup"><span data-stu-id="904bf-154">Teams documentation</span></span>](/microsoftteams/platform/overview)
* [<span data-ttu-id="904bf-155">GitHub</span><span class="sxs-lookup"><span data-stu-id="904bf-155">GitHub</span></span>](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a><span data-ttu-id="904bf-156">次の手順</span><span class="sxs-lookup"><span data-stu-id="904bf-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="904bf-157">Microsoft Docs の更新プログラムと最新のお知らせを取得する</span><span class="sxs-lookup"><span data-stu-id="904bf-157">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
