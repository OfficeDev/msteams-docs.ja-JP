---
title: アプリのトラブルシューティング
description: Microsoft Teams 用アプリの作成中に発生する問題やエラーのトラブルシューティング
keywords: teams アプリ開発のトラブルシューティング
ms.date: 07/09/2018
ms.openlocfilehash: f7fe42e7c1f3ff2c4d8d1cbe81ed8f71e6c04384
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674646"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a><span data-ttu-id="05281-104">Microsoft Teams アプリのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="05281-104">Troubleshoot your Microsoft Teams app</span></span>

## <a name="troubleshooting-tabs"></a><span data-ttu-id="05281-105">トラブルシューティングのタブ</span><span class="sxs-lookup"><span data-stu-id="05281-105">Troubleshooting tabs</span></span>

### <a name="accessing-the-devtools"></a><span data-ttu-id="05281-106">DevTools へのアクセス</span><span class="sxs-lookup"><span data-stu-id="05281-106">Accessing the DevTools</span></span>

<span data-ttu-id="05281-107">[Teams クライアントで Devtools](~/tabs/how-to/developer-tools.md)を開くには、ブラウザーで F12 キー (Windows の場合) またはコマンドオプション-I (MacOS) を押した場合と同様の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="05281-107">You can open [DevTools in the Teams client](~/tabs/how-to/developer-tools.md) for a similar experience as pressing F12 (on Windows) or Command-Option-I (on MacOS) in a browser.</span></span>

### <a name="blank-tab-screen"></a><span data-ttu-id="05281-108">空白のタブ画面</span><span class="sxs-lookup"><span data-stu-id="05281-108">Blank tab screen</span></span>

<span data-ttu-id="05281-109">タブビューにコンテンツが表示されない場合は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="05281-109">If you are not seeing your content in the tab view, it could be:</span></span>

