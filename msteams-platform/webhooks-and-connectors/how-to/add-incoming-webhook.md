---
title: 受信 web フックを使用して Microsoft Teams に外部要求を投稿する
author: laujan
description: 受信 webhook を Teams アプリに追加する方法
keywords: Teams、タブ、送信 Webhook*
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 3aa795170af9695fc375043c94e794f814b38646
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819068"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a><span data-ttu-id="8e4be-104">受信 web フックを使用して Teams に外部要求を投稿する</span><span class="sxs-lookup"><span data-stu-id="8e4be-104">Post external requests to Teams with incoming webhooks</span></span>

## <a name="what-are-incoming-webhooks-in-teams"></a><span data-ttu-id="8e4be-105">Teams での受信 web フックとは</span><span class="sxs-lookup"><span data-stu-id="8e4be-105">What are incoming webhooks in Teams?</span></span>

<span data-ttu-id="8e4be-106">受信 web フックは、外部アプリがチームチャネル内のコンテンツを共有するための簡単な方法を提供し、多くの場合、追跡および通知ツールとして使用される、Teams の特別な種類のコネクタです。</span><span class="sxs-lookup"><span data-stu-id="8e4be-106">Incoming webhooks are special type of Connector in Teams that provide a simple way for an external app to share content in team channels and are often used as tracking and notification tools.</span></span> <span data-ttu-id="8e4be-107">Teams には、POST するメッセージで JSON ペイロードを送信するための一意の URL が用意されています (通常はカード形式)。</span><span class="sxs-lookup"><span data-stu-id="8e4be-107">Teams provides a unique URL to which you send a JSON payload with the message that you want to POST, typically in a card format.</span></span> <span data-ttu-id="8e4be-108">カードは、1つのトピックに関連するコンテンツとアクションを含むユーザーインターフェイス (UI) コンテナーで、一貫性のある方法でメッセージデータを表示する方法です。</span><span class="sxs-lookup"><span data-stu-id="8e4be-108">Cards are user-interface (UI) containers that contain content and actions related to a single topic and are a way to present message data in a consistent way.</span></span> <span data-ttu-id="8e4be-109">Teams は3つの機能内でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-109">Teams uses cards within three capabilities:</span></span>

* <span data-ttu-id="8e4be-110">ボット</span><span class="sxs-lookup"><span data-stu-id="8e4be-110">Bots</span></span>
* <span data-ttu-id="8e4be-111">メッセージングの拡張機能</span><span class="sxs-lookup"><span data-stu-id="8e4be-111">Messaging extensions</span></span>
* <span data-ttu-id="8e4be-112">コネクタ</span><span class="sxs-lookup"><span data-stu-id="8e4be-112">Connectors</span></span>

## <a name="incoming-webhook-key-features"></a><span data-ttu-id="8e4be-113">受信 webhook キー機能</span><span class="sxs-lookup"><span data-stu-id="8e4be-113">Incoming webhook key features</span></span>

