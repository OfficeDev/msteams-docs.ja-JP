## <a name="update-your-application"></a>アプリケーションを更新する

### <a name="_layoutcshtml"></a>_Layout.cshtml

タブをTeamsに表示するには **、javaScript クライアント SDK Microsoft Teams** を含め、 `microsoftTeams.initialize()` ページの読み込み後に呼び出しを含める必要があります。 これは、タブとTeamsアプリが通信する方法です。

- **[共有**] フォルダに移動し **、_Layout.cshtml** を開き、次のタグ セクションに `<head>` 追加します。

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a>パーソナルタブ.cshtml

**PersonalTab.cshtml** を開き、 `<script>` を呼び出して埋め込みタグを更新 `microsoftTeams.initialize()` します。

更新された **パーソナルタブ.cshtml** を保存してください。