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
# <a name="create-a-share-to-teams-button-for-your-website"></a>Web サイトの [Teams で共有] ボタンを作成する

>[!NOTE]
> * Edge と Chrome のデスクトップ バージョンだけがサポートされます。
> * Freemium またはゲスト アカウントの使用はサポートされていません。

サード パーティの Web サイトでは、ランチャー スクリプトを使用して、Teams への共有ボタンを Web ページに埋め込み、クリックするとポップアップ ウィンドウで Teams への共有エクスペリエンスを起動できます。 これにより、コンテキストを切り替えなくても、任意のユーザーまたは Microsoft Teams チャネルに直接リンクを共有できます。

![Teams への共有ポップアップ](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>[Teams に共有] ボタンを埋め込む方法

最初に、Web ページにスクリプト `launcher.js` を追加する必要があります。

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

次に、クラス属性と属性で共有するリンクを含む HTML 要素を Web ページ `teams-share-button` に追加 `data-href` します。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

これにより、Microsoft Teams アイコンが Web サイトに追加されます。

![[Teams に共有] アイコン](~/assets/icons/share-to-teams-icon.png)

必要に応じて、[Teams に共有] ボタンに別のアイコン サイズが必要な場合は、属性を使用 `data-icon-px-size` します。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

共有するリンクからの URL プレビューが Teams で正しく表示されていないことが分かっている場合 (たとえば、リンクはユーザー認証を必要とします)、設定された属性を追加して URL プレビューを無効に `data-preview` できます `false` 。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

ページがコンテンツを動的にレンダリングする場合は、このメソッドを使用して、パイプライン内の適切な場所に [共有] ボタンを強制的 `shareToMicrosoftTeams.renderButtons()` にレンダリングできます。 

## <a name="crafting-your-website-preview"></a>Web サイト プレビューの作成

Web サイトを Teams と共有すると、選択したチャネルに挿入されたカードに Web サイトのプレビューが含まれる。 共有する Web サイト (URL) に適切なメタデータを追加することで、このプレビューの動作を制御 `data-href` できます。 次の表に、必要なタグの概要を示します。 HTML の既定のバージョンまたは Open Graph バージョンを使用できます。

プレビューを表示するには、次の条件を実行する必要があります。

* サムネイル画像、またはタイトルと説明の両方を含める (最適な結果を得る場合は、3 つすべてが含まれます)。
* 共有される URL は認証を必要とできません。 それでも共有できますが、プレビューは作成されません。

|値|メタ タグ| Open Graph|
|----|----|----|
|タイトル|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|説明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|サムネイル画像| なし |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>Teams for Education への共有

[Teams に共有] ボタンを使用する教師には、追加のオプションが表示されます `Create an Assignment` 。 これにより、共有リンクに基づいて選択したチームに割り当てを簡単に作成できます。

![Teams への共有ポップアップ](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完全launcher.js定義

| プロパティ | HTML 属性 | 種類 | 既定値 | 説明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | 文字列 | 該当なし | 共有するコンテンツの href。 |
| preview | `data-preview` | boolean (文字列として) | `true` | 共有するコンテンツのプレビューを表示するかどうか。 |
| iconPxSize | `data-icon-px-size` | number (文字列) | `32` | レンダリングする [Share-to-Teams] ボタンのサイズ (ピクセル単位)。 |
| msgText | `data-msg-text` | 文字列 | 該当なし | メッセージ作成ボックスのリンクの前に挿入される既定のテキスト (200 文字制限) |
| assignInstr | `data-assign-instr` | 文字列 | 該当なし | 割り当ての "命令" フィールドに挿入される既定のテキスト (200 文字制限) |
| assignTitle | `data-assign-title` | 文字列 | 該当なし | 割り当ての "タイトル" フィールドに挿入される既定のテキスト (50 文字制限) |

### <a name="methods"></a>メソッド

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (省略可能): `{ elements?: HTMLElement[] }`

現在ページ上のすべての共有ボタンをレンダリングします。 オプションのオブジェクトに要素のリストが指定されている場合、それらの要素 `options` は共有ボタンにレンダリングされます。

### <a name="setting-default-form-values"></a>既定のフォーム値の設定

必要に応じて、[Teams に共有] フォームの次のフィールドの既定値を設定することもできます。

* このことを言う ( `msgText` )
* 割り当て命令 ( `assignInstr` )
* 割り当てタイトル ( `assignTitle` )

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
