---
title: 最初の Teams アプリを構築して実行する
author: heath-hamilton
description: 最初の Microsoft Teams アプリを実行します。
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652106"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a>最初の Microsoft Teams アプリを構築して実行する

基本的なアプリをすばやく構築して実行することにより、Microsoft Teams プラットフォームでの開発にすぐにジャンプできます。

> [!NOTE]
> このチュートリアルを実行する際には、JavaScript (特に反応する) についての実用的な知識を持っていると便利です。

## <a name="set-up-your-development-account"></a>開発アカウントをセットアップする

Teams 用のアプリを構築するには、サイドローディングを許可する Teams アカウントが必要です (アカウントで既に提供されている場合があります)。 そうでない場合は、Microsoft 365 開発者向けサブスクリプションに登録して、テストテナントを取得できるようにします。

1. Teams でアプリをサイドロードできるかどうかを確認します。
    1. Teams クライアントで、[**アプリ**] を選択します。
    1. **カスタムアプリをアップロード**するオプションを探します。
1. このオプションを使用している場合は、作成を開始できます。 そうでない場合は、次の操作を行います。
    1. [Microsoft 365 開発者向けサブスクリプション](../doc-links/prepare-your-o365-tenant.md)に登録します。
    1. テストアカウントの[カスタムアプリのサイドロードを有効に](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)します。

## <a name="get-your-development-tools"></a>開発ツールを入手する

好みのツールで Teams アプリを構築することができますが、ここでは、Visual Studio Code と Microsoft Teams Toolkit を使用してすぐに作業を開始するために必要な情報を紹介します。

1. [Visual Studio Code](https://code.visualstudio.com/download)の最新バージョンをインストールします。
1. Visual Studio Code で、 **Extensions** ![ 左側のアクティビティバーにある [visual studio ツールキットビュー] を選択し、 ](../doc-links/images/vs-code-extensions.png) **Microsoft Teams toolkit**をインストールします。
1. [Node.js](https://nodejs.org/en/) をインストールします。

## <a name="create-an-app-project"></a>アプリプロジェクトを作成する

Microsoft Teams Toolkit は、最初のアプリプロジェクトをセットアップするのに役立ちます。

1. Visual Studio Code で、[Teams] アイコンを選択してツールキットを開きます。 ![teams アイコン](../doc-links/images/favicon-16x16.png) 左側のアクティビティバー
1. [**新しい Teams アプリの作成**] を選択します。
1. メッセージが表示されたら、アプリの名前を入力します。 これは、アプリの既定の名前であり、ローカルコンピューター上のプロジェクトディレクトリの名前でもあります。
1. [**機能の追加**] 画面で、[**タブ]** 、[**次へ**] の順に選択します。
1. [**個人用] タブ**のオプションを確認し、[**完了**] を選択してプロジェクトを構成します。

![ツールキットのタブの追加ビュー](../doc-links/images/toolkit-add-tabs.PNG)

完了したら、個人タブを作成するためのアプリのスキャフォールディングコンポーネントが用意されています。

## <a name="run-your-app"></a>アプリを実行する

プロジェクトの「」の手順に従って、 `README.md` アプリを作成、実行、および展開します。 一般的に、次の手順を実行するのに役立ちます。

* アプリをホスト `localhost` します。
* Teams がアプリにアクセスできるように、 [ngrok を使用してセキュリティで保護されたトンネルを設定](../doc-links/debug.md#locally-hosted)します。 ( [Ngrok](https://ngrok.com/download)をインストールします。)
* フォルダーのを使用して、アプリを Teams クライアントで[サイドロード](../doc-links/apps-upload.md)し `Development.zip` `.publish` ます。

アプリのサイドロードが完了すると、Teams クライアントでこのように表示されます。

![Hello world の例タブ](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a>重要なアプリプロジェクトファイル

アプリプロジェクトとスキャフォールディングを設定したら、Teams アプリ開発者が扱う主要なファイルの一部について理解しておきましょう。

### <a name="app-manifest-manifestjson"></a>アプリマニフェスト ( `manifest.json` )

アプリケーションマニフェストは、ディレクトリに配置されており、 `.publish` アプリプロジェクトの開始点となります。 マニフェストは、アプリの基本属性を定義し、必要なリソースをポイントします。 アプリをインストールすると、チームはマニフェストを解析して、アプリをクライアントにレンダリングする方法を理解します。

次のチュートリアルでは、個人およびチャネルのタブを作成するためのアプリマニフェストのセクションに重点を置いて説明します。

### <a name="package-developmentzip"></a>Package ( `Development.zip` )

また、ディレクトリにあるアプリパッケージを使用して、 `.publish` アプリを Teams に[サイドロード](../../overview.md#how-can-you-share-your-teams-app)する必要があります。 [組織のアプリカタログ](../../overview.md#how-can-you-share-your-teams-app)または[appsource](../../concepts/deploy-and-publish/appsource/publish.md)に発行するときにも使用されます。

アプリパッケージファイルの詳細については、以下を参照してください。

|Name|型|Size|マニフェストの場所|ツールキットのファイル名|
|---|---|:---:|:---:|-----|
|**アプリマニフェスト**|`.json`| — | — |`.publish/manifest.json`|
|**色のロゴ**|`.png`|192 &times; 192 ピクセル|`icon.color`|`.publish/color.png`|
|**アウトラインロゴ**|`.png`|32 &times; 32 ピクセル|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a>スキャフォールディング ( `src` )

このツールキットは、 `src` セットアップ時に追加された機能に基づいてディレクトリ内に自動的にスキャフォールディングを作成します。

ただし、どのような種類のアプリであっても、どのような種類のファイルも作成されません。 たとえば、 `App.js` ディレクトリ内のファイル `src/components` は、アプリの初期化とルーティングを処理するので重要です。 最も重要なのは、 [Microsoft TEAMS SDK](../doc-links/using-teams-client-sdk.md)を呼び出して、アプリと teams 間の通信を確立することです。

スキャフォールディングの詳細については、「個人用およびチャネルのタブを作成するためのチュートリアル」を参照してください。

## <a name="next-step"></a>次の手順

おめでとうございます🎉 Teams アプリが実行されている。 実際の機能を追加する方法については、次のボタンを選択してください。

> [!div class="nextstepaction"]
> [[個人用] タブを作成する](add-personal-tab.md)
