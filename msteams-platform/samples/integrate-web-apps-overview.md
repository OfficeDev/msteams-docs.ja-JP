---
title: Web アプリを統合する
author: Rajeshwari-v
description: Web アプリケーションとデバイス機能をアプリと統合するMicrosoft Teams概要。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 7d4056a23f126d636de3920d02a316440e51564e
ms.sourcegitcommit: 329447310013a2672216793dab79145b24ef2cd2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2021
ms.locfileid: "60017311"
---
# <a name="integrate-web-apps"></a>Web アプリを統合する

既存の Web アプリケーションの機能を新しいプラットフォームに統合することで、充実したユーザー エクスペリエンスMicrosoft Teamsできます。 アプリをアプリ[Teamsネイティブに](~/concepts/design/understand-use-cases.md)するための設計ガイドラインに従Teams。
このドキュメントでは、Web アプリケーションを Teams、Power プラットフォームと統合して Power アプリ、Power Virtual Agents、Virtual Assistant、アプリ テンプレート、シフト コネクタ、Moodle LMS を作成し、web サイトの共有と Teams ボタンを作成し、SharePoint で Microsoft Teams タブを追加し、ディープ リンクを作成し、デバイス機能を統合するための前提条件について説明します。

## <a name="prerequisites"></a>前提条件   

効果的な統合を行う場合は、以下の前提条件について理解してください。
* Teams機能。 
* SharePointストレージの要件を満たす必要があります。
* API の要件。
* 認証。
* アプリとアプリの詳細なTeams。
* アプリの使用例をプラットフォームの機能Teamsマップします。
* 個人使用、共同作業、その両方など、アプリのエントリ ポイントを決定します。

## <a name="low-code-platforms"></a>低コード プラットフォーム

低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションとプロセスを構築するためにコーディングをほとんどまたは全く必要とします。 低コード プラットフォームを使用すると、カスタム アプリを簡単に作成できます。 これらのプラットフォームは、ビジュアル インターフェイス、バック エンド サービスへのコネクタ、およびアプリケーションのビルド、デバッグ、展開、および保守を行う組み込みのアプリ ライフサイクル管理システムで構成されます。 Microsoft では、低コード属性を使用して互換性のあるアプリTeams迅速に構築するための、次の革新的なゲートウェイを提供しています。
* Microsoft Power プラットフォーム
* Microsoft Teams アプリ テンプレート

## <a name="microsoft-power-platform"></a>Microsoft Power プラットフォーム

Microsoft Power プラットフォームは、1 つの強力なアプリケーション プラットフォームで、Power BI、Power Apps、Power Automate、Power Virtual Agentsなど、4 つの堅牢な Microsoft テクノロジを組み合わせたプラットフォームです。 これらのテクノロジを使用すると、ソリューションの構築、プロセスの自動化、データの分析、統合された統合環境内での仮想エージェントの作成が可能になります。

### <a name="power-apps"></a>Power アプリ

このPower Apps、ビジネス データに接続し、組織のニーズに合わせてカスタマイズされたビジネス アプリを構築できます。 Power Appsキャンバス アプリを通じてビジネスの課題を解決するために、さまざまなアプリ シナリオを有効にします。 アプリを構築した後、アプリをメーカー ポータルからエクスポートしPower Appsに埋め込Microsoft Teams。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent はコードなし、ガイド付きグラフィカル インターフェイス ソリューションです。 これは、Microsoft Power Platform と Bot Framework 上に構築されています。 この機能を使用すると、チームのすべてのメンバーが、チャット プラットフォームと簡単に統合できる豊富な会話型チャットボットを作成Teamsできます。 開発環境をセットアップしたり、Web サービスを作成したり、ボット フレームワークに直接登録したりすることなく、Teams 用のインテリジェント仮想エージェントを設計、開発、発行できます。

### <a name="create-virtual-assistant"></a>仮想アシスタントを作成する

Virtual Assistantは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープン ソース テンプレートです。 

## <a name="app-templates"></a>アプリ テンプレート

アプリ テンプレートを使用して、組織のニーズに合わせてカスタム作成アプリを作成できます。 これらは、コミュニティによって駆動され、オープンソースMicrosoft Teams、およびアプリで利用可能な、製品向けアプリGitHub。 各テンプレートには、組織のアプリを展開およびインストールする詳細な手順が含まれている。 すぐにインストールして使用を開始できるすぐに使用できるアプリケーションが提供されます。 

## <a name="teams-shifts-work-force-management-connectors"></a>TeamsShifts Work Force Management コネクタ

TeamsShifts Work Force Management コネクタは、運用対応、オープンソース、コミュニティ駆動型の統合です。 シームレスなエクスペリエンスと迅速なプロセスを提供し、シフトを使用したファーストラインワーカーのデジタルTeams提供します。

