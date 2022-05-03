---
title: Microsoft 365 間で Teams メッセージ拡張機能を拡張する
description: 検索ベースのTeams メッセージ拡張機能を更新してOutlookで実行する方法を次に示します。
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 7e3a0d772367952c1726648fce2f10e1d8b885b2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111375"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Microsoft 365 間で Teams メッセージ拡張機能を拡張する

> [!NOTE]
> *Teams メッセージ拡張機能を Microsoft 365 全体に拡張する* ことは、現在、[パブリック開発者向けプレビュー](../resources/dev-preview/developer-preview-intro.md)でのみ使用できます。 プレビューに含まれている機能は完全でないため、一般公開前に変更される場合があります。 これらは、テストと調査のみを目的としています。 実稼働アプリケーションでは使用しないでください。

検索ベースの[メッセージ拡張機能](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)を使用すると、ユーザーは外部システムを検索し、Microsoft Teams クライアントのメッセージ作成領域で結果を共有できます。 [Teams アプリを Microsoft 365 (プレビュー) に拡張](overview.md)することで、検索ベースのTeams メッセージ拡張機能を Windows デスクトップと Web エクスペリエンスの Outlook に追加できるようになりました。

検索ベースの Teams メッセージ拡張機能を更新して Outlook を実行するプロセスには、次の手順が含まれます。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新する
> * ボットの Outlook チャネルを追加する
> * Teams でアプリをサイドロードする

このガイドの残りの部分では、これらの手順について説明し、Windows デスクトップと Web の両方の Outlook でメッセージ拡張機能をプレビューする方法について説明します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次のものが必要です。

* Microsoft 365 開発者プログラム サンドボックス テナント
* *[Office 365 対象指定リリース]* に登録されているサンドボックス テナント
* Microsoft 365 Apps *ベータ チャネル* からインストールされた Office アプリを含むテスト環境
* Teams Toolkit (プレビュー) 拡張機能を使用したコードの Microsoft Visual Studio (省略可能)

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>アップグレードのメッセージ拡張機能を準備する

既存のメッセージ拡張機能がある場合は、テスト用の運用プロジェクトのコピーまたはブランチを作成し、アプリ マニフェストでアプリ ID を更新して、(運用環境のアプリ ID とは異なる) 新しい識別子を使用します。

