---
title: UI テンプレートを使用したアプリの設計
author: heath-hamilton
description: Microsoft Teamsで一般的に見られる標準化された UI コンポーネント、レイアウト、パターンを使用して、アプリをより迅速に設計します。
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
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="6900a-103">UI テンプレートを使用したMicrosoft Teams アプリの設計</span><span class="sxs-lookup"><span data-stu-id="6900a-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="6900a-104">UI テンプレートを使用して、Microsoft Teams アプリをより迅速に設計します。</span><span class="sxs-lookup"><span data-stu-id="6900a-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="6900a-105">テンプレートは、一般的なTeamsのユースケースで動作する Fluent UI ベースのコンポーネントのコレクションであり、ユーザーにとって最適なエクスペリエンスを把握する時間が増えます。</span><span class="sxs-lookup"><span data-stu-id="6900a-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="6900a-106">ツールとサンプルの概要</span><span class="sxs-lookup"><span data-stu-id="6900a-106">Getting started with tools and samples</span></span>

<span data-ttu-id="6900a-107">次のリソースは、UI テンプレートを使用してアプリを設計および開発するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="6900a-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="6900a-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="6900a-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="6900a-109">アプリデザイン用の UI テンプレートをMicrosoft Teams UI Kit から取得し、使用状況、解剖学、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="6900a-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6900a-110">UIキットを入手する(Figma)</span><span class="sxs-lookup"><span data-stu-id="6900a-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="6900a-111">Microsoft TeamsUI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="6900a-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="6900a-112">ブラウザーで個々のTeams UI テンプレートおよび関連コンポーネントを表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="6900a-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6900a-113">UIライブラリ(プレイグラウンド)を試してみてください</span><span class="sxs-lookup"><span data-stu-id="6900a-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="6900a-114">これらのテンプレートと関連コンポーネントをTeams アプリ プロジェクトに直接インポートします。</span><span class="sxs-lookup"><span data-stu-id="6900a-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6900a-115">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="6900a-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="6900a-116">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="6900a-116">Sample app</span></span>

<span data-ttu-id="6900a-117">サンプル アプリをインストールして、UI テンプレートの外観と動作をTeamsコンテキストで確認します。</span><span class="sxs-lookup"><span data-stu-id="6900a-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6900a-118">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="6900a-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="6900a-119">List</span><span class="sxs-lookup"><span data-stu-id="6900a-119">List</span></span>

<span data-ttu-id="6900a-120">リストを使用して、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="6900a-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、リスト UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-122">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-122">Top use cases</span></span>

* <span data-ttu-id="6900a-123">データの表示</span><span class="sxs-lookup"><span data-stu-id="6900a-123">Display data</span></span>
* <span data-ttu-id="6900a-124">アプリ コンテンツに対するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="6900a-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="6900a-125">ダッシュボード</span><span class="sxs-lookup"><span data-stu-id="6900a-125">Dashboard</span></span>

<span data-ttu-id="6900a-126">ダッシュボードには、さまざまな種類のコンテンツが一元的な場所 (個人用アプリまたはタブTeams) に表示されます。</span><span class="sxs-lookup"><span data-stu-id="6900a-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="6900a-127">ユーザーは、ダッシュボードに表示される内容の少なくとも一部をカスタマイズできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="6900a-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例は、ダッシュボード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-129">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-129">Top use cases</span></span>

* <span data-ttu-id="6900a-130">データの分析</span><span class="sxs-lookup"><span data-stu-id="6900a-130">Analyze data</span></span>
* <span data-ttu-id="6900a-131">レポートの指標</span><span class="sxs-lookup"><span data-stu-id="6900a-131">Report metrics</span></span>
* <span data-ttu-id="6900a-132">異なる情報を 1 か所にまとめる</span><span class="sxs-lookup"><span data-stu-id="6900a-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="6900a-133">フォーム</span><span class="sxs-lookup"><span data-stu-id="6900a-133">Form</span></span>

<span data-ttu-id="6900a-134">フォームは、構造化された方法でユーザー入力を収集、検証、および送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="6900a-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="6900a-135">入力フィールドの明確なラベル付けと論理グループ化は、優れたユーザー エクスペリエンスにとって重要です。</span><span class="sxs-lookup"><span data-stu-id="6900a-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、フォーム UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-137">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-137">Top use cases</span></span>

* <span data-ttu-id="6900a-138">サインイン</span><span class="sxs-lookup"><span data-stu-id="6900a-138">Sign in</span></span>
* <span data-ttu-id="6900a-139">ユーザー プロファイル</span><span class="sxs-lookup"><span data-stu-id="6900a-139">User profiles</span></span>
* <span data-ttu-id="6900a-140">設定</span><span class="sxs-lookup"><span data-stu-id="6900a-140">Settings</span></span>
* <span data-ttu-id="6900a-141">ユーザー入力コレクション</span><span class="sxs-lookup"><span data-stu-id="6900a-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="6900a-142">サインイン</span><span class="sxs-lookup"><span data-stu-id="6900a-142">Sign in</span></span>

