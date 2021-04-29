---
title: はじめに - 最初のアプリを構築して実行する
author: girliemac
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams のツールキットを使用したメッセージ。"
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068783"
---
# <a name="create-your-first-microsoft-teams-app"></a>最初の Microsoft Teams アプリを作成する

このクイック スタートでは、"Hello, World! を表示する Microsoft Teams アプリをビルドして実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

開始する前に、Teams 開発テナント [をセットアップし、Teams](#set-up-your-teams-development-tenant) [開発ツールをインストールする必要があります](#install-your-development-tools)。

### <a name="set-up-your-teams-development-tenant"></a>Teams 開発テナントをセットアップする

テナント **は** 、組織のコンテナーに似たものになります。 Teams の用語では、テナントとは、その組織のチャット、ファイルの共有、会議の実行を行うユーザーです。 開発者は、構築する Teams アプリをサイドロードしてテストするテナントが必要です。  

# <a name="do-not-have-a-tenant"></a>[テナントを持たない](#tab/do-not-have-a-tenant)

Microsoft 365 開発者プログラムに参加することで、アプリのサイドローディングを許可するテナントを含む無料の Teams テスト アカウントを取得できます。 登録プロセスには約 2 分かかります。

**テナントを取得するには**

1. [Microsoft 365 開発者プログラムに移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
1. [今 **すぐ参加] を** 選択し、画面の指示に従います。
1. [ようこそ] 画面で **、[E5 サブスクリプションの設定] を選択します**。
1. Microsoft 365 開発者アカウントを設定します。 
   完了すると、次の画面が表示されます。

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後に表示される例。":::

1. 新しいアカウントで Teams にサインインします。
1. Teams クライアントで、[アプリ] を **選択します**。
1. [カスタム アプリのアップロード] **オプションが表示されるのを確認** します。 これを行う場合は、アプリをサイドロードできます。

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタム アプリをアップロードできる場所を示す図。":::

# <a name="have-a-tenant"></a>[テナントを持つ](#tab/have-a-tenant)

テナントが既にある場合は、Teams でアプリをサイドロードできるのか確認します。

**アプリをサイドロードできると確認する** 

1. Teams クライアントで、[アプリ] を **選択します**。 
1.  [カスタム アプリのアップロード] **オプションが表示されるのを確認** します。 これを行う場合は、アプリをサイドロードできます。 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタム アプリをアップロードできる場所を示す図。":::

---

### <a name="install-your-development-tools"></a>開発ツールのインストール

このアプリをビルドするには、Teams ToolkitコードVisual Studioすぐに開始します。 また、任意のプレファード ツールを使用して Teams アプリをビルドすることもできます。 

> [!NOTE]
> Teams は、HTTPS 接続を介してアプリのコンテンツのみを表示します。 ボットなど、特定の種類のアプリをローカルでデバッグするには、ngrok を使用して Teams とアプリの間にセキュリティで保護されたトンネルを設定する方法について説明します。
> 
> Production Teams アプリはクラウドでホストされます。

**Microsoft Teams ツールをインストールするには**

1. [Node.js](https://nodejs.org/en/) をインストールします。
1. ボットまたはメッセージング拡張機能を作成する場合は [、ngrok](https://ngrok.com/download) をインストールし [、ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)を使用してローカル ホストをインターネットに公開します。
1. 最新バージョンのコードを [インストールVisual Studioします](https://code.visualstudio.com/download)。 
   
   > [!NOTE]
   > ツールキットは、以前のバージョンのコードをVisual Studioされていません。

1. 左側のアクティビティ バーで、[拡張機能] **を選択します** :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 。
1. **[Microsoft Teams Toolkit]** で、[インストール] を **選択します**。

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="コード内の Microsoft Teams Visual Studio拡張機能をインストールできる場所を示Toolkit図。":::

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

1. Visual Studio Code を開きます。
1. [Microsoft **Teams] を選択Toolkit** :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams アプリを作成します**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="アプリ プロジェクトを作成する方法を示Visual Studio Code Teams Toolkit。":::
   
1. Microsoft 365 開発アカウントでサインインします。 作成したアカウントか、アプリのサイドローディングを許可するアカウントのどちらかです。
1. [プロジェクトの **選択] 画面** で、[個人用アプリ] に **移動し** 、[次へ] の **[JS** (JavaScript) > **選択します**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Visual Studio Code Teams ツールキットを使用して、アプリ プロジェクトを構成する方法を示すスクリーンショット。":::

1. Teams アプリの名前を入力します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="アプリ プロジェクトに名前を追加する方法を示すスクリーンショットで、コード Teams Visual StudioをToolkit。":::

1. [**完了**] を選択します。 
   これで、プロジェクトが構成されます。 

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントについて

ツールキットでアプリ プロジェクトを構成した後、"Hello, World! Teams アプリ。 プロジェクトのディレクトリとファイルは、コード エクスプローラー Visual Studioにあります。 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="アプリ プロジェクトのスキャフォールディングを示すスクリーンショットと、Visual Studio Teams Toolkit。":::

ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにアプリスキャフォールディング `src` を自動的に作成します。 セットアップ中にタブを作成したので、ディレクトリ内のファイルはアプリの初期化と `App.js` `src/components` ルーティングを処理します。 このファイルは、Microsoft Teams JavaScript クライアント SDK を呼び出して、アプリと Teams の間の通信を確立します。 

## <a name="3-build-and-run-your-app"></a>3. アプリの構築と実行

アプリをローカルに構築して実行することで、時間を節約できます。 

**アプリをビルドして実行するには**

1. [コードVisual Studioで、[ターミナルの表示 **] を**  >  **選択します**。
1. `npm install` を実行します。
1. `npm start` を実行します。
  
  コンパイル **が正常に完了しました。** メッセージがターミナルに表示されます。 これで、アプリが localhost で実行されています `https://localhost:3000` 。 

## <a name="4-sideload-your-app-in-teams"></a>4. Teams でアプリをサイドロードする

サイドローディングとは、管理者または Microsoft によって承認されていないアプリを Teams にインストールするプロセスです。 サイドローディングは、Teams アプリのテストとデバッグを行う場合に一般的です。

既定では、Teams ではアプリのサイドローディングは許可されません。 この設定は、Teams 管理センターで変更できます。

**Teams でアプリのサイドローディングを有効にするには**

1. 管理者資格情報を [使用して Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理センターにサインインします。  
1. [**すべての** > **Teams の表示**]を選択します。 

   ![管理センター メニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > Teams オプションが表示されるには、最大で 24 **時間かかる** 場合があります。 

1. [Teams アプリ **の**  >  **セットアップ ポリシー] グローバル**  >  (**組織** 全体の既定) に移動します。

   ![sideload ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. [カスタム アプリの **アップロード] トグルをオン** にします。

1. [保存 **] を** 選択して変更を保存します。

   テスト テナントでカスタム アプリのサイドローディングが許可されます。

   > [!Note]
   > ツールキットに含まれている App Studio の検証機能を使用してアプリをサイドロードする前に問題を確認します。 エラーを修正して、アプリを正常にサイドロードします。


### <a name="sideload-your-app"></a>アプリをサイドロードする

1. [Visual Studioコード] で、Teams ファイルを開Toolkit。
1. [App **Studio] に移動します**。  
1. [インストール **のテストと配布] を**  >  **選択します**。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="アプリを Teams クライアントにサイドロードする方法を示すスクリーンショットで、Visual Studio Teams Toolkit。":::

**または、**

1. **F5 キーを選択して** ブラウザー ウィンドウを開き、インストールします。 これにより、ブラウザーの **App Studio** とラウチ Teams のインストール プロセスがスキップされます。
1. インストール ダイアログで、[追加] を **選択** して、アプリを Teams にインストールします。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="アプリを Teams クライアントにサイドロードする方法を示すスクリーンショット。":::

   > [!Note]
   > App Studio は、Teams クライアント用のスタンドアロン アプリとして利用することもできます。

### <a name="troubleshoot-sideloading-issues"></a>サイドローディングの問題のトラブルシューティング

**インストールに失敗しました**

アプリのインストール中にエラー メッセージが表示される場合は、アプリ `Manifest parsing has failed` 情報が正しく入力されていることを確認します。

**アプリ情報を確認するには**

* Teams の設定Toolkit App Studio **App** の詳細に移動し、必要なすべての情報が正しく  >  入力されていることを確認します。
*  ファイルを手動で編集した場合は、APP Studio のアプリ マニフェスト ツールで JSON が適切に定義 `manifest.json` されている必要があります。 

**タブ コンテンツが表示されない**

アプリが実行されているのを確認します。 ない場合は、ターミナルに移動して実行します `npm start` 。

## <a name="see-also"></a>関連項目

* [Microsoft 365 テナントを準備する](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [Microsoft Teams アプリをテストおよびデバッグするためのセットアップの選択](../concepts/build-and-test/debug.md)
* [Microsoft Teams JavaScript クライアント SDK でタブやその他のホストされたエクスペリエンスを構築する](../tabs/how-to/using-teams-client-sdk.md)
* [AppSource 申請の準備](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Microsoft Teams 用の App Studio を使用してアプリをすばやく開発する](../concepts/build-and-test/app-studio-overview.md)
* [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Microsoft Teams の個人用タブを作成する](../build-your-first-app/build-personal-tab.md)
