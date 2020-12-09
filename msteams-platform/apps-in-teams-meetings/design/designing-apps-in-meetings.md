---
title: 会議の拡張機能を設計する
author: heath-hamilton
description: Teams 会議でアプリを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606134"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="67b65-103">Microsoft Teams の会議の拡張機能を設計する</span><span class="sxs-lookup"><span data-stu-id="67b65-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="67b65-104">会議の生産性を高めるために、アプリを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="67b65-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="67b65-105">たとえば、通話中にアンケートを完了したり、会議のフローを中断しない簡単なアラームを送信したりするようにユーザーに求めます。</span><span class="sxs-lookup"><span data-stu-id="67b65-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="67b65-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="67b65-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="67b65-107">Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="67b65-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="67b65-108">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="67b65-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="67b65-109">会議の内線番号を追加する</span><span class="sxs-lookup"><span data-stu-id="67b65-109">Add a meeting extension</span></span>

<span data-ttu-id="67b65-110">会議の前と後に会議の内線番号を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="67b65-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="67b65-111">また、Teams ストア (AppSource) から直接特定の会議用アプリを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="67b65-111">You also can an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="67b65-112">会議の前に追加する</span><span class="sxs-lookup"><span data-stu-id="67b65-112">Add before a meeting</span></span>

<span data-ttu-id="67b65-113">会議の前の会議の詳細 [ **タブを追加する]** を選択して、アプリのポップアップを開き、会議用に最適化されたアプリを検索します。</span><span class="sxs-lookup"><span data-stu-id="67b65-113">Before a meeting, the meeting details select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線番号を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="67b65-115">会議中に追加する</span><span class="sxs-lookup"><span data-stu-id="67b65-115">Add during a meeting</span></span>

会議で、[アプリの追加 **] を選択** し、 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Add an app** 必要なアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線番号を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="67b65-118">会議の前</span><span class="sxs-lookup"><span data-stu-id="67b65-118">Before a meeting</span></span>

<span data-ttu-id="67b65-119">会議の前に、タブにコンテンツを追加することができます。次の例は、通話中にユーザーが回答する下書きアンケートの質問を示しています。</span><span class="sxs-lookup"><span data-stu-id="67b65-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、電話をかける前に、会議の詳細のアプリコンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="67b65-121">[構造]: [会議] タブ (会議の前と後)</span><span class="sxs-lookup"><span data-stu-id="67b65-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前後の [会議] タブの構造上の構造を示しています。" border="false":::

|<span data-ttu-id="67b65-123">カウンター</span><span class="sxs-lookup"><span data-stu-id="67b65-123">Counter</span></span>|<span data-ttu-id="67b65-124">説明</span><span class="sxs-lookup"><span data-stu-id="67b65-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="67b65-125">1</span><span class="sxs-lookup"><span data-stu-id="67b65-125">1</span></span>|<span data-ttu-id="67b65-126">**[タブ名**]: タブのナビゲーションラベル。</span><span class="sxs-lookup"><span data-stu-id="67b65-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="67b65-127">2 </span><span class="sxs-lookup"><span data-stu-id="67b65-127">2</span></span>|<span data-ttu-id="67b65-128">**Tab overflow**: 名前の変更や削除などのタブアクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="67b65-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="67b65-129">3 </span><span class="sxs-lookup"><span data-stu-id="67b65-129">3</span></span>|<span data-ttu-id="67b65-130">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="67b65-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="67b65-131">UI テンプレートを使用して設計する</span><span class="sxs-lookup"><span data-stu-id="67b65-131">Designing with UI templates</span></span>

