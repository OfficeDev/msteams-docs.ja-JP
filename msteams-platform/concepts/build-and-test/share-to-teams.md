---
title: Teams への共有の組み込みボタン
description: Web サイトに [Teams に共有] を埋め込むボタンを追加する方法
keywords: Teams 共有チームの共有
ms.openlocfilehash: 219724e6ef3448db8a5b1fc70a519803255ffee6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674972"
---
# <a name="creating-a-share-to-teams-embedded-button"></a><span data-ttu-id="db1cf-104">Teams への共有の組み込みボタンを作成する</span><span class="sxs-lookup"><span data-stu-id="db1cf-104">Creating a Share to Teams embedded button</span></span>

>[!NOTE]
> * <span data-ttu-id="db1cf-105">デスクトップバージョンのエッジおよびクロムのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="db1cf-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="db1cf-106">Freemium または guest アカウントの使用はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="db1cf-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="db1cf-107">サードパーティの web サイトでは、ラウンチャースクリプトを使用して、web ページに Teams ボタンへの共有を埋め込むことができます。これにより、クリックしたときに、Teams への共有がポップアップウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="db1cf-108">これにより、コンテキストを切り替えずに、任意のユーザーまたは Microsoft Teams チャネルにリンクを直接共有することができます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![Teams ポップアップに共有](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="db1cf-110">[方法] [チームに共有] ボタンを埋め込む</span><span class="sxs-lookup"><span data-stu-id="db1cf-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="db1cf-111">最初に、 `launcher.js`スクリプトを web ページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="db1cf-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="db1cf-112">次に、 `teams-share-button` class 属性を使用して web ページに HTML 要素を追加し、 `data-href`属性で共有するリンクを追加します。</span><span class="sxs-lookup"><span data-stu-id="db1cf-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="db1cf-113">これにより、Microsoft Teams アイコンが web サイトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-113">This will add the Microsoft Teams icon to your website.</span></span>

![Teams への共有アイコン](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="db1cf-115">必要に応じて、[Teams への共有] ボタンに異なるアイコンサイズを使用`data-icon-px-size`する場合は、属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="db1cf-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="db1cf-116">リンクから共有される URL プレビューが Teams に適切に表示されないことがわかっている場合 (たとえば、リンクにユーザー認証が必要な場合)、に設定`data-preview`した属性`false`をに追加することで、url プレビューを無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="db1cf-117">ページでコンテンツを動的にレンダリングする場合は、 `shareToMicrosoftTeams.renderButtons()`メソッドを使用して、[**共有**] ボタンをパイプライン内の適切な場所に強制的に表示することができます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="db1cf-118">Web サイトのプレビューを作成する</span><span class="sxs-lookup"><span data-stu-id="db1cf-118">Crafting your website preview</span></span>

<span data-ttu-id="db1cf-119">Web サイトが Teams に対して共有されると、選択したチャネルに挿入されるカードには、web サイトのプレビューが表示されます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="db1cf-120">このプレビューの動作を制御するには、共有する web サイト ( `data-href` URL) に適切なメタデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="db1cf-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="db1cf-121">次の表は、必要なタグの概要を示しています。</span><span class="sxs-lookup"><span data-stu-id="db1cf-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="db1cf-122">Html の既定のバージョン、または Open Graph のバージョンのいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="db1cf-123">プレビューを表示するためには、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="db1cf-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="db1cf-124">サムネイルイメージを含めるか、タイトルと説明の両方を含めます (最適な結果を得るために3つすべてを含みます)。</span><span class="sxs-lookup"><span data-stu-id="db1cf-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="db1cf-125">共有されている URL は認証を必要としません。</span><span class="sxs-lookup"><span data-stu-id="db1cf-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="db1cf-126">このまま共有することはできますが、プレビューは作成されません。</span><span class="sxs-lookup"><span data-stu-id="db1cf-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="db1cf-127">値</span><span class="sxs-lookup"><span data-stu-id="db1cf-127">Value</span></span>|<span data-ttu-id="db1cf-128">メタ タグ</span><span class="sxs-lookup"><span data-stu-id="db1cf-128">Meta tag</span></span>| <span data-ttu-id="db1cf-129">グラフを開く</span><span class="sxs-lookup"><span data-stu-id="db1cf-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="db1cf-130">タイトル</span><span class="sxs-lookup"><span data-stu-id="db1cf-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="db1cf-131">説明</span><span class="sxs-lookup"><span data-stu-id="db1cf-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="db1cf-132">サムネイルイメージ</span><span class="sxs-lookup"><span data-stu-id="db1cf-132">Thumbnail Image</span></span>| <span data-ttu-id="db1cf-133">none</span><span class="sxs-lookup"><span data-stu-id="db1cf-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="db1cf-134">教育機関との Teams への共有</span><span class="sxs-lookup"><span data-stu-id="db1cf-134">Share to Teams for Education</span></span>

<span data-ttu-id="db1cf-135">教師の場合、[Teams に共有] ボタンを使用するに`Create an Assignment`は、追加のオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="db1cf-136">これにより、共有リンクを基にして、選択したチームの割り当てをすばやく作成できます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![Teams ポップアップに共有](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="db1cf-138">完全な起動プログラム .js の定義</span><span class="sxs-lookup"><span data-stu-id="db1cf-138">Full launcher.js definition</span></span>

| <span data-ttu-id="db1cf-139">プロパティ</span><span class="sxs-lookup"><span data-stu-id="db1cf-139">Property</span></span> | <span data-ttu-id="db1cf-140">HTML 属性</span><span class="sxs-lookup"><span data-stu-id="db1cf-140">HTML attribute</span></span> | <span data-ttu-id="db1cf-141">型</span><span class="sxs-lookup"><span data-stu-id="db1cf-141">Type</span></span> | <span data-ttu-id="db1cf-142">既定値</span><span class="sxs-lookup"><span data-stu-id="db1cf-142">Default</span></span> | <span data-ttu-id="db1cf-143">説明</span><span class="sxs-lookup"><span data-stu-id="db1cf-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="db1cf-144">href</span><span class="sxs-lookup"><span data-stu-id="db1cf-144">href</span></span> | `data-href` | <span data-ttu-id="db1cf-145">string</span><span class="sxs-lookup"><span data-stu-id="db1cf-145">string</span></span> | <span data-ttu-id="db1cf-146">該当なし</span><span class="sxs-lookup"><span data-stu-id="db1cf-146">n/a</span></span> | <span data-ttu-id="db1cf-147">共有するコンテンツの href。</span><span class="sxs-lookup"><span data-stu-id="db1cf-147">The href of the content to share.</span></span> |
| <span data-ttu-id="db1cf-148">preview</span><span class="sxs-lookup"><span data-stu-id="db1cf-148">preview</span></span> | `data-preview` | <span data-ttu-id="db1cf-149">ブール型 (string)</span><span class="sxs-lookup"><span data-stu-id="db1cf-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="db1cf-150">共有するコンテンツのプレビューを表示するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="db1cf-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="db1cf-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="db1cf-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="db1cf-152">数値 (文字列型)</span><span class="sxs-lookup"><span data-stu-id="db1cf-152">number (as a string)</span></span> | `32` | <span data-ttu-id="db1cf-153">表示する [チーム間共有] ボタンのサイズ (ピクセル単位)。</span><span class="sxs-lookup"><span data-stu-id="db1cf-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="db1cf-154">msgText</span><span class="sxs-lookup"><span data-stu-id="db1cf-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="db1cf-155">string</span><span class="sxs-lookup"><span data-stu-id="db1cf-155">string</span></span> | <span data-ttu-id="db1cf-156">該当なし</span><span class="sxs-lookup"><span data-stu-id="db1cf-156">n/a</span></span> | <span data-ttu-id="db1cf-157">メッセージ作成ボックスのリンクの前に挿入する既定のテキスト (200 文字制限)</span><span class="sxs-lookup"><span data-stu-id="db1cf-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="db1cf-158">Instr の割り当て</span><span class="sxs-lookup"><span data-stu-id="db1cf-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="db1cf-159">string</span><span class="sxs-lookup"><span data-stu-id="db1cf-159">string</span></span> | <span data-ttu-id="db1cf-160">該当なし</span><span class="sxs-lookup"><span data-stu-id="db1cf-160">n/a</span></span> | <span data-ttu-id="db1cf-161">割り当ての [指示] フィールドに挿入される既定のテキスト (200 文字制限)</span><span class="sxs-lookup"><span data-stu-id="db1cf-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="db1cf-162">割り当てのタイトル</span><span class="sxs-lookup"><span data-stu-id="db1cf-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="db1cf-163">string</span><span class="sxs-lookup"><span data-stu-id="db1cf-163">string</span></span> | <span data-ttu-id="db1cf-164">該当なし</span><span class="sxs-lookup"><span data-stu-id="db1cf-164">n/a</span></span> | <span data-ttu-id="db1cf-165">割り当て "Title" フィールドに挿入される既定のテキスト (50 文字制限)</span><span class="sxs-lookup"><span data-stu-id="db1cf-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="db1cf-166">メソッド</span><span class="sxs-lookup"><span data-stu-id="db1cf-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="db1cf-167">`options`(オプション):`{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="db1cf-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="db1cf-168">現在ページにあるすべての共有ボタンをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="db1cf-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="db1cf-169">要素のリスト`options`にオプションのオブジェクトが指定されている場合、これらの要素は共有ボタンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="db1cf-170">既定のフォーム値の設定</span><span class="sxs-lookup"><span data-stu-id="db1cf-170">Setting default form values</span></span>

<span data-ttu-id="db1cf-171">必要に応じて、[Teams への共有] フォームで、次のフィールドの既定値を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="db1cf-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="db1cf-172">この点について`msgText`説明してください ()</span><span class="sxs-lookup"><span data-stu-id="db1cf-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="db1cf-173">割り当ての指示`assignInstr`()</span><span class="sxs-lookup"><span data-stu-id="db1cf-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="db1cf-174">割り当てのタイトル`assignTitle`()</span><span class="sxs-lookup"><span data-stu-id="db1cf-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="db1cf-175">例: 既定のフォーム値</span><span class="sxs-lookup"><span data-stu-id="db1cf-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
