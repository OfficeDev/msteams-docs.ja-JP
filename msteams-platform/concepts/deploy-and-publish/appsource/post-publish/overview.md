---
title: 公開後にすべきこと
description: アプリの公開後にすべきこと
keywords: Teams、公開後、更新、証明書
ms.openlocfilehash: 77b74d77546de0ae93b0ae39aec925d2e3dec2cf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867096"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="2b567-104">公開したアプリの保守およびサポート</span><span class="sxs-lookup"><span data-stu-id="2b567-104">Maintain and support your published app</span></span> 

<span data-ttu-id="2b567-105">アプリが承認され、公開アプリ カタログに一覧表示されたら、アプリの認定を取得するか、Web サイトに [ダウンロード] ボタンを追加して、利用対象者を増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="2b567-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="2b567-106">アプリケーション証明書</span><span class="sxs-lookup"><span data-stu-id="2b567-106">Application Certificate</span></span>

<span data-ttu-id="2b567-107">Microsoft では、[アプリケーション証明書プログラム](./application-certification.md)を用意しています。アプリ情報を編集するプログラムで、[Microsoft Teams アプリのセキュリティとコンプライアンスのページ](https://aka.ms/AppCertification)で提供されます。</span><span class="sxs-lookup"><span data-stu-id="2b567-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="2b567-108">この情報は、管理者が組織にとって安全なアプリを選択できるようにすることを目的としています。</span><span class="sxs-lookup"><span data-stu-id="2b567-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="2b567-109">製品サイトに [ダウンロード] ボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="2b567-109">Add a download button to your product site</span></span>

<span data-ttu-id="2b567-110">アプリが Microsoft Teams ストアにある場合、Web サイトのリンクを生成できます。このリンクによって、Teams が起動し、ユーザーがアプリを追加する際の同意とインストールのダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b567-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="2b567-111">形式は `https://teams.microsoft.com/l/app/<appId>` で、appID は、送信されたマニフェストで宣言する GUID です。</span><span class="sxs-lookup"><span data-stu-id="2b567-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="2b567-112">たとえば、`https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` は、Trello をインストールするためのリンクになります。</span><span class="sxs-lookup"><span data-stu-id="2b567-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="2b567-113">既存の Teams アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="2b567-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="2b567-114">アプリを再送信する際に、*[新しいアプリの追加]* ボタンは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="2b567-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="2b567-115">代わりに、[概要] タブのアプリのタイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="2b567-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="2b567-116">更新されたマニフェストの appId は、現在のマニフェストと同じであり、バージョンの番号もインクリメントされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b567-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="2b567-117">送信に対してマニフェストに変更を加える場合は、マニフェストでバージョン番号をインクリメントします。</span><span class="sxs-lookup"><span data-stu-id="2b567-117">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="2b567-118">新しいレビューおよび検証プロセスを実行するには、更新された提出を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b567-118">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="2b567-119">アプリの更新とユーザーの同意フロー</span><span class="sxs-lookup"><span data-stu-id="2b567-119">App updates and the user consent flow</span></span>

<span data-ttu-id="2b567-120">ユーザーがアプリケーションをインストールするとき、まず、アプリがジョブを実行するのに必要なサービスと情報へのアクセス許可をアプリに与えることに同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2b567-120">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="2b567-121">ほとんどの場合、アプリの更新が完了すると、新しいバージョンがエンドユーザーに対して自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2b567-121">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="2b567-122">ただし、 [Teams アプリのマニフェスト](../../../../resources/schema/manifest-schema.md)には、ユーザーの承認を完了し、この同意の動作を再始動する必要がある、いくつかの更新があります。</span><span class="sxs-lookup"><span data-stu-id="2b567-122">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="2b567-123">Bot が追加または削除されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-123">A bot was added or removed.</span></span>
> * <span data-ttu-id="2b567-124">既存の bot の一意の `botId` 値が変更されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-124">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="2b567-125">既存の bot の `isNotificationOnly` ブール値が変更されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-125">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="2b567-126">既存の bot の `supportsFiles` ブール値が変更されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-126">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="2b567-127">メッセージング拡張機能 ( `composeExtensions` ) が追加または削除されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-127">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="2b567-128">新しいコネクタが追加されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-128">A new connector was added.</span></span>
> * <span data-ttu-id="2b567-129">新しい静的/個人用タブが追加されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-129">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="2b567-130">新しい [構成可能なグループ/チャネル] タブが追加されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-130">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="2b567-131">`webApplicationInfo`値が変更されました。</span><span class="sxs-lookup"><span data-stu-id="2b567-131">The `webApplicationInfo` values changed.</span></span>
>