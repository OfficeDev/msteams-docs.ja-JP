---
title: 会議の拡張機能の設計
author: heath-hamilton
description: Teams会議でアプリをデザインする方法と、Microsoft Teams UI キットを入手する方法について説明します。
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 0a888c333305e9caafcd0bac0e5549bf08ead424
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566027"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="60ed5-103">会議の拡張機能Microsoft Teams設計する</span><span class="sxs-lookup"><span data-stu-id="60ed5-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="60ed5-104">会議の生産性を高めるアプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="60ed5-105">たとえば、通話中にアンケートを完了してもらうか、会議のフローを中断しない簡単なアラームを送信するように依頼します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="60ed5-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="60ed5-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="60ed5-107">必要に応じて取得および変更できる要素を含む、より包括的なデザイン ガイドラインについては、Microsoft Teams UI キットを参照してください。</span><span class="sxs-lookup"><span data-stu-id="60ed5-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60ed5-108">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="60ed5-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="60ed5-109">会議の内線番号を追加する</span><span class="sxs-lookup"><span data-stu-id="60ed5-109">Add a meeting extension</span></span>

<span data-ttu-id="60ed5-110">会議の前と中に会議の内線番号を追加できます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="60ed5-111">また、特定の会議のアプリをTeams ストア (AppSource) から直接追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="60ed5-112">会議の前に追加する</span><span class="sxs-lookup"><span data-stu-id="60ed5-112">Add before a meeting</span></span>

<span data-ttu-id="60ed5-113">会議の詳細で、[ **タブを追加する +** ] を選択してアプリのポップアップを開き、会議に最適化されたアプリを検索します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線番号を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="60ed5-115">会議中に追加する</span><span class="sxs-lookup"><span data-stu-id="60ed5-115">Add during a meeting</span></span>

会議で、[**アプリを追加** する] を選択 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  し、目的のアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線番号を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="60ed5-118">会議の前に</span><span class="sxs-lookup"><span data-stu-id="60ed5-118">Before a meeting</span></span>

<span data-ttu-id="60ed5-119">会議の前に、タブにコンテンツを追加できます。次の例は、通話中に回答する調査質問の下書きを示しています。</span><span class="sxs-lookup"><span data-stu-id="60ed5-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細のコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="60ed5-121">解剖学: [会議] タブ (会議の前後)</span><span class="sxs-lookup"><span data-stu-id="60ed5-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前後の会議タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="60ed5-123">カウンター</span><span class="sxs-lookup"><span data-stu-id="60ed5-123">Counter</span></span>|<span data-ttu-id="60ed5-124">説明</span><span class="sxs-lookup"><span data-stu-id="60ed5-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="60ed5-125">1</span><span class="sxs-lookup"><span data-stu-id="60ed5-125">1</span></span>|<span data-ttu-id="60ed5-126">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="60ed5-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="60ed5-127">2</span><span class="sxs-lookup"><span data-stu-id="60ed5-127">2</span></span>|<span data-ttu-id="60ed5-128">**タブオーバーフロー**: 名前の変更や削除などのタブアクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="60ed5-129">3</span><span class="sxs-lookup"><span data-stu-id="60ed5-129">3</span></span>|<span data-ttu-id="60ed5-130">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="60ed5-131">UI テンプレートを使用したデザイン</span><span class="sxs-lookup"><span data-stu-id="60ed5-131">Designing with UI templates</span></span>

<span data-ttu-id="60ed5-132">次の Teams UI テンプレートのいずれかを使用して、会議タブの設計に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="60ed5-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々の項目に対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="60ed5-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="60ed5-134">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスク ボードは、かんばんボードまたはスイム レーンとも呼ばれ、作業項目やチケットの状態を追跡するためによく使用されるカードの集まりです。</span><span class="sxs-lookup"><span data-stu-id="60ed5-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="60ed5-135">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="60ed5-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="60ed5-136">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および送信するためのものです。</span><span class="sxs-lookup"><span data-stu-id="60ed5-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="60ed5-137">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="60ed5-138">[左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左のナビゲーション テンプレートは、タブが何らかのナビゲーションを必要とする場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="60ed5-139">通常、タブ ナビゲーションは最小限に抑える必要があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="60ed5-140">[会議中] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="60ed5-140">Use an in-meeting tab</span></span>

