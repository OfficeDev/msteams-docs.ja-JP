---
title: Microsoft Teams アプリにボットを追加する
description: Microsoft Teams でボットの開発を始める方法について説明します。
keywords: teams のボット開発
ms.date: 05/20/2018
ms.openlocfilehash: 0ecb268c34275e958103c9905b2ed1f0858cafda
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674659"
---
# <a name="add-bots-to-microsoft-teams-apps"></a><span data-ttu-id="07b2f-104">Microsoft Teams アプリにボットを追加する</span><span class="sxs-lookup"><span data-stu-id="07b2f-104">Add bots to Microsoft Teams apps</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="07b2f-105">チャットを通じて Microsoft Teams ユーザーと対話するためのインテリジェントボットを構築して接続します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-105">Build and connect intelligent bots to interact with Microsoft Teams users naturally through chat.</span></span> <span data-ttu-id="07b2f-106">または、より幅広い Teams アプリ環境の "コマンドライン" インターフェイスとして使用するために、簡単なコマンドベースのボットを提供します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-106">Or provide a simple commands-based bot, to be used as your "command-line" interface for your broader Teams app experience.</span></span> <span data-ttu-id="07b2f-107">通知専用ボットを作成して、ユーザーに関連する情報をチャネルまたは直接メッセージに直接プッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="07b2f-107">You can make a notification-only bot, which can push information relevant to your users directly to them in a channel or direct message.</span></span> <span data-ttu-id="07b2f-108">既存の Bot フレームワークを使用している bot を利用して、チーム固有のサポートを追加して、快適にご利用いただけるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="07b2f-108">You can even bring your existing Bot Framework-based bot and add Teams-specific support to make your experience shine.</span></span>

