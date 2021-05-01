---
title: アップロードアプリを作成する
description: アプリをアプリにサイドロードする方法についてMicrosoft Teams。 サイドローディングは、開発中にアプリをテストおよびデバッグする場合に一般的です。
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: a82f7d6498db4cceb69f1b7f5ff53b1646371ce8
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101570"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="f4ef9-104">アップロードでアプリをMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="f4ef9-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="f4ef9-105">組織または組織のMicrosoft Teamsストアに発行することなく、アプリをサイドロードTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="f4ef9-106">これは、次のシナリオで理にかなっています。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="f4ef9-107">自分または他の開発者と一緒にアプリをローカルでテストおよびデバッグする場合。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="f4ef9-108">自分だけのアプリを構築しました (たとえば、ワークフローを自動化する場合など)。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-108">You built an app just for yourself (for example, to automate a workflow).</span></span>
* <span data-ttu-id="f4ef9-109">小さな一連のユーザー (作業グループなど) 用のアプリを構築しました。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-109">You built an app for a small set of users (such as your work group).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4ef9-110">前提条件</span><span class="sxs-lookup"><span data-stu-id="f4ef9-110">Prerequisites</span></span>

* <span data-ttu-id="f4ef9-111">アプリ パッケージ[を作成し、](~/concepts/build-and-test/apps-package.md)[エラーを検証](https://dev.teams.microsoft.com/appvalidation.html)します。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-111">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="f4ef9-112">[カスタム アプリのアップロードを有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にするには、Teams。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-112">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="f4ef9-113">アプリが実行され、HTTP 経由でアクセス可能な状態にしてください。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-113">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="f4ef9-114">アップロードアプリのインストール</span><span class="sxs-lookup"><span data-stu-id="f4ef9-114">Upload your app</span></span>

<span data-ttu-id="f4ef9-115">アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人用にアプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-115">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="f4ef9-116">開発アカウントを使用Teamsクライアント[にMicrosoft 365します](~/build-your-first-app/build-and-run.md#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-116">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="f4ef9-117">[アプリ **] を** 選択し **、アップロードを選択します**。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-117">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="f4ef9-118">アプリ パッケージファイルを.zipします。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-118">Select your app package .zip file.</span></span> <span data-ttu-id="f4ef9-119">インストール ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-119">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="アプリのインストール ダイアログの例Teamsスクリーンショット。":::
1. <span data-ttu-id="f4ef9-121">アプリをアプリに追加Teams。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-121">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="f4ef9-122">アップロードに関する問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="f4ef9-122">Troubleshoot upload issues</span></span>

<span data-ttu-id="f4ef9-123">アプリがサイドロードに失敗した場合は、問題が解決するまで次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-123">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="f4ef9-124">アプリ パッケージの作成手順に [戻ってください](../../concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-124">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="f4ef9-125">[アプリ パッケージを再度検証](https://dev.teams.microsoft.com/appvalidation.html) します。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-125">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="f4ef9-126">アプリ マニフェストが最新のスキーマと一致する必要 [があります](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-126">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="f4ef9-127">アプリにアクセスする</span><span class="sxs-lookup"><span data-stu-id="f4ef9-127">Access your app</span></span>

<span data-ttu-id="f4ef9-128">Teamsアプリを開く方法がいくつか提供されています。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-128">Teams provides several ways to open apps.</span></span> <span data-ttu-id="f4ef9-129">詳細については、「アプリに[アクセスする」を参照Teams。](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)</span><span class="sxs-lookup"><span data-stu-id="f4ef9-129">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="f4ef9-130">アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="f4ef9-130">Update your app</span></span>

<span data-ttu-id="f4ef9-131">コードを変更する場合は、アプリを再びサイドロードする必要はありません (これらは、リアルタイムでTeams反映されます)。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-131">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="f4ef9-132">ただし、アプリの構成を変更する場合は、再インストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-132">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="f4ef9-133">アプリを削除する</span><span class="sxs-lookup"><span data-stu-id="f4ef9-133">Remove your app</span></span>

<span data-ttu-id="f4ef9-134">アプリを削除するには、アプリのアイコンを右クリックし、[アンインストールTeams選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-134">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="f4ef9-135">個人用ボットアクティビティを完全に削除できない。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-135">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="f4ef9-136">アプリを削除してもう一度追加すると、ボットとの新しい通信が以前の会話に追加されます。</span><span class="sxs-lookup"><span data-stu-id="f4ef9-136">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="f4ef9-137">次の手順</span><span class="sxs-lookup"><span data-stu-id="f4ef9-137">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4ef9-138">アプリをTeamsする</span><span class="sxs-lookup"><span data-stu-id="f4ef9-138">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
