---
author: heath-hamilton
description: 既存の Web アプリと Microsoft Teams を統合するためのベスト プラクティス
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: Web アプリを Microsoft Teams と統合する
ms.openlocfilehash: 4671d2277d5eb7c035421c51b1714eccaac06a31
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696487"
---
# <a name="integrate-web-apps-with-teams"></a>Web アプリを Teams と統合する

Teams のソーシャル機能や共同作業機能に自然に適合すると思う Web アプリはありますか? これらのガイドラインは、次の種類のアプリを統合する方法を理解するのに役立ちます。

* **スタンドアロン アプリ**: 単一ページ アプリまたは大規模で複雑なアプリで、Teams でユーザーがいくつかの側面を使用する場合があります。
* **コラボレーション アプリ**: Teams に固有のソーシャル機能と共同作業機能用に既に構築されたアプリ。
* **SharePoint**: Teams で表示する SharePoint ページ。

各ガイドラインについて、統合シナリオに該当する場合を確認できます。

## <a name="get-to-know-teams-platform-capabilities"></a>Teams プラットフォームの機能を知る

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams アプリには、共同作業時にユーザーが望む機能や期待できる機能を含め、Teams の開発用語に慣れていない可能性があります。

|アプリの一般的な機能   |Teams プラットフォームの機能   |
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

既存のアプリケーションのすべての機能を Teams に統合すると、多くの場合、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスが発生します。 最も影響の大きな機能と、Teams とより自然に統合される機能から始めるのを検討してください。 ユーザーがメイン アプリを起動し、一連の機能にアクセスできるのを常に許可できます。

技術的な作業を開始する前に、Teams アプリの計画を行います。

1. [アプリの使用例を Teams プラットフォームの機能にマップします](../concepts/design/map-use-cases.md)。
1. [アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。 個人の使用、共同作業、または両方の目的ですか?

## <a name="understand-sharepoint-requirements-and-options"></a>SharePoint の要件とオプションについて

***統合シナリオ**: SharePoint*

既存の [SharePoint](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) ページを Teams タブとして統合できます。次のことを覚えておいてください。

* 最新の *SharePoint* Online ページである必要があります
* 個人用タブだけがサポートされています (ページをチャネル タブとして統合できない)

または、SharePoint Framework を使用して [Teams タブを作成することもできます](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)。

## <a name="aim-towards-multi-tenancy"></a>マルチテナントを目指す

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

アプリが複数の組織で使用されている場合は、製品の拡張性を高め、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。

## <a name="review-your-apis"></a>API を確認する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

Teams と統合された場合、アプリの既存の API とデータ構造がアプリを完全にサポートすると想定していけない。 Id マッピング、ディープ リンクサポート、Microsoft Graph[](../concepts/authentication/configure-identity-provider.md)の組[](../concepts/build-and-test/deep-links.md)み込みのために、Teams に関するコンテキスト情報を使用してこれらを拡張[する必要がある場合があります](https://docs.microsoft.com/graph/teams-concept-overview)。

Teams タブまたはボットのコンテキストを取得する [方法について詳しくは、以下をご](../tabs/how-to/access-teams-context.md) 覧 [ください](../bots/how-to/get-teams-context.md)。

## <a name="understand-authentication-options"></a>認証オプションについて

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Azure Active Directory (AD) は Teams の ID プロバイダーです。 アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を行う必要があります。または Azure AD とフェデレーションする必要があります。

Teams には、サードパーティ アプリ用の Azure AD を使用したシングル サインオン (SSO) メカニズムと、OAuth や Open ID Connect (OIDC) などの標準を使用した他の ID プロバイダーへの認証フローのガイダンスがあります。

SharePoint ページの場合は、SSO のみを使用し、SSO を別のアプリ (ID は SharePoint アプリ) で動作する場合は、別の Azure AD ID を追加することはできません。

Teams での認証 [について詳しくは、次のページを参照してください](../concepts/authentication/authentication.md)。

## <a name="follow-teams-design-guidelines"></a>Teams の設計ガイドラインに従う

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

一般に、アプリは Teams で自然に感じる必要があります。 既存のアプリ コンテンツを Teams タブに移行する方法で十分だと思われる場合がありますが、Teams の設計ガイドラインに従ってアプリを使用することを強 [く推奨します](../concepts/design/understand-use-cases.md)。 「Fluent [Design System」も参照してください](https://fluentsite.z22.web.core.windows.net/)。

## <a name="maximize-deep-linking"></a>ディープ リンクを最大化する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams のほとんどすべての情報は、ディープ リンクを使用して直接 [リンクできます](../concepts/build-and-test/deep-links.md)。 アプリでは、特定のメッセージやタブ コンテンツへのリンクやタブ コンテンツへのリンクなど、これらを最大限に活用する必要があります。 ディープ リンクは、実際には複数のアプリを結び付け、よりネイティブな Teams エクスペリエンスを提供します。

## <a name="be-smart-when-messaging-users"></a>メッセージング ユーザーがスマートになる

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams アプリが現在および長期的に送信する可能性があるメッセージの種類を検討します。 アプリがマルチスレッドの会話を行う可能性がある場合、ボットは Webhook よりも柔軟性が[高い可能性があります](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)。 [](../bots/what-are-bots.md)

ボットでは、個々のユーザーまたは *チャネルにプロ* アクティブ メッセージを送信することもできます。 これらは、外部イベントによってトリガーされるプロンプトされていないメッセージであり、ボットに送信されるメッセージではありません。 (たとえば、ボットがインストールされている場合や、新しいユーザーがチャネルに参加するときに、ボットからウェルカム メッセージを送信できます)。

プロアクティブ メッセージを送信するには、Teams 固有の識別子が必要です。[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)この情報は、名簿またはユーザー[](../bots/how-to/conversations/subscribe-to-conversation-events.md)プロファイル データをフェッチしたり、会話イベントをサブスクライブしたり[、Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging)を使用して取得できます。

過剰なメッセージを持つユーザーに迷惑メールを送信しないように注意してください。 Teams 機能でサポートされている場合は、ユーザーにアプリの通知設定を構成させる (たとえば、「プロンプされていないメッセージを送信しない」など) を検討してください。

## <a name="use-sharepoint-for-file-and-data-storage"></a>ファイルおよびデータ ストレージに SharePoint を使用する

***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*

チームが作成されると、そのチームのファイルとデータ ストレージをサポートするために [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) サイト コレクションも準備されます。 アプリがファイルを操作する場合は、この機能を利用できます。また、この機能を利用する必要があります。 サイト コレクションを使用して、生データを SharePoint リストと Excel に保存することもできます。
