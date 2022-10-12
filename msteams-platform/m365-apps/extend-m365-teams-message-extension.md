---
title: Microsoft 365 間で Teams メッセージ拡張機能を拡張する
description: Microsoft Teams に加えて、Outlook で実行するように検索ベースのメッセージ拡張機能を更新する方法について説明します。
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: a0de61f0d1b6414d4ab35b54e4ec708f3b868948
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537508"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Microsoft 365 間で Teams メッセージ拡張機能を拡張する

検索ベースの[メッセージ拡張機能](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)を使用すると、ユーザーは外部システムを検索し、Microsoft Teams クライアントのメッセージ作成領域で結果を共有できます。 [Teams アプリを Microsoft 365 全体に拡張する](overview.md)ことで、運用環境の検索ベースの Teams メッセージ拡張機能を、Outlook for Windows デスクトップおよび outlook.com のプレビュー対象ユーザーに提供できるようになりました。

検索ベースの Teams メッセージ拡張機能を更新して Outlook を実行するプロセスには、次の手順が含まれます。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新します。
> * ボットの Outlook チャネルを追加します。
> * 更新したアプリを Teams にサイドロードします。

このガイドの残りの部分では、順を追ってこれらのステップを説明し、Outlook for Windows デスクトップと outlook.com の両方でメッセージ拡張機能をプレビューする方法を示します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次のものが必要です。

* Microsoft 365 開発者プログラム サンドボックス テナント。
* サンドボックス テナントの *Office 365 対象指定リリース* への登録。
* Microsoft 365 Apps *ベータ チャネル* からインストールされた Office アプリを含むテスト環境。
* (省略可能) Teams Toolkit 拡張機能を備えた Microsoft Visual Studio Code。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="link-unfurling"></a>リンク展開

