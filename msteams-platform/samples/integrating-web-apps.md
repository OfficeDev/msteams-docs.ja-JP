---
author: heath-hamilton
description: 既存の Web アプリと Microsoft Teams を統合するためのベスト プラクティス
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web アプリ
ms.openlocfilehash: 1f46c4a8b9457a00b5000e81c280759f584a50d2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020423"
---
# <a name="web-apps"></a>Web アプリ 

Web アプリを Teams と適切に統合することで、Teams のソーシャル機能や共同作業機能に適した Web アプリを作成できます。
  
Teams と統合できるさまざまな種類のアプリは次のとおりです。
* **スタンドアロン アプリ**: スタンドアロン アプリは、単一ページまたは大規模で複雑なアプリです。 ユーザーは Teams でいくつかの側面を使用できます。
* **コラボレーション アプリ**: Teams に固有のソーシャル機能と共同作業機能用に既に構築されたアプリ。
* **SharePoint**: Teams で表示する SharePoint ページ。

統合シナリオに該当する適切なガイドラインをマップして従えます。
このドキュメントでは、Teams の機能の概要、ファイルとデータストレージの共有ポイント要件、API 要件、認証、アプリと Teams のディープリンクについて説明します。
 
## <a name="get-to-know-teams-platform-capabilities"></a>Teams プラットフォームの機能を知る

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams アプリには、必要な共同作業機能と予期される共同作業機能が含まれる必要があります。 アプリの統合を操作するには、Teams 開発の用語を理解することが重要です。

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

既存のアプリケーションのすべての機能を Teams に統合すると、多くの場合、特に大規模なアプリでは、強制的または不自然なユーザー エクスペリエンスが発生します。 最も影響の大きな機能と、Teams とより自然に統合する機能から始める。 ユーザーがメイン アプリを起動し、一連の機能にアクセスできます。

**アプリを Teams に統合するための前提条件** アプリを Teams に統合するための前提条件を次に示します。 

1. [アプリの使用例を Teams プラットフォームの機能にマップします](../concepts/design/map-use-cases.md)。
1. [アプリのエントリ ポイントを決定します](../concepts/extensibility-points.md)。 個人の使用、共同作業、または両方の目的ですか?

## <a name="understand-sharepoint-requirements-and-options"></a>SharePoint の要件とオプションについて

***統合シナリオ**: SharePoint*

既存の [SharePoint](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) ページを Teams タブとして統合するには、次の点を考慮する必要があります。

* 最新の SharePoint *オンライン* ページである必要があります。
* 個人用タブのみサポートされます。 ページをチャネル タブとして統合することはできません。

または、SharePoint Framework を使用して [Teams タブを作成することもできます](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)。

## <a name="aim-towards-multi-tenancy"></a>マルチテナントを目指す

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

アプリが複数の組織で使用されている場合は、製品の拡張性を高め、配布を大幅に簡素化するマルチテナント ホスティングを検討してください。

## <a name="review-your-apis"></a>API を確認する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

Teams と統合する場合は、アプリの既存の API とデータ構造がアプリをサポートする必要があります。 サポートを拡張するには、ID マッピング、ディープ リンク サポート、および Microsoft Graph[](../concepts/authentication/configure-identity-provider.md)の組[](../concepts/build-and-test/deep-links.md)み込みのために、Teams に関するコンテキスト情報を使用して API とデータ構造を[拡張する必要があります](https://docs.microsoft.com/graph/teams-concept-overview)。

Teams タブまたはボットのコンテキストを取得する [方法について詳しくは、以下をご](../tabs/how-to/access-teams-context.md) 覧 [ください](../bots/how-to/get-teams-context.md)。

## <a name="understand-authentication-options"></a>認証オプションについて

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Azure Active Directory (AD) は Teams の ID プロバイダーです。 アプリで別の ID プロバイダーを使用する場合は、ID マッピングの演習を実行するか、Azure の ID プロバイダーと組み合わせるAD。

Teams には、サード パーティ製アプリ用の Azure ADシングル サインオン (SSO) メカニズムがあります。 また、OIDC と呼ばれる OAuth や Open ID Connect などの標準を使用して、他の ID プロバイダーに対する認証フローのガイダンスも提供します。

SharePoint ページの場合は、SSO のみを使用し、その ID が SharePoint アプリであるとして SSO を別のアプリで動作する場合は、別の Azure AD ID を追加できません。

Teams での認証 [について詳しくは、次のページを参照してください](../concepts/authentication/authentication.md)。

## <a name="follow-teams-design-guidelines"></a>Teams の設計ガイドラインに従う

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ*

Teams のデザイン [ガイドラインに従って、](../concepts/design/understand-use-cases.md) アプリを Teams にネイティブにしてください。 既存のアプリ コンテンツを Teams タブに移行することはできません。アプリの設計の詳細については [、「Fluent Design System」を参照してください](https://fluentsite.z22.web.core.windows.net/)。

## <a name="maximize-deep-linking"></a>ディープ リンクを最大化する

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Teams 内で情報と機能へのリンクを作成できます。 ディープ [リンクを使用](../concepts/build-and-test/deep-links.md) してアプリを Teams とリンクし、複数のアプリを結び付け、よりネイティブな Teams エクスペリエンスを提供します。

## <a name="be-smart-when-messaging-users"></a>メッセージング ユーザーがスマートになる

***統合シナリオ**: スタンドアロン アプリ、コラボレーション アプリ、SharePoint*

Webhook [よりも柔軟性](../bots/what-are-bots.md) が高い Teams アプリのボットをマルチスレッド会話に [使用します](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

ボットでは、個々のユーザーまたは **チャネルにプロ** アクティブ メッセージを送信することもできます。 プロアクティブ メッセージは、ボットに送信されるメッセージではなく、外部イベントによってトリガーされるプロプロンプトされていないメッセージです。 たとえば、ボットがインストールされている場合、または新しいユーザーがチャネルに参加するときに、ボットからウェルカム メッセージが送信されます。 

プロアクティブ メッセージを送信するには、Teams 固有の識別子が必要です。 この情報は、名簿[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)またはユーザー プロファイル データのフェッチ、[](../bots/how-to/conversations/subscribe-to-conversation-events.md)会話イベントのサブスクライブ、または Microsoft Graph を使用して[取得できます](https://docs.microsoft.com/graph/teams-proactive-messaging)。

過剰なメッセージを持つユーザーに迷惑メールを送信しない。 Teams 機能でサポートされている場合、ユーザーはアプリの通知設定を構成できます。   
通知メッセージの例を次に示します。プロンプトされていないメッセージ **は送信しません**。

## <a name="use-sharepoint-for-file-and-data-storage"></a>ファイルおよびデータ ストレージに SharePoint を使用する

***統合シナリオ:** スタンドアロン アプリ、コラボレーション アプリ、SharePoint ページ*

チームが作成されると、そのチームのファイルとデータ ストレージをサポートするために [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) サイト コレクションも準備されます。 アプリがファイルを操作する場合は、この機能を活用する必要があります。 サイト コレクションを使用して、生データを SharePoint リストと Excel に格納します。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
