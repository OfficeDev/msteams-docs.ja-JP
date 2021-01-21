---
title: UI テンプレートを使ったアプリの設計
author: heath-hamilton
description: Microsoft Teams で一般的に見られる標準化された UI コンポーネント、レイアウト、パターンを使用して、アプリをより迅速に設計します。
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: b4d244bbf78ac85042d5caf8ec84afe42e79b3c7
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911927"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="dd981-103">UI テンプレートを使用した Microsoft Teams アプリの設計</span><span class="sxs-lookup"><span data-stu-id="dd981-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="dd981-104">UI テンプレートを使用して、Microsoft Teams アプリをより迅速に設計します。</span><span class="sxs-lookup"><span data-stu-id="dd981-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="dd981-105">テンプレートは、一般的な Teams の使用事例全体で機能する Fluent UI ベースのコンポーネントのコレクションです。ユーザーに最適なエクスペリエンスを見つめる時間が広がっています。</span><span class="sxs-lookup"><span data-stu-id="dd981-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="dd981-106">ツールとサンプルの使用を開始する</span><span class="sxs-lookup"><span data-stu-id="dd981-106">Getting started with tools and samples</span></span>

<span data-ttu-id="dd981-107">次のリソースは、UI テンプレートを使ったアプリの設計と開発に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="dd981-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="dd981-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="dd981-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="dd981-109">Microsoft Teams UI Kit からアプリ設計用の UI テンプレートを取得します。これには、使用状況、構造、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="dd981-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd981-110">UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="dd981-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="dd981-111">Microsoft Teams UI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="dd981-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="dd981-112">ブラウザーで個々の Teams UI テンプレートと関連コンポーネントを表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="dd981-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd981-113">UI ライブラリ (プレイグラウンド) を試す</span><span class="sxs-lookup"><span data-stu-id="dd981-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="dd981-114">これらのテンプレートと関連コンポーネントを Teams アプリ プロジェクトに直接インポートします。</span><span class="sxs-lookup"><span data-stu-id="dd981-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd981-115">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="dd981-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="dd981-116">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="dd981-116">Sample app</span></span>

<span data-ttu-id="dd981-117">サンプル アプリをインストールして、Teams コンテキスト内での UI テンプレートの外観と動作を確認します。</span><span class="sxs-lookup"><span data-stu-id="dd981-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd981-118">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="dd981-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="dd981-119">リスト</span><span class="sxs-lookup"><span data-stu-id="dd981-119">List</span></span>

<span data-ttu-id="dd981-120">リストを使用して、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="dd981-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="リスト UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-122">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-122">Top use cases</span></span>

* <span data-ttu-id="dd981-123">データの表示</span><span class="sxs-lookup"><span data-stu-id="dd981-123">Display data</span></span>
* <span data-ttu-id="dd981-124">アプリ コンテンツに対するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="dd981-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="dd981-125">ダッシュボード</span><span class="sxs-lookup"><span data-stu-id="dd981-125">Dashboard</span></span>

<span data-ttu-id="dd981-126">ダッシュボードは、さまざまな種類のコンテンツを中央の場所 (Teams 個人用アプリまたはタブ) に表示します。</span><span class="sxs-lookup"><span data-stu-id="dd981-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="dd981-127">ユーザーは、ダッシュボードに表示される機能の少なくとも一部をカスタマイズできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd981-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="ダッシュボード UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-129">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-129">Top use cases</span></span>

* <span data-ttu-id="dd981-130">データを分析する</span><span class="sxs-lookup"><span data-stu-id="dd981-130">Analyze data</span></span>
* <span data-ttu-id="dd981-131">レポートの指標</span><span class="sxs-lookup"><span data-stu-id="dd981-131">Report metrics</span></span>
* <span data-ttu-id="dd981-132">異なる情報を 1 か所に整理する</span><span class="sxs-lookup"><span data-stu-id="dd981-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="dd981-133">フォーム</span><span class="sxs-lookup"><span data-stu-id="dd981-133">Form</span></span>

<span data-ttu-id="dd981-134">フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd981-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="dd981-135">ユーザー エクスペリエンスを向上するには、入力フィールドの明確なラベル付けと論理グループが重要です。</span><span class="sxs-lookup"><span data-stu-id="dd981-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="フォーム UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-137">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-137">Top use cases</span></span>

* <span data-ttu-id="dd981-138">サインイン</span><span class="sxs-lookup"><span data-stu-id="dd981-138">Sign in</span></span>
* <span data-ttu-id="dd981-139">ユーザー プロファイル</span><span class="sxs-lookup"><span data-stu-id="dd981-139">User profiles</span></span>
* <span data-ttu-id="dd981-140">設定</span><span class="sxs-lookup"><span data-stu-id="dd981-140">Settings</span></span>
* <span data-ttu-id="dd981-141">ユーザー入力のコレクション</span><span class="sxs-lookup"><span data-stu-id="dd981-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="dd981-142">サインイン</span><span class="sxs-lookup"><span data-stu-id="dd981-142">Sign in</span></span>

