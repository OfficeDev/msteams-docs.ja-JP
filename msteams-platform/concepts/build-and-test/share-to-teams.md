---
title: '[Teams で共有] ボタンを作成する'
description: Web サイトの [埋め込みTeamsに共有を追加する方法
ms.topic: reference
ms.localizationpriority: medium
keywords: 共有Teams共有Teams
ms.openlocfilehash: 0d0fb0d7baf18038cfe87b648d2550bbd20b593a
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156149"
---
# <a name="create-share-to-teams-button"></a>[Teams で共有] ボタンを作成する

サードパーティの Web サイトでは、ランチャー スクリプトを使用して、Web ページに Share-to-Teamsボタンを埋め込む可能性があります。 選択すると、ポップアップ ウィンドウで Share-to-Teamsエクスペリエンスが起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたはMicrosoft Teamsにリンクを直接共有できます。 このドキュメントでは、Web サイト用に Share-to-Teams ボタンを作成して埋め込み、Web サイトのプレビューを作成し、Share-to-Microsoft Teams for Education を拡張する方法についてガイドします。

> [!NOTE]
> * サポートされているのは、Edge と Chrome のデスクトップ バージョンのみです。
> * Freemium アカウントまたはゲスト アカウントの使用はサポートされていません。  

次の図は、Share-to-Teamsポップアップ エクスペリエンスを表示します。

![共有と共有Teamsポップアップ](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>[共有を埋め込む] Teamsボタン

1. Web ページ `launcher.js` にスクリプトを追加します。

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. クラス属性と属性で共有するリンクを含む HTML 要素を Web ページ `teams-share-button` に追加 `data-href` します。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    これを完了すると、Microsoft Teamsアイコンが Web サイトに追加されます。 次の図は、[共有間] アイコンTeams示しています。

    ![[共有Teams] アイコン](~/assets/icons/share-to-teams-icon.png)

1. または、[共有する共有] ボタンに別のアイコン サイズをTeams、属性を使用 `data-icon-px-size` します。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. 共有リンクでユーザー認証が必要で、リンクから共有する URL プレビューが Teams でうまく表示されない場合は、に属性セットを追加して URL プレビューを無効 `data-preview` にできます `false` 。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. ページがコンテンツを動的にレンダリングする場合は、このメソッドを使用して、パイプライン内の適切な場所で `shareToMicrosoftTeams.renderButtons()` **Share** を強制的にレンダリングできます。

## <a name="craft-your-website-preview"></a>Web サイトのプレビューを作成する

Web サイトが web サイトと共有Teams、選択したチャネルに挿入されるカードには、Web サイトのプレビューが含まれる。 このプレビューの動作を制御するには、共有する Web サイト (URL など) に適切なメタ データが追加されます `data-href` 。  

**プレビューを表示するには**

* サムネイル 画像、または **Title と** Description の **両方を含める****必要があります**。 最適な結果を得る場合は、3 つすべてが含まれます。
* 共有 URL は認証を必要とします。 認証が必要な場合は共有できますが、プレビューは作成されません。

次の表に、必要なタグの概要を示します。

|値|メタ タグ| 開くGraph|
|----|----|----|
|役職|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|説明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|サムネイル 画像| none。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

HTML の既定のバージョンまたは Open Graph使用できます。

## <a name="share-to-teams-for-education"></a>共有するMicrosoft Teams for Education

[共有して共有する] ボタンをTeams教師の場合は、 に追加のオプションがあります `Create an Assignment` 。 これにより、共有リンクに基づいて、選択したチームで割り当てを簡単に作成できます。 次の図は、教育のための共有Teamsを表示します。 

![ポップアップ教育Teams共有する](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完全なlauncher.js定義

| プロパティ | HTML 属性 | 型 | 既定値 | 説明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | 文字列 | 該当なし | 共有するコンテンツの href。 |
| preview | `data-preview` | boolean (文字列として) | `true` | 共有するコンテンツのプレビューを表示するかどうかを指定します。 |
| iconPxSize | `data-icon-px-size` | number (文字列として) | `32` | レンダリングする Share-to-Teamsボタンのサイズ (ピクセル単位)。 |
| msgText | `data-msg-text` | string | 該当なし | メッセージ作成ボックスのリンクの前に挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignInstr | `data-assign-instr` | 文字列 | 該当なし | 割り当て "命令" フィールドに挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignTitle | `data-assign-title` | string | 該当なし | 割り当て "Title" フィールドに挿入される既定のテキスト。 最大文字数は 50 です。 |

### <a name="methods"></a>メソッド

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (省略可能): `{ elements?: HTMLElement[] }`

現在、すべての共有ボタンがページにレンダリングされます。 省略可能な `options` オブジェクトに要素のリストが指定されている場合、それらの要素は共有ボタンにレンダリングされます。

### <a name="set-default-form-values"></a>既定のフォーム値を設定する

[共有] フォームの次のフィールドに既定値を設定Teamsできます。

* このことを言います。 `msgText`
* 割り当て手順: `assignInstr`
* 割り当てのタイトル: `assignTitle`

#### <a name="example"></a>例

 既定のフォーム値は、次の例で指定します。

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>関連項目

[Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
