---
title: Microsoft Teams と Microsoft Teams のアプリをToolkitアプリをVisual Studio
description: Microsoft Teams アプリを使用して、Visual Studio 内で直接カスタム アプリを構築Toolkit
keywords: teams visual studio Toolkit
ms.topic: overview
ms.openlocfilehash: 79ea22cfd154313247132c22684d444c0813c66f
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819204"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>Microsoft Teams と Microsoft Teams のアプリをToolkitアプリをVisual Studio

Microsoft Teams の展開Toolkitカスタムの Teams アプリをカスタム統合開発環境 (IDE) 内Visual Studio作成することができます。 Microsoft Teams ツールキットには、プロセス全体が示され、Teams アプリの構築、デバッグ、起動に必要なものがすべて含まれます。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. このプロジェクト パーツ **<span>ASP.NE</span>と Web 開発モジュールが** ユーザーのクラス インスタンスに追加Visual Studioします。 ワークロードおよびコンポーネントのドキュメントを追加または削除する [Visual Studio手順を実行することで、確認](/visualstudio/install/modify-visual-studio?view=vs-2019) できます。

![Visual Studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. アプリを Visual Studio から展開してテストする場合は、開発環境で IIS (インターネット インフォメーション サービス) をインストールする必要があります。 Visual Studioは IIS を含まれていません。既定の Windows 10 構成、Windows 8 構成、Windows 7 構成には含まれていません。ただし、最新バージョンは、Microsoft ダウンロード センター [からダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Teams モードをインストールToolkit

Microsoft Teams Toolkit for Visual Studioは [、Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) からダウンロードするか、Visual Studio に含まれる **[拡張機能]** メニューから直接ダウンロードVisual Studio。

## <a name="using-the-toolkit"></a>ツールキットを使用する

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [Teams でアプリを実行する](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリの発行](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. [新 **しいプロジェクトの作成] を選択します**。
1. **[Microsoft Teams アプリ] を選択し、[** 次へ] を**選択します**。
1. [新しいプロジェクトを構成**します] 画面に表示**されます。この画面では、プロジェクト名、**場所、****および**ソリューション名**を選択できます**。
1. 同じディレクトリ内の **"Place solution" ボックスと "Project" というボックスをオンにします**。
1. [機能の追加] という **ポップアップ** ウィンドウを使用すると、プロジェクトのセットアップに関する 1 つ以上の機能を選択できます。
1. [次へ **] ボタン** を選択して構成プロセスを完了します。
1. ポップアップ ウィンドウの [機能の **追加]** が表示されていると、選択した各機能のプロパティを選択できます。
1. [ **完了]** を選択すると **、Microsoft Teams** のランToolkit表示されます。

## <a name="configure-your-app"></a>アプリを構成する

Teams アプリの中心には、Teams アプリは 3 つのコンポーネントを使用します。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、モバイル)。
  1. TEAMS に表示されるコンテンツの要求に応答するサーバー(HTML タブ コンテンツ、ボット アダプティブ カードなど)。
  1. 3 つの [ファイルで](/concepts/build-and-test/apps-package.md) 構成される Teams アプリ パッケージ:

  > [!div class="checklist"]
  >
  > - メッセージmanifest.jsオン
  > - アプリ [がパブリック](../resources/schema/manifest-schema.md#icons) または組織のアプリ カタログに表示するための色アイコン
 > - Teams [のアクティビティ](../resources/schema/manifest-schema.md#icons) バーに表示されるアウトライン アイコン。

アプリがインストールされると、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を判断します。

> [!NOTE]
>Microsoft 365 またはアカウントにサインインしていない場合は、開発プロセスを続行するには Microsoft 365 またはアカウントにサインインする必要があります。
>
> Microsoft 365 アカウントをお持ての場合は [、Microsoft 365 開発者プログラム サブスクリプションにサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。 無料版 *は* 90 日間無料で、開発アクティビティに使用している限り、引き続き更新されます。 Visual Studio *Enterprise* または *Professional* サブスクリプションをお持つの場合、両方のプログラムに無料の Microsoft 365 [開発者サブスクリプションが含](https://aka.ms/MyVisualStudioBenefits)まれており、そのサブスクリプションの期間Visual Studioアクティブになります。 *Microsoft* [365 開発者サブスクリプションのセットアップを参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。
>

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには **、[Microsoft Teams およびランド処理] Toolkit ページで、[アプリ パッケージの** 編集 **] を選択します** 。
1. [My **Environments] ドロップダウン メニュー** から [開発] を **選択します**。
1. アプリの詳細ページが **表示され** 、アプリのプロパティ フィールドを編集できます。
1. アプリの詳細ページのフィールドを編集すると、ファイルに保存されている manifest.jsの内容が更新されます。この内容は、最終的にはアプリ パッケージに含まれます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの詳細 **ページを変更** したり、マニフェスト **を更新**したり **、アプリの .publish** フォルダーにある  **.env** ファイルを更新したりすると、ファイルが自動的 **Development.zip** されます。 ファイルDevelopment.zipは、3 つの必須ファイル (オンおよび 2**つのアイコン ファイルmanifest.js含**[まれています](../concepts/build-and-test/apps-package.md#icons)。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

1. [ソリューション構成 **] ドロップダウン メニュー** から、[展開] を **選択します**。

![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

2. **[ISS Express + Teams] ボタンを選択**します。

1. Teams が起動し、アプリのインストール ダイアログが Teams クライアントに表示されます。

## <a name="validate-your-app"></a>アプリを検証する

[ **検証]** ページでは、AppSource にアプリを提出する前にアプリ パッケージをチェックすることができます。 マニフェスト パッケージと検証ツールは、単にマニフェストに関連するすべてのテスト ケースに対してアプリをチェックします。 失敗した各テストについて、説明にはエラーの修正に役立つドキュメントへのリンクが示されています。 自動化が簡単なテストの場合、テストが**Preliminary checklist**失敗する最も一般的なテスト ケースの暫定的なチェックリストの詳細 7 と、提出チェックリスト全体へのリンクが含まれています。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に発行する

✔ ホーム ページで、アプリをチームにアップロードしたり、組織内のユーザー用にアプリを会社のカスタム アプリ ストアに提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出したりできます。

✔の IT 管理者がこれらの申請を確認します。

✔ページに戻り **、提出** のステータスを確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認できます。これは、アプリに更新プログラムを提出したり、現在アクティブな提出を取り消す場合にも使用できます。

> [!div class="nextstepaction"]
> [次の手順: 公開されたアプリの管理とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
