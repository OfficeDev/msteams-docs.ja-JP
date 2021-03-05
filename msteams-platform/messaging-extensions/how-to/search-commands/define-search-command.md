---
title: メッセージング拡張機能の検索コマンドを定義する
author: clearab
description: Microsoft Teams アプリのメッセージング拡張機能検索コマンドを定義します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449270"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="ebee7-103">メッセージング拡張機能の検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="ebee7-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="ebee7-104">メッセージング拡張機能検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカード形式でメッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

> [!NOTE]
> <span data-ttu-id="ebee7-105">結果のカード サイズの制限は 28 KB です。</span><span class="sxs-lookup"><span data-stu-id="ebee7-105">The result card size limit is 28 KB.</span></span> <span data-ttu-id="ebee7-106">カードのサイズが 28 KB を超える場合、カードは送信されません。</span><span class="sxs-lookup"><span data-stu-id="ebee7-106">The card is not sent if its size exceeds 28 KB.</span></span> 

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="ebee7-107">メッセージング拡張機能の呼び出し場所の選択</span><span class="sxs-lookup"><span data-stu-id="ebee7-107">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="ebee7-108">最初に決定する必要があるのは、検索コマンドをトリガーできる場所 (具体的には呼び *出し先*) です。</span><span class="sxs-lookup"><span data-stu-id="ebee7-108">The first thing you need to decide is where your search command can be triggered (or specifically, *invoked*) from.</span></span> <span data-ttu-id="ebee7-109">検索コマンドは、次のいずれかの場所または両方から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-109">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="ebee7-110">作成メッセージ領域の下部にあるボタン</span><span class="sxs-lookup"><span data-stu-id="ebee7-110">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="ebee7-111">コマンド @mentioningを使用して</span><span class="sxs-lookup"><span data-stu-id="ebee7-111">By @mentioning in the command box</span></span>

<span data-ttu-id="ebee7-112">作成メッセージ領域から呼び出されると、ユーザーは結果を会話に送信できます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-112">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="ebee7-113">コマンド ボックスから呼び出されると、ユーザーは結果のカードを操作したり、別の場所で使用するためにコピーすることができます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-113">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="ebee7-114">アプリ マニフェストにコマンドを追加する</span><span class="sxs-lookup"><span data-stu-id="ebee7-114">Add the command to your app manifest</span></span>

<span data-ttu-id="ebee7-115">ユーザーが検索コマンドを操作する方法を決めたので、それをアプリ マニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-115">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="ebee7-116">これを行うには、アプリ マニフェスト JSON のトップ レベルに新 `composeExtension` しいオブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-116">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="ebee7-117">これを行うには、App Studio のヘルプを使用するか、手動で実行します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-117">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="ebee7-118">App Studio を使用してコマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="ebee7-118">Create a command using App Studio</span></span>

<span data-ttu-id="ebee7-119">検索コマンドを作成するには、メッセージング拡張機能を既に作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebee7-119">The prerequisite to create a search command is that you must already create a messaging extension.</span></span> <span data-ttu-id="ebee7-120">メッセージング拡張機能を作成する方法の詳細については、「Create [a messaging extension 」を参照してください](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="ebee7-120">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="ebee7-121">**検索コマンドを作成するには**</span><span class="sxs-lookup"><span data-stu-id="ebee7-121">**To create a search command**</span></span>