このチュートリアルを完了するためにサンプル コードを使用する場合は、[Teams メッセージ拡張機能検索サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)のセットアップ手順に従って、Microsoft Teams 検索ベースのメッセージ拡張機能をすばやく構築します。 または、[TeamsJS SDK v2 プレビュー用に更新された同じ Teams メッセージ拡張機能検索サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)から開始し、[Outlook でメッセージ拡張機能のプレビュー](#preview-your-message-extension-in-outlook)に進むことができます。 更新されたサンプルは、以下の場所にある Teams Toolkit 拡張機能内でも利用できます: *[開発]* > *[サンプルを表示]* > **[NPM検索コネクタ]**。

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Teams Toolkit の NPM Search Connector サンプル":::

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

[Teams 開発者プレビュー マニフェスト](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) スキーマと `m365DevPreview` マニフェスト バージョンを使用して、Teams メッセージ拡張機能を Outlook で実行できるようにする必要があります。

アプリ マニフェストを更新するには、次の 2 つのオプションがあります。

# <a name="teams-toolkit"></a>[Teams ツールキット](#tab/manifest-teams-toolkit)

1. *コマンド パレット* を開きます: `Ctrl+Shift+P`
1. `Teams: Upgrade Teams manifest to support Outlook and Office apps` コマンドを実行し、アプリ マニフェスト ファイルを選択します。 変更が行われます。

# <a name="manual-steps"></a>[手動の手順](#tab/manifest-manual)

Teams アプリ マニフェストを開き、`$schema` と `manifestVersion` を次の値で更新します。

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Teams Toolkit を使用してメッセージ拡張アプリを作成した場合は、それを使用してマニフェスト ファイルへの変更を検証し、エラーを特定できます。 コマンド パレットを開いてTeams を`Ctrl+Shift+P`見つけます **。マニフェスト ファイル** を検証するか、Teams ツールキットの [配置] メニューからオプションを選択します (Visual Studio Code の左側にある Teams アイコンを探します)。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams ツールキット [配置] メニューの [マニフェスト ファイルの検証] オプション":::

## <a name="add-an-outlook-channel-for-your-bot"></a>ボットの Outlook チャネルを追加する

Microsoft Teams では、メッセージ拡張機能は、ホストする Web サービスと、Web サービスがホストされる場所を定義するアプリ マニフェストで構成されます。 Web サービスは、ボットに登録された Teams チャネルを介して[ボット フレームワーク SDK](/azure/bot-service/bot-service-overview) メッセージング スキーマと安全な通信プロトコルを利用します。

ユーザーが Outlook からメッセージ拡張機能を操作するには、Outlook チャネルをボットに追加する必要があります。

1. [Microsoft Azure ポータル](https://portal.azure.com) (以前に登録した場合は [Bot Framework ポータル](https://dev.botframework.com)) から、ボット リソースに移動します。

1. *[設定]* から **[チャネル]** を選択します。

1. **Outlook** をクリックし、**[メッセージ拡張機能]** タブを選択して、**[保存]** をクリックします。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="zure ボット チャネル ウィンドウからボットの Outlook 'Message Extensions' チャネルを追加する":::

1. Outlook チャネルがボットの **[チャネル]** ウィンドウに Microsoft Teams と共に表示されていることを確認します。

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Microsoft Teams と Outlook チャネルの両方を一覧表示する Azure ボット チャネル ウィンドウ":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>SSO の Microsoft Azure Active Directory (Azure AD) アプリの登録を更新する

> [!NOTE]
> [Teams メッセージ拡張機能の検索サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)を使用している場合は、シナリオに Azure Active Directory (AAD) シングル サインオン認証が含まれていないため、この手順をスキップできます。

メッセージ拡張機能の Azure Active Directory シングル サインオン (SSO) は、Outlook でも [Teams と同じように](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots)機能しますが、テナントのアプリ登録ポータルでボットの Azure AD *アプリ登録* に複数のクライアント アプリケーション識別子を追加する必要があります。

1. Azure 管理者アカウントを使用して、[Azure portal](https://portal.azure.com) にサインインします。
1. **[アプリ登録]** を開きます。
1. アプリケーションの名前を選択して、アプリの登録を開きます。
1. *[管理]* の下の **[API の公開]** を選択します。

**[承認されたクライアント アプリケーション]** セクションで、次のすべての `Client Id` 値が一覧表示されていることを確認します。

|Microsoft 365 クライアント アプリケーション | クライアント ID |
|--|--|
|Teams デスクトップとモバイル |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>更新されたメッセージ拡張機能を Teams でサイドロードする

最後の手順は、更新されたメッセージ拡張機能 ([アプリ パッケージ](/microsoftteams/platform/concepts/build-and-test/apps-package)) をMicrosoft Teamsにサイドロードすることです。 完了すると、メッセージ拡張機能がインストールされている *[アプリ]* に作成メッセージ領域から表示されます。

1. Teams アプリケーション (マニフェスト アイコンとアプリ [アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) を zip ファイルにパッケージ化します。 Teams Toolkit を使用してアプリを作成した場合は、Teams Toolkit の *[展開]* メニューの **[Zip Teams メタデータ パッケージ]** オプションを使用して簡単に行うことができます。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Visual Studio Code 用のTeams ツールキット拡張機能の 'Zip Teams メタデータ パッケージ' オプション":::

1. サンドボックス テナント アカウントを使用して Teams にログインし、ユーザー プロファイルの省略記号 (**...**) メニューをクリックして開くことにより、*[開発者向けパブリック プレビュー]* にいることを確認します。 **[詳細情報]** をクリックして、*[開発者向けプレビュー]* オプションがオンになっていることを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams の省略記号メニューから、[バージョン情報] を開き、[開発者プレビュー] オプションがオンになっていることを確認する":::

1. *[アプリ]* ウィンドウを開き、**[カスタム アプリのアップロード]** をクリックし、**自分または自分のチームにアップロード** します。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams [アプリ] ウィンドウの [カスタム アプリのアップロード] ボタン":::

1. アプリ パッケージを選択し、*[開く]* をクリックします。

Teams を介してサイドロードされると、メッセージ拡張機能が Web 上の Outlook で利用できるようになります。

## <a name="preview-your-message-extension-in-outlook"></a>Outlook でメッセージ拡張機能をプレビューする

これで、Windows デスクトップおよび Web 上の Outlook で実行されているメッセージ拡張機能をテストする準備が整いました。 更新されたメッセージ拡張機能は引き続き Teams で実行され、[メッセージ拡張機能の完全な機能サポート](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)が提供されますが、この Outlook 対応エクスペリエンスの早期プレビューでは、次の点に注意する必要があります。

* Outlook のメッセージ拡張機能は、メール [*作成* コンテキスト](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)に限定されます。 Teams メッセージ拡張機能のマニフェストに *コンテキスト* として `commandBox` が含まれている場合でも、現在のプレビューはメール構成 (`compose`) オプションに制限されています。 グローバル Outlook *[検索]* ボックスからのメッセージ拡張機能の呼び出しはサポートされていません。
* [[アクション ベースのメッセージ拡張]](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) コマンドは、Outlook ではサポートされていません。 アプリに検索ベースのコマンドとアクション ベースのコマンドの両方がある場合は、Outlook に表示されますが、アクション メニューは使用できません。
* メールへの 5 つ以上の [アダプティブ カード](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) の挿入はサポートされていません。アダプティブ カード v1.4 以降はサポートされていません。
* タイプ`messageBack`、`imBack`、`invoke`、および `signin` の [[カード アクション]](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) は、挿入されたカードではサポートされていません。 サポートは `openURL` に限定されます: クリックすると、ユーザーは新しいタブで指定された URL にリダイレクトされます。

メッセージ拡張機能をテストするときに、[[アクティビティ]](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) オブジェクトの [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) によってボット要求のソース (Teams と Outlook から発信) を識別できます。 ユーザーがクエリを実行すると、サービスは標準の Bot Framework `Activity` オブジェクトを受け取ります。 Activity オブジェクトのプロパティの 1 つは `channelId` であり、ボット リクエストの発信元に応じて `msteams` または `outlook` の値になります。 詳細については、「[検索ベースのメッセージ拡張 SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)」を参照してください。

### <a name="outlook-on-the-web"></a>Outlook on the web

Outlook on the web で実行されているアプリをプレビューするには:

1. テスト テナントの資格情報を使用して [outlook.com](https://www.outlook.com) にログインします。
1. [**新規メッセージ**] を選択します。
1. コンポジション ウィンドウの下部にある **[その他のアプリ]** ポップアップ メニューを開きます。

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="メール構成ウィンドウの下部にある [その他のアプリ] メニューをクリックして、メッセージ拡張機能を使用します":::

メッセージ拡張機能が一覧表示されます。 そこからそれを呼び出し、Teams でメッセージを作成する場合と同じように使用できます。

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> [Microsoft Teams - Microsoft 365 開発者向けブログ](https://devblogs.microsoft.com/microsoft365dev/)の最新の更新プログラムを参照して、Teams 個人用アプリのデスクトップ サポート Windows Outlook がテスト テナントで利用できるかどうかを確認してください。

デスクトップ上の Outlook で実行されているアプリ Windows プレビューするには:

1. テスト テナントの資格情報を使用してログインした Outlook を起動します。 1. **[新しいメール]** をクリックします。
1. 上部のリボンの **[その他のアプリ]** ポップアップ メニューを開きます。

メッセージ拡張機能が一覧表示されます。 そこからそれを呼び出し、Teams でメッセージを作成する場合と同じように使用できます。

## <a name="next-steps"></a>次の手順

Outlook 対応の Teams メッセージ拡張機能はプレビュー段階にあり、運用環境での使用ではサポートされていません。 テスト目的で Outlook 対応のメッセージ拡張機能をプレビュー対象ユーザーに配布する方法を次に示します。

### <a name="single-tenant-distribution"></a>シングルテナント配布

Outlook および Office 対応の個人用タブは、次の 3 つの方法のいずれかで、テスト (または運用環境) テナント全体でプレビュー対象ユーザーに配布できます。

#### <a name="teams-client"></a>Teams クライアント

*[アプリ]* メニューから、*[アプリの管理]* > **[アプリを組織に送信]** の順に選択します。 これには、IT 管理者の承認が必要です。

#### <a name="microsoft-teams-admin-center"></a>‎Microsoft Teams 管理センター

Teams 管理者は、組織のテナント用のアプリ パッケージを [[Teams admin]](https://admin.teams.microsoft.com/) からアップロードしてプレインストールできます。 詳細については、「[Microsoft Teams 管理センターでカスタム アプリをアップロードする](/MicrosoftTeams/upload-custom-apps)」を参照してください。

#### <a name="microsoft-admin-center"></a>Microsoft Admin Center

グローバル管理者は、[[Microsoft 管理者]](https://admin.microsoft.com/)からアプリ パッケージをアップロードして事前インストールできます。詳細については、「[統合アプリ ポータルのパートナーによる Microsoft 365 Apps のテストとデプロイ](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)」に関する説明を参照してください。

### <a name="multitenant-distribution"></a>マルチテナント分布

Outlook 対応の Teams メッセージ拡張機能のこの初期の開発者プレビューでは、Microsoft AppSourc eへの配布はまだサポートされていません。
