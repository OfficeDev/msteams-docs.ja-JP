---
title: Microsoft Teams を使用してアプリを構築ToolkitとVisual Studio
description: Microsoft Teams を使用して、アプリ内で直接、Visual Studioカスタム アプリの構築を開始Toolkit
keywords: Teams Visual Studio ツールキット
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 08df1d3907a1a3683eb42222e247cd7fd6c0177b
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875008"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Teams を使用してアプリを構築ToolkitとVisual Studio

Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。 Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. 新しい ASP.NE **<span></span>T と Web 開発** モジュールが新しいインスタンスに追加Visual Studioします。 ワークロードとコンポーネントのドキュメントを追加または削除することで、Visual Studioの手順 [に従って確認](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) できます。

![Visual Studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. Visual Studio から展開してアプリをテストする場合は、IIS (インターネット インフォメーション サービス) をご使用の環境にインストールする必要があります。 Visual Studio IIS は含まれていないので、既定の Windows 10、Windows 8、または Windows 7 の構成には含まれません。ただし、Microsoft ダウンロード センターから最新バージョン [をダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Teams のインストールToolkit

Microsoft Teams Toolkit Visual Studioは、Visual Studio [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)から、または Visual Studio 内の [拡張機能]メニューから直接ダウンロードできます。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [Teams でアプリを実行する](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. [新 **しいプロジェクトの作成] を選択します**。
1. **Microsoft Teams アプリを選択し、[** 次へ] を **選択します**。
1. [新しいプロジェクトの **構成**] 画面に移動し、[プロジェクト名]、[場所]、および [ソリューション名] を **選択できます**。
1. [ソリューションとプロジェクトを **同じディレクトリに配置する] チェック ボックスをオンにします**。
1. [機能の追加] という名前のポップアップ ウィンドウでは、プロジェクトのセットアップに 1 つ以上の機能を選択できます。
1. [次へ **] ボタン** を選択して、構成プロセスを完了します。
1. [機能の追加] というラベルの付いたポップアップ ウィンドウでは、選択した各機能のプロパティを選択できます。
1. [ **完了]** を選択すると **、Microsoft Teams** Toolkitランディング ページに表示されます。

## <a name="configure-your-app"></a>アプリを構成する

その中核をなす Teams アプリには、次の 3 つのコンポーネントが含されています。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、またはモバイル)。
  1. Html タブ コンテンツやボット アダプティブ カードなど、Teams に表示されるコンテンツの要求に応答するサーバー。
  1. 次の 3 [つのファイルで構成](/concepts/build-and-test/apps-package.md) される Teams アプリ パッケージ。

  > [!div class="checklist"]
  >
  > - the manifest.json
  > - パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン
 > - Teams [アクティビティ バー](../resources/schema/manifest-schema.md#icons) に表示するアウトライン アイコン。

アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

> [!NOTE]
>まだサインインしていない場合は、Microsoft 365 またはアカウントにサインインして、開発プロセスを続行する必要があります。
>
> Microsoft 365 アカウントをお持ちない場合は [、Microsoft 365 Developer Program サブスクリプションにサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。 これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。 Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 「*Microsoft 365 開発者サブスクリプションを設定する*」[を参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。
>

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには **、Microsoft Teams** Toolkitランディング ページで、[アプリ パッケージの編集 **] を選択します** 。
1. [マイ環境 **] ドロップダウン メニュー** から [開発] を **選択します**。
1. アプリのプロパティ フィールド **を編集** できる [アプリの詳細] ページが表示されます。
1. [アプリの詳細] ページのフィールドを編集すると、最終的にアプリ パッケージの一部として出荷される manifest.jsのコンテンツが更新されます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの詳細 **ページを変更** したり、マニフェストを更新したり、アプリの .publish フォルダー内の **.env** ファイルを更新したりすると、アプリのファイル **Development.zipされます。**  The Development.zip file includes three required files— **themanifest.json** and two [icons](../concepts/build-and-test/apps-package.md#app-icons).

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

1. [ソリューション構成 **] ドロップダウン メニューの [** 展開] を **選択します**。

![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

2. **[IIS Express + Teams] ボタンを選択** します。

1. Teams が起動し、アプリのインストールダイアログが Teams クライアントに表示されます。

## <a name="validate-your-app"></a>アプリを検証する

[ **検証** ] ページでは、AppSource にアプリを提出する前にアプリ パッケージを確認できます。 マニフェスト パッケージをアップロードするだけで、検証ツールはマニフェストに関連するテスト ケースすべてについてアプリをチェックします。 失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。 自動化が難しいテストについては、暫定チェックリストで、最も一般的なテスト ケースの 7 を詳しく示し、完全な提出チェックリストへのリンクを示します。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

✔ホーム ページでは、チームにアプリをアップロードしたり、組織内のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出することができます。

✔ IT 管理者がこれらの提出を確認します。

✔発行ページに戻り、申請の状態を確認し、アプリが IT 管理者によって承認または拒否されたのか確認できます。また、アプリに更新プログラムを提出したり、現在アクティブな申請を取り消したりすることもできます。

> [!div class="nextstepaction"]
> [次の手順: 公開されたアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