<span data-ttu-id="60ed5-141">[ミーティング中] タブは、会議中のコラボレーションを強化するためのキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="60ed5-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="60ed5-142">参加者は、共有ビューまたはロールベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示したり、操作したりできます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="60ed5-143">使用例</span><span class="sxs-lookup"><span data-stu-id="60ed5-143">Use cases</span></span>

<span data-ttu-id="60ed5-144">[会議中] タブを使用して、次の場合があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="60ed5-145">詳細なフィードバックを提供します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-145">Provide detailed feedback.</span></span> <span data-ttu-id="60ed5-146">たとえば、求職者を評価します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-146">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="60ed5-147">ミーティング参加者の投票、アンケート、またはタスク アイテムを作成します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-147">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="60ed5-148">会議に関連するメモを表示します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-148">Display notes relevant to the meeting.</span></span> <span data-ttu-id="60ed5-149">たとえば、販売リードに関する情報などです。</span><span class="sxs-lookup"><span data-stu-id="60ed5-149">For example, information about a sales lead.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、ミーティング中のタブで投票コンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="60ed5-151">解剖学: [会議中] タブ</span><span class="sxs-lookup"><span data-stu-id="60ed5-151">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議中のタブの構造構造を示しています。" border="false":::

|<span data-ttu-id="60ed5-153">カウンター</span><span class="sxs-lookup"><span data-stu-id="60ed5-153">Counter</span></span>|<span data-ttu-id="60ed5-154">説明</span><span class="sxs-lookup"><span data-stu-id="60ed5-154">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="60ed5-155">1</span><span class="sxs-lookup"><span data-stu-id="60ed5-155">1</span></span>|<span data-ttu-id="60ed5-156">**アプリアイコン(選択済み)**: 16ピクセル透明アプリのロゴ。</span><span class="sxs-lookup"><span data-stu-id="60ed5-156">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="60ed5-157">2</span><span class="sxs-lookup"><span data-stu-id="60ed5-157">2</span></span>|<span data-ttu-id="60ed5-158">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="60ed5-158">**App name**</span></span>|
|<span data-ttu-id="60ed5-159">3</span><span class="sxs-lookup"><span data-stu-id="60ed5-159">3</span></span>|<span data-ttu-id="60ed5-160">**ヘッダー**: アプリ名を含めます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-160">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="60ed5-161">4</span><span class="sxs-lookup"><span data-stu-id="60ed5-161">4</span></span>|<span data-ttu-id="60ed5-162">**閉じるボタン**: タブを閉じます。フッターのアクションではなく、常に右上の閉じるアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-162">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="60ed5-163">5</span><span class="sxs-lookup"><span data-stu-id="60ed5-163">5</span></span>|<span data-ttu-id="60ed5-164">**通知バー**: エラーアラートはヘッダーの真下に表示され、iframeのコンテンツを20ピクセル下に押し下げます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-164">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="60ed5-165">6</span><span class="sxs-lookup"><span data-stu-id="60ed5-165">6</span></span>|<span data-ttu-id="60ed5-166">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-166">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="60ed5-167">Spacing</span><span class="sxs-lookup"><span data-stu-id="60ed5-167">Spacing</span></span>

<span data-ttu-id="60ed5-168">280 ピクセル幅の iframe 領域内にエッジツーエッジに収まるように、会議中のタブを最適化します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-168">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="60ed5-169">iframe の左右とタブ ヘッダーの間には、20 ピクセルのパディングがあります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-169">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="60ed5-170">iframe は、タブの下部にフルブリードされます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-170">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例は、会議内のタブ間隔の寸法を示しています。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="60ed5-172">スクロール</span><span class="sxs-lookup"><span data-stu-id="60ed5-172">Scrolling</span></span>

<span data-ttu-id="60ed5-173">Iframe の内容は垂直方向にスクロールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-173">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="60ed5-174">スクロールしたコンテンツのみが表示されます (上または下には何もありません)。</span><span class="sxs-lookup"><span data-stu-id="60ed5-174">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="60ed5-175">スクロールバーは iframe コンテンツの一部です。</span><span class="sxs-lookup"><span data-stu-id="60ed5-175">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、会議内のタブがスクロールする方法を示しています。" border="false":::

### <a name="navigation"></a><span data-ttu-id="60ed5-177">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="60ed5-177">Navigation</span></span>

