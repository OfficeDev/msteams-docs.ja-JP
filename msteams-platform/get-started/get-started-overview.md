---
title: 概要 - 概要
description: 開発者向けドキュメントの概要Microsoft Teams概要
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teamsサンプル
ms.openlocfilehash: ee986f04ca760fbf9090f7dda94e1378261db7df
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075480"
---
# <a name="get-started"></a>開始する

カスタマイズされたアプリの構築と展開を開始する方法について、Microsoft Teams!

手順を実行して、基本的な実際のアプリをTeamsします。 Get started では、一般的なツール、基本的な概念、より高度な機能も紹介します。

次に、学習する情報を示します。

- アプリ (拡張機能) を使用してMicrosoft Teams ToolkitをVisual Studio Codeします。
- アプリと SDK のToolkit取得します。
- さまざまな種類のアプリを構成Teamsします。

選択できるビルド環境のオプションと、アプリの構築と展開へのロード マップを簡単にTeamsしましょう。

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="アプリをビルドして展開するための基本的な手順を示Teams図。":::

## <a name="app-capabilities-and-development-tools"></a>アプリの機能と開発ツール

アプリに必要な機能に応じて、適切な開発ツール セットを選択します。

| アプリの機能 | ユーザーの操作 | 推奨されるツール | SDK | テクノロジ スタック /言語 |
|--------|-------------|--------|--------|--------|
| タブ | フルスクリーンの埋め込み Web エクスペリエンス。 | VS Code拡張子Teams Toolkit使用する場合は[TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)を使用する | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) for core libs および ui Teams[クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) | Web テクノロジ全般、HTML、CSS、JavaScript (React)。 |
| ボット | メンバーと会話するチャット ボット。 | VS Code拡張機能Teams Toolkit [TeamsFx CLI を使用する](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) と [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java Python。 |
| メッセージング拡張機能 | 会話に外部コンテンツを挿入したり、メッセージに対してアクションを実行したりするショートカット。 | VS Code拡張機能Teams Toolkit [TeamsFx CLI を使用する](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) と [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java Python。 |

*これらの特定のスタックの使用に限定されるのではありません。*

Yeoman ワークフローを既に理解している場合は [、YoTeams Yeoman Generator](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) を使用してアプリをビルドする方が好きです。

> [!NOTE]
> App Studio を使用している場合は、開発者ポータルを試して、アプリの構成、配布、管理Teams勧めします。


## <a name="build-your-first-teams-app"></a>最初のアプリをTeamsする

次に、最初のアプリをTeamsします。 ただし、まず言語 (またはフレームワーク) を選び、開発環境を準備します。

> [!div class="nextstepaction"]
> [JavaScript を使用Teamsアプリをビルドするには、次のReact](../sbs-gs-javascript.yml)

> [!div class="nextstepaction"]
> [アプリを使用TeamsアプリをSPFx](../sbs-gs-spfx.yml)

> [!div class="nextstepaction"]
> [アプリまたは .NET Teamsを使用C#アプリを構築する](../sbs-gs-csharp.yml)

> [!div class="nextstepaction"]
> [アプリを使用TeamsアプリをNode.js](../sbs-gs-nodejs.yml)
