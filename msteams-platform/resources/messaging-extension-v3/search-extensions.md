---
title: メッセージング拡張機能を使用した検索
description: 検索ベースのメッセージング拡張機能を開発する方法について説明します。
keywords: teams メッセージング拡張メッセージング拡張検索
ms.date: 05/20/2019
ms.openlocfilehash: 7baf55d7184784a436ac5a3d6b82db233389bca7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674911"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="d5922-104">メッセージング拡張機能を使用した検索</span><span class="sxs-lookup"><span data-stu-id="d5922-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="d5922-105">検索ベースのメッセージング拡張機能を使用すると、サービスを照会して、その情報をカードの形式でメッセージに投稿することができます。</span><span class="sxs-lookup"><span data-stu-id="d5922-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message</span></span>

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="d5922-107">次のセクションでは、これを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d5922-107">The following sections describe how to do this.</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="d5922-108">検索の種類メッセージの拡張子</span><span class="sxs-lookup"><span data-stu-id="d5922-108">Search type message extensions</span></span>

<span data-ttu-id="d5922-109">検索ベースのメッセージング拡張機能に`type`ついて`query`は、パラメーターをに設定します。</span><span class="sxs-lookup"><span data-stu-id="d5922-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="d5922-110">単一の検索コマンドを含むマニフェストの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d5922-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="d5922-111">1つのメッセージング拡張機能には、最大10個の異なるコマンドを関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="d5922-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="d5922-112">これには、複数の検索と複数のアクションベースのコマンドの両方を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d5922-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="d5922-113">完全なアプリマニフェストの例</span><span class="sxs-lookup"><span data-stu-id="d5922-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a><span data-ttu-id="d5922-114">アップロードによるテスト</span><span class="sxs-lookup"><span data-stu-id="d5922-114">Test via uploading</span></span>

