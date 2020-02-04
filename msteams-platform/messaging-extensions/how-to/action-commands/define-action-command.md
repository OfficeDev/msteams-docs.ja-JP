---
title: メッセージング拡張機能の操作コマンドを定義する
author: clearab
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7eb734258aa34c69fa34d1413b2d3dab88e0113a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674684"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="9ddea-103">メッセージング拡張機能の操作コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="9ddea-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="9ddea-104">アクションコマンドを使用すると、ユーザーにモーダルポップアップ (Teams でタスクモジュールと呼ばれる) を提示して、情報を収集または表示した後、その操作を処理して、情報を Teams に送信することができます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-104">Action commands allow you present your users with a modal popup (called a task module in Teams) to collect or display information, then process their interaction and send information back to Teams.</span></span> <span data-ttu-id="9ddea-105">コマンドを作成する前に、次のことを決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-105">Before creating your command you'll need to decide:</span></span>

1. <span data-ttu-id="9ddea-106">アクションコマンドはどこからトリガーされますか?</span><span class="sxs-lookup"><span data-stu-id="9ddea-106">Where can the action command be triggered from?</span></span>
1. <span data-ttu-id="9ddea-107">タスクモジュールはどのように作成されますか?</span><span class="sxs-lookup"><span data-stu-id="9ddea-107">How will the task module be created?</span></span>
1. <span data-ttu-id="9ddea-108">最終的なメッセージやカードは bot からチャネルに送信されるか、またはメッセージまたはカードが [メッセージの作成] 領域に挿入されて、ユーザーが送信できるようになりますか。</span><span class="sxs-lookup"><span data-stu-id="9ddea-108">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>

## <a name="choose-action-command-invoke-locations"></a><span data-ttu-id="9ddea-109">アクションコマンドの呼び出し場所を選択する</span><span class="sxs-lookup"><span data-stu-id="9ddea-109">Choose action command invoke locations</span></span>

<span data-ttu-id="9ddea-110">最初に決定する必要があるのは、アクションコマンドをトリガーする (または、より具体的に*呼び出す*) 方法です。</span><span class="sxs-lookup"><span data-stu-id="9ddea-110">The first thing you need to decide is where your action command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="9ddea-111">アプリマニフェスト`context`でを指定することで、コマンドを次の1つ以上の場所から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-111">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="9ddea-112">[メッセージの作成] 領域の下部にあるボタン。</span><span class="sxs-lookup"><span data-stu-id="9ddea-112">The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="9ddea-113">[コマンド] ボックスでアプリを @mentioning します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-113">By @mentioning your app in the command box.</span></span> <span data-ttu-id="9ddea-114">注: メッセージング拡張機能が [コマンド] ボックスから呼び出された場合、直接会話に挿入された bot メッセージで応答することはできません。</span><span class="sxs-lookup"><span data-stu-id="9ddea-114">Note: You cannot respond with a bot message inserted directly into the conversation if your messaging extension is invoked from the command box.</span></span>
* <span data-ttu-id="9ddea-115">既存のメッセージから直接使用する...メッセージのオーバーフローメニュー。</span><span class="sxs-lookup"><span data-stu-id="9ddea-115">Directly from an existing message via the ... overflow menu on a message.</span></span> <span data-ttu-id="9ddea-116">注: bot への最初の呼び出しには、呼び出し元のメッセージが含まれる JSON オブジェクトが含まれています。これは、タスクモジュールで提供する前に処理できます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-116">Note: The initial invoke to your bot will include a JSON object containing the message from which it was invoked, which you can process before presenting them with a task module.</span></span>

## <a name="choose-how-to-build-your-task-module"></a><span data-ttu-id="9ddea-117">タスクモジュールの作成方法を選択する</span><span class="sxs-lookup"><span data-stu-id="9ddea-117">Choose how to build your task module</span></span>

<span data-ttu-id="9ddea-118">でコマンドを起動する場所を選択することに加えて、ユーザーのタスクモジュールでフォームにデータを入力する方法も選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-118">In addition to choosing where your command can be invoked from, you must also chose how to populate the form in the task module for your users.</span></span> <span data-ttu-id="9ddea-119">タスクモジュール内にレンダリングされるフォームを作成するには、次の3つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-119">You have three options for creating the form that is rendered inside the task module:</span></span>

