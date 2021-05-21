---
title: メッセージング拡張機能を使用して検索する
description: 検索ベースのメッセージング拡張機能を開発する方法について説明します。
keywords: teams メッセージング拡張機能メッセージング拡張機能の検索
ms.topic: how-to
localization_priority: Normal
ms.date: 07/20/2019
ms.openlocfilehash: 515472838ff2ad35ef5dd295043ec27c53edb4f1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566732"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="167f2-104">メッセージング拡張機能を使用して検索する</span><span class="sxs-lookup"><span data-stu-id="167f2-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="167f2-105">検索ベースのメッセージング拡張機能を使用すると、サービスにクエリを実行し、その情報をカードの形式でメッセージに投稿できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message.</span></span>

![メッセージング拡張機能カードの例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="167f2-107">次のセクションでは、これを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="167f2-107">The following sections describe how to do this:</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="167f2-108">検索の種類のメッセージ拡張機能</span><span class="sxs-lookup"><span data-stu-id="167f2-108">Search type message extensions</span></span>

<span data-ttu-id="167f2-109">検索ベースのメッセージング拡張機能では、パラメーターを `type` に設定します `query` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="167f2-110">次に、1 つの検索コマンドを使用するマニフェストの例を示します。</span><span class="sxs-lookup"><span data-stu-id="167f2-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="167f2-111">1 つのメッセージング拡張機能には、最大 10 種類のコマンドを関連付けできます。</span><span class="sxs-lookup"><span data-stu-id="167f2-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="167f2-112">これには、複数の検索と複数のアクション ベースのコマンドの両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="167f2-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="167f2-113">アプリ マニフェストの完全な例</span><span class="sxs-lookup"><span data-stu-id="167f2-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

### <a name="test-via-uploading"></a><span data-ttu-id="167f2-114">アップロードによるテスト</span><span class="sxs-lookup"><span data-stu-id="167f2-114">Test via uploading</span></span>

<span data-ttu-id="167f2-115">メッセージング拡張機能をテストするには、アプリをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="167f2-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="167f2-116">メッセージング拡張機能を開くには、チャットまたはチャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="167f2-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="167f2-117">作成ボックス **で** [**その** 他の&#8943;] ボタンを選択し、メッセージング拡張機能を選択します。</span><span class="sxs-lookup"><span data-stu-id="167f2-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="167f2-118">イベント ハンドラーの追加</span><span class="sxs-lookup"><span data-stu-id="167f2-118">Add event handlers</span></span>

<span data-ttu-id="167f2-119">ほとんどの作業にはイベントが含まれるので、メッセージング拡張機能ウィンドウのすべての操作 `onQuery` を処理します。</span><span class="sxs-lookup"><span data-stu-id="167f2-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="167f2-120">マニフェストでに設定した場合は、メッセージング拡張機能設定メニュー項目を有効にし、および `canUpdateConfiguration` `true` を処理する必要 `onQuerySettingsUrl` があります `onSettingsUpdate` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="167f2-121">onQuery イベントの処理</span><span class="sxs-lookup"><span data-stu-id="167f2-121">Handle onQuery events</span></span>

<span data-ttu-id="167f2-122">メッセージング拡張機能は、メッセージング拡張機能ウィンドウで何かが発生した場合、またはウィンドウ `onQuery` に送信された場合にイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="167f2-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="167f2-123">メッセージング拡張機能で構成ページを使用する場合、ハンドラーは最初に格納されている構成情報を確認する必要があります。メッセージング拡張機能が構成されていない場合は、構成ページへのリンクを含む応答を返します。 `onQuery` `config`</span><span class="sxs-lookup"><span data-stu-id="167f2-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="167f2-124">構成ページからの応答もによって処理されます `onQuery` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="167f2-125">唯一の例外は、構成ページがハンドラーによって呼び出される場合です `onQuerySettingsUrl` 。次のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="167f2-125">The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section:</span></span>

<span data-ttu-id="167f2-126">メッセージング拡張機能で認証が必要な場合は、ユーザーの状態情報を確認します。ユーザーがサインインしていない場合は、このトピックの「認証 [」セクションの](#authentication) 指示に従います。</span><span class="sxs-lookup"><span data-stu-id="167f2-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="167f2-127">次に、設定されているかどうかを確認します。設定されている場合は、指示や応答の一覧などの適切なアクション `initialRun` を実行します。</span><span class="sxs-lookup"><span data-stu-id="167f2-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="167f2-128">ハンドラーの残りの部分では、ユーザーに情報の入力を求め、プレビュー カードの一覧を表示し、ユーザーが選択したカード `onQuery` を返します。</span><span class="sxs-lookup"><span data-stu-id="167f2-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="167f2-129">onQuerySettingsUrl イベントと onSettingsUpdate イベントの処理</span><span class="sxs-lookup"><span data-stu-id="167f2-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="167f2-130">イベント `onQuerySettingsUrl` と `onSettingsUpdate` イベントが一緒に機能して、設定を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="167f2-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

![メニュー項目の場所設定スクリーンショット](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="167f2-132">構成ページの URL を返すハンドラー。構成ページが閉じると、返された状態を受け入れて `onQuerySettingsUrl` `onSettingsUpdate` 保存します。</span><span class="sxs-lookup"><span data-stu-id="167f2-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="167f2-133">これは、構成ページから応答を受信しない `onQuery` 1 つのケースです。</span><span class="sxs-lookup"><span data-stu-id="167f2-133">This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="167f2-134">クエリの受信と応答</span><span class="sxs-lookup"><span data-stu-id="167f2-134">Receive and respond to queries</span></span>

<span data-ttu-id="167f2-135">メッセージング拡張機能へのすべての要求は、コールバック URL `Activity` に投稿されるオブジェクトを介して行われます。</span><span class="sxs-lookup"><span data-stu-id="167f2-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="167f2-136">要求には、ID やパラメーター値など、ユーザー コマンドに関する情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="167f2-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="167f2-137">この要求では、ユーザー ID やテナント ID など、拡張機能が呼び出されたコンテキストに関するメタデータと、チャット ID やチャネル ID、チーム ID も提供されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="167f2-138">ユーザー要求の受信</span><span class="sxs-lookup"><span data-stu-id="167f2-138">Receive user requests</span></span>

<span data-ttu-id="167f2-139">ユーザーがクエリを実行すると、Microsoft Teams標準的な Bot Framework オブジェクトが送信 `Activity` されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="167f2-140">サービスは、次の表に示すように、サポートされている型に設定されているロジックを `Activity` `type` `invoke` `name` `composeExtension` 実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="167f2-141">標準のボット アクティビティ プロパティに加えて、ペイロードには次の要求メタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="167f2-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="167f2-142">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="167f2-142">Property name</span></span>|<span data-ttu-id="167f2-143">用途</span><span class="sxs-lookup"><span data-stu-id="167f2-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="167f2-144">要求の種類。する必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="167f2-145">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="167f2-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="167f2-146">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="167f2-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="167f2-147">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="167f2-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="167f2-148">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="167f2-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="167f2-149">Azure Active Directory送信したユーザーのオブジェクト ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="167f2-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="167f2-150">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="167f2-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="167f2-151">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="167f2-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="167f2-152">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="167f2-152">Team ID (if the request was made in a channel).</span></span> |
|`clientInfo`|<span data-ttu-id="167f2-153">ユーザーのメッセージの送信に使用されるクライアント ソフトウェアに関するオプションのメタデータ。</span><span class="sxs-lookup"><span data-stu-id="167f2-153">Optional metadata about the client software used to send a user's message.</span></span> <span data-ttu-id="167f2-154">エンティティには、次の 2 つのプロパティを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="167f2-154">The entity can contain two properties:</span></span><br><span data-ttu-id="167f2-155">フィールド `country` には、ユーザーの検出された場所が含まれる。</span><span class="sxs-lookup"><span data-stu-id="167f2-155">The `country` field contains the user's detected location.</span></span><br><span data-ttu-id="167f2-156">この `platform` フィールドは、メッセージング クライアント プラットフォームについて説明します。</span><span class="sxs-lookup"><span data-stu-id="167f2-156">The `platform` field describes the messaging client platform.</span></span> <br><span data-ttu-id="167f2-157">詳細については[、「Non-IRI エンティティ型 — clientInfo 」を参照してください](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。</span><span class="sxs-lookup"><span data-stu-id="167f2-157">For additional information, please *see* [Non-IRI entity types — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>|

<span data-ttu-id="167f2-158">要求パラメーター自体は、次のプロパティを含む value オブジェクトに含まれています。</span><span class="sxs-lookup"><span data-stu-id="167f2-158">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="167f2-159">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="167f2-159">Property name</span></span> | <span data-ttu-id="167f2-160">用途</span><span class="sxs-lookup"><span data-stu-id="167f2-160">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="167f2-161">アプリ マニフェストで宣言されているコマンドの 1 つと一致する、ユーザーによって呼び出されるコマンドの名前。</span><span class="sxs-lookup"><span data-stu-id="167f2-161">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="167f2-162">パラメーターの配列: 各パラメーター オブジェクトには、ユーザーが指定したパラメーター値と共に、パラメーター名が含まれます。</span><span class="sxs-lookup"><span data-stu-id="167f2-162">Array of parameters: Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="167f2-163">ページネーション パラメーター:</span><span class="sxs-lookup"><span data-stu-id="167f2-163">Pagination parameters:</span></span> <br><span data-ttu-id="167f2-164">`skip`: このクエリのスキップ カウント</span><span class="sxs-lookup"><span data-stu-id="167f2-164">`skip`: skip count for this query</span></span> <br><span data-ttu-id="167f2-165">`count`: 返す要素の数</span><span class="sxs-lookup"><span data-stu-id="167f2-165">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="167f2-166">要求の例</span><span class="sxs-lookup"><span data-stu-id="167f2-166">Request example</span></span>

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
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="167f2-167">作成メッセージ ボックスに挿入されたリンクから要求を受信する</span><span class="sxs-lookup"><span data-stu-id="167f2-167">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="167f2-168">外部サービスの検索に代わる (または追加) として、作成メッセージ ボックスに挿入された URL を使用してサービスにクエリを実行し、カードを返します。</span><span class="sxs-lookup"><span data-stu-id="167f2-168">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="167f2-169">下のスクリーンショットでは、ユーザーがメッセージング拡張機能がカードに解決したAzure DevOpsワーク アイテムの URL に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="167f2-169">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![リンクの分岐解除の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="167f2-171">メッセージング拡張機能でリンクを操作するには、次の例のように、まず配列をアプリ マニフェスト `messageHandlers` に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-171">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

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

<span data-ttu-id="167f2-172">アプリ マニフェストをリッスンするドメインを追加したら、ボット コードを変更して、以下の呼び出し要求に[](#respond-to-user-requests)応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-172">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="167f2-173">アプリが複数のアイテムを返す場合は、最初のアイテムだけが使用されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-173">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="167f2-174">ユーザー要求に応答する</span><span class="sxs-lookup"><span data-stu-id="167f2-174">Respond to user requests</span></span>

<span data-ttu-id="167f2-175">ユーザーがクエリを実行すると、Microsoft Teamsに同期 HTTP 要求が発行されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-175">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="167f2-176">その時点で、要求に対する HTTP 応答を提供する 5 秒のコードがあります。</span><span class="sxs-lookup"><span data-stu-id="167f2-176">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="167f2-177">この間、サービスは追加の参照、または要求を処理するために必要なその他のビジネス ロジックを実行できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-177">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="167f2-178">サービスは、ユーザー クエリに一致する結果で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-178">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="167f2-179">応答は、HTTP 状態コードと、次の本文を持つ有効 `200 OK` な application/json オブジェクトを示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-179">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="167f2-180">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="167f2-180">Property name</span></span>|<span data-ttu-id="167f2-181">用途</span><span class="sxs-lookup"><span data-stu-id="167f2-181">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="167f2-182">トップ レベルの応答エンベロープ。</span><span class="sxs-lookup"><span data-stu-id="167f2-182">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="167f2-183">応答の種類。</span><span class="sxs-lookup"><span data-stu-id="167f2-183">Type of response.</span></span> <span data-ttu-id="167f2-184">次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="167f2-184">The following types are supported:</span></span> <br><span data-ttu-id="167f2-185">`result`: 検索結果の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="167f2-185">`result`: displays a list of search results</span></span> <br><span data-ttu-id="167f2-186">`auth`: ユーザーに認証を求める</span><span class="sxs-lookup"><span data-stu-id="167f2-186">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="167f2-187">`config`: メッセージング拡張機能のセットアップをユーザーに求める</span><span class="sxs-lookup"><span data-stu-id="167f2-187">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="167f2-188">`message`: テキスト形式のメッセージを表示する</span><span class="sxs-lookup"><span data-stu-id="167f2-188">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="167f2-189">添付ファイルのレイアウトを指定します。</span><span class="sxs-lookup"><span data-stu-id="167f2-189">Specifies the layout of the attachments.</span></span> <span data-ttu-id="167f2-190">型の応答に使用されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-190">Used for responses of type `result`.</span></span> <br><span data-ttu-id="167f2-191">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="167f2-191">Currently the following types are supported:</span></span> <br><span data-ttu-id="167f2-192">`list`: サムネイル、タイトル、およびテキスト フィールドを含むカード オブジェクトのリスト</span><span class="sxs-lookup"><span data-stu-id="167f2-192">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="167f2-193">`grid`: サムネイル画像のグリッド</span><span class="sxs-lookup"><span data-stu-id="167f2-193">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="167f2-194">有効な添付ファイル オブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="167f2-194">Array of valid attachment objects.</span></span> <span data-ttu-id="167f2-195">型の応答に使用されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-195">Used for responses of type `result`.</span></span> <br><span data-ttu-id="167f2-196">現在、次の種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="167f2-196">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="167f2-197">推奨されるアクション。</span><span class="sxs-lookup"><span data-stu-id="167f2-197">Suggested actions.</span></span> <span data-ttu-id="167f2-198">型または . の応答に `auth` 使用 `config` されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-198">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="167f2-199">表示するメッセージ。</span><span class="sxs-lookup"><span data-stu-id="167f2-199">Message to display.</span></span> <span data-ttu-id="167f2-200">型の応答に使用されます `message` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-200">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="167f2-201">応答カードの種類とプレビュー</span><span class="sxs-lookup"><span data-stu-id="167f2-201">Response card types and previews</span></span>

<span data-ttu-id="167f2-202">次の添付ファイルの種類がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="167f2-202">We support the following attachment types:</span></span>

* [<span data-ttu-id="167f2-203">サムネイル カード</span><span class="sxs-lookup"><span data-stu-id="167f2-203">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="167f2-204">ヒーロー カード</span><span class="sxs-lookup"><span data-stu-id="167f2-204">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="167f2-205">Office 365コネクタ カード</span><span class="sxs-lookup"><span data-stu-id="167f2-205">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="167f2-206">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="167f2-206">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="167f2-207">詳細については、「カードの [概要」](~/task-modules-and-cards/what-are-cards.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="167f2-207">For more information, see [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="167f2-208">サムネイルカードとヒーロー カードの種類を使用する方法については、「Add card and [card actions」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="167f2-208">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="167f2-209">コネクタ カードの詳細については、「Office 365 コネクタ カードの使用Office 365[参照してください](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="167f2-209">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="167f2-210">結果リストは、各アイテムのプレビュー Microsoft Teams UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-210">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="167f2-211">プレビューは、次の 2 つの方法で生成されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-211">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="167f2-212">オブジェクト内 `preview` のプロパティを使用 `attachment` する。</span><span class="sxs-lookup"><span data-stu-id="167f2-212">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="167f2-213">添付 `preview` ファイルには、ヒーロー カードまたはサムネイル カードのみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-213">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="167f2-214">添付ファイルの基本 `title` 、 `text` および `image` プロパティから抽出されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-214">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="167f2-215">これらは、プロパティが設定されていない `preview` 場合にのみ使用され、これらのプロパティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-215">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="167f2-216">プレビュー プロパティを設定するだけで、アダプティブ または Office 365 コネクタ カードのプレビューを結果リストに表示できます。結果が既にヒーロー カードまたはサムネイル カードである場合、これは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="167f2-216">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="167f2-217">プレビュー添付ファイルを使用する場合は、ヒーロー カードまたはサムネイル カードである必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-217">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="167f2-218">preview プロパティを指定しない場合、カードのプレビューは失敗し、何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="167f2-218">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="167f2-219">応答の例</span><span class="sxs-lookup"><span data-stu-id="167f2-219">Response example</span></span>

<span data-ttu-id="167f2-220">次の使用例は、2 つの結果を持つ応答を示し、異なるカード形式 (コネクタとアダプティブOffice 365混在しています。</span><span class="sxs-lookup"><span data-stu-id="167f2-220">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="167f2-221">応答で 1 つのカード形式に固執する場合は、コレクション内の各要素のプロパティが、前述のようにヒーロー形式またはサムネイル形式でプレビューを明示的に定義する必要がある方法を示しています。 `preview` `attachments`</span><span class="sxs-lookup"><span data-stu-id="167f2-221">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

### <a name="default-query"></a><span data-ttu-id="167f2-222">既定のクエリ</span><span class="sxs-lookup"><span data-stu-id="167f2-222">Default query</span></span>

<span data-ttu-id="167f2-223">マニフェストで設定した場合、Microsoft Teamsが最初にメッセージング拡張機能を開くと、"既定" クエリ `initialRun` `true` が発行されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-223">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="167f2-224">サービスは、事前に設定された結果のセットでこのクエリに応答できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-224">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="167f2-225">これは、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="167f2-225">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="167f2-226">既定のクエリは、文字列値が . を持つパラメーターを除き、通常のユーザー クエリと `initialRun` 同じ構造を持っています `true` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-226">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="167f2-227">既定のクエリの要求例</span><span class="sxs-lookup"><span data-stu-id="167f2-227">Request example for a default query</span></span>

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

## <a name="identify-the-user"></a><span data-ttu-id="167f2-228">ユーザーを識別する</span><span class="sxs-lookup"><span data-stu-id="167f2-228">Identify the user</span></span>

<span data-ttu-id="167f2-229">サービスへのすべての要求には、要求を実行したユーザーの難読化された ID と、ユーザーの表示名とオブジェクト ID Azure Active Directory含まれます。</span><span class="sxs-lookup"><span data-stu-id="167f2-229">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="167f2-230">値 `id` と `aadObjectId` 値は、認証されたユーザーの値Teamsされます。</span><span class="sxs-lookup"><span data-stu-id="167f2-230">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="167f2-231">資格情報またはサービス内のキャッシュされた状態を参照するためのキーとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-231">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="167f2-232">さらに、各要求には、Azure Active Directoryのテナント ID が含まれているので、ユーザーの組織を識別するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-232">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="167f2-233">該当する場合、要求には、要求の発信元であるチームとチャネルの ID も含まれる。</span><span class="sxs-lookup"><span data-stu-id="167f2-233">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="167f2-234">認証</span><span class="sxs-lookup"><span data-stu-id="167f2-234">Authentication</span></span>

<span data-ttu-id="167f2-235">サービスでユーザー認証が必要な場合は、メッセージング拡張機能を使用する前にユーザーにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-235">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="167f2-236">ユーザーにサインインするボットまたはタブを記述している場合は、このセクションをよく理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-236">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="167f2-237">シーケンスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="167f2-237">The sequence is as follows:</span></span>

1. <span data-ttu-id="167f2-238">ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。</span><span class="sxs-lookup"><span data-stu-id="167f2-238">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="167f2-239">サービスは、ユーザーが最初にユーザー ID を調Teamsチェックします。</span><span class="sxs-lookup"><span data-stu-id="167f2-239">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="167f2-240">ユーザーが認証されていない場合は、認証 URL を含む推奨されるアクションを含む応答 `auth` `openUrl` を返します。</span><span class="sxs-lookup"><span data-stu-id="167f2-240">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="167f2-241">クライアントMicrosoft Teams、指定した認証 URL を使用して Web ページをホストするポップアップ ウィンドウを起動します。</span><span class="sxs-lookup"><span data-stu-id="167f2-241">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="167f2-242">ユーザーがサインインした後、ウィンドウを閉じて、"認証コード" をクライアントにTeamsします。</span><span class="sxs-lookup"><span data-stu-id="167f2-242">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="167f2-243">次Teamsクライアントは、手順 5 で渡された認証コードを含むクエリをサービスに再発行します。</span><span class="sxs-lookup"><span data-stu-id="167f2-243">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="167f2-244">サービスは、手順 6 で受信した認証コードが手順 5 の認証コードと一致することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-244">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="167f2-245">これにより、悪意のあるユーザーがサインイン フローのスプーフィングや侵害を試みない。</span><span class="sxs-lookup"><span data-stu-id="167f2-245">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="167f2-246">これにより、効果的に "ループを閉じる" と、セキュリティで保護された認証シーケンスが完了します。</span><span class="sxs-lookup"><span data-stu-id="167f2-246">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="167f2-247">サインイン アクションで応答する</span><span class="sxs-lookup"><span data-stu-id="167f2-247">Respond with a sign-in action</span></span>

<span data-ttu-id="167f2-248">認証されていないユーザーにサインインを求めるメッセージを表示するには、認証 URL を含む種類の推奨 `openUrl` されるアクションで応答します。</span><span class="sxs-lookup"><span data-stu-id="167f2-248">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="167f2-249">サインイン アクションの応答例</span><span class="sxs-lookup"><span data-stu-id="167f2-249">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="167f2-250">サインイン エクスペリエンスを Teams ポップアップでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-250">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="167f2-251">詳細については、マニフェスト [スキーマの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="167f2-251">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="167f2-252">サインイン フローを開始する</span><span class="sxs-lookup"><span data-stu-id="167f2-252">Start the sign-in flow</span></span>

<span data-ttu-id="167f2-253">サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-253">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="167f2-254">メッセージの受け渡し[をMicrosoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-254">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="167f2-255">他の埋め込みエクスペリエンスが Microsoft Teams内で実行されている場合と同様に、ウィンドウ内のコードは最初に呼び出す必要があります `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="167f2-255">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="167f2-256">コードで OAuth フローを実行する場合は、Teams ユーザー ID をウィンドウに渡し、OAuth サインイン URL に渡します。</span><span class="sxs-lookup"><span data-stu-id="167f2-256">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="167f2-257">サインイン フローを完了する</span><span class="sxs-lookup"><span data-stu-id="167f2-257">Complete the sign-in flow</span></span>

<span data-ttu-id="167f2-258">サインイン要求が完了し、ページにリダイレクトすると、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-258">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="167f2-259">セキュリティ コードを生成します。</span><span class="sxs-lookup"><span data-stu-id="167f2-259">Generate a security code.</span></span> <span data-ttu-id="167f2-260">(ランダムな数値を指定できます)。このコードは、OAuth 2.0 トークンなどのサインイン フローで取得した資格情報と共に、サービスにキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="167f2-260">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow such as, OAuth 2.0 tokens.</span></span>
2. <span data-ttu-id="167f2-261">セキュリティ `microsoftTeams.authentication.notifySuccess` コードを呼び出して渡します。</span><span class="sxs-lookup"><span data-stu-id="167f2-261">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="167f2-262">この時点で、ウィンドウが閉じ、コントロールがクライアントにTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="167f2-262">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="167f2-263">クライアントは、プロパティのセキュリティ コードと共に、元のユーザー クエリを再発行 `state` できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-263">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="167f2-264">コードでは、セキュリティ コードを使用して、以前に格納された資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-264">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="167f2-265">再発行された要求の例</span><span class="sxs-lookup"><span data-stu-id="167f2-265">Reissued request example</span></span>

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
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
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

## <a name="sdk-support"></a><span data-ttu-id="167f2-266">SDK のサポート</span><span class="sxs-lookup"><span data-stu-id="167f2-266">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="167f2-267">.NET</span><span class="sxs-lookup"><span data-stu-id="167f2-267">.NET</span></span>

<span data-ttu-id="167f2-268">ボット ビルダー SDK for .NET を使用してクエリを受信および処理するには、受信アクティビティのアクションの種類を確認してから、NuGet パッケージ `invoke` [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)のヘルパー メソッドを使用して、メッセージング拡張機能アクティビティかどうかを判断できます。</span><span class="sxs-lookup"><span data-stu-id="167f2-268">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="167f2-269">.NET のコード例</span><span class="sxs-lookup"><span data-stu-id="167f2-269">Example code in .NET</span></span>

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

### <a name="nodejs"></a><span data-ttu-id="167f2-270">Node.js</span><span class="sxs-lookup"><span data-stu-id="167f2-270">Node.js</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="167f2-271">コードの例 (Node.js</span><span class="sxs-lookup"><span data-stu-id="167f2-271">Example code in Node.js</span></span>

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

## <a name="see-also"></a><span data-ttu-id="167f2-272">関連項目</span><span class="sxs-lookup"><span data-stu-id="167f2-272">See also</span></span>

<span data-ttu-id="167f2-273">[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="167f2-273">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
