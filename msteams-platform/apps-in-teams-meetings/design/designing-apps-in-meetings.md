---
title: 会議の内線情報の設計
author: heath-hamilton
description: Teams 会議でアプリを設計し、Microsoft Teams UI Kit を取得する方法について説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: c6e76356b698da4e32e279b0842ab2cc35254e99
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886759"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="3ce7f-103">Microsoft Teams 会議の内線番号の設計</span><span class="sxs-lookup"><span data-stu-id="3ce7f-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="3ce7f-104">会議の生産性を向上させるアプリを作成できます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="3ce7f-105">たとえば、通話中にアンケートを完了したり、会議の流れを中断しないクイック リマインダーを送信したりします。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3ce7f-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="3ce7f-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3ce7f-107">必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインについては、Microsoft Teams UI Kit をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ce7f-108">Microsoft Teams UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="3ce7f-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="3ce7f-109">会議の内線を追加する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-109">Add a meeting extension</span></span>

<span data-ttu-id="3ce7f-110">会議の前と会議中に会議の内線を追加できます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="3ce7f-111">特定の会議用のアプリを Teams ストア (AppSource) から直接追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="3ce7f-112">会議の前に追加する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-112">Add before a meeting</span></span>

<span data-ttu-id="3ce7f-113">会議の詳細で、タブの追加 **+** を選択してアプリのフライアウトを開き、会議用に最適化されたアプリを検索します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="3ce7f-115">会議中に追加する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-115">Add during a meeting</span></span>

会議で、[その他の **アプリ** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **の追加] を選択し**、目的のアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="3ce7f-118">会議の前に</span><span class="sxs-lookup"><span data-stu-id="3ce7f-118">Before a meeting</span></span>

<span data-ttu-id="3ce7f-119">会議の前に、タブにコンテンツを追加できます。次の例は、通話中に回答する下書きアンケート質問を示しています。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細にコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="3ce7f-121">構造: [会議] タブ (会議の前と後)</span><span class="sxs-lookup"><span data-stu-id="3ce7f-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前と後の会議タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="3ce7f-123">カウンター</span><span class="sxs-lookup"><span data-stu-id="3ce7f-123">Counter</span></span>|<span data-ttu-id="3ce7f-124">説明</span><span class="sxs-lookup"><span data-stu-id="3ce7f-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3ce7f-125">1</span><span class="sxs-lookup"><span data-stu-id="3ce7f-125">1</span></span>|<span data-ttu-id="3ce7f-126">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="3ce7f-127">2 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-127">2</span></span>|<span data-ttu-id="3ce7f-128">**タブ オーバーフロー**: 名前の変更や削除などのタブアクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="3ce7f-129">3</span><span class="sxs-lookup"><span data-stu-id="3ce7f-129">3</span></span>|<span data-ttu-id="3ce7f-130">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="3ce7f-131">UI テンプレートを使用した設計</span><span class="sxs-lookup"><span data-stu-id="3ce7f-131">Designing with UI templates</span></span>

<span data-ttu-id="3ce7f-132">会議タブを設計するには、次のいずれかの Teams UI テンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="3ce7f-133">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="3ce7f-134">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスク ボードは、カンバボードまたはスレーンと呼ばれることもあるタスク ボードで、作業項目やチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="3ce7f-135">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="3ce7f-136">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="3ce7f-137">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="3ce7f-138">[左側のナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="3ce7f-139">一般に、タブ ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="3ce7f-140">会議内タブを使用する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-140">Use an in-meeting tab</span></span>

<span data-ttu-id="3ce7f-141">[会議内] タブは、会議中のコラボレーションを拡張するキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="3ce7f-142">参加者は、共有ビューまたはロール ベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示および操作できます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="3ce7f-143">使用例</span><span class="sxs-lookup"><span data-stu-id="3ce7f-143">Use cases</span></span>

<span data-ttu-id="3ce7f-144">ユーザーは会議中タブを使用して次の場合があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="3ce7f-145">詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)</span><span class="sxs-lookup"><span data-stu-id="3ce7f-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="3ce7f-146">会議参加者の投票、アンケート、またはタスク アイテムをすばやく作成する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="3ce7f-147">会議に関連するメモを表示する (たとえば、営業リードに関する情報)</span><span class="sxs-lookup"><span data-stu-id="3ce7f-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、会議内タブで投票コンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="3ce7f-149">構造: [会議内] タブ</span><span class="sxs-lookup"><span data-stu-id="3ce7f-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議内タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="3ce7f-151">カウンター</span><span class="sxs-lookup"><span data-stu-id="3ce7f-151">Counter</span></span>|<span data-ttu-id="3ce7f-152">説明</span><span class="sxs-lookup"><span data-stu-id="3ce7f-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3ce7f-153">1</span><span class="sxs-lookup"><span data-stu-id="3ce7f-153">1</span></span>|<span data-ttu-id="3ce7f-154">**アプリ アイコン (選択):** 16 ピクセルの透明なアプリ ロゴ。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="3ce7f-155">2 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-155">2</span></span>|<span data-ttu-id="3ce7f-156">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="3ce7f-156">**App name**</span></span>|
|<span data-ttu-id="3ce7f-157">3</span><span class="sxs-lookup"><span data-stu-id="3ce7f-157">3</span></span>|<span data-ttu-id="3ce7f-158">**ヘッダー**: アプリ名が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="3ce7f-159">4 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-159">4</span></span>|<span data-ttu-id="3ce7f-160">**[閉じる] ボタン**: タブを閉じます。フッターのアクションの代わりに、常に右上の閉じるアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="3ce7f-161">5 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-161">5</span></span>|<span data-ttu-id="3ce7f-162">**通知バー**: エラー通知はヘッダーの直下に表示され、iframe コンテンツを 20 ピクセル下にプッシュします。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="3ce7f-163">6 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-163">6</span></span>|<span data-ttu-id="3ce7f-164">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="3ce7f-165">Spacing</span><span class="sxs-lookup"><span data-stu-id="3ce7f-165">Spacing</span></span>

