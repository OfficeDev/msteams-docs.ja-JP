---
title: 公開したアプリの保守およびサポート
description: ストアがアプリ ストアと AppSource に一覧表示された後Teams考える必要があります。
ms.topic: conceptual
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 8e4656ea7ca9f373123026a50ecb837d1a64e3fa
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230918"
---
# <a name="maintain-your-published-microsoft-teams-app"></a><span data-ttu-id="7f891-103">公開済みアプリのMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="7f891-103">Maintain your published Microsoft Teams app</span></span>

<span data-ttu-id="7f891-104">アプリが Microsoft Teamsストアに表示された状態で、今後アプリを維持する方法について考え始め、ダウンロードと使用状況を増やします。</span><span class="sxs-lookup"><span data-stu-id="7f891-104">With your app listed on the Microsoft Teams store, start thinking about how you'll maintain the app going forward and increase downloads and usage.</span></span>

## <a name="publish-updates-to-your-app"></a><span data-ttu-id="7f891-105">アプリに更新プログラムを発行する</span><span class="sxs-lookup"><span data-stu-id="7f891-105">Publish updates to your app</span></span>

<span data-ttu-id="7f891-106">パートナー センターでは、アプリに変更 (新機能やメタデータなど) を送信できます。</span><span class="sxs-lookup"><span data-stu-id="7f891-106">You can submit changes to your app (such as new features or even metadata) in Partner Center.</span></span> <span data-ttu-id="7f891-107">これらの変更には、新しいレビュー プロセスが必要です。</span><span class="sxs-lookup"><span data-stu-id="7f891-107">These changes requires a new review process.</span></span>

<span data-ttu-id="7f891-108">更新プログラムを発行する場合は、次の情報を確認してください。</span><span class="sxs-lookup"><span data-stu-id="7f891-108">Ensure the following when publishing updates:</span></span>

* <span data-ttu-id="7f891-109">アプリ ID を変更しない。</span><span class="sxs-lookup"><span data-stu-id="7f891-109">Don't change your app ID.</span></span>
* <span data-ttu-id="7f891-110">アプリのバージョン番号を増やします。</span><span class="sxs-lookup"><span data-stu-id="7f891-110">Increment your app's version number.</span></span>
* <span data-ttu-id="7f891-111">パートナー センターで、[新しいアプリの追加] **を選択して** 更新を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="7f891-111">In Partner Center, don't select **Add a new app** to do the update.</span></span> <span data-ttu-id="7f891-112">代わりにアプリのページに移動します。</span><span class="sxs-lookup"><span data-stu-id="7f891-112">Go to your app's page instead.</span></span>

### <a name="app-updates-requiring-user-consent"></a><span data-ttu-id="7f891-113">ユーザーの同意を必要とするアプリの更新</span><span class="sxs-lookup"><span data-stu-id="7f891-113">App updates requiring user consent</span></span>

<span data-ttu-id="7f891-114">ユーザーがアプリをインストールする場合、アプリが機能するために必要なサービスと情報にアクセスするためのアクセス許可をアプリに付与する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7f891-114">When a user installs your app, they must give the app permission to access the services and information the app requires to function.</span></span> <span data-ttu-id="7f891-115">ほとんどの場合、ユーザーはこれを行う必要があるだけで、アプリの新しいバージョンが自動的にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="7f891-115">In most cases, users only have to do this once and new versions of your app install automatically.</span></span>

<span data-ttu-id="7f891-116">ただし、アプリに次の変更を加えた場合、既存のユーザーは更新プログラムをインストールするための別のアクセス許可要求を受け入れる必要があります。</span><span class="sxs-lookup"><span data-stu-id="7f891-116">If you make any of the following changes to your app, however, your existing users must accept another permission request to install the update:</span></span>

* <span data-ttu-id="7f891-117">ボットを追加または削除します。</span><span class="sxs-lookup"><span data-stu-id="7f891-117">Add or remove a bot.</span></span>
* <span data-ttu-id="7f891-118">ボット ID を変更します。</span><span class="sxs-lookup"><span data-stu-id="7f891-118">Change the bot ID.</span></span>
* <span data-ttu-id="7f891-119">ボットの一方通行通知構成を変更します。</span><span class="sxs-lookup"><span data-stu-id="7f891-119">Modify a bot's one-way notification configuration.</span></span>
* <span data-ttu-id="7f891-120">ファイルのアップロードとダウンロードに関するボットのサポートを変更します。</span><span class="sxs-lookup"><span data-stu-id="7f891-120">Modify a bot's support for uploading and downloading files.</span></span>
* <span data-ttu-id="7f891-121">メッセージング拡張機能を追加または削除します。</span><span class="sxs-lookup"><span data-stu-id="7f891-121">Add or remove a messaging extension.</span></span>
* <span data-ttu-id="7f891-122">個人用タブを追加します。</span><span class="sxs-lookup"><span data-stu-id="7f891-122">Add a personal tab.</span></span>
* <span data-ttu-id="7f891-123">[チャネルとグループ] タブを追加します。</span><span class="sxs-lookup"><span data-stu-id="7f891-123">Add a channel and group tab.</span></span>
* <span data-ttu-id="7f891-124">コネクタを追加します。</span><span class="sxs-lookup"><span data-stu-id="7f891-124">Add a connector.</span></span>
* <span data-ttu-id="7f891-125">アプリ登録 (Azure Azure Active Directory) にAD構成を変更します。</span><span class="sxs-lookup"><span data-stu-id="7f891-125">Modify configurations related to your Azure Active Directory (Azure AD) app registration.</span></span> <span data-ttu-id="7f891-126">詳細については、「」 を参照してください [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) 。</span><span class="sxs-lookup"><span data-stu-id="7f891-126">For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).</span></span>

