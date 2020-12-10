---
title: 受信 Webhook を使用して外部リクエストを Microsoft Teams に投稿する
author: laujan
description: Teams アプリに受信 Webhook を追加する方法
keywords: Teams タブ 送信 Webhook*
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 3aa795170af9695fc375043c94e794f814b38646
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819068"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a><span data-ttu-id="79b78-104">受信 Webhook を使用して外部リクエストを Teams に投稿する</span><span class="sxs-lookup"><span data-stu-id="79b78-104">Post external requests to Teams with incoming webhooks</span></span>

## <a name="what-are-incoming-webhooks-in-teams"></a><span data-ttu-id="79b78-105">Teams での受信 Webhook とは</span><span class="sxs-lookup"><span data-stu-id="79b78-105">What are incoming webhooks in Teams?</span></span>

<span data-ttu-id="79b78-106">受信 Webhook は Teams の特別な種類のコネクタで、外部アプリがチーム チャネルでコンテンツを共有するためのシンプルな方法を提供し、時にはトラッキングや通知ツールとしても使用されます。</span><span class="sxs-lookup"><span data-stu-id="79b78-106">Incoming webhooks are special type of Connector in Teams that provide a simple way for an external app to share content in team channels and are often used as tracking and notification tools.</span></span> <span data-ttu-id="79b78-107">Teams は、投稿するメッセージと JSON ペイロードを通常カード形式で送信するための一意の URL を提供します。</span><span class="sxs-lookup"><span data-stu-id="79b78-107">Teams provides a unique URL to which you send a JSON payload with the message that you want to POST, typically in a card format.</span></span> <span data-ttu-id="79b78-108">カードは、ある 1 つのトピックに関連するコンテンツとアクションを含んだユーザー インターフェース (UI) コンテナであり、メッセージ データを一貫した方法で表示するための方法です。</span><span class="sxs-lookup"><span data-stu-id="79b78-108">Cards are user-interface (UI) containers that contain content and actions related to a single topic and are a way to present message data in a consistent way.</span></span> <span data-ttu-id="79b78-109">Teams は、次の 3 つの機能でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="79b78-109">Teams uses cards within three capabilities:</span></span>

* <span data-ttu-id="79b78-110">ボット</span><span class="sxs-lookup"><span data-stu-id="79b78-110">Bots</span></span>
* <span data-ttu-id="79b78-111">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="79b78-111">Messaging extensions</span></span>
* <span data-ttu-id="79b78-112">コネクタ</span><span class="sxs-lookup"><span data-stu-id="79b78-112">Connectors</span></span>

## <a name="incoming-webhook-key-features"></a><span data-ttu-id="79b78-113">受信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="79b78-113">Incoming webhook key features</span></span>

