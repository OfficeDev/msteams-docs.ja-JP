---
title: タスク モジュールの作成と送信
author: clearab
description: 最初の呼び出しアクションを処理し、アクション メッセージング拡張機能コマンドからタスク モジュールで応答する方法
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fbe90b3a3af8dbb053fdbaf6b4cd9b96344eaf00
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075592"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="849a1-103">タスク モジュールの作成と送信</span><span class="sxs-lookup"><span data-stu-id="849a1-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="849a1-104">アダプティブ カードまたは埋め込み Web ビューを使用してタスク モジュールを作成できます。</span><span class="sxs-lookup"><span data-stu-id="849a1-104">You can create the task module using an Adaptive Card or an embedded web view.</span></span> <span data-ttu-id="849a1-105">タスク モジュールを作成するには、最初の呼び出し要求と呼ばれるプロセスを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-105">To create a task module, you must perform the process called the initial invoke request.</span></span> <span data-ttu-id="849a1-106">このドキュメントでは、最初の呼び出し要求、1:1 チャット、グループ チャット、チャネル (新しい投稿)、チャネル (スレッドへの返信)、およびコマンド ボックスからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="849a1-106">This document covers the initial invoke request, payload activity properties when a task module is invoked from 1:1 chat, group chat, channel (new post), channel (reply to thread), and command box.</span></span> 
> [!NOTE]
> <span data-ttu-id="849a1-107">アプリ マニフェストで定義されたパラメーターをタスク モジュールに設定しない場合は、アダプティブ カードまたは埋め込み Web ビューを使用するユーザー用のタスク モジュールを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-107">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users with either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="849a1-108">最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="849a1-108">The initial invoke request</span></span>

<span data-ttu-id="849a1-109">最初の呼び出し要求のプロセスで、サービスは型のオブジェクトを受け取り、アダプティブ カードまたは埋め込み Web ビューへの URL を含むオブジェクトで応答する `Activity` `composeExtension/fetchTask` `task` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-109">In the process of the initial invoke request, your service receives an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either an Adaptive Card or a URL to the embedded web view.</span></span> <span data-ttu-id="849a1-110">ボットアクティビティの標準プロパティと共に、最初の呼び出しペイロードには次の要求メタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="849a1-110">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="849a1-111">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-111">Property name</span></span>|<span data-ttu-id="849a1-112">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-112">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="849a1-113">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-113">Type of request.</span></span> <span data-ttu-id="849a1-114">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-114">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="849a1-115">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-115">Type of command that is issued to your service.</span></span> <span data-ttu-id="849a1-116">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-116">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="849a1-117">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-117">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="849a1-118">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="849a1-118">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="849a1-119">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-119">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="849a1-120">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-120">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="849a1-121">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="849a1-121">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="849a1-122">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="849a1-122">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="849a1-123">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="849a1-123">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="849a1-124">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="849a1-124">The context that triggered the event.</span></span> <span data-ttu-id="849a1-125">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-125">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="849a1-126">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="849a1-126">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="849a1-127">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-127">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="849a1-128">例</span><span class="sxs-lookup"><span data-stu-id="849a1-128">Example</span></span>

<span data-ttu-id="849a1-129">最初の呼び出し要求のコードは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="849a1-129">The code for the initial invoke request is given in the following example:</span></span>

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a><span data-ttu-id="849a1-130">タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティプロパティ</span><span class="sxs-lookup"><span data-stu-id="849a1-130">Payload activity properties when a task module is invoked from 1:1 chat</span></span> 

<span data-ttu-id="849a1-131">タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティのプロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="849a1-131">The payload activity properties when a task module is invoked from 1:1 chat are listed as follows:</span></span>

