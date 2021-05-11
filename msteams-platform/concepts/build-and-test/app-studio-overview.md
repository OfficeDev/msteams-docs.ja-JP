---
title: Microsoft Teams 用の App Studio を開始する
description: App Studio を使用して Microsoft Teams で優れたアプリのビルドを開始する
keywords: App Studio Teams の開始
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 0e6a00921b3f24381758b13bd6042da18a3ac2c1
ms.sourcegitcommit: 808a203fb963eeade3a8e32db88d64677e37df7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2021
ms.locfileid: "52304034"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a><span data-ttu-id="05aa9-104">Microsoft Teams 用の App Studio を使用してアプリをすばやく開発する</span><span class="sxs-lookup"><span data-stu-id="05aa9-104">Quickly develop apps with App Studio for Microsoft Teams</span></span>

<span data-ttu-id="05aa9-105">App Studio を使用すると、Microsoft Teams アプリの作成や統合を簡単に始めることができます。自分の組織用にカスタム アプリを開発する場合も、世界各地のチーム用に SaaS アプリケーションを開発する場合も、App Studio ではマニフェストの作成とアプリのパッケージングが合理化され、Card Editor や React 制御ライブラリなどの便利なツールが提供されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-105">App Studio makes it easy to start creating or integrating your own Microsoft Teams apps, whether you develop custom apps for your enterprise or SaaS applications for teams around the world by streamlining the creation of the manifest and package for your app and providing useful tools like the Card Editor and a React control library.</span></span>

## <a name="installing-app-studio"></a><span data-ttu-id="05aa9-106">App Studio をインストールする</span><span class="sxs-lookup"><span data-stu-id="05aa9-106">Installing App Studio</span></span>

