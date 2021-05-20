---
title: カスタム アプリのアップロード
description: Microsoft Teamsでアプリをサイドロードする方法について説明します。 サイドローディングは、開発中にアプリをテストおよびデバッグするときに一般的です。
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565194"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="13198-104">アプリをMicrosoft Teamsでアップロードする</span><span class="sxs-lookup"><span data-stu-id="13198-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="13198-105">組織やTeamsストアに公開しなくても、Microsoft Teamsアプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="13198-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="13198-106">これは、次のシナリオで意味をなします。</span><span class="sxs-lookup"><span data-stu-id="13198-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="13198-107">ローカルで、または他の開発者と共にアプリをテストおよびデバッグする場合。</span><span class="sxs-lookup"><span data-stu-id="13198-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="13198-108">自分のためだけにアプリを構築しました。</span><span class="sxs-lookup"><span data-stu-id="13198-108">You built an app just for yourself.</span></span> <span data-ttu-id="13198-109">たとえば、ワークフローを自動化します。</span><span class="sxs-lookup"><span data-stu-id="13198-109">For example, to automate a workflow.</span></span>
* <span data-ttu-id="13198-110">作業グループなど、少数のユーザー向けのアプリを構築しました。</span><span class="sxs-lookup"><span data-stu-id="13198-110">You built an app for a small set of users, such as, your work group.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13198-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="13198-111">Prerequisites</span></span>

* <span data-ttu-id="13198-112">アプリ [パッケージ](~/concepts/build-and-test/apps-package.md) を作成し、エラーを [検証](https://dev.teams.microsoft.com/appvalidation.html) します。</span><span class="sxs-lookup"><span data-stu-id="13198-112">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="13198-113">Teams[でカスタム アプリのアップロードを有効にします](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。</span><span class="sxs-lookup"><span data-stu-id="13198-113">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="13198-114">アプリが実行され、HTTP 経由でアクセス可能であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="13198-114">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="13198-115">アプリをアップロードする</span><span class="sxs-lookup"><span data-stu-id="13198-115">Upload your app</span></span>

<span data-ttu-id="13198-116">アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人向けにアプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="13198-116">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="13198-117">[Microsoft 365開発アカウント](~/build-your-first-app/build-and-run.md#prerequisites)でTeamsクライアントにログインします。</span><span class="sxs-lookup"><span data-stu-id="13198-117">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="13198-118">[**アプリ] を** 選択し、[**カスタム アプリアップロード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="13198-118">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="13198-119">アプリ パッケージ.zipファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="13198-119">Select your app package .zip file.</span></span> <span data-ttu-id="13198-120">インストールダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="13198-120">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Teamsアプリのインストール ダイアログの例を示すスクリーンショット。":::
1. <span data-ttu-id="13198-122">アプリをTeamsに追加します。</span><span class="sxs-lookup"><span data-stu-id="13198-122">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="13198-123">アップロードに関する問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="13198-123">Troubleshoot upload issues</span></span>

<span data-ttu-id="13198-124">アプリがサイドロードに失敗した場合は、問題が解決するまで次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="13198-124">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="13198-125">[アプリ パッケージの作成](../../concepts/build-and-test/apps-package.md)手順に戻ります。</span><span class="sxs-lookup"><span data-stu-id="13198-125">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="13198-126">[アプリ パッケージを](https://dev.teams.microsoft.com/appvalidation.html) もう一度検証します。</span><span class="sxs-lookup"><span data-stu-id="13198-126">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="13198-127">アプリ マニフェストが最新 [のスキーマ](../../resources/schema/manifest-schema.md)と一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="13198-127">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="13198-128">アプリにアクセスする</span><span class="sxs-lookup"><span data-stu-id="13198-128">Access your app</span></span>

<span data-ttu-id="13198-129">Teamsは、アプリを開く方法を複数提供します。</span><span class="sxs-lookup"><span data-stu-id="13198-129">Teams provides several ways to open apps.</span></span> <span data-ttu-id="13198-130">詳細については、「 Teams[でアプリにアクセスする](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="13198-130">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="13198-131">アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="13198-131">Update your app</span></span>

<span data-ttu-id="13198-132">コードを変更した場合に、アプリを再度サイドロードする必要はありません (これらはリアルタイムでTeamsに反映されます)。</span><span class="sxs-lookup"><span data-stu-id="13198-132">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="13198-133">ただし、アプリの構成を変更する場合は、再インストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="13198-133">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="13198-134">アプリを削除する</span><span class="sxs-lookup"><span data-stu-id="13198-134">Remove your app</span></span>

<span data-ttu-id="13198-135">アプリを削除するには、Teamsのアプリ アイコンを右クリックし、[**アンインストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="13198-135">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="13198-136">個人用ボットアクティビティを完全に削除することはできません。</span><span class="sxs-lookup"><span data-stu-id="13198-136">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="13198-137">アプリを削除して再度追加すると、ボットとの新しい通信が以前の会話に追加されます。</span><span class="sxs-lookup"><span data-stu-id="13198-137">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="13198-138">次の手順</span><span class="sxs-lookup"><span data-stu-id="13198-138">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="13198-139">Teams アプリを使用する</span><span class="sxs-lookup"><span data-stu-id="13198-139">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
