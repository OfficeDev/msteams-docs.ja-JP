---
author: heath-hamilton
description: 既存の Web アプリをMicrosoft Teamsと統合するためのベスト プラクティス
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web アプリ
ms.openlocfilehash: 6783a05079f876cf3c2475a0ad5ca0e1f6687fc4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566223"
---
# <a name="web-apps"></a>Web アプリ 

web アプリをTeamsと適切に統合することで、Teamsのソーシャル機能とコラボレーション機能に適したものにすることができます。
  
Teamsと統合できるさまざまな種類のアプリは次のとおりです。
* **スタンドアロン アプリ**: スタンドアロン アプリは、シングル ページまたは大規模で複雑なアプリです。 ユーザーは、Teamsで、その一部の側面を使用できます。
* **コラボレーションアプリ**: Teamsに固有のソーシャルおよびコラボレーション機能用に既に構築されたアプリ。
* **SharePoint**: Teamsに表示するSharePointページ。

統合シナリオに適用可能な適切なガイドラインをマップして従うことができます。
このドキュメントでは、Teams機能、ファイルとデータのストレージに対する共有ポイント要件、API 要件、認証、およびアプリとTeamsとのディープ リンクの概要を説明します。
 
## <a name="get-to-know-teams-platform-capabilities"></a>プラットフォームの機能Teams知る

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint*

Teamsアプリには、必要なコラボレーション機能と必要なコラボレーション機能が含まれている必要があります。 アプリの統合を操作するには、開発用語Teams理解することが重要です。

