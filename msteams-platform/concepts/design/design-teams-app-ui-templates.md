---
title: UI テンプレートを使用したアプリの設計
author: heath-hamilton
description: 標準化された UI コンポーネント、レイアウト、およびパターンを使用して、アプリを迅速に設計し、Microsoft Teams。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 0cd5c6c4525e340f9aa53a78749211783880225a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566020"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="61bfb-103">UI テンプレートをMicrosoft Teamsアプリを設計する</span><span class="sxs-lookup"><span data-stu-id="61bfb-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="61bfb-104">UI テンプレートを使用Microsoft Teamsアプリを迅速に設計します。</span><span class="sxs-lookup"><span data-stu-id="61bfb-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="61bfb-105">テンプレートは、一般的な Teams の使用例で動作する Fluent UI ベースのコンポーネントのコレクションで、ユーザーに最適なエクスペリエンスを把握する時間が広がっています。</span><span class="sxs-lookup"><span data-stu-id="61bfb-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="61bfb-106">ツールとサンプルの使用を開始する</span><span class="sxs-lookup"><span data-stu-id="61bfb-106">Getting started with tools and samples</span></span>

<span data-ttu-id="61bfb-107">次のリソースは、UI テンプレートを使用してアプリを設計および開発するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="61bfb-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="61bfb-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="61bfb-109">アプリ設計の UI テンプレートを Microsoft Teams UI キットから取得します。これには、使用状況、解剖学、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="61bfb-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61bfb-110">UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="61bfb-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="61bfb-111">Microsoft TeamsUI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="61bfb-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="61bfb-112">ブラウザーで UI テンプレートTeams関連するコンポーネントを個別に表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="61bfb-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61bfb-113">UI ライブラリ (プレイグラウンド) を試す</span><span class="sxs-lookup"><span data-stu-id="61bfb-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="61bfb-114">これらのテンプレートと関連コンポーネントをアプリ プロジェクトに直接Teamsインポートします。</span><span class="sxs-lookup"><span data-stu-id="61bfb-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61bfb-115">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="61bfb-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="61bfb-116">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="61bfb-116">Sample app</span></span>

<span data-ttu-id="61bfb-117">サンプル アプリをインストールして、UI テンプレートの外観と動作を各コンテキストTeamsします。</span><span class="sxs-lookup"><span data-stu-id="61bfb-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61bfb-118">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="61bfb-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="61bfb-119">List</span><span class="sxs-lookup"><span data-stu-id="61bfb-119">List</span></span>

<span data-ttu-id="61bfb-120">リストを使用して、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、リスト UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-122">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-122">Top use cases</span></span>

* <span data-ttu-id="61bfb-123">データの表示</span><span class="sxs-lookup"><span data-stu-id="61bfb-123">Display data</span></span>
* <span data-ttu-id="61bfb-124">アプリ コンテンツに関するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="61bfb-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="61bfb-125">ダッシュボード</span><span class="sxs-lookup"><span data-stu-id="61bfb-125">Dashboard</span></span>

<span data-ttu-id="61bfb-126">ダッシュボードには、さまざまな種類のコンテンツが中央の場所に表示されます (Teamsまたはタブ)。</span><span class="sxs-lookup"><span data-stu-id="61bfb-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="61bfb-127">ユーザーは、ダッシュボードに表示される機能の少なくとも一部をカスタマイズできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="61bfb-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例は、ダッシュボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-129">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-129">Top use cases</span></span>

* <span data-ttu-id="61bfb-130">データの分析</span><span class="sxs-lookup"><span data-stu-id="61bfb-130">Analyze data</span></span>
* <span data-ttu-id="61bfb-131">レポートの指標</span><span class="sxs-lookup"><span data-stu-id="61bfb-131">Report metrics</span></span>
* <span data-ttu-id="61bfb-132">異なる情報を 1 か所に整理する</span><span class="sxs-lookup"><span data-stu-id="61bfb-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="61bfb-133">フォーム</span><span class="sxs-lookup"><span data-stu-id="61bfb-133">Form</span></span>

<span data-ttu-id="61bfb-134">フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="61bfb-135">ユーザー エクスペリエンスを向上するには、入力フィールドの明確なラベル付けと論理グループ化が重要です。</span><span class="sxs-lookup"><span data-stu-id="61bfb-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、フォーム UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-137">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-137">Top use cases</span></span>