<span data-ttu-id="3ce7f-166">280 ピクセル幅の iframe 領域内に端から端まで収まる会議内タブを最適化します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="3ce7f-167">iframe の左右とタブ ヘッダーの間には 20 ピクセルのパディングがあります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="3ce7f-168">iframe はタブの下部にフル ブリードされます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="会議中のタブ間隔のサイズの例を示します。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="3ce7f-170">スクロール</span><span class="sxs-lookup"><span data-stu-id="3ce7f-170">Scrolling</span></span>

<span data-ttu-id="3ce7f-171">Iframe の内容は垂直方向にスクロールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="3ce7f-172">スクロールしたコンテンツのみ表示できます (上または下に何も表示されません)。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="3ce7f-173">スクロール バーは iframe コンテンツの一部です。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="会議中のタブのスクロール方法の例を示します。" border="false":::

### <a name="navigation"></a><span data-ttu-id="3ce7f-175">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="3ce7f-175">Navigation</span></span>

<span data-ttu-id="3ce7f-176">ナビゲーション レイヤーやコンテンツの多いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="3ce7f-177">ユーザーは前のレイヤーに戻れなければならない。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例は、会議内ナビゲーションを示しています。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="3ce7f-179">会議中ダイアログを使用する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="3ce7f-180">会議中のダイアログは Teams の会議ステージに表示されます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="3ce7f-181">ユーザーの注意、確認、またはやり取りが必要ですが、会議を中断することなく、微妙です。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="3ce7f-182">これらは、淡色でタスク指向のシナリオに対して、念入りに使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="3ce7f-183">使用例</span><span class="sxs-lookup"><span data-stu-id="3ce7f-183">Use cases</span></span>

<span data-ttu-id="3ce7f-184">会議内ダイアログは、参加者が次の操作を行うユーザー (会議の開催者など) によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="3ce7f-185">簡単なフィードバックを提供する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-185">Provide brief feedback</span></span>
* <span data-ttu-id="3ce7f-186">短いアンケートまたは投票を行う</span><span class="sxs-lookup"><span data-stu-id="3ce7f-186">Take a short survey or poll</span></span>
* <span data-ttu-id="3ce7f-187">承認を送信する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-187">Submit approvals</span></span>
* <span data-ttu-id="3ce7f-188">アラームを取得する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議中のダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="3ce7f-190">構造: 会議内ダイアログ</span><span class="sxs-lookup"><span data-stu-id="3ce7f-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議中ダイアログの構造構造を示しています。" border="false":::

|<span data-ttu-id="3ce7f-192">カウンター</span><span class="sxs-lookup"><span data-stu-id="3ce7f-192">Counter</span></span>|<span data-ttu-id="3ce7f-193">説明</span><span class="sxs-lookup"><span data-stu-id="3ce7f-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3ce7f-194">1</span><span class="sxs-lookup"><span data-stu-id="3ce7f-194">1</span></span>|<span data-ttu-id="3ce7f-195">**ヘッダー**: アプリ アイコン、名前、アクション文字列、閉じるアイコンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="3ce7f-196">2 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-196">2</span></span>|<span data-ttu-id="3ce7f-197">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="3ce7f-198">構造: 会議内ダイアログ ヘッダー</span><span class="sxs-lookup"><span data-stu-id="3ce7f-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議中ダイアログ ヘッダーの構造構造を示しています。" border="false":::