<span data-ttu-id="60ed5-178">ナビゲーション レイヤーまたはコンテンツの負荷が高いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="60ed5-178">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="60ed5-179">ユーザーは前のレイヤーに戻ることができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-179">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例は、会議内のナビゲーションを示しています。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="60ed5-181">会議内ダイアログを使用する</span><span class="sxs-lookup"><span data-stu-id="60ed5-181">Use an in-meeting dialog</span></span>

<span data-ttu-id="60ed5-182">ミーティング内のダイアログは、ミーティングのTeamsステージに表示されます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-182">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="60ed5-183">ユーザーの注意、確認、または操作が必要ですが、微妙であり、会議を中断しません。</span><span class="sxs-lookup"><span data-stu-id="60ed5-183">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="60ed5-184">軽くてタスク指向のシナリオでは、これらを慎重に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-184">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="60ed5-185">使用例</span><span class="sxs-lookup"><span data-stu-id="60ed5-185">Use cases</span></span>

<span data-ttu-id="60ed5-186">会議中のダイアログは、参加者に次の操作を行うユーザー (会議の開催者など) によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-186">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="60ed5-187">簡単なフィードバックを提供する</span><span class="sxs-lookup"><span data-stu-id="60ed5-187">Provide brief feedback</span></span>
* <span data-ttu-id="60ed5-188">短いアンケートまたはアンケートを実施する</span><span class="sxs-lookup"><span data-stu-id="60ed5-188">Take a short survey or poll</span></span>
* <span data-ttu-id="60ed5-189">承認の送信</span><span class="sxs-lookup"><span data-stu-id="60ed5-189">Submit approvals</span></span>
* <span data-ttu-id="60ed5-190">アラームを取得する</span><span class="sxs-lookup"><span data-stu-id="60ed5-190">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議内のダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="60ed5-192">解剖学: 会議中ダイアログ</span><span class="sxs-lookup"><span data-stu-id="60ed5-192">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議内のダイアログの構造構造を示しています。" border="false":::

|<span data-ttu-id="60ed5-194">カウンター</span><span class="sxs-lookup"><span data-stu-id="60ed5-194">Counter</span></span>|<span data-ttu-id="60ed5-195">説明</span><span class="sxs-lookup"><span data-stu-id="60ed5-195">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="60ed5-196">1</span><span class="sxs-lookup"><span data-stu-id="60ed5-196">1</span></span>|<span data-ttu-id="60ed5-197">**ヘッダー**: アプリアイコン、名前、アクション文字列、および閉じるアイコンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-197">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="60ed5-198">2</span><span class="sxs-lookup"><span data-stu-id="60ed5-198">2</span></span>|<span data-ttu-id="60ed5-199">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-199">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="60ed5-200">解剖学: 会議内ダイアログヘッダー</span><span class="sxs-lookup"><span data-stu-id="60ed5-200">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議内のダイアログ ヘッダーの構造構造を示しています。" border="false":::

<span data-ttu-id="60ed5-202">2 つのヘッダバリアントがあります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-202">There are two header variants.</span></span> <span data-ttu-id="60ed5-203">可能であれば、アバターと共にバリアントを使用して、ダイアログが人から来ることを補強します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-203">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="60ed5-204">カウンター</span><span class="sxs-lookup"><span data-stu-id="60ed5-204">Counter</span></span>|<span data-ttu-id="60ed5-205">説明</span><span class="sxs-lookup"><span data-stu-id="60ed5-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="60ed5-206">1</span><span class="sxs-lookup"><span data-stu-id="60ed5-206">1</span></span>|<span data-ttu-id="60ed5-207">**アバター**: 会議中のダイアログを開始した人。</span><span class="sxs-lookup"><span data-stu-id="60ed5-207">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="60ed5-208">2</span><span class="sxs-lookup"><span data-stu-id="60ed5-208">2</span></span>|<span data-ttu-id="60ed5-209">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="60ed5-209">**App icon**</span></span>|
|<span data-ttu-id="60ed5-210">3</span><span class="sxs-lookup"><span data-stu-id="60ed5-210">3</span></span>|<span data-ttu-id="60ed5-211">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="60ed5-211">**App name**</span></span>|
|<span data-ttu-id="60ed5-212">4</span><span class="sxs-lookup"><span data-stu-id="60ed5-212">4</span></span>|<span data-ttu-id="60ed5-213">**閉じるボタン**: ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-213">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="60ed5-214">5</span><span class="sxs-lookup"><span data-stu-id="60ed5-214">5</span></span>|<span data-ttu-id="60ed5-215">**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-215">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="60ed5-216">応答性の高い動作</span><span class="sxs-lookup"><span data-stu-id="60ed5-216">Responsive behavior</span></span>

