---
title: Microsoft Teams 用にボットを作成する
author: clearab
description: Microsoft Teams 用にボットを作成する方法。
ms.topic: conceptual
localization_priority: Priority
ms.author: anclear
ms.openlocfilehash: 9e0bd603772cf4da8465a638c4a7f5b426a1fbfb
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675021"
---
# <a name="create-a-bot-for-microsoft-teams"></a><span data-ttu-id="a8795-103">Microsoft Teams 用にボットを作成する</span><span class="sxs-lookup"><span data-stu-id="a8795-103">Create a bot for Microsoft Teams</span></span>

<span data-ttu-id="a8795-104">会話ボットを作成するには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8795-104">You'll need to complete the following steps to create a conversational bot:</span></span>

1. <span data-ttu-id="a8795-105">開発環境を準備する。</span><span class="sxs-lookup"><span data-stu-id="a8795-105">Prepare your development environment.</span></span>
1. <span data-ttu-id="a8795-106">Web サービスを作成する。</span><span class="sxs-lookup"><span data-stu-id="a8795-106">Create your web service.</span></span>
1. <span data-ttu-id="a8795-107">Microsoft Bot Framework に Web サービスをボットとして 登録する。</span><span class="sxs-lookup"><span data-stu-id="a8795-107">Register your web service as a bot with Microsoft Bot Framework.</span></span>
1. <span data-ttu-id="a8795-108">アプリ マニフェストとアプリ パッケージを作成する。</span><span class="sxs-lookup"><span data-stu-id="a8795-108">Create your app manifest and your app package.</span></span>
1. <span data-ttu-id="a8795-109">Microsoft Teams にパッケージをアップロードする。</span><span class="sxs-lookup"><span data-stu-id="a8795-109">Upload your package to Microsoft Teams.</span></span>

<span data-ttu-id="a8795-110">Bot Framework に対する Web サービスの作成、Web サービスの登録、およびアプリ パッケージの作成はどの順番で行っても構いません。ただし、これらの 3 つの要素は互いに深く絡み合っているため、実行する順番に関わらず、1 つ実行するごとに Bot Framework に戻り、他 2 つを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8795-110">Creating your web service, registering your web service, and creating your app package, with the Bot Framework can be done in any order; however, because the three pieces are so intertwined, no matter in which order you do them, you'll need to return to update the others.</span></span> <span data-ttu-id="a8795-111">登録するには展開した Web サービスからのメッセージング エンドポイントが必要で、Web サービスでは登録時に作成した ID とパスワードが必要です。</span><span class="sxs-lookup"><span data-stu-id="a8795-111">Your registration needs the messaging endpoint from your deployed web service and your web service needs the ID and password created from your registration.</span></span> <span data-ttu-id="a8795-112">また、アプリ マニフェストでは、Teams を Web サービスに接続するために登録 ID が必要です。</span><span class="sxs-lookup"><span data-stu-id="a8795-112">Your app manifest also needs the registration ID to connect Teams to your web service.</span></span>

<span data-ttu-id="a8795-113">ボットの作成中は、アプリ マニフェストの変更と Web サービスへのコードの展開の間を頻繁に行き来することになります。</span><span class="sxs-lookup"><span data-stu-id="a8795-113">As you're building your bot, you'll regularly move between changing your app manifest and deploying code to your web service.</span></span> <span data-ttu-id="a8795-114">アプリ マニフェストで作業する際は、JSON ファイルを手動で変更することも、App Studio を使用して変更することもできるということを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="a8795-114">When working with the app manifest, keep in mind you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="a8795-115">いずれの場合も、マニフェスに変更を加えた際はアプリを Teams に再展開 (アップロード) する必要があります。ただし、変更を Web サービスに展開する場合は、これを行う必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a8795-115">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest; however, there's no need to do so when you deploy changes to your web service.</span></span>

