---
title: Teams カスタムアプリ用の低コードソリューション
author: laujan
description: Teams の利用可能な Microsoft 低およびコードソリューションの詳細
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 1166de0ae6e5512f4943ca1a3a7e74c62a0d5cf1
ms.sourcegitcommit: 43e1be9d9e3651ce73a8d2139e44d75550a0ca60
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "49366890"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Microsoft Teams 用の低コードカスタムアプリを作成する

[Microsoft Teams](/microsoftteams/platform) は、拡張性と適応性の両方を備えています。 これは、ユーザーの個別のニーズを満たす Teams 用のカスタムアプリケーションを自由に構築できることを意味します。 アプリケーションは最初から作成できますが、将来の迅速なソリューションに対する需要があるため、低コードオプションは、圧縮されたタイムフレーム内で洗練されたアプリを作成するために必要なものにすぎない場合があります。

低コードプラットフォームは、ソフトウェア開発に直観的な方法を提供し、アプリケーションとプロセスを構築するためのコーディングをほとんどまたはまったく必要としません。 開発者は、カスタムアプリを簡単に作成できるようになり、プロフェッショナル開発者は、アプリの開発と展開プロセスを飛躍的に促進することができます。 ほとんどの低コードプラットフォームは、ビジュアルインターフェイス、バックエンドサービスへのコネクタ、および組み込みのアプリライフサイクル管理システムによって構成されており、アプリケーションを構築、デバッグ、展開、および維持します。 Microsoft は、低コード属性を使用して、魅力的な Teams 互換アプリをすばやく構築するためのいくつかの革新的なゲートウェイを提供しています。