## <a name="fix-issues-with-your-published-app"></a><span data-ttu-id="7f891-127">発行済みアプリの問題を修正する</span><span class="sxs-lookup"><span data-stu-id="7f891-127">Fix issues with your published app</span></span>

<span data-ttu-id="7f891-128">Microsoft は、アプリ ストアに一覧表示されているアプリで毎日自動化テストTeams実行します。</span><span class="sxs-lookup"><span data-stu-id="7f891-128">Microsoft runs daily automation tests on apps listed on the Teams store.</span></span> <span data-ttu-id="7f891-129">アプリに関する問題が特定された場合は、問題を再現する方法と問題を解決するための推奨事項に関する詳細なレポートをお客様に連絡します。</span><span class="sxs-lookup"><span data-stu-id="7f891-129">If issues with your app are identified, we contact you with a detailed report on how to reproduce the issues and recommendations to resolve them.</span></span> <span data-ttu-id="7f891-130">指定したタイムライン内で問題を解決できない場合は、アプリの登録情報がストアから削除される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7f891-130">If you can't fix the problems within a stated timeline, your app listing may be removed from the store.</span></span>

## <a name="promote-your-app-on-another-site"></a><span data-ttu-id="7f891-131">別のサイトでアプリを宣伝する</span><span class="sxs-lookup"><span data-stu-id="7f891-131">Promote your app on another site</span></span>

<span data-ttu-id="7f891-132">アプリが Teams ストアに表示されている場合は、Teamsを起動し、アプリをインストールするダイアログを表示するリンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="7f891-132">When your app is listed in the Teams store, you can create a link that launches Teams and displays a dialog to install your app.</span></span> <span data-ttu-id="7f891-133">たとえば、製品のマーケティング ページにダウンロード ボタンを使用して、このリンクを含めできます。</span><span class="sxs-lookup"><span data-stu-id="7f891-133">You could include this link, for example, with a download button on your product's marketing page.</span></span>

<span data-ttu-id="7f891-134">アプリ ID に追加された次の URL を使用してリンクを作成します `https://teams.microsoft.com/l/app/<your-app-id>` 。</span><span class="sxs-lookup"><span data-stu-id="7f891-134">Create the link using the following URL appended with your app ID: `https://teams.microsoft.com/l/app/<your-app-id>`.</span></span>

## <a name="complete-microsoft-365-certification"></a><span data-ttu-id="7f891-135">完全なMicrosoft 365認定</span><span class="sxs-lookup"><span data-stu-id="7f891-135">Complete Microsoft 365 Certification</span></span>

<span data-ttu-id="7f891-136">[Microsoft 365認定は](/microsoft-365-app-certification/docs/certification)、サード パーティ製の Office アプリ またはアドインが Microsoft 365 エコシステムにインストールされている場合に、データとプライバシーが適切に保護され、保護されていることを保証します。</span><span class="sxs-lookup"><span data-stu-id="7f891-136">[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) offers assurances that data and privacy are adequately secured and protected when a third-party Office app or add-in is installed in your Microsoft 365 ecosystem.</span></span> <span data-ttu-id="7f891-137">認定は、アプリが Microsoft テクノロジと互換性があり、クラウド アプリのセキュリティのベスト プラクティスに準拠しており、Microsoft によってサポートされていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="7f891-137">Certification confirms that your app is compatible with Microsoft technologies, compliant with cloud app security best practices, and supported by Microsoft.</span></span>

## <a name="see-also"></a><span data-ttu-id="7f891-138">こちらもご覧ください</span><span class="sxs-lookup"><span data-stu-id="7f891-138">See also</span></span>

[<span data-ttu-id="7f891-139">Microsoft Commercial Marketplace を通してアプリを収益化する</span><span class="sxs-lookup"><span data-stu-id="7f891-139">Monetize your app through Microsoft Commercial Marketplace</span></span>](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
