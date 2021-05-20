---
title: はじめに - チャネルとグループ タブを構築する
author: girliemac
description: Microsoft Teams Toolkitを使用して、Microsoft Teamsチャネルとグループ タブをすばやく作成します。
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: ff9cfbfb7d099db52966f119add4ce8729929aa1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566069"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="82b5c-103">Microsoft Teamsの最初のチャンネルとグループタブを作成する</span><span class="sxs-lookup"><span data-stu-id="82b5c-103">Build your first channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="82b5c-104">このチュートリアルでは、チーム チャネルまたはチャットの全画面表示ページである *グループ タブ* とも呼ばれる基本的な *チャネル タブ* を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-104">This tutorial teaches you to build a basic *channel tab* also known as a *group tab*, which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="82b5c-105">この種類のタブの一部の要素を構成することもできます(たとえば、タブの名前を変更して、そのタブをチャネルに意味のあるものにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-105">You can also configure some aspects of this kind of tab, for example, rename the tab so it's meaningful to their channel, which you cannot do in a Personal Tab.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="82b5c-106">あなたが学ぶこと</span><span class="sxs-lookup"><span data-stu-id="82b5c-106">What you'll learn</span></span>

* <span data-ttu-id="82b5c-107">Visual Studio CodeのMicrosoft Teams Toolkitを使用してアプリ プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-107">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="82b5c-108">チャンネルタブに関連するアプリの構成とスキャフォールディングについて理解する。</span><span class="sxs-lookup"><span data-stu-id="82b5c-108">Understand the app configurations and scaffolding relevant to channel tabs.</span></span>
* <span data-ttu-id="82b5c-109">タブの内容とタブ構成を作成します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-109">Create tab content and tab configuration.</span></span>
* <span data-ttu-id="82b5c-110">テスト用のチームでアプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-110">Build and run your app in teams for testing.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82b5c-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="82b5c-111">Prerequisites</span></span>

<span data-ttu-id="82b5c-112">簡単なTeams アプリを設定して構築する方法を理解していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-112">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="82b5c-113">詳細については、[最初のMicrosoft Teams "Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="82b5c-113">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="82b5c-114">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="82b5c-114">1. Create your app project</span></span>

<span data-ttu-id="82b5c-115">このMicrosoft Teams Toolkitは、アプリを構成し、チャンネルとグループのタブに関連するスキャフォールディングを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-115">The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs.</span></span> <span data-ttu-id="82b5c-116">また、基本的な構成ページとコンテンツ ページが含まれています。</span><span class="sxs-lookup"><span data-stu-id="82b5c-116">It also contains a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="82b5c-117">メッセージ。</span><span class="sxs-lookup"><span data-stu-id="82b5c-117">message.</span></span>

<span data-ttu-id="82b5c-118">**アプリ プロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="82b5c-118">**To create your app project**</span></span>

1. Visual Studio Codeに移動し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 左側のアクティビティバーのMicrosoft Teamsを選択します。
1. <span data-ttu-id="82b5c-120">Microsoft 365開発アカウントでサインインするように求められたらサインインします。</span><span class="sxs-lookup"><span data-stu-id="82b5c-120">Sign in with your Microsoft 365 development account when prompted to do so.</span></span>
1. <span data-ttu-id="82b5c-121">[**プロジェクトの選択**] 画面で、[**チャネルとグループ アプリ**] の下の **[JS** (JavaScript)] を選択します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-121">On the **Select project** screen, select **JS** (JavaScript) under **Channel and group app**.</span></span>
1. <span data-ttu-id="82b5c-122">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-122">Enter a name for your Teams app.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="82b5c-123">これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前でもあります。</span><span class="sxs-lookup"><span data-stu-id="82b5c-123">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>

1. <span data-ttu-id="82b5c-124">[**グループ] タブまたは [チャンネル] タブTeams** 選択します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-124">Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="82b5c-125">画面の下部にある **[完了] を** 選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-125">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="82b5c-126">2. アプリ プロジェクト コンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="82b5c-126">2. Understand your app project components</span></span>

<span data-ttu-id="82b5c-127">ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-127">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="82b5c-128">チャネル タブを作成するための主要なコンポーネントを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="82b5c-128">Let's look at the main components for building a channel tab.</span></span>

* <span data-ttu-id="82b5c-129">**アプリの構成**: **ツールキットでアプリスタジオ** を開き、アプリの構成を表示および更新します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-129">**App configurations**: Open **App Studio** in the toolkit to view and update your app configurations.</span></span>
* <span data-ttu-id="82b5c-130">**アプリスキャフォールディング**: アプリスキャフォールディングは、Teamsでチャンネルタブをレンダリングするために必要なコンポーネントを提供します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-130">**App scaffolding**: The app scaffolding provides the components needed for rendering your channel tab in Teams.</span></span> <span data-ttu-id="82b5c-131">作業できる作業はたくさんありますが、ここでは次の点に焦点を当ててみましょう。</span><span class="sxs-lookup"><span data-stu-id="82b5c-131">There's a lot you can work with, however, for now let's focus on the following:</span></span>
  * <span data-ttu-id="82b5c-132">プロジェクトのディレクトリにあるファイル `src/components` :</span><span class="sxs-lookup"><span data-stu-id="82b5c-132">The files located in the `src/components` directory of your project:</span></span>
    * <span data-ttu-id="82b5c-133">`Tab.js` タブのコンテンツ ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="82b5c-133">`Tab.js` for rendering your tab's content page.</span></span>
    * <span data-ttu-id="82b5c-134">`TabConfig.js` タブの設定ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="82b5c-134">`TabConfig.js` for rendering your tab's configuration page.</span></span>
  * <span data-ttu-id="82b5c-135">Microsoft TeamsJavaScript クライアント SDK は、プロジェクトのフロントエンド コンポーネントにプリロードされます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-135">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="82b5c-136">3. タブコンテンツページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="82b5c-136">3. Customize your tab content page</span></span>

1. <span data-ttu-id="82b5c-137">次のコード サンプルをコピーして、組織に関連する情報を使用して変更します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-137">Copy and modify the following code sample with information that's relevant to your organization.</span></span> <span data-ttu-id="82b5c-138">スニペットを次のように使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-138">You can also use the snippet as it is:</span></span>
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
    
1. <span data-ttu-id="82b5c-139">ディレクトリに移動 `src/components` し、ファイルを開きます `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="82b5c-139">Go to the `src/components` directory and open the `Tab.js` file.</span></span> <span data-ttu-id="82b5c-140">次の `render()` 例に示すように、関数を探して、内部にコードを貼り付けます `return()` 。</span><span class="sxs-lookup"><span data-stu-id="82b5c-140">Locate the `render()` function and paste your code inside `return()` as shown in the following example:</span></span>
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
    
1. <span data-ttu-id="82b5c-141">ディレクトリに移動 `src/components` し、 `App.css` 使用されているテーマで電子メールリンクを読みやすくするために、次のコードでファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="82b5c-142">4. タブ設定ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="82b5c-142">4. Customize your tab configuration page</span></span>

<span data-ttu-id="82b5c-143">チャンネルまたはチャットの各タブには、ユーザーがアプリを追加したときに表示される設定オプションを少なくとも 1 つ備えたモーダルの設定ページがあります。</span><span class="sxs-lookup"><span data-stu-id="82b5c-143">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="82b5c-144">既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-144">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span> <span data-ttu-id="82b5c-145">カスタム コンテンツを追加して、構成ページをカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-145">You can customize the configuration page by adding custom content.</span></span>

<span data-ttu-id="82b5c-146">カスタム コンテンツを追加するには、 `TabConfig.js` ディレクトリからファイルを開 `src/components` き、次の `return()` 例に示すように、内部のプレースホルダ コンテンツを更新します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-146">To add custom content, open `TabConfig.js` file from the `src/components` directory and update the placeholder content inside `return()` as shown in the following example:</span></span>

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
> <span data-ttu-id="82b5c-147">ユーザーが初めて読むので、このページでアプリに関する簡単な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-147">Give a brief information about your app on this page since this would be the first time users are reading about it.</span></span> <span data-ttu-id="82b5c-148">タブの設定ページで一般的なカスタム構成オプションまたは [認証ワークフロー](../tabs/how-to/authentication/auth-aad-sso.md)を含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-148">You can also include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-customize-your-tab-name"></a><span data-ttu-id="82b5c-149">5. タブ名をカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="82b5c-149">5. Customize your tab name</span></span>

<span data-ttu-id="82b5c-150">チャンネルタブを追加すると、デフォルトでアプリ名が表示されます(たとえば、 **ファーストアプリ**)。</span><span class="sxs-lookup"><span data-stu-id="82b5c-150">When you add a channel tab, the app name displays by default, for example, **first-app**.</span></span> <span data-ttu-id="82b5c-151">グループの共同作業のコンテキストで、よりわかりやすい名前を指定 **することもできます。**</span><span class="sxs-lookup"><span data-stu-id="82b5c-151">You can also provide a name that makes more sense in the context of group collaboration, for example, **Team Contacts**:</span></span>

1. <span data-ttu-id="82b5c-152">ディレクトリに移動 `src/components` し、ファイルを開きます `TabConfig.js` 。</span><span class="sxs-lookup"><span data-stu-id="82b5c-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span></span>
1. <span data-ttu-id="82b5c-153">次の `suggestedDisplayName` 例に示すように、既定で表示するタブ名を持つプロパティ `microsoftTeams.settings.setSettings` を追加します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-153">Add the `suggestedDisplayName` property with the tab name you want to display by default under `microsoftTeams.settings.setSettings` as shown in the following example:</span></span>

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="82b5c-154">6. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="82b5c-154">6. Build and run your app</span></span>

<span data-ttu-id="82b5c-155">このチュートリアルでは、アプリをローカルでビルドして実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-155">This tutorial teaches you to build and run your app locally.</span></span> 

1. <span data-ttu-id="82b5c-156">ターミナルでアプリ プロジェクトのルート ディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-156">Go to the root directory of your app project in Terminal.</span></span>
1. <span data-ttu-id="82b5c-157">`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-157">Run `npm install`.</span></span>
1. <span data-ttu-id="82b5c-158">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-158">Run `npm start`.</span></span>

<span data-ttu-id="82b5c-159">この情報は、 `README` ツールキットのセクションにも表示されます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-159">This information is also present in the `README` section of the toolkit.</span></span>
<span data-ttu-id="82b5c-160">コンパイルが正常に完了 `https://localhost:3000` した後、アプリが実行 **されています。**</span><span class="sxs-lookup"><span data-stu-id="82b5c-160">Your app is running on `https://localhost:3000` after the **Compiled successfully!**</span></span> <span data-ttu-id="82b5c-161">メッセージが端末に表示されます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-161">message appears in the terminal.</span></span> 

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="82b5c-162">7. Teamsでアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="82b5c-162">7. Sideload your app in Teams</span></span>

<span data-ttu-id="82b5c-163">お使いのアプリは Teams でテストする準備ができています。</span><span class="sxs-lookup"><span data-stu-id="82b5c-163">Your app is ready to test in Teams.</span></span> <span data-ttu-id="82b5c-164">これを行うには、アプリのサイドロードを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="82b5c-164">To do this, you must have an account that allows app sideloading.</span></span> 

1. <span data-ttu-id="82b5c-165">**F5** キーを使用してVisual Studio CodeでTeams Web クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-165">Open a Teams web client in Visual Studio Code with the **F5** key.</span></span>
1. <span data-ttu-id="82b5c-166">次 `localhost` の手順に従って、アプリのコンテンツをTeamsに表示できるようにして、信頼できるものとして ( ) を追加します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-166">Add (`localhost`) as trustworthy by following these steps to enable your app content to display in Teams:</span></span>

   1. <span data-ttu-id="82b5c-167">**F5** キーで開いた同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブを開きます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-167">Open a new tab in the same browser window (Google Chrome by default) which opened with the **F5** key.</span></span>
   1. <span data-ttu-id="82b5c-168">ページ `https://localhost:3000/tab` を開いて、ページに進みます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-168">Open `https://localhost:3000/tab` and proceed to the page.</span></span>

1. <span data-ttu-id="82b5c-169">[**チームに追加**] または **[チャットに追加] を** 選択し、Teamsのモーダルからテストに使用できるチャネルまたはチャットを探します。</span><span class="sxs-lookup"><span data-stu-id="82b5c-169">Select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing from the modal in Teams.</span></span>
1. <span data-ttu-id="82b5c-170">[ **タブのセットアップ ] を** 選択します。構成ページはモーダルで表示されます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-170">Select **Set up a tab**. The configuration page displays in a modal.</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャンネル タブの構成ページのスクリーンショット。":::

1. <span data-ttu-id="82b5c-172">[ **保存] を** 選択してタブを構成します。次のコンテンツ ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="82b5c-172">Select **Save** to configure the tab. The following content page appears:</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="see-also"></a><span data-ttu-id="82b5c-174">関連項目</span><span class="sxs-lookup"><span data-stu-id="82b5c-174">See also</span></span>

* [<span data-ttu-id="82b5c-175">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="82b5c-175">Build and run your first Microsoft Teams app</span></span>](../build-your-first-app/build-and-run.md) 
* [<span data-ttu-id="82b5c-176">Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="82b5c-176">Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="82b5c-177">デスクトップと Web Microsoft Teams用のタブの設計</span><span class="sxs-lookup"><span data-stu-id="82b5c-177">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="82b5c-178">UI テンプレートを使用したMicrosoft Teams アプリの設計</span><span class="sxs-lookup"><span data-stu-id="82b5c-178">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="82b5c-179">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="82b5c-179">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="82b5c-180">タブのシングル サインオン (SSO) サポート</span><span class="sxs-lookup"><span data-stu-id="82b5c-180">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="82b5c-181">Microsoft Teams API の概要</span><span class="sxs-lookup"><span data-stu-id="82b5c-181">Microsoft Teams API overview</span></span>](/graph/teams-concept-overview)
* [<span data-ttu-id="82b5c-182">Node.jsとヨーマンジェネレータを使用してカスタムパーソナルタブを作成Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="82b5c-182">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="82b5c-183">次の手順</span><span class="sxs-lookup"><span data-stu-id="82b5c-183">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82b5c-184">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="82b5c-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="82b5c-185">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="82b5c-185">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
