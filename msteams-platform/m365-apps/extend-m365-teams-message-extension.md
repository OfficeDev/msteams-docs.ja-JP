---
title: 複数のTeamsメッセージング拡張機能を拡張Microsoft 365
description: 検索ベースのメッセージング拡張機能を更新して、Teamsで実行する方法をOutlook
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: d2369d5a07652055a9474be586470f906ed3de5b
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2022
ms.locfileid: "63727528"
---
# <a name="extend-a-teams-messaging-extension-across-microsoft-365"></a>複数のTeamsメッセージング拡張機能を拡張Microsoft 365

> [!NOTE]
> *現在、Teamsメッセージング拡張機能を拡張Microsoft 365* パブリック開発者向け [プレビューでのみ使用できます](../resources/dev-preview/developer-preview-intro.md)。 プレビューに含まれている機能は完全でないため、一般公開前に変更される場合があります。 これらは、テストと調査のみを目的としています。 実稼働アプリケーションでは使用しないでください。

検索ベースの[メッセージング拡張機能を使用](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)すると、ユーザーは外部システムを検索し、クライアントの作成メッセージ領域を通じて結果をMicrosoft Teamsできます。 [Microsoft 365 (プレビュー)](overview.md) 全体で Teams アプリを拡張することで、Teams デスクトップと web エクスペリエンスの検索ベースの Teams メッセージング拡張機能を Outlook Windows に追加できます。

検索ベースのメッセージング拡張機能を更新してTeams実行するプロセスにはOutlook手順が含まれます。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新する
> * ボットのOutlookチャネルを追加する
> * 更新されたアプリをアプリにサイドロードTeams

このガイドの残りの部分では、以下の手順について説明し、デスクトップと Web の両方でメッセージング拡張機能Outlookプレビュー Windows示します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次の情報が必要です。

* 開発者Microsoft 365サンドボックス テナント
* ターゲットリリースに登録 *Office 365サンドボックス テナント*
* ベータ 版チャネルからOfficeアプリをインストールしたテストMicrosoft 365 Apps *環境*
* Microsoft Visual Studio (Preview) 拡張子Teams Toolkitコード (省略可能)

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="prepare-your-messaging-extension-for-the-upgrade"></a>アップグレード用にメッセージング拡張機能を準備する

既存のメッセージング拡張機能がある場合は、アプリ マニフェストでアプリ ID をテストおよび更新するために、実稼働プロジェクトのコピーまたはブランチを作成し、新しい識別子 (実稼働アプリ ID とは異なる) を使用します。

