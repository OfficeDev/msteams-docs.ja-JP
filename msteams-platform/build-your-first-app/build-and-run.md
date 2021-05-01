---
title: はじめに - 最初のアプリを構築して実行する
author: girliemac
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams のツールキットを使用したメッセージ。"
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: 6c3d215a3f2c1aa89a9a2bf28aad081d98c6dc33
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101724"
---
# <a name="create-your-first-microsoft-teams-app"></a>最初のアプリをMicrosoft Teamsする

このクイック スタートでは、"Hello, World! を表示Microsoft Teamsアプリをビルドして実行する方法について教えています。

## <a name="prerequisites"></a>前提条件

開始する前に、開発テナント[をセットアップし、Teams開発](#set-up-your-teams-development-tenant)ツール[をインストールTeams必要があります](#install-your-development-tools)。

### <a name="set-up-your-teams-development-tenant"></a>開発テナントTeams設定する

テナント **は** 、組織のコンテナーに似たものになります。 つまりTeamsテナントとは、その組織のチャット、ファイルの共有、会議の実行を行う場所です。 開発者は、構築中のアプリをサイドロードしてテストTeamsテナントが必要です。  

# <a name="do-not-have-a-tenant"></a>[テナントを持たない](#tab/do-not-have-a-tenant)

アプリのサイドローディングをTeamsするテナントを含む無料のテスト アカウントを取得するには、開発者プログラムMicrosoft 365参加します。 登録プロセスには約 2 分かかります。

**テナントを取得するには**

1. 開発者プログラムの[Microsoft 365に移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
1. [今 **すぐ参加] を** 選択し、画面の指示に従います。
1. [ようこそ] 画面で **、[E5 サブスクリプションの設定] を選択します**。
1. 開発者アカウントMicrosoft 365設定します。 
   完了すると、次の画面が表示されます。

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="開発者プログラムにサインアップした後に表示されるMicrosoft 365例。":::

1. 新しいアカウントでTeamsサインインします。
1. クライアントで、[Teams] を **選択します**。
1. カスタム アプリ オプションのアップロード **確認** します。 これを行う場合は、アプリをサイドロードできます。

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="カスタム アプリをアップロードTeams場所を示す図。":::

# <a name="have-a-tenant"></a>[テナントを持つ](#tab/have-a-tenant)

テナントが既に存在する場合は、アプリをアプリにサイドロードできるTeams。

**アプリをサイドロードできると確認する** 

1. [クライアント] Teams[アプリ] を **選択します**。 
1.  カスタム アプリ オプションのアップロード **確認** します。 これを行う場合は、アプリをサイドロードできます。 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="カスタム アプリをアップロードTeams場所を示す図。":::

---

### <a name="install-your-development-tools"></a>開発ツールのインストール

このアプリをビルドするには、アプリのTeams ToolkitをVisual Studio Code開始します。 また、任意のTeamsアプリをビルドすることもできます。 

> [!NOTE]
> Teams HTTPS 接続経由でのみアプリ コンテンツが表示されます。 ボットなど、特定の種類のアプリをローカルでデバッグするには、ngrok を使用して、Teams とアプリの間にセキュリティで保護されたトンネルを設定する方法について説明します。
> 
> 実稼働Teamsはクラウドでホストされます。

**ツールをMicrosoft Teamsするには**

1. [Node.js](https://nodejs.org/en/) をインストールします。
1. ボットまたはメッセージング拡張機能を作成する場合は [、ngrok](https://ngrok.com/download) をインストールし [、ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)を使用してローカル ホストをインターネットに公開します。
1. 最新バージョンのファイルを[インストールVisual Studio Code。](https://code.visualstudio.com/download) 
   
   > [!NOTE]
   > このツールキットは、以前のバージョンのアプリケーションをVisual Studio Code。

1. 左側のアクティビティ バーで、[拡張機能] **を選択します** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 。
1. [インストール **Microsoft Teams Toolkit]** を **選択します**。

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="拡張機能をインストールVisual Studio Codeする場所を示Microsoft Teams Toolkit図。":::

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

1. Visual Studio Code を開きます。
1. [新 **Microsoft Teams Toolkit** :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **アプリを作成する] をTeamsします**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="アプリ プロジェクトを作成する方法を示すスクリーンショットをVisual Studio Code Teams Toolkit。":::
   
1. 開発アカウントでサインインMicrosoft 365します。 作成したアカウントか、アプリのサイドローディングを許可するアカウントのどちらかです。
1. [プロジェクトの **選択] 画面** で、[個人用アプリ] に **移動し** 、[次へ] の **[JS** (JavaScript) > **選択します**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Visual Studio Code Teams ツールキットを使用して、アプリ プロジェクトを構成する方法を示すスクリーンショット。":::

1. Teams アプリの名前を入力します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="アプリ プロジェクトに名前を追加する方法を示すスクリーンショットで、Visual Studio Code Teams Toolkit。":::

1. [**完了**] を選択します。 
   これで、プロジェクトが構成されます。 

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントについて

ツールキットでアプリ プロジェクトを構成した後、"Hello, World! Teamsアプリ。 プロジェクトのディレクトリとファイルは、プロジェクト エクスプローラー Visual Studio Codeされます。 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="アプリ プロジェクトのスキャフォールディングを示すスクリーンショットと、Visual Studio Code Teams Toolkit。":::

ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにアプリスキャフォールディング `src` を自動的に作成します。 セットアップ中にタブを作成したので、ディレクトリ内のファイルはアプリの初期化と `App.js` `src/components` ルーティングを処理します。 また、このファイルは JavaScript クライアント SDK Microsoft Teams呼び出して、アプリとアプリ間の通信を確立Teams。 

## <a name="3-build-and-run-your-app"></a>3. アプリの構築と実行

アプリをローカルに構築して実行することで、時間を節約できます。 

**アプリをビルドして実行するには**

1. [Visual Studio Code] で、[ターミナルの表示 **] を**  >  **選択します**。
1. `npm install` を実行します。
1. `npm start` を実行します。
  
  コンパイル **が正常に完了しました。** メッセージがターミナルに表示されます。 これで、アプリが localhost で実行されています `https://localhost:3000` 。 

## <a name="4-sideload-your-app-in-teams"></a>4. Teams でアプリをサイドロードする

サイドローディングは、管理者または Microsoft によって承認されていないアプリをTeamsアプリをインストールするプロセスです。 サイドローディングは、アプリのテストとデバッグを行うTeamsです。

既定では、Teamsアプリのサイドローディングは許可されません。 この設定は、管理センター Teams変更できます。

**アプリのサイドローディングを有効にするには、Teams**

1. 管理者資格情報を使用[Microsoft 365管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサインインします。  
1. [**すべての** > **Teams の表示**]を選択します。 

   ![管理センター メニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > このオプションを表示するには、最大で 24 **Teams** かかる場合があります。 

1. [アプリの **Teamsグローバル ]**(組織全体の既定)  >    >  に移動します。

   ![sideload ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. [カスタム アプリの **アップロード] トグルをオン** にします。

1. [保存 **] を** 選択して変更を保存します。

   テスト テナントでカスタム アプリのサイドローディングが許可されます。

   > [!Note]
   > ツールキットに含まれている App Studio の検証機能を使用してアプリをサイドロードする前に問題を確認します。 エラーを修正して、アプリを正常にサイドロードします。


### <a name="sideload-your-app"></a>アプリをサイドロードする

1. [Visual Studio Code] で、ファイルを開Teams Toolkit。
1. [App **Studio] に移動します**。  
1. [インストール **のテストと配布] を**  >  **選択します**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="アプリをクライアントにサイドロードする方法を示TeamsスクリーンショットをVisual Studio Code Teams Toolkit。":::

**または、**

1. **F5 キーを選択して** ブラウザー ウィンドウを開き、インストールします。 これにより、App **Studio** のインストール プロセスがスキップされ、ブラウザー Teamsが表示されます。
1. インストール ダイアログで、[追加]**を選択** して、アプリをインストールTeams。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="アプリをクライアントにサイドロードする方法を示Teamsスクリーンショット。":::

   > [!Note]
   > App Studio は、クライアントのスタンドアロン アプリTeamsもあります。

### <a name="troubleshoot-sideloading-issues"></a>サイドローディングの問題のトラブルシューティング

**インストールに失敗しました**

アプリのインストール中にエラー メッセージが表示される場合は、アプリ `Manifest parsing has failed` 情報が正しく入力されていることを確認します。

**アプリ情報を確認するには**

* 次のTeams Toolkit **App Studio App** の詳細に移動し、必要なすべての情報が正しく  >  入力されていることを確認します。
*  ファイルを手動で編集した場合は、APP Studio のアプリ マニフェスト ツールで JSON が適切に定義 `manifest.json` されている必要があります。 

**タブ コンテンツが表示されない**

アプリが実行されているのを確認します。 ない場合は、ターミナルに移動して実行します `npm start` 。

## <a name="see-also"></a>関連項目

* [Microsoft 365 テナントを準備する](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [アプリのテストとデバッグを行うセットアップMicrosoft Teamsする](../concepts/build-and-test/debug.md)
* [JavaScript クライアント SDK を使用してタブやその他のホストMicrosoft Teamsエクスペリエンスを構築する](../tabs/how-to/using-teams-client-sdk.md)
* [AppSource 申請の準備](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Microsoft Teams 用の App Studio を使用してアプリをすばやく開発する](../concepts/build-and-test/app-studio-overview.md)
* [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ユーザーの個人用タブを作成Microsoft Teams](../build-your-first-app/build-personal-tab.md)
