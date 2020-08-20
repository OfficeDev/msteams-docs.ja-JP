---
title: 公開後にすべきこと
description: アプリの公開後にすべきこと
keywords: Teams、公開後、更新、証明書
ms.openlocfilehash: d2cc6c5427c5b4f7320f0ec2e022f2c69467a33d
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819155"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="e5747-104">公開したアプリの保守およびサポート</span><span class="sxs-lookup"><span data-stu-id="e5747-104">Maintain and support your published app</span></span> 

<span data-ttu-id="e5747-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span><span class="sxs-lookup"><span data-stu-id="e5747-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="e5747-106">Microsoft 365 認定</span><span class="sxs-lookup"><span data-stu-id="e5747-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="e5747-107">[Microsoft 365 アプリ コンプライアンス プログラムは、アプリ](./application-certification.md)のセキュリティとコンプライアンスに対する 3 層のアプローチです。</span><span class="sxs-lookup"><span data-stu-id="e5747-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="e5747-108">各層は次の層に基づいて構築されます。レイヤー化されたプログラムは、顧客のニーズに合わせて提供されます。</span><span class="sxs-lookup"><span data-stu-id="e5747-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="e5747-109">コンプライアンス ページにアクセスして、Teams アプリのセキュリティとコンプライアンスの状況の詳細を [確認できます](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)。</span><span class="sxs-lookup"><span data-stu-id="e5747-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="e5747-110">製品サイトに [ダウンロード] ボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="e5747-110">Add a download button to your product site</span></span>

<span data-ttu-id="e5747-111">アプリが Microsoft Teams ストアにある場合、Web サイトのリンクを生成できます。このリンクによって、Teams が起動し、ユーザーがアプリを追加する際の同意とインストールのダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5747-111">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="e5747-112">形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。</span><span class="sxs-lookup"><span data-stu-id="e5747-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="e5747-113">たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。</span><span class="sxs-lookup"><span data-stu-id="e5747-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="e5747-114">既存の Teams アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="e5747-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="e5747-115">アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="e5747-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="e5747-116">代わりに、[概要] タブのアプリのタイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="e5747-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="e5747-117">更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5747-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="e5747-118">マニフェストのバージョン番号をインクリメントします (マニフェストに変更を加えい、申請に変更を加える場合)。</span><span class="sxs-lookup"><span data-stu-id="e5747-118">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="e5747-119">新しいレビューと検証プロセスを行るには、更新された提出が必要です。</span><span class="sxs-lookup"><span data-stu-id="e5747-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="e5747-120">アプリの更新プログラムとユーザー同意フロー</span><span class="sxs-lookup"><span data-stu-id="e5747-120">App updates and the user consent flow</span></span>

<span data-ttu-id="e5747-121">ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5747-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="e5747-122">ほとんどの場合、アプリの更新の完了後には、新しいバージョンがエンド ユーザーに自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5747-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="e5747-123">ただし、Teams アプリ マニフェストには、ユーザー受け [入れが必要](../../../../resources/schema/manifest-schema.md) になる更新プログラムがいくつかあり、これに対して同意する動作を再びトリガーできることが必要になります。</span><span class="sxs-lookup"><span data-stu-id="e5747-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="e5747-124">ボットが追加または削除されました。</span><span class="sxs-lookup"><span data-stu-id="e5747-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="e5747-125">既存のボットの固有の `botId` 値が変更されたとき。</span><span class="sxs-lookup"><span data-stu-id="e5747-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="e5747-126">既存のボットのブー `isNotificationOnly` ル値が変更されました。</span><span class="sxs-lookup"><span data-stu-id="e5747-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="e5747-127">既存のボットのブー `supportsFiles` ル値が変更されました。</span><span class="sxs-lookup"><span data-stu-id="e5747-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="e5747-128">メッセージング拡張機能 ( ) `composeExtensions` が追加または削除されました。</span><span class="sxs-lookup"><span data-stu-id="e5747-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="e5747-129">新しいコネクタが追加されました。</span><span class="sxs-lookup"><span data-stu-id="e5747-129">A new connector was added.</span></span>
> * <span data-ttu-id="e5747-130">新しい静的/個人用タブが追加されました。</span><span class="sxs-lookup"><span data-stu-id="e5747-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="e5747-131">新しい構成可能なグループ/チャネル タブが追加されました。</span><span class="sxs-lookup"><span data-stu-id="e5747-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="e5747-132">値 `webApplicationInfo` は変更されます。</span><span class="sxs-lookup"><span data-stu-id="e5747-132">The `webApplicationInfo` values changed.</span></span>
>
