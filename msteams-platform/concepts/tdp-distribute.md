---
title: アプリの配布
description: 開発者ポータルを使用してアプリを配布する方法についてMicrosoft Teams。
keywords: 開発者ポータル チームの開始
localization_priority: Normal
ms.topic: Conceptual
ms.openlocfilehash: d1d098b295492a7dc3b691db4625307b6c3170ce
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635091"
---
# <a name="distribute-your-apps"></a><span data-ttu-id="49f13-104">アプリの配布</span><span class="sxs-lookup"><span data-stu-id="49f13-104">Distribute your apps</span></span>

## <a name="distribute"></a><span data-ttu-id="49f13-105">均等割り付け</span><span class="sxs-lookup"><span data-stu-id="49f13-105">Distribute</span></span>

<span data-ttu-id="49f13-106">アプリケーションの定義が完了したら、[配布] セクションを使用してアプリの定義を zip ファイルとしてエクスポートし、テスト用に Teams クライアントに共有およびアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="49f13-106">After you have finished defining your application, the **Distribute** section allows you to export your app’s definition as a zip file which then can be shared and uploaded into the Teams client for testing.</span></span> <span data-ttu-id="49f13-107">[Export] (エクスポート) をクリックすると、zip ファイルが **appname.zip** として既定のダウンロード ディレクトリにダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="49f13-107">Clicking export downloads the zip file as **appname.zip** in your default download directory.</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_distribute_1.png" alt-text="開発者ポータルの [配布] ページをTeamsスクリーンショット。":::

### <a name="manifest"></a><span data-ttu-id="49f13-109">マニフェスト</span><span class="sxs-lookup"><span data-stu-id="49f13-109">Manifest</span></span>

<span data-ttu-id="49f13-110">マニフェストは、アプリの機能、必要なリソース、その他の重要な属性など、アプリの構成方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="49f13-110">The manifest describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span> <span data-ttu-id="49f13-111">詳細 [については、「マニフェスト スキーマ](~/resources/schema/manifest-schema.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="49f13-111">See [manifest schema](~/resources/schema/manifest-schema.md) for more information.</span></span>

### <a name="flights"></a><span data-ttu-id="49f13-112">フライト</span><span class="sxs-lookup"><span data-stu-id="49f13-112">Flights</span></span>

<span data-ttu-id="49f13-113">アプリの更新プログラムを取得するユーザーを制御します。</span><span class="sxs-lookup"><span data-stu-id="49f13-113">Control who gets app updates.</span></span> <span data-ttu-id="49f13-114">たとえば、Microsoft の従業員に更新プログラムをリリースして、バグを特定して修正してから一般公開することができます。</span><span class="sxs-lookup"><span data-stu-id="49f13-114">For example, you can release an update to Microsoft employees to identify and fix bugs before releasing it to the public.</span></span> <span data-ttu-id="49f13-115">[新 **しい要求の作成] を** 選択して、新しいフライト要求を作成します。</span><span class="sxs-lookup"><span data-stu-id="49f13-115">Select **Create a New Request** to create a new flight request.</span></span>

### <a name="publish-to-org"></a><span data-ttu-id="49f13-116">組織に発行する</span><span class="sxs-lookup"><span data-stu-id="49f13-116">Publish to org</span></span>

<span data-ttu-id="49f13-117">組織のユーザーがアプリを利用できます。IT 管理者によって承認されると、組織向けの [アプリ] Teams [>] の下にアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="49f13-117">Make your app available to people in your org. Once approved by your IT admin, your app will be featured in Teams under Apps > Built for your org.</span></span>

### <a name="publish-your-app-to-teams-store"></a><span data-ttu-id="49f13-118">アプリをストアにTeamsする</span><span class="sxs-lookup"><span data-stu-id="49f13-118">Publish your app to Teams store</span></span>

<span data-ttu-id="49f13-119">プロジェクトのホーム ページでは、アプリをチーム向けにアップロードしたり、組織内のユーザー向けに会社のカスタム App Store に提出したり、すべての Teams ユーザー向けに App Source に提出したりできます。</span><span class="sxs-lookup"><span data-stu-id="49f13-119">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="49f13-120">これらの送信内容は、IT 管理者によって審査されます。</span><span class="sxs-lookup"><span data-stu-id="49f13-120">Your IT admin will review these submissions.</span></span> <span data-ttu-id="49f13-121">**[Publish]** (発行) ページに戻ると提出ステータスを確認することができ、アプリが IT 管理者によって承認または却下されたかどうかを確認できます。このページでは、アプリの更新プログラムを提出したり、現在提出中のアプリをキャンセルしたりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="49f13-121">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="see-also"></a><span data-ttu-id="49f13-122">関連項目</span><span class="sxs-lookup"><span data-stu-id="49f13-122">See also</span></span>

* [<span data-ttu-id="49f13-123">開発者ポータルTeams概要</span><span class="sxs-lookup"><span data-stu-id="49f13-123">Overview of Teams Developer Portal</span></span>](~/concepts/build-and-test/teams-developer-portal.md)
* [<span data-ttu-id="49f13-124">開発者ポータルTeams構成する</span><span class="sxs-lookup"><span data-stu-id="49f13-124">Configure Teams Developer Portal</span></span>](~/concepts/tdp-configuration.md)
* [<span data-ttu-id="49f13-125">開発者ポータルTeamsツール</span><span class="sxs-lookup"><span data-stu-id="49f13-125">Tools in Teams Developer Portal</span></span>](~/concepts/tdp-tools.md)