---
title: Microsoft Teams アプリのデバイスのアクセス許可を要求する
keywords: teams アプリの機能のアクセス許可
description: 通常、ユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
ms.topic: how-to
ms.openlocfilehash: 60c28e1170e8bbdf664145bde7f7de585bd55a45
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294748"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="f6961-104">Microsoft Teams アプリのデバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="f6961-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="f6961-105">カメラ、マイク、場所などのネイティブ デバイス機能を使用して Teams アプリを強化できます。</span><span class="sxs-lookup"><span data-stu-id="f6961-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="f6961-106">このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法についてガイドします。</span><span class="sxs-lookup"><span data-stu-id="f6961-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="f6961-107">Microsoft Teams モバイル アプリにメディア機能を統合するには、「メディア機能の統合 [」を参照してください](mobile-camera-image-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="f6961-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="f6961-108">Microsoft Teams モバイル アプリに QR またはバーコード スキャナー機能を統合するには、「Teams に QR またはバーコード スキャナー機能を統合する」 [を参照してください。](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="f6961-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md)</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="f6961-109">ネイティブ デバイスのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="f6961-109">Native device permissions</span></span>

<span data-ttu-id="f6961-110">ネイティブ デバイス機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6961-110">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="f6961-111">デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリ構成で同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="f6961-111">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="f6961-112">ユーザーは、デバイスのアクセス許可を管理するために Teams 設定のアクセス許可ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6961-112">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="f6961-113">デバイス機能にアクセスすることで、Teams プラットフォームで次のような豊富なエクスペリエンスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="f6961-113">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="f6961-114">画像をキャプチャして表示します。</span><span class="sxs-lookup"><span data-stu-id="f6961-114">Capture and view images.</span></span>
* <span data-ttu-id="f6961-115">QR またはバーコードをスキャンします。</span><span class="sxs-lookup"><span data-stu-id="f6961-115">Scan QR or barcode.</span></span>
* <span data-ttu-id="f6961-116">短いビデオを記録して共有します。</span><span class="sxs-lookup"><span data-stu-id="f6961-116">Record and share short videos.</span></span>
* <span data-ttu-id="f6961-117">オーディオ メモを録音し、後で使用するために保存します。</span><span class="sxs-lookup"><span data-stu-id="f6961-117">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="f6961-118">ユーザーの位置情報を使用して、関連する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f6961-118">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="f6961-119">デバイスのアクセス許可にアクセスする</span><span class="sxs-lookup"><span data-stu-id="f6961-119">Access device permissions</span></span>

