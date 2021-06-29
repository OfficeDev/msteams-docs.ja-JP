---
title: コンテンツ ページを作成する
author: surbhigupta
description: コンテンツ ページを作成する方法
keywords: teams タブ グループ チャネル構成可能静的
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1276fdac2d3a30836b574b8e51b99fcbd7a415d2
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179735"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="349f8-104">タブのコンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="349f8-104">Create a content page for your tab</span></span>

<span data-ttu-id="349f8-105">コンテンツ ページは、クライアント内で表示されるTeamsです。</span><span class="sxs-lookup"><span data-stu-id="349f8-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="349f8-106">これらは、次の一部です。</span><span class="sxs-lookup"><span data-stu-id="349f8-106">These are part of:</span></span>

* <span data-ttu-id="349f8-107">個人用スコープのカスタム タブ: この場合、コンテンツ ページはユーザーが最初に表示するページです。</span><span class="sxs-lookup"><span data-stu-id="349f8-107">A personal-scoped custom tab: In this case, the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="349f8-108">チャネルまたはグループのカスタム タブ: コンテンツ ページは、ユーザーがピンで固定され、適切なコンテキストでタブを構成した後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="349f8-108">A channel or group custom tab: The content page is displayed after the user pins and configures the tab in the appropriate context.</span></span>
* <span data-ttu-id="349f8-109">タスク [モジュール](~/task-modules-and-cards/what-are-task-modules.md): コンテンツ ページを作成し、タスク モジュール内に Web ビューとして埋め込む。</span><span class="sxs-lookup"><span data-stu-id="349f8-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="349f8-110">ページはモーダル ポップアップ内でレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="349f8-110">The page is rendered inside the modal pop-up.</span></span>

<span data-ttu-id="349f8-111">この記事では、コンテンツ ページをタブとして使用する方法について説明します。ただし、ここでのガイダンスの大部分は、コンテンツ ページがユーザーに提示される方法に関係なく適用されます。</span><span class="sxs-lookup"><span data-stu-id="349f8-111">This article is specific to using content pages as tabs; however the majority of the guidance here applies regardless of how the content page is presented to the user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="349f8-112">タブのコンテンツとデザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="349f8-112">Tab content and design guidelines</span></span>

<span data-ttu-id="349f8-113">タブの全体的な目的は、実用的な価値と明らかな目的を持つ有意義で魅力的なコンテンツへのアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="349f8-113">Your tab's overall objective is to provide access to meaningful and engaging content that has practical value and an evident purpose.</span></span> <span data-ttu-id="349f8-114">タブデザインをクリーンにし、直感的にナビゲーションし、コンテンツを没入感のあるものに集中する必要があります。</span><span class="sxs-lookup"><span data-stu-id="349f8-114">You must focus on making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="349f8-115">詳細については、「タブデザイン[ガイドライン」](~/tabs/design/tabs.md)および「ストアMicrosoft Teams[ガイドライン」を参照してください](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。</span><span class="sxs-lookup"><span data-stu-id="349f8-115">For more information, see [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="349f8-116">コードとコードを統合Teams</span><span class="sxs-lookup"><span data-stu-id="349f8-116">Integrate your code with Teams</span></span>

<span data-ttu-id="349f8-117">ページをページに表示するには、Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出し `microsoftTeams.initialize()` を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="349f8-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> 

<span data-ttu-id="349f8-118">次のコードは、ページとクライアントが通信する方法のTeams示しています。</span><span class="sxs-lookup"><span data-stu-id="349f8-118">The following code provides an example of how your page and the Teams client communicate:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="access-additional-content"></a><span data-ttu-id="349f8-119">追加のコンテンツにアクセスする</span><span class="sxs-lookup"><span data-stu-id="349f8-119">Access additional content</span></span>

