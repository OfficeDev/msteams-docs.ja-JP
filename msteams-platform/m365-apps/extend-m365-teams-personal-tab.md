---
title: 個人用タブ Teamsアプリを複数のユーザーにMicrosoft 365
description: 個人用タブ Teamsアプリを複数のユーザーにMicrosoft 365
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: medium
ms.openlocfilehash: 65002e300527a03ef2b7468a97aef06295ce76a8
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453720"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>個人用タブをTeamsに拡張Microsoft 365

> [!NOTE]
> *現在、Teamsの個人用* タブを拡張Microsoft 365パブリック開発者 [向けプレビューでのみ使用できます](../resources/dev-preview/developer-preview-intro.md)。 プレビューに含まれている機能は完全でないため、一般公開前に変更される場合があります。 これらは、テストと調査のみを目的としています。 実稼働アプリケーションでは使用しないでください。

個人用タブを使用すると、ユーザーエクスペリエンスを向上Microsoft Teamsできます。 個人用タブを使用すると、ユーザーがエクスペリエンスを離れる必要や、もう一度サインインすることなく、Teams 内でアプリケーションへのアクセス権をユーザーに提供できます。 このプレビューでは、他のアプリケーション内で個人用タブMicrosoft 365できます。 このチュートリアルでは、既存の Teams 個人用タブを取得し、Outlook デスクトップと Web エクスペリエンスの両方で実行し、Office on the web (office.com) で実行するプロセスを示します。

個人用アプリを更新して、OutlookホームOffice実行するには、次の手順を実行します。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新する
> * TeamsJS SDK の参照を更新する
> * コンテンツ セキュリティ ポリシーのヘッダーを変更する
> * シングル サインオンMicrosoft Azure Active Directory (Azure AD) アプリ登録を更新する (SSO)

アプリをテストするには、次の手順が必要です。

> [!div class="checklist"]
>
> * ターゲットリリースMicrosoft 365にOffice 365 *テナントを登録する*
> * アプリとアプリのプレビュー バージョンにアクセスOutlookアカウントOfficeする
> * 更新したアプリをアプリにサイドロードTeams

これらの手順を実行すると、アプリがプレビュー バージョンのアプリとアプリOutlook表示Officeされます。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次の情報が必要です。

