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
# <a name="contributing-to-microsoft-teams-documentation"></a>Microsoft Teams ドキュメントへの投稿

[Teams ドキュメント](/microsoftteams/platform/overview)は、 [Microsoft Docs](https://docs.microsoft.com/)技術ドキュメントライブラリに含まれています。 コンテンツは、docsets と呼ばれるグループに整理され、それぞれが1つのエンティティとして管理する関連ドキュメントのグループを表します。 同じ docset の記事には、 * <span></span> microsoft.com*の後に同じ URL パス拡張があります。  たとえば、 `/docs.microsoft.com/microsoftteams/...` は Teams docset ファイルパスの先頭です。 Teams の記事は[MarkDown](#markdown-reference)構文で記述され、 [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)でホストされます。

## <a name="set-up-your-workspace"></a>ワークスペースの設定

> [!div class="checklist"]
>
> * [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)をインストールします。
> * [Visual Studio code](https://code.visualstudio.com/) (VS コード) をインストールします。
> * [ドキュメント作成パック](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)を VS Code Marketplace から直接インストールする
<br>&emsp;&emsp;や

> [!div class="checklist"]
>
> * VS Code 内からのインストール:

   1. サイドアクティビティバーで [ **extensions] アイコン**を選択するか、[**表示 => extensions** ] コマンド (Ctrl + Shift + X) を使用して、 *Docs Authoring Pack* (Microsoft) を検索します。
   1. [**インストール**] ボタンを選択します。
   1. インストールが完了すると、[**インストール**] ボタンが [歯車の**管理**] ボタンに変わります。

## <a name="review-the-microsoft-docs-contributors-guide"></a>Microsoft Docs コントリビューターガイドを確認する

[投稿者ガイド](/contribute)は、Microsoft/docの技術的なコンテンツを作成、発行、更新するための指示を提供します。「 [Docs Style」および「voice quick Start](/contribute/style-quick-start) *」も参照してください*。

## <a name="microsoft-writing-style-and-content-guides"></a>Microsoft の書き方、スタイル、およびコンテンツガイド

* **[Microsoft の書き方のスタイルガイド](/style-guide/welcome)** です。 このオンラインガイドをブラウザーの [**お気に入り**] メニューに追加することを検討してください。 これは、今日の技術的な執筆に関する包括的なリソースであり、音声とスタイルに対する Microsoft の先進のアプローチを反映しています。

* **[開発者向けコンテンツを書く](/style-guide/developer-content/)**。 Teams 固有のコンテンツは、プログラミングの概念とプロセスについて基本的に理解している開発者を対象としています。 Microsoft の語調とスタイルを維持しながら、わかりやすく技術的に正確な情報を提供することが重要です。

* ステップ**[ごとの指示を記述](/style-guide/procedures-instructions/writing-step-by-step-instructions)** します。 適用された対話的なエクスペリエンスは、開発者が Microsoft の製品とテクノロジについて理解するのに便利な方法です。 複雑な手順や単純な手順をプログレッシブ形式で表現することは、自然でわかりやすいものです。

## <a name="markdown-reference"></a>MarkDown リファレンス

 Microsoft Docs ページは、MarkDown 構文で記述され、 [Markdig](https://github.com/lunet-io/markdig)エンジンで解析されます。 特定のタグと書式設定規則については、 *「* [Docs Markdown reference](/contribute/markdown-reference) 」を参照してください。

## <a name="file-paths"></a>ファイルパス

ドキュメントでハイパーリンクに有効なファイルパスを設定することは、特に相対パスを使用して他の docsets へのリンクを作成する場合には、課題になることがあります。  ファイルパスが正しくないか、無効な場合は、GitHub でのビルドは成功しません。

ハイパーリンクとファイルパスの詳細については、 *「* [ドキュメントでのリンクの使用](/contribute/how-to-write-links)」を参照してください。

>[!IMPORTANT]
> Teams のプラットフォーム docset*の一部*である記事を参照するには、次の手順を実行します。<br>
> &emsp;&#x2714; には、スラッシュを先頭に付けずに相対パスを使用します。<br>
> &emsp;Markdown ファイル拡張子が含まれている&#x2714;。<br>
>Ex:**親ディレクトリ/ディレクトリ/パス名**: >`[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> <https://docs.microsoft.com/>Teams のプラットフォーム docset に含まれて*いない*Microsoft Docs library () の記事を参照するには、次の手順を実行します。<br>
> &emsp;&#x2714; スラッシュで始まる相対パスを使用します。<br>
> &emsp;&#x2714; ファイル拡張子は含めないでください。 <br> Ex: **/docset/addressofflocation** — >`[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`
>

## <a name="code-samples-and-snippets"></a>コードサンプルとスニペット

コードサンプルは、開発者が Api と Sdk を正常に使用するのに役立つ重要な役割を果たします。 適切に表示されているコードサンプルは、説明テキストと説明情報だけではなく、どのように機能するかを伝えることができます。 コードサンプルは正確で簡潔で、ドキュメント化されている必要があります。また、最も重要なのは閲覧者フレンドリです。 読みやすいコードも理解しやすく、テスト、デバッグ、保守、変更、拡張が簡単です。 *「* [ドキュメントにコードを含める方法」を](/contribute/code-in-docs)参照してください。読みやすさのヒントについては、「[切削エッジ: ソースコードの読みやすさのヒント](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips) *」も参照*してください。

> [!div class="nextstepaction"]
> [Microsoft Docs の更新プログラムと最新のアナウンスを入手する](/teamblog)