<span data-ttu-id="60ed5-217">会議中のダイアログ ボックスは、さまざまなシナリオを考慮してサイズが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-217">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="60ed5-218">パディングとコンポーネントサイズを維持してください。</span><span class="sxs-lookup"><span data-stu-id="60ed5-218">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="60ed5-219">**幅**: サポートされているサイズ範囲内の任意の場所で、ダイアログの iframe の幅を指定できます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-219">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="60ed5-220">**高さ**: サポートされているサイズ範囲内の任意の場所で、ダイアログの iframe の高さを指定できます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-220">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="60ed5-221">アプリのコンテンツが最大の高さを超えた場合、ユーザーが垂直方向にスクロールできるようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-221">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="60ed5-222">実装するには、キーを使用して幅と高さを指定 [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-222">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを示しています。幅: 最小-280ピクセル(248ピクセルのiframe)。最大 --460 ピクセル(428 ピクセルの iframe)高さ:300ピクセル(iframe)。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="60ed5-224">会議の後</span><span class="sxs-lookup"><span data-stu-id="60ed5-224">After a meeting</span></span>

<span data-ttu-id="60ed5-225">終了後に会議に戻ってアプリのコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="60ed5-225">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="60ed5-226">この例では、会議の開催者は **[Contoso]** タブで投票結果を確認できます (注: 設計の観点から見ると、会議前と会議後のタブ エクスペリエンスの間に違いはありません)。</span><span class="sxs-lookup"><span data-stu-id="60ed5-226">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例の図は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="60ed5-228">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="60ed5-228">Best practices</span></span>

<span data-ttu-id="60ed5-229">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-229">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="60ed5-230">相互 作用</span><span class="sxs-lookup"><span data-stu-id="60ed5-230">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="インタラクションの数を制限する方法を示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="60ed5-232">実行: インタラクションの数を制限する</span><span class="sxs-lookup"><span data-stu-id="60ed5-232">Do: Limit the number of interactions</span></span>

<span data-ttu-id="60ed5-233">会議中のダイアログでは、ユーザーがすぐに何かを達成するのに役立たない不要なコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-233">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="不要な要素を導入しない方法を示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="60ed5-235">しない: 不要な要素を導入する</span><span class="sxs-lookup"><span data-stu-id="60ed5-235">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="60ed5-236">複数の対話を行う単一の会議内のダイアログは、通話から気をそらす可能性があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-236">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="60ed5-237">レイアウト</span><span class="sxs-lookup"><span data-stu-id="60ed5-237">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="単一列のダイアログ レイアウトの使用方法を示す例を示します。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="60ed5-239">行う: 単一列のダイアログ レイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="60ed5-239">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="60ed5-240">ダイアログは会議の中心にあるため、ユーザーの不満を避けるために、タスクの完了は迅速かつ簡単に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-240">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議内線のスペースを乱雑にする必要はありません示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="60ed5-242">しない:スペースを乱雑にする</span><span class="sxs-lookup"><span data-stu-id="60ed5-242">Don't: Clutter the space</span></span>

<span data-ttu-id="60ed5-243">密または過度に構造化されたコンテンツは、特に会議中に、気が散り、圧倒的になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-243">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="単一列のタブ レイアウトを示す例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="60ed5-245">実行: 単一列のタブ レイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="60ed5-245">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="60ed5-246">会議内のタブの狭い性質を考えると、1 つの列に内容を表示することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="60ed5-246">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="複数の列を含むタブを表示する例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="60ed5-248">しない: 複数の列を使用する</span><span class="sxs-lookup"><span data-stu-id="60ed5-248">Don't: Use multiple columns</span></span>

<span data-ttu-id="60ed5-249">会議内タブのスペースが限られているため、複数の列を含むレイアウトは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="60ed5-249">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="60ed5-250">コントロール</span><span class="sxs-lookup"><span data-stu-id="60ed5-250">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="主コントロールを右揃えにする方法を示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="60ed5-252">実行: プライマリアクションを右揃えにします</span><span class="sxs-lookup"><span data-stu-id="60ed5-252">Do: Right align the primary action</span></span>

<span data-ttu-id="60ed5-253">最も視覚的に重いアクションを右端に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="60ed5-253">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="主コントロールを左揃えにしない方法を示す例を示します。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="60ed5-255">しない: 左または中央揃えアクション</span><span class="sxs-lookup"><span data-stu-id="60ed5-255">Don't: Left or center align actions</span></span>

<span data-ttu-id="60ed5-256">これは、ダイアログ内のコントロール配置の標準Teamsパターンから外れ、上位のダイアログボックスと競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-256">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="60ed5-257">Scroll</span><span class="sxs-lookup"><span data-stu-id="60ed5-257">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議内のタブで垂直スクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="60ed5-259">行う: 垂直方向にスクロール</span><span class="sxs-lookup"><span data-stu-id="60ed5-259">Do: Scroll vertically</span></span>

<span data-ttu-id="60ed5-260">ユーザーは、Teams(および他の場所)で垂直スクロールを期待しています。</span><span class="sxs-lookup"><span data-stu-id="60ed5-260">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議内のタブで水平スクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="60ed5-262">しない: 水平方向にスクロールする</span><span class="sxs-lookup"><span data-stu-id="60ed5-262">Don't: Scroll horizontally</span></span>

<span data-ttu-id="60ed5-263">水平スクロールは、Teamsで予期される動作ではありません。</span><span class="sxs-lookup"><span data-stu-id="60ed5-263">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="60ed5-264">会議環境の他のキャンバスは、垂直方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="60ed5-264">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="60ed5-265">ワークフロー</span><span class="sxs-lookup"><span data-stu-id="60ed5-265">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議中のタブでの複雑なシナリオの例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="60ed5-267">行う: [ミーティング中] タブの複雑なシナリオを表示します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-267">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="60ed5-268">アプリに複数のタスクが含まれている場合は、単一列レイアウトの [ミーティング中] タブを使用することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="60ed5-268">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議内のダイアログで複雑なシナリオを示す例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="60ed5-270">しない: 会議中のダイアログを複雑にする</span><span class="sxs-lookup"><span data-stu-id="60ed5-270">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="60ed5-271">会議中のダイアログは、簡単な対話を目的としています。</span><span class="sxs-lookup"><span data-stu-id="60ed5-271">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="60ed5-272">テーマ</span><span class="sxs-lookup"><span data-stu-id="60ed5-272">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="暗いテーマを持つ会議の内線番号を示す例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="60ed5-274">行う: Teams色のトークンを使用する</span><span class="sxs-lookup"><span data-stu-id="60ed5-274">Do: Use Teams color tokens</span></span>

<span data-ttu-id="60ed5-275">Teams会議は、ユーザーがディスカッションや共有コンテンツに集中できるように、視覚や認知ノイズを低減するために、ダーク モード用に最適化されています。</span><span class="sxs-lookup"><span data-stu-id="60ed5-275">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="60ed5-276"><a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">カラー トークン (Fluent UI) の</a>使用について学習します。</span><span class="sxs-lookup"><span data-stu-id="60ed5-276">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="既定の (明るい) テーマを持つ会議内線番号を示す例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="60ed5-278">しない: ハードコードの16進値</span><span class="sxs-lookup"><span data-stu-id="60ed5-278">Don't: Hard code hex values</span></span>

<span data-ttu-id="60ed5-279">Teams色のトークンを使用しない場合、デザインの拡張性が低下し、管理に時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-279">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="60ed5-280">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="60ed5-280">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="会議内線番号を [戻る] ボタンで表示する例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="60ed5-282">行う:戻るボタンを持っている</span><span class="sxs-lookup"><span data-stu-id="60ed5-282">Do: Have a back button</span></span>

<span data-ttu-id="60ed5-283">会議内のタブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻ることができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-283">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="2 つの消し込みボタンを持つ会議内線番号を示す例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="60ed5-285">しない: 別の却下ボタンを含める</span><span class="sxs-lookup"><span data-stu-id="60ed5-285">Don't: Include another dismiss button</span></span>

<span data-ttu-id="60ed5-286">[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既に [会議中] タブ自体を閉じるボタンが存在するため、問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-286">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議中のタブ内にモーダル (またはタスク モジュール) を表示する例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="60ed5-288">注意: [会議中] タブ内でモーダルを避ける</span><span class="sxs-lookup"><span data-stu-id="60ed5-288">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="60ed5-289">既に狭い会議内タブのモーダル (タスク モジュールとも呼ばれます) は、コンテンツをラップして隠す可能性があります。</span><span class="sxs-lookup"><span data-stu-id="60ed5-289">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::
