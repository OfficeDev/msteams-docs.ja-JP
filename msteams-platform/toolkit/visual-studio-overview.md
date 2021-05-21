---
title: アプリとアプリのMicrosoft Teams ToolkitをVisual Studio
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studioを構築Microsoft Teams Toolkit
keywords: teams visual studio ツールキット
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
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>アプリとアプリのTeams ToolkitをVisual Studio

Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。 Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。

1. T および web 開発 **<span>ASP.NE</span>モジュールが** インスタンスに追加Visual Studioします。 ワークロードとコンポーネントのドキュメントを追加または削除することで[、Visual Studioの手順に従って確認](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)できます。

![visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. アプリを Visual Studio から展開してテストする場合は、IIS (インターネット インフォメーション サービス) を開発環境にインストールする必要があります。 Visual Studio IIS は含まれていないので、既定のバージョン 7 構成Windows 10、Windows 8、Windowsには含まれません。ただし、Microsoft ダウンロード センターから最新バージョン[をダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>サーバーをインストールTeams Toolkit

このMicrosoft Teams ToolkitはVisual Studio[マーケット](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)プレースから、またはVisual Studio内の [拡張機能] メニューから直接ダウンロードVisual Studio。 

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [アプリをアプリで実行Teams](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しいプロジェクトをTeamsする

1. [新 **しいプロジェクトを作成する] を選択します**。
1. [アプリ **Microsoft Teams選択し、[** 次へ] を **選択します**。
1. [新しいプロジェクトの **構成]** 画面が表示され、新しいプロジェクト名、場所 **Project** ソリューション名を **選択できます**。
1. [ソリューションとプロジェクトを **同じディレクトリに配置する] というラベルのボックスをオンにします**。
1. [機能の追加] というラベル **の** 付いたポップアップ ウィンドウを使用すると、プロジェクトのセットアップに 1 つ以上の機能を選択できます。
1. [次へ **] ボタン** を選択して構成プロセスを完了します。
1. [機能の追加] というラベル **の** 付いたポップアップ ウィンドウを使用すると、選択した各機能のプロパティを選択できます。
1. [**完了]** を選択すると、ランディング **ページ** Microsoft Teams Toolkitされます。

## <a name="configure-your-app"></a>アプリを構成する

このアプリの中核となるのは、Teams 3 つのコンポーネントです。

  1. ユーザー Microsoft Teamsアプリを操作するクライアント (Web、デスクトップ、モバイル) を指定します。
  1. HTML タブ コンテンツやボットアダプティブ カードなど、Teamsに表示されるコンテンツの要求に応答するサーバー。
  1. アプリ Teamsは、次の 3 つのファイルで構成されます。

      > [!div class="checklist"]
      >
      > - [manifest.js]
      > - パブリック [または組織の](../resources/schema/manifest-schema.md#icons) アプリ カタログに表示するアプリの色アイコン
      > - アクティビティ[バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。

アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

> [!NOTE]
>まだ実行していない場合は、開発プロセスを続行するには、Microsoft 365またはアカウントにサインインする必要があります。
>
> ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[サインアップ](https://developer.microsoft.com/microsoft-365/dev-program)できます。 これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。 Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 詳細については、「開発者向けサブスクリプション[のセットアップ」をMicrosoft 365参照してください](/office/developer-program/office-365-developer-program-get-started)。
>

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには、ランディング **ページの**[Microsoft Teams Toolkit] で、[アプリ パッケージの編集 **] を選択します**。
1. [自分の **環境] ドロップダウン** メニューから、[開発] を **選択します**。
1. [アプリの詳細] **ページに移動** し、アプリのプロパティ フィールドを編集できます。
1. [アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの詳細 **ページを変更** したり、マニフェストを更新したり、アプリの .publish フォルダー内の **.env** ファイルを更新すると、アプリのファイルが自動的に **Development.zipされます。**  このDevelopment.zipには、3 つの必須ファイル (manifest.js **と 2** つのアイコン) [が含まれています](../concepts/build-and-test/apps-package.md#app-icons)。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

1. [ソリューション **構成] ドロップダウン メニュー** から、次の **図に示** すように [展開] を選択します。

    ![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

2. [+ **IIS Express] ボタンTeams** します。

1. Teams起動し、アプリのインストールダイアログがクライアントに表示Teamsします。

## <a name="validate-your-app"></a>アプリを検証する

[ **検証]** ページでは、アプリを AppSource に提出する前にアプリ パッケージを確認できます。 マニフェスト パッケージをアップロードするだけで、検証ツールはアプリをマニフェスト関連のすべてのテスト ケースに対してチェックします。 失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。 自動化が難しいテストについては、最も一般的な失敗したテスト ケースの予備チェックリストの詳細 7 と、完全な提出チェックリストへのリンクを示します。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

✔ プロジェクトのホーム ページでは、チームにアプリをアップロードしたり、組織内のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出することができます。

✔ IT 管理者がこれらの申請を確認します。

✔ [発行] ページに戻り、申請の状態を確認し、アプリが IT 管理者によって承認または却下された場合に確認できます。また、アプリに更新プログラムを送信したり、現在アクティブな申請を取り消したりすることもできます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [発行済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
