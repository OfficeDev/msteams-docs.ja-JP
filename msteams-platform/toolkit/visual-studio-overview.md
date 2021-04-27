---
title: Microsoft Teams を使用してアプリをビルドToolkitおよびVisual Studio
description: Microsoft Teams アプリケーションを使用して、Visual Studioカスタム アプリを直接作成Toolkit
keywords: teams visual studio ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bf8250e42bdf96073d729a19e921c400f242c67a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020254"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Teams を使用してアプリをビルドToolkitとVisual Studio

Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。 Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. T および web 開発 **<span>ASP.NE</span>モジュール** がユーザーのインスタンスに追加Visual Studioします。 ワークロードとコンポーネントのドキュメントを追加または削除することで [、Visual Studioの手順に従って確認](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) できます。

![visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. アプリを Visual Studio から展開してテストする場合は、IIS (Internet Information Services) を開発環境にインストールする必要があります。 Visual Studio IIS は含まれていないので、既定の Windows 10、Windows 8、または Windows 7 構成には含まれません。ただし、Microsoft ダウンロード センターから最新バージョン [をダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Teams サーバーをインストールToolkit

Microsoft Teams Toolkit Visual Studioは、Visual Studio [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)から、または Visual Studio 内の [拡張機能]メニューから直接ダウンロードVisual Studio。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [Teams でアプリを実行する](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. [新 **しいプロジェクトを作成する] を選択します**。
1. [Microsoft **Teams App] を選択し、[** 次へ] を **選択します**。
1. [新しいプロジェクトの **構成] 画面が表示** され、プロジェクト名、場所、ソリューション **名を****選択できます**。
1. [ソリューションとプロジェクトを **同じディレクトリに配置する] というラベルのボックスをオンにします**。
1. [機能の追加] というラベル **の** 付いたポップアップ ウィンドウを使用すると、プロジェクトのセットアップに 1 つ以上の機能を選択できます。
1. [次へ **] ボタン** を選択して構成プロセスを完了します。
1. [機能の追加] というラベル **の** 付いたポップアップ ウィンドウを使用すると、選択した各機能のプロパティを選択できます。
1. [ **完了]** を選択すると **、Microsoft Teams** のランディング Toolkitされます。

## <a name="configure-your-app"></a>アプリを構成する

Teams アプリの中核となるのは、次の 3 つのコンポーネントです。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、またはモバイル)。
  1. Teams に表示されるコンテンツの要求 (HTML タブ コンテンツやボットアダプティブ カードなど) に応答するサーバー。
  1. 3 [つのファイルで構成](/concepts/build-and-test/apps-package.md) される Teams アプリ パッケージ。

  > [!div class="checklist"]
  >
  > - [manifest.js]
  > - パブリック [または組織の](../resources/schema/manifest-schema.md#icons) アプリ カタログに表示するアプリの色アイコン
 > - Teams [アクティビティ バー](../resources/schema/manifest-schema.md#icons) に表示するアウトライン アイコン。

アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

> [!NOTE]
>まだ実行していない場合は、開発プロセスを続行するには、Microsoft 365 またはアカウントにサインインする必要があります。
>
> Microsoft 365 アカウントをお持ちでない場合は [、Microsoft 365 Developer Program サブスクリプションにサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。 これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。 Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 「*Microsoft 365 開発者サブスクリプションを設定する*」[を参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。
>

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには **、[Microsoft Teams** Toolkit] ランディング ページで、[アプリ パッケージの編集 **] を選択します** 。
1. [自分の **環境] ドロップダウン** メニューから、[開発] を **選択します**。
1. [アプリの詳細] **ページに移動** し、アプリのプロパティ フィールドを編集できます。
1. [アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの詳細 **ページを変更** したり、マニフェストを更新したり、アプリの .publish フォルダー内の **.env** ファイルを更新すると、アプリのファイルが自動的に **Development.zipされます。**  このDevelopment.zipには、3 つの必須ファイル (manifest.js **と 2** つのアイコン) [が含まれています](../concepts/build-and-test/apps-package.md#app-icons)。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

1. [ソリューション構成 **] ドロップダウン メニューの** [展開] を **選択します**。

![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

2. **[IIS Express + Teams] ボタンを選択** します。

1. Teams が起動し、アプリのインストールダイアログが Teams クライアントに表示されます。

## <a name="validate-your-app"></a>アプリを検証する

[ **検証]** ページでは、アプリを AppSource に提出する前にアプリ パッケージを確認できます。 マニフェスト パッケージをアップロードするだけで、検証ツールはアプリをマニフェスト関連のすべてのテスト ケースに対してチェックします。 失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。 自動化が難しいテストについては、最も一般的な失敗したテスト ケースの予備チェックリストの詳細 7 と、完全な提出チェックリストへのリンクを示します。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

✔ プロジェクトのホーム ページでは、チームにアプリをアップロードしたり、組織内のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出することができます。

✔ IT 管理者がこれらの申請を確認します。

✔ [発行] ページに戻り、申請の状態を確認し、アプリが IT 管理者によって承認または却下された場合に確認できます。また、アプリに更新プログラムを送信したり、現在アクティブな申請を取り消したりすることもできます。

> [!div class="nextstepaction"]
> [次の手順: 発行済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
