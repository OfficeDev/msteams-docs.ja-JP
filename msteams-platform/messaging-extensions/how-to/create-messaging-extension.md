---
title: アプリ Studio を使用してメッセージング拡張機能を作成する
author: clearab
description: アプリ Studio を使用して Microsoft Teams メッセージング拡張機能を作成する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c3437457f7084d2d768af0f0db5208525c368682
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796184"
---
# <a name="create-a-messaging-extension-using-app-studio"></a><span data-ttu-id="b10ba-103">アプリ Studio を使用してメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-103">Create a messaging extension using App Studio</span></span>

> [!TIP]
> <span data-ttu-id="b10ba-104">すばやく開始する方法をお探しですか?</span><span class="sxs-lookup"><span data-stu-id="b10ba-104">Looking for a faster way to get started?</span></span> <span data-ttu-id="b10ba-105">Microsoft Teams ツールキットを使用して、 [メッセージング拡張機能](../../build-your-first-app/build-messaging-extension.md) を作成します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-105">Create a [messaging extension](../../build-your-first-app/build-messaging-extension.md) using the Microsoft Teams Toolkit.</span></span>

<span data-ttu-id="b10ba-106">高レベルでは、次の手順を実行してメッセージング拡張機能を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-106">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="b10ba-107">開発環境を準備する</span><span class="sxs-lookup"><span data-stu-id="b10ba-107">Prepare your development environment</span></span>
2. <span data-ttu-id="b10ba-108">Web サービスを作成および展開する (ngrok のようなトンネリングサービスを使用してローカルに実行する)</span><span class="sxs-lookup"><span data-stu-id="b10ba-108">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="b10ba-109">Web サービスを Bot Framework に登録する</span><span class="sxs-lookup"><span data-stu-id="b10ba-109">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="b10ba-110">アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-110">Create your app package</span></span>
5. <span data-ttu-id="b10ba-111">Microsoft Teams にアプリ パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="b10ba-111">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="b10ba-112">Web サービスを作成し、アプリパッケージを作成し、web サービスを Bot フレームワークに登録するには、任意の順序で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-112">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="b10ba-113">これらの3つの要素は so intertwined なので、どの順序で実行するかにかかわらず、他の要素を更新するために戻る必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-113">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="b10ba-114">登録では、展開された web サービスのメッセージングエンドポイントが必要です。また、web サービスでは、登録から作成された Id とパスワードが必要です。</span><span class="sxs-lookup"><span data-stu-id="b10ba-114">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="b10ba-115">アプリマニフェストには、チームを web サービスに接続するための Id も必要です。</span><span class="sxs-lookup"><span data-stu-id="b10ba-115">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="b10ba-116">メッセージング拡張機能を構築している間は、アプリマニフェストの変更と web サービスへのコードの展開の間に定期的に移行します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-116">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="b10ba-117">アプリマニフェストを操作するときは、JSON ファイルを手動で操作するか、アプリ Studio を使用して変更を行うことができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-117">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="b10ba-118">どちらの方法でも、マニフェストを変更したときに Teams でアプリを再展開 (アップロード) する必要がありますが、変更を web サービスに展開するときには必要ありません。</span><span class="sxs-lookup"><span data-stu-id="b10ba-118">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="b10ba-119">Web サービスを作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-119">Create your web service</span></span>

