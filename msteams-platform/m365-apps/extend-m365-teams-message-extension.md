---
title: 複数のユーザー Teamsメッセージ拡張機能を拡張Microsoft 365
description: 検索ベースのメッセージング拡張機能を更新して、Teamsで実行する方法をOutlook
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 9a8fc4135a2238d1402e25ef31ad7ebb918475b8
ms.sourcegitcommit: 239807b74aa222452559509d49c4f2808cd9c9ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391358"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>複数のユーザー Teamsメッセージ拡張機能を拡張Microsoft 365

> [!NOTE]
> *アプリケーション全体にTeamsメッセージ拡張機能を拡張Microsoft 365* パブリック開発者向け [プレビューでのみ使用できます](../resources/dev-preview/developer-preview-intro.md)。 プレビューに含まれる機能は完全ではない可能性があります。また、パブリック リリースで利用可能になる前に変更が加わる可能性があります。 これらは、テストおよび探索の目的でのみ提供されます。 これらは、実稼働アプリケーションでは使用できません。

検索ベースの[メッセージング拡張機能を使用](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)すると、ユーザーは外部システムを検索し、クライアントの作成メッセージ領域を通じて結果をMicrosoft Teamsできます。 Teams アプリを[Microsoft 365 (プレビュー)](overview.md)に拡張することで、Windows デスクトップと Web エクスペリエンス用に検索ベースの Teams メッセージ拡張機能を Outlook Windows に追加できます。

検索ベースのメッセージ拡張機能を更新して、Teamsを実行するプロセスにはOutlook手順が含まれます。

> [!div class="checklist"]
> * アプリ マニフェストを更新する
> * ボットのOutlookチャネルを追加する
> * 更新されたアプリをアプリのサイドロードTeams

このガイドの残りの部分では、以下の手順について説明し、デスクトップと Web の両方でメッセージ拡張機能Outlookプレビュー Windows示します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次の情報が必要です。

 - 開発者Microsoft 365サンドボックス テナント
 - ターゲットリリースに登録 *Office 365サンドボックス テナント*
 - ベータ 版チャネルからOfficeアプリをインストールしたテストMicrosoft 365 Apps *環境*
 - Visual Studio Code (プレビュー) Teams Toolkit (省略可能)

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="prepare-your-messaging-extension-for-the-upgrade"></a>アップグレード用にメッセージング拡張機能を準備する

既存のメッセージング拡張機能がある場合は、アプリ マニフェストでアプリ ID をテストおよび更新するために、実稼働プロジェクトのコピーまたはブランチを作成し、新しい識別子 (実稼働アプリ ID とは異なる) を使用します。

