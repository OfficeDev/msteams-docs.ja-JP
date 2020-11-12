---
title: Teams でのリソース固有の同意のテスト
description: Postman を使用する Teams でのリソース固有の同意のテストの詳細
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: teams authorization OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: f780829100e47ad04a588106e83843876b8d7932
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995010"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a><span data-ttu-id="effbc-104">Teams でのリソース固有の同意権限をテストする</span><span class="sxs-lookup"><span data-stu-id="effbc-104">Test resource-specific consent permissions  in Teams</span></span>

<span data-ttu-id="effbc-105">リソース固有の同意 (RSC) は Microsoft Teams と Graph API の統合で、アプリが API エンドポイントを使用して組織内の特定のチームを管理できるようにします。</span><span class="sxs-lookup"><span data-stu-id="effbc-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="effbc-106">[リソース固有の同意 (RSC) — Microsoft Teams GRAPH API](resource-specific-consent.md)を *参照* してください。  </span><span class="sxs-lookup"><span data-stu-id="effbc-106">Please *see*  [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
><span data-ttu-id="effbc-107">RSC のアクセス許可をテストするには、Teams アプリのマニフェストファイルに、次のフィールドで設定された **Webapplicationinfo** キーが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="effbc-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="effbc-108">**id** : azure ad アプリ id については、「 [azure ad ポータルでアプリを登録](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)する *」を参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="effbc-108">**id**  — your Azure AD app id, *see* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="effbc-109">**resource** : 任意の文字列。「 [Teams アプリのマニフェストを更新する](resource-specific-consent.md#update-your-teams-app-manifest)」のメモを参照して *ください* 。</span><span class="sxs-lookup"><span data-stu-id="effbc-109">**resource**  — any string, *see* the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest)</span></span>
> - <span data-ttu-id="effbc-110">**アプリケーションのアクセス許可** -アプリの RSC アクセス許可については、「 [リソース固有のアクセス許可](resource-specific-consent.md#resource-specific-permissions) *」を参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="effbc-110">**application permissions** — RSC permissions for  your app, *see* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

>[!IMPORTANT]
><span data-ttu-id="effbc-111">アプリのマニフェストには、アプリに必要な RSC アクセス許可のみが含まれています。</span><span class="sxs-lookup"><span data-stu-id="effbc-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="effbc-112">Postman アプリを使用して、追加された RSC アクセス許可をテストする</span><span class="sxs-lookup"><span data-stu-id="effbc-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="effbc-113">RSC アクセス許可が API 要求ペイロードによって受け入れられているかどうかを確認するには、 [RSC JSON テストコード](test-rsc-json-file.md) をローカル環境にコピーし、次の値を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="effbc-113">To check whether the RSC permissions are being honored by the API request payload, you'll need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

1. <span data-ttu-id="effbc-114">`azureADAppId`  -アプリの Azure AD アプリ id。</span><span class="sxs-lookup"><span data-stu-id="effbc-114">`azureADAppId`  — your app's Azure AD app id.</span></span>
1. <span data-ttu-id="effbc-115">`azureADAppSecret`  -Azure AD アプリシークレット (パスワード)</span><span class="sxs-lookup"><span data-stu-id="effbc-115">`azureADAppSecret`  — your Azure AD app secret (password)</span></span>
1. <span data-ttu-id="effbc-116">`token_scope`  -トークンに値を設定するには、スコープが必要です。 https://graph.microsoft.com/.default</span><span class="sxs-lookup"><span data-stu-id="effbc-116">`token_scope`  — the scope is required to get a token - set the value to https://graph.microsoft.com/.default</span></span>
1. <span data-ttu-id="effbc-117">`teamGroupId` — Teams クライアントからチームグループ id を取得するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="effbc-117">`teamGroupId` — you can get the team group id from the Teams client as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="effbc-118">Teams クライアントで、左端のナビゲーションバーにある [ **teams** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="effbc-118">In the Teams client, select **Teams** from the far left nav bar .</span></span>
> * <span data-ttu-id="effbc-119">アプリがインストールされているチームをドロップダウンメニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="effbc-119">Select the team where the app is installed from the dropdown menu.</span></span>
> * <span data-ttu-id="effbc-120">[ **その他のオプション** ] アイコン (&#8943;) を選択します。</span><span class="sxs-lookup"><span data-stu-id="effbc-120">Select the **More options** icon (&#8943;)</span></span>
> * <span data-ttu-id="effbc-121">[ **チームへのリンクの取得** ] を選択する</span><span class="sxs-lookup"><span data-stu-id="effbc-121">Select **Get link to team**</span></span> 
> * <span data-ttu-id="effbc-122">文字列から **groupId** 値をコピーして保存します。</span><span class="sxs-lookup"><span data-stu-id="effbc-122">Copy and save the **groupId** value from the string.</span></span>

### <a name="using-postman"></a><span data-ttu-id="effbc-123">Postman を使用する</span><span class="sxs-lookup"><span data-stu-id="effbc-123">Using Postman</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="effbc-124">[Postman](https://www.postman.com)アプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="effbc-124">Open the [Postman](https://www.postman.com) app.</span></span>
> * <span data-ttu-id="effbc-125">[ **ファイル**  =>  の **インポート** ] [  =>  **インポートファイル** ] を選択して、更新された JSON ファイルを環境からアップロードします。</span><span class="sxs-lookup"><span data-stu-id="effbc-125">Select **File** => **Import** => **Import file** to upload the updated JSON file from your environment.</span></span>  
> * <span data-ttu-id="effbc-126">[ **コレクション** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="effbc-126">Select the **Collections** tab.</span></span> 
> * <span data-ttu-id="effbc-127">**テスト RSC** の横にある山形 (>) を選択して、詳細ビューを展開し、API 要求を表示します。</span><span class="sxs-lookup"><span data-stu-id="effbc-127">Select the chevron (>) next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="effbc-128">API 呼び出しごとに、アクセス許可のコレクション全体を実行します。</span><span class="sxs-lookup"><span data-stu-id="effbc-128">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="effbc-129">アプリのマニフェストで指定したアクセス許可は成功するはずですが、指定されていない場合は、HTTP 403 状態コードで失敗する必要があります。</span><span class="sxs-lookup"><span data-stu-id="effbc-129">The permissions that you specified in your app manifest should succeed, while those not specified should fail with an HTTP 403 status code.</span></span> <span data-ttu-id="effbc-130">すべての応答状態コードを確認して、アプリの RSC アクセス許可の動作が期待どおりかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="effbc-130">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

>[!NOTE]
><span data-ttu-id="effbc-131">特定の削除および読み取り API 呼び出しをテストするには、これらのインスタンスシナリオを JSON ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="effbc-131">To test specific DELETE and READ API calls, please add those instance scenarios to the JSON file.</span></span>

## <a name="test--revoked-rsc-permissions-using-postman"></a><span data-ttu-id="effbc-132">[Postman](https://www.postman.com/)を使用して失効した RSC アクセス許可をテストする</span><span class="sxs-lookup"><span data-stu-id="effbc-132">Test  revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="effbc-133">特定のチームからアプリをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="effbc-133">Uninstall the app from the specific team.</span></span>
> * <span data-ttu-id="effbc-134">[Postman を使用して、追加された RSC のアクセス許可をテスト](#test-added-rsc-permissions-using-the-postman-app)するには、上記の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="effbc-134">Follow the steps above for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
> * <span data-ttu-id="effbc-135">すべての応答状態コードを調べて、成功した特定の API 呼び出しが HTTP 403 状態コードで失敗したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="effbc-135">Check all of the response status codes to confirm that the specific API calls that succeeded have failed with an HTTP 403 status code.</span></span>

> [!div class="nextstepaction"]
>
> [<span data-ttu-id="effbc-136">Graph API と Teams の詳細情報</span><span class="sxs-lookup"><span data-stu-id="effbc-136">Learn more about the Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
