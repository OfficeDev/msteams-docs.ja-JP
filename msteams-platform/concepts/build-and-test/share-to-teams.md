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
# <a name="create-share-to-teams-button"></a>[Share-to-Teams の作成] ボタン

サードパーティの Web サイトでは、ランチャー スクリプトを使用して、Web ページに Share-to-Teams ボタンを埋め込む可能性があります。 選択すると、ポップアップ ウィンドウで Share-to-Teams エクスペリエンスが起動します。 これにより、コンテキストを切り替えることなく、任意のユーザーまたは Microsoft Teams チャネルへのリンクを直接共有できます。 このドキュメントでは、Web サイトの [Share-to-Teams] ボタンを作成して埋め込み、Web サイトのプレビューを作成し、教育向け Share-to-Teams を拡張する方法についてガイドします。

> [!NOTE]
> * サポートされているのは、Edge と Chrome のデスクトップ バージョンのみです。
> * Freemium アカウントまたはゲスト アカウントの使用はサポートされていません。  

次の図は、Share-to-Teams ポップアップ エクスペリエンスを表示します。

![[チーム間の共有] ポップアップ](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>[Teams への共有の埋め込み] ボタン

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

    これを完了すると、Microsoft Teams アイコンが Web サイトに追加されます。 次の図は、Share-to-Teams アイコンを示しています。

    ![[Teams に共有] アイコン](~/assets/icons/share-to-teams-icon.png)

1. または、[共有する Teams] ボタンに別のアイコン サイズが必要な場合は、属性を使用 `data-icon-px-size` します。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. 共有リンクでユーザー認証が必要で、リンクから共有する URL プレビューが Teams でうまく表示されない場合は、に属性セットを追加して URL プレビューを `data-preview` 無効にできます `false` 。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. ページがコンテンツを動的にレンダリングする場合は、このメソッドを使用して、パイプライン内の適切な場所で [共有] ボタンを強制的 `shareToMicrosoftTeams.renderButtons()` にレンダリングできます。 

## <a name="craft-your-website-preview"></a>Web サイトのプレビューを作成する

Web サイトが Teams に共有されている場合、選択したチャネルに挿入されるカードには、Web サイトのプレビューが含まれる。 このプレビューの動作を制御するには、共有する Web サイト (URL など) に適切なメタ データが追加されます `data-href` 。  

**プレビューを表示するには**

* サムネイル 画像、または **Title と** Description の **両方を含める****必要があります**。 最適な結果を得る場合は、3 つすべてが含まれます。
* 共有 URL は認証を必要とします。 認証が必要な場合は共有できますが、プレビューは作成されません。

次の表に、必要なタグの概要を示します。

|値|メタ タグ| グラフを開く|
|----|----|----|
|タイトル|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|説明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|サムネイル 画像| none。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

HTML の既定のバージョン、または Open Graph バージョンのいずれかを使用できます。

## <a name="share-to-teams-for-education"></a>教育向け Teams への共有

[チームに共有] ボタンを使用する教師の場合は、追加のオプションがあります `Create an Assignment` 。 これにより、共有リンクに基づいて、選択したチームで割り当てを簡単に作成できます。 次の図は、教育用の Share-to-Teams を表示します。 

![Teams ポップアップ教育への共有](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完全なlauncher.js定義

| プロパティ | HTML 属性 | 種類 | 既定値 | 説明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | 文字列 | 該当なし | 共有するコンテンツの href。 |
| preview | `data-preview` | boolean (文字列として) | `true` | 共有するコンテンツのプレビューを表示するかどうかを指定します。 |
| iconPxSize | `data-icon-px-size` | number (文字列として) | `32` | レンダリングする [Share-to-Teams] ボタンのサイズ (ピクセル単位)。 |
| msgText | `data-msg-text` | 文字列 | 該当なし | メッセージ作成ボックスのリンクの前に挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignInstr | `data-assign-instr` | 文字列 | 該当なし | 割り当ての [命令] フィールドに挿入される既定のテキスト。 最大文字数は 200 文字です。 |
| assignTitle | `data-assign-title` | 文字列 | 該当なし | 割り当ての [タイトル] フィールドに挿入される既定のテキスト。 最大文字数は 50 です。 |

### <a name="methods"></a>メソッド

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (省略可能): `{ elements?: HTMLElement[] }`

現在、すべての共有ボタンがページにレンダリングされます。 省略可能な `options` オブジェクトに要素のリストが指定されている場合、それらの要素は共有ボタンにレンダリングされます。

### <a name="set-default-form-values"></a>既定のフォーム値を設定する

[チームへの共有] フォームで、次のフィールドの既定値を設定できます。

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

> [!div class="nextstepaction"]
> [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