<span data-ttu-id="b10ba-120">メッセージング拡張機能の核心部分は、web サービスです。</span><span class="sxs-lookup"><span data-stu-id="b10ba-120">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="b10ba-121">1つのルート (通常は、 `/api/messages` すべての要求を受信する) を定義します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-121">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="b10ba-122">最初から作業を開始する場合は、いくつかのオプションから選択できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-122">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="b10ba-123">Web サービスを作成するためのガイドとして、 [クイックスタート](#learn-more) チュートリアルの1つを使用します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-123">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="b10ba-124">[Bot フレームワークサンプルリポジトリ](https://github.com/Microsoft/BotBuilder-Samples)で使用可能なメッセージング拡張機能のサンプルの1つを選択し、開始します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-124">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="b10ba-125">JavaScript を使用している場合は、 [Microsoft teams 用の](https://github.com/OfficeDev/generator-teams) スキャフォールディングを使用して、web サービスを含む teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-125">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="b10ba-126">Web サービスを一から作成する。</span><span class="sxs-lookup"><span data-stu-id="b10ba-126">Create your web service from scratch.</span></span> <span data-ttu-id="b10ba-127">お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-127">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="b10ba-128">Web サービスを Bot Framework に登録する</span><span class="sxs-lookup"><span data-stu-id="b10ba-128">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="b10ba-129">メッセージング拡張機能は、Bot フレームワークのメッセージングスキーマとセキュリティで保護された通信プロトコルを利用します。まだお持ちでない場合は、ボットフレームワークに web サービスを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-129">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="b10ba-130">Microsoft App Id (Teams の内部から Bot Id として参照されている可能性があります)。また、要求に対する応答を受信して応答するために、ユーザーのメッセージング拡張機能でこの登録が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-130">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="b10ba-131">既存の登録を使用している場合は、 [Microsoft Teams チャネルが有効に](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)なっていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-131">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="b10ba-132">クイックスタートのいずれかを実行した場合、または利用可能なサンプルのいずれかから開始した場合は、web サービスを登録することになります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-132">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="b10ba-133">サービスを手動で登録する場合は、3つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-133">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="b10ba-134">Azure サブスクリプションを使用せずに登録することを選択した場合、Bot フレームワークによって提供される簡素化された OAuth 認証フローを利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="b10ba-134">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="b10ba-135">作成後に、登録を Azure に移行することができます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-135">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="b10ba-136">Azure サブスクリプションを保有している場合 (または新しいサブスクリプションを作成する場合) は、Azure Portal を使用して web サービスを手動で登録できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-136">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="b10ba-137">"Bot チャネル登録" リソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-137">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="b10ba-138">無料料金層は、Microsoft Teams からのメッセージが1か月あたりの合計許容メッセージ数を超えないように、選択することができます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-138">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="b10ba-139">Azure サブスクリプションを使用しない場合は、 [従来の登録ポータル](https://dev.botframework.com/bots/new)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-139">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="b10ba-140">アプリ Studio は、web サービス (bot) の登録にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-140">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="b10ba-141">アプリ Studio によって登録された Web サービスが Azure に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="b10ba-141">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="b10ba-142">[従来のポータル](https://dev.botframework.com/bots)を使用して、登録の表示、管理、移行を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-142">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="b10ba-143">アプリのマニフェストを作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-143">Create your app manifest</span></span>

<span data-ttu-id="b10ba-144">アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-144">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="b10ba-145">アプリ Studio を使用してアプリマニフェストを作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-145">Create your app manifest using App Studio</span></span>

<span data-ttu-id="b10ba-146">アプリのマニフェストを作成するために、Microsoft Teams クライアント内からアプリ Studio アプリを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-146">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="b10ba-147">Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー ( **...** ) から App Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-147">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="b10ba-148">まだインストールされていない場合は、それを検索することができます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-148">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="b10ba-149">[ **マニフェストエディター** ] タブで、[ **新しいアプリの作成** ] を選択します (または、既存のアプリにメッセージング拡張機能を追加している場合は、アプリパッケージをインポートできます)。</span><span class="sxs-lookup"><span data-stu-id="b10ba-149">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="b10ba-150">アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b10ba-150">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="b10ba-151">[ **メッセージング拡張機能** ] タブで、[ **セットアップ** ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b10ba-151">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="b10ba-152">メッセージング拡張機能を使用する新しい web サービス (bot) を作成するか、または既に1つの選択/追加をここに登録していることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-152">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="b10ba-153">必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。</span><span class="sxs-lookup"><span data-stu-id="b10ba-153">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="b10ba-154">だいたい次のようになります: `https://someplace.com/api/messages`</span><span class="sxs-lookup"><span data-stu-id="b10ba-154">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="b10ba-155">**コマンド** セクションの [ **追加** ] ボタンを使用すると、メッセージング拡張機能にコマンドを追加できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-155">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="b10ba-156">コマンドの追加の詳細については、「 [詳細](#learn-more) 情報」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-156">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="b10ba-157">メッセージング拡張機能には最大10個のコマンドを定義できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-157">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="b10ba-158">[ **メッセージハンドラ** ] セクションでは、メッセージングがトリガーされるドメインを追加できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-158">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="b10ba-159">詳細については、「 [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-159">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="b10ba-160">**[完了] => [テストと配布** ] タブで、アプリパッケージ (アプリのマニフェストやアプリのアイコンを含む) を **ダウンロード** したり、パッケージを **インストール** したりできます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-160">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="b10ba-161">アプリのマニフェストを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-161">Create your app manifest manually</span></span>

<span data-ttu-id="b10ba-162">ボットやタブの場合と同様に、メッセージング拡張機能のプロパティを含むようにアプリの [アプリマニフェスト](~/resources/schema/manifest-schema.md#composeextensions) を更新します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-162">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="b10ba-163">これらのプロパティは、Microsoft Teams クライアントでメッセージング拡張機能がどのように表示され、動作するかを制御します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-163">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="b10ba-164">メッセージング内線番号は、マニフェストの v 1.0 以降でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b10ba-164">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="b10ba-165">メッセージング拡張機能を宣言する</span><span class="sxs-lookup"><span data-stu-id="b10ba-165">Declare your messaging extension</span></span>

<span data-ttu-id="b10ba-166">メッセージング拡張機能を追加するには、プロパティを使用して、アプリマニフェストに新しいトップレベルの JSON 構造を含め `composeExtensions` ます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-166">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="b10ba-167">アプリに対して1つのメッセージング拡張機能を作成します。これには最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-167">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="b10ba-168">マニフェストは、としてメッセージング拡張機能を参照し `composeExtensions` ます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-168">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="b10ba-169">これは、下位互換性を維持するためのものです。</span><span class="sxs-lookup"><span data-stu-id="b10ba-169">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="b10ba-170">拡張機能の定義は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="b10ba-170">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="b10ba-171">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="b10ba-171">Property name</span></span> | <span data-ttu-id="b10ba-172">用途</span><span class="sxs-lookup"><span data-stu-id="b10ba-172">Purpose</span></span> | <span data-ttu-id="b10ba-173">必須</span><span class="sxs-lookup"><span data-stu-id="b10ba-173">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="b10ba-174">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="b10ba-174">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="b10ba-175">これは通常、Teams アプリ全体の ID と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-175">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="b10ba-176">必要</span><span class="sxs-lookup"><span data-stu-id="b10ba-176">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="b10ba-177">**設定** メニュー項目を有効にします。</span><span class="sxs-lookup"><span data-stu-id="b10ba-177">Enables **Settings** menu item.</span></span> | <span data-ttu-id="b10ba-178">いいえ</span><span class="sxs-lookup"><span data-stu-id="b10ba-178">No</span></span> |
| `commands` | <span data-ttu-id="b10ba-179">このメッセージング拡張機能がサポートするコマンドの配列です。</span><span class="sxs-lookup"><span data-stu-id="b10ba-179">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="b10ba-180">コマンドは10個に制限されています。</span><span class="sxs-lookup"><span data-stu-id="b10ba-180">You are limited to 10 commands.</span></span> | <span data-ttu-id="b10ba-181">必要</span><span class="sxs-lookup"><span data-stu-id="b10ba-181">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="b10ba-182">コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="b10ba-182">Define your commands</span></span>

<span data-ttu-id="b10ba-183">メッセージング拡張機能では、1つまたは複数のコマンドを宣言します。これにより、ユーザーがメッセージング拡張機能をトリガーする場所、および対話の種類が定義されます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-183">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="b10ba-184">メッセージング拡張機能のコマンドの詳細につい [ては、「詳細情報](#learn-more) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-184">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="b10ba-185">マニフェストの簡単な例</span><span class="sxs-lookup"><span data-stu-id="b10ba-185">Simple manifest example</span></span>

<span data-ttu-id="b10ba-186">次の例では、検索コマンドを使用して、アプリマニフェストの単純なメッセージング拡張オブジェクトを示します。</span><span class="sxs-lookup"><span data-stu-id="b10ba-186">The example below is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="b10ba-187">これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。</span><span class="sxs-lookup"><span data-stu-id="b10ba-187">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="b10ba-188">完全な例については、「 [app manifest schema](~/resources/schema/manifest-schema.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-188">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

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

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="b10ba-189">呼び出しメッセージハンドラーを追加する</span><span class="sxs-lookup"><span data-stu-id="b10ba-189">Add your invoke message handlers</span></span>

<span data-ttu-id="b10ba-190">ユーザーがメッセージング拡張機能をトリガーする場合は、最初の呼び出しメッセージを処理し、ユーザーから情報を収集し、その情報を処理して適切に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-190">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="b10ba-191">そのためには、まずメッセージング拡張機能に追加するコマンドの種類を決定し、 [アクションコマンドを追加](~/messaging-extensions/how-to/action-commands/define-action-command.md) するか、 [検索コマンドを追加](~/messaging-extensions/how-to/search-commands/define-search-command.md)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-191">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="b10ba-192">Teams 会議でのメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="b10ba-192">Messaging extensions in Teams meetings</span></span>

<span data-ttu-id="b10ba-193">会議が開始されると、チームの参加者は、live 呼び出しの間にメッセージング拡張機能と直接対話できます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-193">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="b10ba-194">会議でのメッセージング拡張機能を構築する場合は、次の点を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-194">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="b10ba-195">**Location** 。</span><span class="sxs-lookup"><span data-stu-id="b10ba-195">**Location** .</span></span> <span data-ttu-id="b10ba-196">メッセージング拡張機能は、会議チャットの [メッセージの作成] 領域、コマンドボックス、または @mentioned から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-196">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="b10ba-197">**メタデータ** 。</span><span class="sxs-lookup"><span data-stu-id="b10ba-197">**Metadata** .</span></span> <span data-ttu-id="b10ba-198">メッセージング拡張機能が呼び出されると、との間でユーザーとテナントを識別できるようになり `userId` `tenantId` ます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-198">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="b10ba-199">`meetingId` は、`channelData` オブジェクトに含まれています。</span><span class="sxs-lookup"><span data-stu-id="b10ba-199">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="b10ba-200">アプリでは、および API 要求にを使用して、 `userId` `meetingId`  ユーザーの役割を取得でき `GetParticipant` ます。</span><span class="sxs-lookup"><span data-stu-id="b10ba-200">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="b10ba-201">**コマンドの種類** 。</span><span class="sxs-lookup"><span data-stu-id="b10ba-201">**Command type** .</span></span> <span data-ttu-id="b10ba-202">メッセージ拡張機能が [アクションベースのコマンド](../../messaging-extensions/what-are-messaging-extensions.md#action-commands)を使用している場合は、タブ [シングルサインオン](../../tabs/how-to/authentication/auth-aad-sso.md) 認証に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-202">If your message extension uses [action-based commands](../../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [single sign-on](../../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span>

1. <span data-ttu-id="b10ba-203">**ユーザーの利便性** 。</span><span class="sxs-lookup"><span data-stu-id="b10ba-203">**User experience** .</span></span> <span data-ttu-id="b10ba-204">メッセージング内線番号は、会議の外部と同じように表示および動作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b10ba-204">You messaging extension should look and behave the same as it would outside a meeting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b10ba-205">次の手順</span><span class="sxs-lookup"><span data-stu-id="b10ba-205">Next steps</span></span>

* [<span data-ttu-id="b10ba-206">アクションコマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-206">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="b10ba-207">検索コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="b10ba-207">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="b10ba-208">リンク展開</span><span class="sxs-lookup"><span data-stu-id="b10ba-208">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="b10ba-209">詳細情報</span><span class="sxs-lookup"><span data-stu-id="b10ba-209">Learn more</span></span>

<span data-ttu-id="b10ba-210">クイックスタートで試してみる:</span><span class="sxs-lookup"><span data-stu-id="b10ba-210">Try it out in a quickstart:</span></span>

* <span data-ttu-id="b10ba-211">C のクイックスタート#</span><span class="sxs-lookup"><span data-stu-id="b10ba-211">Quickstarts for C#</span></span>
  * [<span data-ttu-id="b10ba-212">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="b10ba-212">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="b10ba-213">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="b10ba-213">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="b10ba-214">JavaScript のクイックスタート</span><span class="sxs-lookup"><span data-stu-id="b10ba-214">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="b10ba-215">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="b10ba-215">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="b10ba-216">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="b10ba-216">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="b10ba-217">Teams 開発の概念の詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b10ba-217">Learn more about Teams development concepts:</span></span>

* [<span data-ttu-id="b10ba-218">Teams アプリの機能を理解する</span><span class="sxs-lookup"><span data-stu-id="b10ba-218">Understand Teams app capabilities</span></span>](../../concepts/capabilities-overview.md)
* [<span data-ttu-id="b10ba-219">メッセージング拡張機能とは</span><span class="sxs-lookup"><span data-stu-id="b10ba-219">What are messaging extensions?</span></span>](~/messaging-extensions/what-are-messaging-extensions.md)
