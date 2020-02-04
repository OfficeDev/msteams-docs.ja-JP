---
title: メッセージング拡張機能に認証を追加する
author: clearab
description: メッセージング拡張機能に認証を追加する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f7ebbcd99b1ec35900de7ec2f54f93263918e945
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674688"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="a1370-103">メッセージング拡張機能に認証を追加する</span><span class="sxs-lookup"><span data-stu-id="a1370-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="a1370-104">ユーザーを識別する</span><span class="sxs-lookup"><span data-stu-id="a1370-104">Identify the user</span></span>

<span data-ttu-id="a1370-105">サービスへのすべての要求には、要求を実行したユーザーの難読化された ID、およびユーザーの表示名と Azure Active Directory オブジェクト ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a1370-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="a1370-106">と`id` `aadObjectId`の値は、認証された Teams のユーザーのものであることが保証されています。</span><span class="sxs-lookup"><span data-stu-id="a1370-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="a1370-107">これらは、サービスの資格情報またはキャッシュされた状態を検索するためのキーとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="a1370-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="a1370-108">さらに、各要求には、ユーザーの Azure Active Directory テナント ID が含まれています。これは、ユーザーの組織を識別するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="a1370-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="a1370-109">該当する場合、要求には、要求の発行元であるチームおよびチャネル Id も含まれます。</span><span class="sxs-lookup"><span data-stu-id="a1370-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="a1370-110">認証</span><span class="sxs-lookup"><span data-stu-id="a1370-110">Authentication</span></span>

<span data-ttu-id="a1370-111">サービスでユーザー認証が必要な場合は、メッセージング拡張機能を使用できるようにするには、ユーザーにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="a1370-112">ユーザーにサインインする bot またはタブを書いてある場合は、このセクションを理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="a1370-113">順序は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a1370-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="a1370-114">ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。</span><span class="sxs-lookup"><span data-stu-id="a1370-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="a1370-115">サービスは、ユーザーが Teams ユーザー ID を調べて最初に認証されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="a1370-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="a1370-116">ユーザーが認証されていない場合は`auth` 、認証 URL `openUrl`を含む推奨されるアクションを使用して応答を返信に送り返します。</span><span class="sxs-lookup"><span data-stu-id="a1370-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="a1370-117">Microsoft Teams クライアントは、指定された認証 URL を使用して、web ページをホストするポップアップウィンドウを起動します。</span><span class="sxs-lookup"><span data-stu-id="a1370-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="a1370-118">ユーザーがサインインした後、ウィンドウを閉じて、Teams クライアントに "認証コード" を送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="a1370-119">Teams クライアントは、手順5で渡された認証コードを含む、サービスに対してクエリを再度発行します。</span><span class="sxs-lookup"><span data-stu-id="a1370-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="a1370-120">サービスは、手順6で受信した認証コードが手順5と一致することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="a1370-121">これにより、悪意のあるユーザーがサインインフローをスプーフィングしたり、侵害したりすることを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="a1370-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="a1370-122">これにより、"ループを閉じる" というセキュリティで保護された認証シーケンスが完了します。</span><span class="sxs-lookup"><span data-stu-id="a1370-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="a1370-123">サインインアクションで応答する</span><span class="sxs-lookup"><span data-stu-id="a1370-123">Respond with a sign-in action</span></span>

<span data-ttu-id="a1370-124">認証されていないユーザーにサインインを求めるメッセージを表示するに`openUrl`は、認証 URL を含む種類の推奨されるアクションで応答します。</span><span class="sxs-lookup"><span data-stu-id="a1370-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="a1370-125">サインインアクションの応答の例</span><span class="sxs-lookup"><span data-stu-id="a1370-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="a1370-126">チームのポップアップでサインインするために、URL のドメイン部分は、アプリの有効なドメインの一覧に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="a1370-127">(マニフェストスキーマの[Validdomains](~/resources/schema/manifest-schema.md#validdomains)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="a1370-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="a1370-128">サインインフローを開始する</span><span class="sxs-lookup"><span data-stu-id="a1370-128">Start the sign-in flow</span></span>

<span data-ttu-id="a1370-129">サインイン手順は、ポップアップウィンドウ内に表示されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="a1370-130">これは、メッセージパッシングを使用する[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="a1370-131">Microsoft Teams 内部で実行されている他の組み込みエクスペリエンスと同様に、ウィンドウ内`microsoftTeams.initialize()`のコードは最初に呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="a1370-132">コードで OAuth フローを実行すると、Teams ユーザー ID をウィンドウに渡すことができます。これにより、OAuth サインイン URL に渡されます。</span><span class="sxs-lookup"><span data-stu-id="a1370-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="a1370-133">サインインフローを完了する</span><span class="sxs-lookup"><span data-stu-id="a1370-133">Complete the sign-in flow</span></span>

<span data-ttu-id="a1370-134">サインイン要求が完了し、ページにリダイレクトされたら、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="a1370-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="a1370-135">セキュリティコードを生成します。</span><span class="sxs-lookup"><span data-stu-id="a1370-135">Generate a security code.</span></span> <span data-ttu-id="a1370-136">(これはランダムな数値になることがあります。)このコードを、サインインフロー (OAuth 2.0 トークンなど) で取得した資格情報と共にサービスにキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1370-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="a1370-137">を`microsoftTeams.authentication.notifySuccess`呼び出して、セキュリティコードを渡します。</span><span class="sxs-lookup"><span data-stu-id="a1370-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="a1370-138">この時点で、ウィンドウが閉じられ、Teams クライアントに制御が渡されます。</span><span class="sxs-lookup"><span data-stu-id="a1370-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="a1370-139">クライアントは、元のユーザークエリと、 `state`プロパティのセキュリティコードを再発行することができるようになります。</span><span class="sxs-lookup"><span data-stu-id="a1370-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="a1370-140">コードでは、セキュリティコードを使用して、前に保存した資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。</span><span class="sxs-lookup"><span data-stu-id="a1370-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="a1370-141">再発行した要求の例</span><span class="sxs-lookup"><span data-stu-id="a1370-141">Reissued request example</span></span>

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

