---
title: Microsoft Teams のコードサンプル
description: Microsoft Teams 開発者向けプラットフォーム用のサンプルアプリケーションのリンクと説明
keywords: Microsoft Teams の開発者向けサンプル
ms.openlocfilehash: 7a81494d7808c27c495c660b5d58f7779ba87c83
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237959"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Microsoft Teams 開発者向けプラットフォームのチュートリアルとコードサンプル

ここでは、カスタムアプリを作成することによって Teams 開発者プラットフォームの機能を拡張する方法を示すチュートリアルとコードサンプルの一覧を確認できます。

## <a name="getting-started-with-microsoft-learn"></a>Microsoft の概要

| 機能| 学習モジュール|
|--------|-------------|
| タブ-埋め込まれた web エクスペリエンス  |  [Microsoft Teams のタブによる埋め込み Web エクスペリエンスの作成](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhook とコネクタ  |  [Webhook と Office 365 コネクタを使用して Web サービスを Microsoft Teams に接続する](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|メッセージングの拡張機能  | [メッセージング拡張機能による Microsoft Teams でのタスク指向の相互作用](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| タスク モジュール |  [タスクモジュールを使用して Microsoft Teams で入力を収集する](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| 話し言葉の bot  | [Microsoft Teams 向けの対話型ボットの作成](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>コードサンプルの概要

GitHub からサンプルをダウンロードするには、次のようにします。

1. 次に示すプロジェクトのいずれかを選択し、GitHub でプロジェクトを開きます。
2. [ **クローン] または [ダウンロード** ] ボタンを選択し、URL をコピーします。
3. サンプルプロジェクトをインストールする親ディレクトリで、コマンドプロンプトを開きます。
4. `git clone <pasted url>` を実行します。

### <a name="for-netc-samples"></a>.NET/C# サンプルの場合

各 .NET サンプルには、NuGet パッケージの復元を含む、ソリューションを完全にビルドできる Visual Studio ソリューションファイルが含まれています。

### <a name="for-nodejs-samples"></a>Node.js サンプルの場合

サンプルのすべての必要なパッケージを一覧表示するファイルに packages.jsが提供されています。 `npm install`必要なパッケージをインストールするには、Node.js プロジェクトディレクトリのコマンドラインから実行するだけです。 これで、Visual Studio Code でプロジェクトを開き、実験を開始する準備が整いました。

### <a name="for-other-samples"></a>その他のサンプル

プロジェクトの README ファイルには、特定のサンプルの特定のニーズに関する情報が含まれている必要があります。

## <a name="bots-using-the-v4-sdk"></a>Bot (v4 SDK を使用)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>[Bot フレームワークサンプルリポジトリ](https://github.com/Microsoft/BotBuilder-Samples)を参照して、C#、JavaScript、TypeScript、および Python の Microsoft Bot フレームワーク v4 SDK のタスクに重点を置いたサンプルを表示します。

## <a name="messaging-extensions-using-the-v4-sdk"></a>メッセージング拡張機能 (v4 SDK を使用)

| サンプル | 説明 | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| メッセージング拡張機能-検索 | 検索要求を受け付けて結果を返すメッセージング拡張機能。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| メッセージング拡張機能-アクション | パラメーターを受け取り、カードを返すメッセージング拡張機能。 また、メッセージング拡張機能で転送されたメッセージをパラメーターとして受信する方法についても説明します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| メッセージング拡張機能-auth および config | 構成ページがあるメッセージング拡張機能は、検索要求を受け付け、ユーザーがサインインした後に結果を返します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| メッセージング拡張機能-アクションのプレビュー | メッセージング拡張機能のプレビューおよび編集フローを作成する方法について説明します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| リンク展開 | Link unfurling を実行するメッセージング拡張機能。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


## <a name="outgoing-webhooks"></a>送信 Web フック

| サンプル | 説明
|--------|-------------
| [C#/.NET の送信 Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | C#/.NET. で Microsoft Teams の **送信 Webhook** を作成する方法について説明します。
| [Node.jsの送信 Webhook ](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Node.js コードの ~ 50 行に Microsoft Teams 用の簡単な **送信 Webhook** を作成する方法を示します。

## <a name="connectors"></a>コネクタ

| サンプル | 説明
|--------|-------------
| [Node.js用のサンプルコネクタ ](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | このサンプルは Node.js で記述されており、コネクタ通知を生成するための例として GitHub を使用して Microsoft Teams 用のコネクタを構築する方法を示しています。
| [C#/.NET のサンプルコネクタ](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | このサンプルは、C# で記述されており、コネクタ通知を生成するための例としてサンプルのタスクリストアプリを使用して、Microsoft Teams 用のコネクタを構築する方法を示しています。

## <a name="graph-api"></a>Graph API

| サンプル | 説明
|--------|-------------
| [Microsoft Graph API のサンプル](https://github.com/OfficeDev/microsoft-teams-sample-graph) | これらのサンプルでは、microsoft Graph API 呼び出しを使用して、Microsoft Teams の外部で実行されている web サービスからのチームやチャネルのクエリなどのタスクを実行する方法を示します。

### <a name="bot-framework-sdk-v3-samples"></a>Bot フレームワーク SDK v3 のサンプル

| サンプル | 説明 |
|--------|------------- |
| [C#/.NET のサンプル bot](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Bot フレームワーク v3 のサンプル|
| [Node.jsの bot の例 ](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Bot フレームワーク v3 のサンプル |
