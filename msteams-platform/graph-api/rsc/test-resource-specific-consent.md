---
title: リソース固有の同意のアクセス許可をテストTeams
description: Postman を使用したリソース固有の同意Teamsテストする詳細
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 承認 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 328be5b4f1e3597457afb9ce1413eb35aa2df71e
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075620"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="4fcc5-104">リソース固有の同意のアクセス許可をテストTeams</span><span class="sxs-lookup"><span data-stu-id="4fcc5-104">Test resource-specific consent permissions in Teams</span></span>

<span data-ttu-id="4fcc5-105">リソース固有の同意 (RSC) は、アプリが API エンドポイントを使用して組織内の特定のチームを管理Microsoft Teamsおよび Graph API 統合です。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="4fcc5-106">詳細については、「リソース固有[の同意 (RSC) - Microsoft Teams Graph API 」を参照してください](resource-specific-consent.md)。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-106">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4fcc5-107">RSC アクセス許可をテストするには、Teamsアプリ マニフェスト ファイルに、次のフィールドが設定された **webApplicationInfo** キーを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="4fcc5-108">**id**: Azure ADアプリ ID については、「Azure アプリ ポータルにアプリを登録する [」をADしてください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-108">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="4fcc5-109">**resource**: 任意の文字列は、「アプリ マニフェストの更新 [」のTeams参照してください](resource-specific-consent.md#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-109">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="4fcc5-110">**アプリケーションのアクセス許可**: アプリの RSC アクセス許可については、「リソース固有の [アクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-110">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

> [!IMPORTANT]
> <span data-ttu-id="4fcc5-111">アプリ マニフェストには、アプリに付与する RSC アクセス許可のみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="4fcc5-112">Postman アプリを使用して追加された RSC アクセス許可をテストする</span><span class="sxs-lookup"><span data-stu-id="4fcc5-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="4fcc5-113">RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには [、RSC JSON](test-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-113">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="4fcc5-114">`azureADAppId`: アプリの Azure AD ID。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-114">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="4fcc5-115">`azureADAppSecret`: Azure ADパスワード。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-115">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="4fcc5-116">`token_scope`: トークンを取得するには、スコープが必要です。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-116">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="4fcc5-117">に値を設定します https://graph.microsoft.com/.default 。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-117">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="4fcc5-118">`teamGroupId`: 次のように、チーム グループ ID をクライアントTeams取得できます。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-118">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="4fcc5-119">クライアントで、Teams **バーから**[Teams] を選択します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-119">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="4fcc5-120">ドロップダウン メニューからアプリがインストールされているチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-120">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="4fcc5-121">[その他 **のオプション]** アイコンを選択します (&#8943;)。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-121">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="4fcc5-122">[チーム **へのリンクを取得する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-122">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="4fcc5-123">文字列から **groupId 値をコピー** して保存します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-123">Copy and save the **groupId** value from the string.</span></span>

### <a name="use-postman"></a><span data-ttu-id="4fcc5-124">Postman の使用</span><span class="sxs-lookup"><span data-stu-id="4fcc5-124">Use Postman</span></span>

1. <span data-ttu-id="4fcc5-125">Postman [アプリを開](https://www.postman.com) きます。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-125">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="4fcc5-126">[**ファイル**  >  **インポート ファイル**  >  **] を選択** して、更新された JSON ファイルを環境からアップロードします。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-126">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="4fcc5-127">[コレクション **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-127">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="4fcc5-128">テスト RSC の横にあるシェブロンを選択して詳細ビューを **>** 展開し、API 要求を表示します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-128">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="4fcc5-129">API 呼び出しごとにアクセス許可コレクション全体を実行します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-129">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="4fcc5-130">アプリ マニフェストで指定したアクセス許可は成功する必要があります。指定されていないアクセス許可は HTTP 403 状態コードで失敗する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-130">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="4fcc5-131">すべての応答状態コードを確認して、アプリ内の RSC アクセス許可の動作が期待を満たしている状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-131">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="4fcc5-132">特定の DELETE および READ API 呼び出しをテストするには、それらのインスタンス シナリオを JSON ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-132">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="4fcc5-133">Postman を使用して取り消された RSC アクセス [許可をテストする](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="4fcc5-133">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="4fcc5-134">特定のチームからアプリをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-134">Uninstall the app from the specific team.</span></span>
2. <span data-ttu-id="4fcc5-135">Postman を使用して [RSC アクセス許可を追加したテストの手順に従います](#test-added-rsc-permissions-using-the-postman-app)。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-135">Follow the steps for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
3. <span data-ttu-id="4fcc5-136">すべての応答状態コードを確認して、特定の API 呼び出しが成功し **、HTTP 403** 状態コードで失敗したと確認します。</span><span class="sxs-lookup"><span data-stu-id="4fcc5-136">Check all the response status codes to confirm that the specific API calls, **succeeded, have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="4fcc5-137">関連項目</span><span class="sxs-lookup"><span data-stu-id="4fcc5-137">See also</span></span>

[<span data-ttu-id="4fcc5-138">Microsoft Graph API と Teams</span><span class="sxs-lookup"><span data-stu-id="4fcc5-138">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

