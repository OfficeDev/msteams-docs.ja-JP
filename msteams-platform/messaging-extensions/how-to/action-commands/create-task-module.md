---
title: タスク モジュールの作成と送信
author: clearab
description: 最初の呼び出しアクションを処理し、アクション メッセージング拡張機能コマンドからタスク モジュールで応答する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 12af2d788c0579414b544e7e2fd7f07a77d45919
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696277"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="436e2-103">タスク モジュールの作成と送信</span><span class="sxs-lookup"><span data-stu-id="436e2-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="436e2-104">アダプティブ カードまたは埋め込み Web ビューを使用してタスク モジュールを作成できます。</span><span class="sxs-lookup"><span data-stu-id="436e2-104">You can create the task module using an Adaptive Card or an embedded web view.</span></span> <span data-ttu-id="436e2-105">タスク モジュールを作成するには、最初の呼び出し要求と呼ばれるプロセスを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-105">To create a task module, you must perform the process called the initial invoke request.</span></span> <span data-ttu-id="436e2-106">このドキュメントでは、最初の呼び出し要求、1:1 チャット、グループ チャット、チャネル (新しい投稿)、チャネル (スレッドへの返信)、およびコマンド ボックスからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="436e2-106">This document covers the initial invoke request, payload activity properties when a task module is invoked from 1:1 chat, group chat, channel (new post), channel (reply to thread), and command box.</span></span> 
> [!NOTE]
> <span data-ttu-id="436e2-107">アプリ マニフェストで定義されたパラメーターをタスク モジュールに設定しない場合は、アダプティブ カードまたは埋め込み Web ビューを使用するユーザー用のタスク モジュールを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-107">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users with either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="436e2-108">最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="436e2-108">The initial invoke request</span></span>

<span data-ttu-id="436e2-109">最初の呼び出し要求のプロセスで、サービスは型のオブジェクトを受け取り、アダプティブ カードまたは埋め込み Web ビューへの URL を含むオブジェクトで応答する `Activity` `composeExtension/fetchTask` `task` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-109">In the process of the initial invoke request, your service receives an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either an Adaptive Card or a URL to the embedded web view.</span></span> <span data-ttu-id="436e2-110">ボットアクティビティの標準プロパティと共に、最初の呼び出しペイロードには次の要求メタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="436e2-110">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="436e2-111">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-111">Property name</span></span>|<span data-ttu-id="436e2-112">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-112">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="436e2-113">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-113">Type of request.</span></span> <span data-ttu-id="436e2-114">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-114">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="436e2-115">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-115">Type of command that is issued to your service.</span></span> <span data-ttu-id="436e2-116">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-116">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="436e2-117">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-117">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="436e2-118">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="436e2-118">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="436e2-119">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-119">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="436e2-120">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-120">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="436e2-121">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="436e2-121">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="436e2-122">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="436e2-122">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="436e2-123">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="436e2-123">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="436e2-124">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="436e2-124">The context that triggered the event.</span></span> <span data-ttu-id="436e2-125">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-125">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="436e2-126">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="436e2-126">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="436e2-127">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-127">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="436e2-128">例</span><span class="sxs-lookup"><span data-stu-id="436e2-128">Example</span></span>

<span data-ttu-id="436e2-129">最初の呼び出し要求のコードは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="436e2-129">The code for the initial invoke request is given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a><span data-ttu-id="436e2-130">タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティプロパティ</span><span class="sxs-lookup"><span data-stu-id="436e2-130">Payload activity properties when a task module is invoked from 1:1 chat</span></span> 

<span data-ttu-id="436e2-131">タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティのプロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="436e2-131">The payload activity properties when a task module is invoked from 1:1 chat are listed as follows:</span></span>

|<span data-ttu-id="436e2-132">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-132">Property name</span></span>|<span data-ttu-id="436e2-133">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-133">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="436e2-134">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-134">Type of request.</span></span> <span data-ttu-id="436e2-135">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-135">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="436e2-136">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-136">Type of command that is issued to your service.</span></span> <span data-ttu-id="436e2-137">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-137">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="436e2-138">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-138">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="436e2-139">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="436e2-139">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="436e2-140">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-140">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="436e2-141">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-141">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="436e2-142">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="436e2-142">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="436e2-143">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="436e2-143">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="436e2-144">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="436e2-144">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="436e2-145">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="436e2-145">The context that triggered the event.</span></span> <span data-ttu-id="436e2-146">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-146">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="436e2-147">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="436e2-147">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="436e2-148">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-148">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="436e2-149">例</span><span class="sxs-lookup"><span data-stu-id="436e2-149">Example</span></span>

