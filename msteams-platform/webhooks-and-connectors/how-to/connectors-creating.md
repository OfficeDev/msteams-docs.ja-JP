---
title: Office 365 コネクタの作成
author: laujan
description: コネクタの使用を開始するOffice 365説明Microsoft Teams
keywords: Teams o365 コネクタ
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 28a2b35e868baf34e35a11a00e10b30b0f09c236
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179756"
---
# <a name="create-office-365-connectors"></a><span data-ttu-id="56a9b-104">Office 365 コネクタの作成</span><span class="sxs-lookup"><span data-stu-id="56a9b-104">Create Office 365 Connectors</span></span>

<span data-ttu-id="56a9b-105">アプリMicrosoft Teams、既存のコネクタを追加するか、Office 365内に新しいコネクタをTeams。</span><span class="sxs-lookup"><span data-stu-id="56a9b-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one within Teams.</span></span> <span data-ttu-id="56a9b-106">詳細については、「独自のコネクタ [をビルドする」を参照してください](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-106">For more information, see [build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).</span></span>

## <a name="add-a-connector-to-teams-app"></a><span data-ttu-id="56a9b-107">コネクタをアプリにTeamsする</span><span class="sxs-lookup"><span data-stu-id="56a9b-107">Add a connector to Teams app</span></span>

