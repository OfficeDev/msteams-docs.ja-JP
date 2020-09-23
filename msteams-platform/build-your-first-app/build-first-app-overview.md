---
title: 最初の Teams アプリの作成を始める
author: heath-hamilton
description: 最初の Microsoft Teams アプリを構築するための概要と前提条件
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: bcfbcaa9de85f4b7135483aed3d1d11bf8bffad6
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210181"
---
# <a name="building-your-first-teams-app-overview"></a>最初の Teams アプリの概要を作成する

最初の **アプリ** のレッスンを構築するには、基本的な Teams アプリを作成します。 各チュートリアルでは、一般的なツール、基本概念、および高度な機能について紹介しながら、簡単な現実世界の Teams アプリを構築する方法について順を追って説明します。

## <a name="what-youll-learn"></a>学習内容

レッスンを修了した後に知っておくべきことについては、次のアイデアを参照してください。

> [!div class="checklist"]
  >
  > * **Teams ツールキットを使用**して迅速に作業を開始します。 Visual Studio 用の Microsoft Teams toolkit は、アプリプロジェクトとスキャフォールディングを作成するためのものであり、実行中のアプリを数分で利用できるようにします。
  > * **マニフェストを使用**してアプリを定義します。アプリマニフェストは、Teams アプリが使用する機能とサービスを指定する場所です。
  > * **アプリの対象ユーザーの範囲**を作成します。個人利用、グループ作業、またはその両方用の Teams アプリを作成します。
  > * Teams**フレームワークを使用**して作業を開始します。アプリをカスタマイズする (たとえば、チームのテーマに合わせて配色を変更するなど)、TEAMS JavaScript SDK のヘルプを参照してください。 また、ボットを作成および管理するための一般的なツールについても説明します。
  > * **アプリの展開**: レッスン全体を通して、よくある関連トピック (認証やデザインのガイドラインなど) について説明します。

## <a name="teams-app-fundamentals"></a>Teams アプリの基礎

チュートリアルを開始する前に、Teams 用のアプリの作成に関する以下の情報を確認する必要があります。

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>アプリには複数の機能とエントリポイントを含めることができます。

Teams アプリは、1つ以上の [プラットフォーム機能](../concepts/capabilities-overview.md) と [エントリポイント](../concepts/extensibility-points.md)で構成されます。 さまざまなチーム固有の [UI コンポーネントと](../concepts/extensibility-points.md#ui-components)、カードやタスクモジュールなどの規則を使用して、アプリを提示することができます。

### <a name="teams-doesnt-host-your-app"></a>Teams がアプリをホストしていない

Teams アプリには、次の3つの重要な要素があります。

* アプリに電力を供給するロジック、データストレージ、および API 呼び出し。 これらのサービスは Teams でホストされるものではなく、HTTPS 経由でアクセスできる必要があります。
* ユーザーがアプリを使用する Teams クライアント (web、デスクトップ、またはモバイル)。
* アプリパッケージ。 Teams にアプリをインストールするために使用します。 このファイルには、ホストされているサービスへのアプリケーションメタデータとポインターが含まれています。

## <a name="get-prerequisites"></a>前提条件を取得する

Teams アプリを作成するための適切なアカウントを持っており、いくつかの推奨される開発ツールをインストールしていることを確認します。

### <a name="set-up-your-development-account"></a>開発アカウントをセットアップする

カスタムアプリのサイドロードを許可する Teams アカウントが必要です。 (アカウントで既に提供されている場合があります。)

1. Teams アカウントを所有している場合は、Teams でアプリをサイドロードできるかどうかを確認します。
    1. Teams クライアントで、[ **アプリ**] を選択します。
    1. **カスタムアプリをアップロード**するオプションを探します。

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Teams でカスタムアプリをアップロードできる場所を示す図":::

<!-- markdownlint-disable MD033 -->
<details>

<summary>サイドロードオプションが表示されない場合や、Teams アカウントを持っていない場合は、<b>ここを選択し</b>ます。</summary>

Microsoft 365 開発者プログラムに参加することによって、アプリのサイドロードを許可する無料の Teams テストアカウントを取得することができます。 (登録プロセスには約2分かかります)。

1. [Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program)に移動します。
1. [ **今すぐ参加** ] を選択し、画面の指示に従います。
1. [ようこそ] 画面が表示されたら、[ **設定] E5 サブスクリプション**を選択します。
1. 管理者アカウントを設定します。 完了すると、次のような画面が表示になります。
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後の表示例。":::
1. 設定したのと同じ管理者アカウントを使用して Teams にログインします。
1. [ **カスタムアプリをアップロード** する] オプションが選択されているかどうかを確認します。

</details>

### <a name="install-your-development-tools"></a>開発ツールをインストールする

推奨ツールを使用して Teams アプリを構築することはできますが、これらのレッスンでは、Visual Studio Code for the Microsoft Teams Toolkit を使用してすぐに作業を開始する方法を説明します。

Teams では、アプリコンテンツは HTTPS 接続を介してのみ表示されます。 最初のアプリをローカルにホストして時間を節約するので、ngrok を使用して Teams とアプリの間に [セキュリティで保護されたトンネルを設定](../concepts/build-and-test/debug.md#locally-hosted) する方法について説明します。 (運用レベルの Teams アプリは、クラウドでホストされます。)

1. [Node.js](https://nodejs.org/en/) をインストールします。
1. [Ngrok](https://ngrok.com/download)をインストールします。
1. [Visual Studio Code](https://code.visualstudio.com/download)の最新バージョンをインストールします。 (以前のバージョンは、ツールキットでは動作しない可能性があります)。
1. Visual Studio Code で、左側のアクティビティバーにある [ **拡張機能**] を選択 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: し、 **Microsoft Teams Toolkit**をインストールします。
    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Visual Studio Code の場所を示す図は、Microsoft Teams ツールキットの拡張機能をインストールできます。":::

## <a name="about-the-tutorials"></a>チュートリアルについて

**最初のアプリ**レッスンを構築する Teams のいずれかで開始できます。 最初にどこに行くべきかがわからない場合は、初心者フレンドリパスに従って "Hello, World!" を作成します。 アプリ.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Teams ' 最初のアプリのチュートリアルを構築するための学習パスを示すスキルツリー。" border="false":::

## <a name="next-step"></a>次のステップ

アカウントと環境をセットアップしたら、構築を開始できます。

### <a name="beginner-friendly-tutorial"></a>初心者フレンドリなチュートリアル

> [!div class="nextstepaction"]
> ["Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>その他のチュートリアル

> [!div class="nextstepaction"]
> [Bot を構築する](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [メッセージング拡張機能を構築する](../build-your-first-app/build-messaging-extension.md)