このチュートリアルを完了するためにサンプル コードを使用する場合は、[Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) メッセージング拡張機能検索サンプルのセットアップ手順に従って、Microsoft Teams 検索ベースのメッセージング拡張機能をすばやく構築します。 または、[TeamsJS SDK v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365) プレビュー用に更新された同じ Teams メッセージング拡張機能検索サンプルから開始し、Outlook でメッセージング拡張機能のプレビュー[に進みます](#preview-your-messaging-extension-in-outlook)。 更新されたサンプルは、拡張機能 (*DevelopmentView* >  *samplesNPM* >  **Search Connector) Teams Toolkit内でも使用できます**。

:::image type="content" source="images/toolkit-search-sample.png" alt-text="NPM 検索コネクタのサンプル (Teams Toolkit":::

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

開発者プレビュー マニフェスト スキーマとマニフェスト [Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview)`m365DevPreview`を使用して、Teams メッセージング拡張機能を Outlook で実行する必要があります。

アプリ マニフェストを更新するには、次の 2 つのオプションがあります。

# <a name="teams-toolkit"></a>[Teams ツールキット](#tab/manifest-teams-toolkit)

1. コマンド パレット *を開きます*。 `Ctrl+Shift+P`
1. コマンドを実行 `Teams: Upgrade Teams manifest to support Outlook and Office apps` し、アプリ マニフェスト ファイルを選択します。 変更は、その場で行います。

# <a name="manual-steps"></a>[手動の手順](#tab/manifest-manual)

アプリ マニフェストTeams開き、次の値`$schema``manifestVersion`を使用して更新します。

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

メッセージング拡張機能アプリTeams Toolkit使用した場合は、このアプリを使用してマニフェスト ファイルの変更を検証し、エラーを特定できます。 `Ctrl+Shift+P`コマンド パレットを開き、[**Teams:** マニフェスト ファイルの検証] を見つけるか、Teams Toolkit の [展開] メニューからオプションを選択します (Visual Studio Code の左側にある Teams アイコンを探します)。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit [展開] メニューの [マニフェスト ファイルの検証] オプションを選択します。":::

## <a name="add-an-outlook-channel-for-your-bot"></a>ボットのOutlookチャネルを追加する

このMicrosoft Teamsメッセージング拡張機能は、ホストする Web サービスと、Web サービスのホスト場所を定義するアプリ マニフェストで構成されます。 Web サービスは、ボットに登録されているチャネルを通じて、[ボット フレームワーク SDK](/azure/bot-service/bot-service-overview) メッセージング スキーマとセキュリティで保護されたTeamsを利用します。

ユーザーがメッセージ拡張機能を Outlook操作するには、ボットに Outlookチャネルを追加する必要があります。

1. ポータル[Microsoft Azure (](https://portal.azure.com)以前に登録した場合は [Bot Framework](https://dev.botframework.com) ポータル) から、ボット リソースに移動します。

1. [*チャネル設定*] を **選択します**。

1. [メッセージの表示 **Outlook** をクリックし、[**メッセージ** の拡張機能] タブを選択し、[保存] を **クリックします**。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="[Azure ボット Outlook] ウィンドウからボットの [メッセージ拡張機能] チャネルを追加する":::

1. ボットの [チャネルOutlook] ウィンドウに、Microsoft Teamsチャネルが一覧表示されているのを **確認** します。

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Azure Bot チャネル ウィンドウで、チャネルMicrosoft TeamsとOutlook一覧":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>SSO Microsoft Azure Active Directory (Azure AD) アプリ登録を更新する

> [!NOTE]
> [Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) メッセージング拡張機能検索サンプルを使用している場合は、Azure Active Directory (AAD) シングル Sign-On 認証を使用しない場合は、この手順を省略できます。

Azure Active Directory メッセージング拡張機能のシングル サインオン (SSO) は、Outlook [Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots) と同じように動作しますが、テナントのアプリ登録ポータルでボットの Azure AD アプリ登録にいくつかのクライアント アプリケーション識別子を追加する必要があります。

1. サンドボックス テナント アカウント [を使用して Azure portal](https://portal.azure.com) にサインインします。
1. アプリ **の登録を開きます**。
1. アプリケーションの名前を選択して、アプリ登録を開きます。
1. [API  **の公開] ([管理]** の下) を *選択します*。

[承認済 **みクライアント アプリケーション] セクション** で、次のすべての値が `Client Id` 一覧表示されます。

|Microsoft 365 クライアント アプリケーション | クライアント ID |
|--|--|
|Teamsとモバイル |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-00000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>更新されたメッセージング拡張機能をサーバーにサイドロードTeams

最後の手順は、更新されたメッセージング拡張機能 ([アプリ](/microsoftteams/platform/concepts/build-and-test/apps-package) パッケージ) をアプリ 内にサイドロードMicrosoft Teams。 完了すると、メッセージ作成領域からインストールされている *アプリ* にメッセージング拡張機能が表示されます。

1. zip ファイルTeamsアプリケーション (マニフェストアイコンとアプリ [アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) をパッケージ化します。 アプリの作成Teams Toolkit使用した場合は、アプリの [展開] メニューの [Zip Teams メタデータ パッケージ] **オプション** を使用して簡単にTeams Toolkit。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="[zip Teams メタデータ パッケージ] オプションは、Teams Toolkitの拡張機能Visual Studio Code":::

1. サンドボックス テナント アカウントを使用して Teams にログインし、ユーザー プロファイルで省略記号 (**.....**) メニューをクリックして [開発者プレビュー] オプションがオンに切り替わるか確認して、パブリック *Developer Preview* 上にあるか確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="[省略Teams] メニューの [概要] を開き、[Developer Preview] オプションがオンになっています。":::

1. [アプリ *] ウィンドウを* 開き、[カスタム アプリ **アップロードを** クリックし、自分アップロード **チームにアクセスします**。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="[アップロード] ウィンドウの [カスタム アプリTeams] ボタンをクリックします。":::

1. アプリ パッケージを選択し、[開く] を *クリックします*。

メッセージをサイドロードTeams、メッセージング拡張機能を使用して、Outlook on the web。

## <a name="preview-your-messaging-extension-in-outlook"></a>メッセージ拡張機能をプレビュー Outlook

これで、デスクトップと Web 上で実行中のメッセージング拡張機能OutlookテストWindows準備ができました。 更新されたメッセージング拡張機能は、メッセージング拡張機能の完全な機能サポートを備え、Teams [](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)で引き続き実行しますが、Outlook が有効なエクスペリエンスのこの早期プレビューでは、次の点に注意する必要があります。

* メッセージの拡張機能はOutlook作成コンテキストに [*制限* されます](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)。 メッセージ拡張機能にTeamsコンテキスト`commandBox`がマニフェストに含まれる場合でも、現在のプレビューはメール構成 (`compose`) オプションに制限されます。 [検索] ボックスからメッセージング拡張機能Outlook *呼* び出す操作はサポートされていません。
* [アクション ベースのメッセージング拡張機能コマンド](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)は、この機能ではOutlook。 アプリに検索とアクション ベースの両方のコマンドがある場合、アプリは Outlook表示されますが、アクション メニューは使用できません。
* メールに 5 つ以上 [のアダプティブ](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) カードを挿入する機能はサポートされていません。アダプティブ カード v1.4 以降はサポートされていません。
* [タイプ 、](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)、、`messageBack``imBack`のカード `invoke`アクション`signin`は、挿入されたカードではサポートされていません。 サポートは:クリック `openURL`時に、ユーザーは新しいタブで指定された URL にリダイレクトされます。

メッセージング拡張機能をテストする場合は、[Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) オブジェクトの [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) によってボット要求のソース (Teams と Outlook から発信元) を識別できます。 ユーザーがクエリを実行すると、サービスは標準の Bot Framework オブジェクトを受け取 `Activity` ります。 Activity `channelId``msteams` `outlook`オブジェクトのプロパティの 1 つは、ボット要求の発生元に応じて、または 、の値を持つプロパティです。 詳細については、「  [検索ベースのメッセージング拡張機能 SDK」を参照してください](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)。

### <a name="outlook-on-the-web"></a>Outlook on the web

アプリで実行中のアプリをプレビューするには、次Outlook on the web。

1. テスト テナントの [資格情報 outlook.com](https://www.outlook.com) を使用して、ログインしてログインします。
1. [新 **しいメッセージ] を選択します**。
1. コン **ポジション ウィンドウの** 下部にある [その他のアプリ] フライアウト メニューを開きます。

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="メッセージ拡張機能を使用するには、メール構成ウィンドウの下部にある [その他のアプリ] メニューをクリックします。":::

メッセージング拡張機能が表示されます。 そこから呼び出して、メッセージを作成する場合と同じ方法で使用Teams。

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365 開発者](https://devblogs.microsoft.com/microsoft365dev/)向けブログの最新の更新プログラムを参照して、Windows デスクトップ の Outlook で Teams 個人用アプリがテスト テナントで利用できるのか確認してください。

デスクトップで実行中のアプリOutlookプレビューするにはWindows:

1. テスト Outlook資格情報を使用してログインしているユーザーを起動します。 1. [新しい **メール] をクリックします**。
1. 上部リボン **の [その他の** アプリ] フライアウト メニューを開きます。

メッセージング拡張機能が表示されます。 そこから呼び出して、メッセージを作成する場合と同じ方法で使用Teams。

## <a name="next-steps"></a>次の手順

Outlookが有効Teamsメッセージング拡張機能はプレビュー中であり、実稼働環境での使用はサポートされていません。 テスト目的でユーザーをプレビューするために、Outlook有効なメッセージング拡張機能を配布する方法を次に示します。

### <a name="single-tenant-distribution"></a>単一テナントの配布

Outlook有効Office個人用タブは、次の 3 つの方法のいずれかを使用して、テスト (または実稼働) テナント全体でプレビュー対象ユーザーに配布できます。

#### <a name="teams-client"></a>Teams クライアント

[アプリ *] メニューの* [アプリ *の管理* > **] を選択して、アプリを組織に送信します**。これには、IT 管理者からの承認が必要です。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理センター

管理者Teams、組織のテナントのアプリ パッケージを管理者からアップロードして[Teamsできます](https://admin.teams.microsoft.com/)。詳細[についてはアップロード管理センターのカスタム アプリMicrosoft Teamsを参照](/MicrosoftTeams/upload-custom-apps)してください。

#### <a name="microsoft-admin-center"></a>Microsoft 管理センター

グローバル管理者は、Microsoft 管理者からアプリ パッケージをアップロードして事前インストール[できます](https://admin.microsoft.com/)。詳細[については、「統合アプリ ポータルMicrosoft 365 Appsパートナーによるテストと展開」を](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)参照してください。

### <a name="multitenant-distribution"></a>マルチテナント配布

Microsoft AppSource への配布は、この初期の開発者向けプレビューで、Outlookメッセージング拡張機能Teamsサポートされていません。
