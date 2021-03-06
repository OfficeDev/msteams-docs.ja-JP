---
title: 使用を開始する - 最初の会話型ボットのビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams の会話ボットを作成します。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 96bbddd99b6901a4b92e1e2f2dc98482c755dc66
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254252"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a>Microsoft Teams 用の会話型ボットをビルドする

このチュートリアルでは、Teams ボット アプリを構築し、実行し、展開する方法を学びます。 ボットは、Teams ユーザーと Web サービスの間を仲介する役割を果たします。  ユーザーは、ボットとチャットすることで、情報を素早く入手したり、ワークフローを開始したり、Web サービスに可能なすべてのことができます。 

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

1. [機能の **選択] セクションで**、[ボット] を選択 **し、[タブ**] の選択を **解除し****、[OK] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. [ボット登録 **] セクションで** 、[新しい **ボット登録の作成] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

1. [プログラミング **言語] セクションで****、[JavaScript] を選択します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. ワークスペース フォルダーを選択します。  ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。

1. `helloworld` のように、アプリに適した名前を入力します。  アプリの名前には、英数字のみを含む必要があります。  **Enter** キーを押して続行します。

数秒後に Teams アプリが作成されます。

# <a name="command-line"></a>[コマンド ライン](#tab/cli)

`teamsfx` CLI を使用して、最初のプロジェクトを作成します。  プロジェクト フォルダーを作成するフォルダーから開始します。

``` bash
teamsfx new
```

CLI では、プロジェクトを作成するためのいくつかの質問を行います。  各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。  質問に答えた後、**Enter** キーを押して選択を確認します。

1. **[新しい Teams アプリを作成]** を選択します。
1. [ボット **] を選択し** 、[タブ] の **選択を解除します**。
1. **新しいボット登録の作成** を選択します。
1. プログラミング言語として **[JavaScript]** を選択します。
1. **Enter** キーを押して、既定のワークスペース フォルダーを選択します。
1. `helloworld` のように、アプリに適した名前を入力します。  アプリの名前は、英数字のみで構成されている必要があります。

すべての質問に答えた後、プロジェクトが作成されます。

---

## <a name="take-a-tour-of-the-source-code"></a>ソース コードのツアーを開始する

このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。

メッセージング拡張機能では、[[ボット フレームワーク]](https://docs.botframework.com) を使用して、ユーザーが会話を介してサービスと対話できるようにします。  足場を組むと、プロジェクトは以下のようになります。

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="ボット プロジェクトのファイル レイアウト":::。

ボット コードは `bot` ディレクトリに格納されています。  `bot/teamsBot.js` はボットの主な入力ポイントで、ダイアログは `dialogs` ディレクトリに格納されます。

> [!Tip]
> Teams 内で最初のボットを統合する前に、Teams 外のボットに慣れておきましょう。  ボットの詳細については、[[Azure Bot Service]](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) のチュートリアルをご覧ください。

## <a name="run-your-app-locally"></a>アプリをローカルで実行する

Teams ツールキットでは、アプリをローカルでホストすることができます。  これを行うには、次の手順を実行します。

- M365 テナント内に Azure Active Directory アプリケーションが登録されています。
- アプリのマニフェストを Teams の開発者センターに送信します。
- API は Azure Functions Core Tools を使用してローカルで実行され、アプリをサポートします。
- [ngrok](https://ngrok.io) がインストールされ、Teams とボット コードの間のトンネルを指定するために使用されます。

アプリをローカルに構築して実行するには、以下のようにします。

1. 次Visual Studio Code **F5** キーを押して、アプリケーションをデバッグ モードで実行します。

   > アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。  ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。  この作業には 3 ～ 5 分かかります。

1. Web ブラウザーがアプリの実行を開始します。 デスクトップを開くTeams場合は、[キャンセル] を **選択して** ブラウザーに残ります。 また、他の場合はデスクトップに切り替Teams表示される場合があります。この場合Teams Web アプリを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. サインインするように求めるメッセージが表示されることがあります。  その場合は、M365 アカウントを使用してサインインします。
1. アプリをインストールするように求めるメッセージが表示されたら、[Teams] を **選択します**。

   アプリが読み込まれた後、ボットとのチャット セッションに直接アクセスします。  `intro` を入力すると紹介カードが表示され、`show` を入力すると Microsoft Graph からユーザーの詳細情報が表示されます。  (これには追加で許可の承認が必要です)。

   デバッグは通常通りに動作します。実際にお試しください。 `bot/dialogs/rootDialog.js` ファイルを開き、`triggerCommand(...)` メソッドを探します。  既定のケースにブレークポイントを設定します。  次に、テキストを入力します。

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

## <a name="see-also"></a>関連項目

* [チュートリアルの概要](code-samples.md) 
* [アプリを使用してアプリを作成React](first-app-react.md)
* [Blazor を使用してアプリを作成する](first-app-blazor.md)
* [アプリを使用してアプリを作成SPFx](first-app-spfx.md)
* [C# を使用してアプリを作成する](get-started-dotnet-app-studio.md)
* [Node.js を使ってアプリを作成する](get-started-nodejs-app-studio.md)
* [Yeoman ジェネレーターを使用してアプリを作成する](get-started-yeoman.md)
* [メッセージング拡張機能を作成する](first-message-extension.md)
* [コード サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples)