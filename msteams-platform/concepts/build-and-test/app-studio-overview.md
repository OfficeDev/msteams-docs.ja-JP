---
title: Microsoft Teams 用の App Studio を開始する
description: App Studio を使用して Microsoft Teams で優れたアプリのビルドを開始する
keywords: App Studio Teams の開始
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: eda6835a1453f878476b3cc296ff2c0e5dc889a5
ms.sourcegitcommit: 1cc1516e71441f6f3f82b35868e21ba9933333cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52651713"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a><span data-ttu-id="7de39-104">Microsoft Teams 用の App Studio を使用してアプリをすばやく開発する</span><span class="sxs-lookup"><span data-stu-id="7de39-104">Quickly develop apps with App Studio for Microsoft Teams</span></span>

<span data-ttu-id="7de39-105">App Studio を使用すると、Microsoft Teams アプリの作成や統合を簡単に始めることができます。自分の組織用にカスタム アプリを開発する場合も、世界各地のチーム用に SaaS アプリケーションを開発する場合も、App Studio ではマニフェストの作成とアプリのパッケージングが合理化され、Card Editor や React 制御ライブラリなどの便利なツールが提供されます。</span><span class="sxs-lookup"><span data-stu-id="7de39-105">App Studio makes it easy to start creating or integrating your own Microsoft Teams apps, whether you develop custom apps for your enterprise or SaaS applications for teams around the world by streamlining the creation of the manifest and package for your app and providing useful tools like the Card Editor and a React control library.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7de39-106">App Studio は現在、次の種類の組織Teams使用できません。</span><span class="sxs-lookup"><span data-stu-id="7de39-106">App Studio is currently not available in the following types of Teams orgs:</span></span>
>
> * <span data-ttu-id="7de39-107">Government Community Cloud (GCC)</span><span class="sxs-lookup"><span data-stu-id="7de39-107">Government Community Cloud (GCC)</span></span>
> * <span data-ttu-id="7de39-108">GCC High</span><span class="sxs-lookup"><span data-stu-id="7de39-108">GCC High</span></span>
> * <span data-ttu-id="7de39-109">DoD</span><span class="sxs-lookup"><span data-stu-id="7de39-109">DoD</span></span>

## <a name="installing-app-studio"></a><span data-ttu-id="7de39-110">App Studio をインストールする</span><span class="sxs-lookup"><span data-stu-id="7de39-110">Installing App Studio</span></span>

