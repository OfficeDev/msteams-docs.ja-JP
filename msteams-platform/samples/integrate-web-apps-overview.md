---
title: Web アプリを統合する
author: Rajeshwari-v
description: Web アプリケーションとデバイス機能を Microsoft Teams アプリと統合する概要。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
keywords: power platform power apps ユーザー ピッカー ディープ リンク virtual agent assistant share-to-Teams
ms.openlocfilehash: c700755051eebbdb827a0fb9aba0ea51d31dbcf8
ms.sourcegitcommit: bde5f3f409fb6824a5d6ff5618e9386c85879b8b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2022
ms.locfileid: "65604272"
---
# <a name="integrate-web-apps"></a>Web アプリを統合する

既存の Web アプリケーションの機能を Microsoft Teams プラットフォームに統合することにより、充実したユーザー エクスペリエンスを提供できます。 アプリを Teams にネイティブにするには、[Teams 設計ガイドライン](~/concepts/design/understand-use-cases.md)に従ってください。
このドキュメントでは、Web アプリケーションを Teams と統合するための前提条件、Power アプリを作成する Power Platform、Power Virtual Agents、Virtual Assistant、アプリ テンプレート、Shift コネクタ、Moodle LMS、Web サイトの [Share-to-Teams] ボタンを作成する、 SharePoint の [Microsoft Teams] タブの追加、ディープ リンクの作成、およびデバイス機能の統合の概要を説明します。

## <a name="prerequisites"></a>前提条件

効果的に統合するには、次の前提条件をよりよく理解する必要があります。

* Teams 機能。
* ファイルおよびデータ ストレージに関する SharePoint の要件。
* API の要件。
* 認証。
* アプリと Teams のディープ リンク。
* ユース ケースを Teams アプリの機能にマッピングする。
* 個人的な使用、コラボレーション、またはその両方など、アプリのエントリ ポイントを決定します。

## <a name="low-code-platforms"></a>低コード プラットフォーム

低コード プラットフォームは、ソフトウェア開発への直感的なアプローチを提供し、アプリケーションとプロセスを構築するためのコーディングをほとんどまたはまったく必要としません。 低コード プラットフォームを使用して、カスタム アプリを簡単に作成できます。 これらのプラットフォームは、ビジュアル インターフェイス、バック エンド サービスへのコネクタ、およびアプリケーションを構築、デバッグ、展開、および維持するための組み込みのアプリ ライフサイクル管理システムで構成されています。 Microsoft は、低コード属性を使用して Teams 互換アプリを迅速に構築するために、次の革新的なゲートウェイを提供しています。

* Microsoft Power Platform
* Microsoft Teams アプリ テンプレート

## <a name="microsoft-power-platform"></a>Microsoft Power Platform

Microsoft Power Platform は、Power BI、Power Apps、Power Automate、Power Virtual Agents などの 4 つの堅牢な Microsoft テクノロジを 1 つの強力なアプリケーション プラットフォームに統合します。 これらのテクノロジにより、ソリューションの構築、プロセスの自動化、データの分析、および統合環境内での仮想エージェントの作成が可能になります。

>[!NOTE]
>Microsoft Power Platform を使用して、Teams アプリ ストアに発行するアプリを作成することはできません。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ発行できます。

### <a name="power-apps"></a>Power Apps

Power Apps を使用すると、ビジネス データに接続し、組織のニーズに合わせて調整されたビジネス アプリを構築できます。 Power Apps を使用すると、さまざまなアプリ シナリオで、キャンバス アプリを通じてビジネス上の課題を解決できます。 アプリをビルドしたら、Power Apps メーカー ポータルからエクスポートして、Microsoft Teams に埋め込むことができます。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agents は、コードなしのガイド付きグラフィカル インターフェイス ソリューションです。 これは、Microsoft Power Platform と Bot Framework 上に構築されています。 これにより、チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる豊富な会話型チャットボットを作成および維持できるようになります。 開発環境をセットアップしたり、Web サービスを作成したり、Bot Framework に直接登録したりすることなく、Teams 用のインテリジェントな仮想エージェントを設計、開発、および公開できます。

### <a name="create-virtual-assistant"></a>仮想アシスタントを作成する

仮想アシスタントは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープンソース テンプレートです。

## <a name="app-templates"></a>アプリ テンプレート

アプリ テンプレートを使用して、組織のニーズに合わせてカスタム メイドのアプリを作成できます。 これらは、Microsoft Teams 用の実稼働可能なアプリです。コミュニティ主導型、オープン ソースで、GitHub で利用できます。 各テンプレートには、組織用に展開してインストールするための詳細な手順が記載されています。 すぐにインストールしてすぐに使用を開始できる、使用準備が完了したアプリケーションを提供します。

## <a name="install-moodle-lms"></a>Moodle LMS のインストール