* <span data-ttu-id="05281-110">コンテンツをに表示することは`<iframe>`できません。</span><span class="sxs-lookup"><span data-stu-id="05281-110">your content cannot be displayed in an `<iframe>`.</span></span>
* <span data-ttu-id="05281-111">コンテンツドメインは、マニフェストの[Validdomains](~/resources/schema/manifest-schema.md#validdomains)リストに含まれていません。</span><span class="sxs-lookup"><span data-stu-id="05281-111">the content domain is not in the [validDomains](~/resources/schema/manifest-schema.md#validdomains) list in the manifest.</span></span>

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a><span data-ttu-id="05281-112">[設定] ダイアログボックスの [保存] ボタンが有効になっていない</span><span class="sxs-lookup"><span data-stu-id="05281-112">The Save button isn't enabled on the settings dialog</span></span>

<span data-ttu-id="05281-113">[保存] ボタン`microsoftTeams.settings.setValidityState(true)`を有効にするには、ユーザーが入力したか、または [設定] ページですべての必要なデータを選択した場合には、必ず通話してください。</span><span class="sxs-lookup"><span data-stu-id="05281-113">Be sure to call `microsoftTeams.settings.setValidityState(true)` once the user has input or selected all required data on your settings page to enable the save button.</span></span>

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a><span data-ttu-id="05281-114">[保存] ボタンを選択すると、タブの設定を保存できません。</span><span class="sxs-lookup"><span data-stu-id="05281-114">After selecting the Save button, the tab settings cannot be saved</span></span>

<span data-ttu-id="05281-115">タブを追加するときに、[保存] ボタンをクリックしても、設定を保存できないことを示すエラーメッセージが表示される場合は、次の2つのクラスのいずれかの問題が考えられます。</span><span class="sxs-lookup"><span data-stu-id="05281-115">When adding a tab, if you click the save buttons but are presented with an error message indicating the settings cannot be saved, the problem could be one of two classes of issues:</span></span>

* <span data-ttu-id="05281-116">保存成功メッセージは受信されませんでした。</span><span class="sxs-lookup"><span data-stu-id="05281-116">The save success message was never received.</span></span> <span data-ttu-id="05281-117">を使用して保存ハンドラーが`microsoftTeams.settings.registerOnSaveHandler(handler)`登録されている`saveEvent.notifySuccess()`場合、コールバックはを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-117">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler(handler)`, the callback must call `saveEvent.notifySuccess()`.</span></span> <span data-ttu-id="05281-118">このエラーは、コールバックが30秒以内に`saveEvent.notifyFailure(reason)` 、またはその代わりに呼び出しを行わない場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="05281-118">If the callback doesn't call this within 30 seconds or calls `saveEvent.notifyFailure(reason)` instead, this error will be shown.</span></span>

* <span data-ttu-id="05281-119">保存ハンドラーが登録されてい`saveEvent.notifySuccess()`ない場合は、ユーザーが [保存] ボタンを選択すると、その時点で通話が自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="05281-119">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the save button.</span></span>

* <span data-ttu-id="05281-120">指定された設定は無効です。</span><span class="sxs-lookup"><span data-stu-id="05281-120">The provided settings were invalid.</span></span> <span data-ttu-id="05281-121">その他の理由として、設定が無効な設定オブジェクト`microsoftTeams.setSettings(settings)`を呼び出した場合、または呼び出しが行われなかった場合は、設定が保存されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="05281-121">The other reason the settings may not be saved is if the call to `microsoftTeams.setSettings(settings)` provided an invalid settings object, or the call wasn't made at all.</span></span> <span data-ttu-id="05281-122">Settings オブジェクトの一般的な問題については、次のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="05281-122">See the next section, Common problems with the settings object.</span></span>

### <a name="common-problems-with-the-settings-object"></a><span data-ttu-id="05281-123">Settings オブジェクトの一般的な問題</span><span class="sxs-lookup"><span data-stu-id="05281-123">Common problems with the settings object</span></span>

* <span data-ttu-id="05281-124">`settings.entityId`がありません。</span><span class="sxs-lookup"><span data-stu-id="05281-124">`settings.entityId` is missing.</span></span> <span data-ttu-id="05281-125">通常、このフィールドには、定義される年ごとに 1 が指定されます。</span><span class="sxs-lookup"><span data-stu-id="05281-125">This field is required.</span></span>
* <span data-ttu-id="05281-126">`settings.contentUrl`がありません。</span><span class="sxs-lookup"><span data-stu-id="05281-126">`settings.contentUrl` is missing.</span></span> <span data-ttu-id="05281-127">通常、このフィールドには、定義される年ごとに 1 が指定されます。</span><span class="sxs-lookup"><span data-stu-id="05281-127">This field is required.</span></span>
* <span data-ttu-id="05281-128">`settings.contentUrl`またはオプション`settings.removeUrl` `settings.websiteUrl`ですが、有効ではありません。</span><span class="sxs-lookup"><span data-stu-id="05281-128">`settings.contentUrl` or the optional `settings.removeUrl`, or `settings.websiteUrl` are provided but not valid.</span></span> <span data-ttu-id="05281-129">Url は HTTPS を使用する必要があり、また、マニフェストの`validDomains`一覧で指定されているか、または設定ページと同じドメインである必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-129">The URLs must use HTTPS and also must either be the same domain as the settings page or specified in the manifest's `validDomains` list.</span></span>

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a><span data-ttu-id="05281-130">ユーザーを認証できないか、またはタブに認証プロバイダーが表示されない</span><span class="sxs-lookup"><span data-stu-id="05281-130">Can't authenticate the user or display your auth provider in your tab</span></span>

<span data-ttu-id="05281-131">サイレント認証を実行していない場合は、 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client.md)によって提供される認証プロセスに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-131">Unless you are doing silent authentication, you must follow the authentication process provided by the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client.md).</span></span>

> [!NOTE]
><span data-ttu-id="05281-132">すべての認証フローをドメインで開始および終了する必要があります。これはマニフェスト`validDomains`内のオブジェクトに記載されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-132">We require all authentication flow to start and end on your domain, which must be listed in the `validDomains` object in your manifest.</span></span>