<span data-ttu-id="349f8-120">SDK を使用して Teams を操作し、ディープ リンクを作成し、タスク モジュールを使用し、URL ドメインが配列に含まれているか確認することで、追加のコンテンツにアクセス `validDomains` できます。</span><span class="sxs-lookup"><span data-stu-id="349f8-120">You can access additional content by using the SDK to interact with Teams, creating deep links, using task modules, and verifying if URL domains are included in the `validDomains` array.</span></span>

### <a name="use-the-sdk-to-interact-with-teams"></a><span data-ttu-id="349f8-121">SDK を使用してアプリを操作Teams</span><span class="sxs-lookup"><span data-stu-id="349f8-121">Use the SDK to interact with Teams</span></span>

<span data-ttu-id="349f8-122">この[Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)には、コンテンツ ページの開発に役立つ機能が多数含まれています。</span><span class="sxs-lookup"><span data-stu-id="349f8-122">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions that you can find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="349f8-123">ディープ リンク</span><span class="sxs-lookup"><span data-stu-id="349f8-123">Deep links</span></span>

<span data-ttu-id="349f8-124">Teams のエンティティへのディープ リンクを作成できます。</span><span class="sxs-lookup"><span data-stu-id="349f8-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="349f8-125">これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。詳細については、「コンテンツと機能[へのディープ リンク](~/concepts/build-and-test/deep-links.md)を作成する」を参照Teams。</span><span class="sxs-lookup"><span data-stu-id="349f8-125">These are used to create links that navigate to content and information within your tab. For more information, see [create deep links to content and features in Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="349f8-126">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="349f8-126">Task modules</span></span>

<span data-ttu-id="349f8-127">タスク モジュールは、タブからトリガーできるモーダル ポップアップ エクスペリエンスです。コンテンツ ページでは、タスク モジュールを使用して、追加の情報を収集したり、リスト内のアイテムの詳細を表示したり、追加情報をユーザーに提示したりするためにフォームを表示できます。</span><span class="sxs-lookup"><span data-stu-id="349f8-127">A task module is a modal pop-up experience that you can trigger from your tab. In a content page, you can use task modules to present forms for gathering additional information, displaying the details of an item in a list, or presenting the user with additional information.</span></span> <span data-ttu-id="349f8-128">タスク モジュール自体は、追加のコンテンツ ページでも、アダプティブ カードを使用して完全に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="349f8-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="349f8-129">詳細については、「タブでのタスク [モジュールの使用」を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="349f8-129">For more information, see [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

### <a name="valid-domains"></a><span data-ttu-id="349f8-130">有効なドメイン</span><span class="sxs-lookup"><span data-stu-id="349f8-130">Valid domains</span></span>