* <span data-ttu-id="9ddea-120">**パラメーターの静的リスト**-これは最も簡単なオプションです。</span><span class="sxs-lookup"><span data-stu-id="9ddea-120">**Static list of parameters** - This is the simplest option.</span></span> <span data-ttu-id="9ddea-121">Teams クライアントが表示するアプリマニフェストにパラメータ (入力フィールド) のリストを定義することができます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-121">You can define a list of parameters (input fields) in your app manifest the Teams client will render.</span></span> <span data-ttu-id="9ddea-122">このオプションを使用して書式設定を制御することはできません。</span><span class="sxs-lookup"><span data-stu-id="9ddea-122">You cannot control the formatting with this option.</span></span>
* <span data-ttu-id="9ddea-123">**アダプティブカード**-アダプティブカードを使用することもできますが、UI をより詳細に制御することができますが、使用可能なコントロールと書式設定のオプションには制限があります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-123">**Adaptive card** - You can choose to use an adaptive card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="9ddea-124">**埋め込み web ビュー** -UI とコントロールを完全に制御する必要がある場合は、タスクモジュールにカスタム web ビューを埋め込むことを選択できます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-124">**Embedded web view** - If you need complete control over the UI and controls, you can choose to embed a custom web view in the task module.</span></span>

<span data-ttu-id="9ddea-125">パラメーターの静的リストを使用してタスクモジュールを作成する場合は、ユーザーがタスクモジュールを送信するときに、メッセージング拡張機能の最初の呼び出しが行われます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-125">If you choose to create your task module with a static list of parameters, the first call to your messaging extension will be when a user submits the task module.</span></span> <span data-ttu-id="9ddea-126">埋め込まれた web ビューまたはアダプティブカードを使用する場合、メッセージング拡張機能では、ユーザーからの初期 invoke イベントを処理し、タスクモジュールを作成して、クライアントに戻す必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-126">When using an embedded web view or an adaptive card, your messaging extension will need to handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="choose-how-the-final-message-will-be-sent"></a><span data-ttu-id="9ddea-127">最終メッセージが送信される方法を選択する</span><span class="sxs-lookup"><span data-stu-id="9ddea-127">Choose how the final message will be sent</span></span>

<span data-ttu-id="9ddea-128">ほとんどの場合、アクションコマンドによって、作成メッセージボックスにカードが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-128">In most cases, your action command will result in a card inserted into the compose message box.</span></span> <span data-ttu-id="9ddea-129">その後、ユーザーはチャネルまたはチャットに送信するかどうかを決定できます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-129">Your user can then decide to send it into the channel or chat.</span></span> <span data-ttu-id="9ddea-130">この例のメッセージはユーザーからのものであり、bot はカードをさらに編集または更新することはできません。</span><span class="sxs-lookup"><span data-stu-id="9ddea-130">The message in this case comes from the user, and your bot will not be able to edit or update the card further.</span></span>

<span data-ttu-id="9ddea-131">メッセージング拡張機能が [新規作成] ボックスから、または直接メッセージからトリガーされる場合、web サービスは直接チャネルまたはチャットに最終的な応答を挿入できます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-131">If your messaging extension is triggered from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="9ddea-132">この場合、adaptive card は bot からのものであり、bot が更新できるようになります。また、必要に応じて、ボットが会話スレッドに応答することもできます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-132">In this case, the adaptive card comes from the bot, the bot will be able to update it, and can the bot can also reply to the conversation thread if needed.</span></span> <span data-ttu-id="9ddea-133">同じ Id を使用して`bot`アプリケーションマニフェストにオブジェクトを追加し、適切なスコープを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-133">You will need to add the `bot` object to your app manifest using the same Id and defining the appropriate scopes.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="9ddea-134">アプリケーションマニフェストにコマンドを追加する</span><span class="sxs-lookup"><span data-stu-id="9ddea-134">Add the command to your app manifest</span></span>

<span data-ttu-id="9ddea-135">ユーザーがアクションコマンドを操作する方法を決定したので、それをアプリのマニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-135">Now that you've decided how users will interact with your action command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="9ddea-136">これを行うには、アプリマニフェスト`composeExtension` JSON の最上位レベルに新しいオブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-136">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="9ddea-137">そのためには、アプリ Studio のヘルプを使用するか、手動で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-137">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="9ddea-138">アプリ Studio を使用してコマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="9ddea-138">Create a command using App Studio</span></span>

