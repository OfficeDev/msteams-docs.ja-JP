---
title: メッセージングの拡張機能を作成する
author: clearab
description: Microsoft Teams アプリのメッセージング拡張機能を作成する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: ca03469b04c9696b26db3512790e03be26ca63af
ms.sourcegitcommit: b01986739a05c65094618fbe76aeb53d038b1c74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48178310"
---
# <a name="create-a-messaging-extension-in-microsoft-teams"></a><span data-ttu-id="80788-103">Microsoft Teams でメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="80788-103">Create a messaging extension in Microsoft Teams</span></span>

<span data-ttu-id="80788-104">高レベルでは、次の手順を実行してメッセージング拡張機能を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-104">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="80788-105">開発環境を準備する</span><span class="sxs-lookup"><span data-stu-id="80788-105">Prepare your development environment</span></span>
2. <span data-ttu-id="80788-106">Web サービスを作成および展開する (ngrok のようなトンネリングサービスを使用してローカルに実行する)</span><span class="sxs-lookup"><span data-stu-id="80788-106">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="80788-107">Web サービスを Bot Framework に登録する</span><span class="sxs-lookup"><span data-stu-id="80788-107">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="80788-108">アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="80788-108">Create your app package</span></span>
5. <span data-ttu-id="80788-109">Microsoft Teams にアプリ パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="80788-109">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="80788-110">Web サービスを作成し、アプリパッケージを作成し、web サービスを Bot フレームワークに登録するには、任意の順序で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="80788-110">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="80788-111">これらの3つの要素は so intertwined なので、どの順序で実行するかにかかわらず、他の要素を更新するために戻る必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-111">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="80788-112">登録では、展開された web サービスのメッセージングエンドポイントが必要です。また、web サービスでは、登録から作成された Id とパスワードが必要です。</span><span class="sxs-lookup"><span data-stu-id="80788-112">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="80788-113">アプリマニフェストには、チームを web サービスに接続するための Id も必要です。</span><span class="sxs-lookup"><span data-stu-id="80788-113">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="80788-114">メッセージング拡張機能を構築している間は、アプリマニフェストの変更と web サービスへのコードの展開の間に定期的に移行します。</span><span class="sxs-lookup"><span data-stu-id="80788-114">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="80788-115">アプリマニフェストを操作するときは、JSON ファイルを手動で操作するか、アプリ Studio を使用して変更を行うことができることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="80788-115">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="80788-116">どちらの方法でも、マニフェストを変更したときに Teams でアプリを再展開 (アップロード) する必要がありますが、変更を web サービスに展開するときには必要ありません。</span><span class="sxs-lookup"><span data-stu-id="80788-116">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="80788-117">Web サービスを作成する</span><span class="sxs-lookup"><span data-stu-id="80788-117">Create your web service</span></span>

