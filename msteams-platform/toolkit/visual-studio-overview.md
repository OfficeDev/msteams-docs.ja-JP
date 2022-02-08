---
title: アプリとアプリのTeams ToolkitをVisual Studio
description: このアプリを使用して、ユーザー内で直接、Visual Studioカスタム アプリをMicrosoft Teams Toolkit。 アプリの構成方法については、Visual Studioアプリを検証し、アプリと開発者ポータルVisual Studio発行します。
keywords: teams visual studio ツールキット
ms.localizationpriority: medium
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 2fa11fbf0b4bfb3d7c9b4fe376b6517e0313338f
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435853"
---
# <a name="build-apps-with-the-teams-toolkit-and-microsoft-visual-studio"></a>アプリとアプリのTeams ToolkitをMicrosoft Visual Studio

Microsoft Teams ツールキットを使用すると、Visual Studio 統合開発環境 (IDE) 内で直接カスタムの Teams アプリを構築できます。 Microsoft Teams ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="prerequisites"></a>前提条件

1. [開発者プレビューを有効にする](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。

2. アプリケーション と web 開発 **<span>ASP.NET</span>** が、ユーザーインスタンスに追加Visual Studioしてください。 詳細については、「ワークロードとコンポーネントを追加または削除Visual Studioを変更する[」を参照してください](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)。

![Visual studio asp.net モジュール](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a>サーバーをインストールTeams Toolkit

Microsoft Teams ToolkitのVisual Studioは、Visual Studio [Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) から、または Visual Studio 内の [拡張機能] メニューから直接ダウンロードVisual Studio。

## <a name="use-the-toolkit"></a>ツールキットを使う

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをアプリで実行Teams](#install-and-run-your-app-locally)
- [アプリを検証する](#validate-your-app)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しいプロジェクトをTeamsする

1. 2019 Visual Studioを起動します。
2. [新 **しいプロジェクトの作成] を選択します**。
3. [アプリ] を **Microsoft Teamsし、[次** へ] を **選択します**。
4. [新 **しいプロジェクトを構成する**] で、名前、場所 **Project****ソリューション名** を **入力します**。
5. [ **次へ]** を選択して、アプリの名前を入力します。
6. [追加情報] 画面で、アプリの [アプリケーション名 **] と [** 開発者] または **[** 会社名Teamsします。

## <a name="configure-your-app"></a>アプリを構成する

このアプリの中核となるのは、Teams 3 つのコンポーネントです。

- ユーザー Microsoft Teamsアプリを操作するクライアント (Web、デスクトップ、モバイル) を指定します。
- サーバーに表示されるコンテンツの要求に応答するTeams。 たとえば、HTML タブ コンテンツやボットアダプティブ カードなどです。
- アプリ Teamsは、次の 3 つのファイルで構成されます。

    > [!div class="checklist"]
    >
    > - manifest.json
    > - パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン。
    > - アクティビティ [バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。

アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

> [!NOTE]
>まだ実行していない場合は、開発プロセスを続行するには、Microsoft 365アカウントにサインインする必要があります。
>
> ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[サインアップ](https://developer.microsoft.com/microsoft-365/dev-program)できます。 90 日間無料で、開発アクティビティに使用している限り更新されます。 Visual Studio Enterprise または Professional サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 詳細については、「開発者向けサブスクリプション[のMicrosoft 365参照してください](/office/developer-program/office-365-developer-program-get-started)。

### <a name="configuration-steps"></a>構成の手順

1. アプリを構成するには、[**TeamsFx Project > SSO... >の構成] メニューを選択** します。

メッセージが表示されたら、M365 テナントを持つ Microsoft アカウントにサインインします。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

F5 キーを押してデバッグを開始します。 [アプリのインストール] ダイアログ ボックスがクライアントのTeamsされます。

## <a name="validate-your-app"></a>アプリを検証する

[**Project > TeamsFx Validate > Teams マニフェスト**] メニューを使用すると、アプリ パッケージが有効か確認できます。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

[Teams 開発者](https://dev.teams.microsoft.com/home)ポータルでは、チームにアプリをアップロードしたり、組織内のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出することができます。

- これらの送信内容は、IT 管理者によって審査されます。
- [発行] ページ **に戻り** 、申請の状態を確認し、アプリが IT 管理者によって承認または却下された場合に確認できます。また、アプリに更新プログラムを送信したり、現在アクティブな申請を取り消したりすることもできます。