1. [Microsoft 電源プラットフォーム](#teams-and-microsoft-power-platform)
1. [Microsoft Teams アプリテンプレート](#teams-app-templates)

## <a name="teams-and-microsoft-power-platform"></a>Teams と Microsoft Power Platform

[Microsoft 電源プラットフォーム](/power-platform) は、1つの強力なアプリケーションプラットフォームで、4つの堅牢な microsoft テクノロジを組み合わせています。 Power BI、Power Apps、Power オートメーション (旧称 Microsoft Flow) および Power Virtual Agent は、ソリューションの構築、プロセスの自動化、データの分析、および統合された統合環境内の仮想エージェントの作成を支援します。

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="電源プラットフォームサービス":::

### <a name="-teams-and-power-bi"></a>Teams と Power BI の✔

[Microsoft teams の [POWER BI] タブ](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)では、teams ワークスペースにレポートのサポートが追加され、ユーザーは、[インタラクティブな power BI コンテンツを共有](/power-bi/collaborate-share/service-embed-report-microsoft-teams)し、teams チャネルやチャット[で他のユーザーと共同作業](/power-bi/collaborate-share/service-collaborate-microsoft-teams)を行うことができます。 パッケージ化された [POWER bi アプリ](/power-bi/collaborate-share/service-create-distribute-apps) コンテンツを最初から作成してアプリとして配布したり、 [power bi でテンプレートアプリを作成](/connect-data/service-template-apps-create)したりすることができます。 また、 [teams で新しい POWER bi アプリ](https://go.microsoft.com/fwlink/?linkid=2143643) を使用して、基本的な power bi サービスのすべての機能を teams に組み込むことができます。

### <a name="-teams-and-power-apps"></a>✔ Teams およびパワーアプリ

[Power apps](/powerapps/powerapps-overview)を使用すると、ビジネスデータに接続し、組織のニーズに合わせてカスタマイズされたビジネスアプリを作成できます。  Power Apps を使用すると、さまざまなアプリシナリオで、 [キャンバスアプリ](/powerapps/maker/#canvas-apps)を介してビジネス上の課題を解決できます。 アプリが作成されると、それを Power Apps のメーカーポータルからエクスポートして、 [Microsoft Teams に埋め込む](/power-platform/admin/embed-app-teams)ことができます。

Teams の新しい [Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143374) は、アプリの開発者が teams 内でアプリやワークフローを作成および編集して、チーム内のすべてのユーザーが複数のアプリとサービスを切り替えずに使用できるようにするための統合された環境を提供します。

### <a name="-teams-and-power-automate"></a>Teams とパワー自動化の✔

[Teams の Power オートメーションアプリ](/power-automate/flows-teams)を使用すると、[繰り返し作業タスクをチーム環境内で直接自動化するフローを作成](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/)できます。 [Microsoft Teams の任意のメッセージからフローをトリガー](/power-automate/trigger-flow-teams-message)し、[省電力の内部でアダプティブカードを使用](/power-automate/create-adaptive-cards)することができます。 さらに、Teams の新しい [Power Apps アプリ](https://go.microsoft.com/fwlink/?linkid=2143539) 内からカスタマイズして、Microsoft teams にさらなる価値を追加するフローを構築することもできます。

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams およびパワー仮想エージェント

[パワー仮想エージェント](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) は、Microsoft Power Platform および Bot フレームワークを基盤に構築された、コードを使用せずに、チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる豊富な会話を作成および管理できるようにする、コード化されていないグラフィカルインターフェイスソリューションです。 Power Virtual Agent で作成されたすべてのコンテンツは、teams とパワー仮想エージェントの場合、Teams ネイティブチャットキャンバスでユーザーと連携して表示されます。 Power virtual agents[ポータル](https://powervirtualagents.microsoft.com)を使用し[て、power virtual agents Chatbot](/power-virtual-agents/publication-add-bot-to-microsoft-teams)を Teams に統合することができます。

Teams で新しい [Power Virtual Agents アプリ](https://aka.ms/pva-teams-docs) を使用すると、会話仲間を作成、管理、および公開して、組織内の他のユーザーと共有して、チャットや質問に対する回答を得られるようにすることができます。

## <a name="teams-app-templates"></a>Teams アプリテンプレート

:::image type="content" source="../assets/images/power-platform-and-teams/app-template-illustration.png" alt-text="アプリソリューションの図":::

### <a name="-app-template-catalog"></a>✔アプリテンプレートカタログ

[アプリテンプレート](../samples/app-templates.md) とは、コミュニティ主導で、オープンソースで、GitHub 上で利用可能な Microsoft Teams 用のプロダクション対応アプリのことです。 各テンプレートには、組織用のアプリを展開してインストールするための詳細な手順が含まれており、すぐにインストールして使用を開始できる、すぐに使用できるアプリケーションを提供します。 完全なソースコードも利用できます。そのため、詳細について確認したり、コードをフォークして、特定のニーズを満たすように変更したりすることができます。

### <a name="-virtual-assistant-for-teams"></a>Teams の✔仮想アシスタント

仮想アシスタントは、ユーザーの操作、組織のブランド化、必要なデータのフルコントロールを維持しながら、強力な会話ソリューションを作成できる、Microsoft のオープンソーステンプレートです。 [Teams 環境への統合](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)のために仮想アシスタントを構成できます。 

## <a name="additional-resources"></a>その他のリソース

:::image type="content" source="../assets/images/power-platform-and-teams/blogs-and-resources.png" alt-text="ブログとリソースの図":::

### <a name="-teams-shift-connectors"></a>✔ Teams Shift コネクタ

[Teams の作業をシフトするフォース管理コネクタ](../samples/shifts-wfm-connectors.md) は、運用に対応した、オープンソースであり、コミュニティによる統合による統合です。これにより、チームがシフトした第一線ワーカーのデジタル変換に対して、シームレスな操作を行うことができます。 各コネクタは、組織への展開と統合に関する詳細なガイダンスを提供します。 完全なソースコードは、詳細に調査したり、特定のニーズに合わせて調整したりできる、GitHub リポジトリで利用できます。

### <a name="-power-platform-learn-modules"></a>✔電源プラットフォームの詳細モジュール

|トピック|
|-----|
|**Power BI**|
|[Power BI for App メーカー](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)|
|[Power BI (開発者向け)](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|**Power Apps**|
|[アプリメーカー用のパワーアプリ](/learn/browse/?products=power-apps&roles=maker)|
|[開発者向けのパワーアプリ](/learn/browse/?products=power-apps)|
|**Power Automate**|
|[アプリメーカーの電源自動化](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)|
|[開発者のための電源自動化](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|**Power Virtual Agents**|
|[アプリメーカーと開発者のためのパワー仮想エージェント](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)

### <a name="-project-oakdale-preview"></a>✔ Project Oakdale (プレビュー)

[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) は、Microsoft Teams に向けて近日中に公開される新しい低コードデータプラットフォームです。 開発者は teams で Teams の電力プラットフォームソリューションを直接作成することができます。 [Teams ブログの Microsoft Project Oakdale](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)を *参照してください*。

### <a name="-microsoft-blog-insights"></a>✔ Microsoft ブログ insights

[Project Oakdale のデータプラットフォームの機能の詳細については、「」を参照してください。](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[お客様がリモート作業に適応できるように、電力プラットフォームと Teams の更新を発表する](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[開発チームが、デジタルワークスペースを拡張するために低レベルのコード機能を使用した将来の作業を整える](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>電源プラットフォームアプリの管理✔

> [!div class="nextstepaction"]
> [Microsoft Teams 管理センターで Microsoft Power Platform アプリを管理する](/microsoftteams/manage-power-platform-apps)
