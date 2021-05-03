---
title: メッセージング拡張機能の検索コマンドを定義する
author: clearab
description: アプリのメッセージング拡張機能検索コマンドをMicrosoft Teamsします。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 19f1fdf7bd4efdbb0de11d1abad341ec24bc27bd
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696810"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="42341-103">メッセージング拡張機能の検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="42341-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="42341-104">メッセージング拡張機能の検索コマンドを使用すると、ユーザーは外部システムを検索し、その検索結果をカード形式のメッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="42341-104">Messaging extension search commands allow users to search external systems and insert the results of that search into a message in the form of a card.</span></span> <span data-ttu-id="42341-105">このドキュメントでは、検索コマンドの呼び出し場所を選択し、検索コマンドをアプリ マニフェストに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="42341-105">This document guides you on how to select  search command invoke locations, and add the search command to your app manifest.</span></span>

> [!NOTE]
> <span data-ttu-id="42341-106">結果のカード サイズの制限は 28 KB です。</span><span class="sxs-lookup"><span data-stu-id="42341-106">The result card size limit is 28 KB.</span></span> <span data-ttu-id="42341-107">カードのサイズが 28 KB を超える場合、カードは送信されません。</span><span class="sxs-lookup"><span data-stu-id="42341-107">The card is not sent if its size exceeds 28 KB.</span></span>

## <a name="select-search-command-invoke-locations"></a><span data-ttu-id="42341-108">検索コマンドの呼び出し場所を選択する</span><span class="sxs-lookup"><span data-stu-id="42341-108">Select search command invoke locations</span></span>

<span data-ttu-id="42341-109">検索コマンドは、次のいずれかの場所または両方から呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="42341-109">The search command is invoked from any one or both of the following locations:</span></span>

* <span data-ttu-id="42341-110">メッセージの作成領域: 作成メッセージ領域の下部にあるボタン。</span><span class="sxs-lookup"><span data-stu-id="42341-110">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="42341-111">コマンド ボックス: コマンド @mentioningを使用します。</span><span class="sxs-lookup"><span data-stu-id="42341-111">Command box: By @mentioning in the command box.</span></span>

<span data-ttu-id="42341-112">メッセージの作成領域から検索コマンドが呼び出されると、ユーザーは結果を会話に送信します。</span><span class="sxs-lookup"><span data-stu-id="42341-112">When search command is invoked from the compose message area, the user sends the results to the conversation.</span></span> <span data-ttu-id="42341-113">コマンド ボックスから呼び出されると、ユーザーは結果のカードを操作するか、別の場所で使用するためにコピーします。</span><span class="sxs-lookup"><span data-stu-id="42341-113">When it is invoked from the command box, the user interacts with the resulting card, or copies it for use elsewhere.</span></span>

<span data-ttu-id="42341-114">次の図は、検索コマンドの呼び出し場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="42341-114">The following image displays the invoke locations of the search command:</span></span>

