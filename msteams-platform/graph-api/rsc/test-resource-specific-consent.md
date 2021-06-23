---
title: リソース固有の同意のアクセス許可をテストTeams
description: Postman を使用したリソース固有の同意Teamsテストする詳細
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 承認 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 92c6d5d96c103fb5e0da6afd91357b5887b2ba10
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069083"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="5761d-104">リソース固有の同意のアクセス許可をテストTeams</span><span class="sxs-lookup"><span data-stu-id="5761d-104">Test resource-specific consent permissions in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="5761d-105">チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。</span><span class="sxs-lookup"><span data-stu-id="5761d-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="5761d-106">リソース固有の同意 (RSC) は、Microsoft Teams と Graph API の統合であり、アプリは API エンドポイントを使用して組織内の特定のリソース (チームまたはチャット) を管理できます。</span><span class="sxs-lookup"><span data-stu-id="5761d-106">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="5761d-107">詳細については、「リソース固有[の同意 (RSC) - Microsoft Teams Graph API 」を参照してください](resource-specific-consent.md)。</span><span class="sxs-lookup"><span data-stu-id="5761d-107">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5761d-108">RSC アクセス許可をテストするには、Teamsアプリ マニフェスト ファイルに、次のフィールドが設定された **webApplicationInfo** キーを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5761d-108">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="5761d-109">**id**: Azure ADアプリ ID については、「Azure アプリ ポータルにアプリを登録する [」をADしてください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="5761d-109">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="5761d-110">**resource**: 任意の文字列は、「アプリ マニフェストの更新 [」のTeams参照してください](resource-specific-consent.md#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="5761d-110">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="5761d-111">**アプリケーションのアクセス許可**: アプリの RSC アクセス許可については、「リソース固有の [アクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="5761d-111">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

## <a name="example-for-a-team"></a><span data-ttu-id="5761d-112">チームの例</span><span class="sxs-lookup"><span data-stu-id="5761d-112">Example for a team</span></span>
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

## <a name="example-for-a-chat"></a><span data-ttu-id="5761d-113">チャットの例</span><span class="sxs-lookup"><span data-stu-id="5761d-113">Example for a chat</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
          "ChatSettings.Read.Chat",
          "ChatSettings.ReadWrite.Chat",
          "ChatMessage.Read.Chat",
          "ChatMember.Read.Chat",
          "Chat.Manage.Chat",
          "TeamsTab.Read.Chat",
          "TeamsTab.Create.Chat",
          "TeamsTab.Delete.Chat",
          "TeamsTab.ReadWrite.Chat",
          "TeamsAppInstallation.Read.Chat",
          "OnlineMeeting.ReadBasic.Chat"
      ]
   }
```

> [!IMPORTANT]
> <span data-ttu-id="5761d-114">アプリ マニフェストには、アプリに付与する RSC アクセス許可のみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5761d-114">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

>[!NOTE]
><span data-ttu-id="5761d-115">アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions` 。</span><span class="sxs-lookup"><span data-stu-id="5761d-115">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a><span data-ttu-id="5761d-116">Postman アプリを使用してチームに追加された RSC アクセス許可をテストする</span><span class="sxs-lookup"><span data-stu-id="5761d-116">Test added RSC permissions to a team using the Postman app</span></span>

