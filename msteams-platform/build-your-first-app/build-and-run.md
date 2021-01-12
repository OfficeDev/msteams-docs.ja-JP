---
title: 開始する - 最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成します。 Microsoft Teams を使用したメッセージToolkit。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: bc5d18dd887cbdbf56b8d6d013f53c21d1540370
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795469"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>最初の Microsoft Teams アプリをビルドして実行する

"Hello, World!" を表示する個人用タブを作成すると、Microsoft Teams 開発に簡単に移動できます。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

最初のアプリ プロジェクトToolkitセットアップVisual Studioコードで Microsoft Teams プロジェクトを使用します。

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [機能 **の追加] 画面で、[Tab]** を選択し **、[次へ** ] を **選択します**。
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams プロジェクトを使用してアプリ プロジェクトをToolkit。":::
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。
1. [個人用]**タブオプションのみを** オンにし、画面の下部にある [完了] を選択してプロジェクトを構成します。

## <a name="2-understand-important-app-project-components"></a>2. 重要なアプリ プロジェクト コンポーネントを理解する

ツールキットでプロジェクトを構成すると、Teams の基本的な個人用タブを構築するためのコンポーネントが提供されます。 プロジェクト ディレクトリとファイルは、プロジェクト コードのエクスプローラー領域Visual Studioされます。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="[コード] の [個人用] タブのアプリ プロジェクト ファイルVisual Studioスクリーンショット。":::

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにスキャフォールディング `src` を自動的に作成します。

たとえば、セットアップ中にタブを作成する場合は、アプリの初期化とルーティングを処理するディレクトリ内のファイル `App.js` `src/components` が重要です。 Microsoft [Teams JavaScript クライアント SDK を呼び出](../tabs/how-to/using-teams-client-sdk.md) して、アプリと Teams の間の通信を確立します。

### <a name="app-id"></a>アプリ ID

App Studio でアプリを構成するには、Teams アプリ ID が必要です。 ID は、プロジェクト `teamsAppId` のファイルにあるオブジェクト内で確認 `package.json` できます。

## <a name="3-build-and-run-your-app"></a>3. アプリをビルドして実行する

時間の問題として、アプリをローカルでビルドして実行します。

(この情報はツールキットでも利用 `README` できます)。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。
1. `npm start` を実行します。

完了すると、コンパイルに **成功します。** メッセージが表示されます。 アプリが実行されています `https://localhost:3000` 。

## <a name="4-sideload-your-app-in-teams"></a>4. Teams でアプリをサイドロードする

アプリは Teams でテストする準備が整っています。 これを行うには、アプリのサイドローディングを許可するアカウントが必要です。 (それが確実でない場合は、Teams 開発アカウントを取得する方法 [について説明します](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account))。

> [!TIP]
> アプリをサイドロードする前に、ツールキットに含まれている [App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)の検証機能を使用して問題を確認します。 アプリを正常にサイドロードするには、エラーを修正する必要があります。

1. コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。
1. Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 ( `localhost` ) が信頼できる場所を指定します。
   1. F5 キーを押した後に開いた同じブラウザー ウィンドウ (Google Chrome 既定) で新しいタブ **を開きます**。
   1. ページに `https://localhost:3000/tab` 移動し、ページに進みます。
1. Teams に戻る。 ダイアログで、[追加] **を選択してアプリ** をインストールします。
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている &quot;Hello, World!&quot; 個人用タブ アプリの例を示すスクリーンショット。":::

🎉おめでとうございます。 アプリが Teams で実行されている。

## <a name="next-step"></a>次の手順

作成した個人用タブを展開するか、別の種類の Teams アプリをビルドします。

> [!div class="nextstepaction"]
> [個人用タブに追加する](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
