---
title: Microsoft Teams アプリのデバイスのアクセス許可を要求する
keywords: teams アプリの機能のアクセス許可
description: 通常、ユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
ms.topic: how-to
ms.openlocfilehash: e7c5f7ff477bc193924cdf11700c77ae620cd1c0
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449437"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="6f6e8-104">Microsoft Teams アプリのデバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="6f6e8-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="6f6e8-105">カメラ、マイク、場所などのネイティブ デバイス機能を使用して Teams アプリを強化できます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="6f6e8-106">このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法についてガイドします。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="6f6e8-107">Microsoft Teams モバイル アプリにメディア機能を統合するには、「メディア機能の統合 [」を参照してください](mobile-camera-image-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="6f6e8-108">Microsoft Teams モバイル アプリに QR またはバーコード スキャナー機能を統合するには、「Teams に QR またはバーコード スキャナー機能を統合する」 [を参照してください。](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="6f6e8-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md)</span></span>
> * <span data-ttu-id="6f6e8-109">場所の機能を Microsoft Teams モバイル アプリに統合するには、「場所の機能を統合 [する」を参照してください](location-capability.md)。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="6f6e8-110">ネイティブ デバイスのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="6f6e8-110">Native device permissions</span></span>

<span data-ttu-id="6f6e8-111">ネイティブ デバイス機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="6f6e8-112">デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリ構成で同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="6f6e8-113">ユーザーは、デバイスのアクセス許可を管理するために Teams 設定の [アクセス許可] ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="6f6e8-114">デバイス機能にアクセスすることで、Teams プラットフォームで次のような豊富なエクスペリエンスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="6f6e8-115">画像をキャプチャして表示します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-115">Capture and view images.</span></span>
* <span data-ttu-id="6f6e8-116">QR またはバーコードをスキャンします。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="6f6e8-117">短いビデオを記録して共有します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-117">Record and share short videos.</span></span>
* <span data-ttu-id="6f6e8-118">オーディオ メモを録音し、後で使用するために保存します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="6f6e8-119">ユーザーの位置情報を使用して、関連する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-119">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="6f6e8-120">デバイスのアクセス許可にアクセスする</span><span class="sxs-lookup"><span data-stu-id="6f6e8-120">Access device permissions</span></span>

<span data-ttu-id="6f6e8-121">[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)には、Teams モバイル アプリがユーザーのデバイス[](#manage-permissions)アクセス許可にアクセスし、より豊富なエクスペリエンスを構築するために必要なツールが提供されています。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-121">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="6f6e8-122">これらの機能へのアクセスは最新の Web ブラウザーでは標準ですが、アプリ マニフェストを更新して使用する機能について Teams に通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-122">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="6f6e8-123">この更新プログラムを使用すると、アプリが Teams デスクトップ クライアントで実行されている間にアクセス許可を要求できます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-123">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="6f6e8-124">現在、Microsoft Teams はメディア機能をサポートし、QR バーコード スキャナー機能はモバイル クライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-124">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="6f6e8-125">権限の管理</span><span class="sxs-lookup"><span data-stu-id="6f6e8-125">Manage permissions</span></span>

<span data-ttu-id="6f6e8-126">ユーザーは、特定のアプリに対するアクセス許可を許可または拒否を選択して、Teams 設定でデバイスのアクセス許可を管理できます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-126">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="6f6e8-127">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="6f6e8-127">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="6f6e8-128">Teams アプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-128">Open your Teams app.</span></span>
1. <span data-ttu-id="6f6e8-129">ウィンドウの右上隅にあるプロファイル アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-129">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="6f6e8-130">ドロップダウン **メニュー**  >  **から [設定の** アクセス許可] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-130">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="6f6e8-131">目的の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-131">Select your desired settings.</span></span>

   ![[デバイスのアクセス許可] デスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="6f6e8-133">モバイル</span><span class="sxs-lookup"><span data-stu-id="6f6e8-133">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="6f6e8-134">Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-134">Open Teams.</span></span>
1. <span data-ttu-id="6f6e8-135">[設定] **[**  >  **アプリのアクセス許可] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-135">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="6f6e8-136">設定を選択する必要があるアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-136">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="6f6e8-137">目的の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-137">Select your desired settings.</span></span>

    ![[デバイスのアクセス許可] モバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="6f6e8-139">アクセス許可を指定する</span><span class="sxs-lookup"><span data-stu-id="6f6e8-139">Specify permissions</span></span>

<span data-ttu-id="6f6e8-140">アプリケーションで使用する 5 つのプロパティのどちらを追加して指定して、アプリ `manifest.json` `devicePermissions` を更新します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-140">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="6f6e8-141">各プロパティを使用すると、ユーザーに同意を求めるプロンプトを表示できます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-141">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="6f6e8-142">プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f6e8-142">Property</span></span>      | <span data-ttu-id="6f6e8-143">説明</span><span class="sxs-lookup"><span data-stu-id="6f6e8-143">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="6f6e8-144">media</span><span class="sxs-lookup"><span data-stu-id="6f6e8-144">media</span></span>         | <span data-ttu-id="6f6e8-145">カメラ、マイク、スピーカー、およびアクセス メディア ギャラリーを使用する権限。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-145">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="6f6e8-146">地理位置情報</span><span class="sxs-lookup"><span data-stu-id="6f6e8-146">geolocation</span></span>   | <span data-ttu-id="6f6e8-147">ユーザーの場所を返すアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-147">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="6f6e8-148">通知</span><span class="sxs-lookup"><span data-stu-id="6f6e8-148">notifications</span></span> | <span data-ttu-id="6f6e8-149">ユーザー通知を送信するアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-149">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="6f6e8-150">midi</span><span class="sxs-lookup"><span data-stu-id="6f6e8-150">midi</span></span>          | <span data-ttu-id="6f6e8-151">デジタル楽器から楽器デジタル インターフェイス (MIDI) 情報を送受信する権限。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-151">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="6f6e8-152">openExternal</span><span class="sxs-lookup"><span data-stu-id="6f6e8-152">openExternal</span></span>  | <span data-ttu-id="6f6e8-153">外部アプリケーションでリンクを開くアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-153">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="6f6e8-154">アプリからのアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="6f6e8-154">Check permissions from your app</span></span>

<span data-ttu-id="6f6e8-155">アプリ マニフェスト `devicePermissions` に追加した後、プロンプトを表示せずに **HTML5 アクセス** 許可 API を使用してアクセス許可を確認します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-155">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="6f6e8-156">Teams API を使用してデバイスのアクセス許可を取得する</span><span class="sxs-lookup"><span data-stu-id="6f6e8-156">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="6f6e8-157">適切な HTML5 または Teams API を活用して、デバイスのアクセス許可にアクセスする同意を得るプロンプトを表示します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-157">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="6f6e8-158">をサポート `camera` し `gallery` `microphone` 、selectMedia API を [**使用して有効になります**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-158">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="6f6e8-159">1 [**つのイメージ キャプチャに captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-159">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="6f6e8-160">getLocation `location` API を使用して [**サポートが有効になります**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-160">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="6f6e8-161">HTML5 地理位置情報 API は現在 Teams デスクトップ クライアントで完全にサポートされていないので、場所に使用 `getLocation API` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-161">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="6f6e8-162">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-162">For example:</span></span>
 * <span data-ttu-id="6f6e8-163">ユーザーに自分の場所へのアクセスを求めるメッセージを表示するには、次のコマンドを呼び出す必要があります `getCurrentPosition()` 。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-163">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="6f6e8-164">デスクトップまたは Web 上のカメラにアクセスするようにユーザーに求めるには、次のコマンドを呼び出す必要があります `getUserMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-164">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="6f6e8-165">モバイルで画像をキャプチャするには、Teams モバイルから次の呼び出し時にアクセス許可を求めるメッセージが表示されます `captureImage()` 。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-165">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="6f6e8-166">次の呼び出し時に通知がユーザーに表示されます `requestPermission()` 。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-166">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="6f6e8-167">カメラを使用するか、フォト ギャラリーにアクセスするには、Teams モバイルが次の呼び出し時にアクセス許可を求めるメッセージを表示します `selectMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-167">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="6f6e8-168">マイクを使用するには、Teams モバイルから次の呼び出し時にアクセス許可を求めるメッセージが表示されます `selectMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-168">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="6f6e8-169">マップ インターフェイス上の場所を共有するようにユーザーに求めるメッセージを表示するには、Teams モバイルは次の呼び出し時にアクセス許可を求めるメッセージを表示します `getLocation()` 。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-169">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="6f6e8-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="6f6e8-170">Desktop</span></span>](#tab/desktop)

   ![タブ デスクトップ デバイスのアクセス許可のプロンプト](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="6f6e8-172">モバイル</span><span class="sxs-lookup"><span data-stu-id="6f6e8-172">Mobile</span></span>](#tab/mobile)

   ![タブ モバイル デバイスのアクセス許可のプロンプト](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="6f6e8-174">ログイン セッション間のアクセス許可の動作</span><span class="sxs-lookup"><span data-stu-id="6f6e8-174">Permission behavior across login sessions</span></span>

<span data-ttu-id="6f6e8-175">デバイスのアクセス許可は、ログイン セッションごとに格納されます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-175">Device permissions are stored for every login session.</span></span> <span data-ttu-id="6f6e8-176">つまり、別のコンピューターなど、Teams の別のインスタンスにサインインすると、以前のセッションからのデバイスのアクセス許可は使用できません。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-176">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="6f6e8-177">したがって、新しいセッションのデバイスのアクセス許可に再同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-177">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="6f6e8-178">また、Teams からサインアウトするか、Teams でテナントを切り替える場合、デバイスのアクセス許可は以前のログイン セッションから削除されます。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-178">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="6f6e8-179">ネイティブ デバイスのアクセス許可に同意すると、現在のログイン _セッションでのみ有効_ です。</span><span class="sxs-lookup"><span data-stu-id="6f6e8-179">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f6e8-180">次の手順</span><span class="sxs-lookup"><span data-stu-id="6f6e8-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f6e8-181">Teams でのメディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="6f6e8-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f6e8-182">Teams に QR またはバーコード スキャナー機能を統合する</span><span class="sxs-lookup"><span data-stu-id="6f6e8-182">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f6e8-183">Teams での場所機能の統合</span><span class="sxs-lookup"><span data-stu-id="6f6e8-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
