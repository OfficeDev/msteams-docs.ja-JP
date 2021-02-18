---
title: Teams カスタム アプリ用の低コード ソリューション
author: laujan
description: Teams で利用可能な Microsoft の低コード ソリューションとコードなしソリューションについて詳しく説明する
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: f56a252c346350a8fb871914b286570aedcd7488
ms.sourcegitcommit: ec2ca9dbfd1924a6b4ed963179fd54e5ff2c3254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274145"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Microsoft Teams 用の低コード カスタム アプリを作成する

[Microsoft Teams は](/microsoftteams/platform) 拡張性と適応性の両方があります。 つまり、ユーザーの個別のニーズを満たす Teams 用のカスタム アプリケーションを自由に構築できます。 アプリを最初から作成することもできますが、今日の迅速なソリューションの需要では、低コードのオプションが、圧縮された時間枠内で洗練されたアプリを構築するために必要な場合があります。

低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションとプロセスを構築するためにコーディングをほとんどまたは全く必要とします。 開発者はカスタム アプリを簡単に構築できます。プロフェッショナルな開発者は、アプリの開発と展開のプロセスを指数関数的に加速できます。 ほとんどの低コード プラットフォームは、ビジュアル インターフェイス、バック エンド サービスへのコネクタ、およびアプリケーションをビルド、デバッグ、展開、および維持するための組み込みのアプリ ライフサイクル管理システムで構成されています。 Microsoft は、低コード属性を使用して優れた Teams 互換アプリを迅速に構築するためのいくつかの革新的なゲートウェイを提供しています。