## <a name="install-moodle-lms"></a>Moodle LMS のインストール

Moodle は、一般的なオープン ソース ラーニング管理システム (LMS) です。 この機能は現在、Microsoft Teams。 この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をし、通知を直接通知Teams。

## <a name="create-a-share-to-teams-button-for-your-website"></a>Web サイトの [Teams で共有] ボタンを作成する

サードパーティの Web サイトでは、ランチャー スクリプトを使用して、Web ページ上の Teamsボタンに Share を埋め込む可能性があります。 ボタンを選択すると、ポップアップ ウィンドウで [共有Teamsを起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたはMicrosoft Teamsへのリンクを直接共有できます。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>[ページ] Microsoft Teamsタブを追加SharePoint

Microsoft Teams と SharePoint の間の豊富な統合エクスペリエンスを得るには、Microsoft Teams タブを SharePoint web パーツSPFx追加します。 

## <a name="create-deep-link"></a>ディープ リンクの作成

エンティティへのディープ リンクを作成するには、Teams。 情報と機能へのリンクは、Teams。 これらのディープ リンクは、タブ内のコンテンツと情報に移動します。ディープ リンクを使用すると、アプリとアプリTeamsリンクし、アプリの複数の部分を結び付け、よりネイティブなエクスペリエンスTeamsできます。

## <a name="integrate-device-capabilities"></a>デバイス機能の統合

Microsoft Teamsプラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。 拡張された Teams プラットフォームを使用すると、パートナーは、Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、カメラ、QR またはバーコード スキャナー、フォト ギャラリー、マイク、場所などのネイティブ デバイス機能にアクセスして統合できます。 

## <a name="integrate-people-picker"></a>ユーザー ピッカーを統合する

ユーザーが Web アプリ エクスペリエンスTeamsユーザーを検索および選択できる、ネイティブユーザー選択コントロールを統合できます。

## <a name="integrate-teams-in-your-external-app"></a>外部Teamsにアプリを統合する
アプリを構築することで、独自のエクスペリエンスMicrosoft Teams埋め込Teamsできます。 このモデルを元に戻し、Teamsその他の通信機能を独自の外部アプリ エクスペリエンスに統合する場合は[、「Azure Communication Services」を参照してください](/azure/communication-services/overview)。 Azure Communication Services は、独自のカスタム アプリケーションに通信を統合するのに役立つ REST API とクライアント ライブラリ SDK を備え、クラウドベースのサービスです。 UI ライブラリの助けを借Teams呼び出しとチャットReact、汎用またはカスタム スタイルの Web コンポーネントを[埋め込みできます](https://azure.github.io/communication-ui-library/)。

Azure Communication Services アプリケーションでは、パブリック プレビュー[](/azure/communication-services/concepts/teams-interop)機能を使用して、Teamsと相互運用し、カスタム アプリケーションが匿名で会議に参加Teamsできます。 たとえば、ビデオ通話をモバイル バンキング アプリケーションに統合し、エンド ユーザーがモバイル 銀行を使用して銀行の従業員と事実上会Microsoft Teams。 

また、ユーザー ID Microsoft 365統合して、ビデオと PSTN 通話をユーザーに代わって埋め込む外部アプリケーションをTeamsできます。 過去に SDK [](/skype-sdk/appsdk/skypeappsdk) Skype for Business使用した場合は、Azure Communication Services の一部としてこれらの機能を置き換えとしてお勧めします。

## <a name="see-also"></a>関連項目

* [アプリの使用例をプラットフォームの機能Teamsマップする](~/concepts/design/map-use-cases.md)
* [アプリのエントリ ポイントを決定する](~/concepts/extensibility-points.md)
* [Web アプリを統合する](~/samples/integrating-web-apps.md)
* [低コードのカスタム アプリを作成Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Power Virtual Agents チャットボットを追加する](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [仮想アシスタントの作成](~/samples/virtual-assistant.md)
* [Microsoft Teams 用のアプリ テンプレート](~/samples/app-templates.md)
* [実稼働対応のシフト コネクタ](~/samples/shifts-wfm-connectors.md)
* [Moodle LMS のインストール](~/resources/moodleinstructions.md)
* [[Teams で共有] ボタンを作成する](~/concepts/build-and-test/share-to-teams.md)
* [SharePoint に Teams タブを追加する](~/tabs/how-to/tabs-in-sharepoint.md)
* [ディープ リンクの作成](~/concepts/build-and-test/deep-links.md)
* [デバイス機能](~/concepts/device-capabilities/device-capabilities-overview.md)
* [ユーザー選択コントロール](~/concepts/device-capabilities/people-picker-capability.md)
