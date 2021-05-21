---
title: ドキュメントのMicrosoft Teamsする
description: ドキュメントの作成と発行Teams手順
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
# <a name="contributing-to-microsoft-teams-documentation"></a><span data-ttu-id="06b88-103">ドキュメントのMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="06b88-103">Contributing to Microsoft Teams documentation</span></span>

<span data-ttu-id="06b88-104">[Teamsドキュメントは](/microsoftteams/platform/overview)[、Microsoft Docs](https://docs.microsoft.com/)のテクニカル ドキュメント ライブラリの一部です。</span><span class="sxs-lookup"><span data-stu-id="06b88-104">[Teams documentation](/microsoftteams/platform/overview) is part of the [Microsoft Docs](https://docs.microsoft.com/) technical documentation library.</span></span> <span data-ttu-id="06b88-105">コンテンツは docsets と呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。</span><span class="sxs-lookup"><span data-stu-id="06b88-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="06b88-106">同じドキュメントセット内の記事は、docs .microsoft.com の後に同じ *<span></span> URL パス拡張子を持 microsoft.com。*</span><span class="sxs-lookup"><span data-stu-id="06b88-106">Articles in the same docset have the same URL path extension after *docs<span></span>.microsoft.com*.</span></span>  <span data-ttu-id="06b88-107">たとえば、 `/docs.microsoft.com/microsoftteams/...` ドキュメントセット ファイル パスの先頭Teamsです。</span><span class="sxs-lookup"><span data-stu-id="06b88-107">For example,  `/docs.microsoft.com/microsoftteams/...`   is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="06b88-108">Teams記事は[MarkDown](#markdown-reference)構文で記述され、この構文で[ホストGitHub。](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)</span><span class="sxs-lookup"><span data-stu-id="06b88-108">Teams articles are written in  [MarkDown](#markdown-reference) syntax and hosted on [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="06b88-109">ワークスペースのセットアップ</span><span class="sxs-lookup"><span data-stu-id="06b88-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="06b88-110">Git を [インストールします](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。</span><span class="sxs-lookup"><span data-stu-id="06b88-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="06b88-111">インストール[Visual Studio Code](https://code.visualstudio.com/) (VS Code)。</span><span class="sxs-lookup"><span data-stu-id="06b88-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="06b88-112">ドキュメント[オーサリング パックを、VS Code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) Marketplace から直接インストールします。</span><span class="sxs-lookup"><span data-stu-id="06b88-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.</span></span>
<br><span data-ttu-id="06b88-113">&emsp;&emsp; または</span><span class="sxs-lookup"><span data-stu-id="06b88-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="06b88-114">次の手順にVS Code。</span><span class="sxs-lookup"><span data-stu-id="06b88-114">Install from within VS Code:</span></span>

   1. <span data-ttu-id="06b88-115">サイド アクティビティ **バーの [** 拡張機能] アイコンを選択するか、[表示 **] =>** [拡張機能] コマンド (Ctrl + Shift + X) を使用して、ドキュメントオーサリング パック (Microsoft) を *検索* します。</span><span class="sxs-lookup"><span data-stu-id="06b88-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command (Ctrl+Shift+X) and search for the *Docs Authoring Pack* (Microsoft).</span></span>
   1. <span data-ttu-id="06b88-116">[インストール] **ボタンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="06b88-116">Select the **Install** button.</span></span>
   1. <span data-ttu-id="06b88-117">インストールが完了すると、[インストール] **ボタンが** [歯車の管理] **ボタンに** 変わります。</span><span class="sxs-lookup"><span data-stu-id="06b88-117">Once installation is complete, the **Install** button will change to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="06b88-118">Microsoft Docs コントリビューター ガイドを確認する</span><span class="sxs-lookup"><span data-stu-id="06b88-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="06b88-119">投稿者 [向けガイドでは](/contribute) 、Microsoft Docs プラットフォームで技術的なコンテンツを作成、発行、更新するための指示を提供します。</span><span class="sxs-lookup"><span data-stu-id="06b88-119">The [contributors guide](/contribute) offers direction for creating, publishing, and updating technical content on the Microsoft Docs platform.</span></span>

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="06b88-120">Microsoft ライティング、スタイル、およびコンテンツ ガイド</span><span class="sxs-lookup"><span data-stu-id="06b88-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="06b88-121">**[Microsoft 書き込みスタイル ガイド](/style-guide/welcome)**.</span><span class="sxs-lookup"><span data-stu-id="06b88-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**.</span></span> <span data-ttu-id="06b88-122">ブラウザーの [お気に入り] メニューにこのオンライン ガイド **を追加する方法を検討** してください。</span><span class="sxs-lookup"><span data-stu-id="06b88-122">Consider adding this online guide  to your browser's **Favorites** menu.</span></span> <span data-ttu-id="06b88-123">これは、今日の技術的な執筆のための包括的なリソースであり、音声とスタイルに対する Microsoft の最新のアプローチを反映しています。</span><span class="sxs-lookup"><span data-stu-id="06b88-123">It is a comprehensive resource for today's technical writing and reflects Microsoft's modern approach to voice and style.</span></span>

* <span data-ttu-id="06b88-124">**[開発者向けコンテンツの作成](/style-guide/developer-content/)**。</span><span class="sxs-lookup"><span data-stu-id="06b88-124">**[Writing developer content](/style-guide/developer-content/)**.</span></span> <span data-ttu-id="06b88-125">Teams固有のコンテンツは、プログラミングの概念とプロセスに関する基本的な理解を持つ開発者向けのコンテンツです。</span><span class="sxs-lookup"><span data-stu-id="06b88-125">Teams-specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="06b88-126">Microsoft のトーンとスタイルを維持しながら、技術的に正確な明確な情報を説得力のある方法で提供することが重要です。</span><span class="sxs-lookup"><span data-stu-id="06b88-126">It is important that you provide clear, technically-accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="06b88-127">**[ステップ バイ ステップの手順を記述します](/style-guide/procedures-instructions/writing-step-by-step-instructions)**。</span><span class="sxs-lookup"><span data-stu-id="06b88-127">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**.</span></span> <span data-ttu-id="06b88-128">適用された対話型エクスペリエンスは、開発者が Microsoft 製品とテクノロジについて学ぶのに最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="06b88-128">Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="06b88-129">プログレッシブ形式で複雑な手順や簡単な手順を提示する方法は、自然でユーザーフレンドリーです。</span><span class="sxs-lookup"><span data-stu-id="06b88-129">Presenting complex or simple procedures in a progressive format is natural and user-friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="06b88-130">MarkDown リファレンス</span><span class="sxs-lookup"><span data-stu-id="06b88-130">MarkDown reference</span></span>

 <span data-ttu-id="06b88-131">Microsoft Docs ページは MarkDown 構文で記述され [、Markdig](https://github.com/lunet-io/markdig) エンジンを介して解析されます。</span><span class="sxs-lookup"><span data-stu-id="06b88-131">Microsoft Docs pages are written in MarkDown syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="06b88-132">特定 *のタグ*[と書式設定の規則については](/contribute/markdown-reference)、「Docs Markdown リファレンス」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06b88-132">Please *see* [Docs Markdown reference](/contribute/markdown-reference) for specific tags and formatting conventions.</span></span>

## <a name="file-paths"></a><span data-ttu-id="06b88-133">ファイル パス</span><span class="sxs-lookup"><span data-stu-id="06b88-133">File Paths</span></span>

<span data-ttu-id="06b88-134">ドキュメント内のハイパーリンクの有効なファイル パスを設定すると、特に相対パスを使用して他のドキュメントセットへのリンクを作成する場合は、問題になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="06b88-134">Setting a valid file path for hyperlinks in your documentation can be a challenge, especially when using relative paths and creating links to other docsets.</span></span>  <span data-ttu-id="06b88-135">ファイル パスが正しくないか無効GitHub場合、ビルドは成功しません。</span><span class="sxs-lookup"><span data-stu-id="06b88-135">Your build won't succeed on GitHub if the file path is incorrect or invalid.</span></span>

<span data-ttu-id="06b88-136">ハイパーリンクとファイル パスの詳細については、「ドキュメントでリンクを使用 [する」を参照してください](/contribute/how-to-write-links)。</span><span class="sxs-lookup"><span data-stu-id="06b88-136">For more information on hyperlinks and file paths, see [Use links in documentation](/contribute/how-to-write-links).</span></span>

>[!IMPORTANT]
> <span data-ttu-id="06b88-137">プラットフォーム ドキュメントセット *の一部* であるTeams参照するには、次のTeamsします。</span><span class="sxs-lookup"><span data-stu-id="06b88-137">To reference an article that is *part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="06b88-138">&emsp;&#x2714; 先頭スラッシュを付けずに相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="06b88-138">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="06b88-139">&emsp;&#x2714; Markdown ファイル拡張子を含めます。</span><span class="sxs-lookup"><span data-stu-id="06b88-139">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="06b88-140">Ex:  **parent directory/directory/path-to-article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span><span class="sxs-lookup"><span data-stu-id="06b88-140">Ex:  **parent directory/directory/path-to-article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)`</span></span> <br><br>
> <span data-ttu-id="06b88-141">Microsoft Docs ライブラリの記事を参照するには、次のプラットフォーム ドキュメントセットTeams参照してください。</span><span class="sxs-lookup"><span data-stu-id="06b88-141">To reference a Microsoft Docs library article that *is not part of* the Teams platform docset:</span></span><br>
> <span data-ttu-id="06b88-142">&emsp;&#x2714; スラッシュで始まる相対パスを使用します。</span><span class="sxs-lookup"><span data-stu-id="06b88-142">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="06b88-143">&emsp;&#x2714;ファイル拡張子を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="06b88-143">&emsp;&#x2714; Don't include the file extension.</span></span> <br> <span data-ttu-id="06b88-144">例: **/docset/address-to-file-location —>**`[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span><span class="sxs-lookup"><span data-stu-id="06b88-144">Ex:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`</span></span><br><br>
> <span data-ttu-id="06b88-145">Microsoft Docs ライブラリの外部にあるページを参照するには、GitHubパスを `https` 使用します。</span><span class="sxs-lookup"><span data-stu-id="06b88-145">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="06b88-146">コード サンプルとスニペット</span><span class="sxs-lookup"><span data-stu-id="06b88-146">Code Samples and Snippets</span></span>

<span data-ttu-id="06b88-147">コード サンプルは、開発者が API と SDK を正常に使用する上で重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="06b88-147">Code samples play an important role in helping developers successfully use APIs and SDKs.</span></span> <span data-ttu-id="06b88-148">よく示されたコード サンプルは、説明的なテキストや指示情報だけでなく、物事の動作を明確に伝えます。</span><span class="sxs-lookup"><span data-stu-id="06b88-148">Well-presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="06b88-149">コード サンプルは、正確で簡潔で、十分に文書化され、最も重要なのは、読者に優しいコード サンプルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="06b88-149">Your code samples should be accurate, concise, well-documented, and, most importantly, reader-friendly.</span></span> <span data-ttu-id="06b88-150">読みやすくするコードは、理解、テスト、デバッグ、保守、変更、拡張も簡単です。</span><span class="sxs-lookup"><span data-stu-id="06b88-150">Code that is easy-to-read is also easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="06b88-151">詳細については、「ドキュメントに [コードを含める方法」を参照してください](/contribute/code-in-docs)。</span><span class="sxs-lookup"><span data-stu-id="06b88-151">For more information, see [How to include code in docs](/contribute/code-in-docs).</span></span>

## <a name="see-also"></a><span data-ttu-id="06b88-152">関連項目</span><span class="sxs-lookup"><span data-stu-id="06b88-152">See also</span></span>

* [<span data-ttu-id="06b88-153">ドキュメント スタイルと音声クイック スタート</span><span class="sxs-lookup"><span data-stu-id="06b88-153">Docs style and voice quick start</span></span>](/contribute/style-quick-start)
* <span data-ttu-id="06b88-154">[最先端 : ソース コードの読みやすさヒント。](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)</span><span class="sxs-lookup"><span data-stu-id="06b88-154">[Cutting Edge : Source Code Readability Tips](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="06b88-155">Microsoft Docs の更新プログラムと最新のお知らせを取得する</span><span class="sxs-lookup"><span data-stu-id="06b88-155">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
