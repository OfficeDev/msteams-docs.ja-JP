---
title: 新機能
description: Microsoft Teams の最新情報やすべての開発者向け最新機能について説明します
ms.topic: reference
ms.localizationpriority: high
keywords: Teams の最新情報と最新の更新プログラムまたは開発者プレビューと機能
ms.openlocfilehash: 0ce0de2efd6c38e610226db48a6a463942a7ccc6
ms.sourcegitcommit: 1e77573e47fad51a19545949fdac1241b13052e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656167"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Microsoft Teams の開発者向けの新機能

一般提供 (GA) および開発者プレビュー版の Microsoft Teams プラットフォーム機能をご紹介します。 RSS フィード[![ダウンロード フィード](~/assets/images/RSSfeeds.png)](https://aka.ms/TeamsPlatformUpdates)に登録することで、Teams プラットフォームの最新情報を取得できるようになりました。 詳細については、「[RSS フィードの構成](#get-latest-updates)」を参照してください。

## <a name="microsoft-build-2022-image-typeicon-sourceassetsimagesbullhornpng-borderfalse"></a>Microsoft Build 2022 :::image type="icon" source="assets/images/bullhorn.png" border="false":::

| 日付 | 機能 | ここから見つける |
| --- | --- | --- |
|05/24/2022| Outlook と Office が有効なアプリを Teams ストアに送信する | Microsoft 365 間でアプリを拡張する [概要](m365-apps/overview.md) |
|05/24/2022| TeamsJS バージョン 2.0.0 のアプリ ガイダンスと新機能| ツールと SDK > [Teams JavaScript クライアント SDK](tabs/how-to/using-teams-client-sdk.md)  |
| 05/24/2022 | Visual Studio Code 用 Teams Toolkit バージョン 4.0.0 の一般提供開始 | ［ツールと SDK］ > ［Visual Studio Code 用 Teams Toolkit］ <br> • [Teams ツールキットの概要](toolkit/teams-toolkit-fundamentals.md) <br> • [Build コマンド ボットと JavaScript](toolkit/add-capability.md) <br> • [JavaScript を使用した通知ボットのビルド](toolkit/add-capability.md) <br> • [Teams アプリ マニフェストのプレビューとカスタマイズ](toolkit/TeamsFx-preview-and-customize-app-manifest.md) <br> • [既存の API に接続します](toolkit/add-API-connection.md) <br> • [Teams アプリに機能を追加する](toolkit/add-capability.md) <br> • [シングル サインオン エクスペリエンスを追加する](toolkit/add-single-sign-on.md) <br> • [Teams アプリにクラウド リソースを追加する](toolkit/add-resource.md) |
| 05/24/2022 | GCC と GCCH のボットとメッセージ拡張機能 | • [アプリの計画] > [[概要]](concepts/app-fundamentals-overview.md#government-community-cloud) </br> • ボットの作成> [概要](bots/what-are-bots.md) </br> • メッセージ拡張機能の作成> [概要](messaging-extensions/what-are-messaging-extensions.md) |

<!--
## Latest updates ![bullhorn icon](~/assets/images/bullhorn.png)

| Date | Update | Find here |
| --- | --- | --- |
|05/24/2022| Submit your Outlook- and Office-enabled apps to the Teams store | Extend your app across Microsoft 365 > [Overview](m365-apps/overview.md) |
|05/24/2022| App guidance and what's new in TeamsJS version 2.0.0| Tools and SDKs > [Teams JavaScript client SDK](tabs/how-to/using-teams-client-sdk.md)  |
|05/19/2022|Bots and Message extensions in GCC and GCCH| • Plan your app > [Overview](concepts/app-fundamentals-overview.md#government-community-cloud) </br> • Build bots > [Overview](bots/what-are-bots.md) </br> • Build message extensions > [Overview](messaging-extensions/what-are-messaging-extensions.md) |
|04/28/2022| Common reasons for app validation failure | Distribute your app > Publish to the Teams store > [Common reasons for app validation failure](concepts/deploy-and-publish/appsource/common-reasons-for-app-validation-failure.md)|
|04/20/2022 |  Set up CI/CD pipelines | Tools and SDKs > Teams Toolkit for Visual Studio Code > [Set up CI/CD pipelines](toolkit/use-CICD-template.md)|
|04/19/2022 | Upload your app in Microsoft Teams | Distribute your app > [Upload your app](concepts/deploy-and-publish/apps-upload.md)|
|04/06/2022| Share to Teams from personal app or tab (developer preview) | Integrate with Teams > Share to Teams > [Share to Teams from personal app or tab](concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md) |
|04/01/2022| Introduced step-by-step guide to create Teams conversational bot| Build bots > Bot conversations > Channel and group conversations > [Step-by-step guide to create Teams conversational bot](sbs-teams-conversation-bot.yml) |
|03/30/2022| Updated the Get started module with Blazor app using tabs and bots|  Get started > [Build your first app using Blazor](sbs-gs-blazorupdate.yml)|
|03/30/2022|Device permissions for the browser | Integrate device capabilities > [Device permissions for the browser](concepts/device-capabilities/browser-device-permissions.md) |
|03/29/2022 | Integrate People Picker | Integrate with Teams > [Integrate People Picker](concepts/device-capabilities/people-picker-capability.md)|
|03/23/2022| Introduced step-by-step guide to unfurl links in Teams using bot | Build message extensions > Add link unfurling > [Unfurl links in Teams using bot](sbs-botbuilder-linkunfurling.yml)|
|03/22/2022| Added information on debug process| • Tools and SDKs> Teams Toolkit for Visual Studio Code > [Debug your Teams app locally](toolkit/debug-local.md) </br> • Tools and SDKs> Teams Toolkit for Visual Studio Code > [Debug background process](toolkit/debug-background-process.md)|
|03/14/2022| Introduced step-by-step guide to build and test a connector in Microsoft Teams | Build webhooks and connectors > Create Office 365 Connectors > [Build Teams connectors](sbs-teams-connectors.yml)|
|03/10/2022| Added information on Moodle LMS and Microsoft 365 plugins | Integrate with Teams > Moodle LMS > [Moodle learning management system](resources/moodle-overview.md)|
|03/03/2022 | How to add authentication using external OAuth provider| Add authentication > Tabs > [Use external OAuth providers](tabs/how-to/authentication/auth-oauth-provider.md) |
|02/25/2022| Introduced step-by-step guide to invoke task modules in Teams| Build cards and task modules > Build task modules > Use task modules from bots > [Invoke task module from Teams](sbs-botbuilder-taskmodule.yml)|
|02/24/2022| Introduced step-by-step guide to build action based message extension | Build Message Extensions > Action commands > Define action commands > [Build action based message extension](sbs-meetingextension-action.yml)|
|02/24/2022| Introduced step-by-step guide to build search based message extension | Build message extensions > Search commands > Define search commands > [Build search based message extension](sbs-messagingextension-searchcommand.yml)|
|02/24/2022| Introduced step-by-step guide to create Outgoing Webhooks | Build webhooks and connectors > Create Outgoing Webhooks > [Create Outgoing Webhooks](sbs-outgoing-webhooks.yml)|
| 02/23/2022 |Microsoft Teams store ranking parameters| Distribute your app > Publish to the Teams store > [Microsoft Teams store ranking parameters](concepts/deploy-and-publish/appsource/post-publish/teams-store-ranking-parameters.md)|
|02/09/2022| Introduced step-by-step guide how to upload files to Teams from a bot | Build bots > Send and receive files > [step-by-step guide how to upload files to Teams from a bot](sbs-file-handling-in-bot.yml) |
| 02/18/2022 | Introduced extensive Glossary for the Microsoft Teams Developer Documentation to help you find the definition about a term quickly | [Glossary](~/get-started/glossary.md) |
| 02/18/2022 | Updated the Overview module for mapping Teams app to organizational goals, user story, and exploring Teams app features | [Overview > Teams app that fits](overview.md) |
| 02/18/2022 | Updated the App fundamentals module to Plan your app to include mapping use cases to Teams features, and app planning checklist | [Plan your app > Overview](~/concepts/app-fundamentals-overview.md) |
|02/17/2022| What to expect after you submit your app?| Distribute your app > Publish to the Teams store > [Overview](concepts/deploy-and-publish/appsource/publish.md)|
|02/15/2022| Introduced step-by-step guide how to upload files to Teams from a bot | Build bots > Send and receive files > [Step-by-step guide how to upload files to Teams from a bot](sbs-file-handling-in-bot.yml) |
|02/11/2022| Shared meeting stage| • Build apps for Teams meetings > [Shared meeting stage](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md#shared-meeting-stage) </br> • Build apps for Teams meetings > [Meeting apps API references](apps-in-teams-meetings/API-references.md) </br> • App manifest > Public developer preview > [Developer preview manifest schema](resources/schema/manifest-schema-dev-preview.md)|
|02/08/2022| Introduced step-by-step guide to create Calling and Meeting bot| Build bots > Calls and meetings bots > Register calls and meetings bot > [Step-by-step guide to create Calling and Meeting bot](sbs-calling-and-meeting.yml) |
|02/07/2022| Tools and SDKs |Teams Toolkit for Visual Studio Code > </br> • Add capabilities to Teams app> [Add capabilities to your Teams apps](toolkit/add-capability.md) </br> • Add cloud resources to Teams app> [Add cloud resources to your Teams app](toolkit/add-resource.md) |
|02/03/2022| Introduced app manifest version 1.12 | • App manifest > [App manifest schema](resources/schema/manifest-schema.md) </br> • App manifest > Public developer preview > [Manifest schema](resources/schema/manifest-schema-dev-preview.md) |-->


## <a name="ga-features"></a>一般提供の特徴

すべてのアプリ開発者が利用可能な Microsoft Teams プラットフォーム機能。

<br>

<details>
<summary><b>2022</b></summary>

| **Date** | **Update** | **ここで検索** |
| -------- | --------- | ----------------|
|05/24/2022| Outlook と Office が有効なアプリを Teams ストアに送信する | Microsoft 365 間でアプリを拡張する [概要](m365-apps/overview.md) |
|05/24/2022| TeamsJS バージョン 2.0.0 のアプリ ガイダンスと新機能| ツールと SDK > [Teams JavaScript クライアント SDK](tabs/how-to/using-teams-client-sdk.md)  |
| 05/24/2022 | Visual Studio Code 用 Teams Toolkit バージョン 4.0.0 の一般提供開始 | ［ツールと SDK］ > ［Visual Studio Code 用 Teams Toolkit］ <br> •  [Teams ツールキットの概要](toolkit/teams-toolkit-fundamentals.md) <br> • [Build コマンド ボットと JavaScript](toolkit/add-capability.md) <br> • [JavaScript を使用した通知ボットのビルド](toolkit/add-capability.md) <br> • [Teams アプリ マニフェストのプレビューとカスタマイズ](toolkit/TeamsFx-preview-and-customize-app-manifest.md) <br> • [既存の API に接続します](toolkit/add-API-connection.md) <br> • [Teams アプリに機能を追加する](toolkit/add-capability.md) <br> • [シングル サインオン エクスペリエンスを追加する](toolkit/add-single-sign-on.md) <br> • [Teams アプリにクラウド リソースを追加する](toolkit/add-resource.md) |
|05/24/2022|GCC と GCCH のボットとメッセージ拡張機能| • [アプリの計画] > [[概要]](concepts/app-fundamentals-overview.md#government-community-cloud) </br> • ボットの作成> [概要](bots/what-are-bots.md) </br> • メッセージ拡張機能の作成> [概要](messaging-extensions/what-are-messaging-extensions.md) |
|04/26/2022|ボットを使用した個人用アプリのアンインストール動作 | [ボットの構築] > [ボットの会話] > [[ボットを使用した個人用アプリのアンインストール動作]](bots/how-to/conversations/subscribe-to-conversation-events.md#uninstall-behavior-for-personal-app-with-bot)|
|04/22/2022| 収益化されたアプリのテスト プレビュー | [アプリの収益化] > [[収益化アプリのテスト プレビュー]](concepts/deploy-and-publish/appsource/prepare/test-preview-for-monetized-apps.md)
|04/22/2022| アプリの収益化のためのアプリ内購入フロー | [アプリの収益化] > [[アプリ内購入]](concepts/deploy-and-publish/appsource/prepare/in-app-purchase-flow.md)
|2022/04/28| アプリ検証エラーの一般的な理由 | [アプリの配布] > [Teams ストアへの公開] > [[アプリ検証エラーの一般的な理由](concepts/deploy-and-publish/appsource/common-reasons-for-app-validation-failure.md)]|
|04/20/2022 |  CI/CD パイプラインを設定する | [ツールと SDK] > [Visual Studio Code 向け Teams ツールキット] > [[CI/CD パイプラインの設定]](toolkit/use-CICD-template.md)|
|04/19/2022 | Microsoft Teams でアプリをアップロードする | アプリを配布する > [アプリをアップロードする](concepts/deploy-and-publish/apps-upload.md)|
|04/01/2022| Teams ボットを作成するためのステップバイステップのガイドを導入しました| [ボットの構築] > [ボットの会話] > [チャネルとグループの会話]  > [Teams 会話型ボットを作成するためのステップバイステップ ガイド](sbs-teams-conversation-bot.yml) |
|03/30/2022| タブとボットを使用した Blazor アプリの [使用を開始するモジュール] の更新|  はじめに＞[Blazorを使用して初めてのアプリを構築する](sbs-gs-blazorupdate.yml)|
|03/30/2022|ブラウザーのデバイスのアクセス許可 | [デバイス機能を統合する] > [[ブラウザーのデバイス アクセス許可]](concepts/device-capabilities/browser-device-permissions.md) |
|03/29/2022 |ユーザー ピッカーを統合する | [Teams との統合] > [[ユーザー ピッカーを統合する]](concepts/device-capabilities/people-picker-capability.md)
|03/23/2022| ボットを使用して Teams でリンクを展開するためのステップ バイ ステップ ガイドを導入しました | メッセージ拡張機能の構築＞リンクの展開の追加＞ [ボットを使用して Teams でリンクを展開](sbs-botbuilder-linkunfurling.yml)|  
|03/22/2022| デバッグ プロセスに関する情報を追加しました| • ツールと SDK> Visual Studio Code 用 Teams ツールキット> [Teams アプリをローカルでデバッグする](toolkit/debug-local.md) </br> • ツールと SDK> Visual Studio Code 用 Teams ツールキット [バックグラウンド プロセスのデバッグ](toolkit/debug-background-process.md)|
|03/14/2022| Microsoft Teams でコネクタを構築してテストするためのステップバイステップ ガイドを導入しました。 | Webhook とコネクタのビルド> Office 365 コネクタの作成> [Teams コネクタのビルド](sbs-teams-connectors.yml)|
|03/10/2022 | Moodle LMS および Microsoft 365 プラグインに関する情報を追加しました | [Teams との統合] > [Moodle LMS] > [[Moodle ラーニング管理システム]](resources/moodle-overview.md)|  
|03/03/2022 | 外部 OAuth プロバイダーを使用して認証を追加する方法| [認証の追加] > [タブ] >[[外部 OAuth プロバイダーの使用]](tabs/how-to/authentication/auth-oauth-provider.md) |
| 02/25/2022| Teams でタスク モジュールを呼び出すステップ バイ ステップ ガイドを導入しました| [カードとタスク モジュールの構築] > [タスク モジュールの構築] > [ボットからのタスク モジュールの使用] > [[Teams からのタスク モジュールの呼び出し]](sbs-botbuilder-taskmodule.yml)|
| 02/24/2022| アクション ベースのメッセージ拡張機能を構築するためのステップ バイ ステップ ガイドを導入しました | [メッセージ拡張機能の構築] > [アクション コマンド] > [アクション コマンドの定義] > [[アクション ベースのメッセージ拡張機能の構築]](sbs-meetingextension-action.yml)|
| 02/24/2022| 検索ベースのメッセージ拡張機能を構築するためのステップ バイ ステップ ガイドが導入されました | [メッセージ拡張機能の構築] > [検索コマンド] > [検索コマンドの定義] > [[検索ベースのメッセージ拡張機能の構築]](sbs-messagingextension-searchcommand.yml)|
| 02/24/2022| 送信 Webhook を作成するためのステップバイステップ ガイドを導入しました | [Webhook とコネクタの構築] > [送信 Webhook の作成] > [[送信 Webhooks の作成]](sbs-outgoing-webhooks.yml)|
| 02/23/2022 |Microsoft Teams ストアのランク付けパラメーター| [アプリの配布] > [Teams ストアに公開] > [[Microsoft Teams ストアのランク付けパラメーター]](concepts/deploy-and-publish/appsource/post-publish/teams-store-ranking-parameters.md)|
| 02/18/2022 | 用語に関する定義をすばやく見つけるのに役立つ、Microsoft Teams 開発者ドキュメントの広範な用語集を導入しました | [用語集](~/get-started/glossary.md) |
| 02/18/2022 | Teams アプリを組織の目標、ユーザー ストーリーにマッピングし、Teams アプリの機能を検索するための概要モジュールを更新しました | [[概要] > [適合する Teams アプリ]](overview.md) |
| 02/18/2022 | ユース ケースの Teams 機能へのマッピングとアプリ計画チェックリストを含めるために、[アプリの基礎] モジュールを [アプリの計画] に更新しました | [[アプリの計画] > [概要]](~/concepts/app-fundamentals-overview.md) |
| 02/17/2022 | アプリを送信した後、何を期待しますか?| アプリを配布する > Teams ストアに公開する > [概要](concepts/deploy-and-publish/appsource/publish.md) |
| 2022/02/15 | ボットから Teams にファイルをアップロードする方法のステップバイステップ ガイドが導入されました | 「ボットを作成する」 > 「ファイルを送受信する」 > 「[ボットから Teams にファイルをアップロードするためのステップバイステップ ガイド](sbs-file-handling-in-bot.yml)」 |
| 02/11/2022 | 共有会議ステージ| • [Teams 会議用アプリのビルド] > [[共有会議ステージ]](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md#shared-meeting-stage) </br> • [Teams 会議用アプリのビルド] > [[Meeting apps API リファレンス]](apps-in-teams-meetings/API-references.md) </br> • [アプリ マニフェスト] > [開発者向けパブリック プレビュー] > [[開発者向けプレビュー マニフェスト スキーマ]](resources/schema/manifest-schema-dev-preview.md)|
| 02/08/2022 | 通話と会議ボットを作成するステップバイステップ ガイドを導入しました| [ボットの構築] > [通話と会議のボット] > [通話と会議のボットの登録] > [[通話と会議のボットを作成するためのステップバイステップ ガイド]](sbs-calling-and-meeting.yml) |
| 02/02/2022 | アプリ マニフェスト バージョン 1.12 が導入されました | [アプリ マニフェスト] > [[アプリ マニフェストのスキーマ]](resources/schema/manifest-schema.md) |
| 2022 年 1 月 25 日 | リアルタイム キャプション API を送信する | [Teams Meetings 用のアプリを作成する] > [Meeting Apps API リファレンス] > [[Meeting Apps API リファレンス]](apps-in-teams-meetings/API-references.md#send-real-time-captions-api)|
| 01/19/2022 | アダプティブ カードは、完了フィードバックを形成します | ボットのビルド > ボットの会話 > ボットの会話のメッセージ > [フォーム完了フィードバック](bots/how-to/conversations/conversation-messages.md#form-completion-feedback)|
| 2022/1/17 | デスクトップ版アダプティブ カードのユーザー ピッカー | [カードとタスク モジュールの構築] > [カードの構築] > [[アダプティブ カードのユーザー ピッカー]](task-modules-and-cards/cards/people-picker.md)|

</details>

<br>

<details>
<summary><b>さらに以前の更新プログラム</b></summary>
<br>
ここに記載されている以前の GA リリースの更新プログラムについて詳細を確認してください。
<br><br>

<details>
<summary><b>2021</b></summary>

| **Date** | **Update** | **ここで検索** |
| -------- | --------- | ----------------|
|2021/12/24| タブ デバイスのアクセス許可を付与するためのステップバイステップ ガイドを導入しました | 「アプリの基礎」 > 「デバイス機能」 > 「[タブ デバイスのアクセス許可を付与するためのステップバイステップ ガイド](sbs-tab-device-permissions.yml)」 |
|2021/12/23| アダプティブ カード付きタブを作成するためのステップバイステップ ガイドを導入しました| [認証の追加] > [タブ] > [SSO 認証の使用] > [[アダプティブ カードでタブを作成するためのステップバイステップ ガイド]](sbs-tab-with-adaptive-cards.yml) |
|2021/12/21 | 「作業の開始」の Teams Toolkit 3.0.0 用 JavaScript、C#、Node.js モジュールを更新しました | • [使用を開始する] > [[JavaScript を使用した初めてのアプリのビルド]](sbs-gs-javascript.yml) <br> • [使用を開始する] > [[C# または .NET を使用した初めてのアプリのビルド]](sbs-gs-csharp.yml) <br> • [使用を開始する] > [[Node.js を使用した初めてのアプリのビルド]](sbs-gs-nodejs.yml) |
|2021/12/20| シングルサインオン (SSO) を利用したタブ拡張機能およびメッセージ拡張機能向けのステップバイステップ ガイド | [認証の追加] > [タブ] > [SSO 認証の使用] > [[タブ拡張機能およびメッセージ拡張機能向けの SSO を使用してタブを作成するためのステップバイステップ ガイド]](sbs-tabs-and-messaging-extensions-with-SSO.yml)|
|2021/12/20| 会議コンテンツ バブルを作成するためのステップバイステップ ガイドを導入しました | [Teams 会議] > [会議用アプリを有効化して構成する] > [[会議コンテンツ バブルを作成するためのステップバイステップ ガイド]](sbs-meeting-content-bubble.yml) でアプリを作成します |
|2021/12/9| 会議ステージ ビューのステップバイステップ ガイドを導入しました | [Teams 会議] > [会議用アプリを有効化して構成する] > [[会議ステージ ビューを作成するためのステップバイステップ ガイド]](sbs-meetings-stage-view.yml) でアプリを作成します|
|2021/12/13 | SaaS の提供にリンクしたアプリのガイドラインを導入しました | [アプリの配布] > [Teams ストアに公開する] > [ストアの検証ガイドラインを確認する] > [[SaaS の提供にリンクしたアプリのガイドライン]](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#apps-linked-to-saas-offer)|
|2021/12/9| 会議のサイドパネルを作成するためのステップバイステップ ガイドを導入しました | [Teams 会議] > [会議用アプリを有効化して構成する] > [[会議Teams で会議のサイドパネルを作成するためのステップバイステップ ガイド]](sbs-meetings-sidepanel.yml) でアプリを作成します|
|2021/12/1 | 新しいストア アイコンを導入しました | • [アプリの設計] > [アプリの機能] > [[Microsoft Teams 向け個人用アプリの設計]](concepts/design/personal-apps.md)</br> • [アプリの設計] > [UI コンポーネント] > [[高度な UI コンポーネントを使用して Microsoft Teams アプリを設計する]](concepts/design/design-teams-app-advanced-ui-components.md) |
|2021/11/24| 会議のトークンを生成するためのステップバイステップ ガイドを導入しました | [Teams 会議] > [会議用アプリを有効化して構成する] > [[会議Teams で会議のトークンを作成するためのステップバイステップ ガイド]](sbs-meeting-token-generator.yml) でアプリを作成します|
|2021/11/17| 更新された Microsoft Teams ストア検証ガイドライン|[ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)|
|2021/11/17| デスクトップおよびモバイル ユーザー向けの静的/動的先行入力検索 | • [カードとタスク モジュールの構築] > [カードの構築] > [[アダプティブ カードの先行入力検索]](task-modules-and-cards/cards/dynamic-search.md) </br> • [カードとタスク モジュールの構築] > [カードの構築] > [概要] > [[アダプティブ カードの先行入力検索]](task-modules-and-cards/what-are-cards.md#type-ahead-search-in-adaptive-cards) </br> • [カードとタスク モジュールの構築] > [概要] > [[カードとタスク モジュール]](task-modules-and-cards/cards-and-task-modules.md)|
|2021/11/13| ボットは、リソース固有のコンテンツ (RSC) を使用して、すべてのチャネル メッセージの受信を有効化できます | • [ボットの構築] > [ボットの会話] > [ボット会話のメッセージ] > [[RSC を使用してすべてのチャネル メッセージを受信する]](~/bots/how-to/conversations/channel-messages-with-rsc.md) </br> • [ボットの構築] > [ボットの会話] > [[ボット会話の概要]](~/bots/how-to/conversations/conversation-basics.md) </br> • [ボットの構築] > [ボットの会話] > [[チャネルとグループの会話]](~/bots/how-to/conversations/channel-and-group-conversations.md) |
|2021/10/28| 取引可能な SaaS プランを使用して Teams アプリを収益化する | [アプリの配布] > [Teams ストアに公開する] > [[SaaS プランを Teams アプリに含める]](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md) |
|2021/10/25| ステップバイステップのガイドの新しい構造と手順を使用して Microsoft Teams 開発者ドキュメントの [使用を開始する] モジュールが更新されました | [使用を開始する] > [[最初の Teams アプリの使用を開始する]](get-started/get-started-overview.md) |
|2021/10/20| 一般提供で会議ステージを使用できるようになりました | [Teams 会議用アプリの作成] > [[Teams 会議用アプリを有効化して構成する]](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md) |
|2021/10/20| 会議の詳細 API とリアルタイム Teams 会議イベント | [Teams 会議用のアプリをビルドする] > [[会議の詳細 API を取得する]](apps-in-teams-meetings/API-references.md#get-meeting-details-api) |
|2021/10/18| タブのリンクの展開とステージ ビュー | [タブの構築] > [[タブのリンクの展開とステージ ビュー]](tabs/tabs-link-unfurling.md) |
|2021/10/8| アダプティブ カードの設計に関する新しいベスト プラクティス | [アプリの設計] > [UI コンポーネント] > [[Teams アプリのアダプティブ カードを設計する]](task-modules-and-cards/cards/design-effective-cards.md) |
|2021/10/5| 管理者がアプリの表示を許可するまで Teams アプリを非表示にします | [アプリの設計] > [[管理者が承認するまで Teams アプリを非表示にする]](concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves) |
|2021/10/5| Teams モバイル用のアプリを計画します | [アプリの基礎] > [[Teams モバイルの応答タブを計画する]](concepts/design/plan-responsive-tabs-for-teams-mobile.md) |
|2021/10/4| Teams アプリを管理するために、新しい Teams 向け開発者ポータルが導入されました | [ツールと SDK] > [[Teams の開発者ポータル]](concepts/build-and-test/teams-developer-portal.md) |
|2021/9/21|Teams は、ボットや受信 Webhook 向けのユーザーのメンションで Azure AD オブジェクト ID と UPN をサポートしています | • [カードとタスク モジュールの構築] > [カードの構築] > [[ユーザーのメンションでの Azure AD オブジェクト ID と UPN]](task-modules-and-cards/what-are-cards.md#support-for-azure-ad-object-id-and-upn-in-user-mention) </br> • [カードとタスク モジュールの構築] > [カードの構築] > [[カードの概要]](task-modules-and-cards/cards/cards-format.md#format-cards-with-markdown) |
|2021/8/16| アダプティブカード (v1.3、すべての機能向け) およびユニバーサル アクション (v1.4、ボット送信カード向け) での入力の検証をサポートします | • [アダプティブ カード] > [カードの作成] > [[入力の検証]](/adaptive-cards/authoring-cards/input-validation)</br> • [カードとタスク モジュールの構築] > [カードの構築] > [アダプティブ カード向けユニバーサル アクション] > [[アダプティブ カード v1.4 向けユニバーサル アクション]](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|2021/8/30| カスタム Together モードのシーン機能は、参加者を 1 つの仮想シーンにまとめ、そのビデオ ストリームを事前に決定された席に配置します | [Teams 会議用のアプリの構築] > [[カスタム Together モード シーン]](~/apps-in-teams-meetings/teams-together-mode.md) |
|2021/8/25| シングルサインオン (SSO) を使用して Teams ボットを作成するためのステップバイステップのガイドを導入しました | [認証の追加] > [ボット] > [[SSO を使用して Teams ボットを作成するためのステップバイステップのガイド]](sbs-bots-with-sso.yml) |
|2021/8/19| 会話スレッドにボットをインストールしたときに受信するインストール更新イベント | [ボットの構築] > [ボットの会話] > [[インストール更新イベント]](bots/how-to/conversations/subscribe-to-conversation-events.md#installation-update-event) |
|2021/8/12|アダプティブ カードを使用してタブをビルドする| [タブの構築] > [[アダプティブ カードを使用してタブを構築する]](tabs/how-to/build-adaptive-card-tabs.md) |
|2021/8/4|タブのエクスペリエンスを囲む余白がなくなります | [タブの構築] > [[タブの余白を削除する]](resources/removing-tab-margins.md) |
|2021/7/8|Teams モバイルに会議中のアプリのサポートが追加されました | [Teams 会議用アプリの構築] > [[会議アプリの拡張性]](apps-in-teams-meetings/meeting-app-extensibility.md) |
|2021/6/28|ユーザー ピッカー機能を統合する | [Teams との統合] > [[ユーザー ピッカー機能を統合する]](concepts/device-capabilities/people-picker-capability.md) |  
|2021/6/25| プロアクティブ メッセージを送信するためのステップバイステップのガイドを導入しました | [ボットの構築] > [ボットの会話] > [プロアクティブ メッセージ] > [[プロアクティブ メッセージを送信するためのステップバイステップのガイド]](sbs-send-proactive.yml) |
|2021/6/9| `allowExpand` 属性を使用したアダプティブ カードの画像のステージ ビュー | [カードとタスク モジュールの構築] > [カードの構築] > [[アダプティブ カードの画像用ステージ ビュー]](task-modules-and-cards/cards/cards-format.md#stage-view-for-images-in-adaptive-cards) |
|2021/5/31| 会話タブ | [タブの構築] > [[タブ内のコンテンツに関する会話の開始と続行]](~/tabs/how-to/conversational-tabs.md) |
|2021/5/24| モバイル パターンを使用して Teams アプリのデザイン ガイドラインを更新しました | [アプリをデザインする] > [[Teams アプリのデザイン]](~/concepts/design/design-teams-app-overview.md) |
|2021/5/13| mConnect と Skooler の情報を追加しました | [Teams との統合] > [Moodle LMS] > [[Moodle ラーニング管理システム]](resources/moodle-overview.md)|
|2021/5/10| アプリ マニフェスト v1.10 をリリースしました | [アプリ マニフェスト] > [[マニフェストのスキーマ]](resources/schema/manifest-schema.md) |
|2021/5/10| 新しいアプリのカスタマイズ機能 | [アプリをデザインする] > [[組織でアプリをカスタマイズできるようにする]](concepts/design/enable-app-customization.md) |
|2021/5/7| チャットでの音声通話とビデオ通話のためのディープ リンク | [Teams との統合] > [[ディープ リンク]](concepts/build-and-test/deep-links.md#deep-linking-to-an-audio-or-audio-video-call) |
|2021/4/30|Teams ストアにアプリを発行する方法に関する新しいガイダンス | • [Teams ストアに公開する] > [[アプリを Teams ストアに公開する]](concepts/deploy-and-publish/appsource/publish.md)</br> • [Teams ストアに公開する] > [[Teams ストア検証ガイドライン]](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|2021/4/29 | アダプティブ カード v1.4 のユニバーサル アクションのサポート | [カードとタスク モジュールの構築] > [カードの構築] > [アダプティブ カード向けユニバーサル アクション] > [[アダプティブ カード向けユニバーサル アクション]](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|2021/4/29 | ユーザー固有のビュー | [カードとタスク モジュールの構築] > [カードの構築] > [アダプティブ カード向けユニバーサル アクション] > [[ユーザー固有のビュー]](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/User-Specific-Views.md) |
|2021/4/29 | シーケンシャル ワークフロー | [カードとタスク モジュールの構築] > [カードの構築] > [アダプティブ カード向けユニバーサル アクション] > [[シーケンシャル ワークフロー]](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Sequential-Workflows.md) |
|2021/4/29 | 最新のカード | [カードとタスク モジュールの構築] > [カードの構築] > [アダプティブ カード向けユニバーサル アクション] > [[最新のカード]](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Up-To-Date-Views.md) |
|2021/4/8| アプリのカスタマイズ機能 | • [アプリをデザインする] > [[Teams アプリの設計の概要]](concepts/design/enable-app-customization.md)</br> • [ツールと SDK] > [[開発者ポータル]](concepts/build-and-test/teams-developer-portal.md) </br> • [アプリ マニフェスト] > [開発者向けパブリック プレビュー > [[マニフェスト スキーマ]](resources/schema/manifest-schema-dev-preview.md) |
|2021/3/18| 通知: `TeamsInfo.getMembers` と `TeamsInfo.GetMembersAsync` の非推奨プロセスを開始したため、Bot Framework SDK のバージョン 4.10 以上に更新してください。 | [ボットの構築] > [[チーム/チャット メンバーのボット API の変更]](resources/team-chat-member-api-changes.md) |
|2021/3/5|既定のインストール範囲とグループ機能 | [アプリを配布する] > [[既定のインストール範囲とグループ機能]](concepts/deploy-and-publish/add-default-install-scope.md) |
|2021/3/5|個人用アプリ タブの並べ替え | [タブの構築] > [[個人用アプリのチャット タブの並び替え]](tabs/how-to/create-personal-tab.md#reorder-static-personal-tabs) |
|2021/3/4|アダプティブ カードでの情報マスク | [カードとタスク モジュールの構築] > [カードの構築] > [[アダプティブ カードの情報マスキング]](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|2021/2/19|位置情報機能が追加されました。 <br/> 位置情報機能の情報が、デバイス機能の概要、ネイティブ デバイスのアクセス許可、メディア機能の統合、QR またはバーコード スキャナー機能の各ファイルに追加されます | • [アプリの基礎] > [デバイス機能] > [[概要]](concepts/device-capabilities/device-capabilities-overview.md) </br> • [アプリの基礎] > [デバイス機能] > [[デバイス アクセス許可の要求]](concepts/device-capabilities/native-device-permissions.md) </br> • [アプリの基礎] > [デバイス機能] > [[メディア機能を統合する]](concepts/device-capabilities/mobile-camera-image-permissions.md) </br> • [アプリの基礎] > [デバイス機能] > [[QR コードまたはバーコード スキャナー機能を統合する]](concepts/device-capabilities/qr-barcode-scanner-capability.md) </br> • [アプリの基礎] > [デバイス機能] > [[位置情報機能を統合する]](concepts/device-capabilities/location-capability.md) |
|2021/2/18|QR コードまたはバーコード スキャナー機能が追加されました。 <br/> QR またはバーコード スキャナー機能の情報が、デバイス機能の概要、ネイティブ デバイスのアクセス許可、メディア機能の統合の各ファイルに追加されます | • [アプリの基礎] > [デバイス機能] > [[概要]](concepts/device-capabilities/device-capabilities-overview.md) </br> • [アプリの基礎] > [デバイス機能] > [[デバイス アクセス許可の要求]](concepts/device-capabilities/native-device-permissions.md) </br> • [アプリの基礎] > [デバイス機能] > [[メディア機能を統合する]](concepts/device-capabilities/mobile-camera-image-permissions.md) </br> • [アプリの基礎] > [デバイス機能] > [[QR コードまたはバーコード スキャナー機能を統合する]](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|2021/2/9|デバイス機能の概要が追加されました。 <br/> マイク機能の情報が、ネイティブ デバイスのアクセス許可、メディア機能の統合の各ファイルに追加されます |• [アプリの基礎] > [デバイス機能] > [[概要]](concepts/device-capabilities/device-capabilities-overview.md) </br> • [アプリの基礎] > • [デバイス機能] > [[デバイス アクセス許可の要求]](concepts/device-capabilities/native-device-permissions.md) </br> • [アプリの基礎] > [デバイス機能] > [[メディア機能を統合する]](concepts/device-capabilities/mobile-camera-image-permissions.md)|

<br>

</details>

<br>

<details>
<summary><b>2020</b></summary>

| **Date** | **Update** | **ここで検索** |
| -------- | --------- | ------------------ |
|2020/11/30|Teams Toolkit とタブ用 Visual Studio Code を使用した ID プラットフォームの統合 |[Teams ツールキットとタブ用 Visual Studio Code を使用したシングル サインオン認証](toolkit/visual-studio-code-tab-sso.md)|
|2020/11/16|Teams アプリ マニフェストがバージョン 1.8 に更新されました。|[参照: Microsoft Teams のマニフェスト スキーマ](resources/schema/manifest-schema.md)|
|2020/11/10|Teams ボットの設計ガイドライン |[ボット デザイン ガイドライン](bots/design/bots.md)|
|2020/9/30|モバイル デバイスでのボットとのファイルの送受信がサポートされるようになりました |[ボットを介してファイルを送受信する](resources/bot-v3/bots-files.md)|
|2020/9/22|Teams 開発を開始するための新しい情報 |[最初の Teams アプリの構築の概要](build-your-first-app/build-first-app-overview.md)|
|2020/9/18|会議中の Teams アプリのサポート (リリース プレビュー) |[Teams 会議のアプリ](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|2020/8/19|Microsoft Graph を使用して Teams メッセージをインポートします |[Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする](graph-api/import-messages/import-external-messages-to-teams.md)
|2020/8/12 |受信 Webhookでのアダプティブ カードのサポートが一般提供に移行しました |[受信 Webhook を使用してアダプティブ カードを送信する](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|2020/8/10|Visual Studio ツールキットを使用して Teams アプリの構築を開始します |[Microsoft Teams ツールキットと Visual Studio Code を使用してアプリを構築する](toolkit/visual-studio-overview.md) |
|2020/8/6|タブの SSO 認証のサポート |[SSO Microsoft Teams のタブを開発する](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|2020/7/27 | Graph のプロアクティブ ボットとメッセージ (パブリック プレビュー) |[Microsoft Graph を使用した Teams でプロアクティブなボットをインストールしてプロアクティブ メッセージを有効にする](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
|2020/7/22 |モバイル デバイスの機能更新 |[Microsoft Teams タブのデバイス アクセス許可を要求する](concepts/device-capabilities/native-device-permissions.md) |
|2020/7/20|AppSource 申請用の Teams アプリ検証ツール |[Teams アプリ認証ツール](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|2020/7/15|Teams の仮想アシスタントを作成します |[Microsoft Teams 用仮想アシスタント](samples/virtual-assistant.md)|
|2020/7/14|ネイティブ読み込みインジケーターのドキュメントの表示 |[ネイティブ読み込みインジケーターの表示](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|2020/7/1|Visual Studio Code ツールキットを使用して Teams アプリの構築を開始します |[Microsoft Teams ツールキットと Visual Studio Code を使用してアプリを構築する](toolkit/visual-studio-code-overview.md) |
|2020/7/1|Teams Web クライアントおよびデスクトップ クライアント向けタブのシングル サインオンの一般提供 |[シングル サインオン (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|2020/6/5| マニフェスト スキーマがバージョン 1.7 に更新されました。| [参照: Microsoft Teams のマニフェスト スキーマ](resources/schema/manifest-schema.md)|
|2020/5/18|Power Virtual Agent と Teams の統合 |[Power Virtual Agent チャットボットを Microsoft Teams と統合する](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|2020/4/1|WFM システムと Teams 用シフト コネクタの統合 |[Microsoft Teams シフトの WFM コネクタ](samples/shifts-wfm-connectors.md)
|2020/3/24 | 会話の単一メンバーの取得のサポート、ページングされたメンバー取得のサポートを追加しました | [Teams のコンテキストをボット用に取得する](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **Update** | **ここで検索** |
| -------- | --------- | ------------------ |
| 2020/12/26 | ボットに送信されるペイロードの `replyToId` パラメーターが暗号化されなくなったため、この値を使用してこれらのメッセージへのディープ リンクを構築できるようになります。メッセージ ペイロードには、パラメーター に暗号化された値が含まれます`legacy.replyToId`。  |
| 2019/11/5 | Teams JavaScript SDK を使用したシングル サインオン。 | [シングル サインオン](tabs/how-to/authentication/auth-aad-sso.md) |
| 2019/10/31 | 会話ボットとメッセージ拡張機能のドキュメントが 4.6 Bot Framework SDK に合わせて更新されました。 v3 SDK のドキュメントが [リソース] セクションで利用できます。 | すべてのボットとメッセージ拡張機能のドキュメント |
| 2019/10/31 | 新しいドキュメントの構造と記事の大幅なリファクタリング。 デッド リンクや 404 が発生した場合は、GitHub イシューを作成して報告してください。 | すべての項目です。 |
| 2019/9/13 | 要求ボットは、操作ベースのメッセージ拡張機能からインストールされます。 | [メッセージ拡張機能を使用した操作の開始](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 2019/8/28 | タブとコネクターのプライベート チャネルのサポート。 | [タブのコンテキストを取得する](tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) |
| 2019/6/20 | 外部 Web サイトを、外部 Web サイトから、Teams チャネルに共有します。 | [Teams への共有](~/share-to-teams.md) |
| 2019/5/25 | タスク モジュールからのボット メッセージで応答します。 | [タスク モジュールからのボット メッセージで応答する](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 2019/5/25 | グループ チャット内のボット。 | [グループ チャットやチャネルでのボットとの対話](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 2019/5/20 | アプリ マニフェストのローカリゼーション。 | [アプリのローカリゼーション](~/publishing/apps-localization.md) |
| 2019/5/20 | メッセージの操作。 | [メッセージの操作](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 2019/5/20 | リンク展開 (カスタム URL プレビュー)。 | [リンク展開](messaging-extensions/how-to/link-unfurling.md)|
| 2019/5/6 | ストア アプリ用アプリケーション認定プログラム。 | [アプリケーション認定](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 2019/5/6 | アプリ テンプレートが利用可能になりました | [アプリ テンプレート](~/samples/app-templates.md) |
| 2019/4/23 | 操作ベースのメッセージ拡張機能が使用可能です。 | [操作ベースのメッセージング拡張機能](~/concepts/messaging-extensions/create-extensions.md) |
| 2019/2/18 | プライベート チャットへのディープ リンクの作成。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 2019/1/23 | タブ コンテキストで SKU とライセンスの種類の情報を表示します。 | [タブ コンテキスト](~/concepts/tabs/tabs-context.md) |
|
</details>

<br>

<details>
<summary><b>2018</b></summary>

| **Date** | **Update** | **ここで検索** |
| -------- | --------- | ------------------ |
| 2018 年 11 月 12 日 | リリースされたバージョンの Teams で、グループ チャットでタブを使用できるようになりました。 この作業の一環として、タブ セクションが分かりやすく作り直されました。| [構成可能なタブ](~/concepts/tabs/tabs-configurable.md) |
| 2018/11/11 | Node JS と .NET/C# の概要は、Teams で App Studio を使用するために更新され、Node ベースの Teams アプリを Azure でホスティングするための新しいセクションが追加されました。 | [C#/.NET と App Studio を使用して Microsoft Teams プラットフォームの使用を開始する](~/get-started/get-started-dotnet-app-studio.md)、[Node JS と App Studio を使用して Microsoft Teams プラットフォームの使用を開始する](~/get-started/get-started-nodejs-app-studio.md)、[Node Teams アプリを Azure にホストする](~/get-started/get-started-nodejs-in-azure.md)|
| 2018/11/9 | ユーザー間のプライベート チャットへのディープ リンクを作成できるようになりました。 | [チャットへのディープ リンクの設定](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 2018 年 11 月 8 日 | SharePoint Framework 1.7 がリリースされたことに伴い、Microsoft Teams タブを SharePoint Framework の Web パーツとして使用できる新機能が追加されました。 | [SharePoint のタブ](~/concepts/tabs/tabs-in-sharepoint.md) |
| 2018/11/5 | **タスク モジュール** 機能がリリースされました。 タスク モジュールを使用すると、Teams アプリケーションでボットとタブの両方からモーダル ポップアップ エクスペリエンスを作成することができます。 ポップアップ内で、独自のカスタム HTML/JavaScript コードを実行したり、YouTube や Microsoft Stream ビデオなどの `<iframe>` ベースのウィジェットを表示したり、[アダプティブ カード](/adaptive-cards/)を表示したりすることができます。 | [タスク モジュールの概要](~/concepts/task-modules/task-modules-overview.md)、[タブ内のタスク モジュール](~/concepts/task-modules/task-modules-tabs.md)、[ボット内のタスク モジュール](~/concepts/task-modules/task-modules-bots.md) |
| 2018/10/5 | Teams のデスクトップ、iOS、Android クライアントでカードの書式設定情報の更新およびテストが行われました。 | [カード](~/concepts/cards/cards.md)、[カードの書式設定](~/concepts/cards/cards-format.md) |
| 2018/9/24 | 通話やオンライン会議用のMicrosoft Graph API のベータ版がリリースされ、Teams アプリは音声とビデオを使用した豊富な方法でユーザーと対話できるようになりました。 | [通話とオンライン会議のボット](~/concepts/calls-and-meetings/registering-calling-bot.md)、[リアルタイム メディアの概念](~/concepts/calls-and-meetings/real-time-media-concepts.md)、[通話ボットの登録](~/concepts/calls-and-meetings/registering-calling-bot.md)、[デバッグとローカル テスト](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)、[アプリケーションがホストするメディア](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)、[着信通知の処理](~/concepts/calls-and-meetings/call-notifications.md) |
| 2018/9/11 | タブ構成ページが大幅に高くなりました。 | [タブ デザイン](tabs/design/tabs.md) |
| 2018/8/15 | Teams でアダプティブ カードがサポートされるようになりました。|[Teams でのアダプティブ カードのアクション](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 2018/8/10 | DevTools のクライアント サポート。| [Microsoft Teams デスクトップ クライアント用 DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 2018/8/8 | メッセージ拡張機能が複数のコマンドをサポートするようになりました。 | [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 2018/8/7 | コネクタでインライン構成がサポートされるようになりました。 コネクタのドキュメントも改訂され、分かりやすく拡張されました。| [コネクタ](~/concepts/connectors/connectors.md)|
| 2018/8/6 | ボットでファイルを送受信するようになりました。 | [ボットを介してファイルを送受信する](~/bots/how-to/bots-filesv4.md)|
| 2018/7/23 | アプリの再認証に関する情報が公開セクションに追加されました。 |[マニフェストのアクセス許可](resources/schema/manifest-schema.md#permissions)|
| 2018/7/16 | タブ構成ページに、より多くのスペースが割り当てられました。 | [タブ構成ページが大幅に高くなりました](tabs/design/tabs.md)|
| 2018/7/12 | ゲスト アクセスに関する情報。 | [Microsoft Teams でのゲスト アクセス](/microsoftteams/guest-access#guest-access-overview)|
| 2018/6/7 | Microsoft Teams テナント アプリ カタログの情報が追加されました。 | [Microsoft Teams アプリの公開](~/publishing/apps-publish.md)|
| 2018/5/29 | Teams でアダプティブ カードがサポートされます。 | [Teams でのアダプティブ カードのアクション](task-modules-and-cards/cards/cards-reference.md) |
| 2018/4/17 | replyToID が `Invoke` および `MessageBack` カード アクションのペイロードに追加されました。 これは、カード アクションの送信元のメッセージを更新する必要がある場合に特に便利です。 | [カード アクション](~/concepts/cards/cards-actions.md)|
| 2018/4/12 | Teams プログラミング インターフェイスとこのドキュメント セットの変更を追跡するこのトピックが追加されました。 | [最新情報](~/whats-new.md)|
| 2018/4/10 | 認証 URL で、パスにテナント ID を一貫して使用するように変更が行われました。 | [タブの認証フロー](~/concepts/authentication/auth-flow-tab.md)、[Azure AD タブ認証](~/concepts/authentication/auth-tab-AAD.md)|
| 2018/4/6 | コマンド ボックスの使用に関するデザイン ガイドラインが追加されました。 |[コマンド ボックス](~/resources/design/framework/command-box.md)|
| 2018/4/2 | ボットを使用して、アプリの通知を送信します。 |[通知のみのボット](~/concepts/bots/bots-notification-only.md)|
| 2018/3/27 | プロアクティブなメッセージングのためのドキュメントを展開しました。 |[会話の開始](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 2018/3/15 | カードのドキュメントがリファクタリングされました。 |[カード](~/concepts/cards/cards.md)、[カード アクション](~/concepts/cards/cards-actions.md)、[カードの書式設定](~/concepts/cards/cards-format.md)、[カード リファレンス](~/concepts/cards/cards-reference.md)|
| 2018/3/3 | Teams App Studio のドキュメントが追加されました。 |[Teams App Studio を使用したアプリの迅速な開発](~/get-started/get-started-app-studio.md)、[App Studio でのコントロール ライブラリの使用](~/get-started/app-studio-component-library.md)|
| 2018/2/27 | AsTeamsChannelAccounts() メソッドのデモを行うサンプル コードが追加されました。 |[コンテキストをボット用に取得する](~/concepts/bots/bots-context.md)|
| 2018/2/5 | C# の使用を開始するためのトピックが追加されました。 |[Microsoft Teams プラットフォームで C#/.NET を使い始める](./get-started/get-started-dotnet-app-studio.md)|
|
</details>
</details>

## <a name="developer-preview"></a>開発者向けプレビュー

開発者向けプレビューは、リリース前の Teams プラットフォーム機能にいち早くアクセスできる公開プログラムです。  

| **Date** | **Update** | **ここで検索** |
| -------- | --------- | ------------------ |
| 04/06/2022 | 個人用アプリまたはタブから Teams に共有する | [Teams と統合] > [Teams に共有] > [[個人用アプリまたはタブから Teams に共有]](concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md) |
| 02/07/2022 | ツールと SDK |Visual Studio Code 用 Teams ツールキット > </br> • [Teams アプリに機能を追加] > [[Teams アプリに機能を追加]](toolkit/add-capability.md) </br> • [クラウド リソースを Teams アプリに追加] > [[クラウド リソースを Teams アプリに追加]](toolkit/add-resource.md) |
| 02/03/2022 | アプリ マニフェスト バージョン 1.12 が導入されました | • [アプリ マニフェスト] > [[アプリ マニフェストのスキーマ]](resources/schema/manifest-schema.md) </br> • [アプリ マニフェスト] > [開発者向けパブリック プレビュー > [[マニフェスト スキーマ]](resources/schema/manifest-schema-dev-preview.md) |
|2022/1/17 | モバイル版アダプティブ カードのユーザー ピッカー  | [カードとタスク モジュールの構築] > [カードの構築] > [[アダプティブ カードのユーザー ピッカー]](task-modules-and-cards/cards/people-picker.md)|
|2022/1/10 | Visual Studio Code 用 Teams ツールキット | [ツールと SDK] > [Visual Studio Code 向け Teams ツールキット] > [[Teams ツールキットの基本]](toolkit/teams-toolkit-fundamentals.md) |
| 2021/12/24 | タブ デバイスのアクセス許可を付与するためのステップバイステップ ガイドを導入しました | [アプリの基本] > [デバイス機能] > [[タブ デバイスのアクセス許可を付与するためのステップバイステップ ガイド]](sbs-tab-device-permissions.yml) |
| 2021/11/15 | Outlook と Office で実行する個人用タブとメッセージ拡張機能 | [Teams アプリを Microsoft 365 全体に拡張する](~/m365-apps/overview.md) |
| 2021/10/28 |ボットは、リソース固有のコンテンツ (RSC) を使用して、すべてのチャネル メッセージの受信を有効化できます | • [ボットの構築] > [ボットの会話] > [ボット会話のメッセージ] > [[RSC を使用してすべてのメッセージを受信する]](~/bots/how-to/conversations/channel-messages-with-rsc.md) </br> • [ボットの構築] > [ボットの会話] > [[ボット会話の概要]](~/bots/how-to/conversations/conversation-basics.md) </br> • [ボットの構築] > [ボットの会話] > [[チャネルとグループの会話]](~/bots/how-to/conversations/channel-and-group-conversations.md) </br> • [アプリ マニフェスト] > [開発者向けパブリック プレビュー > [[開発者向けプレビュー マニフェスト スキーマ]](~/resources/schema/manifest-schema-dev-preview.md) |
| 2021/6/16 | チャットのリソース固有の同意 | • [Microsoft Graph を使用した Teams データの活用] > [[リソース固有の同意]](graph-api/rsc/resource-specific-consent.md) </br> • [アプリのテスト] > [Microsoft Graph] > [[Teams でリソース固有の同意をテストする]](graph-api/rsc/test-resource-specific-consent.md)|

詳細については、「[Teams の開発者向けパブリック プレビュー](~/resources/dev-preview/developer-preview-intro.md)」を参照してください。

## <a name="teams-app-template-catalog"></a>Teams アプリのテンプレート カタログ

新機能に合わせて、すぐに導入したり、ニーズに合わせて変更したりできる[稼働準備済みの Teams アプリ テンプレート](samples/app-templates.md)も提供しています。新しく追加されたテンプレートは星 ☆ で示されます。

## <a name="submit-your-feedback"></a>フィードバックをお寄せください

Microsoft では、Teams 開発者が質問をしたり、バグを報告したり、機能要求を送信したり、投稿したりすることを奨励しています。 フィードバックは、[利用可能なチャネル](feedback.md)のいずれかを通して送信することができます。

## <a name="get-latest-updates"></a>最新の更新プログラムを取得する

[RSS フィード](https://aka.ms/TeamsPlatformUpdates)を構成することで、Teams プラットフォーム更新プログラムを取得できます。

### <a name="to-configure-rss-feed"></a>RSS フィードを構成するには

1. Microsoft Teams を開きます。
1. 左側のウィンドウから **Teams** を選択します。
1. チーム内のチャネルを選択します。
1. 楕円形 &#x25CF;&#x25CF;&#x25CF; を選択し、ドロップダウン リストで **[コネクタ]** を選択します。
1. 表示された **[コネクタ]** ダイアログ ボックスで **RSS** を検索します。
1. **[構成]** を選択します。
1. **[RSS 接続の名前の入力]** で名前を入力します。
1. **[RSS フィードのアドレス]** で **<https://aka.ms/TeamsPlatformUpdates>** を入力します。
1. **[ダイジェストの頻度]** ドロップダウン リストでフィードの頻度を選択します。
1. **[保存]** を選択します。
