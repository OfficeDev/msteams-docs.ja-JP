---
title: 開発者ポータルでのアプリの構成
description: 開発者ポータルを使用してアプリを構成および管理する方法について説明Microsoft Teams
keywords: 開発者ポータル チームの開始
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: ce290bd7daa46467be279aae7c608321e75e2d57
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635146"
---
# <a name="app-configuration"></a><span data-ttu-id="70b91-104">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="70b91-104">App configuration</span></span>

<span data-ttu-id="70b91-105">アプリ パッケージの最も重要なMicrosoft Teamsは、ファイルのmanifest.jsです。</span><span class="sxs-lookup"><span data-stu-id="70b91-105">The most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="70b91-106">このファイルは、アプリ スキーマの[Teamsする必要があります](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="70b91-106">This file must conform to the [Teams App schema](~/resources/schema/manifest-schema.md).</span></span> <span data-ttu-id="70b91-107">ファイルmanifest.jsにはメタデータが含まれているので、Teamsユーザーにアプリを正しく表示できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-107">The manifest.json file contains metadata, which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="70b91-108">開発者ポータルの [構成] セクション **で、次** の操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-108">You can perform the following actions in the **Configure** section of the Developer Portal:</span></span>

* <span data-ttu-id="70b91-109">アプリ パッケージを簡単に作成します。</span><span class="sxs-lookup"><span data-stu-id="70b91-109">Create an app package easily.</span></span>
* <span data-ttu-id="70b91-110">アプリについて説明します。</span><span class="sxs-lookup"><span data-stu-id="70b91-110">Describe the app.</span></span>
* <span data-ttu-id="70b91-111">アップロードアイコンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="70b91-111">Upload your icons.</span></span>
* <span data-ttu-id="70b91-112">配布を容易.zipファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="70b91-112">Produce a .zip file for easy distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="70b91-113">開発者ポータルは、アプリの機能コードを生成したり、アプリをホストしたりしません。</span><span class="sxs-lookup"><span data-stu-id="70b91-113">Developer Portal does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="70b91-114">アプリは、既にホストされており、アプリのアップロード プロセスのマニフェストに記載されている URL で実行されている必要があります。これにより、アプリが正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="70b91-114">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_configure_1.png" alt-text="開発者ポータルの [構成] ページTeamsスクリーンショット。":::

## <a name="basic-information-and-branding"></a><span data-ttu-id="70b91-116">基本情報とブランド化</span><span class="sxs-lookup"><span data-stu-id="70b91-116">Basic information and Branding</span></span>

<span data-ttu-id="70b91-117">[ **基本情報] セクション** と **[ブランド化]** セクションでは、作成するアプリの概要を定義します。</span><span class="sxs-lookup"><span data-stu-id="70b91-117">The **Basic information** and **Branding** sections define the high-level description of the app you are making.</span></span> <span data-ttu-id="70b91-118">これには、アプリの名前、説明、ビジュアル ブランド化が含まれます。</span><span class="sxs-lookup"><span data-stu-id="70b91-118">This includes the app’s name, description, and visual branding.</span></span> <span data-ttu-id="70b91-119">このセクションの情報は、アプリのストア一覧とアプリTeamsダイアログで使用されます。</span><span class="sxs-lookup"><span data-stu-id="70b91-119">The information in this section will be used in your app's Teams store listing and app installation dialogue.</span></span>

## <a name="capabilities"></a><span data-ttu-id="70b91-120">機能</span><span class="sxs-lookup"><span data-stu-id="70b91-120">Capabilities</span></span>

<span data-ttu-id="70b91-121">[ **構成] の** [機能] セクションには、アプリの機能の詳細が一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="70b91-121">The **Capabilities** section of Configuration has the app's capabilities details listed.</span></span>

> [!NOTE]
> <span data-ttu-id="70b91-122">アプリのカスタマイズ機能は現在、開発者プレビューでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-122">The app customization feature is currently available in the developer preview only.</span></span>
> 
> <span data-ttu-id="70b91-123">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70b91-123">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="70b91-124">詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="70b91-124">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

<span data-ttu-id="70b91-125">機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="70b91-125">Following are the capabilities:</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_capabilities.png" alt-text="開発者ポータルの [構成] ページTeamsスクリーンショット。":::

* <span data-ttu-id="70b91-127">**個人用アプリ**</span><span class="sxs-lookup"><span data-stu-id="70b91-127">**Personal app**</span></span> 

  <span data-ttu-id="70b91-128">このセクションでは、個人アプリ エクスペリエンスで既定で表示されるタブのセット、つまり、ユーザーがチームやチャネルのコンテキスト外でアプリを使用するエクスペリエンスを定義できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-128">This section lets you define a set of tabs that are presented by default in the personal app experience, that is, the experience a user has with your app outside the context of a team or channel.</span></span> <span data-ttu-id="70b91-129">このセクションでは、次の詳細を入力します。</span><span class="sxs-lookup"><span data-stu-id="70b91-129">In this section, provide the following details:</span></span>

  * <span data-ttu-id="70b91-130">タブ名。</span><span class="sxs-lookup"><span data-stu-id="70b91-130">The tab name.</span></span>
  * <span data-ttu-id="70b91-131">一意識別子。</span><span class="sxs-lookup"><span data-stu-id="70b91-131">A unique identifier.</span></span>
  * <span data-ttu-id="70b91-132">ページに表示する UI をポイントする URL Teams。</span><span class="sxs-lookup"><span data-stu-id="70b91-132">The URL that points to the UI to be displayed in Teams.</span></span>
  * <span data-ttu-id="70b91-133">ユーザーがブラウザーでタブを表示することを選択した場合に使用する URL。</span><span class="sxs-lookup"><span data-stu-id="70b91-133">The URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="70b91-134">これはオプションの情報です。</span><span class="sxs-lookup"><span data-stu-id="70b91-134">This is an optional information.</span></span>
  * <span data-ttu-id="70b91-135">タブの読み込みまたはリンクが必要な追加のドメイン。</span><span class="sxs-lookup"><span data-stu-id="70b91-135">Any additional domains from which the tab expects to load from or link to.</span></span>

* <span data-ttu-id="70b91-136">**グループアプリとチャネル アプリ**</span><span class="sxs-lookup"><span data-stu-id="70b91-136">**Group and channel app**</span></span>

  <span data-ttu-id="70b91-137">[Teams] タブはチャネルの一部になり、チームの情報とリソースにすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="70b91-137">A Teams tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="70b91-138">たとえば、チャネルの [Planner] タブには 1 つのプランが含まれている場合、Power BIは特定のレポートにマップされます。</span><span class="sxs-lookup"><span data-stu-id="70b91-138">For example, the Planner tab for a channel contains a single plan, the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="70b91-139">ユーザーは関連するコンテキストにドリルダウンできますが、タブの外側には移動できません。たとえば、Power BI タブでは、その他の Power BI レポートへの移動を有効にすることはできませんが、メインの Power BI Web サイト内のレポートを起動する **[Web サイトに移動]** ボタンを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="70b91-139">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the **Go to website** button that launches the report in the main Power BI website.</span></span>

    > [!NOTE]
    > <span data-ttu-id="70b91-140">チーム タブの場合は、オプションを提示し、情報を収集するための構成 URL を指定する必要があります。これは、タブのコンテンツとエクスペリエンスをカスタマイズするのに役立ちます。この iframed HTML ページは、ユーザーが最初にタブをチャネルに追加するときに表示されます。</span><span class="sxs-lookup"><span data-stu-id="70b91-140">For team tabs, you must provide a Configuration URL to present options and gather information, that would help you to customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>
    > <span data-ttu-id="70b91-141">また、読み込み元またはリンク先になると予測される追加のドメインも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70b91-141">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="70b91-142">**ボット**</span><span class="sxs-lookup"><span data-stu-id="70b91-142">**Bot**</span></span>

  <span data-ttu-id="70b91-143">このセクションでは、[会話ボット](~/bots/what-are-bots.md)をアプリに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="70b91-143">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="70b91-144">Bot Framework にボットが既に登録されている場合、そのボットを追加するには、**[Set Up]** (セットアップ) をクリックし、ボットの名前と Bot Framework ID を指定し、ボットが動作するスコープを定義します。</span><span class="sxs-lookup"><span data-stu-id="70b91-144">If you already have a bot registered with Bot Framework, you can add that bot by clicking **Set Up** and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

  <span data-ttu-id="70b91-145">ボットをボット フレームワークにまだ登録していない場合は、[登録] をクリック **して新しい** ボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="70b91-145">If you have not registered the bot with the Bot Framework yet, click **Register** to create a new one.</span></span> <span data-ttu-id="70b91-146">ボットを登録した後、マニフェスト エディターのこのセクションに戻り、その名前とボット フレームワーク ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="70b91-146">After you have registered your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

  <span data-ttu-id="70b91-147">ボットの情報を提供した後、必要に応じて、ボットがユーザーに提案できるコマンドの一覧を定義できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-147">After you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="70b91-148">コマンドの名前、コマンドの構文と引数を示すコマンドの説明、このコマンドが適用されるスコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="70b91-148">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

  <span data-ttu-id="70b91-149">1 つのスコープのみをサポートするようにボットを定義した場合、サポートされていないスコープに指定したコマンドは無視されます。</span><span class="sxs-lookup"><span data-stu-id="70b91-149">Note that if you have defined your bot to only support one scope, commands specified for the unsupported scope will be ignored.</span></span> <span data-ttu-id="70b91-150">ボットがサポートするスコープはいつでも編集できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-150">You can edit the scopes your bot supports at any time.</span></span>

* <span data-ttu-id="70b91-151">**Connector**</span><span class="sxs-lookup"><span data-stu-id="70b91-151">**Connector**</span></span>

  <span data-ttu-id="70b91-152">このセクションでは、コネクタをアプリに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="70b91-152">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="70b91-153">コネクタを既に登録しているOffice 365[セットアップ] を選択し、コネクタの名前と ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="70b91-153">If you already have registered an Office 365 connector, select **Set up** and enter the name and ID of the connector.</span></span> <span data-ttu-id="70b91-154">新しいコネクタが必要な場合は、**[登録]** をクリックして、ブラウザーでコネクタ開発者ダッシュボードに移動します。</span><span class="sxs-lookup"><span data-stu-id="70b91-154">If you want a new connector click **Register** to be taken to the Connector Developer Dashboard in your browser.</span></span>

  > [!NOTE]
  > <span data-ttu-id="70b91-155">アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれたアプリの外観を変更できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-155">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="70b91-156">たとえば、管理者Teamsからアプリの名前をカスタマイズすると、アプリが新しい名前で `Contoso` ユーザー `Contoso Agent` `Contoso Agent` に表示されます。</span><span class="sxs-lookup"><span data-stu-id="70b91-156">For example, if the Teams admin customizes the name of an app from `Contoso` to `Contoso Agent`, then the app will appear with the new name `Contoso Agent` to the users.</span></span> <span data-ttu-id="70b91-157">ただし、チャットにコネクタを追加している間も、一覧でコネクタにはアプリの名前が表示されます `Contoso` 。</span><span class="sxs-lookup"><span data-stu-id="70b91-157">However, while adding a connector to a chat, in the list, the connectors will still show the name of the app as `Contoso`.</span></span>

* <span data-ttu-id="70b91-158">**メッセージング拡張機能**</span><span class="sxs-lookup"><span data-stu-id="70b91-158">**Messaging Extensions**</span></span>

  <span data-ttu-id="70b91-159">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md) は、ユーザーが Microsoft Teams 内でアプリを使用する強力な方法です。</span><span class="sxs-lookup"><span data-stu-id="70b91-159">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="70b91-160">ユーザーはサービスからの情報に対してクエリを実行して、その情報をカード形式でチャネルやチャット会話に直接投稿できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-160">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

  <span data-ttu-id="70b91-161">メッセージング拡張機能は Bot Framework ボットを利用しているため、動作するには構成済みのボットが必要です。</span><span class="sxs-lookup"><span data-stu-id="70b91-161">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="70b91-162">メッセージング拡張機能を利用するボットの名前と Bot Framework ID がある場合は、入力します。</span><span class="sxs-lookup"><span data-stu-id="70b91-162">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="70b91-163">それ以外の場合は、*[登録]* をクリックしてボットを作成し、後で情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="70b91-163">Otherwise, click *Register* to create one and enter the information afterward.</span></span> <span data-ttu-id="70b91-164">ユーザーがメッセージング拡張機能の構成を更新できるかどうかを選択します。</span><span class="sxs-lookup"><span data-stu-id="70b91-164">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

  <span data-ttu-id="70b91-165">基になるボットを構成した後、メッセージング拡張機能で受け入れられるコマンドとパラメーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="70b91-165">After you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

  <span data-ttu-id="70b91-166">各コマンドには、タイトルと ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="70b91-166">Each command requires a title and an ID.</span></span> <span data-ttu-id="70b91-167">必要に応じて、コマンドにユーザーの説明を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="70b91-167">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="70b91-168">各コマンドでは、最大 5 つのパラメーターをサポートできます。各パラメーターには次の値が必要です。</span><span class="sxs-lookup"><span data-stu-id="70b91-168">Each command can support up to five parameters, each of which requires the following:</span></span>

  * <span data-ttu-id="70b91-169">パラメーターがクライアントに表示され、Teamsに含まれるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="70b91-169">The name of the parameter as it appears in the Teams client and is included in the user request.</span></span>
  * <span data-ttu-id="70b91-170">ユーザーフレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="70b91-170">A user-friendly title.</span></span>
  * <span data-ttu-id="70b91-171">任意の説明。</span><span class="sxs-lookup"><span data-stu-id="70b91-171">An optional description.</span></span>

  > [!NOTE]
  > <span data-ttu-id="70b91-172">アプリ スタジオを使用してメッセージング拡張機能を作成するには、「 [アプリ スタジオを使用してメッセージング拡張機能を作成する」を参照してください](~/resources/create-messaging-extension-using-appstudio.md)。</span><span class="sxs-lookup"><span data-stu-id="70b91-172">To create messaging extension using app studio, see [create messaging extension using app studio](~/resources/create-messaging-extension-using-appstudio.md).</span></span>

