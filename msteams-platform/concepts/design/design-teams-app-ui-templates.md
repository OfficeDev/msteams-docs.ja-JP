---
title: UI テンプレートを使用したアプリの設計
author: heath-hamilton
description: 標準化された UI コンポーネント、レイアウト、およびパターンを使用して、アプリを迅速に設計し、Microsoft Teams。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 5026554070396dcc55390496b6754961e8e037bc
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644858"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="53fde-103">UI テンプレートをMicrosoft Teamsアプリを設計する</span><span class="sxs-lookup"><span data-stu-id="53fde-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="53fde-104">UI テンプレートを使用Microsoft Teamsアプリを迅速に設計します。</span><span class="sxs-lookup"><span data-stu-id="53fde-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="53fde-105">テンプレートは、一般的な Teams の使用例で動作する Fluent UI ベースのコンポーネントのコレクションで、ユーザーに最適なエクスペリエンスを把握する時間が広がっています。</span><span class="sxs-lookup"><span data-stu-id="53fde-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="53fde-106">ツールとサンプルの使用を開始する</span><span class="sxs-lookup"><span data-stu-id="53fde-106">Getting started with tools and samples</span></span>

<span data-ttu-id="53fde-107">次のリソースは、UI テンプレートを使用してアプリを設計および開発するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="53fde-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="53fde-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="53fde-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="53fde-109">アプリ設計の UI テンプレートを Microsoft Teams UI キットから取得します。これには、使用状況、解剖学、アクセシビリティ、ベスト プラクティスに関する広範な情報も含まれています。</span><span class="sxs-lookup"><span data-stu-id="53fde-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53fde-110">UI キットを取得する (Figma)</span><span class="sxs-lookup"><span data-stu-id="53fde-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="53fde-111">Microsoft TeamsUI ライブラリ</span><span class="sxs-lookup"><span data-stu-id="53fde-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="53fde-112">ブラウザーで UI テンプレートTeams関連するコンポーネントを個別に表示およびテストします。</span><span class="sxs-lookup"><span data-stu-id="53fde-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53fde-113">UI ライブラリ (プレイグラウンド) を試す</span><span class="sxs-lookup"><span data-stu-id="53fde-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="53fde-114">これらのテンプレートと関連コンポーネントをアプリ プロジェクトに直接Teamsインポートします。</span><span class="sxs-lookup"><span data-stu-id="53fde-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53fde-115">UI ライブラリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="53fde-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="53fde-116">サンプル アプリ</span><span class="sxs-lookup"><span data-stu-id="53fde-116">Sample app</span></span>

<span data-ttu-id="53fde-117">サンプル アプリをインストールして、UI テンプレートの外観と動作を各コンテキストTeamsします。</span><span class="sxs-lookup"><span data-stu-id="53fde-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53fde-118">サンプル アプリを取得する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="53fde-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a><span data-ttu-id="53fde-119">ダッシュボード</span><span class="sxs-lookup"><span data-stu-id="53fde-119">Dashboard</span></span>

<span data-ttu-id="53fde-120">ダッシュボードには、さまざまな種類のコンテンツが中央の場所に表示されます (Teamsまたはタブ)。</span><span class="sxs-lookup"><span data-stu-id="53fde-120">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="53fde-121">ユーザーは、ダッシュボードに表示される機能の少なくとも一部をカスタマイズできる必要があります。</span><span class="sxs-lookup"><span data-stu-id="53fde-121">Users should be able to customize at least some of what they see on a dashboard.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-122">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-122">Top use cases</span></span>

* <span data-ttu-id="53fde-123">データの分析</span><span class="sxs-lookup"><span data-stu-id="53fde-123">Analyze data</span></span>
* <span data-ttu-id="53fde-124">レポートの指標</span><span class="sxs-lookup"><span data-stu-id="53fde-124">Report metrics</span></span>
* <span data-ttu-id="53fde-125">異なる情報を 1 か所に整理する</span><span class="sxs-lookup"><span data-stu-id="53fde-125">Organize different information in one place</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-126">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-126">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="例は、デスクトップ上のダッシュボード UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-128">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-128">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="例は、モバイルでのダッシュボード UI テンプレートを示しています。" border="false":::