<span data-ttu-id="f6961-120">[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)には、Teams モバイル アプリがユーザーのデバイス[](#manage-permissions)アクセス許可にアクセスし、より豊富なエクスペリエンスを構築するために必要なツールが提供されています。</span><span class="sxs-lookup"><span data-stu-id="f6961-120">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="f6961-121">これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用する機能について Teams に通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6961-121">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="f6961-122">この更新プログラムを使用すると、アプリが Teams デスクトップ クライアントで実行されている間にアクセス許可を要求できます。</span><span class="sxs-lookup"><span data-stu-id="f6961-122">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="f6961-123">現在、Microsoft Teams はメディア機能をサポートし、QR バーコード スキャナー機能はモバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="f6961-123">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="f6961-124">権限の管理</span><span class="sxs-lookup"><span data-stu-id="f6961-124">Manage permissions</span></span>

<span data-ttu-id="f6961-125">ユーザーは、特定のアプリに対するアクセス許可を許可または拒否を選択して、Teams 設定でデバイスのアクセス許可を管理できます。</span><span class="sxs-lookup"><span data-stu-id="f6961-125">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="f6961-126">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="f6961-126">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="f6961-127">Teams アプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="f6961-127">Open your Teams app.</span></span>
1. <span data-ttu-id="f6961-128">ウィンドウの右上隅にあるプロファイル アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="f6961-128">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="f6961-129">ドロップダウン **メニュー**  >  **から [設定の** アクセス許可] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f6961-129">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="f6961-130">目的の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="f6961-130">Select your desired settings.</span></span>

   ![[デバイスのアクセス許可] デスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="f6961-132">モバイル</span><span class="sxs-lookup"><span data-stu-id="f6961-132">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="f6961-133">Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="f6961-133">Open Teams.</span></span>
1. <span data-ttu-id="f6961-134">[設定] **[**  >  **アプリのアクセス許可] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="f6961-134">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="f6961-135">設定を選択する必要があるアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="f6961-135">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="f6961-136">目的の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="f6961-136">Select your desired settings.</span></span>

    ![[デバイスのアクセス許可] モバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="f6961-138">アクセス許可を指定する</span><span class="sxs-lookup"><span data-stu-id="f6961-138">Specify permissions</span></span>

<span data-ttu-id="f6961-139">アプリケーションで使用する 5 つのプロパティのどちらを追加して指定して、アプリ `manifest.json` `devicePermissions` を更新します。</span><span class="sxs-lookup"><span data-stu-id="f6961-139">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="f6961-140">各プロパティを使用すると、ユーザーに同意を求めるプロンプトを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f6961-140">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="f6961-141">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f6961-141">Property</span></span>      | <span data-ttu-id="f6961-142">説明</span><span class="sxs-lookup"><span data-stu-id="f6961-142">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="f6961-143">media</span><span class="sxs-lookup"><span data-stu-id="f6961-143">media</span></span>         | <span data-ttu-id="f6961-144">カメラ、マイク、スピーカー、およびアクセス メディア ギャラリーを使用する権限。</span><span class="sxs-lookup"><span data-stu-id="f6961-144">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="f6961-145">地理位置情報</span><span class="sxs-lookup"><span data-stu-id="f6961-145">geolocation</span></span>   | <span data-ttu-id="f6961-146">ユーザーの場所を返すアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="f6961-146">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="f6961-147">通知</span><span class="sxs-lookup"><span data-stu-id="f6961-147">notifications</span></span> | <span data-ttu-id="f6961-148">ユーザー通知を送信するアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="f6961-148">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="f6961-149">midi</span><span class="sxs-lookup"><span data-stu-id="f6961-149">midi</span></span>          | <span data-ttu-id="f6961-150">デジタル楽器から楽器デジタル インターフェイス (MIDI) 情報を送受信する権限。</span><span class="sxs-lookup"><span data-stu-id="f6961-150">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="f6961-151">openExternal</span><span class="sxs-lookup"><span data-stu-id="f6961-151">openExternal</span></span>  | <span data-ttu-id="f6961-152">外部アプリケーションでリンクを開くアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="f6961-152">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="f6961-153">アプリからのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="f6961-153">Check permissions from your app</span></span>

<span data-ttu-id="f6961-154">アプリ マニフェスト `devicePermissions` に追加した後、プロンプトを表示せずに **HTML5 アクセス** 許可 API を使用してアクセス許可を確認します。</span><span class="sxs-lookup"><span data-stu-id="f6961-154">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="f6961-155">Teams API を使用してデバイスのアクセス許可を取得する</span><span class="sxs-lookup"><span data-stu-id="f6961-155">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="f6961-156">適切な HTML5 または Teams API を活用して、デバイスのアクセス許可にアクセスする同意を得るプロンプトを表示します。</span><span class="sxs-lookup"><span data-stu-id="f6961-156">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f6961-157">をサポート `camera` し `gallery` `microphone` 、selectMedia API を [**使用して有効になります**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f6961-157">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="f6961-158">1 [**つのイメージ キャプチャに captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。</span><span class="sxs-lookup"><span data-stu-id="f6961-158">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="f6961-159">getLocation `location` API を使用して [**サポートが有効になります**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f6961-159">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="f6961-160">HTML5 地理位置情報 API は現在 Teams デスクトップ クライアントで完全にサポートされていないので、場所に使用 `getLocation API` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6961-160">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="f6961-161">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f6961-161">For example:</span></span>
 * <span data-ttu-id="f6961-162">ユーザーに自分の場所へのアクセスを求めるメッセージを表示するには、次のコマンドを呼び出す必要があります `getCurrentPosition()` 。</span><span class="sxs-lookup"><span data-stu-id="f6961-162">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="f6961-163">デスクトップまたは Web 上のカメラにアクセスするようにユーザーに求めるには、次のコマンドを呼び出す必要があります `getUserMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="f6961-163">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="f6961-164">モバイルで画像をキャプチャするには、Teams モバイルから次の呼び出し時にアクセス許可を求めるメッセージが表示されます `captureImage()` 。</span><span class="sxs-lookup"><span data-stu-id="f6961-164">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="f6961-165">次の呼び出し時に通知がユーザーに表示されます `requestPermission()` 。</span><span class="sxs-lookup"><span data-stu-id="f6961-165">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="f6961-166">カメラを使用するか、フォト ギャラリーにアクセスするには、Teams モバイルが次の呼び出し時にアクセス許可を求めるメッセージを表示します `selectMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="f6961-166">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="f6961-167">マイクを使用するには、Teams モバイルから次の呼び出し時にアクセス許可を求めるメッセージが表示されます `selectMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="f6961-167">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="f6961-168">マップ インターフェイス上の場所を共有するようにユーザーに求めるメッセージを表示するには、Teams モバイルは次の呼び出し時にアクセス許可を求めるメッセージを表示します `getLocation()` 。</span><span class="sxs-lookup"><span data-stu-id="f6961-168">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="f6961-169">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="f6961-169">Desktop</span></span>](#tab/desktop)

   ![タブ デスクトップ デバイスのアクセス許可のプロンプト](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="f6961-171">モバイル</span><span class="sxs-lookup"><span data-stu-id="f6961-171">Mobile</span></span>](#tab/mobile)

   ![タブ モバイル デバイスのアクセス許可のプロンプト](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="f6961-173">ログイン セッション間のアクセス許可の動作</span><span class="sxs-lookup"><span data-stu-id="f6961-173">Permission behavior across login sessions</span></span>

<span data-ttu-id="f6961-174">デバイスのアクセス許可は、ログイン セッションごとに格納されます。</span><span class="sxs-lookup"><span data-stu-id="f6961-174">Device permissions are stored for every login session.</span></span> <span data-ttu-id="f6961-175">つまり、別のコンピューターなど、Teams の別のインスタンスにサインインすると、以前のセッションからのデバイスのアクセス許可は使用できません。</span><span class="sxs-lookup"><span data-stu-id="f6961-175">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="f6961-176">したがって、新しいセッションのデバイスのアクセス許可に再同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6961-176">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="f6961-177">また、Teams からサインアウトするか、Teams でテナントを切り替える場合、デバイスのアクセス許可は以前のログイン セッションから削除されます。</span><span class="sxs-lookup"><span data-stu-id="f6961-177">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="f6961-178">ネイティブ デバイスのアクセス許可に同意すると、現在のログイン _セッションでのみ有効_ です。</span><span class="sxs-lookup"><span data-stu-id="f6961-178">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6961-179">次の手順</span><span class="sxs-lookup"><span data-stu-id="f6961-179">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6961-180">Teams でのメディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="f6961-180">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6961-181">Teams に QR またはバーコード スキャナー機能を統合する</span><span class="sxs-lookup"><span data-stu-id="f6961-181">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
