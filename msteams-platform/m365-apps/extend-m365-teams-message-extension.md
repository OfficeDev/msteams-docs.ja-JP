---
title: Microsoft 365 間で Teams メッセージ拡張機能を拡張する
description: Microsoft Teams に加えて、Outlook で実行するように検索ベースのメッセージ拡張機能を更新する方法について説明します。
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 9b153eaaaa4cf3eb59d1a7b34122b569ae0d0d1a
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789943"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Microsoft 365 間で Teams メッセージ拡張機能を拡張する

検索ベースの[メッセージ拡張機能](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)を使用すると、ユーザーは外部システムを検索し、Microsoft Teams クライアントのメッセージ作成領域で結果を共有できます。 Microsoft [365 全体](overview.md)で Teams アプリを拡張することで、運用検索ベースの Teams メッセージ拡張機能を使用して、Outlook for Windows デスクトップおよび outlook.com の対象ユーザーをプレビューできるようになりました。

検索ベースの Teams メッセージ拡張機能を更新するプロセスには、次の手順が含まれます。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新します。
> * ボットの Outlook チャネルを追加します。
> * 更新したアプリを Teams にサイドロードします。

このガイドの残りの部分では、これらの手順について説明し、Outlook for Windows デスクトップと Web でメッセージ拡張機能をプレビューする方法を示します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次のものが必要です。

* Microsoft 365 開発者プログラム サンドボックス テナント。
* サンドボックス テナントの *Office 365 対象指定リリース* への登録。
* Microsoft 365 Apps *ベータ チャネル* からインストールされた Office アプリを含むテスト環境。
* (省略可能) Teams Toolkit 拡張機能を備えた Microsoft Visual Studio Code。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="link-unfurling"></a>リンク展開

