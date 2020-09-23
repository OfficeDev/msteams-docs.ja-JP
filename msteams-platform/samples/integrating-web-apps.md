---
author: heath-hamilton
description: 既存の web アプリケーションを Microsoft Teams と統合するためのベストプラクティス
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Web アプリを Microsoft Teams と統合する
ms.openlocfilehash: e7d4f74526f7a71fe33d5a70d9ed60be960adefc
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210273"
---
# <a name="integrate-web-apps-with-teams"></a>Web アプリを Teams と統合する

Teams のソーシャル機能とコラボレーション機能によく当てはまる web アプリがありますか。 これらのガイドラインは、次の種類のアプリを統合する方法を理解するのに役立ちます。

* **スタンドアロンアプリ**: Teams では、1ページのアプリまたは大規模で複雑なアプリのいずれかを使用することができます。
* **コラボレーションアプリ**: Teams に固有のソーシャル機能とコラボレーション機能のために既に構築されているアプリ。
* **Sharepoint**: Teams に表示する sharepoint ページ。

各ガイドラインについて、統合シナリオに該当するかどうかを確認できます。

## <a name="get-to-know-teams-platform-capabilities"></a>Teams プラットフォームの機能を理解する

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint *

Teams アプリには、共同作業の際にユーザーが必要とする機能を含めることができますが、Teams 開発の用語についてはよくありません。

