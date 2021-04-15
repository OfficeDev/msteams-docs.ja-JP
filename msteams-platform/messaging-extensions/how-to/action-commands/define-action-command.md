---
title: メッセージング拡張機能アクション コマンドの定義
author: clearab
description: メッセージング拡張機能アクション コマンドの概要
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 51c2ce5ac3b8ab265d9bec0b1101ba18138a9365
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696950"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="1965e-103">メッセージング拡張機能アクション コマンドの定義</span><span class="sxs-lookup"><span data-stu-id="1965e-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="1965e-104">アクション コマンドを使用すると、Teams のタスク モジュールと呼ばれるモーダル ポップアップをユーザーに表示できます。</span><span class="sxs-lookup"><span data-stu-id="1965e-104">Action commands allow you to present your users with a modal popup called a task module in Teams.</span></span> <span data-ttu-id="1965e-105">タスク モジュールは、情報を収集または表示し、対話を処理し、その情報を Teams に送信します。</span><span class="sxs-lookup"><span data-stu-id="1965e-105">The task module collects or displays information, processes the interaction and sends the information back to Teams.</span></span> <span data-ttu-id="1965e-106">このドキュメントでは、アクション コマンドの呼び出し場所の選択、タスク モジュールの作成、最終メッセージまたはカードの送信、アプリ スタジオを使用したアクション コマンドの作成、または手動での作成方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1965e-106">This document guides you on how to select action command invoke locations, create your task module, send final message, or card, create action command using app studio, or create it manually.</span></span> 

<span data-ttu-id="1965e-107">アクション コマンドを作成する前に、次の要素を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-107">Before creating the action command you must decide the following factors:</span></span>

