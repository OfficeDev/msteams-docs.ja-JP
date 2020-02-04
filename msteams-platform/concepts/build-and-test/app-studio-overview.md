---
title: Microsoft Teams 用アプリ Studio の使用を開始する
description: アプリ Studio を使用して Microsoft Teams での高度なアプリの作成を始める
keywords: アプリ studio teams の概要
ms.date: 03/20/2019
ms.openlocfilehash: 9a88c6be552905a1dbd41d691c160a39f0123710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675004"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a><span data-ttu-id="32dfe-104">Microsoft Teams 用アプリ Studio を使用してアプリをすばやく開発する</span><span class="sxs-lookup"><span data-stu-id="32dfe-104">Quickly develop apps with App Studio for Microsoft Teams</span></span>

<span data-ttu-id="32dfe-105">アプリ Studio を使用すると、独自の Microsoft Teams アプリの作成や統合を簡単に行うことができます。これにより、世界中のチーム向けのカスタムアプリを開発するかどうか、アプリのマニフェストとパッケージの作成が合理化されます。カードエディターや応答制御ライブラリなどの便利なツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-105">App Studio makes it easy to start creating or integrating your own Microsoft Teams apps, whether you develop custom apps for your enterprise or SaaS applications for teams around the world by streamlining the creation of the manifest and package for your app and providing useful tools like the Card Editor and a React control library.</span></span>

## <a name="installing-app-studio"></a><span data-ttu-id="32dfe-106">アプリ Studio をインストールする</span><span class="sxs-lookup"><span data-stu-id="32dfe-106">Installing App Studio</span></span>

<span data-ttu-id="32dfe-107">App Studio は teams のアプリであり、Teams ストアで見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-107">App Studio is a Teams app which can be found in the Teams store.</span></span> <span data-ttu-id="32dfe-108">直接ダウンロードについては、次のリンクを参照してください。[アプリ Studio](https://aka.ms/InstallTeamsAppStudio) (アプリストアでアプリを検索することもできます)。</span><span class="sxs-lookup"><span data-stu-id="32dfe-108">Follow this link for direct download: [App Studio](https://aka.ms/InstallTeamsAppStudio) (you can also find the app in the app store).</span></span>

<span data-ttu-id="32dfe-109">ストアで、アプリ Studio を検索します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-109">In the store, search for App Studio.</span></span>

![App studio のエントリを格納する](~/assets/images/get-started/storeteamsappstudio.png)

<span data-ttu-id="32dfe-111">アプリ Studio タイルを選択して、[アプリのインストール] ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-111">Select the App Studio tile to open the app install page:</span></span>

![アプリ studio を構成する](~/assets/images/get-started/teamsappstudioconfiguration.png)

<span data-ttu-id="32dfe-113">[*インストール*] を選択します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-113">Select *install*.</span></span>

![app studio](~/assets/images/get-started/teamsappstudio.png)

<span data-ttu-id="32dfe-115">アプリ Studio で、[*マニフェストエディター* ] タブをクリックします。このタブでは、既存のアプリをインポートするか、新しいアプリを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-115">Once you are in App Studio, click on the *Manifest editor* tab where you can either import an existing app or create a new app.</span></span>

## <a name="app-studio-features"></a><span data-ttu-id="32dfe-116">アプリ Studio の機能</span><span class="sxs-lookup"><span data-stu-id="32dfe-116">App Studio Features</span></span>

### <a name="conversation"></a><span data-ttu-id="32dfe-117">スレッド</span><span class="sxs-lookup"><span data-stu-id="32dfe-117">Conversation</span></span>

