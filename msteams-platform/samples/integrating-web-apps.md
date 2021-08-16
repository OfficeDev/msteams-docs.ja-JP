---
author: heath-hamilton
description: 既存の Web アプリとアプリを統合するためのベスト プラクティスMicrosoft Teams
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web アプリ
ms.openlocfilehash: ba34241186484bb838ba3f61e5ca55914115a1f1
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345761"
---
# <a name="web-apps"></a>Web アプリ 

Web アプリを適切に統合することで、Teamsのソーシャル機能や共同作業機能に適Teams。
  
アプリと統合できるさまざまな種類のアプリはTeams次のとおりです。
* **スタンドアロン アプリ**: スタンドアロン アプリは、単一ページまたは大規模で複雑なアプリです。 ユーザーは、その一部の側面をTeams。
* **コラボレーション アプリ**: ソーシャル機能とコラボレーション機能に固有のアプリが既に構築Teams。
* **SharePoint**: SharePointに表示するページTeams。

統合シナリオに該当する適切なガイドラインをマップして従えます。
このドキュメントでは、Teams 機能の概要、ファイルとデータストレージの共有ポイント要件、API 要件、認証、アプリと Teams のディープリンクについて説明します。
 
## <a name="get-to-know-teams-platform-capabilities"></a>プラットフォームの機能Teamsする

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

アプリTeams必要な共同作業機能を含める必要があります。 アプリの統合を操作するには、開発用語を理解Teams重要です。

