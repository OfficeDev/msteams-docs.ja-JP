## <a name="update-your-application"></a>アプリケーションを更新する

### <a name="_layoutcshtml"></a>_Layout.cshtml

タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。 次に、タブとアプリのTeams方法を示します。

- [共有] **フォルダーに** 移動し **、_Layout.cshtml** を開き、[タグ] セクションに次の項目 `<head>` を追加します。

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

**PersonalTab.cshtml を開** き、呼び出して埋め込 `<script>` みタグを更新します `microsoftTeams.initialize()` 。

更新された *PersonalTab.cshtml を保存してください*。