|一般的なアプリの機能   |Teams プラットフォームの機能   |
|----------|-----------|
|埋め込まれた web ページ、ホームページ、または webview  |[タブ](../tabs/what-are-tabs.md)  |
|共有のショートカットと拡張機能  |[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|アクションのショートカットと拡張機能  |[メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[ボット](../bots/what-are-bots.md) |
|チャネル通知  |[ボット](../bots/what-are-bots.md)<br/>[受信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 コネクタ](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|メッセージ外部サービス  |[ボット](../bots/what-are-bots.md)<br/>[送信 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modals  |[タスク モジュール](../task-modules-and-cards/what-are-task-modules.md)  |
|コンテンツの豊富なカード  |[アダプティブ カード](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>機能のサブセットを決定する

***統合シナリオ**: スタンドアロンアプリ *

既存のアプリケーションのすべての機能を Teams に統合することにより、多くの場合、特に大規模なアプリでは、強制または不自然なユーザー環境が発生します。 インパクトのほとんどの機能から始めて、Teams でより自然に統合するものを検討してください。 常に、ユーザーがメインアプリを起動して、機能の完全なセットにアクセスできるようにすることを忘れないでください。

技術的な作業を開始する前に、Teams アプリの計画を行います。

1. [アプリのユースケースを Teams プラットフォームの機能にマップ](../concepts/design/map-use-cases.md)します。
1. [アプリのエントリポイントを決定](../concepts/extensibility-points.md)します。 個人利用、グループ作業、またはその両方を対象としていますか?

## <a name="understand-sharepoint-requirements-and-options"></a>SharePoint の要件とオプションについて

***統合シナリオ**: SharePoint *

既存の [SharePoint ページ](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) を Teams タブとして統合することができます。次の点に注意してください。

* SharePoint Online の *モダン* ページである必要があります。
* 個人用タブのみがサポートされています (ページを [チャネル] タブとして統合することはできません)

または、 [SharePoint Framework を使用して](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)Teams タブを作成することもできます。

## <a name="aim-towards-multi-tenancy"></a>マルチテナントを目指す

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint *

アプリが複数の組織で使用されている場合は、製品をスケーラブルで、配布を大幅に簡素化するマルチテナントのホスティングを検討してください。

## <a name="review-your-apis"></a>Api を確認する

***統合シナリオ**: スタンドアロンアプリ、グループ作業アプリ *

Teams と統合する場合、アプリの既存の Api とデータ構造がアプリを完全にサポートしないことを前提としていません。 [Id マッピング](../concepts/authentication/configure-identity-provider.md)、[ディープリンクサポート](../concepts/build-and-test/deep-links.md)、 [Microsoft Graph の組み込み](https://docs.microsoft.com/graph/teams-concept-overview)に関する Teams に関するコンテキスト情報を使用して、これらを拡張する必要がある場合があります。

Teams [タブ](../tabs/how-to/access-teams-context.md) または [bot](../bots/how-to/get-teams-context.md)のコンテキスト取得の詳細について説明します。

## <a name="understand-authentication-options"></a>認証オプションについて

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint *

Azure Active Directory (AD) は Teams の id プロバイダーです。 アプリで異なる id プロバイダーを使用する場合は、id マッピングの実習または Azure AD とのフェデレーションのどちらかを実行する必要があります。

Teams には、サードパーティ製アプリ用の Azure AD のシングルサインオン (SSO) メカニズムと、OAuth や Open ID Connect (OIDC) などの標準を使用する他の id プロバイダーへの認証フローに関するガイダンスがあります。

SharePoint ページの場合、sso のみを使用でき、別のアプリ (ID は SharePoint アプリ) に SSO を使用する場合は、別の Azure AD ID を追加することはできません。

[Teams での認証の](../concepts/authentication/authentication.md)詳細について説明します。

## <a name="follow-teams-design-guidelines"></a>Teams 設計ガイドラインに従う

***統合シナリオ**: スタンドアロンアプリ、グループ作業アプリ *

一般に、アプリは Teams で自然に感じられます。 既存のアプリコンテンツを Teams タブに移行することは十分ですが、アプリは [teams 設計ガイドライン](../concepts/design/understand-use-cases.md)に従うことを強くお勧めします。 「 [Fluent Design System](https://fluentsite.z22.web.core.windows.net/)」も参照してください。

## <a name="maximize-deep-linking"></a>ディープリンクを最大化する

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint *

Teams のほぼすべてのことは、 [ディープリンク](../concepts/build-and-test/deep-links.md)を使用して直接リンクすることができます。 アプリでは、特定のメッセージとタブコンテンツとの間のリンクを含め、これらの使用を最大化する必要があります。 深いリンクは、多くの場合、ネイティブなチームの環境でアプリの複数の要素を結合します。

## <a name="be-smart-when-messaging-users"></a>メッセージングユーザーにとって賢い

***統合シナリオ**: スタンドアロンアプリ、コラボレーションアプリ、SharePoint *

Teams アプリが今すぐに送信する可能性があるメッセージの種類と長期間について検討します。 アプリにマルチスレッドの会話があると考えられる場合、 [bot](../bots/what-are-bots.md) は [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)よりも高い柔軟性を提供します。

また、ボットを使用すると、個々のユーザーやチャネルに *予防的なメッセージ* を送信することもできます。 これらのメッセージは、外部イベントによってトリガーされるメッセージであり、bot に送信されるメッセージではありません。 (たとえば、ボットがインストールされているときに、または新しいユーザーがチャネルに参加したときに、ウェルカムメッセージを送信することができます)。 

予防的なメッセージを送信するには Teams 固有の識別子が必要です。この情報は、 [名簿またはユーザープロファイルデータを取得](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile)したり、 [会話イベントにサブスクライブ](../bots/how-to/conversations/subscribe-to-conversation-events.md)したり、 [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging)を使用したりすることで取得できます。

過剰なメッセージがある場合は、スパムではないことに注意してください。 Teams 機能でサポートされている場合は、ユーザーがアプリの通知設定を構成することを検討してください (たとえば、[非表示メッセージを送信しない])。

## <a name="use-sharepoint-for-file-and-data-storage"></a>ファイルとデータの記憶域に SharePoint を使用する

***統合シナリオ:** スタンドアロンアプリ、グループ作業アプリ、SharePoint ページ*

チームを作成すると、 [SharePoint サイトコレクション](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) も、そのチームのファイルとデータストレージをサポートするように準備されます。 アプリは、ファイルを操作する場合にこの機能を利用することができます。 サイトコレクションを使用して、SharePoint リストおよび Excel の生データを保存することもできます。