<span data-ttu-id="dd981-143">さまざまな Teams コンテキストと ID プロバイダーに対してアプリのサインイン フローを設計できます。</span><span class="sxs-lookup"><span data-stu-id="dd981-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="dd981-144">次の例にはシングル サインオン (SSO) が含まれています。これは、最も簡単な認証エクスペリエンスに推奨されます。</span><span class="sxs-lookup"><span data-stu-id="dd981-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、サインイン UI テンプレートを示しています。" border="false":::

### <a name="top-use-case"></a><span data-ttu-id="dd981-146">一番上の使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-146">Top use case</span></span>

* <span data-ttu-id="dd981-147">ユーザーを認証する</span><span class="sxs-lookup"><span data-stu-id="dd981-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="dd981-148">タスク ボード</span><span class="sxs-lookup"><span data-stu-id="dd981-148">Task board</span></span>

<span data-ttu-id="dd981-149">タスク ボード (カンバボードまたはスレーンとも呼ばれる) は、作業項目やチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="dd981-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="dd981-150">また、任意の種類のコンテンツをカテゴリに並べ替える場合にも使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd981-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="dd981-151">列間でカードの編集と移動を行います。</span><span class="sxs-lookup"><span data-stu-id="dd981-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="タスク ボード UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-153">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-153">Top use cases</span></span>

* <span data-ttu-id="dd981-154">プロジェクトの管理。</span><span class="sxs-lookup"><span data-stu-id="dd981-154">Project management.</span></span> <span data-ttu-id="dd981-155">タスクの割り当てと状態の追跡</span><span class="sxs-lookup"><span data-stu-id="dd981-155">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="dd981-156">ブレーンストーミング。</span><span class="sxs-lookup"><span data-stu-id="dd981-156">Brainstorming.</span></span> <span data-ttu-id="dd981-157">さまざまなカテゴリにアイデアを追加する</span><span class="sxs-lookup"><span data-stu-id="dd981-157">Adding ideas in different categories</span></span>
* <span data-ttu-id="dd981-158">並べ替えの演習。</span><span class="sxs-lookup"><span data-stu-id="dd981-158">Sorting exercises.</span></span> <span data-ttu-id="dd981-159">任意の種類の情報をバケットに整理する</span><span class="sxs-lookup"><span data-stu-id="dd981-159">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="dd981-160">データ可視化</span><span class="sxs-lookup"><span data-stu-id="dd981-160">Data visualization</span></span>

<span data-ttu-id="dd981-161">異なるカード サイズ (単一、倍数、および完全) を使用して、データの視覚化を同じページに重ね合わせて整理できます。</span><span class="sxs-lookup"><span data-stu-id="dd981-161">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="dd981-162">カードは列レイアウトに合わせて拡大縮小され、空白スペースで埋めることができます。</span><span class="sxs-lookup"><span data-stu-id="dd981-162">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="データ可視化 UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-164">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-164">Top use cases</span></span>

* <span data-ttu-id="dd981-165">複雑な情報を表示する</span><span class="sxs-lookup"><span data-stu-id="dd981-165">Display complex information</span></span>
* <span data-ttu-id="dd981-166">ダッシュボードを作成する</span><span class="sxs-lookup"><span data-stu-id="dd981-166">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="dd981-167">ウィザード</span><span class="sxs-lookup"><span data-stu-id="dd981-167">Wizard</span></span>

<span data-ttu-id="dd981-168">ウィザードを使用すると、ユーザーは複数の画面を介してタスク (セットアップ プロセスなど) を完了できます。</span><span class="sxs-lookup"><span data-stu-id="dd981-168">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="ウィザード UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-170">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-170">Top use cases</span></span>

* <span data-ttu-id="dd981-171">セットアップ</span><span class="sxs-lookup"><span data-stu-id="dd981-171">Setup</span></span>
* <span data-ttu-id="dd981-172">オンボード</span><span class="sxs-lookup"><span data-stu-id="dd981-172">Onboarding</span></span>
* <span data-ttu-id="dd981-173">初回実行時エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="dd981-173">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="dd981-174">空の状態</span><span class="sxs-lookup"><span data-stu-id="dd981-174">Empty state</span></span>

<span data-ttu-id="dd981-175">空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd981-175">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="dd981-176">柔軟性が高く、次の設計で 1 つのコンポーネント、少数のコンポーネント、またはすべてのコンポーネントを使用するために適応できます。</span><span class="sxs-lookup"><span data-stu-id="dd981-176">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="空の状態 UI テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-178">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-178">Top use cases</span></span>

