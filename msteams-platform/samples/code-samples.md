---
title: Microsoft Teams のコードサンプル
description: Microsoft Teams 開発者向けプラットフォーム用のサンプルアプリケーションのリンクと説明
keywords: Microsoft Teams の開発者向けサンプル
ms.openlocfilehash: eb7794e788f8eb39102ac874748e23d8621f281e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674609"
---
# <a name="code-samples-for-the-microsoft-teams-developer-platform"></a>Microsoft Teams 開発者向けプラットフォームのコードサンプル

ここには、Microsoft Teams 開発プラットフォームのさまざまな機能を示すコードサンプルの一覧と、それらの機能を活用するアプリを構築する方法が記載されています。

## <a name="getting-samples"></a>サンプルを取得する

GitHub からサンプルをダウンロードするには、次のようにします。

1. 次に示すプロジェクトのいずれかを選択し、GitHub でプロジェクトを開きます。
2. [**クローン] または [ダウンロード**] ボタンを選択し、URL をコピーします。
3. サンプルプロジェクトをインストールする親ディレクトリで、コマンドプロンプトを開きます。
4. `git clone <pasted url>` を実行します。

### <a name="for-netc-samples"></a>.NET/C# サンプルの場合

各 .NET サンプルには、NuGet パッケージの復元を含む、ソリューションを完全にビルドできる Visual Studio ソリューションファイルが含まれています。

### <a name="for-nodejs-samples"></a>Node.js のサンプルの場合

サンプルのすべての必要なパッケージを一覧表示するパッケージの json ファイルが提供されています。 Node.js プロジェクト`npm install`ディレクトリのコマンドラインから実行して、必要なパッケージをインストールするだけです。 これで、Visual Studio Code でプロジェクトを開き、実験を開始する準備が整いました。

### <a name="for-other-samples"></a>その他のサンプル

プロジェクトの README ファイルには、特定のサンプルの特定のニーズに関する情報が含まれている必要があります。

## <a name="get-started"></a>作業の開始

| 例 | 説明|
|--------|-------------|
| [Node.js を使用した Microsoft Teams での Hello World](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) | 基本的なアプリ機能を`Node.js`紹介するためのサンプル teams アプリ。|
| [C# .NET を使用した Microsoft Teams での Hello World](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) | 基本的なアプリ機能を`C# .NET`紹介するためのサンプル teams アプリ。|
| [Teams 用のごみ箱のジェネレーターを使い始める](~/tutorials/get-started-yeoman.md) | Microsoft Teams 用のごみ箱のジェネレーターを使用して、新規に Teams アプリを作成します。 |

## <a name="bots-using-the-v4-sdk"></a>Bot (v4 SDK を使用)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="messaging-extensions-using-the-v4-sdk"></a>メッセージング拡張機能 (v4 SDK を使用)

| 例 | 説明 | .NET Core | JavaScript |
|--------|------------- |---|---|
| 検索コマンド | 検索コマンドを使用した単純なメッセージング拡張機能 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|
| アクションコマンド | アクションコマンドを使用した単純なメッセージング拡張機能。 [メッセージの作成] 領域に挿入された応答。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|
| アクションコマンド w/bot 応答 | アクションコマンドを使用したメッセージング拡張機能。 Bot が会話に挿入する応答。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|
| 検索コマンド | 検索コマンドを使用したメッセージング拡張機能と認証および構成 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>送信 Web フック

| 例 | 説明
|--------|-------------
| [C#/.NET の送信 Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | C#/.NET. で Microsoft Teams の**送信 Webhook**を作成する方法について説明します。
| [Node.js の送信 Webhook](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Node.js コードの ~ 50 行に Microsoft Teams 用の簡単な**送信 Webhook**を作成する方法について説明します。

## <a name="connectors"></a>コネクタ

| 例 | 説明
|--------|-------------
| [Node.js のサンプルコネクタ](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | このサンプルは、node.js で記述されています。コネクタ通知を生成するための例として、GitHub を使用して Microsoft Teams 用のコネクタを構築する方法を示します。
| [C#/.NET のサンプルコネクタ](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | このサンプルは、C# で記述されており、コネクタ通知を生成するための例としてサンプルのタスクリストアプリを使用して、Microsoft Teams 用のコネクタを構築する方法を示しています。

## <a name="graph-api"></a>Graph API

| 例 | 説明
|--------|-------------
| [Microsoft Graph API のサンプル](https://github.com/OfficeDev/microsoft-teams-sample-graph) | これらのサンプルでは、microsoft Graph API 呼び出しを使用して、Microsoft Teams の外部で実行されている web サービスからのチームやチャネルのクエリなどのタスクを実行する方法を示します。

## <a name="others"></a>その他

| コード | 説明 |
|------|------------- |
| [Node.js の完全なサンプル](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) | このサンプルは、Microsoft Teams プラットフォームのすべての機能を使用する方法を示しています。 メモ: このサンプルでは、Bot Framework v3 SDK を使用します。|
| [C#/.NET の完全なサンプル](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) | このサンプルは、Microsoft Teams プラットフォームのすべての機能を使用する方法を示しています。 メモ: このサンプルでは、Bot Framework v3 SDK を使用します。 |
| [C#/.NET の基幹業務アプリ](https://github.com/OfficeDev/msteams-sample-line-of-business-apps-csharp) | このリポジトリには、インスピレーションまたはテンプレートとして使用できるビジネスアプリの複数の例が含まれています。 注: これらのサンプルでは、Bot Framework v3 SDK を使用します。|
| ["To do" リストのサンプルタブアプリ](https://github.com/OfficeDev/microsoft-teams-sample-todo) | この node.js サンプルは、既存の web アプリをタブに簡単に変換する方法を示しています。 |
| [Orky](https://github.com/OfficeDev/Orky) | Microsoft Teams に独自のローカル bot を登録して、どこからでもスクリプトを実行することができます。 |
| [2017の天気予報を構築する](https://github.com/OfficeDev/microsoft-teams-build2017-weather) | 最新. セッションで以前に生成されたスケルトンアプリに天気予報タブを追加するには、//ビルド2017セッションのソースコードを使用します。 |

### <a name="bot-framework-sdk-v3-samples"></a>Bot フレームワーク SDK v3 のサンプル

| 例 | 説明 |
|--------|------------- |
| [C#/.NET のサンプル bot](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Bot フレームワーク v3 のサンプル|
| [Node.js のサンプル bot](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Bot フレームワーク v3 のサンプル |
