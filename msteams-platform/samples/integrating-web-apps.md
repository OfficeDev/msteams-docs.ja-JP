---
author: heath-hamilton
description: 既存の Web アプリと Microsoft Teamsを統合するためのベスト プラクティスまたは考慮事項
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: medium
ms.topic: conceptual
title: Teams統合に関する考慮事項
ms.openlocfilehash: bbd5b046d7b1afca5cc3fa5c8afb21a3698f43eb
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104351"
---
# <a name="considerations-for-teams-integration"></a>Teams統合に関する考慮事項

web アプリをTeamsと適切に統合することで、Teamsのソーシャルおよびコラボレーション機能に適した Web アプリを作成できます。
  
Teamsと統合できるさまざまな種類のアプリは次のとおりです。

* **スタンドアロン アプリ**: スタンドアロン アプリは、単一ページまたは大規模で複雑なアプリです。 ユーザーは Teams でその一部の側面を使用できます。
* **コラボレーション アプリ**: Teams固有のソーシャル機能とコラボレーション機能用に既に構築されたアプリ。
* **SharePoint**: Teamsに表示するSharePoint ページ。

統合シナリオに適用される適切なガイドラインをマップして従うことができます。
このドキュメントでは、Teams機能の概要、ファイルとデータストレージの共有ポイント要件、API 要件、認証、Teamsとのアプリのディープ リンクについて説明します。

## <a name="get-to-know-teams-platform-capabilities"></a>プラットフォーム機能Teams理解する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams アプリには、必要で想定される共同作業機能が含まれている必要があります。 アプリの統合を操作するには、開発用語Teams理解しておくことが重要です。

