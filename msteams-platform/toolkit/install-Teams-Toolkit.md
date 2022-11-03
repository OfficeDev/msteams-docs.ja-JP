---
title: Teams Toolkit のインストール
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit のインストールについて説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: e079f023d931af48d5c06151c585a059c3f7f803
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833080"
---
# <a name="install-teams-toolkit"></a>Teams Toolkit のインストール

この記事では、Teams Toolkit 拡張機能をインストールする方法について説明します。

## <a name="prerequisites"></a>前提条件

::: zone pivot="visual-studio-code"

Teams Toolkit for Visual Studio Code をインストールする前に、 [Visual Studio Code をダウンロードしてインストール](https://code.visualstudio.com/Download)する必要があります。

::: zone-end

::: zone pivot="visual-studio"

Teams Toolkit for Visual Studio をインストールする前に、Visual Studio インストーラーを使用して [Visual Studio 2022 をダウンロードしてインストール](https://aka.ms/VSDownload)する必要があります。

::: zone-end

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Visual Studio Code 用 Teams ツールキット

Teams Toolkit は、Visual Studio Code の [拡張機能] ウィンドウを使用してインストールすることも、Visual Studio Marketplace からインストールすることもできます。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. **Visual Studio Code を起動します**。
1. [拡張機能] ウィンドウを開きます (**Ctrl + Shift + X** / **⌘⇧-X** または **拡張機能>表示**)。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="インストール方法を示すスクリーンショット。":::

1. 検索ボックスに **「Teams Toolkit** 」と入力します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="ツールキットを示すスクリーンショット。":::

1. **[インストール]** を選択します。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="インストール ツールキット 4.0.0 を示すスクリーンショット。":::

   Visual Studio Code で Teams Toolkit を正常にインストールすると、Visual Studio Code ツール バーに Teams Toolkit アイコンが表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="インストール ビューの後のスクリーンショット。":::

# <a name="marketplace"></a>[市場](#tab/marketplace)

1. Web ブラウザー [で Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) に移動します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="TTK Marketplace のインストールを示すスクリーンショット。":::

1. **[インストール]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="TTK をインストールする方法を示すスクリーンショット。":::

1. ポップアップ ウィンドウで 、[ **開く** ] を選択して Visual Studio Code を起動します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="開いているを選択するスクリーンショット。":::

   Teams Toolkit 拡張機能ページが Visual Studio Code に表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="VSC で TTK を選択する方法を示すスクリーンショット。":::

1. **[インストール]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="VSC で [TTK のインストール] を選択する方法を示すスクリーンショット。":::

   Visual Studio Code で Teams Toolkit を正常にインストールすると、Visual Studio Code ツール バーに Teams Toolkit アイコンが表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="インストール後のビューを示すスクリーンショット。":::

---

## <a name="installing-a-different-release-version"></a>別のリリース バージョンのインストール

既定では、Visual Studio Code は Teams Toolkit を自動的に最新の状態に保ちます。 別のバージョンをインストールする場合は、次の手順に従います。

* Visual Studio Code ツール バーから [拡張機能 (:::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG":::)] アイコンを選択します。
* 検索ボックスに **「Teams Toolkit**  」と入力します。
* [Teams ツールキット] ページで、[ **アンインストール** ] ボタンの横にあるドロップダウン矢印を選択します。
* メニューから [ **別のバージョンのインストール]を** 選択し、インストールするバージョンを選択します。

## <a name="installing-a-pre-release-version"></a>プレリリース バージョンのインストール

Teams Toolkit for Visual Studio Code 拡張機能は、GitHub でも利用できます。 プレリリースをダウンロードするには、 [GitHub の [リリース] ページに](https://github.com/OfficeDev/TeamsFx/releases) 移動し、プレリリースとしてマークされた拡張機能のダウンロードを探します。

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Visual Studio 用 Teams ツールキットのインストール

   > [!IMPORTANT]
   > 以前のバージョンの Visual Studio で既知のいくつかの問題を修正するために、最新リリースである Teams Toolkit には Visual Studio 2022 バージョン 17.3.3 以降を使用することをお勧めします。

1. [Visual Studio インストーラーをダウンロード](https://aka.ms/VSDownload)するか、既にインストールされている場合は開きます。
2. [ **インストール]** を選択するか、Visual Studio が既にインストールされている場合は **[変更] を選択** します。
3. [ワークロード] タブ **を** 選択し、 **ASP.NET と Web 開発ワークロードを** 選択します。
4. 右側の [**インストールの詳細**] パネルの **[省略可能]** セクションで、**Microsoft Teams 開発ツール** を選択します。
5. [ **変更]** または **[インストール]** を選択してインストールを完了します。

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Visual Studio をインストールする方法を示すスクリーンショット。":::

6. インストールが完了したら、[ **起動** ] を選択して Visual Studio を開きます。

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Visual Studio を起動する方法を示すスクリーンショット。":::

::: zone-end

## <a name="next-steps"></a>次の手順

Teams Toolkit がインストールされたら、「 [新しい Teams プロジェクトを作成](create-new-project.md) する」を参照して作業を開始します。

## <a name="see-also"></a>関連項目

* [Teams Toolkit を調べる](explore-Teams-Toolkit.md)
* [Teams Toolkit を使用して新しい Teams アプリを作成する](create-new-project.md)
* [Microsoft Teams Toolkit を使用してアプリを構築する準備をする](build-environments.md)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [Visual Studio で新しい Teams アプリを作成する](create-new-project.md#create-new-teams-app-in-visual-studio)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
