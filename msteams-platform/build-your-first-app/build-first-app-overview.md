---
title: 概要 - 最初のアプリの概要と前提条件を構築する
author: girliemac
description: アプリの開発を開始しMicrosoft Teams環境をセットアップする方法について学習します。
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: 3bc99c535ea659f046b65dc26d9a60de0dd49cab
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068572"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>アプリ開発Microsoft Teams開始する

シンプルなアプリを構築して、アプリ開発の基本Teams学ぶ。 「Hello, World!」と表示された後、一般的なツール、基本的な概念、高度な機能の詳細については、他の開始記事を試してみてください。



## <a name="what-youll-learn"></a>学習する情報

* 新しい拡張機能である Teams Toolkitを使用してVisual Studio Code実行する 
* App Studio でアプリを構成する 
* 開発者向けツールTeams SDK について理解する
* 認証やTeamsなど、アプリの概念に関する重要な点を検討する

コマンド ライン インターフェイスTeamsなど、任意のテクノロジを使用してアプリをビルドできます。 ただし、これらの記事は、次の推奨ツールとテクノロジを使い始めるのに役立ちます。

* Teams Toolkit、Visual Studio Code拡張子
* React.jsの詳細
* Node.jsおよびメッセージング拡張機能の詳細


## <a name="teams-app-fundamentals"></a>Teamsアプリの基本

自分、組織Teams、世界中のユーザー向けカスタム アプリを作成できます。 開始する前に、アプリ開発に関する次の基本的なTeams理解する必要があります。

### <a name="common-app-use-cases"></a>アプリの一般的な使用例

カスタム アプリで役立つ一Teamsシナリオは次のとおりです。

* Web アプリや Web サイトの一部などの Web ベースのコンテンツをクライアントに埋め込Teamsする
* 別のシステムで情報をすばやく参照し、その情報を別のTeamsする 
* 会話で言ったことからワークフローとプロセスを直接トリガーする 

### <a name="app-capabilities-and-tools"></a>アプリの機能とツール

アプリは、1 つ以上の機能とユーザー Teamsポイントで構成されます。 開発ツールセットは、必要な機能によって異なります。

| **アプリの機能**| **対話ポイント** | **推奨されるツール** | **SDK** | **テクノロジ スタック** |
|--------|--------|--------|--------|--------|
| タブ | ユーザーが個人用および共有コンテキストで埋め込み Web コンテンツを操作できるスペース | VS Code拡張子Teams Toolkit Yeoman Generator | Teams JavaScript client SDK | 一般的な Web テクノロジ (HTML、CSS、JavaScript) または React.js |
| ボット | 個人と共有のコンテキストでユーザーと対話するチャットボット | VS Code拡張子Teams Toolkit Yeoman Generator | Bot Franework SDK | Node.js、C#、または Python | 
| メッセージング拡張機能 | 会話から離れることなく、アプリ コンテンツを挿入したり、メッセージに対して操作したりするためのショートカット | VS Code拡張子Teams Toolkit Yeoman Generator | Bot Framework SDK | Node.js、C#、または Python |

### <a name="teams-doesnt-host-your-app"></a>Teamsアプリをホストしない

ユーザーがアプリを Teams にインストールすると、構成ファイル (アプリ マニフェストとも呼ばれる) とアプリのアイコンを含むアプリ パッケージだけがインストールされます。 アプリのロジックとデータ ストレージは、開発中に Azure Web Services や localhost など、他の場所でホストされます。 Teams HTTPS 経由でこれらのリソースにアクセスします。

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="クラウド サーバーでアプリ ロジックTeams示すアプリを示す図。":::

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [最初のアプリをビルドしてTeamsする](../build-your-first-app/build-and-run.md)