|<span data-ttu-id="849a1-132">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-132">Property name</span></span>|<span data-ttu-id="849a1-133">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-133">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="849a1-134">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-134">Type of request.</span></span> <span data-ttu-id="849a1-135">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-135">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="849a1-136">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-136">Type of command that is issued to your service.</span></span> <span data-ttu-id="849a1-137">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-137">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="849a1-138">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-138">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="849a1-139">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="849a1-139">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="849a1-140">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-140">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="849a1-141">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-141">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="849a1-142">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="849a1-142">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="849a1-143">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="849a1-143">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="849a1-144">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="849a1-144">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="849a1-145">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="849a1-145">The context that triggered the event.</span></span> <span data-ttu-id="849a1-146">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-146">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="849a1-147">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="849a1-147">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="849a1-148">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-148">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="849a1-149">例</span><span class="sxs-lookup"><span data-stu-id="849a1-149">Example</span></span>

<span data-ttu-id="849a1-150">タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティプロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="849a1-150">The payload activity properties when a task module is invoked from 1:1 chat are given in the following example:</span></span>

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
## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a><span data-ttu-id="849a1-151">グループ チャットからタスク モジュールが呼び出された場合のペイロード アクティビティのプロパティ</span><span class="sxs-lookup"><span data-stu-id="849a1-151">Payload activity properties when a task module is invoked from a group chat</span></span> 

<span data-ttu-id="849a1-152">タスク モジュールがグループ チャットから呼び出された場合のペイロード アクティビティのプロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="849a1-152">The payload activity properties when a task module is invoked from a group chat are listed as follows:</span></span>

|<span data-ttu-id="849a1-153">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-153">Property name</span></span>|<span data-ttu-id="849a1-154">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-154">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="849a1-155">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-155">Type of request.</span></span> <span data-ttu-id="849a1-156">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-156">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="849a1-157">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-157">Type of command that is issued to your service.</span></span> <span data-ttu-id="849a1-158">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-158">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="849a1-159">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-159">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="849a1-160">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="849a1-160">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="849a1-161">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-161">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="849a1-162">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-162">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="849a1-163">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="849a1-163">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="849a1-164">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="849a1-164">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="849a1-165">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="849a1-165">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="849a1-166">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="849a1-166">The context that triggered the event.</span></span> <span data-ttu-id="849a1-167">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-167">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="849a1-168">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="849a1-168">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="849a1-169">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-169">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="849a1-170">例</span><span class="sxs-lookup"><span data-stu-id="849a1-170">Example</span></span>

<span data-ttu-id="849a1-171">タスク モジュールがグループ チャットから呼び出された場合のペイロード アクティビティプロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="849a1-171">The payload activity properties when a task module is invoked from a group chat are given in the following example:</span></span>

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a><span data-ttu-id="849a1-172">チャネルからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティ (新しい投稿)</span><span class="sxs-lookup"><span data-stu-id="849a1-172">Payload activity properties when a task module is invoked from a channel (new post)</span></span> 

<span data-ttu-id="849a1-173">タスク モジュールがチャネル (新しい投稿) から呼び出された場合のペイロード アクティビティプロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="849a1-173">The payload activity properties when a task module is invoked from a channel (new post) are listed as follows:</span></span>

|<span data-ttu-id="849a1-174">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-174">Property name</span></span>|<span data-ttu-id="849a1-175">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-175">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="849a1-176">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-176">Type of request.</span></span> <span data-ttu-id="849a1-177">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-177">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="849a1-178">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-178">Type of command that is issued to your service.</span></span> <span data-ttu-id="849a1-179">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-179">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="849a1-180">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-180">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="849a1-181">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="849a1-181">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="849a1-182">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-182">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="849a1-183">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-183">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="849a1-184">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="849a1-184">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="849a1-185">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="849a1-185">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="849a1-186">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="849a1-186">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="849a1-187">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="849a1-187">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="849a1-188">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="849a1-188">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="849a1-189">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="849a1-189">The context that triggered the event.</span></span> <span data-ttu-id="849a1-190">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-190">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="849a1-191">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="849a1-191">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="849a1-192">、、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-192">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="849a1-193">例</span><span class="sxs-lookup"><span data-stu-id="849a1-193">Example</span></span>

