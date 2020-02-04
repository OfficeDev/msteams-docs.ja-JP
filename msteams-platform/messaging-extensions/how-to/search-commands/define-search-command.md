---
title: メッセージング拡張機能検索コマンドを定義する
author: clearab
description: Microsoft Teams アプリのメッセージング拡張機能検索コマンドを定義します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674934"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="a794c-103">メッセージング拡張機能検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="a794c-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="a794c-104">メッセージング拡張検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカードの形式でメッセージに挿入することができます。</span><span class="sxs-lookup"><span data-stu-id="a794c-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="a794c-105">メッセージング拡張機能の呼び出し場所を選択する</span><span class="sxs-lookup"><span data-stu-id="a794c-105">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="a794c-106">最初に決定する必要があるのは、検索コマンドをトリガー (または、より具体的に*呼び出す*) できる場所です。</span><span class="sxs-lookup"><span data-stu-id="a794c-106">The first thing you need to decide is where your search command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="a794c-107">検索コマンドは、次の場所のいずれかまたは両方から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="a794c-107">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="a794c-108">[メッセージの作成] 領域の下部にあるボタン</span><span class="sxs-lookup"><span data-stu-id="a794c-108">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="a794c-109">コマンドボックスで @mentioning</span><span class="sxs-lookup"><span data-stu-id="a794c-109">By @mentioning in the command box</span></span>

<span data-ttu-id="a794c-110">[メッセージの作成] 領域から呼び出した場合、ユーザーは会話に結果を送信することができます。</span><span class="sxs-lookup"><span data-stu-id="a794c-110">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="a794c-111">コマンドボックスから呼び出した場合、ユーザーは結果として得られたカードを操作したり、別の場所で使用するためにコピーしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="a794c-111">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="a794c-112">アプリケーションマニフェストにコマンドを追加する</span><span class="sxs-lookup"><span data-stu-id="a794c-112">Add the command to your app manifest</span></span>

<span data-ttu-id="a794c-113">ユーザーが検索コマンドをどのように操作するかが決定したので、それをアプリのマニフェストに追加します。</span><span class="sxs-lookup"><span data-stu-id="a794c-113">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="a794c-114">これを行うには、アプリマニフェスト`composeExtension` JSON の最上位レベルに新しいオブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="a794c-114">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="a794c-115">そのためには、アプリ Studio のヘルプを使用するか、手動で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a794c-115">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="a794c-116">アプリ Studio を使用してコマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="a794c-116">Create a command using App Studio</span></span>

