---
title: "\"Hello, World!\" をビルドして実行します。 Teams アプリ"
author: heath-hamilton
description: 最初の Microsoft Teams アプリ、つまり "Hello, World!" を表示する個人用タブを作成して実行します。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 5be2e8f2932a91ed11137f3a7be544e12bd65559
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210248"
---
# <a name="build-a-hello-world-teams-app"></a>"Hello, World!" を作成します。 Teams アプリ

"Hello, World!" と表示される個人タブを作成することによって、Microsoft Teams プラットフォーム開発に直接ジャンプできます。

## <a name="create-your-app-project"></a>アプリプロジェクトを作成する

最初のアプリプロジェクトをセットアップするには、Visual Studio Code の Microsoft Teams ツールキットを使用します。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="Visual Studio Code Teams ツールキットを使用して新しいアプリを作成する方法を示すスクリーンショット。":::
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)
1. [ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ**] の順に選択します。
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Visual Studio Code Teams Toolkit を使用してアプリプロジェクトを構成する方法を示すスクリーンショット。":::
1. [ **個人用] タブ** のオプションを確認し、画面の下部にある [ **完了** ] を選択してプロジェクトを構成します。

## <a name="understand-important-app-project-components"></a>重要なアプリプロジェクトコンポーネントについて理解する

ツールキットによってプロジェクトが構成されると、Teams 用の基本的な個人用タブを作成するためのコンポーネントが用意されます。 プロジェクトのディレクトリとファイルは、Visual Studio Code のエクスプローラー領域に表示されます。

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Visual Studio Code の [個人用] タブのアプリプロジェクトファイルを示すスクリーンショット。":::

Teams アプリ開発者が扱う主要なファイルのいくつかについて理解しておきましょう。

### <a name="app-manifest-manifestjson"></a>アプリマニフェスト ( `manifest.json` )

アプリケーションマニフェストは、ディレクトリに配置されており、 `.publish` アプリプロジェクトの開始点となります。 マニフェストは、アプリの基本属性を定義し、必要なリソースをポイントします。 アプリをインストールすると、チームはマニフェストを解析して、アプリをクライアントにレンダリングする方法を理解します。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。

たとえば、セットアップ時にタブを作成した場合、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。 [Microsoft TEAMS SDK](../tabs/how-to/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立します。

### <a name="app-package-developmentzip"></a>アプリパッケージ ( `Development.zip` )

このディレクトリには、アプリパッケージを作成して、アプリ `.publish` を Teams に [サイドロード](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) する必要があります。 このパッケージは、 [組織のアプリカタログ](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) または [appsource](../concepts/deploy-and-publish/appsource/publish.md)に発行するときにも使用されます。

アプリパッケージファイルの詳細については、以下を参照してください。

|名前|型|Size|マニフェストの場所|ツールキットのファイル名|
|---|---|:---:|:---:|-----|
|**アプリマニフェスト**|`.json`| — | — |`.publish/manifest.json`|
|**色のロゴ**|`.png`|192 &times; 192 ピクセル|`icon.color`|`.publish/color.png`|
|**アウトラインロゴ**|`.png`|32 &times; 32 ピクセル|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a>アプリを実行する

時間の経過とともに、アプリをローカルでビルドして実行します。

(この情報は、ツールキットでも利用でき `README` ます。)

1. ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。
1. `npm start` を実行します。 完了すると、**コンパイルに成功**しました。 ターミナルのメッセージ。
1. ブラウザーを開き、に移動して、 `https://localhost:3000` **Microsoft Teams タブ**という名前の空の web ページを表示します。(ページ上にコンテンツが表示されないことを心配しないでください)。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="実行中のアプリをブラウザーで表示するときの外観を示すスクリーンショット。":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a>アプリへのセキュリティで保護されたトンネルの設定

アプリは、ローカル web サーバー上で実行されています。 Teams でアプリを実行するには、HTTPS を介してアクセスできるようにする必要があり `localhost` ます。

[Ngrok](https://ngrok.com/download)をまだインストールしていない場合はインストールします。 このツールを実行すると、ローカル web サーバーを指す、グローバルに使用できる2つの Url が作成さ `http://localhost:3000` れます ()。 で始まる転送 URL が必要 `HTTPS` です。

1. 新しいターミナルを開き、を実行 `ngrok http 3000` します。
1. 提供されている HTTPS URL をコピーします (次の例を参照してください)。
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="Ngrok を実行しているターミナルを示すスクリーンショット。":::
1. ディレクトリで `.publish` 、を開き `Development.env` ます。
1. 値を `baseUrl0` コピーした URL に置き換えます。 (たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ba5.ngrok.io` します)。

アプリのマニフェストは、アプリをホストしている場所を指すようになります。

## <a name="sideload-your-app-in-teams"></a>Teams でのアプリのサイドロード

アプリを実行し、HTTPS を介してアクセスできるようにすると、そのアプリを Teams にアップロードする準備ができました。

> [!TIP]
> アプリのサイドロード前に、 [ツールキットの検証機能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)を使用して問題がないかどうかを確認します。 アプリケーションを正常にサイドロードするには、エラーを修正する必要があります。

1. アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。 (あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。
1. [ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。
1. アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。 インストールモーダルが表示されます。
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="Teams アプリのインストールモーダルの例を示すスクリーンショット。":::
1. [ **追加** ] を選択してアプリをインストールします。
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="Teams で実行されている ' Hello, World! ' personal tab アプリの例を示すスクリーンショット。":::

おめでとうございます🎉 アプリは Teams で実行されています。

## <a name="next-step"></a>次のステップ

作成したばかりの [個人] タブを展開するか、別の種類の Teams アプリを作成します。

> [!div class="nextstepaction"]
> [[個人用] タブに追加する](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [[チャネル] タブを作成する](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [Bot を構築する](../build-your-first-app/build-bot.md)