<span data-ttu-id="80788-118">メッセージング拡張機能の核心部分は、web サービスです。</span><span class="sxs-lookup"><span data-stu-id="80788-118">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="80788-119">1つのルート (通常は、 `/api/messages` すべての要求を受信する) を定義します。</span><span class="sxs-lookup"><span data-stu-id="80788-119">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="80788-120">最初から作業を開始する場合は、いくつかのオプションから選択できます。</span><span class="sxs-lookup"><span data-stu-id="80788-120">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="80788-121">Web サービスを作成するためのガイドとして、 [クイックスタート](#learn-more) チュートリアルの1つを使用します。</span><span class="sxs-lookup"><span data-stu-id="80788-121">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="80788-122">[Bot フレームワークサンプルリポジトリ](https://github.com/Microsoft/BotBuilder-Samples)で使用可能なメッセージング拡張機能のサンプルの1つを選択し、開始します。</span><span class="sxs-lookup"><span data-stu-id="80788-122">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="80788-123">JavaScript を使用している場合は、 [Microsoft teams 用の](https://github.com/OfficeDev/generator-teams) スキャフォールディングを使用して、web サービスを含む teams アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="80788-123">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="80788-124">Web サービスを一から作成する。</span><span class="sxs-lookup"><span data-stu-id="80788-124">Create your web service from scratch.</span></span> <span data-ttu-id="80788-125">お使いの言語用の Bot Framework SDK を追加することも、JSON ペイロードに対して直接作業を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="80788-125">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="80788-126">Web サービスを Bot Framework に登録する</span><span class="sxs-lookup"><span data-stu-id="80788-126">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="80788-127">メッセージング拡張機能は、Bot フレームワークのメッセージングスキーマとセキュリティで保護された通信プロトコルを利用します。まだお持ちでない場合は、ボットフレームワークに web サービスを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-127">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="80788-128">Microsoft App Id (Teams の内部から Bot Id として参照されている可能性があります)。また、要求に対する応答を受信して応答するために、ユーザーのメッセージング拡張機能でこの登録が使用されます。</span><span class="sxs-lookup"><span data-stu-id="80788-128">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="80788-129">既存の登録を使用している場合は、 [Microsoft Teams チャネルが有効に](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)なっていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="80788-129">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="80788-130">クイックスタートのいずれかを実行した場合、または利用可能なサンプルのいずれかから開始した場合は、web サービスを登録することになります。</span><span class="sxs-lookup"><span data-stu-id="80788-130">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="80788-131">サービスを手動で登録する場合は、3つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="80788-131">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="80788-132">Azure サブスクリプションを使用せずに登録することを選択した場合、Bot フレームワークによって提供される簡素化された OAuth 認証フローを利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="80788-132">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="80788-133">作成後に、登録を Azure に移行することができます。</span><span class="sxs-lookup"><span data-stu-id="80788-133">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="80788-134">Azure サブスクリプションを保有している場合 (または新しいサブスクリプションを作成する場合) は、Azure Portal を使用して web サービスを手動で登録できます。</span><span class="sxs-lookup"><span data-stu-id="80788-134">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="80788-135">"Bot チャネル登録" リソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="80788-135">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="80788-136">無料料金層は、Microsoft Teams からのメッセージが1か月あたりの合計許容メッセージ数を超えないように、選択することができます。</span><span class="sxs-lookup"><span data-stu-id="80788-136">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="80788-137">Azure サブスクリプションを使用しない場合は、 [従来の登録ポータル](https://dev.botframework.com/bots/new)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="80788-137">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="80788-138">アプリ Studio は、web サービス (bot) の登録にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="80788-138">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="80788-139">アプリ Studio によって登録された Web サービスが Azure に登録されていません。</span><span class="sxs-lookup"><span data-stu-id="80788-139">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="80788-140">[従来のポータル](https://dev.botframework.com/bots)を使用して、登録の表示、管理、移行を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="80788-140">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="80788-141">アプリのマニフェストを作成する</span><span class="sxs-lookup"><span data-stu-id="80788-141">Create your app manifest</span></span>

<span data-ttu-id="80788-142">アプリ マニフェストは、App Studio を使用して作成することも、手動で作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="80788-142">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="80788-143">アプリ Studio を使用してアプリマニフェストを作成する</span><span class="sxs-lookup"><span data-stu-id="80788-143">Create your app manifest using App Studio</span></span>

<span data-ttu-id="80788-144">アプリのマニフェストを作成するために、Microsoft Teams クライアント内からアプリ Studio アプリを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="80788-144">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="80788-145">Teams クライアントで、左側のナビゲーション レールにあるオーバーフロー メニュー (**...**) から App Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="80788-145">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="80788-146">まだインストールされていない場合は、それを検索することができます。</span><span class="sxs-lookup"><span data-stu-id="80788-146">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="80788-147">[ **マニフェストエディター** ] タブで、[ **新しいアプリの作成** ] を選択します (または、既存のアプリにメッセージング拡張機能を追加している場合は、アプリパッケージをインポートできます)。</span><span class="sxs-lookup"><span data-stu-id="80788-147">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="80788-148">アプリの詳細情報を入力します (各フィールドの詳細な説明については、「[マニフェスト スキーマの定義](~/resources/schema/manifest-schema.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="80788-148">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="80788-149">[ **メッセージング拡張機能** ] タブで、[ **セットアップ** ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="80788-149">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="80788-150">メッセージング拡張機能を使用する新しい web サービス (bot) を作成するか、または既に1つの選択/追加をここに登録していることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="80788-150">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="80788-151">必要に応じて、ボット エンドポイント アドレスを変更して、ボットにポイントします。</span><span class="sxs-lookup"><span data-stu-id="80788-151">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="80788-152">だいたい次のようになります: `https://someplace.com/api/messages`</span><span class="sxs-lookup"><span data-stu-id="80788-152">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="80788-153">**コマンド**セクションの [**追加**] ボタンを使用すると、メッセージング拡張機能にコマンドを追加できます。</span><span class="sxs-lookup"><span data-stu-id="80788-153">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="80788-154">コマンドの追加の詳細については、「 [詳細](#learn-more) 情報」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="80788-154">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="80788-155">メッセージング拡張機能には最大10個のコマンドを定義できます。</span><span class="sxs-lookup"><span data-stu-id="80788-155">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="80788-156">[ **メッセージハンドラ** ] セクションでは、メッセージングがトリガーされるドメインを追加できます。</span><span class="sxs-lookup"><span data-stu-id="80788-156">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="80788-157">詳細については、「 [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="80788-157">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="80788-158">**[完了] => [テストと配布**] タブで、アプリパッケージ (アプリのマニフェストやアプリのアイコンを含む) を**ダウンロード**したり、パッケージを**インストール**したりできます。</span><span class="sxs-lookup"><span data-stu-id="80788-158">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="80788-159">アプリのマニフェストを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="80788-159">Create your app manifest manually</span></span>

<span data-ttu-id="80788-160">ボットやタブの場合と同様に、メッセージング拡張機能のプロパティを含むようにアプリの [アプリマニフェスト](~/resources/schema/manifest-schema.md#composeextensions) を更新します。</span><span class="sxs-lookup"><span data-stu-id="80788-160">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="80788-161">これらのプロパティは、Microsoft Teams クライアントでメッセージング拡張機能がどのように表示され、動作するかを制御します。</span><span class="sxs-lookup"><span data-stu-id="80788-161">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="80788-162">メッセージング内線番号は、マニフェストの v 1.0 以降でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="80788-162">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="80788-163">メッセージング拡張機能を宣言する</span><span class="sxs-lookup"><span data-stu-id="80788-163">Declare your messaging extension</span></span>

<span data-ttu-id="80788-164">メッセージング拡張機能を追加するには、プロパティを使用して、アプリマニフェストに新しいトップレベルの JSON 構造を含め `composeExtensions` ます。</span><span class="sxs-lookup"><span data-stu-id="80788-164">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="80788-165">アプリに対して1つのメッセージング拡張機能を作成します。これには最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="80788-165">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="80788-166">マニフェストは、としてメッセージング拡張機能を参照し `composeExtensions` ます。</span><span class="sxs-lookup"><span data-stu-id="80788-166">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="80788-167">これは、下位互換性を維持するためのものです。</span><span class="sxs-lookup"><span data-stu-id="80788-167">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="80788-168">拡張機能の定義は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="80788-168">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="80788-169">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="80788-169">Property name</span></span> | <span data-ttu-id="80788-170">用途</span><span class="sxs-lookup"><span data-stu-id="80788-170">Purpose</span></span> | <span data-ttu-id="80788-171">必須</span><span class="sxs-lookup"><span data-stu-id="80788-171">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="80788-172">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="80788-172">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="80788-173">これは通常、Teams アプリ全体の ID と同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-173">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="80788-174">はい</span><span class="sxs-lookup"><span data-stu-id="80788-174">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="80788-175">**設定**メニュー項目を有効にします。</span><span class="sxs-lookup"><span data-stu-id="80788-175">Enables **Settings** menu item.</span></span> | <span data-ttu-id="80788-176">いいえ</span><span class="sxs-lookup"><span data-stu-id="80788-176">No</span></span> |
| `commands` | <span data-ttu-id="80788-177">このメッセージング拡張機能がサポートするコマンドの配列です。</span><span class="sxs-lookup"><span data-stu-id="80788-177">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="80788-178">コマンドは10個に制限されています。</span><span class="sxs-lookup"><span data-stu-id="80788-178">You are limited to 10 commands.</span></span> | <span data-ttu-id="80788-179">はい</span><span class="sxs-lookup"><span data-stu-id="80788-179">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="80788-180">コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="80788-180">Define your commands</span></span>

<span data-ttu-id="80788-181">メッセージング拡張機能では、1つまたは複数のコマンドを宣言します。これにより、ユーザーがメッセージング拡張機能をトリガーする場所、および対話の種類が定義されます。</span><span class="sxs-lookup"><span data-stu-id="80788-181">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="80788-182">メッセージング拡張機能のコマンドの詳細につい [ては、「詳細情報](#learn-more) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="80788-182">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="80788-183">マニフェストの簡単な例</span><span class="sxs-lookup"><span data-stu-id="80788-183">Simple manifest example</span></span>

<span data-ttu-id="80788-184">次の例では、検索コマンドを使用して、アプリマニフェストの単純なメッセージング拡張オブジェクトを示します。</span><span class="sxs-lookup"><span data-stu-id="80788-184">The example below is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="80788-185">これは、アプリ マニフェスト ファイルの全体ではなく、メッセージング拡張機能に関わる部分のみです。</span><span class="sxs-lookup"><span data-stu-id="80788-185">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="80788-186">完全な例については、「 [app manifest schema](~/resources/schema/manifest-schema.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="80788-186">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

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

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="80788-187">呼び出しメッセージハンドラーを追加する</span><span class="sxs-lookup"><span data-stu-id="80788-187">Add your invoke message handlers</span></span>

<span data-ttu-id="80788-188">ユーザーがメッセージング拡張機能をトリガーする場合は、最初の呼び出しメッセージを処理し、ユーザーから情報を収集し、その情報を処理して適切に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-188">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="80788-189">そのためには、まずメッセージング拡張機能に追加するコマンドの種類を決定し、 [アクションコマンドを追加](~/messaging-extensions/how-to/action-commands/define-action-command.md) するか、 [検索コマンドを追加](~/messaging-extensions/how-to/search-commands/define-search-command.md)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-189">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="80788-190">Teams 会議でのメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="80788-190">Messaging extensions in Teams meetings</span></span>

<span data-ttu-id="80788-191">会議が開始されると、チームの参加者は、live 呼び出しの間にメッセージング拡張機能と直接対話できます。</span><span class="sxs-lookup"><span data-stu-id="80788-191">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="80788-192">会議でのメッセージング拡張機能を構築する場合は、次の点を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="80788-192">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="80788-193">**Location**。</span><span class="sxs-lookup"><span data-stu-id="80788-193">**Location**.</span></span> <span data-ttu-id="80788-194">メッセージング拡張機能は、会議チャットの [メッセージの作成] 領域、コマンドボックス、または @mentioned から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="80788-194">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="80788-195">**メタデータ**。</span><span class="sxs-lookup"><span data-stu-id="80788-195">**Metadata**.</span></span> <span data-ttu-id="80788-196">メッセージング拡張機能が呼び出されると、との間でユーザーとテナントを識別できるようになり `userId` `tenantId` ます。</span><span class="sxs-lookup"><span data-stu-id="80788-196">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="80788-197">は、 `meetingId` オブジェクトの一部として見つけることができ `channelData` ます。</span><span class="sxs-lookup"><span data-stu-id="80788-197">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="80788-198">アプリでは、および API 要求にを使用して、 `userId` `meetingId`  ユーザーの役割を取得でき `GetParticipant` ます。</span><span class="sxs-lookup"><span data-stu-id="80788-198">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="80788-199">**コマンドの種類**。</span><span class="sxs-lookup"><span data-stu-id="80788-199">**Command type**.</span></span> <span data-ttu-id="80788-200">メッセージ拡張機能が [アクションベースのコマンド](../../messaging-extensions/what-are-messaging-extensions.md#action-commands)を使用している場合は、タブ [シングルサインオン](../../tabs/how-to/authentication/auth-aad-sso.md) 認証に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-200">If your message extension uses [action-based commands](../../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [Single Sign-On](../../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span> 

1. <span data-ttu-id="80788-201">**ユーザーの利便性**。</span><span class="sxs-lookup"><span data-stu-id="80788-201">**User experience**.</span></span> <span data-ttu-id="80788-202">会議チャット中に呼び出されるメッセージング拡張機能のエンドユーザーの環境を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="80788-202">You should determine the intended the end-user experience for messaging extensions invoked during a meeting chat.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80788-203">次の手順</span><span class="sxs-lookup"><span data-stu-id="80788-203">Next steps</span></span>

* [<span data-ttu-id="80788-204">アクションコマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="80788-204">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="80788-205">検索コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="80788-205">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="80788-206">リンク展開</span><span class="sxs-lookup"><span data-stu-id="80788-206">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="80788-207">詳細情報</span><span class="sxs-lookup"><span data-stu-id="80788-207">Learn more</span></span>

<span data-ttu-id="80788-208">クイックスタートで試してみる:</span><span class="sxs-lookup"><span data-stu-id="80788-208">Try it out in a quickstart:</span></span>

* <span data-ttu-id="80788-209">C のクイックスタート#</span><span class="sxs-lookup"><span data-stu-id="80788-209">Quickstarts for C#</span></span>
  * [<span data-ttu-id="80788-210">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="80788-210">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="80788-211">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="80788-211">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="80788-212">JavaScript のクイックスタート</span><span class="sxs-lookup"><span data-stu-id="80788-212">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="80788-213">アクションベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="80788-213">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="80788-214">検索ベースのコマンドを使用したメッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="80788-214">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="80788-215">メッセージング拡張機能の概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="80788-215">Learn more about messaging extensions concepts:</span></span>

* [<span data-ttu-id="80788-216">Teams アプリの機能を理解する</span><span class="sxs-lookup"><span data-stu-id="80788-216">Understand Teams app capabilities ?</span></span>](~/concepts/extensibility-points.md)
* [<span data-ttu-id="80788-217">メッセージング拡張機能とは</span><span class="sxs-lookup"><span data-stu-id="80788-217">What are messaging extensions?</span></span>](~/messaging-extensions/what-are-messaging-extensions.md)
