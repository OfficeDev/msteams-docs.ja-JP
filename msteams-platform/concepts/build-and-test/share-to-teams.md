---
title: '[Teams で共有] ボタンを作成する'
description: Web サイトの Teams 埋め込みボタンに共有を追加する方法
ms.topic: reference
keywords: Teams の共有と Teams 間の共有
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014335"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="51ac5-104">Web サイトの [Teams で共有] ボタンを作成する</span><span class="sxs-lookup"><span data-stu-id="51ac5-104">Create a Share-to-Teams button for your website</span></span>

>[!NOTE]
> * <span data-ttu-id="51ac5-105">Edge と Chrome のデスクトップ バージョンだけがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="51ac5-106">Freemium またはゲスト アカウントの使用はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="51ac5-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="51ac5-107">サード パーティの Web サイトでは、ランチャー スクリプトを使用して、Teams への共有ボタンを Web ページに埋め込み、クリックするとポップアップ ウィンドウで Teams への共有エクスペリエンスを起動できます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="51ac5-108">これにより、コンテキストを切り替えなくても、任意のユーザーまたは Microsoft Teams チャネルに直接リンクを共有できます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Teams への共有ポップアップ](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="51ac5-110">[Teams に共有] ボタンを埋め込む方法</span><span class="sxs-lookup"><span data-stu-id="51ac5-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="51ac5-111">最初に、Web ページにスクリプト `launcher.js` を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51ac5-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="51ac5-112">次に、クラス属性と属性で共有するリンクを含む HTML 要素を Web ページ `teams-share-button` に追加 `data-href` します。</span><span class="sxs-lookup"><span data-stu-id="51ac5-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="51ac5-113">これにより、Microsoft Teams アイコンが Web サイトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-113">This will add the Microsoft Teams icon to your website.</span></span>

