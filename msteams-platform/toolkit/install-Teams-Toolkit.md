---
title: Teams Toolkit のインストール
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit のインストールについて説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 9b6492efed353e2f3228a04da292141679401e66
ms.sourcegitcommit: ef545fac5c0dbe970d81f53b1631930e9196eba3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2022
ms.locfileid: "67991657"
---
# <a name="install-teams-toolkit"></a>Teams Toolkit のインストール

Teams Toolkit は、Visual Studio と Visual Studio Code の両方の拡張機能です。 このドキュメントでは、Teams Toolkit をインストールする方法について説明します。

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Visual Studio Code 用 Teams ツールキット

インストールを開始する前に、Visual Studio Code と Teams クライアントをインストールする必要があります。

## <a name="steps-to-install-teams-toolkit"></a>Teams Toolkit をインストールする手順

Teams Toolkit は、Visual Studio Code の拡張機能と Visual Studio Code Marketplace からインストールできます。 次の手順は、Teams Toolkit のインストールに役立ちます。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. **Visual Studio Code** を開きます。
1. 拡張機能ビュー (**Ctrl + Shift + X** / **⌘⇧-X** または **ビュー > Extensions**) を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="インストール":::

1. 検索ボックスに **「Teams Toolkit** 」と入力します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="ツールキット":::

1. [**インストール**] を選択します。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="ツールキット 4.0.0 をインストールする":::

   Visual Studio Code で Teams Toolkit を正常にインストールすると、Visual Studio Code ツール バーに Teams Toolkit アイコンが表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="インストール後":::

# <a name="marketplace"></a>[市場](#tab/marketplace)

1. [Visual Studio Code Marketplace を](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)開きます。

   次のページが表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="TTK Marketplace をインストールする":::

1. [**インストール**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="TTK をインストールする":::

1. ポップアップ ウィンドウで、[ **開く**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="開いているファイルを選択する":::

   次の Visual Studio Code ページが表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="VSC で TTK を選択する":::

1. [**インストール**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="VSC で TTK のインストールを選択する":::

   Visual Studio Code で Teams Toolkit を正常にインストールすると、Visual Studio Code ツール バーに Teams Toolkit アイコンが表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="インストール後":::

---

#### <a name="upgrade-teams-toolkit"></a>Teams Toolkit をアップグレードする

Teams Toolkit は、既定で最新バージョンにアップグレードされます。 次の手順は、異なるバージョンをインストールするのに役立ちます。

* [拡張機能 :::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG"::: ] アイコンを選択します。
* 検索ボックスに **「Teams Toolkit**  」と入力します。
* Teams Toolkit 拡張機能で、アイコンを選択します :::image type="icon" source="../assets/images/teams-toolkit-v2/setting icon.PNG"::: 。
* Teams Toolkit **の最新バージョン** にアップグレードするには、[別のバージョンのインストール] を選択します。

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Visual Studio 用 Teams ツールキットのインストール

インストールを開始する前に、Visual Studio インストーラーをインストールする必要があります。

[Visual Studio](https://visualstudio.microsoft.com) のダウンロード ページから最新のVisual Studio インストーラーをダウンロードできます。

## <a name="steps-to-install-teams-toolkit"></a>Teams Toolkit をインストールする手順

Visual Studio インストーラーを開いた後、ポップアップ ワークロード ウィンドウで次の手順を実行します。

1. **ASP.NET と Web 開発** のワークロードを選択します。
1. **[インストールの詳細**] パネルで **Microsoft Teams 開発ツール** を選択します。
1. [**インストール**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Visual Studio のインストール":::

1. **[起動]** を選択して Visual Studio を開きます。

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Visual Studio を起動する":::

   > [!IMPORTANT]
   > Teams Toolkit for Visual Studio はこのバージョンの GA であるため、Visual Studio 2022 バージョン 17.3.3 をダウンロードすることをお勧めします。 この記事は、Visual Studio 2022 バージョン 17.3.3 用に記述されています。 Teams ツールキット バージョン 17.3.* 以降。

::: zone-end

## <a name="see-also"></a>関連項目

* [Teams Toolkit を調べる](explore-Teams-Toolkit.md)
* [Teams Toolkit を使用して新しい Teams アプリを作成する](create-new-project.md)
* [Microsoft Teams Toolkit を使用してアプリをビルドする準備をする](build-environments.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [Visual Studio で新しい Teams アプリを作成する](create-new-teams-app-for-Visual-Studio.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
