---
author: heath-hamilton
description: 最初の Microsoft Teams アプリで [チャネル] タブを作成する方法について説明します。
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
title: Teams の [チャネルの作成] タブ
ms.openlocfilehash: 2346c67d10ea857bdafbfac6d29a07cb58f5c644
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964614"
---
# <a name="create-a-channel-tab-for-teams"></a><span data-ttu-id="70545-103">Teams の [チャネルの作成] タブ</span><span class="sxs-lookup"><span data-stu-id="70545-103">Create a channel tab for Teams</span></span>

<span data-ttu-id="70545-104">このチュートリアルでは、チームチャネルまたはチャットの全画面コンテンツページである基本 *チャネルタブ*を作成します。</span><span class="sxs-lookup"><span data-stu-id="70545-104">In this tutorial, you'll build a basic *channel tab*, a full-screen content page for a team channel or chat.</span></span> <span data-ttu-id="70545-105">[個人用] タブとは異なり、ユーザーは [チャネル] タブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味がある場合)。</span><span class="sxs-lookup"><span data-stu-id="70545-105">Unlike a personal tab, users can configure some aspects of a channel tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="70545-106">はじめに</span><span class="sxs-lookup"><span data-stu-id="70545-106">Before you begin</span></span>

<span data-ttu-id="70545-107">開始するには、基本的な実行アプリが必要です。</span><span class="sxs-lookup"><span data-stu-id="70545-107">You need a basic running app to get started.</span></span> <span data-ttu-id="70545-108">使用していない場合は、 [ビルドを実行し、Teams 最初のアプリの手順を実行](../build-your-first-app/build-and-run.md)します。</span><span class="sxs-lookup"><span data-stu-id="70545-108">If you don't have one, follow the [build and run your Teams first app instructions](../build-your-first-app/build-and-run.md).</span></span> <span data-ttu-id="70545-109">アプリプロジェクトを作成するときは、[ **グループまたはチームチャネル] タブ** のオプションのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="70545-109">When you create your app project, choose only the **Group or Teams channel tab** option.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="70545-110">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="70545-110">Your assignment</span></span>

<span data-ttu-id="70545-111">以前は、組織で重要な機能 (help desk、HR など) への連絡方法に関する情報を含む Teams タブが作成されていました。</span><span class="sxs-lookup"><span data-stu-id="70545-111">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="70545-112">ただし、タブは個人用の用途に対してのみスコープ設定されているため、各ユーザーはタブをインストールして、それを表示し、導入が予想よりも低くなるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="70545-112">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="70545-113">つまり、まだ多くのワーカーがヘルプデスクに到達する方法がわからない場合があります。</span><span class="sxs-lookup"><span data-stu-id="70545-113">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="70545-114">[チャネル] タブを作成することによって、この情報を見つけやすくすることができます。これにより、アプリのインストールをすべてのユーザーに対して要求する手間が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="70545-114">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="70545-115">代わりに、1人のユーザーが、グループ全体の利点を得るために、チャネルまたはチャットにタブをインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="70545-115">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="70545-116">学習内容</span><span class="sxs-lookup"><span data-stu-id="70545-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="70545-117">チャネルタブに関連するアプリマニフェストのプロパティとスキャフォールディングを特定する</span><span class="sxs-lookup"><span data-stu-id="70545-117">Identify the app manifest properties and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="70545-118">タブのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="70545-118">Create tab content</span></span>
> * <span data-ttu-id="70545-119">タブの構成ページのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="70545-119">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="70545-120">タブを構成およびインストールできるようにする</span><span class="sxs-lookup"><span data-stu-id="70545-120">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="70545-121">提案されたタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="70545-121">Provide a suggested tab name</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="70545-122">関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="70545-122">Identify relevant app project components</span></span>

<span data-ttu-id="70545-123">Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="70545-123">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="70545-124">[チャネル] タブを作成するための主なコンポーネントについて説明します。</span><span class="sxs-lookup"><span data-stu-id="70545-124">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="70545-125">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="70545-125">App manifest</span></span>

