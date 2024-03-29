---
title: 概要-開始する
description: 作業を開始します。 言語 (Node.js、C#、Java、Python) と開発環境に基づいて初めての Microsoft Teams アプリを構築し、アプリの機能、SDK を理解します。
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: 4ad64240c97ab11da6a999f87621fdff6d70ebe2
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100435"
---
# <a name="get-started"></a>概要

Microsoft Teams 用のカスタマイズ アプリの構築・展開にあたり、概要にようこそ!

基本的な、実際の Teams アプリをビルドする手順について説明します。 概要では、一般的なツール、基本的な概念、より高度な機能も紹介します。

次のようなことを学習できます。

- Microsoft Teams Toolkit (Visual Studio Code 拡張機能）を利用して素早く起動・実行。
- ツールキットと SDK のエクスペリエンス。
- さまざまな種類の Teams アプリの設定・ビルド。

選択できるビルド環境オプションと、Teams アプリのビルドと展開のロードマップを簡単に見てみましょう。

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="Teams アプリをビルドして展開するための基本的な手順を示す図":::

## <a name="app-capabilities-and-development-tools"></a>アプリの機能と開発ツール

アプリに必要な機能に応じて、適切な開発ツール セットを選択します。

| アプリの機能 | ユーザーの操作 | 推奨されるツール | SDK | テクノロジー スタック/言語 |
|--------|-------------|--------|--------|--------|
| タブ | 全画面表示の埋め込み Web エクスペリエンス | Teams Toolkit 拡張機能を備えた Microsoft Visual Studio Code、または CLI を使用する場合は [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | コア ライブラリ用の [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)と、UI 機能用に[ Teams クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を使用する | Web テクノロジー全般、HTML、CSS、JavaScript (React を含む)。 |
| ボット | メンバーと会話するチャット ボット。 | Teams Toolkit 拡張機能を備えた Visual Studio Code、または [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) と [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java、Python。 |
| メッセージの拡張機能 | 外部コンテンツを会話に挿入したり、メッセージに対してアクションを実行したりするためのショートカット。 | Teams Toolkit 拡張機能を備えた Visual Studio Code、または [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) と [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java、Python。 |

*これら特定のスタックを必ず利用しなければならないわけではありません!*

既に Yeoman ワークフローに慣れている方は、 [YoTeams Yeoman Generator](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) を使用してアプリをビルドするのを好まれるかも知れません。

## <a name="build-your-first-teams-app"></a>最初の Teams アプリをビルドする

それでは、最初の Teams アプリをビルドしましょう。 まず、言語 (またはフレームワーク) を選択し、開発環境を準備します。

> [!div class="nextstepaction"]
> [React を使用して JavaScript で Teams タブ アプリを構築する](../sbs-gs-javascript.yml)
> [!div class="nextstepaction"]
> [JavaScript で Teams ボット アプリを構築する](../sbs-gs-bot.yml)
> [!div class="nextstepaction"]
> [React を使用して JavaScript で Teams メッセージ拡張アプリを構築する](../sbs-gs-msgext.yml)
> [!div class="nextstepaction"]
> [Blazor を使用して Teams アプリを構築する](../sbs-gs-blazorupdate.yml)
> [!div class="nextstepaction"]
> [SPFx](../sbs-gs-spfx.yml) を使用して Teams アプリを構築する
> [!div class="nextstepaction"]
> [C# または .NETを使用して Teams アプリをビルドする](../sbs-gs-csharp.yml)
> [!div class="nextstepaction"]
> [node.js を使用して Teams アプリをビルドする](../sbs-gs-nodejs.yml)
> [!div class="nextstepaction"]
> [JavaScript を使用した通知ボットのビルド](../sbs-gs-notificationbot.yml)
> [!div class="nextstepaction"]
> [Build コマンド ボットと JavaScript](../sbs-gs-commandbot.yml)
> [!div class="nextstepaction"]

## <a name="see-also"></a>関連項目

- [Microsoft Teamsサンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples#microsoft-teams-samples)
- [Git および GitHub リソース](/contribute/additional-resources)
