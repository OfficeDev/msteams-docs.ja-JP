---
title: Microsoft Teams Toolkit と Visual Studio を使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio toolkit
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: a1221945659b2dd0f45bdd3a966d9b029ddcde09
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604488"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Teams Toolkit と Visual Studio を使用してアプリをビルドする

Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。 Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. **<span>ASP.NE</span>T および web 開発モジュール** が Visual Studio インスタンスに追加されていることを確認してください。 「Modify Visual Studio」の手順に従って確認するには、「 [ワークロードとコンポーネントのドキュメントを追加または削除](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) する」を参照してください。

![visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

3. Visual Studio からアプリケーションを展開してテストする場合は、IIS (インターネットインフォメーションサービス) を開発環境にインストールする必要があります。 Visual Studio には IIS は含まれていません。これは、既定の Windows 10、Windows 8、または Windows 7 の構成には含まれていません。ただし、最新バージョンは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=48264)からダウンロードできます。

![IIS ダウンロードページビュー](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>Teams ツールキットをインストールする

Microsoft Teams Toolkit for Visual Studio は、visual [Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) からダウンロードするか、visual studio の [ **拡張機能** ] メニューから直接ダウンロードできます。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [Teams でアプリを実行する](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを発行する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. [ **新しいプロジェクトを作成する**] を選択します。
1. [ **Microsoft Teams アプリ** ] を選択し、[ **次へ**] を選択します。
1. [ **新しいプロジェクトの構成** ] 画面が表示されるので、 **プロジェクトの名前**、 **場所**、および **ソリューションの名前** を選択できます。
1. [ **ソリューションとプロジェクトを同じディレクトリに配置** する] というボックスをチェックします。
1. [ **機能の追加** ] という名前のポップアップウィンドウでは、プロジェクトのセットアップに対して1つ以上の機能を選択できます。
1. [ **次へ** ] ボタンを選択して、構成プロセスを完了します。
1. [ **機能の追加** ] という名前のポップアップウィンドウでは、選択した各機能のプロパティを選択できます。
1. [ **完了** ] を選択すると、 **Microsoft Teams Toolkit** のランディングページに着陸できます。

## <a name="configure-your-app"></a>アプリを構成する

主に、Teams アプリは3つのコンポーネントをサポートしています。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。
  1. Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。
  1. 3つのファイルで構成される Teams [アプリパッケージ](/concepts/build-and-test/apps-package.md) :

  > [!div class="checklist"]
  >
  > - manifest.js
  > - パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)
 > - Teams アクティビティバーに表示するための [アウトラインアイコン](../resources/schema/manifest-schema.md#icons) 。

アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。

> [!NOTE]
>まだ行っていない場合は、Microsoft 365 またはアカウントにサインインして、開発プロセスを続行する必要があります。
>
> Microsoft 365 アカウントを持っていない場合は、 [microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサインアップできます。 これは90日間 *無料* で、開発アクティビティに使用している間は継続的に更新されます。 Visual Studio *Enterprise* または *Professional* サブスクリプションを所有している場合は、どちらのプログラムにも、visual studio サブスクリプションの有効期間中にアクティブな Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が組み込まれています。 *「* [Microsoft 365 developer サブスクリプションをセットアップする」を](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)参照してください。
>

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには、 **Microsoft Teams ツールキット** のランディングページで、[ **アプリパッケージの編集** ] を選択します。
1. **[マイ環境**] ドロップダウンメニューから、[**開発**] を選択します。
1. アプリの **詳細** ページには、アプリのプロパティフィールドを編集することができます。
1. [アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの **詳細** ページを変更するか、**マニフェスト**、またはアプリの **publish** フォルダー内の **env** ファイルを更新すると、 **Development.zip** ファイルが自動的に生成されます。 Development.zip ファイルには、3つの必須ファイル ( **manifest.js** と [2 つのアイコン](../concepts/build-and-test/apps-package.md#app-icons)) が含まれています。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

1. [ **ソリューションの構成** ] ドロップダウンメニューで、[ **展開**] を選択します。

![[ソリューションの構成] メニュー](../assets/images/solution-configurations.png)

2. [ **ISS Express + Teams** ] ボタンを選択します。

1. Teams が起動し、アプリのインストールダイアログが Teams クライアントに表示されます。

## <a name="validate-your-app"></a>アプリを検証する

[ **検証** ] ページでは、アプリを appsource に提出する前にアプリパッケージを確認できます。 マニフェストパッケージをアップロードすると、検証ツールによって、マニフェスト関連のすべてのテストケースに対してアプリがチェックされます。 失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。 自動化が困難なテストの場合、最も一般的な失敗したテストケースの7つの **事前チェックリスト** と、完全な提出チェックリストへのリンクがあります。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

✔プロジェクトのホームページでは、アプリをチームにアップロードしたり、アプリを組織内のユーザーのために会社のカスタムアプリストアに提出したり、アプリをアプリソースに提出してすべての Teams ユーザーに提供したりすることができます。

✔ IT 管理者は、これらの送信を確認します。

✔ **発行** ページに戻り、送信の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認できます。これは、アプリに更新を送信するか、現在アクティブな提出を取り消すこともできます。

> [!div class="nextstepaction"]
> [次のステップ: 公開アプリの管理とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
