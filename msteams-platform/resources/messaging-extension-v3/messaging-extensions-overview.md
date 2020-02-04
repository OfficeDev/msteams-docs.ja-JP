---
title: メッセージング拡張機能を開発する
description: Microsoft Teams でのメッセージング拡張機能の使用を開始する方法について説明します。
keywords: teams メッセージング拡張メッセージング拡張機能
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674651"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="89fc5-104">Microsoft Teams のメッセージング拡張機能を開発する</span><span class="sxs-lookup"><span data-stu-id="89fc5-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="89fc5-105">メッセージング拡張機能は、ユーザーが Microsoft Teams からアプリを利用できるようにするための強力な手段です。</span><span class="sxs-lookup"><span data-stu-id="89fc5-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="89fc5-106">この機能を使用すると、ユーザーはサービスとの間で情報を照会したり、その情報をカード形式でメッセージに投稿したりできます。</span><span class="sxs-lookup"><span data-stu-id="89fc5-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="89fc5-108">メッセージング拡張機能は、[新規作成] ボックスの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="89fc5-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="89fc5-109">絵文字、Giphy、ステッカーなどのいくつかのが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="89fc5-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="89fc5-110">[その他の**オプション**(**&#8943;**)] ボタンをクリックして、他のメッセージング拡張機能 (アプリギャラリーから追加したものや自分でアップロードしたものなど) を表示します。</span><span class="sxs-lookup"><span data-stu-id="89fc5-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="89fc5-111">メッセージング拡張機能の使用方法</span><span class="sxs-lookup"><span data-stu-id="89fc5-111">How would you use messaging extensions?</span></span> <span data-ttu-id="89fc5-112">いくつかの可能性があります。</span><span class="sxs-lookup"><span data-stu-id="89fc5-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="89fc5-113">作業項目とバグ</span><span class="sxs-lookup"><span data-stu-id="89fc5-113">Work items and bugs</span></span>
* <span data-ttu-id="89fc5-114">カスタマーサポートチケット</span><span class="sxs-lookup"><span data-stu-id="89fc5-114">Customer support tickets</span></span>
* <span data-ttu-id="89fc5-115">使用状況のグラフとレポート</span><span class="sxs-lookup"><span data-stu-id="89fc5-115">Usage charts and reports</span></span>
* <span data-ttu-id="89fc5-116">画像とメディアコンテンツ</span><span class="sxs-lookup"><span data-stu-id="89fc5-116">Images and media content</span></span>
* <span data-ttu-id="89fc5-117">営業案件と潜在顧客</span><span class="sxs-lookup"><span data-stu-id="89fc5-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="89fc5-118">メッセージング拡張機能の種類</span><span class="sxs-lookup"><span data-stu-id="89fc5-118">Types of messaging extensions</span></span>

<span data-ttu-id="89fc5-119">チーム向けに作成できるメッセージング拡張機能には、主に2つの種類があります。</span><span class="sxs-lookup"><span data-stu-id="89fc5-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="89fc5-120">次のトピックでは、これらの作成手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="89fc5-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="89fc5-121">[検索ベースのメッセージング拡張](~/resources/messaging-extension-v3/search-extensions.md): サービスに情報を照会して、それをメッセージに挿入します。</span><span class="sxs-lookup"><span data-stu-id="89fc5-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="89fc5-122">例: 作業項目を検索する</span><span class="sxs-lookup"><span data-stu-id="89fc5-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="89fc5-123">[アクションベースのメッセージング拡張](~/resources/messaging-extension-v3/create-extensions.md): ユーザーから情報を収集し、サードパーティのサービスに投稿します。</span><span class="sxs-lookup"><span data-stu-id="89fc5-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="89fc5-124">例: 作業項目を作成する</span><span class="sxs-lookup"><span data-stu-id="89fc5-124">Example: Create a work item</span></span>