<span data-ttu-id="a794c-117">次の手順では、[メッセージング拡張機能が](~/messaging-extensions/how-to/create-messaging-extension.md)既に作成済みであることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="a794c-117">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="a794c-118">Microsoft Teams クライアントから、 **App Studio**を開き、[**マニフェストエディター** ] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="a794c-118">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="a794c-119">アプリパッケージが既にアプリ Studio で作成されている場合は、一覧から選択します。</span><span class="sxs-lookup"><span data-stu-id="a794c-119">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="a794c-120">それ以外の場合は、既存のアプリパッケージをインポートできます。</span><span class="sxs-lookup"><span data-stu-id="a794c-120">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="a794c-121">[コマンド] セクションの [**追加**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a794c-121">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="a794c-122">[ユーザーがサービスを照会して情報を受信できるようにする] を選択し、**それをメッセージに挿入**します。</span><span class="sxs-lookup"><span data-stu-id="a794c-122">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
5. <span data-ttu-id="a794c-123">**コマンド Id**と**タイトル**を追加します。</span><span class="sxs-lookup"><span data-stu-id="a794c-123">Add a **Command Id** and a **Title**.</span></span>
6. <span data-ttu-id="a794c-124">検索コマンドを開始する場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="a794c-124">Select where you want your search command to be triggered from.</span></span> <span data-ttu-id="a794c-125">現在、**メッセージ**を選択しても、検索コマンドの動作は変更されません。</span><span class="sxs-lookup"><span data-stu-id="a794c-125">Selecting **message** does not currently alter the behavior of your search command.</span></span>
7. <span data-ttu-id="a794c-126">検索パラメーターを追加します。</span><span class="sxs-lookup"><span data-stu-id="a794c-126">Add your search parameter.</span></span>
8. <span data-ttu-id="a794c-127">[保存] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a794c-127">Click Save.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="a794c-128">コマンドを手動で作成する</span><span class="sxs-lookup"><span data-stu-id="a794c-128">Manually create a command</span></span>

<span data-ttu-id="a794c-129">メッセージング拡張機能検索コマンドをアプリマニフェストに手動で追加するには、オブジェクトの`composeExtension.commands`配列に follow パラメーターを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a794c-129">To manually add your messaging extension search command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="a794c-130">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="a794c-130">Property name</span></span> | <span data-ttu-id="a794c-131">用途</span><span class="sxs-lookup"><span data-stu-id="a794c-131">Purpose</span></span> | <span data-ttu-id="a794c-132">必須</span><span class="sxs-lookup"><span data-stu-id="a794c-132">Required?</span></span> | <span data-ttu-id="a794c-133">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="a794c-133">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="a794c-134">このコマンドに割り当てる一意の ID です。</span><span class="sxs-lookup"><span data-stu-id="a794c-134">Unique ID that you assign to this command.</span></span> <span data-ttu-id="a794c-135">ユーザー要求には、この ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a794c-135">The user request will include this ID.</span></span> | <span data-ttu-id="a794c-136">はい</span><span class="sxs-lookup"><span data-stu-id="a794c-136">Yes</span></span> | <span data-ttu-id="a794c-137">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-137">1.0</span></span> |
| `title` | <span data-ttu-id="a794c-138">コマンド名を指定します。</span><span class="sxs-lookup"><span data-stu-id="a794c-138">Command name.</span></span> <span data-ttu-id="a794c-139">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a794c-139">This value appears in the UI.</span></span> | <span data-ttu-id="a794c-140">はい</span><span class="sxs-lookup"><span data-stu-id="a794c-140">Yes</span></span> | <span data-ttu-id="a794c-141">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-141">1.0</span></span> |
| `description` | <span data-ttu-id="a794c-142">このコマンドの機能を示すヘルプテキスト。</span><span class="sxs-lookup"><span data-stu-id="a794c-142">Help text indicating what this command does.</span></span> <span data-ttu-id="a794c-143">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a794c-143">This value appears in the UI.</span></span> | <span data-ttu-id="a794c-144">はい</span><span class="sxs-lookup"><span data-stu-id="a794c-144">Yes</span></span> | <span data-ttu-id="a794c-145">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-145">1.0</span></span> |
| `type` | <span data-ttu-id="a794c-146">にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a794c-146">Must be `query`</span></span> | <span data-ttu-id="a794c-147">いいえ</span><span class="sxs-lookup"><span data-stu-id="a794c-147">No</span></span> | <span data-ttu-id="a794c-148">1.4</span><span class="sxs-lookup"><span data-stu-id="a794c-148">1.4</span></span> |
|`initialRun` | <span data-ttu-id="a794c-149">**True**に設定すると、ユーザーが UI でこのコマンドを選択するとすぐにこのコマンドが実行されることを示します。</span><span class="sxs-lookup"><span data-stu-id="a794c-149">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="a794c-150">いいえ</span><span class="sxs-lookup"><span data-stu-id="a794c-150">No</span></span> | <span data-ttu-id="a794c-151">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-151">1.0</span></span> |
| `context` | <span data-ttu-id="a794c-152">検索アクションを使用できるコンテキストを定義する値のオプションの配列です。</span><span class="sxs-lookup"><span data-stu-id="a794c-152">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="a794c-153">可能な値`message`は`compose`、、 `commandBox`、です。</span><span class="sxs-lookup"><span data-stu-id="a794c-153">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="a794c-154">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="a794c-154">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="a794c-155">いいえ</span><span class="sxs-lookup"><span data-stu-id="a794c-155">No</span></span> | <span data-ttu-id="a794c-156">1.5</span><span class="sxs-lookup"><span data-stu-id="a794c-156">1.5</span></span> |

<span data-ttu-id="a794c-157">また、検索パラメーターの詳細を追加して、Teams クライアントでユーザーに表示されるテキストを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a794c-157">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="a794c-158">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="a794c-158">Property name</span></span> | <span data-ttu-id="a794c-159">用途</span><span class="sxs-lookup"><span data-stu-id="a794c-159">Purpose</span></span> | <span data-ttu-id="a794c-160">必須</span><span class="sxs-lookup"><span data-stu-id="a794c-160">Required?</span></span> | <span data-ttu-id="a794c-161">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="a794c-161">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="a794c-162">コマンドのパラメーターの静的リスト。</span><span class="sxs-lookup"><span data-stu-id="a794c-162">Static list of parameters for the command.</span></span> | <span data-ttu-id="a794c-163">いいえ</span><span class="sxs-lookup"><span data-stu-id="a794c-163">No</span></span> | <span data-ttu-id="a794c-164">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-164">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="a794c-165">パラメーターの名前です。</span><span class="sxs-lookup"><span data-stu-id="a794c-165">The name of the parameter.</span></span> <span data-ttu-id="a794c-166">これは、ユーザーの要求でサービスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="a794c-166">This is sent to your service in the user request.</span></span> | <span data-ttu-id="a794c-167">はい</span><span class="sxs-lookup"><span data-stu-id="a794c-167">Yes</span></span> | <span data-ttu-id="a794c-168">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-168">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="a794c-169">このパラメーターの目的または提供する必要がある値の例について説明します。</span><span class="sxs-lookup"><span data-stu-id="a794c-169">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="a794c-170">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a794c-170">This value appears in the UI.</span></span> | <span data-ttu-id="a794c-171">はい</span><span class="sxs-lookup"><span data-stu-id="a794c-171">Yes</span></span> | <span data-ttu-id="a794c-172">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-172">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="a794c-173">簡単なユーザーフレンドリパラメーターのタイトルまたはラベル。</span><span class="sxs-lookup"><span data-stu-id="a794c-173">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="a794c-174">はい</span><span class="sxs-lookup"><span data-stu-id="a794c-174">Yes</span></span> | <span data-ttu-id="a794c-175">1.0</span><span class="sxs-lookup"><span data-stu-id="a794c-175">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="a794c-176">必要な入力の種類を設定します。</span><span class="sxs-lookup"><span data-stu-id="a794c-176">Set to the type of input required.</span></span> <span data-ttu-id="a794c-177">可能な値`text`は`textarea`、 `number` `date` `time`、、、 `toggle`、です。</span><span class="sxs-lookup"><span data-stu-id="a794c-177">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="a794c-178">既定値はに設定されています`text`</span><span class="sxs-lookup"><span data-stu-id="a794c-178">Default is set to `text`</span></span> | <span data-ttu-id="a794c-179">いいえ</span><span class="sxs-lookup"><span data-stu-id="a794c-179">No</span></span> | <span data-ttu-id="a794c-180">1.4</span><span class="sxs-lookup"><span data-stu-id="a794c-180">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="a794c-181">アプリマニフェストの例</span><span class="sxs-lookup"><span data-stu-id="a794c-181">App manifest example</span></span>

<span data-ttu-id="a794c-182">以下に、検索コマンドを定義`composeExtensions`するオブジェクトの例を示します。</span><span class="sxs-lookup"><span data-stu-id="a794c-182">The below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="a794c-183">完全なマニフェストの例として、完全なアプリマニフェストスキーマについては、「 [app manifest スキーマ](~/resources/schema/manifest-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a794c-183">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a794c-184">次のステップ</span><span class="sxs-lookup"><span data-stu-id="a794c-184">Next steps</span></span>

<span data-ttu-id="a794c-185">検索コマンドが追加されたので、[検索要求を処理](~/messaging-extensions/how-to/search-commands/respond-to-search.md)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a794c-185">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]