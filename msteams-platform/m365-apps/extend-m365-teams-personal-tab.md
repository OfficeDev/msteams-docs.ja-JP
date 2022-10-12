---
title: Teams 個人用タブ アプリを Microsoft 365 に拡張する
description: Microsoft Teams に加えて、Outlook と Office で実行するように個人用タブ アプリを更新する方法について説明します。
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 99b95d72e75bf43381ea441cf2e94f9cf63edc7e
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537592"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Teams 個人用タブを Microsoft 365 全体に拡張する

個人用タブは、Microsoft Teams エクスペリエンスを向上させる優れた方法です。 個人用タブを使用すると、ユーザーがエクスペリエンスを離れるか、もう一度サインインしなくても、Teams 内でアプリケーションへのアクセス権をユーザーに提供できます。 このプレビューを使用すると、他の Microsoft 365 アプリケーション内で個人用タブを点灯させることができます。 このチュートリアルでは、既存の Teams 個人用タブを取得し、Outlook と Office デスクトップと Web の両方のエクスペリエンスと Android 用 Office アプリで実行するように更新するプロセスについて説明します。

Outlook と Office で実行するように個人用アプリを更新するには、次の手順に従います。

> [!div class="checklist"]
>
> * アプリ マニフェストを更新します。
> * TeamsJS SDK の参照を更新します。
> * コンテンツ セキュリティ ポリシーヘッダーを修正します。
> * シングル サインオン (SSO) のMicrosoft Azure Active Directory (Azure AD) アプリ登録を更新します。
> * 更新したアプリを Teams にサイドロードします。

このガイドの残りの部分では、これらの手順について説明し、他の Microsoft 365 アプリケーションで個人用タブをプレビューする方法について説明します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次のものが必要です。

