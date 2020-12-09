---
title: UI テンプレートを使用してアプリを設計する
author: heath-hamilton
description: Microsoft Teams 全体でよく見られる標準化された UI コンポーネント、レイアウト、パターンを使用して、アプリをより迅速に設計します。
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 144c18ab03d76e442a4de64a5c61af76cb2b8b5f
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606081"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="334a0-103">UI テンプレートを使用して Microsoft Teams アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="334a0-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="334a0-104">UI テンプレートを使用して、より迅速に Microsoft Teams アプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="334a0-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="334a0-105">テンプレートは、一般的なチームのユースケースの間で機能する Fluent UI ベースのコンポーネントのコレクションであり、ユーザーにとって最適な環境を得るための時間を増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="334a0-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="334a0-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="334a0-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="334a0-107">Microsoft Teams UI キットから UI テンプレートを取得することができます。これには、利用状況、構造、アクセシビリティ、およびベストプラクティスに関する広範な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="334a0-107">You can grab UI templates from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="334a0-108">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="334a0-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="list"></a><span data-ttu-id="334a0-109">リスト</span><span class="sxs-lookup"><span data-stu-id="334a0-109">List</span></span>

<span data-ttu-id="334a0-110">リストを使用して、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="334a0-110">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、リスト UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-112">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-112">Top use cases</span></span>

* <span data-ttu-id="334a0-113">データの表示</span><span class="sxs-lookup"><span data-stu-id="334a0-113">Display data</span></span>
* <span data-ttu-id="334a0-114">アプリコンテンツに対するコンテキストアクション</span><span class="sxs-lookup"><span data-stu-id="334a0-114">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="334a0-115">ダッシュボード</span><span class="sxs-lookup"><span data-stu-id="334a0-115">Dashboard</span></span>

<span data-ttu-id="334a0-116">ダッシュボードは、さまざまな種類のコンテンツを中央の場所 (Teams の個人アプリまたはタブ) に表示します。</span><span class="sxs-lookup"><span data-stu-id="334a0-116">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="334a0-117">ダッシュボードに表示される情報の一部をユーザーがカスタマイズできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="334a0-117">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例はダッシュボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-119">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-119">Top use cases</span></span>

* <span data-ttu-id="334a0-120">データを分析する</span><span class="sxs-lookup"><span data-stu-id="334a0-120">Analyze data</span></span>
* <span data-ttu-id="334a0-121">レポートの指標</span><span class="sxs-lookup"><span data-stu-id="334a0-121">Report metrics</span></span>
* <span data-ttu-id="334a0-122">異なる情報を1か所にまとめます。</span><span class="sxs-lookup"><span data-stu-id="334a0-122">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="334a0-123">フォーム</span><span class="sxs-lookup"><span data-stu-id="334a0-123">Form</span></span>

<span data-ttu-id="334a0-124">フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="334a0-124">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="334a0-125">適切なユーザー環境では、入力フィールドのラベルと論理グループを明確にすることが重要です。</span><span class="sxs-lookup"><span data-stu-id="334a0-125">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、フォーム UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-127">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-127">Top use cases</span></span>

* <span data-ttu-id="334a0-128">サインイン</span><span class="sxs-lookup"><span data-stu-id="334a0-128">Sign in</span></span>
* <span data-ttu-id="334a0-129">ユーザー プロファイル</span><span class="sxs-lookup"><span data-stu-id="334a0-129">User profiles</span></span>
* <span data-ttu-id="334a0-130">設定</span><span class="sxs-lookup"><span data-stu-id="334a0-130">Settings</span></span>
* <span data-ttu-id="334a0-131">ユーザー入力のコレクション</span><span class="sxs-lookup"><span data-stu-id="334a0-131">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="334a0-132">サインイン</span><span class="sxs-lookup"><span data-stu-id="334a0-132">Sign in</span></span>

<span data-ttu-id="334a0-133">さまざまなチームコンテキストと id プロバイダーに対してアプリのサインインフローを設計できます。</span><span class="sxs-lookup"><span data-stu-id="334a0-133">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="334a0-134">次の例には、シングルサインオン (SSO) が含まれています。これは、最も簡単な認証手順にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="334a0-134">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、サインイン UI テンプレートを示しています。" border="false":::

### <a name="top-use-case"></a><span data-ttu-id="334a0-136">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-136">Top use case</span></span>

* <span data-ttu-id="334a0-137">ユーザーを認証する</span><span class="sxs-lookup"><span data-stu-id="334a0-137">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="334a0-138">タスクボード</span><span class="sxs-lookup"><span data-stu-id="334a0-138">Task board</span></span>