<span data-ttu-id="3ce7f-200">ヘッダーには 2 つのバリエーションがあります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-200">There are two header variants.</span></span> <span data-ttu-id="3ce7f-201">可能であれば、アバターと一緒にバリアントを使用して、ダイアログがユーザーから来ているのを強化します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="3ce7f-202">カウンター</span><span class="sxs-lookup"><span data-stu-id="3ce7f-202">Counter</span></span>|<span data-ttu-id="3ce7f-203">説明</span><span class="sxs-lookup"><span data-stu-id="3ce7f-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3ce7f-204">1</span><span class="sxs-lookup"><span data-stu-id="3ce7f-204">1</span></span>|<span data-ttu-id="3ce7f-205">**アバター**: 会議中のダイアログを開始するユーザー。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="3ce7f-206">2 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-206">2</span></span>|<span data-ttu-id="3ce7f-207">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="3ce7f-207">**App icon**</span></span>|
|<span data-ttu-id="3ce7f-208">3</span><span class="sxs-lookup"><span data-stu-id="3ce7f-208">3</span></span>|<span data-ttu-id="3ce7f-209">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="3ce7f-209">**App name**</span></span>|
|<span data-ttu-id="3ce7f-210">4 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-210">4</span></span>|<span data-ttu-id="3ce7f-211">**[閉じる]** ボタン : ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="3ce7f-212">5 </span><span class="sxs-lookup"><span data-stu-id="3ce7f-212">5</span></span>|<span data-ttu-id="3ce7f-213">**操作文字列**: 通常、ダイアログを開始したユーザーを示します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="3ce7f-214">応答性の高い動作</span><span class="sxs-lookup"><span data-stu-id="3ce7f-214">Responsive behavior</span></span>

<span data-ttu-id="3ce7f-215">会議中のダイアログは、シナリオによってサイズが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="3ce7f-216">パディングとコンポーネントのサイズは必ず維持してください。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="3ce7f-217">**Width**: iframe の幅は、指定した範囲内の絶対値です。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="3ce7f-218">**Height**: ダイアログの高さは、iframe 内のコンテンツによって決まります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="3ce7f-219">垂直方向のスクロールは、最大の高さを超えるコンテンツに引き継がされます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例では、会議中のダイアログを表示します。幅: 最小 - 280 ピクセル (248 ピクセルの iframe)。最大 - 460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="3ce7f-221">会議後</span><span class="sxs-lookup"><span data-stu-id="3ce7f-221">After a meeting</span></span>

<span data-ttu-id="3ce7f-222">会議の終了後に会議に戻り、アプリのコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="3ce7f-223">この例では、会議の開催者は **[Contoso]** タブで投票結果を確認できます (注: 設計上の観点から、会議前と会議後のタブエクスペリエンスの違いはありません)。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="3ce7f-225">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="3ce7f-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="3ce7f-226">操作</span><span class="sxs-lookup"><span data-stu-id="3ce7f-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="操作の数を制限する方法を示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="3ce7f-228">操作の数を制限する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="3ce7f-229">会議中のダイアログの場合は、ユーザーがすばやく何かを成し遂げるのに役立つ不要なコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="不要な要素を導入しない方法を示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="3ce7f-231">不要な要素を導入しない</span><span class="sxs-lookup"><span data-stu-id="3ce7f-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="3ce7f-232">複数の対話を含む 1 つの会議内ダイアログは、通話の邪魔になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="3ce7f-233">レイアウト</span><span class="sxs-lookup"><span data-stu-id="3ce7f-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="単一列のダイアログ レイアウトの使い方を示す例。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="3ce7f-235">行う: 単一列のダイアログ レイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-235">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="3ce7f-236">ダイアログは会議ステージの中心にあるので、ユーザーの不満を避けるため、タスクの完了は迅速かつシンプルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議の内線のスペースを低優先にしてはいけないことを示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="3ce7f-238">不要: スペースを整理する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-238">Don't: Clutter the space</span></span>

<span data-ttu-id="3ce7f-239">密度の高いコンテンツや過剰に構造化されたコンテンツは、特に会議中に、気が散らされ、圧倒される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="1 列のタブ レイアウトを表示する例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="3ce7f-241">行う: 単一列のタブ レイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-241">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="3ce7f-242">会議中タブの性質が狭い場合は、コンテンツを 1 つの列に表示することを強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="複数の列を含むタブを表示する例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="3ce7f-244">使用しない: 複数の列を使用する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="3ce7f-245">会議内タブのスペースが限られているので、複数の列を含むレイアウトは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="3ce7f-246">コントロール</span><span class="sxs-lookup"><span data-stu-id="3ce7f-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="プライマリ コントロールを右揃えする方法を示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="3ce7f-248">Do: Right align the primary action</span><span class="sxs-lookup"><span data-stu-id="3ce7f-248">Do: Right align the primary action</span></span>