<span data-ttu-id="6900a-143">さまざまなTeams コンテキストと ID プロバイダーに対して、アプリのサインイン フローを設計できます。</span><span class="sxs-lookup"><span data-stu-id="6900a-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="6900a-144">次の例には、シングル サインオン (SSO) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6900a-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、UI テンプレートのサインを示しています。" border="false":::

### <a name="top-use-case"></a><span data-ttu-id="6900a-146">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-146">Top use case</span></span>

* <span data-ttu-id="6900a-147">ユーザーの認証</span><span class="sxs-lookup"><span data-stu-id="6900a-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="6900a-148">タスクボード</span><span class="sxs-lookup"><span data-stu-id="6900a-148">Task board</span></span>

<span data-ttu-id="6900a-149">タスク ボードは、かんばんボードまたはスイム レーンとも呼ばれ、作業項目やチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="6900a-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="6900a-150">また、任意の種類のコンテンツをカテゴリに並べ替えるためにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="6900a-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="6900a-151">列間でカードを編集したり移動したりできます。</span><span class="sxs-lookup"><span data-stu-id="6900a-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、タスク ボードの UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-153">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-153">Top use cases</span></span>

* <span data-ttu-id="6900a-154">Project管理: タスクの割り当てとステータスの追跡。</span><span class="sxs-lookup"><span data-stu-id="6900a-154">Project management: Assigning tasks and tracking status.</span></span>
* <span data-ttu-id="6900a-155">ブレーンストーミング: さまざまなカテゴリにアイデアを追加します。</span><span class="sxs-lookup"><span data-stu-id="6900a-155">Brainstorming: Adding ideas in different categories.</span></span>
* <span data-ttu-id="6900a-156">分類の練習: あらゆる種類の情報をバケットにまとめる。</span><span class="sxs-lookup"><span data-stu-id="6900a-156">Sorting exercises: Organizing any kind of information into buckets.</span></span>

## <a name="data-visualization"></a><span data-ttu-id="6900a-157">データ可視化</span><span class="sxs-lookup"><span data-stu-id="6900a-157">Data visualization</span></span>

<span data-ttu-id="6900a-158">異なるカード サイズ (シングル、ダブル、フル) を使用して、同じページ上のデータビジュアライゼーションをスタックして整理できます。</span><span class="sxs-lookup"><span data-stu-id="6900a-158">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="6900a-159">カードは列レイアウトに合わせて拡大縮小され、空白スペースに塗りつぶされます。</span><span class="sxs-lookup"><span data-stu-id="6900a-159">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、データ視覚化 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-161">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-161">Top use cases</span></span>

* <span data-ttu-id="6900a-162">複雑な情報を表示する</span><span class="sxs-lookup"><span data-stu-id="6900a-162">Display complex information</span></span>
* <span data-ttu-id="6900a-163">ダッシュボードの作成</span><span class="sxs-lookup"><span data-stu-id="6900a-163">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="6900a-164">ウィザード</span><span class="sxs-lookup"><span data-stu-id="6900a-164">Wizard</span></span>

<span data-ttu-id="6900a-165">ウィザードは、ユーザーに対して、複数の画面をガイドして、1 つのタスク (セットアッププロセスなど) を完了します。</span><span class="sxs-lookup"><span data-stu-id="6900a-165">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例は、ウィザード UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-167">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-167">Top use cases</span></span>

* <span data-ttu-id="6900a-168">セットアップ</span><span class="sxs-lookup"><span data-stu-id="6900a-168">Setup</span></span>
* <span data-ttu-id="6900a-169">オンボード</span><span class="sxs-lookup"><span data-stu-id="6900a-169">Onboarding</span></span>
* <span data-ttu-id="6900a-170">最初の実行エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="6900a-170">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="6900a-171">空の状態</span><span class="sxs-lookup"><span data-stu-id="6900a-171">Empty state</span></span>

<span data-ttu-id="6900a-172">空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="6900a-172">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="6900a-173">柔軟性が高く、次の設計の 1 つ、数個、またはすべてのコンポーネントを使用するように適応します。</span><span class="sxs-lookup"><span data-stu-id="6900a-173">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、空の状態 UI テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-175">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-175">Top use cases</span></span>

* <span data-ttu-id="6900a-176">サインイン</span><span class="sxs-lookup"><span data-stu-id="6900a-176">Sign in</span></span>
* <span data-ttu-id="6900a-177">ウェルカム メッセージと初回実行エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="6900a-177">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="6900a-178">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="6900a-178">Success messages</span></span>
* <span data-ttu-id="6900a-179">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="6900a-179">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="6900a-180">通知バー</span><span class="sxs-lookup"><span data-stu-id="6900a-180">Notification bar</span></span>

