---
title: タブ用のシングル サインオンTeams ToolkitとVisual Studio Code認証
description: シングル サインオンと Microsoft の呼び出しをサポートするGraphを、Visual Studio CodeでMicrosoft Teams Toolkit
keywords: teams visual studio コード ツールキット タブ sso graph 認証 Azure IDENTITY プラットフォーム
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: b2ba9eb27d00f07ec46ddfe0c1cc13ed0864bbbc
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630993"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="2fb7e-104">タブ用のシングル サインオンTeams ToolkitとVisual Studio Code認証</span><span class="sxs-lookup"><span data-stu-id="2fb7e-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="2fb7e-105">このMicrosoft Teams Toolkitを使用すると、タブ アプリのシングル サインオン (SSO) 認証を直接、Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="2fb7e-106">このツールキットは、このプロセスをガイドし、Azure portal でのユーザー登録のプロビジョニングMicrosoft ID プラットフォーム含めて必要なすべてを提供します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="2fb7e-107">開始する - プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="2fb7e-107">Get started — create a project</span></span>

1. <span data-ttu-id="2fb7e-108">ツールキットで新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="2fb7e-109">作成する拡張機能の種類としてタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="2fb7e-110">SSO をサポートするオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="2fb7e-111">インストール後、アクティビティ バーにTeams ToolkitがVisual Studio Code表示されます。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="2fb7e-112">表示されない場合は、アクティビティ バー内を右クリックし、[Microsoft Teams]を選択してツールキットをピン留めして簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="2fb7e-113">プロジェクトを構成する</span><span class="sxs-lookup"><span data-stu-id="2fb7e-113">Configure your project</span></span>

1. <span data-ttu-id="2fb7e-114">アプリ内で SSO をTeamsするには、アプリに Azure アプリ登録リソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="2fb7e-115">ユーザー Teams Toolkitにアプリ登録を準備します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="2fb7e-116">アプリがホストされる URL を入力し、[次へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="2fb7e-117">アプリの登録は、指定された URL を使用して構成されます。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="2fb7e-118">アプリ登録の構成の詳細は、プロジェクトのソース コード内 `.env` のファイルに格納されます。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="2fb7e-119">Azure アプリ登録のプロビジョニング方法の詳細については、タブのシングル サインオン[(SSO) の](../tabs/how-to/authentication/auth-aad-sso.md)サポートに関するドキュメントを参照してください。 </span><span class="sxs-lookup"><span data-stu-id="2fb7e-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="2fb7e-120">この URL を変更するたびに **、Azure App Registrations** に移動して API URI を更新し *、URL* をリダイレクトする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="2fb7e-121">プロジェクトを実行する</span><span class="sxs-lookup"><span data-stu-id="2fb7e-121">Run your project</span></span>

1. <span data-ttu-id="2fb7e-122">フォルダー **から npm install** を `api-server` 選択します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="2fb7e-123">その **後、npm を開始します**。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-123">Then **npm start**.</span></span>
1. <span data-ttu-id="2fb7e-124">フォルダー **から npm install** を `.src` 選択します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="2fb7e-125">その **後、npm を開始します**。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-125">Then **npm start**.</span></span>
1. <span data-ttu-id="2fb7e-126">[ngrok](https://ngrok.com/)のようなトンネリング サービスを使用している場合は、それを実行し、URL がプロジェクト作成ウィザードで入力した URL と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="2fb7e-127">更新されていない場合は、AZURE で作成されたアプリ登録で _API URI_ を更新し _、URL_ をリダイレクトする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="2fb7e-128">ウィンドウの左側にあるアクティビティ バーにVisual Studio Codeします。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="2fb7e-129">[実行] **アイコンを** 選択して、[実行] ビュー **と [デバッグ] ビューを表示** します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="2fb7e-130">キーボード ショートカット Ctrl + **Shift +D を使用することもできます**。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="2fb7e-131">ブラウザーでポップアップ ウィンドウが無効になっている場合、ブラウザーにアプリインストールダイアログが表示されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="2fb7e-132">この場合は、ポップアップ ウィンドウを有効にしてページを更新します。</span><span class="sxs-lookup"><span data-stu-id="2fb7e-132">If this happens, enable pop-up windows and refresh the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="2fb7e-133">関連項目</span><span class="sxs-lookup"><span data-stu-id="2fb7e-133">See also</span></span>

[<span data-ttu-id="2fb7e-134">アプリとアプリのMicrosoft Teams ToolkitをVisual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2fb7e-134">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
