---
title: アプリ コードのサンプル
description: 開発者向けプラットフォームのサンプル アプリケーションのMicrosoft Teams説明
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teamsサンプル
ms.openlocfilehash: 34c914898f7ae83022f1278bc11cc33ac5084ba5
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156567"
---
# <a name="overview"></a>概要

このチュートリアルでは、React、Blazor、SPFx、C#、.NET、Node.js、および Yeoman Generator を使用してアプリを作成する方法について説明します。 また、最初のボットとメッセージング拡張機能を作成する方法も学習します。 このチュートリアルでは、タブ、ボット、メッセージング拡張機能、Webhooks とコネクタ、およびアプリのカスタマイズと構成に役立つ Graph API 用の複数のコード サンプルについて説明します。 さらに、「Microsoft Learn」セクションを参照して、カスタム アプリを作成することで、開発者Teams機能を拡張することもできます。  

## <a name="getting-started-with-microsoft-learn"></a>Microsoft Learn の使用を開始する

| **機能**| **Learn モジュール**|
|--------|-------------|
| タブ - 埋め込み Web エクスペリエンス  |  [Microsoft Teams のタブによる埋め込み Web エクスペリエンスの作成](/learn/modules/embedded-web-experiences/) |
| Webhook とコネクタ  |  [Webhook と Office 365 コネクタを使用して Web サービスを Microsoft Teams に接続する](/learn/modules/msteams-webhooks-connectors/) |
|メッセージング拡張機能  | [メッセージング拡張機能による Microsoft Teams でのタスク指向の相互作用](/learn/modules/msteams-messaging-extensions/)  |
| タスク モジュール |  [タスク モジュールを使用Microsoft Teams入力を収集する](/learn/modules/msteams-task-modules/) |
| 会話型ボット  | [Microsoft Teams 向けの対話型ボットの作成](/learn/modules/msteams-conversation-bots/)  |

## <a name="build-your-first-microsoft-teams-app-overview"></a>アプリの最初のMicrosoft Teamsを作成する

開始方法 **のレッスン** では、基本的なアプリを作成するTeamsします。 各チュートリアルでは、一般的なツール、基本的な概念、より高度な機能を紹介しながら、Teams実際のアプリを構築する方法について説明します。

### <a name="teams-app-fundamentals"></a>Teamsアプリの基本

開発者[Teamsを使用すると、](../overview.md)カスタム アプリをビルドできます。 Microsoft Teams のカスタム アプリが役立つ一般的なシナリオには、以下のようなシナリが含まれます。

* Web サイトまたは Web アプリを Teams クライアントに直接埋め込む。
* ユーザーが別のシステムで情報をすばやく検索し、その結果を別のシステムの会話に追加Teams。
* Teams での会話に基づいてワークフローとプロセスをトリガーし、会話のコンテキストを保持する。

チュートリアルを開始する前に、アプリの作成に関する以下の情報をTeams。

### <a name="app-capabilities"></a>アプリの機能

アプリTeamsは、1 つ以上の[プラットフォーム機能と](../concepts/capabilities-overview.md)ユーザー操作ポイント[で構成されます](../concepts/extensibility-points.md)。

アプリに必要な機能に応じて、適切な開発ツールセットが必要です。

| アプリの機能 | ユーザーの操作 | 推奨されるツール | SDK | テクノロジ スタック |
|--------|-------------|--------|--------|--------|
| タブ | フルスクリーンの埋め込み Web エクスペリエンス。 | VS Code拡張子Teams Toolkit、または YoTeams (Yeoman Generator) | [Teams SDK](/javascript/api/overview/msteams-client) | Web テクノロジ全般、HTML、CSS、JavaScript |
| ボット | メンバーと会話するチャット ボット。 | VS Code拡張子Teams Toolkit、または YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、または Python |
| メッセージング拡張機能 | 会話に外部コンテンツを挿入したり、メッセージに対してアクションを実行したりするショートカット。 | VS Code拡張子Teams Toolkit、または YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、または Python |

[スタート] セクションでは、これらの特定のスタックの使用に限定されませんが、推奨されるツール セットと一般的に使用されるテクノロジ (Teams 拡張子を持つ Visual Studio Code、タブの場合は React.js、ボットやメッセージング拡張機能の場合は Node.js など) について説明します。

コマンド ライン インターフェイス (CLI) の使用を希望する場合は、「Yeoman ジェネレーターを使用Microsoft Teamsアプリを作成する[」を参照してください](../get-started/get-started-yeoman.md)。

### <a name="teams-does-not-host-your-app"></a>Teamsアプリをホストしない

マニフェストとアプリ アイコンと呼ばれる構成ファイルを含むアプリ パッケージのみをインストールして、クライアントTeamsします。 アプリ ロジックとデータ ストレージの残りの部分は、Azure Web Services などの他の場所でホストされます。 開発中のクラウドまたは localhost 内のアプリは、HTTPS 経由でTeamsアクセスします。

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="クラウド サーバーでアプリ ロジックTeams示すアプリを示す図。":::

## <a name="see-also"></a>関連項目

* [アプリを使用してアプリを作成React](first-app-react.md)
* [Blazor を使用してアプリを作成する](first-app-blazor.md)
* [アプリを使用してアプリを作成SPFx](first-app-spfx.md)
* [C# を使用してアプリを作成する](get-started-dotnet-app-studio.md)
* [Node.js を使ってアプリを作成する](get-started-nodejs-app-studio.md)
* [Yeoman ジェネレーターを使用してアプリを作成する](get-started-yeoman.md)
* [会話ボット アプリを作成する](first-app-bot.md)
* [メッセージング拡張機能を作成する](first-message-extension.md)
* [コード サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples)