|アプリの一般的な機能   |Teams プラットフォーム機能   |
|----------|-----------|
|埋め込み Web ページ、ホームページ、または Web ビュー  |[タブ](../tabs/what-are-tabs.md)  |
|ショートカットと拡張機能を共有する  |[メッセージ拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|アクションのショートカットと拡張機能  |[メッセージ拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots |[ボット](../bots/what-are-bots.md) |
|チャネル通知  |[ボット](../bots/what-are-bots.md)<br/>[受信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 コネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|メッセージ外部サービス  |[ボット](../bots/what-are-bots.md)<br/>[送信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|モーダル  |[タスク モジュール](../task-modules-and-cards/what-are-task-modules.md)  |
|コンテンツリッチ カード  |[アダプティブ カード](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>機能のサブセットを決定する

***統合シナリオ**: スタンドアロン アプリ*

既存のアプリケーションのすべての機能をTeamsに統合すると、多くの場合、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスにつながります。 最もインパクトのある機能と、より自然にTeamsと統合する機能から始めます。 ユーザーがメイン アプリを起動し、その機能の完全なセットにアクセスできるようにします。

アプリとTeamsを統合するための前提条件を次に示します。

1. [アプリのユース ケースをTeams プラットフォーム機能にマップします](../concepts/design/map-use-cases.md)。
1. [アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。 個人的な使用、コラボレーション、またはその両方に対してですか?

## <a name="understand-sharepoint-requirements-and-options"></a>SharePointの要件とオプションについて理解する

***統合シナリオ**: SharePoint*

既存の[SharePoint ページを Teams](/sharepoint/dev/general-development/overview-of-the-sharepoint-page-model) タブとして統合するには、次の点を考慮する必要があります。

* *最新* のSharePoint オンライン ページである必要があります。
* 個人用タブのみがサポートされます。 ページをチャネル タブとして統合することはできません。

または、SharePoint Frameworkを[使用して](/sharepoint/dev/spfx/integrate-with-teams-introduction)Teams タブを作成することもできます。

## <a name="aim-towards-multitenancy"></a>マルチテナントを目指す

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

アプリが複数の組織で使用されている場合は、マルチテナント ホスティングを検討してください。 これにより、製品がスケーラブルになり、配布が簡略化されます。

## <a name="review-your-apis"></a>API を確認する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

アプリの API とデータ構造は、Teamsと統合するときにアプリをサポートする必要があります。 サポートを拡張するには、[ID マッピング](../concepts/authentication/configure-identity-provider.md)、[ディープ リンク](../concepts/build-and-test/deep-links.md) サポート、Microsoft Graphの[組み込み](/graph/teams-concept-overview)のためのTeamsに関するコンテキスト情報を使用して API とデータ構造を拡張する必要があります。

Teams タブまたは[ボット](../bots/how-to/get-teams-context.md)のコンテキストを取得する方法について説明[します](../tabs/how-to/access-teams-context.md)。

## <a name="understand-authentication-options"></a>認証オプションについて

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Azure Active Directoryは、Teamsの ID プロバイダーです。 アプリで別の ID プロバイダーを使用している場合は、ID マッピングの演習を実行するか、Microsoft Azure Active Directory (Azure AD) と組み合わせる必要があります。

Teamsには、サード パーティ製アプリのAzure ADを備えたシングル サインオン (SSO) メカニズムがあります。 また、OAuth や Open ID Connect (OIDC) などの標準を使用して、他の ID プロバイダーへの認証フローのガイダンスも提供されます。

> [!IMPORTANT]
> 現在、サード パーティ製アプリはGovernment Community Cloud (GCC) で利用できますが、GCC-Highおよび国防総省 (DOD) では使用できません。 GCCでは、サード パーティ製アプリは既定で無効になっています。 GCCのサード パーティ製アプリを有効にするには、[アプリのアクセス許可ポリシーの管理とアプリの管理に関するページ](/microsoftteams/teams-app-permission-policies)を参照してください。[](/microsoftteams/manage-apps)

SharePoint ページでは、SSO のみを使用でき、ID がSharePoint アプリであるため、SSO を別のアプリで動作させる場合は、別のAzure AD ID を追加できません。

[Teamsでの認証の](../concepts/authentication/authentication.md)詳細については、こちらを参照してください。

## <a name="follow-teams-design-guidelines"></a>Teams設計ガイドラインに従う

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

[アプリをTeamsにネイティブにするには、Teams設計ガイドライン](../concepts/design/understand-use-cases.md)に従ってください。 既存のアプリ コンテンツを Teams タブに移行することはできません。アプリの設計の詳細については、「[Fluent Design System](https://fluentsite.z22.web.core.windows.net/)」を参照してください。

## <a name="maximize-deep-linking"></a>ディープ リンクを最大化する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams 内の情報や機能へのリンクを作成できます。 [ディープ リンク](../concepts/build-and-test/deep-links.md)を使用して、アプリをTeamsにリンクします。アプリの複数の部分を結び付けて、よりネイティブなTeamsエクスペリエンスを実現します。

## <a name="be-smart-when-messaging-users"></a>ユーザーにメッセージを送信するときにスマートにする

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

[webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) よりも柔軟性が高いため、マルチスレッド会話にはTeams アプリで[ボット](../bots/what-are-bots.md)を使用します。

ボットでは、個々のユーザーまたはチャネルに **プロアクティブ メッセージ** を送信することもできます。 プロアクティブ メッセージは、外部イベントによってトリガーされるプロアクティブメッセージであり、ボットに送信されるメッセージではありません。 たとえば、ボットがインストールされたとき、または新しいユーザーがチャネルに参加したときに、ウェルカム メッセージを送信します。

プロアクティブ メッセージを送信するには、Teams固有の識別子が必要です。 情報をキャプチャするには、[名簿またはユーザー プロファイル データをフェッチ](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)するか、[会話イベントをサブスクライブ](../bots/how-to/conversations/subscribe-to-conversation-events.md)するか、[Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams)を使用します。

過剰なメッセージでユーザーをスパムにしないでください。 Teams機能でサポートされている場合、ユーザーはアプリの通知設定を構成できます。
通知メッセージの例を次に示します。 **プロンプトメッセージを送信しないでください**。

## <a name="use-sharepoint-for-file-and-data-storage"></a>ファイルとデータストレージにSharePointを使用する

***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*

チームが作成されると、そのチームのファイルとデータストレージをサポートするために、[SharePointサイト コレクション](/microsoftteams/sharepoint-onedrive-interact)もプロビジョニングされます。 アプリがファイルと対話する場合は、この機能を利用する必要があります。 サイト コレクションを使用して、SharePoint リストとMicrosoft Excelに生データを格納します。

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [Microsoft Teams用の低コードソリューションとコードなしソリューション](~/samples/teams-low-code-solutions.md)
* [Web アプリから Teams に共有する](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [SameSite cookie 属性](~/resources/samesite-cookie-update.md)
* [チャットボットPower Virtual Agents統合する](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