| <span data-ttu-id="79b78-114">機能</span><span class="sxs-lookup"><span data-stu-id="79b78-114">Feature</span></span> | <span data-ttu-id="79b78-115">説明</span><span class="sxs-lookup"><span data-stu-id="79b78-115">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="79b78-116">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="79b78-116">Scoped Configuration</span></span>|<span data-ttu-id="79b78-117">受信 Webhook にはスコープが設定されており、チャネル レベルで構成されます (例: 送信 Webhook はチーム レベルで構成されます)。</span><span class="sxs-lookup"><span data-stu-id="79b78-117">Incoming webhooks are scoped and configured at the channel level (e.g., outgoing webhooks are scoped and configured at the team level).</span></span>|
|<span data-ttu-id="79b78-118">セキュリティで保護されたリソース定義</span><span class="sxs-lookup"><span data-stu-id="79b78-118">Secure resource definitions</span></span>|<span data-ttu-id="79b78-119">メッセージは JSON ペイロードとして書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="79b78-119">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="79b78-120">この宣言メッセージング構造により、クライアントでコードが実行されることはないため、悪意のあるコードの挿入が防止されます。</span><span class="sxs-lookup"><span data-stu-id="79b78-120">This declarative messaging structure prevents the injection of malicious code as there is no code execution on the client.</span></span>|
|<span data-ttu-id="79b78-121">アクション可能なメッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="79b78-121">Actionable messaging support</span></span>|<span data-ttu-id="79b78-122">カード経由でメッセージを送信する場合は、**アクション可能なメッセージ カード** 形式を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="79b78-122">If you choose to send messages via cards, you must use the **actionable message card** format.</span></span> <span data-ttu-id="79b78-123">アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="79b78-123">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="79b78-124">こちらは、「[従来の操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/message-card-reference)」と「[メッセージ カードのプレイグラウンド](https://messagecardplayground.azurewebsites.net)」へのリンクです。</span><span class="sxs-lookup"><span data-stu-id="79b78-124">Here are links to the [Legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and the [Message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="79b78-125">独立した HTTPS メッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="79b78-125">Independent HTTPS messaging support</span></span>| <span data-ttu-id="79b78-126">カードは、明瞭で一貫した方法で情報を表示する優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="79b78-126">Cards are a great way to present information in a clear and consistent way.</span></span> <span data-ttu-id="79b78-127">HTTPS POST 要求を送信できるツールやフレームワークは、受信 Webhook を介して Teams にメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="79b78-127">Any tool or framework that can send HTTPS POST requests can send messages to Teams via an incoming webhook.</span></span>|
|<span data-ttu-id="79b78-128">Markdown のサポート</span><span class="sxs-lookup"><span data-stu-id="79b78-128">Markdown support</span></span>|<span data-ttu-id="79b78-129">アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="79b78-129">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="79b78-130">**カードには HTML マークアップを使用しないでください**。</span><span class="sxs-lookup"><span data-stu-id="79b78-130">**Don't use HTML markup in your cards**.</span></span> <span data-ttu-id="79b78-131">HTML は無視され、プレーン テキストとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="79b78-131">HTML is ignored and treated as plain text.</span></span>|

> [!Note]  
> <span data-ttu-id="79b78-132">Teams のボット、メッセージング拡張機能、Bot Framework は、オープンなクロスカード プラットフォーム フレームワークであるアダプティブ カードをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="79b78-132">Teams bots, messaging extensions, and the Bot Framework support Adaptive Cards, an open cross-card platform framework.</span></span> <span data-ttu-id="79b78-133">現在、Teams コネクタはアダプティブ カードをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="79b78-133">Teams connectors do not currently support Adaptive Cards.</span></span> <span data-ttu-id="79b78-134">ただし、Teams チャネルにアダプティブ カードを投稿する[フロー](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)を作成することは可能です。</span><span class="sxs-lookup"><span data-stu-id="79b78-134">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts adaptive cards to a Teams channel.</span></span>

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a><span data-ttu-id="79b78-135">Teams チャネルに受信 Webhook を追加する</span><span class="sxs-lookup"><span data-stu-id="79b78-135">Add an incoming webhook to a Teams channel</span></span>

> [!Important]  
> <span data-ttu-id="79b78-136">チームの **[設定]** => **[メンバーのアクセス許可]** => **[Allow members to create, update, and remove connectors]** (メンバーがコネクタを作成、更新、削除することを許可する) が選択されている場合、すべてのチーム メンバーがコネクタの追加、変更、削除を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="79b78-136">If your team's **Settings** => **Member permissions** => **Allow members to create, update, and remove connectors** is selected, any team member can add, modify, or delete a connector.</span></span>

1. <span data-ttu-id="79b78-137">Webhook を追加するチャネルに移動し、上部のナビゲーション バーから (&#8226;&#8226;&#8226;) *[その他のオプション]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="79b78-137">Navigate to the channel where you want to add the webhook and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="79b78-138">ドロップダウン メニューから **[コネクタ]** を選択し、**受信 Webhook** を検索します。</span><span class="sxs-lookup"><span data-stu-id="79b78-138">Choose **Connectors** from the drop-down menu and search for **Incoming Webhook**.</span></span>
1. <span data-ttu-id="79b78-139">**[構成]** ボタンを選択し、名前を入力し、オプションで Webhook 用の画像アバターをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="79b78-139">Select the **Configure** button, provide a name, and, optionally, upload an image avatar for your webhook.</span></span>
1. <span data-ttu-id="79b78-140">ダイアログ ウィンドウに、チャネルにマッピングされる一意の URL が表示されます。</span><span class="sxs-lookup"><span data-stu-id="79b78-140">The dialog window will present a unique URL that will map to the channel.</span></span> <span data-ttu-id="79b78-141">**URL をコピーして保存した** ことをご確認ください (URL は外部サービスに提供する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="79b78-141">Make sure that you **copy and save the URL**—you will need to provide it to the outside service.</span></span>
1. <span data-ttu-id="79b78-142">**[完了]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="79b78-142">Select the **Done** button.</span></span> <span data-ttu-id="79b78-143">Webhook が、チーム チャネルで利用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="79b78-143">The webhook will be available in the team channel.</span></span>

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a><span data-ttu-id="79b78-144">Teams チャネルから受信 Webhook を削除する</span><span class="sxs-lookup"><span data-stu-id="79b78-144">Remove an incoming webhook from a Teams channel</span></span>

1. <span data-ttu-id="79b78-145">Webhook が追加されたチャネルに移動し、上部のナビゲーション バーから (&#8226;&#8226;&#8226;) *[その他のオプション]* を選択します。</span><span class="sxs-lookup"><span data-stu-id="79b78-145">Navigate to the channel where the webhook was added and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="79b78-146">ドロップダウン メニューから **[コネクタ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="79b78-146">Choose **Connectors** from the drop-down menu.</span></span>
1. <span data-ttu-id="79b78-147">左側にある **[管理]** で、**[構成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="79b78-147">On the left, under **Manage**, choose **Configured**.</span></span>
1. <span data-ttu-id="79b78-148">*[number Configured]* (構成されている数) を選択すると、現在のコネクタの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="79b78-148">Select the *number Configured* to see a list of your current connectors.</span></span>
1. <span data-ttu-id="79b78-149">削除するコネクタの横にある **[管理]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="79b78-149">Select **Manage** next to the connector that you want to delete.</span></span>
1. <span data-ttu-id="79b78-150">**[削除]** ボタンを選択すると、*[構成の削除]* ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="79b78-150">Select the **Remove** button and you will be presented with a *Remove Configuration* dialog box.</span></span>
1. <span data-ttu-id="79b78-151">必要に応じて、**[削除]** ボタンを選択する前に、ダイアログ ボックスのフィールドとチェックボックスに入力を行います。</span><span class="sxs-lookup"><span data-stu-id="79b78-151">Optionally, complete the dialog box fields and checkboxes prior to selecting the **Remove** button.</span></span> <span data-ttu-id="79b78-152">Webhook が、チーム チャネルから削除されます。</span><span class="sxs-lookup"><span data-stu-id="79b78-152">The webhook will be deleted from the team channel.</span></span>

## <a name="distribution"></a><span data-ttu-id="79b78-153">配布</span><span class="sxs-lookup"><span data-stu-id="79b78-153">Distribution</span></span>

<span data-ttu-id="79b78-154">受信 Webhook の配布には、次の 3 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="79b78-154">You have three options for distributing your incoming webhook:</span></span>

* <span data-ttu-id="79b78-155">チームに受信 Webhook を直接セットアップする。</span><span class="sxs-lookup"><span data-stu-id="79b78-155">Set up an incoming webhook directly for your team.</span></span>
* <span data-ttu-id="79b78-156">構成ページを追加して、受信 Webhook を [O365 コネクタ](~/webhooks-and-connectors/how-to/connectors-creating.md)でラップする。</span><span class="sxs-lookup"><span data-stu-id="79b78-156">Add a configuration page and wrap your incoming webhook in a [O365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md)</span></span>
* <span data-ttu-id="79b78-157">[AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) への提出の一部としてコネクタをパッケージ化して公開する。</span><span class="sxs-lookup"><span data-stu-id="79b78-157">Package and publish your Connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="learn-more"></a><span data-ttu-id="79b78-158">詳細情報</span><span class="sxs-lookup"><span data-stu-id="79b78-158">Learn more</span></span>

* [<span data-ttu-id="79b78-159">コネクタと Webhook へのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="79b78-159">Sending messages to Connectors and Webhooks</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
