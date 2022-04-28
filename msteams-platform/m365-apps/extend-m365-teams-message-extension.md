---
title: Microsoft 365間でTeamsメッセージ拡張機能を拡張する
description: 検索ベースのTeams メッセージ拡張機能を更新してOutlookで実行する方法を次に示します。
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 3bab70d85d071763ffbbae7cb1dae11534d0e812
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104540"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Microsoft 365間でTeamsメッセージ拡張機能を拡張する

> [!NOTE]
> *Teamsメッセージ拡張機能をMicrosoft 365全体に拡張* することは、現在、[パブリック開発者向けプレビュー](../resources/dev-preview/developer-preview-intro.md)でのみ使用できます。 プレビューに含まれている機能は完全でないため、一般公開前に変更される場合があります。 これらは、テストと調査のみを目的としています。 実稼働アプリケーションでは使用しないでください。

検索ベースの[メッセージ拡張機能](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)を使用すると、ユーザーは外部システムを検索し、Microsoft Teams クライアントのメッセージ作成領域で結果を共有できます。 [Teams アプリをMicrosoft 365 (プレビュー) に拡張](overview.md)することで、検索ベースのTeams メッセージ拡張機能をWindowsデスクトップと Web エクスペリエンスのOutlookに追加できるようになりました。

検索ベースのTeams メッセージ拡張機能を更新してOutlookを実行するプロセスには、次の手順が含まれます。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新する
> * ボットのOutlook チャネルを追加する
> * 更新されたアプリをTeamsにサイドロードする

このガイドの残りの部分では、これらの手順について説明し、Windowsデスクトップと Web の両方のOutlookでメッセージ拡張機能をプレビューする方法について説明します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次のものが必要です。

* Microsoft 365開発者プログラムサンドボックス テナント
* *Office 365対象のリリース* に登録されているサンドボックス テナント
* Microsoft 365 Apps *ベータ チャネル* からインストールされたOffice アプリを含むテスト環境
* Teams Toolkit (プレビュー) 拡張機能を使用したコードのMicrosoft Visual Studio (省略可能)

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>アップグレードのメッセージ拡張機能を準備する

既存のメッセージ拡張機能がある場合は、テスト用の運用プロジェクトのコピーまたはブランチを作成し、アプリ マニフェストでアプリ ID を更新して、(運用環境のアプリ ID とは異なる) 新しい識別子を使用します。

