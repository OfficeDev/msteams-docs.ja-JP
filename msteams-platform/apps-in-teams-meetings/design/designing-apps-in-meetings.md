---
title: 会議拡張機能の設計
author: heath-hamilton
description: 会議でアプリを設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a08e5a850a62b0cf73661d00e07e55e46abce32f
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335411"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="7220c-103">会議の拡張機能Microsoft Teams設計する</span><span class="sxs-lookup"><span data-stu-id="7220c-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="7220c-104">アプリを作成して、会議の生産性を高めることができます。</span><span class="sxs-lookup"><span data-stu-id="7220c-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="7220c-105">たとえば、通話中にアンケートを完了したり、会議のフローを中断しない簡単なリマインダーを送信したりします。</span><span class="sxs-lookup"><span data-stu-id="7220c-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="7220c-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="7220c-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="7220c-107">必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。</span><span class="sxs-lookup"><span data-stu-id="7220c-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7220c-108">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="7220c-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="7220c-109">会議の拡張機能を追加する</span><span class="sxs-lookup"><span data-stu-id="7220c-109">Add a meeting extension</span></span>

<span data-ttu-id="7220c-110">ユーザーは、会議の前と会議中に会議拡張機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="7220c-111">また、特定の会議用のアプリを、その会議ストアから直接Teamsすることもできます。</span><span class="sxs-lookup"><span data-stu-id="7220c-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="7220c-112">会議の前に追加する</span><span class="sxs-lookup"><span data-stu-id="7220c-112">Add before a meeting</span></span>