<span data-ttu-id="6900a-181">通知バーは、ユーザーが直ちに操作を行う必要がない、簡潔で重要なメッセージを表示するための専用領域です。</span><span class="sxs-lookup"><span data-stu-id="6900a-181">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="6900a-182">特定の背景色とアイコンは、特定の種類のメッセージに関連付けられます(下記参照)。</span><span class="sxs-lookup"><span data-stu-id="6900a-182">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="例は、通知バー テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-184">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-184">Top use cases</span></span>

* <span data-ttu-id="6900a-185">重大なメッセージ、エラー、および警告</span><span class="sxs-lookup"><span data-stu-id="6900a-185">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="6900a-186">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="6900a-186">Success messages</span></span>
* <span data-ttu-id="6900a-187">情報メッセージまたはプロモーション メッセージ</span><span class="sxs-lookup"><span data-stu-id="6900a-187">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="6900a-188">左ナビ</span><span class="sxs-lookup"><span data-stu-id="6900a-188">Left nav</span></span>

<span data-ttu-id="6900a-189">左側のナビゲーションを使用して、Teamsタブ内の複数のページを参照します。次の例では、左側のナビゲーションはチャネル リストとタブ コンテンツの間にあります。</span><span class="sxs-lookup"><span data-stu-id="6900a-189">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="例は、左のナビゲーション テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-191">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-191">Top use cases</span></span>

* <span data-ttu-id="6900a-192">Teamsタブ内の複数のページを参照します。</span><span class="sxs-lookup"><span data-stu-id="6900a-192">Browse multiple pages within a Teams tab.</span></span>
* <span data-ttu-id="6900a-193">複雑なアプリを複数のページに分割します。</span><span class="sxs-lookup"><span data-stu-id="6900a-193">Break down complex apps into multiple pages.</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="6900a-194">Breadcrumb</span><span class="sxs-lookup"><span data-stu-id="6900a-194">Breadcrumb</span></span>

<span data-ttu-id="6900a-195">階層リンクは、アプリの階層を伝えるナビゲーション補助です。</span><span class="sxs-lookup"><span data-stu-id="6900a-195">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="6900a-196">ユーザーは、表示しているページが全体的なエクスペリエンスにどのように適合するかを理解し、その階層の上位レベルにワンクリックでアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="6900a-196">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="例は、階層リンク テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-198">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-198">Top use cases</span></span>

* <span data-ttu-id="6900a-199">階層の通信</span><span class="sxs-lookup"><span data-stu-id="6900a-199">Communicate hierarchy</span></span>
* <span data-ttu-id="6900a-200">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="6900a-200">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="6900a-201">ツール バー</span><span class="sxs-lookup"><span data-stu-id="6900a-201">Toolbar</span></span>

<span data-ttu-id="6900a-202">ツールバーは、コントロールのセットをグループ化するためのコンテナです。</span><span class="sxs-lookup"><span data-stu-id="6900a-202">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="例は、ツールバー テンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-204">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-204">Top use cases</span></span>

* <span data-ttu-id="6900a-205">アプリ コンテンツに対するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="6900a-205">Contextual actions on app content</span></span>
* <span data-ttu-id="6900a-206">コンテキスト フィルターと検索</span><span class="sxs-lookup"><span data-stu-id="6900a-206">Contextual filter and find</span></span>
* <span data-ttu-id="6900a-207">ナビゲーションと階層リンク</span><span class="sxs-lookup"><span data-stu-id="6900a-207">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="6900a-208">ステージ</span><span class="sxs-lookup"><span data-stu-id="6900a-208">Stage</span></span>

<span data-ttu-id="6900a-209">Stage では、別のアプリやブラウザーで開く代わりに、Teamsでエンティティ (画像、ファイル、Web サイトなど) を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="6900a-209">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="6900a-210">ステージの主なユース ケースは表示です。サーフェスは複雑な相互作用には使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="6900a-210">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="6900a-211">(実装ノート: 大きな [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)を使用してステージを構築します。</span><span class="sxs-lookup"><span data-stu-id="6900a-211">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="例は、ステージテンプレートを示しています。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="6900a-213">トップユースケース</span><span class="sxs-lookup"><span data-stu-id="6900a-213">Top use cases</span></span>

* <span data-ttu-id="6900a-214">別のアプリやブラウザーではなく、Teamsでエンティティを開きます。</span><span class="sxs-lookup"><span data-stu-id="6900a-214">Open an entity in Teams instead of another app or browser.</span></span>
* <span data-ttu-id="6900a-215">スポットライトメディアやその他のコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="6900a-215">Spotlight media or other content.</span></span>