<span data-ttu-id="05aa9-107">App Studio は、Teams ストアで入手できる Teams アプリです。</span><span class="sxs-lookup"><span data-stu-id="05aa9-107">App Studio is a Teams app which can be found in the Teams store.</span></span> <span data-ttu-id="05aa9-108">直接ダウンローするには、このリンクを参照します: [App Studio](https://aka.ms/InstallTeamsAppStudio) (アプリ ストアでアプリを見つけることもできます)。</span><span class="sxs-lookup"><span data-stu-id="05aa9-108">Follow this link for direct download: [App Studio](https://aka.ms/InstallTeamsAppStudio) (you can also find the app in the app store).</span></span>

<span data-ttu-id="05aa9-109">ストアで、App Studio を検索します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-109">In the store, search for App Studio.</span></span>

![ストアでの App Studio の入力](~/assets/images/get-started/storeteamsappstudio.png)

<span data-ttu-id="05aa9-111">App Studio タイルを選択して、アプリのインストール ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-111">Select the App Studio tile to open the app install page:</span></span>

![App Studio の構成](~/assets/images/get-started/teamsappstudioconfiguration.png)

<span data-ttu-id="05aa9-113">*[インストール]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-113">Select *install*.</span></span>

![App Studio](~/assets/images/get-started/teamsappstudio.png)

<span data-ttu-id="05aa9-115">App Studio を起動したら、*[マニフェスト エディター]* タブをクリックします。そこで、既存のアプリをインポートするか、新しいアプリを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-115">Once you are in App Studio, click on the *Manifest editor* tab where you can either import an existing app or create a new app.</span></span>

## <a name="app-studio-features"></a><span data-ttu-id="05aa9-116">App Studio の機能</span><span class="sxs-lookup"><span data-stu-id="05aa9-116">App Studio Features</span></span>

<span data-ttu-id="05aa9-117">このセクションでは、会話、マニフェスト エディター、詳細、機能などの機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-117">This section covers features, such as conversation, manifest editor, details, and capabilities.</span></span> <span data-ttu-id="05aa9-118">アプリのカスタマイズを使用して機能をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-118">You can customize your capabilities using app customization.</span></span>

### <a name="conversation"></a><span data-ttu-id="05aa9-119">会話</span><span class="sxs-lookup"><span data-stu-id="05aa9-119">Conversation</span></span>

<span data-ttu-id="05aa9-120">ここでは、[App Studio で作成したカード](#card-editor)を自分自身に送信してテストする際に、それらのカードが Teams でどのように表示されるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-120">This is where you can see what [cards you create in App Studio](#card-editor) look like in Teams when you test them by sending them to yourself.</span></span>

### <a name="manifest-editor"></a><span data-ttu-id="05aa9-121">マニフェスト エディター</span><span class="sxs-lookup"><span data-stu-id="05aa9-121">Manifest Editor</span></span>

<span data-ttu-id="05aa9-122">先に述べたように、Microsoft Teams アプリ パッケージの最も重要な部分は、manifest.json ファイルです。</span><span class="sxs-lookup"><span data-stu-id="05aa9-122">As mentioned earlier, the most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="05aa9-123">このファイルは、[Teams アプリのスキーマ](~/resources/schema/manifest-schema.md)に準拠している必要があります。これには、Teams でアプリをユーザーに適切に表示するためのメタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="05aa9-123">This file, which must conform to the [Teams App schema](~/resources/schema/manifest-schema.md), contains metadata which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="05aa9-124">App Studio の [マニフェスト エディター] タブでは、マニフェストの作成が容易になるため、アプリを説明したり、アイコンをアップロードしたり、アプリの機能を追加したりすることができます。また、.zip ファイルを作成し、テスト用に簡単に Teams にアップロードして、他のユーザーが使用できるように配布することができます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-124">The Manifest Editor tab in App Studio simplifies creating the manifest, allowing you to describe the app, upload your icons, add app capabilities, and produce a .zip file which can easily be uploaded into Teams for testing or distributed for others to use.</span></span> <span data-ttu-id="05aa9-125">App Studio では、アプリに対して機能するコードが生成されることも、アプリがホストされることもありません。</span><span class="sxs-lookup"><span data-stu-id="05aa9-125">Note that App Studio does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="05aa9-126">アプリは、既にホストされており、アプリのアップロード プロセスのマニフェストに記載されている URL で実行されている必要があります。これにより、アプリが正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-126">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

#### <a name="details"></a><span data-ttu-id="05aa9-127">詳細</span><span class="sxs-lookup"><span data-stu-id="05aa9-127">Details</span></span>

<span data-ttu-id="05aa9-128">マニフェスト エディターの詳細セクションでは、作成中のアプリに関する詳細な説明を定義します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-128">The details section of the Manifest Editor defines the high-level description of the app you are making.</span></span> <span data-ttu-id="05aa9-129">これには、アプリの名前、説明、視覚的なブランド化などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-129">This includes things such as the app’s name, description, and visual branding.</span></span> <span data-ttu-id="05aa9-130">アプリの GUID を自動的に生成して、プライバシーに関する声明や利用規約の URL を入力できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-130">You can automatically generate a GUID for your app and provide URLs for your privacy statement and terms of use.</span></span>

#### <a name="capabilities"></a><span data-ttu-id="05aa9-131">機能</span><span class="sxs-lookup"><span data-stu-id="05aa9-131">Capabilities</span></span>

<span data-ttu-id="05aa9-132">マニフェスト エディターの機能セクションでは、アプリの機能が定義され、各機能の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-132">The capabilities section of the Manifest Editor is where the app's capabilities are defined and where details of each of those capabilities are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="05aa9-133">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05aa9-133">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="05aa9-134">詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="05aa9-134">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>


##### <a name="tabs"></a><span data-ttu-id="05aa9-135">タブ</span><span class="sxs-lookup"><span data-stu-id="05aa9-135">Tabs</span></span>

* <span data-ttu-id="05aa9-136">**チーム タブ。**</span><span class="sxs-lookup"><span data-stu-id="05aa9-136">**Team Tabs.**</span></span> <span data-ttu-id="05aa9-137">チーム タブは、チャネルの一部となり、そこからチームの情報やリソースにすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-137">A team tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="05aa9-138">たとえば、チャネルの Planner タブには 1 つのプランが含まれており、Power BI タブは特定のレポートにマッピングします。</span><span class="sxs-lookup"><span data-stu-id="05aa9-138">For example, the Planner tab for a channel contains a single plan; the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="05aa9-139">ユーザーは関連するコンテキストにドリルダウンできますが、タブの外側には移動できません。たとえば、Power BI タブでは、その他の Power BI レポートへの移動を有効にすることはできませんが、メインの Power BI Web サイト内のレポートを起動する *[Web サイトに移動]* ボタンを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-139">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the *Go to website* button that launches the report in the main Power BI website.</span></span>

  <span data-ttu-id="05aa9-140">チーム タブでは、オプションを表示して情報を収集するための *構成 URL* を指定して、ユーザーがタブの内容と操作性をカスタマイズできるようにする必要があります。この iframe に対応している HTML ページは、ユーザーが最初にタブをチャネルに追加するときに表示されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-140">For team tabs, you must provide a *Configuration URL* to present options and gather information so users can customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>

  <span data-ttu-id="05aa9-141">また、読み込み元またはリンク先になると予測される追加のドメインも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05aa9-141">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="05aa9-142">**個人タブ。**</span><span class="sxs-lookup"><span data-stu-id="05aa9-142">**Personal Tabs.**</span></span> <span data-ttu-id="05aa9-143">このセクションでは、個人用アプリの操作環境 (つまり、ユーザーがチームやチャネルのコンテキスト外のアプリでのユーザーの操作性) に既定で表示されるタブのセットを定義できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-143">This section lets you define a set of tabs that are presented by default in the personal app experience (i.e. the experience a user has with your app outside the context of a team or channel).</span></span> <span data-ttu-id="05aa9-144">このセクションでは、タブ名、一意識別子、Teams に表示される UI を示す URL を指定します。必要に応じて、ユーザーがブラウザーでタブを表示することを選択した場合に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-144">In this section, provide the tab name, a unique identifier, the URL that points to the UI to be displayed in Teams, and optionally, the URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="05aa9-145">チーム タブの場合と同様に、読み込み元またはリンク先になると予測される追加のドメインを指定します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-145">As with Teams tabs, provide any additional domains from which the tab expects to load from or link to.</span></span>

##### <a name="bots"></a><span data-ttu-id="05aa9-146">ボット</span><span class="sxs-lookup"><span data-stu-id="05aa9-146">Bots</span></span>

<span data-ttu-id="05aa9-147">このセクションでは、[会話ボット](~/bots/what-are-bots.md)をアプリに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-147">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="05aa9-148">Bot Framework にボットが既に登録されている場合、そのボットを追加するには、*[Set Up]* (セットアップ) をクリックし、ボットの名前と Bot Framework ID を指定し、ボットが動作するスコープを定義します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-148">If you already have a bot registered with Bot Framework, you can add that bot by clicking *Set Up* and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

<span data-ttu-id="05aa9-149">Bot Framework にボットをまだ登録していない場合は、*[Register]* (登録) をクリックして新しいボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-149">If you have not yet registered a bot with the Bot Framework, click *Register* to create a new one.</span></span> <span data-ttu-id="05aa9-150">ボットの登録が完了したら、[Manifest Editor] (マニフェスト エディター) のこのセクションに戻り、ボットの名前と Bot Framework ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-150">Once you’re done registering your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

<span data-ttu-id="05aa9-151">ボットの情報を提供した後、必要に応じて、ボットがユーザーに提案できるコマンドの一覧を定義できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-151">After you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="05aa9-152">コマンドの名前、コマンドの構文と引数を示すコマンドの説明、このコマンドが適用されるスコープを追加します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-152">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

<span data-ttu-id="05aa9-153">1 つのスコープのみをサポートするようにボットを定義した場合、サポートされていないスコープに指定したコマンドは無視されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-153">Note that if you have defined your bot to only support one scope, commands specified for the unsupported scope will be ignored.</span></span> <span data-ttu-id="05aa9-154">ボットがサポートするスコープはいつでも編集できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-154">You can edit the scopes your bot supports at any time.</span></span>

##### <a name="connectors"></a><span data-ttu-id="05aa9-155">コネクタ</span><span class="sxs-lookup"><span data-stu-id="05aa9-155">Connectors</span></span>

<span data-ttu-id="05aa9-156">このセクションでは、コネクタをアプリに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-156">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="05aa9-157">Office 365 コネクタが既に登録されている場合は、*[セットアップ]* を選択して、コネクタの名前と ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-157">If you already have registered an Office 365 connector, choose *Set up* and enter the name and ID of the connector.</span></span> <span data-ttu-id="05aa9-158">新しいコネクタが必要な場合は、*[登録]* をクリックして、ブラウザーでコネクタ開発者ダッシュボードに移動します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-158">If you want a new connector click *Register* to be taken to the Connector Developer Dashboard in your browser.</span></span>

> [!NOTE]
> <span data-ttu-id="05aa9-159">アプリのカスタマイズにより、管理者はボット、メッセージング拡張機能、タブ、コネクタを介して読み込まれたアプリの外観を変更できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-159">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="05aa9-160">たとえば、管理者Teams Contoso から *Contoso* *エージェント* にアプリの名前をカスタマイズすると、ユーザーに Contoso *Agent* という新しい名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-160">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="05aa9-161">ただし、チャットにコネクタを追加している間、一覧でコネクタは引き続きアプリの名前を Contoso として表示 *します*。</span><span class="sxs-lookup"><span data-stu-id="05aa9-161">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>


##### <a name="messaging-extensions"></a><span data-ttu-id="05aa9-162">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="05aa9-162">Messaging Extensions</span></span>

<span data-ttu-id="05aa9-163">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md) は、ユーザーが Microsoft Teams 内でアプリを使用する強力な方法です。</span><span class="sxs-lookup"><span data-stu-id="05aa9-163">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="05aa9-164">ユーザーはサービスからの情報に対してクエリを実行して、その情報をカード形式でチャネルやチャット会話に直接投稿できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-164">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

<span data-ttu-id="05aa9-165">メッセージング拡張機能は Bot Framework ボットを利用しているため、動作するには構成済みのボットが必要です。</span><span class="sxs-lookup"><span data-stu-id="05aa9-165">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="05aa9-166">メッセージング拡張機能を利用するボットの名前と Bot Framework ID がある場合は、入力します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-166">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="05aa9-167">それ以外の場合は、*[登録]* をクリックしてボットを作成し、後で情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-167">Otherwise, click *Register* to create one and enter the information afterward.</span></span> <span data-ttu-id="05aa9-168">ユーザーがメッセージング拡張機能の構成を更新できるかどうかを選択します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-168">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

<span data-ttu-id="05aa9-169">基になっているボットを構成したら、メッセージング拡張機能で許可されるコマンドとパラメーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="05aa9-169">Once you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

<span data-ttu-id="05aa9-170">各コマンドには、タイトルと ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="05aa9-170">Each command requires a title and an ID.</span></span> <span data-ttu-id="05aa9-171">必要に応じて、コマンドにユーザーの説明を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-171">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="05aa9-172">各コマンドは最大 5 つのパラメーターをサポートできます。各パラメーターには次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="05aa9-172">Each command can support up to five parameters, each of which requires:</span></span>

* <span data-ttu-id="05aa9-173">Teams クライアントに表示され、ユーザーの要求に含まれているパラメーターの名前</span><span class="sxs-lookup"><span data-stu-id="05aa9-173">The name of the parameter as it appears in the Teams client and is included in the user request</span></span>
* <span data-ttu-id="05aa9-174">ユーザー フレンドリなタイトル</span><span class="sxs-lookup"><span data-stu-id="05aa9-174">A user-friendly title</span></span>
* <span data-ttu-id="05aa9-175">任意の説明</span><span class="sxs-lookup"><span data-stu-id="05aa9-175">An optional description</span></span>

> [!NOTE]
> <span data-ttu-id="05aa9-176">アプリ スタジオを使用してメッセージング拡張機能を作成するには、「 [アプリ スタジオを使用してメッセージング拡張機能を作成する」を参照してください](~/resources/create-messaging-extension-using-appstudio.md)。</span><span class="sxs-lookup"><span data-stu-id="05aa9-176">To create messaging extension using app studio, see [create messaging extension using app studio](~/resources/create-messaging-extension-using-appstudio.md).</span></span>

#### <a name="test-and-distribute"></a><span data-ttu-id="05aa9-177">テストと配布</span><span class="sxs-lookup"><span data-stu-id="05aa9-177">Test and Distribute</span></span>

<span data-ttu-id="05aa9-178">アプリケーションの定義が完了したら、テストと配布のセクションを使用して、アプリの定義を zip ファイルとしてエクスポートし、それをテストのために Teams クライアントに共有およびアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-178">Once you have finished defining your application, the Test and Distribute section allows you export your app’s definition as a zip file which then can be shared and uploaded into the Teams client for testing.</span></span> <span data-ttu-id="05aa9-179">[Export] (エクスポート) をクリックすると、zip ファイルが *appname.zip* として既定のダウンロード ディレクトリにダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-179">Clicking export downloads the zip file as *appname.zip* in your default download directory.</span></span>

##### <a name="publish-your-app-to-teams"></a><span data-ttu-id="05aa9-180">アプリを Teams に公開する</span><span class="sxs-lookup"><span data-stu-id="05aa9-180">Publish your app to Teams</span></span>
<span data-ttu-id="05aa9-181">プロジェクトのホーム ページでは、アプリをチーム向けにアップロードしたり、組織内のユーザー向けに会社のカスタム App Store に提出したり、すべての Teams ユーザー向けに App Source に提出したりできます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-181">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="05aa9-182">これらの送信内容は、IT 管理者によって審査されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-182">Your IT admin will review these submissions.</span></span> <span data-ttu-id="05aa9-183">*[Publish]* (発行) ページに戻ると提出ステータスを確認することができ、アプリが IT 管理者によって承認または却下されたかどうかを確認できます。このページでは、アプリの更新プログラムを提出したり、現在提出中のアプリをキャンセルしたりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-183">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

### <a name="card-editor"></a><span data-ttu-id="05aa9-184">Card Editor</span><span class="sxs-lookup"><span data-stu-id="05aa9-184">Card Editor</span></span>

<span data-ttu-id="05aa9-185">カードは、短い情報または関連する情報のコンテナーです。</span><span class="sxs-lookup"><span data-stu-id="05aa9-185">A card is a container for short or related pieces of information.</span></span> <span data-ttu-id="05aa9-186">Microsoft Teams はカードをサポートしています。このカードには複数のプロパティと添付ファイルを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-186">Microsoft Teams supports cards, which can have multiple properties and attachments.</span></span> <span data-ttu-id="05aa9-187">カードは、ボットとコネクタが実行可能な情報をユーザーに中継するための主要な方法です。</span><span class="sxs-lookup"><span data-stu-id="05aa9-187">Cards are a key way that bots and connectors relay actionable information to users.</span></span> 

<span data-ttu-id="05aa9-188">このプロセスをより簡単でエラーの起きにくいものにするため、Card Editor タブでは、フォームを使用してヒーロー カードやサムネイル カードをビルドし、生成されるカード (ユーザーに表示されるとおりのカード) をボットで検証してテストします。</span><span class="sxs-lookup"><span data-stu-id="05aa9-188">To make this process easier and less error-prone, the Card Editor tab lets you build Hero Cards or Thumbnail Cards using a form and verify and test the resulting card (exactly as a user would see it) via a bot.</span></span> <span data-ttu-id="05aa9-189">また、アプリのソース コードにコピーまたは貼り付けることができるカードの対応する JSON、C#、Node.js コードも提供されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-189">It also provides the corresponding JSON, C#, or Node.js code for the card that you can copy/paste into your app's source code.</span></span>

<span data-ttu-id="05aa9-190">Teams の内部で確認するカードが既にある場合は、そのカードの JSON を *[カード情報の追加]* の JSON タブに貼り付け、自分に送信してチャットでどのように表示されるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-190">If you already have a card that you would like to verify inside Teams, you can paste the JSON for that card into the JSON tab under *Add card info* and send it to yourself to see what it looks like in a chat.</span></span>

### <a name="react-control-library"></a><span data-ttu-id="05aa9-191">React 制御ライブラリ</span><span class="sxs-lookup"><span data-stu-id="05aa9-191">React Control Library</span></span>

>[!Note]
> <span data-ttu-id="05aa9-192">この React 制御ライブラリは今後廃止されます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-192">This React control library will be deprecated in the future.</span></span> <span data-ttu-id="05aa9-193">[代わりに Fluent-UI React 制御](https://microsoft.github.io/fluent-ui-react/) (以前の Stardust UI) を使うことをご検討ください。</span><span class="sxs-lookup"><span data-stu-id="05aa9-193">Consider using the [Fluent-UI react controls as an alternative](https://microsoft.github.io/fluent-ui-react/) (formerly Stardust UI).</span></span>

<span data-ttu-id="05aa9-194">Teams のベスト プラクティスに従ってアプリを作成するのは、アプリを Teams クライアントの操作環境にシームレスに適合する外観にするための優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="05aa9-194">Creating an app that follows the Teams best practices is a great way to give your app a look and feel that fits seamlessly with the Teams client experience.</span></span> <span data-ttu-id="05aa9-195">この目的を達成するため、使用する UI コントロールは重要な要素となります。</span><span class="sxs-lookup"><span data-stu-id="05aa9-195">The UI controls that you use are critical to achieving that end.</span></span> <span data-ttu-id="05aa9-196">一貫性のある UI を簡単に作成できるようにするため、App Studio には、Teams デザインの原則に準拠する UI コントロールのいくつかのカテゴリがあります。</span><span class="sxs-lookup"><span data-stu-id="05aa9-196">To make it easier to create a consistent UI, App Studio provides several categories of UI controls which follow Teams design principles.</span></span>

<span data-ttu-id="05aa9-197">コントロールと対応する React コンポーネントの例が提供され、アプリをビルドするときに使用できます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-197">Examples of the controls and corresponding React components are provided and ready to use in building your app.</span></span>

#### <a name="controls"></a><span data-ttu-id="05aa9-198">コントロール</span><span class="sxs-lookup"><span data-stu-id="05aa9-198">Controls</span></span>

<span data-ttu-id="05aa9-199">コントロールには次が含まれます。</span><span class="sxs-lookup"><span data-stu-id="05aa9-199">Controls include:</span></span>

* <span data-ttu-id="05aa9-200">ボタン</span><span class="sxs-lookup"><span data-stu-id="05aa9-200">Buttons</span></span>
* <span data-ttu-id="05aa9-201">ドロップダウン</span><span class="sxs-lookup"><span data-stu-id="05aa9-201">Dropdowns</span></span>
* <span data-ttu-id="05aa9-202">チェックボックス</span><span class="sxs-lookup"><span data-stu-id="05aa9-202">Checkboxes</span></span>
* <span data-ttu-id="05aa9-203">ラジオ ボタン</span><span class="sxs-lookup"><span data-stu-id="05aa9-203">Radio Buttons</span></span>
* <span data-ttu-id="05aa9-204">切り替え</span><span class="sxs-lookup"><span data-stu-id="05aa9-204">Toggles</span></span>
* <span data-ttu-id="05aa9-205">テキスト領域</span><span class="sxs-lookup"><span data-stu-id="05aa9-205">Text Areas</span></span>
* <span data-ttu-id="05aa9-206">リンク</span><span class="sxs-lookup"><span data-stu-id="05aa9-206">Links</span></span>
* <span data-ttu-id="05aa9-207">タブ</span><span class="sxs-lookup"><span data-stu-id="05aa9-207">Tabs</span></span>
* <span data-ttu-id="05aa9-208">テーブル</span><span class="sxs-lookup"><span data-stu-id="05aa9-208">Tables</span></span>
* <span data-ttu-id="05aa9-209">アイコン</span><span class="sxs-lookup"><span data-stu-id="05aa9-209">Icons</span></span>