|アプリの一般的な機能   |Teamsプラットフォーム機能   |
|----------|-----------|
|埋め込みウェブページ、ホームページ、またはウェブビュー  |[タブ](../tabs/what-are-tabs.md)  |
|ショートカットと拡張機能を共有する  |[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|アクションのショートカットと拡張機能  |[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|チャットボット  |[ボット](../bots/what-are-bots.md) |
|チャンネル通知  |[ボット](../bots/what-are-bots.md)<br/>[受信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 コネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|メッセージ外部サービス  |[ボット](../bots/what-are-bots.md)<br/>[送信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|モーダル  |[タスク モジュール](../task-modules-and-cards/what-are-task-modules.md)  |
|コンテンツが豊富なカード  |[アダプティブ カード](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>機能のサブセットを決定する

***統合シナリオ**: スタンドアロン アプリ*

既存のアプリケーションのすべての機能をTeamsに統合すると、特に大規模なアプリでは、強制的なユーザー エクスペリエンスや不自然なユーザー エクスペリエンスが実現することがよくあります。 最もインパクトのある機能と、より自然にTeamsと統合する機能から始めましょう。 ユーザーがメイン アプリを起動し、その機能の完全なセットにアクセスすることを許可できます。

**アプリをTeamsと統合するための前提条件** アプリをTeamsに統合するための前提条件を次に示します。 

1. [アプリのユース ケースをプラットフォームの機能にTeamsマップ](../concepts/design/map-use-cases.md)する 。
1. [アプリのエントリ ポイントを決定する](../concepts/extensibility-points.md): 個人的な使用、共同作業、またはその両方のためですか?

## <a name="understand-sharepoint-requirements-and-options"></a>SharePoint要件とオプションを理解する

***統合シナリオ**: SharePoint*

既存の[SharePointページ](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites)をTeamsタブとして統合するには、次の点を考慮する必要があります。

* *これは、最新* のSharePointオンラインページでなければなりません。
* 個人用タブのみがサポートされます。 ページをチャンネル タブとして統合することはできません。

または、 SharePoint Framework を[使用して](/sharepoint/dev/spfx/integrate-with-teams-introduction)Teams タブを作成することもできます。

## <a name="aim-towards-multi-tenancy"></a>マルチテナンシーを目指す

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint*

アプリが複数の組織で使用されている場合は、製品をスケーラブルにし、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。

## <a name="review-your-apis"></a>API の確認

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ*

Teamsと統合する場合は、アプリの既存の API とデータ構造がアプリをサポートする必要があります。 サポートを拡張するには[、ID マッピング](../concepts/authentication/configure-identity-provider.md)、[ディープリンク サポート](../concepts/build-and-test/deep-links.md)、および Microsoft Graph の[組み込み](/graph/teams-concept-overview)Teamsに関するコンテキスト情報を使用して、API とデータ構造を拡張する必要があります。

Teams[タブ](../tabs/how-to/access-teams-context.md)または[ボット](../bots/how-to/get-teams-context.md)のコンテキストの取得の詳細については、こちらをご覧ください。

## <a name="understand-authentication-options"></a>認証オプションについて

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint*

Azure Active Directory (AD) は、Teamsの ID プロバイダーです。 アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を行うか、Azure AD と組み合わせる必要があります。

Teamsには、サード パーティ製アプリ用の Azure AD とのシングル サインオン (SSO) メカニズムがあります。 また、OIDC と呼ばれる、OAuth や Open ID Connectなどの標準を使用して、他の ID プロバイダーへの認証フローのガイダンスも提供します。

SharePoint ページの場合、SSO のみを使用でき、ID が SharePoint アプリであるため、別のアプリで SSO を動作させたい場合は、別の Azure AD ID を追加することはできません。

認証の詳細については[、 Teams を参照](../concepts/authentication/authentication.md)してください。

## <a name="follow-teams-design-guidelines"></a>Teams設計ガイドラインに従う

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ*

アプリをネイティブ[Teams Teams](../concepts/design/understand-use-cases.md)に対応するように設計ガイドラインに従ってください。 既存のアプリ コンテンツをTeams タブに移行することはできません。アプリのデザインの詳細については[、「Fluent デザイン システム](https://fluentsite.z22.web.core.windows.net/)」を参照してください。

## <a name="maximize-deep-linking"></a>ディープリンクを最大化

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint*

Teams内の情報や機能へのリンクを作成できます。 [ディープ リンク](../concepts/build-and-test/deep-links.md)を使用して、アプリを複数のアプリを結び付けて、よりネイティブなTeamsエクスペリエンスを提供するTeamsとリンクします。

## <a name="be-smart-when-messaging-users"></a>ユーザーにメッセージを送信する際にスマートにする

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint*

[マルチ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)スレッドの会話にはTeamsアプリで[ボット](../bots/what-are-bots.md)を使用します。

ボットを使用すると、個々のユーザーまたはチャネルに **プロアクティブなメッセージ** を送信することもできます。 プロアクティブ メッセージは、外部イベントによってトリガーされるメッセージで、ボットに送信されるメッセージではありません。 たとえば、ボットがインストールされるとウェルカム メッセージを送信したり、新しいユーザーがチャネルに参加したりすると、ボットからウェルカム メッセージが送信されます。 

プロアクティブ メッセージを送信するには、Teams固有の識別子が必要です。 情報を取得するには、[名簿またはユーザー プロファイル データを取得](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)するか、[会話イベントを購読](../bots/how-to/conversations/subscribe-to-conversation-events.md)するか、または[Microsoft Graph](/graph/teams-proactive-messaging)を使用します。

過度のメッセージでユーザーをスパムしないでください。 Teams機能がサポートしている場合、ユーザーはアプリの通知設定を構成できます。   
次に、通知メッセージの例を示します: **メッセージを表示しないメッセージを送信しないでください**。

## <a name="use-sharepoint-for-file-and-data-storage"></a>ファイルとデータのストレージにSharePointを使用する

***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*

チームを作成すると、そのチームのファイルとデータの格納をサポートするために[、SharePointサイト コレクション](/microsoftteams/sharepoint-onedrive-interact)も準備されます。 アプリがファイルとやり取りする場合は、この機能を利用する必要があります。 サイト コレクションを使用して、SharePoint リストとExcelに生データを格納します。

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