<span data-ttu-id="32dfe-118">ここでは、アプリを自分に送信してテストしたときに、Teams で[作成するカード](#card-editor)の内容を確認できます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-118">This is where you can see what [cards you create in App Studio](#card-editor) look like in Teams when you test them by sending them to yourself.</span></span>

### <a name="manifest-editor"></a><span data-ttu-id="32dfe-119">マニフェストエディター</span><span class="sxs-lookup"><span data-stu-id="32dfe-119">Manifest Editor</span></span>

<span data-ttu-id="32dfe-120">前述したように、Microsoft Teams アプリパッケージの最も重要な部分は、manifest.xml ファイルです。</span><span class="sxs-lookup"><span data-stu-id="32dfe-120">As mentioned earlier, the most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="32dfe-121">このファイルは[Teams アプリスキーマ](~/resources/schema/manifest-schema.md)に準拠している必要があります。メタデータが含まれているので、チームはアプリを適切にユーザーに提供することができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-121">This file, which must conform to the [Teams App schema](~/resources/schema/manifest-schema.md), contains metadata which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="32dfe-122">アプリ Studio の [マニフェストエディター] タブを使用すると、マニフェストの作成が容易になり、アプリを説明したり、アイコンをアップロードしたり、アプリの機能を追加したり、.zip ファイルを作成したりすることができます。このファイルは、他のユーザーが使用するために、テストや配布のために Teams に簡単にアップロードできます</span><span class="sxs-lookup"><span data-stu-id="32dfe-122">The Manifest Editor tab in App Studio simplifies creating the manifest, allowing you to describe the app, upload your icons, add app capabilities, and produce a .zip file which can easily be uploaded into Teams for testing or distributed for others to use.</span></span> <span data-ttu-id="32dfe-123">アプリ Studio はアプリの機能コードを生成しないこと、またはアプリをホストすることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="32dfe-123">Note that App Studio does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="32dfe-124">アプリが正常にホストされ、アプリのアップロードプロセスのマニフェストに記載されている URL で実行されている必要があります。これにより、作業中のアプリになります。</span><span class="sxs-lookup"><span data-stu-id="32dfe-124">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

#### <a name="details"></a><span data-ttu-id="32dfe-125">詳細</span><span class="sxs-lookup"><span data-stu-id="32dfe-125">Details</span></span>

<span data-ttu-id="32dfe-126">マニフェストエディターの [詳細] セクションには、作成するアプリの概要が定義されています。</span><span class="sxs-lookup"><span data-stu-id="32dfe-126">The details section of the Manifest Editor defines the high-level description of the app you are making.</span></span> <span data-ttu-id="32dfe-127">これには、アプリの名前、説明、および視覚的なブランド化などが含まれます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-127">This includes things such as the app’s name, description, and visual branding.</span></span> <span data-ttu-id="32dfe-128">アプリの GUID を自動的に生成し、プライバシーに関する声明と使用条件の Url を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-128">You can automatically generate a GUID for your app and provide URLs for your privacy statement and terms of use.</span></span>

#### <a name="capabilities"></a><span data-ttu-id="32dfe-129">機能</span><span class="sxs-lookup"><span data-stu-id="32dfe-129">Capabilities</span></span>

<span data-ttu-id="32dfe-130">マニフェストエディターの [機能] セクションには、アプリの機能が定義されており、各機能の詳細が表示されています。</span><span class="sxs-lookup"><span data-stu-id="32dfe-130">The capabilities section of the Manifest Editor is where the app's capabilities are defined and where details of each of those capabilities are listed.</span></span>

##### <a name="tabs"></a><span data-ttu-id="32dfe-131">タブ</span><span class="sxs-lookup"><span data-stu-id="32dfe-131">Tabs</span></span>

* <span data-ttu-id="32dfe-132">**チームタブ**</span><span class="sxs-lookup"><span data-stu-id="32dfe-132">**Team Tabs.**</span></span> <span data-ttu-id="32dfe-133">チームタブはチャネルの一部として機能し、チームの情報やリソースにすばやくアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="32dfe-133">A team tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="32dfe-134">たとえば、チャネルの [プランナー] タブには、1つのプランが含まれています。Power BI タブは、特定のレポートにマップされます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-134">For example, the Planner tab for a channel contains a single plan; the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="32dfe-135">ユーザーは関連するコンテキストにドリルダウンすることはできますが、タブの外に移動することはできません。たとえば、Power bi タブでは、他の Power BI レポートへの移動を有効にすることはできませんが、メインの Power BI web サイトでレポートを起動する [ *web サイトに移動*] ボタンを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-135">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the *Go to website* button that launches the report in the main Power BI website.</span></span>

  <span data-ttu-id="32dfe-136">[チーム] タブでは、オプションを提示して情報を収集するための*構成 URL*を提供する必要があります。これにより、ユーザーはタブの内容と動作をカスタマイズできます。この iframed HTML ページは、ユーザーが最初にそのタブをチャネルに追加したときに表示されます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-136">For team tabs, you must provide a *Configuration URL* to present options and gather information so users can customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>

  <span data-ttu-id="32dfe-137">また、タブが読み込むまたはリンクする必要がある追加のドメインも指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32dfe-137">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="32dfe-138">**個人用タブ**</span><span class="sxs-lookup"><span data-stu-id="32dfe-138">**Personal Tabs.**</span></span> <span data-ttu-id="32dfe-139">このセクションでは、個人用アプリの操作で既定で表示されるタブのセットを定義できます (つまり、ユーザーがチームまたはチャネルのコンテキスト外でアプリを使用したときの操作)。</span><span class="sxs-lookup"><span data-stu-id="32dfe-139">This section lets you define a set of tabs that are presented by default in the personal app experience (i.e. the experience a user has with your app outside the context of a team or channel).</span></span> <span data-ttu-id="32dfe-140">このセクションでは、タブ名、一意の識別子、Teams に表示される UI をポイントする URL、および必要に応じて、ユーザーがブラウザーでタブを表示した場合に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-140">In this section, provide the tab name, a unique identifier, the URL that points to the UI to be displayed in Teams, and optionally, the URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="32dfe-141">Teams タブの場合と同様に、タブが読み込むまたはリンク先とするその他のドメインを指定します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-141">As with Teams tabs, provide any additional domains from which the tab expects to load from or link to.</span></span>

##### <a name="bots"></a><span data-ttu-id="32dfe-142">ボット</span><span class="sxs-lookup"><span data-stu-id="32dfe-142">Bots</span></span>

<span data-ttu-id="32dfe-143">このセクションでは、会話の[bot](~/bots/what-are-bots.md)をアプリに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-143">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="32dfe-144">Bot フレームワークに登録されている bot を既に登録している場合は、[*設定*] をクリックして bot の名前を入力し、BOT フレームワーク ID を指定して、bot が動作するスコープを定義することにより、その bot を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-144">If you already have a bot registered with Bot Framework, you can add that bot by clicking *Set Up* and supplying the bot’s name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

<span data-ttu-id="32dfe-145">Bot フレームワークでボットをまだ登録していない場合は、[*登録*] をクリックして新しい bot を作成します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-145">If you have not yet registered a bot with the Bot Framework, click *Register* to create a new one.</span></span> <span data-ttu-id="32dfe-146">Bot の登録が完了したら、マニフェストエディターのこのセクションに戻り、その名前と Bot フレームワーク ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-146">Once you’re done registering your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

<span data-ttu-id="32dfe-147">Bot の情報を提供すると、必要に応じて、ボットがユーザーに提案できるコマンドのリストを定義できるようになります。</span><span class="sxs-lookup"><span data-stu-id="32dfe-147">Once you have supplied your bot’s information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="32dfe-148">コマンドの名前、その構文と引数を示すコマンドの説明、およびこのコマンドが適用されるスコープ (複数可) を追加します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-148">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

<span data-ttu-id="32dfe-149">1つのスコープのみをサポートするように bot が定義されている場合、サポートされていないスコープに対して指定されたコマンドは無視されます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-149">Note that if you have defined your bot to only support one scope, commands specified for the unsupported scope will be ignored.</span></span> <span data-ttu-id="32dfe-150">Bot がサポートするスコープは、いつでも編集できます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-150">You can edit the scopes your bot supports at any time.</span></span>

##### <a name="connectors"></a><span data-ttu-id="32dfe-151">コネクタ</span><span class="sxs-lookup"><span data-stu-id="32dfe-151">Connectors</span></span>

<span data-ttu-id="32dfe-152">このセクションでは、アプリにコネクタを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-152">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="32dfe-153">Office 365 コネクタが既に登録されている場合は、[*設定*] を選択し、コネクタの名前と ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-153">If you already have registered an Office 365 connector, choose *Set up* and enter the name and ID of the connector.</span></span> <span data-ttu-id="32dfe-154">新しいコネクタを使用する場合は、[*登録*] をクリックして、ブラウザーのコネクタ開発者ダッシュボードに移動します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-154">If you want a new connector click *Register* to be taken to the Connector Developer Dashboard in your browser.</span></span>

##### <a name="messaging-extensions"></a><span data-ttu-id="32dfe-155">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="32dfe-155">Messaging Extensions</span></span>

<span data-ttu-id="32dfe-156">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)は、ユーザーが Microsoft Teams 内でアプリを使用できるようにするための強力な方法です。</span><span class="sxs-lookup"><span data-stu-id="32dfe-156">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="32dfe-157">ユーザーは、サービスからの情報を照会し、その情報をカード形式でチャネルまたはチャットの会話に直接投稿できます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-157">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

