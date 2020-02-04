## <a name="update-your-application"></a>アプリケーションを更新する

### <a name="_layoutcshtml"></a>_Layout cshtml

タブを Teams に表示するには、 **Microsoft Teams JavaScript クライアント SDK**を含める必要があります。また`microsoftTeams.initialize()` 、ページが読み込まれた後の呼び出しを含める必要があります。 これは、タブと Teams アプリがどのように通信するかということです。

- **共有**フォルダーに移動し **_Layout cshtml**を開き、次のものを`<head>` tags セクションに追加します。

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a>パーソナルタブ (cshtml)

[**パーソナル] タブ**を開き、を呼び出し`<script>` `microsoftTeams.initialize()`て埋め込みタグを更新します。

更新された*パーソナルタブ*のファイルを保存してください。