* <span data-ttu-id="61bfb-138">サインイン</span><span class="sxs-lookup"><span data-stu-id="61bfb-138">Sign in</span></span>
* <span data-ttu-id="61bfb-139">ユーザー プロファイル</span><span class="sxs-lookup"><span data-stu-id="61bfb-139">User profiles</span></span>
* <span data-ttu-id="61bfb-140">設定</span><span class="sxs-lookup"><span data-stu-id="61bfb-140">Settings</span></span>
* <span data-ttu-id="61bfb-141">ユーザー入力コレクション</span><span class="sxs-lookup"><span data-stu-id="61bfb-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="61bfb-142">サインイン</span><span class="sxs-lookup"><span data-stu-id="61bfb-142">Sign in</span></span>

<span data-ttu-id="61bfb-143">さまざまなコンテキストと ID プロバイダー用にアプリ Teamsフローを設計できます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="61bfb-144">次の例では、シングル サインオン (SSO) を含み、最も簡単な認証エクスペリエンスをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="61bfb-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、サインイン UI テンプレートを示しています。" border="false":::

### <a name="top-use-case"></a><span data-ttu-id="61bfb-146">トップ の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-146">Top use case</span></span>

* <span data-ttu-id="61bfb-147">ユーザーの認証</span><span class="sxs-lookup"><span data-stu-id="61bfb-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="61bfb-148">タスク ボード</span><span class="sxs-lookup"><span data-stu-id="61bfb-148">Task board</span></span>

<span data-ttu-id="61bfb-149">タスク ボード (カンバン ボードまたはスイム レーンとも呼ばれる) は、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="61bfb-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="61bfb-150">また、任意の種類のコンテンツをカテゴリに並べ替える場合にも使用できます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="61bfb-151">列間でカードを編集および移動できます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、タスク ボードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-153">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-153">Top use cases</span></span>

* <span data-ttu-id="61bfb-154">Project管理: タスクの割り当てと追跡の状態。</span><span class="sxs-lookup"><span data-stu-id="61bfb-154">Project management: Assigning tasks and tracking status.</span></span>
* <span data-ttu-id="61bfb-155">ブレインストーミング: さまざまなカテゴリにアイデアを追加する。</span><span class="sxs-lookup"><span data-stu-id="61bfb-155">Brainstorming: Adding ideas in different categories.</span></span>
* <span data-ttu-id="61bfb-156">並べ替えの演習: 任意の種類の情報をバケットに整理します。</span><span class="sxs-lookup"><span data-stu-id="61bfb-156">Sorting exercises: Organizing any kind of information into buckets.</span></span>

## <a name="data-visualization"></a><span data-ttu-id="61bfb-157">データ可視化</span><span class="sxs-lookup"><span data-stu-id="61bfb-157">Data visualization</span></span>

<span data-ttu-id="61bfb-158">異なるカード サイズ (シングル、ダブル、フル) を使用して、データの視覚化を同じページで積み重ね、整理できます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-158">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="61bfb-159">カードは、列のレイアウトに合わせて拡大縮小され、空白を入力します。</span><span class="sxs-lookup"><span data-stu-id="61bfb-159">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、データ可視化 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-161">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-161">Top use cases</span></span>

* <span data-ttu-id="61bfb-162">複雑な情報を表示する</span><span class="sxs-lookup"><span data-stu-id="61bfb-162">Display complex information</span></span>
* <span data-ttu-id="61bfb-163">ダッシュボードの作成</span><span class="sxs-lookup"><span data-stu-id="61bfb-163">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="61bfb-164">ウィザード</span><span class="sxs-lookup"><span data-stu-id="61bfb-164">Wizard</span></span>

<span data-ttu-id="61bfb-165">ウィザードは、ユーザーが複数の画面を介してタスク (セットアップ プロセスなど) を完了する方法を案内します。</span><span class="sxs-lookup"><span data-stu-id="61bfb-165">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例は、ウィザードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-167">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-167">Top use cases</span></span>

* <span data-ttu-id="61bfb-168">セットアップ</span><span class="sxs-lookup"><span data-stu-id="61bfb-168">Setup</span></span>
* <span data-ttu-id="61bfb-169">オンボード</span><span class="sxs-lookup"><span data-stu-id="61bfb-169">Onboarding</span></span>
* <span data-ttu-id="61bfb-170">初回実行エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="61bfb-170">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="61bfb-171">空の状態</span><span class="sxs-lookup"><span data-stu-id="61bfb-171">Empty state</span></span>

<span data-ttu-id="61bfb-172">空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-172">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="61bfb-173">柔軟性が高く、次の設計で 1 つ、少数、またはすべてのコンポーネントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-173">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、空の状態 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-175">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-175">Top use cases</span></span>

* <span data-ttu-id="61bfb-176">サインイン</span><span class="sxs-lookup"><span data-stu-id="61bfb-176">Sign in</span></span>
* <span data-ttu-id="61bfb-177">ウェルカム メッセージと初回実行エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="61bfb-177">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="61bfb-178">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="61bfb-178">Success messages</span></span>
* <span data-ttu-id="61bfb-179">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="61bfb-179">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="61bfb-180">通知バー</span><span class="sxs-lookup"><span data-stu-id="61bfb-180">Notification bar</span></span>