![search コマンドの呼び出し場所](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a><span data-ttu-id="42341-116">アプリ マニフェストに検索コマンドを追加する</span><span class="sxs-lookup"><span data-stu-id="42341-116">Add the search command to your app manifest</span></span>

<span data-ttu-id="42341-117">検索コマンドをアプリ マニフェストに追加するには、アプリ マニフェスト JSON のトップ レベルに新しいオブジェクト `composeExtension` を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42341-117">To add the search command to your app manifest, you must add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="42341-118">検索コマンドは、App Studio の助けを借りて追加するか、手動で追加できます。</span><span class="sxs-lookup"><span data-stu-id="42341-118">You can add the search command either with the help of App Studio, or manually.</span></span>

### <a name="create-a-search-command-using-app-studio"></a><span data-ttu-id="42341-119">App Studio を使用して検索コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="42341-119">Create a search command using App Studio</span></span>

<span data-ttu-id="42341-120">検索コマンドを作成する前提条件は、メッセージング拡張機能を既に作成している必要があります。</span><span class="sxs-lookup"><span data-stu-id="42341-120">The prerequisite to create a search command is that you must already have created a messaging extension.</span></span> <span data-ttu-id="42341-121">メッセージング拡張機能を作成する方法の詳細については、「Create [a messaging extension 」を参照してください](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="42341-121">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="42341-122">**検索コマンドを作成するには**</span><span class="sxs-lookup"><span data-stu-id="42341-122">**To create a search command**</span></span>

1. <span data-ttu-id="42341-123">クライアント **から App Studio** をMicrosoft Teamsし、[マニフェスト エディター]**タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="42341-123">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1.  <span data-ttu-id="42341-124">App Studio でアプリ パッケージを既に作成している **場合** は、一覧から選択します。</span><span class="sxs-lookup"><span data-stu-id="42341-124">If you already created your app package in **App Studio**, select from the list.</span></span> <span data-ttu-id="42341-125">アプリ パッケージを作成していない場合は、既存のパッケージをインポートします。</span><span class="sxs-lookup"><span data-stu-id="42341-125">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="42341-126">アプリ パッケージをインポートした後、[機能] **で [メッセージング拡張機能]** **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="42341-126">After importing app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="42341-127">メッセージング拡張機能を設定するポップアップ ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="42341-127">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="42341-128">ウィンドウ **で [セットアップ** ] を選択して、メッセージング拡張機能をアプリ エクスペリエンスに含めます。</span><span class="sxs-lookup"><span data-stu-id="42341-128">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="42341-129">次の図は、メッセージング拡張機能のセットアップ ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="42341-129">The following image displays the messaging extension set up page:</span></span> 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. <span data-ttu-id="42341-130">メッセージング拡張機能を作成するには、Microsoft 登録済みのボットが必要です。</span><span class="sxs-lookup"><span data-stu-id="42341-130">To create the messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="42341-131">既存のボットを使用するか、新しいボットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="42341-131">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="42341-132">[ **新しいボットの作成]** オプションを選択し、新しいボットの名前を付け、[作成] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="42341-132">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="42341-133">次の図は、メッセージング拡張機能のボットの作成を表示します。</span><span class="sxs-lookup"><span data-stu-id="42341-133">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="42341-134">[ **メッセージング拡張機能** ] **ページの [コマンド** ] セクションで [追加] を選択して、メッセージング拡張機能の動作を決定するコマンドを含めます。</span><span class="sxs-lookup"><span data-stu-id="42341-134">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="42341-135">次の図は、メッセージング拡張機能のコマンド追加を表示します。</span><span class="sxs-lookup"><span data-stu-id="42341-135">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. <span data-ttu-id="42341-136">[ **ユーザーがサービスに情報を照会し、メッセージに挿入する] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="42341-136">Select **Allow users to query your service for information and insert that into a message**.</span></span> <span data-ttu-id="42341-137">次の図は、検索コマンド パラメーターの選択を表示します。</span><span class="sxs-lookup"><span data-stu-id="42341-137">The following image displays the search command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. <span data-ttu-id="42341-138">コマンド ID **と Title** を **追加します**。</span><span class="sxs-lookup"><span data-stu-id="42341-138">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="42341-139">検索コマンドを呼び出す必要がある場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="42341-139">Select the location from where your search command must be invoked.</span></span> <span data-ttu-id="42341-140">メッセージを **選択しても** 、現在、検索コマンドの動作は変更されません。</span><span class="sxs-lookup"><span data-stu-id="42341-140">Selecting **message** does not currently alter the behavior of your search command.</span></span> <span data-ttu-id="42341-141">次の図は、検索コマンドの呼び出し場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="42341-141">The following image displays the search command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. <span data-ttu-id="42341-142">検索パラメーターを追加し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="42341-142">Add your search parameter and select **Save**.</span></span>

### <a name="create-a-search-command-manually"></a><span data-ttu-id="42341-143">手動で検索コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="42341-143">Create a search command manually</span></span> 

<span data-ttu-id="42341-144">メッセージング拡張機能検索コマンドをアプリ マニフェストに手動で追加するには、次のパラメーターをオブジェクトの配列 `composeExtension.commands` に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42341-144">To manually add your messaging extension search command to your app manifest, you must add the following parameters to your `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="42341-145">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="42341-145">Property name</span></span> | <span data-ttu-id="42341-146">用途</span><span class="sxs-lookup"><span data-stu-id="42341-146">Purpose</span></span> | <span data-ttu-id="42341-147">必須</span><span class="sxs-lookup"><span data-stu-id="42341-147">Required?</span></span> | <span data-ttu-id="42341-148">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="42341-148">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="42341-149">このプロパティは、検索コマンドに割り当てる一意の ID です。</span><span class="sxs-lookup"><span data-stu-id="42341-149">This property is an unique ID that you assign to search command.</span></span> <span data-ttu-id="42341-150">ユーザー要求には、この ID が含まれます。</span><span class="sxs-lookup"><span data-stu-id="42341-150">The user request includes this ID.</span></span> | <span data-ttu-id="42341-151">はい</span><span class="sxs-lookup"><span data-stu-id="42341-151">Yes</span></span> | <span data-ttu-id="42341-152">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-152">1.0</span></span> |
| `title` | <span data-ttu-id="42341-153">このプロパティはコマンド名です。</span><span class="sxs-lookup"><span data-stu-id="42341-153">This property is a command name.</span></span> <span data-ttu-id="42341-154">この値は、ユーザー インターフェイス (UI) に表示されます。</span><span class="sxs-lookup"><span data-stu-id="42341-154">This value appears in the user interface (UI).</span></span> | <span data-ttu-id="42341-155">はい</span><span class="sxs-lookup"><span data-stu-id="42341-155">Yes</span></span> | <span data-ttu-id="42341-156">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-156">1.0</span></span> |
| `description` | <span data-ttu-id="42341-157">このプロパティは、このコマンドの動作を示すヘルプ テキストです。</span><span class="sxs-lookup"><span data-stu-id="42341-157">This property is a help text indicating what this command does.</span></span> <span data-ttu-id="42341-158">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="42341-158">This value appears in the UI.</span></span> | <span data-ttu-id="42341-159">はい</span><span class="sxs-lookup"><span data-stu-id="42341-159">Yes</span></span> | <span data-ttu-id="42341-160">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-160">1.0</span></span> |
| `type` | <span data-ttu-id="42341-161">このプロパティは、 である必要があります `query` 。</span><span class="sxs-lookup"><span data-stu-id="42341-161">This property must be a `query`.</span></span> | <span data-ttu-id="42341-162">いいえ</span><span class="sxs-lookup"><span data-stu-id="42341-162">No</span></span> | <span data-ttu-id="42341-163">1.4</span><span class="sxs-lookup"><span data-stu-id="42341-163">1.4</span></span> |
|`initialRun` | <span data-ttu-id="42341-164">このプロパティを true に **設定すると**、ユーザーが UI でこのコマンドを選択するとすぐにこのコマンドを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42341-164">If this property is set to **true**, it indicates this command should be executed as soon as the user selects this command in the UI.</span></span> | <span data-ttu-id="42341-165">いいえ</span><span class="sxs-lookup"><span data-stu-id="42341-165">No</span></span> | <span data-ttu-id="42341-166">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-166">1.0</span></span> |
| `context` | <span data-ttu-id="42341-167">このプロパティは、検索アクションが使用できるコンテキストを定義する値のオプションの配列です。</span><span class="sxs-lookup"><span data-stu-id="42341-167">This property is an optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="42341-168">使用可能な値: `message`、`compose`、`commandBox`。</span><span class="sxs-lookup"><span data-stu-id="42341-168">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="42341-169">既定値は `["compose", "commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="42341-169">The default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="42341-170">いいえ</span><span class="sxs-lookup"><span data-stu-id="42341-170">No</span></span> | <span data-ttu-id="42341-171">1.5</span><span class="sxs-lookup"><span data-stu-id="42341-171">1.5</span></span> |

<span data-ttu-id="42341-172">検索クライアントでユーザーに表示されるテキストを定義する検索パラメーターの詳細を追加Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="42341-172">You must add the details of the search parameter, that defines the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="42341-173">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="42341-173">Property name</span></span> | <span data-ttu-id="42341-174">用途</span><span class="sxs-lookup"><span data-stu-id="42341-174">Purpose</span></span> | <span data-ttu-id="42341-175">必須ですか?</span><span class="sxs-lookup"><span data-stu-id="42341-175">Is required?</span></span> | <span data-ttu-id="42341-176">マニフェストの最小バージョン</span><span class="sxs-lookup"><span data-stu-id="42341-176">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="42341-177">このプロパティは、コマンドのパラメーターの静的リストを定義します。</span><span class="sxs-lookup"><span data-stu-id="42341-177">This property defines a static list of parameters for the command.</span></span> | <span data-ttu-id="42341-178">いいえ</span><span class="sxs-lookup"><span data-stu-id="42341-178">No</span></span> | <span data-ttu-id="42341-179">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-179">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="42341-180">このプロパティは、パラメーターの名前を表します。</span><span class="sxs-lookup"><span data-stu-id="42341-180">This property describes the name of the parameter.</span></span> <span data-ttu-id="42341-181">これは、ユーザー要求でサービスに送信されます。</span><span class="sxs-lookup"><span data-stu-id="42341-181">This is sent to your service in the user request.</span></span> | <span data-ttu-id="42341-182">はい</span><span class="sxs-lookup"><span data-stu-id="42341-182">Yes</span></span> | <span data-ttu-id="42341-183">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-183">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="42341-184">このプロパティは、パラメーターの目的または指定する必要がある値の例を示します。</span><span class="sxs-lookup"><span data-stu-id="42341-184">This property describes the parameter’s purposes or example of the value that must be provided.</span></span> <span data-ttu-id="42341-185">この値は UI に表示されます。</span><span class="sxs-lookup"><span data-stu-id="42341-185">This value appears in the UI.</span></span> | <span data-ttu-id="42341-186">はい</span><span class="sxs-lookup"><span data-stu-id="42341-186">Yes</span></span> | <span data-ttu-id="42341-187">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-187">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="42341-188">このプロパティは、短いユーザーフレンドリーなパラメーターのタイトルまたはラベルです。</span><span class="sxs-lookup"><span data-stu-id="42341-188">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="42341-189">はい</span><span class="sxs-lookup"><span data-stu-id="42341-189">Yes</span></span> | <span data-ttu-id="42341-190">1.0</span><span class="sxs-lookup"><span data-stu-id="42341-190">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="42341-191">このプロパティは、必要な入力の種類に設定されます。</span><span class="sxs-lookup"><span data-stu-id="42341-191">This property is set to the type of the input required.</span></span> <span data-ttu-id="42341-192">可能な値 `text` には `textarea` 、、 `number` 、 、 、 、 `date` `time` が含まれます `toggle` 。</span><span class="sxs-lookup"><span data-stu-id="42341-192">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="42341-193">既定値は に設定されています `text` 。</span><span class="sxs-lookup"><span data-stu-id="42341-193">Default is set to `text`.</span></span> | <span data-ttu-id="42341-194">いいえ</span><span class="sxs-lookup"><span data-stu-id="42341-194">No</span></span> | <span data-ttu-id="42341-195">1.4</span><span class="sxs-lookup"><span data-stu-id="42341-195">1.4</span></span> |

#### <a name="example"></a><span data-ttu-id="42341-196">例</span><span class="sxs-lookup"><span data-stu-id="42341-196">Example</span></span>

<span data-ttu-id="42341-197">次のセクションでは、検索コマンドを定義するオブジェクトの単純 `composeExtensions` なアプリ マニフェストの例を示します。</span><span class="sxs-lookup"><span data-stu-id="42341-197">Following section is an example of the simple app manifest of the `composeExtensions` object defining a search command:</span></span> 

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
<span data-ttu-id="42341-198">完全なアプリ マニフェストについては、「アプリ マニフェスト [スキーマ」を参照してください](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="42341-198">For the complete app manifest, see [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="42341-199">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="42341-199">Code sample</span></span>

| <span data-ttu-id="42341-200">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="42341-200">Sample Name</span></span>           | <span data-ttu-id="42341-201">説明</span><span class="sxs-lookup"><span data-stu-id="42341-201">Description</span></span> | <span data-ttu-id="42341-202">.NET</span><span class="sxs-lookup"><span data-stu-id="42341-202">.NET</span></span>    | <span data-ttu-id="42341-203">Node.js</span><span class="sxs-lookup"><span data-stu-id="42341-203">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="42341-204">Teams拡張アクション</span><span class="sxs-lookup"><span data-stu-id="42341-204">Teams messaging extension action</span></span>| <span data-ttu-id="42341-205">アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="42341-205">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="42341-206">View</span><span class="sxs-lookup"><span data-stu-id="42341-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="42341-207">View</span><span class="sxs-lookup"><span data-stu-id="42341-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="42341-208">Teams拡張機能の検索</span><span class="sxs-lookup"><span data-stu-id="42341-208">Teams messaging extension search</span></span>   |  <span data-ttu-id="42341-209">検索コマンドを定義し、検索に応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="42341-209">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="42341-210">View</span><span class="sxs-lookup"><span data-stu-id="42341-210">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="42341-211">View</span><span class="sxs-lookup"><span data-stu-id="42341-211">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="42341-212">次の手順</span><span class="sxs-lookup"><span data-stu-id="42341-212">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="42341-213">[検索コマンドに応答します](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="42341-213">[Respond to the search commands](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