<span data-ttu-id="70545-126">アプリマニフェストの次のスニペットが表示され [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs) ます。これには、チャネルタブに関連するプロパティと既定値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="70545-126">The following snippet from the app manifest shows [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel tabs.</span></span>

```JSON
    "configurableTabs": [
        {
            "configurationUrl": "{baseUrl0}/config",
            "canUpdateConfiguration": true,
            "scopes": [
                "team",
                "groupchat"
            ]
        }
    ],
```

* <span data-ttu-id="70545-127">`configurationUrl`: タブの構成ページのホスト URL (HTTPS である必要があります)。</span><span class="sxs-lookup"><span data-stu-id="70545-127">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="70545-128">`canUpdateConfiguration`: に設定さ `true` れている場合、ユーザーはタブの設定を変更するか、タブの名前を変更するか、チャネルまたはチャットから削除することができます。</span><span class="sxs-lookup"><span data-stu-id="70545-128">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="70545-129">`scopes`: ユーザーがアプリをチャネル ( `team` ) およびチャット () にインストールできるかどうかを指定し `groupchat` ます。</span><span class="sxs-lookup"><span data-stu-id="70545-129">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="70545-130">少なくとも1つの値が必要です。</span><span class="sxs-lookup"><span data-stu-id="70545-130">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="70545-131">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="70545-131">App scaffolding</span></span>

<span data-ttu-id="70545-132">アプリのスキャフォールディングは、 `TabConfig.js` `src/components` タブの構成ページをレンダリングするために、プロジェクトのディレクトリにあるファイルを提供します (詳細については、すぐに説明します)。</span><span class="sxs-lookup"><span data-stu-id="70545-132">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="70545-133">タブコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="70545-133">Create your tab content</span></span>

<span data-ttu-id="70545-134">アプリのマニフェスト () を開き `manifest.json` [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) 、タブのコンテンツページを定義する次のプロパティをに設定します。</span><span class="sxs-lookup"><span data-stu-id="70545-134">Open your app manifest (`manifest.json`) and set the following properties in [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

```JSON
    "staticTabs": [
        {
            "entityId": "index",
            "name": "My Contacts",
            "contentUrl": "{baseUrl0}/tab",
            "scopes": [ "personal" ]
        }
    ],
```

<span data-ttu-id="70545-135">次のスニペットを、組織に関連する情報でコピーして更新するか、または時間のためにコードをそのように使用します。</span><span class="sxs-lookup"><span data-stu-id="70545-135">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

```JSX
  <div>
    <h1>Important Contacts</h1>
      <ul>
        <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
        <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
        <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
      </ul>
  </div>
```

<span data-ttu-id="70545-136">ディレクトリに移動 `src/components` し、を開き `Tab.js` ます。</span><span class="sxs-lookup"><span data-stu-id="70545-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="70545-137">関数を検索し、その `render()` 中にコンテンツを貼り付け `return()` ます (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="70545-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
  render() {

      let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

      return (
      <div>
        <h1>Important Contacts</h1>
          <ul>
            <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
            <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
            <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
          </ul>
      </div>
      );
  }
```

<span data-ttu-id="70545-138">`App.css`どのテーマが使用されていても、電子メールリンクが読みやすくなるように、次のルールを追加します。</span><span class="sxs-lookup"><span data-stu-id="70545-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
  a {
    color: inherit;
  }
```

## <a name="create-your-tab-configuration-page"></a><span data-ttu-id="70545-139">タブの構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="70545-139">Create your tab configuration page</span></span>

<span data-ttu-id="70545-140">各 [チャネル] タブには構成ページがあり、アプリをインストールするときに表示される1つ以上のセットアップオプションを持つモーダルです。</span><span class="sxs-lookup"><span data-stu-id="70545-140">Every channel tab has a configuration page, a modal with at least one setup option that displays when installing the app.</span></span> <span data-ttu-id="70545-141">既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。</span><span class="sxs-lookup"><span data-stu-id="70545-141">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="70545-142">構成ページにコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="70545-142">Add some content to your configuration page.</span></span> <span data-ttu-id="70545-143">プロジェクトのディレクトリに移動し、を `src/components` 開いて、その内部にコンテンツを挿入し `TabConfig.js` `return()` ます (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="70545-143">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

```JavaScript
    return (
        <div>
          <h1>Add My Contoso Contacts</h1>
          <div>
            Select <b>Save</b> to add our organization's important contacts to this workspace.
          </div>
        </div>
    );
```
 
> [!TIP]
> <span data-ttu-id="70545-144">少なくとも、ユーザーが初めて理解しているときに、このページにあるアプリについて簡単な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="70545-144">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="70545-145">また、タブの構成ページに共通のカスタム構成オプションまたは [認証ワークフロー](../../tabs/how-to/authentication/auth-aad-sso.md)を含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="70545-145">You also could include custom configuration options or an [authentication workflow](../../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="70545-146">タブを構成およびインストールできるようにする</span><span class="sxs-lookup"><span data-stu-id="70545-146">Allow the tab to be configured and installed</span></span>

<span data-ttu-id="70545-147">ユーザーが [チャネル] タブを正しく構成してインストールするには、 [最初のアプリを作成し](../build-your-first-app/build-and-run.md) て構成ページコンポーネントに対して実行するときに設定するホスト URL を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70545-147">For users to successfully configure and install the channel tab, you must add the host URL you set up when [creating and running your first app](../build-your-first-app/build-and-run.md) to the configuration page component.</span></span>

<span data-ttu-id="70545-148">に移動 `TabConfig.js` し、を見つけ `microsoftTeams.settings.setSettings` ます。</span><span class="sxs-lookup"><span data-stu-id="70545-148">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="70545-149">の場合は `"contentUrl"` 、 `localhost:3000` URL の部分を、タブの内容をホストしているドメインに置き換えます (図を見てください)。</span><span class="sxs-lookup"><span data-stu-id="70545-149">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
    });
```

<span data-ttu-id="70545-150">また、があることを確認してください `microsoftTeams.settings.setValidityState(true);` 。</span><span class="sxs-lookup"><span data-stu-id="70545-150">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="70545-151">既定では、がに設定されている場合 `false` 、[構成] ページの [ **保存** ] ボタンは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="70545-151">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="provide-a-suggested-tab-name"></a><span data-ttu-id="70545-152">提案されたタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="70545-152">Provide a suggested tab name</span></span>

<span data-ttu-id="70545-153">個人用に使用するタブをインストールすると、表示名は、 `name` `staticTabs` アプリマニフェストの一部のプロパティ (たとえば、 **[連絡先**]) になります。</span><span class="sxs-lookup"><span data-stu-id="70545-153">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="70545-154">[チャネル] タブをインストールすると、既定ではアプリケーション名が表示されます (たとえば、 **最初のアプリ**)。</span><span class="sxs-lookup"><span data-stu-id="70545-154">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="70545-155">これは、アプリの呼び出し方法によっては適切な場合もありますが、グループコラボレーションのコンテキスト (たとえば、 **チーム連絡先**) にとってわかりやすい名前を指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="70545-155">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="70545-156">で `TabConfig.js` 、に戻り `microsoftTeams.settings.setSettings` ます。</span><span class="sxs-lookup"><span data-stu-id="70545-156">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="70545-157">`suggestedDisplayName`既定で表示するタブ名を持つプロパティを追加します (表示されています)。</span><span class="sxs-lookup"><span data-stu-id="70545-157">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="70545-158">指定した名前を使用するか、独自の名前を作成します。</span><span class="sxs-lookup"><span data-stu-id="70545-158">Use the provided name or create your own.</span></span> <span data-ttu-id="70545-159">マニフェストでは、必要に応じてユーザーが名前を変更できるようにすることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="70545-159">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
      "suggestedDisplayName": "Team Contacts"
    });
```

## <a name="view-the-channel-tab"></a><span data-ttu-id="70545-160">[チャネル] タブを表示する</span><span class="sxs-lookup"><span data-stu-id="70545-160">View the channel tab</span></span>

<span data-ttu-id="70545-161">チャネルタブの構成とコンテンツページを表示するには、チャネルまたはチャットにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="70545-161">To see your channel tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="70545-162">Teams クライアントで、[ **アプリ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="70545-162">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="70545-163">[ **カスタムアプリのアップロード** ] を選択し、アプリを選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="70545-163">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="70545-164">[ **チームに追加する** ] または [ **チャットに追加** する] を選択し、テストに使用できるチャネルまたはチャットを探します。</span><span class="sxs-lookup"><span data-stu-id="70545-164">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="70545-165">[ **タブの設定]** を選択します。[構成] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="70545-165">Select **Set up a tab**. The configuration page displays.</span></span>

:::image type="content" source="../doc-links/images/channel-tab-tutorial-content.png" alt-text="静的コンテンツを含む [チャネル] タブのスクリーンショットの例です。":::

<span data-ttu-id="70545-167">[ **保存** ] を選択してタブを構成すると、コンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="70545-167">Once you select **Save** to configure the tab, the content displays.</span></span>

:::image type="content" source="../doc-links/images/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツを含む [チャネル] タブのスクリーンショットの例です。":::

## <a name="well-done"></a><span data-ttu-id="70545-169">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="70545-169">Well done</span></span>

<span data-ttu-id="70545-170">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="70545-170">Congratulations!</span></span> <span data-ttu-id="70545-171">[チャネル] タブを備えた Teams アプリを使用すると、チャンネルやチャットに役立つコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="70545-171">You have a Teams app with a channel tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="70545-172">詳細情報</span><span class="sxs-lookup"><span data-stu-id="70545-172">Learn more</span></span>

* <span data-ttu-id="70545-173">[認証タブのユーザーに SSO を使用](../../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。</span><span class="sxs-lookup"><span data-stu-id="70545-173">[Authenticate tab users with SSO](../../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="70545-174">[既存の web アプリまたは web ページからコンテンツを埋め込む](../../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。</span><span class="sxs-lookup"><span data-stu-id="70545-174">[Embed content from an existing web app or webpage](../../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="70545-175">[タブに対してシームレスな環境を作成する](../../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="70545-175">[Create a seamless experience for your tab](../../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="70545-176">[モバイル用のタブの作成](../../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。</span><span class="sxs-lookup"><span data-stu-id="70545-176">[Build tabs for mobile](../../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>

## <a name="next-lesson"></a><span data-ttu-id="70545-177">次のレッスン</span><span class="sxs-lookup"><span data-stu-id="70545-177">Next lesson</span></span>

<span data-ttu-id="70545-178">グループ作業用のタブを作成する方法を理解していること。</span><span class="sxs-lookup"><span data-stu-id="70545-178">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="70545-179">別の種類の Teams アプリを作成しようとしていますか?</span><span class="sxs-lookup"><span data-stu-id="70545-179">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70545-180">Bot を構築する</span><span class="sxs-lookup"><span data-stu-id="70545-180">Build a bot</span></span>](../build-your-first-app/add-bot.md)
