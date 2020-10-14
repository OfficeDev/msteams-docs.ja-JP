---
title: 「はじめに」-「チャネルとグループの作成」タブ
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams のチャネルとグループタブをすばやく作成できます。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: f890754cdf4ca43f39c25e3ba24fcf47b08c5a9f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452856"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="bf2d2-103">Microsoft Teams の [チャネルとグループの作成] タブ</span><span class="sxs-lookup"><span data-stu-id="bf2d2-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="bf2d2-104">このチュートリアルでは、チームチャネルまたはチャットの全画面ページである基本 *チャネルタブ* ( *グループタブ*とも呼ばれます) を作成します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="bf2d2-105">[個人用] タブとは異なり、ユーザーはこの種類のタブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味がある場合)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="bf2d2-106">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="bf2d2-106">Your assignment</span></span>

<span data-ttu-id="bf2d2-107">以前は、組織で重要な機能 (help desk、HR など) への連絡方法に関する情報を含む Teams タブが作成されていました。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-107">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="bf2d2-108">ただし、タブは個人用の用途に対してのみスコープ設定されているため、各ユーザーはタブをインストールして、それを表示し、導入が予想よりも低くなるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-108">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="bf2d2-109">つまり、まだ多くのワーカーがヘルプデスクに到達する方法がわからない場合があります。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="bf2d2-110">[チャネル] タブを作成することによって、この情報を見つけやすくすることができます。これにより、アプリのインストールをすべてのユーザーに対して要求する手間が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="bf2d2-111">代わりに、1人のユーザーが、グループ全体の利点を得るために、チャネルまたはチャットにタブをインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-111">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="bf2d2-112">学習内容</span><span class="sxs-lookup"><span data-stu-id="bf2d2-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="bf2d2-113">Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="bf2d2-114">チャネルおよびグループのタブに関連するアプリマニフェストのプロパティとスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-114">Identify some of the app manifest properties and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="bf2d2-115">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="bf2d2-115">Host an app locally</span></span>
> * <span data-ttu-id="bf2d2-116">タブのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-116">Create tab content</span></span>
> * <span data-ttu-id="bf2d2-117">タブの構成ページのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-117">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="bf2d2-118">タブを構成およびインストールできるようにする</span><span class="sxs-lookup"><span data-stu-id="bf2d2-118">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="bf2d2-119">提案されたタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-119">Provide a suggested tab name</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="bf2d2-120">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-120">1. Create your app project</span></span>

<span data-ttu-id="bf2d2-121">Microsoft Teams Toolkit は、"Hello, World!" と表示される基本的な構成ページやコンテンツページなど、チャネルおよびグループのタブに関連するアプリのマニフェストとスキャフォールディングを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-121">The Microsoft Teams Toolkit helps you set up the app manifest and scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="bf2d2-122">メッセージ。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-122">message.</span></span>

> [!TIP]
> <span data-ttu-id="bf2d2-123">以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. <span data-ttu-id="bf2d2-125">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="bf2d2-126">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="bf2d2-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="bf2d2-127">[ **機能の追加** ] 画面で、[ **タブ** 、 **グループ、またはチームチャネル] タブ**を選択します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-127">On the **Add capabilities** screen, select **Tab** then **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="bf2d2-128">画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-128">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="bf2d2-129">2. 関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-129">2. Identify relevant app project components</span></span>

<span data-ttu-id="bf2d2-130">Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-130">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="bf2d2-131">[チャネルとグループ] タブを構築するための主なコンポーネントについて見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-131">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="bf2d2-132">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="bf2d2-132">App manifest</span></span>

<span data-ttu-id="bf2d2-133">アプリマニフェストの次のスニペットは [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) 、[チャネル] タブおよび [グループ] タブに関連するプロパティと既定値を含みます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-133">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel and group tabs.</span></span>

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

* <span data-ttu-id="bf2d2-134">`configurationUrl`: タブの構成ページのホスト URL (HTTPS である必要があります)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-134">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="bf2d2-135">`canUpdateConfiguration`: に設定さ `true` れている場合、ユーザーはタブの設定を変更するか、タブの名前を変更するか、チャネルまたはチャットから削除することができます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-135">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="bf2d2-136">`scopes`: ユーザーがアプリをチャネル ( `team` ) およびチャット () にインストールできるかどうかを指定し `groupchat` ます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-136">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="bf2d2-137">少なくとも1つの値が必要です。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-137">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="bf2d2-138">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="bf2d2-138">App scaffolding</span></span>

