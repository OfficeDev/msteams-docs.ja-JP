### <a name="_layoutcshtml"></a>_Layout cshtml

タブを Teams に表示するには、 **Microsoft Teams JavaScript クライアント SDK** を含める必要があり `microsoftTeams.initialize()` ます。また、ページが読み込まれた後の呼び出しを含める必要があります。 ここでは、タブと Teams クライアントが通信する方法を説明します。

- **共有** フォルダーに移動し **_Layout cshtml** を開き、タグに以下を追加し `<head>` ます。

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
>`<script src="...">`このページでは、最新のバージョンではない可能性があるので、url をコピー/貼り付けないでください。 SDK の最新バージョンを入手するには、「 [Microsoft Teams JAVASCRIPT API](https://www.npmjs.com/package/@microsoft/teams-js)」に常にアクセスしてください。

### <a name="tabcshtml"></a>Tab. cshtml

**Tab** を開いて、埋め込みを次のように更新します。 `<script>`

- スクリプトの先頭に、を呼び出し `microsoftTeams.initialize()` ます。

- `websiteUrl` `contentUrl` HTTPS ngrok URL を使用して、各関数の値と値をタブに更新します。

コードは、 **y8rCgT2b** で次のようになり、ngrok URL に置き換えられます。

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

更新した Tab を必ず保存してください **。**

## <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

- Visual Studio で **F5** キーを押すか、[**デバッグ**] メニューの [**デバッグ開始**] を選択します。 ブラウザーを開き、コマンドプロンプトウィンドウで提供された ngrok HTTPS URL を使用してコンテンツページにアクセスすることにより、 **ngrok** が実行されて正常に動作していることを確認します。

>[!TIP]
>このクイックスタートを完了するには、Visual Studio と ngrok の両方のアプリケーションが実行されている必要があります。 Visual Studio でのアプリケーションの実行を停止する必要がある場合は、 **ngrok の実行を継続** します。 Visual Studio で再起動すると、アプリケーションの要求のルーティングが続行され、再開されます。 Ngrok サービスを再起動する必要がある場合は、新しい URL を返し、新しい URL を使用してアプリケーションを更新する必要があります。

## <a name="upload-your-tab-to-teams-with-app-studio"></a>アプリ Studio を使用して、タブを Teams にアップロードする

>[!Note]
> アプリ Studio を使用して、ファイル **のmanifest.js** を編集し、完成したパッケージを Teams にアップロードします。 必要に応じて、ファイルの **manifest.js** を手動で編集することもできます。 その場合は、ソリューションを再度ビルドして、アップロードする **tab.zip** ファイルを作成してください。

- Microsoft Teams クライアントを開きます。 [Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。

- App studio を開き、[ **マニフェストエディター** ] タブを選択します。

- [マニフェストエディター] の [ **既存のアプリ** タイルをインポートする] を選択して、タブのアプリパッケージの更新を開始します。ソースコードには、部分的に完成したマニフェストがあります。 アプリパッケージの名前は **tab.zip**。 この場所は、ここから入手できます。

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- **tab.zip** を App Studio にアップロードします。

### <a name="update-your-app-package-with-manifest-editor"></a>マニフェストエディターを使用してアプリパッケージを更新する

アプリパッケージをアプリ Studio にアップロードしたら、構成を完了する必要があります。

- マニフェストエディターのウェルカムページの右パネルで、新しくインポートしたタブのタイルを選択します。

マニフェストエディターの左側と右側に、各手順の値を指定する必要があるプロパティの一覧が表示され、それらの手順の一覧が表示されます。 *manifest.js* によって提供される情報の多くは、更新する必要があるフィールドがいくつかあります。

#### <a name="details-app-details"></a>詳細: アプリの詳細

- [ *識別* ] の下で、プレースホルダー id をタブの必須の GUID で置換する _ を **生成** します。

- [_Developer 情報] で、 *ngrok* HTTPS url を使用して **WEB サイトの url** フィールドを更新します。

- [*アプリの url* ] の下にある *ngrok* HTTPS url を使用して、プライバシーに関する **声明** と **Terms of use** url フィールドを更新します。 Url の末尾には、「 */privacy* *」および「/」* のパスを必ず含めてください。

#### <a name="capabilities-tabs"></a>機能: タブ

[ *タブ* ] セクションで、次の手順を実行します。

- [ *チーム] タブ* で、[ **追加**] を選択します。

- [チーム] タブのポップアップウィンドウで、 *構成 URL* をに更新し `https://<yourngrokurl>/tab` ます。

- 最後に、が *構成を更新できるかどうかを確認します。チーム* および *グループのチャット* ボックスがチェックされ、[ **保存**] を選択します。

#### <a name="finish-domains-and-permissions"></a>[完了]: ドメインとアクセス許可

[ *ドメインと権限* ] セクションの [ *タブからのドメイン* ] フィールドに、NGROK の URL が HTTPS プレフィックスなしで含まれている必要があり `<yourngrokurl>.ngrok.io/` ます。

#### <a name="test-and-distribute-test-and-distribute"></a>テストと配布: テストと配布

>[!IMPORTANT]
>右側の [ **説明** ] フィールドに、次の警告が表示されます。
>
>&#9888; "**validDomains ' 配列は、トンネリングサイトを含むことはできません...**"
>
>タブのテスト中は、この警告を無視できます。

[ *テストと配布* ] セクションで、次の手順を実行します。

- **[インストール]** を選択します。

- ポップアップウィンドウの [ *チームまたはチャットに追加する* ] フィールドにチームを入力し、[ **インストール**] を選択します。

- 次のポップアップウィンドウで、タブを表示するチームチャネルを選択し、[ **設定**] を選択します。

- 最後のポップアップウィンドウで、タブページ (赤または灰色のアイコン) の値を選択し、[ **保存**] を選択します。

タブを表示するには、タブをインストールしたチームに移動し、タブバーからそれを選択します。 構成時に選択したページが表示されます。
