---
title: Microsoft Teams 用の低コードカスタム アプリを作成する
author: laujan
description: Teams で使用可能な Microsoft の低コードソリューションとコード なしソリューションの詳細
localization_priority: Normal
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: d294bf335a7688584e52c22d2585f3db2ef1c788
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075725"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Microsoft Teams 用の低コードカスタム アプリを作成する

Microsoft Teams は拡張可能でアダプティブです。 つまり、ユーザーの個別のニーズを満たす Teams 用のカスタム アプリケーションを構築できます。 低コードのカスタム アプリは、時間を節約し、迅速なソリューションを提供し、ゼロから作成されたアプリよりも需要を満たします。 このドキュメントでは、Microsoft Power Platform、Power Virtual Agents chatbot、Virtual Assistant の概要を説明します。

低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションとプロセスを構築するためにコーディングをほとんどまたは全く必要とします。 開発者は、経験のない開発者がコーディングをほとんどまたは全くせずにカスタム アプリを簡単に構築し、プロの開発者がアプリを迅速に開発および展開できます。 これらのプラットフォームは、ビジュアル インターフェイス、バックエンド サービスへのコネクタ、およびアプリケーションのビルド、デバッグ、展開、および保守を行う組み込みのアプリ ライフサイクル管理システムで構成されます。 Microsoft Power Platform は、低コード属性を使用して Teams 互換アプリを迅速に構築するための革新的なゲートウェイです。

## <a name="teams-and-microsoft-power-platform"></a>Teams と Microsoft Power Platform

Microsoft Power Platform は、Power BI、Power Apps、Power Automate、旧 Microsoft Flow、Power Virtual Agents など、4 つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに組み合わせたものになります。 これらのテクノロジを使用すると、ソリューションの構築、プロセスの自動化、データの分析、統合環境内での仮想エージェントの作成が可能になります。

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Power プラットフォーム サービス":::

> [!NOTE]
> Microsoft Power Platform を使用して、Teams アプリ ストアに発行するアプリを作成することはできません。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ発行できます。

### <a name="-teams-and-power-bi"></a>✔ Teams と Power BI

[Microsoft Teams の [Power BI]](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)タブでは、Teams ワークスペースでのレポートのサポートが追加され、ユーザーは対話型の Power [BI](/power-bi/collaborate-share/service-embed-report-microsoft-teams)コンテンツを共有し[、Teams](/power-bi/collaborate-share/service-collaborate-microsoft-teams)チャネルやチャットで他のユーザーと共同作業できます。 パッケージ化された [Power BI](/power-bi/collaborate-share/service-create-distribute-apps) アプリ コンテンツを最初から作成し、アプリとして配布するか、Power BI でテンプレート アプリ [を作成できます](/connect-data/service-template-apps-create)。 さらに [、Teams](https://go.microsoft.com/fwlink/?linkid=2143643) の新しい Power BI アプリを使用して、基本的な Power BI サービス エクスペリエンス全体を Teams に取り込む。

### <a name="-teams-and-power-apps"></a>✔ Teams と Power Apps

[Power Apps を使用](/powerapps/powerapps-overview)すると、ビジネス データに接続し、組織のニーズに合わせてカスタマイズされたビジネス アプリを構築できます。  Power Apps を使用すると、キャンバス アプリを通じてビジネス上の課題を解決するための幅広いアプリ [シナリオが可能になります](/powerapps/maker/#canvas-apps)。 作成後、Power Apps メーカー ポータルからアプリをエクスポートし [、Microsoft Teams に埋め込みできます](/power-platform/admin/embed-app-teams)。

Teams の [新しい Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143374) は、アプリ作成者が Teams 内でアプリとワークフローを作成および編集する統合エクスペリエンスを提供します。 アプリをすばやく発行し、チーム メンバーに共有できます。 メンバーは、複数のアプリとサービスを切り替えなくてもアプリを使用できます。

### <a name="-teams-and-power-automate"></a>✔ Teams と Power Automate

Teams の Power Automate アプリ [を](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) 使用して、Teams 環境内で繰り返し作業タスクを直接自動化する [フローを作成できます](/power-automate/flows-teams)。 Microsoft [Teams の任意のメッセージから](/power-automate/trigger-flow-teams-message) フローをトリガーし、Power Automate 内 [でアダプティブ カードを使用できます](/power-automate/create-adaptive-cards)。 さらに、フローを構築して、Teams の新しい [Power Apps](https://go.microsoft.com/fwlink/?linkid=2143539) アプリ内から Microsoft Teams にさらに価値を追加できます。

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams と Power Virtual Agents

[Power Virtual Agents は](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 、Microsoft Power Platform と Bot Framework 上に構築されたコードガイド付きグラフィカル インターフェイス ソリューションです。 チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる豊富で会話型のチャットボットを作成し、維持できます。 Power Virtual Agents で作成されたコンテンツはすべて、Teams および Power Virtual Agents ボットで自然にレンダリングされ、Teams ネイティブ チャット キャンバスでユーザーと関わり合います。 Power Virtual [Agents ポータルを使用して、Power Virtual Agents](/power-virtual-agents/publication-add-bot-to-microsoft-teams) チャットボットを Teams [に統合できます](https://powervirtualagents.microsoft.com)。

Teams の [新しい Power Virtual Agents](https://aka.ms/pva-teams-docs) アプリを使用して、Teams 内から会話型チャットボットを簡単に作成、管理、発行できます。 ボットを組織内の他のユーザーと共有してチャットし、質問に対する回答を取得できます。

### <a name="-virtual-assistant-for-teams"></a>✔の仮想アシスタント

Virtual Assistant は、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープン ソース テンプレートです。 Teams 環境に統合する仮想 [アシスタントを構成できます](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)。 

### <a name="-power-platform-learn-modules"></a>✔ Power Platform Learn モジュール

|  トピック  |  リンク  |
|:---------|:----------------------|
|Power BI|[Power BI for App Makers](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[開発者向け Power BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[Power Apps for App Makers](/learn/browse/?products=power-apps&roles=maker)</br>[開発者向け Power Apps](/learn/browse/?products=power-apps)|
|Power Automate|[Power Automate for App Makers](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[開発者向けの Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[Power Virtual Agents for App Makers and Developers](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project Oakdale (プレビュー)

> [!NOTE]
> Project **Oakdale は** 、Teams の **プロジェクト Dataverse に名前が変更されます**。

[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) は、Microsoft Teams に近日公開される新しい低コード データ プラットフォームです。 これにより、開発者は Teams Power Platform ソリューションを Teams 内で直接作成できます。 Project Oakdale の詳細については [、「Teams ブログ Microsoft Project Oakdale」を参照してください](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)。

### <a name="-microsoft-blog-insights"></a>✔ブログの分析情報

[Project Oakdale のデータ プラットフォーム機能を詳しく見る](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[Power Platform と Teams の更新プログラムを発表して、お客様がリモート作業に適応するのに役立ちます](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams は、低コード機能を使用して作業の未来を形成し、デジタル ワークスペースを強化しています](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Power Platform アプリの管理

> [!div class="nextstepaction"]
> [Microsoft Teams 管理センターで Microsoft Power Platform アプリを管理する](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)