* <span data-ttu-id="70b91-173">**会議の拡張機能**</span><span class="sxs-lookup"><span data-stu-id="70b91-173">**Meeting extension**</span></span>

  <span data-ttu-id="70b91-174">TODO: Rajesh R.</span><span class="sxs-lookup"><span data-stu-id="70b91-174">//TODO: Rajesh R.</span></span>

* <span data-ttu-id="70b91-175">**シーン**</span><span class="sxs-lookup"><span data-stu-id="70b91-175">**Scene**</span></span>

  <span data-ttu-id="70b91-176">一緒にモードのシーンは、Microsoft Scene studio を使用してシーン開発者が作成した成果物で、シーン作成者が考えたクリエイティブな設定でビデオ ストリームと共にユーザーをまとめます。</span><span class="sxs-lookup"><span data-stu-id="70b91-176">Scenes in Together Mode is an artifact created by the scene developer using the Microsoft Scene studio that brings people together along with their video stream in a creative setting as conceived by the scene creator.</span></span> <span data-ttu-id="70b91-177">考え出されたシーンの設定では、参加者は指定されたシートを持ち、それらのシートにビデオ ストリームがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="70b91-177">In a conceived scene setting, participants have designated seats with video streams rendered in those seats.</span></span> <span data-ttu-id="70b91-178">詳細については、「一緒にTeams[を参照してください](~/apps-in-teams-meetings/teams-together-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="70b91-178">For more information, see [Teams Together Mode](~/apps-in-teams-meetings/teams-together-mode.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="70b91-179">Permissions</span><span class="sxs-lookup"><span data-stu-id="70b91-179">Permissions</span></span>

<span data-ttu-id="70b91-180">カメラ、マイクTeams場所などのネイティブ デバイス機能を使用して、アプリを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="70b91-180">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span>

## <a name="languages"></a><span data-ttu-id="70b91-181">言語</span><span class="sxs-lookup"><span data-stu-id="70b91-181">Languages</span></span>

<span data-ttu-id="70b91-182">アプリでサポートされている言語を設定または変更します。</span><span class="sxs-lookup"><span data-stu-id="70b91-182">Set up or change the languages that your app supports.</span></span>

## <a name="single-sign-on"></a><span data-ttu-id="70b91-183">シングル サインオン</span><span class="sxs-lookup"><span data-stu-id="70b91-183">Single Sign-On</span></span>

<span data-ttu-id="70b91-184">シングル サインオン (SSO) を使用してユーザーを認証するアプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="70b91-184">Configure your app to authenticate users with single sign-on (SSO).</span></span>

## <a name="domains"></a><span data-ttu-id="70b91-185">ドメイン</span><span class="sxs-lookup"><span data-stu-id="70b91-185">Domains</span></span>

<span data-ttu-id="70b91-186">アプリがクライアント内で読み込むと予想される Web サイトの有効なドメインTeamsします。</span><span class="sxs-lookup"><span data-stu-id="70b91-186">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="70b91-187">ドメインの一覧には、ワイルドカード (たとえば) を含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="70b91-187">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="70b91-188">これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="70b91-188">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="70b91-189">タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70b91-189">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="70b91-190">サポートする ID プロバイダーのドメインをアプリに含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="70b91-190">It is not necessary to include the domains of the identity providers you want to support in your app.</span></span> <span data-ttu-id="70b91-191">たとえば、Google ID を使用して認証を行う場合は、accounts.google.com にリダイレクトする必要があります。ただし、accounts.google.com を含 accounts.google.com 必要があります `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="70b91-191">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="70b91-192">Teams機能するために独自の sharepoint URL を必要とするアプリには、有効なドメイン リストに "{teamsitedomain}" が含まれます。</span><span class="sxs-lookup"><span data-stu-id="70b91-192">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70b91-193">直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="70b91-193">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="70b91-194">たとえば、 `yourapp.onmicrosoft.com` 有効ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="70b91-194">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="70b91-195">オブジェクトは、型のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="70b91-195">The object is an array with all elements of the type `string`.</span></span>

## <a name="advanced"></a><span data-ttu-id="70b91-196">詳細情報</span><span class="sxs-lookup"><span data-stu-id="70b91-196">Advanced</span></span>
<span data-ttu-id="70b91-197">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="70b91-197">//Todo by Karthig</span></span>

### <a name="app-content"></a><span data-ttu-id="70b91-198">アプリのコンテンツ</span><span class="sxs-lookup"><span data-stu-id="70b91-198">App content</span></span>
<span data-ttu-id="70b91-199">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="70b91-199">//Todo by Karthig</span></span>

### <a name="first-party-settings"></a><span data-ttu-id="70b91-200">ファースト パーティの設定</span><span class="sxs-lookup"><span data-stu-id="70b91-200">First party settings</span></span>
<span data-ttu-id="70b91-201">Todo by Karthig</span><span class="sxs-lookup"><span data-stu-id="70b91-201">//Todo by Karthig</span></span>

## <a name="see-also"></a><span data-ttu-id="70b91-202">関連項目</span><span class="sxs-lookup"><span data-stu-id="70b91-202">See also</span></span>

* [<span data-ttu-id="70b91-203">開発者ポータルTeams概要</span><span class="sxs-lookup"><span data-stu-id="70b91-203">Overview of Teams Developer Portal</span></span>](~/concepts/build-and-test/teams-developer-portal.md)
* [<span data-ttu-id="70b91-204">開発者ポータルTeams配布する</span><span class="sxs-lookup"><span data-stu-id="70b91-204">Distribute Teams Developer Portal</span></span>](~/concepts/tdp-distribute.md)
* [<span data-ttu-id="70b91-205">開発者ポータルTeamsツール</span><span class="sxs-lookup"><span data-stu-id="70b91-205">Tools in Teams Developer Portal</span></span>](~/concepts/tdp-tools.md)