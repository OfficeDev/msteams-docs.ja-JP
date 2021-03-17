---
title: 会議拡張機能の設計
author: heath-hamilton
description: Teams 会議でアプリを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 83dfaf3f92c00c420f758b66488b4a6b09c75717
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827950"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="08396-103">Microsoft Teams 会議拡張機能の設計</span><span class="sxs-lookup"><span data-stu-id="08396-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="08396-104">アプリを作成して、会議の生産性を高めることができます。</span><span class="sxs-lookup"><span data-stu-id="08396-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="08396-105">たとえば、通話中にアンケートを完了したり、会議のフローを中断しない簡単なリマインダーを送信したりします。</span><span class="sxs-lookup"><span data-stu-id="08396-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="08396-106">Microsoft Teams UI キット</span><span class="sxs-lookup"><span data-stu-id="08396-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="08396-107">必要に応じて取得および変更できる要素を含む、より包括的な設計ガイドラインについては、Microsoft Teams UI Kit を参照してください。</span><span class="sxs-lookup"><span data-stu-id="08396-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08396-108">Microsoft Teams UI キットの取得 (Figma)</span><span class="sxs-lookup"><span data-stu-id="08396-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="08396-109">会議の拡張機能を追加する</span><span class="sxs-lookup"><span data-stu-id="08396-109">Add a meeting extension</span></span>

<span data-ttu-id="08396-110">会議の前と会議中に会議拡張機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="08396-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="08396-111">特定の会議のアプリを Teams ストア (AppSource) から直接追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="08396-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="08396-112">会議の前に追加する</span><span class="sxs-lookup"><span data-stu-id="08396-112">Add before a meeting</span></span>

<span data-ttu-id="08396-113">会議の詳細で、[タブの追加 **] +** を選択してアプリの飛び出しを開き、会議に最適化されたアプリを検索します。</span><span class="sxs-lookup"><span data-stu-id="08396-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="例は、会議の前に会議の内線情報を追加する方法を示しています。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="08396-115">会議中に追加する</span><span class="sxs-lookup"><span data-stu-id="08396-115">Add during a meeting</span></span>

会議で、[その他の :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **アプリの追加] を選択し**、目的のアプリを選択します。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="例は、会議中に会議の内線情報を追加する方法を示しています。" border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="08396-118">会議の前に</span><span class="sxs-lookup"><span data-stu-id="08396-118">Before a meeting</span></span>

<span data-ttu-id="08396-119">会議の前に、タブにコンテンツを追加できます。次の例は、通話中に回答するアンケートの下書き質問を示しています。</span><span class="sxs-lookup"><span data-stu-id="08396-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="例は、通話の前に会議の詳細でコンテンツをアプリする方法を示しています。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="08396-121">解剖学: [会議] タブ (会議の前と後)</span><span class="sxs-lookup"><span data-stu-id="08396-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="例は、会議の前と後の会議タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="08396-123">カウンター</span><span class="sxs-lookup"><span data-stu-id="08396-123">Counter</span></span>|<span data-ttu-id="08396-124">説明</span><span class="sxs-lookup"><span data-stu-id="08396-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="08396-125">1</span><span class="sxs-lookup"><span data-stu-id="08396-125">1</span></span>|<span data-ttu-id="08396-126">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="08396-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="08396-127">2</span><span class="sxs-lookup"><span data-stu-id="08396-127">2</span></span>|<span data-ttu-id="08396-128">**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="08396-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="08396-129">3</span><span class="sxs-lookup"><span data-stu-id="08396-129">3</span></span>|<span data-ttu-id="08396-130">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="08396-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="08396-131">UI テンプレートを使用した設計</span><span class="sxs-lookup"><span data-stu-id="08396-131">Designing with UI templates</span></span>

