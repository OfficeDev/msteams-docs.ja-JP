---
title: はじめに - 最初のアプリの概要と前提条件を構築する
author: girliemac
description: アプリ開発の開始方法Microsoft Teams、環境を設定する方法について説明します。
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565880"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>アプリ開発Microsoft Teams始める

アプリ開発の基本を学ぶ簡単なアプリTeams構築します。 "Hello, World!"が表示されたら、一般的なツール、基本的な概念、高度な機能の詳細については、他の概要記事を参照してください。



## <a name="what-youll-learn"></a>あなたが学ぶこと

* Teams Toolkit、Visual Studio Code拡張機能で迅速に起動して実行します。 
* アプリスタジオでアプリを構成します。
* 開発者ツールと SDK Teamsについて理解する。
* 認証や設計のベスト プラクティスなど、重要なTeamsアプリの概念を考慮します。

任意のテクノロジ (たとえば、コマンド ライン インターフェイス (CLI) を使用して、Teams アプリをビルドできます。 ただし、これらの記事は、次の推奨ツールとテクノロジを使用する際に役立ちます。

* Teams Toolkit、Visual Studio Code拡張
* タブのReact.js
* ボットとメッセージング拡張機能のNode.js


## <a name="teams-app-fundamentals"></a>アプリの基礎をTeamsする

カスタム Teams アプリケーションは、自分自身、組織内のユーザー、または世界中のユーザー用に構築できます。 開始する前に、アプリ開発に関する次の基本概念Teams理解する必要があります。

### <a name="common-app-use-cases"></a>一般的なアプリのユース ケース

カスタム Teams アプリが役立つ一般的なシナリオは次のとおりです。

* web アプリや Web サイトの一部などの Web ベースのコンテンツをTeams クライアントに埋め込みます。
* 別のシステムで情報をすばやく検索し、Teams会話に追加します。
* 会話で言ったことから直接ワークフローとプロセスをトリガーします。

### <a name="app-capabilities-and-tools"></a>アプリの機能とツール

アプリは、1 つ以上のTeams機能とユーザー操作ポイントで構成されます。 開発ツールセットは、必要な機能によって異なります。

| **アプリの機能**| **相互作用ポイント** | **推奨ツール** | **SDK** | **テクノロジースタック** |
|--------|--------|--------|--------|--------|
| タブ | ユーザーが、個人コンテキストおよび共有コンテキストで埋め込み Web コンテンツを操作できるスペース。 | Teams Toolkit拡張またはヨーマンジェネレータを備えたVS Code | Teams JavaScript client SDK | 一般的な Web テクノロジ (HTML、CSS、および JavaScript) またはReact.js |
| ボット | 個人コンテキストおよび共有コンテキストでユーザーと対話するチャットボット。 | Teams Toolkit拡張またはヨーマンジェネレータを備えたVS Code | ボット フレームワーク SDK | Node.js、C# または Python | 
| メッセージング拡張機能 | 会話から離れることなく、アプリコンテンツを挿入したり、メッセージに対して操作を行ったりするためのショートカット。 | Teams Toolkit拡張またはヨーマンジェネレータを備えたVS Code | ボット フレームワーク SDK | Node.js、C# または Python |

### <a name="teams-doesnt-host-your-app"></a>Teamsアプリをホストしない

ユーザーがアプリをTeamsにインストールすると、構成ファイル (アプリ マニフェストとも呼ばれます) とアプリのアイコンを含むアプリ パッケージのみがインストールされます。 アプリのロジックとデータ ストレージは、開発中に Azure Web サービスやローカル ホストなどの他の場所でホストされます。 Teams HTTPS を介してこれらのリソースにアクセスします。

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="アプリをTeamsに示す図は、クラウド サーバーでアプリ ロジックを指しています。":::

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [初めてのTeamsアプリをビルドして実行する](../build-your-first-app/build-and-run.md)
