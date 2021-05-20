---
title: Microsoft Teams用の低コードカスタム アプリを作成する
author: laujan
description: Teams用の利用可能な Microsoft の低いコード ソリューションとコード ソリューションなしの詳細
localization_priority: Normal
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: a5615c5b70e21ea1bcade3dc46c6a2b5b3bc4f92
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566209"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Microsoft Teams用の低コードカスタム アプリを作成する

Microsoft Teamsは拡張可能で適応性があります。 つまり、ユーザーのニーズを満たすTeams用のカスタム アプリケーションを構築できます。 低コードカスタムアプリは、時間を節約し、迅速なソリューションを提供し、ゼロから作成されたアプリよりも需要を満たします。 このドキュメントでは、Microsoft パワー プラットフォーム、Power Virtual Agentsチャットボット、およびバーチャル アシスタントの概要を説明します。

低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションやプロセスを構築するためにコーディングをほとんどまたはまったく必要としません。 経験のない開発者は、ほとんどまたはまったくコーディングなしで簡単にカスタム アプリを構築し、プロの開発者は、アプリを迅速に開発して展開することができます。 これらのプラットフォームは、ビジュアル インターフェイス、バックエンド サービスへのコネクタ、および組み込みのアプリケーション ライフサイクル管理システムで構成され、アプリケーションの構築、デバッグ、デプロイ、および保守を行います。 Microsoft Power Platform は、低いコード属性を使用してTeams互換性のあるアプリを迅速に構築するための革新的なゲートウェイです。

## <a name="teams-and-microsoft-power-platform"></a>Teamsとマイクロソフトのパワープラットフォーム

Microsoft Power Platform は、Power BI、Power Apps、Power Automate、旧Microsoft Flow、Power Virtual Agentsなど、4 つの堅牢なマイクロソフト テクノロジを 1 つの強力なアプリケーション プラットフォームに組み合わせています。 これらのテクノロジーにより、統合された統合環境内で、ソリューションの構築、プロセスの自動化、データの分析、仮想エージェントの作成が可能になります。

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="パワープラットフォームサービス":::

> [!NOTE]
> Microsoft Power プラットフォームを使用して、Teams アプリ ストアに公開するアプリを作成しないでください。 Microsoft Power プラットフォーム アプリは、組織のアプリ ストアにのみ発行できます。

### <a name="-teams-and-power-bi"></a>✔ TeamsとPower BI

