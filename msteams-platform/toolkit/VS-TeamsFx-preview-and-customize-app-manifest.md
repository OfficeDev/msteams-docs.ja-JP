---
title: Teams Toolkit for Visual Studio の Teams アプリ マニフェスト
author: surbhigupta
description: このモジュールでは、Visual Studio のさまざまな環境で Teams アプリ マニフェストを編集、プレビュー、カスタマイズする方法について説明します。
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: c391df383c97638d3c8ff5944afab75db2400580
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027457"
---
# <a name="edit-teams-app-manifest-using-visual-studio"></a>Visual Studio を使用して Teams アプリ マニフェストを編集する

Visual Studio の Teams Toolkit は、アプリの依存関係のプロビジョニングと準備中に、`state.{env}.json` と `config.{env}.json` の構成を使用して `manifest.template.json` からマニフェストを読み込みます。 マニフェストを使用して [[開発者ポータル]](https://dev.teams.microsoft.com/apps) で Microsoft Teams アプリを作成することもできます。

スキャフォールディング後、`templates/appPackage` フォルダーの下のマニフェスト テンプレート ファイルで、`manifest.template.json` がローカル環境とリモート環境の間で共有されます。

マニフェスト テンプレートで、**[プロジェクト]** > **[Teams Toolkit]** > **[マニフェスト ファイルを開く]** の順に選択します。

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="マニフェスト ファイルを開く":::

### <a name="customize-app-manifest-in-teams-toolkit"></a>Teams Toolkit でアプリ マニフェストをカスタマイズする

`manifest.template.json` には、次の 2 種類のプレースホルダーがあります:

- `{{state.xx}}` は定義済みのプレースホルダーであり、その値は Teams Toolkit によって解決されます。これは、`state.{env}.json` で定義されています。 `state.{env}.json` 内の値は変更しないことをお勧めします。
- `{{config.manifest.xx}}` はカスタマイズされたプレースホルダーであり、値は `config.{env}.json` から解決されます

次のようにカスタマイズされたパラメーターを追加できます。

- パターン `{{config.manifest.xx}}` で `manifest.template.json` にプレースホルダーを追加しています。
- `config.{env}.json` で構成値を追加します。

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### <a name="preview-app-manifest-in-teams-toolkit"></a>Teams Toolkit でアプリ マニフェストをプレビューする

アプリ マニフェストの値は、次の 2 つの方法でプレビューできます。

- `manifest.template.json` のプレースホルダーにカーソルを合わせると、**dev** および **local** 環境の値が表示されます。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="プレースホルダーの上にマウス ポインターを置く":::

- `manifest.template.json` の各プレースホルダーの横にあるキーにカーソルを合わせると、**dev** 環境と **local** 環境の同じ値が表示されます。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="プレースホルダーの横にあるキーの上にマウス ポインターを置く":::

   > [!NOTE]
   > 環境がプロビジョニングされていない場合、または Teams アプリの依存関係が準備されていない場合は、プレースホルダーの値が生成されていないことを示します。 対応する値を生成するには、ホバー内のガイダンスに従ってください。

### <a name="preview-manifest-file"></a>マニフェスト ファイルをプレビューする

マニフェスト ファイルをプレビューするには、次の手順を実行します。

- **[プロジェクト]** > **[Teams Toolkit]** メニューの順に選択し、**[Teams アプリの依存関係を準備する]** または **[クラウドでのプロビジョニング]** をトリガーします。 ローカルまたはリモートの Teams アプリの構成を生成します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="マニフェスト ファイルをプレビューする":::

- 実際のコンテンツでマニフェストをプレビューするには、Teams Toolkit によってプレビュー マニフェスト ファイルが生成され、**appPackage** フォルダーの下にある **manifest.template.json** を右クリックします。 **[プレビュー マニフェスト ファイル]** > **[ローカル用]** または **[Azure 用]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="マニフェスト ファイルをプレビューする":::

マニフェスト ファイルをプレビューするには、他に 2 つの方法があります。

- **[プロジェクト]** > **[Teams Toolkit]** > **[Zip アプリ パッケージ]** を選択し、**[ローカル]** または **[Azure 用]** を選択します。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Zip アプリ パッケージ":::

- プロジェクト名を右クリックし、**[ソリューション エクスプローラー]** で **[Teams Toolkit]** を選択すると、[プロジェクト] > [Teams Toolkit] の下にあるメニューと同じリストを表示することもできます。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="ソリューション エクスプローラーの Teams Toolkit メニューの一覧":::

    > [!NOTE]
    >このシナリオでは、プロジェクト名は **MyTeamsApp1** です。

### <a name="sync-local-changes-to-developer-portal"></a>ローカルの変更を開発者ポータルに同期する

マニフェスト ファイルをプレビューした後、ローカルの変更を開発者ポータルに同期できます。 **[プロジェクト]** > **[Teams ツールキット]** > **[Teams 開発者ータルでマニフェストを更新]** を選択するか、ソリューション エクスプローラーからコンテキスト メニューを選択します。

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Teams 開発者ポータルでマニフェストを更新する":::

> [!NOTE]
> 変更は Teams 開発者ポータルに更新されます。 開発者ポータルで手動の更新プログラムがある場合は、上書きできます。 **[警告]** ダイアログ ボックスで、**[上書きと更新]** または **[キャンセル]** を選択できます。

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="更新の警告":::

## <a name="see-also"></a>関連項目

- [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
- [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
