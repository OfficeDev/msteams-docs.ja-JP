---
title: メッセージング拡張機能に認証を追加する
author: clearab
description: メッセージング拡張機能に認証を追加する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 04ece6fe6f5e824873ed6e69385bce017df6927d
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696774"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="5a720-103">メッセージング拡張機能に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="5a720-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="5a720-104">ユーザーを識別する</span><span class="sxs-lookup"><span data-stu-id="5a720-104">Identify the user</span></span>

<span data-ttu-id="5a720-105">サービスに対する要求には、ユーザー ID、ユーザーの表示名、Azure Active Directory オブジェクト ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5a720-105">Every request to your services includes the user  ID, the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="5a720-106">認証 `id` された `aadObjectId` Teams ユーザーの値と値が保証されます。</span><span class="sxs-lookup"><span data-stu-id="5a720-106">The `id` and `aadObjectId` values are guaranteed for the authenticated Teams user.</span></span> <span data-ttu-id="5a720-107">これらは、サービス内の資格情報またはキャッシュされた状態を参照するためのキーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="5a720-107">They are used as keys to look up the credentials or any cached state in your service.</span></span> <span data-ttu-id="5a720-108">さらに、各要求には、ユーザーの組織を識別するために使用される、ユーザーの Azure Active Directory テナント ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5a720-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which is used to identify the user’s organization.</span></span> <span data-ttu-id="5a720-109">該当する場合、要求には、要求の発信元であるチーム ID とチャネル ID も含まれる。</span><span class="sxs-lookup"><span data-stu-id="5a720-109">If applicable, the request also contains the team Id and channel ID from which the request is originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="5a720-110">認証</span><span class="sxs-lookup"><span data-stu-id="5a720-110">Authentication</span></span>

<span data-ttu-id="5a720-111">サービスでユーザー認証が必要な場合、ユーザーはメッセージング拡張機能を使用する前にサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-111">If your service requires user authentication, the users must sign in before they use the messaging extension.</span></span> <span data-ttu-id="5a720-112">認証手順は、ボットまたはタブの認証手順と似ています。シーケンスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5a720-112">The authentication steps are similar to that of a bot or tab. The sequence is as follows:</span></span>

1. <span data-ttu-id="5a720-113">ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。</span><span class="sxs-lookup"><span data-stu-id="5a720-113">User issues a query, or the default query is automatically sent to your service.</span></span>
1. <span data-ttu-id="5a720-114">サービスは、Teams ユーザー ID を検査して、ユーザーが認証されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="5a720-114">Your service checks whether the user is authenticated by inspecting the Teams user ID.</span></span>
1. <span data-ttu-id="5a720-115">ユーザーが認証されていない場合は、認証 URL を含む推奨されるアクションを含む応答 `auth` `openUrl` を返します。</span><span class="sxs-lookup"><span data-stu-id="5a720-115">If the user is not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
1. <span data-ttu-id="5a720-116">Microsoft Teams クライアントは、指定された認証 URL を使用して Web ページをホストするダイアログ ボックスを起動します。</span><span class="sxs-lookup"><span data-stu-id="5a720-116">The Microsoft Teams client launches a dialog box hosting your webpage using the given authentication URL.</span></span>
1. <span data-ttu-id="5a720-117">ユーザーがサインインした後、ウィンドウを閉じて、Teams クライアントに **認証コード** を送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-117">After the user signs in, you should close your window and send an **authentication code** to the Teams client.</span></span>
1. <span data-ttu-id="5a720-118">Teams クライアントは、手順 5 で渡された認証コードを含むクエリをサービスに再発行します。</span><span class="sxs-lookup"><span data-stu-id="5a720-118">The Teams client then reissues the query to your service, which includes the authentication code passed in Step 5.</span></span>

<span data-ttu-id="5a720-119">サービスは、手順 6 で受信した認証コードが手順 5 の認証コードと一致することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-119">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="5a720-120">これにより、悪意のあるユーザーがサインイン フローのスプーフィングや侵害を試みない。</span><span class="sxs-lookup"><span data-stu-id="5a720-120">This ensures that a malicious user does not try to spoof or compromise the sign in flow.</span></span> <span data-ttu-id="5a720-121">これにより、効果的に "ループを閉じる" と、セキュリティで保護された認証シーケンスが完了します。</span><span class="sxs-lookup"><span data-stu-id="5a720-121">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="5a720-122">サインイン アクションで応答する</span><span class="sxs-lookup"><span data-stu-id="5a720-122">Respond with a sign-in action</span></span>

