---
title: '[Share-to-Teams の作成] ボタン'
description: Web サイトの [Teams 埋め込み共有] ボタンを追加する方法
ms.topic: reference
localization_priority: Normal
keywords: チーム間の共有
ms.openlocfilehash: c77c4149c95685e17e8f789a9536b4d81e05d13f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020824"
---
# <a name="create-share-to-teams-button"></a><span data-ttu-id="21423-104">[Share-to-Teams の作成] ボタン</span><span class="sxs-lookup"><span data-stu-id="21423-104">Create Share-to-Teams button</span></span>

<span data-ttu-id="21423-105">サードパーティの Web サイトでは、ランチャー スクリプトを使用して、Web ページに Share-to-Teams ボタンを埋め込む可能性があります。</span><span class="sxs-lookup"><span data-stu-id="21423-105">Third-party websites can use the launcher script to embed Share-to-Teams buttons on their webpages.</span></span> <span data-ttu-id="21423-106">選択すると、ポップアップ ウィンドウで Share-to-Teams エクスペリエンスが起動します。</span><span class="sxs-lookup"><span data-stu-id="21423-106">When you select, it launches the Share-to-Teams experience in a pop-up window.</span></span> <span data-ttu-id="21423-107">これにより、コンテキストを切り替えることなく、任意のユーザーまたは Microsoft Teams チャネルへのリンクを直接共有できます。</span><span class="sxs-lookup"><span data-stu-id="21423-107">This allows you to share a link directly to any person or Microsoft Teams channel without switching the context.</span></span> <span data-ttu-id="21423-108">このドキュメントでは、Web サイトの [Share-to-Teams] ボタンを作成して埋め込み、Web サイトのプレビューを作成し、教育向け Share-to-Teams を拡張する方法についてガイドします。</span><span class="sxs-lookup"><span data-stu-id="21423-108">This document guides you on how to create, and embed a Share-to-Teams button for your website, craft your website preview, and extend Share-to-Teams for Education.</span></span>

> [!NOTE]
> * <span data-ttu-id="21423-109">サポートされているのは、Edge と Chrome のデスクトップ バージョンのみです。</span><span class="sxs-lookup"><span data-stu-id="21423-109">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="21423-110">Freemium アカウントまたはゲスト アカウントの使用はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="21423-110">Use of Freemium or guest accounts is not supported.</span></span>  

<span data-ttu-id="21423-111">次の図は、Share-to-Teams ポップアップ エクスペリエンスを表示します。</span><span class="sxs-lookup"><span data-stu-id="21423-111">The following image displays the Share-to-Teams pop-up experience:</span></span>

