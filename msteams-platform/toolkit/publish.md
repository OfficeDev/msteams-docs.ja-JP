---
title: Teams ツールキットを使用して Teams アプリを公開する
author: zyxiaoyuer
description: アプリTeams発行する
ms.author: yanjiang
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d232ac1d0ac96d46aa5f265f3fedd7b65afb3a86
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435762"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Teams ツールキットを使用して Teams アプリを公開する

アプリを作成した後、アプリを個別、チーム、組織、またはだれでもなど、さまざまなスコープに配布できます。 この配布は、ニーズ、ビジネス要件、技術的要件、アプリの目標など、複数の要因に依存します。 異なる範囲への配布には、異なるレビュー プロセスが必要な場合があります。 一般に、スコープが大きいなると、セキュリティとコンプライアンスに関する懸念のためにアプリを確認する必要があります。

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードでTeamsアプリ プロジェクトがインストールされている必要があります。

## <a name="publish-to-individual-scope-or-sideload-permission"></a>個々のスコープまたはサイドロードのアクセス許可に発行する

ユーザーは、*Teams ファイルにアプリ パッケージを直接チームまたは個人のコンテキストでアップロードすることで、カスタム アプリを .zip に追加できます。 アプリ パッケージをアップロードしてカスタム アプリを追加する方法はサイドローディングと呼ばれる機能で、次のシナリオで説明したように、アプリを広く配布する準備が整う前に、開発中にアプリをテストできます。

* アプリをローカルでテストおよびデバッグします。
* ワークフローの自動化など、自分用のアプリを構築します。
* ワーク グループなどの小さなユーザー セット用のアプリを作成します。

内部使用専用のアプリを構築し、チームと共有できるのは、Teams アプリ ストアの Teams アプリ カタログTeamsできます。

**アプリ パッケージ ファイルを作成.zip *するには**

アプリ パッケージをビルドするには、アプリ の`Zip Teams metadata package`ツリー ビューの **[展開**] から選択Teams Toolkit。 最初に実行する必要 `Provision in the cloud` があります。 生成されたアプリ パッケージは .`{your project folder}/build/appPackage/appPackage.{env}.zip`

アプリ パッケージをアップロードするには、次の手順を実行します。

1. クライアントで、Teamsバーの **[アプリ]** を選択します。
2. [アプリ **の管理] を選択します**。
3. [アプリ **の発行] を選択する**

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pub.png" alt-text="publish":::

4. カスタム **アップロードを選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/uplo.png" alt-text="アップロード":::

## <a name="publish-to-your-organization"></a>組織にアプリを公開する 

アプリを実稼働環境で使用する準備ができたら、Teams ツールキットと一緒にインストールされた Microsoft Visual Studio Code などの統合開発環境 (IDE) である Graph API から呼び出される Teams アプリ申請 API を使用してアプリを提出できます。 TreeView of Teams Toolkit  で [展開Teamsに発行] を選択するか、[Teams: コマンド パレットから Teamsに発行] **を** トリガーします。 次に、[ **組織のインストール] を選択します**。

![組織用にインストールする](./images/installforyourorganization.png)

このアプリは、管理センターの **[** Microsoft Teams管理] で利用できます。ここで、管理者はアプリを確認および承認できます。

管理者として **、管理センター** でアプリMicrosoft Teams [を](https://admin.teams.microsoft.com/policies/manage-apps)管理すると、組織のすべてのアプリを表示Teams管理できます。 アプリの組織レベルの状態とプロパティの確認、組織のアプリ ストアへの新しいカスタム アプリの承認またはアップロード、組織レベルでのアプリのブロックまたは許可、チームへのアプリの追加、サードパーティ アプリのサービスの購入、アプリによって要求されたアクセス許可の表示、アプリに対する管理者の[](https://admin.teams.microsoft.com/policies/manage-apps)同意の付与、組織全体のアプリ設定の管理を行えます。

Teams Visual Studio Code アプリ申請 API の上に構築された Visual Studio Code Teams ツールキットを使用すると、Teams でカスタム アプリの申請から承認へのプロセスを自動化できます。

> [!NOTE]
> アプリがまだ組織のアプリ ストアに発行されていません。 この手順では、アプリを組織のMicrosoft Teamsに発行することを承認できる管理者センターにアプリを送信します。

## <a name="admin-approval-for-teams-apps"></a>アプリの管理者Teams承認

Teams テナントの管理者は、Microsoft Teams 管理センターの [アプリの管理] (左側のナビゲーション) に移動し、[アプリの管理] Teams > に移動します。 組織のすべてのアプリTeams表示できます。 ページの上部にある保留中の承認ウィジェットでは、カスタム アプリが承認のために送信される時間を確認できます。
表では、新しく提出されたアプリは、送信済みアプリとブロックされたアプリの状態を自動的に公開します。 発行状態列を降順に並べ替え、アプリを検索できます。

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="承認":::

アプリ名を選択して、アプリの詳細ページに移動します。 [概要] タブでは、アプリの詳細 (説明、状態、アプリ ID など) を表示できます。

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="送信されたアプリ":::

アプリを発行するには、次の手順を実行します。

1. 管理センターの左側のナビゲーションMicrosoft Teams、[アプリの管理] Teamsアプリ>**移動します**。
2. アプリ名を選択してアプリの詳細ページに移動し、状態ボックスで [発行] を選択 **します**。
アプリを発行すると、発行状態が発行済みに変更され、状態が自動的に [許可] に変わります。

## <a name="publish-to-microsoft-store"></a>Microsoft ストアに発行する

アプリをアプリ内のストアに直接配布Microsoft Teams世界中の何百万人ものユーザーにリーチできます。 アプリがストアでも機能している場合は、潜在的な顧客に即座にアクセスできます。 また、Teamsストアに発行されたアプリは、Microsoft AppSource に自動的に一覧表示されます。これは、Microsoft 365アプリとソリューションの公式マーケットプレースです。

詳細については、「[microsoft Teams ストアに発行する」を参照してください。]([Publish your app to the Microsoft Teams store](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store))

## <a name="see-also"></a>関連項目

* [複数の環境を管理する](TeamsFx-multi-env.md)
* [プロジェクトで他の開発者とTeamsする](TeamsFx-collaboration.md)