Moodle は人気のあるオープンソースのラーニング管理システム (LMS) です。 現在、Microsoft Teams と統合されています。 この統合により、教育者と教師は Moodle コースで共同作業を行い、成績や課題について質問したり、Teams 内で常に最新の通知を受け取ることができます。

## <a name="create-a-share-to-teams-button-for-your-website"></a>Web サイトの [Teams で共有] ボタンを作成する

サードパーティの Web サイトは、ランチャー スクリプトを使用して、Web ページに [Teams に共有​​] ボタンを埋め込むことができます。 ボタンを選択すると、ポップアップ ウィンドウで [Teams に共有] エクスペリエンスが起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたは Microsoft Teams チャネルへのリンクを直接共有できます。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>SharePoint に Microsoft Teams タブを追加する

SPFx Web パーツとして SharePoint に Microsoft Teams タブを追加することで、Microsoft Teams と SharePoint の間のリッチなインテグレーション エクスペリエンスを得ることができます。

## <a name="create-deep-link"></a>ディープ リンクを作成する

Teams のエンティティへのディープ リンクを作成できます。 Teams 内の情報や機能へのリンクを作成できます。 これらのディープ リンクは、タブ内のコンテンツと情報に移動します。ディープ リンクを使用して、アプリを Teams にリンクできます。これは、アプリの複数の部分を結び付けて、よりネイティブな Teams エクスペリエンスを実現するためです。

## <a name="integrate-device-capabilities"></a>デバイスの機能を統合する

Microsoft Teams プラットフォームは、組み込みのファーストパーティ エクスペリエンスに合わせて開発者機能を継続的に強化しています。 強化された Teams プラットフォームにより、パートナーは、Microsoft Teams JavaScript クライアント SDK で利用可能な専用 API を使用して、カメラ、QR またはバーコード スキャナー、フォト ギャラリー、マイク、位置情報などのネイティブ デバイス機能にアクセスして統合できます。

## <a name="integrate-people-picker"></a>ユーザー ピッカーを統合する

Teams のネイティブ ユーザー ピッカー コントロールを統合して、ユーザーが Web アプリ エクスペリエンスでユーザーを検索および選択できるようにすることができます。

## <a name="integrate-teams-in-your-external-app"></a>Teams を外部アプリに統合する

Teams アプリを作成することで、独自のエクスペリエンスを Microsoft Teams に組み込むことができます。 このモデルを *元に戻して*、Teams またはその他の通信機能を独自の外部アプリ エクスペリエンスに統合する場合は、[Azure Communication Services](/azure/communication-services/overview) を参照してください。 Azure Communication Services は、REST API とクライアント ライブラリ SDK を備えたクラウドベースのサービスであり、通信を独自のカスタム アプリケーションに統合するのに役立ちます。 [UI ライブラリ](https://azure.github.io/communication-ui-library/)を使用して、通話やチャットの汎用または Teams スタイルの React Web コンポーネントを埋め込むことができます。

Azure Communication Services アプリケーションは、パブリック プレビュー機能を使用して、[Teams と相互運用し](/azure/communication-services/concepts/teams-interop)、カスタム アプリケーションが Teams 会議に匿名で参加できるようにすることができます。 たとえば、ビデオ通話をモバイル バンキング アプリケーションに統合し、エンドユーザーが Microsoft Teams を使用して銀行の従業員と仮想的に会うことができるようにすることができます。

また、Microsoft 365 ID を統合して、Teams ユーザーに代わってビデオと PSTN 通話を埋め込む外部アプリケーションを構築することもできます。 過去に [Skype for Business SDK](/skype-sdk/appsdk/skypeappsdk) を使用したことがある場合は、代わりに Azure Communication Services の一部としてこれらの機能を使用することをお勧めします。

## <a name="see-also"></a>関連項目

* [アプリのユース ケースを Teams プラットフォームの機能にマッピングする](~/concepts/design/map-use-cases.md)
* [アプリのエントリ ポイントを決定する](~/concepts/extensibility-points.md)
* [Teams 統合に関する考慮事項](~/samples/integrating-web-apps.md)
* [Microsoft Teams 用の低コード カスタム アプリを作成する](~/samples/teams-low-code-solutions.md)
* [Power Virtual Agents チャットボットを追加する](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [仮想アシスタントを作成する](~/samples/virtual-assistant.md)
* [Microsoft Teams 用のアプリ テンプレート](~/samples/app-templates.md)
* [運用環境対応の Shift コネクタ](~/samples/shifts-wfm-connectors.md)
* [Moodle LMS のインストール](~/resources/moodleinstructions.md)
* [Web アプリから Teams に共有する](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [SharePoint に Teams タブを追加する](~/tabs/how-to/tabs-in-sharepoint.md)
* [ディープ リンクの作成](~/concepts/build-and-test/deep-links.md)
* [デバイス機能](~/concepts/device-capabilities/device-capabilities-overview.md)
* [ユーザー ピッカー コントロール](~/concepts/device-capabilities/people-picker-capability.md)
