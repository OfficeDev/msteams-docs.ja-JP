---
title: ボットを他のアプリMicrosoft Teamsする
description: ボットの開発を開始する方法について説明Microsoft Teams
ms.topic: conceptual
keywords: teams ボットの開発
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: c7b719aae3a8d1b09ed8a1be7f54028fe7f2481e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019756"
---
# <a name="add-bots-to-microsoft-teams-apps"></a><span data-ttu-id="b9d36-104">ボットを他のアプリMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="b9d36-104">Add bots to Microsoft Teams apps</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="b9d36-105">インテリジェント ボットを構築して接続し、チャットを通Microsoft Teamsユーザーと対話します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-105">Build and connect intelligent bots to interact with Microsoft Teams users naturally through chat.</span></span> <span data-ttu-id="b9d36-106">または、簡単なコマンド ベースのボットを提供して、より広範なアプリ エクスペリエンスを提供する "コマンドライン" インターフェイスTeams提供します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-106">Or provide a simple commands-based bot, to be used as your "command-line" interface for your broader Teams app experience.</span></span> <span data-ttu-id="b9d36-107">通知専用ボットを作成して、ユーザーに関連する情報をチャネルまたはダイレクト メッセージで直接プッシュできます。</span><span class="sxs-lookup"><span data-stu-id="b9d36-107">You can make a notification-only bot, which can push information relevant to your users directly to them in a channel or direct message.</span></span> <span data-ttu-id="b9d36-108">既存の Bot Framework ベースのボットを持ち込み、Teams固有のサポートを追加して、エクスペリエンスを向上させる方法も可能です。</span><span class="sxs-lookup"><span data-stu-id="b9d36-108">You can even bring your existing Bot Framework-based bot and add Teams-specific support to make your experience shine.</span></span>