<span data-ttu-id="9ddea-139">次の手順では、[メッセージング拡張機能が](~/messaging-extensions/how-to/create-messaging-extension.md)既に作成済みであることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="9ddea-139">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="9ddea-140">Microsoft Teams クライアントから、 **App Studio**を開き、[**マニフェストエディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-140">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="9ddea-141">アプリパッケージが既にアプリ Studio で作成されている場合は、一覧から選択します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-141">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="9ddea-142">それ以外の場合は、既存のアプリパッケージをインポートできます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-142">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="9ddea-143">[コマンド] セクションの [**追加**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="9ddea-143">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="9ddea-144">[**ユーザーが Teams 内で外部サービスのアクションを開始できるようにする**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span></span>
5. <span data-ttu-id="9ddea-145">静的パラメーターセットを使用してタスクモジュールを作成する場合は、そのオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-145">If you want to use a static set of parameters to create your task module, select that option.</span></span> <span data-ttu-id="9ddea-146">それ以外の場合は、 **bot からパラメーターの動的セットを取得**することを選択します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-146">Otherwise, choose to **Fetch a dynamic set of parameters from your bot**.</span></span>
6. <span data-ttu-id="9ddea-147">**コマンド Id**と**タイトル**を追加します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-147">Add a **Command Id** and a **Title**.</span></span>
7. <span data-ttu-id="9ddea-148">アクションコマンドを起動する場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-148">Select where you want your action command to be triggered from.</span></span>
8. <span data-ttu-id="9ddea-149">タスクモジュールのパラメーターを使用している場合は、最初のパラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-149">If you're using parameters for your task module, add the first one.</span></span>
9. <span data-ttu-id="9ddea-150">Click Save</span><span class="sxs-lookup"><span data-stu-id="9ddea-150">Click Save</span></span>
10. <span data-ttu-id="9ddea-151">さらにパラメーターを追加する必要がある場合は、[ **parameters** ] セクションの [**追加**] ボタンをクリックして追加します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-151">If you need to add more parameters, click the **Add** button in the **Parameters** section to add them.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="9ddea-152">コマンドを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="9ddea-152">Manually create a command</span></span>

<span data-ttu-id="9ddea-153">アクションベースのメッセージング拡張コマンドをアプリのマニフェストに手動で追加するには、オブジェクトの`composeExtension.commands`配列に follow パラメーターを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-153">To manually add your action-based messaging extension command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="9ddea-154">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="9ddea-154">Property name</span></span> | <span data-ttu-id="9ddea-155">用途</span><span class="sxs-lookup"><span data-stu-id="9ddea-155">Purpose</span></span> | <span data-ttu-id="9ddea-156">必須</span><span class="sxs-lookup"><span data-stu-id="9ddea-156">Required?</span></span> | <span data-ttu-id="9ddea-157">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="9ddea-157">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="9ddea-158">このコマンドに割り当てる一意の ID です。</span><span class="sxs-lookup"><span data-stu-id="9ddea-158">Unique ID that you assign to this command.</span></span> <span data-ttu-id="9ddea-159">ユーザー要求には、この ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-159">The user request will include this ID.</span></span> | <span data-ttu-id="9ddea-160">はい</span><span class="sxs-lookup"><span data-stu-id="9ddea-160">Yes</span></span> | <span data-ttu-id="9ddea-161">1.0</span><span class="sxs-lookup"><span data-stu-id="9ddea-161">1.0</span></span> |
| `title` | <span data-ttu-id="9ddea-162">コマンド名を指定します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-162">Command name.</span></span> <span data-ttu-id="9ddea-163">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-163">This value appears in the UI.</span></span> | <span data-ttu-id="9ddea-164">はい</span><span class="sxs-lookup"><span data-stu-id="9ddea-164">Yes</span></span> | <span data-ttu-id="9ddea-165">1.0</span><span class="sxs-lookup"><span data-stu-id="9ddea-165">1.0</span></span> |
| `type` | <span data-ttu-id="9ddea-166">にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9ddea-166">Must be `action`</span></span> | <span data-ttu-id="9ddea-167">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-167">No</span></span> | <span data-ttu-id="9ddea-168">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-168">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="9ddea-169">`true`作業モジュールのアダプティブカードまたは埋め込み web ビューの場合`false` 、パラメーターの静的なリスト、または web ビューを読み込むときに`taskInfo`</span><span class="sxs-lookup"><span data-stu-id="9ddea-169">`true` for an adaptive card or embedded web view for your task module, `false` for a static list of parameters or when loading the web view by a `taskInfo`</span></span> | <span data-ttu-id="9ddea-170">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-170">No</span></span> | <span data-ttu-id="9ddea-171">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-171">1.4</span></span> |
| `context` | <span data-ttu-id="9ddea-172">メッセージング拡張機能を呼び出すことができる場所を定義する値のオプションの配列です。</span><span class="sxs-lookup"><span data-stu-id="9ddea-172">Optional array of values that defines where the messaging extension can be invoked from.</span></span> <span data-ttu-id="9ddea-173">可能な値`message`は`compose`、、 `commandBox`、です。</span><span class="sxs-lookup"><span data-stu-id="9ddea-173">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="9ddea-174">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="9ddea-174">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="9ddea-175">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-175">No</span></span> | <span data-ttu-id="9ddea-176">1.5</span><span class="sxs-lookup"><span data-stu-id="9ddea-176">1.5</span></span> |

<span data-ttu-id="9ddea-177">パラメーターの静的な一覧を使用している場合は、それらも追加します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-177">If you are using a static list of parameters, you'll add them as well.</span></span>

| <span data-ttu-id="9ddea-178">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="9ddea-178">Property name</span></span> | <span data-ttu-id="9ddea-179">用途</span><span class="sxs-lookup"><span data-stu-id="9ddea-179">Purpose</span></span> | <span data-ttu-id="9ddea-180">必須</span><span class="sxs-lookup"><span data-stu-id="9ddea-180">Required?</span></span> | <span data-ttu-id="9ddea-181">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="9ddea-181">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="9ddea-182">コマンドのパラメーターの静的リスト。</span><span class="sxs-lookup"><span data-stu-id="9ddea-182">Static list of parameters for the command.</span></span> <span data-ttu-id="9ddea-183">がである`fetchTask`場合にのみ使用`false`</span><span class="sxs-lookup"><span data-stu-id="9ddea-183">Only use when `fetchTask` is `false`</span></span> | <span data-ttu-id="9ddea-184">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-184">No</span></span> | <span data-ttu-id="9ddea-185">1.0</span><span class="sxs-lookup"><span data-stu-id="9ddea-185">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="9ddea-186">パラメーターの名前です。</span><span class="sxs-lookup"><span data-stu-id="9ddea-186">The name of the parameter.</span></span> <span data-ttu-id="9ddea-187">これは、ユーザーの要求でサービスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-187">This is sent to your service in the user request.</span></span> | <span data-ttu-id="9ddea-188">はい</span><span class="sxs-lookup"><span data-stu-id="9ddea-188">Yes</span></span> | <span data-ttu-id="9ddea-189">1.0</span><span class="sxs-lookup"><span data-stu-id="9ddea-189">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="9ddea-190">このパラメーターの目的または提供する必要がある値の例について説明します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-190">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="9ddea-191">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-191">This value appears in the UI.</span></span> | <span data-ttu-id="9ddea-192">はい</span><span class="sxs-lookup"><span data-stu-id="9ddea-192">Yes</span></span> | <span data-ttu-id="9ddea-193">1.0</span><span class="sxs-lookup"><span data-stu-id="9ddea-193">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="9ddea-194">簡単なユーザーフレンドリパラメーターのタイトルまたはラベル。</span><span class="sxs-lookup"><span data-stu-id="9ddea-194">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="9ddea-195">はい</span><span class="sxs-lookup"><span data-stu-id="9ddea-195">Yes</span></span> | <span data-ttu-id="9ddea-196">1.0</span><span class="sxs-lookup"><span data-stu-id="9ddea-196">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="9ddea-197">必要な入力の種類を設定します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-197">Set to the type of input required.</span></span> <span data-ttu-id="9ddea-198">可能な値`text`は`textarea`、 `number` `date` `time`、、、 `toggle`、です。</span><span class="sxs-lookup"><span data-stu-id="9ddea-198">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="9ddea-199">既定値はに設定されています`text`</span><span class="sxs-lookup"><span data-stu-id="9ddea-199">Default is set to `text`</span></span> | <span data-ttu-id="9ddea-200">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-200">No</span></span> | <span data-ttu-id="9ddea-201">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-201">1.4</span></span> |

<span data-ttu-id="9ddea-202">埋め込みの web ビューを使用している場合は、必要`taskInfo`に応じて、bot を直接呼び出すことなく web ビューを取得するために、オブジェクトを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="9ddea-202">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="9ddea-203">このオプションを使用する場合の動作は、ボットとの最初の操作が[タスクモジュール送信アクションに応答](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)するという点で、パラメータの静的なリストを使用するのと似ています。</span><span class="sxs-lookup"><span data-stu-id="9ddea-203">If you choose to use this option, the behavior is similar to using a static list of parameters in that the first interaction with your bot will be [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="9ddea-204">`taskInfo`オブジェクトを使用している場合は、 `fetchTask`パラメーターもに`false`設定してください。</span><span class="sxs-lookup"><span data-stu-id="9ddea-204">If you are using a `taskInfo` object, be sure to also set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="9ddea-205">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="9ddea-205">Property name</span></span> | <span data-ttu-id="9ddea-206">用途</span><span class="sxs-lookup"><span data-stu-id="9ddea-206">Purpose</span></span> | <span data-ttu-id="9ddea-207">必須</span><span class="sxs-lookup"><span data-stu-id="9ddea-207">Required?</span></span> | <span data-ttu-id="9ddea-208">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="9ddea-208">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="9ddea-209">メッセージ拡張コマンドの使用時にプリロードするタスクモジュールを指定する</span><span class="sxs-lookup"><span data-stu-id="9ddea-209">Specify the task module to preload when using a messaging extension command</span></span>| <span data-ttu-id="9ddea-210">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-210">No</span></span> | <span data-ttu-id="9ddea-211">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-211">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="9ddea-212">最初のタスクモジュールタイトル</span><span class="sxs-lookup"><span data-stu-id="9ddea-212">Initial task module title</span></span>|<span data-ttu-id="9ddea-213">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-213">No</span></span> | <span data-ttu-id="9ddea-214">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-214">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="9ddea-215">タスクモジュールの幅-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-215">Task module width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="9ddea-216">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-216">No</span></span> | <span data-ttu-id="9ddea-217">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-217">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="9ddea-218">タスクモジュールの高さ-数値をピクセル単位で指定するか、' large '、' medium '、または ' small ' などの既定のレイアウトにします。</span><span class="sxs-lookup"><span data-stu-id="9ddea-218">Task module height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="9ddea-219">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-219">No</span></span> | <span data-ttu-id="9ddea-220">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-220">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="9ddea-221">最初の web ビューの URL</span><span class="sxs-lookup"><span data-stu-id="9ddea-221">Initial web view URL</span></span>|<span data-ttu-id="9ddea-222">いいえ</span><span class="sxs-lookup"><span data-stu-id="9ddea-222">No</span></span> | <span data-ttu-id="9ddea-223">1.4</span><span class="sxs-lookup"><span data-stu-id="9ddea-223">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="9ddea-224">アプリマニフェストの例</span><span class="sxs-lookup"><span data-stu-id="9ddea-224">App manifest example</span></span>

<span data-ttu-id="9ddea-225">2つのアクションコマンドを定義`composeExtensions`するオブジェクトの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-225">The below is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="9ddea-226">完全なマニフェストの例として、完全なアプリマニフェストスキーマについては、「 [app manifest スキーマ](~/resources/schema/manifest-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9ddea-226">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": false,
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
      }
    ]
  }
]
...
```

## <a name="next-steps"></a><span data-ttu-id="9ddea-227">次のステップ</span><span class="sxs-lookup"><span data-stu-id="9ddea-227">Next steps</span></span>

<span data-ttu-id="9ddea-228">アダプティブカードを使用している場合、またはオブジェクトを`taskInfo`持たない埋め込み web ビューを使用している場合は、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-228">If you are using either an adaptive card or an embedded web view without a `taskInfo` object, you'll want to:</span></span>

* [<span data-ttu-id="9ddea-229">タスクモジュールを作成して応答する</span><span class="sxs-lookup"><span data-stu-id="9ddea-229">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="9ddea-230">パラメーターを使用している場合、または`taskInfo`オブジェクトに埋め込まれた web ビューを使用している場合は、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="9ddea-230">If you are using parameters or an embedded web view with a `taskInfo` object, the next step for you is to:</span></span>

* [<span data-ttu-id="9ddea-231">タスクモジュール送信に応答する</span><span class="sxs-lookup"><span data-stu-id="9ddea-231">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
