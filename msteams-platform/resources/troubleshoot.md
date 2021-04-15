---
title: アプリのトラブルシューティング
description: Microsoft Teams 用アプリの構築中に問題やエラーのトラブルシューティングを行う
keywords: teams アプリ開発のトラブルシューティング
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: a870a19eac9295f841b44b3b0364c46ffbc2d1d5
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696508"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a><span data-ttu-id="c7e57-104">Microsoft Teams アプリのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="c7e57-104">Troubleshoot your Microsoft Teams app</span></span>

## <a name="troubleshooting-tabs"></a><span data-ttu-id="c7e57-105">タブのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="c7e57-105">Troubleshooting tabs</span></span>

### <a name="accessing-the-devtools"></a><span data-ttu-id="c7e57-106">DevTools へのアクセス</span><span class="sxs-lookup"><span data-stu-id="c7e57-106">Accessing the DevTools</span></span>

<span data-ttu-id="c7e57-107">ブラウザーで F12 (Windows) または Command-Option-I (MacOS の場合) を押すのと同様のエクスペリエンスを得る場合は、Teams クライアントで [DevTools](~/tabs/how-to/developer-tools.md) を開きます。</span><span class="sxs-lookup"><span data-stu-id="c7e57-107">You can open [DevTools in the Teams client](~/tabs/how-to/developer-tools.md) for a similar experience as pressing F12 (on Windows) or Command-Option-I (on MacOS) in a browser.</span></span>

### <a name="blank-tab-screen"></a><span data-ttu-id="c7e57-108">空白のタブ画面</span><span class="sxs-lookup"><span data-stu-id="c7e57-108">Blank tab screen</span></span>

<span data-ttu-id="c7e57-109">タブ ビューにコンテンツが表示されない場合は、次の可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-109">If you are not seeing your content in the tab view, it could be:</span></span>

* <span data-ttu-id="c7e57-110">コンテンツは、 に表示できません `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="c7e57-110">your content cannot be displayed in an `<iframe>`.</span></span>
* <span data-ttu-id="c7e57-111">コンテンツ ドメインがマニフェストの [validDomains リスト](~/resources/schema/manifest-schema.md#validdomains) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="c7e57-111">the content domain is not in the [validDomains](~/resources/schema/manifest-schema.md#validdomains) list in the manifest.</span></span>

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a><span data-ttu-id="c7e57-112">設定ダイアログで [保存] ボタンが有効になっていない</span><span class="sxs-lookup"><span data-stu-id="c7e57-112">The Save button isn't enabled on the settings dialog</span></span>

<span data-ttu-id="c7e57-113">ユーザーが入力を `microsoftTeams.settings.setValidityState(true)` 受け取った後、または設定ページで必要なすべてのデータを選択して保存ボタンを有効にしたら、必ず呼び出してください。</span><span class="sxs-lookup"><span data-stu-id="c7e57-113">Be sure to call `microsoftTeams.settings.setValidityState(true)` once the user has input or selected all required data on your settings page to enable the save button.</span></span>

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a><span data-ttu-id="c7e57-114">[保存] ボタンを選択すると、タブ設定を保存できません。</span><span class="sxs-lookup"><span data-stu-id="c7e57-114">After selecting the Save button, the tab settings cannot be saved</span></span>

<span data-ttu-id="c7e57-115">タブを追加するときに、保存ボタンをクリックしたが、設定を保存できないことを示すエラー メッセージが表示された場合、問題は次の 2 つのクラスの 1 つになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-115">When adding a tab, if you click the save buttons but are presented with an error message indicating the settings cannot be saved, the problem could be one of two classes of issues:</span></span>

* <span data-ttu-id="c7e57-116">成功の保存メッセージは受信されません。</span><span class="sxs-lookup"><span data-stu-id="c7e57-116">The save success message was never received.</span></span> <span data-ttu-id="c7e57-117">保存ハンドラーが使用して登録されている場合 `microsoftTeams.settings.registerOnSaveHandler(handler)` 、コールバックは呼び出す必要があります `saveEvent.notifySuccess()` 。</span><span class="sxs-lookup"><span data-stu-id="c7e57-117">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler(handler)`, the callback must call `saveEvent.notifySuccess()`.</span></span> <span data-ttu-id="c7e57-118">コールバックが 30 秒以内にこれを呼び出したり、代わりに呼び出しを行わない場合は、 `saveEvent.notifyFailure(reason)` このエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c7e57-118">If the callback doesn't call this within 30 seconds or calls `saveEvent.notifyFailure(reason)` instead, this error will be shown.</span></span>