<span data-ttu-id="849a1-194">タスク モジュールがチャネル (新しい投稿) から呼び出された場合のペイロード アクティビティ プロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="849a1-194">The payload activity properties when a task module is invoked from a channel (new post) are given in the following example:</span></span>

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a><span data-ttu-id="849a1-195">チャネルからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティ (スレッドに返信)</span><span class="sxs-lookup"><span data-stu-id="849a1-195">Payload activity properties when a task module is invoked from a channel (reply to thread)</span></span> 

<span data-ttu-id="849a1-196">タスク モジュールがチャネルから呼び出された場合のペイロード アクティビティ プロパティ (スレッドへの返信) は、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="849a1-196">The payload activity properties when a task module is invoked from a channel (reply to thread) are listed as follows:</span></span>

|<span data-ttu-id="849a1-197">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-197">Property name</span></span>|<span data-ttu-id="849a1-198">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-198">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="849a1-199">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-199">Type of request.</span></span> <span data-ttu-id="849a1-200">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-200">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="849a1-201">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-201">Type of command that is issued to your service.</span></span> <span data-ttu-id="849a1-202">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-202">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="849a1-203">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-203">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="849a1-204">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="849a1-204">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="849a1-205">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-205">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="849a1-206">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-206">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="849a1-207">チャネル ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="849a1-207">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="849a1-208">チーム ID (チャネルで要求が行われた場合)。</span><span class="sxs-lookup"><span data-stu-id="849a1-208">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="849a1-209">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="849a1-209">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="849a1-210">このメッセージが返信であるメッセージの ID を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="849a1-210">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="849a1-211">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="849a1-211">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="849a1-212">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="849a1-212">The context that triggered the event.</span></span> <span data-ttu-id="849a1-213">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-213">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="849a1-214">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="849a1-214">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="849a1-215">は、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-215">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="849a1-216">例</span><span class="sxs-lookup"><span data-stu-id="849a1-216">Example</span></span>

<span data-ttu-id="849a1-217">タスク モジュールがチャネルから呼び出された場合のペイロード アクティビティ プロパティ (スレッドへの返信) は、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="849a1-217">The payload activity properties when a task module is invoked from a channel (reply to thread) are given in the following example:</span></span>

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a><span data-ttu-id="849a1-218">タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティ</span><span class="sxs-lookup"><span data-stu-id="849a1-218">Payload activity properties when a task module is invoked from a command box</span></span> 

<span data-ttu-id="849a1-219">タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="849a1-219">The payload activity properties when a task module is invoked from a command box are listed as follows:</span></span>

