## <a name="update-your-application"></a><span data-ttu-id="962c4-101">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="962c4-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="962c4-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="962c4-102">_Layout.cshtml</span></span>

<span data-ttu-id="962c4-103">タブをTeamsに表示するには **、javaScript クライアント SDK Microsoft Teams** を含め、 `microsoftTeams.initialize()` ページの読み込み後に呼び出しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="962c4-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="962c4-104">これは、タブとTeamsアプリが通信する方法です。</span><span class="sxs-lookup"><span data-stu-id="962c4-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="962c4-105">**[共有**] フォルダに移動し **、_Layout.cshtml** を開き、次のタグ セクションに `<head>` 追加します。</span><span class="sxs-lookup"><span data-stu-id="962c4-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a><span data-ttu-id="962c4-106">パーソナルタブ.cshtml</span><span class="sxs-lookup"><span data-stu-id="962c4-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="962c4-107">**PersonalTab.cshtml** を開き、 `<script>` を呼び出して埋め込みタグを更新 `microsoftTeams.initialize()` します。</span><span class="sxs-lookup"><span data-stu-id="962c4-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="962c4-108">更新された **パーソナルタブ.cshtml** を保存してください。</span><span class="sxs-lookup"><span data-stu-id="962c4-108">Make sure to save your updated **PersonalTab.cshtml**.</span></span>