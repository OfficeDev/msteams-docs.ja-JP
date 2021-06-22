---
title: 使用を開始する - 最初のメッセージング拡張機能のビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams のメッセージング拡張機能を作成します。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: cb37bc97c3b9de8ce469728e4c1b0e09ba1c2942
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037636"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a>Microsoft Teams 用の最初のメッセージング拡張機能のビルド及び実行

Teams **メッセージング拡張機能** には、以下の 2 種類があります。

- [検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md)を使用すると、外部システムを検索し、その検索結果をカード形式でメッセージに挿入できます。
- [操作コマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)を使用すると、情報を収集または表示するためのモーダル ポップアップをユーザーに表示し、対話を処理した後 Teams に情報を送り返すことができます。

このチュートリアルでは、外部データを検索し、その結果をメッセージに挿入する *検索コマンド* を作成します。  

## <a name="before-you-begin"></a>始める前に

[前提条件](prerequisites.md)をインストールして、開発環境が整っていることを確認します。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="create-your-project"></a>プロジェクトを作成する

Teams ツールキットを使用して、最初のプロジェクトを作成します。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Visual Studio Code を開きます。
1. サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. **[新しいプロジェクトの作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. **[新しい Teams アプリを作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. **[機能の選択]** 手順で、**[メッセージ拡張機能]** を選択し、**[タブ]** の選択を解除します。**[OK]** を押します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. **[ボットの登録]** 手順で、**[新しいボットの登録を作成する]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

   > [!NOTE]
   > メッセージング拡張機能は、ユーザーとコードの間のダイアログを提供するボットに依存しています。

1. **プログラミング言語** の手順で、**[JavaScript]** を選択します。

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
1. **[メッセージング拡張機能]** 機能を選択し、**[タブ]** 機能の選択を解除します。
1. **新しいボット登録の作成** を選択します。
1. プログラミング言語として **[JavaScript]** を選択します。
1. **Enter** キーを押して、既定のワークスペース フォルダーを選択します。
1. `helloworld` のように、アプリに適した名前を入力します。  アプリの名前は、英数字のみで構成されている必要があります。

すべての質問に答えると、プロジェクトが作成されます。

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

1. Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。

   > アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。  ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。  この作業には 3 ～ 5 分かかります。

1. Teams が Web ブラウザーに読み込まれ、サインインするようメッセージが表示されます。 Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。 M365 アカウントでサインインします。

1. **[追加]** を押して、アプリを自分のアカウントに追加します。

アプリが読み込まれると、そのまま検索ダイアログが表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="検索ベースのメッセージング拡張機能の動作":::

検索ボックスにテキストを入力し、オプションを選択します。  入力ボックスにアダプティブ カードが追加されます。

<!-- markdownlint-disable MD033 -->
<details>
<summary>デバッガーでアプリをローカルに実行した場合に発生することを説明します。</summary>

F5 を押すと、以下のように Teams ツールキットが表示されます。

1. Azure Active Directory を使用してアプリケーションを登録しました。
1. Microsoft Teams で "サイド読み込み" 用にアプリケーションを登録しました。
1. [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) を使用して、アプリケーション バックエンドのローカルでの実行を開始しました。
1. Teams がアプリと通信できるように、ngrok トンネルを開始しました。
1. アプリケーションのサイドロードを Teams に指示するコマンドで Microsoft Teams を開始します。

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

| **サンプル名** | **説明** | **.NET** | **Node.js** | **Python** |
|-----------------|-----------------|-------------|--------------|--------|
| ボット ビルダー | メッセージング拡張機能を作成するには。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [View]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a>追加のコード サンプル

> [!div class="nextstepaction"]
> [ボット フレームワークのサンプルを表示する GitHub](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a>関連項目

- [React を使用して Teams アプリを作成する](first-app-react.md)
- [Blazor を使用して Teams アプリを作成する](first-app-blazor.md)
- [SharePoint Web パーツとして Teams アプリを作成する](first-app-spfx.md) (Azure は必要なし)
- [会話ボットを作成する](first-app-bot.md)
