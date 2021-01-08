---
title: メッセージング拡張機能のアクション コマンドを定義する
author: clearab
description: メッセージング拡張機能アクション コマンドの概要
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: be2135477c4234187f374aef215f90e8329fb74e
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778402"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="2543d-103">メッセージング拡張機能のアクション コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="2543d-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="2543d-104">操作コマンドを使用すると、情報を収集または表示するためのモーダル ポップアップ (Teams ではタスク モジュールと呼びます) をユーザーに表示し、対話を処理した後 Teams に情報を送り返すことができます。</span><span class="sxs-lookup"><span data-stu-id="2543d-104">Action commands allow you present your users with a modal popup (called a task module in Teams) to collect or display information, then process their interaction and send information back to Teams.</span></span> <span data-ttu-id="2543d-105">コマンドを作成する前に、以下を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2543d-105">Before creating your command you'll need to decide:</span></span>

1. <span data-ttu-id="2543d-106">アクション コマンドはどこから実行できますか?</span><span class="sxs-lookup"><span data-stu-id="2543d-106">Where can the action command be triggered from?</span></span>
1. <span data-ttu-id="2543d-107">タスク モジュールの作成方法</span><span class="sxs-lookup"><span data-stu-id="2543d-107">How will the task module be created?</span></span>
1. <span data-ttu-id="2543d-108">最後のメッセージまたはカードがボットからチャネルに送信されるのか、それともユーザーが送信するメッセージ作成領域にメッセージまたはカードが挿入されるのか。</span><span class="sxs-lookup"><span data-stu-id="2543d-108">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>

## <a name="choose-action-command-invoke-locations"></a><span data-ttu-id="2543d-109">操作コマンドの呼び出し場所を選択する</span><span class="sxs-lookup"><span data-stu-id="2543d-109">Choose action command invoke locations</span></span>

<span data-ttu-id="2543d-110">最初に決定する必要があるのは、アクション コマンドをトリガーできる場所 (具体的には呼び出し) *です*。</span><span class="sxs-lookup"><span data-stu-id="2543d-110">The first thing you need to decide is where your action command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="2543d-111">アプリ マニフェストでコマンドを指定すると、次の 1 つ以上の場所 `context` からコマンドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="2543d-111">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="2543d-112">メッセージ作成領域の下部にあるボタン。</span><span class="sxs-lookup"><span data-stu-id="2543d-112">The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="2543d-113">コマンド @mentioningでアプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="2543d-113">By @mentioning your app in the command box.</span></span> <span data-ttu-id="2543d-114">注: メッセージング拡張機能がコマンド ボックスから呼び出された場合、会話にボット メッセージを直接挿入して応答することはできません。</span><span class="sxs-lookup"><span data-stu-id="2543d-114">Note: You cannot respond with a bot message inserted directly into the conversation if your messaging extension is invoked from the command box.</span></span>
* <span data-ttu-id="2543d-115">... を介して既存のメッセージから直接メッセージのオーバーフロー メニュー。</span><span class="sxs-lookup"><span data-stu-id="2543d-115">Directly from an existing message via the ... overflow menu on a message.</span></span> <span data-ttu-id="2543d-116">注: ボットに対する最初の呼び出しには、呼び出されたメッセージを含む JSON オブジェクトが含まれます。このオブジェクトは、タスク モジュールを表示する前に処理できます。</span><span class="sxs-lookup"><span data-stu-id="2543d-116">Note: The initial invoke to your bot will include a JSON object containing the message from which it was invoked, which you can process before presenting them with a task module.</span></span>

## <a name="choose-how-to-build-your-task-module"></a><span data-ttu-id="2543d-117">タスク モジュールの作成方法を選択する</span><span class="sxs-lookup"><span data-stu-id="2543d-117">Choose how to build your task module</span></span>

<span data-ttu-id="2543d-118">コマンドを呼び出すことができる場所を選択する以外に、ユーザーのタスク モジュールでフォームにデータを入力する方法も選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2543d-118">In addition to choosing where your command can be invoked from, you must also chose how to populate the form in the task module for your users.</span></span> <span data-ttu-id="2543d-119">タスク モジュール内でレンダリングされるフォームを作成するには、次の 3 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="2543d-119">You have three options for creating the form that is rendered inside the task module:</span></span>

