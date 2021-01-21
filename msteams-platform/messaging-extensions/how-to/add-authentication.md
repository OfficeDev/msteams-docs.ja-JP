---
title: メッセージング拡張機能に認証を追加する
author: clearab
description: メッセージング拡張機能に認証を追加する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 4ebe65af06240d13ceb99fe3b7640ab402d716c5
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911871"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="c4125-103">メッセージング拡張機能に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="c4125-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="c4125-104">ユーザーを識別する</span><span class="sxs-lookup"><span data-stu-id="c4125-104">Identify the user</span></span>

<span data-ttu-id="c4125-105">サービスへのすべての要求には、要求を実行したユーザーの難読化された ID と、ユーザーの表示名と Azure Active Directory オブジェクト ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c4125-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="c4125-106">これらの `id` 値 `aadObjectId` は、認証された Teams ユーザーの値である必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="c4125-107">これらは、資格情報またはサービス内のキャッシュされた状態を参照するためのキーとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="c4125-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="c4125-108">さらに、各要求にはユーザーの Azure Active Directory テナント ID が含まれます。この ID を使用して、ユーザーの組織を識別できます。</span><span class="sxs-lookup"><span data-stu-id="c4125-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="c4125-109">該当する場合、要求には、要求の発信元のチームとチャネルの ID も含まれる。</span><span class="sxs-lookup"><span data-stu-id="c4125-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="c4125-110">認証</span><span class="sxs-lookup"><span data-stu-id="c4125-110">Authentication</span></span>

<span data-ttu-id="c4125-111">サービスでユーザー認証が必要な場合は、ユーザーがメッセージング拡張機能を使用する前にサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="c4125-112">ユーザーにサインインするボットまたはタブを作成している場合は、このセクションをよく理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="c4125-113">シーケンスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c4125-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="c4125-114">ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。</span><span class="sxs-lookup"><span data-stu-id="c4125-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="c4125-115">サービスは、Teams のユーザー ID を検査して、ユーザーが最初に認証されたかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="c4125-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="c4125-116">ユーザーが認証されていない場合は、認証 URL を含む推奨アクションを含 `auth` `openUrl` む応答を返します。</span><span class="sxs-lookup"><span data-stu-id="c4125-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="c4125-117">Microsoft Teams クライアントは、指定された認証 URL を使用して Web ページをホストするポップアップ ウィンドウを起動します。</span><span class="sxs-lookup"><span data-stu-id="c4125-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="c4125-118">ユーザーがサインインした後、ウィンドウを閉じて、Teams クライアントに「認証コード」を送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="c4125-119">その後、Teams クライアントは、手順 5 で渡された認証コードを含むクエリをサービスに再発行します。</span><span class="sxs-lookup"><span data-stu-id="c4125-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="c4125-120">サービスは、手順 6 で受け取った認証コードが手順 5 の認証コードと一致することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="c4125-121">これにより、悪意のあるユーザーがサインイン フローのスプーフィングや侵害を試みない。</span><span class="sxs-lookup"><span data-stu-id="c4125-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="c4125-122">これにより、実質的に "ループを閉じる" と、セキュリティで保護された認証シーケンスが完了します。</span><span class="sxs-lookup"><span data-stu-id="c4125-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="c4125-123">サインイン アクションで応答する</span><span class="sxs-lookup"><span data-stu-id="c4125-123">Respond with a sign-in action</span></span>

<span data-ttu-id="c4125-124">認証されていないユーザーにサインインを求めるメッセージを表示するには、認証 URL を含む種類の提案 `openUrl` されたアクションで応答します。</span><span class="sxs-lookup"><span data-stu-id="c4125-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="c4125-125">サインイン アクションの応答例</span><span class="sxs-lookup"><span data-stu-id="c4125-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="c4125-126">サインイン エクスペリエンスを Teams ポップアップでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="c4125-127">(マニフェスト [スキーマの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c4125-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="c4125-128">サインイン フローを開始する</span><span class="sxs-lookup"><span data-stu-id="c4125-128">Start the sign-in flow</span></span>

<span data-ttu-id="c4125-129">サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="c4125-130">メッセージの受け渡し [を使用する Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="c4125-131">Microsoft Teams 内で実行される他の埋め込みエクスペリエンスと同様に、ウィンドウ内のコードは最初に呼び出す必要があります `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="c4125-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="c4125-132">コードで OAuth フローを実行する場合は、Teams ユーザー ID をウィンドウに渡し、OAuth サインイン URL に渡します。</span><span class="sxs-lookup"><span data-stu-id="c4125-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="c4125-133">サインイン フローを完了する</span><span class="sxs-lookup"><span data-stu-id="c4125-133">Complete the sign-in flow</span></span>

<span data-ttu-id="c4125-134">サインイン要求が完了し、ページにリダイレクトすると、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="c4125-135">セキュリティ コードを生成します。</span><span class="sxs-lookup"><span data-stu-id="c4125-135">Generate a security code.</span></span> <span data-ttu-id="c4125-136">(ランダムな数値を指定できます)。このコードは、サインイン フロー (OAuth 2.0 トークンなど) によって取得された資格情報と共に、サービスにキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4125-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="c4125-137">セキュリティ `microsoftTeams.authentication.notifySuccess` コードを呼び出して渡します。</span><span class="sxs-lookup"><span data-stu-id="c4125-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="c4125-138">この時点で、ウィンドウが閉じ、制御が Teams クライアントに渡されます。</span><span class="sxs-lookup"><span data-stu-id="c4125-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="c4125-139">クライアントは、プロパティのセキュリティ コードと共に、元のユーザー クエリを再発行 `state` できます。</span><span class="sxs-lookup"><span data-stu-id="c4125-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="c4125-140">コードでは、セキュリティ コードを使用して、前に保存した資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。</span><span class="sxs-lookup"><span data-stu-id="c4125-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="c4125-141">再発行された要求の例</span><span class="sxs-lookup"><span data-stu-id="c4125-141">Reissued request example</span></span>

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

## <a name="samples"></a><span data-ttu-id="c4125-142">サンプル</span><span class="sxs-lookup"><span data-stu-id="c4125-142">Samples</span></span>
<span data-ttu-id="c4125-143">メッセージング拡張機能の認証プロセスを示すサンプル コードについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c4125-143">For sample code showing the messaging-extensions authentication process, see:</span></span>

[<span data-ttu-id="c4125-144">Microsoft Teams メッセージング拡張機能認証のサンプル</span><span class="sxs-lookup"><span data-stu-id="c4125-144">Microsoft Teams messaging-extensions authentication sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)

 