<span data-ttu-id="7220c-113">会議の詳細で、ユーザーは [タブの追加 **] +** を選択してアプリの飛び出しを開き、会議用に最適化されたアプリを検索できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線情報を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="7220c-115">会議中に追加する</span><span class="sxs-lookup"><span data-stu-id="7220c-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7220c-116">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="7220c-116">Desktop</span></span>](#tab/desktop)

会議で、ユーザーは [アプリの **追加]** を選択 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **し**、必要なアプリを選択できます。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線情報を追加する方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7220c-119">モバイル</span><span class="sxs-lookup"><span data-stu-id="7220c-119">Mobile</span></span>](#tab/mobile)

デスクトップにアプリを追加した後、アプリを選択し、[その他] を選択して会議でアプリを使用 **できます** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 。

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="例は、モバイルでの会議中に会議の内線情報を追加する方法を示しています。" border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="7220c-122">会議の前</span><span class="sxs-lookup"><span data-stu-id="7220c-122">Before a meeting</span></span>

<span data-ttu-id="7220c-123">会議の前に、ユーザーはタブにコンテンツを追加できます。次の例は、通話中に回答するアンケートの下書き質問を示しています。</span><span class="sxs-lookup"><span data-stu-id="7220c-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細でコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="7220c-125">解剖学: [会議] タブ (会議の前と後)</span><span class="sxs-lookup"><span data-stu-id="7220c-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前と後の会議タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="7220c-127">カウンター</span><span class="sxs-lookup"><span data-stu-id="7220c-127">Counter</span></span>|<span data-ttu-id="7220c-128">説明</span><span class="sxs-lookup"><span data-stu-id="7220c-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7220c-129">1</span><span class="sxs-lookup"><span data-stu-id="7220c-129">1</span></span>|<span data-ttu-id="7220c-130">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="7220c-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="7220c-131">2</span><span class="sxs-lookup"><span data-stu-id="7220c-131">2</span></span>|<span data-ttu-id="7220c-132">**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="7220c-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="7220c-133">3</span><span class="sxs-lookup"><span data-stu-id="7220c-133">3</span></span>|<span data-ttu-id="7220c-134">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="7220c-135">UI テンプレートを使用した設計</span><span class="sxs-lookup"><span data-stu-id="7220c-135">Designing with UI templates</span></span>

<span data-ttu-id="7220c-136">会議タブを設計するにはTeams UI テンプレートのいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="7220c-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="7220c-137">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="7220c-138">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="7220c-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="7220c-139">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="7220c-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="7220c-140">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="7220c-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="7220c-141">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="7220c-142">[左ナビゲーション](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 左側のナビゲーション コンポーネントは、タブにナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7220c-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="7220c-143">一般に、ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="7220c-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="7220c-144">[会議内] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="7220c-144">Use an in-meeting tab</span></span>

<span data-ttu-id="7220c-145">[会議内] タブは、会議中の共同作業を強化するキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="7220c-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="7220c-146">出席者は、共有ビューまたは役割ベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示および操作できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="7220c-147">使用例</span><span class="sxs-lookup"><span data-stu-id="7220c-147">Use cases</span></span>

<span data-ttu-id="7220c-148">ユーザーは、[会議内] タブを使用して次の場合があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="7220c-149">詳細なフィードバックを提供します。</span><span class="sxs-lookup"><span data-stu-id="7220c-149">Provide detailed feedback.</span></span> <span data-ttu-id="7220c-150">たとえば、ジョブ候補を評価します。</span><span class="sxs-lookup"><span data-stu-id="7220c-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="7220c-151">会議参加者のポーリング、アンケート、またはタスク アイテムを作成します。</span><span class="sxs-lookup"><span data-stu-id="7220c-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="7220c-152">会議に関連するメモを表示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="7220c-153">たとえば、販売リードに関する情報です。</span><span class="sxs-lookup"><span data-stu-id="7220c-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7220c-154">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="7220c-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、会議内タブでポーリング コンテンツを表示する方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7220c-156">モバイル</span><span class="sxs-lookup"><span data-stu-id="7220c-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="例は、モバイル上の会議内タブでポーリング コンテンツを表示する方法を示しています。" border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="7220c-158">解剖学: [会議中] タブ</span><span class="sxs-lookup"><span data-stu-id="7220c-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議内タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="7220c-160">カウンター</span><span class="sxs-lookup"><span data-stu-id="7220c-160">Counter</span></span>|<span data-ttu-id="7220c-161">説明</span><span class="sxs-lookup"><span data-stu-id="7220c-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7220c-162">1</span><span class="sxs-lookup"><span data-stu-id="7220c-162">1</span></span>|<span data-ttu-id="7220c-163">**アプリ アイコン (選択):** 16 ピクセルの透明なアプリ ロゴ。</span><span class="sxs-lookup"><span data-stu-id="7220c-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="7220c-164">2</span><span class="sxs-lookup"><span data-stu-id="7220c-164">2</span></span>|<span data-ttu-id="7220c-165">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="7220c-165">**App name**</span></span>|
|<span data-ttu-id="7220c-166">3</span><span class="sxs-lookup"><span data-stu-id="7220c-166">3</span></span>|<span data-ttu-id="7220c-167">**ヘッダー**: アプリ名が含まれます。</span><span class="sxs-lookup"><span data-stu-id="7220c-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="7220c-168">4 </span><span class="sxs-lookup"><span data-stu-id="7220c-168">4</span></span>|<span data-ttu-id="7220c-169">**[閉じる]** ボタン: タブを閉じます。フッターのアクションではなく、常に右上の閉じるアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="7220c-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="7220c-170">5 </span><span class="sxs-lookup"><span data-stu-id="7220c-170">5</span></span>|<span data-ttu-id="7220c-171">**通知バー**: エラー通知はヘッダーの直下に表示され、iframe コンテンツを 20 ピクセル下にプッシュします。</span><span class="sxs-lookup"><span data-stu-id="7220c-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="7220c-172">6 </span><span class="sxs-lookup"><span data-stu-id="7220c-172">6</span></span>|<span data-ttu-id="7220c-173">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="7220c-174">Spacing</span><span class="sxs-lookup"><span data-stu-id="7220c-174">Spacing</span></span>

<span data-ttu-id="7220c-175">280 ピクセル幅の iframe 領域内にエッジからエッジに合わせて会議内タブを最適化します。</span><span class="sxs-lookup"><span data-stu-id="7220c-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="7220c-176">iframe の左側と右側、およびタブ ヘッダーの間には 20 ピクセルのパディングがあります。</span><span class="sxs-lookup"><span data-stu-id="7220c-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="7220c-177">iframe はタブの下部に完全にブリードされます。</span><span class="sxs-lookup"><span data-stu-id="7220c-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例では、会議中のタブ間隔のディメンションを示します。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="7220c-179">スクロール</span><span class="sxs-lookup"><span data-stu-id="7220c-179">Scrolling</span></span>

<span data-ttu-id="7220c-180">スクロールを許可する場合は、次のことを覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="7220c-180">Remember the following if you allow scrolling:</span></span>

* <span data-ttu-id="7220c-181">iframe コンテンツ内のコンテンツは垂直方向にのみスクロールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-181">Content in the iframe contents should only scroll vertically.</span></span>
* <span data-ttu-id="7220c-182">ユーザーはスクロールしたコンテンツのみを表示する必要があります (上または下に何も表示されません)。</span><span class="sxs-lookup"><span data-stu-id="7220c-182">Users should only see the content they've scrolled to (nothing above or below).</span></span> 
* <span data-ttu-id="7220c-183">スクロール バーは、iframe コンテンツの一部です。</span><span class="sxs-lookup"><span data-stu-id="7220c-183">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、会議内タブのスクロール方法を示しています。" border="false":::

### <a name="navigation"></a><span data-ttu-id="7220c-185">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="7220c-185">Navigation</span></span>

<span data-ttu-id="7220c-186">ナビゲーション レイヤーやコンテンツが多いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7220c-186">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="7220c-187">ユーザーは前のレイヤーに戻る必要があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-187">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例では、会議内ナビゲーションを示します。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="7220c-189">会議内ダイアログの使用</span><span class="sxs-lookup"><span data-stu-id="7220c-189">Use an in-meeting dialog</span></span>

<span data-ttu-id="7220c-190">会議中のダイアログは、会議ステージTeams表示されます。</span><span class="sxs-lookup"><span data-stu-id="7220c-190">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="7220c-191">ユーザーの注意、確認、またはやり取りが必要ですが、微妙であり、会議を中断しません。</span><span class="sxs-lookup"><span data-stu-id="7220c-191">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="7220c-192">これらの使用は、軽くてタスク指向のシナリオに対して使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-192">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="7220c-193">使用例</span><span class="sxs-lookup"><span data-stu-id="7220c-193">Use cases</span></span>

<span data-ttu-id="7220c-194">会議中のダイアログは、参加者が次の操作を行うユーザー (会議の開催者など) によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="7220c-194">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="7220c-195">簡単なフィードバックを提供する</span><span class="sxs-lookup"><span data-stu-id="7220c-195">Provide brief feedback</span></span>
* <span data-ttu-id="7220c-196">短いアンケートまたは投票を行う</span><span class="sxs-lookup"><span data-stu-id="7220c-196">Take a short survey or poll</span></span>
* <span data-ttu-id="7220c-197">承認を送信する</span><span class="sxs-lookup"><span data-stu-id="7220c-197">Submit approvals</span></span>
* <span data-ttu-id="7220c-198">アラームを取得する</span><span class="sxs-lookup"><span data-stu-id="7220c-198">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="7220c-199">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="7220c-199">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議内ダイアログを使用する方法を示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="7220c-201">モバイル</span><span class="sxs-lookup"><span data-stu-id="7220c-201">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="例は、モバイルで会議内ダイアログを使用する方法を示しています。" border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="7220c-203">解剖学: 会議中のダイアログ</span><span class="sxs-lookup"><span data-stu-id="7220c-203">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議内ダイアログの構造構造を示しています。" border="false":::

|<span data-ttu-id="7220c-205">カウンター</span><span class="sxs-lookup"><span data-stu-id="7220c-205">Counter</span></span>|<span data-ttu-id="7220c-206">説明</span><span class="sxs-lookup"><span data-stu-id="7220c-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7220c-207">1</span><span class="sxs-lookup"><span data-stu-id="7220c-207">1</span></span>|<span data-ttu-id="7220c-208">**ヘッダー**: アプリ アイコン、名前、アクション文字列、閉じるアイコンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7220c-208">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="7220c-209">2</span><span class="sxs-lookup"><span data-stu-id="7220c-209">2</span></span>|<span data-ttu-id="7220c-210">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-210">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="7220c-211">Anatomy: 会議内ダイアログ ヘッダー</span><span class="sxs-lookup"><span data-stu-id="7220c-211">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議中のダイアログ ヘッダーの構造構造を示しています。" border="false":::

<span data-ttu-id="7220c-213">2 つのヘッダーバリアントがあります。</span><span class="sxs-lookup"><span data-stu-id="7220c-213">There are two header variants.</span></span> <span data-ttu-id="7220c-214">可能であれば、アバターと一緒にバリアントを使用して、ダイアログが人から来ているのを強化します。</span><span class="sxs-lookup"><span data-stu-id="7220c-214">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="7220c-215">カウンター</span><span class="sxs-lookup"><span data-stu-id="7220c-215">Counter</span></span>|<span data-ttu-id="7220c-216">説明</span><span class="sxs-lookup"><span data-stu-id="7220c-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7220c-217">1</span><span class="sxs-lookup"><span data-stu-id="7220c-217">1</span></span>|<span data-ttu-id="7220c-218">**アバター**: 会議内ダイアログを開始するユーザー。</span><span class="sxs-lookup"><span data-stu-id="7220c-218">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="7220c-219">2</span><span class="sxs-lookup"><span data-stu-id="7220c-219">2</span></span>|<span data-ttu-id="7220c-220">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="7220c-220">**App icon**</span></span>|
|<span data-ttu-id="7220c-221">3</span><span class="sxs-lookup"><span data-stu-id="7220c-221">3</span></span>|<span data-ttu-id="7220c-222">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="7220c-222">**App name**</span></span>|
|<span data-ttu-id="7220c-223">4 </span><span class="sxs-lookup"><span data-stu-id="7220c-223">4</span></span>|<span data-ttu-id="7220c-224">**[閉じる]** ボタン: ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="7220c-224">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="7220c-225">5 </span><span class="sxs-lookup"><span data-stu-id="7220c-225">5</span></span>|<span data-ttu-id="7220c-226">**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-226">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior-in-meeting-dialogs"></a><span data-ttu-id="7220c-227">応答性の高い動作: 会議中のダイアログ</span><span class="sxs-lookup"><span data-stu-id="7220c-227">Responsive behavior: In-meeting dialogs</span></span>

<span data-ttu-id="7220c-228">会議内のダイアログは、さまざまなシナリオを考慮してサイズが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-228">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="7220c-229">パディングとコンポーネントのサイズは必ず維持してください。</span><span class="sxs-lookup"><span data-stu-id="7220c-229">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="7220c-230">**Width**: ダイアログの iframe の幅は、サポートされているサイズ範囲内の任意の場所で指定できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-230">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="7220c-231">**Height**: ダイアログの iframe の高さは、サポートされているサイズ範囲内の任意の場所で指定できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-231">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="7220c-232">アプリのコンテンツが最大の高さを超えた場合は、ユーザーが垂直方向にスクロールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="7220c-232">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="7220c-233">実装するには、キーを使用して幅と高さを指定 [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) します。</span><span class="sxs-lookup"><span data-stu-id="7220c-233">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを表示します。幅: 最小--280 ピクセル (248 ピクセルの iframe)。Max---460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="use-the-shared-meeting-stage"></a><span data-ttu-id="7220c-235">共有会議ステージの使用</span><span class="sxs-lookup"><span data-stu-id="7220c-235">Use the shared meeting stage</span></span>

<span data-ttu-id="7220c-236">共有会議ステージは、会議参加者がアプリ コンテンツをリアルタイムで操作し、共同作業するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7220c-236">Shared meeting stage helps meeting participants interact with and collaborate on app content in real-time.</span></span> <span data-ttu-id="7220c-237">たとえば、ユーザーは、ドキュメントの編集、ホワイトボードによるブレインストーミング、ダッシュボードのレビューに集中できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-237">For example, users can focus their call on editing a document, brainstorming with a whiteboard, or reviewing a dashboard.</span></span>

<span data-ttu-id="7220c-238">会議ステージに共有されるアプリは、共有画面と同じ領域を占有します。</span><span class="sxs-lookup"><span data-stu-id="7220c-238">Apps shared to the meeting stage occupy the same space as a shared screen.</span></span> <span data-ttu-id="7220c-239">ステージは、すべての会議参加者の向きを変更します。</span><span class="sxs-lookup"><span data-stu-id="7220c-239">The stage reorients for all meeting participants.</span></span>

### <a name="use-cases"></a><span data-ttu-id="7220c-240">使用例</span><span class="sxs-lookup"><span data-stu-id="7220c-240">Use cases</span></span>

<span data-ttu-id="7220c-241">共有会議のステージは、共同作業と参加に関するすべてです。</span><span class="sxs-lookup"><span data-stu-id="7220c-241">The shared meeting stage is all about collaboration and participation.</span></span> <span data-ttu-id="7220c-242">開始に役立つシナリオの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-242">Here are some example scenarios to help you get started.</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="7220c-243">**編集とレビュー**: ダッシュボードに飛び込み、通話中の全員と計画を立て込む。</span><span class="sxs-lookup"><span data-stu-id="7220c-243">**Edit and review**: Dive into dashboards and planning with everyone on the call.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="例は、共有会議ステージでレビュー中のダッシュボードを示しています。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="7220c-245">**ホワイトボード:** 共有キャンバスで一緒に描画してアイデアを作成します。</span><span class="sxs-lookup"><span data-stu-id="7220c-245">**Whiteboard**: Draw and ideate together on a shared canvas.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="例は、共有会議ステージのホワイトボードを示しています。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="7220c-247">**クイズ**: 対話的な資料を使って知識をテストし、洞察を得る。</span><span class="sxs-lookup"><span data-stu-id="7220c-247">**Quiz**: Test knowledge and gain insights with interactive materials.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="例では、共有会議ステージでクイズを表示します。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a><span data-ttu-id="7220c-249">解剖学: 共有会議ステージ</span><span class="sxs-lookup"><span data-stu-id="7220c-249">Anatomy: Shared meeting stage</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="イメージは、共有会議ステージの設計構造を示しています。" border="false":::

|<span data-ttu-id="7220c-251">カウンター</span><span class="sxs-lookup"><span data-stu-id="7220c-251">Counter</span></span>|<span data-ttu-id="7220c-252">説明</span><span class="sxs-lookup"><span data-stu-id="7220c-252">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="7220c-253">1</span><span class="sxs-lookup"><span data-stu-id="7220c-253">1</span></span>|<span data-ttu-id="7220c-254">**アプリ アイコン**: 強調表示されたアイコンは、アプリの会議中タブが開いている状態を示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-254">**App icon**: The highlighted icon indicates the app's in-meeting tab is open.</span></span>|
|<span data-ttu-id="7220c-255">2</span><span class="sxs-lookup"><span data-stu-id="7220c-255">2</span></span>|<span data-ttu-id="7220c-256">**[会議ステージに共有] ボタン**: アプリを会議ステージに共有するエントリ ポイント。</span><span class="sxs-lookup"><span data-stu-id="7220c-256">**Share to meeting stage button**: The entry point to share the app to the meeting stage.</span></span> <span data-ttu-id="7220c-257">共有会議ステージを使用するアプリを構成した場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="7220c-257">Displays if you configure your app to use the shared meeting stage.</span></span>|
|<span data-ttu-id="7220c-258">3</span><span class="sxs-lookup"><span data-stu-id="7220c-258">3</span></span>|<span data-ttu-id="7220c-259">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-259">**iframe**: Displays your app content.</span></span>|
|<span data-ttu-id="7220c-260">4 </span><span class="sxs-lookup"><span data-stu-id="7220c-260">4</span></span>|<span data-ttu-id="7220c-261">**[共有を停止する**] ボタン: 会議ステージへのアプリの共有を停止します。</span><span class="sxs-lookup"><span data-stu-id="7220c-261">**Stop sharing button**: Stops sharing the app to the meeting stage.</span></span> <span data-ttu-id="7220c-262">共有を開始した参加者にのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="7220c-262">Displays only for the participant who started the share.</span></span>|
|<span data-ttu-id="7220c-263">5 </span><span class="sxs-lookup"><span data-stu-id="7220c-263">5</span></span>|<span data-ttu-id="7220c-264">**発表者の属性**: アプリを共有した参加者の名前を表示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-264">**Presenter attribution**: Displays the name of the participant who shared the app.</span></span>|

### <a name="responsive-behavior-shared-meeting-stage"></a><span data-ttu-id="7220c-265">応答性の高い動作: 共有会議ステージ</span><span class="sxs-lookup"><span data-stu-id="7220c-265">Responsive behavior: Shared meeting stage</span></span>

<span data-ttu-id="7220c-266">会議ステージに共有されるアプリのサイズは、会議の状態と、ユーザーがウィンドウのサイズを変更する方法によって異なります。</span><span class="sxs-lookup"><span data-stu-id="7220c-266">Apps shared to the meeting stage vary in size based on the state of the meeting and how the user resizes the window.</span></span> <span data-ttu-id="7220c-267">ブラウザーと同様に、ナビゲーションとコントロールのパディングと応答性の高いレイアウトを維持します。</span><span class="sxs-lookup"><span data-stu-id="7220c-267">Maintain padding and the responsive layout of navigation and controls just as you would in a browser.</span></span>

* <span data-ttu-id="7220c-268">**サイド パネル**: ユーザーは、会議中にいつでもサイド パネルを開き、チャットしたり、名簿を表示したり、アプリ (つまり、会議内タブ) を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="7220c-268">**Side panel**: A user can have the side panel open at any time during a meeting to chat, view the roster, or use an app (i.e., in-meeting tab).</span></span> <span data-ttu-id="7220c-269">パネルが開いているときにステージが動的に再配置されます。</span><span class="sxs-lookup"><span data-stu-id="7220c-269">The stage dynamically rearranges when the panel is open.</span></span>
* <span data-ttu-id="7220c-270">**ビデオとオーディオ のグリッド**: ビデオとオーディオ のグリッドは常に表示され、会議の参加者を表示できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-270">**Video and audio grid**: The video and audio grid is always visible to show meeting participants.</span></span> <span data-ttu-id="7220c-271">ユーザーが会議で他のユーザーにスポットライトを当てたりピンを固定したりすると、参加者グリッドの高さまたは幅は、向きに応じて増加します。</span><span class="sxs-lookup"><span data-stu-id="7220c-271">When a user spotlights or pins someone in the meeting, this increases the height or width of the participant grid depending on the orientation.</span></span>

#### <a name="meeting-stage-without-side-panel"></a><span data-ttu-id="7220c-272">会議ステージ (サイド パネルなし)</span><span class="sxs-lookup"><span data-stu-id="7220c-272">Meeting stage (without side panel)</span></span>

<span data-ttu-id="7220c-273">サイド パネルが開いていない場合、会議ステージは既定で 994x678 ピクセルで、最小 792x382 ピクセルを指定できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-273">When the side panel isn't open, the meeting stage is 994x678 pixels by default and can be a minimum 792x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="サイド パネルを閉じた共有会議ステージの応答性を示す画像。" border="false":::

#### <a name="meeting-stage-with-side-panel"></a><span data-ttu-id="7220c-275">会議ステージ (サイド パネル付き)</span><span class="sxs-lookup"><span data-stu-id="7220c-275">Meeting stage (with side panel)</span></span>

<span data-ttu-id="7220c-276">サイド パネルが開いている場合、会議ステージは既定で 918x540 ピクセルで、最小 472x382 ピクセルを指定できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-276">When the side panel is open, the meeting stage is 918x540 pixels by default and can be a minimum 472x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="サイド パネルを開いた状態で共有された会議ステージの応答性を示す画像。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="7220c-278">会議後</span><span class="sxs-lookup"><span data-stu-id="7220c-278">After a meeting</span></span>

<span data-ttu-id="7220c-279">会議の終了後に会議に戻り、アプリのコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-279">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="7220c-280">この例では、会議開催者は **[Contoso]** タブで投票結果を確認できます (注: デザインの観点から、会議前と会議後のタブ エクスペリエンスの違いはありません)。</span><span class="sxs-lookup"><span data-stu-id="7220c-280">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例の図は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="7220c-282">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="7220c-282">Best practices</span></span>

<span data-ttu-id="7220c-283">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="7220c-283">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="7220c-284">対話</span><span class="sxs-lookup"><span data-stu-id="7220c-284">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="操作の数を制限する方法を示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="7220c-286">Do: 操作の数を制限する</span><span class="sxs-lookup"><span data-stu-id="7220c-286">Do: Limit the number of interactions</span></span>

<span data-ttu-id="7220c-287">会議中のダイアログでは、ユーザーが何かを迅速に実行するのに役立つ不要なコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="7220c-287">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="不要な要素を導入しない方法を示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="7220c-289">[しない]: 不要な要素を導入する</span><span class="sxs-lookup"><span data-stu-id="7220c-289">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="7220c-290">複数の操作を含む単一の会議内ダイアログは、通話の邪魔になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-290">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="フォーカス環境を作成する方法を示す例。" border="false":::

#### <a name="do-create-a-focused-environment"></a><span data-ttu-id="7220c-292">Do: フォーカス環境を作成する</span><span class="sxs-lookup"><span data-stu-id="7220c-292">Do: Create a focused environment</span></span>

<span data-ttu-id="7220c-293">アプリのエクスペリエンスを会議のステージに対してスコープを設定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7220c-293">We recommend keeping your app’s experience scoped to just the meeting stage.</span></span> <span data-ttu-id="7220c-294">サイド パネルの会議内タブを、特定のシナリオのセカンダリプライベート ビューとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-294">You can use an in-meeting tab in the side panel as a secondary, private view for certain scenarios.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="会議中に競合するサーフェスを含めない方法を示す例。" border="false":::

#### <a name="dont-include-competing-surfaces"></a><span data-ttu-id="7220c-296">[しない]: 競合するサーフェスを含める</span><span class="sxs-lookup"><span data-stu-id="7220c-296">Don't: Include competing surfaces</span></span>

<span data-ttu-id="7220c-297">アプリは、ステージでの共同作業や会議中のダイアログへの応答など、ユーザーに一度に 1 つのサーフェスにのみ集中を求める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-297">Your app should only ask users to focus on a single surface a time, whether it's collaborating on the stage or responding to an in-meeting dialog.</span></span> <span data-ttu-id="7220c-298">(注: アプリがステージ上にある間は、他のアプリによってダイアログがトリガーされた状態を維持できない)。</span><span class="sxs-lookup"><span data-stu-id="7220c-298">(Note: You can’t keep dialogs being triggered by other apps while your app is on the stage.)</span></span> 

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="7220c-299">レイアウト</span><span class="sxs-lookup"><span data-stu-id="7220c-299">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="1 列のダイアログ レイアウトを使用する方法を示す例。" border="false":::

#### <a name="do-use-a-one-column-dialog"></a><span data-ttu-id="7220c-301">Do: 1 列のダイアログを使用する</span><span class="sxs-lookup"><span data-stu-id="7220c-301">Do: Use a one-column dialog</span></span>

<span data-ttu-id="7220c-302">ダイアログは会議ステージの中心にあるので、タスクの完了はユーザーの不満を避けるために迅速かつ簡単に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-302">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議内線のスペースを煩雑にしてはいけないことを示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="7220c-304">T't: スペースを乱雑にする</span><span class="sxs-lookup"><span data-stu-id="7220c-304">Don't: Clutter the space</span></span>

<span data-ttu-id="7220c-305">密なコンテンツや過剰に構造化されたコンテンツは、特に会議中に気が散り、圧倒的になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-305">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="1 列のタブ レイアウトを表示する例。" border="false":::

#### <a name="do-use-a-one-column-tab"></a><span data-ttu-id="7220c-307">Do: 1 列のタブを使用する</span><span class="sxs-lookup"><span data-stu-id="7220c-307">Do: Use a one-column tab</span></span>

<span data-ttu-id="7220c-308">会議内タブの狭い性質を考えると、コンテンツを 1 つの列に表示することを強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="7220c-308">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="複数の列を持つタブを表示する例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="7220c-310">[しない]: 複数の列を使用する</span><span class="sxs-lookup"><span data-stu-id="7220c-310">Don't: Use multiple columns</span></span>

<span data-ttu-id="7220c-311">会議内タブのスペースが限られているので、複数の列を含むレイアウトは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="7220c-311">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="7220c-312">コントロール</span><span class="sxs-lookup"><span data-stu-id="7220c-312">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="プライマリ コントロールを右揃えする方法を示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="7220c-314">Do: プライマリ アクションを右揃えする</span><span class="sxs-lookup"><span data-stu-id="7220c-314">Do: Right align the primary action</span></span>

<span data-ttu-id="7220c-315">最も視覚的に重いアクションを最も右の位置に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7220c-315">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="プライマリ コントロールを左揃えにしない方法を示す例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="7220c-317">[しない]: 左揃えまたは中央揃えアクション</span><span class="sxs-lookup"><span data-stu-id="7220c-317">Don't: Left or center align actions</span></span>

<span data-ttu-id="7220c-318">これは、ダイアログ内のコントロールTeamsの標準のパターンから離れ、上部のダイアログボックスと競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-318">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="7220c-319">スクロール</span><span class="sxs-lookup"><span data-stu-id="7220c-319">Scrolling</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議内タブで垂直スクロールを表示する例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="共有会議ステージで垂直スクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="7220c-322">Do: 垂直方向にスクロールする</span><span class="sxs-lookup"><span data-stu-id="7220c-322">Do: Scroll vertically</span></span>

<span data-ttu-id="7220c-323">ユーザーは、 (および他の場所) Teams垂直スクロールを期待します。</span><span class="sxs-lookup"><span data-stu-id="7220c-323">Users expect vertical scrolling in Teams (and elsewhere).</span></span> <span data-ttu-id="7220c-324">これは、ユーザーが x 軸と y 軸をパンできるホワイトボードなどのクリエイティブ なキャンバスがある場合は適用されません。</span><span class="sxs-lookup"><span data-stu-id="7220c-324">This may not apply if you have a creative canvas, such as a whiteboard, which users can pan across the x and y axis.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議内タブに水平スクロールを表示する例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="共有会議ステージで水平スクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="7220c-327">[しない]: 水平方向にスクロールする</span><span class="sxs-lookup"><span data-stu-id="7220c-327">Don't: Scroll horizontally</span></span>

<span data-ttu-id="7220c-328">水平方向のスクロールは、(会議環境を含む) Teams予期される動作ではありません。</span><span class="sxs-lookup"><span data-stu-id="7220c-328">Horizontal scrolling isn’t an expected behavior in Teams (including the meeting environment).</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="7220c-329">ワークフロー</span><span class="sxs-lookup"><span data-stu-id="7220c-329">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議内タブに複雑なシナリオを表示する例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="7220c-331">Do: [会議内] タブの複雑なシナリオを表示する</span><span class="sxs-lookup"><span data-stu-id="7220c-331">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="7220c-332">アプリに複数のタスクが含まれる場合は、1 列のレイアウトで会議内タブを使用することを強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="7220c-332">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議内ダイアログで複雑なシナリオを表示する例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="7220c-334">[しない]: 会議内のダイアログを複雑にする</span><span class="sxs-lookup"><span data-stu-id="7220c-334">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="7220c-335">会議中のダイアログは、簡単な操作を目的とします。</span><span class="sxs-lookup"><span data-stu-id="7220c-335">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="7220c-336">テーマ</span><span class="sxs-lookup"><span data-stu-id="7220c-336">Theming</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="暗いテーマで会議の拡張機能を表示する例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="暗いテーマで会議の拡張機能を表示する別の例。" border="false":::

#### <a name="do-focus-on-dark-theme"></a><span data-ttu-id="7220c-339">Do: 暗いテーマに焦点を当てる</span><span class="sxs-lookup"><span data-stu-id="7220c-339">Do: Focus on dark theme</span></span>

<span data-ttu-id="7220c-340">Teams会議は暗いテーマに最適化され、視覚的および認知的なノイズを減らし、ユーザーがディスカッションと共有コンテンツに集中できます。</span><span class="sxs-lookup"><span data-stu-id="7220c-340">Teams meetings are optimized for dark theme to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="7220c-341">特定の種類のアプリ (ホワイトボードやドキュメント編集など) では、暗いキャンバスは必要ない場合があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-341">Keep in mind certain types of apps (such as whiteboarding and document editing) don't need a dark canvas.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="会議のテーマと一致しない色で会議の拡張機能を表示する例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="会議のテーマと一致しない色の会議拡張機能を示す別の例。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="7220c-344">[しない]: 見慣れない色を使用する</span><span class="sxs-lookup"><span data-stu-id="7220c-344">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="7220c-345">会議環境と衝突する色が気を散らし、ユーザーのネイティブな表示が少Teams。</span><span class="sxs-lookup"><span data-stu-id="7220c-345">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span> <span data-ttu-id="7220c-346">通話テーマのニュートラルTeams[含む、](https://developer.microsoft.com/fluentui#/styles/web/colors/products)カラー ランプの詳細について学習します。</span><span class="sxs-lookup"><span data-stu-id="7220c-346">Learn about the Teams [color ramp](https://developer.microsoft.com/fluentui#/styles/web/colors/products), including call theme neutrals.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="7220c-347">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="7220c-347">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="戻るボタンを使用して会議の拡張機能を表示する例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="7220c-349">Do: [戻る] ボタンを持つ</span><span class="sxs-lookup"><span data-stu-id="7220c-349">Do: Have a back button</span></span>

<span data-ttu-id="7220c-350">会議内タブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻る必要があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-350">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="2 つの閉じボタンを使用して会議の内線表示オプションを表示する例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="7220c-352">[しない] : 別の [閉じ] ボタンを含める</span><span class="sxs-lookup"><span data-stu-id="7220c-352">Don't: Include another dismiss button</span></span>

<span data-ttu-id="7220c-353">会議中のタブ コンテンツを閉じるオプションを指定すると、ヘッダーに既に会議中のタブ自体を閉じるボタンが存在するために問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-353">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議内タブ内にモーダル (またはタスク モジュール) を表示する例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="7220c-355">注意: [会議内] タブ内のモーダルを回避する</span><span class="sxs-lookup"><span data-stu-id="7220c-355">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="7220c-356">既に狭い会議内タブのモーダル (タスク モジュールとも呼ばれる) は、コンテンツをラップしてあいまいにしている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-356">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a><span data-ttu-id="7220c-357">応答性の高い動作</span><span class="sxs-lookup"><span data-stu-id="7220c-357">Responsive behavior</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="会議拡張機能のサイズを適切に変更する方法を示す例。" border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a><span data-ttu-id="7220c-359">Do: アプリのサイズ変更とスケーリングを迅速に行う</span><span class="sxs-lookup"><span data-stu-id="7220c-359">Do: Resize and scale your app responsively</span></span>

<span data-ttu-id="7220c-360">アプリのコンテンツは、小さいウィンドウで動的にサイズを変更して凝縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-360">App content should dynamically resize and condense in smaller windows.</span></span> <span data-ttu-id="7220c-361">アプリのメイン ナビゲーションとフローティング コントロールを表示します。</span><span class="sxs-lookup"><span data-stu-id="7220c-361">Keep your app’s main navigation and any floating controls visible.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="会議拡張機能のサイズを適切に変更しない方法を示す例。" border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a><span data-ttu-id="7220c-363">[しない]: プライマリ UI コンポーネントをトリミングまたはクリップする</span><span class="sxs-lookup"><span data-stu-id="7220c-363">Don't: Crop or clip primary UI components</span></span>

<span data-ttu-id="7220c-364">画面外のナビゲーションとコントロールをフローティングし、スクロールして検索する必要がある場合、ユーザーにとって混乱を招く可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7220c-364">Floating navigation and controls off screen and requiring a scroll to find can be confusing for users.</span></span> <span data-ttu-id="7220c-365">アプリコンテンツが iframe に収まらない場合は、アプリのコンテンツを水平方向にスクロールしてはならない。</span><span class="sxs-lookup"><span data-stu-id="7220c-365">Your app content shouldn’t scroll horizontally when it can't fit in the iframe.</span></span>

   :::column-end:::
:::row-end:::

## <a name="next-step"></a><span data-ttu-id="7220c-366">次の手順</span><span class="sxs-lookup"><span data-stu-id="7220c-366">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7220c-367">会議用にアプリを構成する</span><span class="sxs-lookup"><span data-stu-id="7220c-367">Configure your app for meetings</span></span>](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