<span data-ttu-id="7de39-111">App Studio は、Teams ストアで入手できる Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="7de39-111">App Studio is a Teams app which can be found in the Teams store.</span></span> <span data-ttu-id="7de39-112">直接ダウンロード App Studio の場合は、この [リンクに従います](https://aka.ms/InstallTeamsAppStudio)。</span><span class="sxs-lookup"><span data-stu-id="7de39-112">Follow this link for direct download [App Studio](https://aka.ms/InstallTeamsAppStudio).</span></span> <span data-ttu-id="7de39-113">また、アプリ ストアでアプリを検索することもできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-113">You can also find the app in the app store.</span></span>

<span data-ttu-id="7de39-114">ストアで、App Studio を検索します。</span><span class="sxs-lookup"><span data-stu-id="7de39-114">In the store, search for App Studio.</span></span>

![ストアでの App Studio の入力](~/assets/images/get-started/storeteamsappstudio.png)

<span data-ttu-id="7de39-116">App Studio タイルを選択して、アプリのインストール ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="7de39-116">Select the App Studio tile to open the app install page:</span></span>

![App Studio の構成](~/assets/images/get-started/teamsappstudioconfiguration.png)

<span data-ttu-id="7de39-118">**[インストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7de39-118">Select **install**.</span></span>

![App Studio](~/assets/images/get-started/teamsappstudio.png)

<span data-ttu-id="7de39-120">App Studio を起動したら、**[マニフェスト エディター]** タブをクリックします。そこで、既存のアプリをインポートするか、新しいアプリを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="7de39-120">Once you are in App Studio, click on the **Manifest editor** tab where you can either import an existing app or create a new app.</span></span>

## <a name="app-studio-features"></a><span data-ttu-id="7de39-121">App Studio の機能</span><span class="sxs-lookup"><span data-stu-id="7de39-121">App Studio Features</span></span>

<span data-ttu-id="7de39-122">このセクションでは、会話、マニフェスト エディター、詳細、機能などの機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="7de39-122">This section covers features, such as conversation, manifest editor, details, and capabilities.</span></span> <span data-ttu-id="7de39-123">アプリのカスタマイズを使用して機能をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-123">You can customize your capabilities using app customization.</span></span>

### <a name="conversation"></a><span data-ttu-id="7de39-124">会話</span><span class="sxs-lookup"><span data-stu-id="7de39-124">Conversation</span></span>

<span data-ttu-id="7de39-125">ここでは、[App Studio で作成したカード](#card-editor)を自分自身に送信してテストする際に、それらのカードが Teams でどのように表示されるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-125">This is where you can see what [cards you create in App Studio](#card-editor) look like in Teams when you test them by sending them to yourself.</span></span>

### <a name="manifest-editor"></a><span data-ttu-id="7de39-126">マニフェスト エディター</span><span class="sxs-lookup"><span data-stu-id="7de39-126">Manifest Editor</span></span>

<span data-ttu-id="7de39-127">先に述べたように、Microsoft Teams アプリ パッケージの最も重要な部分は、manifest.json ファイルです。</span><span class="sxs-lookup"><span data-stu-id="7de39-127">As mentioned earlier, the most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="7de39-128">このファイルは、[Teams アプリのスキーマ](~/resources/schema/manifest-schema.md)に準拠している必要があります。これには、Teams でアプリをユーザーに適切に表示するためのメタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7de39-128">This file, which must conform to the [Teams App schema](~/resources/schema/manifest-schema.md), contains metadata which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="7de39-129">App Studio の [マニフェスト エディター] タブでは、マニフェストの作成が容易になるため、アプリを説明したり、アイコンをアップロードしたり、アプリの機能を追加したりすることができます。また、.zip ファイルを作成し、テスト用に簡単に Teams にアップロードして、他のユーザーが使用できるように配布することができます。</span><span class="sxs-lookup"><span data-stu-id="7de39-129">The Manifest Editor tab in App Studio simplifies creating the manifest, allowing you to describe the app, upload your icons, add app capabilities, and produce a .zip file which can easily be uploaded into Teams for testing or distributed for others to use.</span></span> <span data-ttu-id="7de39-130">App Studio では、アプリに対して機能するコードが生成されることも、アプリがホストされることもありません。</span><span class="sxs-lookup"><span data-stu-id="7de39-130">Note that App Studio does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="7de39-131">アプリは、既にホストされており、アプリのアップロード プロセスのマニフェストに記載されている URL で実行されている必要があります。これにより、アプリが正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="7de39-131">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

#### <a name="details"></a><span data-ttu-id="7de39-132">詳細</span><span class="sxs-lookup"><span data-stu-id="7de39-132">Details</span></span>

<span data-ttu-id="7de39-133">マニフェスト エディターの詳細セクションでは、作成中のアプリに関する詳細な説明を定義します。</span><span class="sxs-lookup"><span data-stu-id="7de39-133">The details section of the Manifest Editor defines the high-level description of the app you are making.</span></span> <span data-ttu-id="7de39-134">これには、アプリの名前、説明、視覚的なブランド化などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7de39-134">This includes things such as the app’s name, description, and visual branding.</span></span> <span data-ttu-id="7de39-135">アプリの GUID を自動的に生成して、プライバシーに関する声明や利用規約の URL を入力できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-135">You can automatically generate a GUID for your app and provide URLs for your privacy statement and terms of use.</span></span>

#### <a name="capabilities"></a><span data-ttu-id="7de39-136">機能</span><span class="sxs-lookup"><span data-stu-id="7de39-136">Capabilities</span></span>

<span data-ttu-id="7de39-137">マニフェスト エディターの機能セクションでは、アプリの機能が定義され、各機能の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7de39-137">The capabilities section of the Manifest Editor is where the app's capabilities are defined and where details of each of those capabilities are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="7de39-138">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7de39-138">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="7de39-139">詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="7de39-139">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>


##### <a name="tabs"></a><span data-ttu-id="7de39-140">タブ</span><span class="sxs-lookup"><span data-stu-id="7de39-140">Tabs</span></span>

* <span data-ttu-id="7de39-141">**チーム タブ。**</span><span class="sxs-lookup"><span data-stu-id="7de39-141">**Team Tabs.**</span></span> <span data-ttu-id="7de39-142">チーム タブは、チャネルの一部となり、そこからチームの情報やリソースにすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-142">A team tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="7de39-143">たとえば、チャネルの Planner タブには 1 つのプランが含まれており、Power BI タブは特定のレポートにマッピングします。</span><span class="sxs-lookup"><span data-stu-id="7de39-143">For example, the Planner tab for a channel contains a single plan; the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="7de39-144">ユーザーは関連するコンテキストにドリルダウンできますが、タブの外側には移動できません。たとえば、Power BI タブでは、その他の Power BI レポートへの移動を有効にすることはできませんが、メインの Power BI Web サイト内のレポートを起動する *[Web サイトに移動]* ボタンを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-144">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the *Go to website* button that launches the report in the main Power BI website.</span></span>

  <span data-ttu-id="7de39-145">チーム タブでは、オプションを表示して情報を収集するための *構成 URL* を指定して、ユーザーがタブの内容と操作性をカスタマイズできるようにする必要があります。この iframe に対応している HTML ページは、ユーザーが最初にタブをチャネルに追加するときに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7de39-145">For team tabs, you must provide a *Configuration URL* to present options and gather information so users can customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>

  <span data-ttu-id="7de39-146">また、読み込み元またはリンク先になると予測される追加のドメインも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7de39-146">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="7de39-147">**個人タブ。**</span><span class="sxs-lookup"><span data-stu-id="7de39-147">**Personal Tabs.**</span></span> <span data-ttu-id="7de39-148">このセクションでは、個人用アプリ エクスペリエンスで既定で表示される一連のタブを定義できます (ユーザーがチームやチャネルのコンテキスト外でアプリを使用する場合)。</span><span class="sxs-lookup"><span data-stu-id="7de39-148">This section lets you define a set of tabs that are presented by default in the personal app experience (experience a user has with your app outside the context of a team or channel).</span></span> <span data-ttu-id="7de39-149">このセクションでは、タブ名、一意識別子、Teams に表示される UI を示す URL を指定します。必要に応じて、ユーザーがブラウザーでタブを表示することを選択した場合に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="7de39-149">In this section, provide the tab name, a unique identifier, the URL that points to the UI to be displayed in Teams, and optionally, the URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="7de39-150">[Teamsを使用して、タブが読み込みまたはリンク先と予想される追加のドメインを指定します。</span><span class="sxs-lookup"><span data-stu-id="7de39-150">With Teams tabs, provide any additional domains from which the tab expects to load from or link to.</span></span>

##### <a name="bots"></a><span data-ttu-id="7de39-151">ボット</span><span class="sxs-lookup"><span data-stu-id="7de39-151">Bots</span></span>

<span data-ttu-id="7de39-152">このセクションでは、[会話ボット](~/bots/what-are-bots.md)をアプリに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="7de39-152">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="7de39-153">Bot Framework にボットが既に登録されている場合、そのボットを追加するには、*[Set Up]* (セットアップ) をクリックし、ボットの名前と Bot Framework ID を指定し、ボットが動作するスコープを定義します。</span><span class="sxs-lookup"><span data-stu-id="7de39-153">If you already have a bot registered with Bot Framework, you can add that bot by clicking *Set Up* and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

<span data-ttu-id="7de39-154">Bot Framework にボットをまだ登録していない場合は、**[Register]** (登録) をクリックして新しいボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="7de39-154">If you have not yet registered a bot with the Bot Framework, click **Register** to create a new one.</span></span> <span data-ttu-id="7de39-155">ボットの登録が完了したら、[Manifest Editor] (マニフェスト エディター) のこのセクションに戻り、ボットの名前と Bot Framework ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="7de39-155">Once you’re done registering your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

<span data-ttu-id="7de39-156">ボットの情報を提供した後、必要に応じて、ボットがユーザーに提案できるコマンドの一覧を定義できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-156">After you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="7de39-157">コマンドの名前、コマンドの構文と引数を示すコマンドの説明、このコマンドが適用されるスコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="7de39-157">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

> [!NOTE]
> <span data-ttu-id="7de39-158">ボットが 1 つのスコープのみをサポートするために定義されている場合、サポートされていないスコープに指定されたコマンドは無視されます。</span><span class="sxs-lookup"><span data-stu-id="7de39-158">If you have defined your bot to only support one scope, the commands specified for the unsupported scope is ignored.</span></span> <span data-ttu-id="7de39-159">ボットがサポートするスコープはいつでも編集できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-159">You can edit the scopes your bot supports at any time.</span></span>

##### <a name="connectors"></a><span data-ttu-id="7de39-160">コネクタ</span><span class="sxs-lookup"><span data-stu-id="7de39-160">Connectors</span></span>

<span data-ttu-id="7de39-161">このセクションでは、コネクタをアプリに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="7de39-161">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="7de39-162">Office 365 コネクタが既に登録されている場合は、**[セットアップ]** を選択して、コネクタの名前と ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="7de39-162">If you already have registered an Office 365 connector, choose **Set up** and enter the name and ID of the connector.</span></span> <span data-ttu-id="7de39-163">新しいコネクタが必要な場合は、**[登録]** をクリックして、ブラウザーでコネクタ開発者ダッシュボードに移動します。</span><span class="sxs-lookup"><span data-stu-id="7de39-163">If you want a new connector click **Register** to be taken to the Connector Developer Dashboard in your browser.</span></span>

> [!NOTE]
> <span data-ttu-id="7de39-164">アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれたアプリの外観を変更できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-164">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="7de39-165">たとえば、管理者Teams Contoso から **Contoso** **エージェント** にアプリの名前をカスタマイズすると、ユーザーに Contoso **Agent** という新しい名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7de39-165">For example, if the Teams admin customizes the name of an app from **Contoso** to **Contoso Agent**, then the app will appear with the new name **Contoso Agent** to users.</span></span> <span data-ttu-id="7de39-166">ただし、チャットにコネクタを追加している間、一覧でコネクタは引き続きアプリの名前を Contoso として表示 **します**。</span><span class="sxs-lookup"><span data-stu-id="7de39-166">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as **Contoso**.</span></span>


##### <a name="messaging-extensions"></a><span data-ttu-id="7de39-167">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="7de39-167">Messaging Extensions</span></span>

<span data-ttu-id="7de39-168">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md) は、ユーザーが Microsoft Teams 内でアプリを使用する強力な方法です。</span><span class="sxs-lookup"><span data-stu-id="7de39-168">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="7de39-169">ユーザーはサービスからの情報に対してクエリを実行して、その情報をカード形式でチャネルやチャット会話に直接投稿できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-169">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

<span data-ttu-id="7de39-170">メッセージング拡張機能は Bot Framework ボットを利用しているため、動作するには構成済みのボットが必要です。</span><span class="sxs-lookup"><span data-stu-id="7de39-170">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="7de39-171">メッセージング拡張機能を利用するボットの名前と Bot Framework ID がある場合は、入力します。</span><span class="sxs-lookup"><span data-stu-id="7de39-171">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="7de39-172">それ以外の場合は、**[登録]** をクリックしてボットを作成し、後で情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="7de39-172">Otherwise, click **Register** to create one and enter the information afterward.</span></span> <span data-ttu-id="7de39-173">ユーザーがメッセージング拡張機能の構成を更新できるかどうかを選択します。</span><span class="sxs-lookup"><span data-stu-id="7de39-173">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

<span data-ttu-id="7de39-174">基になっているボットを構成したら、メッセージング拡張機能で許可されるコマンドとパラメーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="7de39-174">Once you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

<span data-ttu-id="7de39-175">各コマンドには、タイトルと ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="7de39-175">Each command requires a title and an ID.</span></span> <span data-ttu-id="7de39-176">必要に応じて、コマンドにユーザーの説明を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="7de39-176">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="7de39-177">各コマンドは最大 5 つのパラメーターをサポートできます。各パラメーターには次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="7de39-177">Each command can support up to five parameters, each of which requires:</span></span>

* <span data-ttu-id="7de39-178">パラメーターがクライアントに表示され、Teamsに含まれるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="7de39-178">The name of the parameter as it appears in the Teams client and is included in the user request.</span></span>
* <span data-ttu-id="7de39-179">ユーザーフレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="7de39-179">A user-friendly title.</span></span>
* <span data-ttu-id="7de39-180">任意の説明。</span><span class="sxs-lookup"><span data-stu-id="7de39-180">An optional description.</span></span>

> [!NOTE]
> <span data-ttu-id="7de39-181">アプリ スタジオを使用してメッセージング拡張機能を作成するには、「 [アプリ スタジオを使用してメッセージング拡張機能を作成する」を参照してください](~/resources/create-messaging-extension-using-appstudio.md)。</span><span class="sxs-lookup"><span data-stu-id="7de39-181">To create messaging extension using app studio, see [create messaging extension using app studio](~/resources/create-messaging-extension-using-appstudio.md).</span></span>

#### <a name="test-and-distribute"></a><span data-ttu-id="7de39-182">テストと配布</span><span class="sxs-lookup"><span data-stu-id="7de39-182">Test and Distribute</span></span>

<span data-ttu-id="7de39-183">アプリケーションの定義が完了したら、テストと配布のセクションを使用して、アプリの定義を zip ファイルとしてエクスポートし、それをテストのために Teams クライアントに共有およびアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-183">Once you have finished defining your application, the Test and Distribute section allows you export your app’s definition as a zip file which then can be shared and uploaded into the Teams client for testing.</span></span> <span data-ttu-id="7de39-184">[Export] (エクスポート) をクリックすると、zip ファイルが *appname.zip* として既定のダウンロード ディレクトリにダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="7de39-184">Clicking export downloads the zip file as *appname.zip* in your default download directory.</span></span>

##### <a name="publish-your-app-to-teams"></a><span data-ttu-id="7de39-185">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="7de39-185">Publish your app to Teams</span></span>
<span data-ttu-id="7de39-186">プロジェクトのホーム ページでは、アプリをチーム向けにアップロードしたり、組織内のユーザー向けに会社のカスタム App Store に提出したり、すべての Teams ユーザー向けに App Source に提出したりできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-186">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="7de39-187">これらの送信内容は、IT 管理者によって審査されます。</span><span class="sxs-lookup"><span data-stu-id="7de39-187">Your IT admin will review these submissions.</span></span> <span data-ttu-id="7de39-188">*[Publish]* (発行) ページに戻ると提出ステータスを確認することができ、アプリが IT 管理者によって承認または却下されたかどうかを確認できます。このページでは、アプリの更新プログラムを提出したり、現在提出中のアプリをキャンセルしたりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-188">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

### <a name="card-editor"></a><span data-ttu-id="7de39-189">Card Editor</span><span class="sxs-lookup"><span data-stu-id="7de39-189">Card Editor</span></span>

<span data-ttu-id="7de39-190">カードは、短い情報または関連する情報のコンテナーです。</span><span class="sxs-lookup"><span data-stu-id="7de39-190">A card is a container for short or related pieces of information.</span></span> <span data-ttu-id="7de39-191">Microsoft Teams はカードをサポートしています。このカードには複数のプロパティと添付ファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="7de39-191">Microsoft Teams supports cards, which can have multiple properties and attachments.</span></span> <span data-ttu-id="7de39-192">カードは、ボットとコネクタが実行可能な情報をユーザーに中継するための主要な方法です。</span><span class="sxs-lookup"><span data-stu-id="7de39-192">Cards are a key way that bots and connectors relay actionable information to users.</span></span> 

<span data-ttu-id="7de39-193">このプロセスを簡単にし、エラーが発生しにくくするために、[カード エディター] タブでは、フォームを使用してヒーロー カードまたはサムネイル カードを作成し、ボットを介して結果のカード (ユーザーが表示するとおり) を確認してテストできます。</span><span class="sxs-lookup"><span data-stu-id="7de39-193">To make this process easier and less error-prone, the Card Editor tab lets you build Hero Cards or Thumbnail Cards using a form and verify and test the resulting card (exactly as a user would see it) through a bot.</span></span> <span data-ttu-id="7de39-194">また、アプリのソース コードにコピーまたは貼り付けることができるカードの対応する JSON、C#、Node.js コードも提供されます。</span><span class="sxs-lookup"><span data-stu-id="7de39-194">It also provides the corresponding JSON, C#, or Node.js code for the card that you can copy/paste into your app's source code.</span></span>

<span data-ttu-id="7de39-195">Teams の内部で確認するカードが既にある場合は、そのカードの JSON を *[カード情報の追加]* の JSON タブに貼り付け、自分に送信してチャットでどのように表示されるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-195">If you already have a card that you would like to verify inside Teams, you can paste the JSON for that card into the JSON tab under *Add card info* and send it to yourself to see what it looks like in a chat.</span></span>

### <a name="react-control-library"></a><span data-ttu-id="7de39-196">React 制御ライブラリ</span><span class="sxs-lookup"><span data-stu-id="7de39-196">React Control Library</span></span>

>[!Note]
> <span data-ttu-id="7de39-197">このReactコントロール ライブラリは今後非推奨です。</span><span class="sxs-lookup"><span data-stu-id="7de39-197">This React control library is deprecated in the future.</span></span> <span data-ttu-id="7de39-198">以前は Stardust UI の代わりに [Fluent-UI](https://microsoft.github.io/fluent-ui-react/) 対応コントロールを使用する場合を検討してください。</span><span class="sxs-lookup"><span data-stu-id="7de39-198">Consider using the [Fluent-UI react controls as an alternative](https://microsoft.github.io/fluent-ui-react/) previously Stardust UI.</span></span>

<span data-ttu-id="7de39-199">Teams のベスト プラクティスに従ってアプリを作成するのは、アプリを Teams クライアントの操作環境にシームレスに適合する外観にするための優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="7de39-199">Creating an app that follows the Teams best practices is a great way to give your app a look and feel that fits seamlessly with the Teams client experience.</span></span> <span data-ttu-id="7de39-200">この目的を達成するため、使用する UI コントロールは重要な要素となります。</span><span class="sxs-lookup"><span data-stu-id="7de39-200">The UI controls that you use are critical to achieving that end.</span></span> <span data-ttu-id="7de39-201">一貫性のある UI を簡単に作成できるようにするため、App Studio には、Teams デザインの原則に準拠する UI コントロールのいくつかのカテゴリがあります。</span><span class="sxs-lookup"><span data-stu-id="7de39-201">To make it easier to create a consistent UI, App Studio provides several categories of UI controls which follow Teams design principles.</span></span>

<span data-ttu-id="7de39-202">コントロールと対応する React コンポーネントの例が提供され、アプリをビルドするときに使用できます。</span><span class="sxs-lookup"><span data-stu-id="7de39-202">Examples of the controls and corresponding React components are provided and ready to use in building your app.</span></span>

#### <a name="controls"></a><span data-ttu-id="7de39-203">コントロール</span><span class="sxs-lookup"><span data-stu-id="7de39-203">Controls</span></span>

<span data-ttu-id="7de39-204">コントロールには次が含まれます。</span><span class="sxs-lookup"><span data-stu-id="7de39-204">Controls include:</span></span>

* <span data-ttu-id="7de39-205">ボタン</span><span class="sxs-lookup"><span data-stu-id="7de39-205">Buttons</span></span>
* <span data-ttu-id="7de39-206">ドロップダウン</span><span class="sxs-lookup"><span data-stu-id="7de39-206">Dropdowns</span></span>
* <span data-ttu-id="7de39-207">チェックボックス</span><span class="sxs-lookup"><span data-stu-id="7de39-207">Checkboxes</span></span>
* <span data-ttu-id="7de39-208">ラジオ ボタン</span><span class="sxs-lookup"><span data-stu-id="7de39-208">Radio Buttons</span></span>
* <span data-ttu-id="7de39-209">切り替え</span><span class="sxs-lookup"><span data-stu-id="7de39-209">Toggles</span></span>
* <span data-ttu-id="7de39-210">テキスト領域</span><span class="sxs-lookup"><span data-stu-id="7de39-210">Text Areas</span></span>
* <span data-ttu-id="7de39-211">リンク</span><span class="sxs-lookup"><span data-stu-id="7de39-211">Links</span></span>
* <span data-ttu-id="7de39-212">タブ</span><span class="sxs-lookup"><span data-stu-id="7de39-212">Tabs</span></span>
* <span data-ttu-id="7de39-213">テーブル</span><span class="sxs-lookup"><span data-stu-id="7de39-213">Tables</span></span>
* <span data-ttu-id="7de39-214">アイコン</span><span class="sxs-lookup"><span data-stu-id="7de39-214">Icons</span></span>
