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
# <a name="creating-a-share-to-teams-embedded-button"></a>Teams への共有の組み込みボタンを作成する

>[!NOTE]
> * デスクトップバージョンのエッジおよびクロムのみがサポートされています。
> * Freemium または guest アカウントの使用はサポートされていません。

サードパーティの web サイトでは、ラウンチャースクリプトを使用して、web ページに Teams ボタンへの共有を埋め込むことができます。これにより、クリックしたときに、Teams への共有がポップアップウィンドウに表示されます。 これにより、コンテキストを切り替えずに、任意のユーザーまたは Microsoft Teams チャネルにリンクを直接共有することができます。

![Teams ポップアップに共有](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>[方法] [チームに共有] ボタンを埋め込む

最初に、 `launcher.js`スクリプトを web ページに追加する必要があります。

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

次に、 `teams-share-button` class 属性を使用して web ページに HTML 要素を追加し、 `data-href`属性で共有するリンクを追加します。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

これにより、Microsoft Teams アイコンが web サイトに追加されます。

![Teams への共有アイコン](~/assets/icons/share-to-teams-icon.png)

必要に応じて、[Teams への共有] ボタンに異なるアイコンサイズを使用`data-icon-px-size`する場合は、属性を使用します。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

リンクから共有される URL プレビューが Teams に適切に表示されないことがわかっている場合 (たとえば、リンクにユーザー認証が必要な場合)、に設定`data-preview`した属性`false`をに追加することで、url プレビューを無効にすることができます。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

ページでコンテンツを動的にレンダリングする場合は、 `shareToMicrosoftTeams.renderButtons()`メソッドを使用して、[**共有**] ボタンをパイプライン内の適切な場所に強制的に表示することができます。

## <a name="crafting-your-website-preview"></a>Web サイトのプレビューを作成する

Web サイトが Teams に対して共有されると、選択したチャネルに挿入されるカードには、web サイトのプレビューが表示されます。 このプレビューの動作を制御するには、共有する web サイト ( `data-href` URL) に適切なメタデータを追加します。 次の表は、必要なタグの概要を示しています。 Html の既定のバージョン、または Open Graph のバージョンのいずれかを使用できます。

プレビューを表示するためには、次のことを行う必要があります。

* サムネイルイメージを含めるか、タイトルと説明の両方を含めます (最適な結果を得るために3つすべてを含みます)。
* 共有されている URL は認証を必要としません。 このまま共有することはできますが、プレビューは作成されません。

|値|メタ タグ| グラフを開く|
|----|----|----|
|タイトル|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|説明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|サムネイルイメージ| none |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>教育機関との Teams への共有

教師の場合、[Teams に共有] ボタンを使用するに`Create an Assignment`は、追加のオプションが表示されます。 これにより、共有リンクを基にして、選択したチームの割り当てをすばやく作成できます。

![Teams ポップアップに共有](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完全な起動プログラム .js の定義

| プロパティ | HTML 属性 | 型 | 既定値 | 説明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 該当なし | 共有するコンテンツの href。 |
| preview | `data-preview` | ブール型 (string) | `true` | 共有するコンテンツのプレビューを表示するかどうかを指定します。 |
| iconPxSize | `data-icon-px-size` | 数値 (文字列型) | `32` | 表示する [チーム間共有] ボタンのサイズ (ピクセル単位)。 |
| msgText | `data-msg-text` | string | 該当なし | メッセージ作成ボックスのリンクの前に挿入する既定のテキスト (200 文字制限) |
| Instr の割り当て | `data-assign-instr` | string | 該当なし | 割り当ての [指示] フィールドに挿入される既定のテキスト (200 文字制限) |
| 割り当てのタイトル | `data-assign-title` | string | 該当なし | 割り当て "Title" フィールドに挿入される既定のテキスト (50 文字制限) |

### <a name="methods"></a>メソッド

**`shareToMicrosoftTeams.renderButtons(options)`**

`options`(オプション):`{ elements?: HTMLElement[] }`

現在ページにあるすべての共有ボタンをレンダリングします。 要素のリスト`options`にオプションのオブジェクトが指定されている場合、これらの要素は共有ボタンに表示されます。

### <a name="setting-default-form-values"></a>既定のフォーム値の設定

必要に応じて、[Teams への共有] フォームで、次のフィールドの既定値を設定することもできます。

* この点について`msgText`説明してください ()
* 割り当ての指示`assignInstr`()
* 割り当てのタイトル`assignTitle`()

#### <a name="example-default-form-values"></a>例: 既定のフォーム値

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