<span data-ttu-id="56a9b-108">AppSource[申請の](~/concepts/build-and-test/apps-package.md)[一部](~/concepts/deploy-and-publish/apps-publish.md)としてコネクタをパッケージ化して発行できます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-108">You can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your connector as part of your AppSource submission.</span></span> <span data-ttu-id="56a9b-109">登録されたコネクタは、アプリ パッケージの一部としてTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-109">You can distribute your registered connector as part of your Teams app package.</span></span> <span data-ttu-id="56a9b-110">アプリのエントリ ポイントの詳細については、「Teams機能」[を参照してください](~/concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-110">For information on entry points for Teams app, see [capabilities](~/concepts/extensibility-points.md).</span></span> <span data-ttu-id="56a9b-111">また、パッケージをユーザーに直接提供して、アプリ内でアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="56a9b-111">You can also provide the package to users directly for uploading within Teams.</span></span>

<span data-ttu-id="56a9b-112">コネクタを配布するには、Connectors Developer [Dashboard を使用して登録する必要があります](https://outlook.office.com/connectors/home/login/#/publish)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-112">To distribute your connector, you must register through [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="56a9b-113">コネクタが登録されている場合は、アプリケーションをサポートしているすべての Office 365 製品で動作OutlookとTeams。</span><span class="sxs-lookup"><span data-stu-id="56a9b-113">When a connector is registered, it is assumed that it works in all Office 365 products that support applications, including Outlook and Teams.</span></span> <span data-ttu-id="56a9b-114">この問題が当てはめず、アプリ申請メールで動作するコネクタのみを作成するMicrosoft Teams:Microsoft Teams[に連絡してください](mailto:teamsubm@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-114">If that is not the case and you must create a connector that only works in Microsoft Teams, contact: [Microsoft Teams App Submissions email](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56a9b-115">コネクタ開発者ダッシュボードで [保存] を **選択** すると、コネクタが登録されます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-115">Your connector is registered after you select **Save** in the Connectors Developer Dashboard.</span></span> <span data-ttu-id="56a9b-116">AppSource でコネクタを発行する場合は、「アプリを AppSource に発行する」のMicrosoft Teams[に従います](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-116">If you want to publish your connector in AppSource, follow the instructions in [publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="56a9b-117">AppSource でアプリを発行しない場合は、組織に直接配布します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-117">If you do not want to publish your app in AppSource, distribute it directly to the organization.</span></span> <span data-ttu-id="56a9b-118">組織 [のコネクタを発行した後](#publish-connectors-for-the-organization)、コネクタ ダッシュボードでそれ以上の操作は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="56a9b-118">After [publishing connectors for your organization](#publish-connectors-for-the-organization), no further action is required on the Connector Dashboard.</span></span>

### <a name="integrate-the-configuration-experience"></a><span data-ttu-id="56a9b-119">構成エクスペリエンスの統合</span><span class="sxs-lookup"><span data-stu-id="56a9b-119">Integrate the configuration experience</span></span>

<span data-ttu-id="56a9b-120">ユーザーは、クライアントから離れることなく、コネクタ構成Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-120">Users can complete the entire connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="56a9b-121">このエクスペリエンスを得Teams、構成ページを iframe 内に直接埋め込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-121">To get the experience, Teams can embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="56a9b-122">操作のシーケンスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="56a9b-122">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="56a9b-123">ユーザーがコネクタを選択して構成プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-123">The user selects the connector to begin the configuration process.</span></span>
1. <span data-ttu-id="56a9b-124">ユーザーは Web エクスペリエンスを操作して構成を完了します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-124">The user interacts with the web experience to complete the configuration.</span></span>
1. <span data-ttu-id="56a9b-125">ユーザーが [保存] **を選択** し、コード内のコールバックをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="56a9b-125">The user selects **Save**, which triggers a callback in code.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="56a9b-126">コードは、Webhook 設定を取得して保存イベントを処理できます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-126">The code can process the save event by retrieving the webhook settings.</span></span> <span data-ttu-id="56a9b-127">後でイベントを投稿する Webhook をコードに格納します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-127">Your code stores the webhook to post events later.</span></span>
    > * <span data-ttu-id="56a9b-128">構成エクスペリエンスは、構成エクスペリエンス内でインラインTeams。</span><span class="sxs-lookup"><span data-stu-id="56a9b-128">The configuration experience is loaded inline within Teams.</span></span>

<span data-ttu-id="56a9b-129">既存の Web 構成エクスペリエンスを再利用したり、別のバージョンを作成して、特にホストTeams。</span><span class="sxs-lookup"><span data-stu-id="56a9b-129">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="56a9b-130">コードには JavaScript SDK Microsoft Teams含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-130">Your code must include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="56a9b-131">これにより、現在のユーザー、チャネル、またはチーム のコンテキストを取得して認証フローを開始するなどの一般的な操作を実行するための API へのコード アクセスが可能になります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-131">This gives your code access to APIs to perform common operations, such as getting the current user, channel, or team context and initiate authentication flows.</span></span>

<span data-ttu-id="56a9b-132">**構成エクスペリエンスを統合するには**</span><span class="sxs-lookup"><span data-stu-id="56a9b-132">**To integrate the configuration experience**</span></span>

1. <span data-ttu-id="56a9b-133">`microsoftTeams.initialize()` を呼び出して SDK を初期化します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-133">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
1. <span data-ttu-id="56a9b-134">[保存 `microsoftTeams.settings.setValidityState(true)` ] を有効にする **呼び出し**。</span><span class="sxs-lookup"><span data-stu-id="56a9b-134">Call `microsoftTeams.settings.setValidityState(true)` to enable **Save**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="56a9b-135">ユーザーの選択または `microsoftTeams.settings.setValidityState(true)` フィールドの更新に対する応答として呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-135">You must call `microsoftTeams.settings.setValidityState(true)` as a response to user selection or field update.</span></span>

1. <span data-ttu-id="56a9b-136">ユーザー  `microsoftTeams.settings.registerOnSaveHandler()` が [保存] を選択すると呼び出されるイベント ハンドラーを登録 **します**。</span><span class="sxs-lookup"><span data-stu-id="56a9b-136">Register  `microsoftTeams.settings.registerOnSaveHandler()` event handler, which is called when the user selects **Save**.</span></span>
1. <span data-ttu-id="56a9b-137">コネクタ `microsoftTeams.settings.setSettings()` の設定を保存するために呼び出します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-137">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="56a9b-138">ユーザーがコネクタの既存の構成を更新しようとすると、保存された設定も構成ダイアログに表示されます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-138">The saved settings are also shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
1. <span data-ttu-id="56a9b-139">`microsoftTeams.settings.getSettings()`URL を含む Webhook プロパティをフェッチする呼び出し。</span><span class="sxs-lookup"><span data-stu-id="56a9b-139">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL.</span></span>

    > [!NOTE]
    > <span data-ttu-id="56a9b-140">再構成の場合 `microsoftTeams.settings.getSettings()` は、ページが最初に読み込まれたときに呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-140">You must call `microsoftTeams.settings.getSettings()` when your page is first loaded in case of reconfiguration.</span></span>

1. <span data-ttu-id="56a9b-141">ユーザー `microsoftTeams.settings.registerOnRemoveHandler()` がコネクタを削除するときに呼び出されるイベント ハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-141">Register `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which is called when the user removes connector.</span></span>

<span data-ttu-id="56a9b-142">このイベントは、サービスにクリーンアップ アクションを実行する機会を提供します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-142">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="56a9b-143">次のコードは、カスタマー サービスとサポートなしでコネクタ構成ページを作成するサンプル HTML を提供します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-143">The following code provides a sample HTML to create a connector configuration page without the customer service and support:</span></span>

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

<span data-ttu-id="56a9b-144">ページの読み込みの一環としてユーザーを認証[](~/tabs/how-to/authentication/auth-flow-tab.md)するには、「ページが埋め込まれているときにサインインを統合するためのタブの認証フロー」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56a9b-144">To authenticate the user as part of loading your page, see [authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md) to integrate sign in when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="56a9b-145">クライアント間の互換性上の理由から、コードは呼び出す前に URL と成功または失敗のコールバック メソッドで呼び `microsoftTeams.authentication.registerAuthenticationHandlers()` 出す必要があります `authenticate()` 。</span><span class="sxs-lookup"><span data-stu-id="56a9b-145">Due to cross client compatibility reasons, your code must call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success or failure callback methods before calling `authenticate()`.</span></span>

#### <a name="getsettings-response-properties"></a><span data-ttu-id="56a9b-146">`GetSettings` 応答プロパティ</span><span class="sxs-lookup"><span data-stu-id="56a9b-146">`GetSettings` response properties</span></span>

>[!NOTE]
><span data-ttu-id="56a9b-147">このメソッドをタブから呼び出すと、呼び出しによって返されるパラメーターは異なります。js 設定に記載されているパラメーター `getSettings` とは [異なります](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-147">The parameters returned by the `getSettings` call are different when you invoke this method from a tab and differ from those documented in [js settings](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="56a9b-148">次の表に、パラメーターと応答プロパティの詳細 `GetSetting` を示します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-148">The following table provides the parameters and the details of `GetSetting` response properties:</span></span>

| <span data-ttu-id="56a9b-149">パラメーター</span><span class="sxs-lookup"><span data-stu-id="56a9b-149">Parameters</span></span>   | <span data-ttu-id="56a9b-150">詳細</span><span class="sxs-lookup"><span data-stu-id="56a9b-150">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="56a9b-151">呼び出し時にコードによって設定されたエンティティ `setSettings()` ID。</span><span class="sxs-lookup"><span data-stu-id="56a9b-151">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="56a9b-152">呼び出し時にコードによって設定される構成名 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="56a9b-152">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="56a9b-153">呼び出し時にコードによって設定された構成ページの `setSettings()` URL。</span><span class="sxs-lookup"><span data-stu-id="56a9b-153">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="56a9b-154">コネクタ用に作成された Webhook URL。</span><span class="sxs-lookup"><span data-stu-id="56a9b-154">The webhook URL created for the connector.</span></span> <span data-ttu-id="56a9b-155">Webhook URL を使用して構造化 JSON を POST し、チャネルにカードを送信します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-155">Use the webhook URL to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="56a9b-156">アプリケーション `webhookUrl` がデータを正常に返した場合にのみ返されます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-156">The `webhookUrl` is returned only when the application returns data successfully.</span></span> |
| `appType` | <span data-ttu-id="56a9b-157">返される値は、メール、グループ、Office 365、またはOffice 365 Office 365に対応Microsoft Teams `mail` `groups` `teams` できます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-157">The values returned can be `mail`, `groups`, or `teams` corresponding to the Office 365 Mail, Office 365 Groups, or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="56a9b-158">コネクタのセットアップを開始Office 365ユーザーに対応する一意の ID。</span><span class="sxs-lookup"><span data-stu-id="56a9b-158">The unique ID corresponding to the Office 365 user who initiated the set up of the connector.</span></span> <span data-ttu-id="56a9b-159">セキュリティで保護されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-159">It must be secured.</span></span> <span data-ttu-id="56a9b-160">この値は、サービスで構成をOffice 365ユーザーを関連付ける場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-160">This value can be used to associate the user in Office 365, who has set up the configuration in your service.</span></span> |

#### <a name="handle-edits"></a><span data-ttu-id="56a9b-161">編集の処理</span><span class="sxs-lookup"><span data-stu-id="56a9b-161">Handle edits</span></span>

<span data-ttu-id="56a9b-162">コードは、既存のコネクタ構成の編集に戻るユーザーを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-162">Your code must handle users who return to edit an existing connector configuration.</span></span> <span data-ttu-id="56a9b-163">これを行うには、次の `microsoftTeams.settings.setSettings()` パラメーターを使用して初期構成中に呼び出します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-163">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="56a9b-164">`entityId` は、ユーザーがサービスで構成および理解した情報を表すカスタム ID です。</span><span class="sxs-lookup"><span data-stu-id="56a9b-164">`entityId` is the custom ID that represents what the user has configured and understood by your service.</span></span>
- <span data-ttu-id="56a9b-165">`configName` は、構成コードが取得できる名前です。</span><span class="sxs-lookup"><span data-stu-id="56a9b-165">`configName` is a name that configuration code can retrieve.</span></span>
- <span data-ttu-id="56a9b-166">`contentUrl` は、ユーザーが既存のコネクタ構成を編集するときに読み込まれるカスタム URL です。</span><span class="sxs-lookup"><span data-stu-id="56a9b-166">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span>

<span data-ttu-id="56a9b-167">この呼び出しは、保存イベント ハンドラーの一部として行います。</span><span class="sxs-lookup"><span data-stu-id="56a9b-167">This call is made as part of your save event handler.</span></span> <span data-ttu-id="56a9b-168">次に、読み込まれると、構成ユーザー インターフェイスの設定やフォームを事前に設定するためにコードを呼び `contentUrl` `getSettings()` 出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-168">Then, when the `contentUrl` is loaded, your code must call `getSettings()` to pre populate any settings or forms in your configuration user interface.</span></span>

#### <a name="handle-removals"></a><span data-ttu-id="56a9b-169">削除の処理</span><span class="sxs-lookup"><span data-stu-id="56a9b-169">Handle removals</span></span>

<span data-ttu-id="56a9b-170">ユーザーが既存のコネクタ構成を削除すると、イベント ハンドラーを実行できます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-170">You can execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="56a9b-171">このハンドラーを登録するには、 を呼び出します `microsoftTeams.settings.registerOnRemoveHandler()` 。</span><span class="sxs-lookup"><span data-stu-id="56a9b-171">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="56a9b-172">このハンドラーは、データベースからエントリを削除するなどのクリーンアップ操作を実行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-172">This handler is used to perform cleanup operations, such as removing entries from a database.</span></span>

### <a name="include-the-connector-in-your-manifest"></a><span data-ttu-id="56a9b-173">マニフェストにコネクタを含める</span><span class="sxs-lookup"><span data-stu-id="56a9b-173">Include the connector in your Manifest</span></span>

<span data-ttu-id="56a9b-174">ポータルから自動生成 `Teams app manifest` をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="56a9b-174">Download the auto generated `Teams app manifest` from the portal.</span></span> <span data-ttu-id="56a9b-175">アプリをテストまたは発行する前に、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-175">Perform the following steps, before testing or publishing the app:</span></span>

1. <span data-ttu-id="56a9b-176">[アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-176">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
1. <span data-ttu-id="56a9b-177">マニフェストの `icons` 部分を変更して、URL ではなくアイコンのファイル名を含める。</span><span class="sxs-lookup"><span data-stu-id="56a9b-177">Modify the `icons` portion of the manifest to include the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="56a9b-178">ファイルのmanifest.jsには、アプリのテストと送信に必要な要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="56a9b-178">The following manifest.json file contains the elements needed to test and submit the app:</span></span>

> [!NOTE]
> <span data-ttu-id="56a9b-179">次 `id` の `connectorId` 例では、コネクタの GUID に置き換え、使用します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-179">Replace `id` and `connectorId` in the following example with the GUID of the connector.</span></span>

#### <a name="example-of-manifestjson-with-connector"></a><span data-ttu-id="56a9b-180">コネクタを使用manifest.jsの例</span><span class="sxs-lookup"><span data-stu-id="56a9b-180">Example of manifest.json with connector</span></span>

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
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="enable-or-disable-connectors-in-teams"></a><span data-ttu-id="56a9b-181">デバイスでコネクタを有効または無効Teams</span><span class="sxs-lookup"><span data-stu-id="56a9b-181">Enable or disable connectors in Teams</span></span>

<span data-ttu-id="56a9b-182">PowerShell V2 Exchange Onlineモジュールは、モダン認証を使用し、多要素認証 (MFA と呼ばれる) を使用して、Exchange に関連する PowerShell 環境に接続Microsoft 365。</span><span class="sxs-lookup"><span data-stu-id="56a9b-182">The Exchange Online PowerShell V2 module uses modern authentication and works with multi factor authentication, called MFA for connecting to all Exchange related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="56a9b-183">管理者は、Exchange Online PowerShell を使用して、テナント全体または特定のグループ メールボックスのコネクタを無効にし、そのテナントまたはメールボックス内のすべてのユーザーに影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-183">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="56a9b-184">一部のユーザーに対して無効にし、他のユーザーに対して無効にはできません。</span><span class="sxs-lookup"><span data-stu-id="56a9b-184">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="56a9b-185">また、コネクタは既定で、テナントと呼ばれるGovernment Community CloudにGCCされます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-185">Also, connectors are disabled by default for Government Community Cloud, called GCC tenants.</span></span>

<span data-ttu-id="56a9b-186">テナント レベルの設定は、グループ レベルの設定より優先されます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-186">The tenant level setting overrides the group level setting.</span></span> <span data-ttu-id="56a9b-187">たとえば、管理者がグループのコネクタを有効にしてテナントで無効にした場合、グループのコネクタは無効になります。</span><span class="sxs-lookup"><span data-stu-id="56a9b-187">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group is disabled.</span></span> <span data-ttu-id="56a9b-188">クライアントでコネクタを有効にするにはTeams MFA のExchange Online[を使用して PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true)に接続します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-188">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-enable-or-disable-connectors"></a><span data-ttu-id="56a9b-189">コネクタを有効または無効にするコマンド</span><span class="sxs-lookup"><span data-stu-id="56a9b-189">Commands to enable or disable connectors</span></span>

<span data-ttu-id="56a9b-190">Exchange Online PowerShell で次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-190">Run the following commands in Exchange Online PowerShell:</span></span>

* <span data-ttu-id="56a9b-191">テナントのコネクタを無効にするには、次のコマンドを実行します `Set-OrganizationConfig -ConnectorsEnabled:$false` 。</span><span class="sxs-lookup"><span data-stu-id="56a9b-191">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="56a9b-192">テナントのアクション可能なメッセージを無効にするには、次の操作を行います `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` 。</span><span class="sxs-lookup"><span data-stu-id="56a9b-192">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="56a9b-193">コネクタを有効にするには、Teamsコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-193">To enable connectors for Teams, run the following commands:</span></span>
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="56a9b-194">PowerShell モジュール交換の詳細については [、「Set-OrganizationConfig」を参照してください](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-194">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="56a9b-195">コネクタを有効または無効にするにはOutlookでアプリを[グループに接続Outlook。](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)</span><span class="sxs-lookup"><span data-stu-id="56a9b-195">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="test-your-connector"></a><span data-ttu-id="56a9b-196">コネクタをテストする</span><span class="sxs-lookup"><span data-stu-id="56a9b-196">Test your connector</span></span>

<span data-ttu-id="56a9b-197">コネクタをテストするには、他のアプリを使用してチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="56a9b-197">To test your connector, upload it to a team with any other app.</span></span> <span data-ttu-id="56a9b-198">マニフェスト ファイルとコネクタ.zipマニフェスト ファイルを使用して、マニフェスト パッケージを作成できます。「マニフェストにコネクタを含める」の指示に基いて [変更されます](#include-the-connector-in-your-manifest)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-198">You can create a .zip package using the manifest file from the two icon files and connectors Developer Dashboard, modified as directed in [Include the connector in your Manifest](#include-the-connector-in-your-manifest).</span></span>

<span data-ttu-id="56a9b-199">アプリをアップロードした後、任意のチャネルからコネクタリストを開きます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-199">After you upload the app, open the connectors list from any channel.</span></span> <span data-ttu-id="56a9b-200">下にスクロールして、[アップロード] セクションにアプリ **を表示** します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-200">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

![[コネクタ] ダイアログ ボックスでアップロードされたセクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> <span data-ttu-id="56a9b-202">フローは、ホストされたエクスペリエンスとしてMicrosoft Teams内で完全に発生します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-202">The flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="56a9b-203">アクションが正 `HttpPOST` しく動作しているのを確認するには [、コネクタにメッセージを送信します](~/webhooks-and-connectors/how-to/connectors-using.md)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-203">To verify that `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-the-organization"></a><span data-ttu-id="56a9b-204">組織の発行コネクタ</span><span class="sxs-lookup"><span data-stu-id="56a9b-204">Publish connectors for the organization</span></span>

<span data-ttu-id="56a9b-205">コネクタを組織内のユーザーだけが使用できる場合は、カスタム コネクタ アプリを組織のアプリ カタログ [にアップロードできます](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="56a9b-205">If you want the connector to be available only to the users in your organization, you can upload your custom connector app to your [organization's app catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span>

<span data-ttu-id="56a9b-206">チームでコネクタを構成して使用するためにアプリ パッケージをアップロードした後、組織のアプリ カタログからコネクタをインストールします。</span><span class="sxs-lookup"><span data-stu-id="56a9b-206">After uploading the app package to configure and use the connector in a team, install the connector from the organization's app catalog.</span></span>

<span data-ttu-id="56a9b-207">**コネクタを設定するには**</span><span class="sxs-lookup"><span data-stu-id="56a9b-207">**To set up a connector**</span></span>

1. <span data-ttu-id="56a9b-208">左側の **ナビゲーション** バーから [アプリ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-208">Select **Apps** from the left navigation bar.</span></span>
1. <span data-ttu-id="56a9b-209">[アプリ **] セクションで** 、[コネクタ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="56a9b-209">In the **Apps** section, select **Connectors**.</span></span>
1. <span data-ttu-id="56a9b-210">追加するコネクタを選択します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-210">Select the connector that you want to add.</span></span> <span data-ttu-id="56a9b-211">ポップアップ ダイアログ ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-211">A pop up dialog window appears.</span></span>
1. <span data-ttu-id="56a9b-212">ドロップダウン メニューから、[チームに **追加] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="56a9b-212">From the dropdown menu, select **Add to a team**.</span></span>
1. <span data-ttu-id="56a9b-213">検索ボックスに、チーム名またはチャネル名を入力します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-213">In the search box, type a team or channel name.</span></span>
1. <span data-ttu-id="56a9b-214">ダイアログ **ウィンドウの右下隅** にあるドロップダウン メニューから [コネクタのセットアップ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-214">Select **Set up a Connector** from the dropdown menu in the bottom right corner of the dialog window.</span></span>

<span data-ttu-id="56a9b-215">コネクタは、「その他のオプション コネクタ &#9679;&#9679;&#9679; > チームのすべてのコネクタ」のセクション  >    >    >  で使用できます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-215">The connector is available in the section &#9679;&#9679;&#9679; > **More options** > **Connectors** > **All** > **Connectors for your team** for that team.</span></span> <span data-ttu-id="56a9b-216">このセクションまでスクロールするか、コネクタ アプリを検索して移動できます。</span><span class="sxs-lookup"><span data-stu-id="56a9b-216">You can navigate by scrolling to this section or search for the connector app.</span></span> <span data-ttu-id="56a9b-217">コネクタを構成または変更するには、[構成] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="56a9b-217">To configure or modify the connector, select **Configure**.</span></span>

## <a name="distribute-webhook-and-connector"></a><span data-ttu-id="56a9b-218">Webhook とコネクタの配布</span><span class="sxs-lookup"><span data-stu-id="56a9b-218">Distribute webhook and connector</span></span>

1. <span data-ttu-id="56a9b-219">[チームに直接受信 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) を設定します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-219">[Set up an Incoming Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directly for your team.</span></span>
1. <span data-ttu-id="56a9b-220">構成ページ [を追加し](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) 、O365 コネクタで受信 [Webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) を発行します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-220">Add a [configuration page](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) and [publish your Incoming Webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) in a O365 Connector.</span></span>
1. <span data-ttu-id="56a9b-221">AppSource 申請の一部としてコネクタをパッケージ化 [して発行](~/concepts/deploy-and-publish/office-store-guidance.md) します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-221">Package and publish your connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="code-sample"></a><span data-ttu-id="56a9b-222">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="56a9b-222">Code sample</span></span>

<span data-ttu-id="56a9b-223">次の表に、サンプル名とその説明を示します。</span><span class="sxs-lookup"><span data-stu-id="56a9b-223">The following table provides the sample name and its description:</span></span>

|<span data-ttu-id="56a9b-224">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="56a9b-224">**Sample name**</span></span> | <span data-ttu-id="56a9b-225">**説明**</span><span class="sxs-lookup"><span data-stu-id="56a9b-225">**Description**</span></span> | <span data-ttu-id="56a9b-226">**.NET**</span><span class="sxs-lookup"><span data-stu-id="56a9b-226">**.NET**</span></span> | <span data-ttu-id="56a9b-227">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="56a9b-227">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="56a9b-228">コネクタ</span><span class="sxs-lookup"><span data-stu-id="56a9b-228">Connectors</span></span>    | <span data-ttu-id="56a9b-229">サンプル Office 365 チャネルへの通知を生成するコネクタTeamsします。</span><span class="sxs-lookup"><span data-stu-id="56a9b-229">Sample Office 365 Connector generating notifications to Teams channel.</span></span>|   [<span data-ttu-id="56a9b-230">View</span><span class="sxs-lookup"><span data-stu-id="56a9b-230">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="56a9b-231">View</span><span class="sxs-lookup"><span data-stu-id="56a9b-231">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="56a9b-232">汎用コネクタのサンプル</span><span class="sxs-lookup"><span data-stu-id="56a9b-232">Generic connectors sample</span></span> |<span data-ttu-id="56a9b-233">Webhook をサポートする任意のシステム用にカスタマイズしやすい汎用コネクタのサンプル コード。</span><span class="sxs-lookup"><span data-stu-id="56a9b-233">Sample code for a generic connector that is easy to customize for any system that supports webhooks.</span></span>|  | [<span data-ttu-id="56a9b-234">View</span><span class="sxs-lookup"><span data-stu-id="56a9b-234">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a><span data-ttu-id="56a9b-235">関連項目</span><span class="sxs-lookup"><span data-stu-id="56a9b-235">See also</span></span>

* [<span data-ttu-id="56a9b-236">メッセージを作成して送信する</span><span class="sxs-lookup"><span data-stu-id="56a9b-236">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
* [<span data-ttu-id="56a9b-237">受信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="56a9b-237">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="56a9b-238">Office 365 コネクタを作成する</span><span class="sxs-lookup"><span data-stu-id="56a9b-238">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