<span data-ttu-id="61bfb-181">通知バーは、ユーザーが即座にアクションを実行する必要が生じない、簡潔で重要なメッセージを表示するための専用の領域です。</span><span class="sxs-lookup"><span data-stu-id="61bfb-181">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="61bfb-182">特定の背景色とアイコンは、特定の種類のメッセージに関連付けられる (以下を参照)。</span><span class="sxs-lookup"><span data-stu-id="61bfb-182">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、通知バー テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-184">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-184">Top use cases</span></span>

* <span data-ttu-id="61bfb-185">重大なメッセージ、エラー、および警告</span><span class="sxs-lookup"><span data-stu-id="61bfb-185">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="61bfb-186">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="61bfb-186">Success messages</span></span>
* <span data-ttu-id="61bfb-187">情報メッセージまたはプロモーション メッセージ</span><span class="sxs-lookup"><span data-stu-id="61bfb-187">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="61bfb-188">左ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="61bfb-188">Left nav</span></span>

<span data-ttu-id="61bfb-189">左側のナビゲーションを使用して、[ページ] タブ内の複数Teamsします。次の例では、左側のナビゲーションはチャネル リストとタブ コンテンツの間にあります。</span><span class="sxs-lookup"><span data-stu-id="61bfb-189">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、左側のナビゲーション テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-191">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-191">Top use cases</span></span>

* <span data-ttu-id="61bfb-192">[ページ] タブ内の複数Teams参照します。</span><span class="sxs-lookup"><span data-stu-id="61bfb-192">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="61bfb-193">複雑なアプリを複数のページに分割します。</span><span class="sxs-lookup"><span data-stu-id="61bfb-193">Break down complex apps into multiple pages.</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="61bfb-194">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="61bfb-194">Breadcrumb</span></span>

<span data-ttu-id="61bfb-195">Breadcrumbs は、アプリの階層を伝えるナビゲーション支援です。</span><span class="sxs-lookup"><span data-stu-id="61bfb-195">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="61bfb-196">ユーザーは、表示しているページが全体的なエクスペリエンスに適合する方法を理解し、その階層内の上位レベルへの 1 回のクリックアクセスを許可するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-196">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、パンくずテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-198">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-198">Top use cases</span></span>

* <span data-ttu-id="61bfb-199">コミュニケーション階層</span><span class="sxs-lookup"><span data-stu-id="61bfb-199">Communicate hierarchy</span></span>
* <span data-ttu-id="61bfb-200">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="61bfb-200">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="61bfb-201">ツール バー</span><span class="sxs-lookup"><span data-stu-id="61bfb-201">Toolbar</span></span>

<span data-ttu-id="61bfb-202">ツールバーは、コントロールのセットをグループ化するコンテナーです。</span><span class="sxs-lookup"><span data-stu-id="61bfb-202">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="ツール バー テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-204">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-204">Top use cases</span></span>

* <span data-ttu-id="61bfb-205">アプリ コンテンツに関するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="61bfb-205">Contextual actions on app content</span></span>
* <span data-ttu-id="61bfb-206">コンテキスト フィルターと検索</span><span class="sxs-lookup"><span data-stu-id="61bfb-206">Contextual filter and find</span></span>
* <span data-ttu-id="61bfb-207">ナビゲーションとパンくず</span><span class="sxs-lookup"><span data-stu-id="61bfb-207">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="61bfb-208">ステージ</span><span class="sxs-lookup"><span data-stu-id="61bfb-208">Stage</span></span>

<span data-ttu-id="61bfb-209">Stage は、ユーザーが別のアプリやブラウザーでエンティティを開く代わりに、Teams、ファイル、web サイトなど、エンティティを開く方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="61bfb-209">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="61bfb-210">ステージの主な使用例は表示です。サーフェスを複雑な操作に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="61bfb-210">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="61bfb-211">(実装ノート: 大規模なタスク モジュールを使用してステージ [をビルド](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)します。)</span><span class="sxs-lookup"><span data-stu-id="61bfb-211">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="ステージ テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="61bfb-213">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="61bfb-213">Top use cases</span></span>

* <span data-ttu-id="61bfb-214">別のアプリまたはブラウザーではなくTeamsエンティティを開きます。</span><span class="sxs-lookup"><span data-stu-id="61bfb-214">Open an entity in Teams instead of another app or browser.</span></span>
* <span data-ttu-id="61bfb-215">スポットライト メディアまたは他のコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="61bfb-215">Spotlight media or other content.</span></span>
