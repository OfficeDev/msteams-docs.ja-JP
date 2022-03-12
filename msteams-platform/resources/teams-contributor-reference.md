---
title: Teams ドキュメントに投稿する
description: ドキュメントの作成と発行Teams手順
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 10c7bbf952311dd1668a3fa1b013228d9dd58000
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453118"
---
# <a name="contribute-to-teams-documentation"></a>Teams ドキュメントに投稿する

Teamsドキュメントは、Microsoft Docs のテクニカル ドキュメント **ライブラリの** 一部です。 コンテンツは docsets と呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。 同じドキュメントセット内の記事の URL パスの拡張子は、同じ **docs.microsoft.com。** たとえば、ドキュメント`/docs.microsoft.com/microsoftteams/...`セット ファイル パスの先頭Teamsです。 Teams記事は Markdown 構文で記述され、この構文でホストGitHub。

## <a name="set-up-your-workspace"></a>ワークスペースのセットアップ

> [!div class="checklist"]
>
> * [Git をインストールします](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * コード [(Microsoft Visual Studio)](https://code.visualstudio.com/) をインストールVS Code。
> * ドキュメント[オーサリング パックを、](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)VS Code Marketplace から直接インストールします。
<br>&emsp;&emsp; または
> [!div class="checklist"]
>
> * 次の手順でインストールVS Code。

   1. サイド アクティビティ **バーの [** 拡張機能] アイコンを選択するか、[表示 **] =>** [拡張機能] コマンドまたは [Ctrl+ Shift+ X] を使用して **、Microsoft Docs Authoring Pack を検索します**。
   1. [**インストール**] を選択します。
   1. インストール後、[インストール] **が [** 歯車の管理] **ボタンに** 変わります。

## <a name="review-the-microsoft-docs-contributors-guide"></a>Microsoft Docs コントリビューター ガイドを確認する

投稿者ガイドでは、Microsoft Docs プラットフォームで技術的なコンテンツを作成、発行、更新 **する方向を示** します。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft ライティング、スタイル、およびコンテンツ ガイド

* **[Microsoft Writing Style Guide](/style-guide/welcome)**: Microsoft Writing Style Guide は、テクニカル ライティングの包括的なリソースであり、音声とスタイルに対する Microsoft の最新のアプローチを反映しています。 簡単に参照するには、ブラウザーの [お気に入り] メニューにこのオンライン **ガイドを追加** します。

* **[開発者向けコンテンツ](/style-guide/developer-content/)** の作成: Teams特定のコンテンツの作成は、プログラミングの概念とプロセスに関する基本的な理解を持つ開発者対象ユーザーを対象とします。 Microsoft のトーンとスタイルを維持しながら、明確で技術的に正確な情報を説得力のある方法で提供することが重要です。

* **[ステップ バイ ステップの](/style-guide/procedures-instructions/writing-step-by-step-instructions)** 手順を記述する: 適用された対話型エクスペリエンスは、開発者が Microsoft 製品とテクノロジについて学ぶのに最適な方法です。 プログレッシブ形式で複雑な手順や簡単な手順を提示する場合は、自然でユーザーフレンドリーです。

## <a name="markdown-reference"></a>MarkDown リファレンス

**Microsoft Docs** ページは **MarkDown 構文で記述され** 、 [Markdig](https://github.com/lunet-io/markdig) エンジンを介して解析されます。 特定のタグと書式設定の規則の詳細については、「 [Docs Markdown リファレンス」を参照してください](/contribute/markdown-reference)。

## <a name="file-paths"></a>ファイル パス

相対パスを使用して他のドキュメントセットへのリンクを作成する場合は、ドキュメント内のハイパーリンクの有効なファイル パスを設定することが重要です。 ビルドは、ファイル パスGitHubまたは有効な場合にのみ、ビルドが成功します。

ハイパーリンクとファイル パスの詳細については、ドキュメントのリンク [を使用するを参照してください](/contribute/how-to-write-links)。

> [!IMPORTANT]
> プラットフォーム ドキュメントセットの一部である **記事Teams参照** するには、次のTeams使用します。<br>
> &emsp;&#x2714; 先頭スラッシュを使用せずに相対パスを使用します。<br>
> &emsp;&#x2714; Markdown ファイル拡張子を含めます。<br>
>Ex: **parent directory/directory/path-to-article.md** —> アプリの構築 [Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Microsoft Docs ライブラリの記事を参照するには、次のプラットフォーム ドキュメントセットTeams参照してください。<br>
> &emsp;&#x2714; スラッシュで始まる相対パスを使用します。<br>
> &emsp;&#x2714;ファイル拡張子を含めることはできません。 <br>
> 例: **/docset/address-to-file-location** —> [Microsoft Graph API](/graph/api/resources/teams-api-overview) を使用してファイルをMicrosoft Teams<br><br>
> Microsoft Docs ライブラリの外部にあるページを参照するには、GitHubパスを使用`https`します。<br>

## <a name="code-samples-and-snippets"></a>コード サンプルとスニペット

コード サンプルは、API と SDK を効果的に使用する重要な役割を果たします。 よく提示されたコード サンプルは、説明的なテキストや指示情報だけでなく、物事の動作を明確に伝えます。 コード サンプルは、正確で簡潔で、十分に文書化され、読者に優しい必要があります。 読みやすくするコードは、理解、テスト、デバッグ、保守、変更、拡張が容易である必要があります。 詳細については、「ドキュメントに [コードを含める方法」を参照してください](/contribute/code-in-docs)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Microsoft Docs の更新プログラムと最新のお知らせを取得する](/teamblog)

## <a name="see-also"></a>関連項目

* [Microsoft Docs](/)
* [投稿者ガイド](/contribute)
* [ドキュメント スタイルと音声クイック スタート](/contribute/style-quick-start)
* [最先端: ソース コードの読みやすさのヒント](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teamsドキュメント](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
