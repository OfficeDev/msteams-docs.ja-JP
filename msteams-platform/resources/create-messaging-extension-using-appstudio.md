---
title: App Studio を使用してメッセージングの拡張機能を作成する
author: clearab
description: App Studio を使用してメッセージング拡張機能Microsoft Teams作成する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 10de4c6f9e7b81e1edc47622cb5c0c814d2eb3a7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019742"
---
# <a name="create-a-messaging-extension-using-app-studio"></a><span data-ttu-id="bae3a-103">App Studio を使用してメッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-103">Create a messaging extension using App Studio</span></span>

> [!TIP]
> <span data-ttu-id="bae3a-104">早く始める方法をお探しですか?</span><span class="sxs-lookup"><span data-stu-id="bae3a-104">Looking for a faster way to get started?</span></span> <span data-ttu-id="bae3a-105">ユーザー設定を[使用してメッセージング](../build-your-first-app/build-messaging-extension.md)拡張機能をMicrosoft Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="bae3a-105">Create a [messaging extension](../build-your-first-app/build-messaging-extension.md) using the Microsoft Teams Toolkit.</span></span>

<span data-ttu-id="bae3a-106">高レベルでは、メッセージング拡張機能を作成するには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-106">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="bae3a-107">開発環境を準備する</span><span class="sxs-lookup"><span data-stu-id="bae3a-107">Prepare your development environment</span></span>
2. <span data-ttu-id="bae3a-108">Web サービスを作成して展開する (開発中は ngrok のようなトンネリング サービスを使用してローカルで実行する)</span><span class="sxs-lookup"><span data-stu-id="bae3a-108">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="bae3a-109">Web サービスを Bot Framework に登録する</span><span class="sxs-lookup"><span data-stu-id="bae3a-109">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="bae3a-110">アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-110">Create your app package</span></span>
5. <span data-ttu-id="bae3a-111">Microsoft Teams にアプリ パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="bae3a-111">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="bae3a-112">Web サービスの作成、アプリ パッケージの作成、ボット フレームワークへの Web サービスの登録は、任意の順序で実行できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-112">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="bae3a-113">これらの 3 つのピースは非常に相互に絡み合うので、どの順序で行っても、他の部分を更新するには戻る必要があります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-113">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="bae3a-114">登録には、展開された Web サービスからのメッセージング エンドポイントが必要であり、Web サービスには登録から作成された ID とパスワードが必要です。</span><span class="sxs-lookup"><span data-stu-id="bae3a-114">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="bae3a-115">アプリ マニフェストには、Web サービスに接続するための id Teamsも必要です。</span><span class="sxs-lookup"><span data-stu-id="bae3a-115">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="bae3a-116">メッセージング拡張機能を構築する場合、アプリ マニフェストの変更と Web サービスへのコードの展開の間を定期的に移動します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-116">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="bae3a-117">アプリ マニフェストを操作する場合は、JSON ファイルを手動で操作するか、App Studio で変更を加えることができます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-117">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="bae3a-118">いずれにしろ、マニフェストに変更を加える場合は Teams でアプリを再展開 (アップロード) する必要がありますが、Web サービスに変更を展開する場合は、アプリを再展開する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="bae3a-118">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="bae3a-119">Web サービスを作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-119">Create your web service</span></span>