検索ベースのメッセージ拡張機能で Teams での[リンクの展開が](../messaging-extensions/how-to/link-unfurling.md)サポートされている場合は、このチュートリアルの手順を完了すると、Outlook on the webおよび Windows デスクトップ環境でのリンクの展開も可能になります。 以下の [コード サンプル](#code-sample) セクションでは、テスト用の簡単なリンク展開アプリを提供します。

## <a name="prepare-your-message-extension-for-the-upgrade"></a>アップグレードのメッセージ拡張機能を準備する

運用環境に既存のメッセージ拡張機能がある場合は、テスト用のプロジェクトのコピーまたはブランチを作成し、アプリ マニフェストでアプリ ID を更新して、(テスト用の運用アプリ ID とは異なる) 新しい識別子を使用します。

既存の Teams アプリの更新の際に、チュートリアル全体を完了するためにサンプル コードを使用する場合は、[Teams メッセージ拡張機能検索サンプル](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search)のセットアップ手順に従うと、Microsoft Teams 検索ベースのメッセージ拡張機能をすばやく構築できます。

あるいは、次のセクションで既製の Outlook 対応アプリを使用し、このチュートリアルの [*アプリ マニフェストの更新*](#update-the-app-manifest)部分をスキップすることもできます。

### <a name="quickstart"></a>クイックスタート

Outlook で実行が既に有効になっている[サンプル メッセージ拡張機能](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365)から開始するには、Visual Studio Code 用の Teams Toolkit 拡張機能を使用します。

1. Visual Studio Code から、コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Create a new Teams app`」と入力します。
1. **[新しい Teams アプリを作成]** オプションを選択します。
1. **検索ベースのメッセージ拡張機能** を選択し、最新の Teams アプリ マニフェスト (バージョン`1.13`) を使用して、Teams メッセージ拡張機能用のサンプル コードをダウンロードします。

    :::image type="content" source="images/toolkit-palatte-search-sample.png" alt-text="「Create a new Teams app」と VS Code コマンド パレットに入力して、Teams のサンプル オプションを一覧表示する":::

    このサンプルは、Teams Toolkit サンプル ギャラリーにある *NPM Search Connector* としても使用できます。 Teams Toolkit ウィンドウで、*[開発]* > *[サンプルを見る]* > **[NPM Search Connector]** の順に選択します。

    :::image type="content" source="images/toolkit-search-sample.png" alt-text="Teams Toolkit サンプル ギャラリーにある NPM Search Connector サンプル":::

1. ワークスペース フォルダーのために、ローカル コンピューター上の場所を選択します。
1. コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Provision in the cloud`」と入力して、必要なアプリ リソース (Azure App Service、App Service プラン、Azure Bot、マネージド ID) を Azure アカウントに作成します。
1. コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Deploy to the cloud`」と入力して、サンプル コードを Azure のプロビジョニング済みリソースにデプロイしてアプリを起動します。

ここから、「[ボットの Outlook チャネルを追加する](#add-an-outlook-channel-for-your-bot)」に進み、Teams メッセージ拡張機能を Outlook で機能させる最後の手順を完了できます。 (アプリ マニフェストは既に正しいバージョンを参照しているため、更新は必要ありません。)

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

[Teams 開発者マニフェスト](../resources/schema/manifest-schema.md) スキーマ バージョン `1.13` を使用して、Teams メッセージ拡張機能を Outlook で実行できるようにする必要があります。

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

If you used Teams Toolkit to create your message extension app, you can use it to validate the changes to your manifest file and identify any errors. Open the command palette `Ctrl+Shift+P` and find **Teams: Validate manifest file**.

## <a name="add-an-outlook-channel-for-your-bot"></a>ボットの Outlook チャネルを追加する

Microsoft Teams では、メッセージ拡張機能は、ホストする Web サービスと、Web サービスがホストされる場所を定義するアプリ マニフェストで構成されます。 Web サービスは、ボットに登録された Teams チャネルを介して[ボット フレームワーク SDK](/azure/bot-service/bot-service-overview) メッセージング スキーマと安全な通信プロトコルを利用します。

ユーザーが Outlook からメッセージ拡張機能を操作するには、Outlook チャネルをボットに追加する必要があります。

1. [Microsoft Azure portal](https://portal.azure.com) (以前に登録した場合は [Bot Framework ポータル](https://dev.botframework.com)) から、ボット リソースに移動します。

1. *[設定]* から **[チャネル]** を選択します。

1. *[利用可能なチャネル]* で、**[Outlook]** を選択します。 **[メッセージの拡張機能]** タブを選択し、**[適用]** を選択します。

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="zure ボット チャネル ウィンドウからボットの Outlook 'Message Extensions' チャネルを追加する":::

1. Outlook チャネルがボットの **[チャネル]** ウィンドウに Teams と共に表示されていることを確認します。

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Teams と Outlook チャネルの両方を一覧表示する Azure ボット チャネル ウィンドウ":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>SSO の Microsoft Azure Active Directory (Azure AD) アプリの登録を更新する

> [!NOTE]
> このチュートリアルで提供される [サンプル アプリ](#quickstart) を使用している場合は、シナリオに Azure Active Directory (AAD) シングル サインオン認証が含まれていないため、この手順をスキップできます。

メッセージ拡張機能の Azure Active Directory シングル サインオン (SSO) は、Outlook でも [Teams と同じように](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots)機能します。 ただし、テナントの *アプリの登録* ポータルで、ボットの Azure AD アプリ登録にいくつかのクライアント アプリケーション識別子を追加する必要があります。

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

最後の手順は、更新されたメッセージ拡張機能 ([アプリ パッケージ](/microsoftteams/platform/concepts/build-and-test/apps-package)) を Teams にサイドロードすることです。 完了すると、メッセージ拡張機能がインストールされている *[アプリ]* に作成メッセージ領域から表示されます。

1. Teams アプリケーション (マニフェスト アイコンとアプリ [アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) を zip ファイルにパッケージ化します。 Teams Toolkit を使用してアプリを作成した場合は、Teams Toolkit の *[展開]* メニューの **[Zip Teams メタデータ パッケージ]** オプションを使用して簡単に行うことができます。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Visual Studio Code 用のTeams ツールキット拡張機能の 'Zip Teams メタデータ パッケージ' オプション":::

1. サンドボックス テナント アカウントで Teams にサインインし、*開発者プレビュー* モードに切り替えます。 ユーザープロファイルの横にある省略記号 (**...**) メニューから、**[詳細]** > **[開発者プレビュー]** の順に選択します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams の省略記号メニューから、[バージョン情報] を開き、[開発者プレビュー] オプションを選択する":::

1. **[アプリ]** を選択して、**[アプリを管理]** ウィンドウを開きます。 次に、**[アプリの発行]** を選択します。

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="[アプリを管理] ウィンドウを開き、[アプリの発行] を選択する":::

1. **[カスタム アプリをアップロード]** オプションを選択し、アプリ パッケージを選択して、Teams クライアントにインストール (*追加*) します。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams の [カスタム アプリをアップロード] オプション":::

Teams を通じてサイドロードされると、メッセージ拡張機能は outlook.com および Outlook for Windows デスクトップで利用できるようになります。

## <a name="preview-your-message-extension-in-outlook"></a>Outlook でメッセージ拡張機能をプレビューする

Windows デスクトップと Web 上の Outlook で実行されているメッセージ拡張機能をテストする方法は次のとおりです。

### <a name="outlook-on-the-web"></a>Outlook on the web

Outlook on the web で実行されているアプリをプレビューするには:

1. テスト テナントの資格情報を使用して [outlook.com](https://www.outlook.com) にサインインします。
1. [**新規メッセージ**] を選択します。
1. コンポジション ウィンドウの下部にある **[その他のアプリ]** ポップアップ メニューを開きます。

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="メール構成ウィンドウの下部にある [その他のアプリ] メニューをクリックして、メッセージ拡張機能を使用します":::

Your message extension is listed. You can invoke it from there and use it just as you would while composing a message in Teams.

### <a name="outlook"></a>Outlook

デスクトップ上の Outlook で実行されているアプリ Windows プレビューするには:

1. テスト テナントの資格情報を使用してログインした Outlook を起動します。
1. [**新しい電子メール**] を選択します。
1. 上部のリボンの **[その他のアプリ]** ポップアップ メニューを開きます。

    :::image type="content" source="images/outlook-desktop-compose-more-apps.png" alt-text="コンポジション ウィンドウ リボンにある [その他のアプリ] をクリックして、メッセージ拡張機能を使用する":::

メッセージ拡張機能が一覧表示され、隣接するウィンドウが開き、検索結果が表示されます。

## <a name="troubleshooting"></a>トラブルシューティング

 更新されたメッセージ拡張機能は引き続き Teams で実行され、[メッセージ拡張機能の完全な機能サポート](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions)が提供されますが、この Outlook 対応エクスペリエンスの早期プレビューでは、次の点に注意する必要があります。

* Outlook のメッセージ拡張機能は、メール [*作成* コンテキスト](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions)に限定されます。 Teams メッセージ拡張機能のマニフェストに *コンテキスト* として `commandBox` が含まれている場合でも、現在のプレビューはメール構成 (`compose`) オプションに制限されています。 グローバル Outlook *[検索]* ボックスからのメッセージ拡張機能の呼び出しはサポートされていません。
* [アクション ベースのメッセージ拡張機能](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS)コマンドは、Outlook ではサポートされていません。 アプリに検索ベースのコマンドとアクション ベースのコマンドの両方がある場合は、Outlook に表示されますが、アクション メニューは使用できません。
* 5 つを超える[アダプティブ カード](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design)のメールへの挿入はサポートされていません。アダプティブ カード v1.4 以降はサポートされていません。
* タイプ `messageBack`、`imBack`、`invoke`、および `signin` の[カード アクション](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)は、挿入されたカードではサポートされていません。 サポートは `openURL` に限定されます: クリックすると、ユーザーは新しいタブで指定された URL にリダイレクトされます。

[Microsoft Teams 開発者コミュニティ チャネル](/microsoftteams/platform/feedback)を使用して、問題を報告し、フィードバックを提供します。

### <a name="debugging"></a>デバッグ

メッセージ拡張機能をテストするときに、[[アクティビティ]](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md) オブジェクトの [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) によってボット要求のソース (Teams と Outlook から発信) を識別できます。 ユーザーがクエリを実行すると、サービスは標準の Bot Framework `Activity` オブジェクトを受け取ります。 Activity オブジェクトのプロパティの 1 つは `channelId` であり、ボット リクエストの発信元に応じて `msteams` または `outlook` の値になります。 詳細については、「[検索ベースのメッセージ拡張機能 SDK](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions)」を参照してください。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Node.js** |
|---------------|--------------|--------|
| NPM Search Connector | Teams Toolkit を使用して、メッセージ拡張機能アプリをビルドします。 Teams、Outlook で動作します。 |  [表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) |
| Teams Link Unfurling | リンクの展開を示すシンプルな Teams アプリ。 Teams、Outlook で動作します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling)

## <a name="next-step"></a>次の手順

Teams、Outlook、Office でアプリを公開します。

> [!div class="nextstepaction"]
> [Outlook と Office 用の Teams アプリを発行する](publish.md)
