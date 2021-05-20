---
title: 新機能
description: Microsoft Teamsでの新しい開発者向け機能をすべて説明します。
ms.topic: reference
localization_priority: Normal
keywords: チーム最新情報
ms.openlocfilehash: aa78d187b3fa771c7e7f0fadfe1aa8f571203cb7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566517"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Microsoft Teamsの開発者向けの新機能

一般Microsoft Teams利用可能なプラットフォーム機能 (GA) と開発者プレビューを確認します。

## <a name="ga-features"></a>GA の機能

Microsoft Teamsすべてのアプリ開発者が利用できるプラットフォーム機能です。

<br>

<details>

<summary><b>2021</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|05/13/2021|mConnect とスクーラーに関する情報を追加しました。|[Moodle学習管理システム](resources/moodle-overview.md)
|05/10/2021| マニフェスト v1.10 がリリースされます。|[マニフェスト スキーマ](resources/schema/manifest-schema.md) |
|05/10/2021| アプリのカスタマイズ機能。| [Microsoft Teams アプリの設計](~/concepts/design/design-teams-app-overview.md#app-customization) |
|05/07/2021| チャットでの音声通話とビデオ通話のディープリンク。 |[ディープ リンク](concepts/build-and-test/deep-links.md#deep-linking-to-an-audio-or-audio-video-call) |
|04/30/2021|Teams ストアにアプリを公開する方法に関する新しいガイダンス。|[Teams ストア へのアプリの公開](concepts/deploy-and-publish/appsource/publish.md) [、Teamsストア検証ガイドライン](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|04/29/2021 | 新機能: アダプティブ カードのユニバーサル アクション。 | [アダプティブ カードのユニバーサル アクション](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|03/18/2021|注意: Bot Framework SDK のバージョン 4.10 以降に更新します `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 。 | [チーム/チャット メンバーのボット API の変更](resources/team-chat-member-api-changes.md) |
|03/05/2021|注意: タブには、そのエクスペリエンスを囲む余白がなくなります。 タブ開発者は、アプリを確認して更新する必要があります。 | [タブ余白の削除](resources/removing-tab-margins.md) |
|03/05/2021|既定のインストール スコープとグループの機能は、開発者プレビューで行われます。| [既定のインストール スコープとグループの機能](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|個人用アプリのタブを並べ替えます。|[個人用アプリでチャット タブを並べ替え](tabs/how-to/create-tab-pages/content-page.md#reorder-static-personal-tabs)|
|03/04/2021|アダプティブカードでの情報マスキング。| [アダプティブカードでの情報マスキング](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|位置情報機能を追加しました。 <br/> 位置情報の情報は、デバイス機能の概要、ネイティブデバイスのアクセス許可、メディア機能の統合、QR またはバーコード スキャナー機能ファイルに追加されます。|[概要](concepts/device-capabilities/device-capabilities-overview.md), [デバイスのアクセス許可を要求](concepts/device-capabilities/native-device-permissions.md)する , [メディア機能の統合](concepts/device-capabilities/mobile-camera-image-permissions.md), [QR またはバーコード スキャナ機能の統合](concepts/device-capabilities/qr-barcode-scanner-capability.md), [位置情報機能の統合](concepts/device-capabilities/location-capability.md) |
|02/18/2021|QRまたはバーコードスキャナ機能を追加しました。 <br/> QR またはバーコード スキャナーの機能情報は、デバイス機能の概要、ネイティブデバイスのアクセス許可、および統合メディア機能ファイルに追加されます。|[概要](concepts/device-capabilities/device-capabilities-overview.md), [デバイスのアクセス許可を要求](concepts/device-capabilities/native-device-permissions.md)する , [メディア機能の統合](concepts/device-capabilities/mobile-camera-image-permissions.md), [QR またはバーコード スキャナ機能の統合](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|デバイス機能の概要を追加しました。 <br/> マイクロフォン機能情報は、ネイティブデバイスのアクセス許可に追加され、メディアケーパビリティファイルを統合します。|[概要](concepts/device-capabilities/device-capabilities-overview.md), [デバイスのアクセス許可を要求](concepts/device-capabilities/native-device-permissions.md)する , [メディア機能の統合](concepts/device-capabilities/mobile-camera-image-permissions.md)|

<br>

</details>

<br>

<details>
  
<summary><b>2020</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|11/30/2020|タブのTeams ToolkitとVisual Studio Codeとのアイデンティティ プラットフォームの統合。|[Teams ToolkitとタブのVisual Studio Codeを使用したシングル サインオン認証](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Teamsアプリ マニフェストがバージョン 1.8 に更新されました。|[リファレンス: Microsoft Teamsのマニフェスト スキーマ](resources/schema/manifest-schema.md)|
|11/10/2020|Teamsボット設計ガイドライン。|[ボットの設計ガイドライン](bots/design/bots.md)|
|09/30/2020|モバイル デバイス上のボットへのファイルの送受信がサポートされるようになりました。|[ボットを介してファイルを送受信する](resources/bot-v3/bots-files.md)|
|09/22/2020|Teams開発の開始に関する新しい情報。|[初めてのTeamsアプリの概要を構築する](build-your-first-app/build-first-app-overview.md)|
|09/18/2020|会議中のTeamsアプリのサポート (リリース プレビュー)。|Teams[会議での会議とアプリのTeams用](apps-in-teams-meetings/create-apps-for-teams-meetings.md)[のアプリを作成する](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|08/19/2020|マイクロソフト Graph でTeams メッセージをインポートします。|[Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする](graph-api/import-messages/import-external-messages-to-teams.md)
| 08/12/2020 |受信 Webhook でのアダプティブ カードのサポートが GA に移動しました。|[受信 Webhook を使用してアダプティブ カードを送信する](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|Visual Studio Toolkitを使用してTeamsアプリの構築を開始します。|[Microsoft Teams ToolkitとVisual Studio Codeを使用してアプリを構築する](toolkit/visual-studio-overview.md) |
|08/06/2020|タブ SSO 認証のサポート。|[SSO Microsoft Teams タブの開発](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | プロアクティブなボットとメッセージをGraphします (パブリック プレビュー)。|[Microsoft GraphでのTeamsで、プロアクティブなボットのインストールとプロアクティブなメッセージングを有効にします。](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
| 07/22/2020 |モバイル デバイス機能の更新。|[[Microsoft Teams] タブのデバイスのアクセス許可を要求する](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|Teamsアプリソース提出のためのアプリ検証ツール。|[Teamsアプリ検証ツール](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|07/15/2020|Teamsの仮想アシスタントを作成します。|[Microsoft Teamsのバーチャルアシスタント](samples/virtual-assistant.md)|
|07/14/2020|ネイティブロードインジケータのドキュメントを表示します。|[ネイティブローディングインジケータの表示](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Visual Studio Code Toolkitを使用してTeamsアプリの構築を開始します。|[Microsoft Teams ToolkitとVisual Studio Codeを使用してアプリを構築する](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Teams Web クライアントおよびデスクトップ クライアントのタブ GA のシングル サインオン。|[シングルSign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| マニフェスト スキーマがバージョン 1.7 に更新されました。| [リファレンス: Microsoft Teamsのマニフェスト スキーマ](resources/schema/manifest-schema.md)|
|05/18/2020|Power Virtual AgentsをTeamsと統合します。|[Power Virtual AgentsチャットボットをMicrosoft Teamsと統合する](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|TEAMS用のシフトコネクタとWFMシステムを統合します。|[Microsoft TeamsWFM コネクタをシフトする](samples/shifts-wfm-connectors.md)
| 03/24/2020 | 会話の 1 つのメンバーを取得するためのサポートと、ページ化されたメンバーの取得に対する追加のサポートが追加されました。 | [Teams のコンテキストをボット用に取得する](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
| 12/26/2019 | `replyToId`ボットに送信されるペイロードのパラメーターは暗号化されなくなり、この値を使用してこれらのメッセージへのディープリンクを構築できます。 メッセージ ペイロードには、 パラメータに暗号化された値が含まれます `legacy.replyToId` 。  |
| 11/05/2019 | Teams JavaScript SDK を使用したシングル サインオン。 | [シングル サインオン](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | 会話型ボットとメッセージング拡張機能のドキュメントは、4.6 Bot Framework SDK を反映するように更新されました。 v3 SDK のドキュメントは、「リソース」セクションで参照できます。 | すべてのボットとメッセージングの拡張機能のドキュメント。 |
| 10/31/2019 | 新しいドキュメント構造、および主要な記事リファクタリング。 GitHub問題を作成して、デッドリンクまたは404のを報告してください。 | 彼ら皆！ |
| 09/13/2019 | 要求ボットは、アクションベースのメッセージング拡張機能からインストールされます。 | [メッセージング拡張機能を使用してアクションを開始する](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 08/28/2019 | タブとコネクタでのプライベート チャネルのサポート。 | [タブのコンテキストを取得する](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | 外部 Web サイトからTeamsチャネルに外部 Web サイトを共有します。 | [Teamsに共有](~/share-to-teams.md) |
| 05/25/2019 | タスク モジュールからのボット メッセージで応答します。 | [タスク モジュールからのボット メッセージで応答する](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | グループチャットのボット。 | [グループチャットまたはチャンネルでボットとの対話](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | アプリ マニフェストのローカライズ。 | [アプリのローカライズ](~/publishing/apps-localization.md) |
| 05/20/2019 | メッセージアクション。 | [メッセージアクション](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | リンクの展開 (カスタム URL プレビュー) | [リンク展開](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | ストア アプリのアプリケーション認定プログラム。 | [アプリケーション認定](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 05/06/2019 | アプリ テンプレートが利用可能になりました。 | [アプリ テンプレート](~/samples/app-templates.md) |
| 04/23/2019 | アクションベースのメッセージング拡張機能を使用できるようになりました。 | [アクション ベースのメッセージ拡張](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | プライベートチャットへのディープリンクを作成することは、開発者のプレビューから外れ、利用可能です。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | SKU とライセンスのサーフェーシングタブコンテキストの情報を入力します。 | [タブコンテキスト](~/concepts/tabs/tabs-context.md) |

<br>

</details>

<br>

<details>

<summary><b>2018</b></summary>

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
| 2018 年 11 月 12 日 | グループ チャットのタブは、リリース版のTeamsで使用できるようになっており、開発者プレビューから移動されました。 この作業の一環として、タブセクションはわかりやすくするために修正されました。| [構成可能なタブ](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | ノード JS と .NET/C# の開始は、Teamsのアプリ スタジオを使用するように更新され、Azure でのノードベースのTeamsアプリのホスティングに関する新しいセクションが追加されました。 | [C#/.NET とアプリ スタジオを使用してMicrosoft Teams プラットフォームを開始](~/get-started/get-started-dotnet-app-studio.md)し、[ノード JS とアプリ スタジオを使用して Microsoft Teams プラットフォームを開始し](~/get-started/get-started-nodejs-app-studio.md)[、Azure でノード Teams アプリをホストする](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | ユーザー間のプライベート チャットへのディープ リンクを作成できるようになりました。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 2018 年 11 月 8 日 | SharePoint Framework 1.7 は、SharePoint Framework Web パーツとしてタブを使用する新しい機能Microsoft Teams出荷されています。 | [SharePoint内のタブ](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | **タスク モジュール** 機能がリリースされました。 タスク モジュールを使用すると、ボットとタブの両方から、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成できます。 ポップアップの内部では、独自の HTML/JavaScript コードを実行したり `<iframe>` 、YouTube や Microsoft Stream のビデオなどのウィジェットを表示したり、 [アダプティブ カード](/adaptive-cards/)を表示したりできます。 | [タスク モジュールの概要](~/concepts/task-modules/task-modules-overview.md)、 [タブのタスク モジュール](~/concepts/task-modules/task-modules-tabs.md)、  [ボットのタスク モジュール](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | カードの書式設定情報は、デスクトップ、iOS、およびAndroidクライアントでTeamsに更新され、テストされています。 | [カード](~/concepts/cards/cards.md)、 [カードの書式設定](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Microsoft Graphの通話とオンライン会議 API はベータ版にリリースされ、Teamsアプリは音声とビデオを使用して豊富な方法でユーザーと対話できるようになりました。 | [通話とオンライン会議ボット](~/concepts/calls-and-meetings/registering-calling-bot.md), [リアルタイムメディア概念](~/concepts/calls-and-meetings/real-time-media-concepts.md), [呼び出しボットの登録](~/concepts/calls-and-meetings/registering-calling-bot.md), [デバッグとローカルテスト](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md), [アプリケーションホストメディア](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md), [着信コール通知の処理](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | タブ構成ページの方が大幅に大きくなりました。 | [タブデザイン](tabs/design/tabs.md) |
| 08/15/2018 | アダプティブ カードは、Teamsでサポートされるようになりました。|[Teams でのアダプティブ カードのアクション](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | クライアントによる開発ツールのサポート。| [Microsoft Teams デスクトップ クライアント用の DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | メッセージング拡張機能で複数のコマンドがサポートされるようになりました。 この機能は開発者プレビューに含まれ、すべてのユーザーにリリースされました。| [コンスタブスエクステンション.コマンド](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | インライン構成がコネクタでサポートされるようになりました。 コネクタのドキュメントも、わかりやすくするために改訂および拡張されています。| [コネクタ](~/concepts/connectors/connectors.md)|
| 08/06/2018 | ボットはファイルの送受信ができるようになりました。| [ボットを介してファイルを送受信する](~/bots/how-to/bots-filesv4.md)|
| 07/23/2018 | アプリの再認定に関する情報が[公開]セクションに追加されました。 |[マニフェストのアクセス許可](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | タブ構成ページに割り当てられている領域が増えました。 | [タブ構成ページは大幅に高くなっています](tabs/design/tabs.md)|
| 07/12/2018 | ゲスト アクセスに関する情報。 | [Microsoft Teams でのゲスト アクセス](/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Microsoft Teamsテナント アプリ カタログの情報が追加されました。 | [Microsoft Teams アプリを公開する](~/publishing/apps-publish.md)|
| 05/29/2018 | アダプティブ カードは、Teamsでサポートされています。 | [Teams でのアダプティブ カードのアクション](task-modules-and-cards/cards/cards-reference.md) |
| 04/17/2018 | 応答ToIDは、 `Invoke` およびカードアクションのペイロードに追加されました `MessageBack` 。 これは、カードアクションの送信元のメッセージを更新する必要がある場合に特に便利です。 | [カードアクション](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Teams プログラミング インターフェイスおよびこのドキュメント セットの変更を追跡するために、このトピックを追加しました。 | [新機能](~/whats-new.md)|
| 04/10/2018 | パス内のテナント ID を一貫して使用するように認証 URL を変更しました。 | タブ[、AAD](~/concepts/authentication/auth-tab-AAD.md) [タブ認証の認証フロー](~/concepts/authentication/auth-flow-tab.md)|
| 04/06/2018 | コマンド ボックスの使用に関する設計ガイドラインを追加しました。 |[コマンドボックス](~/resources/design/framework/command-box.md)|
| 04/02/2018 | ボットを使用してアプリの通知を送信する。 |[通知のみのボット](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | プロアクティブなメッセージングのドキュメントが拡張されました。 |[会話の開始](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | カードのリファクタリングド。 |[カード](~/concepts/cards/cards.md), [カードアクション](~/concepts/cards/cards-actions.md), [カードフォーマット](~/concepts/cards/cards-format.md), [カードリファレンス](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | アプリケーションスタジオTeamsのドキュメントを追加しました。 |[アプリスタジオでTeamsアプリを開発](~/get-started/get-started-app-studio.md)する 、[アプリスタジオのコントロールライブラリを使用して](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | メソッドをデモンストレーションするサンプル コードを追加しました。 |[コンテキストをボット用に取得する](~/concepts/bots/bots-context.md)|
| 02/05/2018 | C# の使用を開始するためのトピックを追加しました。 |[Microsoft Teams プラットフォームで C#/.NET を使い始める](./get-started/get-started-dotnet-app-studio.md)|

<br>

</details>

## <a name="developer-preview"></a>開発者向けプレビュー

開発者向けプレビューは、未リリースのTeamsプラットフォーム機能に早期アクセスできるパブリックプログラムです。  

| **Date** | **注** | **変更されたトピック** |
| -------- | --------- | ------------------ |
|03/05/2021| タブには、そのエクスペリエンスを囲む余白がなくなります。 タブ開発者は、アプリを確認して更新する必要があります。 | [タブ余白の削除](resources/removing-tab-margins.md) |

詳細については、「 [Teams のパブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)」を参照してください。

## <a name="teams-app-template-catalog"></a>アプリ テンプレート カタログTeams

新機能に加えて、すぐにデプロイしたり、ニーズに合わせて変更したりできる[、実稼働環境のTeamsアプリ テンプレート](samples/app-templates.md)も提供します。 新しく追加されたテンプレートは、星の☆で示されています。

## <a name="submit-your-feedback"></a>フィードバックを送信する

Teams開発者は、質問、バグの報告、機能リクエストの送信、投稿を行うことをお勧めします。 [利用可能なチャネル](feedback.md)を通じてフィードバックを送信できます。
