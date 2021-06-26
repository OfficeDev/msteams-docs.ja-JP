---
title: 受信 Webhook の作成
author: laujan
description: 受信 Webhook をアプリに追加し、Teams Webhook を使用して外部要求をTeamsする方法について説明します。
keywords: teams タブ送信 Webhook
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 53fe9725148579325386fa4677bebb61fdb72c56
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140119"
---
# <a name="create-incoming-webhook"></a><span data-ttu-id="a88ae-104">受信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="a88ae-104">Create Incoming Webhook</span></span>

<span data-ttu-id="a88ae-105">受信 Webhook を使用すると、外部アプリがチャネル内のコンテンツTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-105">Incoming Webhook allows any external apps to share content in Teams channels.</span></span> <span data-ttu-id="a88ae-106">これらの Webhook は、追跡および通知ツールとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-106">These webhooks are used as tracking and notifying tools.</span></span> <span data-ttu-id="a88ae-107">これらは一意の URL を提供し、カード形式のメッセージを含む JSON ペイロードを送信します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-107">They provide a unique URL, to which you send a JSON payload with a message in card format.</span></span> <span data-ttu-id="a88ae-108">カードは、1 つのトピックに関連するコンテンツとアクションを含むユーザー インターフェイス コンテナーです。</span><span class="sxs-lookup"><span data-stu-id="a88ae-108">Cards are user interface containers that include content and actions related to a single topic.</span></span> <span data-ttu-id="a88ae-109">Teams機能内でカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-109">Teams use cards within the following capabilities:</span></span>

* <span data-ttu-id="a88ae-110">ボット</span><span class="sxs-lookup"><span data-stu-id="a88ae-110">Bots</span></span>
* <span data-ttu-id="a88ae-111">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="a88ae-111">Messaging extensions</span></span>
* <span data-ttu-id="a88ae-112">コネクタ</span><span class="sxs-lookup"><span data-stu-id="a88ae-112">Connectors</span></span>

## <a name="key-features-of-incoming-webhook"></a><span data-ttu-id="a88ae-113">受信 Webhook の主な機能</span><span class="sxs-lookup"><span data-stu-id="a88ae-113">Key features of Incoming Webhook</span></span>

<span data-ttu-id="a88ae-114">次の表に、受信 Webhook の機能と説明を示します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-114">The following table provides the features and description of Incoming Webhook:</span></span>