<span data-ttu-id="5a720-123">認証されていないユーザーにサインインを求めるメッセージを表示するには、認証 URL を含む種類の推奨 `openUrl` されるアクションで応答します。</span><span class="sxs-lookup"><span data-stu-id="5a720-123">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="5a720-124">サインイン アクションの応答例</span><span class="sxs-lookup"><span data-stu-id="5a720-124">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="5a720-125">サインイン エクスペリエンスを Teams ポップアップ ウィンドウでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-125">For the sign in experience to be hosted in a Teams pop-up window, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="5a720-126">詳細については、マニフェスト [スキーマの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5a720-126">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="5a720-127">サインイン フローを開始する</span><span class="sxs-lookup"><span data-stu-id="5a720-127">Start the sign in flow</span></span>

<span data-ttu-id="5a720-128">サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-128">Your sign in experience must be responsive and fit within a pop-up window.</span></span> <span data-ttu-id="5a720-129">メッセージの受け渡しを [使用する Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-129">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="5a720-130">Microsoft Teams 内で実行されている他の埋め込みエクスペリエンスと同様に、ウィンドウ内のコードは最初に呼び出す必要があります `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="5a720-130">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="5a720-131">コードで OAuth フローを実行する場合は、Teams ユーザー ID をウィンドウに渡し、OAuth サインイン URL に渡します。</span><span class="sxs-lookup"><span data-stu-id="5a720-131">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then passes it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="5a720-132">サインイン フローを完了する</span><span class="sxs-lookup"><span data-stu-id="5a720-132">Complete the sign in flow</span></span>

<span data-ttu-id="5a720-133">サインイン要求が完了し、ページにリダイレクトしたら、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-133">When the sign in request completes and redirects back to your page, it must perform the following steps:</span></span>

1. <span data-ttu-id="5a720-134">セキュリティ コードを生成します。</span><span class="sxs-lookup"><span data-stu-id="5a720-134">Generate a security code.</span></span> <span data-ttu-id="5a720-135">これは乱数です。</span><span class="sxs-lookup"><span data-stu-id="5a720-135">This is a random number.</span></span> <span data-ttu-id="5a720-136">このコードは、OAuth 2.0 トークンなどのサインイン フローで取得した資格情報と共に、サービスにキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a720-136">You must cache this code on your service, along with the credentials obtained through the sign in flow, such as OAuth 2.0 tokens.</span></span>
1. <span data-ttu-id="5a720-137">セキュリティ `microsoftTeams.authentication.notifySuccess` コードを呼び出して渡します。</span><span class="sxs-lookup"><span data-stu-id="5a720-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="5a720-138">この時点で、ウィンドウが閉じ、コントロールが Teams クライアントに渡されます。</span><span class="sxs-lookup"><span data-stu-id="5a720-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="5a720-139">クライアントは、プロパティのセキュリティ コードと共に、元のユーザー クエリを再発行 `state` します。</span><span class="sxs-lookup"><span data-stu-id="5a720-139">The client now reissues the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="5a720-140">コードでは、セキュリティ コードを使用して、以前に格納された資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。</span><span class="sxs-lookup"><span data-stu-id="5a720-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="5a720-141">再発行された要求の例</span><span class="sxs-lookup"><span data-stu-id="5a720-141">Reissued request example</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="5a720-142">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="5a720-142">Code sample</span></span>
|<span data-ttu-id="5a720-143">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="5a720-143">**Sample name**</span></span> | <span data-ttu-id="5a720-144">**説明**</span><span class="sxs-lookup"><span data-stu-id="5a720-144">**Description**</span></span> |<span data-ttu-id="5a720-145">**.NET**</span><span class="sxs-lookup"><span data-stu-id="5a720-145">**.NET**</span></span> | <span data-ttu-id="5a720-146">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="5a720-146">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="5a720-147">メッセージング拡張機能 - auth と config</span><span class="sxs-lookup"><span data-stu-id="5a720-147">Messaging extensions - auth and config</span></span> | <span data-ttu-id="5a720-148">構成ページを持ち、検索要求を受け入れ、ユーザーがサインインした後に結果を返すメッセージング拡張機能。</span><span class="sxs-lookup"><span data-stu-id="5a720-148">A Messaging Extension that has a configuration page, accepts search requests, and returns results after the user has signed in.</span></span> |[<span data-ttu-id="5a720-149">View</span><span class="sxs-lookup"><span data-stu-id="5a720-149">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[<span data-ttu-id="5a720-150">View</span><span class="sxs-lookup"><span data-stu-id="5a720-150">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