---

## <a name="data-visualization"></a><span data-ttu-id="53fde-130">データ可視化</span><span class="sxs-lookup"><span data-stu-id="53fde-130">Data visualization</span></span>

<span data-ttu-id="53fde-131">異なるカード サイズ (シングル、ダブル、フル) を使用して、データの視覚化を同じページで積み重ね、整理できます。</span><span class="sxs-lookup"><span data-stu-id="53fde-131">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="53fde-132">カードは、列のレイアウトに合わせて拡大縮小され、空白を入力します。</span><span class="sxs-lookup"><span data-stu-id="53fde-132">The cards scale to fit the column layout and fill in blank spaces.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-133">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-133">Top use cases</span></span>

* <span data-ttu-id="53fde-134">複雑な情報を表示する</span><span class="sxs-lookup"><span data-stu-id="53fde-134">Display complex information</span></span>
* <span data-ttu-id="53fde-135">ダッシュボードの作成</span><span class="sxs-lookup"><span data-stu-id="53fde-135">Create a dashboard</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-136">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-136">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="例は、デスクトップ上のデータ可視化 UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-138">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="例は、モバイルでのデータ可視化 UI テンプレートを示しています。" border="false":::

---

## <a name="empty-state"></a><span data-ttu-id="53fde-140">空の状態</span><span class="sxs-lookup"><span data-stu-id="53fde-140">Empty state</span></span>

<span data-ttu-id="53fde-141">空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="53fde-141">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="53fde-142">柔軟性が高く、次の設計で 1 つ、少数、またはすべてのコンポーネントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="53fde-142">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-143">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-143">Top use cases</span></span>

* <span data-ttu-id="53fde-144">サインイン</span><span class="sxs-lookup"><span data-stu-id="53fde-144">Sign in</span></span>
* <span data-ttu-id="53fde-145">ウェルカム メッセージと初回実行エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="53fde-145">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="53fde-146">成功メッセージ</span><span class="sxs-lookup"><span data-stu-id="53fde-146">Success messages</span></span>
* <span data-ttu-id="53fde-147">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="53fde-147">Error messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-148">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-148">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="例は、デスクトップ上の空の状態 UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-150">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-150">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="例は、モバイル上の空の状態 UI テンプレートを示しています。" border="false":::

---

## <a name="filter"></a><span data-ttu-id="53fde-152">Filter</span><span class="sxs-lookup"><span data-stu-id="53fde-152">Filter</span></span>

<span data-ttu-id="53fde-153">フィルターを使用すると、選択した条件に基づいて表示される情報を減らします。</span><span class="sxs-lookup"><span data-stu-id="53fde-153">A filter allows you to reduce the information you see based on the criteria selected.</span></span> <span data-ttu-id="53fde-154">コンテンツを整理するテーブル、リスト、カード、その他のコンポーネントを含むフィルターを含めできます。</span><span class="sxs-lookup"><span data-stu-id="53fde-154">You can include filters with tables, lists, cards, and other components that organize content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-155">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-155">Top use cases</span></span>

<span data-ttu-id="53fde-156">次の場所でコンテンツを整理します。</span><span class="sxs-lookup"><span data-stu-id="53fde-156">Organizing content in:</span></span>

