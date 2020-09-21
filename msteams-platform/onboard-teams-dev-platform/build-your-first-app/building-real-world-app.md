---
title: 初めて Teams アプリの作成を始める
author: heath-hamilton
ms.author: lajanuar
description: 最初の Microsoft Teams アプリを作成するための概要と前提条件
ms.openlocfilehash: 9392096a285a43d3a1f8bed5020e3464da0f7f18
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964702"
---
# <a name="get-started-building-your-first-teams-app"></a>初めて Teams アプリの作成を始める

最初の **アプリ** のレッスンを構築するには、基本的な Teams アプリを作成します。 各チュートリアルでは、シンプルで実際の Teams アプリを構築する方法を説明しながら、一般的なツール、基本概念、およびその他の高度な機能を紹介します。

## <a name="what-youll-learn"></a>学習内容

レッスンを修了した後に知っておくべきことについては、次のアイデアを参照してください。

> [!div class="checklist"]
  >
  > * **Teams ツールキットを使用**して迅速に作業を開始します。 Visual Studio 用の Microsoft Teams toolkit は、アプリプロジェクトとスキャフォールディングを作成するためのものであり、実行中のアプリを数分で利用できるようにします。
  > * **マニフェストを使用**してアプリを定義します。アプリマニフェストは、Teams アプリが使用する機能とサービスを指定する場所です。
  > * **アプリの対象ユーザーの範囲**を作成します。個人利用、グループ作業、またはその両方用の Teams アプリを作成します。
  > * **フレームワークの使用**状況を把握する: アプリをカスタマイズします (たとえば、チームのテーマに合わせて配色を変更するなど)。 Teams の JavaScript SDK のヘルプを参照してください。 また、ボットを作成および管理するための一般的なツールについても説明します。
  > * **アプリの展開**: レッスン全体を通して、よくある関連トピック (認証やデザインのガイドラインなど) について説明します。

## <a name="teams-app-fundamentals"></a>Teams アプリの基礎

チュートリアルを開始する前に、Teams 用のアプリの作成に関する以下の情報を確認する必要があります。

### <a name="apps-can-have-multiple-capabilities"></a>アプリは複数の機能を持つことができる

Teams アプリは、1つ以上の [プラットフォーム機能](../capabilities-overview.md)で構成されています。 これらの機能は、さまざまなチーム固有の [UI コンポーネントと](../doc-links/teams-ui-conventions.md)、カードやタスクモジュールなどの規則を使用して表示できます。

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

    :::image type="content" source="../doc-links/images/upload-custom-app-closeup.png" alt-text="サイドロードオプションビュー":::

<!-- markdownlint-disable MD033 -->
<details>

<summary>サイドロードオプションが表示されない場合や、Teams アカウントを持っていない場合は、<b>ここを選択し</b>ます。</summary>

Microsoft 365 開発者プログラムに参加することによって、アプリのサイドロードを許可する無料の Teams テストアカウントを取得することができます。 (登録プロセスには約2分かかります)。

1. [Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program)に移動します。
1. [ **今すぐ参加** ] を選択し、画面の指示に従います。
1. [ようこそ] 画面が表示されたら、[ **設定] E5 サブスクリプション**を選択します。
1. 管理者アカウントを設定します。 完了すると、次のような画面が表示になります。
:::image type="content" source="../doc-links/images/dev-program-subscription.png" alt-text="開発プログラムのサブスクリプションビュー":::
1. 設定したのと同じ管理者アカウントを使用して Teams にログインします。
1. [ **カスタムアプリをアップロード** する] オプションが選択されているかどうかを確認します。

</details>

### <a name="install-your-development-tools"></a>開発ツールをインストールする

推奨ツールを使用して Teams アプリを構築することはできますが、これらのレッスンでは、Visual Studio Code for the Microsoft Teams Toolkit を使用してすぐに作業を開始する方法を説明します。

Teams では、アプリコンテンツは HTTPS 接続を介してのみ表示されます。 最初のアプリをローカルでホストすることになるため、ngrok を使用して Teams とアプリの間に [セキュリティで保護されたトンネルを設定](../doc-links/debug.md#locally-hosted) する方法について説明します。

1. [Node.js](https://nodejs.org/en/) をインストールします。
1. [Visual Studio Code](https://code.visualstudio.com/download)の最新バージョンをインストールします。 (以前のバージョンは、ツールキットでは動作しない可能性があります)。
1. Visual Studio Code で、左側のアクティビティバーにある [ **拡張機能**] を選択 :::image type="icon" source="../doc-links/images/vs-code-extensions.png"::: し、 **Microsoft Teams Toolkit**をインストールします。
    :::image type="content" source="../doc-links/images/vsc-install-toolkit.png" alt-text="ツールキットビューをインストールする":::
1. [Ngrok](https://ngrok.com/download)をインストールします。

## <a name="next-step"></a>次の手順

アカウントと環境をセットアップしたら、構築を開始できます。

> [!div class="nextstepaction"]
> [最初のアプリをビルドして実行する](../build-your-first-app/build-and-run.md)