<span data-ttu-id="32dfe-158">メッセージング拡張機能は Bot フレームワークのボットによって処理されるため、構成された bot が動作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32dfe-158">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="32dfe-159">メッセージング拡張機能の電源をオンにしたいボットの名前とボットフレームワーク ID がある場合は、それを入力します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-159">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="32dfe-160">それ以外の場合は、[*登録*] をクリックして作成し、その後に情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-160">Otherwise, click *Register* to create one and enter the information afterward.</span></span> <span data-ttu-id="32dfe-161">メッセージング拡張機能の構成をユーザーが更新できるかどうかを選択します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-161">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

<span data-ttu-id="32dfe-162">基礎となる bot を構成したら、メッセージング拡張機能が受け入れることができるコマンドとパラメーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-162">Once you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

<span data-ttu-id="32dfe-163">各コマンドには、タイトルと ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="32dfe-163">Each command requires a title and an ID.</span></span> <span data-ttu-id="32dfe-164">コマンドには、必要に応じてユーザーの説明を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-164">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="32dfe-165">各コマンドは最大5つのパラメーターをサポートでき、それぞれに次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="32dfe-165">Each command can support up to five parameters, each of which requires:</span></span>

* <span data-ttu-id="32dfe-166">Teams クライアントに表示されるパラメーターの名前。ユーザー要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="32dfe-166">The name of the parameter as it appears in the Teams client and is included in the user request</span></span>
* <span data-ttu-id="32dfe-167">ユーザーフレンドリなタイトル</span><span class="sxs-lookup"><span data-stu-id="32dfe-167">A user-friendly title</span></span>
* <span data-ttu-id="32dfe-168">オプションの説明</span><span class="sxs-lookup"><span data-stu-id="32dfe-168">An optional description</span></span>

