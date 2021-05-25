---
title: RSC を使用してすべてのチャネル メッセージを受信する
author: surbhigupta12
description: RSC アクセス許可を持つすべてのチャネル メッセージを受信する
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 833bdbc015cf852fcd899ce4e75f742448b89978
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631413"
---
# <a name="receive-all-channel-messages-with-rsc"></a><span data-ttu-id="31fb4-103">RSC を使用してすべてのチャネル メッセージを受信する</span><span class="sxs-lookup"><span data-stu-id="31fb4-103">Receive all channel messages with RSC</span></span>

> [!NOTE]
> <span data-ttu-id="31fb4-104">この機能は現在、パブリック開発者 [プレビューでのみ利用](../../../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="31fb4-104">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="31fb4-105">リソース固有の同意 (RSC) アクセス許可モデルは、もともと api 用に開発されたTeams Graphボット シナリオに拡張されました。</span><span class="sxs-lookup"><span data-stu-id="31fb4-105">The resource-specific consent (RSC) permissions model, originally developed for Teams Graph APIs, is now extended to bot scenarios.</span></span>

<span data-ttu-id="31fb4-106">現在、ボットはユーザー チャネル メッセージを受信できるのは、ユーザー チャネル メッセージが@mentioned。</span><span class="sxs-lookup"><span data-stu-id="31fb4-106">Currently, bots can only receive user channel messages when they are @mentioned.</span></span> <span data-ttu-id="31fb4-107">RSC を使用すると、ボットがチーム内の標準チャネル間でユーザー メッセージを受信する同意をチームの所有者に要求@mentioned。</span><span class="sxs-lookup"><span data-stu-id="31fb4-107">Using RSC, you can now request team owners to consent for a bot to receive user messages across standard channels in a team without being @mentioned.</span></span> <span data-ttu-id="31fb4-108">この機能は、アプリで有効になっている RSC のマニフェストでアクセス許可 `ChannelMessage.Read.Group` をTeamsします。</span><span class="sxs-lookup"><span data-stu-id="31fb4-108">This capability is enabled by specifying the `ChannelMessage.Read.Group` permission in the manifest of an RSC enabled Teams app.</span></span> <span data-ttu-id="31fb4-109">構成後、チームの所有者はアプリのインストール プロセス中に同意を付与できます。</span><span class="sxs-lookup"><span data-stu-id="31fb4-109">After configuration, team owners can grant consent during the app installation process.</span></span>

<span data-ttu-id="31fb4-110">アプリで RSC を有効にする方法の詳細については、「リソース固有の同意」を参照[Teams。](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="31fb4-110">For more information about enabling RSC for your app, see [resource-specific consent in Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).</span></span>

## <a name="enable-bots-to-receive-all-channel-messages"></a><span data-ttu-id="31fb4-111">ボットがすべてのチャネル メッセージを受信可能にする</span><span class="sxs-lookup"><span data-stu-id="31fb4-111">Enable bots to receive all channel messages</span></span>

<span data-ttu-id="31fb4-112">`ChannelMessage.Read.Group`RSC アクセス許可はボットに拡張されます。</span><span class="sxs-lookup"><span data-stu-id="31fb4-112">The `ChannelMessage.Read.Group` RSC permission is extended to bots.</span></span> <span data-ttu-id="31fb4-113">ユーザーの同意を得た場合、このアクセス許可を使用すると、グラフ アプリケーションは会話内のすべてのメッセージを取得し、ボットはメッセージを読み取ることなくすべてのチャネル @mentioned。</span><span class="sxs-lookup"><span data-stu-id="31fb4-113">With user consent, this permission allows graph applications to get all messages in a conversation and bots to receive all channel messages without being @mentioned.</span></span>

## <a name="update-app-manifest"></a><span data-ttu-id="31fb4-114">アプリ マニフェストの更新</span><span class="sxs-lookup"><span data-stu-id="31fb4-114">Update app manifest</span></span>

<span data-ttu-id="31fb4-115">ボットがすべてのチャネル メッセージを受信するには、プロパティで指定されたアクセス許可Teamsアプリ マニフェストで RSC を `ChannelMessage.Read.Group` 構成する必要 `webApplicationInfo` があります。</span><span class="sxs-lookup"><span data-stu-id="31fb4-115">For your bot to receive all channel messages, RSC must be configured in the Teams app manifest with the `ChannelMessage.Read.Group` permission specified in the `webApplicationInfo` property.</span></span>

![アプリ マニフェストの更新](~/bots/how-to/conversations/Media/appmanifest.png)

<span data-ttu-id="31fb4-117">オブジェクトの例を次に示 `webApplicationInfo` します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-117">The following is an example of the `webApplicationInfo` object:</span></span>

* <span data-ttu-id="31fb4-118">**id**: Azure Active Directory (AAD) アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="31fb4-118">**id**: Your Azure Active Directory (AAD) app ID.</span></span> <span data-ttu-id="31fb4-119">これは、ボット ID と同じものにできます。</span><span class="sxs-lookup"><span data-stu-id="31fb4-119">This can be the same as your bot ID.</span></span>
* <span data-ttu-id="31fb4-120">**resource**: 任意の文字列。</span><span class="sxs-lookup"><span data-stu-id="31fb4-120">**resource**: Any string.</span></span> <span data-ttu-id="31fb4-121">このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31fb4-121">This field has no operation in RSC, but must be added and have a value to avoid error response.</span></span>
* <span data-ttu-id="31fb4-122">**applicationPermissions**: アプリの RSC アクセス許可を指定 `ChannelMessage.Read.Group` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31fb4-122">**applicationPermissions**: RSC permissions for your app with `ChannelMessage.Read.Group` must be specified.</span></span> <span data-ttu-id="31fb4-123">詳細については、「リソース固有 [のアクセス許可」を参照してください](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="31fb4-123">For more information, see [resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).</span></span>

<span data-ttu-id="31fb4-124">次のコードは、アプリ マニフェストの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="31fb4-124">The following code provides an example of the app manifest:</span></span>

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team-to-test"></a><span data-ttu-id="31fb4-125">テストするチームのサイドロード</span><span class="sxs-lookup"><span data-stu-id="31fb4-125">Sideload in a team to test</span></span>

<span data-ttu-id="31fb4-126">テストするチームにサイドロードするには、RSC を持つチーム内のすべてのチャネル メッセージが、次の情報を取得せずに受信@mentioned。</span><span class="sxs-lookup"><span data-stu-id="31fb4-126">To sideload in a team to test, whether all channel messages in a team with RSC are received without being @mentioned:</span></span>

1. <span data-ttu-id="31fb4-127">チームを選択または作成します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-127">Select or create a team.</span></span>
1. <span data-ttu-id="31fb4-128">左側のウィンドウから &#x25CF;&#x25CF;&#x25CF; 省略記号を選択します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-128">Select the ellipses &#x25CF;&#x25CF;&#x25CF; from the left pane.</span></span> <span data-ttu-id="31fb4-129">ドロップダウン メニューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="31fb4-129">The drop-down menu appears.</span></span>
1. <span data-ttu-id="31fb4-130">ドロップダウン **メニューから [チーム** の管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-130">Select **Manage team** from the drop-down menu.</span></span> <span data-ttu-id="31fb4-131">詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="31fb4-131">The details appear.</span></span>

   ![チームでのアプリの管理](~/bots/how-to/conversations/Media/managingteam.png)

1. <span data-ttu-id="31fb4-133">**[アプリ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-133">Select **Apps**.</span></span> <span data-ttu-id="31fb4-134">複数のアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="31fb4-134">Multiple apps appear.</span></span>
1. <span data-ttu-id="31fb4-135">右下 **アップロードカスタム アプリを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-135">Select **Upload a custom app** from the lower right corner.</span></span>

    ![カスタム アプリのアップロード](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. <span data-ttu-id="31fb4-137">[開く] ダイアログ ボックスから **アプリ パッケージを** 選択します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-137">Select the app package from the **Open** dialog box.</span></span>
1. <span data-ttu-id="31fb4-138">[**開く**]を選択します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-138">Select **Open**.</span></span>

    ![アプリ パッケージの選択](~/bots/how-to/conversations/Media/selectapppackage.png)

1. <span data-ttu-id="31fb4-140">アプリ **の詳細** ポップアップから [追加] を選択して、選択したチームにボットを追加します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-140">Select **Add** from the app details pop-up, to add the bot to your selected team.</span></span>

    ![ボットの追加](~/bots/how-to/conversations/Media/addingbot.png)

1. <span data-ttu-id="31fb4-142">チャネルを選択し、ボットのチャネルにメッセージを入力します。</span><span class="sxs-lookup"><span data-stu-id="31fb4-142">Select a channel and enter a message in the channel for your bot.</span></span>

    <span data-ttu-id="31fb4-143">ボットは、メッセージを受信せずにメッセージを@mentioned。</span><span class="sxs-lookup"><span data-stu-id="31fb4-143">The bot receives the message without being @mentioned.</span></span>

    ![ボットがメッセージを受信する](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="see-also"></a><span data-ttu-id="31fb4-145">関連項目</span><span class="sxs-lookup"><span data-stu-id="31fb4-145">See also</span></span>

* [<span data-ttu-id="31fb4-146">ボットの会話</span><span class="sxs-lookup"><span data-stu-id="31fb4-146">Bot conversations</span></span>](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [<span data-ttu-id="31fb4-147">リソース固有の同意</span><span class="sxs-lookup"><span data-stu-id="31fb4-147">Resource-specific consent</span></span>](/microsoftteams/resource-specific-consent)
* [<span data-ttu-id="31fb4-148">リソース固有の同意をテストする</span><span class="sxs-lookup"><span data-stu-id="31fb4-148">Test resource-specific consent</span></span>](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [<span data-ttu-id="31fb4-149">アップロードカスタム アプリのTeams</span><span class="sxs-lookup"><span data-stu-id="31fb4-149">Upload custom app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
