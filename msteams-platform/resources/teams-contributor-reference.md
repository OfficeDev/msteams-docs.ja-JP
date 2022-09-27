---
title: Teams ドキュメントに投稿する
description: Teams ドキュメントの作成と発行の手順について説明します
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 4a0c522b5e9d4bcf99ee884de41b1d75846b004a
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044666"
---
# <a name="contribute-to-teams-documentation"></a>Teams ドキュメントに投稿する

Teams のドキュメントは、 **Microsoft Learn** テクニカル ドキュメント ライブラリの一部です。 コンテンツは、ドキュメントセットと呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。 同じドキュメントセット内のアーティクルの URL パスの拡張子は 、次の場合 `learn.microsoft.com`と同じです。 たとえば、 `/learn.microsoft.com/microsoftteams/...` Teams docset ファイル パスの先頭です。 Teams の記事は Markdown 構文で記述され、GitHub でホストされています。

## <a name="set-up-your-workspace"></a>ワークスペースを設定する

> [!div class="checklist"]
>
> * [Git をインストールします](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。
> * [Microsoft Visual Studio Code](https://code.visualstudio.com/) (VS Code) をインストールします。
> * VS Code Marketplace から [直接 Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) をインストールします。
<br>&emsp;&emsp; または
> [!div class="checklist"]
>
> * VS Code 内にインストールする:

   1. サイド アクティビティ バーの **[拡張機能] アイコン** を選択するか、[ **表示 ] = [拡張機能の>** ] コマンドまたは Ctrl + Shift + X キーを押して、 **Docs Authoring Pack を検索します**。
   1. [**インストール**] を選択します。
   1. インストール後、[ **インストール** ] は [ **管理** ] 歯車ボタンに変更されます。

## <a name="review-the-microsoft-docs-contributor-guide"></a>Microsoft Docs共同作成者ガイドを確認する

共同作成者ガイドでは、 **Microsoft Learn** プラットフォームで技術コンテンツを作成、発行、更新する方向を提供します。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft の書き込み、スタイル、およびコンテンツ ガイド

* **[Microsoft ライティング スタイル ガイド](/style-guide/welcome)**: Microsoft ライティング スタイル ガイドは、テクニカル ライティングのための包括的なリソースであり、Microsoft の音声とスタイルに対する最新のアプローチを反映しています。 簡単に参照するには、ブラウザー **の [お気に入り** ] メニューにこのオンライン ガイドを追加します。

* **[開発者向けコンテンツの作成](/style-guide/developer-content/)**: Teams 固有のコンテンツは、プログラミングの概念とプロセスの基本的な理解を持つ開発者向けコンテンツです。 Microsoft のトーンとスタイルを維持しながら、説得力のある方法で明確で技術的に正確な情報を提供することが重要です。

* **[ステップ バイ ステップの手順を記述する](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: 適用された対話型のエクスペリエンスは、開発者が Microsoft 製品とテクノロジについて学ぶのに最適な方法です。 複雑なプロシージャまたは単純なプロシージャをプログレッシブ形式で表示することは、自然で使いやすい方法です。

## <a name="markdown-reference"></a>MarkDown リファレンス

**Microsoft Learn** ページは **MarkDown** 構文で記述され、 [Markdig](https://github.com/lunet-io/markdig) エンジンを介して解析されます。 特定のタグと書式設定規則の詳細については、「 [Docs Markdown リファレンス」を参照してください](/contribute/markdown-reference)。

## <a name="file-paths"></a>ファイル パス

相対パスを使用し、他のドキュメントセットへのリンクを作成する場合は、ドキュメント内のハイパーリンクの有効なファイル パスを設定することが重要です。 GitHub でビルドが成功するのは、ファイル パスが正しいか有効な場合のみです。

ハイパーリンクとファイル パスの詳細については、 [ドキュメントのリンクを参照してください](/contribute/how-to-write-links)。

> [!IMPORTANT]
> Teams プラットフォームドキュメントセット **の一部** である記事を参照するには:<br>
> &emsp;&#x2714; 前にスラッシュを付けずに相対パスを使用します。<br>
> &emsp;&#x2714; Markdown ファイル拡張子を含めます。<br>
>例:  **親ディレクトリ/ディレクトリ/path-to-article.md** —> [Microsoft Teams 用のアプリを構築する](../concepts/building-an-app.md) <br><br>
> Teams プラットフォーム のドキュメントセットの **一部ではない** Microsoft Learn の記事を参照するには、次の手順を実行します。<br>
> &emsp;&#x2714; スラッシュで始まる相対パスを使用します。<br>
> &emsp;&#x2714; ファイル拡張子を含めないでください。 <br>
> 例: **/docset/address-to-file-location** —> [Microsoft Graph APIを使用して Microsoft Teams と連携する](/graph/api/resources/teams-api-overview)<br><br>
> GitHub などの Microsoft Learn の外部のページを参照するには、完全な `https` ファイル パスを使用します。<br>

## <a name="code-samples-and-snippets"></a>コード サンプルとスニペット

コード サンプルは、API と SDK を効果的に使用するために重要な役割を果たします。 よく示されたコード サンプルは、説明的なテキストや指示情報だけでなく、物事がどのように動作するかを明確に伝えることができます。 コード サンプルは、正確で簡潔で、十分に文書化され、リーダーフレンドリである必要があります。 読みやすいコードは、理解しやすく、テスト、デバッグ、保守、変更、拡張が容易である必要があります。 詳細については、 [記事にコードを含める方法を](/contribute/code-in-docs)参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Microsoft Learn の更新プログラムと最新のお知らせを入手する](/teamblog)

## <a name="see-also"></a>関連項目

* [Microsoft Learn](/)
* [Microsoft Learn ドキュメント共同作成者ガイド](/contribute)
* [Microsoft Learn のスタイルと音声のクイック スタート](/contribute/style-quick-start)
* [最先端: ソース コードの読みやすさに関するヒント](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teams のドキュメント](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