<span data-ttu-id="3ce7f-249">視覚的に最も大きなアクションは、最も右の位置に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-249">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="プライマリ コントロールを左揃えにしない方法を示す例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="3ce7f-251">Don't: 左揃えまたは中央揃えアクション</span><span class="sxs-lookup"><span data-stu-id="3ce7f-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="3ce7f-252">これは、ダイアログでのコントロール配置の標準の Teams パターンとは異なり、上部のダイアログと競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="3ce7f-253">Scroll</span><span class="sxs-lookup"><span data-stu-id="3ce7f-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議中のタブでの垂直方向のスクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="3ce7f-255">行う: 縦方向にスクロールする</span><span class="sxs-lookup"><span data-stu-id="3ce7f-255">Do: Scroll vertically</span></span>

<span data-ttu-id="3ce7f-256">ユーザーは、Teams (および他の場所) での垂直方向のスクロールを期待します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-256">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議中のタブで水平方向のスクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="3ce7f-258">水平方向にスクロールしない</span><span class="sxs-lookup"><span data-stu-id="3ce7f-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="3ce7f-259">水平方向のスクロールは、Teams では想定される動作ではありません。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="3ce7f-260">会議環境内の他のキャンバスは垂直方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="3ce7f-261">ワークフロー</span><span class="sxs-lookup"><span data-stu-id="3ce7f-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議内タブに複雑なシナリオを表示する例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="3ce7f-263">行う: 会議内タブで複雑なシナリオを表示する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="3ce7f-264">アプリに複数のタスクが含まれる場合は、1 列のレイアウトで会議内タブを使用することを強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-264">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議中のダイアログで複雑なシナリオを表示する例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="3ce7f-266">[しない]: 会議内ダイアログを複雑にする</span><span class="sxs-lookup"><span data-stu-id="3ce7f-266">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="3ce7f-267">会議中のダイアログは、簡単な対話を目的とします。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="3ce7f-268">テーマ</span><span class="sxs-lookup"><span data-stu-id="3ce7f-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="濃色テーマの会議の拡張機能を表示する例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="3ce7f-270">行う: Teams のカラー トークンを使用する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="3ce7f-271">Teams 会議は、ユーザーがディスカッションと共有コンテンツに集中できるよう、視覚的および認知的な雑音を減らすために、濃色モード用に最適化されています。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="3ce7f-272">カラー トークン <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI) の使用について学習します</a>。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="既定 (淡色) テーマの会議の内線を表示する例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="3ce7f-274">[しない]: ハード コードの 16 進値</span><span class="sxs-lookup"><span data-stu-id="3ce7f-274">Don't: Hard code hex values</span></span>

<span data-ttu-id="3ce7f-275">Teams のカラー トークンを使用しない場合、設計の拡張性が低く、管理に時間がかかる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-275">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="3ce7f-276">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="3ce7f-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="[戻る] ボタンを使用して会議の内線を表示する例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="3ce7f-278">実行する: [戻る] ボタンがある</span><span class="sxs-lookup"><span data-stu-id="3ce7f-278">Do: Have a back button</span></span>

<span data-ttu-id="3ce7f-279">会議中のタブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻れなければならない。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="2 つの閉じボタンを持つ会議の内線を表示する例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="3ce7f-281">[しない]: 別の閉じボタンを含める</span><span class="sxs-lookup"><span data-stu-id="3ce7f-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="3ce7f-282">会議中のタブ コンテンツを閉じるオプションを指定すると、会議内タブ自体を閉じるボタンがヘッダーに既に存在する場合に問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議内タブ内にモーダル (またはタスク モジュール) を表示する例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="3ce7f-284">注意: [会議中] タブ内でモーダルを回避する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="3ce7f-285">既に狭い会議内タブのモーダル (タスク モジュールとも呼ばれる) は、コンテンツを折り返してあいまいにしている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="3ce7f-286">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-286">Validate your design</span></span>

<span data-ttu-id="3ce7f-287">アプリを AppSource に公開する予定の場合は、申請中にアプリが失敗する一般的な設計上の問題を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ce7f-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ce7f-288">設計検証のガイドラインを確認する</span><span class="sxs-lookup"><span data-stu-id="3ce7f-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
