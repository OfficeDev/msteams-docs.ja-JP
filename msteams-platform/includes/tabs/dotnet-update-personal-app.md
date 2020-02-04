## <a name="update-your-application"></a><span data-ttu-id="d6507-101">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="d6507-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="d6507-102">_Layout cshtml</span><span class="sxs-lookup"><span data-stu-id="d6507-102">_Layout.cshtml</span></span>

<span data-ttu-id="d6507-103">タブを Teams に表示するには、 **Microsoft Teams JavaScript クライアント SDK**を含める必要があります。また`microsoftTeams.initialize()` 、ページが読み込まれた後の呼び出しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6507-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="d6507-104">これは、タブと Teams アプリがどのように通信するかということです。</span><span class="sxs-lookup"><span data-stu-id="d6507-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="d6507-105">**共有**フォルダーに移動し **_Layout cshtml**を開き、次のものを`<head>` tags セクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="d6507-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a><span data-ttu-id="d6507-106">パーソナルタブ (cshtml)</span><span class="sxs-lookup"><span data-stu-id="d6507-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="d6507-107">[**パーソナル] タブ**を開き、を呼び出し`<script>` `microsoftTeams.initialize()`て埋め込みタグを更新します。</span><span class="sxs-lookup"><span data-stu-id="d6507-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="d6507-108">更新された*パーソナルタブ*のファイルを保存してください。</span><span class="sxs-lookup"><span data-stu-id="d6507-108">Make sure to save your updated *PersonalTab.cshtml*.</span></span>