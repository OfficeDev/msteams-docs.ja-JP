---
title: Teams Toolkit を使用して新しい Teams アプリを作成する
author: zyxiaoyuer
description: Teams Toolkit を使用して新しい Teams アプリを作成する
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: e287d6251af6d44b78010449dce751b938f390bd
ms.sourcegitcommit: 05285653b2548e0b39e788cd07d414ac87ba3eaf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2022
ms.locfileid: "65191265"
---
# <a name="create-a-new-teams-app-using-teams-toolkit"></a>Teams Toolkit を使用して新しい Teams アプリを作成する

Teams Toolkit を使用して新しい Teams アプリを作成するには、次のいずれかのオプションを選択できます。

* [[新しい Teams アプリを作成]](create-new-project.md#create-a-new-teams-app)
* [[サンプルを見る]](create-new-project.md#create-a-new-teams-app-using-view-samples)

### <a name="create-a-new-teams-app"></a>新しい Teams アプリを作成する

1. Visual Studio Code を開きます。
1. Visual Studio Code のサイド バーで Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG" border="true"::: アイコンを選択します。
1. **[新しい Teams アプリを作成]** を選択します。
1. 使用可能な機能タブ、ボット、メッセージング拡張機能、または SharePoint Framework (SPFx) を使用して任意のタブから選択します。 
1. 少なくとも 1 つのオプションを選択すると、Teams アプリの作成を開始できます。

### <a name="create-a-new-teams-app-using-view-samples"></a>[サンプルを見る] を使用して、新しい Teams アプリを作成する

**[サンプルを見る]** を検索して既存のサンプルを選択すると、新しいアプリを作成することができます。 選択したサンプルには、Azure バックエンドを使用した To Do リストや、Microsoft Graph ツールキットとの統合など、一部の機能が既にある場合があります。

 1. Microsoft Visual Studio Code から **[Teams ツールキット]** を開きます。
 1. ツリービューで **[開発]** セクションを選択します。
 1. [**サンプルを表示**] を選択します。次の図に示すように、サンプル ギャラリーが表示されます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/view-samples.png" alt-text="[サンプルを見る]":::

サンプルを探索してダウンロードし、アプリをローカルで実行するか、リモートで Teams web クライアントを利用してプレビューすることができます。 各サンプルの指示に従うか、**[GitHub で表示]** を選択して `TeamsFx Samples repository` 内でサンプルを開き、ソース コードを参照します。

詳細については、「[新しい Teams タブ アプリを作成する (React)](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=2)」を参照してください。

## <a name="step-by-step-guides-using-teams-toolkit"></a>Teams ツールキットを使用したステップバイステップ ガイド

* [Blazor を使用して Teams アプリを構築する](../sbs-gs-blazorupdate.yml)
* [React](../sbs-gs-javascript.yml) を使用して JavaScript で Teams アプリを構築する
* [SPFx](../sbs-gs-spfx.yml) を使用して Teams アプリを構築する
* [C# または .NETを使用して Teams アプリをビルドする](../sbs-gs-csharp.yml)

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [Teams アプリの発行](../concepts/deploy-and-publish/appsource/publish.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)