---
title: 受信 Webhook を使用して外部リクエストを Microsoft Teams に投稿する
author: surbhigupta
description: Teams アプリに受信 Webhook を追加する方法
keywords: teams タブ送信 Webhook
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: acaf2c7ba8c9c6d34399b51f3c0ef9a1110c0fb4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068936"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a><span data-ttu-id="7983b-104">受信 Webhook を使用して外部リクエストを Teams に投稿する</span><span class="sxs-lookup"><span data-stu-id="7983b-104">Post external requests to Teams with incoming webhooks</span></span>

## <a name="what-are-incoming-webhooks-in-teams"></a><span data-ttu-id="7983b-105">Teams での受信 Webhook とは</span><span class="sxs-lookup"><span data-stu-id="7983b-105">What are incoming webhooks in Teams?</span></span>

<span data-ttu-id="7983b-106">受信 Webhook は Teams の特別な種類のコネクタで、外部アプリがチーム チャネルでコンテンツを共有するためのシンプルな方法を提供し、時にはトラッキングや通知ツールとしても使用されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-106">Incoming webhooks are special type of Connector in Teams that provide a simple way for an external app to share content in team channels and are often used as tracking and notification tools.</span></span> <span data-ttu-id="7983b-107">Teams は、投稿するメッセージと JSON ペイロードを通常カード形式で送信するための一意の URL を提供します。</span><span class="sxs-lookup"><span data-stu-id="7983b-107">Teams provides a unique URL to which you send a JSON payload with the message that you want to POST, typically in a card format.</span></span> <span data-ttu-id="7983b-108">カードは、ある 1 つのトピックに関連するコンテンツとアクションを含んだユーザー インターフェース (UI) コンテナであり、メッセージ データを一貫した方法で表示するための方法です。</span><span class="sxs-lookup"><span data-stu-id="7983b-108">Cards are user-interface (UI) containers that contain content and actions related to a single topic and are a way to present message data in a consistent way.</span></span> <span data-ttu-id="7983b-109">Teams は、次の 3 つの機能でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="7983b-109">Teams uses cards within three capabilities:</span></span>

* <span data-ttu-id="7983b-110">ボット</span><span class="sxs-lookup"><span data-stu-id="7983b-110">Bots</span></span>
* <span data-ttu-id="7983b-111">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="7983b-111">Messaging extensions</span></span>
* <span data-ttu-id="7983b-112">コネクタ</span><span class="sxs-lookup"><span data-stu-id="7983b-112">Connectors</span></span>

## <a name="incoming-webhook-key-features"></a><span data-ttu-id="7983b-113">受信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="7983b-113">Incoming webhook key features</span></span>

