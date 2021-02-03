---
title: タスク モジュールの作成と送信
author: clearab
description: 最初の呼び出しアクションを処理し、アクション メッセージング拡張機能コマンドからタスク モジュールで応答する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072876"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="7cfa7-103">タスク モジュールの作成と送信</span><span class="sxs-lookup"><span data-stu-id="7cfa7-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="7cfa7-104">アプリ マニフェストで定義されたパラメーターを使ってタスク モジュールにデータを入力しない場合は、ユーザー用のタスク モジュールを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-104">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users.</span></span> <span data-ttu-id="7cfa7-105">アダプティブ カードまたは埋め込み Web ビューのいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-105">Use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="7cfa7-106">最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="7cfa7-106">The initial invoke request</span></span>

<span data-ttu-id="7cfa7-107">このメソッドを使用すると、サービスは型のオブジェクトを受け取り、アダプティブ カードまたは埋め込み Web ビューへの URL を含むオブジェクトで応答 `Activity` `composeExtension/fetchTask` `task` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-107">Using this method your service will receive an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="7cfa7-108">標準のボット アクティビティ プロパティと共に、最初の呼び出しペイロードには次の要求メタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-108">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="7cfa7-109">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-109">Property name</span></span>|<span data-ttu-id="7cfa7-110">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="7cfa7-111">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-111">Type of request.</span></span> <span data-ttu-id="7cfa7-112">この値は次の値である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-112">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="7cfa7-113">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-113">Type of command that is issued to your service.</span></span> <span data-ttu-id="7cfa7-114">この値は次の値である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-114">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="7cfa7-115">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-115">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="7cfa7-116">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-116">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="7cfa7-117">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-117">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="7cfa7-118">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-118">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="7cfa7-119">チャネル ID (要求がチャネルで行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-119">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="7cfa7-120">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-120">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="7cfa7-121">呼び出されたコマンドの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-121">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="7cfa7-122">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-122">The context that triggered the event.</span></span> <span data-ttu-id="7cfa7-123">この値は次の値である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-123">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="7cfa7-124">ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-124">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="7cfa7-125">この値は `default` 、次の値 `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-125">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a><span data-ttu-id="7cfa7-126">1 対 1 のチャットからタスク モジュールが呼び出された場合のペイロード アクティビティのプロパティは、次のセクションに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-126">Payload activity properties when invoked a task module from 1:1 chat are listed in the following section:</span></span>

|<span data-ttu-id="7cfa7-127">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-127">Property name</span></span>|<span data-ttu-id="7cfa7-128">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-128">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="7cfa7-129">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-129">Type of request.</span></span> <span data-ttu-id="7cfa7-130">この値は、次の値である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-130">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="7cfa7-131">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-131">Type of command that is issued to your service.</span></span> <span data-ttu-id="7cfa7-132">この値は次の値である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-132">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="7cfa7-133">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-133">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="7cfa7-134">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-134">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="7cfa7-135">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-135">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="7cfa7-136">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-136">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="7cfa7-137">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-137">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="7cfa7-138">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-138">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="7cfa7-139">呼び出されたコマンドの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-139">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="7cfa7-140">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-140">The context that triggered the event.</span></span> <span data-ttu-id="7cfa7-141">この値は次の値である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-141">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="7cfa7-142">ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-142">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="7cfa7-143">この値は `default` 、次の値 `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-143">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a><span data-ttu-id="7cfa7-144">グループ チャットからタスク モジュールを呼び出した場合のペイロード アクティビティプロパティは、次のセクションに示されています。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-144">Payload activity properties when invoked a task module from a group chat are listed in the following section:</span></span>

|<span data-ttu-id="7cfa7-145">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-145">Property name</span></span>|<span data-ttu-id="7cfa7-146">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-146">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="7cfa7-147">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-147">Type of request.</span></span> <span data-ttu-id="7cfa7-148">この値は次の値である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-148">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="7cfa7-149">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-149">Type of command that is issued to your service.</span></span> <span data-ttu-id="7cfa7-150">この値は、次の値である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-150">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="7cfa7-151">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-151">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="7cfa7-152">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-152">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="7cfa7-153">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-153">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="7cfa7-154">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-154">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="7cfa7-155">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-155">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="7cfa7-156">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-156">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="7cfa7-157">呼び出されたコマンドの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-157">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="7cfa7-158">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-158">The context that triggered the event.</span></span> <span data-ttu-id="7cfa7-159">この値は次の値である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-159">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="7cfa7-160">ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-160">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="7cfa7-161">この値は 、または `default` `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="7cfa7-161">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a><span data-ttu-id="7cfa7-162">チャネルからタスク モジュールを呼び出した場合のペイロード アクティビティ プロパティ (新しい投稿) は、次のセクションに一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-162">Payload activity properties when invoked a task module from a channel (new post) are listed in the following section:</span></span>

