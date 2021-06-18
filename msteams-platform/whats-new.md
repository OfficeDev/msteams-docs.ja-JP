---
title: 新機能
description: アプリ内のすべての新しい開発者機能について説明Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: チームの最新情報
ms.openlocfilehash: b2237119c046c85593cf1979b7076b88279187cf
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994344"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>アプリの開発者向けの新機能Microsoft Teams

Microsoft ビルド 2021 Microsoft Teams一般提供 (GA)、および開発者向けプレビューで導入されているプラットフォーム機能について説明します。

## <a name="microsoft-build-2021"></a>Microsoft ビルド 2021

# <a name="features-in-developer-preview"></a>[開発者プレビューの機能](#tab/devpreview)

| **Date** | **機能** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|06/16/2021| チャットに対するリソース固有の同意。 |[リソース固有の同意](graph-api/rsc/resource-specific-consent.md)、[リソースに固有](graph-api/rsc/test-resource-specific-consent.md)の同意のアクセス許可をテストするTeams|
|05/26/2021| アダプティブ カードを使用してタブを作成します。 |[タブを作成する](tabs/how-to/build-adaptive-card-tabs.md)|
|05/25/2021| 更新された[Teams ToolkitとVisual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)[の](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit&ssr=false#overview)Visual Studio。 | [アプリ開発Teams開始する](~/get-started/prerequisites.md) |
|05/25/2021| アプリを管理Teamsするための新しい開発者ポータルがTeamsされました。 | [Teams の開発者ポータル](concepts/build-and-test/teams-developer-portal.md) |
|05/25/2021| カスタム 一緒にモードのシーン機能は、参加者を 1 つの仮想シーンに結合し、事前に決定されたシートにビデオ ストリームを設定します。 | [カスタム一緒にモードのシーン](~/apps-in-teams-meetings/teams-together-mode.md) |
|05/24/2021| ボットは、リソース固有の同意 (RSC) を使用してすべてのチャネル メッセージを受信できます。|[RSC、ボット会話の](~/bots/how-to/conversations/channel-messages-with-rsc.md)概要、[チャネルと](~/bots/how-to/conversations/conversation-basics.md)グループ[](~/bots/how-to/conversations/channel-and-group-conversations.md)の会話、開発者プレビュー マニフェスト スキーマを使用して[すべてのメッセージを受信する](~/resources/schema/manifest-schema-dev-preview.md) |
|05/21/2021| タブは、リンク解除とステージ ビューをリンクします。 |[タブリンクの分岐とステージ ビュー](tabs/tabs-link-unfurling.md) |

> [!NOTE]
> 開発者プレビューで使用できる機能の詳細については、「開発者向けパブリック プレビュー」[を参照Teams。](~/resources/dev-preview/developer-preview-intro.md)

# <a name="features-in-ga"></a>[GA の機能](#tab/GA)

| **Date** | **機能** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|04/29/2021 | アダプティブ カードのユニバーサル アクション。 | [アダプティブ カードのユニバーサル アクション](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|04/29/2021 | アダプティブ カードのユーザー固有のビュー。 | [ユーザー固有のビュー](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/User-Specific-Views.md) |
|04/29/2021 | アダプティブ カードのシーケンシャル ワークフロー。 | [シーケンシャル ワークフロー](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Sequential-Workflows.md) |
|04/29/2021 | 最新のカード。 | [最新のカード](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Up-To-Date-Views.md) |
|04/08/2021| アプリのカスタマイズ。|[デザイン チーム アプリの概要](concepts/design/enable-app-customization.md)[、App studio の概要](concepts/build-and-test/app-studio-overview.md#connectors)、マニフェスト[スキーマ](resources/schema/manifest-schema-dev-preview.md) |
|03/29/2021 | カードの書式を設定Teams。 | [カードの書式を設定Teams](task-modules-and-cards/cards/cards-format.md) |
|02/19/2021|場所の機能が追加されました。 <br/> 場所機能の情報は、デバイス機能の概要、ネイティブ デバイスのアクセス許可、メディア機能の統合、QR またはバーコード スキャナー機能ファイルに追加されます。|[概要](concepts/device-capabilities/device-capabilities-overview.md)、[デバイスのアクセス許可の要求](concepts/device-capabilities/native-device-permissions.md)、[メディア機能の統合](concepts/device-capabilities/mobile-camera-image-permissions.md)[、QR またはバーコード](concepts/device-capabilities/qr-barcode-scanner-capability.md)スキャナー機能の統合、[場所の統合機能](concepts/device-capabilities/location-capability.md) |

---

## <a name="ga-features"></a>GA の機能

Microsoft Teamsすべてのアプリ開発者が利用できるプラットフォーム機能について説明します。

<br>

<details>

<summary><b>2021</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|06/09/2021| 属性付きアダプティブ カードのイメージのステージ `allowExpand` ビュー。 | [アダプティブ カードの画像のステージ ビュー](~/task-modules-and-cards/cards/cards-format.md) |
|05/31/2021| 会話タブ。 | [タブ内のコンテンツに関する会話を開始および続行する](~/tabs/how-to/conversational-tabs.md) |
|05/24/2021| モバイル パターンTeamsを使用して、アプリの設計ガイドラインを更新しました。|[アプリのTeamsする](~/concepts/design/design-teams-app-overview.md)
|05/13/2021| mConnect と Skooler に関する情報を追加しました。|[Moodle ラーニング管理システム](resources/moodle-overview.md)
|05/10/2021| マニフェスト v1.10 がリリースされました。|[マニフェスト スキーマ](resources/schema/manifest-schema.md) |
|05/10/2021| 新しいアプリのカスタマイズ機能。| [組織でアプリをカスタマイズする](concepts/design/enable-app-customization.md) |
|05/07/2021| チャットでの音声通話とビデオ通話のディープ リンク。 |[ディープ リンク](concepts/build-and-test/deep-links.md#deep-linking-to-an-audio-or-audio-video-call) |
|04/30/2021|アプリをストアに発行する方法に関する新Teamsガイダンス。|[アプリを Teams ストア](concepts/deploy-and-publish/appsource/publish.md)に発行Teams[検証ガイドライン](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|04/29/2021 | アダプティブ カードのユニバーサル アクション。 | [アダプティブ カードのユニバーサル アクション](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|04/29/2021 | ユーザー固有のビュー。 | [ユーザー固有のビュー](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/User-Specific-Views.md) |
|04/29/2021 | シーケンシャル ワークフロー。 | [シーケンシャル ワークフロー](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Sequential-Workflows.md) |
|04/29/2021 | 最新のカード。 | [最新のカード](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Up-To-Date-Views.md) |
|04/08/2021| アプリのカスタマイズ機能。|[デザイン チーム アプリの概要](concepts/design/enable-app-customization.md)[、App studio の概要](concepts/build-and-test/app-studio-overview.md#connectors)、マニフェスト[スキーマ](resources/schema/manifest-schema-dev-preview.md) |
|03/18/2021|注意: Bot Framework SDK のバージョン 4.10 以上に更新します。廃止プロセスと廃止プロセスを開始しました `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 。 | [チーム/チャット メンバーのボット API の変更](resources/team-chat-member-api-changes.md) |
|03/05/2021|注意: タブには、エクスペリエンスを囲む余白がなくなりました。 タブ開発者は、アプリを確認して更新する必要があります。 | [タブ余白の削除](resources/removing-tab-margins.md) |
|03/05/2021|既定のインストール スコープとグループ機能。| [既定のインストール スコープとグループ機能](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|個人用アプリのタブを並べ替えます。|[個人用アプリのチャット タブを並べ替える](tabs/how-to/create-tab-pages/content-page.md#reorder-static-personal-tabs)|
|03/04/2021|アダプティブ カードの情報マスキング。| [アダプティブ カードの情報マスキング](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|場所の機能が追加されました。 <br/> 場所機能の情報は、デバイス機能の概要、ネイティブ デバイスのアクセス許可、メディア機能の統合、QR またはバーコード スキャナー機能ファイルに追加されます。|[概要](concepts/device-capabilities/device-capabilities-overview.md)、[デバイスのアクセス許可の要求](concepts/device-capabilities/native-device-permissions.md)、[メディア機能の統合](concepts/device-capabilities/mobile-camera-image-permissions.md)[、QR またはバーコード](concepts/device-capabilities/qr-barcode-scanner-capability.md)スキャナー機能の統合、[場所の統合機能](concepts/device-capabilities/location-capability.md) |
|02/18/2021|QR またはバーコード スキャナー機能を追加しました。 <br/> QR またはバーコード スキャナーの機能情報は、デバイス機能の概要、ネイティブ デバイスのアクセス許可、およびメディア機能ファイルの統合に追加されます。|[概要](concepts/device-capabilities/device-capabilities-overview.md)、[デバイスのアクセス許可の要求](concepts/device-capabilities/native-device-permissions.md)、[メディア機能の統合](concepts/device-capabilities/mobile-camera-image-permissions.md)[、QR またはバーコード スキャナー機能の統合](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|デバイス機能の概要を追加しました。 <br/> マイク機能情報は、ネイティブ デバイスのアクセス許可に追加され、メディア機能ファイルを統合します。|[概要](concepts/device-capabilities/device-capabilities-overview.md)、 [デバイスのアクセス許可の要求](concepts/device-capabilities/native-device-permissions.md)、 [メディア機能の統合](concepts/device-capabilities/mobile-camera-image-permissions.md)|

<br>

</details>

<br>

<details>
  
<summary><b>2020</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|11/30/2020|ID プラットフォームとタブTeams Toolkit Visual Studio Code統合。|[タブ用のシングル サインオンTeams ToolkitとVisual Studio Code認証](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Teamsバージョン 1.8 に更新されたアプリ マニフェスト。|[リファレンス: マニフェスト スキーマのMicrosoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Teamsの設計ガイドラインを参照してください。|[ボットの設計ガイドライン](bots/design/bots.md)|
|09/30/2020|モバイル デバイス上のボットへのファイルの送受信がサポートされています。|[ボットを介してファイルを送受信する](resources/bot-v3/bots-files.md)|
|09/22/2020|開発の開始に関する新Teams。|[アプリの最初のTeamsを作成する](build-your-first-app/build-first-app-overview.md)|
|09/18/2020|会議中のアプリのTeams (リリース プレビュー)。|[会議や会議Teamsアプリ](apps-in-teams-meetings/create-apps-for-teams-meetings.md)[のアプリをTeamsする](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|08/19/2020|Microsoft TeamsメッセージをインポートGraph。|[Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする](graph-api/import-messages/import-external-messages-to-teams.md)
|08/12/2020 |受信 Webhook でのアダプティブ カードのサポートが GA に移動しました。|[受信 Webhook を使用してアダプティブ カードを送信する](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|アプリを使用Teamsを構築するVisual Studio Toolkit。|[アプリとアプリのMicrosoft Teams ToolkitをVisual Studio Code](toolkit/visual-studio-overview.md) |
|08/06/2020|タブ SSO 認証のサポート。|[[SSO の設定] タブMicrosoft Teamsする](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Graphボットとメッセージの管理 (パブリック プレビュー)。|[Microsoft Teams を使用して、プロアクティブ ボットのインストールとプロアクティブ メッセージングをGraph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
|07/22/2020 |モバイル デバイス機能の更新。|[[デバイスのアクセス許可を要求する] Microsoft Teamsタブ](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|TeamsAppSource 申請のアプリ検証ツール。|[Teamsアプリ検証ツール](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|07/15/2020|ユーザーの仮想アシスタントを作成Teams。|[Virtual Assistant Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|ネイティブ読み込みインジケーターのドキュメントを表示する。|[ネイティブ読み込みインジケーターの表示](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|アプリの作成Teamsを開始Visual Studio Code Toolkit。|[アプリとアプリのMicrosoft Teams ToolkitをVisual Studio Code](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Web クライアントおよびデスクトップ クライアント用のタブ GA Teamsシングル サインオン。|[シングル Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| バージョン 1.7 に更新されたマニフェスト スキーマ。| [リファレンス: マニフェスト スキーマのMicrosoft Teams](resources/schema/manifest-schema.md)|
|05/18/2020|アプリケーションとPower Virtual Agents統合Teams。|[チャットボットとPower Virtual Agentsを統合Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|WFM システムを Shifts Connector と統合して、Teams。|[Microsoft TeamsWFM コネクタをシフトする](samples/shifts-wfm-connectors.md)
|03/24/2020 | 会話の 1 つのメンバーを取得するためのサポート、およびページメンバーの取得に関する追加のサポートが追加されました。 | [Teams のコンテキストをボット用に取得する](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
| 12/26/2019 | ボットに送信されるペイロード内のパラメーターは暗号化されなくなったため、この値を使用してこれらのメッセージへのディープリンク `replyToId` を作成できます。 メッセージ ペイロードには、パラメーターに暗号化された値が含まれます `legacy.replyToId` 。  |
| 11/05/2019 | JavaScript SDK を使用したシングル サインオンTeams使用します。 | [シングル サインオン](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | 4.6 Bot Framework SDK を反映するように更新された会話型ボットとメッセージング拡張機能のドキュメント。 v3 SDK のドキュメントは、「リソース」セクションで参照できます。 | すべてのボットとメッセージング拡張機能のドキュメント。 |
| 10/31/2019 | 新しいドキュメント構造と主要な記事のリファクタリング。 問題を作成して、任意のデッド リンクまたは 404 をGitHubしてください。 | 彼ら皆！ |
| 09/13/2019 | 要求ボットは、アクション ベースのメッセージング拡張機能からインストールされます。 | [メッセージング拡張機能を使用してアクションを開始する](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 08/28/2019 | タブとコネクタのプライベート チャネルのサポート。 | [タブのコンテキストを取得する](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | 外部 Web サイトから、外部 Web サイトを別のチャネルTeamsします。 | [共有するTeams](~/share-to-teams.md) |
| 05/25/2019 | タスク モジュールからのボット メッセージで応答します。 | [タスク モジュールからのボット メッセージで応答する](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | グループ チャット内のボット。 | [グループ チャットまたはチャネルでボットを操作する](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | アプリ マニフェストのローカライズ。 | [アプリのローカライズ](~/publishing/apps-localization.md) |
| 05/20/2019 | メッセージアクション。 | [メッセージアクション](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | リンク解除 (カスタム URL プレビュー)。 | [リンク展開](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | ストア アプリのアプリケーション認定プログラム。 | [アプリケーション認定](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 05/06/2019 | アプリ テンプレートが利用可能になります。 | [アプリ テンプレート](~/samples/app-templates.md) |
| 04/23/2019 | アクション ベースのメッセージング拡張機能が利用可能になります。 | [アクション ベースのメッセージ拡張機能](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | プライベート チャットへのディープ リンクの作成。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | タブ コンテキストでの SKU と licenceType 情報の表示。 | [タブ コンテキスト](~/concepts/tabs/tabs-context.md) |

<br>

</details>

<br>

<details>

<summary><b>2018</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
| 2018 年 11 月 12 日 | グループ チャット内のタブは、リリースされたバージョンのグループ チャットでTeams。 この作業の一環として、[タブ] セクションはわかりやすくするために再作業されています。| [構成可能なタブ](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | ノード JS と .NET/C# の開始は、Teams で App Studio を使用するように更新され、Azure での Node ベースの Teams アプリのホスティングに新しいセクションが追加されました。 | [C#/.NET](~/get-started/get-started-dotnet-app-studio.md)と App Studio を使用して Microsoft Teams プラットフォームで始める 、 Node JS と[App Studio](~/get-started/get-started-nodejs-app-studio.md)を使用した Microsoft Teams プラットフォームの使用を開始する[、Azure](~/get-started/get-started-nodejs-in-azure.md)でノード Teams アプリをホストする|
| 11/09/2018 | これで、ユーザー間のプライベート チャットへのディープ リンクを作成できます。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 2018 年 11 月 8 日 | SharePoint Framework 1.7 が出荷され、web パーツとして [Microsoft Teams] タブSharePoint Framework機能が追加されました。 | [[タブ] SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | タスク **モジュール機能** がリリースされました。 タスク モジュールを使用すると、ボットとタブの両方から、Teamsアプリケーションでモーダル ポップアップ エクスペリエンスを作成できます。 ポップアップ内では、独自のカスタム HTML/JavaScript コードを実行したり、YouTube や Microsoft Stream ビデオなどの -based ウィジェットを表示したり、アダプティブ カードを `<iframe>` [表示することができます](/adaptive-cards/)。 | [タスク モジュールの概要](~/concepts/task-modules/task-modules-overview.md)、 [タブ内のタスク モジュール](~/concepts/task-modules/task-modules-tabs.md)、  [ボット内のタスク モジュール](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | カードの書式設定情報は、デスクトップ、iOS、Android クライアントで更新され、テストTeams。 | [カード](~/concepts/cards/cards.md)、 [カードの書式設定](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Microsoft Graph 用の通話とオンライン会議 API がベータ版にリリースされ、Teams アプリは音声とビデオを使用してユーザーと豊富なやり取りを行うことができます。 | [通話とオンライン会議](~/concepts/calls-and-meetings/registering-calling-bot.md)ボット [,](~/concepts/calls-and-meetings/real-time-media-concepts.md)リアルタイムメディアの概念 [,](~/concepts/calls-and-meetings/registering-calling-bot.md)呼び出しボットの登録 [,](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)デバッグとローカルテスト , [アプリケーション](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)ホスト型メディア , 着信通話通知 [の処理](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | タブ構成ページの高さが大幅に向上しました。 | [タブデザイン](tabs/design/tabs.md) |
| 08/15/2018 | アダプティブ カードは、アダプティブ カードでサポートTeams。|[Teams でのアダプティブ カードのアクション](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | DevTools のクライアント サポート。| [デスクトップ クライアントMicrosoft Teams DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | メッセージング拡張機能は複数のコマンドをサポートしています。 | [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | コネクタでインライン構成がサポートされました。 Connectors のドキュメントも、わかりやすくするために改訂および拡張されました。| [コネクタ](~/concepts/connectors/connectors.md)|
| 08/06/2018 | これで、ボットはファイルの送受信を行うことができます。| [ボットを介してファイルを送受信する](~/bots/how-to/bots-filesv4.md)|
| 07/23/2018 | アプリの再認定に関する情報が [発行] セクションに追加されました。 |[マニフェストのアクセス許可](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | タブ構成ページには、より多くの領域が割り当てられている。 | [タブ構成ページが大幅に高い](tabs/design/tabs.md)|
| 07/12/2018 | ゲスト アクセスに関する情報。 | [Microsoft Teams でのゲスト アクセス](/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | テナント アプリ カタログMicrosoft Teams情報が追加されました。 | [アプリをMicrosoft Teamsする](~/publishing/apps-publish.md)|
| 05/29/2018 | アダプティブ カードは、Teams。 | [Teams でのアダプティブ カードのアクション](task-modules-and-cards/cards/cards-reference.md) |
| 04/17/2018 | replyToID がペイロードに追加され、カード `Invoke` アクションが `MessageBack` 実行されます。 これは、カードアクションが送信されたメッセージを更新する必要がある場合に特に便利です。 | [カードアクション](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | このトピックは、プログラミング インターフェイスとこのドキュメント セットTeams変更を追跡するために追加されました。 | [新機能](~/whats-new.md)|
| 04/10/2018 | パスでテナント ID を一貫して使用する認証 URL を変更しました。 | [タブの認証フロー](~/concepts/authentication/auth-flow-tab.md) [、AAD タブ認証](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | コマンド ボックスの使用に関する設計ガイドラインを追加しました。 |[[コマンド] ボックス](~/resources/design/framework/command-box.md)|
| 04/02/2018 | ボットを使用してアプリの通知を送信する。 |[通知のみのボット](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | プロアクティブ メッセージングのドキュメントを拡張しました。 |[会話の開始](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | カードのリファクタリングされたドキュメント。 |[カード](~/concepts/cards/cards.md)、 [カードアクション](~/concepts/cards/cards-actions.md)、 [カードの書式設定](~/concepts/cards/cards-format.md)、 [カード参照](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | App Studio のTeams追加しました。 |App Studio[でアプリTeams開発](~/get-started/get-started-app-studio.md)する 、 App Studio で[コントロール ライブラリを使用する](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | AsTeamsChannelAccounts() メソッドを示すサンプル コードを追加しました。 |[コンテキストをボット用に取得する](~/concepts/bots/bots-context.md)|
| 02/05/2018 | ユーザー設定の使用を開始する方法に関するC#。 |[Microsoft Teams プラットフォームで C#/.NET を使い始める](./get-started/get-started-dotnet-app-studio.md)|

<br>

</details>

## <a name="developer-preview"></a>開発者向けプレビュー

開発者プレビューは、リリースされていないプラットフォーム機能に早期にアクセスできるTeamsプログラムです。  

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|06/16/2021| チャットに対するリソース固有の同意。 |[リソース固有の同意](graph-api/rsc/resource-specific-consent.md)、[リソースに固有](graph-api/rsc/test-resource-specific-consent.md)の同意のアクセス許可をテストするTeams|  
|05/26/2021|アダプティブ カードを使用してタブをビルドする|[タブを作成する](tabs/how-to/build-adaptive-card-tabs.md)|
|05/25/2021| 更新された[Teams ToolkitとVisual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)[の](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit&ssr=false#overview)Visual Studio。 | [アプリ開発Teams開始する](~/get-started/prerequisites.md) |
|05/25/2021| アプリを管理Teamsするための新しい開発者ポータルがTeamsされました。 | [Teams の開発者ポータル](concepts/build-and-test/teams-developer-portal.md) |
|05/25/2021| カスタム 一緒にモードのシーン機能は、参加者を 1 つの仮想シーンに結合し、事前に決定されたシートにビデオ ストリームを設定します。 | [カスタム一緒にモードのシーン](~/apps-in-teams-meetings/teams-together-mode.md) |
|05/24/2021|ボットは、リソース固有の同意 (RSC) を使用してすべてのチャネル メッセージを受信できます。|[RSC、ボット会話の](~/bots/how-to/conversations/channel-messages-with-rsc.md)概要、[チャネルと](~/bots/how-to/conversations/conversation-basics.md)グループ[](~/bots/how-to/conversations/channel-and-group-conversations.md)の会話、開発者プレビュー マニフェスト スキーマを使用して[すべてのメッセージを受信する](~/resources/schema/manifest-schema-dev-preview.md) |
|05/21/2021|タブリンクの分岐とステージ ビュー|[タブリンクの分岐とステージ ビュー](tabs/tabs-link-unfurling.md) |
|03/05/2021| タブのエクスペリエンスを囲む余白がなくなりました。 タブ開発者は、アプリを確認して更新する必要があります。 | [タブ余白の削除](resources/removing-tab-margins.md) |

詳細については、「パブリック開発者[向けプレビュー」を参照Teams。](~/resources/dev-preview/developer-preview-intro.md)

## <a name="teams-app-template-catalog"></a>Teams テンプレート カタログ

新しい機能に加え、すぐに[](samples/app-templates.md)展開したり、ニーズTeams変更したりできる、実稼働可能なアプリ テンプレートも提供しています。 新しく追加されたテンプレートは、星付き ☆で示されます。

## <a name="submit-your-feedback"></a>フィードバックを送信する

開発者にTeams、バグのファイル、機能要求の提出、投稿をお勧めしています。 利用可能なチャネルを通じてフィードバックを [送信できます](feedback.md)。
