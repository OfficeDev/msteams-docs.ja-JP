---
title: '[スタート] - [チャネルとグループ] タブを作成する'
author: girliemac
description: '[チャネルとグループ] Microsoft Teamsを使用して、チャネルとグループ タブをすばやく作成Microsoft Teams Toolkit。'
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
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="ac869-103">ユーザーの最初のチャネルとグループ タブをMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="ac869-103">Build your first channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="ac869-104">このチュートリアルでは、チーム チャネルまたはチャットのフルスクリーン ページであるグループタブとも呼ばれる基本的なチャネル タブを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ac869-104">This tutorial teaches you to build a basic *channel tab* also known as a *group tab*, which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="ac869-105">また、この種のタブのいくつかの側面を構成することもできます。たとえば、タブの名前を変更して、個人用タブでは行えないチャネルにとって意味のあるものにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ac869-105">You can also configure some aspects of this kind of tab, for example, rename the tab so it's meaningful to their channel, which you cannot do in a Personal Tab.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ac869-106">学習する情報</span><span class="sxs-lookup"><span data-stu-id="ac869-106">What you'll learn</span></span>

* <span data-ttu-id="ac869-107">アプリプロジェクトを作成するには、アプリのMicrosoft Teams ToolkitをVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="ac869-107">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="ac869-108">チャネル タブに関連するアプリの構成とスキャフォールディングについて理解します。</span><span class="sxs-lookup"><span data-stu-id="ac869-108">Understand the app configurations and scaffolding relevant to channel tabs.</span></span>
* <span data-ttu-id="ac869-109">タブコンテンツとタブ構成を作成します。</span><span class="sxs-lookup"><span data-stu-id="ac869-109">Create tab content and tab configuration.</span></span>
* <span data-ttu-id="ac869-110">テスト用にチームでアプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="ac869-110">Build and run your app in teams for testing.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac869-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="ac869-111">Prerequisites</span></span>