<span data-ttu-id="349f8-131">タブで使用されている URL ドメインすべてがマニフェストの配列に含 `validDomains` まれているか確認 [します](~/concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="349f8-131">Ensure that all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="349f8-132">詳細については、マニフェスト スキーマ [リファレンスの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="349f8-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span>

> [!NOTE]
> <span data-ttu-id="349f8-133">タブのコア機能は、Teamsの外部ではなく、Teams。</span><span class="sxs-lookup"><span data-stu-id="349f8-133">The core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="349f8-134">ネイティブ読み込みインジケーターの表示</span><span class="sxs-lookup"><span data-stu-id="349f8-134">Show a native loading indicator</span></span>

<span data-ttu-id="349f8-135">マニフェスト スキーマ [v1.7](../../../resources/schema/manifest-schema.md)から、ネイティブ読み込みインジケーター [を指定できます](../../../resources/schema/manifest-schema.md#showloadingindicator)。</span><span class="sxs-lookup"><span data-stu-id="349f8-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator).</span></span> <span data-ttu-id="349f8-136">たとえば、タブ[コンテンツ ページ、](#integrate-your-code-with-teams)[構成ページ、](configuration-page.md)[削除ページ](removal-page.md)、タブ[内のタスク モジュールなどです](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="349f8-136">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="349f8-137">モバイル クライアントでの動作は、ネイティブ読み込みインジケーター プロパティでは構成できません。</span><span class="sxs-lookup"><span data-stu-id="349f8-137">The behavior on mobile clients is not configurable through the native loading indicator property.</span></span> <span data-ttu-id="349f8-138">モバイル クライアントは、コンテンツ ページと iframe ベースのタスク モジュール全体で既定でこのインジケーターを表示します。</span><span class="sxs-lookup"><span data-stu-id="349f8-138">Mobile clients show this indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="349f8-139">モバイル上のこのインジケーターは、コンテンツの取得要求が行われたときに表示され、要求が完了するとすぐに却下されます。</span><span class="sxs-lookup"><span data-stu-id="349f8-139">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>

<span data-ttu-id="349f8-140">アプリ マニフェストで指定する場合は、すべてのタブ構成、コンテンツ、および削除ページとすべての iframe ベースのタスク モジュールは、次の手順 `showLoadingIndicator : true`  に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="349f8-140">If you indicate `showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow these steps:</span></span>

<span data-ttu-id="349f8-141">**読み込みインジケーターを表示する**</span><span class="sxs-lookup"><span data-stu-id="349f8-141">**To show the loading indicator**</span></span>

1. <span data-ttu-id="349f8-142">マニフェスト `"showLoadingIndicator": true` に追加します。</span><span class="sxs-lookup"><span data-stu-id="349f8-142">Add `"showLoadingIndicator": true` to your manifest.</span></span>
1. <span data-ttu-id="349f8-143">`microsoftTeams.initialize();` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="349f8-143">Call `microsoftTeams.initialize();`.</span></span>
1. <span data-ttu-id="349f8-144">必須の **手順として、** アプリが正常に読み込まれたTeamsを呼び出して通知 `microsoftTeams.appInitialization.notifySuccess()` します。</span><span class="sxs-lookup"><span data-stu-id="349f8-144">As a **mandatory** step, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="349f8-145">Teams場合は、読み込みインジケーターを非表示にしてください。</span><span class="sxs-lookup"><span data-stu-id="349f8-145">Teams then hides the loading indicator, if applicable.</span></span> <span data-ttu-id="349f8-146">30 秒以内に呼び出されない場合は、アプリがタイム アウトし、再試行オプションが設定されたエラー画面 `notifySuccess`  が表示されます。</span><span class="sxs-lookup"><span data-stu-id="349f8-146">If `notifySuccess`  is not called within 30 seconds, it is assumed that your app timed out and an error screen with a retry option appears.</span></span>
1. <span data-ttu-id="349f8-147">**必要に** 応じて、画面に印刷する準備が整い、アプリケーションの残りのコンテンツを遅延読み込みする場合は、呼び出しによって読み込みインジケーターを手動で非表示にできます `microsoftTeams.appInitialization.notifyAppLoaded();` 。</span><span class="sxs-lookup"><span data-stu-id="349f8-147">**Optionally**, if you are ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`.</span></span>
1. <span data-ttu-id="349f8-148">アプリケーションの読み込みに失敗した場合は、エラーが発生 `microsoftTeams.appInitialization.notifyFailure(reason);` Teamsを呼び出して確認できます。</span><span class="sxs-lookup"><span data-stu-id="349f8-148">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="349f8-149">エラー画面がユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="349f8-149">An error screen is shown to the user.</span></span> <span data-ttu-id="349f8-150">次のコードは、アプリケーションエラーの理由の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="349f8-150">The following code provides an example of application failure reasons:</span></span>

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a><span data-ttu-id="349f8-151">関連項目</span><span class="sxs-lookup"><span data-stu-id="349f8-151">See also</span></span>

* [<span data-ttu-id="349f8-152">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="349f8-152">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="349f8-153">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="349f8-153">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="349f8-154">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="349f8-154">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="349f8-155">コンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="349f8-155">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a><span data-ttu-id="349f8-156">次の手順</span><span class="sxs-lookup"><span data-stu-id="349f8-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="349f8-157">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="349f8-157">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