* Microsoft 365 開発者プログラム サンドボックス テナント
* *[Office 365 対象指定リリース]* に登録されているサンドボックス テナント
* Microsoft 365 Apps *ベータ チャネル* からインストールされた Office アプリを含むコンピューター
* (省略可能)Android 用 Office アプリがインストールされ、*ベータ プログラム* に登録されている Android デバイスまたはエミュレーター
* (省略可能) Microsoft Visual Studio コードの [Teams ツールキット](https://aka.ms/teams-toolkit) 拡張機能を使用してコードを更新する

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>アップグレードの個人用タブを準備する

既存の個人用タブ アプリがある場合は、テスト用の運用プロジェクトのコピーまたはブランチを作成し、アプリ マニフェストでアプリ ID を更新して、新しい識別子 (運用環境のアプリ ID とは異なるテスト用) を使用します。

このチュートリアルを完了するためにサンプル コードを使用する場合は、 [Todo List Sample](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) のセットアップ手順に従って、Visual Studio Code 用 Teams Toolkit 拡張機能を使用して個人用タブ アプリを作成し、この記事に戻って Microsoft 365 用に更新します。

または、次の [クイック スタート](#quickstart) セクションで Microsoft 365 が既に有効になっている基本的なシングル サインオン *hello world* アプリを使用し、[Teams でアプリをサイドロード](#sideload-your-app-in-teams)する手順に進むことができます。

### <a name="quickstart"></a>クイックスタート

Outlook と Office での実行が既に有効になっている [個人用タブ](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365) から始めるには、Visual Studio Code 用の Teams Toolkit 拡張機能を使用します。

1. Visual Studio Code から、コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Create a new Teams app`」と入力します。
1. **[SSO が有効な個人用] タブを選択します**。

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text="Teams ツールキットの Todo List サンプル (Teams、Outlook、Office で動作)":::

1. ワークスペース フォルダーのために、ローカル コンピューター上の場所を選択します。
1. コマンド パレット (`Ctrl+Shift+P`) を開き、Azure `Teams: Provision in the cloud` アカウントに必要なアプリ リソース (App Service プラン、ストレージ アカウント、Function App、Managed Identity) を作成します。
1. コマンド パレット (`Ctrl+Shift+P`) を開き、「`Teams: Deploy to the cloud`」と入力して、サンプル コードを Azure のプロビジョニング済みリソースにデプロイしてアプリを起動します。

ここから、先に進んで [Teams でアプリをサイドロード](#sideload-your-app-in-teams) し、Outlook と Office でアプリをプレビューできます。 (アプリ マニフェストと TeamsJS API 呼び出しは、Microsoft 365 用に既に更新されています)。

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

[Teams の開発者マニフェスト](../resources/schema/manifest-schema.md) スキーマ バージョン`1.13`を使用して、Teams の個人用タブを Outlook と Office で実行できるようにする必要があります。

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

Teams ツールキットを使用して個人用アプリを作成した場合は、それを使用してマニフェスト ファイルの変更を検証し、エラーを特定することもできます。 コマンド パレット (`Ctrl+Shift+P`) を開き、 **Teams: Validate マニフェスト ファイルを探します**。

## <a name="update-sdk-references"></a>SDK 参照を更新する

Outlook と Office で実行するには、アプリで npm パッケージ `@microsoft/teams-js@2.0.0` (またはそれ以降) を参照する必要があります。 Outlook と Office ではダウンレベル バージョンのコードがサポートされていますが、非推奨の警告がログに記録され、Outlook と Office のダウンレベル バージョンの TeamsJS のサポートは最終的に停止します。

Teams Toolkit を使用すると、1.x TeamsJS バージョンから TeamsJS バージョン 2.x.x にアップグレードするために必要なコード変更を特定して自動化できます。 または、同じ手順を手動で実行することもできます。詳細については、 [Microsoft Teams JavaScript クライアント SDK](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) を参照してください。

1. *コマンド パレット* を開きます。 `Ctrl+Shift+P`
1. コマンド`Teams: Upgrade Teams JS SDK and code references`を実行します。

完了すると、 *package.json* ファイルが参照 `@microsoft/teams-js@2.0.0` (またはそれ以降) され、ファイル `*.js/.ts` と `*.jsx/.tsx` ファイルは次のように更新されます。

> [!div class="checklist"]
>
> * teams-js@2.x.x の Import ステートメント
> * teams-js@2.x.x の[関数、列挙型、インターフェイス呼び出し](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20)
> * `TODO` コメントリマインダーは、 [コンテキスト](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface) インターフェイスの変更の影響を受ける可能性がある領域にフラグを設定します
> * [コールバック関数を Promise に変換する](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)ための `TODO` コメント リマインダー

> [!IMPORTANT]
> *.html* ファイル内のコードはアップグレード ツールではサポートされておらず、手動による変更が必要です。

## <a name="configure-content-security-policy-headers"></a>コンテンツ セキュリティ ポリシー ヘッダーを構成する

Microsoft Teams と同様に、タブ アプリケーションは Office および Outlook Web クライアントの [iframe 要素](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) 内でホストされます。

アプリで [コンテンツ セキュリティ ポリシー](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) ヘッダーを使用する場合は、CSP ヘッダーで次のすべての [フレーム先祖](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) を許可してください。

|Microsoft 365 ホスト| frame-ancestor 権限|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>SSO の Azure AD アプリ登録を更新します

個人用タブの [Azure Active Directory (AD) シングル サインオン (SSO)](../tabs/how-to/authentication/tab-sso-overview.md) は、Office と Outlook と Teams の場合と同じように機能します。 ただし、テナントの *アプリの登録* ポータルで、タブ アプリの Azure AD アプリ登録にいくつかのクライアント アプリケーション識別子を追加する必要があります。

1. サンドボックス テナント アカウントで [[Microsoft Azure ポータル]](https://portal.azure.com) にサインインします。
1. **[アプリの登録]** ブレードを開きます。
1. 個人用タブ アプリケーションの名前を選択して、アプリの登録を開きます。
1. *[管理]* の下の **[API の公開]** を選択します。

    :::image type="content" source="images/azure-app-registration-clients.png" alt-text="Azure portal の *アプリの登録* ブレードからクライアント ID を承認する":::

1. **[承認されたクライアント アプリケーション]** セクションで、次のすべての `Client Id` 値が追加されていることを確認します。

    |Microsoft 365 クライアント アプリケーション | クライアント ID |
    |--|--|
    |Teams デスクトップ、モバイル |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
    |Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
    |Office Web  |4765445b-32c6-49b0-83e6-1d93765276ca|
    |Office デスクトップ  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
    |Office Mobile  | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook デスクトップ、モバイル | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook Web | bc59ab01-8403-45c6-8796-ac3ef710b3e3|

    > [!NOTE]
    > Microsoft 365 クライアント アプリケーションの中には、クライアント ID を共有するものもあります。

## <a name="sideload-your-app-in-teams"></a>Teams でアプリをサイドロード

Office と Outlook でアプリを実行する最後の手順は、更新された個人用タブ [アプリ パッケージ](..//concepts/build-and-test/apps-package.md) を Microsoft Teams にサイドロードすることです。

1. Teams アプリケーション ([マニフェスト](../resources/schema/manifest-schema.md) アイコンと [アプリ アイコン](/microsoftteams/platform/resources/schema/manifest-schema#icons)) を zip ファイルにパッケージ化します。 Teams Toolkit を使用してアプリを作成した場合は、Teams Toolkit の **[展開]** メニューの **[Zip Teams メタデータ パッケージ]** オプションを使用して簡単に行うことができます。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Visual Studio Code 用のTeams ツールキット拡張機能の 'Zip Teams メタデータ パッケージ' オプション":::

1. サンドボックス テナント アカウントで Teams にサインインし、*開発者プレビュー* モードに切り替えます。 ユーザープロファイルの横にある省略記号 (**...**) メニューから、**[詳細]** > **[開発者プレビュー]** の順に選択します。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Teams の省略記号メニューから、[バージョン情報] を開き、[開発者プレビュー] オプションを選択する":::

1. **[アプリ]** を選択して、**[アプリを管理]** ウィンドウを開きます。 次に、**[アプリの発行]** を選択します。

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="[アプリを管理] ウィンドウを開き、[アプリの発行] を選択する":::

1. [ **カスタム アプリのアップロード** ] オプションを選択し、アプリ パッケージを選択します。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Teams の [カスタム アプリをアップロード] オプション":::

Teams にサイドロードすると、Outlook と Office で個人用タブを使用できるようになります。 Teams でアプリをサイドロードするために使用したのと同じ資格情報でサインインする必要があります。 Android 用 Office アプリを実行するときは、Office アプリから個人用タブ アプリを使用するためにアプリを再起動する必要があります。

アプリをピン留めしてすばやくアクセスすることも、左側のサイドバーにある最近のアプリケーション間の省略記号 (**...**) ポップアップでアプリを見つけることもできます。 Teams でアプリをピン留めしても、Office または Outlook ではアプリとしてピン留めされません。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>他の Microsoft 365 エクスペリエンスで個人用タブをプレビューする

Office および Outlook、Web、Windows デスクトップ クライアントで実行されているアプリをプレビューする方法を次に示します。

> [!NOTE]
> Teams からアプリをアンインストールすると、Outlook と Office の **[その他のアプリ]** カタログからもアプリが削除されます。 上記の Teams Toolkit サンプル アプリを使用している場合。

### <a name="outlook-on-windows"></a>Windows での Outlook

Windows デスクトップの Outlook で実行されているアプリを表示するには:

1. Outlook を起動し、開発テナント アカウントを使用してサインインします。
1. サイド バーで、[  **その他のアプリ**] を選択します。 サイドロードされたアプリのタイトルが、インストールされているアプリの間に表示されます。
1. アプリ アイコンを選択して、Outlook でアプリを起動します。

    :::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Outlook デスクトップ クライアントのサイドバーにある楕円（[その他のアプリ]）オプションをクリックして、インストールされている個人用タブを表示する":::

### <a name="outlook-on-the-web"></a>Outlook on the web

Outlook on the web でアプリを表示するには:

1. [Outlook on the web](https://outlook.office.com)に移動し、開発テナント アカウントを使用してサインインします。
1. サイド バーで、[  **その他のアプリ**] を選択します。 サイドロードされたアプリのタイトルが、インストールされているアプリの間に表示されます。
1. アプリ アイコンを選択して、Outlook on the webで実行されているアプリを起動してプレビューします。

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text="outlook.com のサイド バーにある楕円 ([その他のアプリ]) オプションをクリックして、インストールされている個人用タブを表示する":::

### <a name="office-on-windows"></a>Windows での Office

Windows デスクトップの Office で実行されているアプリを表示するには:

1. Office を起動し、開発テナント アカウントを使用してサインインします。
1. サイド バーの **[アプリ** ] アイコンを選択します。 サイドロードされたアプリのタイトルが、インストールされているアプリの間に表示されます。
1. アプリ アイコンを選択して、Office でアプリを起動します。

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text="Office デスクトップ クライアントのサイドバーにある楕円（[その他のアプリ]）オプションをクリックして、インストールされている個人用タブを表示する":::

### <a name="office-on-the-web"></a>Office on the web

Office on the web で実行されているアプリをプレビューするには:

1. テスト テナント資格情報 **を使用して office.com** にログインします。
1. サイド バーの **[アプリ** ] アイコンを選択します。 サイドロードされたアプリのタイトルが、インストールされているアプリの間に表示されます。
1. アプリ アイコンを選択して、Office on the webでアプリを起動します。

    :::image type="content" source="images/office-web-more-apps.png" alt-text="インストールされている個人用タブを表示するには、office.com のサイド バーにある [その他のアプリ] オプションをクリックします":::

### <a name="office-app-for-android"></a>Android 用 Office アプリ

> [!NOTE]
> アプリをインストールする前に、 [最新の Office アプリ ベータ ビルドをインストールし、ベータ](prerequisites.md#mobile) プログラムの一部になる手順を実行します。

Android 用 Office アプリで実行されているアプリを表示するには:

1. Office アプリを起動し、開発テナント アカウントを使用してサインインします。 Office アプリ for Android が Teams でアプリをサイドロードする前に既に実行されていた場合は、インストールされているアプリ間でアプリを表示するには、アプリを再起動する必要があります。
1. **[アプリ**] アイコンを選択します。 サイドロードされたアプリは、インストールされているアプリの間に表示されます。
1. アプリ アイコンを選択して、Android 用 Office アプリでアプリを起動します。

:::image type="content" source="images/office-mobile-apps.png" alt-text="Office アプリのサイド バーにある [アプリ] オプションをタップすると、インストールされている個人用タブが表示されます":::

## <a name="troubleshooting"></a>トラブルシューティング

現在、Outlook クライアントと Office クライアントでは、Teams アプリケーションの種類と機能のサブセットがサポートされています。 このサポートは、時間の経過と共に拡張されます。

さまざまな TeamsJS 機能のホスト サポートを確認するには、 [Microsoft 365](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook) サポートを参照してください。

Teams アプリの Microsoft 365 ホストとプラットフォームのサポートの全体的な概要については、「 [Microsoft 365 全体で Teams アプリを拡張](overview.md)する」を参照してください。

実行時に特定の機能のホスト サポートを確認するには、その機能 (名前空間) で関数を `isSupported()` 呼び出し、必要に応じてアプリの動作を調整します。 これにより、アプリは、それをサポートするホストの UI と機能を明るくし、そうでないホストで正常なフォールバック エクスペリエンスを提供できます。 詳細については、「 [アプリ エクスペリエンスを区別する](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience)」を参照してください。

[Microsoft Teams 開発者コミュニティ チャネル](/microsoftteams/platform/feedback)を使用して、問題を報告し、フィードバックを提供します。

### <a name="debugging"></a>デバッグ

Teams Toolkit では、Teams に加えて、Office と Outlook で実行されているタブ アプリケーションをデバッグ (`F5`) できます。

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="Teams Toolkit で Teams、Outlook、Office のデバッグ ターゲットから選択する":::

Office または Outlook へのローカル デバッグを初めて実行すると、Microsoft 365 テナント アカウントにサインインし、自己署名証明書をインストールするように求められます。 Teams を手動でインストールするように求めるメッセージも表示されます。 **[Teams にインストール] を** 選択してブラウザー ウィンドウを開き、アプリを手動でインストールします。 次に、[ **続行** ] を選択して、Office/Outlook でアプリのデバッグに進みます。

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="Toolkit ダイアログ Teams のインストール":::

フィードバックを提供し、 [Microsoft Teams Framework (TeamsFx)](https://github.com/OfficeDev/TeamsFx/issues) での Teams Toolkit デバッグ エクスペリエンスに関する問題を報告します。

#### <a name="mobile-debugging"></a>モバイル デバッグ

Teams Toolkit (`F5`) のデバッグは、Android 用 Office アプリではまだサポートされていません。 Android 用 Office アプリで実行されているアプリをリモートでデバッグする方法を次に示します。

1. 物理 Android デバイスを使用してデバッグする場合は、開発用コンピューターに接続し、 [USB デバッグ](https://developer.android.com/studio/debug/dev-options)のオプションを有効にします。 これは、Android エミュレーターで既定で有効になっています。
1. Android デバイスから Office アプリを起動します。
1. プロファイル **の [Me > Settings] > [デバッグを許可する**] を開き、[ **リモート デバッグを有効にする]** オプションをオンにします。

    :::image type="content" source="images/office-android-enable-remote-debugging.png" alt-text="リモート デバッグを有効にするを示すスクリーンショット":::

1. 終了 **設定**。
1. プロファイル画面を終了します。
1. **[アプリ] を** 選択し、サイドロードされたアプリを起動して Office アプリ内で実行します。
1. Android デバイスが開発用コンピューターに接続されていることを確認します。 開発用コンピューターから、ブラウザーを開いて DevTools 検査ページに移動します。 たとえば、Microsoft Edge に移動して `edge://inspect/#devices` 、デバッグが有効な Android WebView の一覧を表示します。
1. タブの `Microsoft Teams Tab` URL を見つけて **検査** を選択し、DevTools を使用してアプリのデバッグを開始します。

    :::image type="content" source="images/office-android-debug.png" alt-text="devtool の Web ビューの一覧を示すスクリーンショット":::

1. Android WebView 内でタブ アプリをデバッグします。 同様に、Android デバイスで通常の Web サイトを [リモートでデバッグ](/microsoft-edge/devtools-guide-chromium/remote-debugging) します。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Node.js** |
|---------------|--------------|--------|
| Todo List | ReactとAzure Functionsを使用して構築された SSO を使用した編集可能な todo リスト。 Teams でのみ動作します (このサンプル アプリを使用して、このチュートリアルで説明されているアップグレード プロセスを試してください)。 | [表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| Todo List (Microsoft 365) | ReactとAzure Functionsを使用して構築された SSO を使用した編集可能な todo リスト。 Teams、Outlook、Office で動作します。 | [表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
| イメージ エディター (Microsoft 365) | Microsoft Graph APIを使用してイメージを作成、編集、開き、保存します。 Teams、Outlook、Office で動作します。 | [表示](https://github.com/OfficeDev/m365-extensibility-image-editor) |
| サンプル起動ページ (Microsoft 365) | 異なるホストで使用可能な SSO 認証と TeamsJS SDK の機能について説明します。 Teams、Outlook、Office で動作します。 | [表示](https://github.com/OfficeDev/microsoft-teams-library-js/tree/main/apps/sample-app) |
| Northwind Orders アプリ | Microsoft TeamsJS SDK V2 を使用してチーム アプリケーションを他の M365 ホスト アプリに拡張する方法を示します。 Teams、Outlook、Office で動作します。 モバイル向けに最適化されています。| [表示](https://github.com/microsoft/app-camp/tree/main/experimental/ExtendTeamsforM365) |

## <a name="next-step"></a>次の手順

Teams、Outlook、Office でアプリを公開します。

> [!div class="nextstepaction"]
> [Outlook と Office 用の Teams アプリを発行する](publish.md)