<span data-ttu-id="ac869-112">簡単なアプリをセットアップして構築する方法を理解Teamsしてください。</span><span class="sxs-lookup"><span data-stu-id="ac869-112">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="ac869-113">詳細については[、「Hello, World!」アプリMicrosoft Teamsを作成するを参照してください](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="ac869-113">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="ac869-114">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="ac869-114">1. Create your app project</span></span>

<span data-ttu-id="ac869-115">このMicrosoft Teams Toolkitは、アプリを構成し、チャネルタブとグループ タブに関連するスキャフォールディングを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ac869-115">The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs.</span></span> <span data-ttu-id="ac869-116">また、基本的な構成ページと、"Hello, World!</span><span class="sxs-lookup"><span data-stu-id="ac869-116">It also contains a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="ac869-117">メッセージ。</span><span class="sxs-lookup"><span data-stu-id="ac869-117">message.</span></span>

<span data-ttu-id="ac869-118">**アプリ プロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="ac869-118">**To create your app project**</span></span>

1. [アクティビティ] Visual Studio Code左側の [アクティビティ バー **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択します。
1. <span data-ttu-id="ac869-120">開発アカウントでサインインMicrosoft 365求めるメッセージが表示されたら、そのアカウントを使用します。</span><span class="sxs-lookup"><span data-stu-id="ac869-120">Sign in with your Microsoft 365 development account when prompted to do so.</span></span>
1. <span data-ttu-id="ac869-121">[プロジェクトの **選択] 画面** で、[チャネルとグループ アプリ] の下の **[JS** (JavaScript)] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ac869-121">On the **Select project** screen, select **JS** (JavaScript) under **Channel and group app**.</span></span>
1. <span data-ttu-id="ac869-122">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac869-122">Enter a name for your Teams app.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ac869-123">これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。</span><span class="sxs-lookup"><span data-stu-id="ac869-123">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>

1. <span data-ttu-id="ac869-124">[**グループまたはチャネルTeams] タブを選択します**。</span><span class="sxs-lookup"><span data-stu-id="ac869-124">Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="ac869-125">画面 **の下部** にある [完了] を選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="ac869-125">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="ac869-126">2. アプリ プロジェクト コンポーネントについて</span><span class="sxs-lookup"><span data-stu-id="ac869-126">2. Understand your app project components</span></span>

<span data-ttu-id="ac869-127">ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="ac869-127">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="ac869-128">チャネル タブを作成する主要なコンポーネントを見てみ取ってみろ。</span><span class="sxs-lookup"><span data-stu-id="ac869-128">Let's look at the main components for building a channel tab.</span></span>

* <span data-ttu-id="ac869-129">**アプリの構成**: ツールキット **で App Studio** を開き、アプリ構成を表示および更新します。</span><span class="sxs-lookup"><span data-stu-id="ac869-129">**App configurations**: Open **App Studio** in the toolkit to view and update your app configurations.</span></span>
* <span data-ttu-id="ac869-130">**アプリのスキャフォール** ディング: アプリのスキャフォールディングは、チャネル タブのレンダリングに必要なコンポーネントを提供Teams。</span><span class="sxs-lookup"><span data-stu-id="ac869-130">**App scaffolding**: The app scaffolding provides the components needed for rendering your channel tab in Teams.</span></span> <span data-ttu-id="ac869-131">ただし、ここでは次の作業に重点を置き、多くの作業を行います。</span><span class="sxs-lookup"><span data-stu-id="ac869-131">There's a lot you can work with, however, for now let's focus on the following:</span></span>
  * <span data-ttu-id="ac869-132">プロジェクトのディレクトリにある `src/components` ファイル:</span><span class="sxs-lookup"><span data-stu-id="ac869-132">The files located in the `src/components` directory of your project:</span></span>
    * <span data-ttu-id="ac869-133">`Tab.js` タブのコンテンツ ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="ac869-133">`Tab.js` for rendering your tab's content page.</span></span>
    * <span data-ttu-id="ac869-134">`TabConfig.js` タブの構成ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="ac869-134">`TabConfig.js` for rendering your tab's configuration page.</span></span>
  * <span data-ttu-id="ac869-135">Microsoft TeamsJavaScript クライアント SDK は、プロジェクトのフロントエンド コンポーネントに事前に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="ac869-135">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="ac869-136">3. タブ コンテンツ ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="ac869-136">3. Customize your tab content page</span></span>

1. <span data-ttu-id="ac869-137">組織に関連する情報を使用して、次のコード サンプルをコピーして変更します。</span><span class="sxs-lookup"><span data-stu-id="ac869-137">Copy and modify the following code sample with information that's relevant to your organization.</span></span> <span data-ttu-id="ac869-138">スニペットは次のように使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="ac869-138">You can also use the snippet as it is:</span></span>
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
    
1. <span data-ttu-id="ac869-139">ディレクトリに移動 `src/components` し、ファイルを開 `Tab.js` きます。</span><span class="sxs-lookup"><span data-stu-id="ac869-139">Go to the `src/components` directory and open the `Tab.js` file.</span></span> <span data-ttu-id="ac869-140">次の例 `render()` に示すように、関数を見つけて `return()` コードを内部に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="ac869-140">Locate the `render()` function and paste your code inside `return()` as shown in the following example:</span></span>
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
    
1. <span data-ttu-id="ac869-141">ディレクトリに移動し、次のコードでファイルを更新して、使用されているテーマで電子メール リンクを読みやすく `src/components` `App.css` します。</span><span class="sxs-lookup"><span data-stu-id="ac869-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="ac869-142">4. タブ構成ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="ac869-142">4. Customize your tab configuration page</span></span>

<span data-ttu-id="ac869-143">チャネルまたはチャットのすべてのタブには構成ページがあります。モーダルで、ユーザーがアプリを追加するときに少なくとも 1 つのセットアップ オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac869-143">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="ac869-144">既定では、構成ページは、タブがインストールされているときにチャネルまたはチャットに通知する必要がある場合に、ユーザーに通知を求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="ac869-144">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span> <span data-ttu-id="ac869-145">カスタム コンテンツを追加することで、構成ページをカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="ac869-145">You can customize the configuration page by adding custom content.</span></span>

<span data-ttu-id="ac869-146">カスタム コンテンツを追加するには、ディレクトリからファイルを開き、次の例に示すようにプレースホルダー コンテンツ `TabConfig.js` `src/components` `return()` を内部で更新します。</span><span class="sxs-lookup"><span data-stu-id="ac869-146">To add custom content, open `TabConfig.js` file from the `src/components` directory and update the placeholder content inside `return()` as shown in the following example:</span></span>

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
> <span data-ttu-id="ac869-147">ユーザーがアプリについて初めて読むので、このページでアプリに関する簡単な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="ac869-147">Give a brief information about your app on this page since this would be the first time users are reading about it.</span></span> <span data-ttu-id="ac869-148">カスタム構成オプションや、タブ構成ページで一般的 [な](../tabs/how-to/authentication/auth-aad-sso.md)認証ワークフローを含めすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ac869-148">You can also include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-customize-your-tab-name"></a><span data-ttu-id="ac869-149">5. タブ名をカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="ac869-149">5. Customize your tab name</span></span>

<span data-ttu-id="ac869-150">チャネル タブを追加すると、アプリ名が既定で表示されます (たとえば、 **ファースト** アプリ)。</span><span class="sxs-lookup"><span data-stu-id="ac869-150">When you add a channel tab, the app name displays by default, for example, **first-app**.</span></span> <span data-ttu-id="ac869-151">グループの共同作業のコンテキストで意味のある名前を指定できます 。たとえば、 **チーム** 連絡先:</span><span class="sxs-lookup"><span data-stu-id="ac869-151">You can also provide a name that makes more sense in the context of group collaboration, for example, **Team Contacts**:</span></span>

1. <span data-ttu-id="ac869-152">ディレクトリに移動 `src/components` し、ファイルを開 `TabConfig.js` きます。</span><span class="sxs-lookup"><span data-stu-id="ac869-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span></span>
1. <span data-ttu-id="ac869-153">次の例に示すように、既定で表示するタブ名を持 `suggestedDisplayName` つ `microsoftTeams.settings.setSettings` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="ac869-153">Add the `suggestedDisplayName` property with the tab name you want to display by default under `microsoftTeams.settings.setSettings` as shown in the following example:</span></span>

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="ac869-154">6. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="ac869-154">6. Build and run your app</span></span>

<span data-ttu-id="ac869-155">このチュートリアルでは、アプリをローカルでビルドして実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ac869-155">This tutorial teaches you to build and run your app locally.</span></span> 

1. <span data-ttu-id="ac869-156">ターミナルのアプリ プロジェクトのルート ディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="ac869-156">Go to the root directory of your app project in Terminal.</span></span>
1. <span data-ttu-id="ac869-157">`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="ac869-157">Run `npm install`.</span></span>
1. <span data-ttu-id="ac869-158">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="ac869-158">Run `npm start`.</span></span>

<span data-ttu-id="ac869-159">この情報は、ツールキットの `README` セクションにも表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac869-159">This information is also present in the `README` section of the toolkit.</span></span>
<span data-ttu-id="ac869-160">コンパイルが正常に完了 `https://localhost:3000` した後、 **アプリが実行されています。**</span><span class="sxs-lookup"><span data-stu-id="ac869-160">Your app is running on `https://localhost:3000` after the **Compiled successfully!**</span></span> <span data-ttu-id="ac869-161">メッセージがターミナルに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac869-161">message appears in the terminal.</span></span> 

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="ac869-162">7. アプリをサイドロードTeams</span><span class="sxs-lookup"><span data-stu-id="ac869-162">7. Sideload your app in Teams</span></span>

<span data-ttu-id="ac869-163">お使いのアプリは Teams でテストする準備ができています。</span><span class="sxs-lookup"><span data-stu-id="ac869-163">Your app is ready to test in Teams.</span></span> <span data-ttu-id="ac869-164">これを行うには、アプリのサイドローディングを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="ac869-164">To do this, you must have an account that allows app sideloading.</span></span> 

1. <span data-ttu-id="ac869-165">F5 キー Teamsを使用して、Visual Studio Code Web クライアント **を開** きます。</span><span class="sxs-lookup"><span data-stu-id="ac869-165">Open a Teams web client in Visual Studio Code with the **F5** key.</span></span>
1. <span data-ttu-id="ac869-166">次の手順に従って信頼できる ( ) を追加し、アプリ コンテンツをアプリ コンテンツを次の手順 `localhost` で表示Teams。</span><span class="sxs-lookup"><span data-stu-id="ac869-166">Add (`localhost`) as trustworthy by following these steps to enable your app content to display in Teams:</span></span>

   1. <span data-ttu-id="ac869-167">F5 キーで開いたのと同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブ **を開** きます。</span><span class="sxs-lookup"><span data-stu-id="ac869-167">Open a new tab in the same browser window (Google Chrome by default) which opened with the **F5** key.</span></span>
   1. <span data-ttu-id="ac869-168">ページ `https://localhost:3000/tab` を開いて続行します。</span><span class="sxs-lookup"><span data-stu-id="ac869-168">Open `https://localhost:3000/tab` and proceed to the page.</span></span>

1. <span data-ttu-id="ac869-169">[**チームに追加] または**[チャット **に** 追加] を選択し、チャットのモーダルからテストに使用できるチャネルまたはチャットTeams。</span><span class="sxs-lookup"><span data-stu-id="ac869-169">Select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing from the modal in Teams.</span></span>
1. <span data-ttu-id="ac869-170">[タブ **の設定] を選択します**。構成ページはモーダルで表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac869-170">Select **Set up a tab**. The configuration page displays in a modal.</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャネル タブ構成ページのスクリーンショット。":::

1. <span data-ttu-id="ac869-172">[保存 **] を** 選択してタブを構成します。次のコンテンツ ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac869-172">Select **Save** to configure the tab. The following content page appears:</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="see-also"></a><span data-ttu-id="ac869-174">関連項目</span><span class="sxs-lookup"><span data-stu-id="ac869-174">See also</span></span>

* [<span data-ttu-id="ac869-175">最初の Microsoft Teams アプリを構築して実行する</span><span class="sxs-lookup"><span data-stu-id="ac869-175">Build and run your first Microsoft Teams app</span></span>](../build-your-first-app/build-and-run.md) 
* [<span data-ttu-id="ac869-176">Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="ac869-176">Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="ac869-177">デスクトップと Web のタブMicrosoft Teamsデザインする</span><span class="sxs-lookup"><span data-stu-id="ac869-177">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="ac869-178">UI テンプレートをMicrosoft Teamsアプリを設計する</span><span class="sxs-lookup"><span data-stu-id="ac869-178">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="ac869-179">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="ac869-179">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="ac869-180">タブのシングル サインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="ac869-180">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="ac869-181">Microsoft Teams API の概要</span><span class="sxs-lookup"><span data-stu-id="ac869-181">Microsoft Teams API overview</span></span>](/graph/teams-concept-overview)
* [<span data-ttu-id="ac869-182">カスタム個人用タブを作成し、Node.jsの Yeoman Generator を使用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ac869-182">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="ac869-183">次の手順</span><span class="sxs-lookup"><span data-stu-id="ac869-183">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac869-184">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="ac869-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac869-185">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="ac869-185">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
