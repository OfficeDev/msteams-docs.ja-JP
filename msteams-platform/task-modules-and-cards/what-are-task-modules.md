---
title: タスク モジュール
author: surbhigupta
description: モーダル ポップアップ エクスペリエンスを追加して、アプリからユーザーに情報を収集または表示Microsoft Teamsします。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 257ca54ab53d310116cc301dded01a7582c11532
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140538"
---
# <a name="task-modules"></a><span data-ttu-id="9a993-103">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="9a993-103">Task modules</span></span>

<span data-ttu-id="9a993-104">タスク モジュールを使用すると、アプリケーションでモーダル ポップアップ エクスペリエンスをTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="9a993-104">Task modules permit you to create modal pop-up experiences in your Teams application.</span></span> <span data-ttu-id="9a993-105">ポップアップでは、次の方法を実行できます。</span><span class="sxs-lookup"><span data-stu-id="9a993-105">In the pop-up, you can:</span></span>

* <span data-ttu-id="9a993-106">独自のカスタム HTML または JavaScript コードを実行します。</span><span class="sxs-lookup"><span data-stu-id="9a993-106">Run your own custom HTML or JavaScript code.</span></span>
* <span data-ttu-id="9a993-107">`<iframe>`YouTube や Microsoft Stream ビデオなどの -based ウィジェットを表示します。</span><span class="sxs-lookup"><span data-stu-id="9a993-107">Show an `<iframe>`-based widget such as a YouTube or Microsoft Stream video.</span></span>
* <span data-ttu-id="9a993-108">アダプティブ カード [を表示します](/adaptive-cards/)。</span><span class="sxs-lookup"><span data-stu-id="9a993-108">Display an [Adaptive Card](/adaptive-cards/).</span></span>

<span data-ttu-id="9a993-109">タスク モジュールは、タスクの開始と完了、またはビデオや Power Business Intelligence (BI) ダッシュボードなどの豊富な情報の表示に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9a993-109">Task modules are useful for initiating and completing tasks or displaying rich information, such as videos or Power Business Intelligence (BI) dashboards.</span></span> <span data-ttu-id="9a993-110">多くの場合、ポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスと比較して、ユーザーがタスクを開始して完了する方が自然です。</span><span class="sxs-lookup"><span data-stu-id="9a993-110">A pop-up experience is often more natural for users initiating and completing tasks compared to a tab or a conversation-based bot experience.</span></span>

<span data-ttu-id="9a993-111">タスク モジュールは、タブの基礎Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="9a993-111">Task modules build on the foundation of Microsoft Teams tabs.</span></span> <span data-ttu-id="9a993-112">基本的には、ポップアップ ウィンドウ内のタブです。</span><span class="sxs-lookup"><span data-stu-id="9a993-112">They are essentially a tab inside a pop-up window.</span></span> <span data-ttu-id="9a993-113">同じ SDK を使用します。タブを作成している場合は、タスク モジュールの作成に慣れ親しまれています。</span><span class="sxs-lookup"><span data-stu-id="9a993-113">They use the same SDK, so if you have built a tab you are already familiar with creating a task module.</span></span>

<span data-ttu-id="9a993-114">タスク モジュールは次の 3 つの方法で呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="9a993-114">Task modules can be invoked in three ways:</span></span>