* <span data-ttu-id="53fde-157">リスト</span><span class="sxs-lookup"><span data-stu-id="53fde-157">Lists</span></span>
* <span data-ttu-id="53fde-158">テーブル</span><span class="sxs-lookup"><span data-stu-id="53fde-158">Tables</span></span>
* <span data-ttu-id="53fde-159">ダッシュボード</span><span class="sxs-lookup"><span data-stu-id="53fde-159">Dashboards</span></span>
* <span data-ttu-id="53fde-160">データ可視化</span><span class="sxs-lookup"><span data-stu-id="53fde-160">Data visualization</span></span>

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="例は、フィルター テンプレートを示しています。" border="false":::

## <a name="form"></a><span data-ttu-id="53fde-162">フォーム</span><span class="sxs-lookup"><span data-stu-id="53fde-162">Form</span></span>

<span data-ttu-id="53fde-163">フォームは、構造化された方法でユーザー入力を収集、検証、送信するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="53fde-163">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="53fde-164">ユーザー エクスペリエンスを向上するには、入力フィールドの明確なラベル付けと論理グループ化が重要です。</span><span class="sxs-lookup"><span data-stu-id="53fde-164">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-165">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-165">Top use cases</span></span>

* <span data-ttu-id="53fde-166">サインイン</span><span class="sxs-lookup"><span data-stu-id="53fde-166">Sign in</span></span>
* <span data-ttu-id="53fde-167">ユーザー プロファイル</span><span class="sxs-lookup"><span data-stu-id="53fde-167">User profiles</span></span>
* <span data-ttu-id="53fde-168">設定</span><span class="sxs-lookup"><span data-stu-id="53fde-168">Settings</span></span>
* <span data-ttu-id="53fde-169">ユーザー入力コレクション</span><span class="sxs-lookup"><span data-stu-id="53fde-169">User input collection</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="例は、デスクトップ上のフォーム UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-172">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="例は、モバイルでのフォーム UI テンプレートを示しています。" border="false":::

---

## <a name="list"></a><span data-ttu-id="53fde-174">List</span><span class="sxs-lookup"><span data-stu-id="53fde-174">List</span></span>

<span data-ttu-id="53fde-175">リストを使用して、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="53fde-175">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-176">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-176">Top use cases</span></span>

* <span data-ttu-id="53fde-177">データの表示</span><span class="sxs-lookup"><span data-stu-id="53fde-177">Display data</span></span>
* <span data-ttu-id="53fde-178">アプリ コンテンツに関するコンテキスト アクション</span><span class="sxs-lookup"><span data-stu-id="53fde-178">Contextual actions on app content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-179">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="例は、デスクトップ上のリスト UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-181">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="例は、モバイルのリスト UI テンプレートを示しています。" border="false":::

---

## <a name="sign-in"></a><span data-ttu-id="53fde-183">サインイン</span><span class="sxs-lookup"><span data-stu-id="53fde-183">Sign in</span></span>

<span data-ttu-id="53fde-184">さまざまなコンテキストと ID プロバイダー用にアプリ Teamsフローを設計できます。</span><span class="sxs-lookup"><span data-stu-id="53fde-184">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="53fde-185">次の例では、シングル サインオン (SSO) を含み、最も簡単な認証エクスペリエンスをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="53fde-185">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

### <a name="top-use-case"></a><span data-ttu-id="53fde-186">トップ の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-186">Top use case</span></span>

* <span data-ttu-id="53fde-187">ユーザーの認証</span><span class="sxs-lookup"><span data-stu-id="53fde-187">Authenticate users</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-188">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-188">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="例は、デスクトップ上の UI テンプレートのサインインを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-190">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-190">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="例は、モバイルでのサインイン UI テンプレートを示しています。" border="false":::

---

## <a name="settings"></a><span data-ttu-id="53fde-192">設定</span><span class="sxs-lookup"><span data-stu-id="53fde-192">Settings</span></span>

