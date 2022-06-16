---
title: Microsoft Teams 用の低コード カスタム アプリを作成する
author: surbhigupta
description: Microsoft Power Platform をTeamsして、利用可能な Microsoft の低コードソリューションとコード ソリューションについて説明します。
ms.localizationpriority: medium
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 04fc4537969d3866e31e9c35e8484326b0ccbb56
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123175"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Microsoft Teams 用の低コード カスタム アプリを作成する

Microsoft Teamsは拡張可能でアダプティブです。 つまり、ユーザーの個別のニーズを満たすTeams用のカスタム アプリケーションを構築できます。 低コードのカスタム アプリは、時間を節約し、迅速なソリューションを提供し、ゼロから作成されたアプリと同じ需要を満たします。 このドキュメントでは、Microsoft Power Platform、Power Virtual Agents チャットボット、およびVirtual Assistantの概要について説明します。

低コード プラットフォームは、アプリケーションとプロセスを構築するためのコーディングを最小限またはまったく使用せずに、ソフトウェア開発に直感的なアプローチを提供します。 これにより、開発者は経験のない開発者が、コーディングをほとんどまたはまったく行わずにカスタム アプリを簡単に構築でき、プロの開発者はアプリを迅速に開発してデプロイできます。 これらのプラットフォームは、ビジュアル インターフェイス、バックエンド サービスへのコネクタ、およびアプリケーションをビルド、デバッグ、デプロイ、および管理するための組み込みのアプリ ライフサイクル管理システムで構成されます。 Microsoft Power Platform は、低コード属性を使用して互換性のあるアプリTeams迅速に構築するための革新的なゲートウェイです。

## <a name="teams-and-microsoft-power-platform"></a>Teamsと Microsoft Power Platform

Microsoft Power Platform は、Power BI、Power Apps、Power Automate、以前のMicrosoft Flow、Power Virtual Agentsなど、4 つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに組み合わせたものです。 これらのテクノロジを使用すると、ソリューションを構築し、プロセスを自動化し、データを分析し、統合された統合環境内で仮想エージェントを作成できます。

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Power Platform サービス":::

> [!NOTE]
> Microsoft Power Platform を使用して、Teams アプリ ストアに発行するアプリを作成することはできません。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ発行できます。

### <a name="-teams-and-power-bi"></a>✔ TeamsとPower BI

[Microsoft Teamsの [Power BI] タブでは、](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)Teams ワークスペースにレポートのサポートが追加され、ユーザーは[対話型のPower BI コンテンツを共有したり、](/power-bi/collaborate-share/service-embed-report-microsoft-teams)Teams チャネルやチャット[で他のユーザーと共同作業](/power-bi/collaborate-share/service-collaborate-microsoft-teams)したりできます。 パッケージ化[されたPower BIアプリ](/power-bi/collaborate-share/service-create-distribute-apps) コンテンツを一から作成し、アプリとして配布したり[、Power BIでテンプレート アプリを作成](/power-bi/connect-data/service-template-apps-create)したりできます。 さらに、Teamsの新しい[Power BI アプリを](https://go.microsoft.com/fwlink/?linkid=2143643)使用して、基本的なPower BI サービスエクスペリエンス全体をTeamsに取り込めます。

### <a name="-teams-and-power-apps"></a>✔ TeamsとPower Apps

[Power Apps](/powerapps/powerapps-overview)を使用すると、ビジネス データに接続し、組織のニーズに合わせて調整されたビジネス アプリを構築できます。  Power Apps、キャンバス アプリを通じてビジネス上の課題を解決するために、さまざまなアプリ シナリオを実現[できます](/powerapps/maker/#canvas-apps)。 ビルド後、Power Apps メーカー ポータルからアプリをエクスポートし、[Microsoft Teamsに埋め込むことができます](/power-platform/admin/embed-app-teams)。

Teamsの新しい[Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143374)は、アプリ作成者がTeams内でアプリとワークフローを作成および編集するための統合エクスペリエンスを提供します。 チーム メンバーは、アプリをすばやく公開して共有できます。 メンバーは、複数のアプリとサービスを切り替えることなく、アプリを使用できます。

### <a name="-teams-and-power-automate"></a>✔ TeamsとPower Automate

TeamsのPower Automate アプリを使用して、Teams環境内で[繰り返し作業タスク](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/)を直接自動化するフロー[を](/power-automate/flows-teams)作成できます。 [Microsoft Teams内の任意のメッセージからフローをトリガーし、Power Automate](/power-automate/trigger-flow-teams-message)[内でアダプティブ カードを使用](/power-automate/create-adaptive-cards)できます。 さらに、フローを構築して、Teamsの新しいPower Apps [アプリ](https://go.microsoft.com/fwlink/?linkid=2143539)内からMicrosoft Teamsをカスタマイズして追加することができます。

### <a name="-teams-and-power-virtual-agents"></a>✔ TeamsとPower Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft Power Platform と Bot Framework 上に構築されたコードのないガイド付きグラフィカル インターフェイス ソリューションです。 チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる、豊富な会話型チャットボットを作成し、維持できるようになります。 Power Virtual Agentsで作成されたすべてのコンテンツは、TeamsおよびPower Virtual Agents ボットで自然にレンダリングされ、Teamsネイティブ チャット キャンバスでユーザーと対話します。 Power Virtual Agents ポータルを使用して[、Power Virtual Agents チャットボット](/power-virtual-agents/publication-add-bot-to-microsoft-teams)を[Teams](https://powervirtualagents.microsoft.com)に統合できます。

Teamsで新しい[Power Virtual Agents アプリ](https://aka.ms/pva-teams-docs)を使用して、Teams内から会話チャットボットを簡単に作成、管理、発行します。 ボットを組織内の他のユーザーと共有して、チャットして質問の回答を得ることができます。

### <a name="-virtual-assistant-for-teams"></a>✔ TeamsのVirtual Assistant

仮想アシスタントは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープンソース テンプレートです。 [Teams環境への統合用に](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)仮想アシスタントを構成できます。

### <a name="-power-platform-learn-modules"></a>✔ Power Platform Learn モジュール

|  トピック  |  リンク  |
|:---------|:----------------------|
|Power BI|[App Maker のPower BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[開発者向けのPower BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[App Maker のPower Apps](/learn/browse/?products=power-apps&roles=maker)</br>[開発者向けのPower Apps](/learn/browse/?products=power-apps)|
|Power Automate|[App Maker のPower Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[開発者向けのPower Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[アプリ作成者と開発者向けのPower Virtual Agents](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project Oakdale (プレビュー)

> [!NOTE]
> **Project Oakdale** は、**Teams用に project Dataverse** に名前が変更されました。

[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) は、Microsoft Teamsに近い新しい低コード データ プラットフォームです。 これにより、開発者はTeams内で直接Teams Power Platform ソリューションを作成できます。 Project Oakdale の詳細については、「[Teams ブログ Microsoft Project Oakdale](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)」を参照してください。

### <a name="-microsoft-blog-insights"></a>✔ Microsoft ブログの分析情報

[Project Oakdale でのデータ プラットフォーム機能の詳細](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[お客様がリモート作業に適応できるように Power Platform とTeamsの更新プログラムを発表する](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teamsは、デジタル ワークスペースを強化するために低コード機能を使用した作業の将来を形成しています](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Power Platform アプリの管理

> [!div class="nextstepaction"]
> [Microsoft Teams管理センターで Microsoft Power Platform アプリを管理する](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