<span data-ttu-id="436e2-150">タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティプロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="436e2-150">The payload activity properties when a task module is invoked from 1:1 chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```
## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a><span data-ttu-id="436e2-151">グループ チャットからタスク モジュールが呼び出された場合のペイロード アクティビティのプロパティ</span><span class="sxs-lookup"><span data-stu-id="436e2-151">Payload activity properties when a task module is invoked from a group chat</span></span> 

<span data-ttu-id="436e2-152">タスク モジュールがグループ チャットから呼び出された場合のペイロード アクティビティのプロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="436e2-152">The payload activity properties when a task module is invoked from a group chat are listed as follows:</span></span>

|<span data-ttu-id="436e2-153">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-153">Property name</span></span>|<span data-ttu-id="436e2-154">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-154">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="436e2-155">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-155">Type of request.</span></span> <span data-ttu-id="436e2-156">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-156">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="436e2-157">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-157">Type of command that is issued to your service.</span></span> <span data-ttu-id="436e2-158">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-158">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="436e2-159">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-159">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="436e2-160">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="436e2-160">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="436e2-161">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-161">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="436e2-162">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-162">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="436e2-163">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="436e2-163">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="436e2-164">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="436e2-164">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="436e2-165">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="436e2-165">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="436e2-166">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="436e2-166">The context that triggered the event.</span></span> <span data-ttu-id="436e2-167">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-167">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="436e2-168">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="436e2-168">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="436e2-169">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-169">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="436e2-170">例</span><span class="sxs-lookup"><span data-stu-id="436e2-170">Example</span></span>

<span data-ttu-id="436e2-171">タスク モジュールがグループ チャットから呼び出された場合のペイロード アクティビティプロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="436e2-171">The payload activity properties when a task module is invoked from a group chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a><span data-ttu-id="436e2-172">チャネルからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティ (新しい投稿)</span><span class="sxs-lookup"><span data-stu-id="436e2-172">Payload activity properties when a task module is invoked from a channel (new post)</span></span> 

<span data-ttu-id="436e2-173">タスク モジュールがチャネル (新しい投稿) から呼び出された場合のペイロード アクティビティプロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="436e2-173">The payload activity properties when a task module is invoked from a channel (new post) are listed as follows:</span></span>

|<span data-ttu-id="436e2-174">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-174">Property name</span></span>|<span data-ttu-id="436e2-175">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-175">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="436e2-176">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-176">Type of request.</span></span> <span data-ttu-id="436e2-177">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-177">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="436e2-178">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-178">Type of command that is issued to your service.</span></span> <span data-ttu-id="436e2-179">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-179">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="436e2-180">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-180">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="436e2-181">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="436e2-181">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="436e2-182">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-182">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="436e2-183">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-183">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="436e2-184">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="436e2-184">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="436e2-185">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="436e2-185">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="436e2-186">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="436e2-186">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="436e2-187">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="436e2-187">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="436e2-188">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="436e2-188">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="436e2-189">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="436e2-189">The context that triggered the event.</span></span> <span data-ttu-id="436e2-190">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-190">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="436e2-191">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="436e2-191">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="436e2-192">、、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-192">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="436e2-193">例</span><span class="sxs-lookup"><span data-stu-id="436e2-193">Example</span></span>

<span data-ttu-id="436e2-194">タスク モジュールがチャネル (新しい投稿) から呼び出された場合のペイロード アクティビティ プロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="436e2-194">The payload activity properties when a task module is invoked from a channel (new post) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a><span data-ttu-id="436e2-195">チャネルからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティ (スレッドに返信)</span><span class="sxs-lookup"><span data-stu-id="436e2-195">Payload activity properties when a task module is invoked from a channel (reply to thread)</span></span> 

<span data-ttu-id="436e2-196">タスク モジュールがチャネルから呼び出された場合のペイロード アクティビティ プロパティ (スレッドへの返信) は、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="436e2-196">The payload activity properties when a task module is invoked from a channel (reply to thread) are listed as follows:</span></span>

|<span data-ttu-id="436e2-197">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-197">Property name</span></span>|<span data-ttu-id="436e2-198">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-198">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="436e2-199">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-199">Type of request.</span></span> <span data-ttu-id="436e2-200">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-200">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="436e2-201">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-201">Type of command that is issued to your service.</span></span> <span data-ttu-id="436e2-202">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-202">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="436e2-203">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-203">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="436e2-204">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="436e2-204">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="436e2-205">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-205">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="436e2-206">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-206">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="436e2-207">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="436e2-207">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="436e2-208">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="436e2-208">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="436e2-209">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="436e2-209">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="436e2-210">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="436e2-210">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="436e2-211">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="436e2-211">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="436e2-212">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="436e2-212">The context that triggered the event.</span></span> <span data-ttu-id="436e2-213">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-213">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="436e2-214">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="436e2-214">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="436e2-215">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-215">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="436e2-216">例</span><span class="sxs-lookup"><span data-stu-id="436e2-216">Example</span></span>

<span data-ttu-id="436e2-217">タスク モジュールがチャネルから呼び出された場合のペイロード アクティビティ プロパティ (スレッドへの返信) は、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="436e2-217">The payload activity properties when a task module is invoked from a channel (reply to thread) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a><span data-ttu-id="436e2-218">タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティ</span><span class="sxs-lookup"><span data-stu-id="436e2-218">Payload activity properties when a task module is invoked from a command box</span></span> 

<span data-ttu-id="436e2-219">タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="436e2-219">The payload activity properties when a task module is invoked from a command box are listed as follows:</span></span>

|<span data-ttu-id="436e2-220">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-220">Property name</span></span>|<span data-ttu-id="436e2-221">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-221">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="436e2-222">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-222">Type of request.</span></span> <span data-ttu-id="436e2-223">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-223">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="436e2-224">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="436e2-224">Type of command that is issued to your service.</span></span> <span data-ttu-id="436e2-225">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-225">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="436e2-226">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-226">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="436e2-227">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="436e2-227">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="436e2-228">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-228">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="436e2-229">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="436e2-229">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="436e2-230">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="436e2-230">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="436e2-231">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="436e2-231">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="436e2-232">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="436e2-232">The context that triggered the event.</span></span> <span data-ttu-id="436e2-233">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-233">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="436e2-234">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="436e2-234">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="436e2-235">、、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-235">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="436e2-236">例</span><span class="sxs-lookup"><span data-stu-id="436e2-236">Example</span></span>

<span data-ttu-id="436e2-237">タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="436e2-237">The payload activity properties when a task module is invoked from a command box are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a><span data-ttu-id="436e2-238">例</span><span class="sxs-lookup"><span data-stu-id="436e2-238">Example</span></span> 

<span data-ttu-id="436e2-239">次のコード セクションは、要求の例 `fetchTask` です。</span><span class="sxs-lookup"><span data-stu-id="436e2-239">The following code section is an example of `fetchTask` request:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="436e2-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="436e2-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="436e2-241">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="436e2-241">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="436e2-242">JSON</span><span class="sxs-lookup"><span data-stu-id="436e2-242">JSON</span></span>](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="436e2-243">メッセージからの最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="436e2-243">Initial invoke request from a message</span></span>

<span data-ttu-id="436e2-244">ボットがメッセージから呼び出されると、最初の呼び出し要求のオブジェクトに、メッセージング拡張機能が呼び出されるメッセージの詳細が `value` 含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-244">When your bot is invoked from a message,  the `value` object in the initial invoke request must contain the details of the message that your messaging extension is invoked from.</span></span> <span data-ttu-id="436e2-245">配列 `reactions` と配列は省略可能で、元のメッセージにリアクションやメンションがない場合は `mentions` 存在しません。</span><span class="sxs-lookup"><span data-stu-id="436e2-245">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span> <span data-ttu-id="436e2-246">次のセクションは、オブジェクトの例 `value` です。</span><span class="sxs-lookup"><span data-stu-id="436e2-246">The following section is an example of the `value` object:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="436e2-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="436e2-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="436e2-248">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="436e2-248">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="436e2-249">JSON</span><span class="sxs-lookup"><span data-stu-id="436e2-249">JSON</span></span>](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="436e2-250">fetchTask に応答する</span><span class="sxs-lookup"><span data-stu-id="436e2-250">Respond to the fetchTask</span></span>

<span data-ttu-id="436e2-251">アダプティブ カードまたは Web URL を持つオブジェクト、または単純な文字列メッセージを含むオブジェクトを使用して、呼び出し要求 `task` `taskInfo` に応答します。</span><span class="sxs-lookup"><span data-stu-id="436e2-251">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the Adaptive Card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="436e2-252">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-252">Property name</span></span>|<span data-ttu-id="436e2-253">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-253">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="436e2-254">フォームを表示 `continue` するか、単純な `message` ポップアップを表示できます。</span><span class="sxs-lookup"><span data-stu-id="436e2-254">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="436e2-255">フォーム `taskInfo` のオブジェクト、またはメッセージ `string` の a。</span><span class="sxs-lookup"><span data-stu-id="436e2-255">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="436e2-256">taskInfo オブジェクトのスキーマは次の値です。</span><span class="sxs-lookup"><span data-stu-id="436e2-256">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="436e2-257">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="436e2-257">Property name</span></span>|<span data-ttu-id="436e2-258">用途</span><span class="sxs-lookup"><span data-stu-id="436e2-258">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="436e2-259">タスク モジュールのタイトル。</span><span class="sxs-lookup"><span data-stu-id="436e2-259">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="436e2-260">整数 (ピクセル単位) または 、 `small` 、 のいずれか `medium` である必要があります `large` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-260">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="436e2-261">整数 (ピクセル単位) または 、 `small` 、 のいずれか `medium` である必要があります `large` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-261">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="436e2-262">フォームを定義するアダプティブ カード (使用している場合)。</span><span class="sxs-lookup"><span data-stu-id="436e2-262">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="436e2-263">埋め込み Web ビューとしてタスク モジュール内で開く URL。</span><span class="sxs-lookup"><span data-stu-id="436e2-263">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="436e2-264">クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。</span><span class="sxs-lookup"><span data-stu-id="436e2-264">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a><span data-ttu-id="436e2-265">アダプティブ カードを使用して fetchTask に応答する</span><span class="sxs-lookup"><span data-stu-id="436e2-265">Respond to the fetchTask with an Adaptive Card</span></span>

<span data-ttu-id="436e2-266">アダプティブ カードを使用する場合は、アダプティブ カードを含むオブジェクトでオブジェクト `task` `value` に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-266">When using an adaptive card, you must respond with a `task` object with the `value` object containing an Adaptive Card.</span></span>

#### <a name="example"></a><span data-ttu-id="436e2-267">例</span><span class="sxs-lookup"><span data-stu-id="436e2-267">Example</span></span>

<span data-ttu-id="436e2-268">次のコード セクションは、アダプティブ カードで `fetchTask` 応答する例です。</span><span class="sxs-lookup"><span data-stu-id="436e2-268">The following code section is an example to `fetchTask` response with an adaptive card:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="436e2-269">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="436e2-269">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="436e2-270">このサンプルでは、Bot Framework SDK に加えて [AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="436e2-270">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="436e2-271">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="436e2-271">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="436e2-272">JSON</span><span class="sxs-lookup"><span data-stu-id="436e2-272">JSON</span></span>](#tab/json)

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

### <a name="create-a-task-module-with-an-embedded-web-view"></a><span data-ttu-id="436e2-273">埋め込み Web ビューを使用してタスク モジュールを作成する</span><span class="sxs-lookup"><span data-stu-id="436e2-273">Create a task module with an embedded web view</span></span>

<span data-ttu-id="436e2-274">埋め込み Web ビューを使用する場合は、読み込む Web フォームへの URL を含むオブジェクトを持つオブジェクトに応答 `task` `value` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-274">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form that you want to load.</span></span> <span data-ttu-id="436e2-275">読み込む URL のドメインは、アプリのマニフェストの配列 `validDomains` に含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-275">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="436e2-276">埋め込み Web ビューの構築の詳細については、タスク モジュールの [ドキュメントを参照してください](~/task-modules-and-cards/what-are-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="436e2-276">For more information on building your embedded web view, see the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md).</span></span> 

# <a name="cnet"></a>[<span data-ttu-id="436e2-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="436e2-277">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="436e2-278">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="436e2-278">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="436e2-279">JSON</span><span class="sxs-lookup"><span data-stu-id="436e2-279">JSON</span></span>](#tab/json)

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="436e2-280">会話型ボットのインストールを要求する</span><span class="sxs-lookup"><span data-stu-id="436e2-280">Request to install your conversational bot</span></span>

<span data-ttu-id="436e2-281">アプリに会話型ボットが含まれている場合は、会話にボットをインストールし、タスク モジュールを読み込む。</span><span class="sxs-lookup"><span data-stu-id="436e2-281">If the app contains a conversational bot, install the bot in the conversation and then load the task module.</span></span> <span data-ttu-id="436e2-282">ボットは、タスク モジュールの追加コンテキストを取得する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="436e2-282">The bot is useful to get additional context for the task module.</span></span> <span data-ttu-id="436e2-283">このシナリオの例は、名簿をフェッチして、ユーザー選択コントロールまたはチーム内のチャネルの一覧を設定します。</span><span class="sxs-lookup"><span data-stu-id="436e2-283">An example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="436e2-284">メッセージング拡張機能が呼び出しを受信したら、ボットが現在のコンテキストにインストールされていることを確認して、フロー `composeExtension/fetchTask` を容易にしてください。</span><span class="sxs-lookup"><span data-stu-id="436e2-284">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="436e2-285">たとえば、取得名簿呼び出しでフローを確認します。</span><span class="sxs-lookup"><span data-stu-id="436e2-285">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="436e2-286">ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。</span><span class="sxs-lookup"><span data-stu-id="436e2-286">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="436e2-287">ユーザーは、チェックのためにその場所にアプリをインストールする権限を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-287">The user must have the permission to install the apps in that location for checking.</span></span> <span data-ttu-id="436e2-288">アプリのインストールが失敗した場合、ユーザーは管理者に連絡するメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="436e2-288">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example"></a><span data-ttu-id="436e2-289">例</span><span class="sxs-lookup"><span data-stu-id="436e2-289">Example</span></span> 

<span data-ttu-id="436e2-290">次のコード セクションは、応答の例です。</span><span class="sxs-lookup"><span data-stu-id="436e2-290">The following code section is an example of the response:</span></span>

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

<span data-ttu-id="436e2-291">会話型ボットのインストール後、別の呼び出しメッセージを受け `name = composeExtension/submitAction` 取ります `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="436e2-291">After the installation of conversational bot, it receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example"></a><span data-ttu-id="436e2-292">例</span><span class="sxs-lookup"><span data-stu-id="436e2-292">Example</span></span> 