[Microsoft TeamsのPower BIタブ](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)では、Teamsワークスペースでレポートのサポートが追加され、ユーザーは[インタラクティブなPower BIコンテンツを共有](/power-bi/collaborate-share/service-embed-report-microsoft-teams)したり、Teamsチャンネルやチャット[で他のユーザーと共同作業](/power-bi/collaborate-share/service-collaborate-microsoft-teams)したりできます。 パッケージ化された[Power BIアプリ](/power-bi/collaborate-share/service-create-distribute-apps)コンテンツを最初から作成してアプリとして配布したり[、Power BI でテンプレート アプリを作成](/connect-data/service-template-apps-create)したりできます。 さらに、Teamsに基本的なPower BIサービスエクスペリエンス全体を持ち込む[には、Teamsの新しいPower BIアプリ](https://go.microsoft.com/fwlink/?linkid=2143643)を使用します。

### <a name="-teams-and-power-apps"></a>✔ TeamsとPower Apps

[Power Apps](/powerapps/powerapps-overview)を使用すると、ビジネス データに接続し、組織のニーズに合わせて調整されたビジネス アプリを構築できます。  Power Appsキャンバス アプリを通じてビジネス上の課題を解決するための幅広いアプリ シナリオ[を可能に](/powerapps/maker/#canvas-apps)します。 ビルド後、Power Appsメーカーポータルからアプリをエクスポートし[、Microsoft Teamsに埋め込むことができます](/power-platform/admin/embed-app-teams)。

Teamsの新しい[Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143374)は、アプリ作成者がTeams内でアプリやワークフローを作成および編集するための統合エクスペリエンスを提供します。 チーム メンバーは、アプリを簡単に公開して共有できます。 メンバーは、複数のアプリとサービスを切り替えることなく、アプリを使用できます。

### <a name="-teams-and-power-automate"></a>✔ TeamsとPower Automate

フローを作成すると、Teams環境内で繰[り返し作業タスク](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/)を直接自動化できます( [Teams のPower Automate アプリを](/power-automate/flows-teams)使用します)。 [Microsoft Teams内の任意のメッセージからフローをトリガー](/power-automate/trigger-flow-teams-message)し[、Power Automate内でアダプティブ カードを使用](/power-automate/create-adaptive-cards)できます。 さらに、フローを構築してカスタマイズし、Teamsの新しい[Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143539)内からMicrosoft Teamsにさらなる価値を追加できます。

### <a name="-teams-and-power-virtual-agents"></a>✔ TeamsとPower Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、Microsoft Power プラットフォームと Bot フレームワーク上に構築されたコードなしのガイド付きグラフィカル インターフェイス ソリューションです。 チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる、豊かで会話型のチャットボットを作成し、維持できるようになります。 Power Virtual Agentsで作成されたすべてのコンテンツは、Teamsで自然にレンダリングされ、ボットPower Virtual Agents Teamsネイティブチャットキャンバス内のユーザーと交流します。 [Power Virtual Agents ポータル](https://powervirtualagents.microsoft.com)を使用して[Power Virtual Agentsチャットボット](/power-virtual-agents/publication-add-bot-to-microsoft-teams)をTeamsに統合できます。

Teamsの新しい[Power Virtual Agentsアプリ](https://aka.ms/pva-teams-docs)を使用して、会話型チャットボットをTeams内から簡単に作成、管理、公開できます。 ボットを組織内の他のユーザーと共有して、チャットを行い、質問に対する回答を得ることができます。

### <a name="-virtual-assistant-for-teams"></a>Teams用✔バーチャルアシスタント

Virtual Assistant は、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話ソリューションを作成できる Microsoft オープンソース テンプレートです。 仮想アシスタントを[設定して、Teams環境に統合](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)することができます。 

### <a name="-power-platform-learn-modules"></a>✔パワープラットフォーム学習モジュール

|  トピック  |  リンク  |
|:---------|:----------------------|
|Power BI|[アプリメーカー向けのPower BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[開発者向けのPower BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power アプリ|[アプリメーカー向けのPower Apps](/learn/browse/?products=power-apps&roles=maker)</br>[開発者向けPower Apps](/learn/browse/?products=power-apps)|
|Power Automate|[アプリメーカー向けのPower Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[開発者向けPower Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[アプリメーカーと開発者向けのPower Virtual Agents](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Projectオークデール(プレビュー)

> [!NOTE]
> Project **オークデール** は **、Teamsのプロジェクトデータバース** に名前が変更されます。

[Projectオークデール](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
)は、Microsoft Teamsに近い新しい低コードデータプラットフォームです。 開発者は、Teams内で直接Teams Powerプラットフォームソリューションを作成できます。 Projectオークデールの詳細については[、「TeamsブログMicrosoft Projectオークデール](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)」を参照してください。

### <a name="-microsoft-blog-insights"></a>マイクロソフトブログの洞察を✔する

[オークデールProjectにおけるデータ プラットフォーム機能の詳細](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[パワープラットフォームの発表と、お客様がリモート作業に適応できるようアップデートをTeams](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teamsは、デジタルワークスペースを強化するために低コード機能を使用して作業の未来を形作っています](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>パワープラットフォームアプリの管理✔

> [!div class="nextstepaction"]
> [Microsoft Teams管理センターで Microsoft 電源プラットフォーム アプリを管理する](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)