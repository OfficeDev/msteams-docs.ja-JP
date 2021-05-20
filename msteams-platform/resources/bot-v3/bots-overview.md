---
title: Microsoft Teamsアプリにボットを追加する
description: Microsoft Teamsでボットの開発を開始する方法について説明します。
ms.topic: conceptual
keywords: チームボット開発
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566755"
---
# <a name="add-bots-to-microsoft-teams-apps"></a><span data-ttu-id="8688b-104">Microsoft Teamsアプリにボットを追加する</span><span class="sxs-lookup"><span data-stu-id="8688b-104">Add bots to Microsoft Teams apps</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="8688b-105">インテリジェントボットを構築し、チャットを通じて自然にMicrosoft Teamsユーザーと対話するように接続します。</span><span class="sxs-lookup"><span data-stu-id="8688b-105">Build and connect intelligent bots to interact with Microsoft Teams users naturally through chat.</span></span> <span data-ttu-id="8688b-106">または、より幅広いTeamsアプリエクスペリエンスのための「コマンドライン」インターフェイスとして使用する、単純なコマンドベースのボットを提供します。</span><span class="sxs-lookup"><span data-stu-id="8688b-106">Or provide a simple commands-based bot, to be used as your "command-line" interface for your broader Teams app experience.</span></span> <span data-ttu-id="8688b-107">通知専用のボットを作成すると、チャンネルまたはダイレクトメッセージでユーザーに関連する情報を直接ユーザーにプッシュできます。</span><span class="sxs-lookup"><span data-stu-id="8688b-107">You can make a notification-only bot, which can push information relevant to your users directly to them in a channel or direct message.</span></span> <span data-ttu-id="8688b-108">既存の Bot Framework ベースのボットを利用して、Teams固有のサポートを追加して、エクスペリエンスを高めることができます。</span><span class="sxs-lookup"><span data-stu-id="8688b-108">You can even bring your existing Bot Framework-based bot and add Teams-specific support to make your experience shine.</span></span>