* <span data-ttu-id="dd981-179">サインイン</span><span class="sxs-lookup"><span data-stu-id="dd981-179">Sign in</span></span>
* <span data-ttu-id="dd981-180">ウェルカム メッセージと最初の実行エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="dd981-180">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="dd981-181">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="dd981-181">Success messages</span></span>
* <span data-ttu-id="dd981-182">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="dd981-182">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="dd981-183">通知バー</span><span class="sxs-lookup"><span data-stu-id="dd981-183">Notification bar</span></span>

<span data-ttu-id="dd981-184">通知バーは、ユーザーがすぐにアクションを実行する必要が生じない、簡潔で重要なメッセージを表示するための専用領域です。</span><span class="sxs-lookup"><span data-stu-id="dd981-184">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="dd981-185">特定の背景色とアイコンは、特定の種類のメッセージに関連付けます (下記を参照)。</span><span class="sxs-lookup"><span data-stu-id="dd981-185">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="通知バー テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-187">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-187">Top use cases</span></span>

* <span data-ttu-id="dd981-188">重大なメッセージ、エラー、および警告</span><span class="sxs-lookup"><span data-stu-id="dd981-188">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="dd981-189">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="dd981-189">Success messages</span></span>
* <span data-ttu-id="dd981-190">情報メッセージまたはプロモーション メッセージ</span><span class="sxs-lookup"><span data-stu-id="dd981-190">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="dd981-191">左ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="dd981-191">Left nav</span></span>

<span data-ttu-id="dd981-192">左側のナビゲーションを使用して、Teams タブ内の複数のページを参照します。次の例では、左側のナビゲーションはチャネルリストとタブ コンテンツの間にあります。</span><span class="sxs-lookup"><span data-stu-id="dd981-192">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="左側のナビゲーション テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-194">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-194">Top use cases</span></span>

* <span data-ttu-id="dd981-195">Teams タブ内の複数のページを参照する</span><span class="sxs-lookup"><span data-stu-id="dd981-195">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="dd981-196">複雑なアプリを複数のページに分割する</span><span class="sxs-lookup"><span data-stu-id="dd981-196">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="dd981-197">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="dd981-197">Breadcrumb</span></span>

<span data-ttu-id="dd981-198">階層リンクは、アプリの階層を伝えるナビゲーションの補助です。</span><span class="sxs-lookup"><span data-stu-id="dd981-198">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="dd981-199">ユーザーは、表示しているページが全体的なエクスペリエンスに適合する方法を理解し、その階層内の上位レベルに 1 回のクリックでアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="dd981-199">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、階層リンク テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-201">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-201">Top use cases</span></span>

* <span data-ttu-id="dd981-202">通信階層</span><span class="sxs-lookup"><span data-stu-id="dd981-202">Communicate hierarchy</span></span>
* <span data-ttu-id="dd981-203">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="dd981-203">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="dd981-204">ツールバー</span><span class="sxs-lookup"><span data-stu-id="dd981-204">Toolbar</span></span>

<span data-ttu-id="dd981-205">ツールバーは、コントロールのセットをグループ化するコンテナーです。</span><span class="sxs-lookup"><span data-stu-id="dd981-205">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="ツール バー テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-207">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-207">Top use cases</span></span>

* <span data-ttu-id="dd981-208">アプリ コンテンツに対するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="dd981-208">Contextual actions on app content</span></span>
* <span data-ttu-id="dd981-209">コンテキスト フィルターと検索</span><span class="sxs-lookup"><span data-stu-id="dd981-209">Contextual filter and find</span></span>
* <span data-ttu-id="dd981-210">ナビゲーションと階層リンク</span><span class="sxs-lookup"><span data-stu-id="dd981-210">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="dd981-211">ステージ</span><span class="sxs-lookup"><span data-stu-id="dd981-211">Stage</span></span>

<span data-ttu-id="dd981-212">ステージは、ユーザーが別のアプリやブラウザーでエンティティを開くのではなく、Teams で (画像、ファイル、Web サイトなど) エンティティを開く方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="dd981-212">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="dd981-213">ステージの主な使用例は表示中です。サーフェスは複雑な対話操作には使用できません。</span><span class="sxs-lookup"><span data-stu-id="dd981-213">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="dd981-214">(実装メモ: 大規模なタスク モジュールを使用してステージ [をビルドします](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="dd981-214">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="ステージ テンプレートの例を示します。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="dd981-216">主な使用事例</span><span class="sxs-lookup"><span data-stu-id="dd981-216">Top use cases</span></span>

* <span data-ttu-id="dd981-217">別のアプリまたはブラウザーではなく、Teams でエンティティを開く</span><span class="sxs-lookup"><span data-stu-id="dd981-217">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="dd981-218">スポットライト メディアまたは他のコンテンツ</span><span class="sxs-lookup"><span data-stu-id="dd981-218">Spotlight media or other content</span></span>
