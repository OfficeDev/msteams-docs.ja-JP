---
title: Microsoft Teams のコード サンプル
description: Microsoft Teams 開発者プラットフォーム用のサンプル アプリケーションのリンクと説明
keywords: Microsoft Teams 開発者向けサンプル
ms.openlocfilehash: 665d3565f4f453d263fef6a17cb27f5060111468
ms.sourcegitcommit: 6d9c60cce1f2e5204e680c074ce77a8376233b59
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49912317"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Microsoft Teams 開発者プラットフォームのチュートリアルとコード サンプル

ここでは、カスタム アプリを作成して Teams 開発者プラットフォーム機能を拡張する方法を示すチュートリアルとコード サンプルの一覧を示します。

## <a name="getting-started-with-microsoft-learn"></a>Microsoft Learn の使用を開始する

| 機能| Learn モジュール|
|--------|-------------|
| タブ - 埋め込み Web エクスペリエンス  |  [Microsoft Teams のタブによる埋め込み Web エクスペリエンスの作成](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhook とコネクタ  |  [Webhook と Office 365 コネクタを使用して Web サービスを Microsoft Teams に接続する](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|メッセージング拡張機能  | [メッセージング拡張機能による Microsoft Teams でのタスク指向の相互作用](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| タスク モジュール |  [タスク モジュールを使用して Microsoft Teams で入力を収集する](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| 会話ボット  | [Microsoft Teams 向けの対話型ボットの作成](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>コード サンプルの使用を開始する

GitHub からサンプルをダウンロードするには:

1. 以下のプロジェクトのいずれかを選択し、GitHub でプロジェクトを開きます。
2. [複製 **またはダウンロード] ボタンを選択** して URL をコピーする
3. サンプル プロジェクトをインストールする親ディレクトリでコマンド プロンプトを開きます。
4. `git clone <pasted url>` を実行します。

### <a name="for-netc-samples"></a>.NET/C# サンプルの場合

各 .NET サンプルには、NuGet パッケージの復元Visual Studio含め、ソリューションを完全に構築できる新しいソリューション ファイルが含まれています。

### <a name="for-nodejs-samples"></a>サンプルNode.js

サンプルに必要packages.jsパッケージの一覧を示すファイルに関する情報を提供します。 必要な `npm install` パッケージをインストールするには、プロジェクト ディレクトリNode.jsコマンド ラインから実行します。 これで、プロジェクトをコードで開き、Visual Studio開始する準備ができました。

### <a name="for-other-samples"></a>その他のサンプルの場合

常に、プロジェクトの README ファイルには、特定のサンプルに関する特定のニーズに関する詳細な情報が含まれています。

## <a name="bots-using-the-v4-sdk"></a>ボット (v4 SDK を使用)

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>Bot [Framework サンプル リポジトリに](https://github.com/Microsoft/BotBuilder-Samples) アクセスして、C#、JavaScript、TypeScript、Python の Microsoft Bot Framework v4 SDK タスクに焦点を当てたサンプルを表示します。

## <a name="messaging-extensions-using-the-v4-sdk"></a>メッセージング拡張機能 (v4 SDK を使用)

| サンプル | 説明 | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| メッセージング拡張機能 - 検索 | 検索要求を受け入れて結果を返すメッセージング拡張機能。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| メッセージング拡張機能 - アクション | パラメーターを受け取り、カードを返すメッセージング拡張機能。 また、メッセージング拡張機能でパラメーターとして転送されたメッセージを受信する方法について説明します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| メッセージング拡張機能 - 認証と構成 | 構成ページを持つメッセージング拡張機能は、検索要求を受け入れ、ユーザーがサインインした後に結果を返します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| メッセージング拡張機能 - アクション プレビュー | メッセージング拡張機能のプレビューフローと編集フローを作成する方法を示します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| リンク展開 | リンクの分岐を実行するメッセージング拡張機能。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


## <a name="outgoing-webhooks"></a>送信 Webhook

| サンプル | 説明
|--------|-------------
| [C#/.NET の送信 Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | C#/.NET で Microsoft Teams 用 **の送信 Webhook** を作成する方法を示します。
| [送信 Webhook for Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | Microsoft Teams 用の簡単な **送信 Webhook** を約 50 行のコードで作成Node.jsしています。

## <a name="connectors"></a>コネクタ

| サンプル | 説明
|--------|-------------
| [サンプル コネクタのNode.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | Node.js で記述されたこのサンプルでは、コネクタ通知を生成する例として GitHub を使用して Microsoft Teams のコネクタを構築する方法を示します。
| [C#/.NET のサンプル コネクタ](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | C# で記述されたこのサンプルでは、コネクタ通知を生成する例としてサンプル タスク リスト アプリを使用して Microsoft Teams のコネクタを構築する方法を示します。 このサンプルでは、コネクタ構成ページでログイン機能を実装する方法も示します。 

## <a name="graph-api"></a>Graph API

| サンプル | 説明
|--------|-------------
| [Microsoft Graph API サンプル](https://github.com/OfficeDev/microsoft-teams-sample-graph) | これらのサンプルでは、Microsoft Graph API 呼び出しを使用して、Microsoft Teams の外部で実行される Web サービスからチームやチャネルにクエリを実行するなどのタスクを実行する方法を示します。

### <a name="bot-framework-sdk-v3-samples"></a>Bot Framework SDK v3 サンプル

| サンプル | 説明 |
|--------|------------- |
| [C#/.NET のサンプル ボット](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Bot Framework v3 サンプル|
| [サンプル ボット (Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Bot Framework v3 サンプル |