![ユーザーを支援するボットの例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a><span data-ttu-id="8688b-110">知っておくべきこと: ボット</span><span class="sxs-lookup"><span data-stu-id="8688b-110">What you need to know: Bots</span></span>

<span data-ttu-id="8688b-111">ボットは、会話でやり取りする他のチーム メンバーと同じように表示されます。</span><span class="sxs-lookup"><span data-stu-id="8688b-111">A bot appears just like any other team member you interact with in a conversation except that it has a hexagonal avatar icon and is always online.</span></span>

<span data-ttu-id="8688b-112">ボットは、どのような会話に関係するかによって動作が異なります。</span><span class="sxs-lookup"><span data-stu-id="8688b-112">A bot behaves differently depending on what kind of conversation it is involved in.</span></span> <span data-ttu-id="8688b-113">Teamsのボットは、[アプリ マニフェスト](~/resources/schema/manifest-schema.md)のスコープと呼ばれるいくつかの種類の会話をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="8688b-113">Bots in Teams support several kinds of conversations called scopes in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

* <span data-ttu-id="8688b-114">`teams` チャネル会話とも呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="8688b-114">`teams` Also called channel conversations.</span></span>
* <span data-ttu-id="8688b-115">`personal` ボットと単一ユーザーの会話。</span><span class="sxs-lookup"><span data-stu-id="8688b-115">`personal` Conversations between a bot and a single user.</span></span>
* <span data-ttu-id="8688b-116">`groupChat` ボットと 2 人以上のユーザーの間の会話。</span><span class="sxs-lookup"><span data-stu-id="8688b-116">`groupChat` A conversation between a bot and 2 or more users.</span></span>

<span data-ttu-id="8688b-117">詳細については、「 [Microsoft Teams ボットとの会話 」](~/resources/bot-v3/bot-conversations/bots-conversations.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8688b-117">For more information, see [Have a conversation with a Microsoft Teams bot](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="8688b-118">Microsoft Teamsアプリを使用すると、ボットをエクスペリエンスのスターにしたり、単なるヘルパーにすることができます。</span><span class="sxs-lookup"><span data-stu-id="8688b-118">With Microsoft Teams apps, you can make the bot the star of your experience, or just a helper.</span></span> <span data-ttu-id="8688b-119">ボットは、 [タブ](~/tabs/what-are-tabs.md) や [メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)などの他の機能を含むことができる、より広範なアプリ パッケージの一部として配布されます。</span><span class="sxs-lookup"><span data-stu-id="8688b-119">Bots are distributed as part of your broader app package which can include other capabilities such as [tabs](~/tabs/what-are-tabs.md) or [messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="bot-apis"></a><span data-ttu-id="8688b-120">ボット API</span><span class="sxs-lookup"><span data-stu-id="8688b-120">Bot APIs</span></span>

<span data-ttu-id="8688b-121">Microsoft Teams[は、ほとんどのMicrosoft Bot Framework](https://dev.botframework.com/)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="8688b-121">Microsoft Teams supports most of the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="8688b-122">(Bot Framework に基づくボットが既にある場合は、そのボットを Microsoft Teams での動作に容易に適応させることができます)。[SDK](/microsoftteams/platform/#pivot=sdk-tools) を利用するには、C# か Node.js のどちらかを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8688b-122">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="8688b-123">これらのパッケージは、以下の基本的な Bot Builder SDK のクラスとメソッドを拡張します。</span><span class="sxs-lookup"><span data-stu-id="8688b-123">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="8688b-124">Office 365 コネクタ カードなどの専用のカードの使用。</span><span class="sxs-lookup"><span data-stu-id="8688b-124">Using specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="8688b-125">アクティビティに関する Teams 固有のチャネル データの使用と設定。</span><span class="sxs-lookup"><span data-stu-id="8688b-125">Consuming and setting Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="8688b-126">メッセージング拡張要求の処理。</span><span class="sxs-lookup"><span data-stu-id="8688b-126">Processing messaging extension requests.</span></span>

<span data-ttu-id="8688b-127">SDK 拡張機能は、ボット ビルダー SDK を含む依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="8688b-127">The SDK extensions install dependencies, including the Bot Builder SDK.</span></span>

* <span data-ttu-id="8688b-128">**NET** ボット ビルダー SDK for .NET のMicrosoft Teams拡張機能を使用するには、Visual Studio プロジェクトに [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8688b-128">**.NET** To use the Microsoft Teams extensions for the Bot Builder SDK for .NET, install the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package in your Visual Studio project.</span></span> <span data-ttu-id="8688b-129">Node.js開発のために、ボットビルダーのMicrosoft Teams機能は v4.6 の[時点でボット フレームワーク SDK](https://github.com/microsoft/botframework-sdk)に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="8688b-129">For Node.js development, the BotBuilder for Microsoft Teams functionality has been incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) as of v4.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8688b-130">他の Web プログラミング テクノロジでTeamsアプリを開発し[、Bot Framework REST API を](/bot-framework/rest-api/bot-framework-rest-overview)直接呼び出すことができますが、すべてのトークン処理を自分で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8688b-130">You can develop Teams apps in any other web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="8688b-131">*Teamsアプリスタジオ* では、アプリ マニフェストの作成と構成を行い、ボット フレームワーク ボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="8688b-131">*Teams App Studio* helps you create and configure your app manifest, and can create your Bot Framework bot for you.</span></span> <span data-ttu-id="8688b-132">また、React 制御ライブラリと、対話型カードのビルダーも用意されています。</span><span class="sxs-lookup"><span data-stu-id="8688b-132">It also contains a React control library and an interactive card builder.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="8688b-133">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="8688b-133">Outgoing webhooks</span></span>

<span data-ttu-id="8688b-134">送信 webhook を使用すると、ワークフローや必要なその他の簡単なコマンドを開始するなどの基本的な操作のための単純なボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="8688b-134">Outgoing webhooks allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands you may need.</span></span> <span data-ttu-id="8688b-135">送信 webhook は、ユーザーが作成したチーム内にのみ存続し、会社のワークフローに固有の単純なプロセスを対象としています。</span><span class="sxs-lookup"><span data-stu-id="8688b-135">Outgoing webhooks live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="8688b-136">詳細については、発信 [webhook を](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="8688b-136">For more information, see [outgoing webhooks](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

## <a name="build-a-great-teams-bot"></a><span data-ttu-id="8688b-137">優れたTeamsボットを構築する</span><span class="sxs-lookup"><span data-stu-id="8688b-137">Build a great Teams bot</span></span>

<span data-ttu-id="8688b-138">次のトピックでは、Teamsに最適なボットを作成するプロセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="8688b-138">The following topics will guide you through the process of creating a great bot for Teams:</span></span>

* <span data-ttu-id="8688b-139">[ボットの作成](~/resources/bot-v3/bots-create.md): Bot Framework チームが提供する優れたツール、ドキュメント、コミュニティを活用します。</span><span class="sxs-lookup"><span data-stu-id="8688b-139">[Create a bot](~/resources/bot-v3/bots-create.md): Take advantage of the great tools, documentation, and community provided by the Bot Framework team.</span></span>
* <span data-ttu-id="8688b-140">[ボットに話す](~/resources/bot-v3/bot-conversations/bots-conversations.md): 基本的な会話フローを追加し、チャネル固有の機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="8688b-140">[Talk to your bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): Add basic conversation flow and leverage channel-specific functionality.</span></span> <span data-ttu-id="8688b-141">NET または Node.js で開発する場合は、Bot Builder SDK の拡張機能を使用して作業を簡略化します。</span><span class="sxs-lookup"><span data-stu-id="8688b-141">If you develop in .NET or Node.js, use our extensions for the Bot Builder SDK to simplify your work.</span></span>
* <span data-ttu-id="8688b-142">[ボットでカードを使用](~/resources/bot-v3/bots-cards.md)する : カードをデザインして通信し、ユーザーの応答を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="8688b-142">[Using cards in your bot](~/resources/bot-v3/bots-cards.md): Design cards to communicate and accept user response.</span></span>
* [<span data-ttu-id="8688b-143">ボット イベントに応答する</span><span class="sxs-lookup"><span data-stu-id="8688b-143">Respond to bot events</span></span>](~/resources/bot-v3/bots-notifications.md)
* <span data-ttu-id="8688b-144">[通知専用ボット](~/resources/bot-v3/bots-notification-only.md): ボットを使用してアプリの通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="8688b-144">[Notification-only bots](~/resources/bot-v3/bots-notification-only.md): Using bots to send notifications for your app.</span></span>
* <span data-ttu-id="8688b-145">[コンテキストの取得](~/resources/bot-v3/bots-context.md): ユーザーに関する情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="8688b-145">[Get context](~/resources/bot-v3/bots-context.md): Get information about the user.</span></span>
* <span data-ttu-id="8688b-146">[ボットメニュー](~/resources/bot-v3/bots-menus.md): ボットでメニューを使用する。</span><span class="sxs-lookup"><span data-stu-id="8688b-146">[Bot menus](~/resources/bot-v3/bots-menus.md): Using menus in bots.</span></span>
* <span data-ttu-id="8688b-147">[ボットとファイル](~/resources/bot-v3/bots-files.md): ボットからファイルを送受信します。</span><span class="sxs-lookup"><span data-stu-id="8688b-147">[Bots and files](~/resources/bot-v3/bots-files.md): Sending and receiving files from bots.</span></span>
* <span data-ttu-id="8688b-148">[ボットでタブを使用](~/resources/bot-v3/bots-with-tabs.md)する : タブとボットを連携させる。</span><span class="sxs-lookup"><span data-stu-id="8688b-148">[Using tabs with bots](~/resources/bot-v3/bots-with-tabs.md): Making tabs and bots work together.</span></span>
* <span data-ttu-id="8688b-149">[ボットをテストする](~/resources/bot-v3/bots-test.md): ボットを追加して、個人やチームでの会話を行って、実際に見ることができます。</span><span class="sxs-lookup"><span data-stu-id="8688b-149">[Test your bot](~/resources/bot-v3/bots-test.md): Add your bot for personal or team conversations to see it in action.</span></span>

## <a name="see-also"></a><span data-ttu-id="8688b-150">関連項目</span><span class="sxs-lookup"><span data-stu-id="8688b-150">See also</span></span>

<span data-ttu-id="8688b-151">[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="8688b-151">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>