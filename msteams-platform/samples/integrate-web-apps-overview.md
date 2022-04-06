---
title: Web アプリを統合する
author: Rajeshwari-v
description: Web アプリケーションとデバイス機能とMicrosoft Teamsアプリの統合の概要。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: power Platform Power Apps people picker deep link virtual agent assistant share-to-Teams
ms.openlocfilehash: 8fe6b41f129497d439d9cf5ef391c800d6ddea0e
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685591"
---
# <a name="integrate-web-apps"></a>Web アプリを統合する

既存の Web アプリケーションの機能をMicrosoft Teams プラットフォームに統合することで、強化されたユーザー エクスペリエンスを提供できます。 [アプリをTeamsにネイティブにするには、Teams設計ガイドライン](~/concepts/design/understand-use-cases.md)に従ってください。
このドキュメントでは、Web アプリケーションとTeams、Power プラットフォームを統合して Power アプリ、Power Virtual Agents、Virtual Assistant、アプリ テンプレート、Shift コネクタ、Moodle LMS を作成するための前提条件の概要を説明し、Web サイトの [共有からTeams] ボタンを作成し、Microsoft Teamsを追加します。 タブをSharePointし、ディープ リンクを作成し、デバイス機能を統合します。

## <a name="prerequisites"></a>前提条件

効果的な統合を実現するには、次の前提条件について理解を深める必要があります。

* Teams機能。
* SharePointファイルとデータストレージの要件です。
* API の要件。
* 認証。
* アプリとTeamsのディープ リンク。
* アプリのユース ケースをTeams プラットフォーム機能にマップします。
* 個人使用、コラボレーション、またはその両方など、アプリのエントリ ポイントを決定します。

## <a name="low-code-platforms"></a>低コード プラットフォーム

低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションとプロセスを構築するためにコーディングをほとんどまたはまったく必要としません。 低コード プラットフォームを使用して、カスタム アプリを簡単に作成できます。 これらのプラットフォームは、ビジュアル インターフェイス、バックエンド サービスへのコネクタ、およびアプリケーションをビルド、デバッグ、デプロイ、および管理するための組み込みのアプリ ライフサイクル管理システムで構成されます。 Microsoft では、低コード属性を使用してTeams互換性のあるアプリを迅速に構築するための革新的なゲートウェイを次に示します。

* Microsoft Power プラットフォーム
* Microsoft Teams アプリ テンプレート

## <a name="microsoft-power-platform"></a>Microsoft Power プラットフォーム

Microsoft Power プラットフォームは、Power BI、Power Apps、Power Automate、Power Virtual Agentsなど、4 つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに組み合わせたものです。 これらのテクノロジを使用すると、統合された統合環境内で、ソリューションの構築、プロセスの自動化、データの分析、仮想エージェントの作成を行うことができます。

>[!NOTE]
>Microsoft Power Platform を使用して、Teams アプリ ストアに発行するアプリを作成することはできません。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ発行できます。

### <a name="power-apps"></a>Power アプリ

Power Appsを使用すると、ビジネス データに接続し、組織のニーズに合わせて調整されたビジネス アプリを構築できます。 Power Apps、キャンバス アプリを通じてビジネス上の課題を解決するために、さまざまなアプリ シナリオを実現できます。 アプリをビルドした後、Power Apps メーカー ポータルからエクスポートし、Microsoft Teamsに埋め込むことができます。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent は、コードのないガイド付きグラフィカル インターフェイス ソリューションです。 これは、Microsoft Power Platform と Bot Framework 上に構築されています。 チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる豊富な会話型チャットボットを作成し、維持できるようになります。 開発環境をセットアップしたり、Web サービスを作成したり、Bot Framework に直接登録したりする必要なく、Teams用のインテリジェント仮想エージェントを設計、開発、発行できます。

### <a name="create-virtual-assistant"></a>仮想アシスタントを作成する

Virtual Assistantは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft オープンソース テンプレートです。

## <a name="app-templates"></a>アプリ テンプレート

アプリ テンプレートを使用して、組織のニーズに合わせてカスタム作成されたアプリを作成できます。 これらは、コミュニティが主導し、オープンソースであり、GitHubで利用できるMicrosoft Teams向けの実稼働対応アプリです。 各テンプレートには、組織のアプリをデプロイしてインストールするための詳細な手順が含まれています。 すぐにインストールして使用を開始できるすぐに使用できるアプリケーションが提供されます。

## <a name="teams-shifts-work-force-management-connectors"></a>Teams Shifts Work Force Management コネクタ

Teams Shifts Work Force Management コネクタは、実稼働対応、オープンソース、コミュニティ主導の統合です。 彼らは、Teamsシフトを使用したファーストライン ワーカーのデジタル変革のためのシームレスなエクスペリエンスと迅速なプロセスを提供します。

## <a name="install-moodle-lms"></a>Moodle LMS のインストール

