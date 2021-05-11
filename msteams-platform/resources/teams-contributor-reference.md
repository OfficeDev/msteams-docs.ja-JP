---
title: ドキュメントのMicrosoft Teamsする
description: ドキュメントの作成と発行Teams手順
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a6742b8b994cc3752df923db75a3d7d77cbebd83
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019672"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>ドキュメントのMicrosoft Teamsする

[Teamsドキュメントは](/microsoftteams/platform/overview)[、Microsoft Docs](https://docs.microsoft.com/)のテクニカル ドキュメント ライブラリの一部です。 コンテンツは docsets と呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。 同じドキュメントセット内の記事は、docs .microsoft.com の後に同じ *<span></span> URL パス拡張子を持 microsoft.com。*  たとえば、 `/docs.microsoft.com/microsoftteams/...` ドキュメントセット ファイル パスの先頭Teamsです。 Teams記事は[MarkDown](#markdown-reference)構文で記述され、この構文で[ホストGitHub。](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)

## <a name="set-up-your-workspace"></a>ワークスペースのセットアップ

> [!div class="checklist"]
>
> * Git を [インストールします](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * インストール[Visual Studio Code](https://code.visualstudio.com/) (VS Code)。
> * ドキュメント[オーサリング パックを、VS Code](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) Marketplace から直接インストールする
<br>&emsp;&emsp; または

> [!div class="checklist"]
>
> * 次の手順にVS Code。

   1. サイド アクティビティ **バーの [** 拡張機能] アイコンを選択するか、[表示 **] =>** [拡張機能] コマンド (Ctrl + Shift + X) を使用して、ドキュメントオーサリング パック (Microsoft) を *検索* します。
   1. [インストール] **ボタンを選択** します。
   1. インストールが完了すると、[インストール] **ボタンが** [歯車の管理] **ボタンに** 変わります。

## <a name="review-the-microsoft-docs-contributors-guide"></a>Microsoft Docs コントリビューター ガイドを確認する

投稿者 [向けガイドでは](/contribute) 、Microsoft Docs プラットフォームで技術的なコンテンツを作成、発行、更新するための指示を提供します。 *「ドキュメント スタイル*[と音声クイック スタート」も参照してください](/contribute/style-quick-start)。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft ライティング、スタイル、およびコンテンツ ガイド

* **[Microsoft 書き込みスタイル ガイド](/style-guide/welcome)**. ブラウザーの [お気に入り] メニューにこのオンライン ガイド **を追加する方法を検討** してください。 これは、今日の技術的な執筆のための包括的なリソースであり、音声とスタイルに対する Microsoft の最新のアプローチを反映しています。

* **[開発者向けコンテンツの作成](/style-guide/developer-content/)**。 Teams固有のコンテンツは、プログラミングの概念とプロセスに関する基本的な理解を持つ開発者向けのコンテンツです。 Microsoft のトーンとスタイルを維持しながら、技術的に正確な明確な情報を説得力のある方法で提供することが重要です。

* **[ステップ バイ ステップの手順を記述します](/style-guide/procedures-instructions/writing-step-by-step-instructions)**。 適用された対話型エクスペリエンスは、開発者が Microsoft 製品とテクノロジについて学ぶのに最適な方法です。 プログレッシブ形式で複雑な手順や簡単な手順を提示する方法は、自然でユーザーフレンドリーです。

## <a name="markdown-reference"></a>MarkDown リファレンス

 Microsoft Docs ページは MarkDown 構文で記述され [、Markdig](https://github.com/lunet-io/markdig) エンジンを介して解析されます。 特定 *のタグ*[と書式設定の規則については](/contribute/markdown-reference)、「Docs Markdown リファレンス」を参照してください。

## <a name="file-paths"></a>ファイル パス

ドキュメント内のハイパーリンクの有効なファイル パスを設定すると、特に相対パスを使用して他のドキュメントセットへのリンクを作成する場合は、問題になる可能性があります。  ファイル パスが正しくないか無効GitHub場合、ビルドは成功しません。

ハイパーリンクとファイル パスの詳細については、「ドキュメントでリンクを使用[する」を参照してください](/contribute/how-to-write-links)。

>[!IMPORTANT]
> プラットフォーム ドキュメントセット *の一部* であるTeams参照するには、次のTeamsします。<br>
> &emsp;&#x2714; 先頭スラッシュを付けずに相対パスを使用します。<br>
> &emsp;&#x2714; Markdown ファイル拡張子を含めます。<br>
>Ex:  **parent directory/directory/path-to-article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Microsoft Docs ライブラリの記事を参照するには、次のプラットフォーム ドキュメントセットTeams参照してください。<br>
> &emsp;&#x2714; スラッシュで始まる相対パスを使用します。<br>
> &emsp;&#x2714;ファイル拡張子を含めることはできません。 <br> 例: **/docset/address-to-file-location —>**`[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Microsoft Docs ライブラリの外部にあるページを参照するには、GitHubパスを `https` 使用します。<br>

## <a name="code-samples-and-snippets"></a>コード サンプルとスニペット

コード サンプルは、開発者が API と SDK を正常に使用する上で重要な役割を果たします。 よく示されたコード サンプルは、説明的なテキストや指示情報だけでなく、物事の動作を明確に伝えます。 コード サンプルは、正確で簡潔で、十分に文書化され、最も重要なのは、読者に優しいコード サンプルである必要があります。 読みやすくするコードは、理解、テスト、デバッグ、保守、変更、拡張も簡単です。 *「*[ドキュメントにコードを含める方法」を参照してください](/contribute/code-in-docs)。読みやすさに関するヒントについては、「Edge : Source [Code Readability ヒント」 も参照してください](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)。

> [!div class="nextstepaction"]
> [Microsoft Docs の更新プログラムと最新のお知らせを取得する](/teamblog)
