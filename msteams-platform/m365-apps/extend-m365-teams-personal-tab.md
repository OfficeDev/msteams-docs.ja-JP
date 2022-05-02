---
title: Teams 個人用タブ アプリを Microsoft 365 に拡張する
description: Teams 個人用タブ アプリを Microsoft 365 に拡張する
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: high
ms.openlocfilehash: 873a6fa6207d122581e18cef0ae922ffca87762f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111522"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Teams 個人用タブを Microsoft 365 全体に拡張する

> [!NOTE]
> *Teams 個人用タブを Microsoft 365 全体に拡張する* 機能は、現在、[パブリック開発者プレビュー](../resources/dev-preview/developer-preview-intro.md)でのみ使用できます。 プレビューに含まれている機能は完全でないため、一般公開前に変更される場合があります。 これらは、テストと調査のみを目的としています。 実稼働アプリケーションでは使用しないでください。

個人用タブは、Microsoft Teams エクスペリエンスを向上させる優れた方法です。 個人用タブを使用すると、ユーザーがエクスペリエンスを離れるか、もう一度サインインしなくても、Teams 内でアプリケーションへのアクセス権をユーザーに提供できます。 このプレビューを使用すると、他の Microsoft 365 アプリケーション内で個人用タブを点灯させることができます。 このチュートリアルでは、既存の Teams 個人用タブを取得し、Outlook デスクトップと Web エクスペリエンスの両方、および Office on the web (office.com) で実行するように更新するプロセスを示します。

Outlook および Office Home で実行するように個人用アプリを更新するには、次の手順を実行します。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新する
> * TeamsJS SDK リファレンスを更新する
> * コンテンツ セキュリティ ポリシーヘッダーを修正する
> * シングル サインオン (SSO) の Microsoft Azure Active Directory (Azure AD) アプリ登録を更新する

アプリをテストするには、次の手順が必要です。

> [!div class="checklist"]
>
> * *Office 365ターゲット リリース* に Microsoft 365 テナントを登録する
> * Outlook アプリと Office アプリのプレビュー バージョンにアクセスするようにアカウントを構成する
> * 更新されたアプリを Teams にサイドロードする

これらの手順の後、アプリは Outlook アプリと Office アプリのプレビュー バージョンに表示されます。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次のものが必要です。

