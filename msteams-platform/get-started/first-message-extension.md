---
title: 使用を開始する - 最初のメッセージング拡張機能のビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams のメッセージング拡張機能を作成します。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: 39659b6c58b61f8b8880bd277effba1c8f9d115e
ms.sourcegitcommit: 72de146d11e81fd9777374dd3915ad290fd07d82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2021
ms.locfileid: "59360686"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a>Microsoft Teams 用の最初のメッセージング拡張機能のビルド及び実行

このチュートリアルでは、外部データを検索して結果をメッセージに挿入する検索コマンドを作成する方法について説明します。 

Teams **メッセージング拡張機能** には、以下の 2 種類があります。

- [検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md)を使用すると、外部システムを検索し、その検索結果をカード形式でメッセージに挿入できます。
- [操作コマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)を使用すると、情報を収集または表示するためのモーダル ポップアップをユーザーに表示し、対話を処理した後 Teams に情報を送り返すことができます。

## <a name="before-you-begin"></a>はじめに

前提条件をインストールして、開発環境がセットアップされていることを確認します。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="create-your-project"></a>プロジェクトを作成する

Teams ツールキットを使用して、最初のプロジェクトを作成します。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Visual Studio Code を開きます。
1. サイドバーのTeamsアイコンを選択して、ウィンドウを開Teams Toolkit。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. **[新しいプロジェクトの作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. **[新しい Teams アプリを作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. [機能 **の選択] セクションで**、[メッセージ拡張機能] を **選択し、[** タブ] の選択を **解除し****、[OK] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. [ボット登録 **] セクションで** 、[新しい **ボット登録の作成] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

   > [!NOTE]
   > メッセージング拡張機能は、ユーザーとコードの間のダイアログを提供するボットに依存しています。

1. [プログラミング **言語] セクションで****、[JavaScript] を選択します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. ワークスペース フォルダーを選択します。  ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。

1. `helloworld` のように、アプリに適した名前を入力します。  アプリの名前は、英数字のみで構成されている必要があります。  **Enter** キーを押して続行します。

   数秒後に Teams アプリが作成されます。

# <a name="command-line"></a>[コマンド ライン](#tab/cli)

`teamsfx` CLI を使用して、最初のプロジェクトを作成します。  プロジェクト フォルダーを作成するフォルダーから開始します。

``` bash
teamsfx new
```

CLI では、プロジェクトを作成するためのいくつかの質問を行います。  各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。  質問に答えた後、**Enter** キーを押して選択を確認します。

1. **[新しい Teams アプリを作成]** を選択します。
1. [メッセージ拡張機能] **を選択し** 、[タブ] の選択を **解除します**。
1. **新しいボット登録の作成** を選択します。
1. プログラミング言語として **[JavaScript]** を選択します。
1. **Enter** キーを押して、既定のワークスペース フォルダーを選択します。
1. `helloworld` のように、アプリに適した名前を入力します。  アプリの名前は、英数字のみで構成されている必要があります。

   すべての質問に答えた後、プロジェクトが作成されます。

---

## <a name="take-a-tour-of-the-source-code"></a>ソース コードのツアーを開始する

このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。

メッセージング拡張機能では、[[ボット フレームワーク]](https://docs.botframework.com) を使用して、ユーザーが会話を介してサービスと対話できるようにします。  足場を組むと、プロジェクトは以下のようになります。

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="ボット プロジェクトのファイル レイアウト":::。

ボット コードは `bot` ディレクトリに格納されています。  `bot/messageExtensionBot.js` は、メッセージング拡張機能の主な入力ポイントです。

> [!Tip]
> Teams 内で最初のボットを統合する前に、Teams 外のボットに慣れておきましょう。  ボットの詳細については、[[Azure Bot Service]](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) のチュートリアルをご覧ください。

## <a name="run-your-app-locally"></a>アプリをローカルで実行する

Teams ツールキットでは、アプリをローカルでホストすることができます。  これを行うには、次の手順を実行します。

- M365 テナント内に Azure Active Directory アプリケーションが登録されています。
- アプリのマニフェストをDeveloper Portal for Teams に送信します。
- API は Azure Functions Core Tools を使用してローカルで実行され、アプリをサポートします。
- [ngrok](https://ngrok.io) がインストールされ、Teams とメッセージング拡張機能の間のトンネルを指定するために使用されます。

アプリをローカルに構築して実行するには、以下のようにします。

1. 次Visual Studio Code **F5** キーを押して、アプリケーションをデバッグ モードで実行します。

   > アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。  ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。  この作業には 3 ～ 5 分かかります。

1. Teams が Web ブラウザーに読み込まれ、サインインするようメッセージが表示されます。 Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。 M365 アカウントでサインインします。

1. [ **追加] を** 選択して、アプリをアカウントに追加します。

   アプリが読み込まれたら、サンプル機能を使用できます。作成領域の 3 つのドットからメッセージ拡張機能を起動し、検索バーから npm パッケージを検索できます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/search-message-extension.png" alt-text="検索ベースのメッセージング拡張機能の動作":::
   
   また、メッセージ拡張インスタンスの一番上の行にある検索バーから @を試Teams npm パッケージを検索することもできます。
    :::image type="content" source="../assets/images/teams-toolkit-v2/msgext-teams-search-bar.png" alt-text="検索ベースのメッセージング拡張機能の動作":::

   検索ボックスにテキストを入力し、オプションのいずれかを選択すると、検索結果のアダプティブ カードを作成して送信できます。
    :::image type="content" source="../assets/images/teams-toolkit-v2/msgext-adptive-card.png" alt-text="検索ベースのメッセージング拡張機能の動作":::

<!-- markdownlint-disable MD033 -->
<details>
<summary>デバッガーでアプリをローカルに実行した場合に発生することを説明します。</summary>

**F5** キーを押すと、次のTeams Toolkit。

1. アプリケーションをアプリケーションに登録Azure Active Directory。
1. アプリケーションを"サイド ローディング" に登録Microsoft Teams。
1. Azure Function Core Tools を使用してローカルで実行されている [アプリケーション バックエンドを開始します](/azure/azure-functions/functions-run-local?#start)。
1. アプリと通信Teams ngrok トンネルを開始します。
1. アプリケーションMicrosoft Teams読み込むようTeamsコマンドを使用して開始します。

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</summary>

Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。 アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。

> [!TIP]
> ツールキットに含まれる[アプリ認証ツール](https://dev.teams.microsoft.com/appvalidation.html)を使用して、アプリをサイドロードする前に問題がないか確認します。 エラーを修正して、アプリを正常にサイドロードします。
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary>アプリを Azure に展開した場合に発生することを説明します</summary>

展開前は、このアプリケーションは以下のようにローカルで動作しています。

1. バックエンドは、_Azure Functions Core Tools_ を使用して実行します。
1. アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。

展開では、アクティブな Azure サブスクリプションにリソースをプロビジョニングし、アプリケーションのバックエンドとフロントエンドのコードを Azure に展開 (アップロード) します。 バックエンドには、Azure App Service や Azure Bot Service など、さまざまな Azure のサービスが使用されています。

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a>メッセージング拡張機能に構成ページを追加する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a>コード サンプル

Teams上GitHubサンプル プロジェクトの検索 Auth Config では、構成ページとボット サービス認証を含むメッセージング拡張機能を作成する方法[を示します](https://github.com/microsoft/BotBuilder-Samples#teams-samples)。 このサンプルでは、ユーザーがサインインした後に、検索要求を受け入れ、結果を返すメッセージ拡張機能を作成する方法も示しています。

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|-----------------|-----------------|-------------|--------------|--------|
| ボット ビルダー | メッセージング拡張機能を作成するには。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [表示]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a>追加のコード サンプル

> [!div class="nextstepaction"]
> [ボット フレームワークのサンプルを表示する GitHub](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a>関連項目

* [チュートリアルの概要](code-samples.md) 
* [アプリを使用してアプリを作成React](first-app-react.md)
* [Blazor を使用してアプリを作成する](first-app-blazor.md)
* [アプリを使用してアプリを作成SPFx](first-app-spfx.md)
* [C# を使用してアプリを作成する](get-started-dotnet-app-studio.md)
* [Node.js を使ってアプリを作成する](get-started-nodejs-app-studio.md)
* [Yeoman ジェネレーターを使用してアプリを作成する](get-started-yeoman.md)
* [会話ボット アプリを作成する](first-app-bot.md)
* [コード サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples)