1. [Microsoft Power Platform](#teams-and-microsoft-power-platform)
1. [Microsoft Teams アプリ テンプレート](#teams-app-templates)

## <a name="teams-and-microsoft-power-platform"></a>Teams と Microsoft Power Platform

[Microsoft Power Platform は、4](/power-platform) つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに結合します。 Power BI、Power Apps、Power Automate (旧 Microsoft Flow) および Power Virtual Agents を使用すると、統合された統合環境内でソリューションの構築、プロセスの自動化、データの分析、仮想エージェントの作成を行えます。

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="電源プラットフォーム サービス":::

### <a name="-teams-and-power-bi"></a>✔ Teams と Power BI

[Microsoft Teams の [Power BI]](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)タブでは、Teams ワークスペースでのレポートのサポートが追加され、ユーザーは対話型の Power [BI](/power-bi/collaborate-share/service-embed-report-microsoft-teams)コンテンツを共有し[、Teams](/power-bi/collaborate-share/service-collaborate-microsoft-teams)のチャネルやチャットで他のユーザーと共同作業を行えます。 パッケージ化された [Power BI](/power-bi/collaborate-share/service-create-distribute-apps) アプリ コンテンツを最初から作成してアプリとして配布するか、Power BI でテンプレート アプリ [を作成できます](/connect-data/service-template-apps-create)。 さらに [、Teams](https://go.microsoft.com/fwlink/?linkid=2143643) の新しい Power BI アプリを使用して、基本的な Power BI サービスエクスペリエンス全体を Teams に取り込む。

### <a name="-teams-and-power-apps"></a>✔ Teams と Power Apps

[Power Apps を使用](/powerapps/powerapps-overview)すると、ビジネス データに接続し、組織のニーズに合わせて調整されたビジネス アプリを構築できます。  Power Apps を使用すると、キャンバス アプリを使ってさまざまなアプリ シナリオでビジネス上の課題 [を解決できます](/powerapps/maker/#canvas-apps)。 アプリがビルドされた後は、Power Apps メーカーポータルからエクスポートし [、Microsoft Teams に埋め込む必要があります](/power-platform/admin/embed-app-teams)。

Teams の新しい [Power Apps](https://go.microsoft.com/fwlink/?linkid=2143374) アプリは、アプリ作成者が Teams 内でアプリとワークフローを作成および編集し、複数のアプリとサービスを切り替えなくても、チームのすべてのユーザーにすばやく公開して共有する統合エクスペリエンスを提供します。

### <a name="-teams-and-power-automate"></a>✔ Teams と Power Automate

Teams の[Power Automate アプリ](/power-automate/flows-teams)を[](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/)使用すると、繰り返し行う作業タスクを Teams 環境内で直接自動化するためのフローを作成できます。 Microsoft [Teams の任意のメッセージからフロー](/power-automate/trigger-flow-teams-message) をトリガーし、Power Automate 内 [でアダプティブ カードを使用できます](/power-automate/create-adaptive-cards)。 さらに、Teams の新しい [Power Apps](https://go.microsoft.com/fwlink/?linkid=2143539) アプリ内から Microsoft Teams をカスタマイズし、さらに価値を高めするためのフローを構築できます。

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams と Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) は、Microsoft Power Platform と Bot Framework 上に構築されたコードなしガイド付きグラフィカル インターフェイス ソリューションで、Teams プラットフォームと簡単に統合できる、豊富で会話的なチャットボットをチームのすべてのメンバーが作成および維持できます。 Power Virtual Agents で作成されたコンテンツはすべて、Teams および Power Virtual Agents ボットで自然に表示され、Teams ネイティブ チャット キャンバスでユーザーと関わり合います。 Power Virtual [Agents ポータルを使用して、Power Virtual Agents](/power-virtual-agents/publication-add-bot-to-microsoft-teams) チャットボットを Teams [に統合できます](https://powervirtualagents.microsoft.com)。

Teams の新しい [Power Virtual Agents](https://aka.ms/pva-teams-docs) アプリを使用すると、Teams 内から会話チャットボットを簡単に作成、管理、公開し、組織内の他のユーザーとボットを共有して、チャットして質問に回答することができます。

## <a name="teams-app-templates"></a>Teams アプリ テンプレート

:::image type="content" source="../assets/images/power-platform-and-teams/app-template-illustration.png" alt-text="アプリ ソリューションの図":::

### <a name="-app-template-catalog"></a>✔ アプリ テンプレート カタログ

[アプリ テンプレートは](../samples/app-templates.md) 、コミュニティ駆動型、オープン ソースであり、GitHub で利用できる、Microsoft Teams 用の実稼働可能なアプリです。 各テンプレートには、組織用のアプリを展開およびインストールするための詳細な手順が含まれているので、すぐにインストールして使用を開始できるすぐに使用できるアプリケーションが提供されます。 完全なソースコードも利用できるので、詳細を調べたり、コードをフォークして特定のニーズに合わせて変更したりできます。

### <a name="-virtual-assistant-for-teams"></a>✔ Teams の仮想アシスタント

仮想アシスタントは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータのフル コントロールを維持しながら、堅牢な会話ソリューションを作成できる Microsoft オープン ソース テンプレートです。 Teams 環境に統合する仮想アシスタント [を構成できます](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)。 

## <a name="additional-resources"></a>その他のリソース

:::image type="content" source="../assets/images/power-platform-and-teams/blogs-and-resources.png" alt-text="ブログとリソースの図":::

### <a name="-teams-shift-connectors"></a>✔ Teams シフト コネクタ

[Teams シフトワーク](../samples/shifts-wfm-connectors.md) フォース管理コネクタは、Teams シフトを使用したファーストライン ワーカーのデジタル変換のためのシームレスなエクスペリエンスと迅速なプロセスを提供する、実稼働対応、オープン ソース、およびコミュニティ駆動型の統合です。 各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。 完全なソース コードは、GitHub リポジトリで入手できます。このリポジトリでは、特定のニーズに合わせて詳細に探索したり、フォークしたり、カスタマイズすることができます。

### <a name="-power-platform-learn-modules"></a>✔ Power Platform Learn モジュール

|トピック|
|-----|
|**Power BI**|
|[アプリ作成者向け Power BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)|
|[Power BI for Developers](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|**Power Apps**|
|[アプリ作成者向け Power Apps](/learn/browse/?products=power-apps&roles=maker)|
|[開発者向け Power Apps](/learn/browse/?products=power-apps)|
|**Power Automate**|
|[アプリ作成者向け Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)|
|[開発者向けの Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|**Power Virtual Agents**|
|[アプリ作成者と開発者向けの Power Virtual Agents](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)

### <a name="-project-oakdale-preview"></a>✔ プロジェクト パーク (プレビュー)

> [!NOTE]
> Project **Oak rename** is renamed to project **Dataverse for Teams**.

[Project Oak oak は](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) 、Microsoft Teams に近日公開される新しい低コード データ プラットフォームです。 開発者は Teams Power Platform ソリューションを Teams 内で直接作成できます。 *Teams* [のブログ「Microsoft Project Oak のブログ」を参照してください](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)。

### <a name="-microsoft-blog-insights"></a>✔ Microsoft ブログの分析情報

[Project Oak oak のデータ プラットフォーム機能について詳しく見る](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[お客様がリモート作業に適応するのに役立つ Power Platform と Teams の更新プログラムを発表](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams は、デジタル ワークスペースを強化するために、低コード機能を使用して作業の将来を形成しています](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Power Platform アプリの管理

> [!div class="nextstepaction"]
> [Microsoft Teams 管理センターで Microsoft Power Platform アプリを管理する](/microsoftteams/manage-power-platform-apps)
