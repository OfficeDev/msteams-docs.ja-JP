---
title: 新機能
description: Microsoft Teams のすべての新しい開発者向け機能について説明します。
keywords: teams 新しい最新情報
ms.openlocfilehash: 28e83375ecbfec7f2adac14a4b5419a6cc40c61e
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434532"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Microsoft Teams の開発者向けの新機能

>[!TIP]
> 「 [**Teams アプリテンプレートカタログ**](samples/app-templates.md)」の「運用可能なテンプレート」を参照してください。 カタログはアルファベット順で、最新の追加内容にはスター **&#9734;** でタグが付けられます。

## <a name="change-log"></a>変更ログ

変更ログには、Microsoft Teams プラットフォームおよびこのドキュメントセットに対する変更が一覧表示されます。 場合によっては、Teams 開発者にとって重要な新しい機能に注意を向けるためにエントリを使用することがあります。

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
| 07/22/2020 |モバイルデバイスの機能の更新。|[Microsoft Teams タブのデバイスへのアクセス許可を要求する](~/tabs/how-to/native-device-permissions.md) |
|07/15/2020|Teams 用の仮想アシスタントを作成する|[Microsoft Teams の仮想アシスタント](samples/virtual-assistant.md)|
|07/14/2020|ネイティブの読み込みインジケーターのドキュメントを提示する|[ネイティブローディングインジケーターの表示](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
| 07/01/2020 |Visual Studio Code Toolkit を使用して Teams アプリの作成を開始します。|[Microsoft Teams Toolkit と Visual Studio コードを使用してアプリをビルドする](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Teams web およびデスクトップクライアント用のタブ (GA) のシングルサインオン|[シングルサインオン (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| バージョン1.7 に更新されたマニフェストスキーマ| [リファレンス: Microsoft Teams のマニフェストスキーマ](resources/schema/manifest-schema.md)|
| 05/20/2020 | Microsoft Graph Api を使用したリソース固有の同意アクセス許可は、開発者向けプレビューで表示されます。 |[リソース固有の同意 (RSC)-開発者プレビュー](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|Power Virtual Agent を Teams と統合する|[Power Virtual Agents chatbot を Microsoft Teams と統合する](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Teams の交代コネクタを使用して、WFM システムを統合する|[Microsoft Teams が WFM コネクタをシフトする](samples/shifts-wfm-connectors.md)
| 03/24/2020 | 会話の単一メンバーを取得するためのサポートが追加され、ページングされたメンバーを取得するためのサポートが追加されました。 | [Teams のコンテキストをボット用に取得する](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | `replyToId`Bot に送信されるペイロードのパラメーターは暗号化されなくなりました。この値を使用して、これらのメッセージに deeplinks を構築できます。 メッセージペイロードには、パラメーターに暗号化された値が含まれています。 `legacy.replyToId`.  |
| 11/5/2019 | Web コンテンツページで Teams JavaScript SDK を使用したシングルサインオンは、開発者向けプレビューで表示されます。 | [シングル サインオン](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | 話し言葉のボットとメッセージング拡張機能のドキュメントは、4.6 Bot フレームワーク SDK を反映するように更新されました。 V3 SDK のドキュメントについては、「Resources」セクションを参照してください。 | すべてのボットおよびメッセージング拡張機能のドキュメント。 |
| 10/31/2019 | 新しいドキュメント構造と主要な記事のリファクタリング。 GitHub の問題を作成して、すべての配信不能リンクまたは404を報告してください。 | 彼ら皆！ |
| 9/13/2019 | 要求 bot は、アクションベースのメッセージング拡張機能からインストールされます。 | [メッセージング拡張機能を使用したアクションの開始](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | タブおよびコネクタのプライベートチャネルのサポート。 | [タブのコンテキストを取得する](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | 外部 web サイトから Teams チャネルに外部 web サイトを共有します。 | [Teams への共有](~/share-to-teams.md) |
| 05/25/2019 | タスクモジュールからの bot メッセージで応答します。 | [タスクモジュールからの bot メッセージで応答する](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | グループチャットの bot。 | [グループチャットまたはチャネルで bot と対話する](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | アプリマニフェストのローカライズ。 | [アプリのローカライズ](~/publishing/apps-localization.md) |
| 05/20/2019 | メッセージアクション。 | [メッセージアクション](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Link unfurling (カスタム URL プレビュー)。 | [リンク展開](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Store アプリ用のアプリケーション証明書プログラム。 | [アプリケーション証明書](~/publishing/application-certification.md) |
| 05/06/2019 | アプリテンプレートが使用可能になりました。 | [アプリテンプレート](~/samples/app-templates.md) |
| 04/23/2019 | アクションベースのメッセージング拡張機能が使用できるようになりました。 | [アクションベースのメッセージ拡張機能](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | プライベートチャットへの詳細なリンクを作成することは、開発者向けのプレビューではありません。 | [チャットへの詳細なリンク](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | タブコンテキストで SKU と licenceType の情報を提示します。 | [タブのコンテキスト](~/concepts/tabs/tabs-context.md) |
| 2018 年 11 月 12 日 | グループチャットのタブは、リリースされたバージョンの Teams で利用できるようになり、開発者向けプレビューの外に移動しました。 この作業の一環として、[タブ] セクションは、わかりやすくなるように手直しされています。| [構成可能なタブ](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | ノード JS および .NET/C# のための作業を開始し、Teams でアプリ Studio を使用するように更新され、Azure でのホスティングノードベース Teams アプリに新しいセクションが追加されました。 | [Microsoft teams プラットフォームで C#/.NET および App studio を使用](~/get-started/get-started-dotnet-app-studio.md)して作業を開始し、[ノード JS とアプリ studio を使用して microsoft teams プラットフォームで作業を開始](~/get-started/get-started-nodejs-app-studio.md)し、 [Azure でノードチームアプリをホストする](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | ユーザー間のプライベートチャットへの深いリンクを作成できるようになりました。 | [チャットへの詳細なリンク](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 2018 年 11 月 8 日 | SharePoint Framework 1.7 には、Microsoft Teams タブを SharePoint Framework web パーツとして使用するための新機能が付属しています。 | [SharePoint のタブ](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | "タスクモジュール" 機能がリリースされました。 タスクモジュールを使用すると、ボットとタブの両方から、Teams アプリケーションでモーダルポップアップエクスペリエンスを作成できます。 ポップアップ内では、独自のカスタム HTML/JavaScript コードを実行したり、 `<iframe>` YouTube や Microsoft Stream ビデオなどのベースのウィジェットを表示したり、[アダプティブカード](https://docs.microsoft.com/adaptive-cards/)を表示したりすることができます。 | [タスクモジュールの概要](~/concepts/task-modules/task-modules-overview.md)、[タブのタスクモジュール](~/concepts/task-modules/task-modules-tabs.md)、[ボットのタスクモジュール](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | カードの書式設定情報が更新され、Teams のデスクトップ、iOS、Android クライアントでテストされています。 | [カード](~/concepts/cards/cards.md)、[カードの書式設定](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Microsoft Graph 用の通話とオンライン会議 Api がベータ版にリリースされ、Teams アプリが音声とビデオを使用してさまざまな方法でユーザーと対話できるようになりました。 | [通話とオンライン会議のボット](~/concepts/calls-and-meetings/registering-calling-bot.md)、[リアルタイムのメディア概念](~/concepts/calls-and-meetings/real-time-media-concepts.md)、[呼び出し側](~/concepts/calls-and-meetings/registering-calling-bot.md)のアプリの登録、[デバッグおよびローカルテスト](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)、[アプリケーションホスト型メディア](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)、[着信呼び出し通知の処理](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | タブの構成ページの高さが大幅に向上しました。 | [タブのデザイン](tabs/design/tabs.md) |
| 08/15/2018 | Teams でアダプティブカードがサポートされるようになりました。|[Teams でのアダプティブカードアクション](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | DevTools のクライアントサポートについては、開発者向けのプレビューを対象にドキュメント化されています。| [Microsoft Teams デスクトップクライアント用の DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | メッセージング拡張機能は、複数のコマンドをサポートするようになりました。 この機能は開発者向けプレビューに含まれており、すべてのユーザーにリリースされました。| [このコマンドの機能](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | コネクタでインライン構成がサポートされるようになりました。 また、コネクタのドキュメントも改訂され、わかりやすくなるように展開されています。| [コネクタ](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Bot は、ファイルを送受信できるようになります。| [Bot を使用してファイルを送受信する](~/concepts/bots/bots-files.md)|
| 07/27/2018 | 開発者プレビューは、メッセージング拡張機能で複数のコマンドをサポートするようになりました。 | [メッセージング拡張機能が拡張されました](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | アプリの再証明に関する情報が、公開セクションに追加されました。 |[マニフェストのアクセス許可](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | 開発者向けプレビューでは、[タブの構成] ページに割り当てられている領域が増えています。 | [タブの構成ページの高さが大幅に大きくなっています。](tabs/design/tabs.md#configuration-page-height)|
| 07/12/2018 | ゲストアクセスに関する情報。 | [Microsoft Teams でのゲスト アクセス](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Microsoft Teams テナントアプリカタログのリリース前の情報が追加されました。 | [Microsoft Teams アプリを公開する](~/publishing/apps-publish.md)|
| 05/31/2018 | Teams 開発者プレビュー (リング 3.6) は、ボットとタブをグループチャットに追加する機能を含むように更新されました。 | [開発者プレビューの機能](~/resources/dev-preview/developer-preview-features.md)、[開発者プレビュースキーマ](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Teams でのアダプティブ[カードアクション](task-modules-and-cards/cards/cards-reference.md)では、アダプティブカードがサポートされるようになりました。 |
| 05/29/2018 | [開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md)を使用している場合は、ボットがファイルを送受信できるようになりました。| [Bot を使用](~/concepts/bots/bots-files.md)してファイルを送受信する、 [Microsoft Teams の公開開発者向けプレビューで](~/resources/dev-preview/developer-preview-features.md)提供される機能|
| 04/17/2018 | およびカードのアクションのペイロードに replyToID が追加されました `Invoke` `MessageBack` 。 これは、カードアクションのメッセージを更新する必要がある場合に特に便利です。 | [カードのアクション](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Teams プログラミングインターフェイスとこのドキュメントセットに加えられた変更を追跡するために、このトピックを追加しました。 | [新機能](~/whats-new.md)|
| 04/10/2018 | パス内のテナント ID を一貫して使用するように認証 Url が変更されました。 | [タブの認証フロー](~/concepts/authentication/auth-flow-tab.md)、 [AAD タブの認証](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | コマンドボックスを使用するためのデザインガイドラインが追加されました。 |[コマンドボックス](~/resources/design/framework/command-box.md)|
| 04/02/2018 | ボットを使用してアプリの通知を送信します。 |[通知のみのボット](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | 予防的なメッセージングのためのドキュメントが拡張されました。 |[会話の開始](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | カードのリファクタリングしたドキュメント。 |[カード](~/concepts/cards/cards.md)、[カードの操作](~/concepts/cards/cards-actions.md)、カードの[書式設定](~/concepts/cards/cards-format.md)、[カードリファレンス](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Teams アプリ Studio のドキュメントを追加しました。 |アプリ[studio でコントロールライブラリを使用して](~/get-started/app-studio-component-library.md) [Teams アプリ studio でアプリをすばやく開発](~/get-started/get-started-app-studio.md)する|
| 02/27/2018 | AsTeamsChannelAccounts () メソッドをデモンストレーションするサンプルコードを追加しました。 |[Bot のコンテキストを取得する](~/concepts/bots/bots-context.md)|
| 02/05/2018 | C# の使用を開始するためのトピックを追加しました。 |[Microsoft Teams プラットフォームで C#/.NET を使い始める](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>ご質問、バグ、機能のリクエスト、投稿を提出する

開発者コミュニティは[複数のチャネル](feedback.md)にわたって耳にします。
