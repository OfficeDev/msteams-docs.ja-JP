---
title: FAQ
author: MuyangAmigo
description: このモジュールでは、Visual Studio Code を使用した Teams Toolkit の FAQ を参照してください
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 88a1fba1213dce01ed48fccbc72ca02757859033
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617174"
---
# <a name="faq-for-teams-toolkit-using-visual-studio-code"></a>Visual Studio Code を使用した Teams Toolkit の FAQ

Teams Toolkit for Visual Studio Code のすべてのセクションに関する FAQ を確認できます。

[Teams Toolkit を使用したクラウド リソースのプロビジョニング](provision.md)に関する FAQ

<br>

<details>

<summary><b>トラブルシューティングの方法</b></summary>

Visual Studio Code で Teams Toolkit でエラーが発生した場合は、エラー通知で **[ヘルプの取得** ] を選択して関連ドキュメントに移動できます。 TeamsFx CLI を使用している場合は、ヘルプ ドキュメントを指すハイパーリンクがエラー メッセージの最後に表示されます。 [プロビジョニング ヘルプ ドキュメント](https://aka.ms/teamsfx-arm-help) を直接表示することもできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中に別の Azure サブスクリプションに切り替えるにはどうすればよいですか。</b></summary>

1. 現在のアカウントでサブスクリプションを切り替えるか、ログアウトして新しいサブスクリプションを選択します。
2. 現在の環境を既にプロビジョニングしている場合は、ARM がリソースの移動をサポートしていないため、新しい環境を作成し、プロビジョニングを実行する必要があります。
3. 現在の環境をプロビジョニングしていない場合は、プロビジョニングを直接トリガーできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中にリソース グループを変更するにはどうすればよいですか?</b></summary>

プロビジョニングの前に、新しいリソース グループを作成するか、既存のリソース グループを使用するかを確認するメッセージが表示されます。 新しいリソース グループ名を指定するか、この手順で既存のリソース グループ名を選択できます。

<br>

</details>

<details>

<summary><b>Sharepoint ベースのアプリをプロビジョニングするにはどうすればよいですか?</b></summary>

[SharePoint ベースのアプリのプロビジョニングに](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4)従うことができます。

> [!NOTE]
> 現時点では、Teams Toolkit を使用して SharePoint フレームワークを使用して Teams アプリを構築しても、Azure と直接統合することはできません。ドキュメント内のコンテンツは SPFx ベースのアプリには適用されません。

<br>

</details>