* <span data-ttu-id="2543d-120">**パラメーターの静的リスト** - これは最も簡単なオプションです。</span><span class="sxs-lookup"><span data-stu-id="2543d-120">**Static list of parameters** - This is the simplest option.</span></span> <span data-ttu-id="2543d-121">アプリ マニフェストで、Teams クライアントがレンダリングするパラメーター (入力フィールド) の一覧を定義できます。</span><span class="sxs-lookup"><span data-stu-id="2543d-121">You can define a list of parameters (input fields) in your app manifest the Teams client will render.</span></span> <span data-ttu-id="2543d-122">このオプションでは書式設定を制御できません。</span><span class="sxs-lookup"><span data-stu-id="2543d-122">You cannot control the formatting with this option.</span></span>
* <span data-ttu-id="2543d-123">**アダプティブ カード** - アダプティブ カードの使用を選択できます。アダプティブ カードを使って UI を詳細に制御できますが、使用可能なコントロールと書式設定オプションは制限されます。</span><span class="sxs-lookup"><span data-stu-id="2543d-123">**Adaptive card** - You can choose to use an adaptive card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="2543d-124">**埋め込み Web ビュー** - UI とコントロールを完全に制御する必要がある場合は、タスク モジュールにカスタム Web ビューを埋め込む方法を選択できます。</span><span class="sxs-lookup"><span data-stu-id="2543d-124">**Embedded web view** - If you need complete control over the UI and controls, you can choose to embed a custom web view in the task module.</span></span>

<span data-ttu-id="2543d-125">パラメーターの静的リストを使用してタスク モジュールを作成する場合、メッセージング拡張機能への最初の呼び出しは、ユーザーがタスク モジュールを送信するときに行います。</span><span class="sxs-lookup"><span data-stu-id="2543d-125">If you choose to create your task module with a static list of parameters, the first call to your messaging extension will be when a user submits the task module.</span></span> <span data-ttu-id="2543d-126">埋め込み Web ビューまたはアダプティブ カードを使用する場合、メッセージング拡張機能は、ユーザーからの最初の呼び出しイベントを処理し、タスク モジュールを作成して、それをクライアントに返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="2543d-126">When using an embedded web view or an adaptive card, your messaging extension will need to handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="choose-how-the-final-message-will-be-sent"></a><span data-ttu-id="2543d-127">最後のメッセージの送信方法を選択する</span><span class="sxs-lookup"><span data-stu-id="2543d-127">Choose how the final message will be sent</span></span>

<span data-ttu-id="2543d-128">ほとんどの場合、アクション コマンドを実行すると、メッセージの作成ボックスにカードが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="2543d-128">In most cases, your action command will result in a card inserted into the compose message box.</span></span> <span data-ttu-id="2543d-129">その後、ユーザーはチャネルまたはチャットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="2543d-129">Your user can then decide to send it into the channel or chat.</span></span> <span data-ttu-id="2543d-130">この場合のメッセージはユーザーから送信され、ボットはそれ以上カードの編集や更新を行えなされません。</span><span class="sxs-lookup"><span data-stu-id="2543d-130">The message in this case comes from the user, and your bot will not be able to edit or update the card further.</span></span>

<span data-ttu-id="2543d-131">メッセージング拡張機能が作成ボックスまたはメッセージから直接トリガーされた場合、Web サービスは最後の応答をチャネルまたはチャットに直接挿入できます。</span><span class="sxs-lookup"><span data-stu-id="2543d-131">If your messaging extension is triggered from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="2543d-132">この場合、アダプティブ カードはボットから提供され、ボットはボットを更新し、必要に応じてボットも会話スレッドに返信できます。</span><span class="sxs-lookup"><span data-stu-id="2543d-132">In this case, the adaptive card comes from the bot, the bot will be able to update it, and the bot can also reply to the conversation thread if needed.</span></span> <span data-ttu-id="2543d-133">同じ ID を使用してアプリ マニフェストにオブジェクトを追加し、適切なスコープ `bot` を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2543d-133">You will need to add the `bot` object to your app manifest using the same Id and defining the appropriate scopes.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="2543d-134">アプリ マニフェストにコマンドを追加する</span><span class="sxs-lookup"><span data-stu-id="2543d-134">Add the command to your app manifest</span></span>

<span data-ttu-id="2543d-135">これで、ユーザーがアクション コマンドを操作する方法が決まったので、次にアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="2543d-135">Now that you've decided how users will interact with your action command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="2543d-136">これを行うには、アプリ マニフェスト JSON のトップ レベルに新 `composeExtension` しいオブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="2543d-136">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="2543d-137">これを行うには、App Studio の支援を受けるか、手動で行います。</span><span class="sxs-lookup"><span data-stu-id="2543d-137">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="2543d-138">App Studio を使用してコマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="2543d-138">Create a command using App Studio</span></span>

