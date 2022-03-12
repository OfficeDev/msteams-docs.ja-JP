---
title: アプリとアプリのTeams ToolkitをVisual Studio
description: 新しいアプリを使用して、アプリ内で直接Visual Studioカスタム アプリをMicrosoft Teams Toolkit。 アプリの構成方法については、Visual Studioアプリを検証し、アプリをアプリと開発者ポータルVisual Studio発行する方法について説明します。
keywords: teams visual studio ツールキット
ms.localizationpriority: medium
ms.topic: overview
ms.date: 1/13/2022
ms.author: johmil
ms.openlocfilehash: c34f1113cd4da5f1b416dba6bc950b3588accecf
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453431"
---
# <a name="teams-toolkit-for-visual-studio"></a>Visual Studio 用 Teams ツールキット

IDE 内のアプリケーションをビルド、テストTeams開発します。

Teams Toolkit Visual Studio の拡張機能を使用すると、Teams 用の新しいプロジェクトを簡単に作成し、Teams 開発者ポータルでアプリを自動的にセットアップし、Teams で実行およびデバッグし、クラウド ホスティングを構成し、IDE から [TeamsFx](https://github.com/OfficeDev/teamsfx) を使用できます。

## <a name="install-teams-toolkit-for-visual-studio"></a>インストールTeams ToolkitのVisual Studio

>[!NOTE]
> 前提条件として、以下の手順に従Visual Studio 2022 17.1 Preview 2 以降を使用してください。

1. 2022 17.1 Visual Studioプレビュー 2 が既にインストールされている場合は、次の手順に進みます。 それ以外の場合[は、2022 プレビュー Visual Studioインストールします](https://visualstudio.microsoft.com/vs/preview/)。
2. ファイルを開Visual Studio インストーラー。
3. 既存 **の VS** 2022 プレビュー インストールの [変更] を選択します。
4. アプリケーションと **ASP.NET ワークロードを選択** します。
5. 右側の [コンポーネントと web 開発 ASP.NET **] セクション** を展開し、[**オプション**] Microsoft Teamsの一覧で [開発ツール] を選択します。
6. インストール **プロセスを****完了するには**、Visual Studio インストーラーで [インストール] または [変更] を選択します。

![インストールされているMicrosoft Teamsの開発ツールVisual Studio選択します。](images/teams-development-tools-vs-installer.png)

## <a name="get-started-quickly-with-a-new-project"></a>新しいプロジェクトをすばやく開始する

Teams Toolkit テンプレートには、アプリ プロジェクトの開始に必要なすべてのコード、ファイル、および構成Teams提供されます。

アプリ Microsoft Teams テンプレートを使用すると、新しいアプリを自動的に登録Microsoft 365構成するために必要なアカウントをTeamsできます。

> [!NOTE]
> ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[サインアップ](https://developer.microsoft.com/microsoft-365/dev-program)できます。 90 日間無料で、開発アクティビティに使用している限り更新されます。 Visual Studio Enterprise または Professional サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 詳細については、「開発者向けサブスクリプション[のMicrosoft 365参照してください](/office/developer-program/office-365-developer-program-get-started)。

1. 2022 Visual Studio起動します。
1. スタート ウィンドウで、[新しいプロジェクトの **作成] を選択します**。
1. [テンプレートの **検索] ボックスに**、「アプリ」とMicrosoft Teams入力します。
1. [アプリ テンプレート] **Microsoft Teams選択し**、[次へ] を **選択します**。
1. [新しい **プロジェクトの構成] ウィンドウ** で、[新しいプロジェクト名] ボックスに _「HelloTeams_**」と入力Project入力** します。 次に、[作成] を **選択します**。
1. [新しい **アプリケーション アプリケーションのTeams]** ウィンドウで、[アカウントの選択] セレクターを使用して、Microsoft 365アカウント **にサインインまたは選択** します。 次に、[作成] を **選択します**。

![新しいアプリ プロジェクトMicrosoft Teamsを作成Visual Studio。](images/teams-toolkit-vs-new-project.png)

Visual Studio新しいプロジェクトが開きTeams Toolkit開発者ポータルで新しいプロジェクトTeamsセットアップされます。 プロジェクトは、上記の手順でTeamsした Microsoft 365 アカウントにリンクされている組織に対して追加され、新しいユーザー登録Azure Active Directoryされます。 これは、アプリをアプリで実行するために必要Teams。

## <a name="run-and-debug-your-app-in-teams"></a>アプリを実行してデバッグTeams

アプリ プロジェクトをローカルで実行するには、アプリ プロジェクトVisual Studio。

1. アプリ プロジェクト[を開Teams作成します](#get-started-quickly-with-a-new-project)。
2. **F5 キーを押** するか、または [デバッグ **>デバッグの** 開始] を選択Visual Studio。

Visual Studioブラウザーでアプリ Teamsを起動し、デバッグを開始します。

## <a name="host-your-teams-app-in-the-cloud-and-preview-it"></a>クラウドでTeamsアプリをホストし、プレビューする

Azure でアプリをホストするクラウド リソースを作成し、自動的に構成Teams Toolkit。

1. [クラウド] **Project > Teams Toolkit >の [プロビジョニング] を選択** します。
2. [サブスクリプションの選択] ウィンドウで、リソースの作成に使用する Azure サブスクリプションを選択します。

Teams Toolkitサブスクリプションに Azure リソースを作成しますが、この手順ではコードは展開されません。 プロジェクトを次の新しいリソースに展開するには、次の手順を実行します。

1. [クラウド] **Project > Teams Toolkit >で [展開] を選択** します。

## <a name="preview-your-app-running-from-cloud-resources"></a>クラウド リソースから実行しているアプリをプレビューする

リモート リソースを使用してブラウザーでアプリを実行して、すべてが機能するのを確認できます。 このシナリオでは、まだデバッグできません。

1. [アプリの **プレビュー Project > Teams Toolkit >] Teams選択** します。

アプリはブラウザーで開き、[プロビジョニングと展開] の手順で作成されたリソースを使用します。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

[Teams 開発者](https://dev.teams.microsoft.com/home)ポータルでは、チームにアプリをアップロードしたり、組織内のユーザー用に会社のカスタム アプリ ストアにアプリを提出したり、すべての Teams ユーザーのアプリ ソースにアプリを提出することができます。

- これらの送信内容は、IT 管理者によって審査されます。
- [発行] ページ **に戻り** 、申請の状態を確認し、アプリが IT 管理者によって承認または却下された場合に確認できます。また、アプリに更新プログラムを送信したり、現在アクティブな申請を取り消したりすることもできます。