<span data-ttu-id="08396-132">会議タブを設計するには、次のいずれかの Teams UI テンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="08396-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="08396-133">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="08396-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="08396-134">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="08396-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="08396-135">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="08396-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="08396-136">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="08396-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="08396-137">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="08396-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="08396-138">[左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="08396-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="08396-139">一般に、タブ ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="08396-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="08396-140">[会議内] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="08396-140">Use an in-meeting tab</span></span>

<span data-ttu-id="08396-141">[会議内] タブは、会議中の共同作業を強化するキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="08396-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="08396-142">出席者は、共有ビューまたは役割ベースのビューを使用して、会議ステージ外の専用スペースでアプリ コンテンツを表示および操作できます。</span><span class="sxs-lookup"><span data-stu-id="08396-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="08396-143">ユース ケース</span><span class="sxs-lookup"><span data-stu-id="08396-143">Use cases</span></span>

<span data-ttu-id="08396-144">ユーザーは、[会議内] タブを使用して次の場合があります。</span><span class="sxs-lookup"><span data-stu-id="08396-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="08396-145">詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)</span><span class="sxs-lookup"><span data-stu-id="08396-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="08396-146">会議参加者のポーリング、アンケート、またはタスク アイテムをすばやく作成する</span><span class="sxs-lookup"><span data-stu-id="08396-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="08396-147">会議に関連するメモを表示する (たとえば、営業担当に関する情報)</span><span class="sxs-lookup"><span data-stu-id="08396-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="例は、会議内タブでポーリング コンテンツを表示する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="08396-149">解剖学: [会議中] タブ</span><span class="sxs-lookup"><span data-stu-id="08396-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="例は、会議内タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="08396-151">カウンター</span><span class="sxs-lookup"><span data-stu-id="08396-151">Counter</span></span>|<span data-ttu-id="08396-152">説明</span><span class="sxs-lookup"><span data-stu-id="08396-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="08396-153">1</span><span class="sxs-lookup"><span data-stu-id="08396-153">1</span></span>|<span data-ttu-id="08396-154">**アプリ アイコン (選択):** 16 ピクセルの透明なアプリ ロゴ。</span><span class="sxs-lookup"><span data-stu-id="08396-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="08396-155">2</span><span class="sxs-lookup"><span data-stu-id="08396-155">2</span></span>|<span data-ttu-id="08396-156">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="08396-156">**App name**</span></span>|
|<span data-ttu-id="08396-157">3</span><span class="sxs-lookup"><span data-stu-id="08396-157">3</span></span>|<span data-ttu-id="08396-158">**ヘッダー**: アプリ名が含まれます。</span><span class="sxs-lookup"><span data-stu-id="08396-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="08396-159">4 </span><span class="sxs-lookup"><span data-stu-id="08396-159">4</span></span>|<span data-ttu-id="08396-160">**[閉じる]** ボタン: タブを閉じます。フッターのアクションではなく、常に右上の閉じるアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="08396-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="08396-161">5 </span><span class="sxs-lookup"><span data-stu-id="08396-161">5</span></span>|<span data-ttu-id="08396-162">**通知バー**: エラー通知はヘッダーの直下に表示され、iframe コンテンツを 20 ピクセル下にプッシュします。</span><span class="sxs-lookup"><span data-stu-id="08396-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="08396-163">6 </span><span class="sxs-lookup"><span data-stu-id="08396-163">6</span></span>|<span data-ttu-id="08396-164">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="08396-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="08396-165">Spacing</span><span class="sxs-lookup"><span data-stu-id="08396-165">Spacing</span></span>

<span data-ttu-id="08396-166">280 ピクセル幅の iframe 領域内にエッジからエッジに合わせて会議内タブを最適化します。</span><span class="sxs-lookup"><span data-stu-id="08396-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="08396-167">iframe の左側と右側、およびタブ ヘッダーの間には 20 ピクセルのパディングがあります。</span><span class="sxs-lookup"><span data-stu-id="08396-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="08396-168">iframe はタブの下部に完全にブリードされます。</span><span class="sxs-lookup"><span data-stu-id="08396-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="例では、会議中のタブ間隔のディメンションを示します。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="08396-170">スクロール</span><span class="sxs-lookup"><span data-stu-id="08396-170">Scrolling</span></span>

<span data-ttu-id="08396-171">Iframe のコンテンツは垂直方向にスクロールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="08396-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="08396-172">スクロールしたコンテンツのみを表示できます (上または下に何も表示されません)。</span><span class="sxs-lookup"><span data-stu-id="08396-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="08396-173">スクロール バーは、iframe コンテンツの一部です。</span><span class="sxs-lookup"><span data-stu-id="08396-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="例は、会議内タブのスクロール方法を示しています。" border="false":::

### <a name="navigation"></a><span data-ttu-id="08396-175">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="08396-175">Navigation</span></span>

<span data-ttu-id="08396-176">ナビゲーション レイヤーやコンテンツが多いシナリオでは、ユーザーがセカンダリ レイヤーに移動できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="08396-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="08396-177">ユーザーは前のレイヤーに戻る必要があります。</span><span class="sxs-lookup"><span data-stu-id="08396-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="例では、会議内ナビゲーションを示します。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="08396-179">会議内ダイアログの使用</span><span class="sxs-lookup"><span data-stu-id="08396-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="08396-180">会議中のダイアログが Teams 会議ステージに表示されます。</span><span class="sxs-lookup"><span data-stu-id="08396-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="08396-181">ユーザーの注意、確認、またはやり取りが必要ですが、微妙であり、会議を中断しません。</span><span class="sxs-lookup"><span data-stu-id="08396-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="08396-182">これらの使用は、軽くてタスク指向のシナリオに対して使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="08396-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="08396-183">ユース ケース</span><span class="sxs-lookup"><span data-stu-id="08396-183">Use cases</span></span>

<span data-ttu-id="08396-184">会議中のダイアログは、参加者が次の操作を行うユーザー (会議の開催者など) によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="08396-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="08396-185">簡単なフィードバックを提供する</span><span class="sxs-lookup"><span data-stu-id="08396-185">Provide brief feedback</span></span>
* <span data-ttu-id="08396-186">短いアンケートまたは投票を行う</span><span class="sxs-lookup"><span data-stu-id="08396-186">Take a short survey or poll</span></span>
* <span data-ttu-id="08396-187">承認を送信する</span><span class="sxs-lookup"><span data-stu-id="08396-187">Submit approvals</span></span>
* <span data-ttu-id="08396-188">アラームを取得する</span><span class="sxs-lookup"><span data-stu-id="08396-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="例は、会議内ダイアログを使用する方法を示しています。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="08396-190">解剖学: 会議中のダイアログ</span><span class="sxs-lookup"><span data-stu-id="08396-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議内ダイアログの構造構造を示しています。" border="false":::

|<span data-ttu-id="08396-192">カウンター</span><span class="sxs-lookup"><span data-stu-id="08396-192">Counter</span></span>|<span data-ttu-id="08396-193">説明</span><span class="sxs-lookup"><span data-stu-id="08396-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="08396-194">1</span><span class="sxs-lookup"><span data-stu-id="08396-194">1</span></span>|<span data-ttu-id="08396-195">**ヘッダー**: アプリ アイコン、名前、アクション文字列、閉じるアイコンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="08396-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="08396-196">2</span><span class="sxs-lookup"><span data-stu-id="08396-196">2</span></span>|<span data-ttu-id="08396-197">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="08396-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="08396-198">Anatomy: 会議内ダイアログ ヘッダー</span><span class="sxs-lookup"><span data-stu-id="08396-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="例は、会議中のダイアログ ヘッダーの構造構造を示しています。" border="false":::

<span data-ttu-id="08396-200">2 つのヘッダーバリアントがあります。</span><span class="sxs-lookup"><span data-stu-id="08396-200">There are two header variants.</span></span> <span data-ttu-id="08396-201">可能であれば、アバターと一緒にバリアントを使用して、ダイアログが人から来ているのを強化します。</span><span class="sxs-lookup"><span data-stu-id="08396-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="08396-202">カウンター</span><span class="sxs-lookup"><span data-stu-id="08396-202">Counter</span></span>|<span data-ttu-id="08396-203">説明</span><span class="sxs-lookup"><span data-stu-id="08396-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="08396-204">1</span><span class="sxs-lookup"><span data-stu-id="08396-204">1</span></span>|<span data-ttu-id="08396-205">**アバター**: 会議内ダイアログを開始するユーザー。</span><span class="sxs-lookup"><span data-stu-id="08396-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="08396-206">2</span><span class="sxs-lookup"><span data-stu-id="08396-206">2</span></span>|<span data-ttu-id="08396-207">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="08396-207">**App icon**</span></span>|
|<span data-ttu-id="08396-208">3</span><span class="sxs-lookup"><span data-stu-id="08396-208">3</span></span>|<span data-ttu-id="08396-209">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="08396-209">**App name**</span></span>|
|<span data-ttu-id="08396-210">4 </span><span class="sxs-lookup"><span data-stu-id="08396-210">4</span></span>|<span data-ttu-id="08396-211">**[閉じる]** ボタン: ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="08396-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="08396-212">5 </span><span class="sxs-lookup"><span data-stu-id="08396-212">5</span></span>|<span data-ttu-id="08396-213">**アクション文字列**: 通常、ダイアログを開始したユーザーを示します。</span><span class="sxs-lookup"><span data-stu-id="08396-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="08396-214">応答性の高い動作</span><span class="sxs-lookup"><span data-stu-id="08396-214">Responsive behavior</span></span>

<span data-ttu-id="08396-215">会議内のダイアログは、さまざまなシナリオを考慮してサイズが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="08396-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="08396-216">パディングとコンポーネントのサイズは必ず維持してください。</span><span class="sxs-lookup"><span data-stu-id="08396-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="08396-217">**Width**: ダイアログの iframe 幅は、指定した範囲内の絶対値です。</span><span class="sxs-lookup"><span data-stu-id="08396-217">**Width**: The iframe width of the dialog is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="08396-218">**Height**: ダイアログの iframe の高さは、指定した範囲内の絶対値です。</span><span class="sxs-lookup"><span data-stu-id="08396-218">**Height**: The iframe height of the dialog is an absolute value within the range you specify.</span></span>

> [!NOTE]
> <span data-ttu-id="08396-219">幅と高さに対して定義する値は、会議内 `externalResourceURL` ダイアログで使用されます。</span><span class="sxs-lookup"><span data-stu-id="08396-219">The values that you define for the width and height are used in `externalResourceURL` of in-meeting dialog.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="例は、会議中のダイアログを表示します。幅: 最小--280 ピクセル (248 ピクセルの iframe)。Max---460 ピクセル (428 ピクセルの iframe)。高さ: 300 ピクセル (iframe)。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="08396-221">会議の後</span><span class="sxs-lookup"><span data-stu-id="08396-221">After a meeting</span></span>

<span data-ttu-id="08396-222">会議の終了後に会議に戻り、アプリのコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="08396-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="08396-223">この例では、会議開催者は **[Contoso]** タブで投票結果を確認できます (注: デザインの観点から、会議前と会議後のタブ エクスペリエンスの違いはありません)。</span><span class="sxs-lookup"><span data-stu-id="08396-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="例は、会議後のタブを示しています。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="08396-225">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="08396-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="08396-226">対話</span><span class="sxs-lookup"><span data-stu-id="08396-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="操作の数を制限する方法を示す例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="08396-228">Do: 操作の数を制限する</span><span class="sxs-lookup"><span data-stu-id="08396-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="08396-229">会議中のダイアログでは、ユーザーが何かを迅速に実行するのに役立つ不要なコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="08396-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="不要な要素を導入しない方法を示す例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="08396-231">[しない]: 不要な要素を導入する</span><span class="sxs-lookup"><span data-stu-id="08396-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="08396-232">複数の操作を含む単一の会議内ダイアログは、通話の邪魔になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="08396-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="08396-233">レイアウト</span><span class="sxs-lookup"><span data-stu-id="08396-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="1 列のダイアログ レイアウトを使用する方法を示す例。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="08396-235">Do: 1 列のダイアログ レイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="08396-235">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="08396-236">ダイアログは会議ステージの中心にあるので、タスクの完了はユーザーの不満を避けるために迅速かつ簡単に行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="08396-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="会議内線のスペースを煩雑にしてはいけないことを示す例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="08396-238">T't: スペースを乱雑にする</span><span class="sxs-lookup"><span data-stu-id="08396-238">Don't: Clutter the space</span></span>

<span data-ttu-id="08396-239">密なコンテンツや過剰に構造化されたコンテンツは、特に会議中に気が散り、圧倒的になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="08396-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="1 列のタブ レイアウトを表示する例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="08396-241">Do: 1 列のタブ レイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="08396-241">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="08396-242">会議内タブの狭い性質を考えると、コンテンツを 1 つの列に表示することを強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="08396-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="複数の列を持つタブを表示する例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="08396-244">[しない]: 複数の列を使用する</span><span class="sxs-lookup"><span data-stu-id="08396-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="08396-245">会議内タブのスペースが限られているので、複数の列を含むレイアウトは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="08396-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="08396-246">コントロール</span><span class="sxs-lookup"><span data-stu-id="08396-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="プライマリ コントロールを右揃えする方法を示す例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="08396-248">Do: プライマリ アクションを右揃えする</span><span class="sxs-lookup"><span data-stu-id="08396-248">Do: Right align the primary action</span></span>

<span data-ttu-id="08396-249">最も視覚的に重いアクションを最も右の位置に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="08396-249">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="プライマリ コントロールを左揃えにしない方法を示す例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="08396-251">[しない]: 左揃えまたは中央揃えアクション</span><span class="sxs-lookup"><span data-stu-id="08396-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="08396-252">これは、ダイアログ内のコントロールの配置に関する標準的な Teams パターンから離れ、上部のダイアログボックスと競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="08396-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="08396-253">Scroll</span><span class="sxs-lookup"><span data-stu-id="08396-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="会議内タブで垂直スクロールを表示する例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="08396-255">Do: 垂直方向にスクロールする</span><span class="sxs-lookup"><span data-stu-id="08396-255">Do: Scroll vertically</span></span>

<span data-ttu-id="08396-256">ユーザーは Teams (および他の場所) での垂直スクロールを期待します。</span><span class="sxs-lookup"><span data-stu-id="08396-256">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="会議内タブに水平スクロールを表示する例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="08396-258">[しない]: 水平方向にスクロールする</span><span class="sxs-lookup"><span data-stu-id="08396-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="08396-259">Teams での水平方向のスクロールは予期しない動作です。</span><span class="sxs-lookup"><span data-stu-id="08396-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="08396-260">会議環境内の他のキャンバスは垂直方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="08396-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="08396-261">ワークフロー</span><span class="sxs-lookup"><span data-stu-id="08396-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="会議内タブに複雑なシナリオを表示する例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="08396-263">Do: [会議内] タブの複雑なシナリオを表示する</span><span class="sxs-lookup"><span data-stu-id="08396-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="08396-264">アプリに複数のタスクが含まれる場合は、1 列のレイアウトで会議内タブを使用することを強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="08396-264">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="会議内ダイアログで複雑なシナリオを表示する例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="08396-266">[しない]: 会議内のダイアログを複雑にする</span><span class="sxs-lookup"><span data-stu-id="08396-266">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="08396-267">会議中のダイアログは、簡単な操作を目的とします。</span><span class="sxs-lookup"><span data-stu-id="08396-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="08396-268">テーマ</span><span class="sxs-lookup"><span data-stu-id="08396-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="暗いテーマで会議の拡張機能を表示する例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="08396-270">Do: Teams カラー トークンを使用する</span><span class="sxs-lookup"><span data-stu-id="08396-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="08396-271">Teams の会議は、ユーザーがディスカッションと共有コンテンツに集中できるよう、視覚的および認知的なノイズを減らすのに役立つダーク モード用に最適化されています。</span><span class="sxs-lookup"><span data-stu-id="08396-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="08396-272">カラー トークン <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">(Fluent UI) の使用について学習します</a>。</span><span class="sxs-lookup"><span data-stu-id="08396-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="既定の (明るい) テーマを持つ会議拡張機能を表示する例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="08396-274">Don't: ハード コードの 16 進値</span><span class="sxs-lookup"><span data-stu-id="08396-274">Don't: Hard code hex values</span></span>

<span data-ttu-id="08396-275">Teams カラー トークンを使用しない場合、デザインの拡張性が低く、管理に時間がかかっています。</span><span class="sxs-lookup"><span data-stu-id="08396-275">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="08396-276">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="08396-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="戻るボタンを使用して会議の拡張機能を表示する例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="08396-278">Do: [戻る] ボタンを持つ</span><span class="sxs-lookup"><span data-stu-id="08396-278">Do: Have a back button</span></span>

<span data-ttu-id="08396-279">会議内タブに複数のナビゲーション レイヤーがある場合、ユーザーは以前のビューに戻る必要があります。</span><span class="sxs-lookup"><span data-stu-id="08396-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="2 つの閉じボタンを使用して会議の内線表示オプションを表示する例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="08396-281">[しない] : 別の [閉じ] ボタンを含める</span><span class="sxs-lookup"><span data-stu-id="08396-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="08396-282">会議中のタブ コンテンツを閉じるオプションを指定すると、ヘッダーに既に会議中のタブ自体を閉じるボタンが存在するために問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="08396-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="会議内タブ内にモーダル (またはタスク モジュール) を表示する例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="08396-284">注意: [会議内] タブ内のモーダルを回避する</span><span class="sxs-lookup"><span data-stu-id="08396-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="08396-285">既に狭い会議内タブのモーダル (タスク モジュールとも呼ばれる) は、コンテンツをラップしてあいまいにしている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="08396-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="08396-286">デザインを検証する</span><span class="sxs-lookup"><span data-stu-id="08396-286">Validate your design</span></span>

<span data-ttu-id="08396-287">アプリを AppSource に発行する予定の場合は、申請中にアプリが失敗する一般的な設計上の問題を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="08396-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08396-288">デザイン検証のガイドラインを確認する</span><span class="sxs-lookup"><span data-stu-id="08396-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
