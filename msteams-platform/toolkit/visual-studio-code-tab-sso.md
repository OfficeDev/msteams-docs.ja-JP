---
title: Teams ToolkitとタブのVisual Studio Codeを使用したシングル サインオン認証
description: シングル サインオンと Microsoft Graph 呼び出しをサポートするタブを、Visual Studio Code内で直接Microsoft Teams Toolkit
keywords: チーム ビジュアル スタジオ コード ツールキット タブ sso グラフ認証 Azure ID プラットフォーム
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 11e642ce335dae4344f1c730b73763e9172fd76c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566832"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="85d45-104">Teams ToolkitとタブのVisual Studio Codeを使用したシングル サインオン認証</span><span class="sxs-lookup"><span data-stu-id="85d45-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="85d45-105">Microsoft Teams Toolkitを使用すると、Visual Studio Code内で直接タブ アプリのシングル サインオン (SSO) 認証を作成できます。</span><span class="sxs-lookup"><span data-stu-id="85d45-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="85d45-106">ツールキットは、プロセスをガイドし、Azure ポータルでのMicrosoft ID プラットフォーム登録のプロビジョニングを含む必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="85d45-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="85d45-107">はじめに - プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="85d45-107">Get started — create a project</span></span>

1. <span data-ttu-id="85d45-108">ツールキットで新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="85d45-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="85d45-109">作成する拡張機能の種類としてタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="85d45-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="85d45-110">SSO をサポートするオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="85d45-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="85d45-111">インストール後、Visual Studio CodeアクティビティバーにTeams Toolkitが表示されます。</span><span class="sxs-lookup"><span data-stu-id="85d45-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="85d45-112">アクセスできない場合は、アクティビティバー内を右クリックし **、Microsoft Teams** 選択してツールキットをピン留めして簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="85d45-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="85d45-113">プロジェクトを構成する</span><span class="sxs-lookup"><span data-stu-id="85d45-113">Configure your project</span></span>

1. <span data-ttu-id="85d45-114">Teams内で SSO を有効にするには、アプリに Azure アプリ登録リソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="85d45-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="85d45-115">Teams Toolkitは、ユーザーに代わってアプリ登録をプロビジョニングします。</span><span class="sxs-lookup"><span data-stu-id="85d45-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="85d45-116">アプリをホストする URL を入力し、[ **次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="85d45-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="85d45-117">アプリの登録は、指定された URL を使用して構成されます。</span><span class="sxs-lookup"><span data-stu-id="85d45-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="85d45-118">アプリの登録の詳細は、 `.env` プロジェクトのソース コード内のファイルに格納されます。</span><span class="sxs-lookup"><span data-stu-id="85d45-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="85d45-119">Azure アプリの登録がどのようにプロビジョニングされるかの詳細については、[タブのシングル サインオン (SSO) サポートを](../tabs/how-to/authentication/auth-aad-sso.md)_参照_ してください。</span><span class="sxs-lookup"><span data-stu-id="85d45-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="85d45-120">この URL を変更するたびに **、Azure アプリの登録** に移動し *、API URI* を更新して *URL をリダイレクト* する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85d45-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="85d45-121">プロジェクトを実行する</span><span class="sxs-lookup"><span data-stu-id="85d45-121">Run your project</span></span>

1. <span data-ttu-id="85d45-122">フォルダから **npm インストール** を選択 `api-server` します。</span><span class="sxs-lookup"><span data-stu-id="85d45-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="85d45-123">それから **npmは始まります**。</span><span class="sxs-lookup"><span data-stu-id="85d45-123">Then **npm start**.</span></span>
1. <span data-ttu-id="85d45-124">フォルダから **npm インストール** を選択 `.src` します。</span><span class="sxs-lookup"><span data-stu-id="85d45-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="85d45-125">それから **npmは始まります**。</span><span class="sxs-lookup"><span data-stu-id="85d45-125">Then **npm start**.</span></span>
1. <span data-ttu-id="85d45-126">[ngrok](https://ngrok.com/)のようなトンネリング サービスを使用している場合は、それを実行し、URL がプロジェクト作成ウィザードで入力した URL と一致することを確認します。</span><span class="sxs-lookup"><span data-stu-id="85d45-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="85d45-127">そうでない場合は _、API URI_ を更新し、Azure で作成されたアプリ登録で _URL をリダイレクト_ する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85d45-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="85d45-128">Visual Studio Code ウィンドウの左側にあるアクティビティ バーに移動します。</span><span class="sxs-lookup"><span data-stu-id="85d45-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="85d45-129">[ **実行** ] アイコンを選択して、[ **実行] ビューと [デバッグ** ] ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="85d45-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="85d45-130">キーボード ショートカット Ctrl キーを押 **しながら Shift キーを押しながら D** キーを押すこともできます。</span><span class="sxs-lookup"><span data-stu-id="85d45-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="85d45-131">ブラウザーでポップアップ ウィンドウが無効になっている場合、ブラウザーでアプリのインストール ダイアログが表示されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="85d45-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="85d45-132">この場合は、ポップアップ ウィンドウを有効にしてページを更新します。</span><span class="sxs-lookup"><span data-stu-id="85d45-132">If this happens, enable pop-up windows and refresh the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="85d45-133">関連項目</span><span class="sxs-lookup"><span data-stu-id="85d45-133">See also</span></span>

- [<span data-ttu-id="85d45-134">Microsoft Teams ToolkitとVisual Studio Codeを使用してアプリを構築する</span><span class="sxs-lookup"><span data-stu-id="85d45-134">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