<span data-ttu-id="05281-133">認証の詳細については、「[ユーザーの認証](~/concepts/authentication/authentication.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="05281-133">For more information about authentication, please see [Authenticate a user](~/concepts/authentication/authentication.md).</span></span>

### <a name="static-tabs-not-showing-up"></a><span data-ttu-id="05281-134">静的タブが表示されない</span><span class="sxs-lookup"><span data-stu-id="05281-134">Static tabs not showing up</span></span>

<span data-ttu-id="05281-135">新規または更新された静的なタブを使用して既存のボットアプリを更新すると、個人のチャット会話からアプリにアクセスしたときにそのタブの変更が表示されないという既知の問題があります。</span><span class="sxs-lookup"><span data-stu-id="05281-135">There is a known issue where updating an existing bot app with a new or updated static tab will not show that tab change when accessing the app from a personal chat conversation.</span></span>  <span data-ttu-id="05281-136">変更を確認するには、新しいユーザーまたはテストインスタンスでテストするか、アプリのポップアップから bot にアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-136">To see the change, you should test on a new user or test instance, or access the bot from the Apps flyout.</span></span>

## <a name="troubleshooting-bots"></a><span data-ttu-id="05281-137">ボットのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="05281-137">Troubleshooting bots</span></span>

### <a name="cant-add-my-bot"></a><span data-ttu-id="05281-138">Bot を追加できません</span><span class="sxs-lookup"><span data-stu-id="05281-138">Can't add my bot</span></span>

<span data-ttu-id="05281-139">アプリをエンドユーザーが読み込むには、Office 365 テナント管理者が有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-139">Apps must be enabled by the Office 365 tenant admin for them to be loaded by end users.</span></span> <span data-ttu-id="05281-140">場合によっては、Office 365 テナントに複数の Sku が関連付けられている可能性があります。また、bot がどのような場合でも機能するには、すべての Sku で有効になっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-140">Note that in some cases, the Office 365 tenant might have multiple SKUs associated with it, and for bots to work in any, they must be enabled in all SKUs.</span></span> <span data-ttu-id="05281-141">詳細については[、「Office 365 テナントの準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="05281-141">See [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for more information.</span></span>

### <a name="cant-add-bot-as-a-member-of-a-team"></a><span data-ttu-id="05281-142">Bot をチームのメンバーとして追加できません</span><span class="sxs-lookup"><span data-stu-id="05281-142">Can't add bot as a member of a team</span></span>

<span data-ttu-id="05281-143">そのチームのチャネル内でアクセスできるようにするには、最初に bot をチームにアップロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-143">Bots must first be upload into a team before it is accessible within any channel of that team.</span></span> <span data-ttu-id="05281-144">このプロセスの詳細については、「[チームでアプリをアップロードする」](~/concepts/deploy-and-publish/apps-upload.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="05281-144">Please review [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for more information on this process.</span></span>

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a><span data-ttu-id="05281-145">自分の bot がチャネルでメッセージを受信できない</span><span class="sxs-lookup"><span data-stu-id="05281-145">My bot doesn't get my message in a channel</span></span>

<span data-ttu-id="05281-146">チャネル内の bot は、前の bot メッセージに返信する場合でも、明示的に @mentioned ときにのみメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="05281-146">Bots in channels receive messages only when they are explicitly @mentioned, even if you are replying to a previous bot message.</span></span> <span data-ttu-id="05281-147">メッセージに bot 名が表示されない唯一の例外は、最初に送信した CardAction の結果として bot が`imBack`アクションを受け取った場合です。</span><span class="sxs-lookup"><span data-stu-id="05281-147">The only exception where you might not see the bot name in a message is if the bot receives an `imBack` action as a result of a CardAction that it originally sent.</span></span>

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a><span data-ttu-id="05281-148">自分の bot がチャネル内で自分のコマンドを理解していない</span><span class="sxs-lookup"><span data-stu-id="05281-148">My bot doesn't understand my commands when in a channel</span></span>

<span data-ttu-id="05281-149">チャネル内のボットは @mentioned 時にのみメッセージを受信するので、ボットがチャネル内で受信するすべてのメッセージには、テキストフィールドに @mention が含まれます。</span><span class="sxs-lookup"><span data-stu-id="05281-149">Because bots in channels only receive messages when they are @mentioned, all messages that your bot receives in a channel include that @mention in the text field.</span></span> <span data-ttu-id="05281-150">解析ロジックに渡す前に、すべての受信テキストメッセージから bot 名自体を削除することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="05281-150">It is a best practice to strip the bot name itself out of all incoming text messages before passing along to your parsing logic.</span></span> <span data-ttu-id="05281-151">このケースを処理する方法に関するヒントについては、[メンション](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions)を確認してください。</span><span class="sxs-lookup"><span data-stu-id="05281-151">Review [Mentions](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions) for tips on how to handle this case.</span></span>

## <a name="issues-with-packaging-and-uploading"></a><span data-ttu-id="05281-152">パッケージ化とアップロードに関する問題</span><span class="sxs-lookup"><span data-stu-id="05281-152">Issues with packaging and uploading</span></span>

### <a name="error-while-reading-manifestjson"></a><span data-ttu-id="05281-153">Manifest.xml の読み取り中にエラーが発生しました</span><span class="sxs-lookup"><span data-stu-id="05281-153">Error while reading manifest.json</span></span>

<span data-ttu-id="05281-154">ほとんどのマニフェストエラーは、不足している、または無効なフィールドに関するヒントを提供します。</span><span class="sxs-lookup"><span data-stu-id="05281-154">Most  manifest errors will provide a hint at what specific field is missing or invalid.</span></span> <span data-ttu-id="05281-155">ただし、JSON ファイルを JSON として読み取ることができない場合は、この一般的なエラーメッセージが使用されます。</span><span class="sxs-lookup"><span data-stu-id="05281-155">However, if the JSON file cannot be read as JSON at all, this generic error message is used.</span></span>

<span data-ttu-id="05281-156">マニフェストの読み取りエラーの一般的な理由:</span><span class="sxs-lookup"><span data-stu-id="05281-156">Common reasons for manifest read errors:</span></span>

* <span data-ttu-id="05281-157">無効な JSON です。</span><span class="sxs-lookup"><span data-stu-id="05281-157">Invalid JSON.</span></span> <span data-ttu-id="05281-158">JSON 構文を自動的に検証する[Visual Studio Code](https://code.visualstudio.com)または[visual STUDIO](https://www.visualstudio.com/vs/)などの IDE を使用します。</span><span class="sxs-lookup"><span data-stu-id="05281-158">Use an IDE such as [Visual Studio Code](https://code.visualstudio.com) or [Visual Studio](https://www.visualstudio.com/vs/) that automatically validates the JSON syntax.</span></span>
* <span data-ttu-id="05281-159">エンコードの問題。</span><span class="sxs-lookup"><span data-stu-id="05281-159">Encoding issues.</span></span> <span data-ttu-id="05281-160">*Manifest.xml*ファイルには、utf-8 を使用します。</span><span class="sxs-lookup"><span data-stu-id="05281-160">Use UTF-8 for the *manifest.json* file.</span></span> <span data-ttu-id="05281-161">その他のエンコーディング (具体的には、BOM を含む) は読み取ることができない場合があります。</span><span class="sxs-lookup"><span data-stu-id="05281-161">Other encodings, specifically with the BOM, may not be readable.</span></span>
* <span data-ttu-id="05281-162">.Zip パッケージの形式が正しくない。</span><span class="sxs-lookup"><span data-stu-id="05281-162">Malformed .zip package.</span></span> <span data-ttu-id="05281-163">*Manifest.xml*ファイルは、.zip ファイルの最上位レベルにある必要があります。</span><span class="sxs-lookup"><span data-stu-id="05281-163">The *manifest.json* file must be at the top level of the .zip file.</span></span> <span data-ttu-id="05281-164">既定の Mac ファイル圧縮では、*マニフェスト*がサブディレクトリに配置される可能性があることに注意してください。これは、Microsoft Teams に適切に読み込まれません。</span><span class="sxs-lookup"><span data-stu-id="05281-164">Note that default Mac file compression might place the *manifest.json* in a subdirectory, which will not properly load in Microsoft Teams.</span></span>

### <a name="another-extension-with-same-id-exists"></a><span data-ttu-id="05281-165">同じ ID を持つ別の内線番号が存在します</span><span class="sxs-lookup"><span data-stu-id="05281-165">Another extension with same ID exists</span></span>

<span data-ttu-id="05281-166">同じ ID を持つ更新されたパッケージを再アップロードする場合は、[**アップロード**] ボタンではなく、タブの table 行の最後にある [**置換**] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="05281-166">If you're attempting to re-upload an updated package with the same ID, choose the **Replace** icon at the end of the tab's table row rather than the **Upload** button.</span></span>

<span data-ttu-id="05281-167">更新されたパッケージを再アップロードしない場合は、ID が一意であることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="05281-167">If you're not re-uploading an updated package, ensure that the ID is unique.</span></span>
