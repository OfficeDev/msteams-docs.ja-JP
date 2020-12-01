---
title: Teams ツールキットを使用したシングルサインオン認証と、タブ用 Visual Studio コード
description: Microsoft Teams Toolkit を使用して、Visual Studio Code 内でシングルサインオンと Microsoft Graph の呼び出しを直接サポートするタブを構築する
keywords: teams visual studio code toolkit タブ sso graph authentication Azure identity platform
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477737"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="abe0f-104">Teams ツールキットを使用したシングルサインオン認証と、タブ用 Visual Studio コード</span><span class="sxs-lookup"><span data-stu-id="abe0f-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="abe0f-105">Microsoft Teams ツールキットを使用すると、tab アプリのシングルサインオン (SSO) 認証を Visual Studio Code 内で直接作成できます。</span><span class="sxs-lookup"><span data-stu-id="abe0f-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="abe0f-106">このツールキットではプロセスを順を追って説明しており、Azure portal で Microsoft identity platform の登録をプロビジョニングするなど、必要な情報をすべて提供しています。</span><span class="sxs-lookup"><span data-stu-id="abe0f-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="abe0f-107">作業の開始-プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="abe0f-107">Get started — create a project</span></span>

1. <span data-ttu-id="abe0f-108">ツールキットに新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="abe0f-109">作成する拡張機能の種類として [タブ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="abe0f-110">SSO をサポートするオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="abe0f-111">インストール後に、Visual Studio Code アクティビティバーに Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="abe0f-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="abe0f-112">表示されていない場合は、アクティビティバー内を右クリックし、[ **Microsoft Teams** ] を選択して、簡単にアクセスできるようにツールキットを固定します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="abe0f-113">プロジェクトを構成する</span><span class="sxs-lookup"><span data-stu-id="abe0f-113">Configure your project</span></span>

1. <span data-ttu-id="abe0f-114">Teams 内で SSO を有効にするには、アプリに Azure アプリ登録リソースが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="abe0f-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="abe0f-115">Teams ツールキットは、ユーザーの代わりにアプリの登録をプロビジョニングします。</span><span class="sxs-lookup"><span data-stu-id="abe0f-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="abe0f-116">アプリがホストされる URL を入力し、[ **次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="abe0f-117">アプリの登録は、指定した URL を使用して構成されます。</span><span class="sxs-lookup"><span data-stu-id="abe0f-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="abe0f-118">アプリ登録の構成の詳細は、 `.env` プロジェクトのソースコード内のファイルに格納されます。</span><span class="sxs-lookup"><span data-stu-id="abe0f-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="abe0f-119">Azure アプリの登録方法の詳細については、「[シングルサインオン (SSO) に関するタブのサポート」の](../tabs/how-to/authentication/auth-aad-sso.md)ドキュメントを _参照_ してください。</span><span class="sxs-lookup"><span data-stu-id="abe0f-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="abe0f-120">この URL を変更する場合は、 **Azure アプリの登録** に移動して、 *API URI* と *リダイレクト url* を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="abe0f-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="abe0f-121">プロジェクトを実行する</span><span class="sxs-lookup"><span data-stu-id="abe0f-121">Run your project</span></span>

1. <span data-ttu-id="abe0f-122">フォルダーから [ **npm install** ] を選択し `api-server` ます。</span><span class="sxs-lookup"><span data-stu-id="abe0f-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="abe0f-123">その後、 **npm を開始** します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-123">Then **npm start**.</span></span>
1. <span data-ttu-id="abe0f-124">フォルダーから [ **npm install** ] を選択し `.src` ます。</span><span class="sxs-lookup"><span data-stu-id="abe0f-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="abe0f-125">その後、 **npm を開始** します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-125">Then **npm start**.</span></span>
1. <span data-ttu-id="abe0f-126">[Ngrok](https://ngrok.com/)のようなトンネリングサービスを使用している場合は、それを実行して、プロジェクト作成ウィザードで入力した URL と一致することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="abe0f-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="abe0f-127">そうでない場合は、Azure で作成されたアプリ登録で _API URI_ と _リダイレクト URL_ を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="abe0f-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="abe0f-128">Visual Studio の [コード] ウィンドウの左側にあるアクティビティバーに移動します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="abe0f-129">[実行 **] アイコンを** 選択して、[ **実行] および [デバッグ** ] ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="abe0f-130">キーボードショートカット **ctrl + Shift + D** を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="abe0f-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="abe0f-131">ブラウザーでポップアップウィンドウが無効になっている場合、ブラウザーにアプリのインストールダイアログが表示されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="abe0f-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="abe0f-132">この問題が発生した場合は、ポップアップウィンドウを有効にしてページを更新します。</span><span class="sxs-lookup"><span data-stu-id="abe0f-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abe0f-133">詳細情報: Microsoft Teams Toolkit と Visual Studio Code を使用してアプリをビルドする</span><span class="sxs-lookup"><span data-stu-id="abe0f-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
