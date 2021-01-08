---
title: 新機能
description: Microsoft Teams のすべての新しい開発者向け機能について説明します。
keywords: Teams の新機能
ms.openlocfilehash: da2378446f39ab8398cdc569987d14f5c6095330
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739043"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Microsoft Teams の開発者向けの新機能

>[!TIP]
> Teams アプリ テンプレート カタログで、実稼働可能な   [**テンプレートを確認してください**](samples/app-templates.md)。 カタログはアルファベット順に表示され、最新の追加項目には星の **タグが付**&#9734;。

## <a name="change-log"></a>変更ログ

変更ログには、Microsoft Teams プラットフォームとこのドキュメント セットに対する変更が一覧表示されます。 場合によっては、エントリを使用して、Teams 開発者が関心を持つ新しい機能に注意を引く場合があります。

| **日付** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|11/30/2020|新機能: タブ用の Id プラットフォームと Teams Toolkit Visual Studioコードの統合|[Teams を使用したシングル サインオン認証ToolkitタブVisual Studioコード](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|バージョン 1.8 に更新された Teams アプリ マニフェスト|[リファレンス: Microsoft Teams のマニフェスト スキーマ](resources/schema/manifest-schema.md)|
|11/10/2020|Teams ボット設計ガイドライン|[ボットの設計ガイドライン](bots/design/bots.md)|
|9/30/2020|モバイル デバイス上のボットへのファイルの送受信がサポートされました。|[ボットを介してファイルを送受信する](resources/bot-v3/bots-files.md)|
|09/22/2020|新しい 「Teams の使用を開始する」ガイダンス|[最初の Teams アプリの概要を作成する](build-your-first-app/build-first-app-overview.md)|
|9/18/2020|会議中の Teams アプリのサポート (リリース プレビュー)|[Teams 会議用アプリと Teams 会議](apps-in-teams-meetings/create-apps-for-teams-meetings.md)[でのアプリの作成](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|8/19/2020|Microsoft Graph を使用して Teams メッセージをインポートする|[Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする](graph-api/import-messages/import-external-messages-to-teams.md)
| 08/12/2020 |受信 Webhook でのアダプティブ カードのサポートは GA に移動されました。|[受信 Webhook を使用してアダプティブ カードを送信する](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|この機能を使用して Teams アプリの構築をVisual Studio Toolkit。|[Microsoft Teams Toolkit および Visual Studio コードを使用してアプリをVisual Studioする](toolkit/visual-studio-overview.md) |
|08/06/2020|タブ SSO 認証のサポート|[SSO Microsoft Teams タブを開発する](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | プロアクティブボットとメッセージをグラフ化する (パブリック プレビュー)|[Microsoft Graph を使用して Teams でプロアクティブ ボットのインストールとプロアクティブ メッセージングを有効にする](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
| 07/22/2020 |モバイル デバイス機能の更新。|[Microsoft Teams タブのデバイスのアクセス許可を要求する](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|AppSource 申請用の Teams アプリ検証ツール。|[Teams アプリ検証ツール](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)
|07/15/2020|Teams の仮想アシスタントを作成する|[Microsoft Teams の仮想アシスタント](samples/virtual-assistant.md)|
|07/14/2020|ネイティブ読み込みインジケーター ドキュメントの表示|[ネイティブ読み込みインジケーターの表示](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Visual Studio Code Toolkit を使用して Teams アプリのToolkit。|[Microsoft Teams Toolkit および Visual Studio コードを使用してアプリをVisual Studioする](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Teams Web およびデスクトップ クライアント用のタブ GA のシングル サインオン|[単一Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| バージョン 1.7 に更新されたマニフェスト スキーマ| [リファレンス: Microsoft Teams のマニフェスト スキーマ](resources/schema/manifest-schema.md)|
| 05/20/2020 | Microsoft Graph API を使用したリソース固有の同意のアクセス許可は、開発者プレビューで提供されています。 |[リソース固有の同意 (RSC) — Developer Preview](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|Power Virtual Agents と Teams の統合|[Power Virtual Agents のチャットボットを Microsoft Teams と統合する](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|WFM システムを Shifts Connector for Teams と統合する|[Microsoft Teams が WFM コネクタをシフトする](samples/shifts-wfm-connectors.md)
| 03/24/2020 | 会話の 1 人のメンバーを取得するためのサポートと、ページ化されたメンバーの取得に関する追加のサポートが追加されました。 | [Teams のコンテキストをボット用に取得する](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | ボットに送信されるペイロードのパラメーターは暗号化されなくなったため、この値を使用してこれらのメッセージへの `replyToId` ディープリンクを作成できます。 メッセージ ペイロードには、パラメーター内の暗号化された値が含まれます。 `legacy.replyToId`.  |
| 11/5/2019 | Web コンテンツ ページで Teams JavaScript SDK を使用したシングル サインオンは、開発者プレビューに含まれています。 | [シングル サインオン](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | 会話ボットとメッセージング拡張機能のドキュメントが更新され、4.6 Bot Framework SDK が反映されました。 v3 SDK のドキュメントについては、「リソース」セクションを参照してください。 | すべてのボットとメッセージングの拡張機能のドキュメント。 |
| 10/31/2019 | 新しいドキュメント構造と主要な記事のリファクタリング。 GitHub の問題を作成して、デッド リンクまたは 404 を報告してください。 | 彼ら皆！ |
| 9/13/2019 | 要求ボットは、アクション ベースのメッセージング拡張機能からインストールされます。 | [メッセージング拡張機能を使用してアクションを開始する](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | タブとコネクタでのプライベート チャネルのサポート。 | [タブのコンテキストを取得する](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | 外部 Web サイトから Teams チャネルに外部 Web サイトを共有します。 | [Teams に共有する](~/share-to-teams.md) |
| 05/25/2019 | タスク モジュールからのボット メッセージで応答します。 | [タスク モジュールからのボット メッセージで応答する](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | グループ チャットのボット。 | [グループ チャットまたはチャネルでボットを操作する](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | アプリ マニフェストのローカライズ。 | [アプリのローカライズ](~/publishing/apps-localization.md) |
| 05/20/2019 | メッセージアクション。 | [メッセージアクション](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | リンクの分岐 (カスタム URL プレビュー)。 | [リンク展開](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | ストア アプリのアプリケーション認定プログラム。 | [アプリケーション認定](~/publishing/application-certification.md) |
| 05/06/2019 | アプリ テンプレートが使用可能になります。 | [アプリ テンプレート](~/samples/app-templates.md) |
| 04/23/2019 | アクションベースのメッセージング拡張機能が使用可能になります。 | [アクションベースのメッセージ拡張](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | プライベート チャットへのディープ リンクの作成は、開発者プレビューから外れ、利用できます。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | タブ コンテキストで SKU と licenceType の情報を表示します。 | [タブ コンテキスト](~/concepts/tabs/tabs-context.md) |
| 2018 年 11 月 12 日 | グループ チャットのタブは、リリースされたバージョンの Teams で利用可能にされ、開発者プレビューから移動されました。 この作業の一環として、タブ セクションはわかりやすくするために作り替えされています。| [構成可能なタブ](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | Node JS と .NET/C# の使用の開始は、Teams で App Studio を使用するように更新され、Azure でのノード ベースの Teams アプリのホストに関する新しいセクションが追加されました。 | [C#/.NET](~/get-started/get-started-dotnet-app-studio.md)と App Studio を使用した Microsoft Teams プラットフォームの使用を開始する[、Node JS](~/get-started/get-started-nodejs-app-studio.md)と App Studio を使用した Microsoft Teams プラットフォームの使用を開始する[、Azure](~/get-started/get-started-nodejs-in-azure.md)でノード Teams アプリをホストする|
| 11/09/2018 | これで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 2018 年 11 月 8 日 | SharePoint Framework 1.7 が出荷され、Microsoft Teams タブを SharePoint Framework Web パーツとして使用する新機能が追加されました。 | [SharePoint のタブ](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | "タスク モジュール" 機能がリリースされました。 タスク モジュールを使用すると、ボットとタブの両方から Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成できます。 ポップアップ内では、独自のカスタム HTML/JavaScript コードを実行したり、YouTube や Microsoft Stream ビデオなどの -based ウィジェットを表示したり、アダプティブ カードを `<iframe>` [表示することができます](https://docs.microsoft.com/adaptive-cards/)。 | [タスク モジュールの概要](~/concepts/task-modules/task-modules-overview.md), [タブ内のタスク モジュール](~/concepts/task-modules/task-modules-tabs.md), ボット  [のタスク モジュール](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | カードの書式設定情報が更新され、Teams のデスクトップ、iOS、Android クライアントでテストされました。 | [カード](~/concepts/cards/cards.md)、 [カードの書式設定](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Microsoft Graph の通話とオンライン会議 API はベータ版にリリースされ、Teams アプリは音声とビデオを使用してユーザーと豊富な方法で対話できます。 | [通話とオンライン会議](~/concepts/calls-and-meetings/registering-calling-bot.md)ボット , [リアルタイム](~/concepts/calls-and-meetings/real-time-media-concepts.md)メディアの概念, 通話 [ボット](~/concepts/calls-and-meetings/registering-calling-bot.md)の登録, [デバッグ](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)とローカル テスト, アプリケーションホスト型 [メディア](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md), 着信呼び出し通知 [の処理](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | タブ構成ページの方が大幅に高くなっています。 | [タブデザイン](tabs/design/tabs.md) |
| 08/15/2018 | Teams でアダプティブ カードがサポートされました。|[Teams でのアダプティブ カードのアクション](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | DevTools のクライアント サポートについては、次のDeveloper Preview。| [Microsoft Teams デスクトップ クライアント用 DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | メッセージング拡張機能では、複数のコマンドがサポートされます。 この機能は現在Developer Preview、すべてのユーザーにリリースされました。| [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | インライン構成がコネクタでサポートされました。 また、コネクタのドキュメントは、わかりやすくするために改訂され、拡張されています。| [コネクタ](~/concepts/connectors/connectors.md)|
| 08/06/2018 | ボットはファイルを送受信できます。| [ボットを介してファイルを送受信する](~/concepts/bots/bots-files.md)|
| 07/27/2018 | 開発者プレビューでは、メッセージング拡張機能で複数のコマンドがサポートされます。 | [メッセージング拡張機能が拡張されました](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | アプリの再認定に関する情報が [発行] セクションに追加されました。 |[マニフェストのアクセス許可](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | 開発者プレビューでは、タブ構成ページにより多くの領域が割り当てされています。 | [タブ構成ページの高さ](tabs/design/tabs.md)|
| 07/12/2018 | ゲスト アクセスに関する情報。 | [Microsoft Teams でのゲスト アクセス](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Microsoft Teams テナント アプリ カタログのプレリリース情報が追加されました。 | [Microsoft Teams アプリを公開する](~/publishing/apps-publish.md)|
| 05/31/2018 | Teams 開発者プレビュー (リング 3.6) が更新され、ボットとタブをグループ チャットに追加する機能が追加されました。 | [開発者プレビュー、開発者プレビュー](~/resources/dev-preview/developer-preview-features.md)[スキーマの機能](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | アダプティブ カードは、Teams のアダプティブ カード アクションで Teams [でサポートされます](task-modules-and-cards/cards/cards-reference.md)。 |
| 05/29/2018 | 開発者プレビューを使用 [している場合、](~/resources/dev-preview/developer-preview-intro.md)ボットはファイルを送受信できます。| [ボットを介してファイルを送受信](~/concepts/bots/bots-files.md)する[、Microsoft Teams](~/resources/dev-preview/developer-preview-features.md)のパブリック Developer Preview機能|
| 04/17/2018 | replyToID が、ペイロードに追加され、カード `Invoke` アクションが `MessageBack` 実行されます。 これは、カードアクションのメッセージを更新する必要がある場合に特に便利です。 | [カードアクション](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Teams プログラミング インターフェイスとこのドキュメント セットの変更を追跡するために、このトピックを追加しました。 | [新機能](~/whats-new.md)|
| 04/10/2018 | パス内のテナント ID を一貫して使用する認証 URL を変更しました。 | [タブ、AAD タブ](~/concepts/authentication/auth-flow-tab.md)[認証の認証フロー](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | コマンド ボックスを使用する設計ガイドラインを追加しました。 |[コマンド ボックス](~/resources/design/framework/command-box.md)|
| 04/02/2018 | ボットを使用してアプリの通知を送信する。 |[通知のみのボット](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | プロアクティブ メッセージングに関するドキュメントを拡張しました。 |[会話の開始](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | カードのリファクタリングされたドキュメント。 |[カード](~/concepts/cards/cards.md), [カードアクション](~/concepts/cards/cards-actions.md), [カードの書式設定](~/concepts/cards/cards-format.md), [カード リファレンス](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Teams App Studio のドキュメントを追加しました。 |[Teams App Studio でアプリをすばやく開発し、App](~/get-started/get-started-app-studio.md) [Studio のコントロール ライブラリを使用する](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | AsTeamsChannelAccounts() メソッドを示すサンプル コードを追加しました。 |[ボットのコンテキストを取得する](~/concepts/bots/bots-context.md)|
| 02/05/2018 | C# の使用を開始する方法に関するトピックを追加しました。 |[Microsoft Teams プラットフォームで C#/.NET を使い始める](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>質問、バグ、機能の要求、投稿を送信する

複数のチャネルで開発者コミュニティに [耳を傾ける](feedback.md)。