|<span data-ttu-id="849a1-220">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-220">Property name</span></span>|<span data-ttu-id="849a1-221">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-221">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="849a1-222">要求の種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-222">Type of request.</span></span> <span data-ttu-id="849a1-223">この値は、 である必要があります `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-223">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="849a1-224">サービスに発行されるコマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="849a1-224">Type of command that is issued to your service.</span></span> <span data-ttu-id="849a1-225">この値は、 である必要があります `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-225">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="849a1-226">要求を送信したユーザーの ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-226">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="849a1-227">要求を送信したユーザーの名前。</span><span class="sxs-lookup"><span data-stu-id="849a1-227">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="849a1-228">要求を送信したユーザーの Azure Active Directory オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-228">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="849a1-229">Azure Active Directory テナント ID。</span><span class="sxs-lookup"><span data-stu-id="849a1-229">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="849a1-230">タスク モジュールの呼び出し元のソース名。</span><span class="sxs-lookup"><span data-stu-id="849a1-230">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="849a1-231">呼び出されたコマンドの ID が含まれる。</span><span class="sxs-lookup"><span data-stu-id="849a1-231">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="849a1-232">イベントをトリガーしたコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="849a1-232">The context that triggered the event.</span></span> <span data-ttu-id="849a1-233">この値は、 である必要があります `compose` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-233">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="849a1-234">ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="849a1-234">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="849a1-235">、、または `default` `contrast` である必要があります `dark` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-235">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="849a1-236">例</span><span class="sxs-lookup"><span data-stu-id="849a1-236">Example</span></span>

<span data-ttu-id="849a1-237">タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティは、次の例で示されています。</span><span class="sxs-lookup"><span data-stu-id="849a1-237">The payload activity properties when a task module is invoked from a command box are given in the following example:</span></span>

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

### <a name="example"></a><span data-ttu-id="849a1-238">例</span><span class="sxs-lookup"><span data-stu-id="849a1-238">Example</span></span> 

<span data-ttu-id="849a1-239">次のコード セクションは、要求の例 `fetchTask` です。</span><span class="sxs-lookup"><span data-stu-id="849a1-239">The following code section is an example of `fetchTask` request:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="849a1-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="849a1-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="849a1-241">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="849a1-241">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="849a1-242">JSON</span><span class="sxs-lookup"><span data-stu-id="849a1-242">JSON</span></span>](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="849a1-243">メッセージからの最初の呼び出し要求</span><span class="sxs-lookup"><span data-stu-id="849a1-243">Initial invoke request from a message</span></span>

<span data-ttu-id="849a1-244">ボットがメッセージから呼び出されると、最初の呼び出し要求のオブジェクトに、メッセージング拡張機能が呼び出されるメッセージの詳細が `value` 含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-244">When your bot is invoked from a message,  the `value` object in the initial invoke request must contain the details of the message that your messaging extension is invoked from.</span></span> <span data-ttu-id="849a1-245">配列 `reactions` と配列は省略可能で、元のメッセージにリアクションやメンションがない場合は `mentions` 存在しません。</span><span class="sxs-lookup"><span data-stu-id="849a1-245">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span> <span data-ttu-id="849a1-246">次のセクションは、オブジェクトの例 `value` です。</span><span class="sxs-lookup"><span data-stu-id="849a1-246">The following section is an example of the `value` object:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="849a1-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="849a1-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="849a1-248">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="849a1-248">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="849a1-249">JSON</span><span class="sxs-lookup"><span data-stu-id="849a1-249">JSON</span></span>](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="849a1-250">fetchTask に応答する</span><span class="sxs-lookup"><span data-stu-id="849a1-250">Respond to the fetchTask</span></span>

<span data-ttu-id="849a1-251">アダプティブ カードまたは Web URL を持つオブジェクト、または単純な文字列メッセージを含むオブジェクトを使用して、呼び出し要求 `task` `taskInfo` に応答します。</span><span class="sxs-lookup"><span data-stu-id="849a1-251">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the Adaptive Card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="849a1-252">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-252">Property name</span></span>|<span data-ttu-id="849a1-253">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-253">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="849a1-254">フォームを表示 `continue` するか、単純な `message` ポップアップを表示できます。</span><span class="sxs-lookup"><span data-stu-id="849a1-254">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="849a1-255">フォーム `taskInfo` のオブジェクト、またはメッセージ `string` の a。</span><span class="sxs-lookup"><span data-stu-id="849a1-255">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="849a1-256">taskInfo オブジェクトのスキーマは次の値です。</span><span class="sxs-lookup"><span data-stu-id="849a1-256">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="849a1-257">プロパティ名</span><span class="sxs-lookup"><span data-stu-id="849a1-257">Property name</span></span>|<span data-ttu-id="849a1-258">用途</span><span class="sxs-lookup"><span data-stu-id="849a1-258">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="849a1-259">タスク モジュールのタイトル。</span><span class="sxs-lookup"><span data-stu-id="849a1-259">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="849a1-260">整数 (ピクセル単位) または 、 `small` 、 のいずれか `medium` である必要があります `large` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-260">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="849a1-261">整数 (ピクセル単位) または 、 `small` 、 のいずれか `medium` である必要があります `large` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-261">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="849a1-262">フォームを定義するアダプティブ カード (使用している場合)。</span><span class="sxs-lookup"><span data-stu-id="849a1-262">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="849a1-263">埋め込み Web ビューとしてタスク モジュール内で開く URL。</span><span class="sxs-lookup"><span data-stu-id="849a1-263">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="849a1-264">クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。</span><span class="sxs-lookup"><span data-stu-id="849a1-264">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a><span data-ttu-id="849a1-265">アダプティブ カードを使用して fetchTask に応答する</span><span class="sxs-lookup"><span data-stu-id="849a1-265">Respond to the fetchTask with an Adaptive Card</span></span>

<span data-ttu-id="849a1-266">アダプティブ カードを使用する場合は、アダプティブ カードを含むオブジェクトでオブジェクト `task` `value` に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-266">When using an adaptive card, you must respond with a `task` object with the `value` object containing an Adaptive Card.</span></span>

#### <a name="example"></a><span data-ttu-id="849a1-267">例</span><span class="sxs-lookup"><span data-stu-id="849a1-267">Example</span></span>

<span data-ttu-id="849a1-268">次のコード セクションは、アダプティブ カードで `fetchTask` 応答する例です。</span><span class="sxs-lookup"><span data-stu-id="849a1-268">The following code section is an example to `fetchTask` response with an adaptive card:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="849a1-269">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="849a1-269">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="849a1-270">このサンプルでは、Bot Framework SDK に加えて [AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="849a1-270">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="849a1-271">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="849a1-271">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="849a1-272">JSON</span><span class="sxs-lookup"><span data-stu-id="849a1-272">JSON</span></span>](#tab/json)

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

### <a name="create-a-task-module-with-an-embedded-web-view"></a><span data-ttu-id="849a1-273">埋め込み Web ビューを使用してタスク モジュールを作成する</span><span class="sxs-lookup"><span data-stu-id="849a1-273">Create a task module with an embedded web view</span></span>

<span data-ttu-id="849a1-274">埋め込み Web ビューを使用する場合は、読み込む Web フォームへの URL を含むオブジェクトを持つオブジェクトに応答 `task` `value` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-274">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form that you want to load.</span></span> <span data-ttu-id="849a1-275">読み込む URL のドメインは、アプリのマニフェストの配列 `validDomains` に含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-275">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="849a1-276">埋め込み Web ビューの構築の詳細については、タスク モジュールの [ドキュメントを参照してください](~/task-modules-and-cards/what-are-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="849a1-276">For more information on building your embedded web view, see the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md).</span></span> 

# <a name="cnet"></a>[<span data-ttu-id="849a1-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="849a1-277">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="849a1-278">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="849a1-278">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="849a1-279">JSON</span><span class="sxs-lookup"><span data-stu-id="849a1-279">JSON</span></span>](#tab/json)

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="849a1-280">会話型ボットのインストールを要求する</span><span class="sxs-lookup"><span data-stu-id="849a1-280">Request to install your conversational bot</span></span>

<span data-ttu-id="849a1-281">アプリに会話型ボットが含まれている場合は、会話にボットをインストールし、タスク モジュールを読み込む。</span><span class="sxs-lookup"><span data-stu-id="849a1-281">If the app contains a conversational bot, install the bot in the conversation and then load the task module.</span></span> <span data-ttu-id="849a1-282">ボットは、タスク モジュールの追加コンテキストを取得する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="849a1-282">The bot is useful to get additional context for the task module.</span></span> <span data-ttu-id="849a1-283">このシナリオの例は、名簿をフェッチして、ユーザー選択コントロールまたはチーム内のチャネルの一覧を設定します。</span><span class="sxs-lookup"><span data-stu-id="849a1-283">An example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="849a1-284">メッセージング拡張機能が呼び出しを受信したら、ボットが現在のコンテキストにインストールされていることを確認して、フロー `composeExtension/fetchTask` を容易にしてください。</span><span class="sxs-lookup"><span data-stu-id="849a1-284">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="849a1-285">たとえば、取得名簿呼び出しでフローを確認します。</span><span class="sxs-lookup"><span data-stu-id="849a1-285">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="849a1-286">ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。</span><span class="sxs-lookup"><span data-stu-id="849a1-286">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="849a1-287">ユーザーは、チェックのためにその場所にアプリをインストールする権限を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-287">The user must have the permission to install the apps in that location for checking.</span></span> <span data-ttu-id="849a1-288">アプリのインストールが失敗した場合、ユーザーは管理者に連絡するメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="849a1-288">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example"></a><span data-ttu-id="849a1-289">例</span><span class="sxs-lookup"><span data-stu-id="849a1-289">Example</span></span> 

<span data-ttu-id="849a1-290">次のコード セクションは、応答の例です。</span><span class="sxs-lookup"><span data-stu-id="849a1-290">The following code section is an example of the response:</span></span>

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

<span data-ttu-id="849a1-291">会話型ボットのインストール後、別の呼び出しメッセージを受け `name = composeExtension/submitAction` 取ります `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="849a1-291">After the installation of conversational bot, it receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example"></a><span data-ttu-id="849a1-292">例</span><span class="sxs-lookup"><span data-stu-id="849a1-292">Example</span></span> 

