## <a name="update-your-application"></a><span data-ttu-id="d6a8f-101">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="d6a8f-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="d6a8f-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="d6a8f-102">_Layout.cshtml</span></span>

<span data-ttu-id="d6a8f-103">タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6a8f-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="d6a8f-104">次に、タブとアプリのTeams方法を示します。</span><span class="sxs-lookup"><span data-stu-id="d6a8f-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="d6a8f-105">[共有] **フォルダーに** 移動し **、_Layout.cshtml** を開き、[タグ] セクションに次の項目 `<head>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="d6a8f-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a><span data-ttu-id="d6a8f-106">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="d6a8f-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="d6a8f-107">**PersonalTab.cshtml を開** き、呼び出して埋め込 `<script>` みタグを更新します `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="d6a8f-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="d6a8f-108">更新された **PersonalTab.cshtml を保存してください**。</span><span class="sxs-lookup"><span data-stu-id="d6a8f-108">Make sure to save your updated **PersonalTab.cshtml**.</span></span>