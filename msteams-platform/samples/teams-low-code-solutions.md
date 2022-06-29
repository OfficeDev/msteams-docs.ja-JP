---
title: Microsoft Teams 用の低コード カスタム アプリを作成する
author: surbhigupta
description: Teams an Microsoft Power Platform で利用可能な Microsoft の低コード ソリューションとコード ソリューションについて説明します。
ms.localizationpriority: medium
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 74dd4eb094c31510319932ec96cbb0db34a1fca5
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503313"
---
# <a name="create-low-code-custom-apps-for-teams"></a>Teams 用のローコード カスタム アプリを作成する

Microsoft Teams は拡張性と適応性に優れています。 つまり、ユーザーの個別のニーズを満たす Teams 用のカスタム アプリケーションを構築できます。 低コードのカスタム アプリは、時間を節約し、迅速なソリューションを提供し、ゼロから作成されたアプリと同じ需要を満たします。 このドキュメントでは、Microsoft Power Platform、Power Virtual Agents チャットボット、および Virtual Assistant の概要について説明します。

低コード プラットフォームは、アプリケーションとプロセスを構築するためのコーディングを最小限またはまったく使用せずに、ソフトウェア開発に直感的なアプローチを提供します。 これにより、開発者は経験のない開発者が、コーディングをほとんどまたはまったく行わずにカスタム アプリを簡単に構築でき、プロの開発者はアプリを迅速に開発してデプロイできます。 これらのプラットフォームは、ビジュアル インターフェイス、バックエンド サービスへのコネクタ、およびアプリケーションをビルド、デバッグ、デプロイ、および管理するための組み込みのアプリ ライフサイクル管理システムで構成されます。 Microsoft Power Platform は、低コード属性を使用して Teams 互換アプリを迅速に構築するための革新的なゲートウェイです。

## <a name="teams-and-microsoft-power-platform"></a>Teams と Microsoft Power Platform

Microsoft Power Platform は、Power BI、Power Apps、Power Automate、以前の Microsoft Flow、Power Virtual Agents など、4 つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに組み合わせたものです。 これらのテクノロジを使用すると、ソリューションを構築し、プロセスを自動化し、データを分析し、統合された統合環境内で仮想エージェントを作成できます。

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Power Platform サービス":::

> [!NOTE]
> Microsoft Power Platform を使用して、Teams アプリ ストアに発行するアプリを作成することはできません。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ発行できます。

### <a name="-teams-and-power-bi"></a>✔ Teams と Power BI

[Microsoft Teams の [Power BI] タブでは、](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)Teams ワークスペースにレポートのサポートが追加され、ユーザーは[対話型の Power BI コンテンツを共有](/power-bi/collaborate-share/service-embed-report-microsoft-teams)したり、Teams チャネルやチャット[で他のユーザーと共同作業](/power-bi/collaborate-share/service-collaborate-microsoft-teams)したりできます。 パッケージ化された [Power BI アプリ](/power-bi/collaborate-share/service-create-distribute-apps) コンテンツを最初から作成し、アプリとして配布したり [、Power BI でテンプレート アプリを作成](/power-bi/connect-data/service-template-apps-create)したりできます。 さらに、Teams で新しい [Power BI アプリ](https://go.microsoft.com/fwlink/?linkid=2143643)を使用して、基本的なPower BI サービスエクスペリエンス全体を Teams に導入します。

### <a name="-teams-and-power-apps"></a>✔ Teams と Power Apps

[Power Apps を](/powerapps/powerapps-overview)使用すると、ビジネス データに接続し、組織のニーズに合わせて調整されたビジネス アプリを構築できます。  Power Apps を使用すると、キャンバス アプリを通じてビジネス上の課題を解決するために、さまざまなアプリ シナリオが可能 [になります](/powerapps/maker/#canvas-apps)。 ビルド後、Power Apps Maker ポータルからアプリをエクスポートし、 [Microsoft Teams に埋め込むことができます](/power-platform/admin/embed-app-teams)。

Teams の新しい [Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143374) は、アプリ作成者が Teams 内でアプリとワークフローを作成および編集するための統合エクスペリエンスを提供します。 チーム メンバーは、アプリをすばやく公開して共有できます。 メンバーは、複数のアプリとサービスを切り替えることなく、アプリを使用できます。

### <a name="-teams-and-power-automate"></a>✔ Teams と Power Automate

Teams の [Power Automate アプリ](/power-automate/flows-teams)を使用して、Teams 環境内で[繰り返し作業タスク](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/)を直接自動化するフローを作成できます。 [Microsoft Teams の任意のメッセージからフローをトリガー](/power-automate/trigger-flow-teams-message)し、[Power Automate 内でアダプティブ カードを使用](/power-automate/create-adaptive-cards)できます。 さらに、Teams の新しい [Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143539) 内から Microsoft Teams をカスタマイズして追加するフローを構築できます。

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams と Power Virtual Agent

[Power Virtual Agent](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) は、Microsoft Power Platform と Bot Framework 上に構築された、コードのないガイド付きグラフィカル インターフェイス ソリューションです。 チームのすべてのメンバーは、Teams プラットフォームと簡単に統合できる、豊富な会話型チャットボットを作成し、維持できるようになります。 Power Virtual Agent で作成されたすべてのコンテンツは、Teams と Power Virtual Agents ボットで自然にレンダリングされ、Teams ネイティブ チャット キャンバスでユーザーと対話します。 [Power Virtual Agent ポータルを使用して、Power Virtual Agents チャットボット](/power-virtual-agents/publication-add-bot-to-microsoft-teams)を Teams [に](https://powervirtualagents.microsoft.com)統合できます。

Teams で新しい [Power Virtual Agents アプリ](https://aka.ms/pva-teams-docs) を使用して、Teams 内から会話チャットボットを簡単に作成、管理、発行します。 ボットを組織内の他のユーザーと共有して、チャットして質問の回答を得ることができます。

### <a name="-virtual-assistant-for-teams"></a>✔ Teams 用仮想アシスタント

仮想アシスタントは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープンソース テンプレートです。 [Teams 環境への統合](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)のために仮想アシスタントを構成できます。

### <a name="-power-platform-learn-modules"></a>✔ Power Platform Learn モジュール

|  トピック  |  リンク  |
|:---------|:----------------------|
|Power BI|[Power BI for App Maker](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[開発者向け Power BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[Power Apps for App Maker](/learn/browse/?products=power-apps&roles=maker)</br>[開発者向け Power Apps](/learn/browse/?products=power-apps)|
|Power Automate|[Power Automate for App Maker](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[開発者向けの Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[アプリ作成者と開発者向けの Power Virtual Agent](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project Oakdale (プレビュー)

> [!NOTE]
> Project **Oakdale** の名前が Project **Dataverse for Teams** に変更されました。

[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) は、Microsoft Teams に間もなく提供される新しい低コード データ プラットフォームです。 これにより、開発者は Teams 内で直接 Teams Power Platform ソリューションを作成できます。 Project Oakdale の詳細については、「 [Teams ブログ Microsoft Project Oakdale](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)」を参照してください。

### <a name="-microsoft-blog-insights"></a>✔ Microsoft ブログの分析情報

[Project Oakdale でのデータ プラットフォーム機能の詳細](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[お客様がリモート作業に適応できるように Power Platform と Teams の更新プログラムを発表する](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams は、デジタル ワークスペースを強化するために、低コード機能を使用して作業の将来を形成しています](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Power Platform アプリの管理

> [!div class="nextstepaction"]
> [Microsoft Teams 管理センターで Microsoft Power Platform アプリを管理する](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