<span data-ttu-id="334a0-139">タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="334a0-139">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="334a0-140">また、任意の種類のコンテンツをカテゴリ別に並べ替えるために使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="334a0-140">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="334a0-141">列間でカードを編集し、移動することができます。</span><span class="sxs-lookup"><span data-stu-id="334a0-141">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、タスクボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-143">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-143">Top use cases</span></span>

* <span data-ttu-id="334a0-144">プロジェクトの管理。</span><span class="sxs-lookup"><span data-stu-id="334a0-144">Project management.</span></span> <span data-ttu-id="334a0-145">タスクの割り当てと進捗状況の追跡</span><span class="sxs-lookup"><span data-stu-id="334a0-145">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="334a0-146">ブレイン.</span><span class="sxs-lookup"><span data-stu-id="334a0-146">Brainstorming.</span></span> <span data-ttu-id="334a0-147">さまざまなカテゴリにアイデアを追加する</span><span class="sxs-lookup"><span data-stu-id="334a0-147">Adding ideas in different categories</span></span>
* <span data-ttu-id="334a0-148">演習の並べ替え。</span><span class="sxs-lookup"><span data-stu-id="334a0-148">Sorting exercises.</span></span> <span data-ttu-id="334a0-149">任意の種類の情報をバケットに編成する</span><span class="sxs-lookup"><span data-stu-id="334a0-149">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="334a0-150">データ可視化</span><span class="sxs-lookup"><span data-stu-id="334a0-150">Data visualization</span></span>

<span data-ttu-id="334a0-151">1つのページでデータの視覚エフェクトを積み重ねて整理するには、異なるカードサイズ (単一、2、完全) を使用できます。</span><span class="sxs-lookup"><span data-stu-id="334a0-151">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="334a0-152">カードは、列のレイアウトに合わせて拡大または縮小されます。</span><span class="sxs-lookup"><span data-stu-id="334a0-152">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、データビジュアライゼーション UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-154">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-154">Top use cases</span></span>

* <span data-ttu-id="334a0-155">複雑な情報を表示する</span><span class="sxs-lookup"><span data-stu-id="334a0-155">Display complex information</span></span>
* <span data-ttu-id="334a0-156">ダッシュボードを作成する</span><span class="sxs-lookup"><span data-stu-id="334a0-156">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="334a0-157">ウィザード</span><span class="sxs-lookup"><span data-stu-id="334a0-157">Wizard</span></span>

<span data-ttu-id="334a0-158">ウィザードを使用すると、1つのタスクを完了するためにユーザーが複数の画面を移動できます (セットアッププロセスなど)。</span><span class="sxs-lookup"><span data-stu-id="334a0-158">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例は、ウィザードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-160">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-160">Top use cases</span></span>

* <span data-ttu-id="334a0-161">セットアップ</span><span class="sxs-lookup"><span data-stu-id="334a0-161">Setup</span></span>
* <span data-ttu-id="334a0-162">オンボード</span><span class="sxs-lookup"><span data-stu-id="334a0-162">Onboarding</span></span>
* <span data-ttu-id="334a0-163">初回実行時のエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="334a0-163">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="334a0-164">空の状態</span><span class="sxs-lookup"><span data-stu-id="334a0-164">Empty state</span></span>

<span data-ttu-id="334a0-165">空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="334a0-165">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="334a0-166">次の設計では、1つまたはいくつかのコンポーネントを使用するように柔軟に適応できます。</span><span class="sxs-lookup"><span data-stu-id="334a0-166">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、ウィザードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-168">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-168">Top use cases</span></span>

* <span data-ttu-id="334a0-169">サインイン</span><span class="sxs-lookup"><span data-stu-id="334a0-169">Sign in</span></span>
* <span data-ttu-id="334a0-170">ウェルカムメッセージと初回実行時のエクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="334a0-170">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="334a0-171">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="334a0-171">Success messages</span></span>
* <span data-ttu-id="334a0-172">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="334a0-172">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="334a0-173">通知バー</span><span class="sxs-lookup"><span data-stu-id="334a0-173">Notification bar</span></span>

<span data-ttu-id="334a0-174">通知バーは、ユーザーがすぐにアクションを実行しなくてもよい、簡単な重要なメッセージを表示するための専用の領域です。</span><span class="sxs-lookup"><span data-stu-id="334a0-174">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="334a0-175">特定の種類のメッセージ (下の図を参照) には、特定の背景色とアイコンが関連付けられています。</span><span class="sxs-lookup"><span data-stu-id="334a0-175">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、通知バーテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-177">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-177">Top use cases</span></span>