<span data-ttu-id="849a1-293">次のコード セクションは、呼び出しに対するタスク応答の例です。</span><span class="sxs-lookup"><span data-stu-id="849a1-293">The following code section is an example of the task response to the invoke:</span></span>

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

<span data-ttu-id="849a1-294">呼び出しに対するタスク応答は、インストールされているボットのタスク応答と似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="849a1-294">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example"></a><span data-ttu-id="849a1-295">例</span><span class="sxs-lookup"><span data-stu-id="849a1-295">Example</span></span> 

<span data-ttu-id="849a1-296">次のコード セクションは、アダプティブ カードを使用したアプリの just-in time インストールの例です。</span><span class="sxs-lookup"><span data-stu-id="849a1-296">The following code section is an example of just-in time installation of app with Adaptive card:</span></span> 

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

## <a name="code-sample"></a><span data-ttu-id="849a1-297">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="849a1-297">Code sample</span></span>

| <span data-ttu-id="849a1-298">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="849a1-298">Sample Name</span></span>           | <span data-ttu-id="849a1-299">説明</span><span class="sxs-lookup"><span data-stu-id="849a1-299">Description</span></span> | <span data-ttu-id="849a1-300">.NET</span><span class="sxs-lookup"><span data-stu-id="849a1-300">.NET</span></span>    | <span data-ttu-id="849a1-301">Node.js</span><span class="sxs-lookup"><span data-stu-id="849a1-301">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="849a1-302">Teams メッセージング拡張機能アクション</span><span class="sxs-lookup"><span data-stu-id="849a1-302">Teams messaging extension action</span></span>| <span data-ttu-id="849a1-303">アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="849a1-303">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="849a1-304">View</span><span class="sxs-lookup"><span data-stu-id="849a1-304">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="849a1-305">View</span><span class="sxs-lookup"><span data-stu-id="849a1-305">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="849a1-306">Teams メッセージング拡張機能の検索</span><span class="sxs-lookup"><span data-stu-id="849a1-306">Teams messaging extension search</span></span>   |  <span data-ttu-id="849a1-307">検索コマンドを定義し、検索に応答する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="849a1-307">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="849a1-308">View</span><span class="sxs-lookup"><span data-stu-id="849a1-308">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="849a1-309">View</span><span class="sxs-lookup"><span data-stu-id="849a1-309">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="849a1-310">関連項目</span><span class="sxs-lookup"><span data-stu-id="849a1-310">See also</span></span>

[<span data-ttu-id="849a1-311">操作コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="849a1-311">Define action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a><span data-ttu-id="849a1-312">次の手順</span><span class="sxs-lookup"><span data-stu-id="849a1-312">Next step</span></span>

> [!div class="nextstepaction"] 
> <span data-ttu-id="849a1-313">[[アクションに応答] コマンド](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)</span><span class="sxs-lookup"><span data-stu-id="849a1-313">[Respond to action command](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)</span></span>