#### <a name="test-and-distribute"></a><span data-ttu-id="32dfe-169">テストと配布</span><span class="sxs-lookup"><span data-stu-id="32dfe-169">Test and Distribute</span></span>

<span data-ttu-id="32dfe-170">アプリケーションの定義が完了すると、[テストと配布] セクションを使用すると、アプリの定義を zip ファイルとしてエクスポートして、テスト用に Teams クライアントに共有してアップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-170">Once you have finished defining your application, the Test and Distribute section allows you export your app’s definition as a zip file which then can be shared and uploaded into the Teams client for testing.</span></span> <span data-ttu-id="32dfe-171">[エクスポート] をクリックすると、既定のダウンロードディレクトリに、 *.zip とし*て zip ファイルがダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-171">Clicking export downloads the zip file as *appname.zip* in your default download directory.</span></span>

### <a name="card-editor"></a><span data-ttu-id="32dfe-172">カードエディタ</span><span class="sxs-lookup"><span data-stu-id="32dfe-172">Card Editor</span></span>

<span data-ttu-id="32dfe-173">カードは、短いまたは関連する情報の断片のコンテナーです。</span><span class="sxs-lookup"><span data-stu-id="32dfe-173">A card is a container for short or related pieces of information.</span></span> <span data-ttu-id="32dfe-174">Microsoft Teams では、複数のプロパティと添付ファイルを持つことができるカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="32dfe-174">Microsoft Teams supports cards, which can have multiple properties and attachments.</span></span> <span data-ttu-id="32dfe-175">カードは、ボットおよびコネクタが操作可能な情報をユーザーに中継するための主要な手段です。</span><span class="sxs-lookup"><span data-stu-id="32dfe-175">Cards are a key way that bots and connectors relay actionable information to users.</span></span> 

<span data-ttu-id="32dfe-176">このプロセスを簡単に、エラーを発生させないようにするために、[カードエディター] タブを使用すると、フォームを使用して英雄カードやサムネイルカードを作成し、(ユーザーが表示するのと同じように) そのカードを確認してテストすることができます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-176">To make this process easier and less error-prone, the Card Editor tab lets you build Hero Cards or Thumbnail Cards using a form and verify and test the resulting card (exactly as a user would see it) via a bot.</span></span> <span data-ttu-id="32dfe-177">また、アプリのソースコードにコピー/貼り付けできるカードに対応する JSON、C#、または node.js コードを提供します。</span><span class="sxs-lookup"><span data-stu-id="32dfe-177">It also provides the corresponding JSON, C#, or Node.js code for the card that you can copy/paste into your app's source code.</span></span>

