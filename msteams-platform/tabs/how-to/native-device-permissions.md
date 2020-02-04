---
title: Microsoft Teams タブのデバイスへのアクセス許可を要求する
description: 通常、ユーザーの同意を必要とするネイティブ機能へのアクセスを要求するためにアプリのマニフェストを更新する方法
keywords: teams タブの開発
ms.openlocfilehash: 454466ff17ecf275f6ae6c7413df8e117335f3c8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674626"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="fa6dd-104">Microsoft Teams タブのデバイスへのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="fa6dd-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="fa6dd-105">次のような、ネイティブデバイスへのアクセスを必要とする機能を使用して、タブを充実させることができます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="fa6dd-106">デジタル</span><span class="sxs-lookup"><span data-stu-id="fa6dd-106">Camera</span></span>
* <span data-ttu-id="fa6dd-107">マイク</span><span class="sxs-lookup"><span data-stu-id="fa6dd-107">Microphone</span></span>
* <span data-ttu-id="fa6dd-108">場所</span><span class="sxs-lookup"><span data-stu-id="fa6dd-108">Location</span></span>
* <span data-ttu-id="fa6dd-109">通知</span><span class="sxs-lookup"><span data-stu-id="fa6dd-109">Notifications</span></span>

![デバイスアクセス許可の設定画面](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> <span data-ttu-id="fa6dd-111">ネイティブデバイスの機能は、現在、モバイルクライアントのタブではサポートされていませんが、完全なサポートは近日予定されています。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-111">Native device functionality is currently not supported for tabs on mobile clients but full support is coming soon.</span></span> <span data-ttu-id="fa6dd-112">この変更を準備するには、タブを作成するときに[[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-112">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="fa6dd-113">個人用アプリ (静的タブ) は現在、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-113">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="fa6dd-114">タブの完全なサポートがリリースされると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-114">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="fa6dd-115">すべてのタブがモバイルで常に使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-115">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="fa6dd-116">`contentUrl` **は、モバイル Teams クライアントにロードされ**ます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-116">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="fa6dd-117">[チャネル/グループ] タブでは、ユーザーは自分`websiteUrl`のを経由して別のブラウザーで`contentUrl`タブを開くことができます。ただし、は最初に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-117">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>  

## <a name="device-permissions"></a><span data-ttu-id="fa6dd-118">デバイス アクセス許可</span><span class="sxs-lookup"><span data-stu-id="fa6dd-118">Device permissions</span></span>

<span data-ttu-id="fa6dd-119">ユーザーのデバイスのアクセス許可にアクセスすると、次のように、より高度なエクスペリエンスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-119">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="fa6dd-120">短いビデオを録音および共有する</span><span class="sxs-lookup"><span data-stu-id="fa6dd-120">Record and share short videos</span></span>
* <span data-ttu-id="fa6dd-121">短い音声メモを録音し、後で保存する</span><span class="sxs-lookup"><span data-stu-id="fa6dd-121">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="fa6dd-122">ユーザーの場所情報を使用して関連情報を表示する</span><span class="sxs-lookup"><span data-stu-id="fa6dd-122">Use user location information to display relevant information</span></span>

<span data-ttu-id="fa6dd-123">これらの機能へのアクセスは、ほとんどのモダン web ブラウザーで標準になっていますが、アプリマニフェストを更新することによって、使用する機能を Teams に知らせる必要があります。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-123">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="fa6dd-124">これにより、アプリが Teams デスクトップクライアント上で実行されているときに、ブラウザーと同じ方法でアクセス許可を要求することができます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-124">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="fa6dd-125">プロパティ</span><span class="sxs-lookup"><span data-stu-id="fa6dd-125">Properties</span></span>

<span data-ttu-id="fa6dd-126">アプリケーションで使用する`manifest.json` 5 つ`devicePermissions`のプロパティを追加して指定することにより、アプリを更新します。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-126">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="fa6dd-127">各プロパティによって、ユーザーに同意を求めるように求めるメッセージを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-127">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="fa6dd-128">プロパティ</span><span class="sxs-lookup"><span data-stu-id="fa6dd-128">Property</span></span>      | <span data-ttu-id="fa6dd-129">説明</span><span class="sxs-lookup"><span data-stu-id="fa6dd-129">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="fa6dd-130">書き込め</span><span class="sxs-lookup"><span data-stu-id="fa6dd-130">media</span></span>         | <span data-ttu-id="fa6dd-131">カメラ、マイク、およびスピーカーを使用するためのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="fa6dd-131">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="fa6dd-132">地理位置情報</span><span class="sxs-lookup"><span data-stu-id="fa6dd-132">geolocation</span></span>   | <span data-ttu-id="fa6dd-133">ユーザーの場所を返すためのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="fa6dd-133">permission to return the user's location</span></span>      |
| <span data-ttu-id="fa6dd-134">受け取る</span><span class="sxs-lookup"><span data-stu-id="fa6dd-134">notifications</span></span> | <span data-ttu-id="fa6dd-135">ユーザー通知を送信するためのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="fa6dd-135">permission to send the user notifications</span></span>      |
| <span data-ttu-id="fa6dd-136">次回</span><span class="sxs-lookup"><span data-stu-id="fa6dd-136">midi</span></span>          | <span data-ttu-id="fa6dd-137">デジタル音楽機器から midi 情報を送受信するためのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="fa6dd-137">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="fa6dd-138">openExternal</span><span class="sxs-lookup"><span data-stu-id="fa6dd-138">openExternal</span></span>  | <span data-ttu-id="fa6dd-139">外部アプリケーションでリンクを開くためのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="fa6dd-139">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="fa6dd-140">タブから権限を確認する</span><span class="sxs-lookup"><span data-stu-id="fa6dd-140">Checking permissions from your tab</span></span>

<span data-ttu-id="fa6dd-141">アプリマニフェストに追加`devicePermissions`した後は、メッセージを表示せずに、HTML5 の "PERMISSIONS" API を使用してアクセス許可を確認できます。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-141">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="fa6dd-142">ユーザーに確認を求める</span><span class="sxs-lookup"><span data-stu-id="fa6dd-142">Prompting the user</span></span>

<span data-ttu-id="fa6dd-143">デバイスのアクセス許可にアクセスするための同意を得るためのプロンプトを表示するには、適切な HTML5 API を利用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fa6dd-143">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="fa6dd-144">たとえば、ユーザーにカメラへのアクセスを要求するために、を呼び出す必要があります。`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="fa6dd-144">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="fa6dd-145">呼び出し時に地理位置情報にアクセス許可プロンプトが表示される`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="fa6dd-145">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="fa6dd-146">を呼び出したときに通知が表示されます。`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="fa6dd-146">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![タブのデバイスアクセス許可のプロンプト](~/assets/images/tabs/device-permissions-prompt.png)