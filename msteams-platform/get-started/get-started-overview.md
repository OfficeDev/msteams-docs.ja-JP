---
title: 概要-開始する
description: Microsoft Teams 開発者向けドキュメントの概要の概要
ms.localizationpriority: high
ms.topic: reference
keywords: Microsoft Teams 開発者向けサンプル
ms.openlocfilehash: 32f6e94e7c1773812fbdca26106dbd319cc45262
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399003"
---
# <a name="get-started"></a>概要

Microsoft Teams 用のカスタマイズされたアプリを構築して展開するための概要へようこそ。

基本的な実際の Teams アプリを構築する手順について説明します。 概要では、一般的なツール、基本的な概念、より高度な機能も紹介します。

学習のアイデアを次に示します。

- Microsoft Teams Toolkit (Visual Studio Code拡張機能) を使用すると、すぐに起動して実行できます。
- ツールキットと SDK のエクスペリエンスを取得します。
- さまざまな種類の Teams アプリを構成して構築します。

選択できるビルド環境オプションと、Teams アプリのビルドと展開のロードマップを簡単に見てみましょう。

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="Teams アプリをビルドして展開するための基本的な手順を示す図":::

## <a name="app-capabilities-and-development-tools"></a>アプリの機能と開発ツール

アプリに必要な機能に応じて、適切な開発ツール セットを選択します。

| アプリの機能 | ユーザーの操作 | 推奨されるツール | SDK | テクノロジ スタック/言語 |
|--------|-------------|--------|--------|--------|
| タブ | 全画面表示の埋め込み Web エクスペリエンス。 | Teams Toolkit 拡張機能を備えた Microsoft Visual Studio Code、または CLI を使用する場合は [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | コア ライブラリ用の [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)と、UI 機能用に[ Teams クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用する | Web テクノロジ全般、HTML、CSS、JavaScript (React を含む)。 |
| ボット | メンバーと会話するチャット ボット。 | Teams Toolkit 拡張機能を備えた Visual Studio Code、または [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) と [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java Python。 |
| メッセージング拡張機能 | 外部コンテンツを会話に挿入したり、メッセージに対してアクションを実行したりするためのショートカット。 | Teams Toolkit 拡張機能を備えた Visual Studio Code、または [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) と [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java Python。 |

*これらの特定のスタックの使用に限定されません。*

Yeoman ワークフローに既に慣れている場合は、 [YoTeams Yeoman Generator](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) を使用してアプリをビルドすることを好むかもしれません。

> [!NOTE]
> App Studio を使用している場合は、Teams アプリを構成、配布、管理するための開発者ポータルを試してみることをお勧めします。

## <a name="build-your-first-teams-app"></a>最初の Teams アプリを構築する

では、最初の Teams アプリを構築しましょう。 ただし、まず、言語 (またはフレームワーク) を選択し、開発環境を準備します。

> [!div class="nextstepaction"]
> [React](../sbs-gs-javascript.yml) を使用して JavaScript で Teams アプリを構築する
> [!div class="nextstepaction"]
> [SPFx](../sbs-gs-spfx.yml) を使用して Teams アプリを構築する
> [!div class="nextstepaction"]
> [C# または .NETを使用して Teams アプリをビルドする](../sbs-gs-csharp.yml)
> [!div class="nextstepaction"]
> [node.js を使用して Teams アプリをビルドする](../sbs-gs-nodejs.yml)

## <a name="see-also"></a>関連項目

* [Microsoft Teamsサンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples#microsoft-teams-samples)
* [Git および GitHub リソース](/contribute/additional-resources)