<span data-ttu-id="436e2-293">次のコード セクションは、呼び出しに対するタスク応答の例です。</span><span class="sxs-lookup"><span data-stu-id="436e2-293">The following code section is an example of the task response to the invoke:</span></span>

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

<span data-ttu-id="436e2-294">呼び出しに対するタスク応答は、インストールされているボットのタスク応答と似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="436e2-294">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example"></a><span data-ttu-id="436e2-295">例</span><span class="sxs-lookup"><span data-stu-id="436e2-295">Example</span></span> 

<span data-ttu-id="436e2-296">次のコード セクションは、アダプティブ カードを使用したアプリの just-in time インストールの例です。</span><span class="sxs-lookup"><span data-stu-id="436e2-296">The following code section is an example of just-in time installation of app with Adaptive card:</span></span> 

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

## <a name="code-sample"></a><span data-ttu-id="436e2-297">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="436e2-297">Code sample</span></span>

| <span data-ttu-id="436e2-298">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="436e2-298">Sample Name</span></span>           | <span data-ttu-id="436e2-299">説明</span><span class="sxs-lookup"><span data-stu-id="436e2-299">Description</span></span> | <span data-ttu-id="436e2-300">.NET</span><span class="sxs-lookup"><span data-stu-id="436e2-300">.NET</span></span>    | <span data-ttu-id="436e2-301">Node.js</span><span class="sxs-lookup"><span data-stu-id="436e2-301">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="436e2-302">Teams メッセージング拡張機能アクション</span><span class="sxs-lookup"><span data-stu-id="436e2-302">Teams messaging extension action</span></span>| <span data-ttu-id="436e2-303">アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="436e2-303">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="436e2-304">View</span><span class="sxs-lookup"><span data-stu-id="436e2-304">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="436e2-305">View</span><span class="sxs-lookup"><span data-stu-id="436e2-305">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="436e2-306">Teams メッセージング拡張機能の検索</span><span class="sxs-lookup"><span data-stu-id="436e2-306">Teams messaging extension search</span></span>   |  <span data-ttu-id="436e2-307">検索コマンドを定義し、検索に応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="436e2-307">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="436e2-308">View</span><span class="sxs-lookup"><span data-stu-id="436e2-308">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="436e2-309">View</span><span class="sxs-lookup"><span data-stu-id="436e2-309">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="436e2-310">関連項目</span><span class="sxs-lookup"><span data-stu-id="436e2-310">See also</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="436e2-311">操作コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="436e2-311">Define action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a><span data-ttu-id="436e2-312">次の手順</span><span class="sxs-lookup"><span data-stu-id="436e2-312">Next step</span></span>

> [!div class="nextstepaction"] 
> <span data-ttu-id="436e2-313">[[アクションに応答] コマンド](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)</span><span class="sxs-lookup"><span data-stu-id="436e2-313">[Respond to action command](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)</span></span>