<span data-ttu-id="bf2d2-139">アプリのスキャフォールディングは、 `TabConfig.js` `src/components` タブの構成ページをレンダリングするために、プロジェクトのディレクトリにあるファイルを提供します (詳細については、すぐに説明します)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-139">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="3-run-your-app"></a><span data-ttu-id="bf2d2-140">3. アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-140">3. Run your app</span></span>

<span data-ttu-id="bf2d2-141">時間の経過とともに、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-141">In the interest of time, you'll build and run your app locally.</span></span>

1. <span data-ttu-id="bf2d2-142">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-142">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="bf2d2-143">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-143">Run `npm start`.</span></span>

<span data-ttu-id="bf2d2-144">完了すると、**コンパイルに成功**しました。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-144">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="bf2d2-145">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-145">message in the terminal.</span></span>

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="bf2d2-146">4. アプリへのセキュリティで保護されたトンネルをセットアップする</span><span class="sxs-lookup"><span data-stu-id="bf2d2-146">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="bf2d2-147">テストを目的として、ローカル web サーバー (ポート 3000) 上でタブをホストしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-147">For testing purposes, let's host your tab on a local web server (port 3000).</span></span>

1. <span data-ttu-id="bf2d2-148">ターミナルで、を実行 `ngrok http 3000` します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-148">In a terminal, run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="bf2d2-149">提供されている HTTPS URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-149">Copy the HTTPS URL you're provided.</span></span>
1. <span data-ttu-id="bf2d2-150">ディレクトリで `.publish` 、を開き `Development.env` ます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-150">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="bf2d2-151">値を `baseUrl0` コピーした URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-151">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="bf2d2-152">(たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ca5.ngrok.io` します)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-152">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="bf2d2-153">アプリのマニフェストは、タブをホストしている場所を指しています。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-153">Your app manifest is pointing to where you're hosting the tab.</span></span>

## <a name="5-customize-your-tab-content-page"></a><span data-ttu-id="bf2d2-154">5. タブのコンテンツページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="bf2d2-154">5. Customize your tab content page</span></span>

<span data-ttu-id="bf2d2-155">ディレクトリでアプリマニフェスト ( `manifest.json` ) を開き `.publish` 、で次のプロパティを設定し [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) ます。タブのコンテンツページが定義されています。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-155">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

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

<span data-ttu-id="bf2d2-156">次のスニペットを、組織に関連する情報でコピーして更新するか、または時間のためにコードをそのように使用します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-156">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="bf2d2-157">ディレクトリに移動 `src/components` し、を開き `Tab.js` ます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-157">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="bf2d2-158">関数を検索し、その `render()` 中にコンテンツを貼り付け `return()` ます (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-158">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="bf2d2-159">`App.css`どのテーマが使用されていても、電子メールリンクが読みやすくなるように、次のルールを追加します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-159">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="6-create-your-tab-configuration-page"></a><span data-ttu-id="bf2d2-160">6. [タブの構成] ページを作成する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-160">6. Create your tab configuration page</span></span>

<span data-ttu-id="bf2d2-161">チャネルまたはチャットのすべてのタブには構成ページがあります。このページには、ユーザーがアプリをインストールするときに表示されるセットアップオプションが1つ以上あるモーダルがあります。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-161">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users install your app.</span></span> <span data-ttu-id="bf2d2-162">既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-162">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="bf2d2-163">構成ページにコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-163">Add some content to your configuration page.</span></span> <span data-ttu-id="bf2d2-164">プロジェクトのディレクトリに移動し、を `src/components` 開いて、その内部にコンテンツを挿入し `TabConfig.js` `return()` ます (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-164">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="bf2d2-165">少なくとも、ユーザーが初めて理解しているときに、このページにあるアプリについて簡単な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-165">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="bf2d2-166">また、タブの構成ページに共通のカスタム構成オプションまたは [認証ワークフロー](../tabs/how-to/authentication/auth-aad-sso.md)を含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-166">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="bf2d2-167">7. タブを構成してインストールできるようにする</span><span class="sxs-lookup"><span data-stu-id="bf2d2-167">7. Allow the tab to be configured and installed</span></span>

<span data-ttu-id="bf2d2-168">ユーザーがタブを正しく構成およびインストールするには、構成ページコンポーネントに設定した、 [セキュリティで保護さ](#4-set-up-a-secure-tunnel-to-your-app) れたホストの URL を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-168">For users to successfully configure and install the tab, you must add the [secure host URL you set up](#4-set-up-a-secure-tunnel-to-your-app) to the configuration page component.</span></span>

<span data-ttu-id="bf2d2-169">に移動 `TabConfig.js` し、を見つけ `microsoftTeams.settings.setSettings` ます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-169">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="bf2d2-170">の場合は `"contentUrl"` 、 `localhost:3000` URL の部分を、タブの内容をホストしているドメインに置き換えます (図を見てください)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-170">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="bf2d2-171">また、があることを確認してください `microsoftTeams.settings.setValidityState(true);` 。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-171">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="bf2d2-172">既定では、がに設定されている場合 `false` 、[構成] ページの [ **保存** ] ボタンは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-172">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="8-provide-a-suggested-tab-name"></a><span data-ttu-id="bf2d2-173">8. 提案されたタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-173">8. Provide a suggested tab name</span></span>

<span data-ttu-id="bf2d2-174">個人用に使用するタブをインストールすると、表示名は、 `name` `staticTabs` アプリマニフェストの一部のプロパティ (たとえば、 **[連絡先**]) になります。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-174">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="bf2d2-175">[チャネル] タブをインストールすると、既定ではアプリケーション名が表示されます (たとえば、 **最初のアプリ**)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-175">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="bf2d2-176">これは、アプリの呼び出し方法によっては適切な場合もありますが、グループコラボレーションのコンテキスト (たとえば、 **チーム連絡先**) にとってわかりやすい名前を指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-176">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="bf2d2-177">で `TabConfig.js` 、に戻り `microsoftTeams.settings.setSettings` ます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-177">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="bf2d2-178">`suggestedDisplayName`既定で表示するタブ名を持つプロパティを追加します (表示されています)。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-178">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="bf2d2-179">指定した名前を使用するか、独自の名前を作成します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-179">Use the provided name or create your own.</span></span> <span data-ttu-id="bf2d2-180">マニフェストでは、必要に応じてユーザーが名前を変更できるようにすることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-180">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a><span data-ttu-id="bf2d2-181">9. タブを表示する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-181">9. View the tab</span></span>

<span data-ttu-id="bf2d2-182">タブの構成とコンテンツページを表示するには、チャネルまたはチャットにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-182">To see your tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="bf2d2-183">Teams クライアントで、[ **アプリ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-183">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="bf2d2-184">[ **カスタムアプリのアップロード** ] を選択し、アプリを選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-184">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="bf2d2-185">[ **チームに追加する** ] または [ **チャットに追加** する] を選択し、テストに使用できるチャネルまたはチャットを探します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-185">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="bf2d2-186">[ **タブの設定]** を選択します。[構成] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-186">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="[チャネル] タブの構成ページのスクリーンショット。":::
1. <span data-ttu-id="bf2d2-188">[ **保存** ] を選択してタブを構成します。コンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-188">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="[チャネル] タブの構成ページのスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="bf2d2-190">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="bf2d2-190">Well done</span></span>

<span data-ttu-id="bf2d2-191">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="bf2d2-191">Congratulations!</span></span> <span data-ttu-id="bf2d2-192">Teams アプリには、チャネルとチャットに役立つコンテンツを表示するためのタブがあります。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-192">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="bf2d2-193">詳細情報</span><span class="sxs-lookup"><span data-stu-id="bf2d2-193">Learn more</span></span>

* <span data-ttu-id="bf2d2-194">[認証タブのユーザーに SSO を使用](../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-194">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="bf2d2-195">[既存の web アプリまたは web ページからコンテンツを埋め込む](../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-195">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="bf2d2-196">[タブに対してシームレスな環境を作成する](../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-196">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="bf2d2-197">[モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-197">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="bf2d2-198">ツールキットなしでタブを作成する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-198">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="bf2d2-199">次のレッスン</span><span class="sxs-lookup"><span data-stu-id="bf2d2-199">Next lesson</span></span>

<span data-ttu-id="bf2d2-200">グループ作業用のタブを作成する方法を理解していること。</span><span class="sxs-lookup"><span data-stu-id="bf2d2-200">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="bf2d2-201">別の種類の Teams アプリを作成しようとしていますか?</span><span class="sxs-lookup"><span data-stu-id="bf2d2-201">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf2d2-202">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="bf2d2-202">Build a bot</span></span>](../build-your-first-app/build-bot.md)