検索ベースのメッセージ拡張機能で Teams での[リンク展開](../messaging-extensions/how-to/link-unfurling.md)がサポートされている場合は、このチュートリアルの手順を完了すると、Outlook on the webおよび Windows デスクトップ環境でのリンク展開も有効になります。 以下の [「コード サンプル](#code-sample) 」セクションでは、テスト用の簡単なリンク展開アプリを提供します。

## <a name="prepare-your-message-extension-for-the-upgrade"></a>アップグレードのメッセージ拡張機能を準備する

運用環境に既存のメッセージ拡張機能がある場合は、テスト用のプロジェクトのコピーまたはブランチを作成し、アプリ マニフェストでアプリ ID を更新して、(テスト用の運用アプリ ID とは異なる) 新しい識別子を使用します。

既存の Teams アプリの更新の際に、チュートリアル全体を完了するためにサンプル コードを使用する場合は、[Teams メッセージ拡張機能検索サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)のセットアップ手順に従うと、Microsoft Teams 検索ベースのメッセージ拡張機能をすばやく構築できます。

あるいは、次のセクションで既製の Outlook 対応アプリを使用し、このチュートリアルの [*アプリ マニフェストの更新*](#update-the-app-manifest)部分をスキップすることもできます。

### <a name="quickstart"></a>クイックスタート

Outlook で実行が既に有効になっている[サンプル メッセージ拡張機能](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365)から開始するには、Visual Studio Code 用の Teams Toolkit 拡張機能を使用します。

1. Visual Studio Code から、コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Create a new Teams app`」と入力します。
1. **[新しい Teams アプリを作成]** オプションを選択します。
1. **検索ベースのメッセージ拡張機能** を選択し、最新の Teams アプリ マニフェスト (バージョン`1.13`) を使用して、Teams メッセージ拡張機能用のサンプル コードをダウンロードします。

    :::image type="content" source="images/toolkit-palatte-search-sample.png" alt-text="スクリーンショットは、「新しい Teams アプリを作成する」VS Code コマンド パレットで Teams サンプル オプションを一覧表示する例です。":::

    このサンプルは、Teams Toolkit サンプル ギャラリーにある *NPM Search Connector* としても使用できます。 Teams Toolkit ウィンドウで、*[開発]* > *[サンプルを見る]* > **[NPM Search Connector]** の順に選択します。

    :::image type="content" source="images/toolkit-search-sample.png" alt-text="スクリーンショットは、Teams Toolkit サンプル ギャラリーの NPM Search Connector サンプルを示す例です。":::

1. 優先プログラミング言語を選択します。
1. ワークスペース フォルダーのローカル コンピューター上の場所を選択し、アプリケーション名を入力します。
1. コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Provision in the cloud`」と入力して、必要なアプリ リソース (Azure App Service、App Service プラン、Azure Bot、マネージド ID) を Azure アカウントに作成します。
1. サブスクリプションとリソース グループを選択します。
1. **[プロビジョニング]** を選択します。
1. コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Deploy to the cloud`」と入力して、サンプル コードを Azure のプロビジョニング済みリソースにデプロイしてアプリを起動します。
1. **[展開]** を選択します。

ここから、「[ボットの Outlook チャネルを追加する](#add-an-outlook-channel-for-your-bot)」に進み、Teams メッセージ拡張機能を Outlook で機能させる最後の手順を完了できます。 (アプリ マニフェストは既に正しいバージョンを参照しているため、更新は必要ありません)。

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

[Teams 開発者マニフェスト](../resources/schema/manifest-schema.md) スキーマ バージョン`1.13`を使用して、Teams メッセージ拡張機能を Outlook で実行できるようにする必要があります。

アプリ マニフェストを更新するには、次の 2 つのオプションがあります。

# <a name="teams-toolkit"></a>[Teams ツールキット](#tab/manifest-teams-toolkit)

1. コマンド パレットを開きます: `Ctrl+Shift+P`。
1. `Teams: Upgrade Teams manifest` コマンドを実行し、アプリ マニフェスト ファイルを選択します。 変更が行われます。

# <a name="manual-steps"></a>[手動の手順](#tab/manifest-manual)

Teams アプリ マニフェストを開き、`$schema` と `manifestVersion` を次の値で更新します。

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Teams Toolkit を使用してメッセージ拡張アプリを作成した場合は、それを使用してマニフェスト ファイルへの変更を検証し、エラーを特定できます。 コマンド パレット (`Ctrl+Shift+P`) を開き、[ **Teams: マニフェスト ファイルの検証]** を見つけます。

## <a name="add-an-outlook-channel-for-your-bot"></a>ボットの Outlook チャネルを追加する

Microsoft Teams では、メッセージ拡張機能は、ホストする Web サービスと、Web サービスがホストされる場所を定義するアプリ マニフェストで構成されます。 Web サービスは、ボットに登録された Teams チャネルを介して[ボット フレームワーク SDK](/azure/bot-service/bot-service-overview) メッセージング スキーマと安全な通信プロトコルを利用します。

ユーザーが Outlook からメッセージ拡張機能を操作するには、Outlook チャネルをボットに追加する必要があります。

1. [Microsoft Azure portal](https://portal.azure.com) (以前に登録した場合は [Bot Framework ポータル](https://dev.botframework.com)) から、ボット リソースに移動します。

1. *[設定]* から **[チャネル]** を選択します。

1. *[利用可能なチャネル]* で、**[Outlook]** を選択します。 **[メッセージの拡張機能]** タブを選択し、**[適用]** を選択します。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="スクリーンショットは、Azure Bot Channels ペインからボットの Outlook 'Message Extensions' チャネルを示す例です。":::

1. Outlook チャネルがボットの **[チャネル]** ウィンドウに Teams と共に表示されていることを確認します。

    :::image type="content" source="images/azure-bot-channels.png" alt-text="スクリーンショットは、Teams と Outlook の両方のチャネルを一覧表示する [Azure Bot Channels]\(Azure Bot Channels\) ペインを示す例です。":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>SSO の Microsoft Azure Active Directory (Azure AD) アプリの登録を更新する

> [!NOTE]
> このチュートリアルで提供されている [サンプル アプリ](#quickstart) を使用している場合は、この手順をスキップできます。このシナリオでは、Azure Active Directory (AAD) の単一Sign-On認証は含まれません。

メッセージ拡張機能の Azure Active Directory シングル サインオン (SSO) は、Outlook でも [Teams と同じように](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots)機能します。 ただし、テナントのアプリの登録 ポータルで、ボットの Azure AD アプリ登録に複数のクライアント アプリケーション識別子を追加 *する* 必要があります。

1. Azure 管理者アカウントを使用して、[Azure portal](https://portal.azure.com) にサインインします。
1. **[アプリ登録]** を開きます。
1. アプリケーションの名前を選択して、アプリの登録を開きます。
1. *[管理]* の下の **[API の公開]** を選択します。
1. **[承認されたクライアント アプリケーション]** セクションで、次のすべての `Client Id` 値が一覧表示されていることを確認します。

   |Microsoft 365 クライアント アプリケーション | クライアント ID |
   |--|--|
   |Teams デスクトップとモバイル |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
   |Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
   |Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
   |Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
   |Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>更新されたメッセージ拡張機能を Teams でサイドロードする

最後の手順では、更新されたメッセージ拡張機能 ([アプリ パッケージ](/microsoftteams/platform/concepts/build-and-test/apps-package)) を Teams にサイドロードします。 完了すると、メッセージの作成領域からインストールされている *アプリ* にメッセージ拡張機能が表示されます。

1. Teams アプリケーション (マニフェスト アイコンとアプリ [アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) を zip ファイルにパッケージ化します。 Teams Toolkit を使用してアプリを作成した場合は、Teams Toolkit の *[展開]* メニューの **[Zip Teams メタデータ パッケージ]** オプションを使用して簡単に行うことができます。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="スクリーンショットは、Visual Studio Code 用 Teams Toolkit 拡張機能の [Zip Teams メタデータ パッケージ] オプションを示す例です。":::

1. サンドボックス テナント アカウントで Teams にサインインし、*開発者プレビュー* モードに切り替えます。 ユーザープロファイルの横にある省略記号 (**...**) メニューから、**[詳細]** > **[開発者プレビュー]** の順に選択します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="スクリーンショットは、&quot;Developer Preview&quot; オプションを示す例です。":::

1. **[アプリ]** を選択して、**[アプリを管理]** ウィンドウを開きます。 次に、[ **アプリのアップロード**] を選択します。

    :::image type="content" source="../assets/images/teams-manage-your-apps.png" alt-text="スクリーンショットは、[アプリのアップロード] オプションを示す例です。":::

1. [ **カスタマイズされたアプリのアップロード** ] オプションを選択し、アプリ パッケージを選択し、それを Teams クライアントにインストール (*追加*) します。

    :::image type="content" source="../assets/images/teams-upload-custom-app.png" alt-text="スクリーンショットは、Teams の [カスタマイズされたアプリのアップロード] オプションを示す例です。":::

Teams を介してサイドロードされた後、メッセージ拡張機能は Outlook for Windows デスクトップと Web で使用できます。

## <a name="preview-your-message-extension-in-outlook"></a>Outlook でメッセージ拡張機能をプレビューする

Windows デスクトップと Web 上の Outlook で実行されているメッセージ拡張機能をテストする方法は次のとおりです。

### <a name="outlook-on-the-web"></a>Outlook on the web

Outlook on the web で実行されているアプリをプレビューするには:

1. テスト テナント資格情報を使用して [outlook.com](https://www.outlook.com) にサインインします。
1. [**新規メッセージ**] を選択します。
1. コンポジション ウィンドウの下部にある **[その他のアプリ]** ポップアップ メニューを開きます。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="スクリーンショットは、メール合成ウィンドウの下部にある [その他のアプリ] メニューを表示して、メッセージ拡張機能を使用する例です。":::

Your message extension is listed. You can invoke it from there and use it just as you would while composing a message in Teams.

### <a name="outlook"></a>Outlook

デスクトップ上の Outlook で実行されているアプリ Windows プレビューするには:

1. Outlook を起動し、テスト テナントの資格情報を使用してサインインします。
1. [**新しい電子メール**] を選択します。
1. 上部のリボンの **[その他のアプリ]** ポップアップ メニューを開きます。

    :::image type="content" source="images/outlook-desktop-compose-more-apps.png" alt-text="スクリーンショットは、コンポジション ウィンドウ リボンの [その他のアプリ] を表示してメッセージ拡張機能を使用する例です。":::

メッセージ拡張機能が一覧表示され、隣接するウィンドウが開き、検索結果が表示されます。

## <a name="troubleshooting"></a>トラブルシューティング

 更新されたメッセージ拡張機能は引き続き Teams で実行され、[メッセージ拡張機能の完全な機能サポート](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)が提供されますが、この Outlook 対応エクスペリエンスの早期プレビューでは、次の点に注意する必要があります。

* Outlook のメッセージ拡張機能は、メール [*作成* コンテキスト](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)に限定されます。 Teams メッセージ拡張機能のマニフェストに *コンテキスト* として `commandBox` が含まれている場合でも、現在のプレビューはメール構成 (`compose`) オプションに制限されています。 グローバル Outlook *[検索]* ボックスからのメッセージ拡張機能の呼び出しはサポートされていません。
* [Outlook では、アクション ベースのメッセージ拡張](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) コマンドはサポートされていません。 アプリに検索ベースとアクション ベースの両方のコマンドがある場合は、Outlook に表示されますが、アクション メニューは使用できません。
* 5 つを超える[アダプティブ カード](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design)のメールへの挿入はサポートされていません。アダプティブ カード v1.4 以降はサポートされていません。
* タイプ `messageBack`、`imBack`、`invoke`、および `signin` の[カード アクション](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)は、挿入されたカードではサポートされていません。 サポートは に `openURL`制限されています。 を選択すると、ユーザーは新しいタブで指定された URL にリダイレクトされます。

[Microsoft Teams 開発者コミュニティ チャネル](/microsoftteams/platform/feedback)を使用して、問題を報告し、フィードバックを提供します。

### <a name="debugging"></a>デバッグ

メッセージ拡張機能をテストするときに、[[アクティビティ]](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) オブジェクトの [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) によってボット要求のソース (Teams と Outlook から発信) を識別できます。 ユーザーがクエリを実行すると、サービスは標準の Bot Framework `Activity` オブジェクトを受け取ります。 Activity オブジェクト`channelId`のプロパティの 1 つは です。これは、ボット要求の発生場所に応じて、 または `outlook`の値`msteams`を持ちます。 詳細については、「 [検索ベースのメッセージ拡張機能 SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)」を参照してください。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Node.js** |
|---------------|--------------|--------|
| NPM Search Connector | Teams Toolkit を使用して、メッセージ拡張機能アプリをビルドします。 Teams、Outlook で動作します。 |  [表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) |
| Teams リンクの展開解除 | リンクの展開を示すシンプルな Teams アプリ。 Teams、Outlook で動作します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling)

## <a name="next-step"></a>次の手順

Teams、Outlook、Office でアプリを公開します。

> [!div class="nextstepaction"]
> [Outlook と Office 用の Teams アプリを発行する](publish.md)