* <span data-ttu-id="c7e57-119">保存ハンドラーが登録されていない場合、ユーザーが [保存] ボタンを選択すると、すぐに `saveEvent.notifySuccess()` 呼び出しが自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="c7e57-119">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the save button.</span></span>

* <span data-ttu-id="c7e57-120">指定された設定が無効でした。</span><span class="sxs-lookup"><span data-stu-id="c7e57-120">The provided settings were invalid.</span></span> <span data-ttu-id="c7e57-121">設定を保存できないもう 1 つの理由は、呼び出しが無効な設定オブジェクトを提供した場合、または呼び出しが行われた `microsoftTeams.setSettings(settings)` のではない場合です。</span><span class="sxs-lookup"><span data-stu-id="c7e57-121">The other reason the settings may not be saved is if the call to `microsoftTeams.setSettings(settings)` provided an invalid settings object, or the call wasn't made at all.</span></span> <span data-ttu-id="c7e57-122">次のセクション「settings オブジェクトに関する一般的な問題」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7e57-122">See the next section, Common problems with the settings object.</span></span>

### <a name="common-problems-with-the-settings-object"></a><span data-ttu-id="c7e57-123">settings オブジェクトに関する一般的な問題</span><span class="sxs-lookup"><span data-stu-id="c7e57-123">Common problems with the settings object</span></span>

* <span data-ttu-id="c7e57-124">`settings.entityId` が見つからない。</span><span class="sxs-lookup"><span data-stu-id="c7e57-124">`settings.entityId` is missing.</span></span> <span data-ttu-id="c7e57-125">通常、このフィールドには、定義される年ごとに 1 が指定されます。</span><span class="sxs-lookup"><span data-stu-id="c7e57-125">This field is required.</span></span>
* <span data-ttu-id="c7e57-126">`settings.contentUrl` が見つからない。</span><span class="sxs-lookup"><span data-stu-id="c7e57-126">`settings.contentUrl` is missing.</span></span> <span data-ttu-id="c7e57-127">通常、このフィールドには、定義される年ごとに 1 が指定されます。</span><span class="sxs-lookup"><span data-stu-id="c7e57-127">This field is required.</span></span>
* <span data-ttu-id="c7e57-128">`settings.contentUrl` または省略可能 `settings.removeUrl` な 、 `settings.websiteUrl` または指定されているが無効です。</span><span class="sxs-lookup"><span data-stu-id="c7e57-128">`settings.contentUrl` or the optional `settings.removeUrl`, or `settings.websiteUrl` are provided but not valid.</span></span> <span data-ttu-id="c7e57-129">URL は HTTPS を使用する必要があります。また、設定ページと同じドメインか、マニフェストの一覧で指定する必要 `validDomains` があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-129">The URLs must use HTTPS and also must either be the same domain as the settings page or specified in the manifest's `validDomains` list.</span></span>

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a><span data-ttu-id="c7e57-130">ユーザーを認証できない、またはタブに認証プロバイダーを表示できない</span><span class="sxs-lookup"><span data-stu-id="c7e57-130">Can't authenticate the user or display your auth provider in your tab</span></span>

<span data-ttu-id="c7e57-131">サイレント認証を行う場合をしない限り、Microsoft Teams JavaScript クライアント SDK によって提供される認証プロセス [に従う必要があります](/javascript/api/overview/msteams-client.md)。</span><span class="sxs-lookup"><span data-stu-id="c7e57-131">Unless you are doing silent authentication, you must follow the authentication process provided by the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client.md).</span></span>

> [!NOTE]
><span data-ttu-id="c7e57-132">ドメインで開始および終了するには、すべての認証フローが必要です。これはマニフェストのオブジェクトに一 `validDomains` 覧表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-132">We require all authentication flow to start and end on your domain, which must be listed in the `validDomains` object in your manifest.</span></span>