このチュートリアルを完了するためにサンプル コードを使用する場合は、[Teamsメッセージ拡張機能検索サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)のセットアップ手順に従って、Microsoft Teams検索ベースのメッセージ拡張機能をすばやく構築します。 または、[TeamsJS SDK v2 プレビュー用に更新された同じTeamsメッセージ拡張機能検索サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)から開始し、[Outlookでメッセージ拡張機能のプレビューに](#preview-your-message-extension-in-outlook)進むことができます。 更新されたサンプルは、*Teams Toolkit拡張機能である DevelopmentView* >  *samplesNPM* >  **Search Connector** 内でも使用できます。

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Teams Toolkitの NPM Search Connector サンプル":::

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

[Teams開発者プレビュー マニフェスト](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) スキーマとマニフェスト バージョンを`m365DevPreview`使用して、Teams メッセージ拡張機能をOutlookで実行できるようにする必要があります。

アプリ マニフェストを更新するには、次の 2 つのオプションがあります。

# <a name="teams-toolkit"></a>[Teams ツールキット](#tab/manifest-teams-toolkit)

1. *コマンド パレット* を開きます。`Ctrl+Shift+P`
1. コマンドを `Teams: Upgrade Teams manifest to support Outlook and Office apps` 実行し、アプリ マニフェスト ファイルを選択します。 変更が行われます。

# <a name="manual-steps"></a>[手動の手順](#tab/manifest-manual)

Teams アプリ マニフェストを開き、次の値を`$schema``manifestVersion`使用して更新します。

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Teams Toolkitを使用してメッセージ拡張アプリを作成した場合は、それを使用してマニフェスト ファイルの変更を検証し、エラーを特定できます。 コマンド パレット`Ctrl+Shift+P`を開いてTeamsを見つけます **。マニフェスト ファイルを検証** するか、Teams Toolkitの [配置] メニューからオプションを選択します (Visual Studio Codeの左側にあるTeams アイコンを探します)。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit [配置] メニューの [マニフェスト ファイルの検証] オプション":::

## <a name="add-an-outlook-channel-for-your-bot"></a>ボットのOutlook チャネルを追加する

Microsoft Teamsでは、メッセージ拡張機能は、ホストする Web サービスと、Web サービスがホストされる場所を定義するアプリ マニフェストで構成されます。 Web サービスは [Bot Framework SDK](/azure/bot-service/bot-service-overview) メッセージング スキーマを利用し、ボットに登録されたTeams チャネルを介して通信プロトコルをセキュリティで保護します。

ユーザーがOutlookからメッセージ拡張機能を操作するには、Outlook チャネルをボットに追加する必要があります。

1. [Microsoft Azure ポータル](https://portal.azure.com) (以前に登録した場合は [Bot Framework ポータル](https://dev.botframework.com)) から、ボット リソースに移動します。

1. *設定* から [チャネル] を選択 **します**。

1. **Outlook** をクリックし、[**メッセージ拡張機能**] タブを選択して、[保存] をクリック **します**。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Azure Bot Channels ペインからボットのOutlook 'Message Extensions' チャネルを追加する":::

1. Outlook チャネルがボットの [**チャネル**] ウィンドウにMicrosoft Teamsと共に表示されていることを確認します。

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Microsoft TeamsチャネルとOutlook チャネルの両方を一覧表示する Azure Bot Channels ペイン":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>SSO のMicrosoft Azure Active Directory (Azure AD) アプリの登録を更新する

> [!NOTE]
> [メッセージ拡張機能検索サンプルTeams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)使用している場合は、シナリオに単一のSign-On認証Azure Active Directory (AAD) が含まれていないので、手順をスキップできます。

メッセージ拡張機能のシングル サインオン (SSO) Azure Active Directoryは、Outlook Teamsの場合と同じように機能しますが、テナントのアプリの登録 *ポータル*[で](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots)ボットのAzure AD アプリ登録にいくつかのクライアント アプリケーション識別子を追加する必要があります。

1. サンドボックス テナント アカウント[を使用してAzure portal](https://portal.azure.com)にサインインします。
1. **アプリの登録** を開きます。
1. アプリケーションの名前を選択して、アプリの登録を開きます。
1. [*管理*] で [**API の公開**] を選択します。

[ **承認済みクライアント アプリケーション** ] セクションで、次 `Client Id` のすべての値が一覧表示されていることを確認します。

|Microsoft 365 クライアント アプリケーション | クライアント ID |
|--|--|
|デスクトップとモバイルのTeams |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>更新されたメッセージ拡張機能をTeamsでサイドロードする

最後の手順は、更新されたメッセージ拡張機能 ([アプリ パッケージ](/microsoftteams/platform/concepts/build-and-test/apps-package)) をMicrosoft Teamsにサイドロードすることです。 完了すると、メッセージ拡張機能がインストールされている *アプリ* に作成メッセージ領域から表示されます。

1. Teams アプリケーション (マニフェストアイコンとアプリ [アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) を zip ファイルにパッケージ化します。 Teams Toolkitを使用してアプリを作成した場合は、Teams Toolkitの *[展開]* メニューの **[Zip Teams メタデータ パッケージ**] オプションを使用して簡単に行うことができます。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Visual Studio CodeのTeams Toolkit拡張機能の 'zip Teamsメタデータ パッケージ' オプション":::

1. サンドボックス テナント アカウントでTeamsにログインし、ユーザー プロファイルの省略記号 (**...**) メニューをクリックし、[**バージョン情報**] を開いて *[開発者プレビュー*] オプションがオンになっていることを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="省略記号Teamsメニューから 、'About' を開き、'Developer Preview' オプションがオンになっていることを確認します":::

1. *[アプリ*] ウィンドウを開き、**カスタム アプリアップロード** クリックし、**自分または自分のチームにアップロード** します。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams [アプリ] ウィンドウの [カスタム アプリのアップロード] ボタン":::

1. アプリ パッケージを選択し、[ *開く*] をクリックします。

Teamsを介してサイドロードされると、メッセージ拡張機能はOutlook on the webで使用できるようになります。

## <a name="preview-your-message-extension-in-outlook"></a>Outlookでメッセージ拡張機能をプレビューする

これで、デスクトップと Web 上のOutlookで実行されているメッセージ拡張機能Windowsテストする準備が整いました。 更新されたメッセージ拡張機能は引き続きTeamsで実行され、メッセージ拡張機能の完全な[機能サポートが提供](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)されますが、このOutlook対応エクスペリエンスの早期プレビューでは、次の点に注意する必要があります。

* Outlookのメッセージ拡張機能は、メール [*作成* コンテキスト](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)に限定されます。 Teamsメッセージ拡張機能がマニフェストのコンテキストとして含まれている`commandBox`場合でも、現在のプレビューはメール構成 (`compose`) オプションに制限されます。 グローバル Outlook *検索* ボックスからのメッセージ拡張機能の呼び出しはサポートされていません。
* [アクション ベースのメッセージ拡張](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)コマンドは、Outlookではサポートされていません。 アプリに検索ベースのコマンドとアクション ベースのコマンドの両方がある場合は、Outlookに表示されますが、アクション メニューは使用できません。
* メールへの 5 つ以上の [アダプティブ カード](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) の挿入はサポートされていません。アダプティブ カード v1.4 以降はサポートされていません。
* [挿入されたカード](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) の種類 `messageBack`、 `imBack`、 `invoke`および `signin` サポートされていないカード アクション。 サポートは次に `openURL`限定されます。クリックすると、ユーザーは新しいタブで指定された URL にリダイレクトされます。

メッセージ拡張機能をテストするときに、[アクティビティ](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) オブジェクトの [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) によってボット要求のソース (TeamsとOutlookから発信) を識別できます。 ユーザーがクエリを実行すると、サービスは標準の Bot Framework `Activity` オブジェクトを受け取ります。 Activity オブジェクト `channelId`のプロパティの 1 つは、ボット要求の `msteams` 発信元に応じて値または `outlook`値を持つプロパティです。 詳細については、「  [検索ベースのメッセージ拡張機能 SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)」を参照してください。

### <a name="outlook-on-the-web"></a>Outlook on the web

Outlook on the webで実行されているアプリをプレビューするには:

1. テスト テナントの資格情報を使用して [outlook.com](https://www.outlook.com) にログインします。
1. [ **新しいメッセージ]** を選択します。
1. コンポジション ウィンドウの下部にある **[その他のアプリ** ] ポップアップ メニューを開きます。

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="メール構成ウィンドウの下部にある [その他のアプリ] メニューをクリックして、メッセージ拡張機能を使用します":::

メッセージ拡張機能が一覧表示されます。 そこからそれを呼び出し、Teamsでメッセージを作成する場合と同じように使用できます。

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365開発者向けブログ](https://devblogs.microsoft.com/microsoft365dev/)の最新の更新プログラムを参照して、Teams個人用アプリのデスクトップ サポートWindows Outlookがテスト テナントで利用できるかどうかを確認してください。

デスクトップ上のOutlookで実行されているアプリWindowsプレビューするには:

1. テスト テナントの資格情報でログインOutlook起動します。 1. [ **新しいメール**] をクリックします。
1. 上部のリボンの **[その他のアプリ** ] ポップアップ メニューを開きます。

メッセージ拡張機能が一覧表示されます。 そこからそれを呼び出し、Teamsでメッセージを作成する場合と同じように使用できます。

## <a name="next-steps"></a>次の手順

Outlook対応のTeams メッセージ拡張機能はプレビュー段階にあり、運用環境での使用ではサポートされていません。 テスト目的でOutlook対応のメッセージ拡張機能をプレビュー対象ユーザーに配布する方法を次に示します。

### <a name="single-tenant-distribution"></a>シングルテナント配布

OutlookおよびOffice対応の個人用タブは、次の 3 つの方法のいずれかで、テスト (または運用環境) テナント全体でプレビュー対象ユーザーに配布できます。

#### <a name="teams-client"></a>Teams クライアント

[*アプリ*] メニューの [*アプリ* > の管理] を選択し、**組織にアプリを提出します**。これには、IT 管理者の承認が必要です。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理センター

Teams管理者は、組織のテナントのアプリ パッケージをアップロードして、管理者から事前にインストール[Teams](https://admin.teams.microsoft.com/)。詳細については[、Microsoft Teams管理センターでカスタム アプリのアップロード](/MicrosoftTeams/upload-custom-apps)を参照してください。

#### <a name="microsoft-admin-center"></a>Microsoft Admin Center

グローバル管理者は、[Microsoft 管理者](https://admin.microsoft.com/)からアプリ パッケージをアップロードして事前インストールできます。詳細については、[統合アプリ ポータルのパートナーによるMicrosoft 365 Appsのテストとデプロイ](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)に関する説明を参照してください。

### <a name="multitenant-distribution"></a>マルチテナント分布

Microsoft AppSource への配布は、Outlook対応のTeams メッセージ拡張機能の初期の開発者向けプレビューではサポートされていません。