1. <span data-ttu-id="ebee7-122">Microsoft Teams クライアントで App Studio を **開** き、[マニフェスト エディター] **タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-122">From the Microsoft Teams client, open **App Studio**, and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="ebee7-123">App Studio でアプリ パッケージを既に作成している **場合** は、一覧からアプリ パッケージを選択します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-123">If you already created an app package in the **App Studio**, choose it from the list.</span></span> <span data-ttu-id="ebee7-124">アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。</span><span class="sxs-lookup"><span data-stu-id="ebee7-124">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="ebee7-125">アプリ パッケージをインポートした後、[機能] で [ **メッセージング拡張機能]** **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ebee7-125">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span>
1. <span data-ttu-id="ebee7-126">[ **メッセージング拡張機能** ] **ページの [コマンド** ] セクションで [追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-126">Select **Add** in the **Command** section in the messaging extensions page.</span></span>
1. <span data-ttu-id="ebee7-127">[ **ユーザーにサービスの情報のクエリを許可する] を選択し、メッセージに挿入します**。</span><span class="sxs-lookup"><span data-stu-id="ebee7-127">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
1. <span data-ttu-id="ebee7-128">コマンド ID **と Title** を **追加します**。</span><span class="sxs-lookup"><span data-stu-id="ebee7-128">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="ebee7-129">検索コマンドをトリガーする必要がある場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-129">Select the location from where your search command must be triggered.</span></span> <span data-ttu-id="ebee7-130">メッセージを **選択しても** 、現在、検索コマンドの動作は変更されません。</span><span class="sxs-lookup"><span data-stu-id="ebee7-130">Selecting **message** does not currently alter the behavior of your search command.</span></span>
1. <span data-ttu-id="ebee7-131">検索パラメーターを追加し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="ebee7-131">Add your search parameter and select **Save**.</span></span>
 
### <a name="manually-create-a-command"></a><span data-ttu-id="ebee7-132">コマンドを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="ebee7-132">Manually create a command</span></span>

<span data-ttu-id="ebee7-133">メッセージング拡張機能の検索コマンドをアプリ マニフェストに手動で追加するには、次のパラメーターをオブジェクトの配列 `composeExtension.commands` に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebee7-133">To manually add your messaging extension search command to your app manifest, you'll need to add the following parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="ebee7-134">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="ebee7-134">Property name</span></span> | <span data-ttu-id="ebee7-135">用途</span><span class="sxs-lookup"><span data-stu-id="ebee7-135">Purpose</span></span> | <span data-ttu-id="ebee7-136">必須</span><span class="sxs-lookup"><span data-stu-id="ebee7-136">Required?</span></span> | <span data-ttu-id="ebee7-137">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="ebee7-137">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="ebee7-138">このコマンドに割り当てる一意の ID。</span><span class="sxs-lookup"><span data-stu-id="ebee7-138">Unique ID that you assign to this command.</span></span> <span data-ttu-id="ebee7-139">ユーザー要求には、この ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-139">The user request will include this ID.</span></span> | <span data-ttu-id="ebee7-140">はい</span><span class="sxs-lookup"><span data-stu-id="ebee7-140">Yes</span></span> | <span data-ttu-id="ebee7-141">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-141">1.0</span></span> |
| `title` | <span data-ttu-id="ebee7-142">コマンド名。</span><span class="sxs-lookup"><span data-stu-id="ebee7-142">Command name.</span></span> <span data-ttu-id="ebee7-143">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-143">This value appears in the UI.</span></span> | <span data-ttu-id="ebee7-144">はい</span><span class="sxs-lookup"><span data-stu-id="ebee7-144">Yes</span></span> | <span data-ttu-id="ebee7-145">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-145">1.0</span></span> |
| `description` | <span data-ttu-id="ebee7-146">このコマンドの動作を示すヘルプ テキスト。</span><span class="sxs-lookup"><span data-stu-id="ebee7-146">Help text indicating what this command does.</span></span> <span data-ttu-id="ebee7-147">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-147">This value appears in the UI.</span></span> | <span data-ttu-id="ebee7-148">はい</span><span class="sxs-lookup"><span data-stu-id="ebee7-148">Yes</span></span> | <span data-ttu-id="ebee7-149">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-149">1.0</span></span> |
| `type` | <span data-ttu-id="ebee7-150">にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebee7-150">Must be `query`</span></span> | <span data-ttu-id="ebee7-151">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebee7-151">No</span></span> | <span data-ttu-id="ebee7-152">1.4</span><span class="sxs-lookup"><span data-stu-id="ebee7-152">1.4</span></span> |
|`initialRun` | <span data-ttu-id="ebee7-153">true に **設定されている場合** は、ユーザーが UI でこのコマンドを選択するとすぐにこのコマンドを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebee7-153">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="ebee7-154">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebee7-154">No</span></span> | <span data-ttu-id="ebee7-155">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-155">1.0</span></span> |
| `context` | <span data-ttu-id="ebee7-156">検索アクションが使用できるコンテキストを定義する値の任意の配列。</span><span class="sxs-lookup"><span data-stu-id="ebee7-156">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="ebee7-157">指定できる値 `message` は `compose` 、、、または `commandBox` です。</span><span class="sxs-lookup"><span data-stu-id="ebee7-157">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="ebee7-158">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="ebee7-158">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="ebee7-159">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebee7-159">No</span></span> | <span data-ttu-id="ebee7-160">1.5</span><span class="sxs-lookup"><span data-stu-id="ebee7-160">1.5</span></span> |

<span data-ttu-id="ebee7-161">また、Teams クライアントでユーザーに表示されるテキストを定義する検索パラメーターの詳細を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebee7-161">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="ebee7-162">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="ebee7-162">Property name</span></span> | <span data-ttu-id="ebee7-163">用途</span><span class="sxs-lookup"><span data-stu-id="ebee7-163">Purpose</span></span> | <span data-ttu-id="ebee7-164">必須</span><span class="sxs-lookup"><span data-stu-id="ebee7-164">Required?</span></span> | <span data-ttu-id="ebee7-165">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="ebee7-165">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="ebee7-166">コマンドのパラメーターの静的リスト。</span><span class="sxs-lookup"><span data-stu-id="ebee7-166">Static list of parameters for the command.</span></span> | <span data-ttu-id="ebee7-167">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebee7-167">No</span></span> | <span data-ttu-id="ebee7-168">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-168">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="ebee7-169">パラメーターの名前です。</span><span class="sxs-lookup"><span data-stu-id="ebee7-169">The name of the parameter.</span></span> <span data-ttu-id="ebee7-170">これは、ユーザー要求でサービスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-170">This is sent to your service in the user request.</span></span> | <span data-ttu-id="ebee7-171">はい</span><span class="sxs-lookup"><span data-stu-id="ebee7-171">Yes</span></span> | <span data-ttu-id="ebee7-172">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-172">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="ebee7-173">指定する必要がある値のこのパラメーターの目的または例について説明します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-173">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="ebee7-174">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ebee7-174">This value appears in the UI.</span></span> | <span data-ttu-id="ebee7-175">はい</span><span class="sxs-lookup"><span data-stu-id="ebee7-175">Yes</span></span> | <span data-ttu-id="ebee7-176">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-176">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="ebee7-177">短いユーザーフレンドリーなパラメーターのタイトルまたはラベル。</span><span class="sxs-lookup"><span data-stu-id="ebee7-177">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="ebee7-178">はい</span><span class="sxs-lookup"><span data-stu-id="ebee7-178">Yes</span></span> | <span data-ttu-id="ebee7-179">1.0</span><span class="sxs-lookup"><span data-stu-id="ebee7-179">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="ebee7-180">必要な入力の種類に設定します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-180">Set to the type of input required.</span></span> <span data-ttu-id="ebee7-181">可能な値 `text` には `textarea` 、、 `number` 、 、 、 、 `date` `time` が含まれます `toggle` 。</span><span class="sxs-lookup"><span data-stu-id="ebee7-181">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="ebee7-182">既定値はに設定されています `text`</span><span class="sxs-lookup"><span data-stu-id="ebee7-182">Default is set to `text`</span></span> | <span data-ttu-id="ebee7-183">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebee7-183">No</span></span> | <span data-ttu-id="ebee7-184">1.4</span><span class="sxs-lookup"><span data-stu-id="ebee7-184">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="ebee7-185">アプリ マニフェストの例</span><span class="sxs-lookup"><span data-stu-id="ebee7-185">App manifest example</span></span>

<span data-ttu-id="ebee7-186">検索コマンドを定義する `composeExtensions` オブジェクトの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ebee7-186">Below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="ebee7-187">完全なマニフェストの例ではありません。完全なアプリ マニフェスト スキーマについては、「アプリ マニフェスト [スキーマ」を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="ebee7-187">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```

## <a name="next-steps"></a><span data-ttu-id="ebee7-188">次の手順</span><span class="sxs-lookup"><span data-stu-id="ebee7-188">Next steps</span></span>

<span data-ttu-id="ebee7-189">検索コマンドが追加されたので、検索要求を [処理する必要があります](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="ebee7-189">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