<span data-ttu-id="32dfe-178">Teams 内で確認するカードが既にある場合は、[*カード情報の追加*] の下の [json] タブにそのカードの json を貼り付けて、それを自分に送信して、チャットでどのように表示されるか確認できます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-178">If you already have a card that you would like to verify inside Teams, you can paste the JSON for that card into the JSON tab under *Add card info* and send it to yourself to see what it looks like in a chat.</span></span>

### <a name="react-control-library"></a><span data-ttu-id="32dfe-179">コントロールライブラリの反応</span><span class="sxs-lookup"><span data-stu-id="32dfe-179">React Control Library</span></span>

>[!Note]
> <span data-ttu-id="32dfe-180">今後、このような対処のためのコントロールライブラリは廃止されます。</span><span class="sxs-lookup"><span data-stu-id="32dfe-180">This React control library will be deprecated in the future.</span></span> <span data-ttu-id="32dfe-181">[FLUENT ui を代替とし](https://microsoft.github.io/fluent-ui-react/)て使用することを検討してください (以前の stardust)。</span><span class="sxs-lookup"><span data-stu-id="32dfe-181">Consider using the [Fluent-UI react controls as an alternative](https://microsoft.github.io/fluent-ui-react/) (formerly Stardust UI).</span></span>

<span data-ttu-id="32dfe-182">Teams のベストプラクティスに従うアプリを作成することは、Teams のクライアント環境にシームレスに適合するルックアンドフィールをアプリに提供する優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="32dfe-182">Creating an app that follows the Teams best practices is a great way to give your app a look and feel that fits seamlessly with the Teams client experience.</span></span> <span data-ttu-id="32dfe-183">このエンドを実現するには、使用する UI コントロールが重要です。</span><span class="sxs-lookup"><span data-stu-id="32dfe-183">The UI controls that you use are critical to achieving that end.</span></span> <span data-ttu-id="32dfe-184">一貫性のある UI を簡単に作成できるように、アプリ Studio には、Teams デザインの原則に従う UI コントロールのカテゴリがいくつか用意されています。</span><span class="sxs-lookup"><span data-stu-id="32dfe-184">To make it easier to create a consistent UI, App Studio provides several categories of UI controls which follow Teams design principles.</span></span>

<span data-ttu-id="32dfe-185">これらのコントロールの例と、対応する対処コンポーネントが提供され、アプリの作成に使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="32dfe-185">Examples of the controls and corresponding React components are provided and ready to use in building your app.</span></span>

#### <a name="controls"></a><span data-ttu-id="32dfe-186">Controls</span><span class="sxs-lookup"><span data-stu-id="32dfe-186">Controls</span></span>

<span data-ttu-id="32dfe-187">次のようなコントロールがあります。</span><span class="sxs-lookup"><span data-stu-id="32dfe-187">Controls include:</span></span>

* <span data-ttu-id="32dfe-188">ボタン</span><span class="sxs-lookup"><span data-stu-id="32dfe-188">Buttons</span></span>
* <span data-ttu-id="32dfe-189">ドロップ</span><span class="sxs-lookup"><span data-stu-id="32dfe-189">Dropdowns</span></span>
* <span data-ttu-id="32dfe-190">ックス</span><span class="sxs-lookup"><span data-stu-id="32dfe-190">Checkboxes</span></span>
* <span data-ttu-id="32dfe-191">ラジオボタン</span><span class="sxs-lookup"><span data-stu-id="32dfe-191">Radio Buttons</span></span>
* <span data-ttu-id="32dfe-192">切り替え</span><span class="sxs-lookup"><span data-stu-id="32dfe-192">Toggles</span></span>
* <span data-ttu-id="32dfe-193">テキスト領域</span><span class="sxs-lookup"><span data-stu-id="32dfe-193">Text Areas</span></span>
* <span data-ttu-id="32dfe-194">リンク</span><span class="sxs-lookup"><span data-stu-id="32dfe-194">Links</span></span>
* <span data-ttu-id="32dfe-195">タブ</span><span class="sxs-lookup"><span data-stu-id="32dfe-195">Tabs</span></span>
* <span data-ttu-id="32dfe-196">テーブル</span><span class="sxs-lookup"><span data-stu-id="32dfe-196">Tables</span></span>
* <span data-ttu-id="32dfe-197">アイコン</span><span class="sxs-lookup"><span data-stu-id="32dfe-197">Icons</span></span>