<span data-ttu-id="67b65-132">次の Teams UI テンプレートのいずれかを使用して、[会議] タブのデザインに役立ててください。</span><span class="sxs-lookup"><span data-stu-id="67b65-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="67b65-133">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="67b65-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="67b65-134">[タスクボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="67b65-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="67b65-135">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="67b65-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="67b65-136">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。</span><span class="sxs-lookup"><span data-stu-id="67b65-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="67b65-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="67b65-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="67b65-138">[左](../../concepts/design/design-teams-app-ui-templates.md#left-nav)ナビゲーション: タブにいくつかのナビゲーションが必要な場合は、左側のナビゲーションテンプレートが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="67b65-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="67b65-139">一般的に、タブナビゲーションは最小限にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="67b65-140">[会議中] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="67b65-140">Use an in-meeting tab</span></span>

<span data-ttu-id="67b65-141">[会議中] タブは、会議中に共同作業を補強するためのキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="67b65-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="67b65-142">出席者は、共有またはロールベースのビューを使用して、会議ステージ外の専用の領域にあるアプリコンテンツを表示したり操作したりできます。</span><span class="sxs-lookup"><span data-stu-id="67b65-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="67b65-143">ユース ケース</span><span class="sxs-lookup"><span data-stu-id="67b65-143">Use cases</span></span>

<span data-ttu-id="67b65-144">[会議中] タブを使用して、次のことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="67b65-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="67b65-145">詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)</span><span class="sxs-lookup"><span data-stu-id="67b65-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="67b65-146">会議の参加者用に投票、調査、または仕事アイテムをすばやく作成する</span><span class="sxs-lookup"><span data-stu-id="67b65-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="67b65-147">会議に関連するメモを表示する (たとえば、販売リードに関する情報)</span><span class="sxs-lookup"><span data-stu-id="67b65-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、[会議中] タブに投票の内容を表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="67b65-149">分析: [会議中] タブ</span><span class="sxs-lookup"><span data-stu-id="67b65-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、[会議中] タブの構造上の構造を示しています。" border="false":::

|<span data-ttu-id="67b65-151">カウンター</span><span class="sxs-lookup"><span data-stu-id="67b65-151">Counter</span></span>|<span data-ttu-id="67b65-152">説明</span><span class="sxs-lookup"><span data-stu-id="67b65-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="67b65-153">1</span><span class="sxs-lookup"><span data-stu-id="67b65-153">1</span></span>|<span data-ttu-id="67b65-154">**アプリアイコン (選択済み)**:16 ピクセルの透過アプリロゴ。</span><span class="sxs-lookup"><span data-stu-id="67b65-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="67b65-155">2 </span><span class="sxs-lookup"><span data-stu-id="67b65-155">2</span></span>|<span data-ttu-id="67b65-156">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="67b65-156">**App name**</span></span>|
|<span data-ttu-id="67b65-157">3 </span><span class="sxs-lookup"><span data-stu-id="67b65-157">3</span></span>|<span data-ttu-id="67b65-158">**Header**: アプリ名を含めます。</span><span class="sxs-lookup"><span data-stu-id="67b65-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="67b65-159">4 </span><span class="sxs-lookup"><span data-stu-id="67b65-159">4</span></span>|<span data-ttu-id="67b65-160">[**閉じる] ボタン**: タブを閉じます。フッター内のアクションではなく、右上にある閉じるアイコンを常に使用します。</span><span class="sxs-lookup"><span data-stu-id="67b65-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="67b65-161">5 </span><span class="sxs-lookup"><span data-stu-id="67b65-161">5</span></span>|<span data-ttu-id="67b65-162">**通知バー**: エラー通知はヘッダーのすぐ下に表示され、iframe のコンテンツは20ピクセル下にプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="67b65-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="67b65-163">6 </span><span class="sxs-lookup"><span data-stu-id="67b65-163">6</span></span>|<span data-ttu-id="67b65-164">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="67b65-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="67b65-165">Spacing</span><span class="sxs-lookup"><span data-stu-id="67b65-165">Spacing</span></span>

<span data-ttu-id="67b65-166">280ピクセル幅の iframe 領域内のエッジツーエッジに収まるように、[ミーティング中] タブを最適化します。</span><span class="sxs-lookup"><span data-stu-id="67b65-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="67b65-167">Iframe の左側と右側、タブヘッダー間には、20ピクセルのパディングがあります。</span><span class="sxs-lookup"><span data-stu-id="67b65-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="67b65-168">Iframe はタブの一番下までの完全な裁ち落としです。</span><span class="sxs-lookup"><span data-stu-id="67b65-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例は、[会議中] タブの間隔の大きさを示しています。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="67b65-170">量</span><span class="sxs-lookup"><span data-stu-id="67b65-170">Scrolling</span></span>

<span data-ttu-id="67b65-171">Iframe の内容は垂直方向にスクロールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="67b65-172">スクロールした内容のみが表示されます (何も上または下にありません)。</span><span class="sxs-lookup"><span data-stu-id="67b65-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="67b65-173">Scrollbar は、iframe コンテンツの一部です。</span><span class="sxs-lookup"><span data-stu-id="67b65-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、[会議中] タブのスクロール方法を示しています。" border="false":::

### <a name="navigation"></a><span data-ttu-id="67b65-175">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="67b65-175">Navigation</span></span>

<span data-ttu-id="67b65-176">ナビゲーション層またはヘビーコンテンツがあるシナリオでは、ユーザーがセカンダリレイヤーに移動できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67b65-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="67b65-177">ユーザーは前のレイヤーに戻ることができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例は、会議中のナビゲーションを示しています。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="67b65-179">会議中のダイアログを使用する</span><span class="sxs-lookup"><span data-stu-id="67b65-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="67b65-180">会議中のダイアログは Teams の会議のステージに表示されます。</span><span class="sxs-lookup"><span data-stu-id="67b65-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="67b65-181">ユーザーの注意、確認、または対話が必要ですが、それは微妙で、会議に割り込むことはありません。</span><span class="sxs-lookup"><span data-stu-id="67b65-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="67b65-182">これらは控えめで、タスク指向のシナリオでは使用してください。</span><span class="sxs-lookup"><span data-stu-id="67b65-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="67b65-183">ユース ケース</span><span class="sxs-lookup"><span data-stu-id="67b65-183">Use cases</span></span>

<span data-ttu-id="67b65-184">会議中のダイアログは、参加者が必要になる可能性のあるユーザー (会議の開催者など) によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="67b65-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="67b65-185">簡単なフィードバックを提供する</span><span class="sxs-lookup"><span data-stu-id="67b65-185">Provide brief feedback</span></span>
* <span data-ttu-id="67b65-186">簡単なアンケートまたは投票を行う</span><span class="sxs-lookup"><span data-stu-id="67b65-186">Take a short survey or poll</span></span>
* <span data-ttu-id="67b65-187">承認の提出</span><span class="sxs-lookup"><span data-stu-id="67b65-187">Submit approvals</span></span>
* <span data-ttu-id="67b65-188">アラームを取得する</span><span class="sxs-lookup"><span data-stu-id="67b65-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議中のダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="67b65-190">分析: 会議中のダイアログ</span><span class="sxs-lookup"><span data-stu-id="67b65-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議中のダイアログの構造上の構造を示しています。" border="false":::

|<span data-ttu-id="67b65-192">カウンター</span><span class="sxs-lookup"><span data-stu-id="67b65-192">Counter</span></span>|<span data-ttu-id="67b65-193">説明</span><span class="sxs-lookup"><span data-stu-id="67b65-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="67b65-194">1</span><span class="sxs-lookup"><span data-stu-id="67b65-194">1</span></span>|<span data-ttu-id="67b65-195">**ヘッダー**: アプリアイコン、名前、アクション文字列、および閉じるアイコンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="67b65-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="67b65-196">2 </span><span class="sxs-lookup"><span data-stu-id="67b65-196">2</span></span>|<span data-ttu-id="67b65-197">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="67b65-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="67b65-198">分析: 会議中のダイアログヘッダー</span><span class="sxs-lookup"><span data-stu-id="67b65-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議中のダイアログヘッダーの構造上の構造を示しています。" border="false":::

<span data-ttu-id="67b65-200">2つのヘッダーバリエーションがあります。</span><span class="sxs-lookup"><span data-stu-id="67b65-200">There are two header variants.</span></span> <span data-ttu-id="67b65-201">可能であれば、アバターで variant を使用して、ダイアログがユーザーから送られてくることを強調します。</span><span class="sxs-lookup"><span data-stu-id="67b65-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="67b65-202">カウンター</span><span class="sxs-lookup"><span data-stu-id="67b65-202">Counter</span></span>|<span data-ttu-id="67b65-203">説明</span><span class="sxs-lookup"><span data-stu-id="67b65-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="67b65-204">1</span><span class="sxs-lookup"><span data-stu-id="67b65-204">1</span></span>|<span data-ttu-id="67b65-205">**アバター**: 会議中のダイアログを開始したユーザー。</span><span class="sxs-lookup"><span data-stu-id="67b65-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="67b65-206">2 </span><span class="sxs-lookup"><span data-stu-id="67b65-206">2</span></span>|<span data-ttu-id="67b65-207">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="67b65-207">**App icon**</span></span>|
|<span data-ttu-id="67b65-208">3 </span><span class="sxs-lookup"><span data-stu-id="67b65-208">3</span></span>|<span data-ttu-id="67b65-209">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="67b65-209">**App name**</span></span>|
|<span data-ttu-id="67b65-210">4 </span><span class="sxs-lookup"><span data-stu-id="67b65-210">4</span></span>|<span data-ttu-id="67b65-211">**[閉じる] ボタン**: ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="67b65-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="67b65-212">5 </span><span class="sxs-lookup"><span data-stu-id="67b65-212">5</span></span>|<span data-ttu-id="67b65-213">**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。</span><span class="sxs-lookup"><span data-stu-id="67b65-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="67b65-214">応答性の高い動作</span><span class="sxs-lookup"><span data-stu-id="67b65-214">Responsive behavior</span></span>

<span data-ttu-id="67b65-215">会議中のダイアログのサイズは、シナリオによって異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="67b65-216">パディングとコンポーネントのサイズを維持するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="67b65-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="67b65-217">**幅**: iframe 幅は指定した範囲内の絶対的な値です。</span><span class="sxs-lookup"><span data-stu-id="67b65-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="67b65-218">**高さ**: ダイアログの高さは、iframe のコンテンツによって決まります。</span><span class="sxs-lookup"><span data-stu-id="67b65-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="67b65-219">高さの最大値を超えるコンテンツに対して垂直スクロールが行われます。</span><span class="sxs-lookup"><span data-stu-id="67b65-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを示しています。幅: 最小--280 ピクセル (248 ピクセルの iframe)。Max--460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="67b65-221">会議の後</span><span class="sxs-lookup"><span data-stu-id="67b65-221">After a meeting</span></span>

<span data-ttu-id="67b65-222">会議が終了した後、アプリのコンテンツを表示した後で、会議に戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="67b65-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="67b65-223">この例では、会議の開催者は [ **Contoso** ] タブの [投票結果] を見ることができます。 (注: 設計上の観点からは、[事前に予定されている予定の投稿] および [ミーティング後] タブの動作に違いはありません)。</span><span class="sxs-lookup"><span data-stu-id="67b65-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例は、[ミーティング後] タブを示しています。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="67b65-225">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="67b65-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="67b65-226">関係</span><span class="sxs-lookup"><span data-stu-id="67b65-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="67b65-228">Do: 操作の数を制限する</span><span class="sxs-lookup"><span data-stu-id="67b65-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="67b65-229">会議中のダイアログでは、ユーザーがすばやく作業を行うことができない不要なコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="67b65-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="67b65-231">いいえ: 不要な要素を紹介します。</span><span class="sxs-lookup"><span data-stu-id="67b65-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="67b65-232">複数の対話がある1つの会議中のダイアログでは、通話があいまいになることがあります。</span><span class="sxs-lookup"><span data-stu-id="67b65-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="67b65-233">レイアウト</span><span class="sxs-lookup"><span data-stu-id="67b65-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="67b65-235">手順: 単一列のレイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="67b65-235">Do: Use single-column layouts</span></span>

<span data-ttu-id="67b65-236">ダイアログは会議ステージの中央にあります。タスクの完了は、ユーザーの不満を回避するために、迅速かつシンプルにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="67b65-238">[しない: スペースを整頓する」</span><span class="sxs-lookup"><span data-stu-id="67b65-238">Don't: Clutter the space</span></span>

<span data-ttu-id="67b65-239">高密度または過度に構造化されたコンテンツは、特に会議中に煩雑で圧倒的なものになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-use-single-columns"></a><span data-ttu-id="67b65-241">Do: 単一の列を使用する</span><span class="sxs-lookup"><span data-stu-id="67b65-241">Do: Use single columns</span></span>

<span data-ttu-id="67b65-242">[会議中] タブの絞り込みの性質を考えると、コンテンツを1列で表示することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67b65-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="67b65-244">いいえ: 複数の列を使用します</span><span class="sxs-lookup"><span data-stu-id="67b65-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="67b65-245">[会議中] タブの容量に制限があるため、複数の列を持つレイアウトは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="67b65-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="67b65-246">コントロール</span><span class="sxs-lookup"><span data-stu-id="67b65-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="67b65-248">Do: 右揃えで主な操作を行います。</span><span class="sxs-lookup"><span data-stu-id="67b65-248">Do: Right align the primary action</span></span>

<span data-ttu-id="67b65-249">最も視覚的に大きい操作を、右端に positioining することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67b65-249">We recommend positioining the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="67b65-251">いいえ: 左揃えまたは中央揃えのアクション</span><span class="sxs-lookup"><span data-stu-id="67b65-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="67b65-252">これは、ダイアログでのコントロールの配置に関する標準 Teams パターンとは異なり、一番上にあるダイアログと競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="67b65-253">Scroll</span><span class="sxs-lookup"><span data-stu-id="67b65-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="67b65-255">Do: 上下にスクロール</span><span class="sxs-lookup"><span data-stu-id="67b65-255">Do: Scroll vertically</span></span>

<span data-ttu-id="67b65-256">最も視覚的に大きなアクションは、右端の位置に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67b65-256">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="67b65-258">いいえ: 横方向にスクロール</span><span class="sxs-lookup"><span data-stu-id="67b65-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="67b65-259">水平方向のスクロールは、Teams では予期された動作ではありません。</span><span class="sxs-lookup"><span data-stu-id="67b65-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="67b65-260">会議環境でのその他のキャンバスは、垂直方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="67b65-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="67b65-261">ワークフロー</span><span class="sxs-lookup"><span data-stu-id="67b65-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="67b65-263">Do: [会議中] タブで複雑なシナリオを表示する</span><span class="sxs-lookup"><span data-stu-id="67b65-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="67b65-264">アプリに複数のタスクが含まれている場合は、[会議中] タブで1列のレイアウトを使用することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="67b65-264">If your app includes multiple tasks, we strongly recommend a single-column layout in an in-meeting tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a><span data-ttu-id="67b65-266">[いいえ: 会議中] ダイアログで複雑なシナリオをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="67b65-266">Don't: Package complex scenarios in the in-meeting dialog</span></span>

<span data-ttu-id="67b65-267">会議中のダイアログは、簡単な相互作用を目的としています。</span><span class="sxs-lookup"><span data-stu-id="67b65-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="67b65-268">テーマ</span><span class="sxs-lookup"><span data-stu-id="67b65-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="67b65-270">Do: Teams のカラートークンを使用する</span><span class="sxs-lookup"><span data-stu-id="67b65-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="67b65-271">Teams 会議は、ビジュアルおよび認知ノイズを軽減するために最適化されており、ユーザーがディスカッションと共有コンテンツに集中できるようにするために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="67b65-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="67b65-272">カラートークンの使用について説明します <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(FLUENT UI)</a>。</span><span class="sxs-lookup"><span data-stu-id="67b65-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="67b65-274">[いいえ: 他の消去ボタンを含める]</span><span class="sxs-lookup"><span data-stu-id="67b65-274">Don't: Include another dismiss button</span></span>

<span data-ttu-id="67b65-275">[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既にボタンが表示されているために、会議中のタブ自体が閉じられるという問題が発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="67b65-275">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="67b65-276">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="67b65-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="67b65-278">Do: [戻る] ボタンを用意する</span><span class="sxs-lookup"><span data-stu-id="67b65-278">Do: Have a back button</span></span>

<span data-ttu-id="67b65-279">[会議中] タブでナビゲーションのレイヤーが複数ある場合、ユーザーは前のビューに戻ることができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="67b65-281">[いいえ: 他の消去ボタンを含める]</span><span class="sxs-lookup"><span data-stu-id="67b65-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="67b65-282">[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既にボタンが表示されているために、会議中のタブ自体が閉じられるという問題が発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="67b65-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議の拡張のベストプラクティスを示す例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="67b65-284">注意: [会議中] タブでは modals を回避する</span><span class="sxs-lookup"><span data-stu-id="67b65-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="67b65-285">すでに制限のある [会議中] タブの modals (タスクモジュールとも呼ばれます) は、コンテンツを折り返したり不明瞭にしたりします。</span><span class="sxs-lookup"><span data-stu-id="67b65-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="67b65-286">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="67b65-286">Validate your design</span></span>

<span data-ttu-id="67b65-287">アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="67b65-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="67b65-288">設計検証ガイドラインの確認</span><span class="sxs-lookup"><span data-stu-id="67b65-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
