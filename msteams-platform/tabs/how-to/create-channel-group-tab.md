---
title: '[チャネルの作成] タブ'
author: laujan
description: Node.js、ASP.NET Core、ASP.NET Core MVC を含むカスタム チャネル、グループ タブを作成します。 アプリの生成、パッケージの作成、アプリのビルドと実行、シークレット トンネル、Teams へのアップロード
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 0febbd535f5375f03599009d32d9b613cf5af6d6
ms.sourcegitcommit: e4ccbbdce620418c129689c0ba6ad246a81068c0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2022
ms.locfileid: "68329085"
---
# <a name="create-a-channel-tab"></a>[チャネルの作成] タブ

チャネル/グループ タブは、コンテンツをチャネルやグループのチャットに配信します。また、専用の Web ベースのコンテンツまわりに関する共同作業スペースを作成するのに優れた方法です。

チャネルまたはグループ タブを構築するための [前提条件](~/tabs/how-to/tab-requirements.md) がすべて揃っていることを確認します。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Node.js を使用してカスタム チャネル/グループ タブを作成する

1. コマンド プロンプトで、**Node.js** をインストールした後に次のコマンドを入力して、[Yeoman](https://yeoman.io/) と [gulp-cli](https://www.npmjs.com/package/gulp-cli) のパッケージをインストールします。

    ```cmd
    npm install yo gulp-cli --global
    ```

2. コマンド プロンプトで、次のコマンドを入力して Microsoft Teams アプリ ジェネレーターをインストールします。

    ```cmd
    npm install generator-teams --global
    ```

チャネル/グループ タブを作成する手順を次に示します。

* [チャネル/グループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab)
* [アプリ パッケージを作成する](#create-your-app-package)
* [アプリケーションをビルドして実行する](#build-and-run-your-application)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab)
* [Teams にアプリケーションをアップロードする](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネル/グループ タブを使用してアプリケーションを生成する

1. コマンド プロンプトで、チャネル/グループ タブの新しいディレクトリを作成します。

1. 新しいディレクトリに次のコマンドを入力して、Microsoft Teams アプリ ジェネレーターを起動します。

    ```cmd
    yo teams
    ```

1. Microsoft Teams アプリ ジェネレーターによって求められる一連の質問に値を入力し、`manifest.json` ファイルを更新します。

    ![ジェネレーターを開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <details>
    <summary><b>manifest.json ファイルを更新するための一連の質問</b></summary>

    * **ソリューション名は何ですか?**

        ソリューション名はプロジェクト名です。 候補の名前をそのまま使用するには、**Enter** キーを押します。

    * **ファイルをどこに保存しますか?**

        現在、プロジェクト ディレクトリにいます。 **Enter** キーを押します。

    * **Microsoft Teams アプリ プロジェクトのタイトル**

        タイトルはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。 タイトルを入力するか、**Enter** キーを押して既定の名前をそのまま使用します。

    * **(会社) 名 (最大 32 文字)**

        会社名はアプリ マニフェストで使用されます。 会社名を入力するか、**Enter** キーを押して既定の名前をそのまま使用します。

    * **使用するマニフェスト バージョン**

        既定のスキーマを選択します。

    * **クイック スキャフォールディング (Y/n)**

        既定値は [はい] です。Microsoft パートナー ID を入力するには、**[n]** を入力します。

    * **Microsoft パートナー ID (お持ちの場合): (空白のままにする)**

        このフィールドは必須ではなく、既に [Microsoft Partner Network](https://partner.microsoft.com) に参加している場合にのみ使用する必要があります。

    * **プロジェクトに何を追加しますか?**

        **( &ast; ) A タブ** を選択します。

    * **このソリューションをホストする URL**

        既定では、ジェネレーターは Azure Web サイトの URL を提案します。 アプリをローカルでのみテストしているため、有効な URL は必要ありません。

    * **アプリ/タブが読み込まれたときに、読み込みインジケーターを表示しますか?**

        アプリまたはタブの読み込み時に読み込みインジケーターを含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **個人用アプリをタブ ヘッダーバーなしでレンダリングしますか?**

        タブのヘッダーバーなしで表示される個人用アプリを含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **Test フレームワークと初期テストを含めますか? (y/N)**

        このプロジェクトのテスト フレームワークを含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **ESLint のサポートを含めますか? (y/N)**

        ESLint サポートを含めないことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **テレメトリに Azure Application Insights を使用しますか? (y/N)**

        [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview) を含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **既定のタブ名 (最大 16 文字)**

        タブに名前を付けます。このタブ名は、ファイルまたは URL パス コンポーネントとしてプロジェクト全体で使用されます。

    * **どのような種類のタブを作成しますか?**

        方向キーを使用して **[構成可能]** タブを選択します。

    * **タブにどのようなスコープを使用しますか?**

        チームまたはグループ チャットを選択できます。

    * **タブに Microsoft Azure Active Directory (Azure AD) シングル サインオンのサポートが必要ですか?**

        タブに Microsoft Azure Active Directory (Azure AD) シングル サインオンのサポートを含め **ない** ことを選択します。既定値は [はい] です。**[n]** を入力します。

    * **このタブを SharePoint Online で使用できるようにしますか? (Y/n)**

        **[n]** を入力します。

    </details>

> [!IMPORTANT]
> パス コンポーネント **[yourDefaultTabNameTab]** は、**[既定のタブ名]** のジェネレーターに入力した値に、**[Tab]** という単語を加えたものです。たとえば、`DefaultTabName` が **[myTab]** なら、**[/MyTabTab/]** となります。

<!--- TBD: this info seems removed from the main branch.
* A **full color icon** measuring 192 x 192 pixels.
* A **transparent outline icon** measuring 32 x 32 pixels.
* A `manifest.json` file that specifies the attributes of your app.
--->

### <a name="create-your-app-package"></a>アプリ パッケージを作成する

Teams でアプリケーションをビルドして実行するには、アプリ パッケージが必要です。 アプリ パッケージは、`manifest.json` ファイルを検証し、`./package` ディレクトリに zip フォルダーを生成する gulp タスクを使用して作成されます。 コマンド プロンプトで、次のコマンドを入力します。

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

#### <a name="build-your-application"></a>アプリケーションをビルドする

コマンド プロンプトで次のコマンドを入力して、ソリューションを `./dist` フォルダーに移します:

```cmd
gulp build
```

#### <a name="run-your-application"></a>アプリケーションを実行する

1. コマンド プロンプトで次のコマンドを入力して、ローカル Web サーバーを起動します。

    ```bash
    gulp serve
    ```

1. ブラウザーで `http://localhost:3007/<yourDefaultAppNameTab>/` を入力して、アプリケーションのホーム ページを表示します。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="既定のタブ":::

1. タブ構成ページを表示するには、`http://localhost:3007/<yourDefaultAppNameTab>/config.html` に移動します。 以下の内容が表示されます。

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="タブ構成ページ":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

タブへのセキュリティで保護されたトンネルを確立するには、localhost を終了し、次のコマンドを入力します。

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが **ngrok** 経由で Microsoft Teams にアップロードされ、正常に保存されたら、トンネル セッションが終了するまで Teams で表示できます。 ngrok セッションを再起動する場合は、新しい URL でアプリを更新する必要があります。

### <a name="upload-your-application-to-teams"></a>Microsoft Teams にアプリ パッケージをアップロードする

1. Teams に移動し、**[アプリ]**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="[Teams ストア]"::: を選択します。
1. [**アプリの管理] を** > 選択 **します。アプリ** > を **アップロードする カスタム アプリをアップロードします**。
1. プロジェクト ディレクトリに移動し、**./package** フォルダーに移動し、アプリ パッケージの zip フォルダーを選択し、**[開く]** を選択します。

    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="アップロードされたチャネル タブ":::

1. ダイアログで **[追加]** を選択します。 タブが Teams にアップロードされます。

    > [!NOTE]
    > **[追加]** がダイアログ ボックスに表示されない場合は、アップロードされたアプリ パッケージ zip フォルダーのマニフェストから次のコードを削除します。 もう一度フォルダーを zip 圧縮し、Teams にアップロードします。
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. タブを追加する手順に従います。チャネルまたはグループ タブのカスタム構成ダイアログがあります。
1. **[保存]** を選択すると、タブがチャネルのタブ バーに追加されます。

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="アップロードされたチャネル タブ":::

    これで、Teams でチャネルまたはグループ タブが正常に作成され、追加されました。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>ASP.NET Core を使用してカスタム チャネル/グループ タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、[ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples)をダウンロードしてファイルを抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

チャネル/グループ タブを作成する手順を次に示します。

* [チャネル/グループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab-1)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-1)
* [アプリケーションを更新する](#update-your-application)
* [アプリケーションをビルドして実行する](#build-and-run-your-application-1)
* [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal)
* [Teams でアプリをプレビューする](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネル/グループ タブを使用してアプリケーションを生成する

1. Visual Studio を開き、**[プロジェクトまたはソリューションを開く]** を選択します。

1. **Microsoft-Teams-Samples** > **samples** > **tab-channel-group** > **razor-csharp** フォルダーに移動し、**channelGroupTab.sln** を開きます。

1. Visual Studio で **[F5]** を選択するか、アプリケーションの **デバッグ** メニューから **[デバッグの開始]** を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * `https://localhost:3978/`
    * `https://localhost:3978/privacy`
    * `https://localhost:3978/tou`

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは ASP.NET Core 3.1 Web アプリケーションの空のテンプレートから作成され、セットアップ時に **[Advanced * Configure for HTTPS]** チェック ボックスがオンになっています。 MVC サービスは、依存関係挿入フレームワーク `ConfigureServices()` のメソッドによって登録されます。 また、空のテンプレートでは、既定では静的コンテンツの提供が有効にされないため、次のコードを使用して静的ファイル ミドルウェアがメソッド `Configure()` に追加されます。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options => options.EnableEndpointRouting = false);
}

public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();
    app.UseMvc();
}
```

#### <a name="wwwroot-folder"></a>wwwroot フォルダー

ASP.NET Core では、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core は、**Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、**Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="tabcs"></a>Tab.cs

この C# ファイルには、構成中に **Tab.cshtml** から呼び出されるメソッドが含まれています。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています:

* 192 x 192 ピクセルの **フル カラー アイコン**。
* 32 x 32 ピクセルの **透明なアウトライン アイコン**。
* アプリの属性を指定する `manifest.json` ファイル。

これらのファイルは、Teams へのタブのアップロードに使用するために、アプリ パッケージで zip 形式にする必要があります。 ユーザーがタブの追加または更新を選択すると、Teams は指定されたマニフェストを `configurationUrl` 読み込み、IFrame に埋め込み、タブにレンダリングします。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラー ウィンドウで、プロジェクトを右クリックし、**[プロジェクト ファイルの編集]** を選択します。 ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます。

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

ngrok を実行したままコマンド プロンプトを確実に維持し、URL をメモしておきます。

### <a name="update-your-application"></a>アプリケーションを更新する

1. Visual Studio ソリューション エクスプローラーを開き、**[ページ]** > **[共有]** フォルダーに移動し、**_Layout.cshtml** を開き、次を追加します: <head> タグ セクション:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js"></script>
    ```

    > [!IMPORTANT]
    > 最新バージョンを表していないため、このページから `<script src="...">` URL をコピーして貼り付けないでください。 SDK の最新バージョンを取得するには、常に [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js) に移動してください。

1. `script` タグに `microsoftTeams.app.initialize();` の呼び出しを挿入します。

1. Visual Studio ソリューション エクスプローラーで **[ページ]** フォルダーに移動し、**Tab.cshtml** を開きます。

    **Tab.cshtml** 内では、アプリケーションによって、赤または灰色のアイコンでタブを表示するための 2 つのオプションがユーザーに表示されます。 **[灰色の選択]** ボタンまたは **[赤の選択]** ボタンがトリガー`saveGray()`されるか、それぞれ`saveRed()`設定`pages.config.setValidityState(true)`され、構成ページで **[保存]** が有効になります。 このコードを使用すると、要件の構成が完了し、インストールを続行できることを Teams に知らせます。 `pages.config.setConfig` のパラメーターが設定されます。 最後に、コンテンツ URL が正常に解決されたことを示すために、`saveEvent.notifySuccess()` が呼び出されます。

1. タブの HTTPS ngrok URL を使用して、各関数の `websiteUrl` と `contentUrl` の値を更新します。

    コードには、**y8rCgT2b** が ngrok URL に置き換えられた次のものが含まれるはずです。

    ```javascript
        
        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl: ""
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl: ""
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. 更新された **Tab.cshtml** を保存します。

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

1. Visual Studioで **F5** を選択するか、**[デバッグ]** メニューから **[デバッグの開始]** を選択します。

1. ブラウザーを開き、コマンド プロンプト ウィンドウに表示された ngrok HTTPS URL を使用してコンテンツ ページに移動して、**ngrok** が正常に動作していることを確認します。

    > [!TIP]
    > この記事で説明する手順を完了するには、アプリケーションを Visual Studio と ngrok の両方で実行する必要があります。 Visual Studio でアプリケーションの実行を停止して作業する必要がある場合は、**ngrok を実行し続けます**。 Visual Studio で再起動すると、アプリケーションの要求をリッスンしてルーティングを再開します。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、アプリケーションを新しい URL で更新する必要があります。

<!--- TBD: This note seems to be removed from main. Commenting it for now.
> [!NOTE]
> App Studio can be used to edit your `manifest.json` file and upload the completed package to Teams. You can also manually edit the `manifest.json` file. If you do, ensure that you build the solution again to create the `tab.zip` file to upload.
--->

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. Teams に移動します。 [Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを検査することができます。

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **[アプリ]** を開き、**[アプリのインポート]** を選択します。

<!--- TBD: This steps seems to be removed from main now so commenting it for now.

1. Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest. The name of your app package is `tab.zip`. It is available from the following path:
--->

1. アプリ パッケージの名前は `tab.zip` です。 次のパスで使用できます:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 開発者ポータルで `tab.zip` を選択して開きます。

1. 既定の **アプリ ID** が作成され、**[基本情報]** セクションに入力されます。

1. **[説明]** にアプリの短い説明と長い説明を追加します。

1. **[開発者情報]** で、必要な詳細を追加し、**Web サイト (有効な HTTPS URL である必要があります)** に ngrok HTTPS URL を指定します。

1. **アプリの URL** で、プライバシー ポリシーを `https://<yourngrokurl>/privacy` に、利用規約を `https://<yourngrokurl>/tou` に更新して保存します。

1. **アプリの機能** で、[**グループアプリとチャネル アプリ**] を選択します。 `https://<yourngrokurl>/tab` で **構成 URL** を更新し、**[スコープ]** タブを選択します。

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io` のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teams でアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー]** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの **[追加]** ページが表示されます。

1. **[チームに追加]** を選択して、チームのタブを設定します。 タブを構成し、**[保存]** を選択します。 タブが Teams で利用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="アップロードされたチャネル タブの ASPNET":::

    これで、Teams でチャネルまたはグループ タブが正常に作成され、追加されました。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>ASP.NET Core MVC を使用してカスタム チャネル/グループ タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、[ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples)をダウンロードしてファイルを抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

チャネル/グループ タブを作成する手順を次に示します。

* [チャネル/グループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab-2)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-2)
* [アプリケーションを更新する](#update-your-application-1)
* [アプリケーションをビルドして実行する](#build-and-run-your-application-2)
* [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal-1)
* [Teams でアプリをプレビューする](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネル/グループ タブを使用してアプリケーションを生成する

1. Visual Studio を開き、**[プロジェクトまたはソリューションを開く]** を選択します。

1. **Microsoft-Teams-Samples** > **samples** > **tab-channel-group** > **mvc-csharp** フォルダーに移動し、**ChannelGroupTabMVC.sln** を開きます。

1. Visual Studio で **[F5]** を選択するか、アプリケーションの **デバッグ** メニューから **[デバッグの開始]** を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * `https://localhost:3978/`
    * `https://localhost:3978/privacy`
    * `https://localhost:3978/tou`

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは ASP.NET Core 3.1 Web アプリケーションの空のテンプレートから作成され、セットアップ時に **[Advanced - Configure for HTTPS]** チェック ボックスがオンになっています。 MVC サービスは、依存関係挿入フレームワーク `ConfigureServices()` のメソッドによって登録されます。 また、空のテンプレートでは、既定では静的コンテンツの提供が有効にされないため、次のコードを使用して静的ファイル ミドルウェアがメソッド `Configure()` に追加されます。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options => options.EnableEndpointRouting = false);
}

public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();
    app.UseMvc();
}
```

#### <a name="wwwroot-folder"></a>wwwroot フォルダー

ASP.NET Core では、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています:

* 192 x 192 ピクセルの **フル カラー アイコン**。
* 32 x 32 ピクセルの **透明なアウトライン アイコン**。
* アプリの属性を指定する `manifest.json` ファイル。

これらのファイルは、Teams へのタブのアップロードに使用するために、アプリ パッケージで zip 形式にする必要があります。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラー ウィンドウで、プロジェクトを右クリックし、**[プロジェクト ファイルの編集]** を選択します。 ファイルの最後にアプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます。

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

#### <a name="models"></a>モデル

**ChannelGroup.cs** は、構成中にコントローラーから呼び出されるメッセージ オブジェクトとメソッドを表わします。

#### <a name="views"></a>ビュー

これらは、ASP.NET Core MVC のさまざまなビューです。

* ホーム: ASP.NET Core は、**Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、**Index.cshtml** がアプリケーションのホーム ページとして表示されます。

* 共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれています。 また、Teams ライブラリも参照します。

#### <a name="controllers"></a>コントローラー

コントローラーは、`ViewBag` プロパティを使用して、ビューに値を動的に転送します。

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

ngrok を実行したままコマンド プロンプトを確実に維持し、URL をメモしておきます。

### <a name="update-your-application"></a>アプリケーションを更新する

1. Visual Studio ソリューション エクスプローラーを開き、**[ビュー]** > **[共有]** フォルダーに移動し、**_Layout.cshtml** を開き、次を追加します: <head> タグ セクション:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js"></script>
    ```

    > [!IMPORTANT]
    > 最新バージョンを表していないため、このページから `<script src="...">` URL をコピーして貼り付けないでください。 SDK の最新バージョンを取得するには、常に [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js) に移動してください。

1. `script` タグに `microsoftTeams.app.initialize();` の呼び出しを挿入します。

1. Visual Studio ソリューション エクスプローラーで **[タブ]** フォルダーに移動し、**Tab.cshtml** を開きます。

    **Tab.cshtml** 内では、アプリケーションによって、赤または灰色のアイコンでタブを表示するための 2 つのオプションがユーザーに表示されます。 **[灰色の選択]** ボタンまたは **[赤の選択]** ボタンがトリガー`saveGray()`されるか、それぞれ`saveRed()`設定`pages.config.setValidityState(true)`され、構成ページで **[保存]** が有効になります。 このコードを使用すると、要件の構成が完了し、インストールを続行できることを Teams に知らせます。 `pages.config.setConfig` のパラメーターが設定されます。 最後に、コンテンツ URL が正常に解決されたことを示すために、`saveEvent.notifySuccess()` が呼び出されます。

1. タブの HTTPS ngrok URL を使用して、各関数の `websiteUrl` と `contentUrl` の値を更新します。

    コードには、**y8rCgT2b** が ngrok URL に置き換えられた次のものが含まれるはずです。

    ```javascript

        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl:""
                });
                saveEvent.notifySuccess();
            });
        }
    
        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.pages.config.setConfig({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab",
                    removeUrl:""
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. 更新された **Tab.cshtml** を必ず保存してください。

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

1. Visual Studioで **F5** を選択するか、**[デバッグ]** メニューから **[デバッグの開始]** を選択します。

1. ブラウザーを開き、コマンド プロンプト ウィンドウに表示された ngrok HTTPS URL を使用してコンテンツ ページに移動して、**ngrok** が正常に動作していることを確認します。

    > [!TIP]
    > この記事で説明する手順を完了するには、アプリケーションを Visual Studio と ngrok の両方で実行する必要があります。 Visual Studio でアプリケーションの実行を停止して作業する必要がある場合は、**ngrok を実行し続けます**。 Visual Studio で再起動すると、アプリケーションの要求をリッスンしてルーティングを再開します。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、アプリケーションを新しい URL で更新する必要があります。

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. Teams に移動します。 [Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを検査することができます。

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **アプリ** を開き、[**アプリのインポート**] を選択します。

1. アプリ パッケージの名前は **tab.zip** です。 次のパスで使用できます:

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **tab.zip** を選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID** が作成され、**[基本情報]** セクションに入力されます。

1. **[説明]** にアプリの短い説明と長い説明を追加します。

1. **[開発者情報]** で、必要な詳細を追加し、**Web サイト (有効な HTTPS URL である必要があります)** に ngrok HTTPS URL を指定します。

1. **アプリの URL** で、プライバシー ポリシーを `https://<yourngrokurl>/privacy` に、利用規約を `https://<yourngrokurl>/tou` に更新して保存します。

1. **アプリの機能** で、[**グループアプリとチャネル アプリ**] を選択します。 `https://<yourngrokurl>/tab` で **構成 URL** を更新し、**[スコープ]** タブを選択します。

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io` のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teams でアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー]** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの **[追加]** ページが表示されます。

1. **[チームに追加]** を選択して、チームのタブを設定します。 タブを構成し、**[保存]** を選択します。 タブが Teams で利用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="アップロードされたチャネル タブの ASPNET MVC":::

    これで、Teams でチャネルまたはグループ タブが正常に作成され、追加されました。

::: zone-end

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)
* [Teams のタブとして SharePoint ページを追加する](https://support.microsoft.com/en-us/office/add-a-sharepoint-page-list-or-document-library-as-a-tab-in-teams-131edef1-455f-4c67-a8ce-efa2ebf25f0b)