| <span data-ttu-id="a88ae-115">機能</span><span class="sxs-lookup"><span data-stu-id="a88ae-115">Features</span></span> | <span data-ttu-id="a88ae-116">説明</span><span class="sxs-lookup"><span data-stu-id="a88ae-116">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="a88ae-117">受信 Webhook を使用したアダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="a88ae-117">Adaptive Cards using an Incoming Webhook</span></span>|<span data-ttu-id="a88ae-118">アダプティブ カードは、受信 Webhooks 経由で送信できます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-118">Adaptive Cards can be sent through Incoming Webhooks.</span></span> <span data-ttu-id="a88ae-119">詳細については、「受信 [Webhooks を使用してアダプティブ カードを送信する」を参照してください](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)。</span><span class="sxs-lookup"><span data-stu-id="a88ae-119">For more information, see [Send Adaptive Cards using Incoming Webhooks](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook).</span></span>|
|<span data-ttu-id="a88ae-120">アクション可能なメッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="a88ae-120">Actionable messaging support</span></span>|<span data-ttu-id="a88ae-121">アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a88ae-121">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="a88ae-122">カードを介してメッセージを送信する場合は、操作可能なメッセージ カード形式を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a88ae-122">If you send messages through cards, you must use the actionable message card format.</span></span> <span data-ttu-id="a88ae-123">詳細については、「従来の操作可能な [メッセージ カード参照と](/outlook/actionable-messages/message-card-reference) メッセージ カード [のプレイグラウンド」を参照してください](https://messagecardplayground.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="a88ae-123">For more information, see [legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and [message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="a88ae-124">独立した HTTPS メッセージングのサポート</span><span class="sxs-lookup"><span data-stu-id="a88ae-124">Independent HTTPS messaging support</span></span>|<span data-ttu-id="a88ae-125">カードは、情報を明確に一貫して提供します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-125">Cards provide information clearly and consistently.</span></span> <span data-ttu-id="a88ae-126">HTTPS POST 要求を送信できる任意のツールまたはフレームワークは、受信 Webhook を介してTeamsにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-126">Any tool or framework that can send HTTPS POST requests, can send messages to Teams through an Incoming Webhook.</span></span>|
|<span data-ttu-id="a88ae-127">Markdown のサポート</span><span class="sxs-lookup"><span data-stu-id="a88ae-127">Markdown support</span></span>|<span data-ttu-id="a88ae-128">アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="a88ae-128">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="a88ae-129">カードで HTML マークアップを使用しない。</span><span class="sxs-lookup"><span data-stu-id="a88ae-129">Do not use HTML markup in your cards.</span></span> <span data-ttu-id="a88ae-130">HTML は無視され、プレーン テキストとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-130">HTML is ignored and treated as plain text.</span></span>|
|<span data-ttu-id="a88ae-131">スコープ構成</span><span class="sxs-lookup"><span data-stu-id="a88ae-131">Scoped configuration</span></span>|<span data-ttu-id="a88ae-132">受信 Webhook はスコープ設定され、チャネル レベルで構成されます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-132">Incoming Webhook is scoped and configured at the channel level.</span></span>|
|<span data-ttu-id="a88ae-133">セキュリティで保護されたリソース定義</span><span class="sxs-lookup"><span data-stu-id="a88ae-133">Secure resource definitions</span></span>|<span data-ttu-id="a88ae-134">メッセージは JSON ペイロードとして書式設定されます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-134">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="a88ae-135">この宣言型メッセージング構造は、悪意のあるコードの挿入を防止します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-135">This declarative messaging structure prevents the insertion of malicious code.</span></span>|

> [!NOTE]
> * <span data-ttu-id="a88ae-136">Teams、メッセージング拡張機能、受信 Webhook、およびボット フレームワークは、オープンクロスカード プラットフォーム フレームワークであるアダプティブ カードをサポートします。</span><span class="sxs-lookup"><span data-stu-id="a88ae-136">Teams bots, messaging extensions, Incoming Webhook, and the Bot Framework support Adaptive Cards, an open cross card platform framework.</span></span> <span data-ttu-id="a88ae-137">現在、Teams[は](../../webhooks-and-connectors/how-to/connectors-creating.md)アダプティブ カードをサポートしていない。</span><span class="sxs-lookup"><span data-stu-id="a88ae-137">Currently, [Teams connectors](../../webhooks-and-connectors/how-to/connectors-creating.md) do not support Adaptive Cards.</span></span> <span data-ttu-id="a88ae-138">ただし、アダプティブ カードを[チャネルに投稿](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)するフローをTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-138">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts Adaptive Cards to a Teams channel.</span></span>
> * <span data-ttu-id="a88ae-139">カードと Webhook の詳細については、「アダプティブ カード [と受信 Webhooks」を参照してください](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)。</span><span class="sxs-lookup"><span data-stu-id="a88ae-139">For more information on cards and webhooks, see [Adaptive cards and Incoming Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).</span></span>

## <a name="create-incoming-webhook"></a><span data-ttu-id="a88ae-140">受信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="a88ae-140">Create Incoming Webhook</span></span>

<span data-ttu-id="a88ae-141">**受信 Webhook を新しいチャネルにTeamsするには**</span><span class="sxs-lookup"><span data-stu-id="a88ae-141">**To add an Incoming Webhook to a Teams channel**</span></span>

1. <span data-ttu-id="a88ae-142">Webhook を追加するチャネルに移動し、上部の &#8226;&#8226;&#8226; から [その他 **の** オプション] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-142">Go to the channel where you want to add the webhook and select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="a88ae-143">ドロップダウン **メニューから [** コネクタ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-143">Select **Connectors** from the dropdown menu:</span></span>

    ![コネクタの選択](~/assets/images/connectors.png)

1. <span data-ttu-id="a88ae-145">受信 **Webhook を検索し、[** 追加] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="a88ae-145">Search for **Incoming Webhook** and select **Add**.</span></span>
1. <span data-ttu-id="a88ae-146">[ **構成]** を選択し、名前を指定し、必要に応じて webhook の画像をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="a88ae-146">Select **Configure**, provide a name, and upload an image for your webhook if required:</span></span>

    ![[構成] ボタン](~/assets/images/configure.png)

1. <span data-ttu-id="a88ae-148">ダイアログ ウィンドウには、チャネルにマップされる一意の URL が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-148">The dialog window presents a unique URL that maps to the channel.</span></span> <span data-ttu-id="a88ae-149">Webhook URL をコピーして保存し、ユーザーに情報を送信Microsoft Teamsし、[完了] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="a88ae-149">Copy and save the webhook URL, to send information to Microsoft Teams and select **Done**:</span></span>

    ![一意の URL](~/assets/images/url.png)

<span data-ttu-id="a88ae-151">Webhook は、webhook チャネルTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-151">The webhook is available in the Teams channel.</span></span>

> [!NOTE]
> <span data-ttu-id="a88ae-152">[Teams] で、[設定メンバーのアクセス許可] [コネクタの作成、更新、および削除をメンバーに許可する] を選択して、チーム メンバーがコネクタを追加、変更、または削除できます  >    >  。</span><span class="sxs-lookup"><span data-stu-id="a88ae-152">In Teams, select **Settings** > **Member permissions** > **Allow members to create, update, and remove connectors**, so that any team member can add, modify, or delete a connector.</span></span>

## <a name="remove-incoming-webhook"></a><span data-ttu-id="a88ae-153">受信 Webhook の削除</span><span class="sxs-lookup"><span data-stu-id="a88ae-153">Remove Incoming Webhook</span></span>

<span data-ttu-id="a88ae-154">**受信 Webhook をチャネルからTeamsするには**</span><span class="sxs-lookup"><span data-stu-id="a88ae-154">**To remove an Incoming Webhook from a Teams channel**</span></span>

1. <span data-ttu-id="a88ae-155">チャネルに移動します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-155">Go to the channel.</span></span>
1. <span data-ttu-id="a88ae-156">上部 &#8226;&#8226;&#8226; **バーから [その他のオプション** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-156">Select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="a88ae-157">ドロップダウン **メニューから [** コネクタ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-157">Select **Connectors** from the dropdown menu.</span></span>
1. <span data-ttu-id="a88ae-158">左側の [管理] で **、[構成** 済み] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="a88ae-158">On the left, under **Manage**, select **Configured**.</span></span>
1. <span data-ttu-id="a88ae-159">[構成 **< *済みの 1*>] を** 選択して、現在のコネクタの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-159">Select the **<*1*> Configured** to see a list of your current connectors:</span></span>

    ![構成済みの Webhook](~/assets/images/configured.png)

1. <span data-ttu-id="a88ae-161">削除 **するコネクタ** の横にある [管理] を選択します。</span><span class="sxs-lookup"><span data-stu-id="a88ae-161">Select **Manage** next to the connector that you want to remove:</span></span>

    ![Webhook の管理](~/assets/images/manage.png)

1. <span data-ttu-id="a88ae-163">[削除 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="a88ae-163">Select **Remove**:</span></span>

    ![Webhook を削除する](~/assets/images/remove.png)

    <span data-ttu-id="a88ae-165">[ **構成の削除]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-165">The **Remove Configuration** dialog box appears:</span></span>

    ![構成の削除](~/assets/images/removeconfiguration.png)

1. <span data-ttu-id="a88ae-167">ダイアログ ボックスのフィールドとチェック ボックスを入力し、[削除] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="a88ae-167">Complete the dialog box fields and checkboxes and select **Remove**:</span></span>

    ![最終的な削除](~/assets/images/finalremove.png)

    <span data-ttu-id="a88ae-169">webhook は、チャネルからTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="a88ae-169">The webhook is removed from the Teams channel.</span></span>

## <a name="see-also"></a><span data-ttu-id="a88ae-170">関連項目</span><span class="sxs-lookup"><span data-stu-id="a88ae-170">See also</span></span>

* [<span data-ttu-id="a88ae-171">送信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="a88ae-171">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [<span data-ttu-id="a88ae-172">Office 365 コネクタを作成する</span><span class="sxs-lookup"><span data-stu-id="a88ae-172">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="a88ae-173">メッセージを作成して送信する</span><span class="sxs-lookup"><span data-stu-id="a88ae-173">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
