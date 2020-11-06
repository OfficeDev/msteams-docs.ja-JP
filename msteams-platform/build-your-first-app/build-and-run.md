---
title: 作業の開始-最初のアプリをビルドして実行する
author: heath-hamilton
description: "\"Hello, World!\" を表示する Microsoft Teams アプリをすばやく作成する Microsoft Teams ツールキットを使用したメッセージ。"
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931779"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>最初の Microsoft Teams アプリを構築して実行する

"Hello, World!" と表示される個人タブを作成することによって、Microsoft Teams 開発に直接ジャンプできます。

## <a name="1-create-your-app-project"></a>1. アプリプロジェクトを作成します。

最初のアプリプロジェクトをセットアップするには、Visual Studio Code の Microsoft Teams ツールキットを使用します。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成** ] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ** ] の順に選択します。
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams Toolkit を使用してアプリプロジェクトを構成する方法を示すスクリーンショット。":::
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)
1. [ **個人用] タブ** のオプションのみをチェックし、画面の下部にある [ **完了** ] を選択してプロジェクトを構成します。

## <a name="2-understand-important-app-project-components"></a>2. 重要なアプリプロジェクトコンポーネントを理解する

ツールキットによってプロジェクトが構成されると、Teams 用の基本的な個人用タブを作成するためのコンポーネントが用意されます。 プロジェクトのディレクトリとファイルは、Visual Studio Code のエクスプローラー領域に表示されます。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code の [個人用] タブのアプリプロジェクトファイルを示すスクリーンショット。":::

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。

たとえば、セットアップ時にタブを作成した場合、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。 [Microsoft TEAMS SDK](../tabs/how-to/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立します。

### <a name="app-id"></a>アプリ ID

Teams アプリ ID は、アプリをアプリ Studio で構成するために必要です。 ID は、 `teamsAppId` プロジェクトのファイル内にあるオブジェクトで見つけることができ `package.json` ます。

## <a name="3-build-and-run-your-app"></a>3. アプリをビルドして実行します。

時間の経過とともに、アプリをローカルでビルドして実行します。

(この情報は、ツールキットでも利用でき `README` ます。)

1. ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。
1. `npm start` を実行します。

完了すると、 **コンパイルに成功** しました。 ターミナルのメッセージ。 アプリが実行されている `https://localhost:3000` 。

## <a name="4-sideload-your-app-in-teams"></a>4. アプリを Teams でサイドロード

アプリは Teams でテストする準備ができています。 これを行うには、アプリのサイドロードを許可するアカウントが必要です。 (あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。

> [!TIP]
> アプリのサイドロード前に、ツールキットに含まれている [アプリ Studio の検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)を使用して、問題点を確認します。 アプリケーションを正常にサイドロードするには、エラーを修正する必要があります。

1. Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。
1. Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 () を信頼するように指定し `localhost` ます。
   1. **F5** キーを押した後に開いた同じブラウザーウィンドウ (既定では Google Chrome) で新しいタブを開きます。
   1. に移動 `https://localhost:3000/tab` して、ページに進みます。
1. Teams に戻ります。 ダイアログボックスで、[ **追加** ] を選択してアプリをインストールします。
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている ' Hello, World! ' personal tab アプリの例を示すスクリーンショット。":::

おめでとうございます🎉 アプリは Teams で実行されています。

## <a name="next-step"></a>次の手順

作成したばかりの [個人] タブを展開するか、別の種類の Teams アプリを作成します。

> [!div class="nextstepaction"]
> [[個人用] タブに追加する](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
