---
title: 公開されたアプリの保守とサポート
description: アプリの公開後にすべきこと
ms.topic: how-to
keywords: teams post publish update certification app update manifest
ms.openlocfilehash: ce63b840307f7e12a5cd05a1c67aed017cf6199b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014328"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="637eb-104">公開したアプリの保守およびサポート</span><span class="sxs-lookup"><span data-stu-id="637eb-104">Maintain and support your published app</span></span> 

<span data-ttu-id="637eb-105">アプリが承認され、公開アプリ カタログに一覧表示された後は、Microsoft 365 アプリ コンプライアンス プログラムを完了するか、Web サイトにダウンロード ボタンを追加することで、リーチを拡大できます。</span><span class="sxs-lookup"><span data-stu-id="637eb-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="637eb-106">Microsoft 365 認定</span><span class="sxs-lookup"><span data-stu-id="637eb-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="637eb-107">[Microsoft 365 アプリ コンプライアンス](./application-certification.md)プログラムは、アプリのセキュリティとコンプライアンスに対する 3 層のアプローチです。</span><span class="sxs-lookup"><span data-stu-id="637eb-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="637eb-108">各層は次の階層に構築されます。お客様のニーズに合わせて階層化されたプログラムを提供します。</span><span class="sxs-lookup"><span data-stu-id="637eb-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="637eb-109">Teams アプリのセキュリティとコンプライアンスの体制の詳細については、コンプライアンス ページを [参照してください](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)。</span><span class="sxs-lookup"><span data-stu-id="637eb-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="637eb-110">製品サイトに [ダウンロード] ボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="637eb-110">Add a download button to your product site</span></span>

<span data-ttu-id="637eb-111">アプリが Microsoft Teams グローバル ストアにある場合は、Teams を起動し、ユーザーがアプリを追加する同意とインストールダイアログを表示する Web サイトのリンクを生成できます。</span><span class="sxs-lookup"><span data-stu-id="637eb-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="637eb-112">形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。</span><span class="sxs-lookup"><span data-stu-id="637eb-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="637eb-113">たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。</span><span class="sxs-lookup"><span data-stu-id="637eb-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="637eb-114">既存の Teams アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="637eb-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="637eb-115">アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="637eb-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="637eb-116">代わりに、[概要] タブのアプリのタイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="637eb-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="637eb-117">更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="637eb-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="637eb-118">アプリ名やマニフェスト内のメタデータなど、申請に変更を加えた場合は、マニフェストでバージョン番号を増やします。</span><span class="sxs-lookup"><span data-stu-id="637eb-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="637eb-119">更新された提出は、新しいレビューと検証プロセスを受ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="637eb-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="637eb-120">アプリの更新とユーザーの同意フロー</span><span class="sxs-lookup"><span data-stu-id="637eb-120">App updates and the user consent flow</span></span>

<span data-ttu-id="637eb-121">ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="637eb-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="637eb-122">ほとんどの場合、アプリの更新が完了すると、エンド ユーザーに新しいバージョンが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="637eb-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="637eb-123">ただし [、Teams](../../../../resources/schema/manifest-schema.md) アプリ マニフェストには、完了するためにユーザー承認が必要で、この同意動作を再トリガーできる更新プログラムがいくつか含まれています。</span><span class="sxs-lookup"><span data-stu-id="637eb-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="637eb-124">ボットが追加または削除されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="637eb-125">既存のボットの一意の値 `botId` が変更されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="637eb-126">既存のボットのブール値 `isNotificationOnly` が変更されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="637eb-127">既存のボットのブール値 `supportsFiles` が変更されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="637eb-128">メッセージング拡張機能 ( `composeExtensions` ) が追加または削除されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="637eb-129">新しいコネクタが追加されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-129">A new connector was added.</span></span>
> * <span data-ttu-id="637eb-130">新しい静的/個人用タブが追加されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="637eb-131">新しい構成可能なグループ/チャネル タブが追加されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="637eb-132">値 `webApplicationInfo` が変更されました。</span><span class="sxs-lookup"><span data-stu-id="637eb-132">The `webApplicationInfo` values changed.</span></span>
>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="637eb-133">ユーザーの同意フローの画像:</span><span class="sxs-lookup"><span data-stu-id="637eb-133">Images of user consent flow:</span></span>

<span data-ttu-id="637eb-134">**コネクタのセットアップ** - この画面は Teams ユーザーにのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="637eb-134">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![同意フローのセットアップコネクタ図](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="637eb-136">**ユーザーの同意フロー** - この画面は、個人用スコープとグループ スコープの両方で一般的です。</span><span class="sxs-lookup"><span data-stu-id="637eb-136">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="637eb-137">ここで、組織の代 **わりに [同意** ] チェック ボックスをオンにし、[承諾] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="637eb-137">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![アクセス許可の図](../../../../assets/images/user-consent-flow.png)
