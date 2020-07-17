---
title: Office 365 コネクタ
description: Microsoft Teams で Office 365 コネクタを使い始める方法について説明します。
keywords: Teams o365 コネクタ
ms.date: 04/19/2019
ms.openlocfilehash: 9c89463830d46512e622dcf4c256a867d419de83
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137655"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="05e77-104">Microsoft Teams 用 Office 365 コネクタの作成</span><span class="sxs-lookup"><span data-stu-id="05e77-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="05e77-105">Microsoft Teams アプリを使用すると、既存の Office 365 コネクタを追加したり、Microsoft Teams に含める新しい Office コネクタを作成したりできます。</span><span class="sxs-lookup"><span data-stu-id="05e77-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="05e77-106">詳細については[、「独自のコネクタを作成](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="05e77-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="05e77-107">Teams アプリにコネクタを追加する</span><span class="sxs-lookup"><span data-stu-id="05e77-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="05e77-108">登録済みのコネクタを Teams アプリ パッケージの一部として配布できます。</span><span class="sxs-lookup"><span data-stu-id="05e77-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="05e77-109">スタンドアロンソリューションとして、または Teams で利用できるいくつかの[機能](~/concepts/extensibility-points.md)の1つとして、appsource の提出の一環として、コネクタを[パッケージ化](~/concepts/build-and-test/apps-package.md)して[発行](~/concepts/deploy-and-publish/apps-publish.md)することができます。また、teams 内でアップロードするために直接ユーザーに提供することもできます。</span><span class="sxs-lookup"><span data-stu-id="05e77-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="05e77-110">コネクタを配布するには、[コネクタ開発者ダッシュボード](https://outlook.office.com/connectors/home/login/#/publish)を使用して登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="05e77-111">既定では、コネクタが登録されると、そのコネクタは、それらをサポートするすべての Office 365 製品 (Outlook と Teams を含む) で動作していると見なされます。</span><span class="sxs-lookup"><span data-stu-id="05e77-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="05e77-112">それ以外の_場合は、_ microsoft teams でのみ動作するコネクタを作成する必要がある場合は、 [microsoft Teams アプリの提出](mailto:teamsubm@microsoft.com)に直接お問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="05e77-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05e77-113">コネクタ開発者ダッシュボードで [**保存**] を選択すると、コネクタが登録されます。</span><span class="sxs-lookup"><span data-stu-id="05e77-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="05e77-114">AppSource でコネクタを公開する場合は、「 [Microsoft Teams アプリを AppSource に発行](~/concepts/deploy-and-publish/apps-publish.md)する」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="05e77-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="05e77-115">アプリを AppSource で公開せず、組織に直接配布するだけではなく、[組織に公開](#publish-connectors-for-your-organization)することもできます。</span><span class="sxs-lookup"><span data-stu-id="05e77-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="05e77-116">組織への発行のみを希望する場合は、コネクタのダッシュボードで、これ以上の操作は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="05e77-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="05e77-117">構成作業の統合</span><span class="sxs-lookup"><span data-stu-id="05e77-117">Integrating the configuration experience</span></span>

<span data-ttu-id="05e77-118">ユーザーは、Teams クライアントを離れることなく、コネクタ構成作業全体を完了します。</span><span class="sxs-lookup"><span data-stu-id="05e77-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="05e77-119">この操作を実現するために、Teams は構成ページを iframe 内に直接埋め込みます。</span><span class="sxs-lookup"><span data-stu-id="05e77-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="05e77-120">操作の順序は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="05e77-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="05e77-121">ユーザーがコネクタをクリックして、構成プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="05e77-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="05e77-122">Teams は、構成の操作を行に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="05e77-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="05e77-123">ユーザーは、web experience と対話して構成を完了します。</span><span class="sxs-lookup"><span data-stu-id="05e77-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="05e77-124">ユーザーが [保存] を押すと、コード内でコールバックがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="05e77-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="05e77-125">コードでは、webhook 設定 (以下に記載) を取得することによって、save イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="05e77-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="05e77-126">コードでは、後でイベントを post するために webhook を格納する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="05e77-127">既存の web 構成機能を再利用するか、Teams で特別にホストされる個別のバージョンを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="05e77-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="05e77-128">コードは次のようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-128">Your code should:</span></span>

1. <span data-ttu-id="05e77-129">Microsoft Teams JavaScript SDK を含めます。</span><span class="sxs-lookup"><span data-stu-id="05e77-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="05e77-130">これにより、コードは、現在のユーザー/チャネル/チームコンテキストを取得し、認証フローを開始するなどの一般的な操作を実行するための Api にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="05e77-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="05e77-131">`microsoftTeams.initialize()` を呼び出して SDK を初期化します。</span><span class="sxs-lookup"><span data-stu-id="05e77-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="05e77-132">`microsoftTeams.settings.setValidityState(true)`[保存] ボタンを有効にする場合に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="05e77-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="05e77-133">これは、選択範囲またはフィールドの更新など、有効なユーザー入力に対する応答として実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="05e77-134">`microsoftTeams.settings.registerOnSaveHandler()`ユーザーが [保存] をクリックしたときに呼び出されるイベントハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="05e77-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="05e77-135">`microsoftTeams.settings.setSettings()`を呼び出して、コネクタの設定を保存します。</span><span class="sxs-lookup"><span data-stu-id="05e77-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="05e77-136">ここに保存される内容は、ユーザーがコネクタの既存の構成を更新しようとした場合に、[構成] ダイアログに表示される内容にもなります。</span><span class="sxs-lookup"><span data-stu-id="05e77-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="05e77-137">`microsoftTeams.settings.getSettings()`URL 自体を含む webhook プロパティをフェッチする呼び出し。</span><span class="sxs-lookup"><span data-stu-id="05e77-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="05e77-138">Save イベントの実行時に加えて、この関数は、ページが最初に読み込まれたときに再構成したときにも呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="05e77-139">オプション`microsoftTeams.settings.registerOnRemoveHandler()`ユーザーがコネクタを削除したときに呼び出されるイベントハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="05e77-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="05e77-140">このイベントは、サービスにクリーンアップアクションを実行する機会を提供します。</span><span class="sxs-lookup"><span data-stu-id="05e77-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

#### <a name="getsettings-response-properties"></a><span data-ttu-id="05e77-141">`GetSettings()`応答のプロパティ</span><span class="sxs-lookup"><span data-stu-id="05e77-141">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="05e77-142">この呼び出しによって返されるパラメーター `getSettings` は、このメソッドをタブから呼び出した場合とは異なり、[ここ](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest)に記載されているものとは異なります。</span><span class="sxs-lookup"><span data-stu-id="05e77-142">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest).</span></span>

| <span data-ttu-id="05e77-143">パラメーター</span><span class="sxs-lookup"><span data-stu-id="05e77-143">Parameter</span></span>   | <span data-ttu-id="05e77-144">詳細</span><span class="sxs-lookup"><span data-stu-id="05e77-144">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="05e77-145">呼び出し時にコードによって設定されたエンティティ ID `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="05e77-145">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="05e77-146">呼び出し時にコードによって設定された構成名 `setSettings()` 。</span><span class="sxs-lookup"><span data-stu-id="05e77-146">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="05e77-147">呼び出し時にコードによって設定された、構成ページの URL`setSettings()`</span><span class="sxs-lookup"><span data-stu-id="05e77-147">The URL of the configuration page, as set by your code when calling `setSettings()`</span></span> |
| `webhookUrl` | <span data-ttu-id="05e77-148">このコネクタ用に作成された webhook URL。</span><span class="sxs-lookup"><span data-stu-id="05e77-148">The webhook URL created for this connector.</span></span> <span data-ttu-id="05e77-149">Webhook URL を保持し、それを使用して、カードをチャネルに送信するように構造化された JSON をポストします。</span><span class="sxs-lookup"><span data-stu-id="05e77-149">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="05e77-150">は、アプリケーションが正常に返される場合にのみ返されます。</span><span class="sxs-lookup"><span data-stu-id="05e77-150">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="05e77-151">返される値には、Office 365 メール、Office 365 グループ、Microsoft Teams のそれぞれに対応する `mail`、`groups`、`teams` を指定できます。</span><span class="sxs-lookup"><span data-stu-id="05e77-151">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="05e77-152">これは、コネクタのセットアップを開始した Office 365 ユーザーに対応する一意の id です。</span><span class="sxs-lookup"><span data-stu-id="05e77-152">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="05e77-153">セキュリティで保護する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-153">It should be secured.</span></span> <span data-ttu-id="05e77-154">この値は、構成をセットアップした Office 365 内のユーザーをサービス内のユーザーに関連付けるために使用できます。</span><span class="sxs-lookup"><span data-stu-id="05e77-154">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="05e77-155">ページの読み込みの一環としてユーザーを認証する必要がある場合は、ページが埋め込まれているときにログインを統合する方法の詳細については、[このリンク](~/tabs/how-to/authentication/auth-flow-tab.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="05e77-155">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="05e77-156">クライアント間の互換性に関する理由から、コードは、 `microsoftTeams.authentication.registerAuthenticationHandlers()` URL と、成功/失敗のコールバックメソッドを呼び出してから呼び出す必要があり `authenticate()` ます。</span><span class="sxs-lookup"><span data-stu-id="05e77-156">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="05e77-157">編集の処理</span><span class="sxs-lookup"><span data-stu-id="05e77-157">Handling edits</span></span>

<span data-ttu-id="05e77-158">コードは、既存のコネクタ構成を編集するために戻るユーザーを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-158">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="05e77-159">これを行うには、 `microsoftTeams.settings.setSettings()` 次のパラメーターを使用して、初期構成中にを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="05e77-159">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="05e77-160">`entityId`は、サービスによって認識されるカスタム ID であり、ユーザーが構成した内容を表します。</span><span class="sxs-lookup"><span data-stu-id="05e77-160">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="05e77-161">`configName`は、構成コードが取得できるフレンドリ名です。</span><span class="sxs-lookup"><span data-stu-id="05e77-161">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="05e77-162">`contentUrl`は、ユーザーが既存のコネクタ構成を編集したときに読み込まれるカスタム URL です。</span><span class="sxs-lookup"><span data-stu-id="05e77-162">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="05e77-163">この URL を使用して、コードが編集ケースを簡単に処理できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="05e77-163">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="05e77-164">通常、この呼び出しは、save イベントハンドラーの一部として行われます。</span><span class="sxs-lookup"><span data-stu-id="05e77-164">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="05e77-165">次に、 `contentUrl` 上記のコードが読み込まれたときに、 `getSettings()` 設定またはフォームを構成 UI に事前に設定するためのコードを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-165">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="05e77-166">削除の処理</span><span class="sxs-lookup"><span data-stu-id="05e77-166">Handling removals</span></span>

<span data-ttu-id="05e77-167">ユーザーが既存のコネクタ構成を削除したときに、必要に応じてイベントハンドラーを実行することができます。</span><span class="sxs-lookup"><span data-stu-id="05e77-167">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="05e77-168">このハンドラーは、を呼び出して登録し `microsoftTeams.settings.registerOnRemoveHandler()` ます。</span><span class="sxs-lookup"><span data-stu-id="05e77-168">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="05e77-169">このハンドラーは、データベースからエントリを削除するなど、クリーンアップ操作を実行するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="05e77-169">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="05e77-170">マニフェストにコネクタを含める</span><span class="sxs-lookup"><span data-stu-id="05e77-170">Including the Connector in your Manifest</span></span>

<span data-ttu-id="05e77-171">自動生成された Teams アプリのマニフェストは、ポータルからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="05e77-171">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="05e77-172">ただし、これを使用してアプリをテストまたは発行するには、次の操作を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-172">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="05e77-173">「[アイコン](~/concepts/build-and-test/apps-package.md#icons)」の説明に従い、アイコンを 2 つ含めます。</span><span class="sxs-lookup"><span data-stu-id="05e77-173">Include two icons, following the instructions in [Icons](~/concepts/build-and-test/apps-package.md#icons).</span></span>
- <span data-ttu-id="05e77-174">マニフェストの `icons` の部分を変更し、アイコンの URL ではなくアイコンのファイル名を参照するようにします。</span><span class="sxs-lookup"><span data-stu-id="05e77-174">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="05e77-175">次の manifest.json ファイルには、アプリをテストして送信するために必要な基本的な要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="05e77-175">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="05e77-176">次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="05e77-176">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="05e77-177">コネクタを使用した manifest.json の例</span><span class="sxs-lookup"><span data-stu-id="05e77-177">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

## <a name="testing-your-connector"></a><span data-ttu-id="05e77-178">コネクタのテスト</span><span class="sxs-lookup"><span data-stu-id="05e77-178">Testing your Connector</span></span>

<span data-ttu-id="05e77-179">コネクタをテストするには、他のアプリと同じ方法でコネクタをチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="05e77-179">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="05e77-180">(前のセクションの指示に従って変更された) コネクタ開発者ダッシュボードからのマニフェスト ファイルと 2 つのアイコン ファイルを使用して .zip パッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="05e77-180">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="05e77-181">アプリをアップロードしたら、任意のチャネルからコネクタ リストを開きます。</span><span class="sxs-lookup"><span data-stu-id="05e77-181">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="05e77-182">一番下までスクロールして、アプリが [**アップロード済み**] セクションに表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="05e77-182">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![コネクタ ダイアログ ボックスの [アップロード済み] セクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="05e77-184">構成機能を起動できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="05e77-184">You can now launch the configuration experience.</span></span> <span data-ttu-id="05e77-185">このフローは、Microsoft Teams 内でホストされる環境として全面的に発生することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="05e77-185">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="05e77-186">アクションが正常に動作していることを確認するには `HttpPOST` 、[コネクタにメッセージを送信](~/webhooks-and-connectors/how-to/connectors-using.md)します。</span><span class="sxs-lookup"><span data-stu-id="05e77-186">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="05e77-187">組織の公開コネクタ</span><span class="sxs-lookup"><span data-stu-id="05e77-187">Publish Connectors for your organization</span></span>

<span data-ttu-id="05e77-188">場合によっては、コネクタアプリを公開する AppSource/Store に公開する必要はありませんが、組織内のユーザーのみが使用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="05e77-188">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="05e77-189">そのような場合は、カスタムコネクタアプリを[組織のアプリカタログ](~/concepts/deploy-and-publish/apps-publish.md)にアップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="05e77-189">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="05e77-190">このようにすると、コネクタアプリはその組織のみが使用できるようになり、パブリックストアにコネクタを公開する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="05e77-190">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="05e77-191">アプリパッケージをアップロードした後、チーム内でコネクタを構成して使用するには、次の手順を実行して組織のアプリカタログからインストールできます。</span><span class="sxs-lookup"><span data-stu-id="05e77-191">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="05e77-192">左端の垂直ナビゲーションバーから [アプリ] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="05e77-192">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="05e77-193">[**アプリ**] ウィンドウで、[**コネクタ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="05e77-193">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="05e77-194">追加するコネクタを選択すると、ポップアップダイアログウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="05e77-194">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="05e77-195">[**チームバーに追加] を**選択します。</span><span class="sxs-lookup"><span data-stu-id="05e77-195">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="05e77-196">次のダイアログウィンドウで、チームまたはチャネルの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="05e77-196">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="05e77-197">ダイアログウィンドウの右下隅にあるコネクタバーの**設定**を選択します。</span><span class="sxs-lookup"><span data-stu-id="05e77-197">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="05e77-198">このコネクタは、「 &#9679;&#9679;&#9679; =」の「> その*他のオプション*コネクタのすべてのコネクタ」のセクションで使用でき  =>  *Connectors*  =>  *All*  =>  *Connectors for you team*ます。</span><span class="sxs-lookup"><span data-stu-id="05e77-198">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="05e77-199">このセクションまでスクロールするか、コネクタアプリを検索することによって移動できます。</span><span class="sxs-lookup"><span data-stu-id="05e77-199">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="05e77-200">コネクタを構成または変更するには、[**構成**] バーを選択します。</span><span class="sxs-lookup"><span data-stu-id="05e77-200">To configure or modify the connector select the **Configure** bar.</span></span>
