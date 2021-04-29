---
title: 概要 - 最初のアプリの概要と前提条件を構築する
author: girliemac
description: Microsoft Teams アプリ開発を開始し、環境をセットアップする方法について説明します。
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
# <a name="get-started-with-microsoft-teams-app-development"></a>Microsoft Teams アプリ開発の開始

Teams アプリ開発の基本を学ぶ簡単なアプリを構築します。 「Hello, World!」と表示された後、一般的なツール、基本的な概念、高度な機能の詳細については、他の開始記事を試してみてください。



## <a name="what-youll-learn"></a>学習する情報

* Teams コード拡張機能である Teams ToolkitをVisual Studio実行する 
* App Studio でアプリを構成する 
* Teams 開発者ツールと SDK について理解する
* 認証や設計のベスト プラクティスなど、Teams アプリの重要な概念を検討する

コマンド ライン インターフェイス (CLI) など、任意のテクノロジを使用して Teams アプリをビルドできます。 ただし、これらの記事は、次の推奨ツールとテクノロジを使い始めるのに役立ちます。

* Teams ToolkitコードVisual Studio拡張機能
* React.jsの詳細
* Node.jsおよびメッセージング拡張機能の詳細


## <a name="teams-app-fundamentals"></a>Teams アプリの基本

自分、組織のユーザー、または世界中のユーザー用にカスタム Teams アプリを作成できます。 開始する前に、Teams アプリ開発に関する次の基本的な概念を理解する必要があります。

### <a name="common-app-use-cases"></a>アプリの一般的な使用例

カスタム Teams アプリで役立つ一般的なシナリオは次のとおりです。

* Web アプリや Web サイトの一部などの Web ベースのコンテンツを Teams クライアントに埋め込む
* 別のシステムで情報をすばやく参照し、Teams の会話に追加する 
* 会話で言ったことからワークフローとプロセスを直接トリガーする 

### <a name="app-capabilities-and-tools"></a>アプリの機能とツール

アプリは、1 つ以上の Teams 機能とユーザー操作ポイントで構成されます。 開発ツールセットは、必要な機能によって異なります。

| **アプリの機能**| **対話ポイント** | **推奨されるツール** | **SDK** | **テクノロジ スタック** |
|--------|--------|--------|--------|--------|
| タブ | ユーザーが個人用および共有コンテキストで埋め込み Web コンテンツを操作できるスペース | Vs Code with Teams Toolkitまたは Yeoman Generator | Teams JavaScript client SDK | 一般的な Web テクノロジ (HTML、CSS、JavaScript) または React.js |
| ボット | 個人と共有のコンテキストでユーザーと対話するチャットボット | Vs Code with Teams Toolkitまたは Yeoman Generator | Bot Franework SDK | Node.js、C#、または Python | 
| メッセージング拡張機能 | 会話から離れることなく、アプリ コンテンツを挿入したり、メッセージに対して操作したりするためのショートカット | Vs Code with Teams Toolkitまたは Yeoman Generator | Bot Framework SDK | Node.js、C#、または Python |

### <a name="teams-doesnt-host-your-app"></a>Teams がアプリをホストしない

ユーザーが Teams にアプリをインストールする場合、構成ファイル (アプリ マニフェストとも呼ばれる) とアプリのアイコンを含むアプリ パッケージのみをインストールします。 アプリのロジックとデータ ストレージは、開発中に Azure Web Services や localhost など、他の場所でホストされます。 Teams は HTTPS を介してこれらのリソースにアクセスします。

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Teams でアプリを示す図は、クラウド サーバー内のアプリ ロジックを指しています。":::

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [最初の Teams アプリをビルドして実行する](../build-your-first-app/build-and-run.md)