1. [<span data-ttu-id="1965e-108">アクション コマンドはどこからトリガーできますか?</span><span class="sxs-lookup"><span data-stu-id="1965e-108">Where can the action command be triggered from?</span></span>](#select-action-command-invoke-locations)
1. [<span data-ttu-id="1965e-109">タスク モジュールの作成方法</span><span class="sxs-lookup"><span data-stu-id="1965e-109">How will the task module be created?</span></span>](#select-how-to-create-your-task-module)
1. [<span data-ttu-id="1965e-110">最終的なメッセージまたはカードはボットからチャネルに送信されますか、それともメッセージまたはカードがユーザーが送信するメッセージの作成領域に挿入されますか?</span><span class="sxs-lookup"><span data-stu-id="1965e-110">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a><span data-ttu-id="1965e-111">Select action command invoke locations</span><span class="sxs-lookup"><span data-stu-id="1965e-111">Select action command invoke locations</span></span>

<span data-ttu-id="1965e-112">まず、アクション コマンドを呼び出す場所を決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-112">First, you must decide the location from where your action command must be invoked.</span></span> <span data-ttu-id="1965e-113">アプリ マニフェストで指定すると、次の 1 つ以上の場所からコマンド `context` を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="1965e-113">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="1965e-114">メッセージの作成領域: 作成メッセージ領域の下部にあるボタン。</span><span class="sxs-lookup"><span data-stu-id="1965e-114">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="1965e-115">[コマンド] ボックス: @mentioningボックスにアプリを追加します。</span><span class="sxs-lookup"><span data-stu-id="1965e-115">Command box: By @mentioning your app in the command box.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="1965e-116">コマンド ボックスからメッセージング拡張機能が呼び出された場合は、ボット メッセージをスレッドに直接挿入して応答できません。</span><span class="sxs-lookup"><span data-stu-id="1965e-116">If messaging extension is invoked from the command box, you cannot respond with a bot message inserted directly into the conversation.</span></span>

* <span data-ttu-id="1965e-117">メッセージ: 既存のメッセージから、メッセージのオーバーフロー `...` メニューから直接移動します。</span><span class="sxs-lookup"><span data-stu-id="1965e-117">Message: Directly from an existing message through the `...` overflow menu on a message.</span></span> 
    > [!NOTE] 
    > <span data-ttu-id="1965e-118">ボットへの最初の呼び出しには、呼び出されたメッセージを含む JSON オブジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="1965e-118">The initial invoke to your bot includes a JSON object containing the message from which it was invoked.</span></span> <span data-ttu-id="1965e-119">メッセージをタスク モジュールで表示する前に、メッセージを処理できます。</span><span class="sxs-lookup"><span data-stu-id="1965e-119">You can process the message before presenting them with a task module.</span></span>

<span data-ttu-id="1965e-120">次の図は、アクション コマンドが呼び出された場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-120">The following image displays the locations from where action command is invoked:</span></span>

![action コマンドの呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a><span data-ttu-id="1965e-122">タスク モジュールの作成方法を選択する</span><span class="sxs-lookup"><span data-stu-id="1965e-122">Select how to create your task module</span></span>

<span data-ttu-id="1965e-123">コマンドの呼び出し先を選択する以外に、ユーザーのタスク モジュールにフォームを設定する方法も選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-123">In addition to selecting where your command can be invoked from, you must also select how to populate the form in the task module for your users.</span></span> <span data-ttu-id="1965e-124">タスク モジュール内でレンダリングされるフォームを作成するには、次の 3 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="1965e-124">You have the following three options for creating the form that is rendered inside the task module:</span></span>   

* <span data-ttu-id="1965e-125">**パラメーターの静的な一覧**: これは最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="1965e-125">**Static list of parameters**: This is the simplest method.</span></span> <span data-ttu-id="1965e-126">アプリ マニフェストで Teams クライアントがレンダリングするパラメーターの一覧を定義できますが、この場合は書式設定を制御できません。</span><span class="sxs-lookup"><span data-stu-id="1965e-126">You can define a list of parameters in your app manifest the Teams client renders, but cannot control the formatting in this case.</span></span>
* <span data-ttu-id="1965e-127">**アダプティブ カード**: アダプティブ カードの使用を選択すると、UI の制御が向上しますが、使用可能なコントロールと書式設定オプションは制限されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-127">**Adaptive Card**:  You can select to use an Adaptive Card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="1965e-128">**埋め込み Web ビュー**: カスタム Web ビューをタスク モジュールに埋め込み、UI とコントロールを完全に制御できます。</span><span class="sxs-lookup"><span data-stu-id="1965e-128">**Embedded web view**: You can select to embed a custom web view in the task module to have a complete control over the UI and controls.</span></span> 

<span data-ttu-id="1965e-129">パラメーターの静的リストを使用してタスク モジュールを作成する場合、ユーザーがタスク モジュールを送信すると、メッセージング拡張機能が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-129">If you select to create the task module with a static list of parameters and when the user submits the task module, the messaging extension is called.</span></span> <span data-ttu-id="1965e-130">埋め込み Web ビューまたはアダプティブ カードを使用する場合、メッセージング拡張機能は、ユーザーからの最初の呼び出しイベントを処理し、タスク モジュールを作成し、クライアントに戻す必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-130">When using an embedded web view or an Adaptive Card, your messaging extension must handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="select-how-the-final-message-is-sent"></a><span data-ttu-id="1965e-131">最終メッセージの送信方法を選択する</span><span class="sxs-lookup"><span data-stu-id="1965e-131">Select how the final message is sent</span></span>

<span data-ttu-id="1965e-132">ほとんどの場合、アクション コマンドを実行すると、作成メッセージ ボックスにカードが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-132">In most cases, the action command results in a card inserted into the compose message box.</span></span> <span data-ttu-id="1965e-133">ユーザーはチャネルまたはチャットに送信できます。</span><span class="sxs-lookup"><span data-stu-id="1965e-133">The user can send it into the channel or chat.</span></span> <span data-ttu-id="1965e-134">この場合、メッセージはユーザーから送信され、ボットはカードをさらに編集または更新できません。</span><span class="sxs-lookup"><span data-stu-id="1965e-134">In this case, the message comes from the user, and the bot cannot edit or update the card further.</span></span>

<span data-ttu-id="1965e-135">メッセージング拡張機能が作成ボックスから、またはメッセージから直接呼び出された場合、Web サービスは最終的な応答をチャネルまたはチャットに直接挿入できます。</span><span class="sxs-lookup"><span data-stu-id="1965e-135">If the messaging extension is invoked from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="1965e-136">この場合、アダプティブ カードはボットから取得され、ボットによって更新され、必要に応じてスレッドに返信されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-136">In this case, the Adaptive Card comes from the bot, the bot updates it, and replies to the conversation thread if needed.</span></span> <span data-ttu-id="1965e-137">同じ ID を使用して適切なスコープを定義して、アプリ マニフェストに `bot` オブジェクトを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-137">You must add the `bot` object to the app manifest using  the same ID and defining the appropriate scopes.</span></span>

## <a name="add-the-action-command-to-your-app-manifest"></a><span data-ttu-id="1965e-138">アクション コマンドをアプリ マニフェストに追加する</span><span class="sxs-lookup"><span data-stu-id="1965e-138">Add the action command to your app manifest</span></span>

<span data-ttu-id="1965e-139">アクション コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON のトップ レベルに新しいオブジェクト `composeExtension` を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-139">To add the action command to the app manifest, you must add a new `composeExtension` object to the top level of the app manifest JSON.</span></span> <span data-ttu-id="1965e-140">これを行うには、次のいずれかの方法を使用できます。</span><span class="sxs-lookup"><span data-stu-id="1965e-140">You can use one of the following ways to do so:</span></span>

* [<span data-ttu-id="1965e-141">App Studio を使用してアクション コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="1965e-141">Create an action command using App Studio</span></span>](#create-an-action-command-using-app-studio)
* [<span data-ttu-id="1965e-142">アクション コマンドを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="1965e-142">Create an action command manually</span></span>](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a><span data-ttu-id="1965e-143">App Studio を使用してアクション コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="1965e-143">Create an action command using App Studio</span></span>

> [!NOTE]
> <span data-ttu-id="1965e-144">アクション コマンドを作成する前提条件は、メッセージング拡張機能を既に作成している必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-144">The prerequisite to create an action command is that you have already created a messaging extension.</span></span> <span data-ttu-id="1965e-145">メッセージング拡張機能を作成する方法の詳細については、「Create [a messaging extension 」を参照してください](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="1965e-145">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="1965e-146">**アクション コマンドを作成するには**</span><span class="sxs-lookup"><span data-stu-id="1965e-146">**To create an action command**</span></span>

1. <span data-ttu-id="1965e-147">Microsoft **Teams クライアントから App Studio** を開き、[マニフェスト エディター] **タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="1965e-147">Open **App Studio** from the Microsoft Teams client and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="1965e-148">App Studio でアプリ パッケージを既に作成している **場合** は、一覧からアプリ パッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="1965e-148">If you already created your app package in **App Studio**, select it from the list.</span></span> <span data-ttu-id="1965e-149">アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。</span><span class="sxs-lookup"><span data-stu-id="1965e-149">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="1965e-150">アプリ パッケージをインポートした後、[機能] で [ **メッセージング拡張機能]** **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1965e-150">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="1965e-151">メッセージング拡張機能を設定するポップアップ ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-151">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="1965e-152">ウィンドウ **で [セットアップ** ] を選択して、メッセージング拡張機能をアプリ エクスペリエンスに含めます。</span><span class="sxs-lookup"><span data-stu-id="1965e-152">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="1965e-153">次の図は、メッセージング拡張機能のセットアップ ウィンドウを表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-153">The following image displays the messaging extension set up window:</span></span>

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. <span data-ttu-id="1965e-154">メッセージング拡張機能を作成するには、Microsoft 登録済みのボットが必要です。</span><span class="sxs-lookup"><span data-stu-id="1965e-154">To create a messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="1965e-155">既存のボットを使用するか、新しいボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="1965e-155">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="1965e-156">[ **新しいボットの作成]** オプションを選択し、新しいボットの名前を付け、[作成] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="1965e-156">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="1965e-157">次の図は、メッセージング拡張機能のボットの作成を表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-157">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="1965e-158">[ **メッセージング拡張機能** ] **ページの [コマンド** ] セクションで [追加] を選択して、メッセージング拡張機能の動作を決定するコマンドを含めます。</span><span class="sxs-lookup"><span data-stu-id="1965e-158">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="1965e-159">次の図は、メッセージング拡張機能のコマンド追加を表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-159">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. <span data-ttu-id="1965e-160">[Teams **の内部で外部サービスのアクションをトリガーするユーザーを許可する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1965e-160">Select **Allow users to trigger actions in external services while inside of Teams**.</span></span> <span data-ttu-id="1965e-161">次の図は、アクション コマンドの選択を表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-161">The following image displays the action command selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. <span data-ttu-id="1965e-162">静的な一連のパラメーターを使用してタスク モジュールを作成するには、[コマンドの静的パラメーターのセット **を定義する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1965e-162">To use a static set of parameters to create your task module, select **Define a set of static parameters for the command**.</span></span> 

    <span data-ttu-id="1965e-163">次の図は、アクション コマンドの静的パラメーターの選択を表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-163">The following image displays the action command static parameter selection:</span></span>

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    <span data-ttu-id="1965e-164">次の図は、静的パラメーターのセットアップ例を示しています。</span><span class="sxs-lookup"><span data-stu-id="1965e-164">The following image displays an example static parameter set-up:</span></span> 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    <span data-ttu-id="1965e-165">次の図は、静的パラメーターテストの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="1965e-165">The following image displays an example static parameter testing:</span></span>

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. <span data-ttu-id="1965e-166">動的パラメーターを使用するには、[ボットからパラメーター **の動的セットをフェッチする] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="1965e-166">To use dynamic parameters, select to **Fetch a dynamic set of parameters from your bot**.</span></span> <span data-ttu-id="1965e-167">次の図は、アクション コマンド パラメーターの選択を表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-167">The following image displays the action command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. <span data-ttu-id="1965e-168">コマンド ID **と Title** を **追加します**。</span><span class="sxs-lookup"><span data-stu-id="1965e-168">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="1965e-169">アクション コマンドを呼び出す場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="1965e-169">Select the location from where you want to invoke the action command.</span></span> <span data-ttu-id="1965e-170">次の図は、アクション コマンドの呼び出し場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-170">The following image displays the action command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. <span data-ttu-id="1965e-171">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="1965e-171">Select **Save**.</span></span>
1. <span data-ttu-id="1965e-172">パラメーターを追加するには、[パラメーター] セクション **の [追加** ] ボタン **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="1965e-172">To add more parameters, select the **Add** button in the **Parameters** section.</span></span>

### <a name="create-an-action-command-manually"></a><span data-ttu-id="1965e-173">アクション コマンドを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="1965e-173">Create an action command manually</span></span>

<span data-ttu-id="1965e-174">アクション ベースのメッセージング拡張機能コマンドをアプリ マニフェストに手動で追加するには、次のパラメーターをオブジェクトの `composeExtension.commands` 配列に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-174">To manually add your action-based messaging extension command to your app manifest, you must add the following parameters to the `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="1965e-175">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="1965e-175">Property name</span></span> | <span data-ttu-id="1965e-176">用途</span><span class="sxs-lookup"><span data-stu-id="1965e-176">Purpose</span></span> | <span data-ttu-id="1965e-177">必須</span><span class="sxs-lookup"><span data-stu-id="1965e-177">Required?</span></span> | <span data-ttu-id="1965e-178">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="1965e-178">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="1965e-179">このプロパティは、このコマンドに割り当てる一意の ID です。</span><span class="sxs-lookup"><span data-stu-id="1965e-179">This property is an unique ID that you assign to this command.</span></span> <span data-ttu-id="1965e-180">ユーザー要求には、この ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="1965e-180">The user request includes this ID.</span></span> | <span data-ttu-id="1965e-181">はい</span><span class="sxs-lookup"><span data-stu-id="1965e-181">Yes</span></span> | <span data-ttu-id="1965e-182">1.0</span><span class="sxs-lookup"><span data-stu-id="1965e-182">1.0</span></span> |
| `title` | <span data-ttu-id="1965e-183">このプロパティはコマンド名です。</span><span class="sxs-lookup"><span data-stu-id="1965e-183">This property is a command name.</span></span> <span data-ttu-id="1965e-184">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-184">This value appears in the UI.</span></span> | <span data-ttu-id="1965e-185">はい</span><span class="sxs-lookup"><span data-stu-id="1965e-185">Yes</span></span> | <span data-ttu-id="1965e-186">1.0</span><span class="sxs-lookup"><span data-stu-id="1965e-186">1.0</span></span> |
| `type` | <span data-ttu-id="1965e-187">このプロパティは、 である必要があります `action` 。</span><span class="sxs-lookup"><span data-stu-id="1965e-187">This property must be an `action`.</span></span> | <span data-ttu-id="1965e-188">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-188">No</span></span> | <span data-ttu-id="1965e-189">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-189">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="1965e-190">このプロパティは、タスク モジュールのアダプティブ カードまたは埋め込み Web ビュー、およびパラメーターの静的リストまたは Web ビューを読み込むときにに設定 `true` `false` されます `taskInfo` 。</span><span class="sxs-lookup"><span data-stu-id="1965e-190">This property is set to `true` for an adaptive card or embedded web view for your task module, and`false` for a static list of parameters or when loading the web view by a `taskInfo`.</span></span> | <span data-ttu-id="1965e-191">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-191">No</span></span> | <span data-ttu-id="1965e-192">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-192">1.4</span></span> |
| `context` | <span data-ttu-id="1965e-193">このプロパティは、メッセージング拡張機能の呼び出し先を定義する値の任意の配列です。</span><span class="sxs-lookup"><span data-stu-id="1965e-193">This property is an optional array of values that defines where the messaging extension is invoked from.</span></span> <span data-ttu-id="1965e-194">使用可能な値: `message`、`compose`、`commandBox`。</span><span class="sxs-lookup"><span data-stu-id="1965e-194">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="1965e-195">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="1965e-195">The default value is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="1965e-196">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-196">No</span></span> | <span data-ttu-id="1965e-197">1.5</span><span class="sxs-lookup"><span data-stu-id="1965e-197">1.5</span></span> |

<span data-ttu-id="1965e-198">静的なパラメーターの一覧を使用している場合は、次のパラメーターも追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1965e-198">If you are using a static list of parameters, you must also add the following parameters:</span></span>

| <span data-ttu-id="1965e-199">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="1965e-199">Property name</span></span> | <span data-ttu-id="1965e-200">用途</span><span class="sxs-lookup"><span data-stu-id="1965e-200">Purpose</span></span> | <span data-ttu-id="1965e-201">必須ですか?</span><span class="sxs-lookup"><span data-stu-id="1965e-201">Is required?</span></span> | <span data-ttu-id="1965e-202">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="1965e-202">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="1965e-203">このプロパティは、コマンドのパラメーターの静的な一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-203">This property describes the static list of parameters for the command.</span></span> <span data-ttu-id="1965e-204">の場合にのみ `fetchTask` 使用します `false` 。</span><span class="sxs-lookup"><span data-stu-id="1965e-204">Only use when `fetchTask` is `false`.</span></span> | <span data-ttu-id="1965e-205">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-205">No</span></span> | <span data-ttu-id="1965e-206">1.0</span><span class="sxs-lookup"><span data-stu-id="1965e-206">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="1965e-207">このプロパティは、パラメーターの名前を表します。</span><span class="sxs-lookup"><span data-stu-id="1965e-207">This property describes the name of the parameter.</span></span> <span data-ttu-id="1965e-208">これは、ユーザー要求でサービスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-208">This is sent to your service in the user request.</span></span> | <span data-ttu-id="1965e-209">はい</span><span class="sxs-lookup"><span data-stu-id="1965e-209">Yes</span></span> | <span data-ttu-id="1965e-210">1.0</span><span class="sxs-lookup"><span data-stu-id="1965e-210">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="1965e-211">このプロパティは、パラメーターの目的または指定する必要がある値の例を示します。</span><span class="sxs-lookup"><span data-stu-id="1965e-211">This property describes the parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="1965e-212">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-212">This value appears in the UI.</span></span> | <span data-ttu-id="1965e-213">はい</span><span class="sxs-lookup"><span data-stu-id="1965e-213">Yes</span></span> | <span data-ttu-id="1965e-214">1.0</span><span class="sxs-lookup"><span data-stu-id="1965e-214">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="1965e-215">このプロパティは、短いユーザーフレンドリーなパラメーターのタイトルまたはラベルです。</span><span class="sxs-lookup"><span data-stu-id="1965e-215">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="1965e-216">はい</span><span class="sxs-lookup"><span data-stu-id="1965e-216">Yes</span></span> | <span data-ttu-id="1965e-217">1.0</span><span class="sxs-lookup"><span data-stu-id="1965e-217">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="1965e-218">このプロパティは、必要な入力の種類に設定されます。</span><span class="sxs-lookup"><span data-stu-id="1965e-218">This property is set to the type of input required.</span></span> <span data-ttu-id="1965e-219">指定できる値には `text` `textarea` 、、 `number` 、 、 、 `date` 、 `time` が含まれます `toggle` 。</span><span class="sxs-lookup"><span data-stu-id="1965e-219">The possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="1965e-220">既定値は に設定されます `text` 。</span><span class="sxs-lookup"><span data-stu-id="1965e-220">The default value is set to `text`.</span></span> | <span data-ttu-id="1965e-221">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-221">No</span></span> | <span data-ttu-id="1965e-222">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-222">1.4</span></span> |

<span data-ttu-id="1965e-223">埋め込み Web ビューを使用している場合は、ボットを直接呼び出さずに、必要に応じてオブジェクトを追加して Web ビュー `taskInfo` をフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="1965e-223">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="1965e-224">このオプションを選択した場合の動作は、静的なパラメーターの一覧を使用する動作と似ています。</span><span class="sxs-lookup"><span data-stu-id="1965e-224">If you select this option, the behavior is similar to that of using a static list of parameters.</span></span> <span data-ttu-id="1965e-225">ボットとの最初のやり取りが [タスク モジュール送信アクションに応答しているという場合](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。</span><span class="sxs-lookup"><span data-stu-id="1965e-225">In that the first interaction with your bot is [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="1965e-226">オブジェクトを使用している場合 `taskInfo` は、パラメーターをに設定 `fetchTask` する必要があります `false` 。</span><span class="sxs-lookup"><span data-stu-id="1965e-226">If you are using a `taskInfo` object, you must set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="1965e-227">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="1965e-227">Property name</span></span> | <span data-ttu-id="1965e-228">用途</span><span class="sxs-lookup"><span data-stu-id="1965e-228">Purpose</span></span> | <span data-ttu-id="1965e-229">必須ですか?</span><span class="sxs-lookup"><span data-stu-id="1965e-229">Is required?</span></span> | <span data-ttu-id="1965e-230">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="1965e-230">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="1965e-231">メッセージング拡張機能コマンドを使用するときにプリロードするタスク モジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="1965e-231">Specify the task module to preload when using a messaging extension command.</span></span> | <span data-ttu-id="1965e-232">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-232">No</span></span> | <span data-ttu-id="1965e-233">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-233">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="1965e-234">初期タスク モジュールのタイトル。</span><span class="sxs-lookup"><span data-stu-id="1965e-234">Initial task module title.</span></span> |<span data-ttu-id="1965e-235">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-235">No</span></span> | <span data-ttu-id="1965e-236">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-236">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="1965e-237">タスク モジュールの幅 (ピクセル単位の数値または既定のレイアウトなど) `large` `medium` `small`</span><span class="sxs-lookup"><span data-stu-id="1965e-237">Task module width, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span> |<span data-ttu-id="1965e-238">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-238">No</span></span> | <span data-ttu-id="1965e-239">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-239">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="1965e-240">タスク モジュールの高さ (ピクセル単位の数値または既定のレイアウトなど) `large` `medium` `small`</span><span class="sxs-lookup"><span data-stu-id="1965e-240">Task module height, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span>|<span data-ttu-id="1965e-241">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-241">No</span></span> | <span data-ttu-id="1965e-242">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-242">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="1965e-243">初期 Web ビューの URL。</span><span class="sxs-lookup"><span data-stu-id="1965e-243">Initial web view URL.</span></span>|<span data-ttu-id="1965e-244">いいえ</span><span class="sxs-lookup"><span data-stu-id="1965e-244">No</span></span> | <span data-ttu-id="1965e-245">1.4</span><span class="sxs-lookup"><span data-stu-id="1965e-245">1.4</span></span> | 

#### <a name="app-manifest-example"></a><span data-ttu-id="1965e-246">アプリ マニフェストの例</span><span class="sxs-lookup"><span data-stu-id="1965e-246">App manifest example</span></span>

<span data-ttu-id="1965e-247">次のセクションは、2 つのアクション コマンド `composeExtensions` を定義するオブジェクトの例です。</span><span class="sxs-lookup"><span data-stu-id="1965e-247">The following section is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="1965e-248">完全なマニフェストの例ではありません。</span><span class="sxs-lookup"><span data-stu-id="1965e-248">It is not an example of the complete manifest.</span></span> <span data-ttu-id="1965e-249">完全なアプリ マニフェスト スキーマについては、「アプリ マニフェスト [スキーマ」を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="1965e-249">For the complete app manifest schema, see [app manifest schema](~/resources/schema/manifest-schema.md):</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="1965e-250">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="1965e-250">Code sample</span></span>

| <span data-ttu-id="1965e-251">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="1965e-251">Sample Name</span></span>           | <span data-ttu-id="1965e-252">説明</span><span class="sxs-lookup"><span data-stu-id="1965e-252">Description</span></span> | <span data-ttu-id="1965e-253">.NET</span><span class="sxs-lookup"><span data-stu-id="1965e-253">.NET</span></span>    | <span data-ttu-id="1965e-254">Node.js</span><span class="sxs-lookup"><span data-stu-id="1965e-254">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="1965e-255">Teams メッセージング拡張機能アクション</span><span class="sxs-lookup"><span data-stu-id="1965e-255">Teams messaging extension action</span></span>| <span data-ttu-id="1965e-256">アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1965e-256">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="1965e-257">View</span><span class="sxs-lookup"><span data-stu-id="1965e-257">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="1965e-258">View</span><span class="sxs-lookup"><span data-stu-id="1965e-258">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="1965e-259">Teams メッセージング拡張機能の検索</span><span class="sxs-lookup"><span data-stu-id="1965e-259">Teams messaging extension search</span></span>   |  <span data-ttu-id="1965e-260">検索コマンドを定義し、検索に応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1965e-260">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="1965e-261">View</span><span class="sxs-lookup"><span data-stu-id="1965e-261">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="1965e-262">View</span><span class="sxs-lookup"><span data-stu-id="1965e-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="1965e-263">次の手順</span><span class="sxs-lookup"><span data-stu-id="1965e-263">Next step</span></span>

<span data-ttu-id="1965e-264">アダプティブ カードまたはオブジェクトのない埋め込み Web ビューのいずれかを使用している場合、次の `taskInfo` 手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1965e-264">If you are using either an Adaptive Card or an embedded web view without a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1965e-265">タスク モジュールを使用して作成および応答する</span><span class="sxs-lookup"><span data-stu-id="1965e-265">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="1965e-266">オブジェクトでパラメーターまたは埋め込み Web ビューを使用する場合は、次 `taskInfo` の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="1965e-266">If you are using the parameters or an embedded web view with a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1965e-267">タスク モジュールの送信に応答する</span><span class="sxs-lookup"><span data-stu-id="1965e-267">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