<span data-ttu-id="53fde-193">設定は、ユーザーがアプリで自分の設定を構成できる画面です。</span><span class="sxs-lookup"><span data-stu-id="53fde-193">Settings screens are where users can configure their preferences with your app.</span></span> <span data-ttu-id="53fde-194">(注: 設定は基本的な UI コンポーネント[のコンテナーです](~/concepts/design/design-teams-app-basic-ui-components.md)。)</span><span class="sxs-lookup"><span data-stu-id="53fde-194">(Note: Settings is a container for [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md).)</span></span>

### <a name="top-use-case"></a><span data-ttu-id="53fde-195">トップ の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-195">Top use case</span></span>

* <span data-ttu-id="53fde-196">アプリの機能を管理する</span><span class="sxs-lookup"><span data-stu-id="53fde-196">Manage app features</span></span>

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="設定テンプレートの例を示します。" border="false":::

## <a name="task-board"></a><span data-ttu-id="53fde-198">タスク ボード</span><span class="sxs-lookup"><span data-stu-id="53fde-198">Task board</span></span>

<span data-ttu-id="53fde-199">タスク ボード (カンバン ボードまたはスイム レーンとも呼ばれる) は、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="53fde-199">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="53fde-200">また、任意の種類のコンテンツをカテゴリに並べ替える場合にも使用できます。</span><span class="sxs-lookup"><span data-stu-id="53fde-200">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="53fde-201">列間でカードを編集および移動できます。</span><span class="sxs-lookup"><span data-stu-id="53fde-201">You can edit and move the cards between columns.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-202">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-202">Top use cases</span></span>

* <span data-ttu-id="53fde-203">プロジェクトの管理。</span><span class="sxs-lookup"><span data-stu-id="53fde-203">Project management.</span></span> <span data-ttu-id="53fde-204">タスクの割り当てと追跡状態</span><span class="sxs-lookup"><span data-stu-id="53fde-204">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="53fde-205">ブレインストーミング。</span><span class="sxs-lookup"><span data-stu-id="53fde-205">Brainstorming.</span></span> <span data-ttu-id="53fde-206">さまざまなカテゴリにアイデアを追加する</span><span class="sxs-lookup"><span data-stu-id="53fde-206">Adding ideas in different categories</span></span>
* <span data-ttu-id="53fde-207">並べ替えの演習。</span><span class="sxs-lookup"><span data-stu-id="53fde-207">Sorting exercises.</span></span> <span data-ttu-id="53fde-208">任意の種類の情報をバケットに整理する</span><span class="sxs-lookup"><span data-stu-id="53fde-208">Organizing any kind of information into buckets</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-209">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-209">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="例は、デスクトップ上のタスク ボード UI テンプレートを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-211">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-211">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="例は、モバイル上のタスク ボード UI テンプレートを示しています。" border="false":::

---

## <a name="wizard"></a><span data-ttu-id="53fde-213">ウィザード</span><span class="sxs-lookup"><span data-stu-id="53fde-213">Wizard</span></span>

<span data-ttu-id="53fde-214">ウィザードは、ユーザーが複数の画面を介してタスク (セットアップ プロセスなど) を完了する方法を案内します。</span><span class="sxs-lookup"><span data-stu-id="53fde-214">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="53fde-215">上位の使用例</span><span class="sxs-lookup"><span data-stu-id="53fde-215">Top use cases</span></span>

* <span data-ttu-id="53fde-216">セットアップ</span><span class="sxs-lookup"><span data-stu-id="53fde-216">Setup</span></span>
* <span data-ttu-id="53fde-217">オンボード</span><span class="sxs-lookup"><span data-stu-id="53fde-217">Onboarding</span></span>
* <span data-ttu-id="53fde-218">初回実行エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="53fde-218">First-run experiences</span></span>

# <a name="desktop"></a>[<span data-ttu-id="53fde-219">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="53fde-219">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="例では、デスクトップにウィザード UI テンプレートを表示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="53fde-221">モバイル</span><span class="sxs-lookup"><span data-stu-id="53fde-221">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="例は、モバイルでのウィザード UI テンプレートを示しています。" border="false":::

---