このチュートリアルを完了するためにサンプル コードを使用する場合は、Teams メッセージング拡張機能検索サンプルのセットアップ手順に従って[、Microsoft Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)検索ベースのメッセージング拡張機能をすばやく構築します。 または[、TeamsJS SDK v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)プレビュー用に更新された同じ Teams メッセージング拡張機能検索サンプルから開始し、Outlook でメッセージング拡張機能のプレビュー[に進みます](#preview-your-message-extension-in-outlook)。 更新されたサンプルは、開発ビュー サンプル NPM Search Connector Teams Toolkit *内*  >    >  **でも使用できます**。

:::image type="content" source="images/toolkit-search-sample.png" alt-text="NPM 検索コネクタのサンプル (Teams Toolkit":::

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

開発者プレビュー マニフェスト スキーマとマニフェスト[Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview)を使用して、Teams メッセージング拡張機能を Outlook `m365DevPreview` で実行する必要があります。

アプリ マニフェストを更新するには、次の 2 つのオプションがあります。

# <a name="teams-toolkit"></a>[Teams Toolkit](#tab/manifest-teams-toolkit)

1. コマンド パレット *を開きます*。 `Ctrl+Shift+P`
1. コマンドを実行 `Teams: Upgrade Teams manifest to support Outlook and Office apps` し、アプリ マニフェスト ファイルを選択します。 変更は、その場で行います。

# <a name="manual-steps"></a>[手動の手順](#tab/manifest-manual)

アプリ マニフェストTeams開き、次の `$schema` 値 `manifestVersion` を使用して更新します。

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

メッセージング拡張機能アプリTeams Toolkit使用した場合は、このアプリを使用してマニフェスト ファイルの変更を検証し、エラーを特定できます。 コマンド パレットを開き、Teams: マニフェスト ファイルを検証するか、Teams Toolkit の [展開] メニューからオプションを選択します (Visual Studio Code の左側にある Teams アイコン `Ctrl+Shift+P` を探します)。 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit [展開] メニューの [マニフェスト ファイルの検証] オプションを選択します。":::

## <a name="add-an-outlook-channel-for-your-bot"></a>ボットのOutlookチャネルを追加する

このMicrosoft Teamsメッセージング拡張機能は、ホストする Web サービスと、Web サービスのホスト場所を定義するアプリ マニフェストで構成されます。 Web サービスは、ボットに登録されているチャネルを通じて[、ボット フレームワーク SDK](/azure/bot-service/bot-service-overview)メッセージング スキーマとセキュリティで保護されたTeamsを利用します。

ユーザーがメッセージ拡張機能を Outlook操作するには、ボットに Outlookチャネルを追加する必要があります。

1. [Azure portal](https://portal.azure.com) (以前に[登録した場合は](https://dev.botframework.com)ボット フレームワーク ポータル) から、ボット リソースに移動します。

1. [*チャネル設定]* を **選択します**。

1. [メッセージ **]** Outlookをクリックし、[**メッセージ** の拡張機能] タブを選択し、[保存] を **クリックします**。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="[Azure ボット Outlook] ウィンドウからボットの [メッセージ拡張機能] チャネルを追加する":::

1. ボットの [チャネルOutlook] ウィンドウに、Microsoft Teamsチャネルが一 **覧表示されます。**

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Azure Bot チャネル ウィンドウで、チャネルMicrosoft TeamsとOutlook一覧":::

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>更新されたメッセージング拡張機能をサーバーにサイドロードTeams

最後の手順は、更新されたメッセージング拡張機能 ([アプリ](/microsoftteams/platform/concepts/build-and-test/apps-package)パッケージ) をアプリ 内にサイドロードMicrosoft Teams。 完了すると、メッセージ作成領域からインストールされている *アプリ* にメッセージング拡張機能が表示されます。

1. zip ファイルTeamsアプリケーション (マニフェストアイコンとアプリ[アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) をパッケージ化します。 アプリの作成Teams Toolkit使用した場合は、アプリの [展開] メニューの **[Zip** Teams メタデータ パッケージ]オプションを使用して簡単にTeams Toolkit。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="[zip Teams メタデータ パッケージ] オプションは、Teams Toolkitの拡張機能Visual Studio Code":::

1. サンドボックス テナント アカウントを使用して Teams にログインし、ユーザー プロファイルの省略記号 (**...**) メニューをクリックして [約] を開き、[開発者プレビュー] オプションがオンに切り替わるのを確認して、パブリック *Developer Preview* 上にあるか確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="[省略Teams] メニューの [概要] を開き、[Developer Preview] オプションがオンに設定されているのを確認します。":::

1. [アプリ *] ウィンドウを* 開き、[カスタム アプリ **アップロード] を** クリックし、[自分または **アップロード] をクリックします**。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="[アップロード] ウィンドウの [カスタム アプリTeams] ボタンをクリックします。":::

1. アプリ パッケージを選択し、[開く] を *クリックします*。

メッセージをサイドロードTeams、メッセージング拡張機能を使用して、Outlook on the web。

## <a name="preview-your-message-extension-in-outlook"></a>メッセージ拡張機能をプレビュー Outlook

これで、デスクトップと Web 上で実行中のメッセージング拡張機能OutlookテストWindows準備ができました。 更新されたメッセージング拡張機能は、メッセージング拡張機能の完全な機能サポートを使用して[](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)Teams で引き続き実行されますが、Outlook が有効なエクスペリエンスのこの早期プレビューでは、次の点に注意する必要があります。

* メッセージ内のメッセージングOutlookは、メール作成コンテキストに [*制限* されます](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)。 メッセージ拡張機能にTeamsコンテキストがマニフェストに含まれる場合でも、現在のプレビューはメール構成 ( ) オプション `commandBox` に `compose` 制限されます。 [検索] ボックスに表示されるグローバル Outlook *の呼* び出しはサポートされていません。
* [アクション ベースのメッセージング拡張機能コマンド](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)は、Outlook。 アプリに検索ベースとアクション ベースの両方のコマンドがある場合は、Outlookに表示されますが、アクション メニューは使用できません。
* [シングル サインオンのサイレント認証](/microsoftteams/platform/messaging-extensions/how-to/enable-sso-auth-me)は、ユーザーのメッセージング拡張機能ではOutlook。
* メールに 5 つ以上 [のアダプティブ](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) カードを挿入する機能はサポートされていません。アダプティブ カード v1.4 以降はサポートされていません。
* [タイプ 、、、](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) の `messageBack` カード アクションは `imBack` `invoke` `signin` 、挿入されたカードではサポートされていません。 サポートは:クリック `openURL` 時に、ユーザーは新しいタブで指定された URL にリダイレクトされます。

メッセージング拡張機能をテストすると[、Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md)オブジェクトの[channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id)によってボット要求のソース (Teams と Outlook から発信元) を識別できます。 ユーザーがクエリを実行すると、サービスは標準の Bot Framework オブジェクトを受け取 `Activity` ります。 Activity オブジェクトのプロパティの 1 つは、ボット要求の発生元に応じて、または 、の値を持つ `channelId` `msteams` `outlook` プロパティです。 詳細については、「  [検索ベースのメッセージング拡張機能 SDK」を参照してください](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)。

### <a name="outlook"></a>Outlook

デスクトップ上で実行中のアプリOutlookプレビュー Windows、テスト テナントOutlook資格情報を使用してログインしているアプリを開きます。 [新しい **メール] をクリックします**。 上部リボン **の [その他の** アプリ] フライアウト メニューを開きます。 メッセージ拡張機能が表示されます。 そこから呼び出して、メッセージを作成する場合と同じ方法で使用Teams。

### <a name="outlook-on-the-web"></a>Outlook on the web

テスト テナントで実行中のアプリOutlook on the webするには、テスト テナント[outlook.com](https://www.outlook.com)を使用してログインします。 [新しいメッセージ **] をクリックします**。 コンポジション **ウィンドウの下部** にある [その他のアプリ] フライアウト メニューを開きます。 メッセージ拡張機能が表示されます。 そこから呼び出して、メッセージを作成する場合と同じ方法で使用Teams。

## <a name="next-steps"></a>次の手順

Outlookが有効Teamsメッセージング拡張機能はプレビュー中であり、実稼働環境での使用はサポートされていません。 テスト目的でユーザーをプレビューするために、Outlook有効なメッセージング拡張機能を配布する方法を次に示します。

### <a name="single-tenant-distribution"></a>単一テナントの配布

OutlookおよびOffice有効な個人用タブは、次の 3 つの方法の 1 つで、テスト (または実稼働) テナント全体でプレビュー対象ユーザーに配布できます。

#### <a name="teams-client"></a>Teams クライアント

[アプリ *] メニューの*[アプリの *管理]*  >  **を選択して、組織にアプリを送信します**。これには、IT 管理者からの承認が必要です。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理センター

管理者はTeams、組織のテナントのアプリ パッケージをアップロードして事前インストールできます https://admin.teams.microsoft.com/ 。 詳細[についてはアップロード管理センターのカスタム アプリMicrosoft Teamsを参照](/MicrosoftTeams/upload-custom-apps)してください。

#### <a name="microsoft-admin-center"></a>Microsoft 管理センター

グローバル管理者は、アプリ パッケージをアップロードして事前インストールできます https://admin.microsoft.com/ 。 詳細[については、「統合アプリ ポータルMicrosoft 365 Appsパートナーによるテストと展開」を](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)参照してください。

### <a name="multi-tenant-distribution"></a>マルチテナント配布

Microsoft AppSource への配布は、この初期の開発者向けプレビューで、Outlookが有効Teamsサポートされていません。
