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
# <a name="contributing-to-microsoft-teams-documentation"></a>Microsoft Teamsドキュメントへの貢献

[Teams ドキュメント](/microsoftteams/platform/overview)は[、Microsoft Docs](https://docs.microsoft.com/)テクニカル ドキュメント ライブラリの一部です。 コンテンツは docsets と呼ばれるグループに編成され、それぞれが 1 つのエンティティとして管理される関連ドキュメントのグループを表します。 同じドキュメントセット内のアーティクルは *、ドキュメント <span></span> .microsoft.com* の後に同じ URL パス拡張子を持ちます。  たとえば `/docs.microsoft.com/microsoftteams/...` 、docset ファイルパスの先頭Teams。 Teams記事は[MarkDown](#markdown-reference)構文で記述され[、GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)でホストされます。

## <a name="set-up-your-workspace"></a>ワークスペースを設定する

> [!div class="checklist"]
>
> * [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)をインストールします。
> * [Visual Studio Code](https://code.visualstudio.com/) (VS Code) をインストールします。
> * [ドキュメントオーサリングパックを](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack)VS Codeマーケットプレースから直接インストールします。
<br>&emsp;&emsp; 又は

> [!div class="checklist"]
>
> * VS Code内からインストールする:

   1. サイドアクティビティバーの **[拡張機能]アイコン** を選択するか、[ **表示 =>拡張** ]コマンド(Ctrl +Shift+X)を使用して *ドキュメントオーサリングパック* (Microsoft)を検索します。
   1. [ **インストール** ] ボタンを選択します。
   1. インストールが完了すると、[ **インストール** ]ボタンが[歯車の **管理** ]ボタンに変わります。

## <a name="review-the-microsoft-docs-contributors-guide"></a>マイクロソフト ドキュメント寄稿者ガイドを確認する

[寄稿者ガイド](/contribute)では、Microsoft Docs プラットフォーム上での技術的なコンテンツの作成、公開、および更新の手順を示します。

## <a name="microsoft-writing-style-and-content-guides"></a>マイクロソフトライティングガイド、スタイルガイド、コンテンツガイド

* **[マイクロソフトライティングスタイルガイド](/style-guide/welcome)**. このオンライン ガイドをブラウザ **のお気に入り** メニューに追加することを検討してください。 これは、今日の技術的な執筆のための包括的なリソースであり、音声とスタイルに対するマイクロソフトの現代的なアプローチを反映しています。

* **[開発者コンテンツの作成](/style-guide/developer-content/)**: Teams固有のコンテンツは、プログラミングの概念とプロセスを基本的に理解している開発者の対象読者を対象としています。 マイクロソフトのトーンとスタイルを維持しながら、明確で技術的に正確な情報を説得力のある方法で提供することが重要です。

* **[ステップバイステップの手順を書く](/style-guide/procedures-instructions/writing-step-by-step-instructions)**. 開発者が Microsoft 製品やテクノロジについて理解するには、応用エクスペリエンスと対話型エクスペリエンスを使用できます。 複雑なプロシージャや単純なプロシージャをプログレッシブ形式で提示するのは自然で、ユーザーフレンドリーです。

## <a name="markdown-reference"></a>マークダウン リファレンス

 マイクロソフトドキュメントページは、マークダウン構文で記述され、 [マークディグ](https://github.com/lunet-io/markdig) エンジンを介して解析されます。 特定のタグと書式規則 *については*[、ドキュメントマークダウンのリファレンス](/contribute/markdown-reference)を参照してください。

## <a name="file-paths"></a>ファイル パス

特に、相対パスを使用して他のドキュメントセットへのリンクを作成する場合は、ドキュメント内のハイパーリンクに有効なファイル パスを設定するのが難しい場合があります。  ファイル パスが正しくない場合や無効な場合、ビルドはGitHubで成功しません。

ハイパーリンクとファイル パスの詳細については、 [ドキュメントのリンクを使用するを参照してください](/contribute/how-to-write-links)。

>[!IMPORTANT]
> Teamsプラットフォームの docset *の一部* である記事を参照するには、次の手順を実行します。<br>
> &emsp;&#x2714;先頭のスラッシュを付けずに相対パスを使用します。<br>
> &emsp;&#x2714; マークダウン ファイル拡張子を含めます。<br>
>Ex:  **親ディレクトリ/ディレクトリ/パスから article.md へ** -> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Teams プラットフォームのドキュメントセットに *含まれていない* Microsoft Docs ライブラリの記事を参照するには、次の手順を実行します。<br>
> &emsp;&#x2714; スラッシュで始まる相対パスを使用します。<br>
> &emsp;&#x2714; ファイル拡張子を含まない <br> 指定する場所:  **/docset/アドレスからファイルへの場所** -> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> GitHubなどの Microsoft Docs ライブラリの外部にあるページを参照するには、完全 `https` なファイル パスを使用します。<br>

## <a name="code-samples-and-snippets"></a>コード サンプルとスニペット

コード サンプルは、開発者が API と SDK を正常に使用するうえで重要な役割を果たします。 適切に提示されたコード サンプルは、説明テキストや説明情報よりも、物事の動作を明確に伝えることができます。 コード サンプルは、正確で簡潔で、十分に文書化されていて、最も重要なのは読者に優しい必要があります。 読みやすいコードは、理解、テスト、デバッグ、保守、変更、拡張も簡単です。 詳細については、「 [docs にコードを含める方法](/contribute/code-in-docs)」を参照してください。

## <a name="see-also"></a>関連項目

* [ドキュメントスタイルと音声クイックスタート](/contribute/style-quick-start)
* [最先端: ソースコードの読みやすヒント。](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)

> [!div class="nextstepaction"]
> [マイクロソフト ドキュメントの更新プログラムと最新のお知らせを入手する](/teamblog)
