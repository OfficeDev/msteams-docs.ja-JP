---
author: heath-hamilton
description: 既存の Web アプリとアプリを統合するためのベスト プラクティスMicrosoft Teams
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: medium
ms.topic: conceptual
title: 統合のTeams検討事項
ms.openlocfilehash: 0e80a051bb3964b3ade44e1f2c60fe4bf2242138
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518472"
---
# <a name="considerations-for-teams-integration"></a>統合のTeams検討事項 

Web アプリを適切に統合することで、Teamsのソーシャル機能や共同作業機能に適Teams。
  
アプリと統合できるさまざまな種類のアプリはTeams次のとおりです。
* **スタンドアロン アプリ**: スタンドアロン アプリは、単一ページまたは大規模で複雑なアプリです。 ユーザーは、その一部の側面をTeams。
* **コラボレーション アプリ**: ユーザーに固有のソーシャル機能と共同作業機能用に既に構築Teams。
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
|チャネル通知  |[ボット](../bots/what-are-bots.md)<br/>[受信 Webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 コネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|メッセージ外部サービス  |[ボット](../bots/what-are-bots.md)<br/>[送信 Webhooks](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|モーダル  |[タスク モジュール](../task-modules-and-cards/what-are-task-modules.md)  |
|コンテンツが豊富なカード  |[アダプティブ カード](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>機能のサブセットを決定する

***統合シナリオ**: スタンドアロン アプリ*

既存のアプリケーションのすべての機能をアプリケーションに統合Teams、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスが発生します。 最も影響の大きな機能と、より自然に機能と統合する機能からTeams。 ユーザーがメイン アプリを起動し、一連の機能にアクセスできます。

**アプリとアプリを統合するための前提条件Teams**

1. [アプリの使用例をプラットフォームの機能Teamsマップします](../concepts/design/map-use-cases.md)。
1. [アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。 個人向け、共同作業用、または両方用ですか?

## <a name="understand-sharepoint-requirements-and-options"></a>要件SharePointオプションについて理解する

***統合シナリオ**: SharePoint*

既存のページを [SharePoint[]](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) タブTeams統合するには、次の点を考慮する必要があります。

* 最新のオンライン ページ *SharePoint* 必要があります。
* 個人用タブのみサポートされます。 ページをチャネル タブとして統合することはできません。

または、タブを使用してTeamsタブ[をSharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction)。

## <a name="aim-towards-multi-tenancy"></a>マルチテナントを目指す

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

アプリが複数の組織で使用されている場合は、マルチテナント ホスティングを検討してください。 これにより、製品の拡張性が高く、配布が簡素化されます。

## <a name="review-your-apis"></a>API を確認する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

アプリの API とデータ構造は、アプリと統合するときにアプリをサポートするTeams。 サポートを拡張するには、ID マッピング、ディープリンク サポート、Microsoft Graph の組み込みのために、Teams に[](../concepts/authentication/configure-identity-provider.md)関するコンテキスト[](../concepts/build-and-test/deep-links.md)情報を使用して API とデータ構造を拡張する[必要があります](/graph/teams-concept-overview)。

[ユーザー] タブまたはボットのコンテキストをTeams[する方法を](../tabs/how-to/access-teams-context.md)参照[してください](../bots/how-to/get-teams-context.md)。

## <a name="understand-authentication-options"></a>認証オプションについて

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Azure Active Directoryは、ユーザーの ID プロバイダー Teams。 アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を行う必要があります。または id マッピングとMicrosoft Azure Active Directory (Azure AD)。

Teamsサード パーティ製アプリ用のシングル サインオン (SSO) メカニズムMicrosoft Azure Active Directory (Azure AD) があります。 また、OIDC と呼ばれる OAuth や Open ID などの標準を使用して、他の ID プロバイダー Connectガイダンスを提供します。

> [!IMPORTANT]
> 現在、サード パーティ製アプリは Government Community Cloud (GCC) で利用できますが、GCC-High国防総省 (DOD) では使用できません。 サード パーティ製アプリは、既定では無効になっています。GCC。 アプリのサードパーティ 製アプリを有効にするGCC、[アプリのアクセス](/microsoftteams/teams-app-permission-policies)許可ポリシーの管理とアプリの[管理に関するページをご覧ください](/microsoftteams/manage-apps)。

SHAREPOINT ページの場合は、SSO のみを使用し、ID が SharePoint アプリであるとして SSO を別のアプリで動作する場合は、別の Microsoft Azure Active Directory (Azure AD) ID を追加できません。

認証の詳細[については、](../concepts/authentication/authentication.md)Teams。

## <a name="follow-teams-design-guidelines"></a>設計Teamsに従う

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

アプリをアプリ[Teamsネイティブに](../concepts/design/understand-use-cases.md)するための設計ガイドラインに従Teams。 既存のアプリ コンテンツを [アプリ] タブTeamsできません。アプリの設計の詳細については、「アプリの設計」[を参照Fluent Design System](https://fluentsite.z22.web.core.windows.net/)。

## <a name="maximize-deep-linking"></a>ディープ リンクを最大化する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams 内の情報や機能へのリンクを作成できます。 ディープ [リンクを使用](../concepts/build-and-test/deep-links.md)してアプリとアプリTeamsリンクし、アプリの複数の部分を結び付け、よりネイティブなエクスペリエンスTeamsします。

## <a name="be-smart-when-messaging-users"></a>メッセージング ユーザーがスマートになる

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Webhook [よりも柔軟性](../bots/what-are-bots.md)が高Teams、マルチスレッド会話を行う場合は、アプリで[ボットを使用します](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

ボットでは、個々のユーザーまたは **チャネルにプロ** アクティブ メッセージを送信することもできます。 プロアクティブ メッセージは、ボットに送信されるメッセージではなく、外部イベントによってトリガーされるプロプロンプトされていないメッセージです。 たとえば、ボットがインストールされている場合、または新しいユーザーがチャネルに参加するときに、ボットからウェルカム メッセージが送信されます。

プロアクティブ メッセージの送信には、Teams固有の識別子が必要です。 情報を取得するには、名[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)簿またはユーザー プロファイル データをフェッチするか、[](../bots/how-to/conversations/subscribe-to-conversation-events.md)会話イベントをサブスクライブするか、[Microsoft](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams) Graph。

過剰なメッセージを持つユーザーに迷惑メールを送信しない。 この機能Teamsサポートしている場合、ユーザーはアプリの通知設定を構成できます。
通知メッセージの例を次に示します **。プロ** ンプトされていないメッセージは送信しません。

## <a name="use-sharepoint-for-file-and-data-storage"></a>ファイルSharePointストレージに使用する

***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*

チームが作成されると、そのチーム[](/microsoftteams/sharepoint-onedrive-interact)SharePointファイルとデータ ストレージをサポートするサイト コレクションも準備されます。 アプリがファイルを操作する場合は、この機能を活用する必要があります。 サイト コレクションを使用して、生データを [リストとSharePointに保存Microsoft Excel。

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [低コードおよびコードなしソリューションのMicrosoft Teams](~/samples/teams-low-code-solutions.md)
* [[Teams で共有] ボタンを作成する](../concepts/build-and-test/share-to-teams.md)
* [SameSite cookie 属性](~/resources/samesite-cookie-update.md)
* [チャットボットPower Virtual Agents統合](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
