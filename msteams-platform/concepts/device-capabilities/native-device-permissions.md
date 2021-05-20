---
title: Microsoft Teams アプリのデバイスのアクセス許可を要求する
keywords: チーム アプリの機能のアクセス許可
description: 通常はユーザーの同意が必要なネイティブ機能へのアクセスを要求するためにアプリ マニフェストを更新する方法
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 34f84285dc883cc474cf1720c42b1699f76c6653
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566181"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="2a80d-104">Microsoft Teams アプリのデバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="2a80d-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="2a80d-105">カメラ、マイク、位置情報などのネイティブデバイス機能を使用して、Teamsアプリを強化できます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="2a80d-106">このドキュメントでは、ユーザーの同意を要求し、ネイティブ デバイスのアクセス許可にアクセスする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="2a80d-107">Microsoft Teamsモバイル アプリ内でメディア機能を統合するには、「[メディア](mobile-camera-image-permissions.md)機能の統合」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2a80d-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="2a80d-108">Microsoft Teamsモバイル アプリ内で QR またはバーコード スキャナー機能を統合するには[、qr またはバーコード スキャナーの機能を Teams に統合](qr-barcode-scanner-capability.md)するを参照してください。</span><span class="sxs-lookup"><span data-stu-id="2a80d-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md).</span></span>
> * <span data-ttu-id="2a80d-109">Microsoft Teamsモバイルアプリ内で位置情報機能を統合するには、「[位置情報機能の統合](location-capability.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2a80d-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="2a80d-110">ネイティブ デバイスのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="2a80d-110">Native device permissions</span></span>

<span data-ttu-id="2a80d-111">ネイティブ デバイス機能にアクセスするには、デバイスのアクセス許可を要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a80d-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="2a80d-112">デバイスのアクセス許可は、タブ、タスク モジュール、メッセージング拡張機能など、すべてのアプリコンストラクトで同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="2a80d-113">ユーザーは、デバイスのアクセス許可を管理するために、Teams設定のアクセス許可ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a80d-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="2a80d-114">デバイス機能にアクセスすることで、Teams プラットフォームで次のような豊富なエクスペリエンスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="2a80d-115">画像をキャプチャして表示します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-115">Capture and view images.</span></span>
* <span data-ttu-id="2a80d-116">QRまたはバーコードをスキャンします。</span><span class="sxs-lookup"><span data-stu-id="2a80d-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="2a80d-117">短い動画を録画して共有する。</span><span class="sxs-lookup"><span data-stu-id="2a80d-117">Record and share short videos.</span></span>
* <span data-ttu-id="2a80d-118">オーディオメモを録音し、後で使用するためにそれらを保存します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="2a80d-119">ユーザーの位置情報を使用して、関連情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-119">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="2a80d-120">デバイスのアクセス許可にアクセスする</span><span class="sxs-lookup"><span data-stu-id="2a80d-120">Access device permissions</span></span>

<span data-ttu-id="2a80d-121">[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)には、Teamsモバイル アプリがユーザーの[デバイスのアクセス許可](#manage-permissions)にアクセスし、より充実したエクスペリエンスを構築するために必要なツールが用意されています。</span><span class="sxs-lookup"><span data-stu-id="2a80d-121">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="2a80d-122">これらの機能へのアクセスは、最新の Web ブラウザーでは標準的ですが、アプリ マニフェストを更新して、使用する機能についてTeamsに通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a80d-122">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="2a80d-123">この更新プログラムを使用すると、アプリがTeams デスクトップ クライアントで実行されている間にアクセス許可を要求できます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-123">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="2a80d-124">現在、メディア機能とQRバーコードスキャナ機能のMicrosoft Teamsサポートは、モバイルクライアントでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-124">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="2a80d-125">権限の管理</span><span class="sxs-lookup"><span data-stu-id="2a80d-125">Manage permissions</span></span>

<span data-ttu-id="2a80d-126">ユーザーは、特定のアプリに対するアクセス許可を **許可** または **拒否** を選択して、Teams設定でデバイスのアクセス許可を管理できます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-126">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="2a80d-127">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="2a80d-127">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="2a80d-128">Teams アプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-128">Open your Teams app.</span></span>
1. <span data-ttu-id="2a80d-129">ウィンドウの右上隅にあるプロフィールアイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-129">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="2a80d-130">ドロップダウン メニューから **[**  >  **権限** 設定]を選択します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-130">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="2a80d-131">希望の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-131">Select your desired settings.</span></span>

   ![デバイスのアクセス許可デスクトップ設定画面](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="2a80d-133">モバイル</span><span class="sxs-lookup"><span data-stu-id="2a80d-133">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="2a80d-134">Teamsを開きます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-134">Open Teams.</span></span>
1. <span data-ttu-id="2a80d-135">  >  **[アプリのアクセス許可設定] に** 移動します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-135">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="2a80d-136">設定を選択する必要があるアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-136">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="2a80d-137">希望の設定を選択します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-137">Select your desired settings.</span></span>

    ![デバイスのアクセス許可 モバイル設定画面](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="2a80d-139">アクセス許可の指定</span><span class="sxs-lookup"><span data-stu-id="2a80d-139">Specify permissions</span></span>

<span data-ttu-id="2a80d-140">`manifest.json`アプリケーションで使用する 5 `devicePermissions` つのプロパティのうち、どれを追加して指定してアプリを更新します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-140">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="2a80d-141">各プロパティを使用すると、ユーザーに同意を求めるよう求めることができます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-141">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="2a80d-142">プロパティ</span><span class="sxs-lookup"><span data-stu-id="2a80d-142">Property</span></span>      | <span data-ttu-id="2a80d-143">説明</span><span class="sxs-lookup"><span data-stu-id="2a80d-143">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="2a80d-144">media</span><span class="sxs-lookup"><span data-stu-id="2a80d-144">media</span></span>         | <span data-ttu-id="2a80d-145">カメラ、マイク、スピーカー、およびアクセス メディア ギャラリーを使用する権限。</span><span class="sxs-lookup"><span data-stu-id="2a80d-145">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="2a80d-146">地理位置情報</span><span class="sxs-lookup"><span data-stu-id="2a80d-146">geolocation</span></span>   | <span data-ttu-id="2a80d-147">ユーザーの場所を返すアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="2a80d-147">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="2a80d-148">通知</span><span class="sxs-lookup"><span data-stu-id="2a80d-148">notifications</span></span> | <span data-ttu-id="2a80d-149">ユーザー通知を送信する権限。</span><span class="sxs-lookup"><span data-stu-id="2a80d-149">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="2a80d-150">ミディ</span><span class="sxs-lookup"><span data-stu-id="2a80d-150">midi</span></span>          | <span data-ttu-id="2a80d-151">デジタル楽器から楽器デジタルインターフェイス(MIDI)情報を送受信する権限。</span><span class="sxs-lookup"><span data-stu-id="2a80d-151">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="2a80d-152">オープン外部</span><span class="sxs-lookup"><span data-stu-id="2a80d-152">openExternal</span></span>  | <span data-ttu-id="2a80d-153">外部アプリケーションでリンクを開く権限。</span><span class="sxs-lookup"><span data-stu-id="2a80d-153">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="2a80d-154">アプリからアクセス許可を確認する</span><span class="sxs-lookup"><span data-stu-id="2a80d-154">Check permissions from your app</span></span>

<span data-ttu-id="2a80d-155">アプリ `devicePermissions` マニフェストに追加した後、プロンプトを表示せずに **HTML5 アクセス許可 API** を使用してアクセス許可を確認します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-155">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="2a80d-156">Teams API を使用してデバイスのアクセス許可を取得する</span><span class="sxs-lookup"><span data-stu-id="2a80d-156">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="2a80d-157">適切な HTML5 またはTeams API を活用して、デバイスのアクセス許可へのアクセスに同意するためのプロンプトを表示します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-157">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="2a80d-158">のサポート `camera` `gallery` 、 および `microphone` は [**、 [メディア API] を選択**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)して有効にします。</span><span class="sxs-lookup"><span data-stu-id="2a80d-158">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="2a80d-159">1 つのイメージ キャプチャに [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) を使用します。</span><span class="sxs-lookup"><span data-stu-id="2a80d-159">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="2a80d-160">のサポート `location` は [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)を通じて有効になります。</span><span class="sxs-lookup"><span data-stu-id="2a80d-160">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="2a80d-161">`getLocation API`HTML5 地理位置情報 API は現在、デスクトップ クライアントでは完全にサポートされていないので、この場所Teams使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a80d-161">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="2a80d-162">例:</span><span class="sxs-lookup"><span data-stu-id="2a80d-162">For example:</span></span>
 * <span data-ttu-id="2a80d-163">ユーザーに自分の場所にアクセスするよう求めるには、 を呼び出す必要があります `getCurrentPosition()` 。</span><span class="sxs-lookup"><span data-stu-id="2a80d-163">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="2a80d-164">デスクトップまたは Web 上でカメラにアクセスするようユーザーに求めるには、 を呼び出す必要があります `getUserMedia()` 。</span><span class="sxs-lookup"><span data-stu-id="2a80d-164">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="2a80d-165">モバイルで画像をキャプチャするには、モバイルTeams電話時に許可を求めます `captureImage()` 。</span><span class="sxs-lookup"><span data-stu-id="2a80d-165">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="2a80d-166">お問い合いの際に、通知を受け取るとユーザーにメッセージが表示 `requestPermission()` されます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-166">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="2a80d-167">カメラを使用したり、フォトギャラリーにアクセスするには、モバイルTeamsあなたが呼び出すときに許可を求めます `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="2a80d-167">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="2a80d-168">マイクを使用するには、携帯電話Teams電話時に許可を求めます `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="2a80d-168">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="2a80d-169">マップ インターフェイスで場所を共有するようにユーザーに確認するには、モバイルTeams、電話時に許可を求めます `getLocation()` 。</span><span class="sxs-lookup"><span data-stu-id="2a80d-169">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="2a80d-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="2a80d-170">Desktop</span></span>](#tab/desktop)

   ![タブ デスクトップ デバイスのアクセス許可のプロンプト](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="2a80d-172">モバイル</span><span class="sxs-lookup"><span data-stu-id="2a80d-172">Mobile</span></span>](#tab/mobile)

   ![タブ モバイル デバイスのアクセス許可のプロンプト](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="2a80d-174">ログイン セッション間でのアクセス許可の動作</span><span class="sxs-lookup"><span data-stu-id="2a80d-174">Permission behavior across login sessions</span></span>

<span data-ttu-id="2a80d-175">デバイスのアクセス許可は、ログイン セッションごとに保存されます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-175">Device permissions are stored for every login session.</span></span> <span data-ttu-id="2a80d-176">つまり、Teamsの別のインスタンス (たとえば、別のコンピューター) にサインインした場合、以前のセッションからのデバイスのアクセス許可は利用できません。</span><span class="sxs-lookup"><span data-stu-id="2a80d-176">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="2a80d-177">したがって、新しいセッションのデバイスのアクセス許可に再同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2a80d-177">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="2a80d-178">また、TeamsでTeamsからサインアウトしたりテナントを切り替えたりすると、デバイスのアクセス許可は前回のログイン セッションから削除されます。</span><span class="sxs-lookup"><span data-stu-id="2a80d-178">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="2a80d-179">ネイティブデバイスのアクセス許可に同意すると、 _現在_ のログインセッションでのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="2a80d-179">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a80d-180">次の手順</span><span class="sxs-lookup"><span data-stu-id="2a80d-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a80d-181">Teamsでのメディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="2a80d-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a80d-182">TeamsでQRまたはバーコードスキャナ機能を統合</span><span class="sxs-lookup"><span data-stu-id="2a80d-182">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a80d-183">Teamsでの位置情報機能の統合</span><span class="sxs-lookup"><span data-stu-id="2a80d-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
