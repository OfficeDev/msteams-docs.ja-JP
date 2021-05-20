---
title: Office 365 コネクタ
description: Microsoft TeamsでコネクタをOffice 365する方法について説明します。
keywords: Teams o365 コネクタ
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 9eaaedf88d907dd7a7422068ab5d20450345f0e7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566811"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="11275-104">Microsoft Teams用Office 365コネクタの作成</span><span class="sxs-lookup"><span data-stu-id="11275-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="11275-105">Microsoft Teamsアプリを使用すると、既存のOffice 365コネクタを追加したり、Microsoft Teamsに含める新しいOffice 365を構築したりできます。</span><span class="sxs-lookup"><span data-stu-id="11275-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="11275-106">詳細については、「 [独自のコネクタを構築](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="11275-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="11275-107">Teams アプリへのコネクタの追加</span><span class="sxs-lookup"><span data-stu-id="11275-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="11275-108">登録済みのコネクタを Teams アプリ パッケージの一部として配布できます。</span><span class="sxs-lookup"><span data-stu-id="11275-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="11275-109">スタンドアロン ソリューションとして、またはTeamsでエクスペリエンスで有効にするいくつかの[機能](~/concepts/extensibility-points.md)の 1 つとして、[パッケージ化して](~/concepts/build-and-test/apps-package.md)、AppSource 申請の一部として、またはTeams内でアップロードするユーザーに直接提供することができます。 [](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="11275-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="11275-110">コネクタを配布するには、コネクタ [開発者ダッシュボード](https://outlook.office.com/connectors/home/login/#/publish)を使用して登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="11275-111">既定では、コネクタが登録されると、コネクタは、OutlookやTeamsを含む、それらをサポートするすべてのOffice 365製品で動作することを前提としています。</span><span class="sxs-lookup"><span data-stu-id="11275-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="11275-112">そう _ではなく_、Microsoft Teamsでのみ動作するコネクタを作成する必要がある場合は [、Microsoft Teamsアプリの提出書類](mailto:teamsubm@microsoft.com)に直接お問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="11275-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11275-113">コネクタ開発者ダッシュボードで **[保存]** を選択すると、コネクタが登録されます。</span><span class="sxs-lookup"><span data-stu-id="11275-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="11275-114">コネクタを AppSource で公開する場合は[、「Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md)」の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="11275-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="11275-115">AppSource でアプリを公開せず、単に組織にのみ直接配布する場合は、 [組織 に公開](#publish-connectors-for-your-organization)します。</span><span class="sxs-lookup"><span data-stu-id="11275-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="11275-116">組織に公開するだけの場合は、コネクタ ダッシュボードでそれ以上の操作は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="11275-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="11275-117">構成エクスペリエンスの統合</span><span class="sxs-lookup"><span data-stu-id="11275-117">Integrating the configuration experience</span></span>

<span data-ttu-id="11275-118">ユーザーは、Teams クライアントから離れることなく、コネクタ構成エクスペリエンス全体を完了します。</span><span class="sxs-lookup"><span data-stu-id="11275-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="11275-119">このエクスペリエンスを実現するために、Teamsは iframe 内に直接構成ページを埋め込みます。</span><span class="sxs-lookup"><span data-stu-id="11275-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="11275-120">操作の順序は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="11275-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="11275-121">ユーザーがコネクタをクリックして、構成プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="11275-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="11275-122">Teamsは、構成エクスペリエンスを一列に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="11275-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="11275-123">ユーザーは Web エクスペリエンスを操作して構成を完了します。</span><span class="sxs-lookup"><span data-stu-id="11275-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="11275-124">ユーザーは "Save" を押すと、コード内のコールバックがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="11275-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="11275-125">コードは、webhook 設定を取得して保存イベントを処理します (以下に記載)。</span><span class="sxs-lookup"><span data-stu-id="11275-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="11275-126">その後、コードは Webhook を保存してイベントを後で投稿する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="11275-127">既存の Web 構成エクスペリエンスを再利用したり、Teamsで特別にホストされる別のバージョンを作成したりできます。</span><span class="sxs-lookup"><span data-stu-id="11275-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="11275-128">コードは次のコードを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-128">Your code should:</span></span>

1. <span data-ttu-id="11275-129">Microsoft Teams JavaScript SDK を含めます。</span><span class="sxs-lookup"><span data-stu-id="11275-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="11275-130">これにより、コードから API にアクセスして、現在のユーザ/チャネル/チーム コンテキストの取得や認証フローの実行などの一般的な操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="11275-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="11275-131">`microsoftTeams.initialize()` を呼び出して SDK を初期化します。</span><span class="sxs-lookup"><span data-stu-id="11275-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="11275-132">`microsoftTeams.settings.setValidityState(true)`[保存] ボタンを有効にするときに呼び出します。</span><span class="sxs-lookup"><span data-stu-id="11275-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="11275-133">これは、選択やフィールドの更新など、有効なユーザー入力に対する応答として行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="11275-134">`microsoftTeams.settings.registerOnSaveHandler()`ユーザーが [保存] をクリックしたときに呼び出されるイベント ハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="11275-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="11275-135">`microsoftTeams.settings.setSettings()`コネクタの設定を保存するために呼び出します。</span><span class="sxs-lookup"><span data-stu-id="11275-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="11275-136">ここに保存されているのは、ユーザーがコネクタの既存の構成を更新しようとした場合に、構成ダイアログに表示される内容です。</span><span class="sxs-lookup"><span data-stu-id="11275-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="11275-137">`microsoftTeams.settings.getSettings()`URL 自体を含む、webhook プロパティを取得する呼び出し。</span><span class="sxs-lookup"><span data-stu-id="11275-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="11275-138">これを呼び出す必要があります 保存イベント中に、再設定の場合にページが最初に読み込まれたときに、これを呼び出す必要もあります。</span><span class="sxs-lookup"><span data-stu-id="11275-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="11275-139">(オプション) `microsoftTeams.settings.registerOnRemoveHandler()` ユーザーがコネクタを削除したときに呼び出されるイベント ハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="11275-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="11275-140">このイベントは、サービスにクリーンアップ操作を実行する機会を与えます。</span><span class="sxs-lookup"><span data-stu-id="11275-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="11275-141">CSS を使用せずにコネクタ構成ページを作成する HTML の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="11275-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a><span data-ttu-id="11275-142">`GetSettings()` 応答のプロパティ</span><span class="sxs-lookup"><span data-stu-id="11275-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="11275-143">`getSettings`ここでの呼び出しによって返されるパラメータは、このメソッドをタブから呼び出す場合とは異なり[、ここで](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)説明しているパラメータとは異なります。</span><span class="sxs-lookup"><span data-stu-id="11275-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="11275-144">パラメーター</span><span class="sxs-lookup"><span data-stu-id="11275-144">Parameter</span></span>   | <span data-ttu-id="11275-145">詳細</span><span class="sxs-lookup"><span data-stu-id="11275-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="11275-146">を呼び出すときにコードによって設定されるエンティティ `setSettings()` ID。</span><span class="sxs-lookup"><span data-stu-id="11275-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="11275-147">を呼び出すときにコードによって設定される構成名 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="11275-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="11275-148">を呼び出すときにコードによって設定される構成ページの `setSettings()` URL。</span><span class="sxs-lookup"><span data-stu-id="11275-148">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="11275-149">このコネクタ用に作成された webhook URL。</span><span class="sxs-lookup"><span data-stu-id="11275-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="11275-150">ウェブフック URL を保持し、それを使用して、構造化 JSON を POST して、カードをチャネルに送信します。</span><span class="sxs-lookup"><span data-stu-id="11275-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="11275-151">は、アプリケーションが正常に返される場合にのみ返されます。</span><span class="sxs-lookup"><span data-stu-id="11275-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="11275-152">返される値には、Office 365 メール、Office 365 グループ、Microsoft Teams のそれぞれに対応する `mail`、`groups`、`teams` を指定できます。</span><span class="sxs-lookup"><span data-stu-id="11275-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="11275-153">これは、コネクタのセットアップを開始したOffice 365ユーザーに対応する一意の ID です。</span><span class="sxs-lookup"><span data-stu-id="11275-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="11275-154">セキュリティで保護する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-154">It should be secured.</span></span> <span data-ttu-id="11275-155">この値は、構成をセットアップした Office 365 内のユーザーをサービス内のユーザーに関連付けるために使用できます。</span><span class="sxs-lookup"><span data-stu-id="11275-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="11275-156">上記のステップ 2 でのページのロードの一部としてユーザーを認証する必要がある場合は、ページが埋め込まれているときにログインを統合する方法の詳細については、 [このリンク](~/tabs/how-to/authentication/auth-flow-tab.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="11275-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="11275-157">クライアント間の互換性の理由から、コードは、 を呼び `microsoftTeams.authentication.registerAuthenticationHandlers()` 出す前に URL および成功/失敗コールバック メソッドを呼び出す必要があります `authenticate()` 。</span><span class="sxs-lookup"><span data-stu-id="11275-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="11275-158">編集の処理</span><span class="sxs-lookup"><span data-stu-id="11275-158">Handling edits</span></span>

<span data-ttu-id="11275-159">コードは、既存のコネクタ構成を編集するために戻るユーザーを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="11275-160">これを行うには、 `microsoftTeams.settings.setSettings()` 次のパラメータを使用して初期設定時に呼び出します。</span><span class="sxs-lookup"><span data-stu-id="11275-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="11275-161">`entityId` は、サービスによって認識され、ユーザーが構成した内容を表すカスタム ID です。</span><span class="sxs-lookup"><span data-stu-id="11275-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="11275-162">`configName` は、構成コードが取得できるフレンドリ名です</span><span class="sxs-lookup"><span data-stu-id="11275-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="11275-163">`contentUrl` は、ユーザーが既存のコネクタ構成を編集するときに読み込まれるカスタム URL です。</span><span class="sxs-lookup"><span data-stu-id="11275-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="11275-164">この URL を使用すると、コードでの編集ケースの処理を容易にすることができます。</span><span class="sxs-lookup"><span data-stu-id="11275-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="11275-165">通常、この呼び出しは、保存イベント ハンドラーの一部として行われます。</span><span class="sxs-lookup"><span data-stu-id="11275-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="11275-166">次に、 `contentUrl` 上記のコードが読み込まれると、コードを呼び出 `getSettings()` して、構成 UI の設定やフォームを事前に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="11275-167">削除の処理</span><span class="sxs-lookup"><span data-stu-id="11275-167">Handling removals</span></span>

<span data-ttu-id="11275-168">ユーザーが既存のコネクタ構成を削除したときに、必要に応じてイベント ハンドラーを実行できます。</span><span class="sxs-lookup"><span data-stu-id="11275-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="11275-169">このハンドラを登録する `microsoftTeams.settings.registerOnRemoveHandler()` 場合は、 を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="11275-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="11275-170">このハンドラーを使用して、データベースからエントリを削除するなどのクリーンアップ操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="11275-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="11275-171">マニフェストにコネクタを含めます</span><span class="sxs-lookup"><span data-stu-id="11275-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="11275-172">自動生成されたTeamsアプリ マニフェストは、ポータルからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="11275-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="11275-173">ただし、アプリをテストまたは公開するために使用する前に、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="11275-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="11275-174">[アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="11275-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="11275-175">マニフェストの `icons` の部分を変更し、アイコンの URL ではなくアイコンのファイル名を参照するようにします。</span><span class="sxs-lookup"><span data-stu-id="11275-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="11275-176">次の manifest.json ファイルには、アプリをテストして送信するために必要な基本的な要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="11275-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="11275-177">次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="11275-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="11275-178">コネクタを使用した manifest.json の例</span><span class="sxs-lookup"><span data-stu-id="11275-178">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="testing-your-connector"></a><span data-ttu-id="11275-179">コネクタのテスト</span><span class="sxs-lookup"><span data-stu-id="11275-179">Testing your Connector</span></span>

<span data-ttu-id="11275-180">コネクタをテストするには、他のアプリと同じ方法でコネクタをチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="11275-180">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="11275-181">(前のセクションの指示に従って変更された) コネクタ開発者ダッシュボードからのマニフェスト ファイルと 2 つのアイコン ファイルを使用して .zip パッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="11275-181">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="11275-182">アプリをアップロードしたら、任意のチャネルからコネクタ リストを開きます。</span><span class="sxs-lookup"><span data-stu-id="11275-182">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="11275-183">一番下までスクロールして、アプリが [**アップロード済み**] セクションに表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="11275-183">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![コネクタ ダイアログ ボックスの [アップロード済み] セクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="11275-185">構成機能を起動できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="11275-185">You can now launch the configuration experience.</span></span> <span data-ttu-id="11275-186">このフローは、ホストされたエクスペリエンスとしてMicrosoft Teams内で発生します。</span><span class="sxs-lookup"><span data-stu-id="11275-186">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="11275-187">`HttpPOST`操作が正常に動作していることを確認するには、[コネクタ にメッセージを送信](~/webhooks-and-connectors/how-to/connectors-using.md)します。</span><span class="sxs-lookup"><span data-stu-id="11275-187">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="11275-188">組織のコネクタを公開する</span><span class="sxs-lookup"><span data-stu-id="11275-188">Publish Connectors for your organization</span></span>

<span data-ttu-id="11275-189">コネクタ アプリをパブリック AppSource/Store に公開したくない場合がありますが、組織のユーザーのみが使用できるようにしたい場合があります。</span><span class="sxs-lookup"><span data-stu-id="11275-189">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="11275-190">このような場合は、組織の [App Catalog](~/concepts/deploy-and-publish/apps-publish.md)にカスタム コネクタ アプリをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="11275-190">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="11275-191">この方法では、コネクタ アプリはその組織でのみ使用でき、コネクタをパブリック ストアに発行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="11275-191">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="11275-192">アプリ パッケージをアップロードしたら、チームのコネクタを構成して使用するには、次の手順に従って組織のアプリ カタログからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="11275-192">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="11275-193">左端の垂直ナビゲーション バーからアプリ アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="11275-193">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="11275-194">**[アプリ**] ウィンドウで [**コネクタ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="11275-194">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="11275-195">追加するコネクタを選択すると、ポップアップ ダイアログ ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="11275-195">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="11275-196">[ **チームに追加** ] バーを選択します。</span><span class="sxs-lookup"><span data-stu-id="11275-196">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="11275-197">次のダイアログ ウィンドウで、チーム名またはチャネル名を入力します。</span><span class="sxs-lookup"><span data-stu-id="11275-197">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="11275-198">ダイアログ ウィンドウの右下隅から[コネクタ バーを **設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="11275-198">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="11275-199">コネクタは、そのチームのチームの [その他のオプション] &#9679;&#9679;&#9679; => [*その他のオプション*  =>  *コネクタ*  =>  *] セクション*  =>  で使用できます。</span><span class="sxs-lookup"><span data-stu-id="11275-199">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="11275-200">このセクションまでスクロールするか、コネクタ アプリを検索して移動できます。</span><span class="sxs-lookup"><span data-stu-id="11275-200">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="11275-201">コネクタを構成または変更するには、[ **構成** ] バーを選択します。</span><span class="sxs-lookup"><span data-stu-id="11275-201">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="11275-202">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="11275-202">Code sample</span></span>
|<span data-ttu-id="11275-203">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="11275-203">**Sample name**</span></span> | <span data-ttu-id="11275-204">**説明**</span><span class="sxs-lookup"><span data-stu-id="11275-204">**Description**</span></span> | <span data-ttu-id="11275-205">**.NET**</span><span class="sxs-lookup"><span data-stu-id="11275-205">**.NET**</span></span> | <span data-ttu-id="11275-206">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="11275-206">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="11275-207">コネクタ</span><span class="sxs-lookup"><span data-stu-id="11275-207">Connectors</span></span>    | <span data-ttu-id="11275-208">サンプル Office 365 チームチャネルへの通知を生成するコネクタを示します。</span><span class="sxs-lookup"><span data-stu-id="11275-208">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="11275-209">View</span><span class="sxs-lookup"><span data-stu-id="11275-209">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="11275-210">View</span><span class="sxs-lookup"><span data-stu-id="11275-210">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="11275-211">汎用コネクタのサンプル</span><span class="sxs-lookup"><span data-stu-id="11275-211">Generic connectors sample</span></span> |<span data-ttu-id="11275-212">webhook をサポートするシステムに合わせて簡単にカスタマイズできる汎用コネクタのサンプル コード。</span><span class="sxs-lookup"><span data-stu-id="11275-212">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="11275-213">View</span><span class="sxs-lookup"><span data-stu-id="11275-213">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
