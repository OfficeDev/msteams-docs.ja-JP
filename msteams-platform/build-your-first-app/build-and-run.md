---
title: 開始する - 最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成します。 Microsoft Teams を使用したメッセージToolkit。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093951"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>最初の Microsoft Teams アプリをビルドして実行する

"Hello, World!" を表示する個人用タブを作成して、Microsoft Teams の開発を開始します。
次の手順を使用して、最初の Teams アプリをビルドして実行します。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

最初のアプリ プロジェクトToolkitセットアップVisual Studioコードで Microsoft Teams プロジェクトを使用します。 次の手順を使用して、アプリ プロジェクトを作成します。

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [機能 **の追加] 画面で、[Tab]** を選択し **、[次へ** ] を **選択します**。
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams プロジェクトを使用してアプリ プロジェクトをToolkit。":::
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。
1. [個人用]**タブオプションのみを** オンにし、画面の下部にある [完了] を選択してプロジェクトを構成します。

## <a name="2-understand-important-app-project-components"></a>2. 重要なアプリ プロジェクト コンポーネントを理解する

ツールキットでプロジェクトを構成すると、Teams の基本的な個人用タブを構築するためのコンポーネントが作成されます。 プロジェクト ディレクトリとファイルは、プロジェクト コードのエクスプローラー領域Visual Studioされます。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="[コード] の [個人用] タブのアプリ プロジェクト ファイルVisual Studioスクリーンショット。":::

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

ツールキットは、セットアップ時に追加した機能に基づいて、ディレクトリにスキャフォールディング `src` を自動的に作成します。

たとえば、セットアップ中にタブを作成する場合は、アプリの初期化とルーティングを処理するディレクトリ内のファイル `App.js` `src/components` が重要です。 Microsoft [Teams JavaScript クライアント SDK を呼び出](../tabs/how-to/using-teams-client-sdk.md) して、アプリと Teams の間の通信を確立します。

### <a name="app-id"></a>アプリ ID

Teams アプリ ID を使用して App Studio でアプリを構成します。 プロジェクトのファイルにある `teamsAppId` オブジェクト内の ID を検索 `package.json` します。

## <a name="3-build-and-run-your-app"></a>3. アプリをビルドして実行する

時間を節約するために、ローカルでアプリをビルドして実行します。 この情報は、ツールキットでも利用できます `README` 。 次の手順を使用して、アプリをビルドして実行します。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。
1. `npm start` を実行します。

完了すると、コンパイルに **成功します。** メッセージが表示されます。 アプリが実行されています `https://localhost:3000` 。

## <a name="4-sideload-your-app-in-teams"></a>4. Teams でアプリをサイドロードする

アプリは Teams でテストする準備が整っています。 これを行うには、アプリのサイドローディングを許可する Microsoft 365 開発アカウントが必要です。 アカウントを開く方法について詳しくは、Teams の開発アカウント [をご覧ください](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 

> [!TIP]
> アプリをサイドロードする前に、ツールキットに含まれている [App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)の検証機能を使用して問題を確認します。 エラーを修正して、アプリを正常にサイドローディングします。

次の手順を使用して、Teams でアプリをサイドロードします。

> [!NOTE]
> Teams でアプリをサイドローディングする前にサイドローディングを有効にするには、「アプリのサイドローディングを有効にする」の [手順に従います](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

1. **F5 キーを選択** して、Teams の Web クライアントを Visual Studioします。
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