| <span data-ttu-id="7983b-114">機能</span><span class="sxs-lookup"><span data-stu-id="7983b-114">Feature</span></span> | <span data-ttu-id="7983b-115">説明</span><span class="sxs-lookup"><span data-stu-id="7983b-115">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="7983b-116">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="7983b-116">Scoped Configuration</span></span>|<span data-ttu-id="7983b-117">受信 Webhook はスコープ設定され、チャネル レベルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-117">Incoming webhooks are scoped and configured at the channel level.</span></span> <span data-ttu-id="7983b-118">たとえば、送信 Webhook はスコープ設定され、チーム レベルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-118">For example, outgoing webhooks are scoped and configured at the team level.</span></span>|
|<span data-ttu-id="7983b-119">セキュリティで保護されたリソース定義</span><span class="sxs-lookup"><span data-stu-id="7983b-119">Secure resource definitions</span></span>|<span data-ttu-id="7983b-120">メッセージは JSON ペイロードとして書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-120">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="7983b-121">この宣言メッセージング構造により、クライアントでコードが実行されることはないため、悪意のあるコードの挿入が防止されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-121">This declarative messaging structure prevents the injection of malicious code as there is no code execution on the client.</span></span>|
|<span data-ttu-id="7983b-122">アクション可能なメッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="7983b-122">Actionable messaging support</span></span>|<span data-ttu-id="7983b-123">カード経由でメッセージを送信する場合は、**アクション可能なメッセージ カード** 形式を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7983b-123">If you choose to send messages via cards, you must use the **actionable message card** format.</span></span> <span data-ttu-id="7983b-124">アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7983b-124">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="7983b-125">こちらは、「[従来の操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/message-card-reference)」と「[メッセージ カードのプレイグラウンド](https://messagecardplayground.azurewebsites.net)」へのリンクです。</span><span class="sxs-lookup"><span data-stu-id="7983b-125">Here are links to the [Legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and the [Message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="7983b-126">独立した HTTPS メッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="7983b-126">Independent HTTPS messaging support</span></span>| <span data-ttu-id="7983b-127">カードは、明瞭で一貫した方法で情報を表示する優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="7983b-127">Cards are a great way to present information in a clear and consistent way.</span></span> <span data-ttu-id="7983b-128">HTTPS POST 要求を送信できるツールやフレームワークは、受信 Webhook を介して Teams にメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="7983b-128">Any tool or framework that can send HTTPS POST requests can send messages to Teams via an incoming webhook.</span></span>|
|<span data-ttu-id="7983b-129">Markdown のサポート</span><span class="sxs-lookup"><span data-stu-id="7983b-129">Markdown support</span></span>|<span data-ttu-id="7983b-130">アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7983b-130">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="7983b-131">**カードには HTML マークアップを使用しないでください**。</span><span class="sxs-lookup"><span data-stu-id="7983b-131">**Don't use HTML markup in your cards**.</span></span> <span data-ttu-id="7983b-132">HTML は無視され、プレーン テキストとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="7983b-132">HTML is ignored and treated as plain text.</span></span>|

> [!Note]
> <span data-ttu-id="7983b-133">Teams、メッセージング拡張機能、受信 Webhook、および Bot Framework は、オープンなクロスカード プラットフォーム フレームワークであるアダプティブ カードをサポートします。</span><span class="sxs-lookup"><span data-stu-id="7983b-133">Teams bots, messaging extensions, incoming webhooks, and the Bot Framework support Adaptive Cards, an open cross-card platform framework.</span></span> <span data-ttu-id="7983b-134">[Teamsアダプティブ カード](../../webhooks-and-connectors/how-to/connectors-creating.md)は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="7983b-134">[Teams connectors](../../webhooks-and-connectors/how-to/connectors-creating.md) do not currently support Adaptive Cards.</span></span> <span data-ttu-id="7983b-135">ただし、アダプティブ カードを[チャネルに投稿](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)するフローをTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="7983b-135">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts Adaptive Cards to a Teams channel.</span></span>

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a><span data-ttu-id="7983b-136">Teams チャネルに受信 Webhook を追加する</span><span class="sxs-lookup"><span data-stu-id="7983b-136">Add an incoming webhook to a Teams channel</span></span>

> [!Important]  
> <span data-ttu-id="7983b-137">チームの **[設定]** => **[メンバーのアクセス許可]** => **[Allow members to create, update, and remove connectors]** (メンバーがコネクタを作成、更新、削除することを許可する) が選択されている場合、すべてのチーム メンバーがコネクタの追加、変更、削除を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7983b-137">If your team's **Settings** => **Member permissions** => **Allow members to create, update, and remove connectors** is selected, any team member can add, modify, or delete a connector.</span></span>

<span data-ttu-id="7983b-138">**受信 Webhook を追加するには**</span><span class="sxs-lookup"><span data-stu-id="7983b-138">**To add an incoming webhook**</span></span>

1. <span data-ttu-id="7983b-139">Webhook を追加するチャネルに移動し、上部のナビゲーション バーから (&#8226;&#8226;&#8226;) *[その他のオプション]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="7983b-139">Navigate to the channel where you want to add the webhook and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="7983b-140">ドロップダウン メニューから **[コネクタ]** を選択し、**受信 Webhook** を検索します。</span><span class="sxs-lookup"><span data-stu-id="7983b-140">Choose **Connectors** from the drop-down menu and search for **Incoming Webhook**.</span></span>
1. <span data-ttu-id="7983b-141">**[構成]** ボタンを選択し、名前を入力し、オプションで Webhook 用の画像アバターをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="7983b-141">Select the **Configure** button, provide a name, and, optionally, upload an image avatar for your webhook.</span></span>
1. <span data-ttu-id="7983b-142">ダイアログ ウィンドウに、チャネルにマッピングされる一意の URL が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-142">The dialog window will present a unique URL that will map to the channel.</span></span> <span data-ttu-id="7983b-143">**URL をコピーして保存した** ことをご確認ください (URL は外部サービスに提供する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="7983b-143">Make sure that you **copy and save the URL**—you will need to provide it to the outside service.</span></span>
1. <span data-ttu-id="7983b-144">**[完了]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="7983b-144">Select the **Done** button.</span></span> <span data-ttu-id="7983b-145">Webhook が、チーム チャネルで利用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="7983b-145">The webhook will be available in the team channel.</span></span>

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a><span data-ttu-id="7983b-146">Teams チャネルから受信 Webhook を削除する</span><span class="sxs-lookup"><span data-stu-id="7983b-146">Remove an incoming webhook from a Teams channel</span></span>

<span data-ttu-id="7983b-147">**受信 Webhook を削除するには**</span><span class="sxs-lookup"><span data-stu-id="7983b-147">**To remove an incoming webhook**</span></span>

1. <span data-ttu-id="7983b-148">Webhook が追加されたチャネルに移動し、上部のナビゲーション バーから (&#8226;&#8226;&#8226;) *[その他のオプション]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="7983b-148">Navigate to the channel where the webhook was added and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="7983b-149">ドロップダウン メニューから **[コネクタ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7983b-149">Choose **Connectors** from the drop-down menu.</span></span>
1. <span data-ttu-id="7983b-150">左側にある **[管理]** で、**[構成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7983b-150">On the left, under **Manage**, choose **Configured**.</span></span>
1. <span data-ttu-id="7983b-151">*[number Configured]* (構成されている数) を選択すると、現在のコネクタの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-151">Select the *number Configured* to see a list of your current connectors.</span></span>
1. <span data-ttu-id="7983b-152">削除するコネクタの横にある **[管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7983b-152">Select **Manage** next to the connector that you want to delete.</span></span>
1. <span data-ttu-id="7983b-153">**[削除]** ボタンを選択すると、*[構成の削除]* ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-153">Select the **Remove** button and you will be presented with a *Remove Configuration* dialog box.</span></span>
1. <span data-ttu-id="7983b-154">必要に応じて、**[削除]** ボタンを選択する前に、ダイアログ ボックスのフィールドとチェックボックスに入力を行います。</span><span class="sxs-lookup"><span data-stu-id="7983b-154">Optionally, complete the dialog box fields and checkboxes prior to selecting the **Remove** button.</span></span> <span data-ttu-id="7983b-155">Webhook が、チーム チャネルから削除されます。</span><span class="sxs-lookup"><span data-stu-id="7983b-155">The webhook will be deleted from the team channel.</span></span>

## <a name="distribution"></a><span data-ttu-id="7983b-156">配布</span><span class="sxs-lookup"><span data-stu-id="7983b-156">Distribution</span></span>

<span data-ttu-id="7983b-157">受信 Webhook の配布には、次の 3 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="7983b-157">You have three options for distributing your incoming webhook:</span></span>

* <span data-ttu-id="7983b-158">チームに受信 Webhook を直接セットアップする。</span><span class="sxs-lookup"><span data-stu-id="7983b-158">Set up an incoming webhook directly for your team.</span></span>
* <span data-ttu-id="7983b-159">構成ページを追加して、受信 Webhook を [O365 コネクタ](~/webhooks-and-connectors/how-to/connectors-creating.md)でラップする。</span><span class="sxs-lookup"><span data-stu-id="7983b-159">Add a configuration page and wrap your incoming webhook in a [O365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md)</span></span>
* <span data-ttu-id="7983b-160">[AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) への提出の一部としてコネクタをパッケージ化して公開する。</span><span class="sxs-lookup"><span data-stu-id="7983b-160">Package and publish your Connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="see-also"></a><span data-ttu-id="7983b-161">関連項目</span><span class="sxs-lookup"><span data-stu-id="7983b-161">See also</span></span>

[<span data-ttu-id="7983b-162">コネクタと Webhook へのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="7983b-162">Sending messages to Connectors and Webhooks</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