* <span data-ttu-id="9a993-115">チャネルまたは個人用タブ: タブ SDK Microsoft Teamsを使用して、タブのボタン、リンク、またはメニューからタスク モジュールを呼び出します。詳細については、「タブでのタスク[モジュールの使用」を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="9a993-115">Channel or personal tabs: Using the Microsoft Teams Tabs SDK, you can invoke task modules from buttons, links, or menus on your tab. For more information, see [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>
* <span data-ttu-id="9a993-116">ボット: ボットから送信された [カードでボタン](~/task-modules-and-cards/cards/cards-reference.md) を使用する。</span><span class="sxs-lookup"><span data-stu-id="9a993-116">Bots: Using buttons on [cards](~/task-modules-and-cards/cards/cards-reference.md) sent from your bot.</span></span> <span data-ttu-id="9a993-117">これは、チャネル内のすべてのユーザーがボットで何をしているのかを確認する必要が生じない場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="9a993-117">This is useful when you do not require everyone in a channel to see what you are doing with a bot.</span></span> <span data-ttu-id="9a993-118">たとえば、ユーザーがチャネル内のポーリングに応答する場合、そのポーリングのレコードが作成されているのを見るのは役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="9a993-118">For example, when having users respond to a poll in a channel it is not useful to see a record of that poll being created.</span></span> <span data-ttu-id="9a993-119">詳細については、「タスク モジュール[の使用」を参照Teamsしてください](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="9a993-119">For more information, see [using task modules from Teams bots](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>
* <span data-ttu-id="9a993-120">ディープ リンクTeams外部: どこからでもタスク モジュールを呼び出す URL を作成できます。</span><span class="sxs-lookup"><span data-stu-id="9a993-120">Outside of Teams from a deep link: You can also create URLs to invoke a task module from anywhere.</span></span> <span data-ttu-id="9a993-121">詳細については、「タスク モジュールの [ディープ リンク構文」を参照してください](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)。</span><span class="sxs-lookup"><span data-stu-id="9a993-121">For more information, see [task module deep link syntax](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax).</span></span>

## <a name="components-of-a-task-module"></a><span data-ttu-id="9a993-122">タスク モジュールのコンポーネント</span><span class="sxs-lookup"><span data-stu-id="9a993-122">Components of a task module</span></span>

<span data-ttu-id="9a993-123">ボットから呼び出された場合のタスク モジュールの外観を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9a993-123">Here is what a task module looks like when invoked from a bot:</span></span>

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="9a993-125">タスク モジュールには、前の図に示すように、次の内容が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9a993-125">A task module includes the following as shown in the previous image:</span></span>

1. <span data-ttu-id="9a993-126">アプリのアイコン[ `color` です](~/resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="9a993-126">Your app's [`color` icon](~/resources/schema/manifest-schema.md#icons).</span></span>
2. <span data-ttu-id="9a993-127">アプリ[ `short` の名前です](~/resources/schema/manifest-schema.md#name)。</span><span class="sxs-lookup"><span data-stu-id="9a993-127">Your app's [`short` name](~/resources/schema/manifest-schema.md#name).</span></span>
3. <span data-ttu-id="9a993-128">TaskInfo オブジェクトのプロパティで指定 `title` されたタスク モジュール [のタイトル](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)です。</span><span class="sxs-lookup"><span data-stu-id="9a993-128">The task module's title specified in the `title` property of the [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span>
4. <span data-ttu-id="9a993-129">タスク モジュールの [閉じる] または [キャンセル] ボタン。</span><span class="sxs-lookup"><span data-stu-id="9a993-129">The task module's close or cancel button.</span></span> <span data-ttu-id="9a993-130">ユーザーがこのボタンを選択すると、アプリはイベントを受け取 `err` ります。</span><span class="sxs-lookup"><span data-stu-id="9a993-130">If the user selects this button, your app receives an `err` event.</span></span> <span data-ttu-id="9a993-131">詳細については、タスク モジュール [の結果を送信する例を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="9a993-131">For more information, see [example for submitting the result of a task module](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a993-132">現在、タスク モジュールがボットから呼び出された場合、イベント `err` を検出できない。</span><span class="sxs-lookup"><span data-stu-id="9a993-132">It is currently not possible to detect the `err` event when a task module is invoked from a bot.</span></span>

5. <span data-ttu-id="9a993-133">青い四角形は、TaskInfo オブジェクトのプロパティを使用して独自の Web ページを読み込む場合に Web ページ `url` が [表示される場所です](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="9a993-133">The blue rectangle is where your web page appears if you are loading your own web page using the `url` property of the [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="9a993-134">詳細については、「タスク モジュールの [サイズ変更」を参照してください](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="9a993-134">For more information, see [task module sizing](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing).</span></span>
6. <span data-ttu-id="9a993-135">TaskInfo オブジェクトのプロパティを使用してアダプティブ カードを表示する場合 `card` [は](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 、パディングが追加されます。</span><span class="sxs-lookup"><span data-stu-id="9a993-135">If you are displaying an Adaptive Card using the `card` property of the [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) the padding is added for you.</span></span> <span data-ttu-id="9a993-136">詳細については、「HTML または JavaScript タスク モジュールの [タスク モジュール CSS」を参照してください](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)。</span><span class="sxs-lookup"><span data-stu-id="9a993-136">For more information, see [task module CSS for HTML or JavaScript task modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules).</span></span>
7. <span data-ttu-id="9a993-137">[サインアップ] を選択すると、アダプティブ カード ボタン **がレンダリングされます**。</span><span class="sxs-lookup"><span data-stu-id="9a993-137">Adaptive Card buttons render after you select **Sign up**.</span></span> <span data-ttu-id="9a993-138">独自のページを使用する場合は、独自のボタンを作成します。</span><span class="sxs-lookup"><span data-stu-id="9a993-138">When using your own page, create your own buttons.</span></span>

## <a name="see-also"></a><span data-ttu-id="9a993-139">関連項目</span><span class="sxs-lookup"><span data-stu-id="9a993-139">See also</span></span>

[<span data-ttu-id="9a993-140">カード</span><span class="sxs-lookup"><span data-stu-id="9a993-140">Cards</span></span>](~/task-modules-and-cards/what-are-cards.md)

## <a name="next-step"></a><span data-ttu-id="9a993-141">次の手順</span><span class="sxs-lookup"><span data-stu-id="9a993-141">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a993-142">タスク モジュールの呼び出しと終了</span><span class="sxs-lookup"><span data-stu-id="9a993-142">Invoke and dismiss task modules</span></span>](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