* Microsoft 365 開発者プログラム サンドボックス テナント
* *[Office 365 対象指定リリース]* に登録されているサンドボックス テナント
* Microsoft 365 Apps *ベータ チャネル* からインストールされた Office アプリを含むコンピューター
* (省略可能) Microsoft Visual Studio コードの [Teams ツールキット](https://aka.ms/teams-toolkit) 拡張機能を使用してコードを更新する

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>アップグレードの個人用タブを準備する

既存の個人用タブ アプリがある場合は、テスト用の運用プロジェクトのコピーまたはブランチを作成し、アプリ マニフェストでアプリ ID を更新して、(運用環境のアプリ ID とは異なる) 新しい識別子を使用します。

このチュートリアルを完了するためにサンプル コードを使用する場合は、[[Todo リスト サンプル入門]](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) のセットアップ手順に従って、Visual Studio Code 用 Teams ツールキット拡張機能を使用して個人用タブ アプリを構築します。 または、同じ [[Teams JS SDK v2 プレビュー用に更新された Todo リスト サンプル]](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365) から始めて、[[他の Microsoft 365 エクスペリエンスで個人用タブをプレビューする]](#preview-your-personal-tab-in-other-microsoft-365-experiences) に進むこともできます。 更新されたサンプルは、次の場所にある Teams ツールキット拡張機能内でも利用できます: *[開発]* > *[サンプルを表示]* > **[Todo リスト] (Teams、Outlook、および Office で使用可能)**。

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Teams ツールキットの Todo List サンプル (Teams、Outlook、Office で動作)":::

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

[[Teams 開発者 プレビュー マニフェスト]](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) スキーマと`Microsoft 365 DevPreview`マニフェスト バージョンを使用して、Office と Outlook で Teams 個人用タブを実行できるようにする必要があります。

Teams ツールキットを使用してアプリ マニフェストを更新するか、変更を手動で適用できます。

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

Teams ツールキットを使用して個人用アプリを作成した場合は、それを使用してマニフェスト ファイルの変更を検証し、エラーを特定することもできます。 コマンド パレットを開いてTeams を`Ctrl+Shift+P`見つけます **。マニフェスト ファイル** を検証するか、Teams ツールキットの [配置] メニューからオプションを選択します (Visual Studio Code の左側にある Teams アイコンを探します)。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams ツールキット [配置] メニューの [マニフェスト ファイルの検証] オプション":::

## <a name="update-sdk-references"></a>SDK 参照を更新する

Outlook および Office で実行するには、アプリが npm パッケージ `@microsoft/teams-js@2.0.0-beta.1` (またはそれ以降の *ベータ* 版) に依存している必要があります。 ダウンレベル バージョンの `@microsoft/teams-js` コードは Outlook と Office でサポートされていますが、非推奨の警告はログに記録され、Outlook および Office のダウンレベル バージョンの `@microsoft/teams-js` サポートは最終的に停止します。

Teams ツールキットを使用すると、コードの変更の一部を自動化して次のバージョン `@microsoft/teams-js` を採用することができますが、手動で手順を実行する場合は、[[Microsoft Teams JavaScript クライアント SDK プレビュー]](using-teams-client-sdk-preview.md) を参照してください

1. *コマンド パレット* を開きます: `Ctrl+Shift+P`
1. コマンド `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps` を実行します。

完了すると、ユーティリティは TeamsJS SDK プレビュー (`@microsoft/teams-js@2.0.0-beta.1`またはそれ以降) の依存関係を使用して `package.json` ファイルを更新し、ファイル `*.js/.ts` と `*.jsx/.tsx` は次のように更新されます。

> [!div class="checklist"]
>
> * `package.json` TeamsJS SDK プレビューへの参照
> * TeamsJS SDK プレビューの Import ステートメント
> * TeamsJS SDK プレビューへの[関数、列挙型、インターフェイス呼び出し](using-teams-client-sdk-preview.md#apis-organized-into-capabilities)
> * `TODO` コメント リマインダーを使用して、 [コンテキスト](using-teams-client-sdk-preview.md#updates-to-the-context-interface) インターフェイスの変更の影響を受ける可能性がある領域を確認する
> * [コールバック スタイル関数から promises 関数への変換](using-teams-client-sdk-preview.md#callbacks-converted-to-promises)が、ツールが検出したすべての呼び出しサイトでうまくいったことを確認するための `TODO` コメント リマインダー

> [!IMPORTANT]
> *.html* ファイル内のコードはアップグレード ツールではサポートされていないため、手動で変更する必要があります。

> [!NOTE]
> コードを手動で更新する場合は、[[Microsoft Teams JavaScript クライアント SDK プレビュー]](using-teams-client-sdk-preview.md) を参照して、必要な変更について確認してください。

## <a name="configure-content-security-policy-headers"></a>コンテンツ セキュリティ ポリシー ヘッダーを構成する

[Microsoft Teamsと同様に](/microsoftteams/platform/tabs/what-are-tabs)、タブ アプリケーションは、Office およびOutlook Web クライアントの ([iframe 要素](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)) 内でホストされます。

アプリで [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) ヘッダーを使用する場合は、CSP ヘッダーで次のすべての [frame-ancestor](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) を許可していることを確認します。

|Microsoft 365 ホスト| frame-ancestor 権限|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>SSO の Azure AD アプリ登録を更新します

個人用タブの Azure Active Directory シングルサインオン (SSO) は、Office および Outlook でも [Teams と同じように](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso)機能しますが、テナントのアプリ登録ポータル 内 タブ アプリの Azure AD *アプリ登録* に複数のクライアント アプリケーション識別子を追加する必要があります。

1. サンドボックス テナント アカウントで [[Microsoft Azure ポータル]](https://portal.azure.com) にサインインします。
1. **[アプリの登録]** ブレードを開きます。
1. 個人用タブ アプリケーションの名前を選択して、アプリの登録を開きます。
1. *[管理]* の下の **[API の公開]** を選択します。

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Azure portal の *アプリの登録* ブレードからクライアント ID を承認する":::

**[承認されたクライアント アプリケーション]** セクションで、次のすべての `Client Id` 値が追加されていることを確認します。

|Microsoft 365 クライアント アプリケーション | クライアント ID |
|--|--|
|Teams デスクトップ、モバイル |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Office デスクトップ  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Teams でアプリをサイドロード

最後の手順は、更新された個人用タブ ([アプリ パッケージ](/microsoftteams/platform/concepts/build-and-test/apps-package)) をMicrosoft Teamsにサイドロードすることです。 完了すると、アプリは Teams に加えて、Office と Outlook で実行できるようになります。

1. Teams アプリケーション (マニフェスト アイコンとアプリ [アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) を zip ファイルにパッケージ化します。 Teams ツールキットを使用してアプリを作成した場合は、Teams ツールキットの *[展開]* メニューまたは [Visual Studio Code のコマンド パレット`Ctrl+Shift+P`] の [**Zip Teams メタデータ パッケージ**] オプションを使用して簡単に行うことができます。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Visual Studio Code 用のTeams ツールキット拡張機能の 'Zip Teams メタデータ パッケージ' オプション":::

1. サンドボックス テナント アカウントを使用して Teams にログインし、パブリック開発者プレビューを使用していることを確認します。 ユーザー プロファイルの省略記号 (**...**) メニューをクリックし、**About** を開いて *開発者プレビュー* オプションがオンになっていることを確認します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams の省略記号メニューから、[バージョン情報] を開き、[開発者プレビュー] オプションがオンになっていることを確認する":::

1. *[アプリ]* ウィンドウを開き、**[カスタム アプリのアップロード]** をクリックし、**自分または自分のチームにアップロード** します。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams [アプリ] ウィンドウの [カスタム アプリのアップロード] ボタン":::

1. アプリ パッケージを選択し、*[開く]* をクリックします。

Teams を介してサイドロードされると、個人用タブは Outlook と Office で利用できるようになります。 アプリを Teams にサイドロードするために使用したのと同じ資格情報でサインインしてください。

アプリをピン留めしてすばやくアクセスすることも、左側のサイドバーにある最近のアプリケーション間の省略記号 (**...**) ポップアップでアプリを見つけることもできます。

> [!NOTE]
> Teams でアプリをピン留めしても、Office.com または Outlook のアプリとしてピン留めすることはできません。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>他の Microsoft 365 エクスペリエンスで個人用タブをプレビューする

Teams 個人用タブをアップグレードし、Teams にサイドロードすると、Windows、Web、Outlook Windows、および Web (office.com) の Office で実行されます。 これらの Microsoft 365 エクスペリエンスからプレビューする方法を次に示します。

### <a name="outlook-on-windows"></a>Windows での Outlook

Windows デスクトップの Outlook で実行されているアプリを表示するには:

1. Outlook を起動し、開発テナント アカウントを使用してサインインします。
1. サイド バーの省略記号 (**...**) をクリックします。 サイドロードされたアプリ タイトルは、インストールされているアプリの中に表示されます。
1. アプリ アイコンをクリックして、Outlook でアプリを起動します。

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Outlook デスクトップ クライアントのサイドバーにある楕円（[その他のアプリ]）オプションをクリックして、インストールされている個人用タブを表示する":::

### <a name="outlook-on-the-web"></a>Outlook on the web

Outlook on the web でアプリを表示するには:

1. [Outlook on the web](https://outlook.office.com) に移動し、開発テナント アカウントを使用してサインインします。
1. サイド バーの省略記号 (**...**) をクリックします。 サイドロードされたアプリ タイトルは、インストールされているアプリの中に表示されます。
1. アプリ アイコンをクリックして、Outlook on the web で実行されているアプリを起動してプレビューします。

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="outlook.com のサイド バーにある楕円 ([その他のアプリ]) オプションをクリックして、インストールされている個人用タブを表示する":::

### <a name="office-on-windows"></a>Windows での Office

Windows デスクトップの Office で実行されているアプリを表示するには:

1. Office を起動し、開発テナント アカウントを使用してサインインします。
1. サイド バーの省略記号 (**...**) をクリックします。 サイドロードされたアプリ タイトルは、インストールされているアプリの中に表示されます。
1. アプリ アイコンをクリックして、Office でアプリを起動します。

:::image type="content" source="images/office-desktop-more-apps.png" alt-text="Office デスクトップ クライアントのサイドバーにある楕円（[その他のアプリ]）オプションをクリックして、インストールされている個人用タブを表示する":::

### <a name="office-on-the-web"></a>Office on the web

Office on the web で実行されているアプリをプレビューするには:

1. テスト テナント資格情報を使用して office.com にログインします。
1. サイド バーの省略記号 (**...**) をクリックします。 サイドロードされたアプリ タイトルは、インストールされているアプリの中に表示されます。
1. アプリ アイコンをクリックして、Office on the web でアプリを起動します。

:::image type="content" source="images/office-web-more-apps.png" alt-text="office.com のサイド バーにある楕円 ([その他のアプリ]) オプションをクリックして、インストールされている個人用タブを表示する":::

## <a name="next-steps"></a>次の手順

Outlook および Office 対応の個人用タブはプレビュー段階にあり、運用環境での使用ではサポートされていません。 テスト目的で個人用タブ アプリをプレビュー対象ユーザーに配布する方法を次に示します。

### <a name="single-tenant-distribution"></a>シングルテナント配布

Outlook および Office 対応の個人用タブは、次の 3 つの方法のいずれかで、テスト (または運用環境) テナント全体でプレビュー対象ユーザーに配布できます。

#### <a name="teams-client"></a>Teams クライアント

*[アプリ]* メニューから、*[アプリの管理]* > **[アプリを組織に送信]** の順に選択します。 これには、IT 管理者の承認が必要です。

#### <a name="microsoft-teams-admin-center"></a>‎Microsoft Teams 管理センター

Teams 管理者は、組織のテナント用のアプリ パッケージを [[Teams admin]](https://admin.teams.microsoft.com/) からアップロードしてプレインストールできます。 詳細については、「[Microsoft Teams 管理センターでカスタム アプリをアップロードする](/MicrosoftTeams/upload-custom-apps)」を参照してください。

#### <a name="microsoft-admin-center"></a>Microsoft Admin Center

グローバル管理者は、[[Microsoft 管理者]](https://admin.microsoft.com/)からアプリ パッケージをアップロードして事前インストールできます。詳細については、「[統合アプリ ポータルのパートナーによる Microsoft 365 Apps のテストとデプロイ](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)」に関する説明を参照してください。

### <a name="multitenant-distribution"></a>マルチテナント分布

Microsoft AppSource への配布は、Outlook および Office 対応の Teams 個人用タブの初期開発者向けプレビューではサポートされていません。
