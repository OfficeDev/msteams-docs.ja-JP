---
title: Microsoft Teams Toolkit と Visual Studio を使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio toolkit
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: Auto
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051721"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>Microsoft Teams Toolkit と Visual Studio を使用してアプリをビルドする

Microsoft Teams Toolkit を使用すると、カスタム Teams アプリを Visual Studio 環境内で直接作成することができます。 このツールキットは、このプロセスを順を追って説明しており、Teams アプリを構築、デバッグ、および起動するために必要なすべての情報を提供します。

## <a name="installing-the-teams-toolkit"></a>Teams ツールキットをインストールする

Microsoft Teams Toolkit for Visual Studio は、visual [Studio Marketplace](https://aka.ms/teams-toolkit)からダウンロードするか、visual studio 内の拡張機能として直接ダウンロードできます。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [Teams でアプリを実行する](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを発行する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. 新しいプロジェクトを作成し、Microsoft Terams Toolkit テンプレートを選択します。
1. [**機能の追加**] 画面が表示され、新しいアプリのプロパティを構成します。
1. [**完了**] ボタンを選択して、構成プロセスを完了します。

## <a name="configure-your-app"></a>アプリを構成する

主に、Teams アプリは3つのコンポーネントをサポートしています。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。
  1. Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。
  1. 3つのファイルで構成される Teams[アプリパッケージ](/concepts/build-and-test/apps-package.md):

  > [!div class="checklist"]
  >
  > - manifest.js 
  > - パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)
 > - Teams アクティビティバーに表示するための[アウトラインアイコン](../resources/schema/manifest-schema.md#icons)。

アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。

1. アプリを構成するには、 **Microsoft Teams ツールキット**拡張ウィンドウに移動します。
1. [**アプリパッケージの編集**] を選択して、[**アプリの詳細**] ページを表示します。
1. [アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

**アプリの詳細**ページを変更するか、**マニフェスト**を更新するか、またはアプリの**publish**フォルダー内の**env**ファイルを変更すると、 **Development.zip**ファイルが自動的に生成されます。 同じフォルダーに[2 つのアイコン](../concepts/build-and-test/apps-package.md#icons)を含める必要があります。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

[*ソリューションの構成*] ドロップダウンメニューで、[*展開*] を選択します。 [ *ISS Express + Teams* ] ボタンを押します。 Teams が起動し、アプリのインストールダイアログが Teams クライアントに表示されます。

## <a name="validate-your-app"></a>アプリを検証する

[**検証**] ページでは、アプリを appsource に提出する前にアプリパッケージを確認できます。 マニフェストパッケージをアップロードすると、検証ツールによって、マニフェスト関連のすべてのテストケースに対してアプリがチェックされます。 失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。 自動化が困難なテストの場合、最も一般的な失敗したテストケースの7つの**事前チェックリスト**と、完全な提出チェックリストへのリンクがあります。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

プロジェクトのホームページでは、アプリをチームにアップロードしたり、アプリを組織内のユーザーに対して会社のカスタムアプリストアに提出したり、アプリをアプリソースに提出してすべての Teams ユーザーに提供したりすることができます。 IT 管理者は、これらの送信を確認します。 [*発行*] ページに戻り、送信の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認することができます。これは、アプリに更新を送信するか、現在アクティブな提出を取り消すこともできます。

> [!div class="nextstepaction"]
> [次のステップ: 公開アプリの管理とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
