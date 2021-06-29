### <a name="_layoutcshtml"></a>_Layout.cshtml

タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。 次に、タブとクライアントがTeams方法を示します。

[共有] **フォルダーに移動** し **、_Layout.cshtml** を開き、次の項目をタグに追加 `<head>` します。

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> このページの URL は最新バージョンを表していない可能性がありますので、コピーして貼 `<script src="...">` り付けは行ないます。 SDK の最新バージョンを取得するには、常に[JavaScript API Microsoft Teams移動します](https://www.npmjs.com/package/@microsoft/teams-js)。

### <a name="tabcshtml"></a>Tab.cshtml

**埋め込みスクリプトを更新するには**

1. このVisual Studio **Tab.cshtml を** 開き、埋め込みファイルを更新します `<script>` 。

1. スクリプトの上部で、 を呼び出します `microsoftTeams.initialize()` 。

1. タブへの HTTPS ngrok URL を使用して、各関数の値 `websiteUrl` `contentUrl` と値を更新します。

    **y8rCgT2b を ngrok** URL に置き換えたコードは、次のようになります。

    ```javascript
        microsoftTeams.initialize();
    
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. 更新された **Tab.cshtml を保存してください**。

## <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

このVisual Studio F5 キー **を押するか、[** デバッグ] メニューから [**デバッグ** の開始]**を選択** します。 ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して **、ngrok** が正常に実行され、正常に動作されていることを確認します。

> [!TIP]
> アプリケーションをアプリケーションと ngrok Visual Studioする必要があります。 アプリケーションの実行を停止する必要がある場合Visual Studio ngrok を実行 **し続ける必要があります**。 引き続きリッスンし、アプリケーションの要求がサーバーで再起動されると、アプリケーションの要求のルーティングVisual Studio。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。

## <a name="upload-your-tab"></a>アップロードを表示する

>[!Note]
> App Studio を使用すると、ファイル上のmanifest.js **を編集** し、完成したパッケージをファイルにアップロードTeams。 必要に応じて、ファイルmanifest.js **手動** で編集することもできます。 その場合は、必ずソリューションを再度ビルドして、アップロードする **ファイルtab.zip作成** してください。

**タブをアップロードするには**

1. [次へ] にMicrosoft Teams。 Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。

1. [App **Studio] に移動し** 、[マニフェスト エディター **] タブを選択** します。

1. [ **マニフェスト エディターで既存のアプリ** をインポートする] を選択して、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。 アプリ パッケージの名前は次 **tab.zip。** この機能は、次の場所から利用できます。

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. アップロードtab.zipApp  Studio にアクセスします。

### <a name="update-your-app-package-with-manifest-editor"></a>マニフェスト エディターを使用してアプリ パッケージを更新する

アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージの構成を完了する必要があります。

マニフェスト エディターのウェルカム ページの右側のパネルで、新しくインポートしたタブのタイルを選択します。

マニフェスト エディターの左側にある手順の一覧と、右側には、これらの各手順の値が必要なプロパティの一覧があります。 この情報の多くが、manifest.jsによって提供されますが、更新する必要があるフィールドは次のとおりです。

#### <a name="details-app-details"></a>詳細: アプリの詳細

[アプリ **の詳細] セクションで、次の内容を実行** します。

1. **[Id]** で、[**生成] を** 選択して、プレースホルダー ID をタブに必要な GUID に置き換えます。

1. [**開発者情報] で****、ngrok** HTTPS URL を使用して Web **サイトを** 更新します。

1. [**アプリの URL] で**、[プライバシーに関する **声明] と**[使用条件] を更新して、>。 `https://<yourngrokurl>/privacy`  `https://<yourngrokurl>/tou`

#### <a name="capabilities-tabs"></a>機能: タブ

[タブ **] セクションで、次の設定を** 行います。

1. [チーム **] タブで、[** 追加] **を選択します**。

1. [チーム **] タブの** ポップアップ ウィンドウで、構成 **URL をに更新** します `https://<yourngrokurl>/tab` 。

1. [構成を **更新できますか] 、[****チーム]**、および [グループ **チャット]** チェック ボックスがオンになっていることを確認し、[保存] を **選択します**。

#### <a name="finish-domains-and-permissions"></a>完了: ドメインとアクセス許可

[ドメイン **とアクセス許可**] セクションで、タブのドメインには、HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io/` 。

#### <a name="finish-test-and-distribute"></a>完了: テストと配布

>[!IMPORTANT]
> 右側の [説明] **で**、次の警告が表示されます。
>
> &#9888; "**'validDomains' 配列にはトンネリング サイトを含めできません。..**
>
> この警告は、タブのテスト中に無視できます。

1. [テストと **配布] セクションで、[** インストール] を **選択します**。

1. ポップアップ ダイアログ ボックスで、[チームに追加] を選択するか、ドロップダウンから [チャットに追加 **] を選択します**。

1. タブを表示するチームまたはチャットを選択し、[タブの設定 **] を選択します**。

1. 次のポップアップ ダイアログ ボックスで、[灰色の選択]または [赤の選択] を選択し、[保存] を **選択します**。

1. タブを表示するには、タブをインストールしたチームに移動し、タブ バーから選択します。 構成時に選択したページが表示されます。

    ![チャネル タブ ASPNETMVC アップロード](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

