---
title: アプリとアプリのTeams ToolkitをVisual Studio
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studioを構築Microsoft Teams Toolkit
keywords: teams visual studio ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949717"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>アプリとアプリのTeams ToolkitをVisual Studio

Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。 Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。

1. T および web 開発 **<span>ASP.NE</span>モジュールが** インスタンスに追加Visual Studioします。 ワークロードとコンポーネントのドキュメントを追加または削除することで、Visual Studioの手順[に従って確認](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)できます。

![Visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. アプリをアプリから展開してテストする場合は、Visual Studio環境にインターネット インフォメーション サービス (IIS)) がインストールされている必要があります。 Visual Studio IIS は含まれていないので、既定の構成、Windows 10、Windows 8、または 7 Windowsには含まれません。ただし、Microsoft ダウンロード センターから最新バージョン[をダウンロードできます](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS ダウンロード ページ ビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>サーバーをインストールTeams Toolkit

このMicrosoft Teams ToolkitはVisual Studio[マーケット](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)プレースから、またはVisual Studio内の [拡張機能] メニューから直接ダウンロードVisual Studio。  また、Visual Studio Marketplace から[2019 Teams ToolkitのVisual Studioダウンロードします](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [アプリをインストールして実行Teams](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しいプロジェクトをTeamsする

![Teamsツールキットのインストール](../assets/images/teamstoolkiticon.png)

1. **[新しいプロジェクトの作成]** を選択します。

    ![新しいプロジェクトを作成する](../assets/images/createnewproject.png)

1. アプリのクイック スタート ツールを選択し **、[Microsoft Teams]** を **選択します**。
1. [新しい **プロジェクトの構成]** ページで、名前 **、** 場所Project **ソリューション名** を **入力します**。
1. [ソリューションと **プロジェクトを同じディレクトリに配置する] チェック ボックスをオン** にします。
1. [機能 **の追加] ポップアップ** ウィンドウで、プロジェクトのセットアップに使用する 1 つ以上の機能を選択します。
1. [次へ **] ボタン** を選択して構成プロセスを完了します。
1. [機能 **の追加] ポップアップ** ウィンドウで、選択した各機能のプロパティを選択します。
1. [**完了**] を選択します。 ランディング **Microsoft Teams Toolkit** が表示されます。

    ![Teamsツールキットのランディング ページ](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a>アプリを構成する

このアプリの中核となるのは、Teams 3 つのコンポーネントです。

  1. ユーザー Microsoft Teamsアプリを操作する Web、デスクトップ、またはモバイルを含むクライアントです。
  1. HTML タブ コンテンツやボットアダプティブ カードなど、Teamsに表示されるコンテンツの要求に応答するサーバー。
  1. アプリ Teamsは、次の 3 つのファイルで構成されます。

      - [manifest.js]
      - パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン。
      - アクティビティ[バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。

アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

> [!NOTE]
>まだ実行していない場合は、開発プロセスを続行するには、Microsoft 365アカウントにサインインする必要があります。
>
> ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[サインアップ](https://developer.microsoft.com/microsoft-365/dev-program)できます。 90 日間無料で、開発アクティビティに使用している限り更新されます。 Visual Studio Enterprise または Professional サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 詳細については、「開発者向けサブスクリプション[のセットアップ」Microsoft 365参照してください](/office/developer-program/office-365-developer-program-get-started)。

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには、ランディング **ページの**[Microsoft Teams Toolkit] で、[アプリ パッケージの編集 **] を選択します**。
1. [自分の **環境] ドロップダウン** メニューから、[開発] を **選択します**。
1. [アプリ **の詳細] ページ** で、アプリのプロパティ フィールドを編集します。
    
    [アプリの詳細] ページでフィールドを編集すると、アプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。 詳細については、「マニフェストのTeams Toolkit[してください](https://aka.ms/teams-toolkit-manifest)。

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの詳細 **ページを変更** したり、マニフェストを更新したり、アプリの .publish フォルダー内の **.env** ファイルを更新すると、アプリのファイルが自動的に **Development.zipされます。**  このDevelopment.zipには、3 つの必須ファイル、manifest.js **アイコン** が [含まれます](../concepts/build-and-test/apps-package.md#app-icons)。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

1. [ソリューション **構成] ドロップダウン メニュー** から、次の **図に示** すように [展開] を選択します。

    ![[ソリューション構成] メニュー](../assets/images/solution-configurations.png)

1. [+ **IIS Express] ボタンTeams** します。

    [アプリのインストール] ダイアログ ボックスがクライアントのTeamsされます。

## <a name="validate-your-app"></a>アプリを検証する

[ **検証]** ページでは、アプリを AppSource に提出する前にアプリ パッケージを確認できます。 マニフェスト パッケージをアップロードするだけで、検証ツールはアプリをマニフェスト関連のすべてのテスト ケースに対してチェックします。 失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。 自動化が難しいテストについては、最も一般的な失敗したテスト ケースの予備チェックリストの詳細 7 と、完全な提出チェックリストへのリンクを示します。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

* プロジェクトのホーム ページでは、アプリをチーム向けにアップロードしたり、組織内のユーザー向けに会社のカスタム App Store に提出したり、すべての Teams ユーザー向けに App Source に提出したりできます。

* これらの送信内容は、IT 管理者によって審査されます。

* [発行] ページ **に戻り** 、申請の状態を確認し、アプリが IT 管理者によって承認または却下された場合に確認できます。また、アプリに更新プログラムを送信したり、現在アクティブな申請を取り消したりすることもできます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [発行済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