![ユーザーを支援する bot の例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a><span data-ttu-id="07b2f-110">知っておくべきこと: Bot</span><span class="sxs-lookup"><span data-stu-id="07b2f-110">What you need to know: Bots</span></span>

<span data-ttu-id="07b2f-111">Bot は、会話でやりとりする他のチームメンバーと同じように表示されます。ただし、六角アイコンがあり、常にオンラインになっています。</span><span class="sxs-lookup"><span data-stu-id="07b2f-111">A bot appears just like any other team member you interact with in a conversation except that it has a hexagonal avatar icon and is always online.</span></span>

<span data-ttu-id="07b2f-112">Bot の動作は、関係する会話の種類によって異なります。</span><span class="sxs-lookup"><span data-stu-id="07b2f-112">A bot behaves differently depending on what kind of conversation it is involved in.</span></span> <span data-ttu-id="07b2f-113">Teams の bot は、いくつかの種類の会話 ([アプリマニフェスト](~/resources/schema/manifest-schema.md)でのスコープと呼ばれます) をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="07b2f-113">Bots in Teams support several kinds of conversations (called scopes in the [app manifest](~/resources/schema/manifest-schema.md)).</span></span>

* <span data-ttu-id="07b2f-114">`teams`チャネル会話とも呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="07b2f-114">`teams` Also called channel conversations</span></span>
* <span data-ttu-id="07b2f-115">`personal`Bot と1人のユーザーとの会話</span><span class="sxs-lookup"><span data-stu-id="07b2f-115">`personal` Conversations between a bot and a single user</span></span>
* <span data-ttu-id="07b2f-116">`groupChat`ボットと2人以上のユーザー間の会話</span><span class="sxs-lookup"><span data-stu-id="07b2f-116">`groupChat` A conversation between a bot and 2 or more users</span></span>

<span data-ttu-id="07b2f-117">詳細については[、「Microsoft Teams の bot との会話](~/resources/bot-v3/bot-conversations/bots-conversations.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="07b2f-117">See [Have a conversation with a Microsoft Teams bot](~/resources/bot-v3/bot-conversations/bots-conversations.md) for more information.</span></span>

<span data-ttu-id="07b2f-118">Microsoft Teams アプリを使用すると、ボットを星で使用したり、ヘルパーとしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="07b2f-118">With Microsoft Teams apps, you can make the bot the star of your experience, or just a helper.</span></span> <span data-ttu-id="07b2f-119">Bot は、[タブ](~/tabs/what-are-tabs.md)や[メッセージング拡張](~/messaging-extensions/what-are-messaging-extensions.md)機能などの他の機能を含む、幅広いアプリパッケージの一部として配布されます。</span><span class="sxs-lookup"><span data-stu-id="07b2f-119">Bots are distributed as part of your broader app package which can include other capabilities such as [tabs](~/tabs/what-are-tabs.md) or [messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="bot-apis"></a><span data-ttu-id="07b2f-120">Bot Api</span><span class="sxs-lookup"><span data-stu-id="07b2f-120">Bot APIs</span></span>

<span data-ttu-id="07b2f-121">Microsoft Teams は、 [Microsoft Bot フレームワーク](https://dev.botframework.com/)の大部分をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="07b2f-121">Microsoft Teams supports most of the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="07b2f-122">(Bot フレームワークに基づく bot が既にある場合は、それを Microsoft Teams での動作に容易に適応させることができます)。[Sdk](/microsoftteams/platform/#pivot=sdk-tools)を利用するには、C# または node.js のどちらかを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="07b2f-122">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="07b2f-123">これらのパッケージは、基本的な Bot ビルダー SDK のクラスとメソッドを拡張します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-123">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="07b2f-124">Office 365 コネクタカードなどの専用カードの種類を使用する</span><span class="sxs-lookup"><span data-stu-id="07b2f-124">Using specialized card types like the Office 365 Connector card</span></span>
* <span data-ttu-id="07b2f-125">アクティビティでのチーム固有のチャネルデータの使用と設定</span><span class="sxs-lookup"><span data-stu-id="07b2f-125">Consuming and setting Teams-specific channel data on activities</span></span>
* <span data-ttu-id="07b2f-126">メッセージング拡張要求の処理</span><span class="sxs-lookup"><span data-stu-id="07b2f-126">Processing messaging extension requests</span></span>

<span data-ttu-id="07b2f-127">SDK 拡張機能は、Bot ビルダー SDK を含む依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="07b2f-127">The SDK extensions install dependencies, including the Bot Builder SDK.</span></span>

* <span data-ttu-id="07b2f-128">**.Net**Bot ビルダー SDK for .NET の Microsoft Teams 拡張機能を使用するには、Visual Studio プロジェクトに、 [teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="07b2f-128">**.NET** To use the Microsoft Teams extensions for the Bot Builder SDK for .NET, install the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package in your Visual Studio project.</span></span>
* <span data-ttu-id="07b2f-129">**Node.js**を使用して、Node.js のボット Builder SDK の Microsoft Teams 拡張機能を使用するには、 [botbuilder](https://www.npmjs.com/package/botbuilder-teams) npm パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-129">**Node.js** To use the Microsoft Teams extensions for the Bot Builder SDK for Node.js, add the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span>
* <span data-ttu-id="07b2f-130">**ソースコード**拡張機能の完全なソースコードについては、Github の「 [BotBuilder-Microsoft teams](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams)リポジトリ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="07b2f-130">**Source code** You can find the full source code for the extensions in the [BotBuilder-MicrosoftTeams](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams) repo on Github.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07b2f-131">他の web プログラミングテクノロジで Teams アプリを開発し、 [Bot フレームワーク REST api](/bot-framework/rest-api/bot-framework-rest-overview)を直接呼び出すことができますが、すべてのトークン処理を自分自身で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="07b2f-131">You can develop Teams apps in any other web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="07b2f-132">*Teams App Studio*は、アプリのマニフェストを作成および構成するのに役立つので、bot フレームワーク bot を作成できます。</span><span class="sxs-lookup"><span data-stu-id="07b2f-132">*Teams App Studio* helps you create and configure your app manifest, and can create your Bot Framework bot for you.</span></span> <span data-ttu-id="07b2f-133">また、コントロールライブラリとインタラクティブカードビルダーを備えています。</span><span class="sxs-lookup"><span data-stu-id="07b2f-133">It also contains a React control library and an interactive card builder.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="07b2f-134">送信 web フック</span><span class="sxs-lookup"><span data-stu-id="07b2f-134">Outgoing webhooks</span></span>

<span data-ttu-id="07b2f-135">送信用の webhook を使用すると、基本的な操作のための簡単な bot を作成できます。たとえば、ワークフローや、必要に応じた他の単純なコマンドのや議などです。</span><span class="sxs-lookup"><span data-stu-id="07b2f-135">Outgoing webhooks allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands you may need.</span></span> <span data-ttu-id="07b2f-136">送信 web フックは、それらを作成したチーム内のみで、会社のワークフローに固有の単純なプロセスを対象としています。</span><span class="sxs-lookup"><span data-stu-id="07b2f-136">Outgoing webhooks live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="07b2f-137">詳細については、「[送信 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="07b2f-137">See [outgoing webhooks](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) for more information.</span></span>

## <a name="build-a-great-teams-bot"></a><span data-ttu-id="07b2f-138">Teams bot を構築する</span><span class="sxs-lookup"><span data-stu-id="07b2f-138">Build a great Teams bot</span></span>

<span data-ttu-id="07b2f-139">次のトピックでは、Teams の大 bot を作成するプロセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-139">The following topics will guide you through the process of creating a great bot for Teams.</span></span>

* <span data-ttu-id="07b2f-140">[Bot を作成する](~/resources/bot-v3/bots-create.md): bot フレームワークチームによって提供される優れたツール、ドキュメント、コミュニティを活用してください。</span><span class="sxs-lookup"><span data-stu-id="07b2f-140">[Create a bot](~/resources/bot-v3/bots-create.md): Take advantage of the great tools, documentation, and community provided by the Bot Framework team.</span></span>
* <span data-ttu-id="07b2f-141">[Bot に連絡して、](~/resources/bot-v3/bot-conversations/bots-conversations.md)基本的な会話フローを追加し、チャネル固有の機能を利用します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-141">[Talk to your bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): Add basic conversation flow and leverage channel-specific functionality.</span></span> <span data-ttu-id="07b2f-142">.NET または node.js で開発する場合は、ボット Builder SDK の拡張機能を使用して作業を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-142">If you develop in .NET or Node.js, use our extensions for the Bot Builder SDK to simplify your work.</span></span>
* <span data-ttu-id="07b2f-143">[Bot でのカードの使用](~/resources/bot-v3/bots-cards.md)デザインカードを使用して、ユーザーの応答をやり取りします。</span><span class="sxs-lookup"><span data-stu-id="07b2f-143">[Using cards in your bot](~/resources/bot-v3/bots-cards.md) Design cards to communicate and accept user response.</span></span>
* <span data-ttu-id="07b2f-144">[Bot イベントに応答](~/resources/bot-v3/bots-notifications.md)します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-144">[Respond to bot events](~/resources/bot-v3/bots-notifications.md).</span></span>
* <span data-ttu-id="07b2f-145">[通知専用ボット](~/resources/bot-v3/bots-notification-only.md)ボットを使用してアプリの通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-145">[Notification-only bots](~/resources/bot-v3/bots-notification-only.md) Using bots to send notifications for your app.</span></span>
* <span data-ttu-id="07b2f-146">[コンテキストを取得](~/resources/bot-v3/bots-context.md)するユーザーに関する情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-146">[Get context](~/resources/bot-v3/bots-context.md) Get information about the user.</span></span>
* <span data-ttu-id="07b2f-147">[Bot メニュー](~/resources/bot-v3/bots-menus.md)Bot でメニューを使用します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-147">[Bot menus](~/resources/bot-v3/bots-menus.md) Using menus in bots.</span></span>
* <span data-ttu-id="07b2f-148">[ボットとファイル](~/resources/bot-v3/bots-files.md)ボットからファイルを送受信する。</span><span class="sxs-lookup"><span data-stu-id="07b2f-148">[Bots and files](~/resources/bot-v3/bots-files.md) Sending and receiving files from bots.</span></span>
* <span data-ttu-id="07b2f-149">[Bot でタブを使用する](~/resources/bot-v3/bots-with-tabs.md)タブと bot を連携させる。</span><span class="sxs-lookup"><span data-stu-id="07b2f-149">[Using tabs with bots](~/resources/bot-v3/bots-with-tabs.md) Making tabs and bots work together.</span></span>
* <span data-ttu-id="07b2f-150">[Bot をテスト](~/resources/bot-v3/bots-test.md)します。個人またはチームの会話に bot を追加して、動作を確認します。</span><span class="sxs-lookup"><span data-stu-id="07b2f-150">[Test your bot](~/resources/bot-v3/bots-test.md): Add your bot for personal or team conversations to see it in action.</span></span>