| <span data-ttu-id="8e4be-114">機能</span><span class="sxs-lookup"><span data-stu-id="8e4be-114">Feature</span></span> | <span data-ttu-id="8e4be-115">説明</span><span class="sxs-lookup"><span data-stu-id="8e4be-115">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="8e4be-116">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="8e4be-116">Scoped Configuration</span></span>|<span data-ttu-id="8e4be-117">受信 web フックは、チャネルレベルでスコープ設定および構成されます (たとえば、送信 web フックはチームレベルでスコープ設定および構成されます)。</span><span class="sxs-lookup"><span data-stu-id="8e4be-117">Incoming webhooks are scoped and configured at the channel level (e.g., outgoing webhooks are scoped and configured at the team level).</span></span>|
|<span data-ttu-id="8e4be-118">リソース定義の保護</span><span class="sxs-lookup"><span data-stu-id="8e4be-118">Secure resource definitions</span></span>|<span data-ttu-id="8e4be-119">メッセージは JSON ペイロードとして書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="8e4be-119">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="8e4be-120">この宣言型メッセージング構造では、クライアントでコードが実行されていないため、悪意のあるコードが挿入されることはありません。</span><span class="sxs-lookup"><span data-stu-id="8e4be-120">This declarative messaging structure prevents the injection of malicious code as there is no code execution on the client.</span></span>|
|<span data-ttu-id="8e4be-121">アクション可能なメッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="8e4be-121">Actionable messaging support</span></span>|<span data-ttu-id="8e4be-122">カードを経由してメッセージを送信する場合は、操作可能な **メッセージカード** 形式を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e4be-122">If you choose to send messages via cards, you must use the **actionable message card** format.</span></span> <span data-ttu-id="8e4be-123">操作可能なメッセージカードは、Teams を含むすべての Office 365 グループでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8e4be-123">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="8e4be-124">従来の操作可能な [メッセージカード参照](/outlook/actionable-messages/message-card-reference) と [メッセージカードプレイグラウンド](https://messagecardplayground.azurewebsites.net)へのリンクを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-124">Here are links to the [Legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and the [Message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="8e4be-125">独立した HTTPS メッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="8e4be-125">Independent HTTPS messaging support</span></span>| <span data-ttu-id="8e4be-126">カードは、わかりやすく一貫した方法で情報を表示するための最適な方法です。</span><span class="sxs-lookup"><span data-stu-id="8e4be-126">Cards are a great way to present information in a clear and consistent way.</span></span> <span data-ttu-id="8e4be-127">HTTPS POST 要求を送信できる任意のツールまたはフレームワークは、受信した webhook を介してチームにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="8e4be-127">Any tool or framework that can send HTTPS POST requests can send messages to Teams via an incoming webhook.</span></span>|
|<span data-ttu-id="8e4be-128">Markdown のサポート</span><span class="sxs-lookup"><span data-stu-id="8e4be-128">Markdown support</span></span>|<span data-ttu-id="8e4be-129">操作可能なメッセージングカードのすべてのテキストフィールドは、基本的な Markdown をサポートします。</span><span class="sxs-lookup"><span data-stu-id="8e4be-129">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="8e4be-130">**カードには、HTML マークアップを使用しないで**ください。</span><span class="sxs-lookup"><span data-stu-id="8e4be-130">**Don't use HTML markup in your cards**.</span></span> <span data-ttu-id="8e4be-131">HTML は無視され、プレーン テキストとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="8e4be-131">HTML is ignored and treated as plain text.</span></span>|

> [!Note]  
> <span data-ttu-id="8e4be-132">Teams bot、メッセージング拡張機能、ボットフレームワークは、オープンなクロスカードプラットフォームフレームワークであるアダプティブカードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="8e4be-132">Teams bots, messaging extensions, and the Bot Framework support Adaptive Cards, an open cross-card platform framework.</span></span> <span data-ttu-id="8e4be-133">Teams コネクタは現在、アダプティブカードをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="8e4be-133">Teams connectors do not currently support Adaptive Cards.</span></span> <span data-ttu-id="8e4be-134">ただし、アダプティブカードを Teams チャネルにポストする [フロー](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) を作成することは可能です。</span><span class="sxs-lookup"><span data-stu-id="8e4be-134">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts adaptive cards to a Teams channel.</span></span>

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a><span data-ttu-id="8e4be-135">受信 webhook を Teams チャネルに追加する</span><span class="sxs-lookup"><span data-stu-id="8e4be-135">Add an incoming webhook to a Teams channel</span></span>

> [!Important]  
> <span data-ttu-id="8e4be-136">チームの**設定**メンバーのアクセス許可で [  =>  **Member permissions**  =>  **メンバーによるコネクタの作成、更新、および削除を許可**する] が選択されている場合は、すべてのチームメンバーがコネクタを追加、変更、または削除できます。</span><span class="sxs-lookup"><span data-stu-id="8e4be-136">If your team's **Settings** => **Member permissions** => **Allow members to create, update, and remove connectors** is selected, any team member can add, modify, or delete a connector.</span></span>

1. <span data-ttu-id="8e4be-137">Webhook を追加するチャネルに移動し、上部のナビゲーションバーから [ *その他のオプション* ] を選択します (&#8226;&#8226;&#8226;)。</span><span class="sxs-lookup"><span data-stu-id="8e4be-137">Navigate to the channel where you want to add the webhook and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="8e4be-138">ドロップダウンメニューから [ **コネクタ** ] を選択し、 **受信 Webhook**を検索します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-138">Choose **Connectors** from the drop-down menu and search for **Incoming Webhook**.</span></span>
1. <span data-ttu-id="8e4be-139">[ **構成** ] ボタンを選択し、名前を入力します。必要に応じて、webhook の画像アバターをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="8e4be-139">Select the **Configure** button, provide a name, and, optionally, upload an image avatar for your webhook.</span></span>
1. <span data-ttu-id="8e4be-140">ダイアログウィンドウには、チャネルにマップされる一意の URL が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4be-140">The dialog window will present a unique URL that will map to the channel.</span></span> <span data-ttu-id="8e4be-141">**URL をコピーして保存**することを確認し、外部のサービスに提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e4be-141">Make sure that you **copy and save the URL**—you will need to provide it to the outside service.</span></span>
1. <span data-ttu-id="8e4be-142">[ **完了** ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e4be-142">Select the **Done** button.</span></span> <span data-ttu-id="8e4be-143">Webhook はチームチャネルで利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="8e4be-143">The webhook will be available in the team channel.</span></span>

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a><span data-ttu-id="8e4be-144">Teams チャネルから受信 webhook を削除する</span><span class="sxs-lookup"><span data-stu-id="8e4be-144">Remove an incoming webhook from a Teams channel</span></span>

1. <span data-ttu-id="8e4be-145">Webhook が追加されたチャネルに移動し、トップナビゲーションバーから [(&#8226;&#8226;&#8226;)] *オプション* を選択します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-145">Navigate to the channel where the webhook was added and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="8e4be-146">ドロップダウンメニューから [ **コネクタ** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-146">Choose **Connectors** from the drop-down menu.</span></span>
1. <span data-ttu-id="8e4be-147">左側の [ **管理**] で、[ **構成済み**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-147">On the left, under **Manage**, choose **Configured**.</span></span>
1. <span data-ttu-id="8e4be-148">構成した *番号* を選択して、現在のコネクタの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-148">Select the *number Configured* to see a list of your current connectors.</span></span>
1. <span data-ttu-id="8e4be-149">削除するコネクタの横にある [ **管理** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-149">Select **Manage** next to the connector that you want to delete.</span></span>
1. <span data-ttu-id="8e4be-150">[ **削除** ] ボタンを選択すると、[ *構成の削除* ] ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e4be-150">Select the **Remove** button and you will be presented with a *Remove Configuration* dialog box.</span></span>
1. <span data-ttu-id="8e4be-151">必要に応じて、[ **削除** ] ボタンを選択する前に、ダイアログボックスのフィールドとチェックボックスを完了します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-151">Optionally, complete the dialog box fields and checkboxes prior to selecting the **Remove** button.</span></span> <span data-ttu-id="8e4be-152">Webhook はチームチャネルから削除されます。</span><span class="sxs-lookup"><span data-stu-id="8e4be-152">The webhook will be deleted from the team channel.</span></span>

## <a name="distribution"></a><span data-ttu-id="8e4be-153">分配</span><span class="sxs-lookup"><span data-stu-id="8e4be-153">Distribution</span></span>

<span data-ttu-id="8e4be-154">受信 webhook を配布するには、次の3つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="8e4be-154">You have three options for distributing your incoming webhook:</span></span>

* <span data-ttu-id="8e4be-155">チームの受信 webhook を直接設定します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-155">Set up an incoming webhook directly for your team.</span></span>
* <span data-ttu-id="8e4be-156">[構成] ページを追加し、 [O365 コネクタ](~/webhooks-and-connectors/how-to/connectors-creating.md)で受信 webhook をラップする</span><span class="sxs-lookup"><span data-stu-id="8e4be-156">Add a configuration page and wrap your incoming webhook in a [O365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md)</span></span>
* <span data-ttu-id="8e4be-157">[Appsource](~/concepts/deploy-and-publish/office-store-guidance.md)提出の一部として、コネクタをパッケージ化して発行します。</span><span class="sxs-lookup"><span data-stu-id="8e4be-157">Package and publish your Connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="learn-more"></a><span data-ttu-id="8e4be-158">詳細情報</span><span class="sxs-lookup"><span data-stu-id="8e4be-158">Learn more</span></span>

* [<span data-ttu-id="8e4be-159">コネクタと Web フックへのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="8e4be-159">Sending messages to Connectors and Webhooks</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