|アプリの一般的な機能   |Teams機能   |
|----------|-----------|
|埋め込み Web ページ、ホームページ、または Web ビュー  |[タブ](../tabs/what-are-tabs.md)  |
|ショートカットと拡張機能を共有する  |[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|操作のショートカットと拡張機能  |[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|チャットボット  |[ボット](../bots/what-are-bots.md) |
|チャネル通知  |[ボット](../bots/what-are-bots.md)<br/>[受信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 コネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|メッセージ外部サービス  |[ボット](../bots/what-are-bots.md)<br/>[送信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|モーダル  |[タスク モジュール](../task-modules-and-cards/what-are-task-modules.md)  |
|コンテンツが豊富なカード  |[アダプティブ カード](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>機能のサブセットを決定する

***統合シナリオ**: スタンドアロン アプリ*

既存のアプリケーションのすべての機能をアプリケーションに統合Teams、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスが発生します。 最も影響の大きな機能と、より自然に機能と統合する機能からTeams。 ユーザーがメイン アプリを起動し、一連の機能にアクセスできます。

**アプリとアプリを統合するための前提条件Teams** アプリとアプリを統合するための前提条件は次Teams。 

1. [アプリの使用例をプラットフォームの機能Teamsマップします](../concepts/design/map-use-cases.md)。
1. [アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。 個人の使用、共同作業、または両方の目的ですか?

## <a name="understand-sharepoint-requirements-and-options"></a>要件SharePointオプションについて理解する

***統合シナリオ**: SharePoint*

既存のページを[[SharePoint]](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites)タブTeams統合するには、次の点を考慮する必要があります。

* 最新のオンライン ページ *SharePoint* 必要があります。
* 個人用タブのみサポートされます。 ページをチャネル タブとして統合することはできません。

または、タブを使用してTeamsタブ[を作成SharePoint Framework。](/sharepoint/dev/spfx/integrate-with-teams-introduction)

## <a name="aim-towards-multi-tenancy"></a>マルチテナントを目指す

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

アプリが複数の組織で使用されている場合は、製品の拡張性を高め、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。

## <a name="review-your-apis"></a>API を確認する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

アプリと統合する場合は、アプリの既存の API とデータ構造がアプリをサポートTeams。 サポートを拡張するには、ID マッピング、ディープ リンク サポート、Microsoft Graph の組み[](../concepts/authentication/configure-identity-provider.md)込みのために[](../concepts/build-and-test/deep-links.md)、Teams に関するコンテキスト情報を使用して API とデータ構造を拡張する[必要があります](/graph/teams-concept-overview)。

詳細については、「ユーザー設定]タブまたはボットのコンテキストTeamsを取得[する](../bots/how-to/get-teams-context.md)[」を](../tabs/how-to/access-teams-context.md)参照してください。

## <a name="understand-authentication-options"></a>認証オプションについて

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Azure Active Directory (AD) は、ユーザーの ID プロバイダー Teams。 アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を実行するか、Azure の ID プロバイダーと組み合わせるAD。

Teamsサード パーティ製アプリ向け Azure ADシングル サインオン (SSO) メカニズムがあります。 また、OIDC と呼ばれる OAuth や Open ID などの標準を使用して、他の ID プロバイダー Connectガイダンスを提供します。

> [!IMPORTANT]
> 現在、サード パーティ製アプリは Government Community Cloud (GCC) で利用できますが、GCC-High国防総省 (DOD) では使用できません。 サード パーティ製アプリは、既定では無効になっています。GCC。 アプリのサード パーティ製アプリを有効GCC、[アプリのアクセス](/microsoftteams/teams-app-permission-policies)許可ポリシーの管理とアプリの管理に[関するページをご覧ください](/microsoftteams/manage-apps)。

このSharePointでは、SSO のみを使用できます。また、SSO を別のアプリで使用する場合は、別の Azure AD ID を追加することはできません。この ID はアプリの SharePoint です。

認証の詳細[については、「Teams」 を参照してください](../concepts/authentication/authentication.md)。

## <a name="follow-teams-design-guidelines"></a>設計Teamsに従う

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

アプリをアプリ[Teamsネイティブに](../concepts/design/understand-use-cases.md)するための設計ガイドラインに従Teams。 既存のアプリ コンテンツを [アプリ] タブTeamsできません。アプリの設計の詳細については、「アプリの設計」[をFluent Design System。](https://fluentsite.z22.web.core.windows.net/)

## <a name="maximize-deep-linking"></a>ディープ リンクを最大化する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

情報と機能へのリンクは、Teams。 ディープ[リンクを使用](../concepts/build-and-test/deep-links.md)してアプリとアプリTeamsリンクし、アプリの複数の部分を結び付け、よりネイティブなエクスペリエンスTeamsします。

## <a name="be-smart-when-messaging-users"></a>メッセージング ユーザーがスマートになる

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Webhook[よりも柔軟性が](../bots/what-are-bots.md)高Teams、マルチスレッドの会話にアプリで[ボットを使用します](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

ボットでは、個々のユーザーまたは **チャネルにプロ** アクティブ メッセージを送信することもできます。 プロアクティブ メッセージは、ボットに送信されるメッセージではなく、外部イベントによってトリガーされるプロプロンプトされていないメッセージです。 たとえば、ボットがインストールされている場合、または新しいユーザーがチャネルに参加するときに、ボットからウェルカム メッセージが送信されます。 

プロアクティブ メッセージの送信には、Teams固有の識別子が必要です。 この情報は、名簿[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)またはユーザー プロファイル データのフェッチ、[](../bots/how-to/conversations/subscribe-to-conversation-events.md)会話イベントのサブスクライブ、または Microsoft Graph[を使用して取得できます](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams)。

過剰なメッセージを持つユーザーに迷惑メールを送信しない。 この機能Teamsサポートしている場合、ユーザーはアプリの通知設定を構成できます。   
通知メッセージの例を次に示します。プロンプトされていないメッセージ **は送信しません**。

## <a name="use-sharepoint-for-file-and-data-storage"></a>ファイルSharePointストレージに使用する

***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*

チームが作成されると、そのチーム[](/microsoftteams/sharepoint-onedrive-interact)SharePointファイルとデータ ストレージをサポートするサイト コレクションも準備されます。 アプリがファイルを操作する場合は、この機能を活用する必要があります。 サイト コレクションを使用して、生データを [リスト] および [SharePoint] にExcel。

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