<span data-ttu-id="bae3a-120">メッセージング拡張機能の中心は、Web サービスです。</span><span class="sxs-lookup"><span data-stu-id="bae3a-120">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="bae3a-121">通常、すべての要求を受信する単一 `/api/messages` のルートを定義します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-121">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="bae3a-122">最初から始める場合は、いくつかのオプションから選択できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-122">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="bae3a-123">Web サービスの [作成を](#learn-more) ガイドするクイック スタート チュートリアルのいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-123">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="bae3a-124">Bot Framework サンプル リポジトリで使用できるメッセージング拡張機能のサンプルのいずれかを [選択します](https://github.com/Microsoft/BotBuilder-Samples) 。</span><span class="sxs-lookup"><span data-stu-id="bae3a-124">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="bae3a-125">JavaScript を使用している場合は[、Yeoman](https://github.com/OfficeDev/generator-teams)ジェネレーターを使用して、Microsoft Teamsサービスを含む Teamsアプリをスキャフォールディングします。</span><span class="sxs-lookup"><span data-stu-id="bae3a-125">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="bae3a-126">Web サービスを一から作成する。</span><span class="sxs-lookup"><span data-stu-id="bae3a-126">Create your web service from scratch.</span></span> <span data-ttu-id="bae3a-127">お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-127">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="bae3a-128">Web サービスを Bot Framework に登録する</span><span class="sxs-lookup"><span data-stu-id="bae3a-128">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="bae3a-129">メッセージング拡張機能は、ボット フレームワークのメッセージング スキーマとセキュリティで保護された通信プロトコルを利用します。まだ Web サービスを持ってない場合は、ボット フレームワークに Web サービスを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-129">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="bae3a-130">Microsoft App Id (これを Teams の内部からボット ID と参照し、作業している可能性のある他のアプリ ID から識別します)、ボット フレームワークを使用した登録のメッセージング エンドポイントがメッセージング拡張機能で使用され、要求を受信して応答します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-130">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="bae3a-131">既存の登録を使用している場合は、登録チャネルを有効[Microsoft Teamsしてください](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="bae3a-131">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="bae3a-132">クイック スタートの 1 つを実行するか、使用可能なサンプルの 1 つから開始する場合は、Web サービスの登録に関するガイドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-132">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="bae3a-133">サービスを手動で登録する場合は、3 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-133">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="bae3a-134">Azure サブスクリプションを使用せずに登録する場合は、ボット フレームワークによって提供される簡略化された OAuth 認証フローを利用できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-134">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="bae3a-135">作成後に登録を Azure に移行できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-135">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="bae3a-136">Azure サブスクリプションがある場合 (または新しいサブスクリプションを作成する場合) は、Azure Portal を使用して Web サービスを手動で登録できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-136">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="bae3a-137">"ボット チャネル登録" リソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-137">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="bae3a-138">無料の価格レベルを選択できます。ユーザーからのメッセージMicrosoft Teams、1 か月あたりの許容メッセージの総数にはカウントされません。</span><span class="sxs-lookup"><span data-stu-id="bae3a-138">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="bae3a-139">Azure サブスクリプションを使用しない場合は、従来の登録ポータル [を使用できます](https://dev.botframework.com/bots/new)。</span><span class="sxs-lookup"><span data-stu-id="bae3a-139">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="bae3a-140">App Studio は、Web サービス (ボット) の登録にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-140">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="bae3a-141">App Studio を介して登録された Web サービスは Azure に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="bae3a-141">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="bae3a-142">レガシ ポータル [を使用して](https://dev.botframework.com/bots) 、登録を表示、管理、および移行できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-142">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="bae3a-143">アプリ マニフェストを作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-143">Create your app manifest</span></span>

<span data-ttu-id="bae3a-144">アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-144">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="bae3a-145">App Studio を使用してアプリ マニフェストを作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-145">Create your app manifest using App Studio</span></span>

<span data-ttu-id="bae3a-146">アプリ マニフェストの作成に役立つアプリ Microsoft Teams App Studio アプリを使用できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-146">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="bae3a-147">Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー (**...**) から App Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-147">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="bae3a-148">まだインストールされていない場合は、検索してインストールできます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-148">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="bae3a-149">[マニフェスト エディター **] タブで\*\*\*\*、[新** しいアプリの作成] を選択します (または、既存のアプリにメッセージング拡張機能を追加する場合は、アプリ パッケージをインポートできます)</span><span class="sxs-lookup"><span data-stu-id="bae3a-149">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="bae3a-150">アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="bae3a-150">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="bae3a-151">[メッセージング拡張機能 **] タブで、[** セットアップ] ボタン **をクリック** します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-151">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="bae3a-152">メッセージング拡張機能を使用する新しい Web サービス (ボット) を作成するか、ここで既に 1 つの select/add を登録している場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-152">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="bae3a-153">必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。</span><span class="sxs-lookup"><span data-stu-id="bae3a-153">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="bae3a-154">だいたい次のようになります: `https://someplace.com/api/messages`</span><span class="sxs-lookup"><span data-stu-id="bae3a-154">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="bae3a-155">[ **コマンド]** セクションの **[追加] ボタン** では、メッセージング拡張機能にコマンドを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-155">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="bae3a-156">コマンドの追加 [の詳細については](#learn-more) 、「詳細」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bae3a-156">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="bae3a-157">メッセージング拡張機能には最大 10 のコマンドを定義できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-157">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="bae3a-158">[ **メッセージ ハンドラー] セクション** では、メッセージングがトリガーするドメインを追加できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-158">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="bae3a-159">詳細 [については、「リンクの分岐を](~/messaging-extensions/how-to/link-unfurling.md) 解除する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bae3a-159">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="bae3a-160">[**完了] = [テスト>** 配布] タブから、アプリ パッケージ (アプリ マニフェストとアプリ アイコンを含む) をダウンロードするか、パッケージ **をインストールできます**。</span><span class="sxs-lookup"><span data-stu-id="bae3a-160">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="bae3a-161">アプリ マニフェストを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-161">Create your app manifest manually</span></span>

<span data-ttu-id="bae3a-162">ボットとタブと同様に、アプリのアプリ[](~/resources/schema/manifest-schema.md#composeextensions)マニフェストを更新して、メッセージング拡張機能のプロパティを含めます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-162">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="bae3a-163">これらのプロパティは、メッセージング拡張機能がクライアントでどのように表示され、動作Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="bae3a-163">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="bae3a-164">メッセージング拡張機能は、マニフェストの v1.0 からサポートされています。</span><span class="sxs-lookup"><span data-stu-id="bae3a-164">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="bae3a-165">メッセージング拡張機能の宣言</span><span class="sxs-lookup"><span data-stu-id="bae3a-165">Declare your messaging extension</span></span>

<span data-ttu-id="bae3a-166">メッセージング拡張機能を追加するには、アプリ マニフェストに新しいトップ レベルの JSON 構造をプロパティと一緒に含 `composeExtensions` めます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-166">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="bae3a-167">アプリ用に 1 つのメッセージング拡張機能を作成し、最大 10 のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="bae3a-167">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="bae3a-168">マニフェストは、メッセージング拡張機能を次のように参照します `composeExtensions` 。</span><span class="sxs-lookup"><span data-stu-id="bae3a-168">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="bae3a-169">これは、下位互換性を維持するための方法です。</span><span class="sxs-lookup"><span data-stu-id="bae3a-169">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="bae3a-170">拡張定義は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="bae3a-170">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="bae3a-171">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="bae3a-171">Property name</span></span> | <span data-ttu-id="bae3a-172">用途</span><span class="sxs-lookup"><span data-stu-id="bae3a-172">Purpose</span></span> | <span data-ttu-id="bae3a-173">必須</span><span class="sxs-lookup"><span data-stu-id="bae3a-173">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="bae3a-174">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="bae3a-174">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="bae3a-175">通常、これはアプリ全体の ID と同Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-175">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="bae3a-176">はい</span><span class="sxs-lookup"><span data-stu-id="bae3a-176">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="bae3a-177">メニュー **設定** を有効にします。</span><span class="sxs-lookup"><span data-stu-id="bae3a-177">Enables **Settings** menu item.</span></span> | <span data-ttu-id="bae3a-178">いいえ</span><span class="sxs-lookup"><span data-stu-id="bae3a-178">No</span></span> |
| `commands` | <span data-ttu-id="bae3a-179">このメッセージング拡張機能がサポートするコマンドの配列。</span><span class="sxs-lookup"><span data-stu-id="bae3a-179">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="bae3a-180">コマンドは 10 に制限されています。</span><span class="sxs-lookup"><span data-stu-id="bae3a-180">You are limited to 10 commands.</span></span> | <span data-ttu-id="bae3a-181">はい</span><span class="sxs-lookup"><span data-stu-id="bae3a-181">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="bae3a-182">コマンドの定義</span><span class="sxs-lookup"><span data-stu-id="bae3a-182">Define your commands</span></span>

<span data-ttu-id="bae3a-183">メッセージング拡張機能は、ユーザーがメッセージング拡張機能をトリガーできる場所と操作の種類を定義する 1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-183">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="bae3a-184">メッセージング [拡張機能コマンドの](#learn-more) 詳細については、「詳細」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bae3a-184">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="bae3a-185">マニフェストの簡単な例</span><span class="sxs-lookup"><span data-stu-id="bae3a-185">Simple manifest example</span></span>

<span data-ttu-id="bae3a-186">次の例は、検索コマンドを使用したアプリ マニフェスト内の単純なメッセージング拡張機能オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="bae3a-186">The following example is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="bae3a-187">これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。</span><span class="sxs-lookup"><span data-stu-id="bae3a-187">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="bae3a-188">完全な [例については、「アプリ マニフェスト スキーマ](~/resources/schema/manifest-schema.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bae3a-188">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="bae3a-189">アプリ マニフェストの完全な例</span><span class="sxs-lookup"><span data-stu-id="bae3a-189">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="bae3a-190">呼び出しメッセージ ハンドラーを追加する</span><span class="sxs-lookup"><span data-stu-id="bae3a-190">Add your invoke message handlers</span></span>

<span data-ttu-id="bae3a-191">ユーザーがメッセージング拡張機能をトリガーする場合は、最初の呼び出しメッセージを処理し、ユーザーから情報を収集し、その情報を処理し、適切に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-191">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="bae3a-192">これを行うには、まずメッセージング拡張機能に追加するコマンドの種類を決定し、アクション コマンドを追加するか、検索コマンド[](~/messaging-extensions/how-to/action-commands/define-action-command.md)を[追加する必要があります](~/messaging-extensions/how-to/search-commands/define-search-command.md)。</span><span class="sxs-lookup"><span data-stu-id="bae3a-192">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="bae3a-193">会議でのメッセージングTeams拡張機能</span><span class="sxs-lookup"><span data-stu-id="bae3a-193">Messaging extensions in Teams meetings</span></span>

> [!NOTE]
> <span data-ttu-id="bae3a-194">会議またはグループ チャットに名簿にユーザーがフェデレーションされている場合、Teams開催者を含むすべてのユーザーのメッセージング拡張機能へのアクセスが抑制されます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-194">If a meeting or group chat has federated users in the roster, Teams suppresses access to messaging extensions for all users, including the organizer.</span></span>

<span data-ttu-id="bae3a-195">会議が開始すると、Teams参加者は、ライブ通話中にメッセージング拡張機能と直接やり取りできます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-195">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="bae3a-196">会議内メッセージング拡張機能を構築する場合は、次の点を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="bae3a-196">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="bae3a-197">**Location**。</span><span class="sxs-lookup"><span data-stu-id="bae3a-197">**Location**.</span></span> <span data-ttu-id="bae3a-198">メッセージング拡張機能は、メッセージの作成領域、コマンド ボックス、または会議チャット@mentionedから呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-198">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="bae3a-199">**メタデータ**.</span><span class="sxs-lookup"><span data-stu-id="bae3a-199">**Metadata**.</span></span> <span data-ttu-id="bae3a-200">メッセージング拡張機能が呼び出されると、ユーザーとテナントを識別 `userId` できます `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="bae3a-200">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="bae3a-201">`meetingId` は、`channelData` オブジェクトに含まれています。</span><span class="sxs-lookup"><span data-stu-id="bae3a-201">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="bae3a-202">アプリは、API 要求 `userId` とを `meetingId`  使用して `GetParticipant` ユーザー ロールを取得できます。</span><span class="sxs-lookup"><span data-stu-id="bae3a-202">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="bae3a-203">**コマンドの種類**。</span><span class="sxs-lookup"><span data-stu-id="bae3a-203">**Command type**.</span></span> <span data-ttu-id="bae3a-204">メッセージ拡張機能でアクション ベースの [コマンドを使用する](../messaging-extensions/what-are-messaging-extensions.md#action-commands)場合は、タブのシングル サインオン [認証に従う必要](../tabs/how-to/authentication/auth-aad-sso.md) があります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-204">If your message extension uses [action-based commands](../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [single sign-on](../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span>

1. <span data-ttu-id="bae3a-205">**ユーザー エクスペリエンス**。</span><span class="sxs-lookup"><span data-stu-id="bae3a-205">**User experience**.</span></span> <span data-ttu-id="bae3a-206">メッセージング拡張機能は、会議の外部と同じように表示および動作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bae3a-206">You messaging extension should look and behave the same as it would outside a meeting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bae3a-207">次の手順</span><span class="sxs-lookup"><span data-stu-id="bae3a-207">Next steps</span></span>

* [<span data-ttu-id="bae3a-208">操作コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-208">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="bae3a-209">検索コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="bae3a-209">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="bae3a-210">リンク展開</span><span class="sxs-lookup"><span data-stu-id="bae3a-210">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="bae3a-211">詳細情報</span><span class="sxs-lookup"><span data-stu-id="bae3a-211">Learn more</span></span>

<span data-ttu-id="bae3a-212">クイック スタートで試してみてください。</span><span class="sxs-lookup"><span data-stu-id="bae3a-212">Try it out in a quickstart:</span></span>

* <span data-ttu-id="bae3a-213">C のクイック スタート#</span><span class="sxs-lookup"><span data-stu-id="bae3a-213">Quickstarts for C#</span></span>
  * [<span data-ttu-id="bae3a-214">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="bae3a-214">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="bae3a-215">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="bae3a-215">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="bae3a-216">JavaScript のクイック スタート</span><span class="sxs-lookup"><span data-stu-id="bae3a-216">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="bae3a-217">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="bae3a-217">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="bae3a-218">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="bae3a-218">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="bae3a-219">開発の概念Teams詳細を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bae3a-219">Learn more about Teams development concepts:</span></span>

* [<span data-ttu-id="bae3a-220">アプリTeamsについて</span><span class="sxs-lookup"><span data-stu-id="bae3a-220">Understand Teams app capabilities</span></span>](../concepts/capabilities-overview.md)
* [<span data-ttu-id="bae3a-221">メッセージング拡張機能について</span><span class="sxs-lookup"><span data-stu-id="bae3a-221">What are messaging extensions?</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