|<span data-ttu-id="7cfa7-163">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-163">Property name</span></span>|<span data-ttu-id="7cfa7-164">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-164">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="7cfa7-165">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-165">Type of request.</span></span> <span data-ttu-id="7cfa7-166">この値は次の値である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-166">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="7cfa7-167">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-167">Type of command that is issued to your service.</span></span> <span data-ttu-id="7cfa7-168">この値は、次の値である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-168">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="7cfa7-169">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-169">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="7cfa7-170">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-170">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="7cfa7-171">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-171">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="7cfa7-172">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-172">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="7cfa7-173">チャネル ID (要求がチャネルで行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-173">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="7cfa7-174">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-174">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="7cfa7-175">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-175">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="7cfa7-176">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-176">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="7cfa7-177">呼び出されたコマンドの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-177">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="7cfa7-178">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-178">The context that triggered the event.</span></span> <span data-ttu-id="7cfa7-179">この値は、次の値である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-179">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="7cfa7-180">ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-180">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="7cfa7-181">この値は `default` 、次の値 `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-181">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a><span data-ttu-id="7cfa7-182">チャネルからタスク モジュールを呼び出した場合のペイロード アクティビティ プロパティ (スレッドに返信) を次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-182">Payload activity properties when invoked a task module from a channel (reply to thread) are listed in the following section:</span></span>

|<span data-ttu-id="7cfa7-183">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-183">Property name</span></span>|<span data-ttu-id="7cfa7-184">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-184">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="7cfa7-185">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-185">Type of request.</span></span> <span data-ttu-id="7cfa7-186">この値は、次の値である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-186">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="7cfa7-187">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-187">Type of command that is issued to your service.</span></span> <span data-ttu-id="7cfa7-188">この値は次の値である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-188">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="7cfa7-189">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-189">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="7cfa7-190">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-190">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="7cfa7-191">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-191">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="7cfa7-192">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-192">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="7cfa7-193">チャネル ID (要求がチャネルで行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-193">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="7cfa7-194">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-194">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="7cfa7-195">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-195">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="7cfa7-196">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-196">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="7cfa7-197">呼び出されたコマンドの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-197">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="7cfa7-198">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-198">The context that triggered the event.</span></span> <span data-ttu-id="7cfa7-199">この値は次の値である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-199">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="7cfa7-200">ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-200">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="7cfa7-201">この値は 、または `default` `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="7cfa7-201">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a><span data-ttu-id="7cfa7-202">コマンド ボックスからタスク モジュールを呼び出した場合のペイロード アクティビティ のプロパティは、次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-202">Payload activity properties when invoked a task module from a command box are listed in the following section:</span></span>

|<span data-ttu-id="7cfa7-203">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-203">Property name</span></span>|<span data-ttu-id="7cfa7-204">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-204">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="7cfa7-205">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-205">Type of request.</span></span> <span data-ttu-id="7cfa7-206">この値は、次の値である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-206">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="7cfa7-207">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-207">Type of command that is issued to your service.</span></span> <span data-ttu-id="7cfa7-208">この値は次の値である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-208">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="7cfa7-209">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-209">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="7cfa7-210">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-210">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="7cfa7-211">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-211">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="7cfa7-212">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-212">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="7cfa7-213">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-213">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="7cfa7-214">呼び出されたコマンドの ID を格納します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-214">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="7cfa7-215">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-215">The context that triggered the event.</span></span> <span data-ttu-id="7cfa7-216">この値は、次の値である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-216">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="7cfa7-217">ユーザーのクライアント テーマ。埋め込み Web ビューの書式設定に便利です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-217">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="7cfa7-218">この値は 、または `default` `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="7cfa7-218">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="7cfa7-219">fetchTask 要求の例</span><span class="sxs-lookup"><span data-stu-id="7cfa7-219">Example fetchTask request</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7cfa7-220">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7cfa7-220">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7cfa7-221">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfa7-221">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="7cfa7-222">JSON</span><span class="sxs-lookup"><span data-stu-id="7cfa7-222">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="7cfa7-223">メッセージからの最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="7cfa7-223">Initial invoke request from a message</span></span>

<span data-ttu-id="7cfa7-224">ボットが作成領域またはコマンド バーではなくメッセージから呼び出された場合、最初の要求のオブジェクトには、メッセージング拡張機能が呼び出されるメッセージの詳細が含まれている `value` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-224">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request must contain the details of the message your messaging extension is invoked from.</span></span> <span data-ttu-id="7cfa7-225">このオブジェクトの例については、次のセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-225">See the following section  for the example of this object .</span></span> <span data-ttu-id="7cfa7-226">The `reactions` and arrays are `mentions` optional, and they are not present if there are no reactions or mentions in the original message.</span><span class="sxs-lookup"><span data-stu-id="7cfa7-226">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7cfa7-227">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7cfa7-227">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7cfa7-228">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfa7-228">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="7cfa7-229">JSON</span><span class="sxs-lookup"><span data-stu-id="7cfa7-229">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="7cfa7-230">fetchTask に応答する</span><span class="sxs-lookup"><span data-stu-id="7cfa7-230">Respond to the fetchTask</span></span>

<span data-ttu-id="7cfa7-231">アダプティブ カードまたは Web URL を持つオブジェクト、または単純な文字列メッセージを含むオブジェクトを使用して、呼び出し要求 `task` `taskInfo` に応答します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-231">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="7cfa7-232">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-232">Property name</span></span>|<span data-ttu-id="7cfa7-233">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-233">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="7cfa7-234">フォームを `continue` 表示するか、単純な `message` ポップアップを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-234">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="7cfa7-235">フォーム `taskInfo` のオブジェクト、またはメッセージ `string` の a。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-235">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="7cfa7-236">taskInfo オブジェクトのスキーマは次の例です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-236">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="7cfa7-237">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="7cfa7-237">Property name</span></span>|<span data-ttu-id="7cfa7-238">用途</span><span class="sxs-lookup"><span data-stu-id="7cfa7-238">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="7cfa7-239">タスク モジュールのタイトル。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-239">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="7cfa7-240">整数 (ピクセル単位) または , `small` `medium` , . `large`</span><span class="sxs-lookup"><span data-stu-id="7cfa7-240">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="7cfa7-241">整数 (ピクセル単位) または , `small` `medium` , . `large`</span><span class="sxs-lookup"><span data-stu-id="7cfa7-241">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="7cfa7-242">フォームを定義するアダプティブ カード (使用している場合)。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-242">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="7cfa7-243">埋め込み Web ビューとしてタスク モジュール内で開く URL。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-243">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="7cfa7-244">クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-244">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="7cfa7-245">アダプティブ カードを使用する</span><span class="sxs-lookup"><span data-stu-id="7cfa7-245">With an adaptive card</span></span>

<span data-ttu-id="7cfa7-246">アダプティブ カードを使用する場合は、アダプティブ カードを含むオブジェクトを持つ `task` `value` オブジェクトに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-246">When using an adaptive card, you must respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="7cfa7-247">アダプティブ カードを使用した fetchTask 応答の例</span><span class="sxs-lookup"><span data-stu-id="7cfa7-247">Example fetchTask response with an adaptive card</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7cfa7-248">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7cfa7-248">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="7cfa7-249">このサンプルでは、Bot Framework SDK [に加えて AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-249">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7cfa7-250">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfa7-250">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[<span data-ttu-id="7cfa7-251">JSON</span><span class="sxs-lookup"><span data-stu-id="7cfa7-251">JSON</span></span>](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="7cfa7-252">埋め込み Web ビューを使用する</span><span class="sxs-lookup"><span data-stu-id="7cfa7-252">With an embedded web view</span></span>

<span data-ttu-id="7cfa7-253">埋め込み Web ビューを使用する場合は、読み込む Web フォームの URL を含むオブジェクトを持つオブジェクトに応答 `task` `value` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-253">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="7cfa7-254">読み込む URL のドメインは、アプリのマニフェストの配列に含 `validDomains` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-254">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="7cfa7-255">埋め [込み Web ビューの構築](~/task-modules-and-cards/what-are-task-modules.md) に関する詳細については、タスク モジュールのドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-255">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7cfa7-256">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7cfa7-256">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7cfa7-257">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7cfa7-257">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="7cfa7-258">JSON</span><span class="sxs-lookup"><span data-stu-id="7cfa7-258">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="7cfa7-259">会話ボットのインストール要求</span><span class="sxs-lookup"><span data-stu-id="7cfa7-259">Request to install your conversational bot</span></span>

<span data-ttu-id="7cfa7-260">アプリに会話ボットが含まれている場合は、タスク モジュールを読み込む前に会話にボットをインストールします。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-260">If the app contains a conversational bot, install the bot in the conversation before loading the task module.</span></span> <span data-ttu-id="7cfa7-261">タスク モジュールの追加のコンテキストを取得すると便利です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-261">It is useful to get additional context for the task module.</span></span> <span data-ttu-id="7cfa7-262">このシナリオの一般的な例は、名簿をフェッチして、ユーザー選択コントロールまたはチーム内のチャネルの一覧を設定します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-262">Typical example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="7cfa7-263">メッセージング拡張機能が呼び出しを受信したら、ボットが現在のコンテキストにインストールされていることを確認して、フロー `composeExtension/fetchTask` を容易にしてください。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-263">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="7cfa7-264">たとえば、名簿呼び出しを取得してフローを確認します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-264">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="7cfa7-265">ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-265">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="7cfa7-266">次の例のアクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-266">See the action in the following example.</span></span> <span data-ttu-id="7cfa7-267">ユーザーには、その場所にアプリをインストールして確認するためのアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-267">The user must have permission to install the apps in that location for checking.</span></span> <span data-ttu-id="7cfa7-268">アプリのインストールが失敗した場合、ユーザーは管理者に連絡するメッセージを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-268">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example-of-the-response"></a><span data-ttu-id="7cfa7-269">応答の例:</span><span class="sxs-lookup"><span data-stu-id="7cfa7-269">Example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="7cfa7-270">インストール後、ボットは別の呼び出しメッセージを `name = composeExtension/submitAction` 受け取ります `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-270">After the installation, the bot receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example-of-the-invoke"></a><span data-ttu-id="7cfa7-271">呼び出しの例:</span><span class="sxs-lookup"><span data-stu-id="7cfa7-271">Example of the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="7cfa7-272">呼び出しに対するタスクの応答は、インストールされているボットの応答と似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-272">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a><span data-ttu-id="7cfa7-273">アダプティブ カードを含むアプリの just-in Time インストールの例:</span><span class="sxs-lookup"><span data-stu-id="7cfa7-273">Example of just-in time installation of app with Adaptive card:</span></span> 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="next-steps"></a><span data-ttu-id="7cfa7-274">次の手順</span><span class="sxs-lookup"><span data-stu-id="7cfa7-274">Next steps</span></span>

<span data-ttu-id="7cfa7-275">ユーザーがタスク モジュールから応答を返送できる場合は、送信アクションを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7cfa7-275">If you allow your users to send a response back from the task module, you must handle the submit action.</span></span>

* [<span data-ttu-id="7cfa7-276">タスク モジュールを作成して応答する</span><span class="sxs-lookup"><span data-stu-id="7cfa7-276">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
