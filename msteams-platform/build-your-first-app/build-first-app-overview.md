---
title: 概要 - 最初のアプリの概要と前提条件を構築する
author: heath-hamilton
description: Microsoft Teams アプリ開発を開始し、環境をセットアップする方法について説明します。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 6594ac175cd8ad92c5db399bb675ef3a6b271321
ms.sourcegitcommit: 0e252159f53ff9b4452e0574b759bfe73cbf6c84
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "51762040"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>最初の Microsoft Teams アプリの概要を作成する

開始方法 **のレッスン** では、基本的な Teams アプリを作成する方法について説明します。 各チュートリアルでは、一般的なツール、基本的な概念、より高度な機能を紹介しながら、シンプルで実際の Teams アプリを構築する方法について説明します。

## <a name="what-youll-learn"></a>学習する情報

ここでは、レッスンを行った後に知っている情報を示します。

> [!div class="checklist"]
  >
  > * **Teams Toolkit :** microsoft Teams Toolkit for Visual Studio Code を使用すると、アプリ プロジェクトの作成とスキャフォールディングを迅速に実行し、数分で実行中のアプリを作成できます。
  > * **App Studio を使用してアプリを構成** する: Teams アプリで使用する機能とサービスを指定します。
  > * **アプリの対象ユーザーの範囲**: 個人用、共同作業、または両方の目的で Teams アプリを構築します。
> * **Teams ツールと SDK のエクスペリエンスを取得** する: Teams JavaScript クライアント SDK のヘルプを使用してアプリをカスタマイズします。 たとえば、Teams テーマに合わせてアプリの配色を変更します。 また、ボットを作成および管理するための一般的なツールについて学習します。
  > * **アプリを展開する**: レッスン全体を通じて、興味のある関連トピック (認証や設計ガイドラインなど) が表示されます。

## <a name="teams-app-fundamentals"></a>Teams アプリの基本

チュートリアルを開始する前に、Teams 用アプリの構築について次の情報を知っている必要があります。

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>アプリは複数の機能とエントリ ポイントを持つ可能性があります

Teams アプリは、1 つ以上のプラットフォーム機能 [(ユーザー](../concepts/capabilities-overview.md) がアプリを使用する方法) とエントリ ポイント [(ユーザー](../concepts/extensibility-points.md) がアプリを使用する) で構成されます。

### <a name="teams-doesnt-host-your-app"></a>Teams がアプリをホストしない

Teams アプリには、次の重要な機能が含まれています。

* アプリに電力を供給するロジック、データ ストレージ、API 呼び出し。 これらのサービスは Teams によってホストされていないので、HTTPS 経由でアクセスできる必要があります。
* ユーザーがアプリを使用する Teams クライアント (Web、デスクトップ、またはモバイル)。
* アプリ ID を使用すると、App Studio を使用してアプリを構成できます。

## <a name="get-prerequisites"></a>前提条件の取得

Teams アプリを構築するための適切なアカウントを持ち、推奨される開発ツールをインストールしてください。

### <a name="set-up-your-development-account"></a>開発アカウントを設定する

カスタム アプリのサイドローディングを許可する Teams アカウントが必要です。 (アカウントは既にこれを提供している可能性があります)。

1. Teams アカウントを持っている場合は、Teams でアプリをサイドロードできる場合を確認します。
    1. Teams クライアントで、[アプリ] を **選択します**。
    1. カスタム アプリをアップロードする **オプションを探します**。

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタム アプリをアップロードできる場所を示す図。":::
    
    ボタンが表示されていない場合は、組織でカスタム アプリをアップロードする権限を持つ必要があります。この機能は、無料の Microsoft 365 開発者サブスクリプションにサインアップすることで取得できます。

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>無料の Microsoft 365 開発者サブスクリプションを取得する</b></summary>

Microsoft 365 開発者プログラムに参加することで、アプリのサイドローディングを許可する無料の Teams テスト アカウントを取得できます。 (登録プロセスには約 2 分かかります。

1. [Microsoft 365 開発者プログラムに移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
1. [今 **すぐ参加] を** 選択し、画面の指示に従います。
1. ようこそ画面にアクセスすると **、[E5 サブスクリプションの設定] を選択します**。
1. 管理者アカウントを設定します。 完了すると、次のような画面が表示されます。
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後に表示される例。":::
1. セットアップした管理者アカウントを使用して Teams にログインします。
1. [カスタム アプリをアップロードする **] オプションが追加されたのか確認** します。

</details>

> [!Note]
> それでもアプリをサイドロードできない場合は、「カスタム Teams アプリを有効にする」を参照し、カスタム アプリのアップロード [を有効にするを参照してください](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

### <a name="install-your-development-tools"></a>開発ツールのインストール

お好みのツールを使用して Teams アプリを構築できますが、これらのレッスンでは、Microsoft Teams コードを使用して迅速に開始する方法Toolkit示Visual Studioします。

Teams は、HTTPS 接続を介してアプリのコンテンツのみを表示します。 ボットなど、特定の種類のアプリをローカルでデバッグするには [、ngrok](../concepts/build-and-test/debug.md#locally-hosted) を使用して Teams とアプリの間にセキュリティで保護されたトンネルを設定する方法について説明します。 (Production Teams アプリはクラウドでホストされます)。

1. [Node.js](https://nodejs.org/en/) をインストールします。
1. [ボットまたはメッセージング拡張機能を](https://ngrok.com/download)構築し、ngrok を使用してトンネルを作成する場合は[、ngrok をインストールします](https://docs.microsoft.com/microsoftteams/platform/tutorials/get-started-dotnet-app-studio#tunnel-using-ngrok)。
1. 最新バージョンのコードを [インストールVisual Studioします](https://code.visualstudio.com/download)。 (以前のバージョンはツールキットで動作しない場合があります)。
1. [Visual Studio コード] で、左側の [アクティビティ バー] で [拡張機能] を選択し、Microsoft Teams サーバーをインストール :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: **Toolkit。**

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="コード内の Microsoft Teams Visual Studio拡張機能をインストールできる場所を示Toolkit図。":::

## <a name="about-the-tutorials"></a>チュートリアルについて

まず、Teams の開始レッスン **から始** めましょう。 最初に行く場所が不明な場合は、初心者向けのパスに従って"Hello, World! アプリ。

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Teams の 「始める」 レッスンの学習パスを示すスキル ツリー。" border="false":::

## <a name="next-step"></a>次の手順

アカウントと環境を設定したら、構築を開始できます。

### <a name="beginner-friendly-tutorial"></a>初心者向けチュートリアル

> [!div class="nextstepaction"]
> ["Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>その他のチュートリアル

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [メッセージングの拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)