* 開発者Microsoft 365サンドボックス テナント
* ターゲットリリースに登録 *Office 365サンドボックス テナント*
* ベータ チャネルからOfficeアプリがインストールMicrosoft 365 Apps *コンピューター*
* (省略可能)[Teams Toolkit](https://aka.ms/teams-toolkit)コードの更新Microsoft Visual Studioコードの拡張機能

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>アップグレード用に個人用タブを準備する

既存の個人用タブ アプリがある場合は、アプリ マニフェストでアプリ ID をテストおよび更新するために、実稼働プロジェクトのコピーまたはブランチを作成し、新しい識別子 (実稼働アプリ ID とは異なる) を使用します。

このチュートリアルを完了するためにサンプル コードを使用する場合は、「[Todo](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) リスト サンプルの使用を開始する」のセットアップ手順に従って、Visual Studio Code の Teams Toolkit 拡張機能を使用して個人用タブ アプリを作成します。 または、[TeamsJS SDK v2 プレビュー](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365)用に更新された同じ Todo リスト サンプルから開始し、他のユーザー エクスペリエンスで [個人用] タブをプレビューするに[進Microsoft 365できます](#preview-your-personal-tab-in-other-microsoft-365-experiences)。 更新されたサンプルは、拡張機能Teams Toolkit内でも使用できます。*DevelopmentView* >  *samplesTodo* >  **List (Works in Teams、Outlook、Office)**。

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Todo List サンプル (Teams、Outlook、Office) Teams Toolkit":::

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

Teams 個人用タブを [Office](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `Microsoft 365 DevPreview` および Outlook で実行するには、Teams Teams 開発者プレビュー マニフェスト スキーマとマニフェスト バージョンを使用する必要があります。

アプリ マニフェストを更新するにはTeams Toolkitを使用するか、手動で変更を適用します。

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

個人用アプリのTeams Toolkit使用した場合は、マニフェスト ファイルへの変更を検証し、エラーを特定することもできます。 `Ctrl+Shift+P`コマンド パレットを開き、[**Teams:** マニフェスト ファイルの検証] を見つけるか、Teams Toolkit の [展開] メニューからオプションを選択します (Visual Studio Code の左側にある Teams アイコンを探します)。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit [展開] メニューの [マニフェスト ファイルの検証] オプションを選択します。":::

## <a name="update-sdk-references"></a>SDK リファレンスの更新

アプリを Outlook Office実行するには、npm `@microsoft/teams-js@2.0.0-beta.1` パッケージ (または後のベータ版) に依存する *必要* があります。 `@microsoft/teams-js` Outlook および Office `@microsoft/teams-js` ではダウンレベル バージョンのコードがサポートされている間、廃止の警告がログに記録され、Outlook および Office のダウンレベル バージョンのサポートは最終的に停止します。

Teams Toolkit を使用`@microsoft/teams-js`すると、コード変更の一部を自動化して次のバージョンを採用できますが、手順を手動で実行する場合は、「[Microsoft Teams JavaScript クライアント SDK プレビュー](using-teams-client-sdk-preview.md)」を参照してください。

1. コマンド パレット *を開きます*。 `Ctrl+Shift+P`
1. コマンドを実行する `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

完了すると、ユーティリティは `package.json` TeamsJS SDK Preview (`@microsoft/teams-js@2.0.0-beta.1` 以降) `*.js/.ts` `*.jsx/.tsx` 依存関係を持つファイルを更新し、ファイルとファイルは次の形式で更新されます。

> [!div class="checklist"]
>
> * `package.json` TeamsJS SDK プレビューへの参照
> * TeamsJS SDK プレビューのインポート ステートメント
> * TeamsJS SDK [プレビューへの関数、列挙、](using-teams-client-sdk-preview.md#apis-organized-into-capabilities)およびインターフェイスの呼び出し
> * `TODO`コンテキスト インターフェイスの変更によって影響を受け得る可能性がある領域を確認するコメント [リマインダー](using-teams-client-sdk-preview.md#updates-to-the-context-interface)
> * `TODO` コールバック スタイル関数からの [promises](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) 関数への変換がツールが見つかったすべての呼び出しサイトでうまくいったと確認するためのコメントリマインダー

> [!IMPORTANT]
> ファイル内 *.html* アップグレード ツールではサポートされていないので、手動で変更する必要があります。

> [!NOTE]
> コードを手動で更新する場合は、「[JavaScript Microsoft Teams SDK プレビュー](using-teams-client-sdk-preview.md)」を参照して、必要な変更について説明します。

## <a name="configure-content-security-policy-headers"></a>コンテンツ セキュリティ ポリシー ヘッダーの構成

[同様に、Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs)アプリケーションは、Web クライアント内の ([iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) 要素) OfficeホストOutlookされます。

アプリでコンテンツ セキュリティ [ポリシー (CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)) ヘッダーを使用する場合は、CSP ヘッダーで次のすべてのフレーム先祖を[](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors)許可することを確認します。

|Microsoft 365ホスト| frame-ancestor アクセス許可|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>SSO Azure ADアプリ登録の更新

Azure Active Directory 個人用タブのシングル サインオン (SSO) は、Teams と同じように Office と Outlook で動作しますが、テナントのアプリ[](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso)登録ポータルでタブ アプリの Azure AD アプリ登録にいくつかのクライアント アプリケーション識別子を追加する必要があります。

1. サンドボックス テナント アカウントを[Microsoft Azureポータル](https://portal.azure.com)にサインインします。
1. [アプリの **登録] ブレードを開** きます。
1. 個人用タブ アプリケーションの名前を選択して、アプリ登録を開きます。
1. [API  **の公開] ([管理]** の下) を *選択します*。

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Azure portal の *App 登録* ブレードからクライアント ID を承認する":::

[承認済 **みクライアント アプリケーション] セクション** で、次のすべての値が `Client Id` 追加されます。

|Microsoft 365 クライアント アプリケーション | クライアント ID |
|--|--|
|Teamsデスクトップ、モバイル |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4345a7b9-9a63-4910-a426-35363201d503|
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Office デスクトップ  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Outlook デスクトップ | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-00000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Teams でアプリをサイドロード

最後の手順は、更新された個人用タブ ([アプリ](/microsoftteams/platform/concepts/build-and-test/apps-package) パッケージ) をページにサイドロードMicrosoft Teams。 完了すると、アプリは、アプリに加えて、OfficeとOutlookで実行Teams。

1. zip ファイルTeamsアプリケーション (マニフェストアイコンとアプリ [アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) をパッケージ化します。 Teams Toolkit を使用してアプリを作成した場合は、Teams Toolkit  `Ctrl+Shift+P` の [展開] メニューの [**Zip Teams** メタデータ パッケージ] オプションまたは [コマンド パレット] を使用して簡単にVisual Studio Code。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="[zip Teams メタデータ パッケージ] オプションは、Teams Toolkitの拡張機能Visual Studio Code":::

1. サンドボックス テナント アカウントTeamsにログインし、パブリック サーバーにアクセスDeveloper Preview。 ユーザー プロファイルで省略記号 (**....)** メニューをクリックし、[開発者プレビュー] オプションがオンに切り替わるか確認するために [約] を開いて、Teams クライアントのプレビューを使用しているのを確認できます。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="[省略Teams] メニューの [概要] を開き、[Developer Preview] オプションがオンになっています。":::

1. [アプリ *] ウィンドウを* 開き、[カスタム アプリ **アップロードを** クリックし、自分アップロード **チームにアクセスします**。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="[アップロード] ウィンドウの [カスタム アプリTeams] ボタンをクリックします。":::

1. アプリ パッケージを選択し、[開く] を *クリックします*。

サイトをサイドロードTeams、個人用タブは、ユーザーとユーザーのOutlookでOffice。 アプリのサイドロードに使用した資格情報と同じ資格情報でサインインTeams。

アプリをピン留めしてすばやくアクセスすることもできますし、左側のサイドバーの最近のアプリケーション間で省略記号 (**....**) フライアウトでアプリを見つけたりすることもできます。

> [!NOTE]
> アプリをピン留めTeams、Office.com または Outlook でアプリとしてピン留めOutlook。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>他のユーザー エクスペリエンスで個人用タブMicrosoft 365する

Teams 個人用タブをアップグレードし、Teams でサイドロードすると、Outlook デスクトップおよび Web クライアントおよび Office on the web (office.com) でも実行されます。 これらのエクスペリエンスからプレビューする方法をMicrosoft 365します。

### <a name="outlook"></a>Outlook

デスクトップで実行中のアプリをOutlookするにはWindowsします。

1. 開発Outlookアカウントを使用して、アカウントを起動してサインインします。
1. サイド バーの省略記号 (**....**) をクリックします。 サイドロードされたアプリのタイトルが、インストールされているアプリの中に表示されます。
1. アプリのアイコンをクリックして、アプリを起動Outlook。

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="デスクトップ クライアントのサイド バーの省略記号 ('More apps') オプションをクリックしてOutlook個人用タブを表示する":::

### <a name="outlook-on-the-web"></a>Outlook on the web

アプリをアプリで表示するには、次Outlook on the web。

1. 開発テナント アカウント[Outlook on the web](https://outlook.office.com)を使用して、ユーザーに移動してサインインします。
1. サイド バーの省略記号 (**....**) をクリックします。 サイドロードされたアプリのタイトルが、インストールされているアプリの中に表示されます。
1. アプリ アイコンをクリックして、アプリを起動してプレビューし、アプリを起動Outlook on the web。

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="インストールされている個人用タブを表示するには、アプリのサイド バーの省略記号 ('more apps') outlook.com をクリックします。":::

### <a name="office"></a>Office

デスクトップで実行中のアプリをOfficeするにはWindowsします。

1. 開発Officeアカウントを使用して、アカウントを起動してサインインします。
1. サイド バーの省略記号 (**....**) をクリックします。 サイドロードされたアプリのタイトルが、インストールされているアプリの中に表示されます。
1. アプリアイコンをクリックして、アプリを起動Office。

:::image type="content" source="images/office-desktop-more-apps.png" alt-text="デスクトップ クライアントのサイド バーの省略記号 ('More apps') オプションをクリックしてOffice個人用タブを表示する":::

### <a name="office-on-the-web"></a>Office on the web

アプリで実行中のアプリをプレビューするには、次Office on the web。

1. テスト テナント資格情報 office.com ログインします。
1. サイド バーの省略記号 (**....**) をクリックします。 サイドロードされたアプリのタイトルが、インストールされているアプリの中に表示されます。
1. アプリアイコンをクリックして、アプリを起動Office on the web。

:::image type="content" source="images/office-web-more-apps.png" alt-text="インストールされている個人用タブを表示するには、アプリのサイド バーの省略記号 ('more apps') office.com をクリックします。":::

## <a name="next-steps"></a>次の手順

Outlook有効Office個人用タブはプレビュー中であり、実稼働環境での使用はサポートされていません。 テスト目的で対象ユーザーをプレビューするために個人用タブ アプリを配布する方法を次に示します。

### <a name="single-tenant-distribution"></a>単一テナントの配布

Outlook有効Office個人用タブは、次の 3 つの方法のいずれかを使用して、テスト (または実稼働) テナント全体でプレビュー対象ユーザーに配布できます。

#### <a name="teams-client"></a>Teams クライアント

[アプリ *] メニューの* [アプリ *の管理* > **] を選択して、アプリを組織に送信します**。これには、IT 管理者からの承認が必要です。

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams管理センター

管理者Teams、組織のテナントのアプリ パッケージを管理者からアップロードして[Teamsできます](https://admin.teams.microsoft.com/)。詳細[についてはアップロード管理センターのカスタム アプリMicrosoft Teamsを参照](/MicrosoftTeams/upload-custom-apps)してください。

#### <a name="microsoft-admin-center"></a>Microsoft 管理センター

グローバル管理者は、Microsoft 管理者からアプリ パッケージをアップロードして事前インストール[できます](https://admin.microsoft.com/)。詳細[については、「統合アプリ ポータルMicrosoft 365 Appsパートナーによるテストと展開」を](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)参照してください。

### <a name="multitenant-distribution"></a>マルチテナント配布

Microsoft AppSource への配布は、個人用タブの OutlookおよびOffice有効Teamsプレビュー中はサポートされていません。