![[Teams に共有] アイコン](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="51ac5-115">必要に応じて、[Teams に共有] ボタンに別のアイコン サイズが必要な場合は、属性を使用 `data-icon-px-size` します。</span><span class="sxs-lookup"><span data-stu-id="51ac5-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="51ac5-116">共有するリンクからの URL プレビューが Teams で正しく表示されていないことが分かっている場合 (たとえば、リンクはユーザー認証を必要とします)、設定された属性を追加して URL プレビューを無効に `data-preview` できます `false` 。</span><span class="sxs-lookup"><span data-stu-id="51ac5-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="51ac5-117">ページがコンテンツを動的にレンダリングする場合は、このメソッドを使用して、パイプライン内の適切な場所に [共有] ボタンを強制的 `shareToMicrosoftTeams.renderButtons()` にレンダリングできます。 </span><span class="sxs-lookup"><span data-stu-id="51ac5-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="51ac5-118">Web サイト プレビューの作成</span><span class="sxs-lookup"><span data-stu-id="51ac5-118">Crafting your website preview</span></span>

<span data-ttu-id="51ac5-119">Web サイトを Teams と共有すると、選択したチャネルに挿入されたカードに Web サイトのプレビューが含まれる。</span><span class="sxs-lookup"><span data-stu-id="51ac5-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="51ac5-120">共有する Web サイト (URL) に適切なメタデータを追加することで、このプレビューの動作を制御 `data-href` できます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="51ac5-121">次の表に、必要なタグの概要を示します。</span><span class="sxs-lookup"><span data-stu-id="51ac5-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="51ac5-122">HTML の既定のバージョンまたは Open Graph バージョンを使用できます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="51ac5-123">プレビューを表示するには、次の条件を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51ac5-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="51ac5-124">サムネイル画像、またはタイトルと説明の両方を含める (最適な結果を得る場合は、3 つすべてが含まれます)。</span><span class="sxs-lookup"><span data-stu-id="51ac5-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="51ac5-125">共有される URL は認証を必要とできません。</span><span class="sxs-lookup"><span data-stu-id="51ac5-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="51ac5-126">それでも共有できますが、プレビューは作成されません。</span><span class="sxs-lookup"><span data-stu-id="51ac5-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="51ac5-127">値</span><span class="sxs-lookup"><span data-stu-id="51ac5-127">Value</span></span>|<span data-ttu-id="51ac5-128">メタ タグ</span><span class="sxs-lookup"><span data-stu-id="51ac5-128">Meta tag</span></span>| <span data-ttu-id="51ac5-129">Open Graph</span><span class="sxs-lookup"><span data-stu-id="51ac5-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="51ac5-130">タイトル</span><span class="sxs-lookup"><span data-stu-id="51ac5-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="51ac5-131">説明</span><span class="sxs-lookup"><span data-stu-id="51ac5-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="51ac5-132">サムネイル画像</span><span class="sxs-lookup"><span data-stu-id="51ac5-132">Thumbnail Image</span></span>| <span data-ttu-id="51ac5-133">なし</span><span class="sxs-lookup"><span data-stu-id="51ac5-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="51ac5-134">Teams for Education への共有</span><span class="sxs-lookup"><span data-stu-id="51ac5-134">Share to Teams for Education</span></span>

<span data-ttu-id="51ac5-135">[Teams に共有] ボタンを使用する教師には、追加のオプションが表示されます `Create an Assignment` 。</span><span class="sxs-lookup"><span data-stu-id="51ac5-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="51ac5-136">これにより、共有リンクに基づいて選択したチームに割り当てを簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Teams への共有ポップアップ](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="51ac5-138">完全launcher.js定義</span><span class="sxs-lookup"><span data-stu-id="51ac5-138">Full launcher.js definition</span></span>

| <span data-ttu-id="51ac5-139">プロパティ</span><span class="sxs-lookup"><span data-stu-id="51ac5-139">Property</span></span> | <span data-ttu-id="51ac5-140">HTML 属性</span><span class="sxs-lookup"><span data-stu-id="51ac5-140">HTML attribute</span></span> | <span data-ttu-id="51ac5-141">種類</span><span class="sxs-lookup"><span data-stu-id="51ac5-141">Type</span></span> | <span data-ttu-id="51ac5-142">既定値</span><span class="sxs-lookup"><span data-stu-id="51ac5-142">Default</span></span> | <span data-ttu-id="51ac5-143">説明</span><span class="sxs-lookup"><span data-stu-id="51ac5-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="51ac5-144">href</span><span class="sxs-lookup"><span data-stu-id="51ac5-144">href</span></span> | `data-href` | <span data-ttu-id="51ac5-145">文字列</span><span class="sxs-lookup"><span data-stu-id="51ac5-145">string</span></span> | <span data-ttu-id="51ac5-146">該当なし</span><span class="sxs-lookup"><span data-stu-id="51ac5-146">n/a</span></span> | <span data-ttu-id="51ac5-147">共有するコンテンツの href。</span><span class="sxs-lookup"><span data-stu-id="51ac5-147">The href of the content to share.</span></span> |
| <span data-ttu-id="51ac5-148">preview</span><span class="sxs-lookup"><span data-stu-id="51ac5-148">preview</span></span> | `data-preview` | <span data-ttu-id="51ac5-149">boolean (文字列として)</span><span class="sxs-lookup"><span data-stu-id="51ac5-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="51ac5-150">共有するコンテンツのプレビューを表示するかどうか。</span><span class="sxs-lookup"><span data-stu-id="51ac5-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="51ac5-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="51ac5-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="51ac5-152">number (文字列)</span><span class="sxs-lookup"><span data-stu-id="51ac5-152">number (as a string)</span></span> | `32` | <span data-ttu-id="51ac5-153">レンダリングする [Share-to-Teams] ボタンのサイズ (ピクセル単位)。</span><span class="sxs-lookup"><span data-stu-id="51ac5-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="51ac5-154">msgText</span><span class="sxs-lookup"><span data-stu-id="51ac5-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="51ac5-155">文字列</span><span class="sxs-lookup"><span data-stu-id="51ac5-155">string</span></span> | <span data-ttu-id="51ac5-156">該当なし</span><span class="sxs-lookup"><span data-stu-id="51ac5-156">n/a</span></span> | <span data-ttu-id="51ac5-157">メッセージ作成ボックスのリンクの前に挿入される既定のテキスト (200 文字制限)</span><span class="sxs-lookup"><span data-stu-id="51ac5-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="51ac5-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="51ac5-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="51ac5-159">文字列</span><span class="sxs-lookup"><span data-stu-id="51ac5-159">string</span></span> | <span data-ttu-id="51ac5-160">該当なし</span><span class="sxs-lookup"><span data-stu-id="51ac5-160">n/a</span></span> | <span data-ttu-id="51ac5-161">割り当ての "命令" フィールドに挿入される既定のテキスト (200 文字制限)</span><span class="sxs-lookup"><span data-stu-id="51ac5-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="51ac5-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="51ac5-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="51ac5-163">文字列</span><span class="sxs-lookup"><span data-stu-id="51ac5-163">string</span></span> | <span data-ttu-id="51ac5-164">該当なし</span><span class="sxs-lookup"><span data-stu-id="51ac5-164">n/a</span></span> | <span data-ttu-id="51ac5-165">割り当ての "タイトル" フィールドに挿入される既定のテキスト (50 文字制限)</span><span class="sxs-lookup"><span data-stu-id="51ac5-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="51ac5-166">メソッド</span><span class="sxs-lookup"><span data-stu-id="51ac5-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="51ac5-167">`options` (省略可能): `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="51ac5-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="51ac5-168">現在ページ上のすべての共有ボタンをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="51ac5-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="51ac5-169">オプションのオブジェクトに要素のリストが指定されている場合、それらの要素 `options` は共有ボタンにレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="51ac5-170">既定のフォーム値の設定</span><span class="sxs-lookup"><span data-stu-id="51ac5-170">Setting default form values</span></span>

<span data-ttu-id="51ac5-171">必要に応じて、[Teams に共有] フォームの次のフィールドの既定値を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="51ac5-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="51ac5-172">このことを言う ( `msgText` )</span><span class="sxs-lookup"><span data-stu-id="51ac5-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="51ac5-173">割り当て命令 ( `assignInstr` )</span><span class="sxs-lookup"><span data-stu-id="51ac5-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="51ac5-174">割り当てタイトル ( `assignTitle` )</span><span class="sxs-lookup"><span data-stu-id="51ac5-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="51ac5-175">例: 既定のフォーム値</span><span class="sxs-lookup"><span data-stu-id="51ac5-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