<span data-ttu-id="5761d-117">RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チームの [RSC JSON](test-team-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5761d-117">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for team](test-team-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="5761d-118">`azureADAppId`: アプリの Azure AD ID。</span><span class="sxs-lookup"><span data-stu-id="5761d-118">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="5761d-119">`azureADAppSecret`: Azure ADパスワード。</span><span class="sxs-lookup"><span data-stu-id="5761d-119">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="5761d-120">`token_scope`: トークンを取得するには、スコープが必要です。</span><span class="sxs-lookup"><span data-stu-id="5761d-120">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="5761d-121">に値を設定します https://graph.microsoft.com/.default 。</span><span class="sxs-lookup"><span data-stu-id="5761d-121">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="5761d-122">`teamGroupId`: 次のように、チーム グループ ID をクライアントTeams取得できます。</span><span class="sxs-lookup"><span data-stu-id="5761d-122">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="5761d-123">クライアントで、Teams **バーから**[Teams] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5761d-123">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="5761d-124">ドロップダウン メニューからアプリがインストールされているチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="5761d-124">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="5761d-125">[その他 **のオプション]** アイコンを選択します (&#8943;)。</span><span class="sxs-lookup"><span data-stu-id="5761d-125">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="5761d-126">[チーム **へのリンクを取得する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="5761d-126">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="5761d-127">文字列から **groupId 値をコピー** して保存します。</span><span class="sxs-lookup"><span data-stu-id="5761d-127">Copy and save the **groupId** value from the string.</span></span>

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a><span data-ttu-id="5761d-128">Postman アプリを使用してチャットに追加された RSC アクセス許可をテストする</span><span class="sxs-lookup"><span data-stu-id="5761d-128">Test added RSC permissions to a chat using the Postman app</span></span>

<span data-ttu-id="5761d-129">RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チャットの [RSC JSON](test-chat-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5761d-129">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for chats](test-chat-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="5761d-130">`azureADAppId`: アプリの Azure AD ID。</span><span class="sxs-lookup"><span data-stu-id="5761d-130">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="5761d-131">`azureADAppSecret`: Azure ADパスワード。</span><span class="sxs-lookup"><span data-stu-id="5761d-131">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="5761d-132">`token_scope`: トークンを取得するには、スコープが必要です。</span><span class="sxs-lookup"><span data-stu-id="5761d-132">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="5761d-133">に値を設定します https://graph.microsoft.com/.default 。</span><span class="sxs-lookup"><span data-stu-id="5761d-133">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="5761d-134">`tenantId`: テナントの名前または AAD オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="5761d-134">`tenantId`: The name or the AAD Object ID of your tenant.</span></span>
* <span data-ttu-id="5761d-135">`chatId`: 次のように、Web クライアントからチャット スレッド id をTeams *取得* できます。</span><span class="sxs-lookup"><span data-stu-id="5761d-135">`chatId`: You can get the chat thread id from the Teams *web* client as follows:</span></span>

    1. <span data-ttu-id="5761d-136">Web クライアントTeams、左側 **のナビゲーション** バーから [チャット] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5761d-136">In the Teams web client, select **Chat** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="5761d-137">アプリがインストールされているチャットをドロップダウン メニューから選択します。</span><span class="sxs-lookup"><span data-stu-id="5761d-137">Select the chat where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="5761d-138">Web URL をコピーし、文字列からチャット スレッド ID を保存します。</span><span class="sxs-lookup"><span data-stu-id="5761d-138">Copy the web URL and save the chat thread id from the string.</span></span>
<span data-ttu-id="5761d-139">![Web URL からのチャット スレッド ID。](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="5761d-139">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>

### <a name="use-postman"></a><span data-ttu-id="5761d-140">Postman の使用</span><span class="sxs-lookup"><span data-stu-id="5761d-140">Use Postman</span></span>

1. <span data-ttu-id="5761d-141">Postman [アプリを開](https://www.postman.com) きます。</span><span class="sxs-lookup"><span data-stu-id="5761d-141">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="5761d-142">[**ファイル**  >  **インポート ファイル**  >  **] を選択** して、更新された JSON ファイルを環境からアップロードします。</span><span class="sxs-lookup"><span data-stu-id="5761d-142">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="5761d-143">[コレクション **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="5761d-143">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="5761d-144">テスト RSC の横にあるシェブロンを選択して詳細ビューを **>** 展開し、API 要求を表示します。</span><span class="sxs-lookup"><span data-stu-id="5761d-144">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="5761d-145">API 呼び出しごとにアクセス許可コレクション全体を実行します。</span><span class="sxs-lookup"><span data-stu-id="5761d-145">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="5761d-146">アプリ マニフェストで指定したアクセス許可は成功する必要があります。指定されていないアクセス許可は HTTP 403 状態コードで失敗する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5761d-146">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="5761d-147">すべての応答状態コードを確認して、アプリ内の RSC アクセス許可の動作が期待を満たしている状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="5761d-147">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="5761d-148">特定の DELETE および READ API 呼び出しをテストするには、それらのインスタンス シナリオを JSON ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="5761d-148">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="5761d-149">Postman を使用して取り消された RSC アクセス [許可をテストする](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="5761d-149">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="5761d-150">特定のリソースからアプリをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="5761d-150">Uninstall the app from the specific resource.</span></span>
2. <span data-ttu-id="5761d-151">チャットまたはチームの手順に従います。</span><span class="sxs-lookup"><span data-stu-id="5761d-151">Follow the steps for either chat or team:</span></span> 
    1. <span data-ttu-id="5761d-152">[Postman を使用してチームに追加された RSC アクセス許可をテストします](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。</span><span class="sxs-lookup"><span data-stu-id="5761d-152">[Test added RSC permissions to a team using Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).</span></span>
    2. <span data-ttu-id="5761d-153">[Postman を使用してチャットに追加された RSC アクセス許可をテストします](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。</span><span class="sxs-lookup"><span data-stu-id="5761d-153">[Test added RSC permissions to a chat using Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).</span></span>
3. <span data-ttu-id="5761d-154">すべての応答状態コードを確認して、HTTP 403 状態コードで特定の API 呼び出し **が失敗したと確認します**。</span><span class="sxs-lookup"><span data-stu-id="5761d-154">Check all the response status codes to confirm that the specific API calls **have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="5761d-155">関連項目</span><span class="sxs-lookup"><span data-stu-id="5761d-155">See also</span></span>

[<span data-ttu-id="5761d-156">Microsoft Graph API と Teams</span><span class="sxs-lookup"><span data-stu-id="5761d-156">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