<span data-ttu-id="2543d-139">次の手順では、メッセージング拡張機能が [既に作成済みである必要があります](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="2543d-139">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="2543d-140">Microsoft Teams クライアントから App **Studio** を開き、[マニフェスト エディター] **タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="2543d-140">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="2543d-141">App Studio で既にアプリ パッケージを作成している場合は、一覧からアプリ パッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="2543d-141">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="2543d-142">インポートされていない場合は、既存のアプリ パッケージをインポートできます。</span><span class="sxs-lookup"><span data-stu-id="2543d-142">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="2543d-143">[コマンド] **セクション** の [追加] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2543d-143">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="2543d-144">**Choose Allow users to trigger actions in external services while inside of Teams**.</span><span class="sxs-lookup"><span data-stu-id="2543d-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span></span>
5. <span data-ttu-id="2543d-145">静的なパラメーター セットを使用してタスク モジュールを作成する場合は、そのオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2543d-145">If you want to use a static set of parameters to create your task module, select that option.</span></span> <span data-ttu-id="2543d-146">それ以外の場合は、 **ボットからパラメーターの動的セットをフェッチします**。</span><span class="sxs-lookup"><span data-stu-id="2543d-146">Otherwise, choose to **Fetch a dynamic set of parameters from your bot**.</span></span>
6. <span data-ttu-id="2543d-147">コマンド ID **とタイトル** を追加 **します**。</span><span class="sxs-lookup"><span data-stu-id="2543d-147">Add a **Command Id** and a **Title**.</span></span>
7. <span data-ttu-id="2543d-148">アクション コマンドをトリガーする場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="2543d-148">Select where you want your action command to be triggered from.</span></span>
8. <span data-ttu-id="2543d-149">タスク モジュールのパラメーターを使用している場合は、最初のパラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="2543d-149">If you're using parameters for your task module, add the first one.</span></span>
9. <span data-ttu-id="2543d-150">Click Save</span><span class="sxs-lookup"><span data-stu-id="2543d-150">Click Save</span></span>
10. <span data-ttu-id="2543d-151">パラメーターを追加する必要がある場合は、[パラメーター  ] セクションの [追加]**ボタンをクリック** して追加します。</span><span class="sxs-lookup"><span data-stu-id="2543d-151">If you need to add more parameters, click the **Add** button in the **Parameters** section to add them.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="2543d-152">コマンドを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="2543d-152">Manually create a command</span></span>

<span data-ttu-id="2543d-153">アクション ベースのメッセージング拡張機能コマンドをアプリ マニフェストに手動で追加するには、オブジェクトの配列に次のパラメーター `composeExtension.commands` を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2543d-153">To manually add your action-based messaging extension command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="2543d-154">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="2543d-154">Property name</span></span> | <span data-ttu-id="2543d-155">用途</span><span class="sxs-lookup"><span data-stu-id="2543d-155">Purpose</span></span> | <span data-ttu-id="2543d-156">必須</span><span class="sxs-lookup"><span data-stu-id="2543d-156">Required?</span></span> | <span data-ttu-id="2543d-157">最小マニフェスト バージョン</span><span class="sxs-lookup"><span data-stu-id="2543d-157">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="2543d-158">このコマンドに割り当てる一意の ID。</span><span class="sxs-lookup"><span data-stu-id="2543d-158">Unique ID that you assign to this command.</span></span> <span data-ttu-id="2543d-159">ユーザー要求には、この ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2543d-159">The user request will include this ID.</span></span> | <span data-ttu-id="2543d-160">はい</span><span class="sxs-lookup"><span data-stu-id="2543d-160">Yes</span></span> | <span data-ttu-id="2543d-161">1.0</span><span class="sxs-lookup"><span data-stu-id="2543d-161">1.0</span></span> |
| `title` | <span data-ttu-id="2543d-162">コマンド名。</span><span class="sxs-lookup"><span data-stu-id="2543d-162">Command name.</span></span> <span data-ttu-id="2543d-163">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2543d-163">This value appears in the UI.</span></span> | <span data-ttu-id="2543d-164">はい</span><span class="sxs-lookup"><span data-stu-id="2543d-164">Yes</span></span> | <span data-ttu-id="2543d-165">1.0</span><span class="sxs-lookup"><span data-stu-id="2543d-165">1.0</span></span> |
| `type` | <span data-ttu-id="2543d-166">にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2543d-166">Must be `action`</span></span> | <span data-ttu-id="2543d-167">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-167">No</span></span> | <span data-ttu-id="2543d-168">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-168">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="2543d-169">`true`タスク モジュール用のアダプティブ カードビューまたは埋め込み Web ビュー用、パラメーターの静的リスト用、または `false``taskInfo`</span><span class="sxs-lookup"><span data-stu-id="2543d-169">`true` for an adaptive card or embedded web view for your task module, `false` for a static list of parameters or when loading the web view by a `taskInfo`</span></span> | <span data-ttu-id="2543d-170">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-170">No</span></span> | <span data-ttu-id="2543d-171">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-171">1.4</span></span> |
| `context` | <span data-ttu-id="2543d-172">メッセージング拡張機能を呼び出すことができる場所を定義する値のオプションの配列。</span><span class="sxs-lookup"><span data-stu-id="2543d-172">Optional array of values that defines where the messaging extension can be invoked from.</span></span> <span data-ttu-id="2543d-173">指定できる値 `message` は `compose` 、,, または `commandBox` です。</span><span class="sxs-lookup"><span data-stu-id="2543d-173">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="2543d-174">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="2543d-174">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="2543d-175">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-175">No</span></span> | <span data-ttu-id="2543d-176">1.5</span><span class="sxs-lookup"><span data-stu-id="2543d-176">1.5</span></span> |

<span data-ttu-id="2543d-177">静的なパラメーターの一覧を使用している場合は、パラメーターも追加します。</span><span class="sxs-lookup"><span data-stu-id="2543d-177">If you are using a static list of parameters, you'll add them as well.</span></span>

| <span data-ttu-id="2543d-178">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="2543d-178">Property name</span></span> | <span data-ttu-id="2543d-179">用途</span><span class="sxs-lookup"><span data-stu-id="2543d-179">Purpose</span></span> | <span data-ttu-id="2543d-180">必須</span><span class="sxs-lookup"><span data-stu-id="2543d-180">Required?</span></span> | <span data-ttu-id="2543d-181">最小マニフェスト バージョン</span><span class="sxs-lookup"><span data-stu-id="2543d-181">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="2543d-182">コマンドのパラメーターの静的リスト。</span><span class="sxs-lookup"><span data-stu-id="2543d-182">Static list of parameters for the command.</span></span> <span data-ttu-id="2543d-183">次の場合にのみ使用 `fetchTask` します。 `false`</span><span class="sxs-lookup"><span data-stu-id="2543d-183">Only use when `fetchTask` is `false`</span></span> | <span data-ttu-id="2543d-184">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-184">No</span></span> | <span data-ttu-id="2543d-185">1.0</span><span class="sxs-lookup"><span data-stu-id="2543d-185">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="2543d-186">パラメーターの名前です。</span><span class="sxs-lookup"><span data-stu-id="2543d-186">The name of the parameter.</span></span> <span data-ttu-id="2543d-187">これは、ユーザー要求でサービスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="2543d-187">This is sent to your service in the user request.</span></span> | <span data-ttu-id="2543d-188">はい</span><span class="sxs-lookup"><span data-stu-id="2543d-188">Yes</span></span> | <span data-ttu-id="2543d-189">1.0</span><span class="sxs-lookup"><span data-stu-id="2543d-189">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="2543d-190">このパラメーターの目的、または指定する値の例について説明します。</span><span class="sxs-lookup"><span data-stu-id="2543d-190">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="2543d-191">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2543d-191">This value appears in the UI.</span></span> | <span data-ttu-id="2543d-192">はい</span><span class="sxs-lookup"><span data-stu-id="2543d-192">Yes</span></span> | <span data-ttu-id="2543d-193">1.0</span><span class="sxs-lookup"><span data-stu-id="2543d-193">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="2543d-194">短いユーザー フレンドリーなパラメータータイトルまたはラベル。</span><span class="sxs-lookup"><span data-stu-id="2543d-194">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="2543d-195">はい</span><span class="sxs-lookup"><span data-stu-id="2543d-195">Yes</span></span> | <span data-ttu-id="2543d-196">1.0</span><span class="sxs-lookup"><span data-stu-id="2543d-196">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="2543d-197">必要な入力の種類に設定します。</span><span class="sxs-lookup"><span data-stu-id="2543d-197">Set to the type of input required.</span></span> <span data-ttu-id="2543d-198">使用できる値 `text` は `textarea` 、 , , , , `number` , `date` , `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="2543d-198">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="2543d-199">既定値は次の値に設定されます。 `text`</span><span class="sxs-lookup"><span data-stu-id="2543d-199">Default is set to `text`</span></span> | <span data-ttu-id="2543d-200">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-200">No</span></span> | <span data-ttu-id="2543d-201">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-201">1.4</span></span> |

<span data-ttu-id="2543d-202">埋め込み Web ビューを使用している場合は、必要に応じて、ボットを直接呼び出さずに Web ビューをフェッチするオブジェクト `taskInfo` を追加できます。</span><span class="sxs-lookup"><span data-stu-id="2543d-202">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="2543d-203">このオプションを使用する場合の動作は、ボットとの最初の対話がタスク モジュールの送信アクションに応答するという点で、静的なパラメーターの一覧を使用するのと [似ています](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。</span><span class="sxs-lookup"><span data-stu-id="2543d-203">If you choose to use this option, the behavior is similar to using a static list of parameters in that the first interaction with your bot will be [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="2543d-204">オブジェクトを使用している場合 `taskInfo` は、パラメーターも必ず次の値に `fetchTask` 設定してください `false` 。</span><span class="sxs-lookup"><span data-stu-id="2543d-204">If you are using a `taskInfo` object, be sure to also set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="2543d-205">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="2543d-205">Property name</span></span> | <span data-ttu-id="2543d-206">用途</span><span class="sxs-lookup"><span data-stu-id="2543d-206">Purpose</span></span> | <span data-ttu-id="2543d-207">必須</span><span class="sxs-lookup"><span data-stu-id="2543d-207">Required?</span></span> | <span data-ttu-id="2543d-208">最小マニフェスト バージョン</span><span class="sxs-lookup"><span data-stu-id="2543d-208">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="2543d-209">メッセージング拡張機能コマンドを使用するときにプリロードするタスク モジュールを指定する</span><span class="sxs-lookup"><span data-stu-id="2543d-209">Specify the task module to preload when using a messaging extension command</span></span>| <span data-ttu-id="2543d-210">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-210">No</span></span> | <span data-ttu-id="2543d-211">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-211">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="2543d-212">初期タスク モジュールのタイトル</span><span class="sxs-lookup"><span data-stu-id="2543d-212">Initial task module title</span></span>|<span data-ttu-id="2543d-213">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-213">No</span></span> | <span data-ttu-id="2543d-214">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-214">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="2543d-215">タスク モジュールの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、'small' など)</span><span class="sxs-lookup"><span data-stu-id="2543d-215">Task module width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="2543d-216">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-216">No</span></span> | <span data-ttu-id="2543d-217">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-217">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="2543d-218">タスク モジュールの高さ - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、'small' など)</span><span class="sxs-lookup"><span data-stu-id="2543d-218">Task module height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="2543d-219">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-219">No</span></span> | <span data-ttu-id="2543d-220">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-220">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="2543d-221">初期 Web ビューの URL</span><span class="sxs-lookup"><span data-stu-id="2543d-221">Initial web view URL</span></span>|<span data-ttu-id="2543d-222">いいえ</span><span class="sxs-lookup"><span data-stu-id="2543d-222">No</span></span> | <span data-ttu-id="2543d-223">1.4</span><span class="sxs-lookup"><span data-stu-id="2543d-223">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="2543d-224">アプリ マニフェストの例</span><span class="sxs-lookup"><span data-stu-id="2543d-224">App manifest example</span></span>

<span data-ttu-id="2543d-225">2 つのアクション コマンドを定義 `composeExtensions` するオブジェクトの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2543d-225">The below is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="2543d-226">完全なマニフェストの例ではありません。完全なアプリ マニフェスト スキーマについては、「アプリ マニフェスト スキーマ」 [を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="2543d-226">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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
        "fetchTask": true,
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

## <a name="next-steps"></a><span data-ttu-id="2543d-227">次の手順</span><span class="sxs-lookup"><span data-stu-id="2543d-227">Next steps</span></span>

<span data-ttu-id="2543d-228">オブジェクトを使わずにアダプティブ カードまたは埋め込み Web ビューを使う場合は、次の `taskInfo` 方法があります。</span><span class="sxs-lookup"><span data-stu-id="2543d-228">If you are using either an adaptive card or an embedded web view without a `taskInfo` object, you'll want to:</span></span>

* [<span data-ttu-id="2543d-229">タスク モジュールを作成して応答する</span><span class="sxs-lookup"><span data-stu-id="2543d-229">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="2543d-230">パラメーターまたは埋め込み Web ビューをオブジェクトと一緒に使用している場合は、次の `taskInfo` 手順で次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2543d-230">If you are using parameters or an embedded web view with a `taskInfo` object, the next step for you is to:</span></span>

* [<span data-ttu-id="2543d-231">タスク モジュールの送信に応答する</span><span class="sxs-lookup"><span data-stu-id="2543d-231">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