![[チーム間の共有] ポップアップ](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a><span data-ttu-id="21423-113">[Teams への共有の埋め込み] ボタン</span><span class="sxs-lookup"><span data-stu-id="21423-113">Embed a Share to Teams button</span></span>

1. <span data-ttu-id="21423-114">Web ページ `launcher.js` にスクリプトを追加します。</span><span class="sxs-lookup"><span data-stu-id="21423-114">Add the `launcher.js` script on your webpage.</span></span>

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. <span data-ttu-id="21423-115">クラス属性と属性で共有するリンクを含む HTML 要素を Web ページ `teams-share-button` に追加 `data-href` します。</span><span class="sxs-lookup"><span data-stu-id="21423-115">Add a HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    <span data-ttu-id="21423-116">これを完了すると、Microsoft Teams アイコンが Web サイトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="21423-116">After completing this, the Microsoft Teams icon gets added to your website.</span></span> <span data-ttu-id="21423-117">次の図は、Share-to-Teams アイコンを示しています。</span><span class="sxs-lookup"><span data-stu-id="21423-117">The following image shows Share-to-Teams icon:</span></span>

    ![[Teams に共有] アイコン](~/assets/icons/share-to-teams-icon.png)

1. <span data-ttu-id="21423-119">または、[共有する Teams] ボタンに別のアイコン サイズが必要な場合は、属性を使用 `data-icon-px-size` します。</span><span class="sxs-lookup"><span data-stu-id="21423-119">Alternatively, if you want a different icon size for the Share-to Teams button, use the `data-icon-px-size` attribute.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. <span data-ttu-id="21423-120">共有リンクでユーザー認証が必要で、リンクから共有する URL プレビューが Teams でうまく表示されない場合は、に属性セットを追加して URL プレビューを `data-preview` 無効にできます `false` 。</span><span class="sxs-lookup"><span data-stu-id="21423-120">If the shared link requires user authentication, and the URL preview from your link to be shared does not render well in Teams then, you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. <span data-ttu-id="21423-121">ページがコンテンツを動的にレンダリングする場合は、このメソッドを使用して、パイプライン内の適切な場所で [共有] ボタンを強制的 `shareToMicrosoftTeams.renderButtons()` にレンダリングできます。 </span><span class="sxs-lookup"><span data-stu-id="21423-121">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="craft-your-website-preview"></a><span data-ttu-id="21423-122">Web サイトのプレビューを作成する</span><span class="sxs-lookup"><span data-stu-id="21423-122">Craft your website preview</span></span>

<span data-ttu-id="21423-123">Web サイトが Teams に共有されている場合、選択したチャネルに挿入されるカードには、Web サイトのプレビューが含まれる。</span><span class="sxs-lookup"><span data-stu-id="21423-123">When your website is shared to Teams, the card that is inserted into the selected channel contains a preview of your website.</span></span> <span data-ttu-id="21423-124">このプレビューの動作を制御するには、共有する Web サイト (URL など) に適切なメタ データが追加されます `data-href` 。</span><span class="sxs-lookup"><span data-stu-id="21423-124">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared, such as the `data-href` URL.</span></span>  

<span data-ttu-id="21423-125">**プレビューを表示するには**</span><span class="sxs-lookup"><span data-stu-id="21423-125">**To display the preview**</span></span>

* <span data-ttu-id="21423-126">サムネイル 画像、または **Title と** Description の **両方を含める\*\*\*\*必要があります**。</span><span class="sxs-lookup"><span data-stu-id="21423-126">You must include either a **Thumbnail image**, or both a **Title** and **Description**.</span></span> <span data-ttu-id="21423-127">最適な結果を得る場合は、3 つすべてが含まれます。</span><span class="sxs-lookup"><span data-stu-id="21423-127">For best results, include all three.</span></span>
* <span data-ttu-id="21423-128">共有 URL は認証を必要とします。</span><span class="sxs-lookup"><span data-stu-id="21423-128">The shared URL does not require authentication.</span></span> <span data-ttu-id="21423-129">認証が必要な場合は共有できますが、プレビューは作成されません。</span><span class="sxs-lookup"><span data-stu-id="21423-129">If it requires authentication, you can share it, but the preview is not created.</span></span>

<span data-ttu-id="21423-130">次の表に、必要なタグの概要を示します。</span><span class="sxs-lookup"><span data-stu-id="21423-130">The following table outlines the necessary tags:</span></span>

|<span data-ttu-id="21423-131">値</span><span class="sxs-lookup"><span data-stu-id="21423-131">Value</span></span>|<span data-ttu-id="21423-132">メタ タグ</span><span class="sxs-lookup"><span data-stu-id="21423-132">Meta tag</span></span>| <span data-ttu-id="21423-133">グラフを開く</span><span class="sxs-lookup"><span data-stu-id="21423-133">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="21423-134">タイトル</span><span class="sxs-lookup"><span data-stu-id="21423-134">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="21423-135">説明</span><span class="sxs-lookup"><span data-stu-id="21423-135">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="21423-136">サムネイル 画像</span><span class="sxs-lookup"><span data-stu-id="21423-136">Thumbnail Image</span></span>| <span data-ttu-id="21423-137">none。</span><span class="sxs-lookup"><span data-stu-id="21423-137">none.</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

<span data-ttu-id="21423-138">HTML の既定のバージョン、または Open Graph バージョンのいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="21423-138">You can use either the html default versions, or the Open Graph version.</span></span>

## <a name="share-to-teams-for-education"></a><span data-ttu-id="21423-139">教育向け Teams への共有</span><span class="sxs-lookup"><span data-stu-id="21423-139">Share to Teams for Education</span></span>

<span data-ttu-id="21423-140">[チームに共有] ボタンを使用する教師の場合は、追加のオプションがあります `Create an Assignment` 。</span><span class="sxs-lookup"><span data-stu-id="21423-140">For teachers using the Share to Teams button, there is an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="21423-141">これにより、共有リンクに基づいて、選択したチームで割り当てを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="21423-141">This enables you to quickly create an assignment in the chosen Team, based on the shared link.</span></span> <span data-ttu-id="21423-142">次の図は、教育用の Share-to-Teams を表示します。</span><span class="sxs-lookup"><span data-stu-id="21423-142">The following image displays Share-to-Teams for education:</span></span> 

![Teams ポップアップ教育への共有](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="21423-144">完全なlauncher.js定義</span><span class="sxs-lookup"><span data-stu-id="21423-144">Full launcher.js definition</span></span>

| <span data-ttu-id="21423-145">プロパティ</span><span class="sxs-lookup"><span data-stu-id="21423-145">Property</span></span> | <span data-ttu-id="21423-146">HTML 属性</span><span class="sxs-lookup"><span data-stu-id="21423-146">HTML attribute</span></span> | <span data-ttu-id="21423-147">種類</span><span class="sxs-lookup"><span data-stu-id="21423-147">Type</span></span> | <span data-ttu-id="21423-148">既定値</span><span class="sxs-lookup"><span data-stu-id="21423-148">Default</span></span> | <span data-ttu-id="21423-149">説明</span><span class="sxs-lookup"><span data-stu-id="21423-149">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="21423-150">href</span><span class="sxs-lookup"><span data-stu-id="21423-150">href</span></span> | `data-href` | <span data-ttu-id="21423-151">文字列</span><span class="sxs-lookup"><span data-stu-id="21423-151">string</span></span> | <span data-ttu-id="21423-152">該当なし</span><span class="sxs-lookup"><span data-stu-id="21423-152">n/a</span></span> | <span data-ttu-id="21423-153">共有するコンテンツの href。</span><span class="sxs-lookup"><span data-stu-id="21423-153">The href of the content to share.</span></span> |
| <span data-ttu-id="21423-154">preview</span><span class="sxs-lookup"><span data-stu-id="21423-154">preview</span></span> | `data-preview` | <span data-ttu-id="21423-155">boolean (文字列として)</span><span class="sxs-lookup"><span data-stu-id="21423-155">boolean (as a string)</span></span> | `true` | <span data-ttu-id="21423-156">共有するコンテンツのプレビューを表示するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="21423-156">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="21423-157">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="21423-157">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="21423-158">number (文字列として)</span><span class="sxs-lookup"><span data-stu-id="21423-158">number (as a string)</span></span> | `32` | <span data-ttu-id="21423-159">レンダリングする [Share-to-Teams] ボタンのサイズ (ピクセル単位)。</span><span class="sxs-lookup"><span data-stu-id="21423-159">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="21423-160">msgText</span><span class="sxs-lookup"><span data-stu-id="21423-160">msgText</span></span> | `data-msg-text` | <span data-ttu-id="21423-161">文字列</span><span class="sxs-lookup"><span data-stu-id="21423-161">string</span></span> | <span data-ttu-id="21423-162">該当なし</span><span class="sxs-lookup"><span data-stu-id="21423-162">n/a</span></span> | <span data-ttu-id="21423-163">メッセージ作成ボックスのリンクの前に挿入される既定のテキスト。</span><span class="sxs-lookup"><span data-stu-id="21423-163">Default Text to be inserted before the link in the message compose box.</span></span> <span data-ttu-id="21423-164">最大文字数は 200 文字です。</span><span class="sxs-lookup"><span data-stu-id="21423-164">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="21423-165">assignInstr</span><span class="sxs-lookup"><span data-stu-id="21423-165">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="21423-166">文字列</span><span class="sxs-lookup"><span data-stu-id="21423-166">string</span></span> | <span data-ttu-id="21423-167">該当なし</span><span class="sxs-lookup"><span data-stu-id="21423-167">n/a</span></span> | <span data-ttu-id="21423-168">割り当ての [命令] フィールドに挿入される既定のテキスト。</span><span class="sxs-lookup"><span data-stu-id="21423-168">Default Text to be inserted in the assignments "Instructions" field.</span></span> <span data-ttu-id="21423-169">最大文字数は 200 文字です。</span><span class="sxs-lookup"><span data-stu-id="21423-169">Maximum number of characters is 200.</span></span> |
| <span data-ttu-id="21423-170">assignTitle</span><span class="sxs-lookup"><span data-stu-id="21423-170">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="21423-171">文字列</span><span class="sxs-lookup"><span data-stu-id="21423-171">string</span></span> | <span data-ttu-id="21423-172">該当なし</span><span class="sxs-lookup"><span data-stu-id="21423-172">n/a</span></span> | <span data-ttu-id="21423-173">割り当ての [タイトル] フィールドに挿入される既定のテキスト。</span><span class="sxs-lookup"><span data-stu-id="21423-173">Default Text to be inserted in the assignments "Title" field.</span></span> <span data-ttu-id="21423-174">最大文字数は 50 です。</span><span class="sxs-lookup"><span data-stu-id="21423-174">Maximum number of characters is 50.</span></span> |

### <a name="methods"></a><span data-ttu-id="21423-175">メソッド</span><span class="sxs-lookup"><span data-stu-id="21423-175">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="21423-176">`options` (省略可能): `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="21423-176">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="21423-177">現在、すべての共有ボタンがページにレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="21423-177">Currently, all share buttons are rendered on the page.</span></span> <span data-ttu-id="21423-178">省略可能な `options` オブジェクトに要素のリストが指定されている場合、それらの要素は共有ボタンにレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="21423-178">If an optional `options` object is supplied with a list of elements, those elements are rendered into share buttons.</span></span>

### <a name="set-default-form-values"></a><span data-ttu-id="21423-179">既定のフォーム値を設定する</span><span class="sxs-lookup"><span data-stu-id="21423-179">Set default form values</span></span>

<span data-ttu-id="21423-180">[チームへの共有] フォームで、次のフィールドの既定値を設定できます。</span><span class="sxs-lookup"><span data-stu-id="21423-180">You can select to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="21423-181">このことを言います。 `msgText`</span><span class="sxs-lookup"><span data-stu-id="21423-181">Say something about this: `msgText`</span></span>
* <span data-ttu-id="21423-182">割り当て手順: `assignInstr`</span><span class="sxs-lookup"><span data-stu-id="21423-182">Assignment Instructions: `assignInstr`</span></span>
* <span data-ttu-id="21423-183">割り当てのタイトル: `assignTitle`</span><span class="sxs-lookup"><span data-stu-id="21423-183">Assignment Title: `assignTitle`</span></span>

#### <a name="example"></a><span data-ttu-id="21423-184">例</span><span class="sxs-lookup"><span data-stu-id="21423-184">Example</span></span>

 <span data-ttu-id="21423-185">既定のフォーム値は、次の例で指定します。</span><span class="sxs-lookup"><span data-stu-id="21423-185">Default form values are given in the following example:</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a><span data-ttu-id="21423-186">関連項目</span><span class="sxs-lookup"><span data-stu-id="21423-186">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21423-187">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="21423-187">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
