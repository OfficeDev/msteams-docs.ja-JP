---
title: メッセージング拡張機能の開発
description: メッセージング拡張機能の使用を開始する方法について説明Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: teams メッセージング拡張機能メッセージング拡張機能
ms.openlocfilehash: 2301a9af7574c193c7327bb45e38f91bedc73793
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020605"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="0deca-104">ユーザーのメッセージング拡張機能を開発Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0deca-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="0deca-105">メッセージング拡張機能は、ユーザーがユーザーからアプリに参加するための強力なMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="0deca-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="0deca-106">この機能を使用すると、ユーザーはサービスとの間で情報を照会または投稿し、その情報をカード形式でメッセージに投稿できます。</span><span class="sxs-lookup"><span data-stu-id="0deca-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![メッセージング拡張機能カードの例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="0deca-108">メッセージング拡張機能は、作成ボックスの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0deca-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="0deca-109">絵文字、Giphy、ステッカーなど、いくつか組み込みです。</span><span class="sxs-lookup"><span data-stu-id="0deca-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="0deca-110">[その **他のオプション** ]**(&#8943;**) ボタンを選択すると、アプリ ギャラリーから追加したり、自分でアップロードしたりしたメッセージング拡張機能を表示できます。</span><span class="sxs-lookup"><span data-stu-id="0deca-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="0deca-111">メッセージング拡張機能の使い方</span><span class="sxs-lookup"><span data-stu-id="0deca-111">How would you use messaging extensions?</span></span> <span data-ttu-id="0deca-112">いくつかの可能性を次に示します。</span><span class="sxs-lookup"><span data-stu-id="0deca-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="0deca-113">作業項目とバグ</span><span class="sxs-lookup"><span data-stu-id="0deca-113">Work items and bugs</span></span>
* <span data-ttu-id="0deca-114">カスタマー サポート チケット</span><span class="sxs-lookup"><span data-stu-id="0deca-114">Customer support tickets</span></span>
* <span data-ttu-id="0deca-115">使用状況グラフとレポート</span><span class="sxs-lookup"><span data-stu-id="0deca-115">Usage charts and reports</span></span>
* <span data-ttu-id="0deca-116">画像とメディア コンテンツ</span><span class="sxs-lookup"><span data-stu-id="0deca-116">Images and media content</span></span>
* <span data-ttu-id="0deca-117">営業案件とリード</span><span class="sxs-lookup"><span data-stu-id="0deca-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="0deca-118">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="0deca-118">Types of messaging extensions</span></span>

<span data-ttu-id="0deca-119">現在のユーザーに対して作成できるメッセージング拡張機能は、主に 2 Teamsです。</span><span class="sxs-lookup"><span data-stu-id="0deca-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="0deca-120">次のトピックでは、作成プロセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0deca-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="0deca-121">[検索ベースのメッセージング拡張機能](~/resources/messaging-extension-v3/search-extensions.md): サービスに情報を照会し、メッセージに挿入します。</span><span class="sxs-lookup"><span data-stu-id="0deca-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="0deca-122">例: 作業項目を参照する</span><span class="sxs-lookup"><span data-stu-id="0deca-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="0deca-123">[アクション ベースのメッセージング拡張機能](~/resources/messaging-extension-v3/create-extensions.md): ユーザーから情報を収集し、サードパーティ サービスに投稿します。</span><span class="sxs-lookup"><span data-stu-id="0deca-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="0deca-124">例: 作業項目の作成</span><span class="sxs-lookup"><span data-stu-id="0deca-124">Example: Create a work item</span></span>