* <span data-ttu-id="334a0-178">重要なメッセージ、エラー、および警告</span><span class="sxs-lookup"><span data-stu-id="334a0-178">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="334a0-179">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="334a0-179">Success messages</span></span>
* <span data-ttu-id="334a0-180">情報メッセージまたはプロモーションメッセージ</span><span class="sxs-lookup"><span data-stu-id="334a0-180">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="334a0-181">左ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="334a0-181">Left nav</span></span>

<span data-ttu-id="334a0-182">左側のナビゲーションを使用して、Teams タブ内の複数のページを参照します。次の例では、左側のナビゲーションはチャネルリストとタブのコンテンツの間にあります。</span><span class="sxs-lookup"><span data-stu-id="334a0-182">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、左側のナビゲーションテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-184">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-184">Top use cases</span></span>

* <span data-ttu-id="334a0-185">[Teams] タブ内の複数のページを参照する</span><span class="sxs-lookup"><span data-stu-id="334a0-185">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="334a0-186">複雑なアプリを複数のページに分割する</span><span class="sxs-lookup"><span data-stu-id="334a0-186">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="334a0-187">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="334a0-187">Breadcrumb</span></span>

<span data-ttu-id="334a0-188">階層リンクは、アプリの階層を伝達するナビゲーション支援者です。</span><span class="sxs-lookup"><span data-stu-id="334a0-188">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="334a0-189">これにより、ユーザーが表示しているページが全体的な効果にどのように適合し、1回のクリックでその階層の上位レベルにアクセスできるかを理解することができます。</span><span class="sxs-lookup"><span data-stu-id="334a0-189">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、階層リンクテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-191">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-191">Top use cases</span></span>

* <span data-ttu-id="334a0-192">コミュニケーション階層</span><span class="sxs-lookup"><span data-stu-id="334a0-192">Communicate hierarchy</span></span>
* <span data-ttu-id="334a0-193">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="334a0-193">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="334a0-194">ツールバー</span><span class="sxs-lookup"><span data-stu-id="334a0-194">Toolbar</span></span>

<span data-ttu-id="334a0-195">ツールバーは、コントロールのセットをグループ化するためのコンテナーです。</span><span class="sxs-lookup"><span data-stu-id="334a0-195">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="例は、ツールバーテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-197">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-197">Top use cases</span></span>

* <span data-ttu-id="334a0-198">アプリコンテンツに対するコンテキストアクション</span><span class="sxs-lookup"><span data-stu-id="334a0-198">Contextual actions on app content</span></span>
* <span data-ttu-id="334a0-199">コンテキストフィルターと検索</span><span class="sxs-lookup"><span data-stu-id="334a0-199">Contextual filter and find</span></span>
* <span data-ttu-id="334a0-200">ナビゲーションとブレッドクラム</span><span class="sxs-lookup"><span data-stu-id="334a0-200">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="334a0-201">ステージ</span><span class="sxs-lookup"><span data-stu-id="334a0-201">Stage</span></span>

<span data-ttu-id="334a0-202">ステージを使用すると、ユーザーは、画像、ファイル、web サイトなどのエンティティを、別のアプリやブラウザーで開くのではなく、Teams で開くことができます。</span><span class="sxs-lookup"><span data-stu-id="334a0-202">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="334a0-203">ステージの主なユースケースが表示されています。複雑な対話には、サーフェスを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="334a0-203">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="334a0-204">(実装メモ: 大規模な [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用して、ステージを構築します。)</span><span class="sxs-lookup"><span data-stu-id="334a0-204">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="例は、ステージテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="334a0-206">主なユースケース</span><span class="sxs-lookup"><span data-stu-id="334a0-206">Top use cases</span></span>

* <span data-ttu-id="334a0-207">別のアプリまたはブラウザーではなく Teams でエンティティを開く</span><span class="sxs-lookup"><span data-stu-id="334a0-207">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="334a0-208">スポットライトメディアまたはその他のコンテンツ</span><span class="sxs-lookup"><span data-stu-id="334a0-208">Spotlight media or other content</span></span>

## <a name="microsoft-teams-ui-library-coming-soon"></a><span data-ttu-id="334a0-209">Microsoft Teams UI ライブラリ (近日公開予定)</span><span class="sxs-lookup"><span data-stu-id="334a0-209">Microsoft Teams UI Library (coming soon)</span></span>

<span data-ttu-id="334a0-210">Microsoft Teams UI ライブラリを使用すると、これらの運用可能な UI テンプレートをアプリプロジェクトに直接インポートすることができます。</span><span class="sxs-lookup"><span data-stu-id="334a0-210">The Microsoft Teams UI Library will allow you to import these production-ready UI templates directly into your app project.</span></span>
