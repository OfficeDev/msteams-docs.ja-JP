---
title: 概要 - 最初のアプリの概要と前提条件を構築する
author: heath-hamilton
description: Microsoft Teams アプリの開発を開始し、環境をセットアップする方法について説明します。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 06e26c57e6f6d3fd0bbeb981ef7ab46c8217bb4a
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795462"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>最初の Microsoft Teams アプリの概要を作成する

最初の **アプリのレッスンを構築する** 場合は、基本的な Teams アプリを作成します。 各チュートリアルでは、一般的なツール、基本的な概念、より高度な機能を紹介しながら、シンプルで実際の Teams アプリを構築する方法について説明します。

## <a name="what-youll-learn"></a>学習する情報

ここでは、レッスンを行った後に知っている情報を示します。

> [!div class="checklist"]
  >
  > * **Teams Toolkit**: Microsoft Teams Toolkit for Visual Studio Code を使用すると、すぐにアプリ プロジェクトを作成し、スキャフォールディングを行い、数分で実行中のアプリを作成できます。
  > * **App Studio でアプリを構成** する: Teams アプリで使用する機能とサービスを指定します。
  > * **アプリの対象ユーザーの範囲を設定** する : 個人使用、コラボレーション、または両方の Teams アプリを構築します。
> * **Teams ツールと SDK のエクスペリエンスを得** る : Teams JavaScript クライアント SDK のヘルプを利用してアプリをカスタマイズします。 たとえば、Teams のテーマに合わせてアプリの配色を変更します。 また、ボットを作成および管理するための一般的なツールについて学習します。
  > * **アプリを展開** する: 授業全体を通じて、関心のある関連トピック (認証や設計ガイドラインなど) を確認できます。

## <a name="teams-app-fundamentals"></a>Teams アプリの基本

チュートリアルを開始する前に、Teams 用アプリの構築に関する以下の情報を知っている必要があります。

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>アプリは複数の機能とエントリ ポイントを持つ場合があります。

Teams アプリは、1 つ以上のプラットフォーム機能 [(ユーザー](../concepts/capabilities-overview.md) がアプリを使用する方法) とエントリ ポイント [(ユーザー](../concepts/extensibility-points.md) がアプリを検出する場所) で構成されます。

### <a name="teams-doesnt-host-your-app"></a>Teams がアプリをホストしない

Teams アプリには、次の重要な部分が含まれています。

* アプリを起動するロジック、データ ストレージ、API 呼び出し。 これらのサービスは Teams によってホストされていないので、HTTPS 経由でアクセスできる必要があります。
* ユーザーがアプリを使用する Teams クライアント (Web、デスクトップ、またはモバイル)。
* App Studio でアプリを構成できるアプリ ID。

## <a name="get-prerequisites"></a>前提条件を取得する

Teams アプリを構築するための適切なアカウントを持ち、推奨される開発ツールをインストールしてください。

### <a name="set-up-your-development-account"></a>開発アカウントをセットアップする

カスタム アプリのサイドローディングを許可する Teams アカウントが必要です。 (お客様のアカウントで既に提供されている場合があります。

1. Teams アカウントを持っている場合は、Teams でアプリをサイドロードできる場合は、次の手順を実行します。
    1. Teams クライアントで、[アプリ] を **選択します**。
    1. カスタム アプリをアップロード **するオプションを探します**。

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams 内でカスタム アプリをアップロードできる場所を示す図。":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>サイドロード</b> オプションが表示できない場合、または Teams アカウントを持たなかった場合は、ここで選択します。</summary>

Microsoft 365 開発者プログラムに参加することで、アプリのサイドローディングを許可する無料の Teams テスト アカウントを取得できます。 (登録プロセスには約 2 分かかります)。

1. [Microsoft 365 開発者プログラムに移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
1. [ **今すぐ参加] を** 選択し、画面の指示に従います。
1. ようこそ画面にアクセスし、[E5 サブスクリプションのセットアップ **] を選択します**。
1. 管理者アカウントを設定します。 完了すると、次のような画面が表示されます。
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後に表示される例。":::
1. セットアップした管理者アカウントを使用して Teams にログインします。
1. [カスタム アプリのアップロード] **オプションが表示されたのか確認** します。

</details>

> [!Note]
> If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).

### <a name="install-your-development-tools"></a>開発ツールをインストールする

Teams アプリは好みのツールで構築できますが、これらのレッスンでは、Microsoft Teams Toolkit for Visual Studio Code を使用してすぐに開始する方法を説明します。

Teams は、HTTPS 接続を通じてのみアプリのコンテンツを表示します。 ボットなど、特定の種類のアプリをローカルでデバッグするには [、ngrok](../concepts/build-and-test/debug.md#locally-hosted) を使用して Teams とアプリの間のセキュリティで保護されたトンネルを設定する方法について説明します。 (Production Teams アプリはクラウドでホストされます。

1. [Node.js](https://nodejs.org/en/) をインストールします。
1. ボット [またはメッセージング拡張機能を](https://ngrok.com/download) 構築する予定の場合は、ngrok をインストールします。
1. 最新バージョンの Visual Studio [Code をインストールします](https://code.visualstudio.com/download)。 (以前のバージョンでは、このツールキットでは動作しない可能性があります)。
1. [Visual Studioコード] で、左側のアクティビティ バーの [拡張機能] を選択し :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: **、Microsoft Teams** Toolkit。

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="コード内で Microsoft Teams Visual Studio拡張機能をインストールできる場所を示Toolkit図。":::

## <a name="about-the-tutorials"></a>チュートリアルについて

どの Teams でも、最初のアプリの **レッスンを構築できます** 。 最初の場所が不明な場合は、初心者向けのパスに従って"Hello, World!" を構築します。 app.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Teams の「最初のアプリを構築する」チュートリアルのラーニング パスを示すスキル ツリー。" border="false":::

## <a name="next-step"></a>次の手順

アカウントと環境を設定したら、構築を開始できます。

### <a name="beginner-friendly-tutorial"></a>初心者向けのチュートリアル

> [!div class="nextstepaction"]
> ["Hello, World!" アプリを構築する](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>その他のチュートリアル

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [メッセージングの拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)
