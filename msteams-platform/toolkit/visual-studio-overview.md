---
title: Microsoft Teams ToolkitとVisual Studioを使用してアプリを構築する
description: Microsoft Teams Toolkitを使用して、Visual Studio内で優れたカスタム アプリを直接構築し始める
keywords: チームビジュアルスタジオツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: eb94a8de0355283344ebe890a6fa3a3050e243ea
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566552"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Teams ToolkitとVisual Studioを使用してアプリを構築する

Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。 Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効に](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)する :

1. **<span>ASP.NE</span>T と Web 開発モジュール** がVisual Studioインスタンスに追加されていることを確認します。 ワークロードおよびコンポーネントのドキュメントを[追加または削除して、変更Visual Studio](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)の手順に従って確認できます。

![ビジュアルスタジオ asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. Visual Studioからアプリを展開してテストする場合は、開発環境に IIS (インターネット インフォメーション サービス) をインストールする必要があります。 Visual Studioには IIS は含まれておらず、既定のWindows 10、Windows 8、または Windows 7 の構成には含まれません。ただし、最新バージョンは Microsoft ダウンロード[センター](https://www.microsoft.com/download/details.aspx?id=48264)からダウンロードできます。

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Teams Toolkitをインストールする

Visual StudioのMicrosoft Teams Toolkitは [、Visual Studioマーケットプレース](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)から、またはVisual Studio内の **拡張機能** メニューから直接ダウンロードできます。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトを設定する](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [Teamsでアプリを実行する](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しいTeams プロジェクトを設定する

1. [ **新しいプロジェクトの作成 ]** を選択します。
1. [Microsoft Teams **アプリ] を** 選択し、[**次へ**] を選択します。
1. [**新しいプロジェクトの構成]** 画面で **、[Project名**]、[**場所**]、および **[ソリューション名**] を選択します。
1. [ **ソリューションとプロジェクトを同じディレクトリに配置]** というラベルの付いたチェック ボックスをオンにします。
1. [ **機能の追加]** というラベルのポップアップ ウィンドウを使用すると、プロジェクトのセットアップに使用する 1 つ以上の機能を選択できます。
1. [ **次へ** ] を選択して、構成プロセスを完了します。
1. [ **機能の追加]** というラベルのポップアップ ウィンドウを使用すると、選択した各機能のプロパティを選択できます。
1. [**完了] を** 選択すると **、Microsoft Teams Toolkit** ランディング ページに移動します。

## <a name="configure-your-app"></a>アプリを構成する

その中核となるTeamsアプリには、次の 3 つのコンポーネントが含まれます。

  1. ユーザーがアプリを操作するクライアント (web、デスクトップ、モバイル) をMicrosoft Teams。
  1. html タブコンテンツやボットアダプティブカードなど、Teamsに表示されるコンテンツの要求に応答するサーバー。
  1. Teams アプリ パッケージは、次の 3 つのファイルで構成されます。

      > [!div class="checklist"]
      >
      > - 上のmanifest.js
      > - アプリがパブリックまたは組織のアプリ カタログに表示される[色のアイコン](../resources/schema/manifest-schema.md#icons)
      > - Teamsアクティビティ バーに表示する[アウトライン アイコン](../resources/schema/manifest-schema.md#icons)。

アプリがインストールされると、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を判断します。

> [!NOTE]
>まだ行っていない場合は、Microsoft 365またはアカウントにサインインして開発プロセスを続行する必要があります。
>
> Microsoft 365アカウントをお持ちの場合は[、Microsoft 365デベロッパー プログラム](https://developer.microsoft.com/microsoft-365/dev-program)のサブスクリプションにサインアップできます。 これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。 Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 詳細については、「 [Microsoft 365開発者サブスクリプションの設定](/office/developer-program/office-365-developer-program-get-started)」を参照してください。
>

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには **、Microsoft Teams Toolkit** のランディング ページで、[**アプリ パッケージの編集**] を選択します。
1. [ **マイ環境]** ドロップダウン メニューから [ **開発**] を選択します。
1. **[アプリの詳細**] ページに移動して、アプリのプロパティ フィールドを編集できます。
1. [アプリの詳細] ページのフィールドを編集すると、最終的にアプリ パッケージの一部として出荷されるファイル上のmanifest.jsの内容が更新されます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

**アプリの詳細** ページを変更するか、アプリの .publish フォルダー内の **マニフェスト**、または **.env** ファイルを更新すると **、Development.zip** ファイルが自動的に生成されます。  Development.zip ファイルには **、manifest.js** と [2 つのアイコン](../concepts/build-and-test/apps-package.md#app-icons)という 3 つの必須ファイルが含まれています。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

1. 次の図に示すように、[ **ソリューション構成]** ドロップダウン メニューから [ **展開** ] を選択します。

    ![ソリューション構成メニュー](../assets/images/solution-configurations.png)

2. [IIS Express **+ Teams]** ボタンを選択します。

1. Teamsが起動し、アプリのインストールダイアログがTeamsクライアントに表示されます。

## <a name="validate-your-app"></a>アプリを検証する

[ **検証]** ページでは、アプリを AppSource に提出する前にアプリ パッケージを確認できます。 マニフェスト パッケージをアップロードするだけで、検証ツールは、マニフェスト関連のすべてのテスト ケースに対してアプリをチェックします。 失敗した各テストについて、説明にエラーの修正に役立つドキュメント リンクが記載されています。 自動化が困難なテストの場合、 **暫定チェックリスト** の詳細 7 最も一般的な失敗したテスト ケースの詳細と、完全なサブミッション チェックリストへのリンク。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

✔プロジェクトのホーム ページで、アプリをチームにアップロードしたり、組織のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべてのTeamsユーザーのアプリ ソースにアプリを送信したりできます。

✔ IT 管理者がこれらの提出を確認します。

✔ **[発行** ] ページに戻って、申請の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認できます。また、アプリの更新を送信したり、現在アクティブな提出をキャンセルしたりすることもできます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [公開済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
