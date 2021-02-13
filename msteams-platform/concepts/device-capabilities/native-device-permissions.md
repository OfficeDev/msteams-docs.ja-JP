---
title: Microsoft Teams アプリのデバイスアクセス許可を要求する
keywords: Teams アプリ機能のアクセス許可
description: 通常はユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
ms.topic: how-to
ms.openlocfilehash: 0343754eacbb6088a3e44fa5df8ec90e3b10b076
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231611"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="7843d-104">Microsoft Teams アプリのデバイスアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="7843d-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="7843d-105">カメラ、マイク、位置情報などのネイティブ デバイス機能を使用して、Teams アプリを強化できます。</span><span class="sxs-lookup"><span data-stu-id="7843d-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="7843d-106">このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法について示します。</span><span class="sxs-lookup"><span data-stu-id="7843d-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="7843d-107">Microsoft Teams モバイル アプリにメディア機能を統合するには、「メディア機能の統合 [」を参照してください](mobile-camera-image-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="7843d-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="7843d-108">ネイティブ デバイスのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="7843d-108">Native device permissions</span></span>

<span data-ttu-id="7843d-109">ネイティブ デバイス機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7843d-109">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="7843d-110">デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリ構成で同様に動作します。</span><span class="sxs-lookup"><span data-stu-id="7843d-110">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="7843d-111">ユーザーがデバイスのアクセス許可を管理するには、Teams の設定の [アクセス許可] ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7843d-111">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="7843d-112">デバイスの機能にアクセスすることで、Teams プラットフォームで次のような豊富なエクスペリエンスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="7843d-112">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="7843d-113">画像をキャプチャして表示します。</span><span class="sxs-lookup"><span data-stu-id="7843d-113">Capture and view images.</span></span>
* <span data-ttu-id="7843d-114">短いビデオを録画して共有します。</span><span class="sxs-lookup"><span data-stu-id="7843d-114">Record and share short videos.</span></span>
* <span data-ttu-id="7843d-115">オーディオ メモを録音し、後で使用するために保存します。</span><span class="sxs-lookup"><span data-stu-id="7843d-115">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="7843d-116">ユーザーの場所情報を使用して、関連情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="7843d-116">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="7843d-117">アクセス デバイスのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="7843d-117">Access device permissions</span></span>

<span data-ttu-id="7843d-118">[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)は、Teams モバイル アプリがユーザーのデバイス[](#manage-permissions)のアクセス許可にアクセスし、より豊富なエクスペリエンスを構築するために必要なツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="7843d-118">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="7843d-119">これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用する機能について Teams に通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7843d-119">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="7843d-120">この更新プログラムでは、アプリが Teams デスクトップ クライアントで実行されている間にアクセス許可を要求できます。</span><span class="sxs-lookup"><span data-stu-id="7843d-120">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="7843d-121">現在、メディア機能に対する Microsoft Teams のサポートはモバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="7843d-121">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="7843d-122">権限の管理</span><span class="sxs-lookup"><span data-stu-id="7843d-122">Manage permissions</span></span>

<span data-ttu-id="7843d-123">ユーザーは、特定のアプリに対するアクセス許可を許可または拒否するを選択して、Teams の **設定でデバイス** のアクセス許可を管理できます。</span><span class="sxs-lookup"><span data-stu-id="7843d-123">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="7843d-124">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="7843d-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="7843d-125">Teams アプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="7843d-125">Open your Teams app.</span></span>
1. <span data-ttu-id="7843d-126">ウィンドウの右上隅にあるプロファイル アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="7843d-126">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="7843d-127">ドロップダウン **メニュー**  >  **から [設定の** アクセス許可] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7843d-127">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="7843d-128">目的の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="7843d-128">Select your desired settings.</span></span>

   ![デバイスのアクセス許可のデスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="7843d-130">モバイル</span><span class="sxs-lookup"><span data-stu-id="7843d-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="7843d-131">Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="7843d-131">Open Teams.</span></span>
1. <span data-ttu-id="7843d-132">[設定]**アプリの**  >  **アクセス許可に移動します**。</span><span class="sxs-lookup"><span data-stu-id="7843d-132">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="7843d-133">設定を選択する必要があるアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="7843d-133">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="7843d-134">目的の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="7843d-134">Select your desired settings.</span></span>

    ![デバイスのアクセス許可のモバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="7843d-136">アクセス許可を指定する</span><span class="sxs-lookup"><span data-stu-id="7843d-136">Specify permissions</span></span>

<span data-ttu-id="7843d-137">アプリケーションで使用する 5 つのプロパティの中から、次のプロパティを追加して指定することで、アプリ `manifest.json` `devicePermissions` を更新します。</span><span class="sxs-lookup"><span data-stu-id="7843d-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="7843d-138">各プロパティを使用すると、ユーザーに同意を求めるメッセージを表示できます。</span><span class="sxs-lookup"><span data-stu-id="7843d-138">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="7843d-139">プロパティ</span><span class="sxs-lookup"><span data-stu-id="7843d-139">Property</span></span>      | <span data-ttu-id="7843d-140">説明</span><span class="sxs-lookup"><span data-stu-id="7843d-140">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="7843d-141">media</span><span class="sxs-lookup"><span data-stu-id="7843d-141">media</span></span>         | <span data-ttu-id="7843d-142">カメラ、マイク、スピーカー、およびメディア ギャラリーへのアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="7843d-142">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="7843d-143">geolocation</span><span class="sxs-lookup"><span data-stu-id="7843d-143">geolocation</span></span>   | <span data-ttu-id="7843d-144">ユーザーの位置情報を返すアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="7843d-144">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="7843d-145">notifications</span><span class="sxs-lookup"><span data-stu-id="7843d-145">notifications</span></span> | <span data-ttu-id="7843d-146">ユーザー通知を送信するアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="7843d-146">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="7843d-147">midi</span><span class="sxs-lookup"><span data-stu-id="7843d-147">midi</span></span>          | <span data-ttu-id="7843d-148">デジタル 音楽機器から、Instrument Instrument Digital Interface (MIDI) 情報を送受信するためのアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="7843d-148">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="7843d-149">openExternal</span><span class="sxs-lookup"><span data-stu-id="7843d-149">openExternal</span></span>  | <span data-ttu-id="7843d-150">外部アプリケーションでリンクを開く権限。</span><span class="sxs-lookup"><span data-stu-id="7843d-150">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="7843d-151">アプリからアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="7843d-151">Check permissions from your app</span></span>

<span data-ttu-id="7843d-152">アプリ マニフェスト `devicePermissions` に追加した後、プロンプトを表示せずに **HTML5** アクセス許可 API を使用してアクセス許可を確認します。</span><span class="sxs-lookup"><span data-stu-id="7843d-152">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

``` Javascript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="7843d-153">Teams API を使用してデバイスのアクセス許可を取得する</span><span class="sxs-lookup"><span data-stu-id="7843d-153">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="7843d-154">適切な HTML5 または Teams API を利用して、デバイスのアクセス許可にアクセスするための同意を求めるプロンプトを表示します。</span><span class="sxs-lookup"><span data-stu-id="7843d-154">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7843d-155">selectMedia `camera` `gallery` API を通じて `microphone` サポート [**され、有効になります**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7843d-155">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="7843d-156">1 [**つのイメージ キャプチャに captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。</span><span class="sxs-lookup"><span data-stu-id="7843d-156">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="7843d-157">getLocation `location` API を使用してサポート [**が有効になります**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7843d-157">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="7843d-158">HTML5 位置情報 API は現在 Teams デスクトップ クライアントで完全にはサポートされていないので、場所に使用する `getLocation API` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="7843d-158">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="7843d-159">以下に例を示します。</span><span class="sxs-lookup"><span data-stu-id="7843d-159">For example:</span></span>
 * <span data-ttu-id="7843d-160">ユーザーに位置情報へのアクセスを求めるメッセージを表示するには、次のコマンドを呼び出す必要があります `getCurrentPosition()` 。</span><span class="sxs-lookup"><span data-stu-id="7843d-160">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="7843d-161">デスクトップまたは Web 上のカメラにアクセスするようにユーザーに求めるには、次を呼び出す必要があります `getUserMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="7843d-161">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="7843d-162">モバイルでイメージをキャプチャするために、Teams モバイルは、次を呼び出す際にアクセス許可を求めるメッセージを表示します `captureImage()` 。</span><span class="sxs-lookup"><span data-stu-id="7843d-162">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="7843d-163">通知は、次の呼び出し時にユーザーに表示されます `requestPermission()` 。</span><span class="sxs-lookup"><span data-stu-id="7843d-163">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="7843d-164">カメラを使用するか、フォト ギャラリーにアクセスするために、Teams モバイルは次を呼び出す際にアクセス許可を求めるメッセージを表示します `selectMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="7843d-164">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="7843d-165">マイクを使用するために、Teams モバイルは通話時にアクセス許可を求めるメッセージを表示します `selectMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="7843d-165">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="7843d-166">マップ インターフェイス上の場所を共有するようにユーザーに求めるメッセージを表示するために、Teams モバイルは次を呼び出す際にアクセス許可を求めるメッセージを表示します `getLocation()` 。</span><span class="sxs-lookup"><span data-stu-id="7843d-166">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="7843d-167">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="7843d-167">Desktop</span></span>](#tab/desktop)

   ![タブ デスクトップ デバイスのアクセス許可の確認メッセージ](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="7843d-169">モバイル</span><span class="sxs-lookup"><span data-stu-id="7843d-169">Mobile</span></span>](#tab/mobile)

   ![タブ モバイル デバイスのアクセス許可の確認メッセージ](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="7843d-171">ログイン セッション間のアクセス許可の動作</span><span class="sxs-lookup"><span data-stu-id="7843d-171">Permission behavior across login sessions</span></span>

<span data-ttu-id="7843d-172">デバイスのアクセス許可は、ログイン セッションごとに格納されます。</span><span class="sxs-lookup"><span data-stu-id="7843d-172">Device permissions are stored for every login session.</span></span> <span data-ttu-id="7843d-173">つまり、たとえば別のコンピューターで Teams の別のインスタンスにサインインすると、以前のセッションからのデバイスのアクセス許可は使用できません。</span><span class="sxs-lookup"><span data-stu-id="7843d-173">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="7843d-174">したがって、新しいセッションのデバイスのアクセス許可に再同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7843d-174">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="7843d-175">また、Teams からサインアウトするか、Teams でテナントを切り替える場合、デバイスのアクセス許可は以前のログイン セッションから削除されます。</span><span class="sxs-lookup"><span data-stu-id="7843d-175">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="7843d-176">ネイティブ デバイスのアクセス許可に同意すると、現在のログイン _セッションでのみ有効_ です。</span><span class="sxs-lookup"><span data-stu-id="7843d-176">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-step"></a><span data-ttu-id="7843d-177">次の手順</span><span class="sxs-lookup"><span data-stu-id="7843d-177">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7843d-178">Teams でのメディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="7843d-178">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