![ユーザーを支援するボットの例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a><span data-ttu-id="b9d36-110">知る必要があるもの: ボット</span><span class="sxs-lookup"><span data-stu-id="b9d36-110">What you need to know: Bots</span></span>

<span data-ttu-id="b9d36-111">ボットは、会話で操作する他のチーム メンバーと同様に表示されます。ただし、ボットは六角形のアバター アイコンを持ち、常にオンラインです。</span><span class="sxs-lookup"><span data-stu-id="b9d36-111">A bot appears just like any other team member you interact with in a conversation except that it has a hexagonal avatar icon and is always online.</span></span>

<span data-ttu-id="b9d36-112">ボットの動作は、関係する会話の種類に応じて異なります。</span><span class="sxs-lookup"><span data-stu-id="b9d36-112">A bot behaves differently depending on what kind of conversation it is involved in.</span></span> <span data-ttu-id="b9d36-113">ボットは、Teamsの種類 (アプリ マニフェストのスコープと呼ばれる) を[サポートします](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="b9d36-113">Bots in Teams support several kinds of conversations (called scopes in the [app manifest](~/resources/schema/manifest-schema.md)).</span></span>

* <span data-ttu-id="b9d36-114">`teams` チャネル会話とも呼ばれる</span><span class="sxs-lookup"><span data-stu-id="b9d36-114">`teams` Also called channel conversations</span></span>
* <span data-ttu-id="b9d36-115">`personal` ボットと 1 人のユーザーの会話</span><span class="sxs-lookup"><span data-stu-id="b9d36-115">`personal` Conversations between a bot and a single user</span></span>
* <span data-ttu-id="b9d36-116">`groupChat` ボットと 2 人以上のユーザーとの会話</span><span class="sxs-lookup"><span data-stu-id="b9d36-116">`groupChat` A conversation between a bot and 2 or more users</span></span>

<span data-ttu-id="b9d36-117">詳細[については、「チャット ボットと会話Microsoft Teamsする」](~/resources/bot-v3/bot-conversations/bots-conversations.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9d36-117">See [Have a conversation with a Microsoft Teams bot](~/resources/bot-v3/bot-conversations/bots-conversations.md) for more information.</span></span>

<span data-ttu-id="b9d36-118">アプリMicrosoft Teams、ボットをエクスペリエンスのスターにしたり、ヘルパーにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b9d36-118">With Microsoft Teams apps, you can make the bot the star of your experience, or just a helper.</span></span> <span data-ttu-id="b9d36-119">ボットは、タブやメッセージング拡張機能などの他の機能を含む、より広範なアプリ[](~/tabs/what-are-tabs.md)パッケージの一部[として配布されます](~/messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="b9d36-119">Bots are distributed as part of your broader app package which can include other capabilities such as [tabs](~/tabs/what-are-tabs.md) or [messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="bot-apis"></a><span data-ttu-id="b9d36-120">ボット API</span><span class="sxs-lookup"><span data-stu-id="b9d36-120">Bot APIs</span></span>

<span data-ttu-id="b9d36-121">Microsoft Teamsは、ほとんどの機能をサポート[Microsoft Bot Framework。](https://dev.botframework.com/)</span><span class="sxs-lookup"><span data-stu-id="b9d36-121">Microsoft Teams supports most of the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="b9d36-122">(Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b9d36-122">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="b9d36-123">これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-123">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="b9d36-124">コネクタ カードのような特殊なカードOffice 365使用する</span><span class="sxs-lookup"><span data-stu-id="b9d36-124">Using specialized card types like the Office 365 Connector card</span></span>
* <span data-ttu-id="b9d36-125">アクティビティに関Teams固有のチャネル データの使用と設定</span><span class="sxs-lookup"><span data-stu-id="b9d36-125">Consuming and setting Teams-specific channel data on activities</span></span>
* <span data-ttu-id="b9d36-126">メッセージング拡張機能要求の処理</span><span class="sxs-lookup"><span data-stu-id="b9d36-126">Processing messaging extension requests</span></span>

<span data-ttu-id="b9d36-127">SDK 拡張機能は、ボット ビルダー SDK を含む依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="b9d36-127">The SDK extensions install dependencies, including the Bot Builder SDK.</span></span>

* <span data-ttu-id="b9d36-128">**.NET** ボット ビルダー SDK for .NET Microsoft Teams拡張機能を使用するには [、Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)パッケージを Visual Studio プロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="b9d36-128">**.NET** To use the Microsoft Teams extensions for the Bot Builder SDK for .NET, install the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package in your Visual Studio project.</span></span> <span data-ttu-id="b9d36-129">開発Node.js、v4.6 のMicrosoft Teamsボット フレームワーク[SDK](https://github.com/microsoft/botframework-sdk)に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="b9d36-129">For Node.js development, the BotBuilder for Microsoft Teams functionality has been incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) as of v4.6.</span></span>

<span data-ttu-id="b9d36-130">*「Bot* [Framework のサンプル」も参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="b9d36-130">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9d36-131">他の web プログラミング テクノロジTeamsアプリを開発し[、Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview)を直接呼び出できますが、すべてのトークン処理を自分で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9d36-131">You can develop Teams apps in any other web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="b9d36-132">*Teams App Studio を* 使用すると、アプリ マニフェストを作成および構成し、ボット フレームワーク ボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b9d36-132">*Teams App Studio* helps you create and configure your app manifest, and can create your Bot Framework bot for you.</span></span> <span data-ttu-id="b9d36-133">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="b9d36-133">It also contains a React control library and an interactive card builder.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="b9d36-134">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="b9d36-134">Outgoing webhooks</span></span>

<span data-ttu-id="b9d36-135">送信 Webhook を使用すると、ワークフローのキックオフや必要なその他の簡単なコマンドなど、基本的な操作のための簡単なボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b9d36-135">Outgoing webhooks allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands you may need.</span></span> <span data-ttu-id="b9d36-136">送信 Webhook は、作成したチームにのみ適用され、会社のワークフローに固有の単純なプロセスを対象とします。</span><span class="sxs-lookup"><span data-stu-id="b9d36-136">Outgoing webhooks live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="b9d36-137">詳細 [については、「送信 Webhooks」](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9d36-137">See [outgoing webhooks](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) for more information.</span></span>

## <a name="build-a-great-teams-bot"></a><span data-ttu-id="b9d36-138">最適なボットをTeamsする</span><span class="sxs-lookup"><span data-stu-id="b9d36-138">Build a great Teams bot</span></span>

<span data-ttu-id="b9d36-139">次のトピックでは、ユーザーに最適なボットを作成するプロセスをTeams。</span><span class="sxs-lookup"><span data-stu-id="b9d36-139">The following topics will guide you through the process of creating a great bot for Teams.</span></span>

* <span data-ttu-id="b9d36-140">[ボットを作成する](~/resources/bot-v3/bots-create.md): Bot Framework チームが提供する素晴らしいツール、ドキュメント、コミュニティを活用します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-140">[Create a bot](~/resources/bot-v3/bots-create.md): Take advantage of the great tools, documentation, and community provided by the Bot Framework team.</span></span>
* <span data-ttu-id="b9d36-141">[ボットに相談する](~/resources/bot-v3/bot-conversations/bots-conversations.md): 基本的な会話フローを追加し、チャネル固有の機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-141">[Talk to your bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): Add basic conversation flow and leverage channel-specific functionality.</span></span> <span data-ttu-id="b9d36-142">.NET またはユーザー設定で開発Node.js、ボット ビルダー SDK の拡張機能を使用して作業を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-142">If you develop in .NET or Node.js, use our extensions for the Bot Builder SDK to simplify your work.</span></span>
* <span data-ttu-id="b9d36-143">[ボットでのカードの使用](~/resources/bot-v3/bots-cards.md) ユーザーの応答を伝え、受け入れるカードを設計します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-143">[Using cards in your bot](~/resources/bot-v3/bots-cards.md) Design cards to communicate and accept user response.</span></span>
* <span data-ttu-id="b9d36-144">[ボット イベントに応答します](~/resources/bot-v3/bots-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="b9d36-144">[Respond to bot events](~/resources/bot-v3/bots-notifications.md).</span></span>
* <span data-ttu-id="b9d36-145">[通知専用ボット](~/resources/bot-v3/bots-notification-only.md) ボットを使用してアプリの通知を送信する。</span><span class="sxs-lookup"><span data-stu-id="b9d36-145">[Notification-only bots](~/resources/bot-v3/bots-notification-only.md) Using bots to send notifications for your app.</span></span>
* <span data-ttu-id="b9d36-146">[コンテキストの取得](~/resources/bot-v3/bots-context.md) ユーザーに関する情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-146">[Get context](~/resources/bot-v3/bots-context.md) Get information about the user.</span></span>
* <span data-ttu-id="b9d36-147">[ボット メニュー](~/resources/bot-v3/bots-menus.md) ボットでメニューを使用する。</span><span class="sxs-lookup"><span data-stu-id="b9d36-147">[Bot menus](~/resources/bot-v3/bots-menus.md) Using menus in bots.</span></span>
* <span data-ttu-id="b9d36-148">[ボットとファイル](~/resources/bot-v3/bots-files.md) ボットからのファイルの送受信。</span><span class="sxs-lookup"><span data-stu-id="b9d36-148">[Bots and files](~/resources/bot-v3/bots-files.md) Sending and receiving files from bots.</span></span>
* <span data-ttu-id="b9d36-149">[ボットでのタブの使用](~/resources/bot-v3/bots-with-tabs.md) タブとボットを組み合わせて動作します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-149">[Using tabs with bots](~/resources/bot-v3/bots-with-tabs.md) Making tabs and bots work together.</span></span>
* <span data-ttu-id="b9d36-150">[ボットをテストする](~/resources/bot-v3/bots-test.md): ボットを追加して、個人またはチームの会話を行い、そのボットを実際に確認します。</span><span class="sxs-lookup"><span data-stu-id="b9d36-150">[Test your bot](~/resources/bot-v3/bots-test.md): Add your bot for personal or team conversations to see it in action.</span></span>