<span data-ttu-id="c7e57-133">認証の詳細については、「ユーザーの認証 [」を参照してください](~/concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="c7e57-133">For more information about authentication, please see [Authenticate a user](~/concepts/authentication/authentication.md).</span></span>

### <a name="static-tabs-not-showing-up"></a><span data-ttu-id="c7e57-134">静的タブが表示されない</span><span class="sxs-lookup"><span data-stu-id="c7e57-134">Static tabs not showing up</span></span>

<span data-ttu-id="c7e57-135">新しい静的タブまたは更新された静的タブを使用して既存のボット アプリを更新すると、個人のチャット会話からアプリにアクセスするときにタブの変更が表示されないという既知の問題があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-135">There is a known issue where updating an existing bot app with a new or updated static tab will not show that tab change when accessing the app from a personal chat conversation.</span></span>  <span data-ttu-id="c7e57-136">変更を確認するには、新しいユーザーまたはテスト インスタンスでテストするか、アプリ のフライアウトからボットにアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-136">To see the change, you should test on a new user or test instance, or access the bot from the Apps flyout.</span></span>

## <a name="troubleshooting-bots"></a><span data-ttu-id="c7e57-137">ボットのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="c7e57-137">Troubleshooting bots</span></span>

### <a name="cant-add-my-bot"></a><span data-ttu-id="c7e57-138">ボットを追加できない</span><span class="sxs-lookup"><span data-stu-id="c7e57-138">Can't add my bot</span></span>

<span data-ttu-id="c7e57-139">エンド ユーザーが読み込むには、Office 365 テナント管理者がアプリを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-139">Apps must be enabled by the Office 365 tenant admin for them to be loaded by end users.</span></span> <span data-ttu-id="c7e57-140">場合によっては、Office 365 テナントに複数の SKU が関連付けられている可能性があります。ボットが任意で動作するには、すべての SKU で有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-140">Note that in some cases, the Office 365 tenant might have multiple SKUs associated with it, and for bots to work in any, they must be enabled in all SKUs.</span></span> <span data-ttu-id="c7e57-141">詳細 [については、「prepare your Office 365 テナント](~/concepts/build-and-test/prepare-your-o365-tenant.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7e57-141">See [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for more information.</span></span>

### <a name="cant-add-bot-as-a-member-of-a-team"></a><span data-ttu-id="c7e57-142">チームのメンバーとしてボットを追加できない</span><span class="sxs-lookup"><span data-stu-id="c7e57-142">Can't add bot as a member of a team</span></span>

<span data-ttu-id="c7e57-143">ボットは、そのチームのチャネル内でアクセスできる前に、まずチームにアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-143">Bots must first be upload into a team before it is accessible within any channel of that team.</span></span> <span data-ttu-id="c7e57-144">このプロセス [の詳細については、「チームでのアプリのアップロード](~/concepts/deploy-and-publish/apps-upload.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c7e57-144">Please review [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for more information on this process.</span></span>

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a><span data-ttu-id="c7e57-145">ボットがチャネルでメッセージを受け取らない</span><span class="sxs-lookup"><span data-stu-id="c7e57-145">My bot doesn't get my message in a channel</span></span>

<span data-ttu-id="c7e57-146">チャネル内のボットは、以前のボット メッセージに返信している場合@mentionedメッセージを明示的に受信した場合にのみメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="c7e57-146">Bots in channels receive messages only when they are explicitly @mentioned, even if you are replying to a previous bot message.</span></span> <span data-ttu-id="c7e57-147">メッセージにボット名が表示されない唯一の例外は、ボットが最初に送信した CardAction の結果としてアクションを受信 `imBack` した場合です。</span><span class="sxs-lookup"><span data-stu-id="c7e57-147">The only exception where you might not see the bot name in a message is if the bot receives an `imBack` action as a result of a CardAction that it originally sent.</span></span>

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a><span data-ttu-id="c7e57-148">チャネルで自分のコマンドをボットが理解していない</span><span class="sxs-lookup"><span data-stu-id="c7e57-148">My bot doesn't understand my commands when in a channel</span></span>

<span data-ttu-id="c7e57-149">チャネル内のボットはメッセージを受信する@mentioned、チャネルで受信するメッセージはすべてテキスト フィールドに@mention含まれます。</span><span class="sxs-lookup"><span data-stu-id="c7e57-149">Because bots in channels only receive messages when they are @mentioned, all messages that your bot receives in a channel include that @mention in the text field.</span></span> <span data-ttu-id="c7e57-150">解析ロジックに渡す前に、ボット名自体をすべての受信テキスト メッセージから取り除くのがベスト プラクティスです。</span><span class="sxs-lookup"><span data-stu-id="c7e57-150">It is a best practice to strip the bot name itself out of all incoming text messages before passing along to your parsing logic.</span></span> <span data-ttu-id="c7e57-151">この [ケースを処理](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) する方法に関するヒントについては、メンションを確認してください。</span><span class="sxs-lookup"><span data-stu-id="c7e57-151">Review [mentions](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) for tips on how to handle this case.</span></span>

## <a name="issues-with-packaging-and-uploading"></a><span data-ttu-id="c7e57-152">パッケージ化とアップロードに関する問題</span><span class="sxs-lookup"><span data-stu-id="c7e57-152">Issues with packaging and uploading</span></span>

### <a name="error-while-reading-manifestjson"></a><span data-ttu-id="c7e57-153">読み取り中のエラーmanifest.jsオン</span><span class="sxs-lookup"><span data-stu-id="c7e57-153">Error while reading manifest.json</span></span>

<span data-ttu-id="c7e57-154">ほとんどのマニフェスト エラーは、特定のフィールドが見つからないか無効かを示すヒントを提供します。</span><span class="sxs-lookup"><span data-stu-id="c7e57-154">Most  manifest errors will provide a hint at what specific field is missing or invalid.</span></span> <span data-ttu-id="c7e57-155">ただし、JSON ファイルを JSON として全く読み取りできない場合は、この汎用エラー メッセージが使用されます。</span><span class="sxs-lookup"><span data-stu-id="c7e57-155">However, if the JSON file cannot be read as JSON at all, this generic error message is used.</span></span>

<span data-ttu-id="c7e57-156">マニフェストの読み取りエラーの一般的な理由:</span><span class="sxs-lookup"><span data-stu-id="c7e57-156">Common reasons for manifest read errors:</span></span>

* <span data-ttu-id="c7e57-157">JSON が無効です。</span><span class="sxs-lookup"><span data-stu-id="c7e57-157">Invalid JSON.</span></span> <span data-ttu-id="c7e57-158">JSON 構文を自動的に検証[Visual Studioコード](https://code.visualstudio.com)Visual Studio [](https://www.visualstudio.com/vs/) IDE を使用します。</span><span class="sxs-lookup"><span data-stu-id="c7e57-158">Use an IDE such as [Visual Studio Code](https://code.visualstudio.com) or [Visual Studio](https://www.visualstudio.com/vs/) that automatically validates the JSON syntax.</span></span>
* <span data-ttu-id="c7e57-159">エンコードの問題。</span><span class="sxs-lookup"><span data-stu-id="c7e57-159">Encoding issues.</span></span> <span data-ttu-id="c7e57-160">ファイルUTF-8にmanifest.js *を使用* します。</span><span class="sxs-lookup"><span data-stu-id="c7e57-160">Use UTF-8 for the *manifest.json* file.</span></span> <span data-ttu-id="c7e57-161">その他のエンコード (特に BOM を使用) は読み取り可能ではない場合があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-161">Other encodings, specifically with the BOM, may not be readable.</span></span>
* <span data-ttu-id="c7e57-162">不正な形式の .zip パッケージ。</span><span class="sxs-lookup"><span data-stu-id="c7e57-162">Malformed .zip package.</span></span> <span data-ttu-id="c7e57-163">ファイル *manifest.jsは* 、.zip ファイルのトップ レベルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-163">The *manifest.json* file must be at the top level of the .zip file.</span></span> <span data-ttu-id="c7e57-164">既定の Mac ファイル圧縮では、サブディレクトリにmanifest.jsがオンになる可能性があり、Microsoft Teams では正しく読み込まれなかねない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="c7e57-164">Note that default Mac file compression might place the *manifest.json* in a subdirectory, which will not properly load in Microsoft Teams.</span></span>

### <a name="another-extension-with-same-id-exists"></a><span data-ttu-id="c7e57-165">同じ ID を持つ別の拡張機能が存在する</span><span class="sxs-lookup"><span data-stu-id="c7e57-165">Another extension with same ID exists</span></span>

<span data-ttu-id="c7e57-166">同じ ID で更新されたパッケージを再アップロードする場合は、[アップロード] ボタンではなく、タブのテーブル行の末尾にある [置換] アイコン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="c7e57-166">If you're attempting to re-upload an updated package with the same ID, choose the **Replace** icon at the end of the tab's table row rather than the **Upload** button.</span></span>

<span data-ttu-id="c7e57-167">更新されたパッケージを再アップロードしない場合は、ID が一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7e57-167">If you're not re-uploading an updated package, ensure that the ID is unique.</span></span>
