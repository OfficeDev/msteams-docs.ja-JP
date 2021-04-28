---
title: Web アプリを統合する
author: Rajeshwari-v
description: Web アプリケーションとデバイス機能を Microsoft Teams アプリと統合する概要。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 01977e22d79f7e39986367e647a2d48ea9b2905c
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058657"
---
# <a name="integrate-web-apps"></a>Web アプリを統合する

既存の Web アプリケーションの機能を Microsoft Teams プラットフォームに統合することで、充実したユーザー エクスペリエンスを提供できます。 Teams のデザイン [ガイドラインに従って、](~/concepts/design/understand-use-cases.md) アプリを Teams にネイティブにしてください。
このドキュメントでは、Web アプリケーションを Teams、Power プラットフォームと統合して Power アプリ、Power Virtual Agents、Virtual Assistant、アプリ テンプレート、シフト コネクタ、Moodle LMS を作成し、Web サイトの Share-to-Teams ボタンを作成し、SharePoint に Microsoft Teams タブを追加し、ディープ リンクを作成し、デバイス機能を統合するための前提条件について説明します。

## <a name="prerequisites"></a>前提条件   

効果的な統合を行う場合は、以下の前提条件について理解してください。
* Teams の機能。 
* ファイルとデータストレージの SharePoint 要件。
* API の要件。
* 認証。
* アプリと Teams の深いリンク。
* アプリの使用例を Teams プラットフォームの機能にマップします。
* 個人使用、共同作業、その両方など、アプリのエントリ ポイントを決定します。

## <a name="low-code-platforms"></a>低コード プラットフォーム

低コード プラットフォームは、ソフトウェア開発に直感的なアプローチを提供し、アプリケーションとプロセスを構築するためにコーディングをほとんどまたは全く必要とします。 低コード プラットフォームを使用すると、カスタム アプリを簡単に作成できます。 これらのプラットフォームは、ビジュアル インターフェイス、バック エンド サービスへのコネクタ、およびアプリケーションのビルド、デバッグ、展開、および保守を行う組み込みのアプリ ライフサイクル管理システムで構成されます。 Microsoft では、低コード属性を使用して Teams 互換アプリを迅速に構築するための、次の革新的なゲートウェイを提供しています。
* Microsoft Power プラットフォーム
* Microsoft Teams アプリ テンプレート

## <a name="microsoft-power-platform"></a>Microsoft Power プラットフォーム

Microsoft Power プラットフォームは、Power BI、Power Apps、Power Automate、Power Virtual Agents などの 4 つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに組み合わせたプラットフォームです。 これらのテクノロジを使用すると、ソリューションの構築、プロセスの自動化、データの分析、統合された統合環境内での仮想エージェントの作成が可能になります。

### <a name="power-apps"></a>Power Apps

Power Apps を使用すると、ビジネス データに接続し、組織のニーズに合わせてカスタマイズされたビジネス アプリを構築できます。 Power Apps を使用すると、キャンバス アプリを通じてビジネス上の課題を解決するために、さまざまなアプリ シナリオを利用できます。 アプリを構築した後、Power Apps メーカー ポータルからアプリをエクスポートし、Microsoft Teams に埋め込みできます。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent はコードなし、ガイド付きグラフィカル インターフェイス ソリューションです。 これは、Microsoft Power Platform と Bot Framework 上に構築されています。 チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる豊富な会話型チャットボットを作成および維持できます。 開発環境をセットアップしたり、Web サービスを作成したり、ボット フレームワークに直接登録したりすることなく、Teams 用のインテリジェント仮想エージェントを設計、開発、発行できます。

### <a name="create-virtual-assistant"></a>仮想アシスタントを作成する

Virtual Assistant は、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープン ソース テンプレートです。 

## <a name="app-templates"></a>アプリ テンプレート

アプリ テンプレートを使用して、組織のニーズに合わせてカスタム作成アプリを作成できます。 これらは、コミュニティ駆動型、オープンソースであり、GitHub で利用可能な Microsoft Teams 用の実稼働可能なアプリです。 各テンプレートには、組織のアプリを展開およびインストールする詳細な手順が含まれている。 すぐにインストールして使用を開始できるすぐに使用できるアプリケーションが提供されます。 

## <a name="teams-shifts-work-force-management-connectors"></a>Teams Shifts Work Force Management コネクタ

Teams Shifts Work Force Management コネクタは、運用対応、オープンソース、コミュニティ駆動型の統合です。 Teams Shifts を使用したファーストライン ワーカーのデジタル変換のためのシームレスなエクスペリエンスと迅速なプロセスを提供します。

## <a name="install-moodle-lms"></a>Moodle LMS のインストール

Moodle は、一般的なオープン ソース学習管理システム (LMS) です。 これで、Microsoft Teams と統合されました。 この統合により、教育者と教師は、Moodle コースを中心に共同作業を行い、成績と課題に関する質問をし、Teams 内で直接通知を更新できます。

## <a name="create-a-share-to-teams-button-for-your-website"></a>Web サイトの [Teams で共有] ボタンを作成する

サードパーティの Web サイトでは、ランチャー スクリプトを使用して、Web ページに [Teams に共有] ボタンを埋め込む可能性があります。 ボタンを選択すると、ポップアップ ウィンドウで Teams への共有エクスペリエンスが起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたは Microsoft Teams チャネルへのリンクを直接共有できます。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>SharePoint で [Microsoft Teams] タブを追加する

SharePoint の [Microsoft Teams] タブを SPFx Web パーツとして追加すると、Microsoft Teams と SharePoint の豊富な統合エクスペリエンスを得られる可能性があります。 

## <a name="create-deep-link"></a>ディープ リンクの作成

Teams でエンティティへのディープ リンクを作成できます。 Teams 内で情報と機能へのリンクを作成できます。 これらのディープ リンクは、タブ内のコンテンツと情報に移動します。ディープ リンクを使用すると、アプリを Teams とリンクし、複数のアプリを結び付け、よりネイティブな Teams エクスペリエンスを提供できます。

## <a name="integrate-device-capabilities"></a>デバイス機能の統合

Microsoft Teams プラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。 強化された Teams プラットフォームを使用すると、パートナーは、Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、カメラ、QR、バーコード スキャナー、フォト ギャラリー、マイク、場所などのネイティブ デバイス機能にアクセスして統合できます。 

## <a name="see-also"></a>関連項目

- [アプリの使用例を Teams プラットフォーム機能にマップする](~/concepts/design/map-use-cases.md)

- [アプリのエントリ ポイントを決定する](~/concepts/extensibility-points.md)

- [Web アプリを統合する](~/samples/integrating-web-apps.md)

- [Microsoft Teams 用の低コードカスタム アプリを作成する](~/samples/teams-low-code-solutions.md)

- [Power Virtual Agents チャットボットを追加する](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)

- [仮想アシスタントの作成](~/samples/virtual-assistant.md)

- [Microsoft Teams 用のアプリ テンプレート](~/samples/app-templates.md)

- [実稼働対応のシフト コネクタ](~/samples/shifts-wfm-connectors.md)

- [Moodle LMS のインストール](~/resources/moodleinstructions.md)

- [[Teams で共有] ボタンを作成する](~/concepts/build-and-test/share-to-teams.md)

- [SharePoint に Teams タブを追加する](~/tabs/how-to/tabs-in-sharepoint.md)

- [ディープ リンクの作成](~/concepts/build-and-test/deep-links.md)

- [デバイス機能](~/concepts/device-capabilities/device-capabilities-overview.md)