<span data-ttu-id="a8795-116">Bot Framework の詳細については、「[Bot Framework のドキュメント](/azure/bot-service/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a8795-116">See the [Bot Framework Documentation](/azure/bot-service/) for additional information on the Bot Framework.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="a8795-117">Web サービスを作成する</span><span class="sxs-lookup"><span data-stu-id="a8795-117">Create your web service</span></span>

<span data-ttu-id="a8795-118">ボットで一番重要なのは、Web サービスです。</span><span class="sxs-lookup"><span data-stu-id="a8795-118">The heart of your bot is your web service.</span></span> <span data-ttu-id="a8795-119">すべての要求を受信する単一のルート (通常は `/api/messages`) が Web サービスにより定義されます。</span><span class="sxs-lookup"><span data-stu-id="a8795-119">It will define a single route, typically `/api/messages`, on which to receive all requests.</span></span> <span data-ttu-id="a8795-120">作成を開始する際に選ぶことができる選択肢がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="a8795-120">To get started, you have a few options to choose from:</span></span>

* <span data-ttu-id="a8795-121">[C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) または [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) のいずれかの Teams 会話ボット サンプルを使用して開始します。</span><span class="sxs-lookup"><span data-stu-id="a8795-121">Start with the Teams conversation bot sample in either [C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) or [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot).</span></span>
* <span data-ttu-id="a8795-122">JavaScript を使用している場合は、[Microsoft Teams 用 Yeoman ジェネレーター](https://github.com/OfficeDev/generator-teams)を使用して、Web サービスを含む、Teams アプリをスキャフォールドします。</span><span class="sxs-lookup"><span data-stu-id="a8795-122">If you're using JavaScript, use the [Yeoman Generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span> <span data-ttu-id="a8795-123">これは、会話ボット以外のコンポーネントも含まれる Team アプリを構築する場合に特に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a8795-123">This is particularly helpful when building a Teams app that contains more than just a conversational bot.</span></span>
* <span data-ttu-id="a8795-124">Web サービスを一から作成する。</span><span class="sxs-lookup"><span data-stu-id="a8795-124">Create your web service from scratch.</span></span> <span data-ttu-id="a8795-125">お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-125">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="a8795-126">Web サービスを Bot Framework に登録する</span><span class="sxs-lookup"><span data-stu-id="a8795-126">Register your web service with the Bot Framework</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8795-127">Web サービスを登録する際は、**表示名**を、アプリ マニフェストで使用した**短い名前**と必ず同じ名前にします。</span><span class="sxs-lookup"><span data-stu-id="a8795-127">When registering your web service, be sure to set the **Display name** to the same name you used for your **Short name** in your app manifest.</span></span> <span data-ttu-id="a8795-128">直接のアップロードまたは組織のアプリ カタログ経由でのアップロードのいずれかの方法でアプリを発行すると、ボットにより会話に送信されるメッセージでは、アプリの**短い名前**ではなく、登録時の**表示名**がボットにより使用されます。</span><span class="sxs-lookup"><span data-stu-id="a8795-128">When your app is distributed by either direct uploading or through an organization's app catalog, messages sent to a conversation by your bot will use the registration's **Display name** rather than the app's **Short name**.</span></span>

<span data-ttu-id="a8795-129">Web サービスを Bot Framework に登録することで、Teams クライアントと Web サービスの間に安全な通信チャネルが提供されます。</span><span class="sxs-lookup"><span data-stu-id="a8795-129">Registering your web service with the Bot Framework provides a secure communication channel between the Teams client and your web service.</span></span> <span data-ttu-id="a8795-130">Teams クライアントと Web サービスが直接通信することはありません。</span><span class="sxs-lookup"><span data-stu-id="a8795-130">The Teams client and your web service never communicate directly.</span></span> <span data-ttu-id="a8795-131">代わりに、メッセージは Bot Framework サービス経由でルーティングされます (Microsoft Teams では、このサービスの、Office 365 の基準に準拠する別のインスタンスが使用されます)。</span><span class="sxs-lookup"><span data-stu-id="a8795-131">Instead, messages are routed through the Bot Framework Service (Microsoft Teams uses a separate instance of this service that is compliant with Office 365 standards).</span></span>

<span data-ttu-id="a8795-132">Web サービスを Bot Framework に登録するときは、2 つの選択肢があります。</span><span class="sxs-lookup"><span data-stu-id="a8795-132">You have two options when registering your web service with the Bot Framework.</span></span> <span data-ttu-id="a8795-133">Azure サブスクリプションを使用せずに、[App Studio](#using-app-studio) または[従来のポータル](#in-the-legacy-portal)のいずれかを使用してボットを登録できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-133">You can use either [App Studio](#using-app-studio) or the [legacy portal](#in-the-legacy-portal) to register your bot without using an Azure subscription.</span></span> <span data-ttu-id="a8795-134">または、Azure サブスクリプションがすでにある (または取得するつもりの) 場合は、[Azure ポータル](#with-an-azure-subscription)を使用して Web サービスを登録できます。 </span><span class="sxs-lookup"><span data-stu-id="a8795-134">Or, if you already have an Azure subscription (or don't mind creating one), you can use [the Azure portal](#with-an-azure-subscription) to register your web service.</span></span>

### <a name="without-an-azure-subscription"></a><span data-ttu-id="a8795-135">Azure サブスクリプションがない場合</span><span class="sxs-lookup"><span data-stu-id="a8795-135">Without an Azure subscription</span></span>

<span data-ttu-id="a8795-136">ボットの登録を Azure で作成しない場合は、こちらのリンク (https://dev.botframework.com/bots/new) または App Studio のいずれかを使用する**必要があります**。</span><span class="sxs-lookup"><span data-stu-id="a8795-136">If you do not wish to create your bot registration in Azure, you **must** use either this link - https://dev.botframework.com/bots/new, or App Studio.</span></span> <span data-ttu-id="a8795-137">Bot Framework ポータルで [*ボットを作成*] ボタンをクリックすると Microsoft Azure にボット登録が作成され、Azure サブスクリプション情報の提供を求められます。</span><span class="sxs-lookup"><span data-stu-id="a8795-137">If you click on the *Create a bot* button in the Bot Framework portal, you will create your bot registration in Microsoft Azure, and will need to provide an Azure subscription.</span></span> <span data-ttu-id="a8795-138">登録の管理を行う場合、または登録作成後に登録を Azure サブスクリプションに移動する場合は、https://dev.botframework.com/bots にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="a8795-138">To manage your registration or migrate it to an Azure subscription after creation go to: https://dev.botframework.com/bots.</span></span>

<span data-ttu-id="a8795-139">Azure に登録されていない既存の Bot Framework 登録のプロパティを編集すると、[移行の状態] 列と、Microsoft Azure ポータルに移動するための [移行] ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a8795-139">When you edit the properties of an existing Bot Framework registration not registered in Azure, you'll see A "Migration status" column and a blue "Migrate" button that will take you to the Microsoft Azure portal.</span></span> <span data-ttu-id="a8795-140">意図する場合を除き、[移行] ボタンは選択しないでください。</span><span class="sxs-lookup"><span data-stu-id="a8795-140">Don't select the "Migrate" button unless that's what you want to do.</span></span> <span data-ttu-id="a8795-141">代わりに、ボットの [**名前**] を選択し、そのプロパティを編集できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-141">Instead, select the **name** of the bot and you can edit its properties:</span></span>

   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)

<span data-ttu-id="a8795-143">ボットを Azure で登録 (Azure ポータルでの登録作成または移行のいずれかの方法で) する**必要がある**シナリオ: </span><span class="sxs-lookup"><span data-stu-id="a8795-143">Scenarios when you **must** have your bot registration in Azure (either by creating it in the Azure portal or via migration):</span></span>

* <span data-ttu-id="a8795-144">Bot Framework の [OAuthPrompt](./authentication/auth-flow-bot.md) を認証に使用する場合。</span><span class="sxs-lookup"><span data-stu-id="a8795-144">You want to use the Bot Framework's [OAuthPrompt](./authentication/auth-flow-bot.md) for authentication.</span></span>
* <span data-ttu-id="a8795-145">Web チャット、Direct Line、または Skype などの追加のチャネルを有効にする場合。</span><span class="sxs-lookup"><span data-stu-id="a8795-145">You want to enable additional channels like Web Chat, Direct Line, or Skype.</span></span>

#### <a name="using-app-studio"></a><span data-ttu-id="a8795-146">App Studio を使用する場合</span><span class="sxs-lookup"><span data-stu-id="a8795-146">Using App Studio</span></span>

<span data-ttu-id="a8795-147">*App Studio* は Teams アプリの作成に役立つ Teams アプリで、これを使用して Web サービスをボットとして登録したり、アプリ マニフェストを作成したり、アプリ パッケージを作成したりできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-147">*App Studio* is a Teams app that helps you build Teams apps, including registering your web service as a bot, creating an app manifest, and your app package.</span></span> <span data-ttu-id="a8795-148">React 制御ライブラリとカード用の構成可能なサンプルも含まれています。</span><span class="sxs-lookup"><span data-stu-id="a8795-148">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="a8795-149">「[Teams App Studio を使う](../../concepts/build-and-test/app-studio-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a8795-149">See [Getting started with Teams App Studio](../../concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="a8795-150">繰り返しますが、App Studio を使用して Web サービスを登録する場合は、https://dev.botframework.com/bots にアクセスして登録を管理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8795-150">Remember, if you use App Studio to register your web service you'll need to go to https://dev.botframework.com/bots to manage your registration.</span></span> <span data-ttu-id="a8795-151">一部の設定 (メッセージング エンドポイントなど) は App Studio でも更新できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-151">Some settings (like your messaging endpoint) can be updated in App Studio as well.</span></span>

#### <a name="in-the-legacy-portal"></a><span data-ttu-id="a8795-152">従来のポータルを使用する場合</span><span class="sxs-lookup"><span data-stu-id="a8795-152">In the legacy portal</span></span>

<span data-ttu-id="a8795-153">ボットの登録を、こちらのリンク (https://dev.botframework.com/bots/new) を使用して作成します。</span><span class="sxs-lookup"><span data-stu-id="a8795-153">Create your bot registration using this link: https://dev.botframework.com/bots/new.</span></span> <span data-ttu-id="a8795-154">**ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。**</span><span class="sxs-lookup"><span data-stu-id="a8795-154">**Be sure to add Microsoft Teams as a channel from the featured channels list after creating your bot.**</span></span> <span data-ttu-id="a8795-155">アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-155">Feel free to re-use any Microsoft App ID you generated if you've already created your app package/manifest.</span></span>

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

### <a name="with-an-azure-subscription"></a><span data-ttu-id="a8795-157">Azure サブスクリプションがある場合</span><span class="sxs-lookup"><span data-stu-id="a8795-157">With an Azure subscription</span></span>

<span data-ttu-id="a8795-158">Web サービスは、Azure ポータルでボット チャネル登録リソースを作成する方法でも登録できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-158">You can also register your web service by creating a Bot Channels Registration resource in the Azure portal.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="a8795-159">[Bot Framework ポータル](https://dev.botframework.com)は、Microsoft Azure でのボットの登録に最適化されています。</span><span class="sxs-lookup"><span data-stu-id="a8795-159">The [Bot Framework portal](https://dev.botframework.com) is optimized for registering bots in Microsoft Azure.</span></span> <span data-ttu-id="a8795-160">留意事項がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="a8795-160">Here are some things to know:</span></span>

* <span data-ttu-id="a8795-161">Azure で登録したボット用の Microsoft Teams チャネルは**無料**です。</span><span class="sxs-lookup"><span data-stu-id="a8795-161">The Microsoft Teams channel for bots registered on Azure is **free**.</span></span> <span data-ttu-id="a8795-162">Teams チャネル経由で送信されるメッセージは、ボットの消費メッセージとしてはカウントされません。</span><span class="sxs-lookup"><span data-stu-id="a8795-162">Messages sent over the Teams channel will NOT count towards the consumed messages for the bot.</span></span>
* <span data-ttu-id="a8795-163">Microsoft Azure を使用してボットを登録する場合、ボット コードは Microsoft Azure で*ホスト*される必要はあります。</span><span class="sxs-lookup"><span data-stu-id="a8795-163">If you register your bot using Microsoft Azure, your bot code doesn't need to be *hosted* on Microsoft Azure.</span></span>
* <span data-ttu-id="a8795-164">Microsoft Azure ポータルを使用してボットを登録する場合は、Microsoft Azure アカウントを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8795-164">If you do register a bot using Microsoft Azure portal, you must have a Microsoft Azure account.</span></span> <span data-ttu-id="a8795-165">このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-165">You can [create one for free](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="a8795-166">Azure アカウントを作成するときは、ユーザーの ID を確認するためにユーザーはクレジット カードを提供する必要がありますが、課金はされません。Microsoft Teams を使用してのボットの作成と使用は常に無料です。</span><span class="sxs-lookup"><span data-stu-id="a8795-166">To verify your identity when you create an Azure account, you must provide a credit card, but it won't be charged; it's always free to create and use bots with Microsoft Teams.</span></span>

## <a name="create-your-app-manifest-and-package"></a><span data-ttu-id="a8795-167">独自のアプリ マニフェストとアプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="a8795-167">Create your app manifest and package</span></span>

<span data-ttu-id="a8795-168">[アプリ マニフェスト](~/resources/schema/manifest-schema.md)により、アプリのメタデータ、アプリが使用する拡張点、これらの拡張点の接続先の Web サービスへのポインターが定義されます。</span><span class="sxs-lookup"><span data-stu-id="a8795-168">Your [app manifest](~/resources/schema/manifest-schema.md) defines the metadata for your app, the extension points your app is using, and pointers to the web services those extension points connect to.</span></span> <span data-ttu-id="a8795-169">アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-169">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="add-using-app-studio"></a><span data-ttu-id="a8795-170">App Studio を使用して追加する</span><span class="sxs-lookup"><span data-stu-id="a8795-170">Add using App Studio</span></span>

1. <span data-ttu-id="a8795-171">Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー (**...**) から App Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="a8795-171">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="a8795-172">App Studio がまだインストールされていない場合は、それを検索してインストールできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-172">If App Studio isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="a8795-173">On the [**Manifest editor**] (マニフェスト エディター) タブで、[**Create a new app**] (新しいアプリの作成) を選択します (または、ボットを既存のアプリに追加する場合は、アプリ パッケージをインポートできます)。</span><span class="sxs-lookup"><span data-stu-id="a8795-173">On the **Manifest editor** tab select **Create a new app** (or if you're adding a bot to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="a8795-174">アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="a8795-174">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="a8795-175">[**Bots**] (ボット) タブで、[**セットアップ**] (セットアップ) ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="a8795-175">On the **Bots** tab select the **Setup** button.</span></span>
5. <span data-ttu-id="a8795-176">新しい Web サービス登録を作成することも ([**New bot**] (新しいボット))、既に登録したものがある場合は、[**Existing bot**] (既存のボット) を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-176">You can either create a new web service registration (**New bot**), or if you've already registered one, select **Existing bot**.</span></span>
6. <span data-ttu-id="a8795-177">ボットで必要な機能とスコープを選択します。</span><span class="sxs-lookup"><span data-stu-id="a8795-177">Select the capabilities and scopes your bot will need.</span></span>
7. <span data-ttu-id="a8795-178">必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。</span><span class="sxs-lookup"><span data-stu-id="a8795-178">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="a8795-179">だいたい次のようになります: `https://someplace.com/api/messages`</span><span class="sxs-lookup"><span data-stu-id="a8795-179">It should look something like `https://someplace.com/api/messages`.</span></span>
8. <span data-ttu-id="a8795-180">必要に応じて、[ボット コマンド](~/bots/how-to/create-a-bot-commands-menu.md)を追加します。</span><span class="sxs-lookup"><span data-stu-id="a8795-180">Optionally, add [bot commands](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>
9. <span data-ttu-id="a8795-181">必要な場合、完成したアプリ パッケージを [**Test and distribute**] (テストと発行) タブからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-181">Optionally, you can download your completed app package from the **Test and distribute** tab.</span></span>

### <a name="create-it-manually"></a><span data-ttu-id="a8795-182">手動で作成する</span><span class="sxs-lookup"><span data-stu-id="a8795-182">Create it manually</span></span>

<span data-ttu-id="a8795-183">メッセージング拡張機能やタブの場合と同様、ボットを定義するには [app-manifest](~/resources/schema/manifest-schema.md) を更新します。</span><span class="sxs-lookup"><span data-stu-id="a8795-183">As with messaging extensions and tabs, you update the [app-manifest](~/resources/schema/manifest-schema.md) to define your bot.</span></span> <span data-ttu-id="a8795-184">`bots` プロパティを使用して、新しいトップレベル の JSON 構造をアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="a8795-184">Add new top-level JSON structure in your app manifest with the `bots` property.</span></span>

|<span data-ttu-id="a8795-185">名前</span><span class="sxs-lookup"><span data-stu-id="a8795-185">Name</span></span>| <span data-ttu-id="a8795-186">型</span><span class="sxs-lookup"><span data-stu-id="a8795-186">Type</span></span>| <span data-ttu-id="a8795-187">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="a8795-187">Maximum size</span></span> | <span data-ttu-id="a8795-188">必須</span><span class="sxs-lookup"><span data-stu-id="a8795-188">Required</span></span> | <span data-ttu-id="a8795-189">説明</span><span class="sxs-lookup"><span data-stu-id="a8795-189">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a8795-190">String</span><span class="sxs-lookup"><span data-stu-id="a8795-190">String</span></span>|<span data-ttu-id="a8795-191">64 文字</span><span class="sxs-lookup"><span data-stu-id="a8795-191">64 characters</span></span>|<span data-ttu-id="a8795-192">✔</span><span class="sxs-lookup"><span data-stu-id="a8795-192">✔</span></span>|<span data-ttu-id="a8795-193">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="a8795-193">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="a8795-194">これは、全体的なアプリ ID と同じにすることができます。</span><span class="sxs-lookup"><span data-stu-id="a8795-194">This may well be the same as the overall app ID.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="a8795-195">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8795-195">Boolean</span></span>|||<span data-ttu-id="a8795-196">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="a8795-196">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="a8795-197">既定値: `false`。</span><span class="sxs-lookup"><span data-stu-id="a8795-197">Default: `false`.</span></span>|
|`isNotificationOnly`|<span data-ttu-id="a8795-198">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8795-198">Boolean</span></span>|||<span data-ttu-id="a8795-199">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="a8795-199">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="a8795-200">既定値: `false`。</span><span class="sxs-lookup"><span data-stu-id="a8795-200">Default: `false`.</span></span>|
|`supportsFiles`|<span data-ttu-id="a8795-201">Boolean</span><span class="sxs-lookup"><span data-stu-id="a8795-201">Boolean</span></span>|||<span data-ttu-id="a8795-202">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="a8795-202">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="a8795-203">既定値: `false`。</span><span class="sxs-lookup"><span data-stu-id="a8795-203">Default: `false`.</span></span>|
|`scopes`|<span data-ttu-id="a8795-204">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="a8795-204">Array of enum</span></span>|<span data-ttu-id="a8795-205">3</span><span class="sxs-lookup"><span data-stu-id="a8795-205">3</span></span>|<span data-ttu-id="a8795-206">✔</span><span class="sxs-lookup"><span data-stu-id="a8795-206">✔</span></span>|<span data-ttu-id="a8795-207">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="a8795-207">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a8795-208">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="a8795-208">These options are non-exclusive.</span></span>|

<span data-ttu-id="a8795-209">必要に応じて、ボットがユーザーに勧めることが可能なコマンド リスト (1 つまたは複数) を定義できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-209">Optionally, you can define one or more lists of commands that your bot can recommend to users.</span></span> <span data-ttu-id="a8795-210">オブジェクトは配列で (要素は最大で 2 つ)、`object` タイプのすべての要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a8795-210">The object is an array (maximum of 2 elements) with all elements of type `object`.</span></span> <span data-ttu-id="a8795-211">ボットがサポートする各スコープについて、個別のコマンド リストを定義する必要があります。 </span><span class="sxs-lookup"><span data-stu-id="a8795-211">You must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="a8795-212">\*\* 詳細については、「[ボット メニュー](./create-a-bot-commands-menu.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a8795-212">*See* [Bot menus](./create-a-bot-commands-menu.md), for more information.</span></span>

|<span data-ttu-id="a8795-213">名前</span><span class="sxs-lookup"><span data-stu-id="a8795-213">Name</span></span>| <span data-ttu-id="a8795-214">型</span><span class="sxs-lookup"><span data-stu-id="a8795-214">Type</span></span>| <span data-ttu-id="a8795-215">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="a8795-215">Maximum size</span></span> | <span data-ttu-id="a8795-216">必須</span><span class="sxs-lookup"><span data-stu-id="a8795-216">Required</span></span> | <span data-ttu-id="a8795-217">説明</span><span class="sxs-lookup"><span data-stu-id="a8795-217">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="a8795-218">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="a8795-218">array of enum</span></span>|<span data-ttu-id="a8795-219">3</span><span class="sxs-lookup"><span data-stu-id="a8795-219">3</span></span>|<span data-ttu-id="a8795-220">✔</span><span class="sxs-lookup"><span data-stu-id="a8795-220">✔</span></span>|<span data-ttu-id="a8795-221">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="a8795-221">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="a8795-222">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="a8795-222">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="a8795-223">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="a8795-223">array of objects</span></span>|<span data-ttu-id="a8795-224">10</span><span class="sxs-lookup"><span data-stu-id="a8795-224">10</span></span>|<span data-ttu-id="a8795-225">✔</span><span class="sxs-lookup"><span data-stu-id="a8795-225">✔</span></span>|<span data-ttu-id="a8795-226">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="a8795-226">An array of commands the bot supports:</span></span><br><span data-ttu-id="a8795-227">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="a8795-227">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="a8795-228">`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)</span><span class="sxs-lookup"><span data-stu-id="a8795-228">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

#### <a name="simple-manifest-example"></a><span data-ttu-id="a8795-229">マニフェストの簡単な例</span><span class="sxs-lookup"><span data-stu-id="a8795-229">Simple manifest example</span></span>

<span data-ttu-id="a8795-230">次の例は単純なボット オブジェクトで、2 つのコマンド リストが定義されています。</span><span class="sxs-lookup"><span data-stu-id="a8795-230">The example below is a simple bot object, with two command lists defined.</span></span> <span data-ttu-id="a8795-231">これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。</span><span class="sxs-lookup"><span data-stu-id="a8795-231">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span>

```json
...
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
...
```

#### <a name="create-your-app-package-manually"></a><span data-ttu-id="a8795-232">アプリ パッケージを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="a8795-232">Create your app package manually</span></span>

<span data-ttu-id="a8795-233">アプリ パッケージを作成するには、アプリ マニフェストと (必要に応じて) アプリ アイコンを .zip アーカイブ ファイルに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a8795-233">To create an app package, you need to add your app manifest and (optionally) your app icons to a .zip archive file.</span></span> <span data-ttu-id="a8795-234">詳細については、「[アプリ パッケージを作成する](~/concepts/build-and-test/apps-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a8795-234">See [Create your app package](~/concepts/build-and-test/apps-package.md) for complete details.</span></span> <span data-ttu-id="a8795-235">.zip アーカイブには必要なファイルのみを含めるようにし、アーカイブ内にフォルダー構造が何もないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="a8795-235">Make sure your .zip archive contains only the necessary files, and has no additional folder structure inside of it.</span></span>

## <a name="upload-your-package-to-microsoft-teams"></a><span data-ttu-id="a8795-236">Microsoft Teams にアプリ パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="a8795-236">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="a8795-237">App Studio を使用した場合は、[**Manifest editor**] (マニフェスト エディター) の [**Test and distribute**] (テストと発行) タブからアプリをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-237">If you've been using App Studio, you can install your app from the **Test and distribute** tab of the **Manifest editor**.</span></span> <span data-ttu-id="a8795-238">また、左側のオーバーフロー メニュー (`...`) をクリックし、[**その他のアプリ**] をクリックし、[**カスタム アプリをアップロード**] リンクをクリックする方法でもアプリ パッケージをインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="a8795-238">Alternatively, you can install your app package by clicking the `...` overflow menu from the left navigation rail, clicking **More apps**, then the **Upload a custom app** link.</span></span> <span data-ttu-id="a8795-239">アプリ マニフェストまたはアプリ パッケージを App Studio にインポートして、アップロードする前に追加の更新を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="a8795-239">You can also import an app manifest or app package into App Studio to make additional updates before uploading.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8795-240">次の手順</span><span class="sxs-lookup"><span data-stu-id="a8795-240">Next steps</span></span>

* [<span data-ttu-id="a8795-241">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="a8795-241">Bot conversation basics</span></span>](./conversations/conversation-basics.md)
* [<span data-ttu-id="a8795-242">会話イベントにサブスクライブする</span><span class="sxs-lookup"><span data-stu-id="a8795-242">Subscribe to conversation events</span></span>](./conversations/subscribe-to-conversation-events.md)