Moodle は、一般的なオープンソースラーニング管理システム (LMS) です。 これで、Microsoft Teamsと統合されるようになりました。 この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をしたり、Teams内で直接通知を更新したりできます。

## <a name="create-a-share-to-teams-button-for-your-website"></a>Web サイトの [Teams で共有] ボタンを作成する

サード パーティの Web サイトでは、起動スクリプトを使用して、Web ページの Teams ボタンに Share を埋め込むことができます。 ボタンを選択すると、ポップアップ ウィンドウで [Share to Teams エクスペリエンス] が起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたはMicrosoft Teams チャネルへのリンクを直接共有できます。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>SharePointで [Microsoft Teams] タブを追加する

SPFx Web パーツとしてSharePointにMicrosoft Teams タブを追加することで、Microsoft TeamsとSharePointの間の豊富な統合エクスペリエンスを得ることができます。

## <a name="create-deep-link"></a>ディープ リンクを作成する

Teams内のエンティティへのディープ リンクを作成できます。 Teams 内の情報や機能へのリンクを作成できます。 これらのディープ リンクは、タブ内のコンテンツと情報に移動します。ディープ リンクを使用すると、アプリを複数のアプリで結び付けて、よりネイティブなTeamsエクスペリエンスを実現するために、アプリをTeamsにリンクできます。

## <a name="integrate-device-capabilities"></a>デバイスの機能を統合する

Microsoft Teams プラットフォームは、組み込みのファースト パーティ エクスペリエンスに合わせて開発者機能を継続的に強化しています。 強化されたTeams プラットフォームを使用すると、パートナーは、Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、カメラ、QR、バーコード スキャナー、フォト ギャラリー、マイク、場所などのネイティブ デバイス機能にアクセスして統合できます。

## <a name="integrate-people-picker"></a>ユーザー ピッカーを統合する

ユーザーが Web アプリ エクスペリエンスでユーザーを検索して選択できるようにする、Teamsネイティブユーザー ピッカー コントロールを統合できます。

## <a name="integrate-teams-in-your-external-app"></a>外部アプリにTeamsを統合する

Teams アプリを構築することで、独自のエクスペリエンスをMicrosoft Teamsに埋め込むことができます。 このモデルを *元に戻* し、Teamsやその他の通信機能を独自の外部アプリ エクスペリエンスに統合する場合は、[Azure Communication Services](/azure/communication-services/overview)を参照してください。 Azure Communication Servicesは、REST API とクライアント ライブラリ SDK を使用したクラウドベースのサービスであり、通信を独自のカスタム アプリケーションに統合するのに役立ちます。 汎用またはTeamsスタイルのReact Web コンポーネントを埋め込んで、[UI ライブラリ](https://azure.github.io/communication-ui-library/)の助けを借りて呼び出しとチャットを行うことができます。

Azure Communication Services アプリケーションは、パブリック プレビュー機能を使用して[Teamsと相互運用](/azure/communication-services/concepts/teams-interop)し、カスタム アプリケーションが匿名で会議Teams参加できるようにします。 たとえば、ビデオ通話をモバイル 銀行アプリケーションに統合し、エンド ユーザーがMicrosoft Teamsを使用して銀行員と仮想的に会えるようにすることができます。

Microsoft 365 ID を統合して、Teams ユーザーに代わってビデオと PSTN 通話を埋め込む外部アプリケーションを構築することもできます。 以前[に SKYPE FOR BUSINESS SDK を](/skype-sdk/appsdk/skypeappsdk)使用したことがある場合は、Azure Communication Servicesの一部としてこれらの機能を置き換えとしてお勧めします。

## <a name="see-also"></a>関連項目

* [アプリのユース ケースをTeams プラットフォーム機能にマップする](~/concepts/design/map-use-cases.md)
* [アプリのエントリ ポイントを決定する](~/concepts/extensibility-points.md)
* [Teams 統合に関する考慮事項](~/samples/integrating-web-apps.md)
* [Microsoft Teams用のローコード カスタム アプリを作成する](~/samples/teams-low-code-solutions.md)
* [Power Virtual Agents チャットボットを追加する](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [仮想アシスタントを作成する](~/samples/virtual-assistant.md)
* [Microsoft Teams 用のアプリ テンプレート](~/samples/app-templates.md)
* [運用環境対応の Shift コネクタ](~/samples/shifts-wfm-connectors.md)
* [Moodle LMS のインストール](~/resources/moodleinstructions.md)
* [Web アプリからTeamsに共有する](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [SharePoint に Teams タブを追加する](~/tabs/how-to/tabs-in-sharepoint.md)
* [ディープ リンクの作成](~/concepts/build-and-test/deep-links.md)
* [デバイス機能](~/concepts/device-capabilities/device-capabilities-overview.md)
* [ユーザー ピッカー コントロール](~/concepts/device-capabilities/people-picker-capability.md)
