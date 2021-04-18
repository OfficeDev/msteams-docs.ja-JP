---
title: はじめに - 最初のアプリを構築して実行する
author: heath-hamilton
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 Microsoft Teams のツールキットを使用したメッセージ。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093951"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>最初の Microsoft Teams アプリを構築して実行する

"こんにちは!!" を表示する個人タブを構築することから Microsoft Teams の開発を開始します。
以下の手順で、最初の Teams アプリを構築して実行します。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Visual Studio Code で Microsoft Teams ツールキットを使用して、最初のアプリ プロジェクトを設定します。 以下の手順でアプリ プロジェクトを作成します。

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。
1. [**機能の追加**] 画面で、[**タブ**] を選択し、[**次へ**] を選択します。
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams ツールキットを使用して、アプリ プロジェクトを構成する方法を示すスクリーンショット。":::
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカル コンピューター上のアプリのプロジェクト ディレクトリの名前でもあります)。
1. [**個人用タブ**] オプションのみをチェックし、画面下の [**終了**] を選択して、プロジェクトを構成します。

## <a name="2-understand-important-app-project-components"></a>2. アプリ プロジェクトの重要なコンポーネントを理解する

ツールキットでプロジェクトを構成すると、Teams 向けの基本的な個人用タブを構築するためのコンポーネントがあります。 プロジェクトのディレクトリとファイルには、Visual Studio Code の [エクスプローラー] 領域に表示されます。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code で個人用タブ向けのアプリのプロジェクト ファイルを表示したスクリーンショット。":::

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

ツールキットは、セットアップ時に追加した機能に基づいて、`src` ディレクトリにスキャフォールディングを自動的に作成します。

たとえば、セットアップ中にタブを作成した場合、`src/components` ディレクトリ内の `App.js` ファイルは、アプリの初期化とルーティングを処理するため重要です。 [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) を呼び出して、アプリと Teams の間の通信を確立します。

### <a name="app-id"></a>アプリ ID

Teams アプリ ID を使用して、App Studio でアプリを構成します。 プロジェクトの `package.json` ファイルにある `teamsAppId` オブジェクトで ID を検索します。

## <a name="3-build-and-run-your-app"></a>3. アプリの構築と実行

アプリをローカルに構築して実行することで、時間を節約できます。 この情報は、ツールキット `README` でも参照できます。 以下の手順を使用して、最初のアプリを構築して実行します。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。
1. `npm start` を実行します。

完了すると、[**正常にコンパイルされました**] と表示されます。 ターミナルのメッセージ。 お使いのアプリは `https://localhost:3000` で動作しています。

## <a name="4-sideload-your-app-in-teams"></a>4. Teams でアプリをサイドロードする

お使いのアプリは Teams でテストする準備ができています。 そのためには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。 アカウント開設の詳細については、「[Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)」を参照してください。 

> [!TIP]
> ツールキットに含まれる [App Studio の検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool) を使用して、アプリをサイドロードする前に問題がないか確認します。 エラーを修正して、アプリを正常にサイドロードします。

以下の手順を使用して、Teams でアプリをサイドロードします。

> [!NOTE]
> Teams でアプリをサイドロードする前にサイドロードを有効にするには、[[アプリのサイドロードをオンにする](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)] の手順に従ってください。

1. **F5** キーを選択すると、Visual Studio Code で Teams Web クライアントが起動します。
1. アプリ コンテンツを Teams で表示するには、信頼できるアプリを実行する場所 (`localhost`) を指定します。
   1. **F5** を押した後に開いたのと同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブを開きます。
   1. `https://localhost:3000/tab` に進み、ページを進めます。
1. Teams に戻ります。 ダイアログで [**自分に追加**] を選択して、アプリをインストールします。
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で動作する個人用タブ アプリの ' こんにちは! ' の例を表示するスクリーンショット。":::

🎉 おめでとうございます! お使いのアプリは Teams で動作しています。

## <a name="next-step"></a>次の手順

先ほど作成した個人用タブの拡張や別のタイプの Teams アプリを作成します。

> [!div class="nextstepaction"]
> [個人用タブに追加](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