<span data-ttu-id="d5922-115">アプリをアップロードすることで、メッセージング拡張機能をテストできます。</span><span class="sxs-lookup"><span data-stu-id="d5922-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="d5922-116">メッセージング拡張機能を開くには、いずれかのチャットまたはチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="d5922-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="d5922-117">[新規作成] ボックスの [**その他のオプション**(**&#8943;**)] ボタンをクリックして、メッセージング拡張機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="d5922-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="d5922-118">イベントハンドラーを追加する</span><span class="sxs-lookup"><span data-stu-id="d5922-118">Add event handlers</span></span>

<span data-ttu-id="d5922-119">ほとんどの作業では、 `onQuery`メッセージング拡張ウィンドウでのすべての操作を処理するイベントが必要になります。</span><span class="sxs-lookup"><span data-stu-id="d5922-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="d5922-120">マニフェストにが`canUpdateConfiguration`に`true`設定されている場合は、メッセージング拡張機能の [**設定**] メニュー項目を`onQuerySettingsUrl`有効`onSettingsUpdate`にして、とも処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="d5922-121">OnQuery イベントを処理する</span><span class="sxs-lookup"><span data-stu-id="d5922-121">Handle onQuery events</span></span>

<span data-ttu-id="d5922-122">メッセージング拡張機能は、 `onQuery`メッセージング拡張ウィンドウで何らかの問題が発生した場合、またはウィンドウに送信された場合に、イベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="d5922-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="d5922-123">メッセージング拡張機能が構成ページを使用している場合`onQuery`は、のハンドラーで、格納されている構成情報があるかどうかをまずチェックする必要があります。メッセージング拡張機能が構成されてい`config`ない場合は、構成ページへのリンクを含む応答を返します。</span><span class="sxs-lookup"><span data-stu-id="d5922-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="d5922-124">構成ページからの応答もによって`onQuery`処理されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d5922-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="d5922-125">(唯一の例外は、の`onQuerySettingsUrl`ハンドラーによって構成ページが呼び出されたときです。次のセクションを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="d5922-125">(The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section.)</span></span>

<span data-ttu-id="d5922-126">メッセージング拡張機能で認証が必要な場合は、ユーザー状態情報を確認してください。ユーザーがサインインしていない場合は、このトピックで後述する「[認証](#authentication)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="d5922-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="d5922-127">次に、が`initialRun`設定されているかどうかを確認します。その場合は、指示の提供や応答の一覧などの適切なアクションを実行します。</span><span class="sxs-lookup"><span data-stu-id="d5922-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="d5922-128">ハンドラーの残りの部分で`onQuery`は、ユーザーに情報の入力を求め、プレビューカードの一覧を表示し、ユーザーが選択したカードを返します。</span><span class="sxs-lookup"><span data-stu-id="d5922-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="d5922-129">OnQuerySettingsUrl と onSettingsUpdate イベントを処理する</span><span class="sxs-lookup"><span data-stu-id="d5922-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="d5922-130">イベント`onQuerySettingsUrl`と`onSettingsUpdate`イベントは連携して、[**設定**] メニュー項目を有効にします。</span><span class="sxs-lookup"><span data-stu-id="d5922-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

![設定メニュー項目の場所のスクリーンショット](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="d5922-132">の`onQuerySettingsUrl`ハンドラーは、構成ページの URL を返します。構成ページが閉じられると、の`onSettingsUpdate`ハンドラーは、返された状態を受け入れて保存します。</span><span class="sxs-lookup"><span data-stu-id="d5922-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="d5922-133">(の1つのケースで`onQuery`は、構成ページから応答を受信し*ません*)。</span><span class="sxs-lookup"><span data-stu-id="d5922-133">(This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.)</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="d5922-134">クエリを受信して応答する</span><span class="sxs-lookup"><span data-stu-id="d5922-134">Receive and respond to queries</span></span>

<span data-ttu-id="d5922-135">メッセージング拡張機能へのすべての要求は、 `Activity`コールバック URL にポストされたオブジェクトによって実行されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="d5922-136">要求には、ID やパラメーターの値など、ユーザーコマンドに関する情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d5922-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="d5922-137">また、この要求は、ユーザーやテナント ID など、拡張機能が呼び出されたコンテキストに関するメタデータと共に、チャット ID またはチャネルとチーム Id も提供します。</span><span class="sxs-lookup"><span data-stu-id="d5922-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="d5922-138">ユーザー要求を受信する</span><span class="sxs-lookup"><span data-stu-id="d5922-138">Receive user requests</span></span>

<span data-ttu-id="d5922-139">ユーザーがクエリを実行すると、Microsoft Teams はサービスを標準 Bot フレームワーク`Activity`オブジェクトに送信します。</span><span class="sxs-lookup"><span data-stu-id="d5922-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="d5922-140">サービスは、次の表に示す`Activity`ように`type` `invoke` 、がサポート`name`されている`composeExtension`型に設定されていて、に設定されているのロジックを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="d5922-141">標準の bot アクティビティプロパティに加えて、ペイロードには次の要求メタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d5922-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="d5922-142">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="d5922-142">Property name</span></span>|<span data-ttu-id="d5922-143">用途</span><span class="sxs-lookup"><span data-stu-id="d5922-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="d5922-144">要求の種類。で`invoke`ある必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="d5922-145">サービスに対して発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="d5922-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="d5922-146">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5922-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="d5922-147">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="d5922-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="d5922-148">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="d5922-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="d5922-149">要求を送信したユーザーの Azure Active Directory オブジェクト id。</span><span class="sxs-lookup"><span data-stu-id="d5922-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="d5922-150">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="d5922-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="d5922-151">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="d5922-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="d5922-152">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="d5922-152">Team ID (if the request was made in a channel).</span></span> |
|<span data-ttu-id="d5922-153">`clientInfo`エンティティ</span><span class="sxs-lookup"><span data-stu-id="d5922-153">`clientInfo` entity</span></span> | <span data-ttu-id="d5922-154">クライアントに関する追加のメタデータ (ロケール/言語、クライアントの種類など)。</span><span class="sxs-lookup"><span data-stu-id="d5922-154">Additional metadata about the client, such as locale/language and type of client.</span></span> |

<span data-ttu-id="d5922-155">要求パラメーター自体は、次のプロパティを含む value オブジェクトにあります。</span><span class="sxs-lookup"><span data-stu-id="d5922-155">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="d5922-156">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="d5922-156">Property name</span></span> | <span data-ttu-id="d5922-157">用途</span><span class="sxs-lookup"><span data-stu-id="d5922-157">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="d5922-158">アプリマニフェストで宣言されているコマンドのいずれかと一致する、ユーザーによって起動されたコマンドの名前。</span><span class="sxs-lookup"><span data-stu-id="d5922-158">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="d5922-159">パラメーターの配列。</span><span class="sxs-lookup"><span data-stu-id="d5922-159">Array of parameters.</span></span> <span data-ttu-id="d5922-160">各 parameter オブジェクトには、ユーザーによって提供されるパラメータ値とともにパラメータ名が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d5922-160">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="d5922-161">改ページのパラメーター:</span><span class="sxs-lookup"><span data-stu-id="d5922-161">Pagination parameters:</span></span> <br><span data-ttu-id="d5922-162">`skip`: このクエリの skip count</span><span class="sxs-lookup"><span data-stu-id="d5922-162">`skip`: skip count for this query</span></span> <br><span data-ttu-id="d5922-163">`count`: 返される要素の数</span><span class="sxs-lookup"><span data-stu-id="d5922-163">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="d5922-164">要求の例</span><span class="sxs-lookup"><span data-stu-id="d5922-164">Request example</span></span>

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "timezone": "America/Los_Angeles",
      "type": "clientInfo"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="d5922-165">新規作成メッセージボックスに挿入されたリンクからの要求を受信する</span><span class="sxs-lookup"><span data-stu-id="d5922-165">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="d5922-166">または、外部サービスを検索する代わりに、[作成] メッセージボックスに挿入された URL を使用してサービスを照会し、カードを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="d5922-166">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="d5922-167">次のスクリーンショットでは、ユーザーが Azure DevOps で作業項目の URL を貼り付けて、メッセージング拡張機能がカードに解決されたことを示しています。</span><span class="sxs-lookup"><span data-stu-id="d5922-167">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Link unfurling の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="d5922-169">この方法でメッセージング拡張機能がリンクを操作できるようにするには、まず`messageHandlers` 、次の例に示すように、最初に、アプリケーションマニフェストに配列を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-169">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

<span data-ttu-id="d5922-170">アプリマニフェストをリッスンするためにドメインを追加したら、次の呼び出し要求に[応答](#respond-to-user-requests)するように bot コードを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-170">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="d5922-171">アプリが複数の項目を返す場合は、最初の項目のみが使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-171">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="d5922-172">ユーザー要求に応答する</span><span class="sxs-lookup"><span data-stu-id="d5922-172">Respond to user requests</span></span>

<span data-ttu-id="d5922-173">ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行します。</span><span class="sxs-lookup"><span data-stu-id="d5922-173">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="d5922-174">その時点で、コードには、要求に対する HTTP 応答を提供する5秒の時間があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-174">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="d5922-175">この間、サービスは、追加の参照、または要求の提供に必要なその他のビジネスロジックを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d5922-175">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="d5922-176">サービスは、ユーザークエリに一致する結果で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-176">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="d5922-177">応答は、HTTP 状態コード`200 OK`と、次の本文を含む有効な application/json オブジェクトを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-177">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="d5922-178">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="d5922-178">Property name</span></span>|<span data-ttu-id="d5922-179">用途</span><span class="sxs-lookup"><span data-stu-id="d5922-179">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="d5922-180">最上位レベルの応答封筒。</span><span class="sxs-lookup"><span data-stu-id="d5922-180">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="d5922-181">応答の種類。</span><span class="sxs-lookup"><span data-stu-id="d5922-181">Type of response.</span></span> <span data-ttu-id="d5922-182">次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5922-182">The following types are supported:</span></span> <br><span data-ttu-id="d5922-183">`result`: 検索結果の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="d5922-183">`result`: displays a list of search results</span></span> <br><span data-ttu-id="d5922-184">`auth`: ユーザーに認証を要求する</span><span class="sxs-lookup"><span data-stu-id="d5922-184">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="d5922-185">`config`: メッセージング拡張機能をセットアップするようにユーザーに要求します。</span><span class="sxs-lookup"><span data-stu-id="d5922-185">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="d5922-186">`message`: テキスト形式のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-186">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="d5922-187">添付ファイルのレイアウトを指定します。</span><span class="sxs-lookup"><span data-stu-id="d5922-187">Specifies the layout of the attachments.</span></span> <span data-ttu-id="d5922-188">種類`result`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-188">Used for responses of type `result`.</span></span> <br><span data-ttu-id="d5922-189">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5922-189">Currently the following types are supported:</span></span> <br><span data-ttu-id="d5922-190">`list`: サムネイル、タイトル、テキストフィールドを含む card オブジェクトのリスト</span><span class="sxs-lookup"><span data-stu-id="d5922-190">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="d5922-191">`grid`: サムネイル画像のグリッド</span><span class="sxs-lookup"><span data-stu-id="d5922-191">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="d5922-192">有効な attachment オブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="d5922-192">Array of valid attachment objects.</span></span> <span data-ttu-id="d5922-193">種類`result`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-193">Used for responses of type `result`.</span></span> <br><span data-ttu-id="d5922-194">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5922-194">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="d5922-195">推奨されるアクション。</span><span class="sxs-lookup"><span data-stu-id="d5922-195">Suggested actions.</span></span> <span data-ttu-id="d5922-196">種類`auth`または`config`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-196">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="d5922-197">表示するメッセージ。</span><span class="sxs-lookup"><span data-stu-id="d5922-197">Message to display.</span></span> <span data-ttu-id="d5922-198">種類`message`の応答に使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-198">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="d5922-199">応答カードの種類とプレビュー</span><span class="sxs-lookup"><span data-stu-id="d5922-199">Response card types and previews</span></span>

<span data-ttu-id="d5922-200">次の種類の添付ファイルがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d5922-200">We support the following attachment types:</span></span>

* [<span data-ttu-id="d5922-201">サムネイルカード</span><span class="sxs-lookup"><span data-stu-id="d5922-201">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="d5922-202">英雄カード</span><span class="sxs-lookup"><span data-stu-id="d5922-202">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="d5922-203">Office 365 コネクタカード</span><span class="sxs-lookup"><span data-stu-id="d5922-203">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="d5922-204">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="d5922-204">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="d5922-205">概要については、「[カード](~/task-modules-and-cards/what-are-cards.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d5922-205">See [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="d5922-206">サムネイルおよびヒーローカードの種類を使用する方法については、「[カードおよびカードのアクションを追加](~/task-modules-and-cards/cards/cards-actions.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d5922-206">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="d5922-207">Office 365 コネクタカードに関するその他のドキュメントについては、「 [office 365 コネクタカードの使用](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d5922-207">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="d5922-208">結果リストは、Microsoft Teams UI に各アイテムのプレビューと共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-208">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="d5922-209">プレビューは、次の2つの方法のいずれかで生成されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-209">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="d5922-210">`attachment`オブジェクト内で`preview`プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="d5922-210">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="d5922-211">添付`preview`ファイルには、ヒーローまたはサムネイルカードのみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="d5922-211">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="d5922-212">添付ファイルの基本`title`、 `text`、および`image`プロパティから抽出されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-212">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="d5922-213">これらのプロパティは、 `preview`プロパティが設定されておらず、これらのプロパティを使用できる場合にのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-213">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="d5922-214">プレビュープロパティを設定するだけで、アダプティブまたは Office 365 のコネクタカードのプレビューを結果リストに表示することができます。結果が既にヒーローまたはサムネイルカードである場合は、この手順は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="d5922-214">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="d5922-215">プレビューの添付ファイルを使用する場合は、ヒーローまたは Thumbnail カードである必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-215">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="d5922-216">Preview プロパティが指定されていない場合、カードのプレビューは失敗し、何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="d5922-216">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="d5922-217">応答の例</span><span class="sxs-lookup"><span data-stu-id="d5922-217">Response example</span></span>

<span data-ttu-id="d5922-218">この例では、異なるカード形式が混在する2つの結果を含む応答を示します。 Office 365 コネクタとアダプティブ。</span><span class="sxs-lookup"><span data-stu-id="d5922-218">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="d5922-219">応答に1枚のカード形式を維持したい場合がありますが、前述し`preview`たように、 `attachments`コレクション内の各要素のプロパティが、ヒーローまたは thumbnail 形式でプレビューを明示的に定義する必要があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="d5922-219">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a><span data-ttu-id="d5922-220">既定のクエリ</span><span class="sxs-lookup"><span data-stu-id="d5922-220">Default query</span></span>

<span data-ttu-id="d5922-221">マニフェスト内に`initialRun`が`true`設定されている場合、Microsoft Teams は、ユーザーが最初にメッセージング拡張機能を開いたときに "既定" クエリを発行します。</span><span class="sxs-lookup"><span data-stu-id="d5922-221">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="d5922-222">サービスは、一連の事前設定された結果を使用してこのクエリに応答できます。</span><span class="sxs-lookup"><span data-stu-id="d5922-222">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="d5922-223">これは、たとえば、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="d5922-223">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="d5922-224">既定のクエリは、通常のユーザークエリと同じ構造を持っています`initialRun`が、文字列値`true`があるパラメーターは除きます。</span><span class="sxs-lookup"><span data-stu-id="d5922-224">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="d5922-225">既定のクエリの要求の例</span><span class="sxs-lookup"><span data-stu-id="d5922-225">Request example for a default query</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a><span data-ttu-id="d5922-226">ユーザーを識別する</span><span class="sxs-lookup"><span data-stu-id="d5922-226">Identify the user</span></span>

<span data-ttu-id="d5922-227">サービスへのすべての要求には、要求を実行したユーザーの難読化された ID、およびユーザーの表示名と Azure Active Directory オブジェクト ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d5922-227">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="d5922-228">と`id` `aadObjectId`の値は、認証された Teams のユーザーのものであることが保証されています。</span><span class="sxs-lookup"><span data-stu-id="d5922-228">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="d5922-229">これらは、サービスの資格情報またはキャッシュされた状態を検索するためのキーとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="d5922-229">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="d5922-230">さらに、各要求には、ユーザーの Azure Active Directory テナント ID が含まれています。これは、ユーザーの組織を識別するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="d5922-230">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="d5922-231">該当する場合、要求には、要求の発行元であるチームおよびチャネル Id も含まれます。</span><span class="sxs-lookup"><span data-stu-id="d5922-231">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="d5922-232">認証</span><span class="sxs-lookup"><span data-stu-id="d5922-232">Authentication</span></span>

<span data-ttu-id="d5922-233">サービスでユーザー認証が必要な場合は、メッセージング拡張機能を使用できるようにするには、ユーザーにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-233">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="d5922-234">ユーザーにサインインする bot またはタブを書いてある場合は、このセクションを理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-234">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="d5922-235">順序は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d5922-235">The sequence is as follows:</span></span>

1. <span data-ttu-id="d5922-236">ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-236">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="d5922-237">サービスは、ユーザーが Teams ユーザー ID を調べて最初に認証されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="d5922-237">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="d5922-238">ユーザーが認証されていない場合は`auth` 、認証 URL `openUrl`を含む推奨されるアクションを使用して応答を返信に送り返します。</span><span class="sxs-lookup"><span data-stu-id="d5922-238">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="d5922-239">Microsoft Teams クライアントは、指定された認証 URL を使用して、web ページをホストするポップアップウィンドウを起動します。</span><span class="sxs-lookup"><span data-stu-id="d5922-239">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="d5922-240">ユーザーがサインインした後、ウィンドウを閉じて、Teams クライアントに "認証コード" を送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-240">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="d5922-241">Teams クライアントは、手順5で渡された認証コードを含む、サービスに対してクエリを再度発行します。</span><span class="sxs-lookup"><span data-stu-id="d5922-241">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="d5922-242">サービスは、手順6で受信した認証コードが手順5と一致することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-242">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="d5922-243">これにより、悪意のあるユーザーがサインインフローをスプーフィングしたり、侵害したりすることを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="d5922-243">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="d5922-244">これにより、"ループを閉じる" というセキュリティで保護された認証シーケンスが完了します。</span><span class="sxs-lookup"><span data-stu-id="d5922-244">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="d5922-245">サインインアクションで応答する</span><span class="sxs-lookup"><span data-stu-id="d5922-245">Respond with a sign-in action</span></span>

<span data-ttu-id="d5922-246">認証されていないユーザーにサインインを求めるメッセージを表示するに`openUrl`は、認証 URL を含む種類の推奨されるアクションで応答します。</span><span class="sxs-lookup"><span data-stu-id="d5922-246">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="d5922-247">サインインアクションの応答の例</span><span class="sxs-lookup"><span data-stu-id="d5922-247">Response example for a sign-in action</span></span>

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> <span data-ttu-id="d5922-248">チームのポップアップでサインインするために、URL のドメイン部分は、アプリの有効なドメインの一覧に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-248">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="d5922-249">(マニフェストスキーマの[Validdomains](~/resources/schema/manifest-schema.md#validdomains)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="d5922-249">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="d5922-250">サインインフローを開始する</span><span class="sxs-lookup"><span data-stu-id="d5922-250">Start the sign-in flow</span></span>

<span data-ttu-id="d5922-251">サインイン手順は、ポップアップウィンドウ内に表示されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-251">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="d5922-252">これは、メッセージパッシングを使用する[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-252">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="d5922-253">Microsoft Teams 内部で実行されている他の組み込みエクスペリエンスと同様に、ウィンドウ内`microsoftTeams.initialize()`のコードは最初に呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-253">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="d5922-254">コードで OAuth フローを実行すると、Teams ユーザー ID をウィンドウに渡すことができます。これにより、OAuth サインイン URL に渡されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-254">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="d5922-255">サインインフローを完了する</span><span class="sxs-lookup"><span data-stu-id="d5922-255">Complete the sign-in flow</span></span>

<span data-ttu-id="d5922-256">サインイン要求が完了し、ページにリダイレクトされたら、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="d5922-256">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="d5922-257">セキュリティコードを生成します。</span><span class="sxs-lookup"><span data-stu-id="d5922-257">Generate a security code.</span></span> <span data-ttu-id="d5922-258">(これはランダムな数値になることがあります。)このコードを、サインインフロー (OAuth 2.0 トークンなど) で取得した資格情報と共にサービスにキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5922-258">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="d5922-259">を`microsoftTeams.authentication.notifySuccess`呼び出して、セキュリティコードを渡します。</span><span class="sxs-lookup"><span data-stu-id="d5922-259">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="d5922-260">この時点で、ウィンドウが閉じられ、Teams クライアントに制御が渡されます。</span><span class="sxs-lookup"><span data-stu-id="d5922-260">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="d5922-261">クライアントは、元のユーザークエリと、 `state`プロパティのセキュリティコードを再発行することができるようになります。</span><span class="sxs-lookup"><span data-stu-id="d5922-261">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="d5922-262">コードでは、セキュリティコードを使用して、前に保存した資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。</span><span class="sxs-lookup"><span data-stu-id="d5922-262">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="d5922-263">再発行した要求の例</span><span class="sxs-lookup"><span data-stu-id="d5922-263">Reissued request example</span></span>

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="sdk-support"></a><span data-ttu-id="d5922-264">SDK サポート</span><span class="sxs-lookup"><span data-stu-id="d5922-264">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="d5922-265">.NET</span><span class="sxs-lookup"><span data-stu-id="d5922-265">.NET</span></span>

<span data-ttu-id="d5922-266">Bot ビルダー SDK for .NET を使用してクエリを受信して処理するには`invoke` 、受信アクティビティのアクションの種類を確認してから、NuGet パッケージの[各 Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)でヘルパーメソッドを使用して、メッセージング拡張アクティビティであるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="d5922-266">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="d5922-267">.NET でのコード例</span><span class="sxs-lookup"><span data-stu-id="d5922-267">Example code in .NET</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a><span data-ttu-id="d5922-268">Node.js</span><span class="sxs-lookup"><span data-stu-id="d5922-268">Node.js</span></span>

<span data-ttu-id="d5922-269">Node.js のボット Builder SDK の[Teams 拡張機能](https://www.npmjs.com/package/botbuilder-teams)には、メッセージング拡張要求の受信、処理、応答を簡略化するヘルパーオブジェクトとメソッドが用意されています。</span><span class="sxs-lookup"><span data-stu-id="d5922-269">The [Teams extensions](https://www.npmjs.com/package/botbuilder-teams) for the Bot Builder SDK for Node.js provide helper objects and methods to simplify receiving, processing, and responding to messaging extension requests.</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="d5922-270">Node.js のコード例</span><span class="sxs-lookup"><span data-stu-id="d5922-270">Example code in Node.js</span></span>

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
