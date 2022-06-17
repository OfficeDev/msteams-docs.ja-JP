---
title: Teams ドキュメントに投稿する
description: Teamsドキュメントの作成と発行の手順について説明します
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 165f5df18395d329aa2f383d2f07e6f7ff3afdcf
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143082"
---
# <a name="contribute-to-teams-documentation"></a>Teams ドキュメントに投稿する

Teamsドキュメントは、**Microsoft Docs** 技術ドキュメント ライブラリの一部です。 コンテンツは、ドキュメントセットと呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。 同じドキュメント セット内のアーティクルは **、docs.microsoft.com** 後に同じ URL パス拡張機能を持ちます。 たとえば、 `/docs.microsoft.com/microsoftteams/...` Teams docset ファイル パスの先頭です。 Teamsアーティクルは Markdown 構文で記述され、GitHubでホストされています。

## <a name="set-up-your-workspace"></a>ワークスペースを設定する

> [!div class="checklist"]
>
> * [Git をインストールします](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * [Microsoft Visual Studio コード](https://code.visualstudio.com/) (VS Code) をインストールします。
> * VS Code Marketplace から[直接 Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) をインストールします。
<br>&emsp;&emsp; または
> [!div class="checklist"]
>
> * VS Code内にインストールします。

   1. サイド アクティビティ バーの **[拡張機能] アイコン** を選択するか、[**表示 =>拡張機能**] コマンドまたは Ctrl + Shift + X キーを押して、**Microsoft Docs作成パックを検索します**。
   1. [**インストール**] を選択します。
   1. インストール後、[ **インストール** ] は [ **管理** ] 歯車ボタンに変更されます。

## <a name="review-the-microsoft-docs-contributors-guide"></a>Microsoft Docs共同作成者ガイドを確認する

共同作成者ガイドでは、**Microsoft Docs** プラットフォームで技術コンテンツを作成、発行、更新する方向を提供します。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft の書き込み、スタイル、およびコンテンツ ガイド

* **[Microsoft ライティング スタイル ガイド](/style-guide/welcome)**: Microsoft ライティング スタイル ガイドは、テクニカル ライティングのための包括的なリソースであり、Microsoft の音声とスタイルに対する最新のアプローチを反映しています。 簡単に参照するには、ブラウザー **の [お気に入り** ] メニューにこのオンライン ガイドを追加します。

* **[開発者向けコンテンツの作成](/style-guide/developer-content/)**: Teams特定のコンテンツは、プログラミングの概念とプロセスの基本的な理解を持つ開発者向けコンテンツです。 Microsoft のトーンとスタイルを維持しながら、説得力のある方法で明確で技術的に正確な情報を提供することが重要です。

* **[ステップ バイ ステップの手順を記述する](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: 適用された対話型のエクスペリエンスは、開発者が Microsoft 製品とテクノロジについて学ぶのに最適な方法です。 複雑なプロシージャまたは単純なプロシージャをプログレッシブ形式で表示することは、自然で使いやすい方法です。

## <a name="markdown-reference"></a>MarkDown リファレンス

**Microsoft Docs** ページは **MarkDown** 構文で記述され、[Markdig](https://github.com/lunet-io/markdig) エンジンを使用して解析されます。 特定のタグと書式設定規則の詳細については、「 [Docs Markdown リファレンス」を参照してください](/contribute/markdown-reference)。

## <a name="file-paths"></a>ファイル パス

相対パスを使用し、他のドキュメントセットへのリンクを作成する場合は、ドキュメント内のハイパーリンクの有効なファイル パスを設定することが重要です。 ビルドは、ファイル パスが正しいか有効な場合にのみGitHubで成功します。

ハイパーリンクとファイル パスの詳細については、 [ドキュメントのリンクを参照してください](/contribute/how-to-write-links)。

> [!IMPORTANT]
> Teams プラットフォームドキュメントセット **の一部** である記事を参照するには:<br>
> &emsp;&#x2714; 前にスラッシュを付けずに相対パスを使用します。<br>
> &emsp;&#x2714; Markdown ファイル拡張子を含めます。<br>
>例: **親ディレクトリ/ディレクトリ/path-to-article.md** —> [Microsoft Teams用のアプリをビルドする](../concepts/building-an-app.md) <br><br>
> Teams プラットフォームドキュメントセットの **一部ではない** Microsoft Docs ライブラリの記事を参照するには:<br>
> &emsp;&#x2714; スラッシュで始まる相対パスを使用します。<br>
> &emsp;&#x2714; ファイル拡張子を含めないでください。 <br>
> 例: **/docset/address-to-file-location** —> [Microsoft Graph APIを使用してMicrosoft Teamsを操作する](/graph/api/resources/teams-api-overview)<br><br>
> GitHubなど、Microsoft Docs ライブラリの外部にあるページを参照するには、完全な`https`ファイル パスを使用します。<br>

## <a name="code-samples-and-snippets"></a>コード サンプルとスニペット

コード サンプルは、API と SDK を効果的に使用するために重要な役割を果たします。 よく示されたコード サンプルは、説明的なテキストや指示情報だけでなく、物事がどのように動作するかを明確に伝えることができます。 コード サンプルは、正確で簡潔で、十分に文書化され、リーダーフレンドリである必要があります。 読みやすいコードは、理解しやすく、テスト、デバッグ、保守、変更、拡張が容易である必要があります。 詳細については、 [ドキュメントにコードを含める方法に関するページを参照](/contribute/code-in-docs)してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Microsoft Docs更新プログラムと最新のお知らせを取得する](/teamblog)

## <a name="see-also"></a>関連項目

* [Microsoft Docs](/)
* [共同作成者ガイド](/contribute)
* [ドキュメント スタイルと音声クイック スタート](/contribute/style-quick-start)
* [最先端: ソース コードの読みやすさに関するヒント](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teamsドキュメント](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
