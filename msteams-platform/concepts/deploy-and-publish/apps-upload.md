---
title: アップロードアプリを作成する
description: アプリをアプリにサイドロードする方法についてMicrosoft Teams。 サイドローディングは、開発中にアプリをテストおよびデバッグする場合に一般的です。
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
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="a27dc-104">アップロードでアプリをMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="a27dc-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="a27dc-105">組織または組織のMicrosoft Teamsストアに発行することなく、アプリをサイドロードTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="a27dc-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="a27dc-106">これは、次のシナリオで理にかなっています。</span><span class="sxs-lookup"><span data-stu-id="a27dc-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="a27dc-107">自分または他の開発者と一緒にアプリをローカルでテストおよびデバッグする場合。</span><span class="sxs-lookup"><span data-stu-id="a27dc-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="a27dc-108">自分だけのアプリを構築しました。</span><span class="sxs-lookup"><span data-stu-id="a27dc-108">You built an app just for yourself.</span></span> <span data-ttu-id="a27dc-109">たとえば、ワークフローを自動化します。</span><span class="sxs-lookup"><span data-stu-id="a27dc-109">For example, to automate a workflow.</span></span>
* <span data-ttu-id="a27dc-110">作業グループなどの小さなユーザー セット用のアプリを構築しました。</span><span class="sxs-lookup"><span data-stu-id="a27dc-110">You built an app for a small set of users, such as, your work group.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a27dc-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="a27dc-111">Prerequisites</span></span>

* <span data-ttu-id="a27dc-112">アプリ パッケージ[を作成し、](~/concepts/build-and-test/apps-package.md)[エラーを検証](https://dev.teams.microsoft.com/appvalidation.html)します。</span><span class="sxs-lookup"><span data-stu-id="a27dc-112">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="a27dc-113">[カスタム アプリのアップロードを有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にするには、Teams。</span><span class="sxs-lookup"><span data-stu-id="a27dc-113">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="a27dc-114">アプリが実行され、HTTP 経由でアクセス可能な状態にしてください。</span><span class="sxs-lookup"><span data-stu-id="a27dc-114">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="a27dc-115">アプリをアップロードする</span><span class="sxs-lookup"><span data-stu-id="a27dc-115">Upload your app</span></span>

<span data-ttu-id="a27dc-116">アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人用にアプリをサイドロードできます。</span><span class="sxs-lookup"><span data-stu-id="a27dc-116">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="a27dc-117">開発アカウントを使用Teamsクライアント[にMicrosoft 365します](~/build-your-first-app/build-and-run.md#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="a27dc-117">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="a27dc-118">[アプリ **] を** 選択し **、アップロードを選択します**。</span><span class="sxs-lookup"><span data-stu-id="a27dc-118">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="a27dc-119">アプリ パッケージファイルを.zipします。</span><span class="sxs-lookup"><span data-stu-id="a27dc-119">Select your app package .zip file.</span></span> <span data-ttu-id="a27dc-120">インストール ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a27dc-120">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="アプリのインストール ダイアログの例Teamsスクリーンショット。":::
1. <span data-ttu-id="a27dc-122">アプリをアプリに追加Teams。</span><span class="sxs-lookup"><span data-stu-id="a27dc-122">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="a27dc-123">アップロードに関する問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="a27dc-123">Troubleshoot upload issues</span></span>

<span data-ttu-id="a27dc-124">アプリがサイドロードに失敗した場合は、問題が解決するまで次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="a27dc-124">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="a27dc-125">アプリ パッケージの作成手順に [戻ってください](../../concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a27dc-125">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="a27dc-126">[アプリ パッケージを再度検証](https://dev.teams.microsoft.com/appvalidation.html) します。</span><span class="sxs-lookup"><span data-stu-id="a27dc-126">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="a27dc-127">アプリ マニフェストが最新のスキーマと一致する必要 [があります](../../resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="a27dc-127">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="a27dc-128">アプリにアクセスする</span><span class="sxs-lookup"><span data-stu-id="a27dc-128">Access your app</span></span>

<span data-ttu-id="a27dc-129">Teamsアプリを開く方法がいくつか提供されています。</span><span class="sxs-lookup"><span data-stu-id="a27dc-129">Teams provides several ways to open apps.</span></span> <span data-ttu-id="a27dc-130">詳細については、「アプリに[アクセスする」を参照Teams。](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)</span><span class="sxs-lookup"><span data-stu-id="a27dc-130">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="a27dc-131">アプリを更新する</span><span class="sxs-lookup"><span data-stu-id="a27dc-131">Update your app</span></span>

<span data-ttu-id="a27dc-132">コードを変更する場合は、アプリを再びサイドロードする必要はありません (これらは、リアルタイムでTeams反映されます)。</span><span class="sxs-lookup"><span data-stu-id="a27dc-132">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="a27dc-133">ただし、アプリの構成を変更する場合は、再インストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a27dc-133">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="a27dc-134">アプリを削除する</span><span class="sxs-lookup"><span data-stu-id="a27dc-134">Remove your app</span></span>

<span data-ttu-id="a27dc-135">アプリを削除するには、アプリのアイコンを右クリックし、[アンインストールTeams選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="a27dc-135">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="a27dc-136">個人用ボットアクティビティを完全に削除できない。</span><span class="sxs-lookup"><span data-stu-id="a27dc-136">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="a27dc-137">アプリを削除してもう一度追加すると、ボットとの新しい通信が以前の会話に追加されます。</span><span class="sxs-lookup"><span data-stu-id="a27dc-137">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="a27dc-138">次の手順</span><span class="sxs-lookup"><span data-stu-id="a27dc-138">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a27dc-139">アプリをTeamsする</span><span class="sxs-lookup"><span data-stu-id="a27dc-139">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
